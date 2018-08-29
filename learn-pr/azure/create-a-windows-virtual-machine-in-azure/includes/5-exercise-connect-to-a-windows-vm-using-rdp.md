W tym ćwiczeniu użyjesz klienta RDP w celu nawiązania połączenia z maszyną wirtualną z systemem Windows, która została utworzona w poprzednim module. Połączenie można nawiązać, pobierając i uruchamiając plik RDP z witryny Azure Portal. Ten plik RDP będzie miał następujące właściwości:

* Publiczny adres IP maszyny wirtualnej.
* Numer portu.

## <a name="motivation"></a>Motywacja

Zgodnie z naszym scenariuszem ćwiczenia jesteś teraz studentem i chcesz uzyskać informacje o dodawaniu ról i funkcji do komputera z systemem Windows Server. Jednak administrator sieci nie pozwala Ci na wykonanie tego ćwiczenia na komputerze fizycznym w sieci, a komputery uczelniane nie spełniają wymagań dotyczących uruchamiania funkcji Hyper-V systemu Windows. Platforma Azure oferuje idealne rozwiązanie.

## <a name="configure-network-and-public-ip-address-settings"></a>Konfigurowanie ustawień sieć i publicznego adresu IP

1. W witrynie Azure Portal upewnij się, że otwarty jest blok dotyczący utworzonej wcześniej maszyny wirtualnej. Jeśli musisz otworzyć ten blok, możesz go znaleźć w obszarze **Wszystkie zasoby**.

1. Przejdź do sekcji **Sieć**. W górnej części tej sekcji znajdują się linki do podsieci wirtualnej i dynamicznego adresu IP, które zostały utworzone razem z maszyną wirtualną, ponieważ użyliśmy wartości domyślnych. Te linki umożliwiają zmianę wymienionych zasobów (na przykład zmianę na statyczny adres IP).

1. Kliknij pozycję **Dodaj regułę portu wejściowego**.

1. W górnej części okna dialogowego **Dodawanie reguły zabezpieczeń dla ruchu przychodzącego** kliknij pozycję **podstawowe**.

1. W obszarze **Usługa** wybierz pozycję **RDP**, a następnie kliknij przycisk **Dodaj**.

## <a name="connect-to-the-vm-by-using-rdp"></a>Nawiązywanie połączenia z maszyną wirtualną przy użyciu protokołu RDP

Aby pobrać plik RDP i nawiązać połączenie z maszyną wirtualną, wykonaj następujące kroki.

### <a name="download-the-rdp-file"></a>Pobieranie pliku RDP

1. W sekcji **Przegląd** bloku maszyny wirtualnej kliknij pozycję **Połącz**.

1. W bloku **Nawiązywanie połączenia z maszyną wirtualną** zanotuj wartości ustawień z pól **Adres IP** i **Numer portu**, a następnie kliknij pozycję **Pobierz plik RDP**.

1. W przeglądarce kliknij pozycję **Otwórz** lub **Uruchom** w celu otwarcia pliku RDP.

### <a name="connect-to-the-windows-vm"></a>Nawiązywanie połączenia z maszyną wirtualną z systemem Windows

1. W oknie dialogowym **Podłączanie pulpitu zdalnego** zanotuj ostrzeżenie o zabezpieczeniach i adres IP komputera zdalnego, a następnie kliknij przycisk **Połącz**.

1. W oknie dialogowym **Zabezpieczenia systemu Windows** wprowadź swoją nazwę użytkownika i hasło użyte w krokach 6 i 7.

1. W drugim oknie dialogowym **Podłączanie pulpitu zdalnego** zapoznaj się z błędami certyfikatów i kliknij pozycję **Tak**.

   > [!Note]
   > Po chwili zostanie wyświetlony pulpit maszyny wirtualnej. Dzieje się tak, ponieważ obraz B1 nie jest w pełni zgodny ze specyfikacją. Może pojawić się komunikat o niskiej alokacji pamięci.

1. W oknie dialogowym **Sieci** kliknij pozycję **Nie**.

### <a name="resize-the-vm-in-the-azure-portal"></a>Zmiana rozmiaru maszyny wirtualnej w witrynie Azure Portal

1. Wróć do witryny Azure Portal. Na stronie właściwości maszyny wirtualnej w obszarze **Ustawienia** kliknij pozycję **Rozmiar**.

1. Kliknij opcję **D2s_v3** (2 wirtualne procesory CPU, 8 GB pamięci RAM), a następnie kliknij pozycję **Wybierz**. Zostanie wyświetlony komunikat o zmianie rozmiaru maszyny wirtualnej. Maszyna wirtualna w oknie RDP zostanie również zamknięta.

1. Wróć do witryny Azure Portal. W lewym okienku kliknij pozycję **Maszyny wirtualne**.

1. W obszarze **Maszyny wirtualne** poczekaj, aż dla Twojej maszyny wirtualnej pojawi się stan **Uruchomiona**. Może być konieczne kliknięcie pozycji **Odśwież**.

1. Kliknij nazwę maszyny wirtualnej, a następnie w obszarze **Ustawienia** kliknij pozycję **Rozmiar**. Zauważ, że rozmiar maszyny wirtualnej jest teraz ustawiony na **D2s_v3**.

### <a name="reconnect-to-the-resized-vm"></a>Ponowne nawiązywanie połączenia z maszyną wirtualną o zmienionym rozmiarze

1. Kliknij pozycję **Maszyny wirtualne**, a następnie kliknij nazwę swojej maszyny wirtualnej. Zauważ, że wartość w polu **Publiczny adres IP** prawdopodobnie uległa zmianie. Kliknij pozycję **Połącz**, a następnie w przeglądarce kliknij pozycję **Uruchom** lub **Otwórz**.

1. W oknie dialogowym **Podłączanie pulpitu zdalnego** zanotuj ostrzeżenie o zabezpieczeniach i adres IP komputera zdalnego, a następnie kliknij przycisk **Połącz**.

1. W oknie dialogowym **Zabezpieczenia systemu Windows** wprowadź swoją nazwę użytkownika i hasło użyte w krokach 6 i 7.

1. W drugim oknie dialogowym **Podłączanie pulpitu zdalnego** zapoznaj się z błędami certyfikatów i kliknij pozycję **Tak**. Zwróć uwagę, że proces logowania do maszyny wirtualnej trwa teraz znacznie krócej.

1. Kliknij prawym przyciskiem myszy pasek zadań, a następnie kliknij opcję **Menedżer zadań**.

1. W oknie **Menedżer zadań** kliknij pozycję **Więcej szczegółów**.

1. Kliknij kartę **Wydajność**. Zauważ, że całkowitej dostępnej pamięci jest 8 GB, z których około 1,2 GB będzie używanych. Zamknij okno **Menedżer zadań**.

## <a name="summary"></a>Podsumowanie

Nawiązano połączenie z maszyną wirtualną z systemem Windows przy użyciu protokołu RDP. Dostęp za pomocą interfejsu użytkownika pulpitu umożliwia administrowanie tą maszyną wirtualną tak jak komputerem z systemem Windows.
