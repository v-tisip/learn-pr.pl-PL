Program Azure PowerShell umożliwia pisanie poleceń i ich natychmiastowe wykonywanie. Jest to nazywane **trybem interaktywnym**.

Tak jak pamiętasz, ogólnym celem w przykładzie dotyczącym zarządzania relacjami z klientami (CRM, Customer Relationship Management) jest utworzenie trzech środowisk testowych zawierających maszyny wirtualne. Używane będą grupy zasobów w celu zapewnienia, że maszyny wirtualne są zorganizowane w ramach oddzielnych środowisk: jedno dla testów jednostkowych, jedno dla testów integracyjnych, a jedno dla testów akceptacyjnych. Grupy zasobów wystarczy utworzyć tylko raz, co oznacza, że używanie trybu interaktywnego programu PowerShell jest dobrym rozwiązaniem.

W tej sekcji przedstawiono kilka przykładów użycia programu PowerShell w sposób interaktywny w celu zalogowania się do subskrypcji platformy Azure i utworzenia grup zasobów.

## <a name="what-are-powershell-cmdlets"></a>Co to są polecenia cmdlet programu PowerShell?
Polecenie programu PowerShell jest nazywane **poleceniem cmdlet** (wymawiane jako „command-let”). Polecenie cmdlet służy do manipulowania pojedynczą funkcją. Termin **polecenie cmdlet** ma oznaczać „niewielkie polecenie”. Zgodnie z przyjętą konwencją autorzy poleceń cmdlet są zachęcani do tego, aby były one proste i miały jeden cel.

Podstawowy produkt programu PowerShell jest dostarczany wraz z poleceniami cmdlet działających z funkcjami, takimi jak sesje i zadania w tle. Do instalacji programu PowerShell możesz dodawać moduły, aby uzyskać polecenia cmdlet służące do manipulowania innymi funkcjami. Na przykład istnieją moduły innych firm służące do pracy z serwerem FTP, administrowania systemem operacyjnym, dostępu do systemu plików itd.

Polecenia cmdlet mają nazwy zgodne z konwencją nazewnictwa czasownik-rzeczownik; na przykład **Get-Process**, **Format-Table** i **Start-Service**. Istnieje również konwencja dotycząca wybierania czasowników: „get” w przypadku pobierania danych, „set” w przypadku wstawiania lub aktualizowania danych, „format” w przypadku formatowania danych, „out” w przypadku przekazywania danych wyjściowych do elementu docelowego itd.

Autorzy polecenia są zachęcani do dołączania pliku pomocy do każdego polecenia cmdlet. Polecenie cmdlet **Get-Help** wyświetla plik pomocy dla dowolnego polecenia cmdlet:

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>Co to jest moduł AzureRM?
**AzureRM** to formalna nazwa modułu programu Azure PowerShell zawierającego polecenia cmdlet służące do pracy z funkcjami platformy Azure (**RM** w nazwie oznacza usługę **Resource Manager**). Zawiera ona setki poleceń cmdlet, które pozwalają kontrolować niemal każdy aspekt wszystkich zasobów platformy Azure. Możesz pracować z grupami zasobów, magazynem, maszynami wirtualnymi, usługą Azure Active Directory, kontenerami, uczeniem maszynowym itd.

## <a name="how-to-create-a-resource-group"></a>Jak utworzyć grupę zasobów
Następnym krokiem będzie utworzenie grupy zasobów za pomocą lokalnej instalacji programu Azure PowerShell. 

W tym celu należy wykonać cztery kroki: 
1. Zaimportuj polecenia cmdlet platformy Azure.
1. Nawiąż połączenie z subskrypcją platformy Azure.
1. Utwórz grupę zasobów.
1. Sprawdź, czy tworzenie zakończyło się pomyślnie (patrz poniżej).

![Procedura tworzenia zasobu na platformie Azure przy użyciu programu Azure PowerShell](../media-drafts/5-create-resource-overview.png)

Każdy krok odnosi się do innego polecenia cmdlet.

### <a name="import"></a>Import
W momencie uruchamiania program PowerShell domyślnie ładuje tylko podstawowe polecenia cmdlet. Oznacza to, że polecenia cmdlet, które są potrzebne do pracy z platformą Azure, nie zostaną załadowane. Najbardziej niezawodnym sposobem ładowania wymaganych poleceń cmdlet jest ich ręczne zaimportowanie na początku sesji programu PowerShell.

Do załadowania modułów możesz użyć polecenia cmdlet **Import-Module**. To polecenie cmdlet ma wiele parametrów służących do obsługi wielu różnych sytuacji. Na przykład za jego pomocą można załadować wiele modułów, określoną wersję modułu, część modułu itd. Aby załadować jeden moduł w całości, składnia jest po prostu następująca:

```powershell
Import-Module <module-name>
```

> [!TIP]
> Jeśli okaże się, że często pracujesz z programem Azure PowerShell, istnieją dwa sposoby na zautomatyzowanie procesu ładowania modułów. Możesz dodać wpis do Twojego profilu programu PowerShell służący do importowania modułu platformy Azure podczas uruchamiania lub użyć najnowszych wersji programu PowerShell, które automatycznie ładują zawarty moduł w momencie użycia polecenia cmdlet.

### <a name="connect"></a>Połączenie
Ponieważ pracujesz z lokalną instalacją programu Azure PowerShell, zanim możliwe będzie wykonywanie poleceń platformy Azure konieczne jest przeprowadzenie uwierzytelniania. Polecenie cmdlet **Connect-AzureRmAccount** wyświetla monit o podanie poświadczeń platformy Azure, a następnie nawiązuje połączenie z Twoją subskrypcją platformy Azure. Zawiera ono wiele parametrów opcjonalnych, ale jeśli potrzebny jest jedynie monit interaktywny, nie są wymagane żadne parametry:

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a>Przycisk Utwórz
Polecenie cmdlet **New-AzureRmResourceGroup** służy do tworzenia grupy zasobów. Musisz określić nazwę i lokalizację. Nazwa musi być unikatowa w ramach Twojej subskrypcji. Lokalizacja określa, gdzie będą przechowywane metadane dla Twojej grupy zasobów (co może być istotne w celu zachowania zgodności). Ciągi, takie jak „Zachodnie stany USA”, „Europa Północna” lub „Indie Zachodnie” umożliwiają określenie lokalizacji. Podobnie jak w przypadku większości poleceń cmdlet platformy Azure, polecenie cmdlet **New-AzureRmResourceGroup** ma wiele parametrów opcjonalnych. Podstawowa składnia jest jednak następująca:

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a>Weryfikuj
Polecenie cmdlet **Get-AzureRmResource** służy do wyświetlania listy zasobów platformy Azure. Jest ono przydatne w tym przypadku w celu sprawdzenia, czy tworzenie grupy zasobów zakończyło się pomyślnie.

```powershell
Get-AzureRmResource
```

Aby uzyskać bardziej zwięzły widok, możesz wysłać dane wyjściowe z polecenia cmdlet **Get-AzureRmResource** do polecenia cmdlet **Format-Table** przy użyciu potoku „|”.

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a>Podsumowanie
Tryb interaktywny programu PowerShell jest odpowiedni dla zadań jednorazowych. W tym przykładzie dla okresu istnienia projektu będzie używana taka sama grupa zasobów, co oznacza, że uzasadnione jest tworzenie jej w sposób interaktywny. Użycie trybu interaktywnego jest często szybsze i łatwiejsze na potrzeby tego zadania niż pisanie skryptu i jego jednorazowe wykonanie.