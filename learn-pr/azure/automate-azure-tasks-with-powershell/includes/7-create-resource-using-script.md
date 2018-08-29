<span data-ttu-id="c47b7-101">Złożone lub powtarzające się zadania często zajmują większość czasu przeznaczanego na administrację.</span><span class="sxs-lookup"><span data-stu-id="c47b7-101">Complex or repetitive tasks often take a great deal of administrative time.</span></span> <span data-ttu-id="c47b7-102">Organizacje wolą automatyzować te zadania w celu zmniejszenia kosztów i uniknięcia błędów.</span><span class="sxs-lookup"><span data-stu-id="c47b7-102">Organizations prefer to automate these tasks to reduce costs and avoid errors.</span></span>

<span data-ttu-id="c47b7-103">Jest to ważne w przykładowej firmie zajmującej się zarządzaniem relacjami z klientami (CRM, Customer Relationship Management).</span><span class="sxs-lookup"><span data-stu-id="c47b7-103">This is important in the Customer Relationship Management (CRM) company example.</span></span> <span data-ttu-id="c47b7-104">W tym przykładzie oprogramowanie jest testowane na wielu maszynach wirtualnych z systemem Linux, które są nieustannie usuwane i ponownie tworzone.</span><span class="sxs-lookup"><span data-stu-id="c47b7-104">There, you test your software on multiple Linux Virtual Machines (VMs) that you need to continuously delete and recreate.</span></span> <span data-ttu-id="c47b7-105">W celu zautomatyzowania procesu tworzenia maszyn wirtualnych chcesz użyć skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c47b7-105">You want to use a PowerShell script to automate the creation of the VMs.</span></span>

<span data-ttu-id="c47b7-106">Poza wykonywaniem podstawowej operacji tworzenia maszyny wirtualnej Twój skrypt powinien spełniać jeszcze kilka dodatkowych warunków.</span><span class="sxs-lookup"><span data-stu-id="c47b7-106">Beyond the core operation of creating a VM you have a few additional requirements for your script.</span></span> 
- <span data-ttu-id="c47b7-107">Będziesz Tworzyć wiele maszyn wirtualnych, więc proces tworzenia powinien być wykonywany w pętli.</span><span class="sxs-lookup"><span data-stu-id="c47b7-107">You will create multiple VMs, so you want to put the creation inside a loop</span></span>
- <span data-ttu-id="c47b7-108">Maszyny wirtualne będą tworzone w trzech różnych grupach zasobów, dlatego nazwa grupy zasobów powinna być przekazywana do skryptu w postaci parametru.</span><span class="sxs-lookup"><span data-stu-id="c47b7-108">You need to create VMs in three different resource groups, so the name of the resource group should be passed to the script as a parameter</span></span>

<span data-ttu-id="c47b7-109">W tej sekcji zobaczysz, jak napisać i wykonać skrypt programu Azure PowerShell spełniający te wymagania.</span><span class="sxs-lookup"><span data-stu-id="c47b7-109">In this section, you will see how to write and execute an Azure PowerShell script that meets these requirements.</span></span>

## <a name="what-is-a-powershell-script"></a><span data-ttu-id="c47b7-110">Co to jest skrypt programu PowerShell?</span><span class="sxs-lookup"><span data-stu-id="c47b7-110">What is a PowerShell script?</span></span>
<span data-ttu-id="c47b7-111">Skrypt programu PowerShell jest plikiem tekstowym zawierającym polecenia i konstrukcje kontrolne.</span><span class="sxs-lookup"><span data-stu-id="c47b7-111">A PowerShell script is a text file containing commands and control constructs.</span></span> <span data-ttu-id="c47b7-112">Polecenia są wywołaniami poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c47b7-112">The commands are invocations of cmdlets.</span></span> <span data-ttu-id="c47b7-113">Konstrukcje kontrolne to funkcje programowania, takie jak pętle, zmienne, parametry, komentarze itp. obsługiwane przez program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c47b7-113">The control constructs are programming features like loops, variables, parameters, comments, etc. supplied by PowerShell.</span></span>

<span data-ttu-id="c47b7-114">Nazwy plików skryptów programu PowerShell mają rozszerzenie **ps1**.</span><span class="sxs-lookup"><span data-stu-id="c47b7-114">PowerShell script files have a **.ps1** file extension.</span></span> <span data-ttu-id="c47b7-115">Te pliki można tworzyć i zapisywać za pomocą dowolnego edytora tekstów.</span><span class="sxs-lookup"><span data-stu-id="c47b7-115">You can create and save these files with any text editor.</span></span> 

> [!TIP]
> <span data-ttu-id="c47b7-116">Jeśli piszesz skrypty programu PowerShell w systemie Windows, możesz użyć środowiska Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="c47b7-116">If you’re writing PowerShell scripts under Windows, you can use the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="c47b7-117">Ten edytor udostępnia przydatne funkcje, takie jak kolorowanie składni oraz lista dostępnych poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c47b7-117">This editor provides features such as syntax coloring and a list of available cmdlets.</span></span>
>
>![Środowisko Windows PowerShell ISE](../media-drafts/7-windows-powershell-ise-screenshot.png)

