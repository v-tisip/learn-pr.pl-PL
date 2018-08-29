Teraz, gdy mamy już utworzoną aplikację funkcji, nauczymy się, jak skonstruować, skonfigurować i wykonać funkcję platformy Azure.

### <a name="triggers"></a>Wyzwalacze
Funkcje platformy Azure są sterowane zdarzeniami i są wykonywane w odpowiedzi na zdarzenie, takie jak odebranie żądania HTTP lub dodanie zdarzenia do kolejki. 

Typ zdarzenia, które inicjuje funkcję, to tak zwany wyzwalacz. Funkcje platformy Azure wymagają skonfigurowania co najmniej jednego wyzwalacza. W przeciwnym razie nie będzie można uruchomić funkcji.

 Platforma Azure obsługuje szeroki zakres wyzwalaczy, w tym:
* HTTPTrigger
* TimerTrigger
* Element webhook GitHub
* CosmosDBTrigger
* BlobTrigger
* QueueTrigger
* EventHubTrigger
* ServiceBusQueueTrigger
* ServiceBusTopicTrigger

### <a name="bindings"></a>Powiązania
Powiązania funkcji platformy Azure to deklaratywna metoda programowego łączenia z danymi z funkcji.

Powiązania stanowią połączenie z usługami danych. Funkcja platformy Azure bez powiązań lub z co najmniej jednym powiązaniem umożliwia uzyskiwanie dostępu do wielu źródeł danych. Powiązania można definiować jako wejściowe lub wyjściowe, bądź traktować jako powiązania odczytu i zapisu.

Załóżmy, że masz wyzwalacz QueueTrigger, który inicjuje funkcję, gdy do kolejki zostanie dodany obiekt blob. Wejściowe powiązanie obiektu blob może służyć do nawiązania połączenia z usługą Azure Blob Storage. 

Powiązania wyjściowe są używane do przechowywania danych. Wysyłają one na przykład zwróconą wartość funkcji do usługi Azure Table Storage.

Pełna lista dostępnych powiązań znajduje się w [dokumentacji platformy Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).

### <a name="a-sample-trigger-and-binding-functionjson"></a>Przykładowy wyzwalacz i powiązanie (function.json)
To jest przykładowa definicja wyzwalacza i powiązania dla funkcji. Pamiętaj, że w zależności od opisywanego typu powiązania trzeba ustawić różne wartości właściwości. Każde powiązanie ma również kierunek, który definiuje, czy jest to powiązanie wejściowe czy wyjściowe. Wyzwalacze zawsze są powiązania wejściowymi. W tym przykładzie pokazano funkcję, która jest wyzwalana przez komunikat dodawany do kolejki o nazwie **myqueue-items**. Zwracana wartość funkcji jest następnie wysyłana do tabeli **outTable** w usłudze Azure Table Storage.

