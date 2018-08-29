Teraz, gdy już rozumiesz, jak jednostki żądania są używane do określania przepływności bazy danych oraz jak klucz partycji tworzy strategię skalowania bazy danych, masz wszystko gotowe, aby utworzyć swoją bazę danych i kolekcję.

## <a name="creating-your-database-and-collection"></a>Tworzenie bazy danych i kolekcji

1. W witrynie Azure Portal kliknij opcję **Eksplorator danych** > **Nowa kolekcja**.
    
    Po prawej stronie zostanie wyświetlony obszar **Dodaj kolekcję**. Należy przewinąć w prawą stronę, aby go zobaczyć.

    ![Eksplorator danych w witrynie Azure Portal, blok Dodaj kolekcję](../media/5-create-a-database-and-collection/azure-cosmosdb-data-explorer.png)

2. Na stronie **Dodaj kolekcję** wprowadź ustawienia dla nowej kolekcji.

    Ustawienie|Sugerowana wartość|Opis
    ---|---|---
    Identyfikator bazy danych|Użytkownicy|Wprowadź *Użytkownicy* jako nazwę nowej bazy danych. Nazwy baz danych muszą zawierać od 1 do 255 znaków i nie mogą zawierać znaków /, \\, #, ? ani mieć spacji na końcu.
    Identyfikator kolekcji|WebCustomers|Wprowadź *WebCustomers* jako nazwę nowej kolekcji. W przypadku identyfikatorów kolekcji obowiązują takie same wymagania dotyczące znaków, jak dla nazw baz danych.
    Pojemność magazynu| Nieograniczona liczba |Użyj wartości domyślnej **Nieograniczona**. Ta wartość oznacza pojemność magazynu bazy danych oraz umożliwia skalowanie bazy danych w poziomie zgodnie z potrzebami.
    Klucz partycji|/UserId|UserID to dobry klucz partycji na potrzeby scenariusza handlu detalicznego online, ponieważ wiele zapytań jest opartych na identyfikatorze klienta.
    Przepływność|1000 RU|Zmień przepływność na 1000 jednostek żądania na sekundę (RU/s). 1000 to minimalna wartość RU/s, jaką można ustawić, aby włączyć skalowanie automatyczne.
    
    Na razie nie zaznaczaj żadnej opcji przepływności bazy danych aprowizacji, a także nie dodawaj żadnych unikatowych kluczy do kolekcji. 
    
3. Kliknij przycisk **OK**.

    W Eksploratorze danych zostanie wyświetlona nowa baza danych i kolekcja.

    ![Eksplorator danych w witrynie Azure Portal z widoczną nową bazą danych i kolekcją](../media/5-create-a-database-and-collection/azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Podsumowanie

W tym module użyto wiedzy o kluczach partycji oraz jednostkach żądania, aby utworzyć bazę danych i kolekcję z ustawieniami przepływności i skalowania dostosowanymi do potrzeb biznesowych.