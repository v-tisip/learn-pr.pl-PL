<span data-ttu-id="16bef-101">Poniżej przedstawiono typowy przepływ pracy aplikacji, które używają usługi Azure Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="16bef-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="16bef-102">**Pobieranie konfiguracji**: podczas uruchamiania załaduj konfigurację, np. parametry połączenia z kluczem konta.</span><span class="sxs-lookup"><span data-stu-id="16bef-102">**Retrieve configuration**: At startup, load the configuration, such as the connection string with the account key.</span></span> <span data-ttu-id="16bef-103">Jest to niezbędne do uwierzytelniania wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16bef-103">This is needed to authenticate API calls.</span></span>
1. <span data-ttu-id="16bef-104">**Inicjowanie klienta**: zainicjuj bibliotekę klienta usługi Azure Storage za pomocą parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="16bef-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="16bef-105">Spowoduje to utworzenie obiektów, których aplikacja będzie używać do pracy z interfejsem API usługi Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="16bef-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="16bef-106">**Używanie**: wykonuj wywołania interfejsu API za pomocą biblioteki klienta, aby wykonywać operacje względem kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="16bef-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="16bef-107">Konfigurowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="16bef-107">Configure your connection string</span></span>

<span data-ttu-id="16bef-108">Przed napisaniem jakiegokolwiek kodu będą potrzebne parametry połączenia dla konta magazynu, które będzie używane.</span><span class="sxs-lookup"><span data-stu-id="16bef-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span> 

<span data-ttu-id="16bef-109">Parametry połączenia zawierają klucz konta.</span><span class="sxs-lookup"><span data-stu-id="16bef-109">The connection string includes your account key.</span></span> <span data-ttu-id="16bef-110">Klucz konta jest uznawany za wpis tajny i powinien być przechowywany w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="16bef-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="16bef-111">Parametry połączenia będą przechowywane w ustawieniu aplikacji usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="16bef-111">We will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="16bef-112">Ustawienie aplikacji to bezpieczne miejsce dla wpisów tajnych aplikacji, ale nie obsługuje ono opracowywania lokalnego i nie stanowi samodzielnie niezawodnego, kompleksowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="16bef-112">An application setting is a secure place for application secrets, but it does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="16bef-113">**Nie umieszczaj kluczy kont magazynu w kodzie ani w niechronionych plikach konfiguracyjnych.**</span><span class="sxs-lookup"><span data-stu-id="16bef-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="16bef-114">Klucze konta magazynu umożliwiają uzyskanie pełnego dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="16bef-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="16bef-115">Wyciek klucza może spowodować nieodwracalne szkody i duże rachunki.</span><span class="sxs-lookup"><span data-stu-id="16bef-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="16bef-116">Sekcja Dodatkowe zasoby na końcu tego modułu zawiera wskazówki dotyczące magazynu oraz porady na temat naprawiania szkód spowodowanych wyciekiem klucza.</span><span class="sxs-lookup"><span data-stu-id="16bef-116">See the Additional Resources section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="16bef-117">Inicjowanie modelu obiektu usługi Blob Storage</span><span class="sxs-lookup"><span data-stu-id="16bef-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="16bef-118">W zestawie SDK usługi Azure Storage dla platformy .NET Core standardowy wzorzec korzystania z usługi Blob Storage składa się z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="16bef-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="16bef-119">Wywołanie metody `CloudStorageAccount.Parse` (lub `TryParse`) z parametrami połączenia, aby uzyskać obiekt `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="16bef-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="16bef-120">Wywołanie metody `CreateCloudBlobClient` względem obiektu `CloudStorageAccount`, aby uzyskać obiekt `CloudBlobClient`.</span><span class="sxs-lookup"><span data-stu-id="16bef-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="16bef-121">Wywołanie metody `GetContainerReference` względem obiektu `CloudBlobClient`, aby uzyskać obiekt `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="16bef-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="16bef-122">Użycie metod w kontenerze, aby uzyskać listę obiektów blob i/lub odwołania do pojedynczych obiektów blob w celu przekazywania i pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="16bef-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="16bef-123">W kodzie kroki 1&ndash;3 wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="16bef-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="16bef-124">Żaden fragment tego kodu inicjowania nie wykonuje wywołań za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="16bef-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="16bef-125">To oznacza, że wyjątki spowodowane nieprawidłowymi informacjami zostaną zgłoszone dopiero później. Na przykład wywołanie metody `GetContainerReference` zakończy się powodzeniem niezależnie od tego, czy kontener rzeczywiście istnieje w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="16bef-125">This means exceptions that occur from incorrect information won't be thrown until later; for example, the call to `GetContainerReference` will succeed whether or not the container actually exists in the account.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="16bef-126">Tworzenie kontenerów podczas uruchamiania</span><span class="sxs-lookup"><span data-stu-id="16bef-126">Create containers at startup</span></span>

<span data-ttu-id="16bef-127">Powszechną praktyką jest tworzenie przez aplikacje wymaganych kontenerów w kodzie nawet wtedy, gdy z góry wiemy, jakie będą to kontenery.</span><span class="sxs-lookup"><span data-stu-id="16bef-127">Common practice is for applications to create needed containers in code, even when we know what those containers will be up-front.</span></span> <span data-ttu-id="16bef-128">Wywoływanie metody `CreateIfNotExistsAsync` względem obiektu `CloudBlobContainer` to najlepszy sposób, aby to zrobić, i powinniśmy tak utworzyć każdy kontener, którego będziemy potrzebować, przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="16bef-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to do this, and we should use it to create each container we know we'll need before we use them.</span></span>

