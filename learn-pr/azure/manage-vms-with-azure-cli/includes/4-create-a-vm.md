<span data-ttu-id="e8845-101">Interfejs wiersza polecenia platformy Azure udostępnia polecenie `vm` umożliwiające pracę z maszynami wirtualnymi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e8845-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="e8845-102">Dostępnych jest kilka podpoleceń, które służą do wykonywania określonych zadań.</span><span class="sxs-lookup"><span data-stu-id="e8845-102">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="e8845-103">Oto najczęściej używane podpolecenia:</span><span class="sxs-lookup"><span data-stu-id="e8845-103">The most common include:</span></span>

| <span data-ttu-id="e8845-104">Podpolecenie</span><span class="sxs-lookup"><span data-stu-id="e8845-104">Sub-command</span></span> | <span data-ttu-id="e8845-105">Opis</span><span class="sxs-lookup"><span data-stu-id="e8845-105">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="e8845-106">Tworzy nową maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="e8845-106">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="e8845-107">Cofa przydział maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8845-107">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="e8845-108">Usuwa maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="e8845-108">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="e8845-109">Wyświetla listę utworzonych maszyn wirtualnych w subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e8845-109">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="e8845-110">Otwiera określony port sieciowy dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e8845-110">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="e8845-111">Uruchamia ponownie maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="e8845-111">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="e8845-112">Pobiera szczegółowe informacje o maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8845-112">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="e8845-113">Uruchamia zatrzymaną maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="e8845-113">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="e8845-114">Zatrzymuje uruchomioną maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="e8845-114">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="e8845-115">Aktualizuje właściwość maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8845-115">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="e8845-116">Pełną listę poleceń można znaleźć w [dokumentacji wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="e8845-116">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="e8845-117">Pierwsze polecenie to: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="e8845-117">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="e8845-118">Służy ono do tworzenia maszyny wirtualnej w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e8845-118">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="e8845-119">Dostępnych jest kilka parametrów, które pozwalają skonfigurować wszystkie aspekty nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8845-119">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="e8845-120">Oto trzy obowiązkowe parametry:</span><span class="sxs-lookup"><span data-stu-id="e8845-120">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="e8845-121">Parametr</span><span class="sxs-lookup"><span data-stu-id="e8845-121">Parameter</span></span> | <span data-ttu-id="e8845-122">Opis</span><span class="sxs-lookup"><span data-stu-id="e8845-122">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="e8845-123">Grupa zasobów, do której będzie należeć maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="e8845-123">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="e8845-124">Nazwa maszyny wirtualnej — musi być unikatowa w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="e8845-124">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="e8845-125">Obraz systemu operacyjnego używany do utworzenia maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8845-125">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="e8845-126">Ponadto warto dodać flagę `--verbose` umożliwiającą wyświetlanie postępu tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8845-126">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="e8845-127">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="e8845-127">Create a Linux virtual machine</span></span>

<span data-ttu-id="e8845-128">Utworzymy nową maszynę wirtualną z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="e8845-128">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="e8845-129">W usłudze Azure Cloud Shell uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e8845-129">Execute the following command in Azure Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="e8845-130">Spowoduje to utworzenie nowej maszyny wirtualnej o nazwie `SampleVM` z systemem Linux **Debian**.</span><span class="sxs-lookup"><span data-stu-id="e8845-130">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="e8845-131">Zwróć uwagę, że podczas tworzenia maszyny wirtualnej narzędzie interfejsu wiersza polecenia platformy Azure jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="e8845-131">Notice that the Azure CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="e8845-132">Jeśli nie chcesz czekać, możesz użyć opcji `--no-wait`. Nakazuje ona natychmiastowe zwrócenie narzędzia interfejsu wiersza polecenia platformy Azure, na przykład w przypadku wykonywania polecenia w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="e8845-132">If you would prefer not to wait, you can use the `--no-wait` option to tell the Azure CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="e8845-133">W dalszej części skryptu jest używane polecenie `azure vm wait --name [vm-name]`. Jego użycie wiąże się z czekaniem na zakończenie tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8845-133">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="e8845-134">Jeśli przyjrzymy się pełnym odpowiedziom, to zobaczymy, że nazwa `SampleVM` odnosi się do różnych zależności maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8845-134">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="e8845-135">Te wygenerowane automatycznie nazwy zasobów można zastąpić za pomocą opcjonalnych parametrów polecenia `vm create`, takich jak `--vnet-name` i `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="e8845-135">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="e8845-136">Zwróć uwagę, że za pomocą flagi `admin-username` jest podawana nazwa konta administratora — „aldis”.</span><span class="sxs-lookup"><span data-stu-id="e8845-136">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="e8845-137">W przypadku jej pominięcia podczas wykonywania polecenia `vm create` zostanie użyta _bieżąca nazwa użytkownika_.</span><span class="sxs-lookup"><span data-stu-id="e8845-137">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="e8845-138">Ponieważ zasady nazewnictwa kont są inne w poszczególnych systemach operacyjnych, bezpieczniej jest podać konkretną nazwę.</span><span class="sxs-lookup"><span data-stu-id="e8845-138">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="e8845-139">W przypadku większości obrazów często używane nazwy, takie jak „root” i „admin”, są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="e8845-139">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="e8845-140">Ponadto jest używana flaga `generate-ssh-keys`.</span><span class="sxs-lookup"><span data-stu-id="e8845-140">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="e8845-141">Ten parametr, używany w dystrybucjach systemu Linux, tworzy parę kluczy zabezpieczeń, które pozwalają zdalnie uzyskiwać dostęp do maszyny wirtualnej za pomocą narzędzia `ssh`.</span><span class="sxs-lookup"><span data-stu-id="e8845-141">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="e8845-142">Oba pliki znajdują się w folderze `.ssh` na komputerze i na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8845-142">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="e8845-143">Jeśli w folderze docelowym już znajduje się klucz SSH o nazwie `id_rsa`, to zostanie on użyty. Nowy klucz nie zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e8845-143">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="e8845-144">Po zakończeniu tworzenia maszyny wirtualnej pojawi się odpowiedź w formacie JSON, zawierająca bieżący stan maszyny wirtualnej oraz adresy IP — publiczny i prywatny — przypisane przez platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="e8845-144">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

