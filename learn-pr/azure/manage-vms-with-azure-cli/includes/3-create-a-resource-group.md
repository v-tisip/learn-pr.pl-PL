Naszym celem jest utworzenie nowej maszyny wirtualnej na platformie Azure. Konieczne jest podanie kilku informacji, aby zidentyfikować lokalizację zasobów, system operacyjny, który ma zostać użyty, i wymaganą konfigurację sprzętu maszyny wirtualnej. Zacznijmy od **grupy zasobów**.

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

_Grupy zasobów_ na platformie Azure służą do grupowania powiązanych zasobów, takich jak maszyny wirtualne i bazy danych. Grupa zasobów określa również konkretną lokalizację (zwaną regionem), która decyduje o tym, w którym centrum danych zostanie umieszczony zasób.

Ponieważ to jest eksperyment, zacznij od utworzenia nowej grupy zasobów o nazwie `ExerciseResources` i umieszczenia jej w regionie `eastus`.

> [!NOTE]
> Upewnij się, że używasz dokładnie tej nazwy nowej grupy zasobów, ponieważ system Microsoft Learn będzie później szukał tej nazwy grupy zasobów. 

Wpisz następujące polecenie interfejsu wiersza polecenia platformy Azure w usłudze Azure Cloud Shell, aby utworzyć tę grupę zasobów w swojej subskrypcji.

```azurecli
az group create --name ExerciseResources --location eastus
```

Spowoduje to zwrócenie bloku w formacie JSON wskazującego, że grupa zasobów została utworzona. Powinien on wyglądać mniej więcej tak:

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

Należy pamiętać, że odpowiedź będzie zawierała unikatowy identyfikator subskrypcji, jej lokalizację oraz nazwę. Możesz użyć tych parametrów, aby zweryfikować, czy grupa została utworzona w odpowiedniej subskrypcji i lokalizacji.

Mamy już grupę zasobów, więc czas na utworzenie nowej maszyny wirtualnej.