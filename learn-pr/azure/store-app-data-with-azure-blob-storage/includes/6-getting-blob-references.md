<span data-ttu-id="2f234-101">Praca z poszczególnymi obiektami blob w zestawie SDK usługi Azure Storage dla platformy .NET Core wymaga *odwołania do obiektu blob* &mdash; wystąpienia obiektu `ICloudBlob`.</span><span class="sxs-lookup"><span data-stu-id="2f234-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="2f234-102">Aby uzyskać obiekt `ICloudBlob`, możesz zażądać go przy użyciu nazwy obiektu blob lub wybrać go z listy obiektów blob w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="2f234-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="2f234-103">Obydwie opcje wymagają kontenera `CloudBlobContainer`. Sposób jego uzyskiwania został przedstawiony w poprzednim module.</span><span class="sxs-lookup"><span data-stu-id="2f234-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="2f234-104">Pobieranie obiektów blob według nazwy</span><span class="sxs-lookup"><span data-stu-id="2f234-104">Getting blobs by name</span></span>

<span data-ttu-id="2f234-105">Wywołaj jedną z metod `GetXXXReference` w kontenerze `CloudBlobContainer`, aby pobrać obiekt `ICloudBlob` według nazwy.</span><span class="sxs-lookup"><span data-stu-id="2f234-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="2f234-106">Jeśli znasz typ pobieranego obiektu blob, wybierz preferowaną metodę spośród kilku bardziej szczegółowych (`GetBlockBlobReference`, `GetAppendBlobReference` lub `GetPageBlobReference`).</span><span class="sxs-lookup"><span data-stu-id="2f234-106">If you know the type of the blob you are retrieving, prefer using one of the more specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`).</span></span>

<span data-ttu-id="2f234-107">Żadna z tych metod nie powoduje wywołania sieci ani nie potwierdza, czy obiekt blob istnieje w rzeczywistości.</span><span class="sxs-lookup"><span data-stu-id="2f234-107">None of these methods make a network call, nor do they confirm whether or not the blob actually exists.</span></span> <span data-ttu-id="2f234-108">Osobna metoda, `GetBlobReferenceFromServerAsync`, wywołuje interfejs API usługi Blob Storage i powoduje zgłoszenie wyjątku, jeśli obiekt blob jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="2f234-108">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="2f234-109">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="2f234-109">Listing blobs in a container</span></span>

<span data-ttu-id="2f234-110">Listę obiektów blob w kontenerze można uzyskać za pomocą metody `ListBlobsSegmentedAsync` kontenera `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="2f234-110">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="2f234-111">Określenie *segmentowane* odwołuje się do osobnych stron zwróconych wyników &mdash; jedno wywołanie elementu `ListBlobsSegmentedAsync` nigdy nie gwarantuje zwrócenia wszystkich wyników na jednej stronie.</span><span class="sxs-lookup"><span data-stu-id="2f234-111">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="2f234-112">Być może trzeba będzie wielokrotnie powtórzyć wywołanie za pomocą zwracanego tokenu `ContinuationToken`, aby przejść przez wszystkie strony.</span><span class="sxs-lookup"><span data-stu-id="2f234-112">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="2f234-113">Powoduje to, że kod służący do wyświetlania listy obiektów blob jest nieco bardziej skomplikowany niż kod służący do przekazywania lub pobierania, ale istnieje standardowy wzorzec, za pomocą którego można pobrać każdy obiekt blob w kontenerze:</span><span class="sxs-lookup"><span data-stu-id="2f234-113">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

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

<span data-ttu-id="2f234-114">Będzie on wywoływać element `ListBlobsSegmentedAsync` wielokrotnie do momentu, gdy token `continuationToken` będzie mieć wartość `null`, co będzie oznaczać koniec wyników.</span><span class="sxs-lookup"><span data-stu-id="2f234-114">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="2f234-115">Przetwarzanie wyników z listy</span><span class="sxs-lookup"><span data-stu-id="2f234-115">Processing list results</span></span>

<span data-ttu-id="2f234-116">Obiekt uzyskiwany z elementu `ListBlobsSegmentedAsync` zawiera właściwość `Results` typu `IEnumerable<IListBlobItem>`.</span><span class="sxs-lookup"><span data-stu-id="2f234-116">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="2f234-117">Elementy `IListBlobItem` zawierają szereg właściwości kontenera obiektów blob i adres URL, ale nie zawierają metod przekazywania ani pobierania.</span><span class="sxs-lookup"><span data-stu-id="2f234-117">`IListBlobItem`s contain a handful of properties about the blob's container and URL, but no upload or download methods.</span></span> <span data-ttu-id="2f234-118">Dzieje się tak, ponieważ niektóre obiekty wynikowe mogą być obiektami `CloudBlobDirectory` reprezentującymi katalogi wirtualne, a nie poszczególne obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="2f234-118">This is because some of the result objects may be `CloudBlobDirectory` objects that represent virtual directories rather than individual blobs.</span></span>

<span data-ttu-id="2f234-119">Jeśli interesują Cię tylko poszczególne obiekty blob, do filtrowania wyników możesz użyć metody `OfType<>`.</span><span class="sxs-lookup"><span data-stu-id="2f234-119">If you are only interested in individual blobs, you can use the `OfType<>` method to filter the results.</span></span> <span data-ttu-id="2f234-120">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="2f234-120">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

<span data-ttu-id="2f234-121">Korzystanie z elementu `OfType<>` wymaga odwołania do przestrzeni nazw `System.Linq` (`using System.Linq;`).</span><span class="sxs-lookup"><span data-stu-id="2f234-121">Using `OfType<>` will require a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="2f234-122">Ćwiczenie</span><span class="sxs-lookup"><span data-stu-id="2f234-122">Exercise</span></span>

<span data-ttu-id="2f234-123">Jedna z funkcji w naszej aplikacji wymaga pobrania listy obiektów blob z interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2f234-123">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="2f234-124">Użyjemy wzorca pokazanego powyżej, aby wyświetlić listę wszystkich obiektów blob w naszym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="2f234-124">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="2f234-125">Podczas przetwarzania listy uzyskujemy nazwy poszczególnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2f234-125">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="2f234-126">Otwórz plik `BlobStorage.cs` w edytorze i wypełnij metodę `GetNames` następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="2f234-126">Open `BlobStorage.cs` in the editor and fill in `GetNames` with the following code:</span></span>

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

<span data-ttu-id="2f234-127">Nazwy zwracane przez tę metodę są przetwarzane przez kontrolera `FilesController` w celu przekształcenia ich w adresy URL.</span><span class="sxs-lookup"><span data-stu-id="2f234-127">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="2f234-128">Podczas zwracania ich do klienta są one renderowane jako hiperlinki na stronie.</span><span class="sxs-lookup"><span data-stu-id="2f234-128">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>