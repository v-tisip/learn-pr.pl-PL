<span data-ttu-id="01990-101">Teraz, gdy już wiesz, jak włączenie funkcji MSI spowoduje utworzenie tożsamości aplikacji do użycia na potrzeby uwierzytelniania, utworzymy aplikację, która będzie używać tej tożsamości, aby uzyskać dostęp do wpisów tajnych w magazynie.</span><span class="sxs-lookup"><span data-stu-id="01990-101">Now that you know how enabling MSI creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="01990-102">Odczytywanie wpisów tajnych w aplikacji ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="01990-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="01990-103">Interfejs API usługi Azure Key Vault to interfejs API REST, który obsługuje wszystkie funkcje zarządzania oraz użycie kluczy i magazynów.</span><span class="sxs-lookup"><span data-stu-id="01990-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="01990-104">Każdy wpis tajny w magazynie ma unikatowy adres URL, a wartości wpisów tajnych są pobierane przy użyciu żądań HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="01990-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="01990-105">Oficjalna biblioteka klienta usługi Key Vault dla platformy .NET Core to klasa `KeyVaultClient` w pakiecie NuGet Microsoft.Azure.KeyVault.</span><span class="sxs-lookup"><span data-stu-id="01990-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="01990-106">Nie musisz jednak używać jej bezpośrednio, mimo że &mdash; za pomocą metody ASP.NET Core `AddAzureKeyVault` możesz załadować wszystkie wpisy tajne z magazynu do interfejsu API konfiguracji podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="01990-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="01990-107">Ta technika umożliwia uzyskanie dostępu do wszystkich wpisów tajnych wg nazwy przy użyciu tego samego interfejsu `IConfiguration`, którego używa się w przypadku pozostałej części konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="01990-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="01990-108">Aplikacje, które używają metody `AddAzureKeyVault`, wymagają uprawnień **Pobieranie** i **Wyświetlanie listy** do magazynu.</span><span class="sxs-lookup"><span data-stu-id="01990-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="01990-109">Niezależnie od infrastruktury lub języka używanego do utworzenia aplikacji należy ładować wpisy tajne do pamięci przy uruchamianiu aplikacji, chyba że istnieje konkretny powód uzasadniający inne podejście.</span><span class="sxs-lookup"><span data-stu-id="01990-109">Regardless of the framework or language you use to build your app, load secrets into memory once at app startup unless you have a specific reason not to.</span></span> <span data-ttu-id="01990-110">Odczytywanie wpisów bezpośrednio z magazynu za każdym razem, gdy są potrzebne, jest niepotrzebnie wolne i kosztowne.</span><span class="sxs-lookup"><span data-stu-id="01990-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="01990-111">Metoda `AddAzureKeyVault` wymaga tylko nazwy magazynu jako danych wejściowych, którą można pozyskać z lokalnej konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01990-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="01990-112">Ponadto to rozwiązanie automatycznie obsługuje uwierzytelnianie MSI &mdash; w przypadku użycia w aplikacji wdrożonej do usługi Azure App Service z włączoną funkcją MSI będzie wykrywać usługę tokenu MSI i używać jej do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="01990-112">It also automatically handles MSI authentication &mdash; when used in an app deployed to Azure App Service with MSI enabled, it will detect the MSI token service and use it to authenticate.</span></span> <span data-ttu-id="01990-113">W większości przypadków jest to dobre rozwiązanie obejmujące wszystkie najlepsze praktyki. Będziemy go używać w ćwiczeniu w tym module.</span><span class="sxs-lookup"><span data-stu-id="01990-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="01990-114">Obsługa wpisów tajnych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="01990-114">Handling secrets in an app</span></span>

<span data-ttu-id="01990-115">Po załadowaniu wpisu tajnego do aplikacji to aplikacja powinna obsługiwać go w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="01990-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="01990-116">W aplikacji tworzonej w tym module wpiszemy wartość wpisu tajnego do odpowiedzi klienta i wyświetlimy ją w przeglądarce internetowej, aby zademonstrować, że została pomyślnie załadowana.</span><span class="sxs-lookup"><span data-stu-id="01990-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="01990-117">**Zwracanie wartości wpisu tajnego do klienta *nie* jest typowym podejściem!**</span><span class="sxs-lookup"><span data-stu-id="01990-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="01990-118">Zazwyczaj używa się wpisów tajnych do wykonywania czynności takich jak inicjowanie bibliotek klienckich na potrzeby baz danych lub zdalnych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="01990-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01990-119">Zawsze dokładnie sprawdzaj kod, aby upewnić się, że aplikacja nigdy nie zapisuje wpisów tajnych w żadnego rodzaju danych wyjściowych, w tym dziennikach, magazynie i odpowiedziach.</span><span class="sxs-lookup"><span data-stu-id="01990-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="01990-120">Ćwiczenie</span><span class="sxs-lookup"><span data-stu-id="01990-120">Exercise</span></span>

