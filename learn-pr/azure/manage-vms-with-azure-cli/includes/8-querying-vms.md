Po utworzeniu maszyny wirtualnej możemy otrzymywać informacje na jej temat za pośrednictwem innych poleceń.

Zacznijmy od polecenia `vm list`.

```azurecli
az vm list
```

To polecenie zwróci _wszystkie_ maszyny wirtualne zdefiniowane w ramach tej subskrypcji. Można filtrować dane wyjściowe według grupy zasobów za pomocą parametru `--resource-group`. 

## <a name="output-types"></a>Typy danych wyjściowych
Należy zwrócić uwagę, że domyślny typ odpowiedzi dla wszystkich wykonanych do tej pory poleceń to JSON. Ten format doskonale nadaje się do tworzenia skryptów, ale jest trudny do odczytania dla większości osób. Możesz zmienić styl danych wyjściowych dla każdej odpowiedzi za pomocą flagi `--output`. Możesz na przykład wypróbować następujące polecenie w usłudze Azure Cloud Shell, aby zobaczyć, jakie są inne style danych wyjściowych.

```azurecli
az vm list --output table
```

Oprócz wartości `table` możesz określić wartości `json` (ustawienie domyślne), `jsonc` (pokolorowany ciąg JSON) lub `tsv` (wartości oddzielone tabulatorami). Wypróbuj kilka kombinacji z powyższym poleceniem, aby sprawdzić, czym się różnią.

## <a name="getting-the-ip-address"></a>Uzyskiwanie adresu IP

Innym przydatnym poleceniem jest polecenie `vm list-ip-addresses`, które zwraca listę publicznych i prywatnych adresów IP maszyny wirtualnej. Jeśli adresy uległy zmianie lub nie zostały zapisane podczas tworzenia, możesz je pobrać w dowolnym momencie.

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

To polecenie zwraca następującą treść:

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> Należy zwrócić uwagę, że korzystamy ze skróconej składni flagi `--output`: `-o`. Większość parametrów poleceń interfejsu wiersza polecenia platformy Azure można skrócić do jednego łącznika i jednej litery. Na przykład parametr `--name` można skrócić do `-n`, a `--resource-group` do `-g`. Jest to przydatne podczas wpisywania tekstu, jednak zalecamy używanie pełnej nazwy w skryptach dla większej przejrzystości. Sprawdź dokumentację, aby zapoznać się ze szczegółowymi informacjami dotyczącymi każdego polecenia.

## <a name="getting-vm-details"></a>Uzyskiwanie szczegółów maszyn wirtualnych

Możemy uzyskać szczegółowe informacje na temat konkretnej maszyny wirtualnej na podstawie jej nazwy lub identyfikatora, używając polecenia `vm show`.

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

Spowoduje to zwrócenie dość dużego bloku w formacie JSON ze wszelkiego rodzaju informacjami dotyczącymi maszyny wirtualnej, na przykład na temat dołączonych urządzeń magazynu, interfejsów sieciowych i wszystkich identyfikatorów obiektów dla zasobów, z którymi połączona jest maszyna wirtualna. W tym przypadku również można zmienić format na tabelę, ale w ten sposób pominiemy niemal wszystkie interesujące dane. Zamiast tego możemy użyć wbudowanego języka zapytań dla formatu JSON o nazwie [JMESPath](http://jmespath.org/).

## <a name="adding-filters-to-queries-with-jmespath"></a>Dodawanie filtrów do zapytań w języku JMESPath

JMESPath to język zapytań zgodny ze standardami branżowymi stworzony pod kątem obiektów w formacie JSON. Najprostsze zapytanie określa _identyfikator_, służący do wybrania klucza w obiekcie JSON.

Na przykład w przypadku obiektu:

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

Możemy użyć zapytania `people`, aby zwrócić tablicę wartości dla tablicy `people`. Jeśli zależy nam tylko na _jednej_ osobie, możemy skorzystać z indeksatora. Na przykład polecenie `people[1]` zwróci:

```json
{
    "name": "Barney",
    "age": 25
}
```

Możemy również dodać konkretne kwalifikatory, które zwrócą tylko obiekty `Fred` i `Wilma`. 

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

Możemy ograniczyć wyniki, dodając wybór: `people[?age > '25'].[name]`, co spowoduje zwrócenie tylko nazwisk:

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

Język JMESQuery oferuje jeszcze kilka innych ciekawych funkcji zapytań. Jeśli masz czas, zapoznaj się z [samouczkiem online](http://jmespath.org/tutorial.html) dostępnym w witrynie [JMESPath.org](http://jmespath.org/).

## <a name="filtering-our-azure-cli-queries"></a>Filtrowanie zapytań interfejsu wiersza polecenia platformy Azure

Mając podstawową wiedzę na temat zapytań JMES, możemy dodać filtry do danych zwracanych przez zapytania, na przykład polecenie `vm show`. Możemy na przykład pobrać nazwę użytkownika administratora:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

Możemy dowiedzieć się, jaki rozmiar został przypisany do naszej maszyny wirtualnej:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

Aby pobrać wszystkie identyfikatory interfejsów sieciowych, możesz użyć zapytania:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

Ta technika zapytań działa z dowolnym poleceniem interfejsu wiersza polecenia platformy Azure i można jej użyć, aby wyciągnąć konkretne elementy danych przy użyciu wiersza polecenia. Jest to przydatne również do tworzenia skryptów — możesz na przykład wyciągnąć wartość z konta platformy Azure i zapisać ją w zmiennej środowiskowej lub zmiennej skryptu. Jeśli zdecydujesz na to rozwiązanie, warto dodać parametr `--output tsv`, który można skrócić do postaci `-o tsv`. Spowoduje to zwrócenie wyników w formie wartości rozdzielonych znakami tabulacji, które zawierają wyłącznie faktyczne wartości danych oraz rozdzielające znaki tabulacji.

Na przykład

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

zwróci tekst: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`
