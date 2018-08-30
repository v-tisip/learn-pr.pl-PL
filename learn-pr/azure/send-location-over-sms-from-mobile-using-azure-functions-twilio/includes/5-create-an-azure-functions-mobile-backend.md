W tym momencie aplikacja pracuje nad uzyskaniem lokalizacji użytkownika i jest gotowa do wysłania do funkcji platformy Azure. W tym rozdziale utworzysz funkcję platformy Azure.

## <a name="create-an-azure-functions-project"></a>Tworzenie projektu usługi Azure Functions

1. Dodaj nowy projekt do rozwiązania `ImHere`, klikając prawym przyciskiem myszy rozwiązanie i wybierając polecenie *Dodaj -> Nowy projekt*.

2. W drzewie po lewej stronie wybierz pozycję *Visual C# -> Chmura*, a następnie pozycję *Azure Functions* z panelu w środku.

3. Nadaj projektowi nazwę „ImHere.Functions”, a następnie kliknij przycisk **OK**.

    ![Okno dialogowe Dodaj nowy projekt](../media-drafts/5-add-new-functions-project.png)

4. W oknie dialogowym konfiguracji **Nowy projekt** jako ustawienie wersji usługi Functions zostaw *Azure Functions v1 (.NET Framework)*. Wybierz pozycję *Wyzwalacz protokołu HTTP*, jako ustawienie konta magazynu zostaw *Emulator magazynu*, a następnie ustaw uprawnienia dostępu na *Anonimowy*. Następnie kliknij przycisk **OK**.

    ![Okno dialogowe konfiguracji projektu usługi Azure Functions](../media-drafts/5-configure-trigger.png)

Zostanie utworzony nowy projekt z domyślną funkcją o nazwie `Function1`.

> Ta funkcja została utworzona z dostępem anonimowym. Po opublikowaniu tej funkcji na platformie Azure każdy, kto zna adres URL, będzie mógł ją wywołać. W rzeczywistym scenariuszu powinna ona być chroniona za pomocą jakiejś formy uwierzytelniania, takiej jak [Uwierzytelnianie usługi Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) czy [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).

## <a name="create-the-function"></a>Tworzenie funkcji

Projekt usługi Azure Functions jest tworzony z pojedynczą funkcją wyzwalacza HTTP o nazwie `Function1`. Sama funkcja jest implementowana jako statyczna metoda `Run` w klasie `Function1`.

1. W Eksploratorze rozwiązań zmień nazwę pliku z „Function1.cs” na „SendLocation.cs”. Po wyświetleniu monitu o zmianę nazw wszystkich odwołań do elementu kodu `Function1` kliknij przycisk **Tak**.

2. Zmień nazwę funkcji w atrybucie na „SendLocation”.

    ```cs
    [FunctionName("SendLocation")]
    ```

3. Usuń zawartość funkcji, z wyjątkiem pierwszego wiersza, który zapisuje komunikat z informacjami w rejestratorze.

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>Tworzenie klasy umożliwiającej udostępnianie danych między aplikacją mobilną i funkcją

Dane są przesyłane do funkcji platformy Azure w formacie JSON. Aplikacja mobilna serializuje dane do formatu JSON, a funkcja deserializuje te dane z formatu JSON. Aby zachować spójność tych danych między aplikacją mobilną i funkcją, utwórz nowy projekt, który będzie zawierał klasę umożliwiającą przechowywanie danych o lokalizacji i numerze telefonu. Aplikacja i funkcja będą odwoływały się do tego projektu.

1. Utwórz nowy projekt w ramach rozwiązania `ImHere`, klikając prawym przyciskiem myszy rozwiązanie i wybierając polecenie *Dodaj -> Nowy projekt*.

2. W drzewie po lewej stronie wybierz pozycję *Visual C# -> .NET Standard*, a następnie pozycję *Biblioteka klas (.NET Standard)* z panelu w środku.

