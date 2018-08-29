<span data-ttu-id="c4c1d-101">W ramach tego ćwiczenia będziemy pracować dalej z przykładem dotyczącym mechanizmu napędowego i dodamy logikę dla usługi temperatury.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="c4c1d-102">Ściślej mówiąc, będziemy odbierać dane z żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="c4c1d-103">Wymagania funkcji</span><span class="sxs-lookup"><span data-stu-id="c4c1d-103">Function requirements</span></span>
<span data-ttu-id="c4c1d-104">Najpierw zdefiniujemy kilka wymagań logiki:</span><span class="sxs-lookup"><span data-stu-id="c4c1d-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="c4c1d-105">temperatury z zakresu 0–25 powinny być oznaczone jako **OK**,</span><span class="sxs-lookup"><span data-stu-id="c4c1d-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="c4c1d-106">temperatury z zakresu 26–50 powinny być oznaczone jako **OSTRZEŻENIE**,</span><span class="sxs-lookup"><span data-stu-id="c4c1d-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="c4c1d-107">temperatury powyżej 50 powinny być oznaczone jako **NIEBEZPIECZEŃSTWO**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="adding-a-function-to-an-azure-function-app"></a><span data-ttu-id="c4c1d-108">Dodawanie funkcji do aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c4c1d-108">Adding a function to an Azure function app</span></span>

