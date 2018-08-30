Zostanie uruchomiona aplikacja mobilna i utworzona wstępna wersja funkcji platformy Azure. W tej jednostce możesz wywołać funkcję platformy Azure z poziomu aplikacji mobilnej, przekazując lokalizację użytkownika i listę numerów telefonów, na które mają być wysyłane wiadomości SMS.

## <a name="calling-the-azure-function-from-the-mobile-app"></a>Wywoływanie funkcji platformy Azure z poziomu aplikacji mobilnej

1. Otwórz klasę `MainViewModel`.

2. W tej klasie dodaj pole prywatne `HttpClient` o nazwie `client`. Konieczne będzie dodanie odwołania do przestrzeni nazw `System.Net.Http`.

    ```cs
    HttpClient client = new HttpClient();
    ```

3. Dodaj pole stałej na potrzeby podstawowego adresu URL dla tej funkcji. Ustaw je na adres, na którym nasłuchuje lokalne środowisko uruchomieniowe usługi Azure Functions. Po wdrożeniu funkcji na platformie Azure tę zmienną można zmienić na adres URL platformy Azure.

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. Wewnątrz metody `SendLocation` po odnalezieniu lokalizacji utwórz nowe wystąpienie klasy `PostData` przy użyciu lokalizacji i listy numerów telefonów wprowadzonej przez użytkownika. Konieczne będzie dodanie dyrektywy using dla przestrzeni nazw `ImHere.Data`.

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > Przyjęto w związku z tym założenie, że numery telefonów wprowadzono w prawidłowym formacie — jeden na wiersz w kontrolce `Editor`. W aplikacji produkcyjnej miałaby w tej sytuacji miejsce weryfikacja w celu sprawdzenia, czy wprowadzono co najmniej jeden numer telefonu i był on w poprawnym formacie.

5. Najprostszym sposobem serializacji danych `PostData` w formacie JSON jest użycie pakietu NuGet Newtonsoft.JSON. Dodaj pakiet NuGet do projektu `ImHere` w taki sam sposób, jak dodano pakiet Xamarin.Essentials we wcześniejszej jednostce.

6. Serializowanie danych `PostData` do danych typu `string` przy użyciu klasy statycznej `JsonConvert`. Konieczne będzie dodanie dyrektywy using dla przestrzeni nazw `Newtonsoft.Json`. Zakoduj ten ciąg do klasy `StringContent`, aby mógł on zostać przekazany do funkcji platformy Azure w formacie JSON.

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. Opublikuj te dane w funkcji i uzyskaj wynik.

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   Dostęp do funkcji platformy Azure odbywa się za pomocą parametru `/api/<function name>`, więc zakładając, że port wybrany przez lokalne środowisko uruchomieniowe usługi Functions to 7071, funkcja `SendLocation` będzie dostępna pod adresem `http://localhost:7071/api/SendLocation`.

8. W zależności od wyniku wyświetl komunikat w interfejsie użytkownika.

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

Pełny kod dla nowych pól i metoda `SendLocation` znajduje się poniżej.

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a>Testowanie

1. Sprawdź, czy funkcja platformy Azure nadal działa lokalnie, a port jest zgodny z metodą `SendLocation`.

2. Ustaw aplikację platformy uniwersalnej systemu Windows jako aplikację startową i uruchom ją. Kliknij przycisk **Wyślij lokalizację**. W oknie konsoli środowiska uruchomieniowego usługi Functions zostaną wyświetlone dane wyjściowe zawierające wywoływaną funkcję oraz zarejestrowane dane przedstawiające wygenerowany adres URL.

    ![Dane wyjściowe wywoływanej funkcji](../media-drafts/6-function-called.png)

3. Aby przetestować generowanie adresu URL, wklej go z poziomu konsoli do przeglądarki. Powinna zostać wyświetlona Twoja bieżąca lokalizacja.

## <a name="summary"></a>Podsumowanie

W tej jednostce pokazaliśmy Ci, jak wywołać funkcję platformy Azure z poziomu aplikacji mobilnej. Za pomocą tego wywołania przekazano lokalizację użytkownika i numery telefonów wprowadzone w formacie JSON. W następnej jednostce powiążesz funkcję platformy Azure z usługą Twilio, aby wysłać tę lokalizację jako wiadomość SMS.