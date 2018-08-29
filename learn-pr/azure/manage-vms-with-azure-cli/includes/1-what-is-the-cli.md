Jan zarządza zbiorem maszyn wirtualnych platformy Azure działających w naszej firmowej infrastrukturze internetowej, która obejmuje kilka witryn internetowych i serwerów baz danych uruchomionych na różnych platformach. 

Witryna Azure Portal jest co prawda łatwa w użyciu, ale Jan zauważył, że nawigowanie po różnych blokach wydłuża wykonywanie niektórych zadań. 

Podczas eksplorowania rozwiązań alternatywnych Jan odkrywa narzędzie interfejsu wiersza polecenia platformy Azure.

Pracując za pomocą interfejsu wiersza polecenia platformy Azure, Jan można pisać skrypty, aby sprawdzać stan swoich serwerów, wdrażać nowe konfiguracje, otwierać port lub nawiązywać połączenie z maszyną wirtualną w celu zmiany ustawienia.

Być może jesteś jak Jan i szukasz narzędzia pomocnego w automatyzacji zadań w Twoim środowisku chmurowym. Pokażemy Ci, jak używać interfejsu wiersza polecenia platformy Azure do tworzenia maszyn wirtualnych hostowanych na platformie Azure i zarządzania nimi. 

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Interfejs wiersza polecenia platformy Azure to wieloplatformowe narzędzie wiersza polecenia do zarządzania zasobami platformy Azure. Jest ono dostępne dla systemów macOS, Linux i Windows oraz w przeglądarce za pomocą usługi [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

> [!IMPORTANT]
> Obecnie są dostępne dwie wersje narzędzia interfejsu wiersza polecenia platformy Azure: 1.0 i 2.0. Będziemy używać interfejsu wiersza polecenia platformy Azure w wersji 2.0, która jest najnowsza i zalecana, chyba że uruchamiasz starsze skrypty napisane dla wersji 1.0. Interfejs wiersza polecenia platformy Azure w wersji 1.0 jest uruchamiany przy użyciu polecenia `azure`, a interfejs wiersza polecenia platformy Azure w wersji 2.0 jest uruchamiany przy użyciu polecenia `az`. 

Interfejs wiersza polecenia platformy Azure może pomóc Ci w zarządzaniu zasobami platformy Azure, takimi jak maszyny wirtualne i dyski, z poziomu wiersza polecenia lub za pomocą skryptów. Zacznijmy i sprawdźmy, co możemy zrobić.

## <a name="learning-objectives"></a>Cele szkolenia
> [!div class="checklist"]
> * Utworzenie maszyny wirtualnej platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure
> * Zmiana rozmiarów maszyn wirtualnych przy użyciu interfejsu wiersza polecenia
> * Zarządzanie maszyną wirtualną i wykonywanie na niej zapytań z poziomu wiersza polecenia
> * Zainstalowanie oprogramowania na maszynie wirtualnej