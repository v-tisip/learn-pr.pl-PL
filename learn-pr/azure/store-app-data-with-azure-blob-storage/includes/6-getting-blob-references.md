Praca z poszczególnymi obiektami blob w zestawie SDK usługi Azure Storage dla platformy .NET Core wymaga *odwołania do obiektu blob* &mdash; wystąpienia obiektu `ICloudBlob`.

Aby uzyskać obiekt `ICloudBlob`, możesz zażądać go przy użyciu nazwy obiektu blob lub wybrać go z listy obiektów blob w kontenerze. Obydwie opcje wymagają kontenera `CloudBlobContainer`. Sposób jego uzyskiwania został przedstawiony w poprzednim module.

## <a name="getting-blobs-by-name"></a>Pobieranie obiektów blob według nazwy

Wywołaj jedną z metod `GetXXXReference` w kontenerze `CloudBlobContainer`, aby pobrać obiekt `ICloudBlob` według nazwy. Jeśli znasz typ pobieranego obiektu blob, wybierz preferowaną metodę spośród kilku bardziej szczegółowych (`GetBlockBlobReference`, `GetAppendBlobReference` lub `GetPageBlobReference`).

Żadna z tych metod nie powoduje wywołania sieci ani nie potwierdza, czy obiekt blob istnieje w rzeczywistości. Osobna metoda, `GetBlobReferenceFromServerAsync`, wywołuje interfejs API usługi Blob Storage i powoduje zgłoszenie wyjątku, jeśli obiekt blob jeszcze nie istnieje.

## <a name="listing-blobs-in-a-container"></a>Wyświetlanie listy obiektów blob w kontenerze

Listę obiektów blob w kontenerze można uzyskać za pomocą metody `ListBlobsSegmentedAsync` kontenera `CloudBlobContainer`. Określenie *segmentowane* odwołuje się do osobnych stron zwróconych wyników &mdash; jedno wywołanie elementu `ListBlobsSegmentedAsync` nigdy nie gwarantuje zwrócenia wszystkich wyników na jednej stronie. Być może trzeba będzie wielokrotnie powtórzyć wywołanie za pomocą zwracanego tokenu `ContinuationToken`, aby przejść przez wszystkie strony. Powoduje to, że kod służący do wyświetlania listy obiektów blob jest nieco bardziej skomplikowany niż kod służący do przekazywania lub pobierania, ale istnieje standardowy wzorzec, za pomocą którego można pobrać każdy obiekt blob w kontenerze:

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

Będzie on wywoływać element `ListBlobsSegmentedAsync` wielokrotnie do momentu, gdy token `continuationToken` będzie mieć wartość `null`, co będzie oznaczać koniec wyników.

### <a name="processing-list-results"></a>Przetwarzanie wyników z listy

Obiekt uzyskiwany z elementu `ListBlobsSegmentedAsync` zawiera właściwość `Results` typu `IEnumerable<IListBlobItem>`. Elementy `IListBlobItem` zawierają szereg właściwości kontenera obiektów blob i adres URL, ale nie zawierają metod przekazywania ani pobierania. Dzieje się tak, ponieważ niektóre obiekty wynikowe mogą być obiektami `CloudBlobDirectory` reprezentującymi katalogi wirtualne, a nie poszczególne obiekty blob.

Jeśli interesują Cię tylko poszczególne obiekty blob, do filtrowania wyników możesz użyć metody `OfType<>`. Oto kilka przykładów:

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

Korzystanie z elementu `OfType<>` wymaga odwołania do przestrzeni nazw `System.Linq` (`using System.Linq;`).

## <a name="exercise"></a>Ćwiczenie

Jedna z funkcji w naszej aplikacji wymaga pobrania listy obiektów blob z interfejsu API. Użyjemy wzorca pokazanego powyżej, aby wyświetlić listę wszystkich obiektów blob w naszym kontenerze. Podczas przetwarzania listy uzyskujemy nazwy poszczególnych obiektów blob.

Otwórz plik `BlobStorage.cs` w edytorze i wypełnij metodę `GetNames` następującym kodem:

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

Nazwy zwracane przez tę metodę są przetwarzane przez kontrolera `FilesController` w celu przekształcenia ich w adresy URL. Podczas zwracania ich do klienta są one renderowane jako hiperlinki na stronie.