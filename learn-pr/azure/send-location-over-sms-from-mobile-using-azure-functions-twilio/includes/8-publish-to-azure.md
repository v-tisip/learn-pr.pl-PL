<span data-ttu-id="89f71-101">Aplikacja i funkcja platformy Azure są teraz kompletne i działają w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="89f71-101">The app and Azure function are now complete and running locally.</span></span> <span data-ttu-id="89f71-102">W tym module opublikujesz funkcję platformy Azure na platformie Azure w celu jej uruchamiania w chmurze.</span><span class="sxs-lookup"><span data-stu-id="89f71-102">In this unit, you publish the Azure function to Azure to run in the cloud.</span></span>

> <span data-ttu-id="89f71-103">W tym module opublikujesz funkcję z poziomu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89f71-103">In this unit, you will publish your function from Visual Studio.</span></span> <span data-ttu-id="89f71-104">Jest to doskonały sposób, aby rozpocząć pracę na potrzeby weryfikacji koncepcji, prototypów i uczenia się, ale w przypadku aplikacji o jakości produkcyjnej **nie** powinno się używać tej metody.</span><span class="sxs-lookup"><span data-stu-id="89f71-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="89f71-105">W zamian należy skorzystać z wdrożenia opartego na elemencie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="89f71-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="89f71-106">Więcej informacji na ten temat można znaleźć w [dokumentach dotyczących wdrażania usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="89f71-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span></span>
>
> <span data-ttu-id="89f71-107">[![Znajomi: nie pozwalaj znajomym na publikowanie przy użyciu kliknięcia prawym przyciskiem myszy](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)</span><span class="sxs-lookup"><span data-stu-id="89f71-107">[![Friends don't let friends right-click publish](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)</span></span>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="89f71-108">Publikowanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="89f71-108">Publishing your app to Azure</span></span>

<span data-ttu-id="89f71-109">Funkcje platformy Azure można publikować na platformie Azure z poziomu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89f71-109">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="89f71-110">Zatrzymaj lokalne środowisko uruchomieniowe usługi Azure Functions, jeśli nadal działa po uruchomieniu w poprzednim module.</span><span class="sxs-lookup"><span data-stu-id="89f71-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="89f71-111">W eksploratorze rozwiązań kliknij prawym przyciskiem myszy aplikację `ImHere.Functions` i wybierz polecenie *Opublikuj...*.</span><span class="sxs-lookup"><span data-stu-id="89f71-111">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Klikanie prawym przyciskiem myszy pozycji Opublikuj w aplikacji usługi Functions](../media/8-right-click-publish.png)

3. <span data-ttu-id="89f71-113">W oknie dialogowym **Wybieranie miejsca docelowego publikacji** wybierz pozycję *Aplikacja funkcji platformy Azure*, a w obszarze **Azure App Service** wybierz pozycję *Utwórz nową*.</span><span class="sxs-lookup"><span data-stu-id="89f71-113">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="89f71-114">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="89f71-114">Click **Publish**.</span></span>

    ![Tworzenie nowej usługi Azure App Service jako docelowej lokalizacji publikowania](../media/8-pick-publish-target.png)

4. <span data-ttu-id="89f71-116">Z listy rozwijanej w prawym górnym rogu wybierz konto platformy Azure, jeśli masz więcej niż jedno takie konto i właściwe konto nie zostało wybrane.</span><span class="sxs-lookup"><span data-stu-id="89f71-116">Select your Azure account from the drop-down in the top-right corner if you have more than one Azure accounts and the right one isn't selected.</span></span>

5. <span data-ttu-id="89f71-117">Nadaj nazwę aplikacji usługi Functions.</span><span class="sxs-lookup"><span data-stu-id="89f71-117">Give your Functions app a name.</span></span> <span data-ttu-id="89f71-118">Ta nazwa musi być globalnie unikatowa wśród wszystkich aplikacji usługi Functions na całej platformie Azure, dlatego użyj nazwy podobnej do „ImHere-\<Twoja_nazwa\>”.</span><span class="sxs-lookup"><span data-stu-id="89f71-118">This name needs to be globally unique across all the Functions apps in the whole of Azure, so use something like "ImHere-\<YourName\>".</span></span>

6. <span data-ttu-id="89f71-119">Wybierz subskrypcję, w ramach której chcesz utworzyć aplikację usługi Functions.</span><span class="sxs-lookup"><span data-stu-id="89f71-119">Select the subscription you want to create this Functions app under.</span></span>

7. <span data-ttu-id="89f71-120">Utwórz nową grupę zasobów dla tej aplikacji usługi Functions, klikając przycisk **Nowy...** obok listy rozwijanej **Grupa zasobów** i nadając jej nazwę, taką jak „ImHere”.</span><span class="sxs-lookup"><span data-stu-id="89f71-120">Create a new resource group for this Functions app by clicking the **New...** button next to the **Resource Group** drop-down and giving it a name such as "ImHere".</span></span> <span data-ttu-id="89f71-121">Nazwy grup zasobów muszą być unikatowe w ramach Twojej subskrypcji, a nie globalnie unikatowe na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="89f71-121">Resource group names need to be unique to your subscription, not globally unique across Azure.</span></span> <span data-ttu-id="89f71-122">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f71-122">Then, click **OK**.</span></span>

    ![Utworzenie nowej grupy zasobów](../media/8-create-new-resource-group.png)

   <span data-ttu-id="89f71-124">Tworzenie nowej grupy zasobów ułatwia jej czyszczenie później.</span><span class="sxs-lookup"><span data-stu-id="89f71-124">Creating a new resource group makes it easier to clean up later.</span></span> <span data-ttu-id="89f71-125">Możesz usunąć grupę zasobów i mieć pewność, że wszystkie elementy utworzone dla tej aplikacji usługi Functions zostaną usunięte w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="89f71-125">You can delete the resource group and know that everything you've created for this Functions app will all be deleted at the same time.</span></span>

8. <span data-ttu-id="89f71-126">Utwórz nowy plan hostingu, klikając przycisk **Nowy...** obok listy rozwijanej **Plan hostingu**.</span><span class="sxs-lookup"><span data-stu-id="89f71-126">Create a new hosting plan by clicking the **New...** button next to the **Hosting Plan** drop-down.</span></span> <span data-ttu-id="89f71-127">Nazwa planu usługi App Service zostanie domyślnie ustawiona na nazwę aplikacji z ciągiem „Plan” dodanym na końcu.</span><span class="sxs-lookup"><span data-stu-id="89f71-127">The App Service plan name will default to your app name with "Plan" on the end.</span></span> <span data-ttu-id="89f71-128">Ustaw pole **Lokalizacja** na najbliższą sobie lokalizację i upewnij się, że **Rozmiar** został ustawiony na wartość użycia.</span><span class="sxs-lookup"><span data-stu-id="89f71-128">Set the **Location** to the closest location to you and make sure **Size** is set to consumption.</span></span> <span data-ttu-id="89f71-129">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f71-129">Then, click **OK**.</span></span>

    ![Konfigurowanie planu hostingu](../media/8-configure-hosting-plan.png)

9. <span data-ttu-id="89f71-131">Utwórz nowe konto magazynu, klikając przycisk **Nowy...** obok listy rozwijanej **Konto usługi Storage**.</span><span class="sxs-lookup"><span data-stu-id="89f71-131">Create a new storage account by clicking the **New...** button next to the **Storage Account** drop-down.</span></span> <span data-ttu-id="89f71-132">Zostanie podana nazwa domyślna. Zachowaj wszystkie wartości domyślne i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f71-132">A default name will be provided, so keep all the default values and click **OK**.</span></span>

    ![Tworzenie konta magazynu](../media/8-create-storage-account.png)

10. <span data-ttu-id="89f71-134">Kliknij pozycję **Utwórz**, aby aprowizować wszystkie zasoby na platformie Azure i opublikować aplikację usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="89f71-134">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![Tworzenie usługi App Service](../media/8-create-app-service.png)

<span data-ttu-id="89f71-136">Uruchamianie aprowizowania może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="89f71-136">Provisioning will take a couple of minutes or so to run.</span></span> <span data-ttu-id="89f71-137">Następujące zasoby zostaną aprowizowane:</span><span class="sxs-lookup"><span data-stu-id="89f71-137">The following resources will be provisioned:</span></span>

* <span data-ttu-id="89f71-138">Konto magazynu do przechowywania plików potrzebnych w aplikacji usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="89f71-138">A storage account to store the files needed for the Azure Functions app</span></span>
* <span data-ttu-id="89f71-139">Plan usługi App Service umożliwiający zarządzanie zasobami obliczeniowymi wymaganymi przez aplikację usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="89f71-139">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
* <span data-ttu-id="89f71-140">Usługa App Service, która uruchamia funkcję platformy Azure</span><span class="sxs-lookup"><span data-stu-id="89f71-140">The App Service that runs the Azure function</span></span>

<span data-ttu-id="89f71-141">Funkcja zostanie teraz opublikowana i będzie dostępna pod adresem https://<nazwa_Twojej_aplikacji>.azurewebsites.net/api/SendLocation.</span><span class="sxs-lookup"><span data-stu-id="89f71-141">The function will now be published and available to call at https://<your-app-name>.azurewebsites.net/api/SendLocation.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="89f71-142">Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="89f71-142">Configuring your app</span></span>

<span data-ttu-id="89f71-143">Funkcja platformy Azure uruchamiana lokalnie używała poświadczeń usługi Twilio przechowywanych w pliku `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="89f71-143">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="89f71-144">Jak sugeruje nazwa, ten plik jest przeznaczony dla ustawień lokalnych, a nie ustawień platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89f71-144">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="89f71-145">Przed wywołaniem funkcji platformy Azure wewnątrz platformy Azure należy skonfigurować ustawienia `TwilioAccountSid` i `TwilioAuthToken`.</span><span class="sxs-lookup"><span data-stu-id="89f71-145">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="89f71-146">Na karcie Publikowanie kliknij opcję **Zarządzaj ustawieniami aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="89f71-146">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![Opcja Zarządzaj ustawieniami aplikacji](../media/8-application-settings-option.png)

2. <span data-ttu-id="89f71-148">Kliknij przycisk **Dodaj**, aby dodać nowe ustawienie.</span><span class="sxs-lookup"><span data-stu-id="89f71-148">Click the **Add** button to add a new setting.</span></span> <span data-ttu-id="89f71-149">Nadaj mu nazwę „TwilioAccountSid” i ustaw wartość identyfikatora SID konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="89f71-149">Name it "TwilioAccountSid" and set the value to your Twilio account SID.</span></span> <span data-ttu-id="89f71-150">Powtórz ten krok dla tokenu uwierzytelniania przy użyciu nazwy „TwilioAuthToken”.</span><span class="sxs-lookup"><span data-stu-id="89f71-150">Repeat this step for your Auth Token using the name "TwilioAuthToken".</span></span>

    ![Ustawianie poświadczeń usługi Twilio w ustawieniach aplikacji](../media/8-set-creds-in-app-settings.png)

3. <span data-ttu-id="89f71-152">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f71-152">Click **OK**.</span></span>

4. <span data-ttu-id="89f71-153">Kliknij pozycję **Opublikuj**, aby ponownie opublikować aplikację usługi Azure Functions z nowymi ustawieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89f71-153">Click **Publish** to republish the Azure Functions app with the new application settings.</span></span>

    ![Przycisk Opublikuj](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="89f71-155">Wskazywanie platformy Azure w aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="89f71-155">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="89f71-156">Na karcie Publikowanie skopiuj **adres URL witryny** przy użyciu przycisku kopiowania obok wartości.</span><span class="sxs-lookup"><span data-stu-id="89f71-156">From the Publish tab, copy the **Site URL** using the copy button next to the value.</span></span>

    ![Kopiowanie adresu URL witryny z poziomu karty Publikowanie](../media/8-copy-site-url.png)

2. <span data-ttu-id="89f71-158">Otwórz model `MainViewModel` z projektu `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="89f71-158">Open the `MainViewModel` from the `ImHere` project.</span></span>

3. <span data-ttu-id="89f71-159">Zaktualizuj wartość pola `baseUrl`, aby była adresem URL witryny skopiowanym z karty Publikowanie.</span><span class="sxs-lookup"><span data-stu-id="89f71-159">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

4. <span data-ttu-id="89f71-160">Zmień protokół dla tej wartości z `http` na `https`.</span><span class="sxs-lookup"><span data-stu-id="89f71-160">Change the protocol for this value from `http` to `https`.</span></span> <span data-ttu-id="89f71-161">Adres URL witryny jest zawsze podawany przy użyciu protokołu HTTP, ale w celu wywołania funkcji platformy Azure trzeba użyć protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="89f71-161">The site URL is always given using HTTP, but you have to use HTTPS to call an Azure function.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="89f71-162">Testowanie działania</span><span class="sxs-lookup"><span data-stu-id="89f71-162">Test it out</span></span>

1. <span data-ttu-id="89f71-163">Ustaw aplikację `ImHere.UWP` jako aplikację uruchamiania i uruchom ją.</span><span class="sxs-lookup"><span data-stu-id="89f71-163">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

2. <span data-ttu-id="89f71-164">Wprowadź numer telefonu, a następnie kliknij przycisk **Wyślij lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="89f71-164">Enter a phone number and click the **Send Location** button.</span></span>

3. <span data-ttu-id="89f71-165">Lokalizacja powinna zostać odebrana w postaci wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="89f71-165">You should receive the location as an SMS message.</span></span>

## <a name="summary"></a><span data-ttu-id="89f71-166">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="89f71-166">Summary</span></span>

<span data-ttu-id="89f71-167">W tym module przedstawiono sposób publikowania projektu usługi Azure Functions do platformy Azure z poziomu programu Visual Studio oraz konfigurowania ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89f71-167">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>