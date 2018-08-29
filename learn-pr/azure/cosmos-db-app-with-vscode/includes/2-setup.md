<span data-ttu-id="2acb9-101">W tym module utworzysz prostą aplikację konsolową za pomocą zintegrowanego terminalu, zainstalujesz pakiety NuGet i użyjesz rozszerzenia usługi Azure Cosmos DB do wyświetlenia baz danych i kolekcji utworzonych w poprzednim module.</span><span class="sxs-lookup"><span data-stu-id="2acb9-101">In this module you will create a simple console app using the integrated terminal, install NuGet packages, and use the Azure Cosmos DB extension to see databases and collections created in the previous module.</span></span> <span data-ttu-id="2acb9-102">Pobierzesz parametry połączenia usługi Azure Cosmos DB z rozszerzenia, a następnie rozpoczniesz programowanie dla usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2acb9-102">You'll retrieve your Azure Cosmos DB connection string from the extension, and then start developing against Azure Cosmos DB.</span></span> 

## <a name="create-a-console-app"></a><span data-ttu-id="2acb9-103">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="2acb9-103">Create a console app</span></span>

1. <span data-ttu-id="2acb9-104">Otwórz program Visual Studio Code, a następnie wybierz pozycję **Plik** > **Otwórz folder**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-104">Open Visual Studio Code, and then select **File** > **Open Folder**.</span></span>

2. <span data-ttu-id="2acb9-105">Utwórz nowy folder o nazwie **learning-module**, w którym będzie znajdować się nowy projekt języka C#, a następnie kliknij pozycję **Wybierz folder**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-105">Create a new folder named **learning-module** where you want your new C# project to be, and then click **Select Folder**.</span></span>

2. <span data-ttu-id="2acb9-106">Otwórz zintegrowany terminal z programu Visual Studio Code, wybierając pozycję **Widok** > **Terminal zintegrowany** z menu głównego.</span><span class="sxs-lookup"><span data-stu-id="2acb9-106">Open the integrated terminal from Visual Studio Code by selecting **View** > **Integrated Terminal** from the main menu.</span></span>

3. <span data-ttu-id="2acb9-107">W oknie terminalu wpisz polecenie **dotnet new console**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-107">In the terminal window, type **dotnet new console**.</span></span>

    <span data-ttu-id="2acb9-108">To polecenie umożliwia utworzenie pliku **Program.cs** w folderze z gotowym prostym programem „Hello World” oraz pliku projektu języka C# o nazwie **learning-module.csproj**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-108">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

4. <span data-ttu-id="2acb9-109">W oknie terminalu wpisz następujące polecenie, aby uruchomić program „Hello World”.</span><span class="sxs-lookup"><span data-stu-id="2acb9-109">In the terminal window, type the following command to run the "Hello World" program.</span></span> 

    ```
    dotnet run
    ```

    <span data-ttu-id="2acb9-110">W oknie terminalu zostanie wyświetlony napis „Hello world!”</span><span class="sxs-lookup"><span data-stu-id="2acb9-110">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="2acb9-111">jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2acb9-111">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="2acb9-112">Łączenie aplikacji z usługą Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2acb9-112">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="2acb9-113">Zaloguj się do platformy Azure, klikając pozycję **Widok** > **Paleta poleceń** i wpisując ciąg **Azure: Sign In**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-113">Sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span>

    <span data-ttu-id="2acb9-114">Postępuj zgodnie z monitami, aby skopiować i wkleić kod udostępniony w przeglądarce internetowej, który uwierzytelnia sesję programu Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2acb9-114">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

2. <span data-ttu-id="2acb9-115">Kliknij ikonę ![Ikona eksploratora](../media/2-setup/visual-studio-code-explorer-icon.png)**Eksplorator** w menu po lewej stronie, a następnie rozwiń pozycję **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-115">Click the ![Explorer icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Explorer** icon on the left menu, and then expand **Azure Cosmos DB**.</span></span>

