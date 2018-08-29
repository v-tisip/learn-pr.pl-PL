Twoja firma podjęła decyzję o zarządzaniu danymi wideo ze swoich kamer ruchu na platformie Azure przy użyciu maszyn wirtualnych. Aby uruchomić wiele koderów, najpierw należy utworzyć maszyny wirtualne. Należy również nawiązać z nimi połączenie i wejść z nimi w interakcję. W tej jednostce dowiesz się, jak utworzyć maszynę wirtualną przy użyciu witryny Azure Portal. Następnie skonfigurujesz maszynę wirtualną na potrzeby połączenia RDP oraz wybierzesz obraz maszyny wirtualnej i odpowiednią opcję magazynu.

## <a name="introduction-to-windows-virtual-machines-in-azure"></a>Wprowadzenie do maszyn wirtualnych z systemem Windows na platformie Azure

Maszyny wirtualne platformy Azure to skalowane zasoby przetwarzania w chmurze na żądanie. Są one podobne do maszyn wirtualnych hostowanych w ramach funkcji Hyper-V systemu Windows. Obejmują one procesor, pamięć, magazyn i zasoby sieciowe. Maszyny wirtualne można uruchomiać i zatrzymywać w dowolnym momencie, podobnie jak w przypadku funkcji Hyper-V, oraz zarządzać nimi z poziomu witryny Azure Portal lub przy użyciu wiersza polecenia platformy Azure. Aby połączyć się bezpośrednio z interfejsem użytkownika pulpitu systemu Windows można również użyć klienta RDP i korzystać z maszyny wirtualnej w taki sposób, jak w przypadku logowania się na lokalnym komputerze z systemem Windows.

## <a name="create-resources-for-a-windows-vm"></a>Tworzenie zasobów na potrzeby maszyny wirtualnej z systemem Windows

Podczas tworzenia maszyny wirtualnej z systemem Windows na platformie Azure można również tworzyć zasoby służące do hostowania maszyny wirtualnej. Podobnie jak w przypadku innych usług platformy Azure, konieczne jest posiadanie **grupy zasobów**. Stosowaną powszechnie praktyką jest dołączanie innych usług, które są powiązane z maszyną wirtualną, do tej samej grupy zasobów, w tym:

* Maszyna wirtualna
* Magazyn
* Sieci wirtualne 
* Interfejsy sieciowe
* Podsieć
* Publiczny adres IP

Podczas tworzenia nowej maszyny wirtualnej możesz użyć istniejącej grupy zasobów lub utworzyć nową grupę zasobów.

## <a name="choose-the-vm-image"></a>Wybieranie obrazu maszyny wirtualnej

Wybieranie obrazu jest jedną z pierwszych i najważniejszych decyzji, które należy podjąć podczas tworzenia maszyny wirtualnej. Obraz to szablon, który jest używany do tworzenia maszyny wirtualnej. Te szablony zawierają system operacyjny i często także inne oprogramowanie, takie jak narzędzia programistyczne lub środowiska hostingu internetowego.

Wszystko to, co można zainstalować na komputerze, może zostać dołączone do obrazu, co daje bardzo duże możliwości. Maszynę wirtualną możesz utworzyć na podstawie obrazu, który został wstępnie skonfigurowany na potrzeby dokładnie tych zadań, których potrzebujesz, na przykład do hostowania aplikacji ASP.NET Core.

Opcjonalnie możesz tworzyć i przekazywać własne obrazy, ale wykracza to poza zakres tego modułu.

> [!Note] 
> Zwróć uwagę na funkcję o nazwie „Maszyna wirtualna (wersja klasyczna)”. Jest to starsza funkcja obsługiwana na potrzeby klientów, którzy już utworzyli wystąpienia. Dla nowych obciążeń należy użyć funkcji „Maszyna wirtualna platformy Azure” lub w skrócie „Maszyny wirtualne”.

## <a name="sizing-your-vm"></a>Ustalanie rozmiaru maszyny wirtualnej

Maszyna wirtualna podobnie, jak maszyna fizyczna, ma określoną ilość pamięci i moc procesora CPU. Na platformie Azure dostępne są różne rozmiary maszyn wirtualnych w różnych cenach. Mogą to być maszyny wirtualne z serii A służące do podstawowych czynności deweloperskich i tworzenia obrazów testowych, jak również maszyny z serii D służące do przeprowadzania obliczeń ogólnego przeznaczenia. Dostępne są również maszyny z serii H służące do wykonywania obliczeń o wysokiej wydajności oraz maszyny z serii N zoptymalizowane pod kątem zastosowań wymagających procesora GPU.

Jak zobaczysz później w module, rozmiar maszyny wirtualnej można zmienić po jej utworzeniu, ale wymaga to jej zamknięcia, co może spowodować przestój naszych obciążeń.

## <a name="choosing-storage-options"></a>Wybieranie opcji magazynu

Następny wybór do dokonania podczas określania maszyny wirtualnej to technologia dysku twardego. Opcje obejmują tradycyjne talerzowe dyski twarde (HDD) lub nowocześniejsze dyski półprzewodnikowe (SSD). Korzystanie z magazynu SSD jest droższe, ale zapewnia lepszą wydajność, szczególnie w środowiskach obsługujących duży transfer danych lub częste operacje we/wy.

> [!Note] 
> Aplikacje w usłudze Azure Virtual Machines można również połączyć z innymi formami trwałości na platformie Azure, takimi jak usługa Azure Cosmos DB i Azure Blob Storage.
