Teraz, po wprowadzeniu do dostępnych usług obliczeniowych na platformie Azure, przyjrzyjmy się każdej z nich, aby ułatwić Ci podjęcie decyzji dotyczącej tego, kiedy należy używać danej usługi.

## <a name="azure-virtual-machines"></a>Maszyny wirtualne platformy Azure

Gdy potrzebujesz pełnej kontroli nad systemem operacyjnym i środowiskiem, właściwym wyborem są maszyny wirtualne. Możesz dostosować całe oprogramowanie na maszynie wirtualnej, tak samo, jak na komputerze fizycznym. Jest to idealne rozwiązanie w przypadku uruchamiania niestandardowego oprogramowania lub niestandardowej konfiguracji hostingu.

Maszyny wirtualne sprawdzają się również doskonale podczas migracji z serwera fizycznego do chmury. Często możliwe jest utworzenie obrazu serwera fizycznego i hostowanie go na maszynie wirtualnej. Dzięki temu masz pełną swobodę wyboru systemów operacyjnych i środowisk wykonawczych aplikacji, a zatem możesz tworzyć aplikacje w niemal dowolnym języku z użyciem wybranych narzędzi.

Konieczna będzie jednak obsługa maszyny wirtualnej. Obejmuje to aktualizowanie systemu operacyjnego i działającego na maszynie oprogramowania. 

Ten wariant wymaga również wzięcia pod uwagę dodatkowych kwestii w kontekście skalowania. Można skalować maszynę wirtualną w górę, czyli dodać do niej więcej zasobów obliczeniowych i pamięci. Jeśli jednak potrzebujesz wielu wystąpień działających równolegle, może być konieczne dodanie innych usług, na przykład modułów równoważenia obciążenia.

Załóżmy, że masz witrynę internetową, w której hostowany jest sklep. W przypadku zduplikowania maszyny wirtualnej potrzebna będzie dodatkowa usługa kierująca żądania do poszczególnych wystąpień maszyny wirtualnej obsługującej tę witrynę.

Na platformie Azure są dostępne również zaawansowane usługi maszyn wirtualnych:

* Aby obsługiwać stale dostępne wystąpienia jednej aplikacji lub zestawy aplikacji na maszynach wirtualnych o podobnej konfiguracji, użyj **zestawów skalowania maszyn wirtualnych**. Ta opcja umożliwia wygenerowanie w kilka minut tysięcy identycznych maszyn wirtualnych z Twoją aplikacją, dzięki czemu użytkownicy nigdy nie będą musieli czekać. A ponieważ wcześniejsze aprowizowanie maszyn nie jest wymagane, używasz tylko takich zasobów obliczeniowych, jakich w danej chwili wymaga aplikacja.

* W niektórych sytuacjach możesz potrzebować większej mocy obliczeniowej — nawet na poziomie superkomputera. Opcja **Batch** umożliwia planowanie zadań i zarządzanie wystąpieniami obliczeniowymi w skali chmury, z możliwością skalowania do dziesiątek, setek lub tysięcy maszyn wirtualnych. Umożliwia nawet wybór maszyn wirtualnych o możliwościach superkomputerów.

## <a name="azure-containers"></a>Kontenery platformy Azure

Kontenery są doskonałym wyborem wówczas, gdy chcesz uruchomić wiele wystąpień aplikacji na jednej maszynie wirtualnej. Koordynator kontenerów umożliwia uruchamianie, zatrzymywanie i skalowanie wystąpień aplikacji stosownie do potrzeb.

Kontenery są też powszechnie używane do tworzenia rozwiązań opartych na architekturze mikrousług. Umożliwiają one podział rozwiązań na mniejsze fragmenty. Możesz na przykład podzielić witrynę internetową pomiędzy kontener hostujący usługi frontonu, kontener hostujący usługi zaplecza oraz kontener magazynu. Dzięki temu możesz podzielić aplikację na sekcje logiczne, które można obsługiwać, skalować i aktualizować niezależnie.

Załóżmy, że zaplecze witryny wyczerpało już dostępne zasoby, ale fronton i magazyn nie są przeciążone. Możesz oddzielnie skalować zaplecze, aby poprawić wydajność. Możesz też zdecydować się na zmianę usługi magazynu. Możesz nawet zastąpić kontener magazynu innym, bez wpływu na pozostałe części aplikacji.

 Jeśli Twój zespół ma doświadczenie w organizowaniu kontenerów Kubernetes, rozważ użycie opcji **Azure Kubernetes Service (AKS)**. Umożliwia ona uproszczenie i automatyzację wdrażania oraz działania kontenerów Kubernetes, a także zarządzanie nimi.

## <a name="azure-functions"></a>Funkcje platformy Azure

Funkcje platformy Azure są właściwym rozwiązaniem wówczas, gdy interesuje Cię tylko kod usługi, a nie platforma czy infrastruktura, na której działa. Są zazwyczaj używane w sytuacjach, gdy konieczne jest wykonanie pracy w reakcji na określone zdarzenie, najczęściej za pośrednictwem żądania REST, czasomierza lub komunikatu z innej usługi platformy Azure, a pracę tę można wykonać szybko, maksymalnie w ciągu kilku sekund.

Funkcje platformy Azure są skalowane automatycznie, dzięki czemu doskonale sprawdzają się przy zmiennym zapotrzebowaniu, a opłaty są naliczane tylko w przypadku wyzwolenia funkcji. Przykładem jest sytuacja, w której odbierasz komunikaty z rozwiązania IoT używanego do monitorowania floty samochodów dostawczych. Prawdopodobnie najwięcej danych będziesz otrzymywać w godzinach pracy.

Funkcje platformy Azure są bezstanowe, czyli działają tak, jakby były uruchamiane ponownie za każdym razem, gdy reagują na zdarzenie. Jest to doskonałe rozwiązanie do przetwarzania danych przychodzących. Jeśli natomiast potrzebujesz obsługi stanów, możesz połączyć je z usługą Azure Storage.
