<span data-ttu-id="84568-101">W tym ćwiczeniu będziesz kontynuować pracę z przykładem firmy, która tworzy narzędzia administracyjne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="84568-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="84568-102">Przypomnij sobie, że planujesz używać maszyn wirtualnych z systemem Linux, aby umożliwić potencjalnym klientom testowanie swojego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="84568-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="84568-103">Masz już gotową grupę zasobów i teraz nadszedł czas na utworzenie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84568-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="84568-104">Twoja firma ma opłacone stoisko na dużych targach dotyczących systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="84568-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="84568-105">Planujesz obszar pokazu zawierający trzy terminale, z których każdy będzie połączony z osobną maszyną wirtualną systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="84568-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="84568-106">Na koniec każdego dnia chcesz usunąć maszyny wirtualne i utworzyć je ponownie, aby następnego dnia rano były gotowe do użytku.</span><span class="sxs-lookup"><span data-stu-id="84568-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="84568-107">Ręczne tworzenie maszyn wirtualnych po pracy, w stanie zmęczenia, może prowadzić do popełnienia błędów.</span><span class="sxs-lookup"><span data-stu-id="84568-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="84568-108">W celu zautomatyzowania procesu tworzenia maszyn wirtualnych warto utworzyć skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84568-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="84568-109">Pisanie skryptu tworzącego maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="84568-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="84568-110">Wykonaj następujące kroki, aby napisać skrypt:</span><span class="sxs-lookup"><span data-stu-id="84568-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="84568-111">Utwórz nowy plik tekstowy o nazwie **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="84568-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

2. <span data-ttu-id="84568-112">Przechwyć parametr w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="84568-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

3. <span data-ttu-id="84568-113">Uwierzytelnij się na platformie Azure przy użyciu swoich poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="84568-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

4. <span data-ttu-id="84568-114">Wyświetl monit o podanie nazwy użytkownika i hasła dla konta administratora maszyny wirtualnej i przechwyć wynik w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="84568-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. <span data-ttu-id="84568-115">Utwórz pętlę wykonywaną trzy razy:</span><span class="sxs-lookup"><span data-stu-id="84568-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. <span data-ttu-id="84568-116">W treści pętli utwórz nazwę dla każdej maszyny wirtualnej i zapisz je w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="84568-116">In the loop body, create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. <span data-ttu-id="84568-117">Następnie utwórz maszynę wirtualną przy użyciu zmiennej `$vmName`:</span><span class="sxs-lookup"><span data-stu-id="84568-117">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. <span data-ttu-id="84568-118">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="84568-118">Save the file.</span></span>

<span data-ttu-id="84568-119">Ukończony skrypt powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="84568-119">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="84568-120">Uruchamianie skryptu</span><span class="sxs-lookup"><span data-stu-id="84568-120">Execute the script</span></span>

<span data-ttu-id="84568-121">Uruchom program PowerShell i przejdź do katalogu, w którym został zapisany plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="84568-121">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="84568-122">Aby uruchomić skrypt, wykonaj następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="84568-122">To run the script, execute the following command:</span></span>

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

<span data-ttu-id="84568-123">Wykonanie skryptu może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="84568-123">The script may take a few minutes to complete.</span></span> <span data-ttu-id="84568-124">Po zakończeniu sprawdź, czy został on uruchomiony pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="84568-124">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="84568-125">Z poziomu przeglądarki zaloguj się do witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="84568-125">In a browser, sign into the Azure portal.</span></span>
2. <span data-ttu-id="84568-126">W obszarze nawigacji po lewej stronie kliknij pozycję **Grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="84568-126">In the navigation on the left, click **Resource Groups**.</span></span>
3. <span data-ttu-id="84568-127">Na liście grup zasobów kliknij pozycję **TrialsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="84568-127">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="84568-128">Na liście zasobów powinny być widoczne nowo utworzone maszyny wirtualne i skojarzone z nimi zasoby.</span><span class="sxs-lookup"><span data-stu-id="84568-128">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="84568-129">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="84568-129">Summary</span></span>
<span data-ttu-id="84568-130">Napisaliśmy skrypt, który automatyzuje proces tworzenia trzech maszyn wirtualnych w grupie zasobów wskazanej przez parametr skryptu.</span><span class="sxs-lookup"><span data-stu-id="84568-130">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="84568-131">Skrypt jest krótki i prosty, ale automatyzuje proces, którego wykonanie ręczne za pomocą witryny Portal trwałoby długo.</span><span class="sxs-lookup"><span data-stu-id="84568-131">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>