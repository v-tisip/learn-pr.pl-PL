Żądanie HTTP jest typową operacją na większości platform i urządzeń. Niezależnie od tego, czy jest to żądanie wyszukania wyrazu w słowniku, czy pozyskania danych o lokalnej pogodzie, cały czas wysyłamy żądania HTTP. Usługa Azure Functions umożliwia szybkie utworzenie fragmentu logiki do wykonania w momencie odebrania żądania HTTP.  

Tutaj dowiesz się, jak utworzyć i wywołać usługę Azure Function przy użyciu wyzwalacza HTTP. Ponadto przedstawimy niektóre dostępne opcje dostosowywania.

## <a name="what-is-an-http-trigger"></a>Czym jest wyzwalacz HTTP?

Wyzwalacz HTTP to wyzwalacz, który wykonuje funkcję po odebraniu żądania HTTP. Wyzwalacze HTTP mają wiele możliwości i opcji dostosowania, w tym:

- Zapewnianie autoryzowanego dostępu poprzez dostarczenie kluczy.
- Ograniczanie obsługiwanych zleceń HTTP.
- Zwracanie danych z powrotem do obiektu wywołującego.
- Odbieranie danych za pośrednictwem parametrów ciągu zapytania lub w treści zapytania.
- Obsługa szablonów trasy adresu URL w celu modyfikowania adresu URL funkcji.

Po utworzeniu wyzwalacza HTTP wybierz język programowania, podaj nazwę wyzwalacza i wybierz poziom autoryzacji.

## <a name="what-is-an-http-trigger-authorization-level"></a>Co to jest poziom autoryzacji wyzwalacza HTTP?

Poziom autoryzacji wyzwalacza HTTP to flaga, która wskazuje, czy przychodzące żądanie HTTP wymaga klucza interfejsu API na potrzeby uwierzytelniania.

Istnieją trzy poziomy autoryzacji:

- Funkcja
- Anonimowe
- Administrator

Poziomy **Funkcja** i **Administrator** są oparte na „kluczu”. Aby wysłać żądanie HTTP, musisz podać klucz na potrzeby uwierzytelniania. Istnieją dwa typy kluczy: *funkcja* i *host*. Różnice pomiędzy dwoma kluczami widoczne są w ich zakresie. Klucze *funkcji* są właściwe dla funkcji. Klucze *hosta* dotyczą wszystkich funkcji w całej aplikacji Azure Functions. Jeśli poziom autoryzacji jest ustawiony na opcję **Funkcja**, możesz użyć klucza *funkcji* lub *hosta*. Jeśli poziom autoryzacji jest ustawiony na opcję **Administrator**, należy podać klucz *hosta*.

Poziom **Anonimowe** oznacza, że nie jest wymagane uwierzytelnienie. Używamy tego poziomu w naszym ćwiczeniu.

## <a name="how-to-create-an-http-trigger"></a>Sposób tworzenia wyzwalacza HTTP

Podobnie jak w przypadku wyzwalacza czasomierza możesz utworzyć wyzwalacz HTTP za pośrednictwem witryny Azure Portal. Wewnątrz funkcji platformy Azure wybierz opcję **Wyzwalacz HTTP** z listy wstępnie zdefiniowanych typów wyzwalaczy. Następnie wprowadź logikę, którą chcesz wykonać oraz zastosuj wszelkie opcje dostosowania, np. ograniczenie użycia wybranych zleceń HTTP. 

Jedno ustawienie, którego zrozumienie jest ważne, to **Nazwa parametru żądania**. To ustawienie jest ciągiem reprezentującym nazwę parametru, który zawiera informacje o przychodzącym żądaniu HTTP. Domyślnie nazwa parametru to *req*.

## <a name="how-to-invoke-an-http-trigger"></a>Sposób wywoływania wyzwalacza HTTP

Aby wywołać wyzwalacz HTTP, należy wysłać żądanie HTTP do adresu URL funkcji. Aby uzyskać ten adres URL, przejdź do strony kodu funkcji i wybierz link **Pobierz adres URL funkcji**.

![Znajdywanie adresu URL funkcji](../media/5-function-url.png)

Po utworzeniu adresu URL dla funkcji możesz wysłać żądania HTTP. Jeżeli funkcja odbiera dane, pamiętaj że możesz użyć parametrów ciągu zapytania lub podać dane bezpośrednio w treści zapytania.

## <a name="summary"></a>Podsumowanie

Wyzwalacz HTTP wywoła funkcję platformy Azure, gdy odbierze żądanie HTTP do adresu URL funkcji. Wyzwalacze HTTP umożliwiają odbieranie danych oraz zwracanie danych z powrotem do obiektu wywołującego.
