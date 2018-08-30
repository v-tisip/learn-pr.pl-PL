<span data-ttu-id="5f602-101">W tym momencie aplikacja mobilna jest kompletna i wysyła lokalizację użytkownika i listę numerów telefonów do funkcji platformy Azure, która może deserializować te dane.</span><span class="sxs-lookup"><span data-stu-id="5f602-101">At this point, the mobile app is complete and sends the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="5f602-102">W tej sekcji powiążesz funkcję platformy Azure z usługą Twilio na potrzeby wysyłania wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="5f602-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="5f602-103">Usługę Azure Functions można połączyć z innymi usługami — na platformie Azure lub innych firm.</span><span class="sxs-lookup"><span data-stu-id="5f602-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="5f602-104">Te połączenia, nazywane powiązaniami, mają dwie postacie: powiązań wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5f602-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="5f602-105">Powiązania wejściowe udostępniają dane funkcji, a powiązania wyjściowe pobierają dane z funkcji i wysyłają je do innej usługi.</span><span class="sxs-lookup"><span data-stu-id="5f602-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="5f602-106">Informacje o powiązaniach są dostępne w [dokumentacji powiązań usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span><span class="sxs-lookup"><span data-stu-id="5f602-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

<span data-ttu-id="5f602-107">Powiązania usługi Azure Functions tworzone w programie Visual Studio są definiowane przy użyciu parametrów funkcji dekorowanej atrybutami.</span><span class="sxs-lookup"><span data-stu-id="5f602-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="5f602-108">Powiązanie funkcji platformy Azure z usługą Twilio</span><span class="sxs-lookup"><span data-stu-id="5f602-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="5f602-109">Wysyłanie wiadomości SMS za pośrednictwem usługi Twilio wymaga powiązania wyjściowego skonfigurowanego przy użyciu identyfikatora subskrypcji konta (SID) i tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5f602-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="5f602-110">Zatrzymaj lokalne środowisko uruchomieniowe usługi Azure Functions, jeśli nadal działa po uruchomieniu w poprzednim module.</span><span class="sxs-lookup"><span data-stu-id="5f602-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="5f602-111">Dodaj pakiet NuGet „Microsoft.Azure.WebJobs.Extensions.Twilio” do projektu `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="5f602-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="5f602-112">Ten pakiet NuGet zawiera odpowiednie klasy dla powiązania.</span><span class="sxs-lookup"><span data-stu-id="5f602-112">This NuGet package contains the relevant classes for the binding.</span></span>