<span data-ttu-id="c47b7-119">Po napisaniu skryptu wykonaj go w wierszu polecenia programu PowerShell, przekazując nazwę pliku poprzedzoną znakiem kropki i ukośnika odwrotnego:</span><span class="sxs-lookup"><span data-stu-id="c47b7-119">Once you have written the script, execute it from the PowerShell command line by passing the name of the file preceded by a dot and a backslash:</span></span>

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a><span data-ttu-id="c47b7-120">Techniki programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c47b7-120">PowerShell techniques</span></span>
<span data-ttu-id="c47b7-121">Program PowerShell ma wiele funkcji, które można znaleźć w typowych językach programowania.</span><span class="sxs-lookup"><span data-stu-id="c47b7-121">PowerShell has many features found in typical programming languages.</span></span> <span data-ttu-id="c47b7-122">Można definiować zmienne, używać gałęzi i pętli, przechwytywać parametry wiersza polecenia, pisać funkcje, dodawać komentarze i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c47b7-122">You can define variables, use branches and loops, capture command-line parameters, write functions, add comments, and so on.</span></span> <span data-ttu-id="c47b7-123">W naszym skrypcie użyjemy trzech funkcji: zmiennych, pętli i parametrów.</span><span class="sxs-lookup"><span data-stu-id="c47b7-123">We will need three features for our script: variables, loops, and parameters.</span></span>

### <a name="variables"></a><span data-ttu-id="c47b7-124">Zmienne</span><span class="sxs-lookup"><span data-stu-id="c47b7-124">Variables</span></span>
<span data-ttu-id="c47b7-125">Program PowerShell obsługuje zmienne.</span><span class="sxs-lookup"><span data-stu-id="c47b7-125">PowerShell supports variables.</span></span> <span data-ttu-id="c47b7-126">Użyj znaku **$**, aby zadeklarować zmienną, i znaku **=**, aby przypisać do niej wartość.</span><span class="sxs-lookup"><span data-stu-id="c47b7-126">Use **$** to declare a variable and **=** to assign a value.</span></span> <span data-ttu-id="c47b7-127">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c47b7-127">For example:</span></span>

```powershell
$loc = "East US"
$iterations = 3
```

<span data-ttu-id="c47b7-128">Zmienne mogą przechowywać obiekty.</span><span class="sxs-lookup"><span data-stu-id="c47b7-128">Variables can hold objects.</span></span> <span data-ttu-id="c47b7-129">Na przykład następująca definicja ustawia zmienną **adminCredential** na obiekt zwrócony przez polecenie cmdlet **Get-Credential**.</span><span class="sxs-lookup"><span data-stu-id="c47b7-129">For example, the following definition sets the **adminCredential** variable to the object returned by the **Get-Credential** cmdlet.</span></span>

```powershell
$adminCredential = Get-Credential
```

<span data-ttu-id="c47b7-130">Aby uzyskać wartość przechowywaną w zmiennej, użyj prefiksu **$** i nazwy zmiennej, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c47b7-130">To obtain the value stored in a variable, use the **$** prefix and its name as shown below:</span></span> 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a><span data-ttu-id="c47b7-131">Pętle</span><span class="sxs-lookup"><span data-stu-id="c47b7-131">Loops</span></span>
<span data-ttu-id="c47b7-132">Program PowerShell obsługuje kilka pętli: **For**, **Do...While**, **For...Each** itd.</span><span class="sxs-lookup"><span data-stu-id="c47b7-132">PowerShell has several loops: **For**, **Do...While**, **For...Each**, and so on.</span></span> <span data-ttu-id="c47b7-133">Pętla **For** nadaje się najlepiej do naszych potrzeb, ponieważ będziemy wykonywać polecenie cmdlet określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="c47b7-133">The **For** loop is the best match for our needs because we will execute a cmdlet a fixed number of times.</span></span>

<span data-ttu-id="c47b7-134">Poniżej pokazano podstawową składnię; przykład jest uruchamiany dla dwóch iteracji i za każdym razem jest drukowana wartość zmiennej **i**.</span><span class="sxs-lookup"><span data-stu-id="c47b7-134">The core syntax is shown below; the example runs for two iterations and prints the value of **i** each time.</span></span> <span data-ttu-id="c47b7-135">Operatory porównań są zapisywane w następujący sposób: **-lt** — „mniejsze niż”, **-le** — „mniejsze niż lub równe”, **eq** — „równe”, **ne** — „różne od” itd.</span><span class="sxs-lookup"><span data-stu-id="c47b7-135">The comparison operators are written **-lt** for "less than", **-le** for "less than or equal", **eq** for "equal", **ne** for "not equal", etc.</span></span>

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a><span data-ttu-id="c47b7-136">Parametry</span><span class="sxs-lookup"><span data-stu-id="c47b7-136">Parameters</span></span>
<span data-ttu-id="c47b7-137">Podczas wykonywania skryptu można przekazywać argumenty w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="c47b7-137">When you execute a script, you can pass arguments on the command line.</span></span> <span data-ttu-id="c47b7-138">Aby ułatwić wyodrębnianie wartości przez skrypt, można nadać nazwy poszczególnym parametrom.</span><span class="sxs-lookup"><span data-stu-id="c47b7-138">You can provide names for each parameter to help the script extract the values.</span></span> <span data-ttu-id="c47b7-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c47b7-139">For example:</span></span>

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

