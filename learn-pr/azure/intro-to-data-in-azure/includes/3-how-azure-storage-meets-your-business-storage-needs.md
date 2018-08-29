Gdy uwzględni się korzyści płynące z używania usługi Azure Storage, to widać, że oferuje ona najlepsze opcje przechowywania portalu szkoleniowego. Przyjrzyjmy się bliżej tym korzyściom i opcjom, aby dowiedzieć się, w jaki sposób można dopasować usługę Azure Storage do potrzeb biznesowych.

## <a name="how-azure-storage-can-meet-your-business-storage-needs"></a>W jaki sposób usługa Azure Storage może spełnić potrzeby Twojej firmy w zakresie magazynu

Usługa Azure Storage udostępnia kilka opcji dostosowanych do różnych wymagań w zakresie przechowywania danych.

### <a name="azure-sql-database"></a>Azure SQL Database

Usługa **Azure SQL Database** to niezawodna, w pełni zarządzana relacyjna baza danych w chmurze, umożliwiająca przechowywanie wszystkich danych. Można jej używać do przechowywania często używanych i aktualizowanych danych, takich jak informacje osobiste i dane szkoleniowe personelu. Można również migrować istniejące bazy danych programu SQL Server bez konieczności zmieniania aplikacji.

![Azure SQL](../images/Azure_SQL.png)

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

Usługa Azure Cosmos DB to wielokrotnie nagradzana funkcja platformy Azure, która jest globalnie rozproszoną bazą danych. Obsługuje ona dane niezależne od schematów, co umożliwia tworzenie szybko reagujących i *zawsze włączonych* aplikacji, które współdziałają ze stale zmieniającymi się danymi. Funkcji tej można używać do przechowywania danych, które są aktualizowane i obsługiwane na podstawie informacji wprowadzanych przez użytkowników na całym świecie.

![CosmosDB](../images/Azure_cosmos_db.png)

### <a name="azure-blob-storage"></a>Azure Blob Storage

Usługa Azure Blob Storage umożliwia przesyłanie strumieniowe dużych plików wideo lub audio bezpośrednio do przeglądarki użytkownika w dowolnym miejscu na świecie. Usługa Blob Storage jest używana również do zapisywania danych w celu tworzenia kopii zapasowych, przywracania, odzyskiwania po awarii i archiwizowania. Usługa Azure Blob Storage może przechowywać do 8 TB danych, np. plików maszyn wirtualnych.

![AzureBlob](../images/Azure_blob.png)

### <a name="azure-data-lake-storage-gen2"></a>Usługa Azure Data Lake Storage 2. generacji

Funkcja Data Lake usługi Azure Storage pozwala przeprowadzać analizy użycia danych i przygotowywać odpowiednie raporty. Data Lake to duże repozytorium, które może przechowywać zarówno dane ze strukturą, jak i dane nieustrukturyzowane.

Usługa **Azure Data Lake Storage Gen2** łączy w sobie skalowalność i zalety ekonomiczne związane z magazynowaniem obiektów z niezawodnością i wydajnością systemu plików Big Data.

![Data_lake_Store_concept](../images/Data_lake_store_concept.png)

### <a name="azure-files"></a>Azure Files

Usługa Azure Files udostępnia w pełni zarządzane udziały plików w chmurze. Aplikacje uruchomione na platformie Azure mogą łatwo współdzielić pliki z różnych maszyn wirtualnych. Udziałów plików platformy Azure można używać jednocześnie w chmurowych i lokalnych wdrożeniach systemów Windows, Linux i macOS.

![Azure_Files](../images/Azure_Files.png)

### <a name="azure-queue"></a>Azure Queue

Azure Queue Storage to usługa do przechowywania dużej liczby komunikatów, do których można uzyskać dostęp w dowolnym miejscu na świecie. Pojedynczy komunikat w kolejce może mieć rozmiar do 64 kB, a kolejka może zawierać miliony komunikatów.

Główne zastosowania kolejki:

