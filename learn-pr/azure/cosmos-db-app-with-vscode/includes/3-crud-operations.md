<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


Dane są przechowywane w dokumentach JSON w usłudze Azure Cosmos DB. [Dokumenty](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) można tworzyć, pobierać, zastępować lub usuwać w portalu, jak pokazano w poprzednim module, lub programowo, zgodnie z opisem w tym module. Usługa Azure Cosmos DB udostępnia zestawy SDK po stronie klienta dla oprogramowania .NET, .NET Core, Java, Node.js i Python, z których każdy obsługuje te operacje. W tym module będziemy używać zestawu .NET Core SDK do wykonywania operacji CRUD (tworzenie, pobieranie, aktualizowanie i usuwanie). 

Główne operacje dla dokumentów usługi Azure Cosmos DB są częścią klasy [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet). Operacja upsert wykonuje operację tworzenia lub zastępowania w zależności od tego, czy dokument już istnieje.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Aby wykonać dowolną z tych operacji, należy utworzyć klasę, która reprezentuje obiekt zapisany w bazie danych. Ponieważ pracujemy z bazą danych użytkowników, należy utworzyć klasę **User** na potrzeby przechowywania danych podstawowych, takich jak nazwa i identyfikator użytkownika (który jest wymagany, ponieważ jest to klucz partycji umożliwiający skalowanie w poziomie), i podklasy na potrzeby udostępniania preferencji i historii zamówień.

Po utworzeniu klas reprezentujących użytkowników utworzysz dokumenty nowych użytkowników dla każdego wystąpienia, a następnie wykonasz pewne proste operacje CRUD na dokumentach.

## <a name="create-documents"></a>Tworzenie dokumentów

1. Najpierw utwórz klasę **User** reprezentującą obiekty do zapisania w usłudze Azure Cosmos DB. Utworzymy także podklasy **OrderHistory** i **ShippingPreference** używane w klasie **User**. Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON. 

    Aby utworzyć te klasy, skopiuj i wklej następujące klasy **User**, **OrderHistory** i **ShippingPreference** pod metodą **BasicOperations**.

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

2. W zintegrowanym terminalu wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.

    ```csharp
    dotnet run
    ```

3. Teraz skopiuj i wklej zadanie **CreateUserDocumentIfNotExists** pod klasą **ShippingPreference**.

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

4. Następnie dodaj poniższy kod do metody **BasicOperations**.

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

5. W zintegrowanym terminalu ponownie wpisz następujące polecenie, aby uruchomić program w celu sprawdzenia, czy działa.

    ```csharp
    dotnet run
    ```

    Terminal wyświetli następujące dane wyjściowe, wskazujące, że oba rekordy użytkowników zostały utworzone pomyślnie. 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>Czytanie dokumentów

1. Aby odczytać dokumenty z bazy danych, skopiuj następujący kod i umieść go na końcu pliku Program.cs.

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

2.  Skopiuj i wklej następujący kod na końcu metody **BasicOperations**, po wierszu `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.

    ```
    dotnet run
    ```
    Terminal wyświetli następujące dane wyjściowe, przy czym komunikat „Found user 1” („Znaleziono użytkownika 1”) wskazuje, że dokument został znaleziony.

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

## <a name="replace-documents"></a>Zastępowanie dokumentów
Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON. W tym przypadku zaktualizujemy rekord użytkownika, aby uwzględnić zmianę jego nazwiska.

1. Skopiuj i wklej metodę **ReplaceFamilyDocument** poniżej metody **CreateUserDocumentIfNotExists**.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. Skopiuj i wklej następujący kod na końcu metody **BasicOperations**, po wierszu `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.

    ```
    dotnet run
    ```
    Terminal wyświetli następujące dane wyjściowe, przy czym komunikat „Replaced last name for Suh” („Zmieniono nazwisko użytkownika Suh”) wskazuje, że dokument został zastąpiony.

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

## <a name="delete-documents"></a>Usuwanie dokumentów

1. Skopiuj i wklej metodę **DeleteUserDocument** poniżej metody **ReplaceUserDocument**.
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. Skopiuj i wklej następujący kod do metody **BasicOperations** poniżej kodu służącego do wykonania drugiego zapytania.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.

    ```
    dotnet run
    ```

    Gratulacje! Pomyślnie usunięto dokument usługi Azure Cosmos DB.

## <a name="summary"></a>Podsumowanie

W tej sekcji utworzono, zastąpiono i usunięto dokumenty w bazie danych Azure Cosmos DB.