<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


<span data-ttu-id="21e49-101">Dane są przechowywane w dokumentach JSON w usłudze Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21e49-101">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="21e49-102">[Dokumenty](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) można tworzyć, pobierać, zastępować lub usuwać w portalu, jak pokazano w poprzednim module, lub programowo, zgodnie z opisem w tym module.</span><span class="sxs-lookup"><span data-stu-id="21e49-102">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="21e49-103">Usługa Azure Cosmos DB udostępnia zestawy SDK po stronie klienta dla oprogramowania .NET, .NET Core, Java, Node.js i Python, z których każdy obsługuje te operacje.</span><span class="sxs-lookup"><span data-stu-id="21e49-103">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="21e49-104">W tym module będziemy używać zestawu .NET Core SDK do wykonywania operacji CRUD (tworzenie, pobieranie, aktualizowanie i usuwanie).</span><span class="sxs-lookup"><span data-stu-id="21e49-104">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="21e49-105">Główne operacje dla dokumentów usługi Azure Cosmos DB są częścią klasy [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):</span><span class="sxs-lookup"><span data-stu-id="21e49-105">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="21e49-106">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="21e49-106">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="21e49-107">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="21e49-107">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="21e49-108">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="21e49-108">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="21e49-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="21e49-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="21e49-110">Operacja upsert wykonuje operację tworzenia lub zastępowania w zależności od tego, czy dokument już istnieje.</span><span class="sxs-lookup"><span data-stu-id="21e49-110">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="21e49-111">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="21e49-111">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="21e49-112">Aby wykonać dowolną z tych operacji, należy utworzyć klasę, która reprezentuje obiekt zapisany w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="21e49-112">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="21e49-113">Ponieważ pracujemy z bazą danych użytkowników, należy utworzyć klasę **User** na potrzeby przechowywania danych podstawowych, takich jak nazwa i identyfikator użytkownika (który jest wymagany, ponieważ jest to klucz partycji umożliwiający skalowanie w poziomie), i podklasy na potrzeby udostępniania preferencji i historii zamówień.</span><span class="sxs-lookup"><span data-stu-id="21e49-113">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their name and UserId (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="21e49-114">Po utworzeniu klas reprezentujących użytkowników utworzysz dokumenty nowych użytkowników dla każdego wystąpienia, a następnie wykonasz pewne proste operacje CRUD na dokumentach.</span><span class="sxs-lookup"><span data-stu-id="21e49-114">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="21e49-115">Tworzenie dokumentów</span><span class="sxs-lookup"><span data-stu-id="21e49-115">Create documents</span></span>

1. <span data-ttu-id="21e49-116">Najpierw utwórz klasę **User** reprezentującą obiekty do zapisania w usłudze Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21e49-116">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="21e49-117">Utworzymy także podklasy **OrderHistory** i **ShippingPreference** używane w klasie **User**.</span><span class="sxs-lookup"><span data-stu-id="21e49-117">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="21e49-118">Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="21e49-118">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> 

    <span data-ttu-id="21e49-119">Aby utworzyć te klasy, skopiuj i wklej następujące klasy **User**, **OrderHistory** i **ShippingPreference** pod metodą **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="21e49-119">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

    <!--TODO: specify JSON for all of these? -->
    ```csharp
    public class User
    {
            [JsonProperty("id")]
            public string Id { get; set; }
            [JsonProperty("userId")]
            public string UserId { get; set; }
            [JsonProperty("lastName")]
            public string LastName { get; set; }
            [JsonProperty("firstName")]
            public string FirstName { get; set; }
            [JsonProperty("email")]
            public string Email { get; set; }
            [JsonProperty("dividend")]
            public string Dividend { get; set; }
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
            public CouponsUsed[] Coupons { get; set; }
            public override string ToString()
            {
            return JsonConvert.SerializeObject(this);
            }
    }
    
    public class OrderHistory
    {
            public string OrderId { get; set; }
            public string DateShipped { get; set; }
            public string Total { get; set; }
    }
    
    public class ShippingPreference
    {
            public int Priority { get; set; }
            public string AddressLine1 { get; set; }
            public string AddressLine2 { get; set; }
            public string City { get; set; }
            public string State { get; set; }
            public string ZipCode { get; set; }
            public string Country { get; set; }
    }
    
    public class CouponsUsed
    {
            public string CouponCode { get; set; }
    
    }
    
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. <span data-ttu-id="21e49-120">W zintegrowanym terminalu wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.</span><span class="sxs-lookup"><span data-stu-id="21e49-120">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="21e49-121">Teraz skopiuj i wklej zadanie **CreateUserDocumentIfNotExists** pod klasą **ShippingPreference**.</span><span class="sxs-lookup"><span data-stu-id="21e49-121">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                    await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                    this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                    throw;
            }
            }
    }
    ```

