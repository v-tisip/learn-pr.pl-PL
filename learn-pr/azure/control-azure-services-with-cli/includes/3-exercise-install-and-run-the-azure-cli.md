
W tym ćwiczeniu zainstalujesz interfejs wiersza polecenia platformy Azure na komputerze lokalnym, a następnie uruchomisz proste polecenie, aby zweryfikować swoją instalację. 

## <a name="installing-the-azure-cli"></a>Instalowanie interfejsu wiersza polecenia platformy Azure
Metoda instalowania interfejsu wiersza polecenia platformy Azure zależy od systemu operacyjnego komputera. Wybierz procedurę dla używanego systemu operacyjnego.

### <a name="linux"></a>Linux
Interfejs wiersza polecenia platformy Azure zostanie zainstalowany w systemie Ubuntu Linux przy użyciu zaawansowanego narzędzia do tworzenia pakietów (**apt**) i wiersza polecenia powłoki Bash.

> [!NOTE]
> Lista poleceń przedstawionych poniżej dotyczy systemu Ubuntu w wersji 18.04. Jeśli używasz innej wersji systemu Ubuntu, musisz dodać inne repozytorium. Aby uzyskać szczegółowe informacje, zobacz [Instalacja interfejsu wiersza polecenia platformy Azure 2.0 przy użyciu narzędzia apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).

1. Zmodyfikuj swoją listę źródeł tak, aby repozytorium firmy Microsoft było zarejestrowane, a menedżer pakietów mógł zlokalizować pakiet interfejsu wiersza polecenia platformy Azure.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. Zaimportuj klucz szyfrowania dla repozytorium Microsoft Ubuntu. Dzięki temu menedżer pakietów może sprawdzić, czy instalowany pakiet interfejsu wiersza polecenia platformy Azure pochodzi z firmy Microsoft.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Zainstaluj interfejs wiersza polecenia platformy Azure.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a>macOS
Interfejs wiersza polecenia platformy Azure zostanie zainstalowany w systemie macOS przy użyciu menedżera pakietów Homebrew.

> [!IMPORTANT]
> Jeśli polecenie **brew** jest niedostępne, może być konieczne zainstalowanie menedżera pakietów Homebrew. Aby uzyskać szczegółowe informacje, zobacz [witrynę internetową oprogramowania Homebrew](https://brew.sh/).

1. Zaktualizuj repozytorium brew, aby upewnić się, że masz najnowszy pakiet interfejsu wiersza polecenia platformy Azure.

    ```bash
    brew update
    ```
1. Zainstaluj interfejs wiersza polecenia platformy Azure.

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a>Windows
Interfejs wiersza polecenia platformy Azure zostanie zainstalowany w systemie Windows za pomocą Instalatora MSI.

1. Przejdź na stronę [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) i w oknie dialogowym zabezpieczeń przeglądarki kliknij pozycję **Uruchom**.
1. W oknie instalatora zaakceptuj postanowienia licencyjne, a następnie kliknij pozycję **Zainstaluj**.
1. W oknie dialogowym **Kontrola konta użytkownika** wybierz opcję **Tak**.

## <a name="running-the-azure-cli"></a>Uruchamianie interfejsu wiersza polecenia platformy Azure
Aby uruchomić wiersz polecenia platformy Azure, należy otworzyć powłokę bash (Linux i macOS) lub użyć wiersza polecenia bądź programu PowerShell (Windows).

1. Uruchom interfejs wiersza polecenia platformy Azure i zweryfikuj instalację, uruchamiając sprawdzanie wersji.

    ```bash
    az --version
    ```

> [!NOTE]
> W systemie Windows uruchomienie interfejsu wiersza polecenia platformy Azure za pomocą programu PowerShell ma kilka zalet w porównaniu z uruchomieniem go z poziomu wiersza polecenia. Program PowerShell na przykład oferuje dodatkowe funkcje uzupełniania po naciśnięciu tabulatora w porównaniu z funkcjami dostępnymi z poziomu wiersza polecenia. 

## <a name="summary"></a>Podsumowanie
W tym ćwiczeniu skonfigurowaliśmy komputery lokalne pod kątem administrowania zasobami platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure. Teraz można lokalnie używać interfejsu wiersza polecenia platformy Azure do wprowadzania poleceń lub wykonywania skryptów. Interfejs wiersza polecenia platformy Azure przekaże polecenia do centrów danych platformy Azure, gdzie są wykonywane w ramach używanej subskrypcji platformy Azure.
