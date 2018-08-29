Projektując aplikację, która wymaga przechowywania danych, należy zastanowić się, jak aplikacja będzie organizować i przechowywać dane na kontach magazynu, w kontenerach i w obiektach blob.

## <a name="storage-accounts"></a>Konta magazynu

Pojedyncze konto magazynu jest na tyle elastyczne, że umożliwia organizowanie obiektów blob w dowolny sposób, należy jednak korzystać z dodatkowych kont magazynu zgodnie z potrzebami, aby logicznie rozdzielić koszty i kontrolować dostęp do danych.

## <a name="containers-and-blobs"></a>Kontenery i obiekty blob

Podczas nazywania i organizowania kontenerów i obiektów blob należy kierować się rodzajem aplikacji i przechowywanymi przez nią danymi.

W aplikacjach używających obiektów blob w ramach schematu magazynu, który zawiera bazę danych, często nie trzeba posługiwać się organizacją, nazewnictwem czy metadanymi, aby wskazać, z jakiego rodzaju danymi mamy do czynienia. W takich aplikacjach nazwami obiektów blob często są identyfikatory (np. GUID), do których aplikacja odwołuje się w rekordach bazy danych. Aplikacja będzie określać, gdzie są przechowywane obiekty blob i jakiego rodzaju dane one zawierają, przy użyciu bazy danych.

Inne aplikacje mogą używać usługi Azure Blob Storage jako osobistego systemu plików, w którym nazwy kontenerów i obiektów blob wskazują znaczenie i strukturę. Nazwy obiektów blob w takich aplikacjach często wyglądają jak tradycyjne nazwy plików i zawierają rozszerzenia nazw plików, takie jak `.jpg`, aby wskazać, jakiego rodzaju dane zawierają. Do organizowania obiektów blob są w nich używane katalogi wirtualne (patrz poniżej), a informacje o obiektach blob i kontenerach często są przechowywane za pomocą metadanych.

Podejmując decyzję dotyczącą sposobu organizacji i przechowywania obiektów blob i kontenerów, warto rozważyć kilka kwestii.

### <a name="naming-limitations"></a>Ograniczenia nazewnictwa

Nazwy kontenerów i obiektów blob muszą być zgodne z zestawem reguł, które ograniczają długość nazwy i określają dozwolone znaki. Sekcja Dodatkowe zasoby na końcu tego modułu zawiera bardziej szczegółowe informacje na temat reguł nazewnictwa.

### <a name="public-access-and-containers-as-security-boundaries"></a>Dostęp publiczny i kontenery jako granice zabezpieczeń

Domyślnie, aby uzyskać dostęp do jakiegokolwiek obiektu blob, wymagane jest uwierzytelnienie. Jednak poszczególne kontenery można skonfigurować tak, aby zezwolić na publiczne pobieranie ich obiektów blob bez uwierzytelniania. Ta funkcja obsługuje wiele zastosowań, takich jak udostępnianie plików czy hostowanie zasobów statycznej witryny internetowej. Jest to spowodowane tym, że pobieranie zawartości obiektów blob działa tak samo, jak odczytywanie każdego innego typu danych w Internecie: wystarczy wskazać w przeglądarce lub w innym narzędziu, które potrafi zgłaszać żądania GET, adres URL obiektu blob.

**Obrazu publicznego kontenera TODO, przedstawiający adres URL dostępu bezpośredniego**

Włączenie dostępu publicznego jest ważne w przypadku skalowalności, ponieważ dane pobierane bezpośrednio z magazynu obiektów blob nie generują żadnego ruchu w aplikacji po stronie serwera. Nawet jeśli nie od razu chcesz korzystać z dostępu publicznego lub jeśli będziesz używać bazy danych, aby kontrolować dostęp do danych za pośrednictwem aplikacji, zaplanuj oddzielne kontenery dla danych, które mają być dostępne publicznie.

> [!CAUTION]
> Obiekty blob znajdujące się w kontenerze skonfigurowanym na potrzeby dostępu publicznego można pobierać bez żadnego uwierzytelniania czy inspekcji, znając jedynie ich adres URL przechowywania. Nigdy nie umieszczaj w kontenerze publicznym danych obiektów blob, których nie chcesz udostępniać publicznie.

Oprócz dostępu publicznego platforma Azure oferuje funkcję sygnatury dostępu współdzielonego, która umożliwia szczegółową kontrolę uprawnień do kontenerów. Precyzyjna kontrola dostępu umożliwia scenariusze, które dodatkowo poprawiają skalowalność, więc traktowanie kontenerów jako granic zabezpieczeń jest ogólnie rzecz biorąc pomocną wskazówką.

### <a name="blob-name-prefixes-virtual-directories"></a>Prefiksy nazw obiektów blob (katalogi wirtualne)

Technicznie rzecz biorąc, kontenery są „płaskie” i nie obsługują żadnego rodzaju zagnieżdżania ani hierarchii. Jeśli jednak nadasz obiektom blob nazwy hierarchiczne, które wyglądają jak ścieżki do plików (na przykład `finance/budgets/2017/q1.xls`), operacja tworzenia listy interfejsu API może filtrować wyniki pod kątem określonych prefiksów. Umożliwia to nawigowanie po liście w taki sposób, jakby była hierarchicznym systemem plików i folderów.

Ta funkcja jest często określana mianem *katalogów wirtualnych*, ponieważ niektóre narzędzia i biblioteki klienckie używają jej, aby wizualizować magazyn obiektów blob i umożliwiać nawigowanie po nim, jakby był on systemem plików. Każda nawigacja po folderach wyzwala oddzielne wywołanie w celu wyświetlenia listy obiektów blob w tym folderze.

**Obraz TODO eksploratora magazynu i/lub portalu z folderami**

Używanie dla obiektów blob nazw, które wyglądają jak nazwy plików, jest często stosowaną techniką organizowania złożonych danych obiektów blob i nawigowania po nich.

### <a name="blob-types"></a>Typy obiektów blob

Istnieją trzy różne rodzaje obiektów blob, w których można przechowywać dane:

- **Blokowe obiekty blob** składają się z bloków o różnych rozmiarach, które można przekazywać i pobierać niezależnie oraz równolegle. Zapisywanie do blokowego obiektu blob obejmuje przekazywanie danych do bloków i zatwierdzanie ich w obiektach blob &mdash; biblioteki klienckie zajmą się tym za Ciebie.
- **Obiekty blob dołączania** to wyspecjalizowane blokowe obiekty blob, które obsługują tylko dołączanie nowych danych (a nie aktualizowanie i usuwanie istniejących danych), są one w tym jednak bardzo wydajne. Obiekty blob dołączania idealnie sprawdzają się w scenariuszach przechowywania dzienników i strumieniowego przesyłania danych.
- **Stronicowe obiekty blob** są przeznaczone dla scenariuszy obejmujących odczyty i zapisy dostępu losowego. Stronicowe obiekty blob są stosowane do przechowywania plików wirtualnego dysku twardego (VHD), które są używane przez usługę Azure Virtual Machines, ale doskonale nadają się one do wszelkich scenariuszy z dostępem losowym.

Blokowe obiekty blob są najlepszym rozwiązaniem dla większości scenariuszy, które nie wymagają zastosowania obiektów blob dołączania ani obiektów stronicowych.