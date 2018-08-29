Wyobraź sobie, że zajmujesz się fotografią i masz witrynę internetową, w której zamieszczasz zdjęcia. Ponieważ masz mało czasu, nie przekazujesz zdjęć regularnie — ale chcesz powiadamiać fanów o przekazaniu nowego zdjęcia. Postanawiasz utworzyć funkcję platformy Azure, która automatycznie wyśle tweeta za każdym razem, gdy prześlesz zdjęcie do kontenera usługi Azure Blob Storage.

Tutaj nauczysz się, jak utworzyć wyzwalacz obiektu blob i wydać mu instrukcję monitorowania konkretnej lokalizacji w kontenerze usługi Azure Blob Storage.

## <a name="what-is-azure-storage"></a>Co to jest Azure Storage?

Azure Storage to rozwiązanie do magazynowania w chmurze firmy Microsoft, które obsługuje wszystkie rodzaje danych, w tym obiekty blob, kolejki oraz dane NoSQL. Celem usługi Azure Storage jest udostępnienie magazynu danych o następujących cechach:

- Wysoka dostępność
- Bezpieczeństwo
- Skalowalność
- Zarządzanie

Nie będziemy skupiać się na omawianiu usługi Azure Storage. Użyjemy jej tylko do utworzenia obiektów blob, które będą wyzwalały funkcję.

## <a name="what-is-azure-blob-storage"></a>Co to jest usługa Azure Blob Storage?

Usługa Azure Blob Storage to rozwiązanie do magazynowania obiektów zaprojektowane do przechowywania dużych ilości danych bez struktury. 

Usługa Azure Blob Storage doskonale sprawdza się w następujących sytuacjach:

- Przechowywanie plików.
- Obsługiwanie plików.
- Przesyłanie strumieniowe audio i wideo.
- Zapisywanie danych dzienników.

Istnieją trzy typy obiektów blob: **blokowe obiekty blob**, **uzupełnialne obiekty blob** i **stronicowe obiekty blob**. Blokowe obiekty blob są używane najczęściej. Umożliwiają sprawne przechowywanie danych tekstowych lub binarnych. Uzupełnialne obiekty blob są podobne do blokowych obiektów blob, ale zostały zaprojektowane pod kątem operacji dołączania, na przykład tworzenia pliku dziennika, który jest stale aktualizowany. Stronicowe obiekty blob składają się ze stronic i zostały zaprojektowane pod kątem częstych losowych operacji odczytu i zapisu.

## <a name="what-is-a-blob-trigger"></a>Co to jest wyzwalacz obiektu blob?

Wyzwalacz obiektu blob to wyzwalacz, który wykonuje funkcję po przekazaniu pliku lub zaktualizowaniu go w usłudze Azure Blob Storage. Aby utworzyć wyzwalacz obiektu blob, należy utworzyć konto usługi Azure Storage i podać lokalizację monitorowaną przez wyzwalacz.

## <a name="how-to-create-a-blob-trigger"></a>Jak utworzyć wyzwalacz obiektu blob

Podobnie jak w przypadku innych wyzwalaczy, które widzieliśmy do tej pory, wyzwalacz obiektu blob jest tworzony w witrynie Azure Portal. W ramach funkcji platformy Azure wybierz pozycję **Wyzwalacz obiektu blob** z listy wstępnie zdefiniowanych typów wyzwalaczy. Następnie wprowadź logikę, która ma zostać wykonana, gdy obiekt blob zostanie utworzony lub zaktualizowany.

Warto przyjrzeć się ustawieniu **Ścieżka**. Ustawienie **Ścieżka** informuje wyzwalacz obiektu blob, jaką lokalizację ma monitorować, aby sprawdzić, czy obiekt blob został przekazany lub zaktualizowany. Domyślnie wartość ustawienia **Ścieżka** to: 

> samples-workitems/{name}

Podzielmy ją na dwie części: *samples-workitems* i *{name}*. Pierwsza część, czyli *samples-workitems*, oznacza kontener obiektów blob monitorowany przez wyzwalacz. Druga część, czyli *{name}*, oznacza, że wyzwalacz wywoła funkcję niezależnie od typu pliku. Funkcja jest wywoływana, ponieważ nie ma żadnego filtru. Można na przykład określić, że wyzwalacz ma wywołać funkcję tylko wtedy, gdy dodany zostanie plik w formacie PNG, używając następującej składni:

> samples-workitems/{name}.png

Ostatnia istotna informacja związana z tą koncepcją to tekst *name*. Tekst *name* reprezentuje parametr w funkcji platformy Azure, który otrzymuje nazwę dodanego pliku. Jeśli na przykład przekażę plik o nazwie *resume.txt*, moja funkcja platformy Azure odbierze tę wartość jako ciąg za pośrednictwem parametru *name*.

## <a name="summary"></a>Podsumowanie

Wyzwalacz obiektu blob wywołuje funkcję platformy Azure, gdy rozpozna aktywność w konkretnej lokalizacji na koncie usługi Azure Blob Storage. Możesz ustawić monitorowaną lokalizację, modyfikując wartość **Ścieżka** w witrynie Azure Portal.
