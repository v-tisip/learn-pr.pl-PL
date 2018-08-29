<span data-ttu-id="d96b7-101">Gdy będziemy mieć odwołanie do obiektu blob, możemy przekazywać i pobierać dane.</span><span class="sxs-lookup"><span data-stu-id="d96b7-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="d96b7-102">Obiekty `ICloudBlob` mają metody `Upload` i `Download`, które obsługują tablice bajtów, strumienie i pliki jako elementy źródłowe i docelowe.</span><span class="sxs-lookup"><span data-stu-id="d96b7-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="d96b7-103">Określone typy mają dla wygody dodatkowe metody &mdash; na przykład klasa `CloudBlockBlob` obsługuje przekazywanie i pobieranie ciągów za pomocą metod `UploadTextAsync` i `DownloadTextAsync`.</span><span class="sxs-lookup"><span data-stu-id="d96b7-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="d96b7-104">Tworzenie nowych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d96b7-104">Creating new blobs</span></span>

<span data-ttu-id="d96b7-105">Aby utworzyć nowy obiekt blob, wywołaj jedną z metod `Upload` względem obiektu blob, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d96b7-105">To create a new blob, you call one of the `Upload` methods on a blob that doesn't exist.</span></span> <span data-ttu-id="d96b7-106">Powoduje to wykonanie dwóch działań: utworzenie obiektu blob i przekazanie danych.</span><span class="sxs-lookup"><span data-stu-id="d96b7-106">This does two things: creates the blob and uploads the data.</span></span> 

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="d96b7-107">Przenoszenie danych do i z obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d96b7-107">Moving data to and from blobs</span></span>

<span data-ttu-id="d96b7-108">Przenoszenie danych do i z obiektu blob to operacja sieciowa, która zajmuje trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="d96b7-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="d96b7-109">W zestawie SDK usługi Azure Storage dla platformy .NET Core wszystkie metody, które wymagają działań sieciowych, zwracają obiekty `Task`, dlatego upewnij się, że Twoje metody kontrolera mają typ `async` zgodnie z potrzebami oraz że względem ich wywołań zastosowano operator `await`, a nie metodę `Wait`.</span><span class="sxs-lookup"><span data-stu-id="d96b7-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure your controller methods are `async` as appropriate and that you are `await`ing method calls and not `Wait`ing on them.</span></span>

<span data-ttu-id="d96b7-110">Powszechnym zaleceniem podczas pracy z dużymi obiektami danych jest użycie strumieni zamiast struktur w pamięci, takich jak tablice bajtów lub ciągi.</span><span class="sxs-lookup"><span data-stu-id="d96b7-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="d96b7-111">W ten sposób można uniknąć buforowania całej zawartości w pamięci przed wysłaniem jej do obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="d96b7-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="d96b7-112">Platforma ASP.NET Core obsługuje odczytywanie strumieni z żądań i odpowiedzi oraz zapisywanie ich w nich.</span><span class="sxs-lookup"><span data-stu-id="d96b7-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="d96b7-113">Równoczesny dostęp</span><span class="sxs-lookup"><span data-stu-id="d96b7-113">Concurrent access</span></span>

<span data-ttu-id="d96b7-114">Inne procesy mogą dodawać, zmieniać lub usuwać obiekty blob, gdy Twoja aplikacja z nich korzysta.</span><span class="sxs-lookup"><span data-stu-id="d96b7-114">It is possible that other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="d96b7-115">Zawsze pisz kod ostrożnie i myśl o problemach powodowanych przez współbieżność, np. usunięcie obiektu blob, gdy próbujesz pobrać z niego dane, lub zmiana w obiekcie blob, gdy nie jest to oczekiwane.</span><span class="sxs-lookup"><span data-stu-id="d96b7-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="d96b7-116">Sekcja Dodatkowe zasoby na końcu tego modułu zawiera informacje o używaniu warunków AccessCondition i dzierżaw obiektów blob do zarządzania równoczesnym dostępem do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d96b7-116">See the Additional Resources section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="d96b7-117">Ćwiczenie</span><span class="sxs-lookup"><span data-stu-id="d96b7-117">Exercise</span></span>

