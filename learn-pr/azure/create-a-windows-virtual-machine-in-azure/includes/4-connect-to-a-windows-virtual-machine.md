Jako administrator sieci w firmie zajmującej się analizą danych ponosisz odpowiedzialność za nawiązywanie połączeń z maszynami wirtualnymi na platformie Azure i weryfikowanie poprawności ich konfiguracji. Robisz to przy użyciu klienta protokołu Remote Desktop Protocol, łącząc się z interfejsem użytkownika pulpitu na maszynie wirtualnej z systemem Windows.

## <a name="what-is-the-remote-desktop-protocol"></a>Co to jest protokół Remote Desktop Protocol?

Protokół Remote Desktop Protocol (RDP) umożliwia zdalną łączność z interfejsem użytkownika komputerów z systemem Windows. Protokół RDP pozwala na zalogowanie się do zdalnego fizycznego lub wirtualnego komputera z systemem Windows i kontrolowanie go tak, jak siedząc przy nim.

> [!Note]
> Funkcja Windows Hyper-V w systemach Windows Server 2016 i Windows 10 używa protokołu RDP do łączenia się z maszynami wirtualnymi uruchomionymi za pomocą funkcji hypervisor.

Połączenie RDP umożliwia wykonywanie ogromnej większości operacji dostępnych z poziomu konsoli komputera fizycznego z wyjątkiem używania niektórych możliwości związanych z zasilaniem i sprzętem.

Połączenie RDP wymaga klienta RDP. Firma Microsoft oferuje klientów RDP dla następujących systemów operacyjnych:

* Windows
* iOS
* MacOS
* Android

Istnieją również klienci systemu Linux typu open source, tacy jak Remmina, umożliwiający nawiązywanie połączenia z komputerem z systemem Windows z poziomu dystrybucji systemu Ubuntu.

System Windows 10 zawiera klienta RDP.

![Klient RDP systemu Windows](../media-drafts/4-rdp-client.PNG)

## <a name="what-functionality-does-an-rdp-connection-support"></a>Jakie funkcje obsługuje połączenie za pomocą protokołu RDP?

Za pomocą połączenia protokołu RDP możesz korzystać z interfejsu użytkownika. Jednak możesz również połączyć się z innymi usługami na komputerze zdalnym. Usługi te obejmują:

* Połączenia drukarek, które umożliwiają komputerowi zdalnemu drukowanie na Twojej drukarce lokalnej.
* Odtwarzanie dźwięku, przy czym dźwięk może być odtwarzany na komputerze lokalnym lub na urządzeniu zdalnym.
* Nagrywanie dźwięku, przy czym jest możliwe nagrywanie dźwięku z komputera lokalnego i przekierowanie go do urządzenia zdalnego.
* Porty, które możesz przekierować do portów na komputerze lokalnym.
* Dyski, w tym zamapowane dyski sieciowe, które są dostępne tak jak dyski podłączone do komputera zdalnego.
* Urządzenia do przechwytywania wideo, takie jak zintegrowane kamery internetowe.
* Inne obsługiwane urządzenia typu plug and play.

Nie wszystkie te funkcje są obsługiwane na platformie Azure, ponieważ dostępność zasobów fizycznych na tej platformie jest ograniczona. Na przykład tylko drukarki programowe można przekierować przez połączenie RDP z maszyny wirtualnej hostowanej na platformie Azure do urządzeń drukujących klienta nawiązującego połączenie.

## <a name="configure-network-settings-for-rdp-access-to-virtual-machines"></a>Konfigurowanie ustawień sieciowych pod kątem dostępu RDP do maszyn wirtualnych

Połączenia z maszynami wirtualnymi platformy Azure można nawiązywać na trzy sposoby:

1. Bezpośrednio za pomocą publicznego adresu IP maszyny wirtualnej.
2. Za pomocą połączenia wirtualnej sieci prywatnej (VPN, virtual private network).
3. Za pośrednictwem połączenia usługi ExpressRoute.

