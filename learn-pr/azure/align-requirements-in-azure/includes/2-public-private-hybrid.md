Wyobraź sobie, że pracujesz w placówce służby zdrowia. Jest wyposażona w starsze systemy i systemy biznesowe, ale są plany, aby wyposażyć ją w nowe systemy. Doszły do Ciebie słuchy, że korzystanie z przetwarzania w chmurze ma swoje zalety. W jaki sposób wybrać najlepszy model wdrożenia różnych rozwiązań — chmury publicznej, prywatnej i hybrydowej?

## <a name="what-is-cloud-computing"></a>Co to jest przetwarzanie w chmurze?

Przetwarzanie w chmurze oznacza aprowizowanie usług i aplikacji na żądanie przez Internet. Serwery, aplikacje, dane i inne zasoby są dostarczane jako usługa. 

Szczegóły dotyczące tych usług są odseparowane od użytkownika. Można szybko aprowizować zasoby obliczeniowe i korzystać z usług, a wymagania dotyczące zarządzania są minimalne. Nie należy myśleć o przetwarzaniu w chmurze jak o centrum danych dostępnym przez Internet. W ramach przetwarzania w chmurze wykorzystuje się wirtualizację, sprzęt masowy oraz zautomatyzowane procesy, aby dostarczyć użytkownikom środowisko samoobsługowe, podobne jak ma to miejsce w przypadku dostawców mediów. 

Istnieją trzy modele wdrożenia przetwarzania w chmurze: chmura publiczna, chmura prywatna i chmura hybrydowa.

![Modele wdrożenia chmury](../media/2-cloud-deployment.png)

## <a name="public-cloud"></a>Chmura publiczna

Chmury publiczne to najpopularniejszy sposób wdrażania przetwarzania w chmurze. Usługi są oferowane za pośrednictwem publicznego Internetu i dostępne dla każdego, kto chce je zakupić. Zasoby w chmurze, takie jak serwery i magazyny, są własnością firmy będącej dostawcą usług w chmurze i są przez nią obsługiwane oraz dostarczane przez Internet. Usługi mogą być bezpłatne lub sprzedawane na żądanie, co umożliwia klientom płacenie tylko za użycie cykli procesora CPU, magazynu lub przepustowości. Przykładem chmury publicznej jest platforma Microsoft Azure. 

Wyobraźmy sobie, że w Twojej placówce służby zdrowia potrzebna jest witryna internetowa do rejestracji. Witryna musi być skalowana i dostosowywać się do okresów wzmożonego zapotrzebowania w ciągu roku. Klienci uzyskują dostęp do witryny z różnych lokalizacji na świecie. Możesz użyć chmury publicznej i automatycznie skalować usługi w górę, aby sprostać wymaganiom w czasie okresów bardziej intensywnej rejestracji. Gdy ruch w witrynie jest niski, możesz skalować usługi w dół, aby zmniejszyć koszty. Twoja witryna reaguje na wyższy popyt, a Ty płacisz za więcej zasobów tylko wtedy, gdy są Ci potrzebne. Możesz również wdrożyć witrynę w wielu regionach geograficznych, aby zwiększyć jej niezawodność i skrócić czas odpowiedzi.

Podczas prac nad witryną deweloperzy tworzą wiele środowisk deweloperskich, aby przyspieszyć ten proces. Deweloperzy mogą korzystać z chmury publicznej, aby szybko aprowizować maszyny wirtualne dla środowisk działających w piaskownicy w celu utworzenia rozwiązania. Gdy środowisko nie jest już potrzebne deweloperom, usuwają je.

### <a name="why-public-cloud"></a>Dlaczego chmura publiczna?

Chmury publiczne można wdrażać szybciej niż infrastrukturę lokalną, a ponadto ich platformy oferują niemal nieograniczone możliwości skalowania. Każdy pracownik firmy może używać tej samej aplikacji w biurze lub oddziale, korzystając z dowolnego urządzenia z dostępem do Internetu. 

