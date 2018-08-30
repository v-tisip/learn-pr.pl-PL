<span data-ttu-id="001de-101">W tym momencie aplikacja pracuje nad uzyskaniem lokalizacji użytkownika i jest gotowa do wysłania do funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="001de-101">At this point, the app is working to get the user's location and is ready to be sent to an Azure function.</span></span> <span data-ttu-id="001de-102">W tym rozdziale utworzysz funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="001de-102">In this unit, you build the Azure function.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="001de-103">Tworzenie projektu usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="001de-103">Create an Azure Functions project</span></span>

1. <span data-ttu-id="001de-104">Dodaj nowy projekt do rozwiązania `ImHere`, klikając prawym przyciskiem myszy rozwiązanie i wybierając polecenie *Dodaj -> Nowy projekt*.</span><span class="sxs-lookup"><span data-stu-id="001de-104">Add a new project to the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="001de-105">W drzewie po lewej stronie wybierz pozycję *Visual C# -> Chmura*, a następnie pozycję *Azure Functions* z panelu w środku.</span><span class="sxs-lookup"><span data-stu-id="001de-105">From the tree on the left-hand side, select *Visual C#->Cloud*, and then select *Azure Functions* from the panel in the center.</span></span>

3. <span data-ttu-id="001de-106">Nadaj projektowi nazwę „ImHere.Functions”, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="001de-106">Name the project "ImHere.Functions", and then click **OK**.</span></span>

    ![Okno dialogowe Dodaj nowy projekt](../media-drafts/5-add-new-functions-project.png)

4. <span data-ttu-id="001de-108">W oknie dialogowym konfiguracji **Nowy projekt** jako ustawienie wersji usługi Functions zostaw *Azure Functions v1 (.NET Framework)*.</span><span class="sxs-lookup"><span data-stu-id="001de-108">In the **New Project** configuration dialog, leave the Functions version set to *Azure Functions v1 (.NET Framework)*.</span></span> <span data-ttu-id="001de-109">Wybierz pozycję *Wyzwalacz protokołu HTTP*, jako ustawienie konta magazynu zostaw *Emulator magazynu*, a następnie ustaw uprawnienia dostępu na *Anonimowy*.</span><span class="sxs-lookup"><span data-stu-id="001de-109">Select *Http Trigger*, leave the storage account set to *Storage Emulator*, and set the access rights to *Anonymous*.</span></span> <span data-ttu-id="001de-110">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="001de-110">Then click **OK**.</span></span>

    ![Okno dialogowe konfiguracji projektu usługi Azure Functions](../media-drafts/5-configure-trigger.png)

<span data-ttu-id="001de-112">Zostanie utworzony nowy projekt z domyślną funkcją o nazwie `Function1`.</span><span class="sxs-lookup"><span data-stu-id="001de-112">The new project will be created and have a default function called `Function1`.</span></span>

