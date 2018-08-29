W tym module utworzysz prostą aplikację konsolową za pomocą zintegrowanego terminalu, zainstalujesz pakiety NuGet i użyjesz rozszerzenia usługi Azure Cosmos DB do wyświetlenia baz danych i kolekcji utworzonych w poprzednim module. Pobierzesz parametry połączenia usługi Azure Cosmos DB z rozszerzenia, a następnie rozpoczniesz programowanie dla usługi Azure Cosmos DB. 

## <a name="create-a-console-app"></a>Tworzenie aplikacji konsolowej

1. Otwórz program Visual Studio Code, a następnie wybierz pozycję **Plik** > **Otwórz folder**.

2. Utwórz nowy folder o nazwie **learning-module**, w którym będzie znajdować się nowy projekt języka C#, a następnie kliknij pozycję **Wybierz folder**.

2. Otwórz zintegrowany terminal z programu Visual Studio Code, wybierając pozycję **Widok** > **Terminal zintegrowany** z menu głównego.

3. W oknie terminalu wpisz polecenie **dotnet new console**.

    To polecenie umożliwia utworzenie pliku **Program.cs** w folderze z gotowym prostym programem „Hello World” oraz pliku projektu języka C# o nazwie **learning-module.csproj**.

4. W oknie terminalu wpisz następujące polecenie, aby uruchomić program „Hello World”. 

    ```
    dotnet run
    ```

    W oknie terminalu zostanie wyświetlony napis „Hello world!” jako dane wyjściowe.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Łączenie aplikacji z usługą Azure Cosmos DB

1. Zaloguj się do platformy Azure, klikając pozycję **Widok** > **Paleta poleceń** i wpisując ciąg **Azure: Sign In**.

    Postępuj zgodnie z monitami, aby skopiować i wkleić kod udostępniony w przeglądarce internetowej, który uwierzytelnia sesję programu Visual Studio Code.

2. Kliknij ikonę ![Ikona eksploratora](../media/2-setup/visual-studio-code-explorer-icon.png)**Eksplorator** w menu po lewej stronie, a następnie rozwiń pozycję **Azure Cosmos DB**.

3. Rozwiń subskrypcję platformy Azure i konto usługi Azure Cosmos DB. Jeśli utworzono bazę danych **Produkty** i kolekcję **Ubrania** w poprzednich modułach, rozszerzenie wyświetli je.

   ![Rozszerzenie usługi Azure Cosmos DB dla programu Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. Teraz utworzymy nową bazę danych i kolekcję dla klientów.

    W oknie eksploratora kliknij prawym przyciskiem myszy konto, a następnie kliknij pozycję **Utwórz bazę danych**. 
    
    W polu tekstowym w górnej części ekranu wpisz **Users** jako nazwę bazy danych > **Enter** > **WebCustomers** jako nazwę kolekcji > **Enter** > **userId** jako klucz partycji > **Enter** > **1000** jako początkową wydajność przepływności > **Enter**.

    ![Rozszerzenie usługi Azure Cosmos DB dla programu Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing-->

    Nowa baza danych Users i kolekcja WebCustomers jest wyświetlana w oknie eksploratora.

5. W zintegrowanym terminalu uruchom osobno każde z następujących poleceń, aby zainstalować wymagane pakiety NuGet.

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. W górnej części okienka eksploratora kliknij pozycję **Program.cs**, aby otworzyć plik.

7. Dodaj następujące instrukcje using po wierszu `using System;`.

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. Dodaj następujące dwie stałe i zmienną *client* do klasy Program:

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. Skopiuj parametry połączenia z poziomu rozszerzenia usługi Azure Cosmos DB, klikając prawym przyciskiem myszy konto learning-module, a następnie polecenie **Kopiuj parametry połączenia**.

    ![Rozszerzenie usługi Azure Cosmos DB dla programu Visual Studio Code](../media/2-setup/vs-code-copy-connection-string.gif) 

10. Wklej parametry połączenia do pliku tekstowego, a następnie skopiuj część **AccountEndpoint** z pliku tekstowego do sekcji **EndpointUrl** w pliku Program.cs.

    Sekcja AccountEndpoint powinna wyglądać podobnie do poniższego kodu:

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. Teraz skopiuj wartość **AccountKey** z wartości tekstowej do wartości **PrimaryKey** w pliku Program.cs.

12. W zintegrowanym terminalu wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.

    ```csharp
    dotnet run
    ```

13. Dodaj nowe zadanie asynchroniczne, aby utworzyć nowego klienta, a następnie sprawdź, czy baza danych Users istnieje, dodając następującą metodę po metodzie main.
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. W zintegrowanym terminalu ponownie wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.

    ```csharp
    dotnet run
    ```

15. Skopiuj i wklej następujący kod do metody **Main**, zastępując bieżący wiersz `Console.WriteLine("Hello World!");`.

    ```csharp
    try
            {
                    Program p = new Program();
                    p.BasicOperations().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }
    ```

16. W zintegrowanym terminalu ponownie wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.

    ```csharp
    dotnet run
    ```

    W konsoli zostaną wyświetlone następujące dane wyjściowe.
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>Podsumowanie

W tym module przygotowano podstawy dla aplikacji usługi Azure Cosmos DB. Skonfigurowano środowisko programistyczne w programie Visual Studio Code, utworzono prosty projekt HelloWorld, połączono projekt z punktem końcowym usługi Azure Cosmos DB i sprawdzono, czy baza danych i kolekcja istnieją.