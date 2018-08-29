<span data-ttu-id="84e97-101">Zostanie uruchomiona aplikacja mobilna i utworzona wstępna wersja funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84e97-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="84e97-102">W tej jednostce możesz wywołać funkcję platformy Azure z poziomu aplikacji mobilnej, przekazując lokalizację użytkownika i listę numerów telefonów, na które mają być wysyłane wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="84e97-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="84e97-103">Wywoływanie funkcji platformy Azure z poziomu aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="84e97-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="84e97-104">Otwórz klasę `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="84e97-104">Open the `MainViewModel`.</span></span>

2. <span data-ttu-id="84e97-105">W tej klasie dodaj pole prywatne `HttpClient` o nazwie `client`.</span><span class="sxs-lookup"><span data-stu-id="84e97-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="84e97-106">Konieczne będzie dodanie odwołania do przestrzeni nazw `System.Net.Http`.</span><span class="sxs-lookup"><span data-stu-id="84e97-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

3. <span data-ttu-id="84e97-107">Dodaj pole stałej na potrzeby podstawowego adresu URL dla tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="84e97-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="84e97-108">Ustaw je na adres, na którym nasłuchuje lokalne środowisko uruchomieniowe usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="84e97-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="84e97-109">Po wdrożeniu funkcji na platformie Azure tę zmienną można zmienić na adres URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84e97-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. <span data-ttu-id="84e97-110">Wewnątrz metody `SendLocation` po odnalezieniu lokalizacji utwórz nowe wystąpienie klasy `PostData` przy użyciu lokalizacji i listy numerów telefonów wprowadzonej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="84e97-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="84e97-111">Konieczne będzie dodanie dyrektywy using dla przestrzeni nazw `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="84e97-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > <span data-ttu-id="84e97-112">Przyjęto w związku z tym założenie, że numery telefonów wprowadzono w prawidłowym formacie — jeden na wiersz w kontrolce `Editor`.</span><span class="sxs-lookup"><span data-stu-id="84e97-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="84e97-113">W aplikacji produkcyjnej miałaby w tej sytuacji miejsce weryfikacja w celu sprawdzenia, czy wprowadzono co najmniej jeden numer telefonu i był on w poprawnym formacie.</span><span class="sxs-lookup"><span data-stu-id="84e97-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>

5. <span data-ttu-id="84e97-114">Najprostszym sposobem serializacji danych `PostData` w formacie JSON jest użycie pakietu NuGet Newtonsoft.JSON.</span><span class="sxs-lookup"><span data-stu-id="84e97-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.JSON NuGet package.</span></span> <span data-ttu-id="84e97-115">Dodaj pakiet NuGet do projektu `ImHere` w taki sam sposób, jak dodano pakiet Xamarin.Essentials we wcześniejszej jednostce.</span><span class="sxs-lookup"><span data-stu-id="84e97-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

6. <span data-ttu-id="84e97-116">Serializowanie danych `PostData` do danych typu `string` przy użyciu klasy statycznej `JsonConvert`.</span><span class="sxs-lookup"><span data-stu-id="84e97-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="84e97-117">Konieczne będzie dodanie dyrektywy using dla przestrzeni nazw `Newtonsoft.Json`.</span><span class="sxs-lookup"><span data-stu-id="84e97-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="84e97-118">Zakoduj ten ciąg do klasy `StringContent`, aby mógł on zostać przekazany do funkcji platformy Azure w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="84e97-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. <span data-ttu-id="84e97-119">Opublikuj te dane w funkcji i uzyskaj wynik.</span><span class="sxs-lookup"><span data-stu-id="84e97-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="84e97-120">Dostęp do funkcji platformy Azure odbywa się za pomocą parametru `/api/<function name>`, więc zakładając, że port wybrany przez lokalne środowisko uruchomieniowe usługi Functions to 7071, funkcja `SendLocation` będzie dostępna pod adresem `http://localhost:7071/api/SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="84e97-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

8. <span data-ttu-id="84e97-121">W zależności od wyniku wyświetl komunikat w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="84e97-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="84e97-122">Pełny kod dla nowych pól i metoda `SendLocation` znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="84e97-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

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

## <a name="testing-it-out"></a><span data-ttu-id="84e97-123">Testowanie</span><span class="sxs-lookup"><span data-stu-id="84e97-123">Testing it out</span></span>

1. <span data-ttu-id="84e97-124">Sprawdź, czy funkcja platformy Azure nadal działa lokalnie, a port jest zgodny z metodą `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="84e97-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

2. <span data-ttu-id="84e97-125">Ustaw aplikację platformy uniwersalnej systemu Windows jako aplikację startową i uruchom ją.</span><span class="sxs-lookup"><span data-stu-id="84e97-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="84e97-126">Kliknij przycisk **Wyślij lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="84e97-126">Click the **Send Location** button.</span></span> <span data-ttu-id="84e97-127">W oknie konsoli środowiska uruchomieniowego usługi Functions zostaną wyświetlone dane wyjściowe zawierające wywoływaną funkcję oraz zarejestrowane dane przedstawiające wygenerowany adres URL.</span><span class="sxs-lookup"><span data-stu-id="84e97-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![Dane wyjściowe wywoływanej funkcji](../media/6-function-called.png)

3. <span data-ttu-id="84e97-129">Aby przetestować generowanie adresu URL, wklej go z poziomu konsoli do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="84e97-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="84e97-130">Powinna zostać wyświetlona Twoja bieżąca lokalizacja.</span><span class="sxs-lookup"><span data-stu-id="84e97-130">It should show your current location.</span></span>

## <a name="summary"></a><span data-ttu-id="84e97-131">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="84e97-131">Summary</span></span>

<span data-ttu-id="84e97-132">W tej jednostce pokazaliśmy Ci, jak wywołać funkcję platformy Azure z poziomu aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="84e97-132">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="84e97-133">Za pomocą tego wywołania przekazano lokalizację użytkownika i numery telefonów wprowadzone w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="84e97-133">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="84e97-134">W następnej jednostce powiążesz funkcję platformy Azure z usługą Twilio, aby wysłać tę lokalizację jako wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="84e97-134">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>