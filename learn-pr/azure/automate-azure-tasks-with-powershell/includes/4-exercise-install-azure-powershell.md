W tym ćwiczeniu zainstalujemy moduł **Azure PowerShell** na komputerze lokalnym. Wybierz sekcję odpowiadająca swojemu systemowi operacyjnemu.

## <a name="linux-and-mac"></a>Linux i Mac
W systemach Linux i macOS przede wszystkim należy zainstalować program **PowerShell Core**.

### <a name="linux"></a>Linux
Jak wspomniano w poprzednim module, instalacja programu PowerShell dla systemu Linux wymaga użycia menedżera pakietów. W tym przykładzie użyjemy systemu **Ubuntu 18.04**, jednak [w dokumentacji są dostępne szczegółowe instrukcje dla innych wersji i dystrybucji](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).

Program PowerShell Core zostanie zainstalowany w systemie Ubuntu Linux przy użyciu zaawansowanego narzędzia do tworzenia pakietów (**apt**) i wiersza polecenia powłoki Bash. 

1. Zaimportuj klucz szyfrowania dla repozytorium Microsoft Ubuntu. Dzięki temu menedżer pakietów może sprawdzić, czy instalowany pakiet programu PowerShell Core pochodzi z firmy Microsoft.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Zarejestruj **repozytorium Microsoft Ubuntu**, aby umożliwić menedżerowi pakietów zlokalizowanie pakietu programu PowerShell Core.

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. Zaktualizuj listę pakietów.

    ```bash
    sudo apt-get update
    ```

1. Zainstaluj program PowerShell Core.

    ```bash
    sudo apt-get install -y powershell
    ```

1. Uruchom program PowerShell, aby sprawdzić, czy instalacja przebiegła poprawnie.

    ```bash
    pwsh
    ```

### <a name="macos"></a>macOS
Następnie zainstaluj program **PowerShell Core** w systemie macOS przy użyciu menedżera pakietów Homebrew.

> [!IMPORTANT]
> Jeśli polecenie **brew** jest niedostępne, może być konieczne zainstalowanie menedżera pakietów Homebrew. Aby uzyskać szczegółowe informacje, zobacz [witrynę internetową oprogramowania Homebrew](https://brew.sh/).

1. Zainstaluj aplikację Homebrew Cask, aby uzyskać więcej pakietów, w tym pakiet programu PowerShell Core:

    ```bash
    brew tap caskroom/cask
    ```
1. Zainstaluj program PowerShell Core:

    ```bash
    brew cask install powershell
    ```

1. Uruchom program PowerShell Core, aby sprawdzić, czy instalacja przebiegła poprawnie:

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a>Instalowanie programu Azure PowerShell
Po zainstalowaniu podstawowego produktu **PowerShell** zainstaluj moduł **Azure PowerShell** umożliwiający dodanie poleceń specyficznych dla platformy Azure.

### <a name="windows"></a>Windows
Zainstaluj moduł Azure PowerShell w systemie Windows za pomocą polecenia programu PowerShell `Install-Module`.

> [!IMPORTANT]
> Do zainstalowania modułu Azure PowerShell jest wymagany program PowerShell w wersji 5.0 lub nowszej. Aby sprawdzić wersję programu PowerShell, użyj następującego polecenia: 
>
> `$PSVersionTable.PSVersion` 
>
>Jeśli numer wersji jest mniejszy niż 5.0, [uaktualnij program Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell) zgodnie z instrukcjami.

1. Otwórz menu **Start** i wpisz **Windows PowerShell**.
2. Kliknij prawym przyciskiem myszy ikonę programu **Windows PowerShell** i wybierz polecenie **Uruchom jako administrator**.
3. W oknie dialogowym **Kontrola konta użytkownika** wybierz opcję **Tak**.
4. Wprowadź następujące polecenie i naciśnij klawisz Enter:

    ```powershell
    Install-Module -Name AzureRM
    ```
5. Jeśli zostanie wyświetlony monit dotyczący wiarygodności modułów z galerii programu PowerShell, wybierz opcję **Tak** lub **Tak na wszystkie**.

> [!NOTE]
> Jeśli pojawi się komunikat o błędzie z informacją o tym, że już zainstalowano wersję modułu Azure Powershell, możesz wykonać aktualizację do _najnowszej_ wersji za pomocą polecenia:
> 
> `Update-Module -Name AzureRM`
> 
> Podobnie jak w przypadku polecenia `Install-Module`, odpowiedz **Tak** lub **Tak na wszystkie** po wyświetleniu monitu dotyczącego wiarygodności modułu.

### <a name="linux-or-macos"></a>Linux lub macOS
Używamy podobnego podstawowego procesu, aby zainstalować moduł Azure PowerShell w systemach Linux i macOS. Procedura jest taka sama w obu systemach operacyjnych. Różnica dotyczy uruchomienia sesji programu PowerShell Core z podwyższonym poziomem uprawnień.

1. W terminalu wpisz następujące polecenie, aby uruchomić program PowerShell Core z podwyższonym poziomem uprawnień.

    ```bash
    sudo pwsh
    ```

1. Aby zainstalować moduł Azure PowerShell, uruchom następujące polecenie w wierszu polecenia programu PowerShell Core.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Jeśli zostanie wyświetlony monit dotyczący wiarygodności modułów z **galerii programu PowerShell**, wybierz opcję **Tak** lub **Tak na wszystkie**.

## <a name="summary"></a>Podsumowanie
W tym ćwiczeniu skonfigurowaliśmy komputery lokalne pod kątem administrowania zasobami platformy Azure przy użyciu modułu Azure PowerShell. Można teraz lokalnie używać modułu Azure PowerShell do wprowadzania poleceń lub wykonywanie skryptów. Moduł Azure PowerShell przekazuje polecenia do centrów danych platformy Azure, gdzie są wykonywane w ramach używanej subskrypcji platformy Azure.