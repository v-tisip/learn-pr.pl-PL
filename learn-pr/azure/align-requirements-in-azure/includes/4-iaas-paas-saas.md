Zasoby obliczeniowe w chmurze są dostarczane za pomocą trzech różnych modeli usług.

- **Infrastruktura jako usługa (IaaS)** zapewnia natychmiast infrastrukturę obliczeniową, którą możesz aprowizować i zarządzać nią za pośrednictwem Internetu.
- **Platforma jako usługa (PaaS)** udostępnia gotowe do użycia środowiska programowania i wdrażania, których możesz użyć do dostarczania własnych usług w chmurze.
- **Oprogramowanie jako usługa (SaaS)** dostarcza aplikacje w Internecie jako usługę internetową.

Podczas wybierania modelu usługi rozważ, który podmiot powinien być odpowiedzialny za zasoby obliczeniowe. Na podstawie swojego scenariusza możesz zdecydować, jaką część wspólnej odpowiedzialności chcesz ponosić.

![Model wspólnej odpowiedzialności](../media/3-shared-responsibility.png)

## <a name="iaas"></a>IaaS

Infrastruktura jako usługa to infrastruktura natychmiastowych obliczeń aprowizowana i zarządzana za pośrednictwem Internetu. Usługa IaaS umożliwia szybkie skalowanie zasobów w celu zaspokojenia wymagań i płacenia tylko za rzeczywiste użycie. Usługa IaaS pozwala uniknąć kosztownego i skomplikowanego kupna własnych serwerów fizycznych i innej infrastruktury centrum danych oraz zarządzania nimi. Każdy zasób jest oferowany jako oddzielny składnik usługi, a zasób jest *wynajmowany* na tak długo, jak długo będzie potrzebny. W rezultacie usługa IaaS jest bardzo elastyczna. Możesz aprowizować wspólną infrastrukturę, taką jak maszyny wirtualne, magazyn, podsieci wirtualne, zapory oraz sieci VPN, w celu skompilowania rozwiązania. Nie musisz zarządzać fizycznymi serwerami i urządzeniami. Odpowiadasz jednak za bezpośrednie konfigurowanie zarządzania i zarządzanie składnikami. Na przykład konfigurowanie zapór, aktualizowanie systemu operacyjnego maszyny wirtualnej, aktualizowanie systemu DBMS i środowisk uruchomieniowych.

### <a name="common-scenarios"></a>Typowe scenariusze 

Załóżmy, że placówka służby zdrowia musi uruchomić specjalną wersję oprogramowania dla komputerów stacjonarnych. Oprogramowanie jest obsługiwane tylko w określonej wersji systemu operacyjnego i wymagany jest tylko jeden użytkownik i licencja. Możesz utworzyć maszynę wirtualną z wymaganym oprogramowaniem. Użytkownik może użyć pulpitu zdalnego w celu nawiązania połączenia z maszyną wirtualną, aby skorzystać z oprogramowania.

Wyobraźmy sobie inny scenariusz. Twoje zespoły programistów potrzebują kilku unikatowych środowisk programistycznych. W ramach cyklu programowania muszą one testować różne wersje produktu. Deweloperzy mogą w razie potrzeby aprowizować środowiska. Jeśli środowisko nie jest już potrzebne, można je łatwo usunąć.

Do niektórych innych typowych scenariuszy należą:

**Hosting witryn internetowych:** jeśli chcesz mieć większą kontrolę nad hostingiem witryny internetowej, użycie usługi IaaS do uruchamiania takich witryn może być lepszym rozwiązaniem niż tradycyjny hosting internetowy.

**Aplikacje internetowe:** usługa IaaS zapewnia całą infrastrukturę do obsługi aplikacji internetowych, w tym magazyn, serwery internetowe i aplikacji oraz zasoby sieciowe. Organizacje mogą szybko wdrażać aplikacje internetowe w usłudze IaaS i łatwo skalować infrastrukturę w górę i w dół, gdy zapotrzebowanie na aplikacje jest nieprzewidywalne.

**Magazyn, kopia zapasowa i odzyskiwanie:** zarządzanie magazynem może być złożone oraz wymagać dużych inwestycji kapitałowych i wykwalifikowanego personelu do zarządzania danymi oraz spełniania wymagań prawnych i dotyczących zgodności. Usługa IaaS może ułatwić obsługę planowania, zarządzania, nieprzewidywalnego zapotrzebowania i stale rosnących potrzeb związanych z magazynem.

