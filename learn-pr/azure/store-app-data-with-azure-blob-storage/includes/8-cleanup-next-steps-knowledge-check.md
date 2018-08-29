W tym module pokazano, jak używać usługi Azure Blob Storage do przechowywania danych aplikacji internetowej. Omówiliśmy wskazówki dotyczące tworzenia strategii wykorzystania usługi Blob Storage w aplikacji internetowej i sposób używania zestawu Azure Storage SDK dla platformy .NET Core do zapisywania w obiektach blob i odczytywaniu z nich. Aplikacja, którą utworzyliśmy, akceptuje pliki przekazane przez użytkowników, zapisuje je w usłudze Blob Storage i udostępnia pobrania.

## <a name="cleanup"></a>Czyszczenie

Aby wyczyścić swoją subskrypcję platformy Azure, uruchom następujące polecenie w usłudze Azure Cloud Shell w celu usunięcia grupy zasobów zawierającej wszystkie zasoby utworzone w tym module.

```console
az group delete --name blob-exercise-group
```

Aby wyczyścić magazyn usługi Cloud Shell, usuń katalog `TODO` przy użyciu polecenia `rm -rf TODO`.

## <a name="additional-resources"></a>Dodatkowe zasoby

**TODO linki między dokumentami?**

* **Bezpieczne przechowywanie kluczy konta magazynu**: najbardziej niezawodnym kompleksowym rozwiązaniem do przechowywania wartości konfiguracji wpisów tajnych jest usługa Azure Key Vault. Zobacz [tutaj](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x), aby uzyskać informacje o korzystaniu z usługi Key Vault w aplikacji ASP.NET Core. Można też bezpiecznie przechowywać parametry połączenia w ustawieniach aplikacji usługi App Service i używać [narzędzia ASP.NET Core Secret Manager](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) do obsługi środowisk deweloperskich.
* [Przekazywanie dużych plików za pomocą przesyłania strumieniowego na platformie ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
* [Współbieżność obiektów blob: element AccessConditions i dzierżawy obiektów blob](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
* [Przyznawanie ograniczonego dostępu do obiektu usługi Azure Storage za pomocą sygnatur dostępu współdzielonego](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
* [Indeksowanie usługi Blob Storage za pomocą usługi Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
* [Ograniczenia dotyczące nazw kontenerów i obiektów blob](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)