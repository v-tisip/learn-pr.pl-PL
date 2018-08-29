Teraz, gdy już wiesz, jak włączenie funkcji MSI spowoduje utworzenie tożsamości aplikacji do użycia na potrzeby uwierzytelniania, utworzymy aplikację, która będzie używać tej tożsamości, aby uzyskać dostęp do wpisów tajnych w magazynie.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>Odczytywanie wpisów tajnych w aplikacji ASP.NET Core

Interfejs API usługi Azure Key Vault to interfejs API REST, który obsługuje wszystkie funkcje zarządzania oraz użycie kluczy i magazynów. Każdy wpis tajny w magazynie ma unikatowy adres URL, a wartości wpisów tajnych są pobierane przy użyciu żądań HTTP GET.

Oficjalna biblioteka klienta usługi Key Vault dla platformy .NET Core to klasa `KeyVaultClient` w pakiecie NuGet Microsoft.Azure.KeyVault. Nie musisz jednak używać jej bezpośrednio, mimo że &mdash; za pomocą metody ASP.NET Core `AddAzureKeyVault` możesz załadować wszystkie wpisy tajne z magazynu do interfejsu API konfiguracji podczas uruchamiania. Ta technika umożliwia uzyskanie dostępu do wszystkich wpisów tajnych wg nazwy przy użyciu tego samego interfejsu `IConfiguration`, którego używa się w przypadku pozostałej części konfiguracji. Aplikacje, które używają metody `AddAzureKeyVault`, wymagają uprawnień **Pobieranie** i **Wyświetlanie listy** do magazynu.

> [!TIP]
> Niezależnie od infrastruktury lub języka używanego do utworzenia aplikacji należy ładować wpisy tajne do pamięci przy uruchamianiu aplikacji, chyba że istnieje konkretny powód uzasadniający inne podejście. Odczytywanie wpisów bezpośrednio z magazynu za każdym razem, gdy są potrzebne, jest niepotrzebnie wolne i kosztowne.

Metoda `AddAzureKeyVault` wymaga tylko nazwy magazynu jako danych wejściowych, którą można pozyskać z lokalnej konfiguracji aplikacji. Ponadto to rozwiązanie automatycznie obsługuje uwierzytelnianie MSI &mdash; w przypadku użycia w aplikacji wdrożonej do usługi Azure App Service z włączoną funkcją MSI będzie wykrywać usługę tokenu MSI i używać jej do uwierzytelniania. W większości przypadków jest to dobre rozwiązanie obejmujące wszystkie najlepsze praktyki. Będziemy go używać w ćwiczeniu w tym module.

## <a name="handling-secrets-in-an-app"></a>Obsługa wpisów tajnych w aplikacji

Po załadowaniu wpisu tajnego do aplikacji to aplikacja powinna obsługiwać go w bezpieczny sposób. W aplikacji tworzonej w tym module wpiszemy wartość wpisu tajnego do odpowiedzi klienta i wyświetlimy ją w przeglądarce internetowej, aby zademonstrować, że została pomyślnie załadowana. **Zwracanie wartości wpisu tajnego do klienta *nie* jest typowym podejściem!** Zazwyczaj używa się wpisów tajnych do wykonywania czynności takich jak inicjowanie bibliotek klienckich na potrzeby baz danych lub zdalnych interfejsów API.

> [!IMPORTANT]
> Zawsze dokładnie sprawdzaj kod, aby upewnić się, że aplikacja nigdy nie zapisuje wpisów tajnych w żadnego rodzaju danych wyjściowych, w tym dziennikach, magazynie i odpowiedziach.

## <a name="exercise"></a>Ćwiczenie

Utworzymy internetowy interfejs API platformy ASP.NET Core i użyjemy metody `AddAzureKeyVault`, aby załadować wpis tajny z magazynu.

### <a name="create-the-app"></a>Tworzymy aplikację.

W terminalu usługi Azure Cloud Shell uruchom następujące polecenie, aby utworzyć nową aplikację internetowego interfejsu API platformy ASP.NET Core i otworzyć ją w edytorze.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

Po załadowaniu edytora uruchom następujące polecenia w powłoce, aby dodać pakiet NuGet zawierający metodę `AddAzureKeyVault` i przywrócić wszystkie zależności aplikacji.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>Dodawanie kodu w celu załadowania i użycia wpisów tajnych

Aby zademonstrować dobre użycie usługi Key Vault, zmodyfikujemy naszą aplikację i załadujemy wpisy tajne z magazynu podczas uruchamiania. Ponadto dodamy nowy kontroler z punktem końcowym, który będzie pobierać wpis tajny **SecretPassword** z magazynu.

Po pierwsze uruchomienie aplikacji: otwórz plik `Program.cs`, usuń jego zawartość i zastąp ją następującym kodem:

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using MSI. If MSI is not available, it will
                    // check if Visual Studio and/or the Azure CLI are installed locally and
                    // see if they are configured with credentials that can access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!NOTE]
> Upewnij się, że zapisujesz pliki przy użyciu kombinacji `Ctrl+S` po zakończeniu ich edycji.

Jedyna zmiana w kodzie uruchomieniowym to dodanie `ConfigureAppConfiguration`. Jest to moment załadowania nazwy magazynu z konfiguracji oraz wywołania metody `AddAzureKeyVault` przy jej użyciu.

Następnie kontroler: w folderze `Controllers` utwórz nowy plik o nazwie `SecretTestController.cs` i wklej do niego następujący kod.

> [!NOTE]
> Aby utworzyć nowy plik, użyj polecenia `touch` w powłoce. W tym przypadku użyj polecenia `touch Controllers/SecretTestController.cs`. Musisz kliknąć przycisk odświeżania w okienku Pliki edytora, aby zobaczyć plik.

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

Uruchom polecenie `dotnet build` w powłoce, aby upewnić się, że wszystko się kompiluje. Aplikacja jest gotowa do uruchomienia &mdash; teraz przenieśmy ją na platformę Azure!