**Obliczenia o wysokiej wydajności:** jeśli masz obciążenie wymagające obliczeń o wysokiej wydajności, możesz uruchomić obciążenie w chmurze, unikając ponoszenia początkowych kosztów sprzętu i płacąc tylko za użycie, gdy jest to potrzebne. 

**Analiza danych big data:** jeśli masz duże zestawy danych, które zawierają potencjalnie cenne wzorce, trendy i skojarzenia, usługa IaaS może zapewnić moc obliczeniową umożliwiającą eksplorację zestawów danych, aby zlokalizować wzorce.

### <a name="advantages"></a>Zalety

**Eliminuje wydatki inwestycyjne i zmniejsza koszty bieżące:** usługa IaaS pozwala uniknąć początkowych wydatków związanych z konfigurowaniem lokalnych centrów danych i zarządzaniem nimi, dzięki czemu jest to ekonomiczna opcja dla startupów i firm testujących nowe pomysły. Gdy zdecydujesz się na uruchomienie nowego produktu lub inicjatywy, niezbędna infrastruktura obliczeniowa może być gotowa w ciągu kilku minut lub godzin, a nie dni lub tygodni — a czasami miesięcy — ponieważ tyle może zająć konfigurowanie wewnętrzne.

**Polepsza ciągłość działalności biznesowej i odzyskiwania po awarii:** osiąganie wysokiej dostępności, ciągłości działalności biznesowej i odzyskiwania po awarii jest kosztowne, ponieważ wymaga znacznej ilości technologii oraz personelu. Jednak z właściwą umową dotyczącą poziomu usług (SLA) usługa IaaS może obniżyć ten koszt i zapewnić dostęp do aplikacji i danych w zwykły sposób podczas awarii lub wyłączenia.

**Szybciej reaguje na zmieniające się warunki biznesowe:** usługa IaaS umożliwia szybkie skalowanie w górę zasobów, aby obsłużyć skoki zapotrzebowania na aplikację — na przykład podczas dni wolnych od pracy — a następnie skalowanie zasobów z powrotem w dół, gdy aktywność się zmniejsza, aby oszczędzać pieniądze. Ponieważ nie musisz najpierw konfigurować infrastruktury, zanim zaczniesz tworzyć i dostarczać aplikacje, możesz je szybciej udostępnić użytkownikom za pomocą usługi IaaS.

**Polepsza stabilność, niezawodność i możliwości obsługi:** dzięki usłudze IaaS nie trzeba utrzymywać i uaktualniać oprogramowania i sprzętu ani rozwiązywać problemów ze sprzętem. Mając odpowiednią umowę, dostawca usług gwarantuje, że infrastruktura będzie stabilna i spełni warunki umów SLA.

## <a name="paas"></a>PaaS

Platforma jako usługa to kompletne środowisko programistyczne i wdrożeniowe w chmurze. Za pomocą usługi PaaS możesz tworzyć i wdrażać wszystko — od prostych aplikacji opartych na chmurze po zaawansowane aplikacje dla przedsiębiorstw z obsługą chmury. Zasoby kupujesz od dostawcy usług w chmurze na zasadzie płatności zgodnie z rzeczywistym użyciem i uzyskujesz do nich dostęp za pośrednictwem bezpiecznego połączenia internetowego. Podobnie jak usługa IaaS, usługa PaaS obejmuje taką infrastrukturę, jak serwery, magazyn i sieć. Ponadto obejmuje ona też oprogramowanie pośredniczące, narzędzia programistyczne i inne usługi. Usługa PaaS obsługuje cały cykl życia aplikacji internetowej: tworzenie, testowanie, wdrażanie, zarządzanie i aktualizowanie. Usługa PaaS eliminuje konieczność zarządzania licencjami na oprogramowanie, oprogramowaniem pośredniczącym i infrastrukturą usług. Zarządzasz aplikacjami i usługami, które tworzysz, a całą resztą zajmuje się zwykle dostawca usług w chmurze.

### <a name="common-scenarios"></a>Typowe scenariusze