> <span data-ttu-id="001de-113">Ta funkcja została utworzona z dostępem anonimowym.</span><span class="sxs-lookup"><span data-stu-id="001de-113">This function was created with anonymous access.</span></span> <span data-ttu-id="001de-114">Po opublikowaniu tej funkcji na platformie Azure każdy, kto zna adres URL, będzie mógł ją wywołać.</span><span class="sxs-lookup"><span data-stu-id="001de-114">Once published to Azure, anybody who knows the URL will be able to call this function.</span></span> <span data-ttu-id="001de-115">W rzeczywistym scenariuszu powinna ona być chroniona za pomocą jakiejś formy uwierzytelniania, takiej jak [Uwierzytelnianie usługi Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) czy [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span><span class="sxs-lookup"><span data-stu-id="001de-115">In a real-world scenario, you would protect this with some form of authentication, such as [Azure App Service authentication](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) or [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span></span>

## <a name="create-the-function"></a><span data-ttu-id="001de-116">Tworzenie funkcji</span><span class="sxs-lookup"><span data-stu-id="001de-116">Create the function</span></span>

<span data-ttu-id="001de-117">Projekt usługi Azure Functions jest tworzony z pojedynczą funkcją wyzwalacza HTTP o nazwie `Function1`.</span><span class="sxs-lookup"><span data-stu-id="001de-117">The Azure Functions project is created with a single HTTP trigger function called `Function1`.</span></span> <span data-ttu-id="001de-118">Sama funkcja jest implementowana jako statyczna metoda `Run` w klasie `Function1`.</span><span class="sxs-lookup"><span data-stu-id="001de-118">The function itself is implemented as a static `Run` method in the `Function1` class.</span></span>

1. <span data-ttu-id="001de-119">W Eksploratorze rozwiązań zmień nazwę pliku z „Function1.cs” na „SendLocation.cs”.</span><span class="sxs-lookup"><span data-stu-id="001de-119">Rename the file in Solution Explorer from "Function1.cs" to "SendLocation.cs".</span></span> <span data-ttu-id="001de-120">Po wyświetleniu monitu o zmianę nazw wszystkich odwołań do elementu kodu `Function1` kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="001de-120">When prompted to rename all references to the code element `Function1`, click **Yes**.</span></span>

2. <span data-ttu-id="001de-121">Zmień nazwę funkcji w atrybucie na „SendLocation”.</span><span class="sxs-lookup"><span data-stu-id="001de-121">Rename the function name in the attribute to "SendLocation".</span></span>

    ```cs
    [FunctionName("SendLocation")]
    ```

3. <span data-ttu-id="001de-122">Usuń zawartość funkcji, z wyjątkiem pierwszego wiersza, który zapisuje komunikat z informacjami w rejestratorze.</span><span class="sxs-lookup"><span data-stu-id="001de-122">Delete the contents of the function, except the first line that writes an information message to the logger.</span></span>

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a><span data-ttu-id="001de-123">Tworzenie klasy umożliwiającej udostępnianie danych między aplikacją mobilną i funkcją</span><span class="sxs-lookup"><span data-stu-id="001de-123">Create a class to share data between the mobile app and function</span></span>

<span data-ttu-id="001de-124">Dane są przesyłane do funkcji platformy Azure w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="001de-124">When data is sent to the Azure function, it will be sent as JSON.</span></span> <span data-ttu-id="001de-125">Aplikacja mobilna serializuje dane do formatu JSON, a funkcja deserializuje te dane z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="001de-125">The mobile app will serialize data into JSON and the function will deserialize from JSON.</span></span> <span data-ttu-id="001de-126">Aby zachować spójność tych danych między aplikacją mobilną i funkcją, utwórz nowy projekt, który będzie zawierał klasę umożliwiającą przechowywanie danych o lokalizacji i numerze telefonu.</span><span class="sxs-lookup"><span data-stu-id="001de-126">To keep this data consistent between the mobile app and the function, create a new project that contains a class to hold the location and phone number data.</span></span> <span data-ttu-id="001de-127">Aplikacja i funkcja będą odwoływały się do tego projektu.</span><span class="sxs-lookup"><span data-stu-id="001de-127">This project will then be referenced by the app and function.</span></span>

1. <span data-ttu-id="001de-128">Utwórz nowy projekt w ramach rozwiązania `ImHere`, klikając prawym przyciskiem myszy rozwiązanie i wybierając polecenie *Dodaj -> Nowy projekt*.</span><span class="sxs-lookup"><span data-stu-id="001de-128">Create a new project under the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="001de-129">W drzewie po lewej stronie wybierz pozycję *Visual C# -> .NET Standard*, a następnie pozycję *Biblioteka klas (.NET Standard)* z panelu w środku.</span><span class="sxs-lookup"><span data-stu-id="001de-129">From the tree on the left-hand side, select *Visual C#->.NET Standard*, and then select *Class Library (.NET Standard)* from the panel in the center.</span></span>

3. <span data-ttu-id="001de-130">Nadaj projektowi nazwę „ImHere.Data”, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="001de-130">Name the project "ImHere.Data", and then click **OK**.</span></span>

    ![Okno dialogowe Dodaj nowy projekt](../media-drafts/5-add-new-net-standard-project.png)

4. <span data-ttu-id="001de-132">Usuń wygenerowany automatycznie plik „Class1.cs”.</span><span class="sxs-lookup"><span data-stu-id="001de-132">Delete the auto-generated "Class1.cs" file.</span></span>

5. <span data-ttu-id="001de-133">Utwórz nową klasę w projekcie `ImHere.Data` o nazwie `PostData`, klikając prawym przyciskiem myszy projekt, a następnie wybierając pozycję *Dodaj -> Klasa*. Nadaj nowej klasie nazwę „PostData”, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="001de-133">Create a new class in the `ImHere.Data` project called `PostData` by right-clicking on the project and then selecting *Add->Class...*. Name the new class "PostData" and click **OK**.</span></span>

6. <span data-ttu-id="001de-134">Dodaj właściwości `double` dla szerokości i długości geograficznej, a także właściwość `string[]` dla numerów telefonów, na które mają być wysyłane dane.</span><span class="sxs-lookup"><span data-stu-id="001de-134">Add `double` properties for the latitude and longitude, as well as a `string[]` property for the phone numbers to send to.</span></span>

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. <span data-ttu-id="001de-135">Dodaj odwołanie do tego projektu do obu projektów (`ImHere.Functions` i `ImHere`), klikając projekt prawym przyciskiem myszy, a następnie wybierając pozycję *Dodaj -> Odwołanie*. W drzewie po lewej stronie wybierz pozycję *Projekty*, a następnie zaznacz pole wyboru obok pozycji *ImHere.Data*.</span><span class="sxs-lookup"><span data-stu-id="001de-135">Add a reference to this project to both the `ImHere.Functions` and `ImHere` projects by right-clicking on the project and then selecting *Add->Reference...*. Select *Projects* from the tree on the left-hand side, and then check the box next to *ImHere.Data*.</span></span>

    ![Konfigurowanie odwołań do projektu](../media-drafts/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a><span data-ttu-id="001de-137">Odczytywanie danych wysłanych do funkcji</span><span class="sxs-lookup"><span data-stu-id="001de-137">Read the data sent to the function</span></span>

<span data-ttu-id="001de-138">W funkcji Azure parametr `req` zawiera wykonane żądanie HTTP, a dane w tym żądaniu są obiektem `PostData` zserializowanym do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="001de-138">In the Azure function, the `req` parameter contains the HTTP request that was made and the data inside this request will be a JSON serialized `PostData` object.</span></span>

1. <span data-ttu-id="001de-139">Otwórz klasę `SendLocation` w projekcie `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="001de-139">Open the `SendLocation` class in the `ImHere.Functions` project.</span></span>

2. <span data-ttu-id="001de-140">Odczytaj zawartość żądania HTTP do obiektu `PostData`, dodając dyrektywę użycia dla przestrzeni nazw `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="001de-140">Read the contents of the HTTP request into a `PostData` object, adding a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. <span data-ttu-id="001de-141">Skonstruuj adres URL aplikacji Mapy Google, używając szerokości i długości geograficznej z obiektu `PostData`.</span><span class="sxs-lookup"><span data-stu-id="001de-141">Construct a Google Maps URL using the latitude and longitude from the `PostData`.</span></span>

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. <span data-ttu-id="001de-142">Zarejestruj adres URL.</span><span class="sxs-lookup"><span data-stu-id="001de-142">Log the URL.</span></span>

    ```cs
    log.Info($"URL created - {url}");
    ```

5. <span data-ttu-id="001de-143">Zwróć kod stanu 200, aby pokazać, że funkcja została wykonana bez błędu.</span><span class="sxs-lookup"><span data-stu-id="001de-143">Return a 200 status code to show the function completed without error.</span></span>

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

<span data-ttu-id="001de-144">Poniżej przedstawiono kompletną funkcję.</span><span class="sxs-lookup"><span data-stu-id="001de-144">The complete function is shown below.</span></span>

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

## <a name="run-the-azure-function-locally"></a><span data-ttu-id="001de-145">Uruchamianie funkcji platformy Azure w środowisku lokalnym</span><span class="sxs-lookup"><span data-stu-id="001de-145">Run the Azure function locally</span></span>

<span data-ttu-id="001de-146">Funkcje można uruchamiać lokalnie za pomocą lokalnego konta magazynu i lokalnego środowiska uruchomieniowego usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="001de-146">Functions can be run locally using a local storage account and local Azure Functions runtime.</span></span> <span data-ttu-id="001de-147">Lokalne środowisko uruchomieniowe umożliwia przetestowanie funkcji przed jej wdrożeniem na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="001de-147">This local runtime allows you to test out your function before deploying it to Azure.</span></span>

1. <span data-ttu-id="001de-148">W eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt `ImHere.Functions`, a następnie wybierz pozycję *Ustaw jako projekt startowy*.</span><span class="sxs-lookup"><span data-stu-id="001de-148">Right-click on the `ImHere.Functions` project in the solution explorer, and then select *Set as StartUp project*.</span></span>

2. <span data-ttu-id="001de-149">Z menu *Debuguj* wybierz pozycję *Uruchom bez debugowania*.</span><span class="sxs-lookup"><span data-stu-id="001de-149">From the *Debug* menu, select *Start Without Debugging*.</span></span> <span data-ttu-id="001de-150">Lokalne środowisko uruchomieniowe usługi Azure Functions zostanie uruchomione w oknie konsoli i uruchomi funkcję, nasłuchując na dostępnym porcie na komputerze `localhost`.</span><span class="sxs-lookup"><span data-stu-id="001de-150">The local Azure Functions runtime will launch inside a console window and start your function, listening on an available port on `localhost`.</span></span>

    ![Funkcja platformy Azure uruchomiona w środowisku lokalnym](../media-drafts/5-function-running-locally.png)

3. <span data-ttu-id="001de-152">Zanotuj numer portu, na którym nasłuchuje funkcja.</span><span class="sxs-lookup"><span data-stu-id="001de-152">Take a note of the port that the function is listening on.</span></span> <span data-ttu-id="001de-153">Będzie on potrzebny w następnym rozdziale do przetestowania aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="001de-153">You'll need this in the next unit to test out the mobile app.</span></span> <span data-ttu-id="001de-154">Na powyższej ilustracji funkcja nasłuchuje na porcie **7071**.</span><span class="sxs-lookup"><span data-stu-id="001de-154">In the image above, the function is listening on port **7071**.</span></span>

    ```sh
    Listening on http://localhost:7071/
    ```

4. <span data-ttu-id="001de-155">Pozostaw funkcję uruchomioną, aby przetestować aplikację mobilną w następnym rozdziale.</span><span class="sxs-lookup"><span data-stu-id="001de-155">Leave the function running so that you can test the mobile app in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="001de-156">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="001de-156">Summary</span></span>

<span data-ttu-id="001de-157">W tym rozdziale pokazaliśmy, jak utworzyć projekt usługi Azure Functions w programie Visual Studio, dodaliśmy projekt udostępniony z obiektem danych, który ma być współużytkowany między aplikacją mobilną i funkcją, oraz przedstawiliśmy sposób tworzenia podstawowego wdrożenia funkcji w celu deserializacji przekazanych danych.</span><span class="sxs-lookup"><span data-stu-id="001de-157">In this unit, you learned how to create an Azure Functions project in Visual Studio, added a shared project with a data object to be shared between the mobile app and the function, and learned how to create a basic implementation of the function to deserialize the data passed in.</span></span> <span data-ttu-id="001de-158">Pokazaliśmy również, jak uruchomić funkcję platformy Azure w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="001de-158">You also learned how to run an Azure function locally.</span></span> <span data-ttu-id="001de-159">W następnym rozdziale wywołasz funkcję platformy Azure z poziomu aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="001de-159">In the next unit, you'll call the Azure function from the mobile app.</span></span>