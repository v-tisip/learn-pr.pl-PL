Aplikacja ma interfejs użytkownika i model widoku (ViewModel). W tym module do modelu widoku (ViewModel) dodasz możliwość wyszukiwania lokalizacji przy użyciu zestawu Xamarin.Essentials.

## <a name="enable-location-permissions"></a>Włączanie uprawnień do lokalizacji

Wszystkie platformy mobilne zapewniają zabezpieczenia informacji o użytkowniku i niektórych elementów sprzętu, takich jak aparat, biblioteka zdjęć czy lokalizacja użytkownika. Zanim aplikacja będzie mogła uzyskiwać dostęp do lokalizacji użytkownika, użytkownik musi udzielić uprawnień — niejawnie podczas instalacji lub wybierając opcję udzielenia uprawnień w czasie wykonywania. W opisie aplikacji platformy uniwersalnej systemu Windows w sklepie znajduje się lista uprawnień, których wymaga aplikacja. Przez zainstalowanie aplikacji niejawnie udzielasz uprawnień. Te uprawnienia są konfigurowane w pliku manifestu aplikacji.

1. W projekcie aplikacji `ImHere.UWP` otwórz plik `Package.appxmanifest`.

2. Przejdź do karty **Możliwości** i sprawdź możliwość *Lokalizacja*.

    ![Karta możliwości platformy uniwersalnej systemu Windows](../media-drafts/4-uwp-location-capability.png)

> Aby aplikacja obsługiwała system Android lub iOS, uprawnienia muszą być skonfigurowane inaczej. Opisano to szczegółowo w [dokumentacji funkcji geolokalizacji pakietu Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).

## <a name="query-for-the-users-location"></a>Wysyłanie zapytania o lokalizację użytkownika

Istnieją dwa rodzaje lokalizacji użytkownika — ostatnia znana i bieżąca. Uzyskanie bieżącej lokalizacji może być czasochłonne, ponieważ urządzenie może musieć nawiązać połączenie GPS i poczekać na pobranie dokładnej lokalizacji. Najszybszą metodą jest uzyskanie ostatniej znanej lokalizacji wykrytej przez urządzenie. Ostatnia znana lokalizacja jest potencjalnie mniej dokładna, ale jej wywołanie jest znacznie szybsze. Lokalizacje są podawane w postaci wartości szerokości i długości geograficznej wyrażonych w [stopniach dziesiętnych](https://en.wikipedia.org/wiki/Decimal_degrees) oraz wartości wysokości urządzenia w metrach nad poziomem morza.

1. Otwórz klasę `MainViewModel` w projekcie standardowym `ImHere` dla platformy .NET.

2. W metodzie `SendLocation` utwórz wywołanie metody statycznej `GetLastKnownLocationAsync` w klasie `Geolocation` w przestrzeni nazw `Xamarin.Essentials`.

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. Zaktualizuj właściwość `Message` lokalizacją użytkownika, jeśli jest ona znana.

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

Pełny kod tej metody znajduje się poniżej.

```cs
async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
}
```

Uruchom aplikację i kliknij przycisk **Send Location** (Wyślij lokalizację), aby wyświetlić lokalizację w interfejsie użytkownika.

![Działająca aplikacja z wyświetloną lokalizacją użytkownika](../media-drafts/4-running-app-showing-location.png)

> Ta aplikacja korzysta z ostatniej znanej lokalizacji. W aplikacji przeznaczonej dla środowiska produkcyjnego warto spróbować uzyskać bieżącą dokładną lokalizację, a w przypadku niemożności jej pobrania w ustalonym czasie — skorzystać z ostatniej znanej lokalizacji. Sposób zaimplementowania tego podejścia opisano w [dokumentacji funkcji geolokalizacji pakietu Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). W tej aplikacji nie zaimplementowano obsługi błędów. W aplikacji przeznaczonej dla środowiska produkcyjnego należy zaimplementować obsługę wszystkich występujących wyjątków, na przykład wyjątku zgłoszonego w przypadku niedostępności lokalizacji.

## <a name="summary"></a>Podsumowanie

W tym module pokazaliśmy Ci, jak można uzyskać lokalizację użytkownika za pomocą pakietu Xamarin.Essentials. W następnym module utworzysz funkcję platformy Azure, która będzie pełniła rolę zaplecza dla aplikacji mobilnej.