<span data-ttu-id="fad31-101">W tym ćwiczeniu utworzysz maszynę wirtualną z systemem Windows na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fad31-101">In this exercise, you'll create a Windows virtual machine in Azure.</span></span>

## <a name="motivation"></a><span data-ttu-id="fad31-102">Motywacja</span><span class="sxs-lookup"><span data-stu-id="fad31-102">Motivation</span></span>

<span data-ttu-id="fad31-103">Rozważmy alternatywny scenariusz dla tego ćwiczenia.</span><span class="sxs-lookup"><span data-stu-id="fad31-103">Let's consider an alternate scenario for this exercise.</span></span> <span data-ttu-id="fad31-104">Twoja organizacja jest uczelnią, która wykorzystuje maszyny wirtualne z systemem Windows do usprawnienia środowisk testowych, w których studenci instalują aplikacje internetowe, konfigurują domeny i eksplorują usługi oraz funkcje systemu Windows bez wywierania wpływu na komputery uczelniane.</span><span class="sxs-lookup"><span data-stu-id="fad31-104">Here, your organization is a school that uses Windows virtual machines to spin up test environments on which students install web apps, configure domains, and explore Windows services and features without affecting the school's computers.</span></span> <span data-ttu-id="fad31-105">Nauczyciele łączą się z tymi maszynami wirtualnymi przy użyciu protokołu RDP, aby sprawdzić postępy studentów.</span><span class="sxs-lookup"><span data-stu-id="fad31-105">Teachers connect to these VMs by using RDP and check on student progress.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="fad31-106">Tworzenie maszyny wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="fad31-106">Create a Windows VM</span></span>

<span data-ttu-id="fad31-107">Aby utworzyć maszynę wirtualną z systemem Windows, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fad31-107">To create a Windows VM, complete the following steps:</span></span>

1. <span data-ttu-id="fad31-108">Zaloguj się do platformy Azure za pośrednictwem witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fad31-108">Log onto Azure through the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="fad31-109">W lewym górnym rogu witryny Azure Portal kliknij pozycję **Utwórz zasób**.</span><span class="sxs-lookup"><span data-stu-id="fad31-109">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="fad31-110">Na **pasku wyszukiwania** wprowadź **Windows Server 2016 Datacenter** i kliknij link o takim samym tytule.</span><span class="sxs-lookup"><span data-stu-id="fad31-110">In the **search bar**, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title.</span></span>

### <a name="configure-the-vm-settings"></a><span data-ttu-id="fad31-111">Konfigurowanie ustawień maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fad31-111">Configure the VM settings</span></span>

1. <span data-ttu-id="fad31-112">W obszarze **Informacje podstawowe** w polu **Nazwa** wprowadź nazwę maszyny wirtualnej, na przykład „StudentVM”.</span><span class="sxs-lookup"><span data-stu-id="fad31-112">Under **Basics**, in the **Name** field, enter a name for your VM, such as "StudentVM."</span></span>

1. <span data-ttu-id="fad31-113">W polu **Typ dysku maszyny wirtualnej** kliknij menu rozwijane, aby wyświetlić opcje.</span><span class="sxs-lookup"><span data-stu-id="fad31-113">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="fad31-114">Upewnij się, że wybrano pozycję **SSD**.</span><span class="sxs-lookup"><span data-stu-id="fad31-114">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="fad31-115">W polu **Nazwa użytkownika** wprowadź odpowiednią nazwę użytkownika używaną na potrzeby logowania się do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fad31-115">In the **Username** field, enter a suitable user name to use to sign in to the VM.</span></span>

1. <span data-ttu-id="fad31-116">W polu **Hasło** wprowadź hasło składające się z co najmniej 12 znaków.</span><span class="sxs-lookup"><span data-stu-id="fad31-116">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="fad31-117">Hasło musi zawierać małe i wielkie litery, cyfry i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="fad31-117">It must also have upper and lowercase characters, numbers, and special characters.</span></span>

