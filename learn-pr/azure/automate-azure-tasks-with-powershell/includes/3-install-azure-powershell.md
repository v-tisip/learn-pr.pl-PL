Załóżmy, że jako rozwiązanie do automatyzacji wybrano program Azure PowerShell. Administratorzy preferują uruchamianie skryptów w środowisku lokalnym, a nie w usłudze Azure Cloud Shell. Zespół korzysta z maszyn z systemem Linux, macOS i Windows. Musisz zapewnić działanie programu Azure PowerShell na wszystkich urządzeniach. 

## <a name="what-must-be-installed"></a>Co należy zainstalować?
Faktyczne instrukcje instalacji wykonamy w następnej sekcji, ale przyjrzyjmy się dwóm składnikom tworzącym program Azure PowerShell.

- **Podstawowy produkt PowerShell** — ma dwa warianty: program PowerShell w systemie Windows oraz program PowerShell Core w systemie macOS i Linux.
- **Moduł Azure PowerShell** — ten dodatkowy moduł należy zainstalować, aby dodać do programu PowerShell polecenia specyficzne dla platformy Azure.

> [!NOTE]
> Program PowerShell jest dołączany do systemu Windows (ale może być dostępna jego aktualizacja). W systemie Linux i macOS należy zainstalować program PowerShell Core.

Po zainstalowaniu produktu podstawowego dodaj moduł Azure PowerShell do instalacji.

## <a name="how-to-install-powershell-core"></a>Jak zainstalować program PowerShell Core
Zarówno w systemie Linux, jak i macOS, do zainstalowania programu PowerShell Core używany jest menedżer pakietów. Zalecany menedżer pakietów różni się w zależności od systemu operacyjnego i dystrybucji.

> [!NOTE]
> Program PowerShell Core jest dostępny w repozytorium firmy Microsoft, więc najpierw musisz dodać to repozytorium do swojego menedżera pakietów.

### <a name="linux"></a>Linux
W systemie Linux menedżer pakietów jest inny w zależności od wybranej dystrybucji systemu.

| Dystrybucja  | Menedżer pakietów |
|------------------|-----------------|
| Ubuntu, Debian   | `apt-get`       |
| Red Hat, CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
W systemie macOS program PowerShell Core możesz zainstalować za pomocą menedżera pakietów `Homebrew`.

## <a name="how-to-install-azure-powershell"></a>Jak zainstalować moduł Azure PowerShell
Gdy program PowerShell jest zainstalowany, preferowaną metodą instalacji modułu Azure PowerShell jest użycie polecenia `Install-Module` w programie PowerShell. Aby instalować moduły, wymagany jest podwyższony poziom uprawnień.

- W systemie Windows musisz uruchomić program PowerShell jako administrator
- W systemie Linux i macOS poziom uprawnień możesz podnieść za pomocą polecenia `sudo`

## <a name="summary"></a>Podsumowanie
Program PowerShell jest wbudowany w system Windows, ale musisz zainstalować moduł Azure PowerShell. W systemie Linux i macOS musisz zainstalować program PowerShell Core i moduł Azure PowerShell. W następnej sekcji zostaną podane szczegółowe kroki instalacji na niektórych popularnych platformach.