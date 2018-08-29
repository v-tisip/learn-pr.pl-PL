Załóżmy, że potrzebujesz narzędzia do administrowania zasobami platformy Azure, których używasz podczas testowania systemu do zarządzania relacjami z klientami (CRM). Najważniejsze operacje, które musisz w tym celu wykonywać, to: tworzenie grup zasobów i aprowizowanie maszyn wirtualnych.

Potrzebujesz rozwiązania, które będzie łatwe w obsłudze dla administratorów, ale wystarczająco zaawansowane, aby umożliwić zautomatyzowanie instalacji i konfiguracji wielu maszyn wirtualnych lub utworzenie pełnego środowiska aplikacji za pomocą skryptu. Dostępnych jest wiele narzędzi, ale potrzebujesz takiego, które będzie optymalnie dostosowane do umiejętności Twojego zespołu i do wykonywanych zadań.

## <a name="what-tools-are-available"></a>Jakie narzędzia są dostępne?
Na platformie Azure są dostępne trzy narzędzia administracyjne: 

1. Azure Portal 
2. Interfejs wiersza polecenia platformy Azure
3. Azure PowerShell

Wszystkie te narzędzia oferują podobny zakres kontroli — jeśli możesz wykonać określone zadanie za pomocą jednego z nich, prawdopodobnie umożliwiają to także oba pozostałe. Wszystkie trzy narzędzia są międzyplatformowe: działają w systemach Windows, macOS i Linux. Różnice między nimi dotyczą składni, wymagań związanych z konfiguracją oraz możliwości automatyzacji.

W tym artykule opisano poszczególne opcje i przedstawiono wskazówki dotyczące wyboru najlepszej z nich. 

## <a name="what-is-the-azure-portal"></a>Co to jest Azure Portal?
Azure Portal to witryna internetowa umożliwiająca tworzenie, konfigurowanie i modyfikowanie zasobów w ramach subskrypcji platformy Azure. Oferuje graficzny interfejs użytkownika umożliwiający łatwe znajdowanie potrzebnych zasobów i wprowadzanie wszelkich wymaganych zmian. Udostępnia też kreatory i etykietki narzędzi, które przeprowadzą Cię przez proces wykonywania złożonych zadań administracyjnych.

Portal nie oferuje jednak żadnego sposobu automatyzowania powtarzających się zadań. Na przykład aby skonfigurować 15 maszyn wirtualnych, trzeba utworzyć te maszyny po kolei, wykonując wszystkie kroki kreatora dla każdej z nich. Wykonywanie w ten sposób złożonych zadań może być czasochłonne i wiąże się z ryzykiem popełnienia błędów. 

## <a name="what-is-the-azure-cli"></a>Co to jest interfejs wiersza polecenia platformy Azure?
Interfejs wiersza polecenia platformy Azure to międzyplatformowy program wiersza polecenia służący do łączenia się z platformą Azure i wykonywania poleceń administracyjnych względem zasobów platformy Azure. Aby na przykład utworzyć maszynę wirtualną, możesz użyć polecenia podobnego do następującego:

