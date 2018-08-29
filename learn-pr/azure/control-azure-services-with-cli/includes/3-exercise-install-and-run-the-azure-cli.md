
<span data-ttu-id="a47e2-101">W tym ćwiczeniu zainstalujesz interfejs wiersza polecenia platformy Azure na komputerze lokalnym, a następnie uruchomisz proste polecenie, aby zweryfikować swoją instalację.</span><span class="sxs-lookup"><span data-stu-id="a47e2-101">In this exercise, you will install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> 

## <a name="installing-the-azure-cli"></a><span data-ttu-id="a47e2-102">Instalowanie interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a47e2-102">Installing the Azure CLI</span></span>
<span data-ttu-id="a47e2-103">Metoda instalowania interfejsu wiersza polecenia platformy Azure zależy od systemu operacyjnego komputera.</span><span class="sxs-lookup"><span data-stu-id="a47e2-103">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="a47e2-104">Wybierz procedurę dla używanego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="a47e2-104">Please choose the steps for your operating system.</span></span>

### <a name="linux"></a><span data-ttu-id="a47e2-105">Linux</span><span class="sxs-lookup"><span data-stu-id="a47e2-105">Linux</span></span>
<span data-ttu-id="a47e2-106">Interfejs wiersza polecenia platformy Azure zostanie zainstalowany w systemie Ubuntu Linux przy użyciu zaawansowanego narzędzia do tworzenia pakietów (**apt**) i wiersza polecenia powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="a47e2-106">Here you will install the Azure CLI on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!NOTE]
> <span data-ttu-id="a47e2-107">Lista poleceń przedstawionych poniżej dotyczy systemu Ubuntu w wersji 18.04.</span><span class="sxs-lookup"><span data-stu-id="a47e2-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="a47e2-108">Jeśli używasz innej wersji systemu Ubuntu, musisz dodać inne repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a47e2-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="a47e2-109">Aby uzyskać szczegółowe informacje, zobacz [Instalacja interfejsu wiersza polecenia platformy Azure 2.0 przy użyciu narzędzia apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="a47e2-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="a47e2-110">Zmodyfikuj swoją listę źródeł tak, aby repozytorium firmy Microsoft było zarejestrowane, a menedżer pakietów mógł zlokalizować pakiet interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e2-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. <span data-ttu-id="a47e2-111">Zaimportuj klucz szyfrowania dla repozytorium Microsoft Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a47e2-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="a47e2-112">Dzięki temu menedżer pakietów może sprawdzić, czy instalowany pakiet interfejsu wiersza polecenia platformy Azure pochodzi z firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a47e2-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="a47e2-113">Zainstaluj interfejs wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e2-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a><span data-ttu-id="a47e2-114">macOS</span><span class="sxs-lookup"><span data-stu-id="a47e2-114">macOS</span></span>
<span data-ttu-id="a47e2-115">Interfejs wiersza polecenia platformy Azure zostanie zainstalowany w systemie macOS przy użyciu menedżera pakietów Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a47e2-115">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a47e2-116">Jeśli polecenie **brew** jest niedostępne, może być konieczne zainstalowanie menedżera pakietów Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a47e2-116">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="a47e2-117">Aby uzyskać szczegółowe informacje, zobacz [witrynę internetową oprogramowania Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="a47e2-117">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="a47e2-118">Zaktualizuj repozytorium brew, aby upewnić się, że masz najnowszy pakiet interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e2-118">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```
1. <span data-ttu-id="a47e2-119">Zainstaluj interfejs wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e2-119">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a><span data-ttu-id="a47e2-120">Windows</span><span class="sxs-lookup"><span data-stu-id="a47e2-120">Windows</span></span>
<span data-ttu-id="a47e2-121">Interfejs wiersza polecenia platformy Azure zostanie zainstalowany w systemie Windows za pomocą Instalatora MSI.</span><span class="sxs-lookup"><span data-stu-id="a47e2-121">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="a47e2-122">Przejdź na stronę [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) i w oknie dialogowym zabezpieczeń przeglądarki kliknij pozycję **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="a47e2-122">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="a47e2-123">W oknie instalatora zaakceptuj postanowienia licencyjne, a następnie kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="a47e2-123">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="a47e2-124">W oknie dialogowym **Kontrola konta użytkownika** wybierz opcję **Tak**.</span><span class="sxs-lookup"><span data-stu-id="a47e2-124">In the **User Account Control** dialog, select **Yes**.</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="a47e2-125">Uruchamianie interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a47e2-125">Running the Azure CLI</span></span>
<span data-ttu-id="a47e2-126">Aby uruchomić wiersz polecenia platformy Azure, należy otworzyć powłokę bash (Linux i macOS) lub użyć wiersza polecenia bądź programu PowerShell (Windows).</span><span class="sxs-lookup"><span data-stu-id="a47e2-126">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="a47e2-127">Uruchom interfejs wiersza polecenia platformy Azure i zweryfikuj instalację, uruchamiając sprawdzanie wersji.</span><span class="sxs-lookup"><span data-stu-id="a47e2-127">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

> [!NOTE]
> <span data-ttu-id="a47e2-128">W systemie Windows uruchomienie interfejsu wiersza polecenia platformy Azure za pomocą programu PowerShell ma kilka zalet w porównaniu z uruchomieniem go z poziomu wiersza polecenia. Program PowerShell na przykład oferuje dodatkowe funkcje uzupełniania po naciśnięciu tabulatora w porównaniu z funkcjami dostępnymi z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a47e2-128">In Windows, running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the command prompt; for example, PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

## <a name="summary"></a><span data-ttu-id="a47e2-129">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a47e2-129">Summary</span></span>
<span data-ttu-id="a47e2-130">W tym ćwiczeniu skonfigurowaliśmy komputery lokalne pod kątem administrowania zasobami platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e2-130">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="a47e2-131">Teraz można lokalnie używać interfejsu wiersza polecenia platformy Azure do wprowadzania poleceń lub wykonywania skryptów.</span><span class="sxs-lookup"><span data-stu-id="a47e2-131">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="a47e2-132">Interfejs wiersza polecenia platformy Azure przekaże polecenia do centrów danych platformy Azure, gdzie są wykonywane w ramach używanej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e2-132">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
