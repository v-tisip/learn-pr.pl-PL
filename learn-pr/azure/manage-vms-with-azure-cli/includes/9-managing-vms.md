<span data-ttu-id="614af-101">Jednym z głównych zadań wykonywanych w stosunku do działających maszyn wirtualnych jest ich uruchamianie i zatrzymywanie.</span><span class="sxs-lookup"><span data-stu-id="614af-101">One of the main tasks you'll want to do to running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="614af-102">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="614af-102">Stopping a VM</span></span>

<span data-ttu-id="614af-103">Uruchomioną maszynę wirtualną możemy zatrzymać za pomocą polecenia `vm stop`.</span><span class="sxs-lookup"><span data-stu-id="614af-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="614af-104">Musisz przekazać nazwę i grupę zasobów lub unikatowy identyfikator maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="614af-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="614af-105">Możemy sprawdzić, czy została ona zatrzymana, próbując wysłać polecenie ping do publicznego adresu IP, przy użyciu elementu `ssh` lub polecenia `vm get-instance-view`.</span><span class="sxs-lookup"><span data-stu-id="614af-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="614af-106">To końcowe podejście powoduje zwrócenie tych samych danych podstawowych jako `vm show`, ale obejmuje szczegółowe informacje o samym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="614af-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="614af-107">Spróbuj wpisać poniższe polecenie w usłudze Azure Cloud Shell, aby wyświetlić bieżący stan działania maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="614af-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

<span data-ttu-id="614af-108">To polecenie powinno zwrócić wynik `VM stopped`.</span><span class="sxs-lookup"><span data-stu-id="614af-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="614af-109">Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="614af-109">Starting a VM</span></span>

<span data-ttu-id="614af-110">Odwrotną czynność możemy wykonać za pomocą polecenia `vm start`.</span><span class="sxs-lookup"><span data-stu-id="614af-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="614af-111">To polecenie uruchomi zatrzymaną maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="614af-111">This command will start a stopped VM.</span></span> <span data-ttu-id="614af-112">Możemy to zweryfikować przy użyciu zapytania `vm get-instance-view`, które powinno teraz zwrócić wartość `VM running`.</span><span class="sxs-lookup"><span data-stu-id="614af-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="614af-113">Ponowne uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="614af-113">Restarting a VM</span></span>

<span data-ttu-id="614af-114">Na koniec możemy można ponownie uruchomić maszynę wirtualną, jeśli wprowadzono zmiany, które wymagają ponownego uruchomienia przy użyciu polecenia `vm restart`.</span><span class="sxs-lookup"><span data-stu-id="614af-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="614af-115">Możesz dodać flagę `--no-wait`, jeśli chcesz, aby interfejs wiersza polecenia platformy Azure był zwracany natychmiast bez oczekiwania na ponowne uruchomienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="614af-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

