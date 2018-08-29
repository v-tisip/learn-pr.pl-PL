Interfejs wiersza polecenia platformy Azure udostępnia polecenie `vm` umożliwiające pracę z maszynami wirtualnymi na platformie Azure. Dostępnych jest kilka podpoleceń, które służą do wykonywania określonych zadań. Oto najczęściej używane podpolecenia:

| Podpolecenie | Opis |
|-------------|-------------|
| `create`    | Tworzy nową maszynę wirtualną |
| `deallocate` | Cofa przydział maszyny wirtualnej |
| `delete` | Usuwa maszynę wirtualną |
| `list` | Wyświetla listę utworzonych maszyn wirtualnych w subskrypcji |
| `open-port` | Otwiera określony port sieciowy dla ruchu przychodzącego |
| `restart` | Uruchamia ponownie maszynę wirtualną |
| `show` | Pobiera szczegółowe informacje o maszynie wirtualnej |
| `start` | Uruchamia zatrzymaną maszynę wirtualną |
| `stop` | Zatrzymuje uruchomioną maszynę wirtualną |
| `update` | Aktualizuje właściwość maszyny wirtualnej |

> [!NOTE]
> Pełną listę poleceń można znaleźć w [dokumentacji wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).

Pierwsze polecenie to: `az vm create`. Służy ono do tworzenia maszyny wirtualnej w grupie zasobów. Dostępnych jest kilka parametrów, które pozwalają skonfigurować wszystkie aspekty nowej maszyny wirtualnej. Oto trzy obowiązkowe parametry:

| Parametr | Opis |
|-----------|-------------|
| `resource-group` | Grupa zasobów, do której będzie należeć maszyna wirtualna |
| `name` | Nazwa maszyny wirtualnej — musi być unikatowa w grupie zasobów |
| `image` | Obraz systemu operacyjnego używany do utworzenia maszyny wirtualnej |

Ponadto warto dodać flagę `--verbose` umożliwiającą wyświetlanie postępu tworzenia maszyny wirtualnej. 

## <a name="create-a-linux-virtual-machine"></a>Tworzenie maszyny wirtualnej z systemem Linux

Utworzymy nową maszynę wirtualną z systemem Linux. W usłudze Azure Cloud Shell uruchom następujące polecenie:

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

Spowoduje to utworzenie nowej maszyny wirtualnej o nazwie `SampleVM` z systemem Linux **Debian**. Zwróć uwagę, że podczas tworzenia maszyny wirtualnej narzędzie interfejsu wiersza polecenia platformy Azure jest zablokowane. Jeśli nie chcesz czekać, możesz użyć opcji `--no-wait`. Nakazuje ona natychmiastowe zwrócenie narzędzia interfejsu wiersza polecenia platformy Azure, na przykład w przypadku wykonywania polecenia w skrypcie. W dalszej części skryptu jest używane polecenie `azure vm wait --name [vm-name]`. Jego użycie wiąże się z czekaniem na zakończenie tworzenia maszyny wirtualnej.

Jeśli przyjrzymy się pełnym odpowiedziom, to zobaczymy, że nazwa `SampleVM` odnosi się do różnych zależności maszyny wirtualnej.

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

Te wygenerowane automatycznie nazwy zasobów można zastąpić za pomocą opcjonalnych parametrów polecenia `vm create`, takich jak `--vnet-name` i `--public-ip-address-dns-name`.

Zwróć uwagę, że za pomocą flagi `admin-username` jest podawana nazwa konta administratora — „aldis”. W przypadku jej pominięcia podczas wykonywania polecenia `vm create` zostanie użyta _bieżąca nazwa użytkownika_. Ponieważ zasady nazewnictwa kont są inne w poszczególnych systemach operacyjnych, bezpieczniej jest podać konkretną nazwę. W przypadku większości obrazów często używane nazwy, takie jak „root” i „admin”, są niedozwolone.

Ponadto jest używana flaga `generate-ssh-keys`. Ten parametr, używany w dystrybucjach systemu Linux, tworzy parę kluczy zabezpieczeń, które pozwalają zdalnie uzyskiwać dostęp do maszyny wirtualnej za pomocą narzędzia `ssh`. Oba pliki znajdują się w folderze `.ssh` na komputerze i na maszynie wirtualnej. Jeśli w folderze docelowym już znajduje się klucz SSH o nazwie `id_rsa`, to zostanie on użyty. Nowy klucz nie zostanie wygenerowany.

Po zakończeniu tworzenia maszyny wirtualnej pojawi się odpowiedź w formacie JSON, zawierająca bieżący stan maszyny wirtualnej oraz adresy IP — publiczny i prywatny — przypisane przez platformę Azure:

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

