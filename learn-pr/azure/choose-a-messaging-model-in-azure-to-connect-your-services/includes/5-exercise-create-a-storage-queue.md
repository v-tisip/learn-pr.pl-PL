<span data-ttu-id="9ff29-101">W tym ćwiczeniu utworzysz nowe konto usługi Storage w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff29-101">In this exercise, you will create a new Storage Account in your Azure subscription.</span></span> <span data-ttu-id="9ff29-102">Następnie użyjesz usługi Azure Cloud Shell, aby utworzyć nową kolejkę, dodać do niej komunikat, a następnie odczytać komunikat i usunąć go z kolejki.</span><span class="sxs-lookup"><span data-stu-id="9ff29-102">You will then use the Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="9ff29-103">Te same działania wykonują składniki w aplikacji rozproszonej.</span><span class="sxs-lookup"><span data-stu-id="9ff29-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="9ff29-104">Aplikacja mobilna może na przykład dodać komunikat do kolejki, gdzie oczekuje on na pobranie i przetworzenie przez usługę internetową.</span><span class="sxs-lookup"><span data-stu-id="9ff29-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="9ff29-105">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="9ff29-105">Create a Storage Account</span></span>

<span data-ttu-id="9ff29-106">Ponieważ kolejki usługi Storage są częścią konta usługi Storage ogólnego przeznaczenia platformy Azure,</span><span class="sxs-lookup"><span data-stu-id="9ff29-106">Since Storage queues are part of Azure general purpose Storage accounts.</span></span> <span data-ttu-id="9ff29-107">należy rozpocząć od utworzenia konta usługi Storage:</span><span class="sxs-lookup"><span data-stu-id="9ff29-107">You must start by creating a Storage account:</span></span>

