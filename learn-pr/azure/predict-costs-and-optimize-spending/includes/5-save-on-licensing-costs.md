Licencjonowanie to kolejny obszar, który może znacząco wpłynąć na Twoje wydatki w chmurze. Przyjrzyjmy się kilku sposobom, dzięki którym można zmniejszyć koszty licencjonowania.

## <a name="azure-hybrid-benefit-for-windows-server"></a>Korzyść użycia hybrydowego platformy Azure dla systemu Windows Server

Wielu klientów zainwestowało w licencje systemu Windows Server i chce zmienić cel tej inwestycji na platformie Azure. Korzyść użycia hybrydowego platformy Azure zapewnia klientom prawo do używania tych licencji dla maszyn wirtualnych na platformie Azure. Oznacza to, że nie zostanie naliczona opłata za licencję systemu Windows Server, a zamiast tego w rozliczeniu będzie używana stawka dla systemu Linux. 

Aby kwalifikować się do tej korzyści, licencje systemu Windows muszą być objęte pakietem Software Assurance. Będą również obowiązywać następujące wskazówki:

- Każda licencja na dwa procesory lub każdy zestaw licencji na 16 rdzeni jest uprawniony do dwóch wystąpień z maksymalnie 8 rdzeniami lub jednego wystąpienia z maksymalnie 16 rdzeniami. 
- Licencje wersji Standard Edition mogą być używane tylko raz — lokalnie lub na platformie Azure. Oznacza to, że nie można użyć tej samej licencji na maszynie wirtualnej platformy Azure i na komputerze lokalnym.
- Korzyści wersji Datacenter Edition pozwalają na równoczesne użycie w środowisku lokalnym i na platformie Azure, dlatego licencja obejmuje dwie działające maszyny z systemem Windows. 

> [!NOTE]
> Większość klientów jest zwykle licencjonowana według liczby rdzeni, dlatego w obliczeniach użyjemy tego modelu. Jeśli masz pytania dotyczące swoich licencji, skontaktuj się z odsprzedawcą licencji lub zespołem ds. kont Microsoft.

Zastosowanie korzyści jest proste. Można ją włączać i wyłączać w dowolnym momencie na istniejących maszynach wirtualnych lub stosować w czasie wdrażania na nowych maszynach wirtualnych. Korzyść użycia hybrydowego (szczególnie w połączeniu z wystąpieniami zarezerwowanymi) może zapewnić znaczne oszczędności związane z licencjami.

## <a name="azure-hybrid-benefit-for-sql-server"></a>Korzyść użycia hybrydowego platformy Azure dla programu SQL Server

Korzyść użycia hybrydowego platformy Azure dla programu SQL Server pomaga zmaksymalizować wartość aktualnych inwestycji dotyczących licencjonowania i przyspieszyć migrację do chmury. Korzyść użycia hybrydowego platformy Azure dla programu SQL Server to oparta na platformie Azure korzyść, która umożliwia używanie licencji programu SQL Server z aktywnym pakietem Software Assurance, co pozwala na płacenie przy użyciu niższej stawki.

Tę korzyść można stosować, nawet jeśli zasób platformy Azure jest aktywny, ale niższa stawka będzie stosowana od momentu wybrania jej w portalu. Żadne środki nie będą wydawane wstecznie.

### <a name="azure-sql-database-vcore-based-options"></a>Oparte na rdzeniach wirtualnych opcje usługi Azure SQL Database

![Obrót licencjami programu SQL Server](../images/sql-tradein-value.jpg)

W przypadku usługi Azure SQL Database korzyść użycia hybrydowego platformy Azure działa w następujący sposób:

