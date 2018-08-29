Przedstawiliśmy sposób szacowania kosztów przed wdrożeniem usług na platformie Azure, ale co zrobić, jeśli masz już wdrożone zasoby? Jak uzyskać wgląd w koszty, które są już naliczane? Jeśli wdrożyliśmy nasze poprzednie rozwiązanie na platformie Azure, a teraz chcemy upewnić się, że rozmiary maszyn wirtualnych są prawidłowe, oraz przewidzieć wysokość rachunku, jak możemy to zrobić? Przyjrzyjmy się kilku narzędziom platformy Azure, które mogą ułatwić Ci rozwiązanie tego problemu.

## <a name="what-is-azure-advisor"></a>Co to jest Azure Advisor? 

**Azure Advisor** to bezpłatna usługa wbudowana w platformę Azure, która udostępnia zalecenia dotyczące wysokiej dostępności, bezpieczeństwa, wydajności i kosztów. Usługa Advisor analizuje wdrożone usługi i szuka sposobów na ulepszenie środowiska w tych czterech obszarach. Skupimy się na zaleceniach dotyczących kosztów, ale warto również poświęcić trochę czasu na zapoznanie się z innymi zaleceniami.

Usługa Advisor oferuje zalecenia dotyczące kosztów w następujących obszarach: 

1. **Zmniejszanie kosztów dzięki wyeliminowaniu nieaprowizowanych obwodów usługi Azure ExpressRoute.** 
    Identyfikuje obwody usługi ExpressRoute, które mają stan dostawcy *Nie aprowizowano* dłużej niż jeden miesiąc i zaleca usunięcie obwodu, jeśli nie planujesz go aprowizować z użyciem dostawcy łączności.

2. **Kupowanie wystąpień zarezerwowanych w celu zaoszczędzenia pieniędzy w porównaniu z płatnością zgodnie z rzeczywistym użyciem.** 
    Przegląda użycie maszyny wirtualnej w ciągu ostatnich 30 dni i określa, czy w przyszłości można zaoszczędzić pieniądze, kupując wystąpienia zarezerwowane. Usługa Advisor pokaże Ci regiony i rozmiary potencjalnie oferujące największe oszczędności, a także przedstawi szacowane oszczędności, które możesz osiągnąć, kupując wystąpienia zarezerwowane.
    
3. **Ustawianie prawidłowego rozmiaru lub zamykanie nie w pełni wykorzystanych maszyn wirtualnych.** 
    Monitoruje użycie maszyn wirtualnych przez 14 dni, a następnie identyfikuje maszyny wirtualne z niskim wykorzystaniem. Maszyny wirtualne, w przypadku których średnie wykorzystanie procesora CPU wynosi 5 procent lub mniej, a użycie sieci to 7 MB lub mniej przez co najmniej cztery dni, są traktowane jako maszyny wirtualne z niskim wykorzystaniem. Próg średniego wykorzystania procesora CPU można dostosować w górę do 20 procent. Identyfikując nie w pełni wykorzystane maszyny wirtualnych, możesz zdecydować się na zmianę ich rozmiaru na mniejszy typ wystąpienia, co pozwali na obniżenie kosztów.

Sprawdźmy, gdzie możesz znaleźć usługę Azure Advisor w portalu. Najpierw zaloguj się do witryny Azure Portal pod adresem [https://portal.azure.com](https://portal.azure.com). Kliknij pozycję **Wszystkie usługi**. W kategorii **Narzędzia do zarządzania** zostanie wyświetlona usługa **Advisor**. Możesz również wpisać ciąg **Advisor** w polu filtru, aby odfiltrować tylko tę usługę. 

Kliknij pozycję Advisor. Nastąpi przeniesienie do pulpitu nawigacyjnego zaleceń usługi Advisor, w którym możesz zobaczyć wszystkie zalecenia dotyczące Twojej subskrypcji. Dla każdej kategorii zaleceń zostanie wyświetlone pole. 

> [!NOTE]
> W usłudze Advisor możesz nie mieć żadnych zaleceń dotyczących kosztów. Może to oznaczać, że oceny nie zostały jeszcze zakończone lub po prostu usługa Advisor nie ma żadnych zaleceń.

![Zalecenia usługi Advisor](../images/advisor-recommendations.png)

Kliknięcie pola **Koszt** spowoduje przeniesienie do szczegółowych zaleceń. W tym obszarze możesz zobaczyć zalecenia przygotowane przez usługę Advisor.

![Zalecenia usługi Advisor dotyczące kosztów](../images/advisor-cost-recommendations.png)

Kliknięcie dowolnego zalecenia spowoduje przeniesienie do szczegółów tego zalecenia. Następnie będzie można wykonać określoną akcję, taką jak zmiana rozmiaru maszyn wirtualnych, w celu ograniczenia wydatków.

![Zalecenie usługi Advisor dotyczące zmiany rozmiary maszyny wirtualnej](../images/advisor-resize-vm.png)

Te zalecenia dotyczą wszystkich miejsc, w których być może nieefektywnie wydajesz pieniądze. To doskonałe miejsce do rozpoczęcia pracy, które można ponownie odwiedzać, aby identyfikować obszary z możliwością zmniejszenia kosztów. W naszym przykładzie mamy szansę zaoszczędzić 700 USD miesięcznie, jeśli zastosujemy się do zaleceń. Te oszczędności są sumowane, więc okresowo przeglądaj zalecenia dotyczące wszystkich czterech obszarów.

## <a name="azure-cost-management"></a>Azure Cost Management

Azure Cost Management to inne bezpłatne, wbudowane narzędzie platformy Azure, które może służyć do uzyskiwania bardziej szczegółowych informacji na temat sposobu wydawania pieniędzy w chmurze. Możesz zobaczyć historyczne podziały usług, w ramach których są wydawane pieniądze, oraz porównanie tych wydatków do ustawionych budżetów. Możesz ustawiać budżety, planować raporty i analizować obszary kosztów.

![Cost Management](../images/cost-management.png)

## <a name="cloudyn"></a>Cloudyn 

Firma Cloudyn, podmiot zależny od firmy Microsoft, umożliwia śledzenie użycia chmury i wydatków na zasoby platformy Azure i innych dostawców rozwiązań w chmurze, w tym Amazon Web Services i Google. Łatwe do zrozumienia raporty pulpitu nawigacyjnego ułatwiają alokację kosztów oraz obsługę przewidywanych kosztów lub obciążeń zwrotnych. Zarządzanie kosztami ułatwia optymalizację wydatków związanych z chmurą przez identyfikowanie niedostatecznie używanych zasobów, którymi można później zarządzać oraz je dostosowywać. Użycie platformy Azure jest bezpłatne. Dostępne są również płatne opcje pomocy technicznej premium oraz wyświetlanie danych z innych chmur. 

![Pulpit nawigacyjny zarządzania firmy Cloudyn](../images/cloudyn-mgt-dash.png)

## <a name="summary"></a>Podsumowanie

Jak widzisz, istnieje kilka narzędzi bezpłatnie dostępnych na platformie Azure, które umożliwiają śledzenie i prognozowanie wydatków związanych z chmurą oraz identyfikowanie, gdzie środowisko może być mało wydajne z perspektywy kosztów. Warto, aby przeglądanie raportów i zaleceń generowanych przez te narzędzia stało się regularną praktyką. Dzięki temu będzie można odblokować oszczędności w całej chmurze. Teraz przyjrzymy się niektórym najlepszym rozwiązaniom zmniejszającym koszty infrastruktury.
