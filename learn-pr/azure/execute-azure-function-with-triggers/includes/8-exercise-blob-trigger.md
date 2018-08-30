<span data-ttu-id="05595-101">Podczas tego ćwiczenia utworzymy funkcję platformy Azure, która wyświetla nazwę i rozmiar obiektu blob, gdy jest on tworzony lub aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="05595-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="05595-102">Aby wykonać to ćwiczenie, musisz zalogować się w witrynie [Azure Portal](https://portal.azure.com/) przy użyciu prawidłowego konta.</span><span class="sxs-lookup"><span data-stu-id="05595-102">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="05595-103">Tworzenie wyzwalacza obiektu blob</span><span class="sxs-lookup"><span data-stu-id="05595-103">Create a blob trigger</span></span>

<span data-ttu-id="05595-104">Ponownie kontynuujmy korzystanie z naszej istniejącej aplikacji usługi Azure Functions i dodajmy wyzwalacz obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="05595-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="05595-105">Wskaż pozycję **Funkcje** i wybierz ikonę plus (+).</span><span class="sxs-lookup"><span data-stu-id="05595-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Wskazywanie pozycji Funkcje i wybieranie ikony plusa](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="05595-107">Wybierz pozycję **Wyzwalacz obiektu blob**.</span><span class="sxs-lookup"><span data-stu-id="05595-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="05595-108">Wybierz język **C#**.</span><span class="sxs-lookup"><span data-stu-id="05595-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="05595-109">W polu **Nazwa** pozostaw wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="05595-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="05595-110">W polu **Ścieżka** pozostaw wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="05595-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="05595-111">Wybierz istniejące konto usługi Azure Storage lub wybierz pozycję **Utwórz**, jeśli chcesz utworzyć nowe konto na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="05595-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="download-storage-explorer"></a><span data-ttu-id="05595-112">Pobieranie Eksploratora usługi Storage</span><span class="sxs-lookup"><span data-stu-id="05595-112">Download Storage explorer</span></span>

<span data-ttu-id="05595-113">Teraz, gdy utworzyliśmy wyzwalacz obiektu blob, pobierz Eksploratora usługi Storage, który pozwoli na łatwe utworzenie obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="05595-113">Now that we've created a blob trigger, let's download Storage explorer, which will allow us to easily create a blob.</span></span>

- <span data-ttu-id="05595-114">Pobierz [Eksploratora usługi Storage](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="05595-114">Download [Storage explorer](http://storageexplorer.com).</span></span>

## <a name="connect-to-your-azure-storage-account"></a><span data-ttu-id="05595-115">Nawiązywanie połączenia z kontem usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="05595-115">Connect to your Azure Storage account</span></span>

<span data-ttu-id="05595-116">Pobraliśmy już Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="05595-116">We now have Storage explorer downloaded.</span></span> <span data-ttu-id="05595-117">Zalogujmy się przy użyciu podanych przez nas poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="05595-117">Let's sign in using the credentials that were supplied.</span></span>

1. <span data-ttu-id="05595-118">W Eksploratorze usługi Storage wybierz ikonę plusa (+) po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="05595-118">In Storage explorer, select the plus (+) icon on the left.</span></span>

1. <span data-ttu-id="05595-119">Wybierz pozycję **Użyj klucza i nazwy konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="05595-119">Select **Use a storage account name and key**.</span></span>

1. <span data-ttu-id="05595-120">Wybierz opcję **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="05595-120">Select **Next**.</span></span>

1. <span data-ttu-id="05595-121">Na platformie Azure w obszarze wyzwalacza obiektu blob wybierz pozycję **Zintegruj**.</span><span class="sxs-lookup"><span data-stu-id="05595-121">In Azure, under your blob trigger, select **Integrate**.</span></span>

1. <span data-ttu-id="05595-122">Wybierz pozycję **Dokumentacja**, aby rozszerzyć widok.</span><span class="sxs-lookup"><span data-stu-id="05595-122">Select **Documentation** to expand the view.</span></span>

1. <span data-ttu-id="05595-123">Skopiuj wartości **Nazwa konta** i **Klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="05595-123">Copy the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="05595-124">W Eksploratorze usługi Storage wklej skopiowane właśnie wartości **Nazwa konta** i **Klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="05595-124">Back in Storage explorer, paste in the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="05595-125">Wypełnij pole **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="05595-125">Enter a **Display name**.</span></span> <span data-ttu-id="05595-126">Ta wartość jest nazwą połączenia w Eksploratorze usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="05595-126">This value is the name of the connection in Storage explorer.</span></span>

1. <span data-ttu-id="05595-127">Wybierz opcję **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="05595-127">Select **Next**.</span></span>

1. <span data-ttu-id="05595-128">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="05595-128">Select **Connect**.</span></span> 

## <a name="create-a-blob-container"></a><span data-ttu-id="05595-129">Tworzenie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="05595-129">Create a blob container</span></span>

<span data-ttu-id="05595-130">Nie jesteśmy połączeni z naszym kontem usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="05595-130">We aren't connected to our Azure Storage account.</span></span> <span data-ttu-id="05595-131">Pamiętaj, że nasz wyzwalacz obiektu blob monitoruje tylko lokalizację opisaną w polu **Ścieżka**.</span><span class="sxs-lookup"><span data-stu-id="05595-131">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="05595-132">Domyślnie ścieżka powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="05595-132">By default, our path should be:</span></span>

> <span data-ttu-id="05595-133">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="05595-133">samples-workitems/{name}</span></span>

<span data-ttu-id="05595-134">Musimy utworzyć kontener o nazwie **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="05595-134">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="05595-135">W Eksploratorze usługi Storage rozwiń swoje konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="05595-135">In Storage explorer, expand your storage account.</span></span> <span data-ttu-id="05595-136">Jego nazwa powinna być zgodna z wartością wprowadzoną w polu **Nazwa wyświetlana** podczas procesu połączenia.</span><span class="sxs-lookup"><span data-stu-id="05595-136">The name should be the **Display name** that you provided during the connection process.</span></span>

1. <span data-ttu-id="05595-137">Kliknij prawym przyciskiem myszy pozycję **Kontenery obiektów blob** i wybierz pozycję **Utwórz kontener obiektów blob**.</span><span class="sxs-lookup"><span data-stu-id="05595-137">Right-click **Blob Containers** and select **Create blob container**.</span></span>

1. <span data-ttu-id="05595-138">Wprowadź ciąg **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="05595-138">Enter **samples-workitems**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="05595-139">Włączanie wyzwalacza obiektu blob</span><span class="sxs-lookup"><span data-stu-id="05595-139">Turn on your blob trigger</span></span>

<span data-ttu-id="05595-140">Teraz, gdy utworzyliśmy kontener do monitorowania, uruchomimy naszą funkcję, aby wyświetlić dane wyjściowe podczas tworzenia obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="05595-140">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="05595-141">Wybierz swój wyzwalacz obiektu blob, aby otworzyć ekran kodu.</span><span class="sxs-lookup"><span data-stu-id="05595-141">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="05595-142">Wybierz pozycję **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="05595-142">Select **Run**.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="05595-143">Tworzenie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="05595-143">Create a blob</span></span>

<span data-ttu-id="05595-144">Wyzwalacz obiektu blob jest teraz włączony i nasłuchuje działań.</span><span class="sxs-lookup"><span data-stu-id="05595-144">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="05595-145">Utwórzmy obiekt blob, aby sprawdzić, czy uzyskamy komunikat dziennika.</span><span class="sxs-lookup"><span data-stu-id="05595-145">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="05595-146">W Eksploratorze usługi Storage wybierz kontener **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="05595-146">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="05595-147">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="05595-147">Select **Upload**.</span></span> 

1. <span data-ttu-id="05595-148">Wybierz pozycję **Przekaż pliki**.</span><span class="sxs-lookup"><span data-stu-id="05595-148">Select **Upload Files**.</span></span>

1. <span data-ttu-id="05595-149">Wybierz dowolny plik z komputera.</span><span class="sxs-lookup"><span data-stu-id="05595-149">Select any file from your computer.</span></span>

1. <span data-ttu-id="05595-150">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="05595-150">Select **Upload**.</span></span>

1. <span data-ttu-id="05595-151">Wróć do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="05595-151">Go back to Azure.</span></span> <span data-ttu-id="05595-152">Sprawdź, czy w dziennikach znajduje się komunikat informujący o przekazanym pliku.</span><span class="sxs-lookup"><span data-stu-id="05595-152">Check your logs for a message that displays what file was uploaded.</span></span>

## <a name="clean-up"></a><span data-ttu-id="05595-153">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="05595-153">Clean up</span></span>

<span data-ttu-id="05595-154">Aby upewnić się, że za tę funkcję nie zostaną naliczone opłaty, nad oknem dziennika wybierz polecenie **Wstrzymaj**.</span><span class="sxs-lookup"><span data-stu-id="05595-154">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Wstrzymaj](../media-drafts/4-pause-timer.png)


