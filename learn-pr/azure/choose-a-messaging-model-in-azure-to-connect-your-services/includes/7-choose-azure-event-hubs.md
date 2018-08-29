Istnieją pewne aplikacje, które tworzą ogromną liczbę zdarzeń z niemal dowolnej liczby źródeł. Często stosuje się termin „dane big data” do opisu tych sytuacji. Ponadto wymagają unikatowej infrastruktury do obsługi.

Załóżmy, że pracujesz dla firmy Contoso Aircraft Engines. Silniki samolotowe wytwarzane przez Twojego pracodawcę mają setki czujników. Zanim samolot będzie mógł wzbijać się w powietrze każdego ranka, jego silniki są podłączane do uprzęży testowej i uruchamiane z różnymi prędkościami. Ponadto dane zebrane podczas lotu są przesyłane strumieniowo po podłączeniu samolotu do urządzeń naziemnych.

Chcesz użyć historycznych danych z czujników, aby odkryć wzorce w odczytach, które wskazują na to, że prawdopodobnie wkrótce dojdzie do awarii silnika. Chcesz porównać odczyty z czujników w czasie rzeczywistym z tymi wzorcami dotyczącymi awarii. Następnie możesz ostrzegać użytkowników w czasie zbliżonym do rzeczywistego, jeżeli silnik zacznie wykazywać odczyty budzące obawy.

## <a name="what-is-azure-event-hubs"></a>Co to jest usługa Azure Event Hubs?

Usługa Azure Event Hub jest pośrednikiem dla wzorca komunikacji publikowania-subskrybowania, ale w przeciwieństwie do usługi Event Grid jest zoptymalizowana pod kątem ekstremalnie wysokiej przepływności, dużej liczby wydawców, zabezpieczeń oraz odporności.

Podczas gdy usługa Event Grid pasuje bardziej lub mniej doskonale do wzorca publikowania-subskrybowania, ponieważ po prostu zarządza subskrypcjami i kieruje komunikację do tych subskrybentów, usługa Event Hub wykonuje kilka dodatkowych funkcji, które w pewien sposób upodabniają ją bardziej do magistrali usług lub kolejki komunikatów zamiast prostego nadawcy zdarzeń.

#### <a name="partitions"></a>Partycje ####
Gdy usługa Event Hub odbiera komunikaty, dzieli je na partycje. Partycje stanowią bufory, w których zapisuje się komunikację. Ze względu na zastosowanie buforów zdarzeń zdarzenia nie są całkowicie tymczasowe — zdarzenie nie zostanie utracone tylko dlatego, że subskrybent był zajęty lub był w trybie offline. Subskrybent zawsze może użyć buforu, żeby „nadrobić zaległości”. Domyślnie zdarzenia pozostają w buforze przez 24 godziny i automatycznie wygasają po tym czasie.

Bufory są zwane partycjami, ponieważ dane są dzielone między nimi. Każda usługa Event Hub ma co najmniej dwie partycje, a każda partycja ma oddzielny zestaw subskrybentów.

#### <a name="capture"></a>Przechwytywanie ####
Usługa Event Hub może wysyłać wszystkie zdarzenia natychmiast do usługi Azure Data Lake lub usługi Blob Storage, aby zapewnić niedrogą trwałość zdarzeń.

#### <a name="authentication"></a>Uwierzytelnianie ####
Wszyscy wydawcy są uwierzytelniani i wystawia się dla nich token. Oznacza to, że usługa Event Hub może akceptować zdarzenia z urządzeń zewnętrznych oraz aplikacji mobilnych bez obaw o to, że fałszywe dane od złośliwych osób zrujnują analizę. 

## <a name="using-azure-event-hub"></a>Używanie usługi Azure Event Hub

Usługa Event Hub obsługuje przetwarzanie potokowe strumieni zdarzeń do innych usług platformy Azure. Na przykład użycie jej wraz z usługą Stream Analytics umożliwia korzystanie ze złożonej analizy danych w czasie zbliżonym do rzeczywistego, z możliwością korelowania wielu zdarzeń oraz wyszukiwania wzorców. W tym przypadku usługa Stream Analytics będzie uznawana za subskrybenta.

Dla naszych silników samolotowych skonfigurujemy architekturę, aby usługa Event Hubs uwierzytelniała komunikację z silnikami. Następnie użyjemy opcji przechwytywania, aby zapisać wszystkie dane w usłudze Azure Data Lake. Później będziemy mogli użyć wszystkich tych danych do ponownego wytrenowania oraz poprawienia modeli uczenia maszynowego. Na koniec nasze strumienie zdarzeń zostaną odebrane przez subskrybentów usługi Azure Stream Analytics. Usługa Stream Analytics użyje modelu uczenia maszynowego, aby wyszukać wzorce w danych z czujników, które mogą wskazywać problemy.

Ponieważ mamy kilka partycji, a każdy silnik wysyła wszystkie dane tylko do jednej partycji na każde wystąpienie usługi Stream Analytics, subskrybent musi sobie poradzić tylko z podzbiorem wszystkich zebranych danych, zamiast filtrować i korelować ich całość.

## <a name="choose-event-grid-or-event-hub"></a>Wybieranie usługi Event Grid lub Event Hub

Obie usługi obsługują semantykę *Co najmniej raz*.

Jeśli potrzebujesz prostej infrastruktury publikowania-subskrybowania zdarzeń od zaufanych wydawców (np. od własnego serwera internetowego), wybierz usługę Azure Event Grid.

### <a name="consider-event-hub-if"></a>Rozważ usługę Event Hub, jeśli:
* potrzebujesz obsługi uwierzytelniania wielu wydawców;
* chcesz zapisać strumień zdarzeń do usługi Azure Data Lake lub usługi Blob Storage;
* chcesz agregować lub analizować strumień zdarzeń;
* potrzebujesz niezawodnej obsługi komunikatów lub odporności. 