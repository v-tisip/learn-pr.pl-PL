<span data-ttu-id="bd94c-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Po utworzeniu dokumentów w aplikacji utwórzmy do nich zapytania z poziomu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd94c-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="bd94c-102">Usługa Azure Cosmos DB używa zapytań SQL i zapytań LINQ.</span><span class="sxs-lookup"><span data-stu-id="bd94c-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="bd94c-103">Zapytania SQL i sposób ich uruchamiania w portalu omówiono w module **Dodawanie danych i wykonywania zapytań o dane w bazie danych**.</span><span class="sxs-lookup"><span data-stu-id="bd94c-103">SQL queries and how to run them in the portal is discussed in the **Add data and query data in your database** module.</span></span> 

<span data-ttu-id="bd94c-104">Dlatego w tym rozdziale skoncentrujemy się na wykonywaniu zapytań SQL i zapytań LINQ z poziomu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd94c-104">So this unit focuses on running SQL queries and LINQ queries from your application.</span></span>

<span data-ttu-id="bd94c-105">Do przetestowania tych zapytań użyjemy dokumentów użytkownika utworzonych na potrzeby Twojej aplikacji sklepu internetowego.</span><span class="sxs-lookup"><span data-stu-id="bd94c-105">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="bd94c-106">Podstawowe informacje na temat zapytań LINQ</span><span class="sxs-lookup"><span data-stu-id="bd94c-106">LINQ query basics</span></span>

<span data-ttu-id="bd94c-107">LINQ to model programowania .NET, który wyraża obliczenia jako kwerendy w strumieniach obiektów.</span><span class="sxs-lookup"><span data-stu-id="bd94c-107">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="bd94c-108">Można utworzyć obiekt **IQueryable** wykonujący zapytania bezpośrednio do usługi Azure Cosmos DB, która tłumaczy zapytanie LINQ na zapytanie Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd94c-108">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="bd94c-109">Zapytanie jest następnie przekazywane do serwera usługi Azure Cosmos DB w celu pobrania zestawu wyników w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="bd94c-109">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="bd94c-110">Zwrócone wyniki są deserializowane na strumień obiektów .NET po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="bd94c-110">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="bd94c-111">Wielu programistów preferuje zapytania LINQ, ponieważ zapewniają one jeden spójny model programowania pod względem sposobu współdziałania z obiektami w kodzie aplikacji i sposobu wyrażania logiki zapytań działającej w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bd94c-111">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="bd94c-112">W poniższej tabeli przedstawiono sposób tłumaczenia zapytań LINQ na zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="bd94c-112">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="bd94c-113">Wyrażenie LINQ</span><span class="sxs-lookup"><span data-stu-id="bd94c-113">LINQ expression</span></span> | <span data-ttu-id="bd94c-114">Tłumaczenie SQL</span><span class="sxs-lookup"><span data-stu-id="bd94c-114">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="bd94c-115">Wykonywanie zapytań SQL i LINQ</span><span class="sxs-lookup"><span data-stu-id="bd94c-115">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="bd94c-116">W poniższym przykładzie pokazano, jak można wykonać zapytanie w środowisku SQL, LINQ lub LINQ lambda z poziomu kodu .NET.</span><span class="sxs-lookup"><span data-stu-id="bd94c-116">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="bd94c-117">Skopiuj kod i dodaj go za metodą **DeleteUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="bd94c-117">Copy the code and add it after your **DeleteUserDocument** method.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };
    
            // Here we find the Andersen family via its LastName
            IQueryable<USer> userQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(u => u.LastName == "Sun");
    
            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (User user in userQuery)
            {
                Console.WriteLine("\tRead {0}", user);
            }
    
            // Now execute the same query via direct SQL
            IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM User WHERE User.LastName = 'Sun'",
                    queryOptions);
    
            Console.WriteLine("Running direct SQL query...");
            foreach (User user in userQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", user);
            }
    
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. <span data-ttu-id="bd94c-118">Skopiuj poniższy kod i wklej go do metody **BasicOperations** przed wierszem `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.</span><span class="sxs-lookup"><span data-stu-id="bd94c-118">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", "1");` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. <span data-ttu-id="bd94c-119">Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="bd94c-119">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>
    
    ```
    dotnet run
    ```

    <span data-ttu-id="bd94c-120">W konsoli zostaną wyświetlone następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="bd94c-120">The console displays the following output.</span></span>

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    <span data-ttu-id="bd94c-121">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="bd94c-121">Congratulations!</span></span> <span data-ttu-id="bd94c-122">Przy użyciu zapytań SQL i LINQ została pomyślnie pobrana kolekcja użytkowników usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd94c-122">You have successfully your Azure Cosmos DB collection of users by using SQL and LINQ queries.</span></span>

## <a name="summary"></a><span data-ttu-id="bd94c-123">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="bd94c-123">Summary</span></span>

<span data-ttu-id="bd94c-124">W tym rozdziale uzyskaliśmy informacje na temat zapytań LINQ, a następnie dodaliśmy zapytanie SQL i LINQ do aplikacji, aby pobrać rekordy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bd94c-124">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>