```bash
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

Interfejs wiersza polecenia platformy Azure jest dostępny na dwa sposoby: w przeglądarce, za pośrednictwem usługi Azure Cloud Shell, lub w aplikacji lokalnej dla systemu Linux, macOS lub Windows. W obu przypadkach interfejsu można używać interaktywnie lub z wykorzystaniem skryptów. W celu korzystania z niego w trybie interaktywnym najpierw uruchom powłokę, taką jak `cmd.exe` w systemie Windows albo Bash w systemie Linux lub macOS, a następnie wydaj polecenie w wierszu polecenia powłoki. Aby zautomatyzować powtarzalne zadania, złóż polecenia w skrypt powłoki przy użyciu składni skryptu wybranej powłoki, a następnie wykonaj skrypt.

## <a name="what-is-azure-powershell"></a>Co to jest Azure PowerShell?
Azure PowerShell to moduł dodawany do programu Windows PowerShell lub PowerShell Core, umożliwiający nawiązanie połączenia z subskrypcją platformy Azure i zarządzanie jej zasobami. Moduł Azure PowerShell wymaga programu PowerShell. Program PowerShell zapewnia takie usługi jak okno powłoki, analizowanie poleceń itp. Moduł Azure PowerShell dodaje polecenia specyficzne dla platformy Azure.

Na przykład moduł Azure PowerShell dodaje polecenie **New-AzureRmVM**, tworzące maszynę wirtualną w ramach subskrypcji platformy Azure. Aby go użyć, należy uruchomić aplikację PowerShell, a następnie wprowadzić polecenie podobne do następującego:

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Moduł Azure PowerShell jest dostępny na dwa sposoby: w przeglądarce, za pośrednictwem usługi Azure Cloud Shell, lub w aplikacji lokalnej dla systemu Linux, macOS lub Windows. W obu przypadkach masz dwa tryby do wyboru. Możesz używać modułu w trybie interaktywnym, w którym ręcznie wprowadzasz kolejne polecenia, lub w trybie skryptowym, umożliwiającym wykonywanie skryptów złożonych z wielu poleceń.

## <a name="how-to-choose-an-administrative-tool"></a>Jak wybrać właściwe narzędzie administracyjne
Witryna Azure Portal, interfejs wiersza polecenia platformy Azure oraz moduł Azure PowerShell są niemal identyczne pod względem obiektów platformy Azure, którymi można za ich pomocą administrować, oraz konfiguracji, które można za ich pomocą tworzyć. Wszystkie te narzędzia są też dostępne na różnych platformach. To oznacza, że dokonując wyboru, zazwyczaj bierze się pod uwagę inne czynniki:

- **Automatyzacja**: czy potrzebujesz możliwości automatyzacji zestawu złożonych lub powtarzalnych zadań? Umożliwia to moduł Azure PowerShell oraz interfejs wiersza polecenia platformy Azure, ale nie witryna Azure Portal.

- **Szybkość nauki**: czy potrzebujesz możliwości szybkiego wykonywania zadań bez konieczności uczenia się nowych poleceń i składni? Witryna Azure Portal nie wymaga znajomości składni ani poleceń. Korzystając z modułu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure, musisz znać dokładną składnie każdego używanego polecenia.

- **Umiejętności zespołu**: czy Twój zespół ma już wcześniej zdobytą wiedzę? Być może członkowie zespołu używali już na przykład programu PowerShell do wykonywania zadań administracyjnych w systemie Windows. W takim przypadku szybko przyswoją sobie sposób korzystania z modułu Azure PowerShell.

## <a name="example"></a>Przykład
Pamiętaj, że wybierasz narzędzie administracyjne do tworzenia środowisk testowych dla aplikacji CRM. Administratorzy będą musieli wykonywać dwa konkretne zadania na platformie Azure:

1. Utworzenie jednej grupy zasobów dla każdej kategorii testów (jednostkowych, integracji i akceptacyjnych).
2. Tworzenie wielu maszyn wirtualnych w każdej grupie zasobów przed każdą kolejną rundą testów.

Witryna Azure Portal to odpowiednie narzędzie do tworzenia grup zasobów. Jest to zadanie jednorazowe i nie wymaga użycia skryptów.

Trudniejszy będzie wybór właściwego narzędzia do tworzenia maszyn wirtualnych. Trzeba będzie to robić wielokrotnie, prawdopodobnie kilka razy w tygodniu, tworząc za każdym razem wiele maszyn wirtualnych. Zatem właściwym rozwiązaniem będzie automatyzacja tego zadania, której nie umożliwia witryna Azure Portal. W takim przypadku potrzebujesz modułu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure. Jeśli członkowie Twojego zespołu potrafią już korzystać z programu PowerShell, prawdopodobnie najlepszym wyborem będzie moduł Azure PowerShell. Moduł Azure PowerShell jest dostępny w systemach operacyjnych używanych przez administratorów i obsługuje automatyzację, a Twój zespół powinien szybko nauczyć się korzystania z niego.

## <a name="summary"></a>Podsumowanie
Dla większości administratorów pierwszy kontakt z platformą Azure ma miejsce w witrynie Azure Portal. To doskonałe rozwiązanie na początek, ponieważ oferuje przejrzysty i uporządkowany interfejs graficzny, ale możliwości automatyzacji są tu ograniczone. Jeśli potrzebujesz automatyzacji, platforma Azure oferuje dwie opcje: moduł Azure PowerShell dla administratorów mających doświadczenie z programem PowerShell oraz interfejs wiersza polecenia platformy Azure dla pozostałych użytkowników.

W praktyce firmy wykonują zarówno zadania jednorazowe, jak i powtarzalne. Dlatego często korzystają zarówno z portalu, jak i z rozwiązania skryptowego. W naszym przykładzie dotyczącym systemu CRM do tworzenia grup zasobów odpowiedni będzie portal, a tworzenie maszyn wirtualnych należy zautomatyzować za pomocą programu PowerShell.

Pozostała część tego modułu dotyczy instalowania i używania aplikacji Azure PowerShell.