Złożone lub powtarzające się zadania często zajmują większość czasu przeznaczanego na administrację. Organizacje wolą automatyzować te zadania w celu zmniejszenia kosztów i uniknięcia błędów.

Jest to ważne w przykładowej firmie zajmującej się zarządzaniem relacjami z klientami (CRM, Customer Relationship Management). W tym przykładzie oprogramowanie jest testowane na wielu maszynach wirtualnych z systemem Linux, które są nieustannie usuwane i ponownie tworzone. W celu zautomatyzowania procesu tworzenia maszyn wirtualnych chcesz użyć skryptu programu PowerShell.

Poza wykonywaniem podstawowej operacji tworzenia maszyny wirtualnej Twój skrypt powinien spełniać jeszcze kilka dodatkowych warunków. 
- Będziesz Tworzyć wiele maszyn wirtualnych, więc proces tworzenia powinien być wykonywany w pętli.
- Maszyny wirtualne będą tworzone w trzech różnych grupach zasobów, dlatego nazwa grupy zasobów powinna być przekazywana do skryptu w postaci parametru.

W tej sekcji zobaczysz, jak napisać i wykonać skrypt programu Azure PowerShell spełniający te wymagania.

## <a name="what-is-a-powershell-script"></a>Co to jest skrypt programu PowerShell?
Skrypt programu PowerShell jest plikiem tekstowym zawierającym polecenia i konstrukcje kontrolne. Polecenia są wywołaniami poleceń cmdlet. Konstrukcje kontrolne to funkcje programowania, takie jak pętle, zmienne, parametry, komentarze itp. obsługiwane przez program PowerShell.

Nazwy plików skryptów programu PowerShell mają rozszerzenie **ps1**. Te pliki można tworzyć i zapisywać za pomocą dowolnego edytora tekstów. 

> [!TIP]
> Jeśli piszesz skrypty programu PowerShell w systemie Windows, możesz użyć środowiska Windows PowerShell Integrated Scripting Environment (ISE). Ten edytor udostępnia przydatne funkcje, takie jak kolorowanie składni oraz lista dostępnych poleceń cmdlet.
>
>![Środowisko Windows PowerShell ISE](../media-drafts/7-windows-powershell-ise-screenshot.png)

Po napisaniu skryptu wykonaj go w wierszu polecenia programu PowerShell, przekazując nazwę pliku poprzedzoną znakiem kropki i ukośnika odwrotnego:

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a>Techniki programu PowerShell
Program PowerShell ma wiele funkcji, które można znaleźć w typowych językach programowania. Można definiować zmienne, używać gałęzi i pętli, przechwytywać parametry wiersza polecenia, pisać funkcje, dodawać komentarze i tak dalej. W naszym skrypcie użyjemy trzech funkcji: zmiennych, pętli i parametrów.

### <a name="variables"></a>Zmienne
Program PowerShell obsługuje zmienne. Użyj znaku **$**, aby zadeklarować zmienną, i znaku **=**, aby przypisać do niej wartość. Na przykład:

```powershell
$loc = "East US"
$iterations = 3
```

Zmienne mogą przechowywać obiekty. Na przykład następująca definicja ustawia zmienną **adminCredential** na obiekt zwrócony przez polecenie cmdlet **Get-Credential**.

```powershell
$adminCredential = Get-Credential
```

Aby uzyskać wartość przechowywaną w zmiennej, użyj prefiksu **$** i nazwy zmiennej, jak pokazano poniżej: 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a>Pętle
Program PowerShell obsługuje kilka pętli: **For**, **Do...While**, **For...Each** itd. Pętla **For** nadaje się najlepiej do naszych potrzeb, ponieważ będziemy wykonywać polecenie cmdlet określoną liczbę razy.

Poniżej pokazano podstawową składnię; przykład jest uruchamiany dla dwóch iteracji i za każdym razem jest drukowana wartość zmiennej **i**. Operatory porównań są zapisywane w następujący sposób: **-lt** — „mniejsze niż”, **-le** — „mniejsze niż lub równe”, **eq** — „równe”, **ne** — „różne od” itd.

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a>Parametry
Podczas wykonywania skryptu można przekazywać argumenty w wierszu polecenia. Aby ułatwić wyodrębnianie wartości przez skrypt, można nadać nazwy poszczególnym parametrom. Na przykład:

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

Wewnątrz skryptu wartości są przechwytywane do zmiennych. W tym przykładzie parametry są dopasowywane według nazwy:

```powershell
param([string]$location, [int]$size)
```

Możesz pominąć nazwy z wiersza polecenia. Na przykład:

```powershell
.\setupEnvironment.ps1 5 "East US"
```

Jeśli parametry nie mają nazw, ich dopasowywanie wewnątrz skryptu odbywa się na podstawie ich pozycji:

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a>Jak utworzyć maszynę wirtualną z systemem Linux
Program Azure PowerShell udostępnia polecenie cmdlet **New-AzureRmVm** umożliwiające utworzenie maszyny wirtualnej. To polecenie cmdlet ma wiele parametrów umożliwiających obsługę dużej liczby ustawień konfiguracji maszyn wirtualnych. Większość parametrów ma odpowiednie wartości domyślne, dlatego wystarczy określić tylko pięć elementów:
- **ResourceGroupName**: grupa zasobów, w której zostanie umieszczona nowa maszyna wirtualna.
- **Name**: nazwa maszyny wirtualnej na platformie Azure.
- **Location**: lokalizacja geograficzna, w której będzie aprowizowana maszyna wirtualna.
- **Credential**: obiekt zawierający nazwę użytkownika i hasło dla konta administratora maszyny wirtualnej. W celu wyświetlenia prośby o podanie nazwy użytkownika i hasła użyjemy polecenia cmdlet **Get-Credential**. Polecenie **Get-Credential** pakuje nazwę użytkownika i hasło w obiekt poświadczeń, który jest zwracany w wyniku działania tego polecenia.
- **Image**: tożsamość systemu operacyjnego do użycia dla maszyny wirtualnej. Użyjemy tutaj wartości „UbuntuLTS”.

Poniżej przedstawiono składnię tego polecenia cmdlet:

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a>Podsumowanie
Kombinacja funkcji programów PowerShell i Azure PowerShell zapewnia wszystkie narzędzia potrzebne do automatyzacji platformy Azure. W naszym przykładzie firmy CRM będziemy mogli tworzyć wiele maszyn wirtualnych z systemem Linux, korzystając z parametru w celu utrzymania ogólnej postaci skryptu i pętli w celu uniknięcia powtarzania kodu. Oznacza to, że wcześniej złożona operacja teraz może zostać wykonana w jednym kroku.