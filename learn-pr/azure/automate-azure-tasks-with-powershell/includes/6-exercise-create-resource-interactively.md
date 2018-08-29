<span data-ttu-id="1ee4b-101">Załóżmy, że pracujesz w firmie, która tworzy pakiet narzędzi administracyjnych dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="1ee4b-102">Twoje zadanie polega na ułatwieniu potencjalnym klientom wypróbowanie Twojego oprogramowania przed zakupem.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="1ee4b-103">Ponieważ oprogramowanie wprowadza zmiany systemu operacyjnego na poziomie administratora, podjęto decyzję o utworzeniu maszyny wirtualnej z systemem Linux dla każdego klienta wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="1ee4b-104">Tworzysz maszyny wirtualne w miarę potrzeb i usuwasz je na koniec okresu subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="1ee4b-105">Dzięki temu każdy klient rozpoczyna od czystej wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="1ee4b-106">Aby zachować separację tych maszyn wirtualnych od maszyn wirtualnych używanych przez firmę do testów wewnętrznych, utworzysz dedykowaną grupę zasobów na potrzeby ich przechowywania.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="1ee4b-107">Wystarczy tylko jedna grupa zasobów, dlatego użycie programu Azure PowerShell w trybie interaktywnym to rozsądny wybór dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="1ee4b-108">Kroki tworzenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="1ee4b-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="1ee4b-109">Uruchom program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="1ee4b-110">Zaimportuj moduł do bieżącej sesji, aby uzyskać dostęp do poleceń cmdlet platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="1ee4b-111">Połącz się z platformą Azure za pomocą polecenia pokazanego poniżej.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="1ee4b-112">Po podaniu polecenia uwierzytelnij się, podając poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="1ee4b-113">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="1ee4b-114">Zweryfikuj, czy grupa zasobów została utworzona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="1ee4b-115">Inny sposób sprawdzenia, czy grupa zasobów została utworzona pomyślnie, to użycie witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="1ee4b-116">Aby to zrobić, zaloguj się do witryny Portal i przejdź do sekcji **Grupy zasobów** (zobacz poniżej).</span><span class="sxs-lookup"><span data-stu-id="1ee4b-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="1ee4b-117">Nowa grupa zasobów powinna zostać wyświetlona na liście.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-117">The new resource group should be displayed in the list.</span></span>

![Używanie witryny Azure Portal do wyświetlania listy grup zasobów](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="1ee4b-119">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="1ee4b-119">Summary</span></span>
<span data-ttu-id="1ee4b-120">To ćwiczenie przedstawia typowy wzorzec interaktywnej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-120">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="1ee4b-121">Użyto standardowego polecenia cmdlet do zaimportowania modułu AzureRM, a następnie poleceń cmdlet programu Azure PowerShell do wykonania określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-121">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="1ee4b-122">Teraz dysponujesz grupą zasobów w ramach subskrypcji i wszystko jest gotowe do tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1ee4b-122">You now have a resource group in your subscription and are ready to create VMs.</span></span>