Publiczny adres IP może być przydzielony na stałe lub dynamicznie. Należy również upewnić się, że dostęp do adresu publicznego maszyny wirtualnej jest możliwy na porcie 3389 (protokół RDP). Ten warunek może wymagać wynegocjowania z zespołem zarządzającym zabezpieczeniami zapory Twojej organizacji udostępnienia portu 3389 dla publicznego adresu IP maszyny wirtualnej przez skonfigurowanie odpowiedniej reguły.

Dynamiczne publiczne adresy IP są przydzielane ponownie za każdym razem, gdy maszyna wirtualna zostanie uruchomiona ponownie. Statyczne adresy są trwałe, lecz kosztują więcej.

Aby połączenie za pośrednictwem sieci VPN było możliwe, sieć lokalna musi mieć aktywne połączenie VPN z platformą Microsoft Azure.

Podejście z użyciem połączenia usługi ExpressRoute umożliwia zarządzanie łącznością z maszyną wirtualną. Ta metoda zapewnia także najmniejsze opóźnienie i największą przepustowość połączenia.

> [!Note]
> Niezależnie od opcji wybranej na potrzeby nawiązywania połączenia z platformą Azure należy upewnić się, że maszyna wirtualna jest dostępna za pośrednictwem protokołu RDP, zwykle na domyślnym porcie 3389. Maszynę wirtualną można skonfigurować tak, aby była dostępna tylko dla Twojego adresu IP klienta. Łączenie z maszyną wirtualną za pośrednictwem portu 3389 i publicznego adresu IP jest zalecane tylko w środowiskach testowych. W środowiskach produkcyjnych należy użyć opcji 2 lub 3.

## <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a>Jak można nawiązać połączenie z maszyną wirtualną na platformie Azure przy użyciu protokołu RDP?

Łączenie z maszyną wirtualną na platformie Azure przy użyciu protokołu RDP jest prostym procesem. W witrynie Azure Portal przejdź do właściwości maszyny wirtualnej i u góry strony kliknij pozycję **Połącz**. Ta akcja spowoduje pobranie wstępnie skonfigurowanego pliku RDP, który system Windows otworzy w kliencie RDP. Plik RDP umożliwia skonfigurowanie łączenia za pośrednictwem publicznego adresu IP maszyny wirtualnej. W przypadku łączenia przez sieć VPN lub za pomocą usługi ExpressRoute możesz wybrać wewnętrzny adres IP. Wtedy możesz również wybrać numer portu dla połączenia.

Jeśli używasz statycznego publicznego adresu IP dla maszyny wirtualnej, możesz zapisać plik RDP na pulpicie. Jeśli używasz dynamicznego adresowania IP, plik RDP pozostaje ważny tylko tak długo, jak długo maszyna wirtualna jest uruchomiona. Jeśli maszyna wirtualna zostanie zatrzymana i uruchomiona ponownie, należy pobrać kolejny plik RDP.

> [!Note]
> Inna możliwość to wpisanie publicznego adresu IP maszyny wirtualnej w kliencie RDP systemu Windows i kliknięcie pozycji **Połącz**.

Po nawiązaniu połączenia są zwykle wyświetlane dwa ostrzeżenia. Są to:

* Ostrzeżenie o wydawcy — spowodowane tym, że plik RDP nie jest podpisany za pomocą klucza publicznego.
* Ostrzeżenie o certyfikacie — spowodowane tym, że certyfikat maszyny nie jest zaufany.

W środowiskach testowych można zignorować te ostrzeżenia. W środowiskach produkcyjnych plik RDP można podpisać przy użyciu programu RDPSIGN.EXE, a certyfikat maszyny umieścić w magazynie **zaufanych głównych urzędów certyfikacji** klienta.

## <a name="summary"></a>Podsumowanie

Teraz możesz nawiązać połączenie z maszyną wirtualną z systemem Windows przy użyciu protokołu RDP. W poniższym ćwiczeniu użyjesz protokołu RDP do połączenia się z maszyną wirtualną, a następnie zainstalujesz rolę serwera na komputerze.
