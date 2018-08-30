W tym momencie aplikacja mobilna jest kompletna i wysyła lokalizację użytkownika i listę numerów telefonów do funkcji platformy Azure, która może deserializować te dane. W tej sekcji powiążesz funkcję platformy Azure z usługą Twilio na potrzeby wysyłania wiadomości SMS.

Usługę Azure Functions można połączyć z innymi usługami — na platformie Azure lub innych firm. Te połączenia, nazywane powiązaniami, mają dwie postacie: powiązań wejściowych i wyjściowych. Powiązania wejściowe udostępniają dane funkcji, a powiązania wyjściowe pobierają dane z funkcji i wysyłają je do innej usługi. Informacje o powiązaniach są dostępne w [dokumentacji powiązań usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

Powiązania usługi Azure Functions tworzone w programie Visual Studio są definiowane przy użyciu parametrów funkcji dekorowanej atrybutami.

## <a name="bind-the-azure-function-to-twilio"></a>Powiązanie funkcji platformy Azure z usługą Twilio

Wysyłanie wiadomości SMS za pośrednictwem usługi Twilio wymaga powiązania wyjściowego skonfigurowanego przy użyciu identyfikatora subskrypcji konta (SID) i tokenu uwierzytelniania.

1. Zatrzymaj lokalne środowisko uruchomieniowe usługi Azure Functions, jeśli nadal działa po uruchomieniu w poprzednim module.

2. Dodaj pakiet NuGet „Microsoft.Azure.WebJobs.Extensions.Twilio” do projektu `ImHere.Functions`. Ten pakiet NuGet zawiera odpowiednie klasy dla powiązania.

3. Dodaj nowy parametr do metody statycznej `Run` w klasie statycznej `SendLocation`, określając dla niego nazwę `messages`. Typ tego parametru to `ICollector<SMSMessage>`. Będzie konieczne dodanie dyrektywy using dla przestrzeni nazw `Twilio`.

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. Udekoruj nowy parametr `messages` za pomocą atrybutu `TwilioSms`. Ten atrybut ma trzy parametry, które należy ustawić.

    | Ustawienie      |  Wartość   | Opis                                        |
    | --- | --- | ---|
    | **AccountSidSetting** | „TwilioAccountSid” | Identyfikator SID dla konta usługi Twilio. Ten parametr jest nazwą wartości ustawień aplikacji funkcji, które będzie używana do pobierania identyfikatora SID zamiast bezpośredniego ustawiania identyfikatora SID. |
    | **AuthTokenSetting** | „TwilioAuthToken” | Token uwierzytelniania dla konta usługi Twilio. Ten parametr jest nazwą wartości ustawień aplikacji funkcji, która będzie używana do pobierania tokenu uwierzytelniania zamiast bezpośredniego ustawiania tokenu uwierzytelniania. |
    | **From** | Twój numer telefonu w usłudze Twilio | Numer telefonu w usłudze Twilio używany jako numer źródłowy wiadomości SMS określony w formacie międzynarodowym (+\<numer kierunkowy kraju\>\<numer telefonu\>, na przykład „+4855123456”). |

    Podczas tworzenia konta usługi Twilio jest przypisywany numer telefonu, z którego można wysyłać wiadomości. Ten numer telefonu możesz znaleźć na pulpicie nawigacyjnym **Phone Numbers** (Numery telefonów) usługi Twilio. W witrynie usługi Twilio wybierz wielokropek u dołu menu po lewej stronie. Następnie wybierz pozycję *SUPER NETWORK->Phone Numbers* (Sieć SUPER->Numery telefonów). Możesz przypiąć ten pulpit nawigacyjny do menu po lewej stronie przy użyciu ikony pinezki. Twój numer Twilio będzie wyświetlony w obszarze *Manage Numbers->Active Numbers* (Zarządzaj numerami->Numery aktywne). Należy usunąć wszystkie spacje z numeru.

    ![Znajdowanie swojego numeru w usłudze Twilio](../media-drafts/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. Ustawienia aplikacji funkcji można skonfigurować lokalnie w pliku `local.settings.json`. Dodaj identyfikator SID konta usługi Twilio i token uwierzytelniania do tego pliku JSON, używając nazw ustawień przekazanych do atrybutu `TwilioSMS`.

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

    Zastąp wartości \<Your SID\> (Twój identyfikator SID) i \<Your Auth Token\> (Twój token uwierzytelniania) wartościami z pulpitu nawigacyjnego usługi Twilio.

    > Te ustawienia lokalne będą dotyczyć tylko uruchamiania lokalnego. W aplikacji produkcyjnej te wartości będą poświadczeniami lokalnego konta deweloperskiego lub testowego. Po wdrożeniu usługi Azure Functions na platformie Azure będzie można skonfigurować wartości produkcyjne.
    > Jeśli zaewidencjonujesz kod w kontroli źródła, wartości lokalnych ustawień aplikacji zostaną także zaewidencjonowane. Należy zatem uważać, aby nie zaewidencjonować żadnych rzeczywistych wartości w tych plikach, jeśli kod jest typu open source lub jest w jakikolwiek sposób publiczny.

## <a name="create-the-sms-messages"></a>Tworzenie wiadomości SMS

Parametr `ICollector<SMSMessage>` to kolekcja wystąpień `SMSMessage` używana do gromadzenia wiadomości SMS do wysłania. Po zakończeniu wykonywania funkcji wszystkie wystąpienia `SMSMessage` dodane do tej kolekcji są przekazywane do usługi Twilio i wysyłane do odpowiednich odbiorców.

1. W funkcji `SendLocation` dodaj kod iterujący numery telefonów w obiekcie `PostData` i tworzący wiadomość SMS dla każdego z nich.

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

    Wysłanie wiadomości wymaga docelowego numeru telefonu i treści zawierającej adres URL usługi Mapy Google utworzony na podstawie lokalizacji użytkownika.

2. Zarejestruj każdą wiadomość, a następnie dodaj ją do kolekcji `messages`.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

Poniżej przedstawiono kompletną metodę `SendLocation`.

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

## <a name="test-it-out"></a>Testowanie działania

1. Ustaw aplikację `ImHere.Functions` jako projekt startowy i uruchom ją bez debugowania.

2. Ustaw aplikację `ImHere.UWP` jako projekt startowy i uruchom ją.

3. Podaj własny numer telefonu w formacie międzynarodowym (+\<numer kierunkowy kraju\>\<numer telefonu\>) w aplikacji platformy Xamarin.Forms. Konto usługi Twilio w wersji próbnej umożliwia wysyłanie wiadomości tylko na zweryfikowane numery telefonów, więc na razie będzie możliwe tylko wysyłanie wiadomości na Twój numer, chyba że uaktualnisz konto do konta płatnego lub zweryfikujesz inne numery.

4. Kliknij przycisk **Send Location** (Wyślij lokalizację). Jeśli wiadomość SMS została wysłana pomyślnie, zobaczysz w aplikacji platformy Xamarin.Forms komunikat „Location sent successfully” („Lokalizacja została wysłana pomyślnie”).

    ![Aplikacja platformy Xamarin.Forms pokazująca lokalizację jako wysłaną](../media-drafts/7-ui-location-sent.png)

5. W dziennikach konsoli funkcji platformy Azure zobaczysz, że wiadomość została utworzona i wysyłana. Jeśli wystąpią jakiekolwiek błędy (takie jak niepoprawny format numeru), zostaną zarejestrowane tutaj.

    ![Konsola funkcji platformy Azure pokazująca, że wiadomość została wysłana](../media-drafts/7-function-message-sent.png)

6. Sprawdź na telefonie, czy nadeszła wiadomość. Użyj linku w wiadomości, aby wyświetlić swoją lokalizację.

    ![Wiadomość SMS odebrana na telefonie komórkowym](../media-drafts/7-message-received.png)

## <a name="summary"></a>Podsumowanie

W tej sekcji przedstawiono sposób tworzenia powiązania usługi Twilio dla funkcji platformy Azure i wysyłania wiadomości SMS z lokalizacją użytkownika do funkcji uruchomionej lokalnie. W następnej sekcji opublikujesz funkcję na platformie Azure.