3. <span data-ttu-id="2acb9-116">Rozwiń subskrypcję platformy Azure i konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2acb9-116">Expand your Azure subscription > Azure Cosmos DB account.</span></span> <span data-ttu-id="2acb9-117">Jeśli utworzono bazę danych **Produkty** i kolekcję **Ubrania** w poprzednich modułach, rozszerzenie wyświetli je.</span><span class="sxs-lookup"><span data-stu-id="2acb9-117">If you created the **Products** database and **Clothing** collection in the previous modules, the extension displays them.</span></span>

   ![Rozszerzenie usługi Azure Cosmos DB dla programu Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. <span data-ttu-id="2acb9-119">Teraz utworzymy nową bazę danych i kolekcję dla klientów.</span><span class="sxs-lookup"><span data-stu-id="2acb9-119">Now let's create a new database and collection for your customers.</span></span>

    <span data-ttu-id="2acb9-120">W oknie eksploratora kliknij prawym przyciskiem myszy konto, a następnie kliknij pozycję **Utwórz bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-120">In the Explorer window, right-click your account, and then click **Create Database**.</span></span> 
    
    <span data-ttu-id="2acb9-121">W polu tekstowym w górnej części ekranu wpisz **Users** jako nazwę bazy danych > **Enter** > **WebCustomers** jako nazwę kolekcji > **Enter** > **userId** jako klucz partycji > **Enter** > **1000** jako początkową wydajność przepływności > **Enter**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-121">In the text box at the top of the screen, type **Users** for the database name > **Enter** > **WebCustomers** for the collection name > **Enter** > **userId** for the partition key > **Enter** > **1000** for the initial throughput capacity > **Enter**.</span></span>

    <span data-ttu-id="2acb9-122">![Rozszerzenie usługi Azure Cosmos DB dla programu Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span><span class="sxs-lookup"><span data-stu-id="2acb9-122">![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span></span>

    <span data-ttu-id="2acb9-123">Nowa baza danych Users i kolekcja WebCustomers jest wyświetlana w oknie eksploratora.</span><span class="sxs-lookup"><span data-stu-id="2acb9-123">The new Users database and WebCustomers collection are displayed in the Explorer window.</span></span>

5. <span data-ttu-id="2acb9-124">W zintegrowanym terminalu uruchom osobno każde z następujących poleceń, aby zainstalować wymagane pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="2acb9-124">In the integrated terminal, run each of the following commands at a new prompt to install the required NuGet packages.</span></span>

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. <span data-ttu-id="2acb9-125">W górnej części okienka eksploratora kliknij pozycję **Program.cs**, aby otworzyć plik.</span><span class="sxs-lookup"><span data-stu-id="2acb9-125">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

7. <span data-ttu-id="2acb9-126">Dodaj następujące instrukcje using po wierszu `using System;`.</span><span class="sxs-lookup"><span data-stu-id="2acb9-126">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. <span data-ttu-id="2acb9-127">Dodaj następujące dwie stałe i zmienną *client* do klasy Program:</span><span class="sxs-lookup"><span data-stu-id="2acb9-127">Add the following two constants and your *client* variable to the Program class:</span></span>

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. <span data-ttu-id="2acb9-128">Skopiuj parametry połączenia z poziomu rozszerzenia usługi Azure Cosmos DB, klikając prawym przyciskiem myszy konto learning-module, a następnie polecenie **Kopiuj parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="2acb9-128">Copy your connection string from the Azure Cosmos DB extension by right-clicking the learning-module account, and clicking **Copy Connection String**.</span></span>

    ![Rozszerzenie usługi Azure Cosmos DB dla programu Visual Studio Code](../media/2-setup/vs-code-copy-connection-string.gif) 

10. <span data-ttu-id="2acb9-130">Wklej parametry połączenia do pliku tekstowego, a następnie skopiuj część **AccountEndpoint** z pliku tekstowego do sekcji **EndpointUrl** w pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="2acb9-130">Paste the connection string into a text file, and then copy the **AccountEndpoint** portion from the text file into the **EndpointUrl** in Program.cs.</span></span>

    <span data-ttu-id="2acb9-131">Sekcja AccountEndpoint powinna wyglądać podobnie do poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="2acb9-131">The AccountEndpoint should look like the following code:</span></span>

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. <span data-ttu-id="2acb9-132">Teraz skopiuj wartość **AccountKey** z wartości tekstowej do wartości **PrimaryKey** w pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="2acb9-132">Now copy the **AccountKey** value from the text value into the **PrimaryKey** value in Program.cs.</span></span>

12. <span data-ttu-id="2acb9-133">W zintegrowanym terminalu wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.</span><span class="sxs-lookup"><span data-stu-id="2acb9-133">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

13. <span data-ttu-id="2acb9-134">Dodaj nowe zadanie asynchroniczne, aby utworzyć nowego klienta, a następnie sprawdź, czy baza danych Users istnieje, dodając następującą metodę po metodzie main.</span><span class="sxs-lookup"><span data-stu-id="2acb9-134">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the main method.</span></span>
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. <span data-ttu-id="2acb9-135">W zintegrowanym terminalu ponownie wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.</span><span class="sxs-lookup"><span data-stu-id="2acb9-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

15. <span data-ttu-id="2acb9-136">Skopiuj i wklej następujący kod do metody **Main**, zastępując bieżący wiersz `Console.WriteLine("Hello World!");`.</span><span class="sxs-lookup"><span data-stu-id="2acb9-136">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

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

16. <span data-ttu-id="2acb9-137">W zintegrowanym terminalu ponownie wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.</span><span class="sxs-lookup"><span data-stu-id="2acb9-137">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="2acb9-138">W konsoli zostaną wyświetlone następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2acb9-138">The console displays the following output.</span></span>
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a><span data-ttu-id="2acb9-139">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="2acb9-139">Summary</span></span>

<span data-ttu-id="2acb9-140">W tym module przygotowano podstawy dla aplikacji usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2acb9-140">In this module, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="2acb9-141">Skonfigurowano środowisko programistyczne w programie Visual Studio Code, utworzono prosty projekt HelloWorld, połączono projekt z punktem końcowym usługi Azure Cosmos DB i sprawdzono, czy baza danych i kolekcja istnieją.</span><span class="sxs-lookup"><span data-stu-id="2acb9-141">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>