Załóżmy, że placówka służby zdrowia potrzebuje witryny internetowej, aby opisać produkt. Deweloperzy chcą użyć środowiska PHP. W usłudze PaaS deweloperzy mogą *utworzyć aplikację internetową*. Szczegóły infrastruktury, takie jak tworzenie maszyny wirtualnej, instalowanie serwera internetowego i instalowanie oprogramowania pośredniczącego, zostają natychmiast odseparowane. Nie musisz dbać o to, w ramach jakiego systemu operacyjnego ona działa lub jaki sprzęt fizyczny jest wymagany. Deweloperzy wdrażają pliki witryny internetowej w chmurze i Twoja witryna internetowa jest dostępna w Internecie.

Wyobraźmy sobie inny scenariusz. Twoja firma wymaga bazy danych SQL do obsługi analityków danych w ramach określonego projektu. Nie masz infrastruktury mogącej spełnić te wymagania. Możesz szybko aprowizować program SQL Server w chmurze, który zaspokoi potrzeby projektu. Analitycy danych mogą połączyć się z serwerem. Baza danych programu SQL Server jest udostępniana jako usługa. W związku z tym nie martwisz się o aktualizacje, poprawki zabezpieczeń lub optymalizację fizycznej pamięci masowej dla operacji odczytu i zapisu.

Do niektórych innych typowych scenariuszy należą:

**Architektura deweloperska:** usługa PaaS udostępnia platformę, na której deweloperzy mogą kompilować w celu tworzenia lub dostosowywania aplikacji opartych na chmurze. Podobnie do sposobu tworzenia makr w programie Excel, usługa PaaS pozwala deweloperom tworzyć aplikacje za pomocą wbudowanych składników oprogramowania. Funkcje chmury, takie jak skalowalność, wysoka dostępność i wielodostępność, są już uwzględnione, co zmniejsza ilość kodowania, które muszą wykonać deweloperzy.

**Analityka lub analiza biznesowa:** narzędzia do analizy oferowane jako usługa umożliwiają analizowanie i eksplorowanie danych. Organizacje mogą znaleźć szczegółowe informacje i wzorce w celu przewidywania wyników na potrzeby poprawy prognozowania, decyzji projektowych dotyczących produktu, zwrotów z inwestycji i innych decyzji biznesowych.

### <a name="advantages"></a>Zalety

Dzięki dostarczaniu infrastruktury jako usługi usługa PaaS ma podobne zalety, jak usługa IaaS. Jednak jej dodatkowe funkcje, a w tym oprogramowanie pośredniczące, narzędzia deweloperskie i inne narzędzia biznesowe, zapewniają dodatkowe korzyści:

**Skrócenie czasu projektowania:** narzędzia deweloperskie usługi PaaS mogą skrócić czas projektowania nowych aplikacji. Deweloperzy mogą używać wstępnie zakodowanych składników aplikacji wbudowanych w platformę, takich jak przepływ pracy, usługi katalogowe, funkcje zabezpieczeń i wyszukiwanie. Składniki platformy jako usługi mogą dać zespołowi deweloperów nowe możliwości bez konieczności zatrudniania dodatkowych pracowników dysponujących niezbędnymi umiejętnościami.

**Programowanie dla wielu platform:** niektórzy dostawcy usług oferuje opcje programowania dla wielu platform, takich jak komputer stacjonarny, urządzenia przenośne i przeglądarki, dzięki czemu aplikacje dla wielu platform można tworzyć szybciej i łatwiej.

**Niedrogie korzystanie z zaawansowanych narzędzi:** model płacenia zgodnie z rzeczywistym użyciem umożliwia użytkownikom indywidualnym i organizacjom korzystanie z zaawansowanego oprogramowania deweloperskiego i analizy biznesowej oraz narzędzi analitycznych, na kupno których nie byłoby ich stać.

**Obsługa geograficznie rozproszonych zespołów deweloperów:** ponieważ dostęp do środowiska programistycznego odbywa się przez Internet, zespoły deweloperów mogą współpracować przy projektach nawet wtedy, gdy członkowie zespołu znajdują się w oddalonych lokalizacjach.

**Efektywne zarządzanie cyklem życia aplikacji:** usługa PaaS udostępnia wszystkie możliwości potrzebne do obsługi całego cyklu życia aplikacji internetowej: kompilowanie, testowanie, wdrażanie, zarządzanie i aktualizowanie w obrębie tego samego zintegrowanego środowiska.

## <a name="saas"></a>i SaaS

