Następnie przyjrzyjmy się danym w naszej bazie danych. Ważne jest upewnienie się, że możemy obsłużyć wolumen transakcji odpowiedni do naszych potrzeb biznesowych. Wymagania dotyczące przepływności nie zawsze są spójne. Na przykład możesz budować internetową witrynę zakupową, która musi być skalowana podczas wyprzedaży lub dni wolnych od pracy. Zaczniemy od oszacowania wymagań dotyczących przepływności bazy danych.

## <a name="what-is-database-throughput"></a>Co to jest przepływność bazy danych? 

Przepływność bazy danych to liczba operacji odczytu i zapisu, które baza danych może wykonać w ciągu jednej sekundy. 

Aby strategicznie skalować przepływność, musisz oszacować potrzebną przepływność, szacując liczbę operacji odczytu i zapisu, które musisz obsłużyć w różnym czasie i w przypadku różnych rozmiarów dokumentów. Jeśli oszacujesz to poprawnie, uszczęśliwisz swoich użytkowników, gdy pojawi się szczyt zapotrzebowania. Jeśli oszacujesz to niepoprawnie, żądania mogą mieć ograniczoną prędkość i operacje będą musiały poczekać i być ponowione, co najprawdopodobniej spowoduje duże opóźnienia i niezadowolenie klientów.

## <a name="what-is-a-request-unit"></a>Co to jest jednostka żądania?

Usługa Azure Cosmos DB mierzy przepływność przy użyciu czegoś, co jest nazywane **jednostką żądania (RU)**. Użycie jednostek żądania jest mierzone na sekundę, dzięki czemu jednostką miary jest **jednostka żądania na sekundę (RU/s)**. Musisz zarezerwować taką liczbę jednostek RU/s, którą ma z wyprzedzeniem aprowizować usługa Azure Cosmos DB, aby obsłużyć oszacowane obciążenie. Następnie możesz skalować jednostki RU/s w górę lub w dół w dowolnym momencie, aby zaspokoić bieżące zapotrzebowanie.

## <a name="request-unit-basics"></a>Podstawowe informacje o jednostce żądania

Pojedyncza jednostka żądania, 1 RU, jest równa szacowanemu kosztowi wykonania pojedynczego żądania GET na dokumencie o wielkości 1 KB za pomocą identyfikatora dokumentu. Wykonywanie operacji GET za pomocą identyfikatora dokumentu jest skutecznym sposobem pobierania dokumentu, a więc koszt jest mały. Tworzenie, zastępowanie lub usuwanie tego samego elementu wymaga dodatkowego przetwarzania przez usługę, a więc wymaga większej liczby jednostek żądania.

Liczba jednostek żądania użytych do zmian operacji zmienia się w zależności od rozmiaru dokumentu, liczby właściwości w dokumencie, wykonywanej operacji i niektórych dodatkowych złożonych pojęć, takich jak spójność i zasady indeksowania.

W poniższej tabeli przedstawiono liczbę jednostek żądania wymaganych dla elementów w trzech różnych rozmiarach (1 KB, 4 KB i 64 KB) i na dwóch różnych poziomach wydajności (500 operacji odczytu na sekundę + 100 operacji zapisu na sekundę oraz 500 operacji odczytu na sekundę + 500 operacji zapisu na sekundę). W tym przykładzie spójność danych została ustawiona na **Sesja**, a zasady indeksowania — na **Brak**.

| Rozmiar elementu | Odczyty/s | Zapisy/s | Jednostki żądania
| --- | --- | --- | --- |
| 1 KB | 500 | 100 | (500 * 1) + (100 * 5) = 1000 RU/s
| 1 KB | 500 | 500 | (500 * 1) + (500 * 5) = 3000 RU/s
| 4 KB | 500 | 100 | (500 * 1,3) + (100 * 7) = 1350 RU/s
| 4 KB | 500 | 500 | (500 * 1,3) + (500 * 7) = 4150 RU/s
| 64 KB | 500 | 100 | (500 * 10) + (100 * 48) = 9800 RU/s
| 64 KB | 500 | 500 | (500 * 10) + (500 * 48) = 29 000 RU/s
 
Jak widać, im większy jest element i im więcej odczytów i zapisów jest wymaganych, tym więcej jednostek żądania należy zarezerwować. Jeśli trzeba oszacować potrzebną przepływność aplikacji, [Planista wydajności](https://www.documentdb.com/capacityplanner) usługi Azure Cosmos DB jest narzędziem internetowym, które pozwala przekazać przykładowy dokument JSON i ustawić liczbę operacji, które należy wykonać na sekundę. Następnie podaje on oszacowaną wartość całkowitą do zarezerwowania.

## <a name="exceeding-throughput-limits"></a>Przekraczanie limitów przepływności

Jeśli nie zarezerwujesz wystarczającej liczby jednostek żądania i podejmiesz próbę odczytu lub zapisu większej ilości danych niż zezwala aprowizowana przepływność, żądanie będzie miało ograniczoną szybkość. Gdy żądanie ma ograniczoną szybkość, musi nastąpić próba jego ponownego wykonania po upływie określonego czasu. Jeśli używasz zestawu .NET SDK, żądanie zostanie automatycznie ponowione po odczekaniu czasu określonego w nagłówku retry-after (ponów po).

## <a name="creating-an-account-built-to-scale"></a>Tworzenie konta utworzonego pod kątem skalowania

W każdej chwili możesz zmienić liczbę jednostek żądania aprowizowanych do bazy danych. Dlatego w okresach dużych obciążeń możesz skalować w górę, aby uwzględnić duże zapotrzebowanie, a następnie zmniejszyć aprowizowaną przepływność poza godzinami szczytu w celu zmniejszenia kosztów.

Podczas tworzenia konta możesz aprowizować w portalu co najmniej 400 RU/s lub co najwyżej 250 000 RU/s. Jeśli potrzebujesz jeszcze większej przepływności, wypełnij bilet w witrynie Azure Portal. Ustawienie początkowej przepływności na 1000 RU/s jest zalecane dla prawie wszystkich kont, ponieważ jest to minimalna wartość, przy której baza danych będzie automatycznie skalowana, jeśli będziesz potrzebować więcej niż 10 GB pamięci masowej. Jeśli ustawisz początkową przepływność na dowolną wartość mniejszą niż 1000 RU/s, Twoja baza danych nie będzie skalowana do wielkości przekraczającej 10 GB, chyba że ponownie aprowizujesz bazę danych i podasz klucz partycji. Klucze partycji pozwalają na szybkie wyszukiwanie danych w usłudze Azure Cosmos DB i umożliwiają jej automatyczne skalowanie bazy danych w razie potrzeby. Klucze partycji zostały omówione w następnej części.

## <a name="summary"></a>Podsumowanie

Teraz rozumiesz sposób szacowania i określania zakresu przepływności dla usługi Azure Cosmos DB przy użyciu jednostek żądania. Jednostki żądania można zmodyfikować w dowolnym momencie, a ustawienie ich na 1000 RU/s podczas tworzenia konta pozwala zagwarantować, że baza danych jest gotowa do późniejszego skalowania.