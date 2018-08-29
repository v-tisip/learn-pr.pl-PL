Załóżmy, że pracujesz w firmie, która tworzy pakiet narzędzi administracyjnych dla systemu Linux. Twoje zadanie polega na ułatwieniu potencjalnym klientom wypróbowanie Twojego oprogramowania przed zakupem. Ponieważ oprogramowanie wprowadza zmiany systemu operacyjnego na poziomie administratora, podjęto decyzję o utworzeniu maszyny wirtualnej z systemem Linux dla każdego klienta wersji próbnej. Tworzysz maszyny wirtualne w miarę potrzeb i usuwasz je na koniec okresu subskrypcji wersji próbnej. Dzięki temu każdy klient rozpoczyna od czystej wersji systemu operacyjnego. 

Aby zachować separację tych maszyn wirtualnych od maszyn wirtualnych używanych przez firmę do testów wewnętrznych, utworzysz dedykowaną grupę zasobów na potrzeby ich przechowywania. Wystarczy tylko jedna grupa zasobów, dlatego użycie programu Azure PowerShell w trybie interaktywnym to rozsądny wybór dla tego zadania.

## <a name="steps-to-create-a-resource-group"></a>Kroki tworzenia grupy zasobów

1. Uruchom program PowerShell.

1. Zaimportuj moduł do bieżącej sesji, aby uzyskać dostęp do poleceń cmdlet platformy Azure.

   ```powershell
   Import-Module AzureRM
   ```

1. Połącz się z platformą Azure za pomocą polecenia pokazanego poniżej. Po podaniu polecenia uwierzytelnij się, podając poświadczenia platformy Azure.

   ```powershell
   Connect-AzureRmAccount
   ```

1. Utwórz grupę zasobów.

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. Zweryfikuj, czy grupa zasobów została utworzona pomyślnie.

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
Inny sposób sprawdzenia, czy grupa zasobów została utworzona pomyślnie, to użycie witryny Azure Portal. Aby to zrobić, zaloguj się do witryny Portal i przejdź do sekcji **Grupy zasobów** (zobacz poniżej). Nowa grupa zasobów powinna zostać wyświetlona na liście.

![Używanie witryny Azure Portal do wyświetlania listy grup zasobów](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a>Podsumowanie
To ćwiczenie przedstawia typowy wzorzec interaktywnej sesji programu PowerShell. Użyto standardowego polecenia cmdlet do zaimportowania modułu AzureRM, a następnie poleceń cmdlet programu Azure PowerShell do wykonania określonego zadania. Teraz dysponujesz grupą zasobów w ramach subskrypcji i wszystko jest gotowe do tworzenia maszyn wirtualnych.