W jakich sytuacjach korzystać z chmury publicznej — przykłady:

- **Użycie usługi na żądanie według potrzeb lub na podstawie subskrypcji:** model usługi na żądanie lub model subskrypcyjny umożliwia naliczanie opłat tylko za używane lub rezerwowane zasoby, takie jak procesor CPU, magazyn i inne.
- **Brak konieczności inwestowania w sprzęt:** nie ma konieczności zakupu sprzętu i infrastruktury aplikacji, a następnie zarządzania nimi i ich utrzymywania. Za zarządzanie systemem i jego utrzymanie odpowiada dostawca usług w chmurze. 
- **Automatyzacja:** możesz szybko aprowizować zasoby infrastruktury przy użyciu portalu internetowego, skryptów lub rozwiązań automatycznych. 
- **Rozproszenie geograficzne:** możesz lokalizować dane w pobliżu miejsc, w których są potrzebne, bez konieczności posiadania wielu własnych centrów danych.
- **Mniej czynności związanych z utrzymaniem sprzętu:** to dostawca usług jest odpowiedzialny za konserwację sprzętu.

## <a name="private-cloud"></a>Chmura prywatna

Chmura prywatna składa się z zasobów obliczeniowych używanych wyłącznie przez wybranych użytkowników z jednej firmy lub organizacji. Może być fizycznie zlokalizowana w lokalnym centrum danych organizacji lub hostowana przez zewnętrznego usługodawcę. Termin „chmura prywatna” nie powinien być traktowany jako nowe określenie dla tradycyjnych lokalnych centrów danych. Chmura prywatna korzysta z lokalnej infrastruktury i usług, aby zapewnić podobne korzyści co chmura publiczna. Dzięki zastosowaniu platformy abstrakcji oferuje usługi *przypominające chmurę*, na przykład klastry usługi Kubernetes lub kompletne środowisko chmury, takie jak Azure Stack. Organizacja jest odpowiedzialna za zakup, konfigurację i utrzymanie sprzętu. Komunikacja pomiędzy systemami odbywa się zwykle w ramach infrastruktury sieci, która należy do firmy i jest przez nią utrzymywana. Jest to na przykład prywatna sieć wewnętrzna lub dedykowane połączenie światłowodowe pomiędzy budynkami.

Wyobraź sobie, że pracujesz w placówce służby zdrowia i masz aplikację, która jest używana w jednym z centrów danych placówki. Środowisko operacyjne nie może zostać zreplikowane w chmurze publicznej. Pojawiło się nowe wymaganie dotyczące uzyskiwania dostępu do danych w innym centrum danych należącym do placówki. Baza danych zawierająca dane musi pozostać w tej drugiej lokacji z uwagi na przepisy. Ten scenariusz dotyczy chmury prywatnej. Masz dwa centra danych należące do Twojej organizacji. Możesz połączyć oba centra danych za pomocą sieci VPN w chmurze publicznej za pośrednictwem Internetu. Nadal jednak będzie to scenariusz użycia chmury prywatnej, ponieważ jest to prywatne rozwiązanie organizacji.

### <a name="why-private-cloud"></a>Dlaczego chmura prywatna?

Chmura prywatna umożliwia organizacji zachowanie większej elastyczności. Organizacja może dostosować środowisko chmury do konkretnych potrzeb biznesowych. Ponieważ zasoby nie są współdzielone, można uzyskać wysoki poziom kontroli i bezpieczeństwa. Ponadto chmury prywatne mogą zapewnić odpowiedni poziom skalowalności i wydajności.

Przykłady tego, w jakich sytuacjach korzystać z chmury prywatnej:

