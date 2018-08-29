## <a name="motivation"></a>Motywacja
Załóżmy, że Twoja firma wybrała interfejs wiersza polecenia platformy Azure jako rozwiązanie wiersza polecenia do zarządzania zasobami platformy Azure. Twoi administratorzy i deweloperzy wolą uruchamiać swoje polecenia i skrypty lokalnie, a nie za pośrednictwem przeglądarki. Zespół korzysta z maszyn z systemem Linux, macOS i Windows. Musisz zapewnić działanie interfejsu wiersza polecenia platformy Azure na wszystkich urządzeniach.

## <a name="what-is-the-azure-cli"></a>Co to jest interfejs wiersza polecenia platformy Azure?
Interfejs wiersza polecenia platformy Azure to program wiersza polecenia służący do łączenia się z platformą Azure i wykonywania poleceń administracyjnych względem zasobów platformy Azure. Aby na przykład ponownie uruchomić maszynę wirtualną, możesz użyć polecenia podobnego do następującego:

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

Interfejs wiersza polecenia platformy Azure udostępnia narzędzia wiersza polecenia dla wielu platform służące do zarządzania zasobami platformy Azure i możesz go zainstalować lokalnie na komputerach z systemem Linux, Mac lub Windows. Z interfejsu wiersza polecenia platformy Azure można także korzystać w przeglądarce za pośrednictwem usługi Azure Cloud Shell. W obu przypadkach interfejsu można używać interaktywnie lub z wykorzystaniem skryptów. W celu korzystania w trybie interaktywnym najpierw uruchom powłokę, taką jak cmd.exe w systemie Windows albo Bash w systemie Linux lub macOS, a następnie wydaj polecenie w wierszu polecenia powłoki. Aby zautomatyzować powtarzalne zadania, złóż polecenia interfejsu wiersza polecenia w skrypt powłoki przy użyciu składni skryptu wybranej powłoki, a następnie wykonaj skrypt.

## <a name="how-to-install-azure-cli"></a>Jak zainstalować interfejs wiersza polecenia platformy Azure
Zarówno w systemie Linux, jak i macOS, do zainstalowania programu PowerShell Core używany jest menedżer pakietów. Zalecany menedżer pakietów różni się w zależności od systemu operacyjnego i dystrybucji:
- Linux: **apt-get** w systemie Ubuntu, **yum** w systemie Red Hat i **zypper** w systemie OpenSUSE
- Mac: **Homebrew**

Interfejs wiersza polecenia platformy Azure jest dostępny w repozytorium firmy Microsoft, więc najpierw musisz dodać to repozytorium do swojego menedżera pakietów.

W systemie Windows interfejs wiersza polecenia platformy Azure można zainstalować, pobierając i uruchamiając plik MSI.

## <a name="using-the-azure-cli-in-scripts"></a>Korzystanie z interfejsu wiersza polecenia platformy Azure w skryptach
Aby używać poleceń interfejsu wiersza polecenia platformy Azure w skryptach, musisz mieć świadomość wszelkich problemów wynikających z powłoki czyli środowiska używanego do uruchamiania skryptu. Na przykład w powłoce bash do ustawiania zmiennych jest używana następująca składnia:

 ```bash
 variable="string"
 variable=integer
 ```

Jeśli do uruchamiania skryptów interfejsu wiersza polecenia platformy Azure używasz środowiska PowerShell, dla zmiennych musisz używać następującej składni:

 ```powershell
 $variable="string"
 $variable=integer
 ```

## <a name="summary"></a>Podsumowanie
Interfejs wiersza polecenia platformy Azure musi zostać zainstalowany, zanim będzie można go używać do zarządzania zasobami platformy Azure z komputera lokalnego. Kroki instalacji w systemach Windows, Linux i macOS są inne, ale po zainstalowaniu polecenia są takie same na wszystkich platformach. 
