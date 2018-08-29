Teraz wszystko jest gotowe do rozpoczęcia implementowania usługi temperatury. W poprzednim module ustalono, że rozwiązanie niewymagające użycia serwera najlepiej odpowiada Twoim potrzebom. Aby zaimplementować funkcję platformy Azure nieużywającą serwera, musi ona mieć miejsce „zwane domem”. Ten „dom” to aplikacja funkcji platformy Azure.

## <a name="azure-function-app-overview"></a>Omówienie aplikacji funkcji platformy Azure
Funkcje platformy Azure są hostowane w kontenerze zwanym aplikacją funkcji. Definiowanie aplikacji funkcji platformy Azure ma na celu logiczne grupowanie funkcji i tworzenie ich struktury. Aplikacje funkcji to zasób obliczeniowy na platformie Azure. W naszym przykładzie dotyczącym podnośników będzie tworzona aplikacja funkcji do hostowania usługi temperatury mechanizmu napędowego schodów ruchomych. Aby utworzyć aplikację, trzeba podjąć kilka decyzji. Musisz wybrać plan usługi, a następnie wybrać zgodne konto magazynu.

### <a name="choosing-a-service-plan"></a>Wybieranie planu usług
Aplikacje funkcji mogą używać jednego z dwóch typów planów usług. Pierwszy plan usług to plan użycia usługi. Jest to plan wybierany w przypadku korzystania z platformy aplikacji nieużywających serwera na platformie Azure. Plan użycia usługi umożliwia automatyczne skalowanie, a opłaty są naliczane po uruchomieniu funkcji. Plan użycia oferuje możliwość skonfigurowania okresu limitu czasu na potrzeby wykonywania funkcji. Domyślnie jest to 5 minut, ale można skonfigurować limit czasu wynoszący 10 minut. 

Drugi plan nosi nazwę „plan usługi Azure App Service”. Ten plan umożliwia uruchamianie funkcji na maszynie wirtualnej w sposób ciągły. Należy wybrać tę opcję, jeśli funkcje są używane w sposób ciągły lub wymagają więcej mocy obliczeniowej albo dłuższego czas wykonywania niż oferowane przez plan użycia. 

### <a name="storage-account-requirements"></a>Wymagania konta magazynu
Tworzona aplikacja funkcji jest zwykle łączona z kontem magazynu, które obsługuje usługi Azure Blob, Queue i Table Storage. Aplikacja funkcji używa tego konta magazynu na potrzeby operacji wewnętrznych, takich jak rejestrowanie wykonań funkcji i zarządzanie wyzwalaczami wykonywania. W tym rozwiązaniu są również przechowywane pliki konfiguracji i kod funkcji platformy Azure powiązane z planem użycia usługi. 
