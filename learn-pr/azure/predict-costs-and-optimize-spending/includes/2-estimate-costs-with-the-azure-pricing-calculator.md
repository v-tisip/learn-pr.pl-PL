Wyobraź sobie, że zwrócono się do Ciebie o utworzenie systemu na platformie Azure i poproszono o oszacowanie jego kosztów operacyjnych dla okresu najbliższych 12 miesięcy. Wiesz już, że cennik platformy Azure jest w pełni przezroczysty i że opłaty są naliczane miesięcznie tylko za usługi, których używasz. Jak możesz wykonać to oszacowanie bez wdrażania i uruchamiania usług ani ręcznego wyceniania każdej usługi na podstawie cenników usług platformy Azure? 

## <a name="introducing-the-azure-pricing-calculator"></a>Wprowadzenie do kalkulatora cen platformy Azure

Aby ułatwić klientom opracowywanie oszacowań, firma Microsoft stworzyła **kalkulator cen platformy Azure**. Kalkulator cen platformy Azure to bezpłatne narzędzie internetowe, która pozwala na podanie usług platformy Azure oraz zmodyfikowanie ich właściwości i opcji. Wyświetla on koszty dla poszczególnych usług i łączny koszt całego oszacowania.

W innym oknie lub na innej karcie przeglądarki przejdź do [kalkulatora cen platformy Azure](https://azure.microsoft.com/pricing/calculator/). Na stronie kalkulatora cen są wyświetlone trzy karty:

1. **Produkty.** Na tej karcie wykonasz większość działań. Ta karta zawiera listę wszystkich usług platformy Azure. Umożliwia również dodawanie i usuwanie usług w celu sformułowania szacowania.
2. **Szacunki.** Ta karta zawiera wszystkie zapisane wcześniej oszacowania. Za chwilę przejdziemy przez ten proces.
3. **Często zadawane pytania.** Zgodnie ze swoją nazwą, ta karta zawiera odpowiedzi na niektóre często zadawane pytania.

Zacznijmy od karty **Produkty**. Zobaczysz pełną listę kategorii usług wzdłuż lewej strony. Kliknięcie dowolnej kategorii spowoduje wyświetlenie usług w tej kategorii. Dostępne jest też pole wyszukiwania, które umożliwia wyszukanie usługi we wszystkich usługach. Kliknięcie usługi spowoduje dodanie tej usługi do oszacowania. Możesz dodać tylko jedną usługę lub tyle usług, ile potrzebujesz, w tym wiele razy tę samą usługę (na przykład wiele maszyn wirtualnych). 

Po dodaniu usług chcesz poznać ich wycenę. Przewijając stronę w dół, możesz wyświetlić dostosowywalne szczegóły dla usługi, które dotyczą ceny. Na przykład dla maszyn wirtualnych możesz wybrać szczegóły takie jak region, system operacyjny i rozmiar wystąpienia — wszystkie z nich mają wpływ na cenę maszyny wirtualnej. Zobaczysz sumę częściową dla usługi. Przewijając dalej w dół, możesz zobaczyć pełną sumę łączną dla wszystkich usług objętych oszacowaniem. Razem z sumą łączną są wyświetlane przyciski pozwalające na wyeksportowanie, zapisanie i udostępnienie oszacowania.

## <a name="estimate-a-solution"></a>Szacowanie rozwiązania

Zgodnie z naszym oryginalnym scenariuszem wyobraźmy sobie, że system będzie pracować na dwóch maszynach wirtualnych platformy Azure i łączyć się z wystąpieniem usługi Azure SQL Database. Chcemy też mieć zainstalowaną zaporę w 7. warstwie w celu zapewnienia, że dysponujemy następującymi rozszerzonymi możliwościami równoważenia obciążenia:

![Diagram architektury systemu](../images/estimate-costs-architecture.png)

Możemy użyć kalkulatora cen platformy Azure, aby określić koszt rozwiązania i wyeksportować oszacowanie w celu jego udostępnienia zespołowi.

> [!NOTE]
> Upewnij się, że kalkulator jest pusty i oszacowanie nie zawiera żadnych elementów. Jeśli oszacowanie nie jest puste, kliknij ikonę kosza na śmieci dla każdego elementu, aby je zresetować.

W kalkulatorze cen platformy Azure na karcie **Produkty** dodaj następujące usługi do oszacowania, klikając je:

- Maszyny wirtualne
- Azure SQL Database
- Application Gateway

Szczegóły dla każdej z nich możemy skonfigurować na karcie **Szacunki**, aby uzyskać pewne oszacowanie kosztów. Użyj regionu **Zachodnie stany USA** dla wszystkich zasobów.

* **Maszyny wirtualne.** To jest aplikacja platformy ASP.NET, dlatego należy użyć maszyny wirtualnej z **systemem operacyjnym Windows**. Ta aplikacja nie wymaga ogromnej ilości mocy obliczeniowej, dlatego wybierz rozmiar wystąpienia **D2v3**. Będziemy potrzebować dwóch maszyn wirtualnych pracujących cały czas (730 godzin/miesiąc). Dla tych maszyn wirtualnych użyjemy magazynu SDD w warstwie Premium. Dla każdej maszyny wirtualnej będzie potrzebny jeden dysk o rozmiarze **E10** — łącznie dwa dyski. 

* **SQL Database.** Jako bazę danych aprowizujemy **pojedynczą bazę danych** przy użyciu **modelu rdzenia wirtualnego**. Chcemy mieć bazę danych ogólnego przeznaczenia 4. generacji z 4 rdzeniami wirtualnymi. Będą potrzebne 32 GB miejsca w magazynie i średnio będziemy przechowywać w magazynie 16 GB. Nasze zasady przechowywania to 8 tygodni, 12 miesięcy i 5 lat. 

* **Application Gateway.** Dla usługi Application Gateway użyjemy warstwy zapory aplikacji internetowej, aby zapewnić ochronę naszego środowiska. Będziemy kontynuować przy użyciu tylko dwóch wystąpień i średniego rozmiaru, ponieważ nasze obciążenie nie będzie duże. Oczekiwana ilość przetwarzanych danych to 1 TB na miesiąc.

Patrząc na oszacowanie, należy zwrócić uwagę na sumaryczny koszt każdej usługi i pełny koszt łączny całego oszacowania. W tym przypadku oszacowanie powinno wynosić w przybliżeniu **1400,00 USD miesięcznie**. Opcje możesz wypróbować, zmieniając ich wartości i obserwując, jak oszacowanie rośnie i maleje.

## <a name="share-and-save-your-estimate"></a>Udostępnianie i zapisywanie oszacowania

Teraz mamy oszacowanie dla naszego rozwiązania. Można zapisać to oszacowanie, aby wrócić do niego później i wprowadzić zmiany w razie potrzeby, wyeksportować je do programu Excel w celu dalszej analizy i udostępnić je za pomocą adresu URL. 

Aby wyeksportować oszacowanie, kliknij pozycję `Export` w dolnej części oszacowania. Spowoduje to pobranie oszacowania w formacie programu Excel (**xlsx**) obejmującego wszystkie usługi dodane do oszacowania.

Możemy udostępnić arkusz kalkulacyjny programu Excel lub kliknąć przycisk `Share` w kalkulatorze. W ten sposób uzyskuje się adres URL, który umożliwia udostępnienia tego oszacowania. Będzie ono dostępne dla każdej osoby mającej ten link, co ułatwia udostępnienie oszacowania zespołowi.

Jeśli do logowania użyto konta platformy Azure, możesz zapisać oszacowanie, aby wrócić do niego później. Przejdź dalej i kliknij przycisk **Zapisz**. Jeśli wykonano logowanie, powinno zostać wyświetlone powiadomienie o zapisaniu oszacowania. Jeśli nie wykonano logowania, zostanie wyświetlony monit o zalogowanie w celu zapisania oszacowania. Po zapisaniu oszacowania przewiń stronę na samą górę i wybierz kartę **Szacunki**. Zobaczysz tam oszacowanie. Następnie możesz je wybrać w celu wyświetlenia lub usunąć, jeśli nie jest już potrzebne.

## <a name="summary"></a>Podsumowanie

Określiliśmy szacowany koszt zestawu usług platformy Azure bez wydawania żadnych pieniędzy. Nie utworzyliśmy niczego, a mamy oszacowanie, które można dowolnie udostępniać, bardziej szczegółowo analizować lub modyfikować w przyszłości. Tej metody można użyć nie tylko do tworzenia oszacowań dla systemów, w przypadku których są znane konkretne usługi planowane do użycia, lecz także do porównywania wpływu różnych usług na ogólny koszt. Na przykład porównywania programu Microsoft SQL Server na maszynie wirtualnej z usługą Azure SQL Database. Teraz dowiedzmy się, jak możemy przeanalizować koszty usług, które są już wdrożone.