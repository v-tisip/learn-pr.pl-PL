<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Po utworzeniu dokumentów w aplikacji utwórzmy do nich zapytania z poziomu aplikacji. Usługa Azure Cosmos DB używa zapytań SQL i zapytań LINQ. Zapytania SQL i sposób ich uruchamiania w portalu omówiono w module **Dodawanie danych i wykonywania zapytań o dane w bazie danych**. 

Dlatego w tym rozdziale skoncentrujemy się na wykonywaniu zapytań SQL i zapytań LINQ z poziomu aplikacji.

Do przetestowania tych zapytań użyjemy dokumentów użytkownika utworzonych na potrzeby Twojej aplikacji sklepu internetowego.

## <a name="linq-query-basics"></a>Podstawowe informacje na temat zapytań LINQ

LINQ to model programowania .NET, który wyraża obliczenia jako kwerendy w strumieniach obiektów. Można utworzyć obiekt **IQueryable** wykonujący zapytania bezpośrednio do usługi Azure Cosmos DB, która tłumaczy zapytanie LINQ na zapytanie Cosmos DB. Zapytanie jest następnie przekazywane do serwera usługi Azure Cosmos DB w celu pobrania zestawu wyników w formacie JSON. Zwrócone wyniki są deserializowane na strumień obiektów .NET po stronie klienta. Wielu programistów preferuje zapytania LINQ, ponieważ zapewniają one jeden spójny model programowania pod względem sposobu współdziałania z obiektami w kodzie aplikacji i sposobu wyrażania logiki zapytań działającej w bazie danych.

W poniższej tabeli przedstawiono sposób tłumaczenia zapytań LINQ na zapytania SQL.

| Wyrażenie LINQ | Tłumaczenie SQL |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a>Wykonywanie zapytań SQL i LINQ

1. W poniższym przykładzie pokazano, jak można wykonać zapytanie w środowisku SQL, LINQ lub LINQ lambda z poziomu kodu .NET. Skopiuj kod i dodaj go za metodą **DeleteUserDocument**.

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

2. Skopiuj poniższy kod i wklej go do metody **BasicOperations** przed wierszem `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.
    
    ```
    dotnet run
    ```

    W konsoli zostaną wyświetlone następujące dane wyjściowe.

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    Gratulacje! Przy użyciu zapytań SQL i LINQ została pomyślnie pobrana kolekcja użytkowników usługi Azure Cosmos DB.

## <a name="summary"></a>Podsumowanie

W tym rozdziale uzyskaliśmy informacje na temat zapytań LINQ, a następnie dodaliśmy zapytanie SQL i LINQ do aplikacji, aby pobrać rekordy użytkowników.