1. <span data-ttu-id="9ff29-108">W przeglądarce przejdź do witryny [Azure Portal](http://portal.azure.com) i zaloguj się przy użyciu swoich zwykłych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="9ff29-108">In a browser, navigate to the [Azure Portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="9ff29-109">W lewym górnym rogu kliknij pozycję **Wszystkie usługi**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-109">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="9ff29-110">Przewiń w dół do sekcji **Storage**, a następnie kliknij przycisk **Konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-110">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="9ff29-111">W lewym górnym rogu bloku**Konta magazynu** kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-111">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![Tworzenie konta magazynu](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="9ff29-113">W polu tekstowym **Nazwa** wpisz unikatową nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9ff29-113">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="9ff29-114">W obszarze **Model wdrożenia** upewnij się, że wybrano opcję **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="9ff29-115">Na liście rozwijanej **Rodzaj konta** wybierz pozycję **Magazyn (ogólnego przeznaczenia wersja 2)**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="9ff29-116">Na liście rozwijanej **Lokalizacja** wybierz pobliski region.</span><span class="sxs-lookup"><span data-stu-id="9ff29-116">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="9ff29-117">Wybierz pozycję **Magazyn lokalnie nadmiarowy (LRS)** z listy rozwijanej **Replikacja**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="9ff29-118">W obszarze **Wydajność** wybierz opcję **Standardowa**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-118">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="9ff29-119">W obszarze **Warstwa dostępu** wybierz pozycję **Chłodna**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-119">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="9ff29-120">W obszarze **Wymagany bezpieczny transfer** wybierz pozycję **Wyłączony**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-120">Under **Secure transfer required** select, **Disabled**.</span></span>
1. <span data-ttu-id="9ff29-121">W obszarze **Subskrypcja** wybierz swoją subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="9ff29-121">Under **Subscription**, select your subscription.</span></span>

    ![Tworzenie konta magazynu](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="9ff29-123">W obszarze **Grupa zasobów** wybierz polecenie **Utwórz nową**, a następnie w polu tekstowym wpisz nazwę **MusicSharingResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-123">Under **Resource group** select **Create new**, and then in the textbox type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="9ff29-124">W obszarze **Sieci wirtualne** wybierz pozycję **Wyłączone**, a następnie kliknij polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-124">Under **Virtual networks** select **Disabled** and then click **Create**.</span></span>

    ![Tworzenie konta magazynu](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="9ff29-126">Na platformie Azure zostanie utworzone nowe konto magazynu i nowa grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="9ff29-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="9ff29-127">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="9ff29-127">Create a Queue</span></span>

<span data-ttu-id="9ff29-128">Po utworzeniu konta usługi Storage możesz dodać do niego nową kolejkę.</span><span class="sxs-lookup"><span data-stu-id="9ff29-128">Now that the Storage Account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="9ff29-129">Należy utworzyć kolejkę przy użyciu poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9ff29-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="9ff29-130">W prawym górnym rogu portalu kliknij link **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Uruchamianie usługi Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="9ff29-132">Na ekranie **Witamy w usłudze Azure Cloud Shell** kliknij przycisk **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="9ff29-133">Jeśli pojawi się ekran **Nie masz zainstalowanego magazynu**, kliknij przycisk **Utwórz magazyn**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="9ff29-134">Aby uzyskać konto magazynu, po wyświetleniu wiersza polecenia `PS Azure` wpisz następujące polecenie, zastępując nazwę `<storageaccountname>` unikatową nazwą Twojego konta magazynu, i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command, substituting `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="9ff29-135">Aby uzyskać kontekst konta magazynu, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-135">To obtain the context of the storage account, type the following command and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="9ff29-136">Aby utworzyć nową kolejkę, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-136">To create a new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="9ff29-137">Dodawanie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="9ff29-137">Add a Message to the Queue</span></span>

<span data-ttu-id="9ff29-138">Po utworzeniu kolejki na koncie magazynu możesz dodać do niej komunikat.</span><span class="sxs-lookup"><span data-stu-id="9ff29-138">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="9ff29-139">Aby utworzyć nowy komunikat, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-139">To create a new message, type the following command and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="9ff29-140">Aby dodać nowy komunikat do nowej kolejki, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-140">To add the new message to the new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="9ff29-141">W witrynie Azure Portal w obszarze nawigacji po lewej stronie kliknij pozycję **Wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-141">In the Azure Portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="9ff29-142">Na liście zasobów kliknij wcześniej utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="9ff29-142">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="9ff29-143">W bloku konta magazynu kliknij pozycję **Eksplorator usługi Storage (wersja zapoznawcza)**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-143">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="9ff29-144">W Eksploratorze usługi Storage w obszarze **KOLEJKI** kliknij pozycję **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-144">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="9ff29-145">W Eksploratorze usługi Storage zostanie wyświetlony dodany komunikat.</span><span class="sxs-lookup"><span data-stu-id="9ff29-145">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="9ff29-146">Pobieranie i usuwanie komunikatu</span><span class="sxs-lookup"><span data-stu-id="9ff29-146">Retrieve and Remove the Message</span></span>

<span data-ttu-id="9ff29-147">Docelowy składnik komunikatu w kolejce usługi Storage musi pobrać komunikat znajdujący się na początku kolejki, przetworzyć go, a następnie usunąć z kolejki, tak aby nie mogły go pobrać inne składniki:</span><span class="sxs-lookup"><span data-stu-id="9ff29-147">A destination component for a message in a Storage queue, must retrieve the message at the front of the queue, process it, and then delete it from the queue so that other components do not retrieve it:</span></span>

1. <span data-ttu-id="9ff29-148">Aby pobrać komunikat znajdujący się na początku kolejki w usłudze Azure Cloud Shell, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-148">In the Azure Cloud Shell, to get the message at the front of the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="9ff29-149">Aby wyświetlić komunikat, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-149">To display the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="9ff29-150">Aby wyświetlić wszystkie właściwości komunikatu, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-150">To display all the properties of the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="9ff29-151">Aby usunąć komunikat z kolejki, wpisz następujące polecenie i naciśnij przycisk Enter:</span><span class="sxs-lookup"><span data-stu-id="9ff29-151">To remove the message from the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="9ff29-152">Aby odświeżyć wyświetlaną kolejkę w bloku Konto magazynu w witrynie Azure Portal, kliknij przycisk **Przegląd**, a następnie kliknij pozycję **Eksplorator usługi Storage**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-152">In the Azure Portal, to refresh the queue display, in the Storage Account blade, click **Overview** and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="9ff29-153">W obszarze **KOLEJKI** kliknij pozycję **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="9ff29-153">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="9ff29-154">W Eksploratorze usługi Storage zobaczysz, że kolejka jest pusta, ponieważ jedyny komunikat został usunięty.</span><span class="sxs-lookup"><span data-stu-id="9ff29-154">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="9ff29-155">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="9ff29-155">Cleanup</span></span>

<span data-ttu-id="9ff29-156">Aby usunąć wszystkie zasoby utworzone w tym ćwiczeniu, wprowadź następujące polecenie w usłudze Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9ff29-156">To remove all resources created during this exercise enter the following command in the Azure Cloud Shell</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="9ff29-157">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9ff29-157">Summary</span></span>

<span data-ttu-id="9ff29-158">Utworzono konto usługi Storage w ramach subskrypcji platformy Azure i utworzono na nim nową kolejkę.</span><span class="sxs-lookup"><span data-stu-id="9ff29-158">Here, you created a Storage Account in your Azure subscription and created a new queue in it.</span></span> <span data-ttu-id="9ff29-159">Użyto również programu PowerShell, aby symulować działania składników aplikacji rozproszonej poprzez dodanie komunikatu do kolejki, a następnie pobranie go i usunięcie.</span><span class="sxs-lookup"><span data-stu-id="9ff29-159">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue and then retrieving and removing it.</span></span>

<span data-ttu-id="9ff29-160">Kolejki konta usługi Azure Storage są dobrym rozwiązaniem, gdy chcesz przekazywać komunikaty pomiędzy składnikami aplikacji rozproszonej.</span><span class="sxs-lookup"><span data-stu-id="9ff29-160">Azure Storage Account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="9ff29-161">Jeśli chcesz publikować zdarzenia, kolejki usługi Storage nie są dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="9ff29-161">Do not choose Storage queues when you want to publish events.</span></span>