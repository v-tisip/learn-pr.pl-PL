<span data-ttu-id="8b42d-101">Utworzyliśmy nową maszynę wirtualną systemu Linux, zmieniliśmy jej rozmiar, zatrzymaliśmy ją i uruchomiliśmy oraz zaktualizowaliśmy konfigurację przy użyciu interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8b42d-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="8b42d-102">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="8b42d-102">Cleanup</span></span>

<span data-ttu-id="8b42d-103">Teraz, gdy skończyliśmy pracę z maszyną wirtualną i już jej nie potrzebujemy, trzeba usunąć zasoby.</span><span class="sxs-lookup"><span data-stu-id="8b42d-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="8b42d-104">Czyszczenie jest ważne ze względu na zasoby obliczeniowe i magazynowe, które nadal będą rozliczane w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="8b42d-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="8b42d-105">Możesz usunąć poszczególne zasoby za pomocą polecenia `delete`, ale najłatwiejszym sposobem na usunięcie wszystkich zasobów jest użycie polecenia `az group delete`.</span><span class="sxs-lookup"><span data-stu-id="8b42d-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="8b42d-106">W interfejsie wiersza polecenia platformy Azure uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8b42d-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="8b42d-107">Odpowiedz „tak” na wyświetlony monit, lub użyj parametru `--yes`, aby odpowiedzieć na niego automatycznie.</span><span class="sxs-lookup"><span data-stu-id="8b42d-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="8b42d-108">To polecenie usuwa wszystkie zasoby skojarzone z grupą zasobów i gwarantuje cofnięcie ich przydziału w odpowiedniej kolejności.</span><span class="sxs-lookup"><span data-stu-id="8b42d-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="8b42d-109">Parametr `--no-wait` zapobiega blokowaniu interfejsu wiersza polecenia platformy Azure podczas usuwania.</span><span class="sxs-lookup"><span data-stu-id="8b42d-109">The `--no-wait` parameter keeps the Azure CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="8b42d-110">Pozostaw go wyłączonego, oczekując na usunięcie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8b42d-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="8b42d-111">Możesz też użyć polecenia `az group wait -n ExerciseResources --deleted` dalej w swoim skrypcie, aby poczekać na zakończenie usuwania.</span><span class="sxs-lookup"><span data-stu-id="8b42d-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to finish.</span></span>


## <a name="further-reading"></a><span data-ttu-id="8b42d-112">Dalsze informacje</span><span class="sxs-lookup"><span data-stu-id="8b42d-112">Further reading</span></span>

* [<span data-ttu-id="8b42d-113">Omówienie interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8b42d-113">Azure CLI overview</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [<span data-ttu-id="8b42d-114">Dokumentacja poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8b42d-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
