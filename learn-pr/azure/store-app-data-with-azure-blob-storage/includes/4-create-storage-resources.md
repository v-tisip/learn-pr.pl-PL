Gdy już wiemy, jak będą przechowywane dane na kontach magazynu, w kontenerach i obiektach blob, możemy zastanowić się, jakie zasoby platformy Azure trzeba utworzyć, aby zapewnić obsługę aplikacji.

### <a name="storage-accounts"></a>Konta magazynu

Tworzenie konta magazynu jest działaniem administracyjnym/zarządzania, które ma miejsce przed wdrożeniem i uruchomieniem aplikacji. Konta są zwykle tworzone przez skrypt konfigurowania wdrożenia lub środowiska, szablon usługi Azure Resource Manager lub ręcznie przez administratora. Aplikacje inne niż narzędzia administracyjne zwykle nie mają uprawnień do tworzenia kont magazynu.

### <a name="containers"></a>Containers

W odróżnieniu od tworzenia konta magazynu, tworzenie kontenera jest prostym działaniem, które można wykonywać z poziomu aplikacji. Nie jest niczym niezwykłym tworzenie i usuwanie kontenerów w ramach zadań wykonywanych przez aplikację.

W przypadku aplikacji bazujących na znanym zbiorze kontenerów z zapisanymi na stałe lub wstępnie skonfigurowanymi nazwami typową praktyką jest umożliwianie aplikacji utworzenia potrzebnych kontenerów, o ile jeszcze nie istnieją, po uruchomieniu lub przy pierwszym użyciu. Zezwolenie aplikacji na utworzenie kontenerów zamiast zrobienia tego podczas wdrażania aplikacji eliminuje konieczność znajomości nazw kontenerów używanych przez aplikację jednocześnie w aplikacji i procesie wdrażania.

## <a name="exercise"></a>Ćwiczenie

Dokończymy niegotową aplikację platformy ASP.NET Core, dodając kod odpowiedzialny za korzystanie z usługi Azure Blob Storage. To ćwiczenie bardziej koncentruje się na poznawaniu interfejsu API usługi Blob Storage niż projektowaniu organizacji i schematu nazewnictwa, ale poniżej przedstawiono krótki przegląd aplikacji i sposobu przechowywania przez nią danych:

**TODO zrzut ekranu aplikacji, ponieważ aż do zakończenia nie będzie on widoczny**

Nasza aplikacja działa jak folder udostępniony, który akceptuje przekazywane pliki i udostępnia je do pobrania. Nie używa bazy danych do organizowania obiektów blob &mdash; zamiast tego oczyszcza nazwy przekazanych plików i używa ich bezpośrednio jako nazw obiektów blob. Wszystkie przekazane pliki są przechowywane w jednym kontenerze.

Kod, od którego zaczniemy, kompiluje się i uruchamia, ale części odpowiedzialne za przechowywanie i ładowanie danych są puste. Gdy uzupełnimy kod, wdrożymy aplikację w usłudze Azure App Service i ją przetestujemy.

Skonfigurujmy infrastrukturę magazynu dla naszej aplikacji.

### <a name="resource-group-and-storage-account"></a>Grupa zasobów i konto magazynu
Najpierw utworzymy grupę zasobów dla wszystkich zasobów w tym ćwiczeniu. Usuniemy ją na końcu, aby wyczyścić wszystko, co utworzymy. Utworzymy też konto magazynu, na którym aplikacja będzie przechowywać obiekty blob.

Użyj terminala usługi Azure Cloud Shell, aby utworzyć grupę zasobów i konto magazynu, uruchamiając następujące polecenia interfejsu wiersza polecenia platformy Azure. Musisz podać unikatową nazwę konta magazynu &mdash; zanotuj ją do późniejszego użycia. Wybór regionu `eastus` dla lokalizacji jest arbitralny.

```console
az group create --name blob-exercise-group --location eastus
az storage account create --name <your-unique-storage-account-name> --resource-group blob-exercise-group --location eastus --kind StorageV2
```

**TODO poniżej powinien się znaleźć moduł usługi Azure Storage**

> [!NOTE]
> Dlaczego `--kind StorageV2`? Istnieje kilka różnych rodzajów kont magazynu. W większości scenariuszy powinno się używać kont magazynu ogólnego przeznaczenia w wersji 2 (oznaczonych jako `StorageV2`). Jedyną przyczyną, dla której konta magazynu w wersji 2 muszą być określone w tym miejscu, jest to, że nadal są dość nowe i nie zostały jeszcze ustawione jako domyślne w witrynie Azure Portal i interfejsie wiersza polecenia platformy Azure.

### <a name="container"></a>Kontener
Aplikacja, nad którą będziemy pracować w tym module, używa jednego kontenera. Zamierzamy zastosować najlepsze rozwiązanie polegające na umożliwieniu aplikacji utworzenia kontenera przy uruchamianiu. Kontener można też jednak utworzyć z poziomu interfejsu wiersza polecenia platformy Azure: uruchom polecenie `az storage container create -h` w terminalu usługi Cloud Shell, jeśli chcesz zobaczyć dokumentację.