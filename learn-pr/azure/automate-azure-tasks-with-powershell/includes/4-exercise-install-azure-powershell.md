<span data-ttu-id="8a9f5-101">W tym ćwiczeniu zainstalujemy moduł **Azure PowerShell** na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-101">In this exercise, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="8a9f5-102">Wybierz sekcję odpowiadająca swojemu systemowi operacyjnemu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-102">Choose the appropriate section for your operating system.</span></span>

## <a name="linux-and-mac"></a><span data-ttu-id="8a9f5-103">Linux i Mac</span><span class="sxs-lookup"><span data-stu-id="8a9f5-103">Linux and Mac</span></span>
<span data-ttu-id="8a9f5-104">W systemach Linux i macOS przede wszystkim należy zainstalować program **PowerShell Core**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="8a9f5-105">Linux</span><span class="sxs-lookup"><span data-stu-id="8a9f5-105">Linux</span></span>
<span data-ttu-id="8a9f5-106">Jak wspomniano w poprzednim module, instalacja programu PowerShell dla systemu Linux wymaga użycia menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-106">As mentioned in the last unit, installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="8a9f5-107">W tym przykładzie użyjemy systemu **Ubuntu 18.04**, jednak [w dokumentacji są dostępne szczegółowe instrukcje dla innych wersji i dystrybucji](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="8a9f5-108">Program PowerShell Core zostanie zainstalowany w systemie Ubuntu Linux przy użyciu zaawansowanego narzędzia do tworzenia pakietów (**apt**) i wiersza polecenia powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="8a9f5-109">Zaimportuj klucz szyfrowania dla repozytorium Microsoft Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="8a9f5-110">Dzięki temu menedżer pakietów może sprawdzić, czy instalowany pakiet programu PowerShell Core pochodzi z firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="8a9f5-111">Zarejestruj **repozytorium Microsoft Ubuntu**, aby umożliwić menedżerowi pakietów zlokalizowanie pakietu programu PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="8a9f5-112">Zaktualizuj listę pakietów.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="8a9f5-113">Zainstaluj program PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="8a9f5-114">Uruchom program PowerShell, aby sprawdzić, czy instalacja przebiegła poprawnie.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="8a9f5-115">macOS</span><span class="sxs-lookup"><span data-stu-id="8a9f5-115">macOS</span></span>
<span data-ttu-id="8a9f5-116">Następnie zainstaluj program **PowerShell Core** w systemie macOS przy użyciu menedżera pakietów Homebrew.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-116">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a9f5-117">Jeśli polecenie **brew** jest niedostępne, może być konieczne zainstalowanie menedżera pakietów Homebrew.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-117">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="8a9f5-118">Aby uzyskać szczegółowe informacje, zobacz [witrynę internetową oprogramowania Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="8a9f5-118">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="8a9f5-119">Zainstaluj aplikację Homebrew Cask, aby uzyskać więcej pakietów, w tym pakiet programu PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-119">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```
1. <span data-ttu-id="8a9f5-120">Zainstaluj program PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-120">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="8a9f5-121">Uruchom program PowerShell Core, aby sprawdzić, czy instalacja przebiegła poprawnie:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-121">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="8a9f5-122">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a9f5-122">Install Azure PowerShell</span></span>
<span data-ttu-id="8a9f5-123">Po zainstalowaniu podstawowego produktu **PowerShell** zainstaluj moduł **Azure PowerShell** umożliwiający dodanie poleceń specyficznych dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-123">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="8a9f5-124">Windows</span><span class="sxs-lookup"><span data-stu-id="8a9f5-124">Windows</span></span>
<span data-ttu-id="8a9f5-125">Zainstaluj moduł Azure PowerShell w systemie Windows za pomocą polecenia programu PowerShell `Install-Module`.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-125">Install Azure PowerShell on Windows using the `Install-Module` PowerShell command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a9f5-126">Do zainstalowania modułu Azure PowerShell jest wymagany program PowerShell w wersji 5.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-126">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="8a9f5-127">Aby sprawdzić wersję programu PowerShell, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-127">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="8a9f5-128">Jeśli numer wersji jest mniejszy niż 5.0, [uaktualnij program Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell) zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-128">If the version number is lower than 5.0, follow the instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="8a9f5-129">Otwórz menu **Start** i wpisz **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-129">Open the **Start** menu and type **Windows PowerShell**.</span></span>
2. <span data-ttu-id="8a9f5-130">Kliknij prawym przyciskiem myszy ikonę programu **Windows PowerShell** i wybierz polecenie **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-130">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>
3. <span data-ttu-id="8a9f5-131">W oknie dialogowym **Kontrola konta użytkownika** wybierz opcję **Tak**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-131">In the **User Account Control** dialog, select **Yes**.</span></span>
4. <span data-ttu-id="8a9f5-132">Wprowadź następujące polecenie i naciśnij klawisz Enter:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-132">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```
5. <span data-ttu-id="8a9f5-133">Jeśli zostanie wyświetlony monit dotyczący wiarygodności modułów z galerii programu PowerShell, wybierz opcję **Tak** lub **Tak na wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-133">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9f5-134">Jeśli pojawi się komunikat o błędzie z informacją o tym, że już zainstalowano wersję modułu Azure Powershell, możesz wykonać aktualizację do _najnowszej_ wersji za pomocą polecenia:</span><span class="sxs-lookup"><span data-stu-id="8a9f5-134">If you get an error message indicating that a version of the Azure Powershell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>
> 
> `Update-Module -Name AzureRM`
> 
> <span data-ttu-id="8a9f5-135">Podobnie jak w przypadku polecenia `Install-Module`, odpowiedz **Tak** lub **Tak na wszystkie** po wyświetleniu monitu dotyczącego wiarygodności modułu.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-135">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="8a9f5-136">Linux lub macOS</span><span class="sxs-lookup"><span data-stu-id="8a9f5-136">Linux or macOS</span></span>
<span data-ttu-id="8a9f5-137">Używamy podobnego podstawowego procesu, aby zainstalować moduł Azure PowerShell w systemach Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-137">We use the same basic process to install the Azure PowerShell on either Linux or macOS.</span></span> <span data-ttu-id="8a9f5-138">Procedura jest taka sama w obu systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-138">The procedure is the same for both operating systems.</span></span> <span data-ttu-id="8a9f5-139">Różnica dotyczy uruchomienia sesji programu PowerShell Core z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-139">The difference is in getting an elevated PowerShell Core session.</span></span>

1. <span data-ttu-id="8a9f5-140">W terminalu wpisz następujące polecenie, aby uruchomić program PowerShell Core z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-140">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="8a9f5-141">Aby zainstalować moduł Azure PowerShell, uruchom następujące polecenie w wierszu polecenia programu PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-141">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="8a9f5-142">Jeśli zostanie wyświetlony monit dotyczący wiarygodności modułów z **galerii programu PowerShell**, wybierz opcję **Tak** lub **Tak na wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-142">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="8a9f5-143">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="8a9f5-143">Summary</span></span>
<span data-ttu-id="8a9f5-144">W tym ćwiczeniu skonfigurowaliśmy komputery lokalne pod kątem administrowania zasobami platformy Azure przy użyciu modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-144">You setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="8a9f5-145">Można teraz lokalnie używać modułu Azure PowerShell do wprowadzania poleceń lub wykonywanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-145">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="8a9f5-146">Moduł Azure PowerShell przekazuje polecenia do centrów danych platformy Azure, gdzie są wykonywane w ramach używanej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9f5-146">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>