- Tworzenie listy prac i przekazywanie komunikatów między różnymi serwerami internetowymi na platformie Azure.
- Równoważenie obciążenia różnych serwerów internetowych lub infrastruktury i zarządzanie wzrostem ruchu.
- Wzmacnianie odporności na awarie składników w sytuacjach, gdy z danych korzysta jednocześnie wielu użytkowników.

![Azure_Queue](../images/Azure_Queue.png)

### <a name="azure-standard-storage"></a>Azure Standard Storage

Maszyny wirtualne na platformie Azure przechowują systemy operacyjne, aplikacje i dane na dyskach. Usługa Azure Standard Storage zapewnia niezawodną i niedrogą obsługę dysków dla maszyn wirtualnych służących do uruchamiania obciążeń o niekluczowym znaczeniu. Dane usługi Standard Storage są przechowywane na dyskach twardych (HDD).

Korzystając z maszyn wirtualnych, można używać dysków SSD i HDD w warstwie Standardowa do obsługi obciążeń o niekluczowym znaczeniu. W przypadku krytycznych aplikacji produkcyjnych zalecane jest używanie dysków SSD w warstwie Premium. Dyski platformy Azure już długo zapewniają niezawodność klasy korporacyjnej z rocznym współczynnikiem awarii w wysokości 0%, który stawia tę usługę w czołówce branży.

![Azure_disk](../images/Azure_disks.png)

### <a name="storage-tiers"></a>Warstwy magazynowania

Usługa Azure Storage udostępnia trzy warstwy do magazynowania obiektów blob:

1. **Warstwa magazynowania Gorąca** — zoptymalizowana pod kątem przechowywania danych, do których często uzyskuje się dostęp. 
1. **Warstwa magazynowania Chłodna** — zoptymalizowana pod kątem magazynowania danych używanych od czasu do czasu, które są przechowywane co najmniej przez 30 dni.
1. **Warstwa magazynowania Archiwum** — zoptymalizowana pod kątem magazynowania rzadko używanych danych, przechowywanych co najmniej przez 180 dni, co do których obowiązują elastyczne wymagania dotyczące opóźnień. Warstwa Archiwum platformy Azure to idealne rozwiązanie do przechowywania starszych danych. Pozwala ono na pobieranie danych zgodnie z wymaganiami inspekcji lub innych nieregularnie wykonywanych czynności.

![Archive_Tier](../images/Archive_Storage_Tier.png)

### <a name="azure-storage-encryptionreplication"></a>Szyfrowanie/replikacja w usłudze Azure Storage

Usługa Azure Storage zapewnia bezpieczeństwo i wysoką dostępność danych dzięki funkcjom szyfrowania i replikacji.

#### <a name="encryption-for-storage-services"></a>Szyfrowanie usług magazynu

Dostępne są następujące typy szyfrowania zasobów:

1. **Szyfrowanie w spoczynku w usłudze Azure Storage** pomaga chronić dane zgodnie z wymaganiami organizacji w zakresie zabezpieczeń i zgodności z przepisami. Dane są szyfrowane przed zapisaniem i odszyfrowywane przed pobraniem. Procesy te są niewidoczne dla użytkownika.
1. W przypadku **szyfrowania po stronie klienta** dane zostały wcześniej zaszyfrowane za pomocą bibliotek klienckich. Nieużywane dane pozostają zaszyfrowane, a podczas ich pobierania następuje odszyfrowanie.

    Funkcja szyfrowania gwarantuje spełnienie globalnych standardów ochrony danych. Rozwiązanie to nadaje się do przechowywanie poufnych informacji, takich jak dane osobiste i finansowe.

#### <a name="replication-for-storage-availability"></a>Replikacja zapewniająca dostępność magazynu

Typ replikacji jest ustawiany podczas tworzenia konta magazynu. Funkcja replikacji gwarantuje trwałość i stałą dostępność danych. Regionalne i geograficzne replikacje w usłudze Azure Storage zapewniają ochronę danych w przypadku klęsk żywiołowych oraz innych zdarzeń, takich jak pożar lub powódź.
