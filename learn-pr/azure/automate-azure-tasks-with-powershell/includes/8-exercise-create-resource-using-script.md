W tym ćwiczeniu będziesz kontynuować pracę z przykładem firmy, która tworzy narzędzia administracyjne systemu Linux. Przypomnij sobie, że planujesz używać maszyn wirtualnych z systemem Linux, aby umożliwić potencjalnym klientom testowanie swojego oprogramowania. Masz już gotową grupę zasobów i teraz nadszedł czas na utworzenie maszyn wirtualnych.

Twoja firma ma opłacone stoisko na dużych targach dotyczących systemu Linux. Planujesz obszar pokazu zawierający trzy terminale, z których każdy będzie połączony z osobną maszyną wirtualną systemu Linux. Na koniec każdego dnia chcesz usunąć maszyny wirtualne i utworzyć je ponownie, aby następnego dnia rano były gotowe do użytku. Ręczne tworzenie maszyn wirtualnych po pracy, w stanie zmęczenia, może prowadzić do popełnienia błędów. W celu zautomatyzowania procesu tworzenia maszyn wirtualnych warto utworzyć skrypt programu PowerShell.

## <a name="write-a-script-that-creates-virtual-machines"></a>Pisanie skryptu tworzącego maszyny wirtualne

Wykonaj następujące kroki, aby napisać skrypt:

1. Utwórz nowy plik tekstowy o nazwie **ConferenceDailyReset.ps1**.

2. Przechwyć parametr w zmiennej:

    ```powershell
    param([string]$resourceGroup)
    ```

3. Uwierzytelnij się na platformie Azure przy użyciu swoich poświadczeń:

    ```powershell
    Connect-AzureRmAccount
    ```

4. Wyświetl monit o podanie nazwy użytkownika i hasła dla konta administratora maszyny wirtualnej i przechwyć wynik w zmiennej:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. Utwórz pętlę wykonywaną trzy razy:

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. W treści pętli utwórz nazwę dla każdej maszyny wirtualnej i zapisz je w zmiennej:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. Następnie utwórz maszynę wirtualną przy użyciu zmiennej `$vmName`:

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. Zapisz plik.

Ukończony skrypt powinien wyglądać następująco:

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>Uruchamianie skryptu

Uruchom program PowerShell i przejdź do katalogu, w którym został zapisany plik skryptu. Aby uruchomić skrypt, wykonaj następujące polecenie:

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

Wykonanie skryptu może potrwać kilka minut. Po zakończeniu sprawdź, czy został on uruchomiony pomyślnie:

1. Z poziomu przeglądarki zaloguj się do witryny Azure Portal.
2. W obszarze nawigacji po lewej stronie kliknij pozycję **Grupy zasobów**.
3. Na liście grup zasobów kliknij pozycję **TrialsResourceGroup**. Na liście zasobów powinny być widoczne nowo utworzone maszyny wirtualne i skojarzone z nimi zasoby.

## <a name="summary"></a>Podsumowanie
Napisaliśmy skrypt, który automatyzuje proces tworzenia trzech maszyn wirtualnych w grupie zasobów wskazanej przez parametr skryptu. Skrypt jest krótki i prosty, ale automatyzuje proces, którego wykonanie ręczne za pomocą witryny Portal trwałoby długo.