<span data-ttu-id="d96b7-118">Dokończmy naszą aplikację, dodając kod do obsługi przekazywania i pobierania, a następnie wdróżmy ją w usłudze Azure App Service, aby ją przetestować.</span><span class="sxs-lookup"><span data-stu-id="d96b7-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="d96b7-119">Upload</span><span class="sxs-lookup"><span data-stu-id="d96b7-119">Upload</span></span>

<span data-ttu-id="d96b7-120">Aby przekazać obiekt blob zaimplementujemy metodę `BlobStorage.Save` przy użyciu metody `GetBlockBlobReference`, aby uzyskać obiekt `CloudBlockBlob` z kontenera.</span><span class="sxs-lookup"><span data-stu-id="d96b7-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="d96b7-121">Metoda `FilesController.Upload` przekazuje strumień plików do metody `Save`, dzięki czemu możemy użyć metody `UploadFromStreamAsync`, aby maksymalnie wydajnie wykonać przekazywanie.</span><span class="sxs-lookup"><span data-stu-id="d96b7-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="d96b7-122">Otwórz plik `BlobStorage.cs` w edytorze i wypełnij implementację metody `Save` następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="d96b7-122">Open `BlobStorage.cs` in the editor and fill in the `Save` implementation with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="d96b7-123">Kod przekazywania w oparciu o strumień jest bardziej wydajny niż wczytywanie pliku do tablicy bajtów przed wysłaniem go do usługi Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d96b7-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="d96b7-124">Jednak technika oparta na interfejsie `IFormFile`, której używamy do pobrania pliku z klienta, nie jest faktyczną kompleksową implementacją przesyłania strumieniowego i jest odpowiednia tylko do obsługi przekazywania małych plików.</span><span class="sxs-lookup"><span data-stu-id="d96b7-124">However, the `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="d96b7-125">Sekcja Dodatkowe zasoby na końcu tego modułu zawiera informacje o całkowicie strumieniowym przekazywaniu plików.</span><span class="sxs-lookup"><span data-stu-id="d96b7-125">See the Additional Resources section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="d96b7-126">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="d96b7-126">Download</span></span>

<span data-ttu-id="d96b7-127">Metoda `BlobStorage.Load` zwraca obiekt `Stream`, co oznacza, że nasz kod nie musi w ogóle fizycznie przenosić bajtów z usługi Blob Storage &mdash; musimy tylko zwrócić odwołanie do strumienia obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d96b7-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="d96b7-128">Możemy to zrobić za pomocą metody `OpenReadAsync`.</span><span class="sxs-lookup"><span data-stu-id="d96b7-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="d96b7-129">Platforma ASP.NET Core obsłuży odczytywanie i zamykanie strumienia podczas tworzenia odpowiedzi klienta.</span><span class="sxs-lookup"><span data-stu-id="d96b7-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="d96b7-130">Wypełnij metodę `Load` przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d96b7-130">Fill in `Load` with this code:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="d96b7-131">Wdrażanie i uruchamianie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d96b7-131">Deploy and run in Azure</span></span>

<span data-ttu-id="d96b7-132">Nasza aplikacja jest gotowa &mdash; wdróżmy ją i zobaczmy, jak działa.</span><span class="sxs-lookup"><span data-stu-id="d96b7-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="d96b7-133">Uruchom poniższy kod w terminalu usługi Azure Cloud Shell, aby skompilować nasz kod i wdrożyć go w nowym wystąpieniu usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="d96b7-133">Run the following code in the Azure Cloud Shell terminal to build our code and deploy it to a new App Service instance.</span></span> <span data-ttu-id="d96b7-134">Dodajemy również parametry połączenia naszego konta magazynu do konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d96b7-134">We also add our storage account connection string to configuration.</span></span>

```console

```

<span data-ttu-id="d96b7-135">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="d96b7-135">...</span></span>

<span data-ttu-id="d96b7-136">Przekaż i pobierz jakieś pliki, aby przetestować aplikację, a następnie uruchom poniższe polecenie w powłoce, aby wyświetlić obiekty blob, które zostały przekazane:</span><span class="sxs-lookup"><span data-stu-id="d96b7-136">Upload and download some files to test the app, then run the following in the shell to see the blobs that have been uploaded:</span></span>

```console

```

<span data-ttu-id="d96b7-137">**TODO: zrzut ekranu portalu**</span><span class="sxs-lookup"><span data-stu-id="d96b7-137">**TODO pic from portal**</span></span>