```javascript
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
## <a name="premade-functions-and-templates"></a>Gotowe funkcje i szablony
Platforma Azure oferuje wstępnie skonfigurowane szablony dla typowych scenariuszy funkcji platformy Azure.

### <a name="quickstart-templates"></a>Szablony szybkiego startu
Aby dodać funkcję platformy Azure, musisz wybrać aplikację funkcji. Aplikację funkcji można rozpoznać po ikonie błyskawicy w nawiasach ostrych.  
![Ikona funkcji](../images/5-function-icon.png)

Podczas dodawania pierwszej funkcji platformy Azure jest wyświetlany ekran przewodnika Szybki start. Ten ekran umożliwia wybranie typu wyzwalacza i języka programowania. Następnie na podstawie dokonanego wyboru platforma Azure wygeneruje dla Ciebie kod funkcji i konfigurację.  
![Funkcja — Przewodnik Szybki start](../images/5-quickstart-form.png)

### <a name="function-templates"></a>Szablony funkcji
Wybór szablonów nie jest ograniczony do tych, które są dostępne w przewodniku Szybki start. Istnieje również możliwość wyboru spośród ponad 30 różnych szablonów. Dostęp do listy szablonów można uzyskać, tworząc kolejne funkcje, lub wybierając opcję **Funkcja niestandardowa** na ekranie Szybki start.  
![Szablony funkcji](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>Przechodzenie do funkcji i plików
Gdy tworzysz funkcję na podstawie szablonu, tworzonych jest kilka plików. Załóżmy, że wybrano przewodnik Szybki start „Element webhook i interfejs API” oraz język JavaScript. Zostanie wygenerowany plik konfiguracji **function.json** oraz plik kodu źródłowego **index.js**. Podczas uzyskiwania dostępu do aplikacji funkcji zostanie wyświetlone drzewo menu zawierające funkcje, które zostały utworzone w aplikacji. Za pomocą elementu menu **Funkcje** można także dodać kolejne funkcje do aplikacji funkcji (gdy umieścisz wskaźnik myszy na tym elemencie menu, zostanie wyświetlona ikona plusa +).  
![Przycisk Dodaj funkcję](../images/5-function-add-button.png) 

W przypadku wspomnianego powyżej przewodnika Szybki start po rozwinięciu elementu menu **Funkcje** w widoku drzewa zostanie wyświetlona jedna funkcja o nazwie domyślnej **HttpTriggerJS1** (oznaczona ikoną funkcji). Wybranie tej funkcji spowoduje otwarcie okna kodu i wyświetlenie pliku źródłowego **index.js**. Po prawej stronie okna kodu znajduje się menu wysuwane, które zawiera kartę **Wyświetl pliki**. Wybranie tej karty umożliwia wyświetlenie struktury plików (takiej samej, jak w magazynie) tworzących funkcję.  
![Szablony funkcji](../images/5-file-navigation.png)

## <a name="execution-options-for-testing-your-azure-function"></a>Opcje wykonywania w celu przetestowania funkcji platformy Azure
Po utworzeniu funkcji platformy Azure musisz wiedzieć, jak ją przetestować. Istnieje na to kilka sposobów: wykonywanie ręczne lub testowanie w witrynie Azure Portal.

### <a name="manual-execution-of-a-function"></a>Ręczne wykonywanie funkcji
Wykonywanie funkcji można zainicjować, ręcznie wyzwalając skonfigurowany wyzwalacz. Jeśli na przykład używasz wyzwalacza HttpTrigger, możesz użyć narzędzia takiego jak Postman lub cURL, aby zainicjować żądanie HTTP do adresu URL punktu końcowego funkcji.  
![Wykonywanie funkcji za pomocą narzędzia Postman](../images/5-postman-execution.png) Adres URL punktu końcowego można uzyskać, wybierając zastosowany wyzwalacz HTTP w lewym obszarze nawigacji, a następnie wybierając przycisk **Pobierz adres URL funkcji**.  
![Pobierz adres URL funkcji](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Testowanie funkcji w witrynie Azure Portal
Witryna Azure Portal także udostępnia wygodny sposób testowania funkcji. Po prawej stronie okna kodu znajduje się wysuwane menu nawigacji z kartami. To menu zawiera element **Test**. Rozwinięcie tego menu i wybranie tej karty to inny sposób na wykonanie funkcji i wyświetlenie wyników. Zachowując zgodność ze scenariuszem wyzwalacza HttpTrigger, możesz skonfigurować metodę HTTP i dodać parametry ciągu kwerendy oraz nagłówki do żądania HTTP. Możesz także zmienić treść żądania, aby przetestować dodatkowe scenariusze. W oknie danych wyjściowych zostanie wyświetlony wynik funkcji.  
![Wykonywanie funkcji w witrynie Portal](../images/5-portal-execution.png)

## <a name="monitoring-an-azure-function"></a>Monitorowanie funkcji platformy Azure
Możliwość rejestrowania komunikatów i określania scenariuszy wyjątków podczas tworzenia funkcji platformy Azure ma krytyczne znaczenie w zakresie odpowiedniego przygotowania funkcji do produkcji. Jest to tak samo ważne w procesie produkcji, jak śledzenie źródła defektu. Witryna Azure Portal oferuje interfejs użytkownika, który udostępnia pulpit nawigacyjny monitorowania, a także sposób na przejrzenie dzienników wykonywania i wyjątków uzyskanych z funkcji platformy Azure.

### <a name="monitoring-dashboard"></a>Pulpit nawigacyjny monitorowania
W menu nawigacji aplikacji funkcji po rozwinięciu węzła funkcji zostanie wyświetlony element menu **Monitoruj**. Pulpit nawigacyjny monitorowania zapewnia szybki sposób na wyświetlenie historii wykonań funkcji. Ten widok zawiera sygnaturę czasową, kod wyniku, czas trwania i identyfikator operacji oraz informację, czy funkcja została wykonana pomyślnie. Te dane są wypełniane za pomocą usługi Azure Application Insights.  
![Monitor funkcji](../images/5-monitor-function.png)

### <a name="log-window"></a>Okno dziennika
Do funkcji możesz także dodać instrukcje dziennika. Te instrukcje będą wyświetlane w oknie dziennika funkcji. Okno dziennika znajduje się w wysuwanym menu z kartami w dolnej części okna kodu. Korzystając z funkcji opartej na języku JavaScript, instrukcję dziennika należy dodać, używając następującej składni:
```javascript
  context.log('Enter your logging statement here');
```  
![Okno dziennika](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>Okno błędów i ostrzeżeń
Karta okna błędów i ostrzeżeń znajduje się w tym samym manu wysuwanym, co okno dziennika. W tym oknie są wyświetlane błędy kompilacji i ostrzeżenia w kodzie. Ponieważ kod JavaScript jest językiem dynamicznym i interpretowanym, na poniższej ilustracji przedstawiono błąd kompilacji w funkcji języka C#.  
![Okno błędów i ostrzeżeń](../images/5-errors-window.png)