3. Nadaj projektowi nazwę „ImHere.Data”, a następnie kliknij przycisk **OK**.

    ![Okno dialogowe Dodaj nowy projekt](../media-drafts/5-add-new-net-standard-project.png)

4. Usuń wygenerowany automatycznie plik „Class1.cs”.

5. Utwórz nową klasę w projekcie `ImHere.Data` o nazwie `PostData`, klikając prawym przyciskiem myszy projekt, a następnie wybierając pozycję *Dodaj -> Klasa*. Nadaj nowej klasie nazwę „PostData”, a następnie kliknij przycisk **OK**.

6. Dodaj właściwości `double` dla szerokości i długości geograficznej, a także właściwość `string[]` dla numerów telefonów, na które mają być wysyłane dane.

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. Dodaj odwołanie do tego projektu do obu projektów (`ImHere.Functions` i `ImHere`), klikając projekt prawym przyciskiem myszy, a następnie wybierając pozycję *Dodaj -> Odwołanie*. W drzewie po lewej stronie wybierz pozycję *Projekty*, a następnie zaznacz pole wyboru obok pozycji *ImHere.Data*.

    ![Konfigurowanie odwołań do projektu](../media-drafts/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>Odczytywanie danych wysłanych do funkcji

W funkcji Azure parametr `req` zawiera wykonane żądanie HTTP, a dane w tym żądaniu są obiektem `PostData` zserializowanym do formatu JSON.

1. Otwórz klasę `SendLocation` w projekcie `ImHere.Functions`.

2. Odczytaj zawartość żądania HTTP do obiektu `PostData`, dodając dyrektywę użycia dla przestrzeni nazw `ImHere.Data`.

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. Skonstruuj adres URL aplikacji Mapy Google, używając szerokości i długości geograficznej z obiektu `PostData`.

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. Zarejestruj adres URL.

    ```cs
    log.Info($"URL created - {url}");
    ```

5. Zwróć kod stanu 200, aby pokazać, że funkcja została wykonana bez błędu.

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

Poniżej przedstawiono kompletną funkcję.

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a>Uruchamianie funkcji platformy Azure w środowisku lokalnym

Funkcje można uruchamiać lokalnie za pomocą lokalnego konta magazynu i lokalnego środowiska uruchomieniowego usługi Azure Functions. Lokalne środowisko uruchomieniowe umożliwia przetestowanie funkcji przed jej wdrożeniem na platformie Azure.

1. W eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt `ImHere.Functions`, a następnie wybierz pozycję *Ustaw jako projekt startowy*.

2. Z menu *Debuguj* wybierz pozycję *Uruchom bez debugowania*. Lokalne środowisko uruchomieniowe usługi Azure Functions zostanie uruchomione w oknie konsoli i uruchomi funkcję, nasłuchując na dostępnym porcie na komputerze `localhost`.

    ![Funkcja platformy Azure uruchomiona w środowisku lokalnym](../media-drafts/5-function-running-locally.png)

3. Zanotuj numer portu, na którym nasłuchuje funkcja. Będzie on potrzebny w następnym rozdziale do przetestowania aplikacji mobilnej. Na powyższej ilustracji funkcja nasłuchuje na porcie **7071**.

    ```sh
    Listening on http://localhost:7071/
    ```

4. Pozostaw funkcję uruchomioną, aby przetestować aplikację mobilną w następnym rozdziale.

## <a name="summary"></a>Podsumowanie

W tym rozdziale pokazaliśmy, jak utworzyć projekt usługi Azure Functions w programie Visual Studio, dodaliśmy projekt udostępniony z obiektem danych, który ma być współużytkowany między aplikacją mobilną i funkcją, oraz przedstawiliśmy sposób tworzenia podstawowego wdrożenia funkcji w celu deserializacji przekazanych danych. Pokazaliśmy również, jak uruchomić funkcję platformy Azure w środowisku lokalnym. W następnym rozdziale wywołasz funkcję platformy Azure z poziomu aplikacji mobilnej.