3. <span data-ttu-id="5f602-113">Dodaj nowy parametr do metody statycznej `Run` w klasie statycznej `SendLocation`, określając dla niego nazwę `messages`.</span><span class="sxs-lookup"><span data-stu-id="5f602-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="5f602-114">Typ tego parametru to `ICollector<SMSMessage>`.</span><span class="sxs-lookup"><span data-stu-id="5f602-114">This parameter will have a type of `ICollector<SMSMessage>`.</span></span> <span data-ttu-id="5f602-115">Będzie konieczne dodanie dyrektywy using dla przestrzeni nazw `Twilio`.</span><span class="sxs-lookup"><span data-stu-id="5f602-115">You'll need to add a using directive for the `Twilio` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. <span data-ttu-id="5f602-116">Udekoruj nowy parametr `messages` za pomocą atrybutu `TwilioSms`.</span><span class="sxs-lookup"><span data-stu-id="5f602-116">Decorate the new `messages` parameter with the `TwilioSms` attribute.</span></span> <span data-ttu-id="5f602-117">Ten atrybut ma trzy parametry, które należy ustawić.</span><span class="sxs-lookup"><span data-stu-id="5f602-117">This attribute has three parameters you need to set.</span></span>

    | <span data-ttu-id="5f602-118">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="5f602-118">Setting</span></span>      |  <span data-ttu-id="5f602-119">Wartość</span><span class="sxs-lookup"><span data-stu-id="5f602-119">Value</span></span>   | <span data-ttu-id="5f602-120">Opis</span><span class="sxs-lookup"><span data-stu-id="5f602-120">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="5f602-121">**AccountSidSetting**</span><span class="sxs-lookup"><span data-stu-id="5f602-121">**AccountSidSetting**</span></span> | <span data-ttu-id="5f602-122">„TwilioAccountSid”</span><span class="sxs-lookup"><span data-stu-id="5f602-122">"TwilioAccountSid"</span></span> | <span data-ttu-id="5f602-123">Identyfikator SID dla konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="5f602-123">The SID for your Twilio account.</span></span> <span data-ttu-id="5f602-124">Ten parametr jest nazwą wartości ustawień aplikacji funkcji, które będzie używana do pobierania identyfikatora SID zamiast bezpośredniego ustawiania identyfikatora SID.</span><span class="sxs-lookup"><span data-stu-id="5f602-124">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> |
    | <span data-ttu-id="5f602-125">**AuthTokenSetting**</span><span class="sxs-lookup"><span data-stu-id="5f602-125">**AuthTokenSetting**</span></span> | <span data-ttu-id="5f602-126">„TwilioAuthToken”</span><span class="sxs-lookup"><span data-stu-id="5f602-126">"TwilioAuthToken"</span></span> | <span data-ttu-id="5f602-127">Token uwierzytelniania dla konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="5f602-127">The Auth Token for your Twilio account.</span></span> <span data-ttu-id="5f602-128">Ten parametr jest nazwą wartości ustawień aplikacji funkcji, która będzie używana do pobierania tokenu uwierzytelniania zamiast bezpośredniego ustawiania tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5f602-128">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> |
    | <span data-ttu-id="5f602-129">**From**</span><span class="sxs-lookup"><span data-stu-id="5f602-129">**From**</span></span> | <span data-ttu-id="5f602-130">Twój numer telefonu w usłudze Twilio</span><span class="sxs-lookup"><span data-stu-id="5f602-130">Your Twilio phone number</span></span> | <span data-ttu-id="5f602-131">Numer telefonu w usłudze Twilio używany jako numer źródłowy wiadomości SMS określony w formacie międzynarodowym (+\<numer kierunkowy kraju\>\<numer telefonu\>, na przykład „+4855123456”).</span><span class="sxs-lookup"><span data-stu-id="5f602-131">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span> |

    <span data-ttu-id="5f602-132">Podczas tworzenia konta usługi Twilio jest przypisywany numer telefonu, z którego można wysyłać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="5f602-132">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="5f602-133">Ten numer telefonu możesz znaleźć na pulpicie nawigacyjnym **Phone Numbers** (Numery telefonów) usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="5f602-133">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span> <span data-ttu-id="5f602-134">W witrynie usługi Twilio wybierz wielokropek u dołu menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5f602-134">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="5f602-135">Następnie wybierz pozycję *SUPER NETWORK->Phone Numbers* (Sieć SUPER->Numery telefonów).</span><span class="sxs-lookup"><span data-stu-id="5f602-135">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="5f602-136">Możesz przypiąć ten pulpit nawigacyjny do menu po lewej stronie przy użyciu ikony pinezki.</span><span class="sxs-lookup"><span data-stu-id="5f602-136">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="5f602-137">Twój numer Twilio będzie wyświetlony w obszarze *Manage Numbers->Active Numbers* (Zarządzaj numerami->Numery aktywne).</span><span class="sxs-lookup"><span data-stu-id="5f602-137">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span> <span data-ttu-id="5f602-138">Należy usunąć wszystkie spacje z numeru.</span><span class="sxs-lookup"><span data-stu-id="5f602-138">You'll need to remove any spaces from the number.</span></span>

    ![Znajdowanie swojego numeru w usłudze Twilio](../media-drafts/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. <span data-ttu-id="5f602-140">Ustawienia aplikacji funkcji można skonfigurować lokalnie w pliku `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="5f602-140">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="5f602-141">Dodaj identyfikator SID konta usługi Twilio i token uwierzytelniania do tego pliku JSON, używając nazw ustawień przekazanych do atrybutu `TwilioSMS`.</span><span class="sxs-lookup"><span data-stu-id="5f602-141">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    <span data-ttu-id="5f602-142">Zastąp wartości \<Your SID\> (Twój identyfikator SID) i \<Your Auth Token\> (Twój token uwierzytelniania) wartościami z pulpitu nawigacyjnego usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="5f602-142">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > <span data-ttu-id="5f602-143">Te ustawienia lokalne będą dotyczyć tylko uruchamiania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5f602-143">These local settings will be only for running locally.</span></span> <span data-ttu-id="5f602-144">W aplikacji produkcyjnej te wartości będą poświadczeniami lokalnego konta deweloperskiego lub testowego.</span><span class="sxs-lookup"><span data-stu-id="5f602-144">In a production app, these value would be your local development or test account credentials.</span></span> <span data-ttu-id="5f602-145">Po wdrożeniu usługi Azure Functions na platformie Azure będzie można skonfigurować wartości produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="5f602-145">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>
    > <span data-ttu-id="5f602-146">Jeśli zaewidencjonujesz kod w kontroli źródła, wartości lokalnych ustawień aplikacji zostaną także zaewidencjonowane. Należy zatem uważać, aby nie zaewidencjonować żadnych rzeczywistych wartości w tych plikach, jeśli kod jest typu open source lub jest w jakikolwiek sposób publiczny.</span><span class="sxs-lookup"><span data-stu-id="5f602-146">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="5f602-147">Tworzenie wiadomości SMS</span><span class="sxs-lookup"><span data-stu-id="5f602-147">Create the SMS messages</span></span>

<span data-ttu-id="5f602-148">Parametr `ICollector<SMSMessage>` to kolekcja wystąpień `SMSMessage` używana do gromadzenia wiadomości SMS do wysłania.</span><span class="sxs-lookup"><span data-stu-id="5f602-148">The `ICollector<SMSMessage>` parameter is a collection of `SMSMessage` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="5f602-149">Po zakończeniu wykonywania funkcji wszystkie wystąpienia `SMSMessage` dodane do tej kolekcji są przekazywane do usługi Twilio i wysyłane do odpowiednich odbiorców.</span><span class="sxs-lookup"><span data-stu-id="5f602-149">After the function has finished running, any instances of `SMSMessage` added to this collection are passed to Twilio and sent to the relevant recipients.</span></span>

1. <span data-ttu-id="5f602-150">W funkcji `SendLocation` dodaj kod iterujący numery telefonów w obiekcie `PostData` i tworzący wiadomość SMS dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="5f602-150">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
    }
    ```

    <span data-ttu-id="5f602-151">Wysłanie wiadomości wymaga docelowego numeru telefonu i treści zawierającej adres URL usługi Mapy Google utworzony na podstawie lokalizacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5f602-151">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

2. <span data-ttu-id="5f602-152">Zarejestruj każdą wiadomość, a następnie dodaj ją do kolekcji `messages`.</span><span class="sxs-lookup"><span data-stu-id="5f602-152">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="5f602-153">Poniżej przedstawiono kompletną metodę `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="5f602-153">The complete `SendLocation` method is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                                AuthTokenSetting = "TwilioAuthToken",
                                                                From = "<your Twilio phone number>")]ICollector<SMSMessage> messages,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="test-it-out"></a><span data-ttu-id="5f602-154">Testowanie działania</span><span class="sxs-lookup"><span data-stu-id="5f602-154">Test it out</span></span>

1. <span data-ttu-id="5f602-155">Ustaw aplikację `ImHere.Functions` jako projekt startowy i uruchom ją bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="5f602-155">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

2. <span data-ttu-id="5f602-156">Ustaw aplikację `ImHere.UWP` jako projekt startowy i uruchom ją.</span><span class="sxs-lookup"><span data-stu-id="5f602-156">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

3. <span data-ttu-id="5f602-157">Podaj własny numer telefonu w formacie międzynarodowym (+\<numer kierunkowy kraju\>\<numer telefonu\>) w aplikacji platformy Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="5f602-157">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="5f602-158">Konto usługi Twilio w wersji próbnej umożliwia wysyłanie wiadomości tylko na zweryfikowane numery telefonów, więc na razie będzie możliwe tylko wysyłanie wiadomości na Twój numer, chyba że uaktualnisz konto do konta płatnego lub zweryfikujesz inne numery.</span><span class="sxs-lookup"><span data-stu-id="5f602-158">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

4. <span data-ttu-id="5f602-159">Kliknij przycisk **Send Location** (Wyślij lokalizację).</span><span class="sxs-lookup"><span data-stu-id="5f602-159">Click the **Send Location** button.</span></span> <span data-ttu-id="5f602-160">Jeśli wiadomość SMS została wysłana pomyślnie, zobaczysz w aplikacji platformy Xamarin.Forms komunikat „Location sent successfully” („Lokalizacja została wysłana pomyślnie”).</span><span class="sxs-lookup"><span data-stu-id="5f602-160">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying "Location sent successfully".</span></span>

    ![Aplikacja platformy Xamarin.Forms pokazująca lokalizację jako wysłaną](../media-drafts/7-ui-location-sent.png)

5. <span data-ttu-id="5f602-162">W dziennikach konsoli funkcji platformy Azure zobaczysz, że wiadomość została utworzona i wysyłana.</span><span class="sxs-lookup"><span data-stu-id="5f602-162">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="5f602-163">Jeśli wystąpią jakiekolwiek błędy (takie jak niepoprawny format numeru), zostaną zarejestrowane tutaj.</span><span class="sxs-lookup"><span data-stu-id="5f602-163">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![Konsola funkcji platformy Azure pokazująca, że wiadomość została wysłana](../media-drafts/7-function-message-sent.png)

6. <span data-ttu-id="5f602-165">Sprawdź na telefonie, czy nadeszła wiadomość.</span><span class="sxs-lookup"><span data-stu-id="5f602-165">Check your phone for a message.</span></span> <span data-ttu-id="5f602-166">Użyj linku w wiadomości, aby wyświetlić swoją lokalizację.</span><span class="sxs-lookup"><span data-stu-id="5f602-166">Follow the link in the message to see your location.</span></span>

    ![Wiadomość SMS odebrana na telefonie komórkowym](../media-drafts/7-message-received.png)

## <a name="summary"></a><span data-ttu-id="5f602-168">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5f602-168">Summary</span></span>

<span data-ttu-id="5f602-169">W tej sekcji przedstawiono sposób tworzenia powiązania usługi Twilio dla funkcji platformy Azure i wysyłania wiadomości SMS z lokalizacją użytkownika do funkcji uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="5f602-169">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="5f602-170">W następnej sekcji opublikujesz funkcję na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5f602-170">In the next unit, you publish the function to Azure.</span></span>