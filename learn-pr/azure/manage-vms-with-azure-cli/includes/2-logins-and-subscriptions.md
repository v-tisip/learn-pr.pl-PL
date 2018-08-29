Zanim zaczniemy, omówmy składnię narzędzia interfejsu wiersza polecenia platformy Azure. Z modułu **Sterowanie usługami platformy Azure za pomocą interfejsu wiersza polecenia platformy Azure** można dowiedzieć się, że polecenia interfejsu wiersza polecenia platformy Azure mają następującą postać:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

Opcja `[command]` identyfikuje określony obszar platformy Azure, który chcesz kontrolować. Na przykład możesz zarządzać informacjami o subskrypcji za pomocą polecenia `account` lub bazami danych SQL za pomocą polecenia `sql`. Opcje `[subcommand]` i `[--parameters]` zależą wówczas od polecenia, z którym pracujesz. 

Wpisując część polecenia, możesz wyświetlić listę poleceń, poleceń podrzędnych i parametrów. Na przykład wpisanie polecenia `az` w wierszu polecenia spowoduje wyświetlenie ekranu pomocy najwyższego poziomu, a wpisanie polecenia `az vm` spowoduje wyświetlenie listy wszystkich poleceń podrzędnych dotyczących maszyn wirtualnych. Takie podejście może być doskonałym sposobem eksplorowania narzędzia interfejsu wiersza polecenia platformy Azure.

> [!NOTE]
> Do pracy z interfejsem wiersza polecenia platformy Azure będziemy używać usługi Azure Cloud Shell hostowanej w przeglądarce. Jeśli wolisz pracować na komputerze lokalnym, wszystkie przedstawione polecenia możesz również wykonać z poziomu wiersza polecenia po [zainstalowaniu interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Pierwszą czynnością, jaką musisz wykonać podczas pracy z interfejsem wiersza polecenia platformy Azure, jest zalogowanie się do konta platformy Azure. Robi się to za pomocą polecenia `login`. Jeśli używasz usługi Cloud Shell, zawiera ona przycisk umożliwiający zalogowanie się do platformy Azure.

```azurecli
az login
```

To polecenie spowoduje uruchomienie okna przeglądarki i umożliwi wybranie konta Microsoft, które ma być używane.

## <a name="working-with-subscriptions"></a>Praca z subskrypcjami

W tym module będziemy pracować w ramach tymczasowej subskrypcji utworzonej jako plac zabaw, ale zwykle będziesz używać subskrypcji z własnego konta. Jeśli masz więcej niż jedną subskrypcję, wpisując instrukcję `az account list --output table`, możesz uzyskać czytelnie sformatowaną listę subskrypcji.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Zwróć uwagę, że polecenie identyfikuje również subskrypcję _domyślną_, w której zostaną zastosowane wszystkie Twoje polecenia. Jeśli wolisz pracować w innej subskrypcji, możesz użyć polecenia `az account set --subscription "[name]"`. Na przykład moglibyśmy ustawić naszą bieżącą subskrypcję na `Visual Studio Enterprise` z powyższej listy, używając następującego polecenia:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```