Zanim utworzysz usługę danych dotyczących temperatury, warto upewnić się, że przetwarzanie bezserwerowe jest w tym przypadku najlepszym rozwiązaniem. 

## <a name="what-is-serverless-compute"></a>Co to jest przetwarzanie bezserwerowe?
O przetwarzaniu bezserwerowym można myśleć jak o funkcji jako usłudze (FaaS) lub jak o mikrousłudze, która jest hostowana na platformie w chmurze. Ta funkcja zawiera kod logiki biznesowej, który można wykonywać bez ręcznego aprowizowania i skalowania infrastruktury. Platforma hostująca jest odseparowana — nie ma serwerów, do których można uzyskać bezpośredni dostęp, ani żadnego skalowania do oszacowania. 

## <a name="what-is-azure-functions"></a>Co to jest usługa Azure Functions?
Usługa Azure Functions to bezserwerowa platforma aplikacji. Umożliwia ona deweloperom hostowanie logiki biznesowej, która może być wykonywana bez aprowizowania infrastruktury. Usługa Azure Functions zapewnia wewnętrzną skalowalność, a opłaty są w niej naliczane tylko za użyte zasoby. Usługa Azure Functions umożliwia kodowanie w różnych językach, między innymi C#, F# i JavaScript, oraz zapewnia obsługę narzędzi NuGet i NPM, dzięki czemu może zawierać wiele popularnych bibliotek. 

## <a name="when-do-you-use-serverless-compute"></a>Kiedy należy używać przetwarzania bezserwerowego?
Przetwarzanie bezserwerowe to doskonałe rozwiązanie do hostowania kodu logiki biznesowej w chmurze. Charakteryzuje się ono automatycznym skalowaniem, brakiem serwerów, którymi trzeba zarządzać, oraz rozliczaniem z dokładnością poniżej sekundy. Ponadto zapewnia szeroki wybór języków programowania na potrzeby implementacji. Poniżej przedstawiono kilka dodatkowych właściwości, którym dobrze służy przetwarzanie bezserwerowe.

### <a name="avoid-overallocation-of-infrastructure"></a>Unikanie nadmiernej alokacji infrastruktury
Załóżmy, że masz aprowizowane serwery maszyn wirtualnych, które skonfigurowano przy użyciu odpowiedniej ilości zasobów, aby obsłużyć szczytowe momenty obciążenia. Gdy obciążenie jest małe, możesz potencjalnie płacić za infrastrukturę, której nie używasz. Przetwarzanie bezserwerowe pomaga rozwiązać problem z nadmierną alokacją dzięki automatycznemu skalowaniu w górę i w dół, oraz naliczaniu opłat tylko wtedy, kiedy funkcja jest uruchomiona.

### <a name="stateless-logic"></a>Logika bezstanowa
Funkcje bezstanowe świetnie nadają się do przetwarzania bezserwerowego — wystąpienia funkcji są tworzone i niszczone na żądanie. Jeśli wymagany jest stan, można go przechowywać w skojarzonej usłudze magazynu.

### <a name="event-driven"></a>Sterowane zdarzeniami
Funkcje platformy Azure są sterowane zdarzeniami. Działają one tylko w odpowiedzi na zdarzenie, takie jak odebranie żądania HTTP lub dodanie zdarzenia do kolejki. Konfiguracja funkcji platformy Azure znacznie upraszcza bazę kodu, umożliwiając zadeklarowanie, skąd pochodzą dane (wyzwalacz/powiązanie wejściowe) i gdzie trafiają (powiązanie wyjściowe). Nie trzeba pisać kodu, aby obserwować kolejki, obiekty blob, centra itp. Możesz skoncentrować się wyłącznie na logice biznesowej.

## <a name="when-do-you-not-use-serverless-compute"></a>Kiedy nie należy używać przetwarzania bezserwerowego?
Przetwarzanie bezserwerowe nie zawsze będzie odpowiednim rozwiązaniem do hostowania logiki biznesowej. Poniżej przedstawiono kilka właściwości usługi Azure Functions, które mogą mieć wpływ na decyzję dotyczącą hostowania usług za pomocą przetwarzania bezserwerowego. 

### <a name="execution-time"></a>Czas wykonywania
Domyślnie usługa Azure Functions ma limit czasu równy 5 minut. Można go skonfigurować i wydłużyć maksymalnie do 10 minut. Jeśli wykonanie Twojej funkcji trwa dłużej niż 10 minut, możesz ją hostować na maszynie wirtualnej. Ponadto jeśli Twoja usługa jest inicjowana za pośrednictwem żądania HTTP i oczekujesz tej wartości jako odpowiedzi HTTP, limit czasu jest ograniczony do 2,5 minuty.

### <a name="execution-frequency"></a>Częstotliwość wykonywania
Drugą właściwością jest częstotliwość wykonywania. Jeśli spodziewasz się, że funkcja będzie stale wykonywana przez wielu klientów, rozsądnie byłoby oszacować jej użycie i odpowiednio obliczyć koszt korzystania z usługi Azure Functions. Równie dobrze może okazać się, że tańsze będzie hostowanie usługi na maszynie wirtualnej.

Podczas skalowania tylko jedno wystąpienie aplikacji funkcji może być tworzone co 10 sekund, łącznie do maksymalnie 200 wystąpień. Pamiętaj, że każde wystąpienie może obsłużyć wiele równoczesnych wykonań, dlatego nie ma ustawionego żadnego ograniczenia określającego, jak duży ruch może obsłużyć pojedyncze wystąpienie. Różne typy wyzwalaczy mają różne wymagania dotyczące skalowania, dlatego zbadaj wybrany wyzwalacz i dowiedz się, jakie ma ograniczenia.
