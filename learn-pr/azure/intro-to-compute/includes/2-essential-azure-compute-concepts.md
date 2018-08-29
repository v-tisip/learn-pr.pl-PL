Twój zespół badawczy musi wykonać zadanie przetwarzania danych wymagające dużej mocy obliczeniowej, ale nie ma sprzętu potrzebnego do wykonania tego zadania. Postanawia użyć platformy Azure do analizy danych.

## <a name="what-is-azure-compute"></a>Czym jest usługa Azure Compute?
Azure Compute to usługa udostępniająca zasoby obliczeniowe na żądanie dla aplikacji w chmurze. Zapewnia zasoby obliczeniowe, takie jak procesory wielordzeniowe i superkomputery, w ramach maszyn wirtualnych i kontenerów. Umożliwia również przetwarzanie bezserwerowe, co pozwala na uruchamianie aplikacji bez konieczności konfigurowania infrastruktury. Zasoby są udostępniane na żądanie i zazwyczaj mogą być tworzone w ciągu kilku minut lub nawet sekund. Opłaty są naliczane tylko za wykorzystane zasoby i tylko za okres, w którym były używane.

Istnieją trzy najpopularniejsze techniki wykonywania obliczeń na platformie Azure:
1. Maszyny wirtualne
1. Containers
1. Przetwarzanie bezserwerowe

## <a name="what-are-virtual-machines"></a>Co to są maszyny wirtualne?

**Maszyna wirtualna**  to oprogramowanie emulujące fizyczny komputer. Zawiera wirtualny procesor, pamięć, magazyn oraz zasoby sieciowe. Hostuje system operacyjny i można na niej instalować i uruchamiać oprogramowanie, tak jak na komputerze fizycznym. Korzystając z klienta pulpitu zdalnego, możesz używać maszyny wirtualnej i kontrolować ją tak samo, jak siedząc przed fizycznym terminalem.

### <a name="virtual-machines-in-azure"></a>Maszyny wirtualne na platformie Azure

Na platformie Azure można tworzyć i hostować maszyny wirtualne. Nowe maszyny wirtualne są zwykle tworzone i aprowizowane w ciągu kilku minut po wybraniu wstępnie skonfigurowanego obrazu maszyny wirtualnej.

Wybranie obrazu to jedna z najważniejszych decyzji jakie należy podjąć podczas tworzenia maszyny wirtualnej. Obraz to szablon używany do utworzenia maszyny wirtualnej. Te szablony zawierają już system operacyjny i często inne oprogramowanie, na przykład narzędzia deweloperskie lub środowiska hostingu internetowego.

## <a name="what-are-containers"></a>Co to są kontenery?

Kontenery to środowisko wirtualizacji, jednak w przeciwieństwie do maszyn wirtualnych, nie obejmują one systemu operacyjnego. Zamiast tego zawierają odwołanie do systemu operacyjnego środowiska hosta, w którym jest uruchomiony kontener. Jeśli na przykład pięć kontenerów jest uruchomionych na serwerze z konkretnym jądrem systemu Linux, wszystkie pięć kontenerów jest uruchomionych na tym samym jądrze. 

Kontenery zwykle zawierają utworzoną przez Ciebie aplikację oraz wszystkie biblioteki konieczne do uruchomienia tej aplikacji na jądrze środowiska hosta. 

Kontenery z założenia są proste i zaprojektowane tak, aby można je było dynamicznie tworzyć, skalować w poziomie i zatrzymywać oraz dostosowywać do zmian środowiska i zapotrzebowania.

Zaletą korzystania z kontenerów jest możliwość uruchomienia wielu izolowanych aplikacji na jednej maszynie wirtualnej. Ponieważ kontenery same w sobie są zabezpieczone i izolowane, nie trzeba używać oddzielnych maszyn wirtualnych do obsługi oddzielnych obciążeń.

Platforma Azure obsługuje kontenery platformy Docker i umożliwia obsługę tych kontenerów na kilka sposobów. Kontenerami można zarządzać ręcznie lub za pomocą usług platformy Azure, takich jak Azure Kubernetes Service.

### <a name="what-is-serverless-computing"></a>Co to jest przetwarzanie bezserwerowe?

Przetwarzanie bezserwerowe to środowisko wykonywania hostowane w chmurze, w którym uruchamiany jest kod, podczas gdy bazowe środowisko hostowania jest całkowicie oddzielone. Po utworzeniu wystąpienia usługi możesz dodać swój kod — nie ma potrzeby (ani nawet możliwości) konfigurowania lub utrzymywania infrastruktury.

Możesz skonfigurować aplikacje bezserwerowe, aby reagowały na zdarzenia. Może być to punkt końcowy usługi REST, czasomierz lub komunikat otrzymany od innej usługi platformy Azure. Bezserwerowa aplikacja jest uruchamiana po wyzwoleniu przez zdarzenie. 

Infrastruktura nie jest Twoim problemem. Skalowanie i wydajność są obsługiwane automatycznie, a opłaty są naliczane wyłącznie za użyte zasoby. Nie ma nawet potrzeby rezerwowania pojemności.

Na platformie Azure są dostępne dwie implementacje przetwarzania bezserwerowego: usługa **Azure Functions**, która może wykonywać kod w niemal każdym nowoczesnym języku, oraz usługa **Azure Logic Apps**, która umożliwia wykonywanie logiki wyzwalanej przez usługi platformy Azure bez konieczności pisania kodu.
