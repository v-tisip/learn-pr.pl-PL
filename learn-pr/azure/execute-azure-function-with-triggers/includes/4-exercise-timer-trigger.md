<span data-ttu-id="7da48-101">W tym ćwiczeniu tworzona jest funkcja platformy Azure wywoływana co 20 sekund przy użyciu wyzwalacza czasomierza.</span><span class="sxs-lookup"><span data-stu-id="7da48-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="7da48-102">Aby wykonać to ćwiczenie, musisz zalogować się w witrynie [Azure Portal](https://portal.azure.com/) przy użyciu prawidłowego konta.</span><span class="sxs-lookup"><span data-stu-id="7da48-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="7da48-103">Tworzenie funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7da48-103">Create an Azure function</span></span>

<span data-ttu-id="7da48-104">Zacznijmy od utworzenia funkcji platformy Azure w portalu.</span><span class="sxs-lookup"><span data-stu-id="7da48-104">Let’s start by creating an Azure function in the portal.</span></span>

1. <span data-ttu-id="7da48-105">W lewym obszarze nawigacji wybierz pozycję **Utwórz zasób**.</span><span class="sxs-lookup"><span data-stu-id="7da48-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="7da48-106">Wybierz polecenie **Obliczenia**.</span><span class="sxs-lookup"><span data-stu-id="7da48-106">Select **Compute**.</span></span>

1. <span data-ttu-id="7da48-107">Znajdź i wybierz pozycję **Aplikacja funkcji**.</span><span class="sxs-lookup"><span data-stu-id="7da48-107">Locate and select **Function App**.</span></span> <span data-ttu-id="7da48-108">Możesz również skorzystać z paska wyszukiwania, aby zlokalizować szablon.</span><span class="sxs-lookup"><span data-stu-id="7da48-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Wybieranie aplikacji funkcji](../media/4-click-function-app.png)

1. <span data-ttu-id="7da48-110">Wpisz unikatową **nazwę aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="7da48-110">Enter a unique **App name**.</span></span>

1. <span data-ttu-id="7da48-111">Wybierz pozycję **Subskrypcja**.</span><span class="sxs-lookup"><span data-stu-id="7da48-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="7da48-112">Utwórz nową **grupę zasobów**.</span><span class="sxs-lookup"><span data-stu-id="7da48-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="7da48-113">Wybierz **system operacyjny** **Windows**.</span><span class="sxs-lookup"><span data-stu-id="7da48-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="7da48-114">Wybierz **plan Zużycie** jako **plan hostingu**.</span><span class="sxs-lookup"><span data-stu-id="7da48-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="7da48-115">Opłaty są naliczane za każde wykonanie funkcji.</span><span class="sxs-lookup"><span data-stu-id="7da48-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="7da48-116">Zasoby są przydzielane automatycznie na podstawie obciążenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7da48-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="7da48-117">Wybierz **lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="7da48-117">Select a **Location**.</span></span>

1. <span data-ttu-id="7da48-118">Utwórz nowe konto usługi **Storage**.</span><span class="sxs-lookup"><span data-stu-id="7da48-118">Create a new **Storage** account.</span></span> <span data-ttu-id="7da48-119">Ta wartość jest wymagana, ale nie będziemy z niej korzystać.</span><span class="sxs-lookup"><span data-stu-id="7da48-119">(This value is required, but we're not going to use it.)</span></span>

1. <span data-ttu-id="7da48-120">Wyłącz usługę **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="7da48-120">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="7da48-121">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7da48-121">Select **Create**.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="7da48-122">Tworzenie wyzwalacza czasomierza</span><span class="sxs-lookup"><span data-stu-id="7da48-122">Create a timer trigger</span></span>

<span data-ttu-id="7da48-123">Teraz utworzymy wyzwalacz czasomierza w ramach funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7da48-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="7da48-124">Po utworzeniu funkcji platformy Azure wybierz pozycję **Wszystkie zasoby** w lewym obszarze nawigacji.</span><span class="sxs-lookup"><span data-stu-id="7da48-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="7da48-125">Zlokalizuj i wybierz funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7da48-125">Locate and select your Azure function.</span></span>

1. <span data-ttu-id="7da48-126">W nowym bloku wskaż pozycję **Funkcje** i wybierz ikonę plus (+).</span><span class="sxs-lookup"><span data-stu-id="7da48-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Wskazywanie pozycji Funkcje i wybieranie ikony plusa](../media/4-hover-function.png)

1. <span data-ttu-id="7da48-128">Wybierz pozycję **Czasomierz**.</span><span class="sxs-lookup"><span data-stu-id="7da48-128">Select **Timer**.</span></span>

1. <span data-ttu-id="7da48-129">Wybierz język **CSharp**.</span><span class="sxs-lookup"><span data-stu-id="7da48-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="7da48-130">Wybierz pozycję **Utwórz tę funkcję**.</span><span class="sxs-lookup"><span data-stu-id="7da48-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="7da48-131">Konfigurowanie wyzwalacza czasomierza</span><span class="sxs-lookup"><span data-stu-id="7da48-131">Configure the timer trigger</span></span>

<span data-ttu-id="7da48-132">Mamy funkcję platformy Azure z logiką drukowania komunikatu w oknie dziennika.</span><span class="sxs-lookup"><span data-stu-id="7da48-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="7da48-133">Ustawimy harmonogram czasomierza, tak aby funkcja była wywoływana co 20 sekund.</span><span class="sxs-lookup"><span data-stu-id="7da48-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="7da48-134">Wybierz pozycję **Integracja**.</span><span class="sxs-lookup"><span data-stu-id="7da48-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="7da48-135">Wprowadź następującą wartość w polu **Harmonogram**:</span><span class="sxs-lookup"><span data-stu-id="7da48-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

1. <span data-ttu-id="7da48-136">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7da48-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="7da48-137">Uruchamianie czasomierza</span><span class="sxs-lookup"><span data-stu-id="7da48-137">Start the timer</span></span>

<span data-ttu-id="7da48-138">Po skonfigurowaniu czasomierza można go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="7da48-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="7da48-139">Wybierz pozycję **TimerTriggerCSharp1**.</span><span class="sxs-lookup"><span data-stu-id="7da48-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7da48-140">Nazwa **TimerTriggerCSharp1** jest nazwą domyślną.</span><span class="sxs-lookup"><span data-stu-id="7da48-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="7da48-141">Jest wybierana automatycznie po utworzeniu wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="7da48-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="7da48-142">Wybierz pozycję **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="7da48-142">Select **Run**.</span></span> 

<span data-ttu-id="7da48-143">Teraz co 20 sekund w oknie dziennika powinien być wyświetlany komunikat.</span><span class="sxs-lookup"><span data-stu-id="7da48-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="7da48-144">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="7da48-144">Clean up</span></span>

<span data-ttu-id="7da48-145">Aby upewnić się, że opłaty za tę funkcję nie są naliczane, nad oknem dziennika wybierz polecenie **Wstrzymaj**, aby zatrzymać czasomierz.</span><span class="sxs-lookup"><span data-stu-id="7da48-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Wstrzymaj](../media/4-pause-timer.png)