- Jeśli masz licencje na rdzeń w wersji Standard Edition z aktywnym pakietem Software Assurance, możesz otrzymać jeden rdzeń wirtualny w warstwie usługi Ogólnego przeznaczenia na każdy licencjonowany rdzeń używany w środowisku lokalnym.
- Jeśli masz licencje na rdzeń w wersji Enterprise Edition z aktywnym pakietem Software Assurance, możesz otrzymać jeden rdzeń wirtualny w warstwie usługi Krytyczne dla działania firmy na każdy licencjonowany rdzeń używany w środowisku lokalnym. Pamiętaj, że korzyść użycia hybrydowego platformy Azure dla programu SQL Server w warstwie usługi Krytyczne dla działania firmy jest dostępna tylko dla klientów, którzy mają licencje Enterprise Edition.
- Jeśli masz licencje na rdzeń w wysoce zwirtualizowanej wersji Standard Edition z aktywnym pakietem Software Assurance, możesz otrzymać cztery rdzenie wirtualne w warstwie usługi Ogólnego przeznaczenia na każdy licencjonowany rdzeń używany w środowisku lokalnym. Jest to unikatowa korzyść wirtualizacji dostępna tylko w usłudze Azure SQL Database.

W przypadku programu SQL Server w usłudze Azure Virtual Machines korzyść użycia hybrydowego platformy Azure działa w następujący sposób:

- Jeśli masz licencje na rdzeń w wersji Enterprise Edition z aktywnym pakietem Software Assurance, możesz otrzymać jeden rdzeń programu SQL Server Enterprise Edition w usłudze Azure Virtual Machines na każdy licencjonowany rdzeń używany w środowisku lokalnym.
- Jeśli masz licencje na rdzeń w wersji Standard Edition z aktywnym pakietem Software Assurance, możesz otrzymać jeden rdzeń programu SQL Server Standard Edition w usłudze Azure Virtual Machines na każdy licencjonowany rdzeń używany w środowisku lokalnym.

Może mieć to znaczący wpływ na wydatki związane z platformą Azure i obciążeniami programu SQL Server.

## <a name="use-devtest-subscription-offers"></a>Korzystanie z ofert subskrypcji warstwy Tworzenie i testowanie

