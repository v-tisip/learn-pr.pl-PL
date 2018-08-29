W ramach tego ćwiczenia będziemy pracować dalej z przykładem dotyczącym mechanizmu napędowego i dodamy logikę dla usługi temperatury. Ściślej mówiąc, będziemy odbierać dane z żądania HTTP.

## <a name="function-requirements"></a>Wymagania funkcji
Najpierw zdefiniujemy kilka wymagań logiki:
- temperatury z zakresu 0–25 powinny być oznaczone jako **OK**,
- temperatury z zakresu 26–50 powinny być oznaczone jako **OSTRZEŻENIE**,
- temperatury powyżej 50 powinny być oznaczone jako **NIEBEZPIECZEŃSTWO**.

## <a name="adding-a-function-to-an-azure-function-app"></a>Dodawanie funkcji do aplikacji funkcji platformy Azure

Jak już wiesz, platforma Azure zawiera elementy ułatwiające rozpoczynanie pracy z usługą Azure Functions. Doskonałą opcją dla osób rozpoczynających przygodę z funkcjami jest wygenerowanie funkcji na podstawie jednego z wielu dostępnych szablonów. W tym ćwiczeniu użyjesz szablonu HttpTrigger w celu wdrożenia usługi temperatury.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com) przy użyciu konta platformy Azure.
1. Przejdź do grupy zasobów utworzonej w pierwszym ćwiczeniu, wybierając pozycję **Wszystkie zasoby** w menu po lewej stronie, a następnie wybierając pozycję **escalator-functions-group**.
1. Zostaną wyświetlone zasoby należące do grupy. Przejdź do aplikacji funkcji utworzonej w poprzednim ćwiczeniu, wybierając element **escalator-functions-xxxxxxx** (oznaczony ikoną pioruna).
  ![Przechodzenie do aplikacji funkcji](../images/6-access-function-app.png)
1. W bloku zostanie wyświetlone omówienie aplikacji funkcji. Po lewej stronie znajduje się drzewo nawigacji, zawierające wszystkie zdefiniowane funkcje, serwery proxy i miejsca. Ponieważ nie utworzyliśmy jeszcze funkcji, będzie ono puste. Aby utworzyć funkcję, umieść wskaźnik myszy na pozycji **Funkcja** w drzewie nawigacji i kliknij wyświetlony przycisk **+**.
  ![Dodawanie funkcji w drzewie nawigacji](../images/5-function-add-button.png)
1. W formularzu szybkiego rozpoczynania pracy przy użyciu gotowej funkcji wybierz link **Funkcja niestandardowa** w sekcji **Rozpocznij pracę samodzielnie**.
  ![Formularz gotowej funkcji](../images/6-custom-function.png)
1. Zostanie wyświetlona lista szablonów. Wybierz szablon wyzwalacza HTTP z wdrożeniem JavaScript.
  ![Szablon wyzwalacza HTTP](../images/6-httptrigger-template.png)
1. Zostanie wyświetlony blok, w którym możesz zdefiniować funkcję generowaną za pomocą szablonu. W tym przypadku chcesz wygenerować funkcję w języku JavaScript o nazwie **DriveGearTemperatureService**. Po wpisaniu nazwy funkcji naciśnij przycisk **Utwórz**.
  ![Formularz tworzenia wyzwalacza HTTP](../images/6-create-httptrigger-form.png)
1. Po chwili zobaczysz utworzony za pomocą szablonu kod źródłowy funkcji. Gotowa funkcja wymaga wprowadzenia imienia i zwraca ciąg **Hello, {imię}** (Witaj).

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');

        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

1. Po prawej stronie kodu źródłowego zobaczysz dwie karty. Na karcie **Wyświetl pliki** możesz wyświetlić wszystkie pliki używane przez funkcję. Aby wyświetlić konfigurację funkcji, wybierz plik **function.json**. Zobaczysz w nim zdefiniowany element httpTrigger oraz powiązanie wyjściowe. Ta konfiguracja określa, że funkcja jest wyzwalana przez żądanie HTTP, a powiązanie wyjściowe wskazuje, że odpowiedź jest wysyłana jako odpowiedź HTTP.

    ```javascript
    {
      "disabled": false,
      "bindings": [
        {
          "authLevel": "function",
          "type": "httpTrigger",
          "direction": "in",
          "name": "req"
        },
        {
          "type": "http",
          "direction": "out",
          "name": "res"
        }
      ]
    }
    ```

## <a name="running-the-premade-azure-function"></a>Uruchamianie gotowej funkcji platformy Azure

Aby uruchomić funkcję, możesz zainicjować żądanie HTTP za pomocą narzędzia cURL w wierszu polecenia. Aby znaleźć adres URL punktu końcowego, wróć do kodu funkcji i wybierz link **Pobierz adres URL funkcji**. Skopiuj ten link do schowka.  Adres URL powinien być podobny do następującego: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Uzyskiwanie adresu URL punktu końcowego](../images/6-get-function-url.png)

Używając tego adresu URL, uruchom polecenie cURL, aby zainicjować funkcję (zastępując adres URL własnym):

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Odpowiedź gotowej funkcji na polecenie cURL](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a>Dodawanie logiki biznesowej do funkcji

Nasza funkcja oczekuje tablicy odczytów temperatury przesłanych przez klienta. Przykładowa treść żądania może być następująca:

```javascript
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

Zmodyfikuj kod gotowej funkcji, aby zaimplementować odpowiednią logikę biznesową. Otwórz plik index.js i zastąp go poniższą treścią:

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        for(var i=0; i<req.body.readings.length; i++){
            var reading = req.body.readings[i];
            if(reading.temperature<=25){
                context.log('Reading is OK');
                reading.status = 'OK';
                continue;
            }
            if(reading.temperature<=50){
                context.log('Reading is CAUTION');
                reading.status = 'CAUTION';
                continue;
            }
            context.log('Reading is DANGER');
            reading.status = 'DANGER'
        }
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

Zwróć uwagę na informacje w dzienniku. Po uruchomieniu funkcji w oknie dziennika będą dodawane komunikaty.

## <a name="testing-your-business-logic"></a>Testowanie logiki biznesowej

Otwórz okno testowania za pomocą menu wysuwanego po prawej stronie, a następnie wklej przykładowe żądanie podane powyżej w polu tekstowym treści żądania. Naciśnij przycisk **Uruchom** i sprawdź dane wyjściowe. Możesz również otworzyć okno dziennika z menu wysuwanego na dole, aby zobaczyć informacje rejestrowane w dzienniku.
![Testowanie logiki biznesowej](../images/6-portal-testing.png) Dane JSON w oknie danych wyjściowych wskazują, że do każdego z odczytów zostało prawidłowo dodane pole określające stan temperatury. Możesz również przejść do pulpitu nawigacyjnego monitorowania, gdzie zobaczysz, że żądanie zostało zarejestrowane w usłudze Application Insights.
![Żądanie w usłudze Application Insights](../images/6-app-insights.png)
