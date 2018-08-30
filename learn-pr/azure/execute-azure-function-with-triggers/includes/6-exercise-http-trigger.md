<span data-ttu-id="0e99a-101">W tym ćwiczeniu utworzymy funkcję platformy Azure, która akceptuje żądanie HTTP z jednym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="0e99a-101">In this exercise, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="0e99a-102">Funkcja zwraca do obiektu wywołującego ciąg wskazujący na powodzenie lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="0e99a-102">The function returns a string back to the caller to represent success or failure.</span></span>

> [!NOTE]
> <span data-ttu-id="0e99a-103">Aby wykonać to ćwiczenie, musisz zalogować się w witrynie [Azure Portal](https://portal.azure.com/) przy użyciu prawidłowego konta.</span><span class="sxs-lookup"><span data-stu-id="0e99a-103">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="0e99a-104">Tworzenie wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="0e99a-104">Create an HTTP trigger</span></span>

<span data-ttu-id="0e99a-105">Będziemy nadal korzystać z istniejącej aplikacji usługi Azure Functions i dodamy wyzwalacz HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e99a-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="0e99a-106">Wskaż pozycję **Funkcje** i wybierz ikonę plus (+).</span><span class="sxs-lookup"><span data-stu-id="0e99a-106">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Wskazywanie pozycji Funkcje i zatrzymywanie wskaźnika nad ikoną plusa](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="0e99a-108">Wybierz pozycję **Wyzwalacz HTTP**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-108">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="0e99a-109">Wybierz język **C#**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-109">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="0e99a-110">W polu **Nazwa** pozostaw wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="0e99a-110">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="0e99a-111">W polu **Poziom autoryzacji** wybierz ustawienie **Anonimowe**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-111">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="0e99a-112">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-112">Select **Create**.</span></span>

1. <span data-ttu-id="0e99a-113">Przyjrzyj się szybko automatycznie wygenerowanemu kodowi, aby zobaczyć, co się dzieje.</span><span class="sxs-lookup"><span data-stu-id="0e99a-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="0e99a-114">Parametr *req* reprezentuje żądanie przychodzące i zawiera parametr *name*.</span><span class="sxs-lookup"><span data-stu-id="0e99a-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="0e99a-115">Sprawdzamy, czy parametr *name* ma wartość.</span><span class="sxs-lookup"><span data-stu-id="0e99a-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="0e99a-116">Jeśli tak, zostanie zwrócone pozdrowienie.</span><span class="sxs-lookup"><span data-stu-id="0e99a-116">If it does, we return a greeting.</span></span> <span data-ttu-id="0e99a-117">Jeśli nie, zwrócony zostanie komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="0e99a-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="0e99a-118">Pobieranie adresu URL funkcji</span><span class="sxs-lookup"><span data-stu-id="0e99a-118">Get your function URL</span></span>

<span data-ttu-id="0e99a-119">Po utworzeniu wyzwalacza HTTP pobierzemy adres URL funkcji, aby rozpocząć tworzenie żądania.</span><span class="sxs-lookup"><span data-stu-id="0e99a-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="0e99a-120">Wybierz wyzwalacz HTTP, aby otworzyć ekran z kodem.</span><span class="sxs-lookup"><span data-stu-id="0e99a-120">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="0e99a-121">Po prawej stronie polecenia **Uruchom** wybierz pozycję **Pobierz adres URL funkcji**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-121">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="0e99a-122">Wybierz polecenie **Kopiuj**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-122">Select **Copy**.</span></span>

1. <span data-ttu-id="0e99a-123">Wybierz polecenie **Uruchom**, aby uruchomić funkcję.</span><span class="sxs-lookup"><span data-stu-id="0e99a-123">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="0e99a-124">Wysyłanie żądania GET do wyzwalacza HTTP</span><span class="sxs-lookup"><span data-stu-id="0e99a-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="0e99a-125">Adres URL funkcji został skopiowany do schowka.</span><span class="sxs-lookup"><span data-stu-id="0e99a-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="0e99a-126">Wyślemy teraz żądanie GET, aby sprawdzić, czy otrzymamy odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="0e99a-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="0e99a-127">Otwórz nową kartę w przeglądarce internetowej.</span><span class="sxs-lookup"><span data-stu-id="0e99a-127">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="0e99a-128">Wklej adres URL na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="0e99a-128">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="0e99a-129">Dodaj parametr ciągu zapytania o nazwie *name* z Twoją nazwą, na przykład:</span><span class="sxs-lookup"><span data-stu-id="0e99a-129">Add a query string parameter called *name* with your name for example:</span></span>

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. <span data-ttu-id="0e99a-130">Naciśnij przycisk ENTER, aby przesłać żądanie.</span><span class="sxs-lookup"><span data-stu-id="0e99a-130">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="0e99a-131">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="0e99a-131">Clean up</span></span>

<span data-ttu-id="0e99a-132">Aby upewnić się, że za tę funkcję nie zostaną naliczone opłaty, nad oknem dziennika wybierz polecenie **Wstrzymaj**.</span><span class="sxs-lookup"><span data-stu-id="0e99a-132">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Wstrzymaj](../media-drafts/4-pause-timer.png)