<span data-ttu-id="c47b7-140">Wewnątrz skryptu wartości są przechwytywane do zmiennych.</span><span class="sxs-lookup"><span data-stu-id="c47b7-140">Inside the script, you capture the values into variables.</span></span> <span data-ttu-id="c47b7-141">W tym przykładzie parametry są dopasowywane według nazwy:</span><span class="sxs-lookup"><span data-stu-id="c47b7-141">In this example, the parameters are matched by name:</span></span>

```powershell
param([string]$location, [int]$size)
```

<span data-ttu-id="c47b7-142">Możesz pominąć nazwy z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c47b7-142">You can omit the names from the command line.</span></span> <span data-ttu-id="c47b7-143">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c47b7-143">For example:</span></span>

```powershell
.\setupEnvironment.ps1 5 "East US"
```

<span data-ttu-id="c47b7-144">Jeśli parametry nie mają nazw, ich dopasowywanie wewnątrz skryptu odbywa się na podstawie ich pozycji:</span><span class="sxs-lookup"><span data-stu-id="c47b7-144">Inside the script, you rely on position for matching when the parameters are unnamed:</span></span>

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a><span data-ttu-id="c47b7-145">Jak utworzyć maszynę wirtualną z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="c47b7-145">How to create a Linux Virtual Machine</span></span>
<span data-ttu-id="c47b7-146">Program Azure PowerShell udostępnia polecenie cmdlet **New-AzureRmVm** umożliwiające utworzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c47b7-146">Azure PowerShell provides the **New-AzureRmVm** cmdlet to create a Virtual Machine.</span></span> <span data-ttu-id="c47b7-147">To polecenie cmdlet ma wiele parametrów umożliwiających obsługę dużej liczby ustawień konfiguracji maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c47b7-147">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="c47b7-148">Większość parametrów ma odpowiednie wartości domyślne, dlatego wystarczy określić tylko pięć elementów:</span><span class="sxs-lookup"><span data-stu-id="c47b7-148">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>
- <span data-ttu-id="c47b7-149">**ResourceGroupName**: grupa zasobów, w której zostanie umieszczona nowa maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="c47b7-149">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="c47b7-150">**Name**: nazwa maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c47b7-150">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="c47b7-151">**Location**: lokalizacja geograficzna, w której będzie aprowizowana maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="c47b7-151">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="c47b7-152">**Credential**: obiekt zawierający nazwę użytkownika i hasło dla konta administratora maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c47b7-152">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="c47b7-153">W celu wyświetlenia prośby o podanie nazwy użytkownika i hasła użyjemy polecenia cmdlet **Get-Credential**.</span><span class="sxs-lookup"><span data-stu-id="c47b7-153">We will use the **Get-Credential** The cmdlet to prompt for a username and password.</span></span> <span data-ttu-id="c47b7-154">Polecenie **Get-Credential** pakuje nazwę użytkownika i hasło w obiekt poświadczeń, który jest zwracany w wyniku działania tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c47b7-154">**Get-Credential** packages the username and password into a credential object, which it returns as its result.</span></span>
- <span data-ttu-id="c47b7-155">**Image**: tożsamość systemu operacyjnego do użycia dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c47b7-155">**Image**: Identity of the operating system to use for the VM.</span></span> <span data-ttu-id="c47b7-156">Użyjemy tutaj wartości „UbuntuLTS”.</span><span class="sxs-lookup"><span data-stu-id="c47b7-156">We will use "UbuntuLTS".</span></span>

<span data-ttu-id="c47b7-157">Poniżej przedstawiono składnię tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c47b7-157">The syntax for the cmdlet is shown below:</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a><span data-ttu-id="c47b7-158">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c47b7-158">Summary</span></span>
<span data-ttu-id="c47b7-159">Kombinacja funkcji programów PowerShell i Azure PowerShell zapewnia wszystkie narzędzia potrzebne do automatyzacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c47b7-159">The combination of PowerShell and Azure PowerShell gives you all the tools you need to automate Azure.</span></span> <span data-ttu-id="c47b7-160">W naszym przykładzie firmy CRM będziemy mogli tworzyć wiele maszyn wirtualnych z systemem Linux, korzystając z parametru w celu utrzymania ogólnej postaci skryptu i pętli w celu uniknięcia powtarzania kodu.</span><span class="sxs-lookup"><span data-stu-id="c47b7-160">In our CRM example, we will be able to create multiple Linux VMs using a parameter to keep the script generic and a loop to avoid repeated code.</span></span> <span data-ttu-id="c47b7-161">Oznacza to, że wcześniej złożona operacja teraz może zostać wykonana w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="c47b7-161">This means that a formerly complex operation can now be executed in a single step.</span></span>