<span data-ttu-id="01990-121">Utworzymy internetowy interfejs API platformy ASP.NET Core i użyjemy metody `AddAzureKeyVault`, aby załadować wpis tajny z magazynu.</span><span class="sxs-lookup"><span data-stu-id="01990-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="01990-122">Tworzymy aplikację.</span><span class="sxs-lookup"><span data-stu-id="01990-122">Create the app</span></span>

<span data-ttu-id="01990-123">W terminalu usługi Azure Cloud Shell uruchom następujące polecenie, aby utworzyć nową aplikację internetowego interfejsu API platformy ASP.NET Core i otworzyć ją w edytorze.</span><span class="sxs-lookup"><span data-stu-id="01990-123">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="01990-124">Po załadowaniu edytora uruchom następujące polecenia w powłoce, aby dodać pakiet NuGet zawierający metodę `AddAzureKeyVault` i przywrócić wszystkie zależności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01990-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="01990-125">Dodawanie kodu w celu załadowania i użycia wpisów tajnych</span><span class="sxs-lookup"><span data-stu-id="01990-125">Add code to load and use secrets</span></span>

<span data-ttu-id="01990-126">Aby zademonstrować dobre użycie usługi Key Vault, zmodyfikujemy naszą aplikację i załadujemy wpisy tajne z magazynu podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="01990-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="01990-127">Ponadto dodamy nowy kontroler z punktem końcowym, który będzie pobierać wpis tajny **SecretPassword** z magazynu.</span><span class="sxs-lookup"><span data-stu-id="01990-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="01990-128">Po pierwsze uruchomienie aplikacji: otwórz plik `Program.cs`, usuń jego zawartość i zastąp ją następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="01990-128">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

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
> <span data-ttu-id="01990-129">Upewnij się, że zapisujesz pliki przy użyciu kombinacji `Ctrl+S` po zakończeniu ich edycji.</span><span class="sxs-lookup"><span data-stu-id="01990-129">Make sure to save files with `Ctrl+S` when you're done editing them.</span></span>

<span data-ttu-id="01990-130">Jedyna zmiana w kodzie uruchomieniowym to dodanie `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="01990-130">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="01990-131">Jest to moment załadowania nazwy magazynu z konfiguracji oraz wywołania metody `AddAzureKeyVault` przy jej użyciu.</span><span class="sxs-lookup"><span data-stu-id="01990-131">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="01990-132">Następnie kontroler: w folderze `Controllers` utwórz nowy plik o nazwie `SecretTestController.cs` i wklej do niego następujący kod.</span><span class="sxs-lookup"><span data-stu-id="01990-132">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!NOTE]
> <span data-ttu-id="01990-133">Aby utworzyć nowy plik, użyj polecenia `touch` w powłoce.</span><span class="sxs-lookup"><span data-stu-id="01990-133">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="01990-134">W tym przypadku użyj polecenia `touch Controllers/SecretTestController.cs`.</span><span class="sxs-lookup"><span data-stu-id="01990-134">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="01990-135">Musisz kliknąć przycisk odświeżania w okienku Pliki edytora, aby zobaczyć plik.</span><span class="sxs-lookup"><span data-stu-id="01990-135">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

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

<span data-ttu-id="01990-136">Uruchom polecenie `dotnet build` w powłoce, aby upewnić się, że wszystko się kompiluje.</span><span class="sxs-lookup"><span data-stu-id="01990-136">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="01990-137">Aplikacja jest gotowa do uruchomienia &mdash; teraz przenieśmy ją na platformę Azure!</span><span class="sxs-lookup"><span data-stu-id="01990-137">The app is ready to run &mdash; now let's get it into Azure!</span></span>