Oferty [Enterprise — tworzenie i testowanie](https://azure.microsoft.com/offers/ms-azr-0148p/) oraz [Płatność zgodnie z rzeczywistym użyciem — tworzenie i testowanie](https://azure.microsoft.com/offers/ms-azr-0023p/) to korzyść, którą można zastosować w celu obniżenia kosztów w środowiskach nieprodukcyjnych. Ta korzyść oferuje szereg rabatów, zwłaszcza w przypadku obciążeń systemu Windows, eliminując opłaty za licencje i pozostawiając tylko rozliczenia używające stawki systemu Linux dla maszyn wirtualnych. Dotyczy to również programu SQL Server i dowolnego innego oprogramowania firmy Microsoft objętego subskrypcją programu Visual Studio (wcześniej znaną jako MSDN). Istnieje kilka wymagań dotyczących tej korzyści. Jedno z nich wskazuje, że jest ona przeznaczona tylko dla obciążeń nieprodukcyjnych, a drugie — że wszyscy użytkownicy tych środowisk (z wyjątkiem testerów) muszą być objęci subskrypcją programu Visual Studio. Krótko mówiąc, w przypadku obciążeń nieprodukcyjnych dzięki tej korzyści można zmniejszyć wydatki na obciążenia związane z systemem Windows i programu SQL Server oraz inne obciążenia maszyn wirtualnych firmy Microsoft.
Poniżej przedstawiono kompletne szczegóły poszczególnych ofert. Jeśli jesteś klientem w ramach umowy Enterprise Agreement, skorzystaj z oferty Enterprise — tworzenie i testowanie. Jeśli jesteś klientem bez umowy Enterprise Agreement i w zamian używasz kont płatności zgodnie z rzeczywistym użyciem, skorzystaj z oferty Płatność zgodnie z rzeczywistym użyciem — tworzenie i testowanie.

## <a name="bring-your-own-sql-server-license"></a>Bring your own license — program SQL Server

Jeśli jesteś klientem w ramach umowy Enterprise Agreement i masz już inwestycję w licencje programu SQL Server, które zostały zwolnione jako część procesu przenoszenia zasobów na platformę Azure, możesz aprowizować obrazy modelu **bring your own license** (BYOL) z witryny Azure Marketplace. Umożliwi Ci to skorzystanie z nieużywanych licencji i zmniejszy koszt maszyny wirtualnej platformy Azure. Taka możliwość zawsze istniała — trzeba było aprowizować maszynę wirtualną z systemem Windows i ręcznie zainstalować program SQL Server. Teraz proces ten jest uproszczony dzięki użyciu certyfikowanych obrazów firmy Microsoft. Wyszukaj pozycję **BYOL** w portalu Marketplace w celu znalezienia tych obrazów.

![Model BYOL dla programu SQL Server na platformie Azure](../images/byol-sql-server.png)

> [!IMPORTANT]
> Do używania certyfikowanych obrazów BYOL jest wymagana subskrypcja Enterprise Agreement.

## <a name="use-sql-server-developer-edition"></a>Korzystanie z programu SQL Server Developer Edition

Wiele osób nie wie, że program SQL Server Developer Edition jest bezpłatnym produktem do **użytku nieprodukcyjnego**. Wersja Developer Edition ma te same funkcje, co wersja Enterprise Edition, ale w przypadku obniżeń nieprodukcyjnych można znacznie zredukować koszty licencjonowania.

Wyszukaj obrazy programu SQL Server dla wersji Developer Edition w witrynie Azure Marketplace i używaj ich dla celów programowania lub testowania w celu wyeliminowania dodatkowych kosztów programu SQL Server w takich przypadkach. 

> [!NOTE]
> Pełne informacje na temat licencjonowania można znaleźć w [dokumentacji zawierającej wskazówki dotyczące cen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="use-constrained-instance-sizes-for-database-workloads"></a>Korzystanie z ograniczonych rozmiarów wystąpień w przypadku obciążeń bazy danych 

Wielu klientów ma wysokie wymagania dotyczące pamięci, magazynu lub przepustowości operacji we/wy, ale potrzebuje małej liczby rdzeni procesorów CPU. Odpowiadając na to popularne żądanie, firma Microsoft udostępniła najpopularniejsze serie maszyn wirtualnych (DS, ES, GS i MS) w nowych rozmiarach, które ograniczają liczbę procesorów wirtualnych do połowy lub ćwierci oryginalnego rozmiaru maszyny wirtualnej przy zachowaniu tej samej pamięci, magazynu i przepustowości operacji we/wy.

| Rozmiar maszyny wirtualnej | Procesory wirtualne | Memory (Pamięć) | Maksymalna liczba dysków | Maksymalna przepustowość operacji we/wy | Koszt licencjonowania programu SQL Server Enterprise na rok | Łączny koszt za rok (obliczenia + licencjonowanie) |
|---------|-------|--------|-----------|--------------------|-----------------------------------------------|---------------------------|
| Standardowa_DS14v2   | 16 | 112 GB | 32 | 51 200 operacji we/wy lub 768 MB/s |           |           |
| Standardowa_DS14-4v2 | **4**  | 112 GB | 32 | 51 200 operacji we/wy lub 768 MB/s | 75% niższy | 57% niższy |
| Standardowa_GS5      | 32 | 448    | 64 | 80 000 operacji we/wy lub 2 GB/s   |           |           |
| Standardowa_GS5-8    | **8**  | 448    | 64 | 80 000 operacji we/wy lub 2 GB/s   | 75% niższy | 42% niższy |

Ponieważ produkty bazodanowe, takie jak SQL Server i Oracle, są licencjonowane według liczby procesorów CPU, klienci mogą zmniejszyć koszt licencjonowania o nawet do 75%, ale nadal utrzymywać wysoką wydajność, której wymaga baza danych. 
