Wiele dokumentów w Twojej bazie danych często wymaga aktualizacji w tym samym czasie. W tym module omówiono sposób tworzenia, rejestrowania i uruchamiania procedur składowanych z aplikacji konsoli .NET.

## <a name="create-a-stored-procedure-in-your-app"></a>Tworzenie procedur składowanych w aplikacji

W tym module procedura składowana OrderId, która zawiera listę wszystkich pozycji w zamówieniu, jest używana do obliczania łącznej kwoty zamówienia. Kwota łączna zamówienia jest obliczana na podstawie sumy pozycji w zamówieniu pomniejszonej o wszelkie dywidendy (kredyty), które ma klient, z uwzględnieniem wszystkich kodów kuponów rabatowych.

1. Skopiuj poniższy kod i wklej go na końcu pliku Program.cs.

    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->
    ```csharp
    private async Task UpdateOrderTotal(string databaseName, string collectionName, Order orderId)
    {
    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    
    
                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }
    
                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };
    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;
    
    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
    }
    ```

2. Teraz skopiuj poniższy kod i wklej go na końcu metody **BasicOperations**.

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.

    ```
    dotnet run
    ```

    W konsoli zostaną wyświetlone następujące dane wyjściowe.

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a>Czyszczenie

Jeśli planujesz kontynuować pracę nad modułami na tej ścieżce szkoleniowej, pomiń proces czyszczenia. W przeciwnym razie wykonaj poniższe kroki, aby usunąć zasoby i uniknąć naliczania opłat za korzystanie z usługi.

1. W witrynie Azure Portal wybierz **grupy zasobów** daleko po lewej stronie, a następnie wybierz utworzoną grupę zasobów.  

    Jeśli menu po lewej stronie jest zwinięte, kliknij ![przycisk Rozwiń,](../media/5-javascript-programming/expand.png) aby je rozwinąć.

   ![Metryki w witrynie Azure Portal](../media/5-javascript-programming/delete-resources-select.png)

2. W nowym oknie wybierz grupę zasobów, a następnie kliknij pozycję **Usuń grupę zasobów**.

   ![Metryki w witrynie Azure Portal](../media/5-javascript-programming/delete-resources.png)

3. W nowym oknie wpisz nazwę grupy zasobów, która ma zostać usunięta, a następnie kliknij pozycję **Usuń**.

## <a name="summary"></a>Podsumowanie

W tym module utworzono aplikację konsoli .NET Core, która tworzy, aktualizuje i usuwa rekordy użytkowników, wysyła zapytania do użytkowników za pomocą języków SQL i LINQ oraz uruchamia procedurę składowaną, aby utworzyć łączną kwotę zamówienia, która uwzględnia dywidendy użytkowników i kupony rabatowe.