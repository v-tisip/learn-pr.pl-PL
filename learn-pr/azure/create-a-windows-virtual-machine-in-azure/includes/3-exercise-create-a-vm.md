W tym ćwiczeniu utworzysz maszynę wirtualną z systemem Windows na platformie Azure.

## <a name="motivation"></a>Motywacja

Rozważmy alternatywny scenariusz dla tego ćwiczenia. Twoja organizacja jest uczelnią, która wykorzystuje maszyny wirtualne z systemem Windows do usprawnienia środowisk testowych, w których studenci instalują aplikacje internetowe, konfigurują domeny i eksplorują usługi oraz funkcje systemu Windows bez wywierania wpływu na komputery uczelniane. Nauczyciele łączą się z tymi maszynami wirtualnymi przy użyciu protokołu RDP, aby sprawdzić postępy studentów.

## <a name="create-a-windows-vm"></a>Tworzenie maszyny wirtualnej z systemem Windows

Aby utworzyć maszynę wirtualną z systemem Windows, wykonaj następujące czynności:

1. Zaloguj się do platformy Azure za pośrednictwem witryny [Azure Portal](https://portal.azure.com).

1. W lewym górnym rogu witryny Azure Portal kliknij pozycję **Utwórz zasób**.

1. Na **pasku wyszukiwania** wprowadź **Windows Server 2016 Datacenter** i kliknij link o takim samym tytule.

### <a name="configure-the-vm-settings"></a>Konfigurowanie ustawień maszyny wirtualnej

1. W obszarze **Informacje podstawowe** w polu **Nazwa** wprowadź nazwę maszyny wirtualnej, na przykład „StudentVM”.

1. W polu **Typ dysku maszyny wirtualnej** kliknij menu rozwijane, aby wyświetlić opcje. Upewnij się, że wybrano pozycję **SSD**.

1. W polu **Nazwa użytkownika** wprowadź odpowiednią nazwę użytkownika używaną na potrzeby logowania się do maszyny wirtualnej.

1. W polu **Hasło** wprowadź hasło składające się z co najmniej 12 znaków. Hasło musi zawierać małe i wielkie litery, cyfry i znaki specjalne.

1. W obszarze **Grupa zasobów** kliknij pozycję **Utwórz nową**. Nazwij grupę zasobów, na przykład „myTestRG”.

1. Wybierz odpowiednią lokalizację dla tworzonej maszyny wirtualnej i kliknij przycisk **OK**.

### <a name="select-the-vm-image-size-and-options"></a>Wybieranie rozmiaru obrazu maszyny wirtualnej i opcji

1. Na stronie **Wybierz rozmiar** kliknij obraz **B1s**, a następnie kliknij pozycję **Wybierz**.

   > [!Note] 
   > Obraz B1 ma tylko 1 GB pamięci RAM i dlatego podczas pierwszego logowania będą występować błędy pamięci. Można jednak zmienić rozmiar tego obrazu później w ramach następnych ćwiczeń.

1. Na stronie **Ustawienia** w obszarze **Wybieranie publicznych portów wejściowych** wybierz opcję **Brak publicznych portów wejściowych**. Dostęp za pomocą protokołu RDP skonfigurujemy później.

### <a name="finish-configuring-the-vm-and-create-the-image"></a>Kończenie konfigurowania maszyny wirtualnej i tworzenie obrazu

1. Przewiń w dół i kliknij przycisk **OK**.

1. W obszarze **Utwórz** sprawdź skonfigurowane ustawienia. Na dole kliknij pozycję **Utwórz**. Na pulpicie nawigacyjnym platformy Azure zostanie wyświetlona wdrażana maszyna wirtualna. Może to potrwać kilka minut.

## <a name="summary"></a>Podsumowanie

Utworzono maszynę wirtualną z systemem Windows Server, która spełnia wymagania studentów i jest dostępna z sieci uczelni. W następnym module zobaczysz, jak można za pomocą protokołu RDP nawiązać połączenie z maszyną wirtualną i nią zarządzać.
