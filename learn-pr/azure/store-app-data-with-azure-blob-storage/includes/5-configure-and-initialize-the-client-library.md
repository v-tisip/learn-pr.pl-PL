Poniżej przedstawiono typowy przepływ pracy aplikacji, które używają usługi Azure Blob Storage:

1. **Pobieranie konfiguracji**: podczas uruchamiania załaduj konfigurację, np. parametry połączenia z kluczem konta. Jest to niezbędne do uwierzytelniania wywołań interfejsu API.
1. **Inicjowanie klienta**: zainicjuj bibliotekę klienta usługi Azure Storage za pomocą parametrów połączenia. Spowoduje to utworzenie obiektów, których aplikacja będzie używać do pracy z interfejsem API usługi Blob Storage.
1. **Używanie**: wykonuj wywołania interfejsu API za pomocą biblioteki klienta, aby wykonywać operacje względem kontenerów i obiektów blob.

## <a name="configure-your-connection-string"></a>Konfigurowanie parametrów połączenia

Przed napisaniem jakiegokolwiek kodu będą potrzebne parametry połączenia dla konta magazynu, które będzie używane. 

Parametry połączenia zawierają klucz konta. Klucz konta jest uznawany za wpis tajny i powinien być przechowywany w bezpieczny sposób. Parametry połączenia będą przechowywane w ustawieniu aplikacji usługi App Service. Ustawienie aplikacji to bezpieczne miejsce dla wpisów tajnych aplikacji, ale nie obsługuje ono opracowywania lokalnego i nie stanowi samodzielnie niezawodnego, kompleksowego rozwiązania.

> [!WARNING]
> **Nie umieszczaj kluczy kont magazynu w kodzie ani w niechronionych plikach konfiguracyjnych.** Klucze konta magazynu umożliwiają uzyskanie pełnego dostępu do konta magazynu. Wyciek klucza może spowodować nieodwracalne szkody i duże rachunki. Sekcja Dodatkowe zasoby na końcu tego modułu zawiera wskazówki dotyczące magazynu oraz porady na temat naprawiania szkód spowodowanych wyciekiem klucza.

## <a name="initialize-the-blob-storage-object-model"></a>Inicjowanie modelu obiektu usługi Blob Storage

W zestawie SDK usługi Azure Storage dla platformy .NET Core standardowy wzorzec korzystania z usługi Blob Storage składa się z następujących czynności:

1. Wywołanie metody `CloudStorageAccount.Parse` (lub `TryParse`) z parametrami połączenia, aby uzyskać obiekt `CloudStorageAccount`.
1. Wywołanie metody `CreateCloudBlobClient` względem obiektu `CloudStorageAccount`, aby uzyskać obiekt `CloudBlobClient`.
1. Wywołanie metody `GetContainerReference` względem obiektu `CloudBlobClient`, aby uzyskać obiekt `CloudBlobContainer`.
1. Użycie metod w kontenerze, aby uzyskać listę obiektów blob i/lub odwołania do pojedynczych obiektów blob w celu przekazywania i pobierania danych.

W kodzie kroki 1&ndash;3 wyglądają następująco:

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

Żaden fragment tego kodu inicjowania nie wykonuje wywołań za pośrednictwem sieci. To oznacza, że wyjątki spowodowane nieprawidłowymi informacjami zostaną zgłoszone dopiero później. Na przykład wywołanie metody `GetContainerReference` zakończy się powodzeniem niezależnie od tego, czy kontener rzeczywiście istnieje w ramach konta.

## <a name="create-containers-at-startup"></a>Tworzenie kontenerów podczas uruchamiania

Powszechną praktyką jest tworzenie przez aplikacje wymaganych kontenerów w kodzie nawet wtedy, gdy z góry wiemy, jakie będą to kontenery. Wywoływanie metody `CreateIfNotExistsAsync` względem obiektu `CloudBlobContainer` to najlepszy sposób, aby to zrobić, i powinniśmy tak utworzyć każdy kontener, którego będziemy potrzebować, przed jego użyciem.

Metoda `CreateIfNotExistsAsync` *wykonuje* wywołanie sieciowe do usługi Azure Storage. Najlepszym rozwiązaniem jest wywołanie jej raz podczas uruchamiania, a nie za każdym razem, gdy uzyskujemy dostęp do kontenera.

## <a name="exercise"></a>Ćwiczenie

### <a name="clone-and-explore-the-unfinished-app"></a>Klonowanie i eksplorowanie niedokończonej aplikacji

Najpierw sklonujmy aplikację startową z usługi GitHub. W terminalu usługi Cloud Shell uruchom następujące polecenie, aby pobrać kopię kodu źródłowego i otworzyć go w edytorze:

```console
git clone TODO
cd TODO
code .
```

Otwórz plik `Controllers/FilesController.cs`.

Ten kontroler implementuje interfejs API z trzema akcjami:

* **Index** (GET /api/Files) zwraca listę adresów URL, po jednym dla każdego przekazanego pliku. Fronton aplikacji wywołuje tę metodę w celu utworzenia listy hiperlinków do przekazanych plików.
* **Upload** (POST /api/Files) odbiera przekazany plik i zapisuje go.
* **Download** (GET /api/Files/{nazwa-pliku}) pobiera pojedynczy plik według jego nazwy.

Każda metoda używa wystąpienia interfejsu `IStorage` o nazwie `storage` do wykonania swojej pracy. W pliku `Models/BlobStorage.cs` znajduje się niekompletna implementacja interfejsu `IStorage`.

### <a name="add-the-nuget-package"></a>Dodawanie pakietu NuGet

Najpierw dodaj odwołanie do zestawu SDK usługi Azure Storage. W terminalu uruchom następujące polecenie:

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

Dzięki temu będziemy mieć pewność, że używamy najnowszej wersji biblioteki klienta usługi Blob Storage.

### <a name="configure"></a>Konfigurowanie

Nasza aplikacja startowa już zawiera szkielet potrzebnej konfiguracji. Parametr konstruktora `IOptions<AzureStorageConfig>` w klasie `BlobStorage` ma dwie właściwości: parametry połączenia konta magazynu i nazwę kontenera, w którym nasza aplikacja będzie zapisywać obiekty blob. W metodzie `ConfigureServices` w pliku `Startup.cs` znajduje się kod, który ładuje wartości z konfiguracji podczas uruchamiania aplikacji.

W tym ćwiczeniu uruchomimy aplikację w usłudze Azure App Service, więc później dodamy wartości konfiguracji do ustawień aplikacji usługi App Service. Na razie nie musimy wykonywać żadnej pracy związanej z konfiguracją.

### <a name="initialize"></a>Inicjowanie

Otwórz plik `BlobStorage.cs`.

Znajdź metodę `Initialize`. Nasza aplikacja wywoła tę metodę przy pierwszym użyciu. Jeśli Cię to ciekawi, możesz przyjrzeć się metodzie `ConfigureServices` w pliku `Startup.cs`, aby zobaczyć, jak to zrobić. 

W metodzie `Initialize` najlepiej utworzyć kontener, jeśli jeszcze nie istnieje. Wypełnij metodę `Initialize` następującym kodem, a następnie zapisz swoją pracę:

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```