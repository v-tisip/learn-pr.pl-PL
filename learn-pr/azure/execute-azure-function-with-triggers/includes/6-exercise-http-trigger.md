W tym ćwiczeniu utworzymy funkcję platformy Azure, która akceptuje żądanie HTTP z jednym ciągiem. Funkcja zwraca do obiektu wywołującego ciąg wskazujący na powodzenie lub niepowodzenie.

> [!NOTE]
> Aby wykonać to ćwiczenie, musisz zalogować się w witrynie [Azure Portal](https://portal.azure.com/) przy użyciu prawidłowego konta.

## <a name="create-an-http-trigger"></a>Tworzenie wyzwalacza HTTP

Będziemy nadal korzystać z istniejącej aplikacji usługi Azure Functions i dodamy wyzwalacz HTTP.

1. Wskaż pozycję **Funkcje** i wybierz ikonę plus (+).

    ![Wskazywanie pozycji Funkcje i zatrzymywanie wskaźnika nad ikoną plusa](../media-drafts/4-hover-function.png)

1. Wybierz pozycję **Wyzwalacz HTTP**.

1. Wybierz język **C#**. 

1. W polu **Nazwa** pozostaw wartość domyślną.

1. W polu **Poziom autoryzacji** wybierz ustawienie **Anonimowe**.

1. Wybierz pozycję **Utwórz**.

1. Przyjrzyj się szybko automatycznie wygenerowanemu kodowi, aby zobaczyć, co się dzieje. Parametr *req* reprezentuje żądanie przychodzące i zawiera parametr *name*. Sprawdzamy, czy parametr *name* ma wartość. Jeśli tak, zostanie zwrócone pozdrowienie. Jeśli nie, zwrócony zostanie komunikat o błędzie.

## <a name="get-your-function-url"></a>Pobieranie adresu URL funkcji

Po utworzeniu wyzwalacza HTTP pobierzemy adres URL funkcji, aby rozpocząć tworzenie żądania.

1. Wybierz wyzwalacz HTTP, aby otworzyć ekran z kodem.

1. Po prawej stronie polecenia **Uruchom** wybierz pozycję **Pobierz adres URL funkcji**.

1. Wybierz polecenie **Kopiuj**.

1. Wybierz polecenie **Uruchom**, aby uruchomić funkcję.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Wysyłanie żądania GET do wyzwalacza HTTP

Adres URL funkcji został skopiowany do schowka. Wyślemy teraz żądanie GET, aby sprawdzić, czy otrzymamy odpowiedź.

1. Otwórz nową kartę w przeglądarce internetowej.

1. Wklej adres URL na pasku adresu.

1. Dodaj parametr ciągu zapytania o nazwie *name* z Twoją nazwą, na przykład:

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. Naciśnij przycisk ENTER, aby przesłać żądanie.

## <a name="clean-up"></a>Czyszczenie

Aby upewnić się, że za tę funkcję nie zostaną naliczone opłaty, nad oknem dziennika wybierz polecenie **Wstrzymaj**.

![Wstrzymaj](../media-drafts/4-pause-timer.png)


