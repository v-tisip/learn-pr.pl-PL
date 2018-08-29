<span data-ttu-id="f3206-101">Teraz nadszedł czas na uruchomienie aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f3206-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="f3206-102">Musimy utworzyć aplikację usługi Azure App Service, skonfigurować ją przy użyciu tożsamości MSI i konfiguracji naszego magazynu oraz wdrożyć nasz kod.</span><span class="sxs-lookup"><span data-stu-id="f3206-102">We need to create an Azure App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

## <a name="exercise"></a><span data-ttu-id="f3206-103">Ćwiczenie</span><span class="sxs-lookup"><span data-stu-id="f3206-103">Exercise</span></span>

### <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="f3206-104">Tworzenie aplikacji i planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="f3206-104">Create the App Service plan and app</span></span>

<span data-ttu-id="f3206-105">Tworzenie aplikacji usługi App Service jest procesem dwuetapowym: najpierw należy utworzyć *plan*, a następnie *aplikację*.</span><span class="sxs-lookup"><span data-stu-id="f3206-105">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="f3206-106">Nazwa *planu* musi być unikatowa tylko w ramach subskrypcji, aby można było stosować nazwę używaną przez nas: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="f3206-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="f3206-107">Nazwa aplikacji musi być globalnie unikatowa, więc musisz wybrać własną.</span><span class="sxs-lookup"><span data-stu-id="f3206-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="f3206-108">W usłudze Azure Cloud Shell uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f3206-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a><span data-ttu-id="f3206-109">Dodawanie konfiguracji do aplikacji</span><span class="sxs-lookup"><span data-stu-id="f3206-109">Add configuration to the app</span></span>

<span data-ttu-id="f3206-110">W przypadku wdrażania na platformie Azure będziemy korzystać z najlepszego rozwiązania w usłudze App Service, które polega na umieszczaniu konfiguracji w ustawieniach aplikacji, a nie w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f3206-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a><span data-ttu-id="f3206-111">Włączanie tożsamości usługi zarządzanej</span><span class="sxs-lookup"><span data-stu-id="f3206-111">Enable MSI</span></span>

<span data-ttu-id="f3206-112">Włączanie tożsamości usługi zarządzanej aplikacji wymaga jednego wiersza kodu:</span><span class="sxs-lookup"><span data-stu-id="f3206-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="f3206-113">Z wynikowych danych wyjściowych JSON skopiuj wartość **principalId**.</span><span class="sxs-lookup"><span data-stu-id="f3206-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="f3206-114">PrincipalId to unikatowy identyfikator nowej tożsamości aplikacji w usłudze Azure Active Directory. Będziemy z niego korzystać w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="f3206-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

### <a name="grant-access-to-the-vault"></a><span data-ttu-id="f3206-115">Udzielanie dostępu do magazynu</span><span class="sxs-lookup"><span data-stu-id="f3206-115">Grant access to the vault</span></span>

<span data-ttu-id="f3206-116">Teraz musisz udzielić aplikacji uprawnień tożsamości do pobierania i wyświetlania listy wpisów tajnych z magazynu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f3206-116">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="f3206-117">Użyj wartości **principalId** skopiowanej w poprzednim kroku jako wartości identyfikatora **object-id** w poleceniu poniżej.</span><span class="sxs-lookup"><span data-stu-id="f3206-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="f3206-118">Wdrażanie aplikacji i jej wypróbowywanie</span><span class="sxs-lookup"><span data-stu-id="f3206-118">Deploy the app and try it out</span></span>

<span data-ttu-id="f3206-119">Konfiguracja została ustawiona i wszystko jest gotowe do wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f3206-119">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="f3206-120">Poniższe polecenia spowodują opublikowanie witryny w folderze `pub`, spakowanie jej w pliku `site.zip` i wdrożenie pliku ZIP w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="f3206-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="f3206-121">Jeśli jeszcze nie znajdujesz się w katalogu KeyVaultDemoApp, musisz do niego wrócić za pomocą polecenia `cd`.</span><span class="sxs-lookup"><span data-stu-id="f3206-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="f3206-122">Po uzyskaniu wyniku wskazującego na to, że witryna została wdrożona, otwórz adres `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="f3206-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="f3206-123">Powinna pojawić się wartość wpisu tajnego **reindeer_flotilla**.</span><span class="sxs-lookup"><span data-stu-id="f3206-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="f3206-124">Twoja aplikacja jest gotowa i wdrożona.</span><span class="sxs-lookup"><span data-stu-id="f3206-124">Your app is finished and deployed!</span></span>