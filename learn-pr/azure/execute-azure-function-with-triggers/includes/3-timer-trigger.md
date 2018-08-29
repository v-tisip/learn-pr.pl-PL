Fragment logiki często jest wykonywany w ustalonych przedziałach czasu. Wyobraź sobie, że prowadzisz blogu i zauważasz, że Twoi subskrybenci nie czytają najnowszych wpisów. Decydujesz, że najlepszym rozwiązaniem będzie wysyłanie im raz w tygodniu wiadomości e-mail z przypomnieniem o odwiedzeniu blogu. Możesz zaimplementować tę logikę za pomocą funkcji platformy Azure z wyzwalaczem czasomierza, który będzie wywoływać funkcję raz na tydzień.

Z tego artykułu dowiesz się, jak utworzyć wyzwalacz czasomierza i napisać instrukcję uruchamiającą go w stałych odstępach czasu.

## <a name="what-is-a-timer-trigger"></a>Co to jest wyzwalacz czasomierza?

Wyzwalacz czasomierza to wyzwalacz, który wykonuje funkcję w stałych odstępach czasu. Aby utworzyć wyzwalacz czasomierza, musisz podać dwie informacje. Pierwsze wymaganie to *Nazwa parametru znacznika czasu*, która jest po prostu identyfikatorem umożliwiającym uzyskanie dostępu do wyzwalacza w kodzie. Drugie wymaganie to *Harmonogram*, czyli *wyrażenie CRON* określające interwał dla czasomierza.

## <a name="what-is-a-cron-expression"></a>Co to jest wyrażenie CRON?

*Wyrażenie CRON* jest ciągiem, który składa się z sześciu pól reprezentujących zestaw czasowy.

Kolejność tych sześciu pól na platformie Azure jest następująca: {sekunda} {minuta} {godzina} {dzień} {miesiąc} {dzień tygodnia}.

*Wyrażenie CRON* tworzące wyzwalacz, który jest wykonywany co pięć minut, może wyglądać następująco:

```
0 */5 * * * *
```

Na pierwszy rzut oka ten ciąg może wydawać się nieco skomplikowany. Wrócimy jeszcze do niego i dokładniej omówimy te pojęcia, gdy lepiej poznamy *wyrażenia CRON*.

Aby utworzyć *wyrażenie CRON*, musisz mieć podstawową wiedzę na temat niektórych znaków specjalnych.

| Znak specjalny | Znaczenie | Przykład |
| ------------- | ------------- | ------------- |
| *      | Wybiera każdą wartość w polu | Gwiazdka „*” w polu dnia tygodnia oznacza *codziennie*. |
| ,      | Oddziela elementy na liście | Przecinek „1,3” w polu dnia tygodnia oznacza tylko poniedziałki (dzień 1) i środy (dzień 3). |
| -      | Określa zakres | Łącznik „10 – 12” w polu godziny oznacza zakres, który obejmuje godzinę 10, 11 i 12. |
| /      | Określa przyrost | Ukośnik „*/10” w polu minut oznacza przyrost co 10 minut. |

Teraz wrócimy do pierwotnego przykładu wyrażenia CRON. Spróbujmy zrozumieć je lepiej, dzieląc je na poszczególne pola.

```
0 */5 * * * *
```

**Pierwsze pole** reprezentuje sekundy. To pole obsługuje wartości od 0 do 59. Ponieważ pole zawiera zero, wybiera pierwszą możliwą wartość, czyli jedną sekundę.

**Drugie pole** reprezentuje minuty. Wartość „*/5” zawiera dwa znaki specjalne. Pierwszy, gwiazdka (*), oznacza „wybierz każdą wartość w polu”. Ponieważ to pole reprezentuje minuty, możliwe wartości to 0–59. Drugi znak specjalny to ukośnik (/), który reprezentuje przyrost. Gdy połączymy te znaki ze sobą, oznacza to „ze wszystkich wartości z zakresu 0–59 wybierz co piątą wartość”. Mówiąc prościej, oznacza to „co pięć minut”.

**Pozostałe cztery pola** reprezentują godzinę, dzień, miesiąc i dzień tygodnia. Gwiazdka dla tych pól oznacza, że ma być wybrana każda możliwa wartość. W tym przykładzie wybieramy „co godzinę każdego dnia każdego miesiąca”.

Po połączeniu tych wszystkich pól otrzymujemy wyrażenie, które mówi „w pierwszej sekundzie każdej co piątej minuty każdej godziny, codziennie w każdym miesiącu”.

## <a name="how-to-create-a-timer-trigger"></a>Jak utworzyć wyzwalacz czasomierza

Wyzwalacz czasomierza można utworzyć całkowicie w witrynie Azure Portal. W funkcji platformy Azure wybierz pozycję **wyzwalacz czasomierza** z listy wstępnie zdefiniowanych wyzwalaczy. Wprowadź logikę, którą chcesz wykonać. Podaj **nazwę parametru znacznika czasu** i **wyrażenie CRON**.

## <a name="summary"></a>Podsumowanie

Wyzwalacz czasomierza wywołuje funkcję platformy Azure zgodnie z ustalonym harmonogramem. Aby zdefiniować harmonogram dla wyzwalacza czasomierza, należy utworzyć *wyrażenie CRON*, czyli ciąg, który reprezentuje zestaw czasowy.

