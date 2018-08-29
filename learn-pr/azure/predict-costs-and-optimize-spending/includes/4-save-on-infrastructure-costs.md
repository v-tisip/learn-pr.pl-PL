Zapoznaliśmy się ze sposobem szacowania kosztów dla środowisk planowanych do utworzenia oraz posłużyliśmy się pewnymi narzędziami, aby uzyskać szczegółowe informacje o miejscach powstawania kosztów i przewidywanych przyszłych wydatkach. Nasze następne wyzwanie to określenie, jak obniżyć koszty infrastruktury.

## <a name="use-reserved-instances"></a>Użycie wystąpień zarezerwowanych

W przypadku z natury statycznych i przewidywalnych obciążeń maszyn wirtualnych, szczególnie występujących w sposób ciągły (24 godziny na dobę, 7 dni w tygodniu, 365 dni w roku), użycie wystąpień zarezerwowanych to doskonały sposób na oszczędności w wysokości do 70% (w zależności od rozmiaru maszyny wirtualnej).

![Oszczędności dzięki wystąpieniom zarezerwowanym](../images/savings-coins.png)

Wystąpienia zarezerwowane można zakupić na okres 1 roku lub 3 lat, przy czym płatność jest wymagana za cały okres z góry. Po zakupie firma Microsoft dopasowuje rezerwację do uruchomionych wystąpień i zmniejsza liczbę godzin pozostałych dla rezerwacji. Rezerwacje można zakupić za pośrednictwem witryny Azure Portal. Ponieważ wystąpienia zarezerwowane stanowią rabat na zasoby obliczeniowe, są dostępne dla maszyn wirtualnych zarówno z systemem Windows, jak i Linux.

## <a name="right-size-underutilized-virtual-machines"></a>Ustawianie prawidłowego rozmiaru dla nie w pełni wykorzystanych maszyn wirtualnych

W ramach poprzedniego omówienia wspomniano, że usługi Azure Cost Management i Azure Advisor mogą zalecić ustawienie prawidłowego rozmiaru lub wyłączenie maszyn wirtualnych. Ustawianie prawidłowego rozmiaru maszyny wirtualnej to proces zmiany jej rozmiaru na odpowiedni. Wyobraźmy sobie serwer pracujący jako kontroler domeny i używający rozmiaru **Standard_D4sv3**. Przez ogromną większość czasu maszyna wirtualna jest w 90% bezczynna. Zmiana rozmiaru tej maszyny wirtualnej na **Standard_D2s_v3** zmniejsza koszt obliczeń o 50%. Koszty są liniowe i podwajają się dla każdego większego rozmiaru w ramach tej samej serii. W tym przypadku korzystna może być nawet zmiana serii wystąpień na mniej kosztowną serię maszyn wirtualnych.

![Zmiana rozmiaru maszyny wirtualnej](../images/vm-resize.png)

Zbyt duże maszyny wirtualne to typowe niepotrzebne wydatki na platformie Azure i to takie, które można łatwo zredukować. Rozmiar maszyny wirtualnej możesz zmienić za pośrednictwem witryny Azure Portal, programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.

> [!NOTE]
> Zmiana rozmiaru maszyny wirtualnej wymaga jej zatrzymania, zmiany rozmiaru, a następnie ponownego uruchomienia. Może to potrwać kilka minut w zależności do zakresu operacji zmiany rozmiaru. Podczas wykonywania tego zadania należy zaplanować przestój lub przenieść ruch do innego wystąpienia.

## <a name="deallocate-virtual-machines-in-off-hours"></a>Cofanie przydziału maszyn wirtualnych poza godzinami pracy

Jeśli masz obciążenia maszyn wirtualnych, które są używane tylko w pewnych okresach, lecz działają nieustannie, marnujesz pieniądze. Te maszyny wirtualne to doskonali kandydaci do wyłączania w okresie bezczynności i ponownego uruchamiania zgodnie z harmonogramem, co pozwala zaoszczędzić na kosztach obliczeń, podczas gdy przydział maszyny wirtualnej jest cofnięty.

To podejście to doskonała strategia dla środowisk deweloperskich. Często programowanie odbywa się tylko podczas godzin pracy, dzięki czemu można elastycznie cofnąć przydział tych systemów poza godzinami pracy i zatrzymać naliczanie kosztów za operacje obliczeniowe. Platforma Azure ma teraz w pełni dostępne [rozwiązanie do automatyzacji](https://docs.microsoft.com/azure/automation/automation-solution-vm-management), którego możesz użyć w swoim środowisku.

Na maszynie wirtualnej jest także dostępna funkcja automatycznego zamykania, co pozwala na zaplanowanie zamykania.

![Automatyczne zamykanie](../images/vm-auto-shutdown.png)

## <a name="delete-unused-virtual-machines"></a>Usuwanie nieużywanych maszyn wirtualnych 

 Ta porada może wydawać się oczywista, ale jeśli nie używasz usługi, wyłącz ją. Często można spotkać już niepotrzebne systemy nieprodukcyjne lub demonstracyjne pozostałe po projekcie. Regularnie przeglądaj środowisko w celu zidentyfikowania tych systemów. Ich zamknięcie może dać wiele korzyści nie tylko w postaci obniżenia kosztów infrastruktury, lecz także w postaci potencjalnych oszczędności na licencjach i kosztach utrzymania.

## <a name="migrate-to-paas-or-saas-services"></a>Migracja do usług PaaS lub SaaS 

W miarę przenoszenia obciążeń do chmury naturalną koleją rzeczy jest rozpoczęcie od usług IaaS (infrastruktura jako usługa), a następnie odpowiednie przenoszenie ich do usług PaaS (platforma jako usługa) w ramach iteracyjnego procesu.

Usługi PaaS zwykle dają znaczące oszczędności dotyczące zarówno zasobów, jak i kosztów operacyjnych. Wyzwanie polega na tym, że w zależności od typu usługi jej przeniesienie może wymagać różnych nakładów z punktu widzenia czasu i zasobów. Przeniesienie bazy danych programu SQL Server do usługi Azure SQL Database może być łatwe, lecz zmiana architektury wielowarstwowej aplikacji na architekturę kontenerową lub bezserwerową może być o wiele większym wysiłkiem. Dobra praktyka to ciągła ocena architektury aplikacji pod kątem określenia, czy zastosowanie usług PaaS może przynieść korzyści.  

Platforma Azure ułatwia testowanie tych usług przy niewielkim ryzyku, umożliwiając stosunkowo łatwe wypróbowanie nowych wzorców architektury. Jednak jest to zwykle dłuższe przedsięwzięcie i może nie stanowić natychmiastowej pomocy, jeśli szukasz szybkiego rozwiązania z punktu widzenia redukcji kosztów. Centrum architektury platformy Azure to doskonałe miejsce do znajdowania pomysłów na transformację Twojej aplikacji oraz poznawanie najlepszych rozwiązań dla szerokiej gamy architektur i usług platformy Azure. 