<span data-ttu-id="5b7de-101">Aplikacja ma interfejs użytkownika i model widoku (ViewModel).</span><span class="sxs-lookup"><span data-stu-id="5b7de-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="5b7de-102">W tym module do modelu widoku (ViewModel) dodasz możliwość wyszukiwania lokalizacji przy użyciu zestawu Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="5b7de-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="5b7de-103">Włączanie uprawnień do lokalizacji</span><span class="sxs-lookup"><span data-stu-id="5b7de-103">Enable location permissions</span></span>

<span data-ttu-id="5b7de-104">Wszystkie platformy mobilne zapewniają zabezpieczenia informacji o użytkowniku i niektórych elementów sprzętu, takich jak aparat, biblioteka zdjęć czy lokalizacja użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b7de-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="5b7de-105">Zanim aplikacja będzie mogła uzyskiwać dostęp do lokalizacji użytkownika, użytkownik musi udzielić uprawnień — niejawnie podczas instalacji lub wybierając opcję udzielenia uprawnień w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5b7de-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="5b7de-106">W opisie aplikacji platformy uniwersalnej systemu Windows w sklepie znajduje się lista uprawnień, których wymaga aplikacja.</span><span class="sxs-lookup"><span data-stu-id="5b7de-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="5b7de-107">Przez zainstalowanie aplikacji niejawnie udzielasz uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5b7de-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="5b7de-108">Te uprawnienia są konfigurowane w pliku manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b7de-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="5b7de-109">W projekcie aplikacji `ImHere.UWP` otwórz plik `Package.appxmanifest`.</span><span class="sxs-lookup"><span data-stu-id="5b7de-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

2. <span data-ttu-id="5b7de-110">Przejdź do karty **Możliwości** i sprawdź możliwość *Lokalizacja*.</span><span class="sxs-lookup"><span data-stu-id="5b7de-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![Karta możliwości platformy uniwersalnej systemu Windows](../media/4-uwp-location-capability.png)

> <span data-ttu-id="5b7de-112">Aby aplikacja obsługiwała system Android lub iOS, uprawnienia muszą być skonfigurowane inaczej.</span><span class="sxs-lookup"><span data-stu-id="5b7de-112">If you want to support Android or iOS, the permissions need to be configured differently.</span></span> <span data-ttu-id="5b7de-113">Opisano to szczegółowo w [dokumentacji funkcji geolokalizacji pakietu Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span><span class="sxs-lookup"><span data-stu-id="5b7de-113">This is detailed in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span></span>

## <a name="query-for-the-users-location"></a><span data-ttu-id="5b7de-114">Wysyłanie zapytania o lokalizację użytkownika</span><span class="sxs-lookup"><span data-stu-id="5b7de-114">Query for the user's location</span></span>

<span data-ttu-id="5b7de-115">Istnieją dwa rodzaje lokalizacji użytkownika — ostatnia znana i bieżąca.</span><span class="sxs-lookup"><span data-stu-id="5b7de-115">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="5b7de-116">Uzyskanie bieżącej lokalizacji może być czasochłonne, ponieważ urządzenie może musieć nawiązać połączenie GPS i poczekać na pobranie dokładnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5b7de-116">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="5b7de-117">Najszybszą metodą jest uzyskanie ostatniej znanej lokalizacji wykrytej przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="5b7de-117">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="5b7de-118">Ostatnia znana lokalizacja jest potencjalnie mniej dokładna, ale jej wywołanie jest znacznie szybsze.</span><span class="sxs-lookup"><span data-stu-id="5b7de-118">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="5b7de-119">Lokalizacje są podawane w postaci wartości szerokości i długości geograficznej wyrażonych w [stopniach dziesiętnych](https://en.wikipedia.org/wiki/Decimal_degrees) oraz wartości wysokości urządzenia w metrach nad poziomem morza.</span><span class="sxs-lookup"><span data-stu-id="5b7de-119">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="5b7de-120">Otwórz klasę `MainViewModel` w projekcie standardowym `ImHere` dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="5b7de-120">Open the `MainViewModel` class in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="5b7de-121">W metodzie `SendLocation` utwórz wywołanie metody statycznej `GetLastKnownLocationAsync` w klasie `Geolocation` w przestrzeni nazw `Xamarin.Essentials`.</span><span class="sxs-lookup"><span data-stu-id="5b7de-121">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span>

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. <span data-ttu-id="5b7de-122">Zaktualizuj właściwość `Message` lokalizacją użytkownika, jeśli jest ona znana.</span><span class="sxs-lookup"><span data-stu-id="5b7de-122">Update the `Message` property with the user's location if one is found.</span></span>

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

<span data-ttu-id="5b7de-123">Pełny kod tej metody znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="5b7de-123">The full code for this method is below.</span></span>

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

<span data-ttu-id="5b7de-124">Uruchom aplikację i kliknij przycisk **Send Location** (Wyślij lokalizację), aby wyświetlić lokalizację w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b7de-124">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

![Działająca aplikacja z wyświetloną lokalizacją użytkownika](../media/4-running-app-showing-location.png)

> <span data-ttu-id="5b7de-126">Ta aplikacja korzysta z ostatniej znanej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5b7de-126">This app uses the last known location.</span></span> <span data-ttu-id="5b7de-127">W aplikacji przeznaczonej dla środowiska produkcyjnego warto spróbować uzyskać bieżącą dokładną lokalizację, a w przypadku niemożności jej pobrania w ustalonym czasie — skorzystać z ostatniej znanej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5b7de-127">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="5b7de-128">Sposób zaimplementowania tego podejścia opisano w [dokumentacji funkcji geolokalizacji pakietu Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). W tej aplikacji nie zaimplementowano obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="5b7de-128">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). This app does not have error handling.</span></span> <span data-ttu-id="5b7de-129">W aplikacji przeznaczonej dla środowiska produkcyjnego należy zaimplementować obsługę wszystkich występujących wyjątków, na przykład wyjątku zgłoszonego w przypadku niedostępności lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5b7de-129">In a production-quality app, you should handle any exceptions that occur, for example, if the location was not available and an exception was thrown.</span></span>

## <a name="summary"></a><span data-ttu-id="5b7de-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5b7de-130">Summary</span></span>

<span data-ttu-id="5b7de-131">W tym module pokazaliśmy Ci, jak można uzyskać lokalizację użytkownika za pomocą pakietu Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="5b7de-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="5b7de-132">W następnym module utworzysz funkcję platformy Azure, która będzie pełniła rolę zaplecza dla aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5b7de-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>