<span data-ttu-id="16bef-129">Metoda `CreateIfNotExistsAsync` *wykonuje* wywołanie sieciowe do usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="16bef-129">`CreateIfNotExistsAsync` *does* make a network call to Azure Storage.</span></span> <span data-ttu-id="16bef-130">Najlepszym rozwiązaniem jest wywołanie jej raz podczas uruchamiania, a nie za każdym razem, gdy uzyskujemy dostęp do kontenera.</span><span class="sxs-lookup"><span data-stu-id="16bef-130">Best practice is to call it once at startup and not every time we access a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="16bef-131">Ćwiczenie</span><span class="sxs-lookup"><span data-stu-id="16bef-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="16bef-132">Klonowanie i eksplorowanie niedokończonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="16bef-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="16bef-133">Najpierw sklonujmy aplikację startową z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="16bef-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="16bef-134">W terminalu usługi Cloud Shell uruchom następujące polecenie, aby pobrać kopię kodu źródłowego i otworzyć go w edytorze:</span><span class="sxs-lookup"><span data-stu-id="16bef-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone TODO
cd TODO
code .
```

<span data-ttu-id="16bef-135">Otwórz plik `Controllers/FilesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="16bef-135">Open the file `Controllers/FilesController.cs`.</span></span>

<span data-ttu-id="16bef-136">Ten kontroler implementuje interfejs API z trzema akcjami:</span><span class="sxs-lookup"><span data-stu-id="16bef-136">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="16bef-137">**Index** (GET /api/Files) zwraca listę adresów URL, po jednym dla każdego przekazanego pliku.</span><span class="sxs-lookup"><span data-stu-id="16bef-137">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="16bef-138">Fronton aplikacji wywołuje tę metodę w celu utworzenia listy hiperlinków do przekazanych plików.</span><span class="sxs-lookup"><span data-stu-id="16bef-138">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="16bef-139">**Upload** (POST /api/Files) odbiera przekazany plik i zapisuje go.</span><span class="sxs-lookup"><span data-stu-id="16bef-139">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="16bef-140">**Download** (GET /api/Files/{nazwa-pliku}) pobiera pojedynczy plik według jego nazwy.</span><span class="sxs-lookup"><span data-stu-id="16bef-140">**Download** (GET /api/Files/{file-name}) downloads an individual file by its name.</span></span>

<span data-ttu-id="16bef-141">Każda metoda używa wystąpienia interfejsu `IStorage` o nazwie `storage` do wykonania swojej pracy.</span><span class="sxs-lookup"><span data-stu-id="16bef-141">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="16bef-142">W pliku `Models/BlobStorage.cs` znajduje się niekompletna implementacja interfejsu `IStorage`.</span><span class="sxs-lookup"><span data-stu-id="16bef-142">There is an incomplete implementation of `IStorage` in  `Models/BlobStorage.cs`.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="16bef-143">Dodawanie pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="16bef-143">Add the NuGet package</span></span>

<span data-ttu-id="16bef-144">Najpierw dodaj odwołanie do zestawu SDK usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="16bef-144">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="16bef-145">W terminalu uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="16bef-145">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="16bef-146">Dzięki temu będziemy mieć pewność, że używamy najnowszej wersji biblioteki klienta usługi Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="16bef-146">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="16bef-147">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="16bef-147">Configure</span></span>

<span data-ttu-id="16bef-148">Nasza aplikacja startowa już zawiera szkielet potrzebnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16bef-148">Our starter app already includes the configuration plumbing we need.</span></span> <span data-ttu-id="16bef-149">Parametr konstruktora `IOptions<AzureStorageConfig>` w klasie `BlobStorage` ma dwie właściwości: parametry połączenia konta magazynu i nazwę kontenera, w którym nasza aplikacja będzie zapisywać obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="16bef-149">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="16bef-150">W metodzie `ConfigureServices` w pliku `Startup.cs` znajduje się kod, który ładuje wartości z konfiguracji podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16bef-150">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

<span data-ttu-id="16bef-151">W tym ćwiczeniu uruchomimy aplikację w usłudze Azure App Service, więc później dodamy wartości konfiguracji do ustawień aplikacji usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="16bef-151">In this exercise, we will run the app in Azure App Service, so we will add the configuration values to the App Service application settings later.</span></span> <span data-ttu-id="16bef-152">Na razie nie musimy wykonywać żadnej pracy związanej z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="16bef-152">For now, we don't need to do any work related to configuration.</span></span>

### <a name="initialize"></a><span data-ttu-id="16bef-153">Inicjowanie</span><span class="sxs-lookup"><span data-stu-id="16bef-153">Initialize</span></span>

<span data-ttu-id="16bef-154">Otwórz plik `BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="16bef-154">Open `BlobStorage.cs`.</span></span>

<span data-ttu-id="16bef-155">Znajdź metodę `Initialize`.</span><span class="sxs-lookup"><span data-stu-id="16bef-155">Location the `Initialize` method.</span></span> <span data-ttu-id="16bef-156">Nasza aplikacja wywoła tę metodę przy pierwszym użyciu.</span><span class="sxs-lookup"><span data-stu-id="16bef-156">Our app will call this method when it's first used.</span></span> <span data-ttu-id="16bef-157">Jeśli Cię to ciekawi, możesz przyjrzeć się metodzie `ConfigureServices` w pliku `Startup.cs`, aby zobaczyć, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="16bef-157">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span> 

<span data-ttu-id="16bef-158">W metodzie `Initialize` najlepiej utworzyć kontener, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="16bef-158">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="16bef-159">Wypełnij metodę `Initialize` następującym kodem, a następnie zapisz swoją pracę:</span><span class="sxs-lookup"><span data-stu-id="16bef-159">Fill in `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```