1. <span data-ttu-id="fad31-118">W obszarze **Grupa zasobów** kliknij pozycję **Utwórz nową**.</span><span class="sxs-lookup"><span data-stu-id="fad31-118">Under **Resource group**, click **Create new**.</span></span> <span data-ttu-id="fad31-119">Nazwij grupę zasobów, na przykład „myTestRG”.</span><span class="sxs-lookup"><span data-stu-id="fad31-119">Give the resource group a name, such as "myTestRG."</span></span>

1. <span data-ttu-id="fad31-120">Wybierz odpowiednią lokalizację dla tworzonej maszyny wirtualnej i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fad31-120">Select a suitable location for the VM to be created, and then click **OK**.</span></span>

### <a name="select-the-vm-image-size-and-options"></a><span data-ttu-id="fad31-121">Wybieranie rozmiaru obrazu maszyny wirtualnej i opcji</span><span class="sxs-lookup"><span data-stu-id="fad31-121">Select the VM image size and options</span></span>

1. <span data-ttu-id="fad31-122">Na stronie **Wybierz rozmiar** kliknij obraz **B1s**, a następnie kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="fad31-122">In the **Choose a size** page, click the **B1s** image, and then click **Select**.</span></span>

   > [!Note] 
   > <span data-ttu-id="fad31-123">Obraz B1 ma tylko 1 GB pamięci RAM i dlatego podczas pierwszego logowania będą występować błędy pamięci.</span><span class="sxs-lookup"><span data-stu-id="fad31-123">The B1 image has only 1 GB of RAM and will result in memory errors when you first sign in.</span></span> <span data-ttu-id="fad31-124">Można jednak zmienić rozmiar tego obrazu później w ramach następnych ćwiczeń.</span><span class="sxs-lookup"><span data-stu-id="fad31-124">However, you can resize the image later as part of a later lab.</span></span>

1. <span data-ttu-id="fad31-125">Na stronie **Ustawienia** w obszarze **Wybieranie publicznych portów wejściowych** wybierz opcję **Brak publicznych portów wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="fad31-125">In the **Settings** page, under **Select Public Inbound Ports**, select **No public inbound ports**.</span></span> <span data-ttu-id="fad31-126">Dostęp za pomocą protokołu RDP skonfigurujemy później.</span><span class="sxs-lookup"><span data-stu-id="fad31-126">We'll configure RDP access later.</span></span>

### <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="fad31-127">Kończenie konfigurowania maszyny wirtualnej i tworzenie obrazu</span><span class="sxs-lookup"><span data-stu-id="fad31-127">Finish configuring the VM and create the image</span></span>

1. <span data-ttu-id="fad31-128">Przewiń w dół i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fad31-128">Scroll to the bottom and click **OK**.</span></span>

1. <span data-ttu-id="fad31-129">W obszarze **Utwórz** sprawdź skonfigurowane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fad31-129">Under **Create**, check the settings that you configured.</span></span> <span data-ttu-id="fad31-130">Na dole kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fad31-130">At the bottom, click **Create**.</span></span> <span data-ttu-id="fad31-131">Na pulpicie nawigacyjnym platformy Azure zostanie wyświetlona wdrażana maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="fad31-131">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="fad31-132">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="fad31-132">This may take several minutes.</span></span>

## <a name="summary"></a><span data-ttu-id="fad31-133">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fad31-133">Summary</span></span>

<span data-ttu-id="fad31-134">Utworzono maszynę wirtualną z systemem Windows Server, która spełnia wymagania studentów i jest dostępna z sieci uczelni.</span><span class="sxs-lookup"><span data-stu-id="fad31-134">You've now created a Windows Server virtual machine that's suitable for student requirements and accessible from the school network.</span></span> <span data-ttu-id="fad31-135">W następnym module zobaczysz, jak można za pomocą protokołu RDP nawiązać połączenie z maszyną wirtualną i nią zarządzać.</span><span class="sxs-lookup"><span data-stu-id="fad31-135">In the next unit, you will look at how you connect to and manage that VM by using RDP.</span></span>
