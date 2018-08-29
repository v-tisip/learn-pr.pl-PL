<span data-ttu-id="0cf5f-101">Po utworzeniu maszyny wirtualnej możemy otrzymywać informacje na jej temat za pośrednictwem innych poleceń.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="0cf5f-102">Zacznijmy od polecenia `vm list`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="0cf5f-103">To polecenie zwróci _wszystkie_ maszyny wirtualne zdefiniowane w ramach tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="0cf5f-104">Można filtrować dane wyjściowe według grupy zasobów za pomocą parametru `--resource-group`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="0cf5f-105">Typy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="0cf5f-105">Output types</span></span>
<span data-ttu-id="0cf5f-106">Należy zwrócić uwagę, że domyślny typ odpowiedzi dla wszystkich wykonanych do tej pory poleceń to JSON.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="0cf5f-107">Ten format doskonale nadaje się do tworzenia skryptów, ale jest trudny do odczytania dla większości osób.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="0cf5f-108">Możesz zmienić styl danych wyjściowych dla każdej odpowiedzi za pomocą flagi `--output`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="0cf5f-109">Możesz na przykład wypróbować następujące polecenie w usłudze Azure Cloud Shell, aby zobaczyć, jakie są inne style danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="0cf5f-110">Oprócz wartości `table` możesz określić wartości `json` (ustawienie domyślne), `jsonc` (pokolorowany ciąg JSON) lub `tsv` (wartości oddzielone tabulatorami).</span><span class="sxs-lookup"><span data-stu-id="0cf5f-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="0cf5f-111">Wypróbuj kilka kombinacji z powyższym poleceniem, aby sprawdzić, czym się różnią.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="0cf5f-112">Uzyskiwanie adresu IP</span><span class="sxs-lookup"><span data-stu-id="0cf5f-112">Getting the IP address</span></span>

<span data-ttu-id="0cf5f-113">Innym przydatnym poleceniem jest polecenie `vm list-ip-addresses`, które zwraca listę publicznych i prywatnych adresów IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="0cf5f-114">Jeśli adresy uległy zmianie lub nie zostały zapisane podczas tworzenia, możesz je pobrać w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="0cf5f-115">To polecenie zwraca następującą treść:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="0cf5f-116">Należy zwrócić uwagę, że korzystamy ze skróconej składni flagi `--output`: `-o`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="0cf5f-117">Większość parametrów poleceń interfejsu wiersza polecenia platformy Azure można skrócić do jednego łącznika i jednej litery.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="0cf5f-118">Na przykład parametr `--name` można skrócić do `-n`, a `--resource-group` do `-g`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="0cf5f-119">Jest to przydatne podczas wpisywania tekstu, jednak zalecamy używanie pełnej nazwy w skryptach dla większej przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="0cf5f-120">Sprawdź dokumentację, aby zapoznać się ze szczegółowymi informacjami dotyczącymi każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="0cf5f-121">Uzyskiwanie szczegółów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="0cf5f-121">Getting VM details</span></span>

<span data-ttu-id="0cf5f-122">Możemy uzyskać szczegółowe informacje na temat konkretnej maszyny wirtualnej na podstawie jej nazwy lub identyfikatora, używając polecenia `vm show`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="0cf5f-123">Spowoduje to zwrócenie dość dużego bloku w formacie JSON ze wszelkiego rodzaju informacjami dotyczącymi maszyny wirtualnej, na przykład na temat dołączonych urządzeń magazynu, interfejsów sieciowych i wszystkich identyfikatorów obiektów dla zasobów, z którymi połączona jest maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="0cf5f-124">W tym przypadku również można zmienić format na tabelę, ale w ten sposób pominiemy niemal wszystkie interesujące dane.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="0cf5f-125">Zamiast tego możemy użyć wbudowanego języka zapytań dla formatu JSON o nazwie [JMESPath](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="0cf5f-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="0cf5f-126">Dodawanie filtrów do zapytań w języku JMESPath</span><span class="sxs-lookup"><span data-stu-id="0cf5f-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="0cf5f-127">JMESPath to język zapytań zgodny ze standardami branżowymi stworzony pod kątem obiektów w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="0cf5f-128">Najprostsze zapytanie określa _identyfikator_, służący do wybrania klucza w obiekcie JSON.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="0cf5f-129">Na przykład w przypadku obiektu:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-129">For example, given the object:</span></span>

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

<span data-ttu-id="0cf5f-130">Możemy użyć zapytania `people`, aby zwrócić tablicę wartości dla tablicy `people`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="0cf5f-131">Jeśli zależy nam tylko na _jednej_ osobie, możemy skorzystać z indeksatora.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="0cf5f-132">Na przykład polecenie `people[1]` zwróci:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="0cf5f-133">Możemy również dodać konkretne kwalifikatory, które zwrócą tylko obiekty `Fred` i `Wilma`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-133">We can also add specific qualifiers that would return just the `Fred` and `Wilma` objects.</span></span> 

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

<span data-ttu-id="0cf5f-134">Możemy ograniczyć wyniki, dodając wybór: `people[?age > '25'].[name]`, co spowoduje zwrócenie tylko nazwisk:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-134">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

<span data-ttu-id="0cf5f-135">Język JMESQuery oferuje jeszcze kilka innych ciekawych funkcji zapytań.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-135">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="0cf5f-136">Jeśli masz czas, zapoznaj się z [samouczkiem online](http://jmespath.org/tutorial.html) dostępnym w witrynie [JMESPath.org](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="0cf5f-136">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="0cf5f-137">Filtrowanie zapytań interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0cf5f-137">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="0cf5f-138">Mając podstawową wiedzę na temat zapytań JMES, możemy dodać filtry do danych zwracanych przez zapytania, na przykład polecenie `vm show`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-138">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="0cf5f-139">Możemy na przykład pobrać nazwę użytkownika administratora:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-139">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="0cf5f-140">Możemy dowiedzieć się, jaki rozmiar został przypisany do naszej maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-140">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="0cf5f-141">Aby pobrać wszystkie identyfikatory interfejsów sieciowych, możesz użyć zapytania:</span><span class="sxs-lookup"><span data-stu-id="0cf5f-141">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="0cf5f-142">Ta technika zapytań działa z dowolnym poleceniem interfejsu wiersza polecenia platformy Azure i można jej użyć, aby wyciągnąć konkretne elementy danych przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-142">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="0cf5f-143">Jest to przydatne również do tworzenia skryptów — możesz na przykład wyciągnąć wartość z konta platformy Azure i zapisać ją w zmiennej środowiskowej lub zmiennej skryptu.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-143">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="0cf5f-144">Jeśli zdecydujesz na to rozwiązanie, warto dodać parametr `--output tsv`, który można skrócić do postaci `-o tsv`.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-144">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="0cf5f-145">Spowoduje to zwrócenie wyników w formie wartości rozdzielonych znakami tabulacji, które zawierają wyłącznie faktyczne wartości danych oraz rozdzielające znaki tabulacji.</span><span class="sxs-lookup"><span data-stu-id="0cf5f-145">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="0cf5f-146">Na przykład</span><span class="sxs-lookup"><span data-stu-id="0cf5f-146">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="0cf5f-147">zwróci tekst: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="0cf5f-147">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
