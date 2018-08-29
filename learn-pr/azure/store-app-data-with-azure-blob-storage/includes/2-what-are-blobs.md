## <a name="what-are-blobs-and-how-are-they-used"></a>Co to są obiekty blob i jak ich używać?

Obiekty blob to „pliki w chmurze”. Aplikacje pracują z obiektami blob prawie w taki sam sposób, jak z plikami na dysku, odczytując i zapisując dane. Jednak w przeciwieństwie do pliku lokalnego do obiektów blob można uzyskać dostęp z dowolnego miejsca mającego połączenie z Internetem. 

Usługa Azure Blob Storage *nie ma określonej struktury*, co oznacza, że nie ma żadnych ograniczeń co do rodzaju danych, które może przechowywać. Na przykład obiekt blob może zawierać dokument PDF, obraz JPG, plik JSON, materiały wideo itd. Obiekty blob nie są ograniczone do typowych formatów plików &mdash; obiekt blob może zawierać gigabajty danych binarnych przesyłanych strumieniowo z przyrządu naukowego, zaszyfrowany komunikat dla innej aplikacji lub dane w niestandardowym formacie dla projektowanej aplikacji.

Obiekty blob zwykle nie są odpowiednie dla danych strukturalnych, które muszą być często używane w zapytaniach. Mają one większe opóźnienie niż pamięć i dysk lokalny oraz nie mają funkcji indeksowania, które powodują, że bazy danych skutecznie obsługują uruchamianie zapytania. Jednak obiekty blob są często stosowane w *połączeniu* z bazami danych w celu przechowywania danych, dla których nie można wysyłać dotyczących ich zapytań. Na przykład aplikacja z bazą danych profilów użytkowników może przechowywać zdjęcia profilowe w obiektach blob. Każdy rekord użytkownika w bazie danych obejmuje nazwę lub adres URL obiektu blob zawierającego zdjęcie użytkownika.

Obiekty blob są używane do przechowywania danych na wiele różnych sposobów we wszelkiego rodzaju aplikacjach i architekturach:

* Aplikacje, które muszą przesyłać duże ilości danych za pośrednictwem systemu obsługi komunikatów obsługującego tylko małe komunikaty, mogą przechowywać dane w obiektach blob i wysyłać adresy URL obiektów blob w komunikatach.
* Magazyn obiektów blob może być używany jak system plików do przechowywania i udostępniania dokumentów i innych danych osobowych.
* Statyczne zasoby internetowe, takie jak obrazy, mogą być przechowywane w obiektach blob i udostępniane do publicznego pobrania tak, jakby były plikami na serwerze internetowym.
* Wiele składników platformy Azure używa obiektów blob w tle. Na przykład usługa Azure Cloud Shell przechowuje Twoje pliki i konfigurację w obiektach blob, a usługa Azure Virtual Machines używa obiektów blob jako magazynu na dysku twardym.

Niektóre aplikacje będą stale tworzyć, aktualizować i usuwać obiekty blob jako część swojej pracy. Inne będą używać niewielkiego zestawu obiektów blob i rzadko je zmienić.

## <a name="storage-accounts-containers-and-metadata"></a>Konta magazynu, kontenery i metadane

W magazynie obiektów blob każdy obiekt blob istnieje wewnątrz *kontenera obiektów blob*. Konto magazynu może zawierać nieograniczoną liczbę kontenerów, a każdy kontener może zawierać nieograniczoną liczbę obiektów blob. Kontenery są „płaskie” &mdash; umożliwiają przechowywanie tylko obiektów blob, a nie innych kontenerów.

**DO WYKONANIA: ten obraz należy zastąpić lepszym**

![Konta, kontenery i obiekty blob](../media-drafts/2-storage-container-blob.png)

Obiekty blob i kontenery obsługują metadane w postaci par ciągów nazwa-wartość. Aplikacje mogą używać metadanych do dowolnych zastosowań: czytelny dla człowieka opis zawartości obiektu blob, który ma być wyświetlany przez aplikację, ciąg, którego aplikacja używa do określenia sposobu przetwarzania danych obiektu blob itd.

> [!TIP]
> Magazyn obiektów blob nie dostarcza żadnych mechanizmów do wyszukiwania i sortowania obiektów blob według metadanych. Zobacz sekcję dotyczącą dodatkowych zasobów na końcu tego modułu, aby poznać informacje o korzystaniu z usługi Azure Search, aby to osiągnąć.

## <a name="the-blob-storage-api-and-client-libraries"></a>Interfejs API usługi Blob Storage i biblioteki klienckie

Interfejs API usługi Blob Storage jest oparty na protokole REST i jest obsługiwany przez biblioteki klienckie w wielu popularnych językach. Umożliwia on pisanie aplikacji, które tworzą i usuwają obiekty blob i kontenery, przekazują i pobierają dane obiektów blob oraz wyświetlają listę obiektów blob w kontenerze.