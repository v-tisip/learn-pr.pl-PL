Gdy będziemy mieć odwołanie do obiektu blob, możemy przekazywać i pobierać dane. Obiekty `ICloudBlob` mają metody `Upload` i `Download`, które obsługują tablice bajtów, strumienie i pliki jako elementy źródłowe i docelowe. Określone typy mają dla wygody dodatkowe metody &mdash; na przykład klasa `CloudBlockBlob` obsługuje przekazywanie i pobieranie ciągów za pomocą metod `UploadTextAsync` i `DownloadTextAsync`.

## <a name="creating-new-blobs"></a>Tworzenie nowych obiektów blob

Aby utworzyć nowy obiekt blob, wywołaj jedną z metod `Upload` względem obiektu blob, który nie istnieje. Powoduje to wykonanie dwóch działań: utworzenie obiektu blob i przekazanie danych. 

## <a name="moving-data-to-and-from-blobs"></a>Przenoszenie danych do i z obiektów blob

Przenoszenie danych do i z obiektu blob to operacja sieciowa, która zajmuje trochę czasu. W zestawie SDK usługi Azure Storage dla platformy .NET Core wszystkie metody, które wymagają działań sieciowych, zwracają obiekty `Task`, dlatego upewnij się, że Twoje metody kontrolera mają typ `async` zgodnie z potrzebami oraz że względem ich wywołań zastosowano operator `await`, a nie metodę `Wait`.

Powszechnym zaleceniem podczas pracy z dużymi obiektami danych jest użycie strumieni zamiast struktur w pamięci, takich jak tablice bajtów lub ciągi. W ten sposób można uniknąć buforowania całej zawartości w pamięci przed wysłaniem jej do obiektu docelowego. Platforma ASP.NET Core obsługuje odczytywanie strumieni z żądań i odpowiedzi oraz zapisywanie ich w nich.

## <a name="concurrent-access"></a>Równoczesny dostęp

Inne procesy mogą dodawać, zmieniać lub usuwać obiekty blob, gdy Twoja aplikacja z nich korzysta. Zawsze pisz kod ostrożnie i myśl o problemach powodowanych przez współbieżność, np. usunięcie obiektu blob, gdy próbujesz pobrać z niego dane, lub zmiana w obiekcie blob, gdy nie jest to oczekiwane. Sekcja Dodatkowe zasoby na końcu tego modułu zawiera informacje o używaniu warunków AccessCondition i dzierżaw obiektów blob do zarządzania równoczesnym dostępem do obiektu blob.

## <a name="exercise"></a>Ćwiczenie

Dokończmy naszą aplikację, dodając kod do obsługi przekazywania i pobierania, a następnie wdróżmy ją w usłudze Azure App Service, aby ją przetestować.

### <a name="upload"></a>Upload

Aby przekazać obiekt blob zaimplementujemy metodę `BlobStorage.Save` przy użyciu metody `GetBlockBlobReference`, aby uzyskać obiekt `CloudBlockBlob` z kontenera. Metoda `FilesController.Upload` przekazuje strumień plików do metody `Save`, dzięki czemu możemy użyć metody `UploadFromStreamAsync`, aby maksymalnie wydajnie wykonać przekazywanie.

Otwórz plik `BlobStorage.cs` w edytorze i wypełnij implementację metody `Save` następującym kodem:

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
> Kod przekazywania w oparciu o strumień jest bardziej wydajny niż wczytywanie pliku do tablicy bajtów przed wysłaniem go do usługi Azure Blob Storage. Jednak technika oparta na interfejsie `IFormFile`, której używamy do pobrania pliku z klienta, nie jest faktyczną kompleksową implementacją przesyłania strumieniowego i jest odpowiednia tylko do obsługi przekazywania małych plików. Sekcja Dodatkowe zasoby na końcu tego modułu zawiera informacje o całkowicie strumieniowym przekazywaniu plików.

### <a name="download"></a>Do pobrania

Metoda `BlobStorage.Load` zwraca obiekt `Stream`, co oznacza, że nasz kod nie musi w ogóle fizycznie przenosić bajtów z usługi Blob Storage &mdash; musimy tylko zwrócić odwołanie do strumienia obiektu blob. Możemy to zrobić za pomocą metody `OpenReadAsync`. Platforma ASP.NET Core obsłuży odczytywanie i zamykanie strumienia podczas tworzenia odpowiedzi klienta.

Wypełnij metodę `Load` przy użyciu następującego kodu:

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a>Wdrażanie i uruchamianie na platformie Azure

Nasza aplikacja jest gotowa &mdash; wdróżmy ją i zobaczmy, jak działa. Uruchom poniższy kod w terminalu usługi Azure Cloud Shell, aby skompilować nasz kod i wdrożyć go w nowym wystąpieniu usługi App Service. Dodajemy również parametry połączenia naszego konta magazynu do konfiguracji.

```console

```

Przyciski ...

Przekaż i pobierz jakieś pliki, aby przetestować aplikację, a następnie uruchom poniższe polecenie w powłoce, aby wyświetlić obiekty blob, które zostały przekazane:

```console

```

**TODO: zrzut ekranu portalu**