Załóżmy, że planujesz architekturę rozproszonej aplikacji do udostępniania muzyki. Chcesz mieć pewność, że aplikacja będzie tak niezawodna i skalowalna, jak to możliwe, i zamierzasz utworzyć niezawodną infrastrukturę komunikacji, korzystając z technologii platformy Azure.

Zanim wybierzesz odpowiednią technologię platformy Azure, musisz poznać całą komunikację wymienianą przez składniki aplikacji. Dla każdego rodzaju komunikacji możesz wybrać inną technologię platformy Azure.

Pierwszą rzeczą, którą należy ustalić, jest to, czy w ramach komunikacji są wysyłane komunikaty, czy zdarzenia. Niektóre technologie platformy Azure są przeznaczone dla zdarzeń, a inne dla komunikatów, więc jest to fundamentalne rozróżnienie.

## <a name="what-is-a-message"></a>Co to jest komunikat?

W terminologii aplikacji rozproszonych **komunikaty** mają następujące cechy:

- Komunikat zawiera dane pierwotne wygenerowane przez jeden składnik, które zostaną wykorzystane przez inny składnik.
- Komunikat zawiera rzeczywiste dane, a nie tylko odwołanie do nich.
- Składnik wysyłający oczekuje, że zawartość komunikatu zostanie przetworzona przez składnik docelowy w określony sposób. Integralność całego systemu może zależeć od wykonania konkretnego zadania zarówno przez nadawcę, jak i odbiorcę.

Na przykład załóżmy, że użytkownik przekazuje nowy utwór za pomocą mobilnej aplikacji do udostępniania muzyki. Aplikacja mobilna musi wysłać ten utwór do internetowego interfejsu API, który działa na platformie Azure. Musi zostać wysłany rzeczywisty plik multimedialny utworu, a nie jedynie alert wskazujący, że dodano nowy utwór. Aplikacja mobilna oczekuje, że internetowy interfejs API zapisze nowy utwór w bazie danych i udostępni go innym użytkownikom. To jest przykład komunikatu.

## <a name="what-is-an-event"></a>Co to jest zdarzenie?

**Zdarzenia** są prostsze niż komunikaty i są najczęściej używane w przypadku emisji. Składniki wysyłające zdarzenia są nazywane **wydawcami**, a odbierające — **subskrybentami**.

W przypadku zdarzeń składniki odbierające zazwyczaj określają, jaka komunikacja jest im potrzebna, i ją subskrybują. Subskrypcją zwykle zarządza pośrednik, np. usługa Azure Event Grid lub Azure Event Hub. Gdy wydawca wyśle zdarzenie, pośrednik skieruje je do odpowiednich subskrybentów. Taki układ jest nazywany architekturą publikowania i subskrybowania. Nie jest to jedyny sposób obsługi zdarzeń, ale jest najbardziej powszechny.

Zdarzenia mają następujące cechy:

- Zdarzenie to uproszczone powiadomienie, które wskazuje, że coś się wydarzyło.
- Zdarzenie może zostać wysłane do wielu odbiorców albo do żadnego.
- Zdarzenia często mają się rozprzestrzeniać, czyli każdy wydawca ma mieć wielu subskrybentów.
- Wydawca zdarzenia nie ma żadnych oczekiwań w stosunku do akcji podejmowanej przez składnik odbierający.
- Niektóre zdarzenia to odrębne jednostki, które nie są powiązane z innymi zdarzeniami. 
- Inne zdarzenia są częścią powiązanej i uporządkowanej serii.  

Załóżmy na przykład, że przekazywanie pliku z muzyką zostało zakończone i nowy utwór został dodany do bazy danych. Aby poinformować użytkowników o nowym pliku, internetowy interfejs API musi powiadomić o nim użytkowników frontonu internetowego i aplikacji mobilnej. Użytkownicy mogą zdecydować, czy posłuchać nowego utworu, więc początkowe powiadomienie nie zawiera pliku z muzyką, a jedynie informuje użytkowników, że plik istnieje. Nadawca nie oczekuje, że odbiorcy zdarzenia wykonają konkretną akcję po otrzymaniu zdarzenia.

To jest przykład odrębnego zdarzenia.

## <a name="how-to-choose-messages-or-events"></a>Jak wybrać komunikaty lub zdarzenia

Pojedyncza aplikacja prawdopodobnie będzie używać zdarzeń w niektórych przypadkach i komunikatów w innych. Przed dokonaniem wyboru musisz przeanalizować architekturę aplikacji oraz wszystkie przypadki jej użycia, aby zidentyfikować cele, w jakich składniki komunikują się ze sobą. 

Zdarzenia będą częściej używane w przypadku emisji i zwykle są efemeryczne. To oznacza, że komunikacja może nie zostać obsłużona przez żadnego odbiorcę, jeśli żaden jej nie subskrybuje. Komunikaty będą częściej używane w przypadku, gdy aplikacja rozproszona wymaga gwarancji przetworzenia komunikacji.

Dla każdego rodzaju komunikacji odpowiedz na pytanie: czy składnik wysyłający oczekuje przetworzenia komunikacji przez składnik docelowy w określony sposób?

Jeśli tak, użyj komunikatu. Jeśli nie, prawdopodobnie możesz użyć zdarzeń.

## <a name="summary"></a>Podsumowanie

Składniki aplikacji rozproszonej komunikują się ze sobą w wielu różnych celach. Dla każdego z tych celów musisz wybrać, czy używać zdarzeń, czy komunikatów, aby zastosować technologię platformy Azure przeznaczoną do odpowiedniego celu. 

Po zrozumieniu, dlaczego składniki komunikują się ze sobą, oraz określeniu, czy używają zdarzeń, czy komunikatów, możesz wybrać kolejki usługi Azure Storage albo usługę Event Hubs, Event Grids lub Service Bus na potrzeby wymiany tych informacji.