Sprzedawca internetowy, dla którego pracujesz, planuje w najbliższej przyszłości poszerzenie geograficznego obszaru działania. Ten ruch zwiększy bazę klientów i liczbę transakcji, które obsługujesz. Musisz mieć pewność, że Twoja baza danych jest przystosowana do tego rozszerzenia w każdej chwili.

Strategia partycjonowania gwarantuje, że gdy trzeba będzie zwiększyć bazę danych, będzie to można z łatwością zrobić i nadal wykonywać wydajne zapytania i transakcje.

## <a name="what-is-a-partition-strategy"></a>Co to jest strategia partycjonowania?

Jeśli wciąż będziesz dodawać nowe dane do pojedynczego serwera lub jednej partycji, po pewnym czasie wolne miejsce skończy się. Aby się do tego przygotować, potrzebujesz strategii partycjonowania w celu **skalowania w poziomie**, a nie w pionie. Skalowanie w poziomie umożliwia dodawanie kolejnych partycji do bazy danych zgodnie z potrzebami aplikacji.

Strategia partycjonowania i skalowania w poziomie w usłudze Azure Cosmos DB działa na podstawie klucza partycji, który jest wartością ustawianą podczas tworzenia kolekcji. Po ustawieniu klucza partycji nie można go zmienić bez ponownego tworzenia kolekcji, dlatego wybór odpowiedniego klucza partycji jest ważnym krokiem, który trzeba wykonać na wczesnym etapie procesu programowania.  

W tym module dowiesz się, jak wybrać klucz partycji odpowiedni dla danego scenariusza, i skorzystasz z zalet skalowania automatycznego usługi Azure Cosmos DB.

## <a name="partition-key-basics"></a>Podstawowe informacje dotyczące klucza partycji

Klucz partycji reprezentuje wartość w Twojej bazie danych, której często dotyczą wykonywane zapytania. Dlatego w scenariuszu sprzedawcy internetowego użycie wartości Nazwa użytkownika lub Identyfikator produktu jako klucza partycji jest dobrym rozwiązaniem. Nazwa użytkownika jest dobrym wyborem, ponieważ aplikacja często musi pobierać takie dane, jak ustawienia personalizacji, koszyk, historia zamówień i informacje o profilu użytkownika. Identyfikator produktu jest również dobrym wyborem, ponieważ aplikacja musi wykonywać zapytania dotyczące poziomu zapasów, kosztów wysyłki, opcji kolorów, lokalizacji magazynu i nie tylko.

Klucz partycji powinien dążyć do dystrybucji operacji w bazie danych. Dystrybucja żądań pozwala uniknąć tzw. gorącej partycji. Gorąca partycja to pojedyncza partycja, która otrzymuje o wiele więcej żądań niż inne, co może prowadzić do utworzenia wąskiego gardła przepustowości. Na przykład w omawianej aplikacji handlu elektronicznego bieżąca godzina byłaby złym kluczem partycji, ponieważ wszystkie dane przychodzące byłyby wysyłane do pojedynczego klucza partycji. Nazwa użytkownika lub Identyfikator produktu byłyby lepsze, ponieważ wszyscy użytkownicy w witrynie prawdopodobnie dodawaliby i aktualizowali swoje koszyki zakupów bądź informacje o profilu mniej więcej z taką samą częstotliwością, dzięki czemu odczyty i zapisy byłyby dystrybuowane we wszystkich partycjach użytkowników. Podobnie aktualizacje danych produktów także byłyby w miarę równomiernie dystrybuowane, dzięki czemu Identyfikator produktu byłby dobrym kluczem partycji.

Maksymalne miejsce do magazynowania każdego klucza partycji wynosi 10 GB — jest to rozmiar jednej partycji fizycznej w usłudze Azure Cosmos DB. Jeśli zatem przewidujesz, że pojedynczy rekord Identyfikator użytkownika lub Identyfikator produktu będzie większy niż 10 GB, rozważ zastosowanie klucza złożonego, aby każdy rekord był mniejszy. Przykładem klucza złożonego może być kombinacja Identyfikator użytkownika-data, co wyglądałoby następująco: NazwiskoKlienta-07082018. Podejście z kluczem złożonym umożliwiłoby tworzenie nowej partycji dla każdego dnia, kiedy użytkownik odwiedzi witrynę.

## <a name="best-practices"></a>Najlepsze praktyki

Gdy próbujesz określić odpowiedni klucz partycji i rozwiązanie nie jest oczywiste, pamiętaj o kilku poniższych wskazówkach.

* Nie obawiaj się, że będziesz mieć zbyt wiele kluczy partycji. Im więcej kluczy partycji, tym lepsza skalowalność.

* Aby określić najlepszy klucz partycji dla obciążenia z dużą liczbą odczytów, przejrzyj od trzech do pięciu zapytań, których planujesz używać. Wartość, która jest najczęściej używana w klauzuli WHERE, jest dobrym kandydatem na klucz partycji.

* W przypadku obciążeń z dużą liczbą zapisów należy zrozumieć transakcyjne wymagania obciążenia, ponieważ klucz partycji jest zakresem transakcji z wieloma dokumentami.
