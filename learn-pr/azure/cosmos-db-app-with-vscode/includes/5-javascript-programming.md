<span data-ttu-id="8038f-101">Wiele dokumentów w Twojej bazie danych często wymaga aktualizacji w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="8038f-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="8038f-102">W tym module omówiono sposób tworzenia, rejestrowania i uruchamiania procedur składowanych z aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="8038f-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="8038f-103">Tworzenie procedur składowanych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="8038f-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="8038f-104">W tym module procedura składowana OrderId, która zawiera listę wszystkich pozycji w zamówieniu, jest używana do obliczania łącznej kwoty zamówienia.</span><span class="sxs-lookup"><span data-stu-id="8038f-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="8038f-105">Kwota łączna zamówienia jest obliczana na podstawie sumy pozycji w zamówieniu pomniejszonej o wszelkie dywidendy (kredyty), które ma klient, z uwzględnieniem wszystkich kodów kuponów rabatowych.</span><span class="sxs-lookup"><span data-stu-id="8038f-105">The order total is calculated from the sum of the items in the order, less any dividend (credit) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="8038f-106">Skopiuj poniższy kod i wklej go na końcu pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="8038f-106">Copy the following code and paste it into the end of the Program.cs file.</span></span>

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

2. <span data-ttu-id="8038f-107">Teraz skopiuj poniższy kod i wklej go na końcu metody **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="8038f-107">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. <span data-ttu-id="8038f-108">Zapisz plik Program.cs, a następnie na zintegrowanym terminalu uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="8038f-108">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="8038f-109">W konsoli zostaną wyświetlone następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="8038f-109">The console displays the following output.</span></span>

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a><span data-ttu-id="8038f-110">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="8038f-110">Clean up</span></span>

<span data-ttu-id="8038f-111">Jeśli planujesz kontynuować pracę nad modułami na tej ścieżce szkoleniowej, pomiń proces czyszczenia. W przeciwnym razie wykonaj poniższe kroki, aby usunąć zasoby i uniknąć naliczania opłat za korzystanie z usługi.</span><span class="sxs-lookup"><span data-stu-id="8038f-111">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="8038f-112">W witrynie Azure Portal wybierz **grupy zasobów** daleko po lewej stronie, a następnie wybierz utworzoną grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="8038f-112">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="8038f-113">Jeśli menu po lewej stronie jest zwinięte, kliknij</span><span class="sxs-lookup"><span data-stu-id="8038f-113">If the left menu is collapsed, click</span></span> ![przycisk Rozwiń,](../media/5-javascript-programming/expand.png) <span data-ttu-id="8038f-115">aby je rozwinąć.</span><span class="sxs-lookup"><span data-stu-id="8038f-115">to expand it.</span></span>

   ![Metryki w witrynie Azure Portal](../media/5-javascript-programming/delete-resources-select.png)

2. <span data-ttu-id="8038f-117">W nowym oknie wybierz grupę zasobów, a następnie kliknij pozycję **Usuń grupę zasobów**.</span><span class="sxs-lookup"><span data-stu-id="8038f-117">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Metryki w witrynie Azure Portal](../media/5-javascript-programming/delete-resources.png)

3. <span data-ttu-id="8038f-119">W nowym oknie wpisz nazwę grupy zasobów, która ma zostać usunięta, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="8038f-119">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="8038f-120">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="8038f-120">Summary</span></span>

<span data-ttu-id="8038f-121">W tym module utworzono aplikację konsoli .NET Core, która tworzy, aktualizuje i usuwa rekordy użytkowników, wysyła zapytania do użytkowników za pomocą języków SQL i LINQ oraz uruchamia procedurę składowaną, aby utworzyć łączną kwotę zamówienia, która uwzględnia dywidendy użytkowników i kupony rabatowe.</span><span class="sxs-lookup"><span data-stu-id="8038f-121">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to create an order total that takes the users dividends and coupons into account.</span></span>