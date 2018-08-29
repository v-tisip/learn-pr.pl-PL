
<span data-ttu-id="c8369-101">W tym ćwiczeniu użyjesz interfejsu wiersza polecenia platformy Azure na maszynie lokalnej do utworzenia grupy zasobów, a następnie do wdrożenia w niej aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="c8369-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="c8369-102">Kroki tworzenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c8369-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="c8369-103">Otwórz powłokę bash w systemie Linux lub macOS bądź otwórz okno wiersza polecenia lub programu PowerShell, jeśli pracujesz w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="c8369-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="c8369-104">Uruchom interfejs wiersza polecenia platformy Azure, a następnie uruchom polecenie logowania.</span><span class="sxs-lookup"><span data-stu-id="c8369-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="c8369-105">Jeśli w przeglądarce internetowej nie zostanie wyświetlona strona logowania platformy Azure, postępuj zgodnie z instrukcjami wiersza polecenia, a następnie wprowadź kod autoryzacji na stronie [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="c8369-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="c8369-106">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="c8369-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="c8369-107">Sprawdź, czy grupa zasobów została pomyślnie utworzona, wyświetlając listę wszystkich grup zasobów w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c8369-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="c8369-108">Opcjonalnie sprawdź w witrynie Azure Portal, czy zasób został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c8369-108">Optionally, confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="c8369-109">Otwórz przeglądarkę internetową, zaloguj się do witryny Azure Portal, a następnie przejdź do sekcji **Grupy zasobów** (zobacz poniżej).</span><span class="sxs-lookup"><span data-stu-id="c8369-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="c8369-110">Nowa grupa zasobów powinna zostać wyświetlona na liście.</span><span class="sxs-lookup"><span data-stu-id="c8369-110">The new resource group should be displayed in the list.</span></span>

![Używanie witryny Azure Portal do wyświetlania listy grup zasobów](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="c8369-112">Procedura tworzenia planu usług</span><span class="sxs-lookup"><span data-stu-id="c8369-112">Steps to create a service plan</span></span>
<span data-ttu-id="c8369-113">W przypadku korzystania z usługi Web Apps w ramach usługi Azure App Service płacisz za zasoby obliczeniowe platformy Azure używane przez aplikację, co jest zależne od planu usługi App Service skojarzonego z usługami Web Apps.</span><span class="sxs-lookup"><span data-stu-id="c8369-113">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="c8369-114">Za pomocą planów usług określany jest region używany na potrzeby centrum danych aplikacji, liczba używanych maszyn wirtualnych i warstwa cenowa.</span><span class="sxs-lookup"><span data-stu-id="c8369-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="c8369-115">Utwórz plan usługi App Service, w ramach którego zostanie uruchomiona Twoja aplikacja.</span><span class="sxs-lookup"><span data-stu-id="c8369-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="c8369-116">Nazwy aplikacji i planu muszą być unikatowe, dlatego zmień ciąg „12345” na losową liczbę.</span><span class="sxs-lookup"><span data-stu-id="c8369-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="c8369-117">Następujące polecenie nie określa warstwy cenowej lub szczegółów wystąpienia maszyny wirtualnej, więc domyślne zostanie użyty plan **Podstawowy** i jedno **małe** wystąpienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8369-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="c8369-118">Sprawdź, czy plan usług został pomyślnie utworzony, wyświetlając listę wszystkich planów w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c8369-118">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="c8369-119">Procedura tworzenia aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="c8369-119">Steps to create a web app</span></span>
<span data-ttu-id="c8369-120">Następnym krokiem jest utworzenie aplikacji internetowej w ramach swojego planu usług.</span><span class="sxs-lookup"><span data-stu-id="c8369-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="c8369-121">Kod można wdrożyć w tym samym czasie, ale w tym przykładzie zrobimy do w oddzielnych krokach.</span><span class="sxs-lookup"><span data-stu-id="c8369-121">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="c8369-122">Utwórz aplikację internetową, pamiętając o zmianie ciągu „12345” na wcześniej użytą losową liczbę.</span><span class="sxs-lookup"><span data-stu-id="c8369-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="c8369-123">Sprawdź, czy aplikacja została pomyślnie utworzona, wyświetlając listę wszystkich aplikacji w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c8369-123">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="c8369-124">Zwróć uwagę na parametr **DefaultHostName**; będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="c8369-124">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="c8369-125">Procedura wdrażania kodu z repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="c8369-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="c8369-126">Ostatnim krokiem jest wdrożenie kodu z repozytorium GitHub do aplikacji internetowej, ponownie pamiętając o zmianie ciągu „12345” na wcześniej użytą losową liczbę.</span><span class="sxs-lookup"><span data-stu-id="c8369-126">The final step is to deploy code from a GitHub repository to the web app, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="c8369-127">Skopiuj następujący adres URL do przeglądarki, aby wyświetlić aplikację internetową.</span><span class="sxs-lookup"><span data-stu-id="c8369-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="c8369-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="c8369-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="c8369-129">Zostanie wyświetlona strona z informacją „HelloWorld!”</span><span class="sxs-lookup"><span data-stu-id="c8369-129">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="c8369-130">Zamknij okno przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="c8369-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="c8369-131">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c8369-131">Summary</span></span>
<span data-ttu-id="c8369-132">W ćwiczeniu przedstawiono typowy wzorzec na potrzeby interaktywnej sesji wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8369-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="c8369-133">Najpierw użyto standardowego polecenia, aby utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="c8369-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="c8369-134">Następnie użyto zestawu poleceń do wdrożenia zasobu (w tym przykładzie jest to aplikacja internetowa) w tej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c8369-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="c8369-135">Ten zestaw poleceń można w łatwy sposób połączyć w skrypt powłoki i wykonywać za każdym razem, gdy konieczne jest utworzenie takiego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c8369-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
