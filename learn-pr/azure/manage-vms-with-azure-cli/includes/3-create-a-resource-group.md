<span data-ttu-id="de475-101">Naszym celem jest utworzenie nowej maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="de475-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="de475-102">Konieczne jest podanie kilku informacji, aby zidentyfikować lokalizację zasobów, system operacyjny, który ma zostać użyty, i wymaganą konfigurację sprzętu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de475-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="de475-103">Zacznijmy od **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="de475-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="de475-104">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="de475-104">Create a resource group</span></span>

<span data-ttu-id="de475-105">_Grupy zasobów_ na platformie Azure służą do grupowania powiązanych zasobów, takich jak maszyny wirtualne i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="de475-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="de475-106">Grupa zasobów określa również konkretną lokalizację (zwaną regionem), która decyduje o tym, w którym centrum danych zostanie umieszczony zasób.</span><span class="sxs-lookup"><span data-stu-id="de475-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="de475-107">Ponieważ to jest eksperyment, zacznij od utworzenia nowej grupy zasobów o nazwie `ExerciseResources` i umieszczenia jej w regionie `eastus`.</span><span class="sxs-lookup"><span data-stu-id="de475-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

> [!NOTE]
> <span data-ttu-id="de475-108">Upewnij się, że używasz dokładnie tej nazwy nowej grupy zasobów, ponieważ system Microsoft Learn będzie później szukał tej nazwy grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="de475-108">Make sure to use this exact name for your new resource group, because the Microsoft Learn system will be looking for this resource name later.</span></span> 

<span data-ttu-id="de475-109">Wpisz następujące polecenie interfejsu wiersza polecenia platformy Azure w usłudze Azure Cloud Shell, aby utworzyć tę grupę zasobów w swojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="de475-109">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="de475-110">Spowoduje to zwrócenie bloku w formacie JSON wskazującego, że grupa zasobów została utworzona.</span><span class="sxs-lookup"><span data-stu-id="de475-110">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="de475-111">Powinien on wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="de475-111">It should look something like:</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="de475-112">Należy pamiętać, że odpowiedź będzie zawierała unikatowy identyfikator subskrypcji, jej lokalizację oraz nazwę.</span><span class="sxs-lookup"><span data-stu-id="de475-112">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="de475-113">Możesz użyć tych parametrów, aby zweryfikować, czy grupa została utworzona w odpowiedniej subskrypcji i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="de475-113">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="de475-114">Mamy już grupę zasobów, więc czas na utworzenie nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de475-114">Now that we have a resource group, let's create a new virtual machine.</span></span>