Tworzenie skryptów administracyjnych to zaawansowany sposób optymalizowania przepływu pracy. Można automatyzować typowe, powtarzalne zadania, a po weryfikacji skrypt będzie działać w spójny sposób, prawdopodobnie zmniejszając liczbę błędów.

Załóżmy, że pracujesz w firmie, która używa usługi Azure Virtual Machines do testowania oprogramowania służącego do zarządzania relacjami z klientami (CRM, Customer Relationship Management). Maszyny wirtualne są tworzone na podstawie obrazów obejmujących fronton internetowy, usługę internetową, która implementuje logikę biznesową, oraz bazę danych SQL.

Na pojedynczej maszynie wirtualnej wykonano wiele rund testów i zauważono, że zmiany bazy danych i plików konfiguracji mogą powodować niespójne wyniki. W jednym przypadku usterka spowodowała utworzenie rekordu połączeń telefonicznych bez odpowiadającego mu klienta w bazie danych. Rekord oddzielony spowodował niepowodzenie kolejnych testów integracji nawet po naprawieniu usterki. Zamierzasz rozwiązać ten problem, używając świeżego wdrożenia maszyny wirtualnej w każdym cyklu testowania. Chcesz zautomatyzować konfigurację tworzenia maszyny wirtualnej, ponieważ będzie ono wykonywane wiele razy na tydzień. 

W tym miejscu zobaczysz, jak zarządzać zasobami platformy Azure przy użyciu programu Azure PowerShell. Będziesz interaktywnie używać programu Azure PowerShell w przypadku zadań jednorazowych i pisać skrypty w celu zautomatyzowania powtarzanych zadań. 

## <a name="learning-objectives"></a>Cele szkolenia
> [!div class="checklist"]
> * Podjęcie decyzji wskazującej, czy program Azure PowerShell jest właściwym narzędziem do wykonywania zadań administracyjnych
> * Zainstalowanie programu Azure PowerShell w systemie Linux, macOS i Windows
> * Połączenie z subskrypcją platformy Azure przy użyciu programu Azure PowerShell
> * Skonfigurowanie zasobów platformy Azure za pomocą programu Azure PowerShell

## <a name="prerequisites"></a>Wymagania wstępne
- Środowisko z interfejsem wiersza polecenia, takie jak program PowerShell lub Bash
- Znajomość podstawowych pojęć dotyczących platformy Azure, takich jak grupy zasobów i maszyny wirtualne
- Doświadczenie w administrowaniu zasobami platformy Azure przy użyciu witryny Azure Portal