Oprogramowanie jako usługa umożliwia użytkownikom nawiązywanie połączenia i korzystanie z aplikacji w chmurze za pośrednictwem Internetu. Typowe przykłady to poczta e-mail, kalendarz i narzędzia biurowe, takie jak Microsoft Office 365. Usługa SaaS zapewnia kompletne rozwiązanie programowe kupowane na zasadzie płacenia zgodnie z rzeczywistym użyciem od dostawcy usług w chmurze. *Wynajmujesz* używanie aplikacji dla Twojej organizacji. Twoi użytkownicy łączą się z usługą za pośrednictwem Internetu, zwykle za pomocą przeglądarki internetowej. Cała podstawowa infrastruktura, oprogramowanie pośredniczące, oprogramowanie i dane aplikacji znajdują się w centrum danych dostawcy usług. Dostawca usług zarządza sprzętem i oprogramowaniem, a dzięki odpowiedniej umowie o świadczenie usług zapewnia również dostępność i bezpieczeństwo Twoich danych i aplikacji. Usługa SaaS pozwala Twojej organizacji szybko zacząć korzystać z aplikacji przy minimalnym koszcie wstępnym.

Jeśli była używana usługa internetowej poczty e-mail, taka jak Outlook, Hotmail lub Yahoo! Mail, to już była używana jedna z postaci usługi SaaS. Za pomocą tych usług logujesz się do swojego konta za pośrednictwem Internetu, zwykle w przeglądarce internetowej. Oprogramowanie poczty e-mail znajduje się w sieci dostawcy usług, a wiadomości są również tam przechowywane. Możesz uzyskać dostęp do swojej poczty e-mail i przechowywanych wiadomości z przeglądarki internetowej na dowolnym komputerze lub urządzeniu połączonym z Internetem.

### <a name="common-scenarios"></a>Typowe scenariusze

Wyobraźmy sobie, że placówka opieki zdrowotnej wymaga rozwiązania do zarządzania relacjami z klientami (CRM) dla swojego zespołu sprzedaży. Zespół jest globalny. Dostawca rozwiązania CRM usługi SaaS umożliwia szybkie wdrożenie rozwiązania dla zespołu sprzedaży w Twojej organizacji.

Do użytku w organizacji możesz wypożyczać aplikacje zwiększające produktywność, takie jak poczta e-mail, współpraca i kalendarz, i zaawansowane aplikacje biznesowe, takie jak zarządzanie relacjami z klientami (CRM), planowanie zasobów przedsiębiorstwa (ERP) i zarządzanie dokumentami. Płacisz za korzystanie z tych aplikacji na podstawie subskrypcji lub zgodnie z poziomem użycia.

### <a name="advantages"></a>Zalety

**Uzyskanie dostępu do zaawansowanych aplikacji:** aby udostępnić użytkownikom aplikacje usługi SaaS, nie musisz kupować, instalować, aktualizować ani utrzymywać żadnego sprzętu, oprogramowania pośredniczącego lub oprogramowania. Usługa SaaS powoduje, że nawet zaawansowane aplikacje dla przedsiębiorstw, takie jak ERP czy CRM, są dostępne cenowo dla organizacji, którym brakuje zasobów na to, aby samodzielnie kupić i wdrożyć wymaganą infrastrukturę i oprogramowanie oraz zarządzać nimi.
Płatność wyłącznie za rzeczywiste użycie. Oszczędzasz pieniądze również dlatego, że usługa SaaS automatycznie jest skalowana w górę i w dół zgodnie z poziomem użycia.

**Korzystanie z bezpłatnego oprogramowania klienckiego:** użytkownicy mogą uruchamiać większość aplikacji usługi SaaS bezpośrednio z przeglądarki internetowej bez konieczności pobierania ani instalowania jakiegokolwiek oprogramowania. Nie musisz kupować ani wdrażać oprogramowania klienckiego dla użytkowników.

**Łatwe mobilizowanie pracowników:** użytkownicy mogą uzyskiwać dostęp do danych i aplikacji usługi SaaS z dowolnego komputera lub urządzenia przenośnego połączonego z Internetem. Dostawca usług koncentruje się na dostarczaniu usług do urządzeń.

**Dostęp do danych aplikacji z dowolnego miejsca:** dzięki danym przechowywanym w chmurze użytkownicy mogą uzyskiwać dostęp do swoich informacji z dowolnego komputera lub urządzenia przenośnego połączonego z Internetem. A gdy dane aplikacji są przechowywane w chmurze, żadne dane nie zostaną utracone w przypadku awarii komputera lub urządzenia użytkownika.