<span data-ttu-id="c4c1d-109">Jak już wiesz, platforma Azure zawiera elementy ułatwiające rozpoczynanie pracy z usługą Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-109">As we have already learned, Azure provides a helping hand when you're learning how to work with Azure Functions.</span></span> <span data-ttu-id="c4c1d-110">Doskonałą opcją dla osób rozpoczynających przygodę z funkcjami jest wygenerowanie funkcji na podstawie jednego z wielu dostępnych szablonów.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-110">One great feature to get your feet wet with Functions is to generate one using one of many templates.</span></span> <span data-ttu-id="c4c1d-111">W tym ćwiczeniu użyjesz szablonu HttpTrigger w celu wdrożenia usługi temperatury.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-111">In this exercise, you will be using the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="c4c1d-112">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com) przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-112">Sign in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
1. <span data-ttu-id="c4c1d-113">Przejdź do grupy zasobów utworzonej w pierwszym ćwiczeniu, wybierając pozycję **Wszystkie zasoby** w menu po lewej stronie, a następnie wybierając pozycję **escalator-functions-group**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-113">Access the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="c4c1d-114">Zostaną wyświetlone zasoby należące do grupy.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-114">The resources for the group will then be displayed.</span></span> <span data-ttu-id="c4c1d-115">Przejdź do aplikacji funkcji utworzonej w poprzednim ćwiczeniu, wybierając element **escalator-functions-xxxxxxx** (oznaczony ikoną pioruna).</span><span class="sxs-lookup"><span data-stu-id="c4c1d-115">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="c4c1d-116">![Przechodzenie do aplikacji funkcji](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-116">![Access the function app](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="c4c1d-117">W bloku zostanie wyświetlone omówienie aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-117">The blade will show an overview of your function app.</span></span> <span data-ttu-id="c4c1d-118">Po lewej stronie znajduje się drzewo nawigacji, zawierające wszystkie zdefiniowane funkcje, serwery proxy i miejsca.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-118">There is also a navigation tree on the left that shows any functions, proxies or slots that are defined.</span></span> <span data-ttu-id="c4c1d-119">Ponieważ nie utworzyliśmy jeszcze funkcji, będzie ono puste.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-119">We don't have a function yet, so this  will be empty.</span></span> <span data-ttu-id="c4c1d-120">Aby utworzyć funkcję, umieść wskaźnik myszy na pozycji **Funkcja** w drzewie nawigacji i kliknij wyświetlony przycisk **+**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-120">To create a function, move your mouse over **Function** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="c4c1d-121">![Dodawanie funkcji w drzewie nawigacji](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-121">![Add function navigation](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="c4c1d-122">W formularzu szybkiego rozpoczynania pracy przy użyciu gotowej funkcji wybierz link **Funkcja niestandardowa** w sekcji **Rozpocznij pracę samodzielnie**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-122">In the quickstart premade function form, select the **Custom function** link in the **Get started on your own** section.</span></span>
  <span data-ttu-id="c4c1d-123">![Formularz gotowej funkcji](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-123">![Premade function form](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="c4c1d-124">Zostanie wyświetlona lista szablonów.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-124">You are now presented with a list of templates.</span></span> <span data-ttu-id="c4c1d-125">Wybierz szablon wyzwalacza HTTP z wdrożeniem JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-125">Select the JavaScript implementation of the HTTP trigger template.</span></span>
  <span data-ttu-id="c4c1d-126">![Szablon wyzwalacza HTTP](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-126">![HTTP trigger template](../images/6-httptrigger-template.png)</span></span>
1. <span data-ttu-id="c4c1d-127">Zostanie wyświetlony blok, w którym możesz zdefiniować funkcję generowaną za pomocą szablonu.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-127">A blade will appear, allowing you to define what the template will generate.</span></span> <span data-ttu-id="c4c1d-128">W tym przypadku chcesz wygenerować funkcję w języku JavaScript o nazwie **DriveGearTemperatureService**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-128">In this case, you are interested in generating a JavaScript function named **DriveGearTemperatureService**.</span></span> <span data-ttu-id="c4c1d-129">Po wpisaniu nazwy funkcji naciśnij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-129">After you have named your function, press the **Create** button.</span></span>
  <span data-ttu-id="c4c1d-130">![Formularz tworzenia wyzwalacza HTTP](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-130">![Create HTTP trigger form](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="c4c1d-131">Po chwili zobaczysz utworzony za pomocą szablonu kod źródłowy funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-131">After a few moments, you will be presented with the templated source code for your function.</span></span> <span data-ttu-id="c4c1d-132">Gotowa funkcja wymaga wprowadzenia imienia i zwraca ciąg **Hello, {imię}** (Witaj).</span><span class="sxs-lookup"><span data-stu-id="c4c1d-132">The premade function expects a name to be passed in, and it will return **Hello, {name}**.</span></span>

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

1. <span data-ttu-id="c4c1d-133">Po prawej stronie kodu źródłowego zobaczysz dwie karty.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-133">On the right-hand side of the source view, you will see two tabs.</span></span> <span data-ttu-id="c4c1d-134">Na karcie **Wyświetl pliki** możesz wyświetlić wszystkie pliki używane przez funkcję. Aby wyświetlić konfigurację funkcji, wybierz plik **function.json**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-134">You are able to view all the files supporting the function in the **View files** tab. You can select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="c4c1d-135">Zobaczysz w nim zdefiniowany element httpTrigger oraz powiązanie wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-135">Here you can see the httpTrigger defined, as well as the output binding.</span></span> <span data-ttu-id="c4c1d-136">Ta konfiguracja określa, że funkcja jest wyzwalana przez żądanie HTTP, a powiązanie wyjściowe wskazuje, że odpowiedź jest wysyłana jako odpowiedź HTTP.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-136">This configuration describes that the function is initiated by an HTTP request, and the output binding describes that the response will be sent as an HTTP response.</span></span>

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

## <a name="running-the-premade-azure-function"></a><span data-ttu-id="c4c1d-137">Uruchamianie gotowej funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c4c1d-137">Running the premade Azure function</span></span>

<span data-ttu-id="c4c1d-138">Aby uruchomić funkcję, możesz zainicjować żądanie HTTP za pomocą narzędzia cURL w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-138">To run the function, you can initiate an HTTP request from cURL from a command prompt.</span></span> <span data-ttu-id="c4c1d-139">Aby znaleźć adres URL punktu końcowego, wróć do kodu funkcji i wybierz link **Pobierz adres URL funkcji**.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-139">To find the endpoint URL, return to your function code and select the **Get function URL** link.</span></span> <span data-ttu-id="c4c1d-140">Skopiuj ten link do schowka.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-140">Copy this link to your clipboard.</span></span>  <span data-ttu-id="c4c1d-141">Adres URL powinien być podobny do następującego: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Uzyskiwanie adresu URL punktu końcowego](../images/6-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-141">Your URL should look something similar to the following: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Get endpoint URL](../images/6-get-function-url.png)</span></span>

<span data-ttu-id="c4c1d-142">Używając tego adresu URL, uruchom polecenie cURL, aby zainicjować funkcję (zastępując adres URL własnym):</span><span class="sxs-lookup"><span data-stu-id="c4c1d-142">With that URL, run a cURL command to initiate your function (replacing the URL with your own):</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Odpowiedź gotowej funkcji na polecenie cURL](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a><span data-ttu-id="c4c1d-144">Dodawanie logiki biznesowej do funkcji</span><span class="sxs-lookup"><span data-stu-id="c4c1d-144">Adding business logic to the function</span></span>

<span data-ttu-id="c4c1d-145">Nasza funkcja oczekuje tablicy odczytów temperatury przesłanych przez klienta.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-145">Our function is expecting an array of temperature readings from the customer.</span></span> <span data-ttu-id="c4c1d-146">Przykładowa treść żądania może być następująca:</span><span class="sxs-lookup"><span data-stu-id="c4c1d-146">This is an example of the request body:</span></span>

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

<span data-ttu-id="c4c1d-147">Zmodyfikuj kod gotowej funkcji, aby zaimplementować odpowiednią logikę biznesową.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-147">Modify the premade function code to implement the required business logic.</span></span> <span data-ttu-id="c4c1d-148">Otwórz plik index.js i zastąp go poniższą treścią:</span><span class="sxs-lookup"><span data-stu-id="c4c1d-148">Open the index.js file, and replace it with the following listing:</span></span>

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

<span data-ttu-id="c4c1d-149">Zwróć uwagę na informacje w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-149">Notice the log statements.</span></span> <span data-ttu-id="c4c1d-150">Po uruchomieniu funkcji w oknie dziennika będą dodawane komunikaty.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-150">When the function runs, they will add messages in the log window.</span></span>

## <a name="testing-your-business-logic"></a><span data-ttu-id="c4c1d-151">Testowanie logiki biznesowej</span><span class="sxs-lookup"><span data-stu-id="c4c1d-151">Testing your business logic</span></span>

<span data-ttu-id="c4c1d-152">Otwórz okno testowania za pomocą menu wysuwanego po prawej stronie, a następnie wklej przykładowe żądanie podane powyżej w polu tekstowym treści żądania.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-152">Open the test window from the right-hand side flyout menu, and paste the sample request from above into the request body text box.</span></span> <span data-ttu-id="c4c1d-153">Naciśnij przycisk **Uruchom** i sprawdź dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-153">Press the **Run** button and view the output.</span></span> <span data-ttu-id="c4c1d-154">Możesz również otworzyć okno dziennika z menu wysuwanego na dole, aby zobaczyć informacje rejestrowane w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-154">You can also open the log window from the bottom flyout menu to see the logging statements in the log.</span></span>
<span data-ttu-id="c4c1d-155">![Testowanie logiki biznesowej](../images/6-portal-testing.png) Dane JSON w oknie danych wyjściowych wskazują, że do każdego z odczytów zostało prawidłowo dodane pole określające stan temperatury.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-155">![Testing the business Logic](../images/6-portal-testing.png) You can see from the JSON data in the output window that our temperature status field has been added to each of the readings correctly.</span></span> <span data-ttu-id="c4c1d-156">Możesz również przejść do pulpitu nawigacyjnego monitorowania, gdzie zobaczysz, że żądanie zostało zarejestrowane w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c4c1d-156">You may also visit the Monitor dashboard to see that the request has been logged to Application Insights.</span></span>
<span data-ttu-id="c4c1d-157">![Żądanie w usłudze Application Insights](../images/6-app-insights.png)</span><span class="sxs-lookup"><span data-stu-id="c4c1d-157">![Request in Application Insights](../images/6-app-insights.png)</span></span>
