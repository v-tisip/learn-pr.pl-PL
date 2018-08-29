Twoja firma wybrała usługę Azure Cosmos DB, aby zaspokoić potrzeby związane z rosnącą bazą klientów i produktów. Tobie przypadło zadanie utworzenia tej bazy danych.

Pierwszym krokiem jest utworzenie konta usługi Azure Cosmos DB. 

## <a name="what-is-an-azure-cosmos-db-account"></a>Co to jest konto usługi Azure Cosmos DB?

Konto usługi Azure Cosmos DB jest zasobem platformy Azure, które działa jako jednostka organizacyjna dla Twoich baz danych. Łączy ono użycie z subskrypcją platformy Azure na potrzeby rozliczeń.

Każde konto usługi Azure Cosmos DB jest skojarzone z jednym z kilku modeli danych obsługiwanych przez usługę Azure Cosmos DB. Możesz utworzyć tyle kont, ile potrzebujesz. 

W przypadku tworzenia nowej aplikacji preferowanym modelem danych jest interfejs API SQL. Jeśli pracujesz z wykresami i tabelami lub migrujesz dane z bazy MongoDB lub Cassandra na platformę Azure, utwórz dodatkowe konta i wybierz odpowiednie modele danych.

Podczas tworzenia konta wybierz znaczący identyfikator — przy jego użyciu będziesz identyfikować swoje konto. Ponadto utwórz konto w regionie platformy Azure, który znajduje się najbliżej Twoich użytkowników, aby zminimalizować opóźnienie między centrum danych i użytkownikami.

Podczas tworzenia konta możesz opcjonalnie skonfigurować sieci wirtualne i nadmiarowość geograficzną, ale można to również zrobić później. W tym module nie będziemy włączać tych ustawień.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Tworzenie konta usługi Azure Cosmos DB w witrynie Azure Portal

<!--TODO: Update portal link with one that routes to free Learning acct-->
1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
2. Kliknij kolejno pozycje **Utwórz zasób** > **Bazy danych** > **Azure Cosmos DB**.
   
   ![Okienko Bazy danych w witrynie Azure Portal](../media/1-introduction/create-nosql-db-databases-json-tutorial-1.png)

3. Na stronie **Nowe konto** wprowadź ustawienia nowego konta usługi Azure Cosmos DB.
 
    Ustawienie|Wartość|Opis
    ---|---|---
    ID|*Wprowadź unikatową nazwę*|Wprowadź unikatową nazwę do identyfikacji tego konta usługi Azure Cosmos DB. Ponieważ adres *documents.azure.com* jest dołączany do podanego identyfikatora w celu utworzenia identyfikatora URI, użyty identyfikator powinien być unikatowy, ale rozpoznawalny.<br><br>Identyfikator może zawierać tylko małe litery, cyfry i znaki łącznika (-) oraz musi zawierać od 3 do 50 znaków.
    Interfejs API|SQL|Interfejs API określa typ konta do utworzenia. Usługa Azure Cosmos DB oferuje pięć interfejsów API odpowiadających potrzebom aplikacji: SQL (baza danych dokumentów), Gremlin (baza danych wykresów), MongoDB (baza danych dokumentów), tabela platformy Azure i Cassandra. Każdy z tych interfejsów wymaga obecnie oddzielnego konta. <br><br>Wybierz pozycję **SQL**, ponieważ w tym module tworzysz bazę danych dokumentów. Zapytania dotyczące tej bazy danych można tworzyć przy użyciu składni języka SQL, a sama baza jest dostępna za pośrednictwem interfejsu API SQL.|
    Subskrypcja|*Twoja subskrypcja*|Wybierz subskrypcję platformy Azure, która ma być używana dla tego konta usługi Azure Cosmos DB. 
    Grupa zasobów|Tworzenie nowego elementu<br><br>*Następnie wprowadź taką samą unikatową nazwę, która została podana powyżej jako identyfikator*|Wybierz pozycję **Utwórz nową**, a następnie wprowadź nazwę nowej grupy zasobów dla konta. Dla uproszczenia można użyć takiej samej nazwy, jak identyfikator. 
    Lokalizacja|*Wybierz region najbliżej Twoich użytkowników*|Wybierz lokalizację geograficzną, w której będzie hostowane Twoje konto usługi Azure Cosmos DB. Użyj lokalizacji znajdującej się najbliżej Twoich użytkowników, aby zapewnić im najszybszy dostęp do danych.
    Włącz nadmiarowość geograficzną| Pozostaw puste | To ustawienie tworzy replikowaną wersję bazy danych w drugim (sparowanym) regionie. Na razie pozostaw to pole puste, ponieważ bazę danych można zreplikować później. 
    Sieci wirtualne|Disabled (Wyłączony)|Na razie pozostaw sieci wirtualne wyłączone. Można je włączyć później. 

4. Kliknij pozycję **Utwórz**.

    ![Strona nowego konta usługi Azure Cosmos DB](../media/1-introduction/azure-cosmos-db-create-new-account.png)

5. Tworzenie konta potrwa kilka minut. Poczekaj, aż w witrynie Portal zostanie wyświetlone powiadomienie, że wdrożenie zakończyło się pomyślnie, a następnie kliknij to powiadomienie. 

    ![Alert powiadomienia](../media/1-introduction/azure-cosmos-db-notification.png)

6. W oknie powiadomienia kliknij pozycję **Przejdź do zasobu**.

    ![Przechodzenie do zasobu](../media/1-introduction/azure-cosmos-db-go-to-resource.png)

    W witrynie Portal zostanie wyświetlona strona **Gratulacje! Konto usługi Azure Cosmos DB zostało utworzone**.

    ![Okienko Powiadomienia w witrynie Azure Portal](../media/1-introduction/azure-cosmos-db-account-created.png)

## <a name="summary"></a>Podsumowanie

Utworzyliśmy konto usługi Azure Cosmos DB, co jest pierwszym krokiem w procedurze tworzenia bazy danych usługi Azure Cosmos DB. Wybraliśmy ustawienia odpowiednie dla Twoich typów danych i ustawiliśmy lokalizację konta w celu zminimalizowania opóźnienia dla użytkowników.