- **Wcześniej istniejące środowisko:** istniejące środowisko operacyjne, które nie może być zreplikowane w chmurze publicznej. Duże inwestycje w sprzęt i pracowników z wiedzą dotyczącą używanych rozwiązań. Duża organizacja może zdecydować się na komodyzację zasobów obliczeniowych.
- **Starsze aplikacje:** starsze aplikacje kluczowe dla biznesu, których nie można łatwo przenieść fizycznie.
- **Niezależność i bezpieczeństwo danych:** granice polityczne lub przepisy prawne mogą decydować o tym, gdzie dane mogą istnieć fizycznie.
- **Zgodność z przepisami/certyfikaty:** zgodność z normami PCI lub HIPAA. Certyfikowane lokalne centrum danych.

## <a name="hybrid-cloud"></a>Chmura hybrydowa

Chmura hybrydowa to środowisko obliczeniowe, które łączy cechy chmury publicznej i prywatnej, umożliwiając współdzielenie pomiędzy nimi danych i aplikacji. Przy zmiennym zapotrzebowaniu na obliczenia i przetwarzanie danych chmura hybrydowa daje firmom możliwość łatwego skalowania swojej lokalnej infrastruktury w górę dzięki użyciu chmury publicznej do obsłużenia zwiększonego zapotrzebowania, bez przekazywania wszystkich swoich danych do centrów danych innych firm. Organizacje zyskują elastyczność i moc obliczeniową chmury publicznej do obsługi podstawowych i niewrażliwych zadań obliczeniowych, jednocześnie mając pewność, że aplikacje i dane kluczowe dla biznesu są bezpiecznie przechowywane lokalnie, za zaporą firmową.

Korzystanie z chmury hybrydowej eliminuje konieczność ponoszenia wysokich nakładów inwestycyjnych w celu obsługi krótkoterminowych wzrostów zapotrzebowania. Oferuje również elastyczność decydowania o tym, które zasoby są przechowywane lokalnie, a które w chmurze. Firmy płacą tylko za te zasoby, z których aktualnie korzystają, i nie muszą kupować, programować ani utrzymywać dodatkowych zasobów i sprzętu, które mogłyby pozostawać bezczynne przez dłuższy czas. Integracja odbywa się zwykle za pośrednictwem bezpiecznej sieci VPN pomiędzy dostawcą chmury, na przykład platformą Azure, a lokalnym centrum danych.

Wyobraź sobie, że pracujesz w placówce służby zdrowia i masz aplikację, dzięki której klienci mogą uzyskać dostęp do swoich informacji zdrowotnych. Prawo wymaga, aby te dane były przechowywane w lokalizacji fizycznej. Witryna dla klientów musi zapewniać krótki czas reakcji, biorąc pod uwagę, że użytkownicy są z całego świata.  Rozwiązaniem może być hostowanie bazy danych w lokalnym centrum danych, a witryny internetowej — w chmurze publicznej. Do nawiązania połączenia pomiędzy lokalnym centrum danych a chmurą publiczną można wykorzystać sieć VPN. W takim scenariuszu używana jest chmura hybrydowa.

### <a name="why-hybrid-cloud"></a>Dlaczego chmura hybrydowa?

Chmura hybrydowa pozwala organizacjom na kontrolowanie i utrzymywanie prywatnej infrastruktury na potrzeby wrażliwych zasobów. Daje również elastyczność wykorzystania dodatkowych zasobów w chmurze publicznej według potrzeb. Dzięki możliwości skalowania w chmurze publicznej płacisz za dodatkową moc obliczeniową tylko wtedy, gdy jest potrzebna. To rozwiązanie może również ułatwić przejście do chmury. Możesz przeprowadzać migrację stopniowo, przenosząc obciążenia etapami.

W jakich sytuacjach korzystać z chmury hybrydowej — przykłady:

- **Istniejące inwestycje w sprzęt:** z przyczyn biznesowych musisz korzystać z istniejącego środowiska operacyjnego i sprzętu.
- **Wymagania prawne:** prawo wymaga, aby dane były przechowywane w lokalizacji fizycznej.
- **Unikatowe środowisko operacyjne:** nie można zreplikować starszego środowiska operacyjnego w chmurze publicznej.
- **Migracja:** rozłożenie w czasie przenoszenia obciążeń do chmury.