4. <span data-ttu-id="21e49-122">Następnie dodaj poniższy kod do metody **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="21e49-122">Then add the following to the **BasicOperations** method.</span></span>

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);
    
                User nelapin = new User
                {
                    Id = "2",
                    UserId = "nelapin",
                    LastName = "Pindakova",
                    FirstName = "Nela",
                    Email = "nelapin@todo.com",
                    Dividend = "8.50",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1001",
                    DateShipped = "08/17/2018",
                    Total = "105.89"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    },
                    new ShippingPreference {
                            Priority = 2,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                    Coupons = new CouponsUsed[]
             {
                 new CouponsUsed{
                     CouponCode = "Fall2018"
                 }
             }
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

5. <span data-ttu-id="21e49-123">W zintegrowanym terminalu ponownie wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.</span><span class="sxs-lookup"><span data-stu-id="21e49-123">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="21e49-124">Terminal wyświetli następujące dane wyjściowe, wskazujące, że oba rekordy użytkowników zostały utworzone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="21e49-124">The terminal displays the following output, indicating that both user records were successfully created.</span></span> 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="21e49-125">Czytanie dokumentów</span><span class="sxs-lookup"><span data-stu-id="21e49-125">Read documents</span></span>

1. <span data-ttu-id="21e49-126">Aby odczytać dokumenty z bazy danych, skopiuj następujący kod i umieść go na końcu pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="21e49-126">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  <span data-ttu-id="21e49-127">Skopiuj i wklej następujący kod na końcu metody **BasicOperations**, po wierszu `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="21e49-127">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="21e49-128">Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="21e49-128">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="21e49-129">Terminal wyświetli następujące dane wyjściowe, przy czym komunikat „Found user 1” („Znaleziono użytkownika 1”) wskazuje, że dokument został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="21e49-129">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a><span data-ttu-id="21e49-130">Zastępowanie dokumentów</span><span class="sxs-lookup"><span data-stu-id="21e49-130">Replace documents</span></span>
<span data-ttu-id="21e49-131">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="21e49-131">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="21e49-132">W tym przypadku zaktualizujemy rekord użytkownika, aby uwzględnić zmianę jego nazwiska.</span><span class="sxs-lookup"><span data-stu-id="21e49-132">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="21e49-133">Skopiuj i wklej metodę **ReplaceFamilyDocument** poniżej metody **CreateUserDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="21e49-133">Copy and paste the **ReplaceFamilyDocument** method underneath your **CreateUserDocumentIfNotExists** method.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. <span data-ttu-id="21e49-134">Skopiuj i wklej następujący kod na końcu metody **BasicOperations**, po wierszu `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="21e49-134">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. <span data-ttu-id="21e49-135">Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="21e49-135">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="21e49-136">Terminal wyświetli następujące dane wyjściowe, przy czym komunikat „Replaced last name for Suh” („Zmieniono nazwisko użytkownika Suh”) wskazuje, że dokument został zastąpiony.</span><span class="sxs-lookup"><span data-stu-id="21e49-136">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh 
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a><span data-ttu-id="21e49-137">Usuwanie dokumentów</span><span class="sxs-lookup"><span data-stu-id="21e49-137">Delete documents</span></span>

1. <span data-ttu-id="21e49-138">Skopiuj i wklej metodę **DeleteUserDocument** poniżej metody **ReplaceUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="21e49-138">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. <span data-ttu-id="21e49-139">Skopiuj i wklej następujący kod do metody **BasicOperations** poniżej kodu służącego do wykonania drugiego zapytania.</span><span class="sxs-lookup"><span data-stu-id="21e49-139">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. <span data-ttu-id="21e49-140">Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="21e49-140">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="21e49-141">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="21e49-141">Congratulations!</span></span> <span data-ttu-id="21e49-142">Pomyślnie usunięto dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21e49-142">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="21e49-143">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="21e49-143">Summary</span></span>

<span data-ttu-id="21e49-144">W tej sekcji utworzono, zastąpiono i usunięto dokumenty w bazie danych Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21e49-144">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>