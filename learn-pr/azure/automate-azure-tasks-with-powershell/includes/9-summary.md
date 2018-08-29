W tym module napisaliśmy skrypt, aby zautomatyzować tworzenie wielu maszyn wirtualnych. Mimo że skrypt był relatywnie krótki, widać, jakie możliwości daje połączenie pętli, zmiennych i funkcji w programie PowerShell z poleceniami cmdlet w programie Azure PowerShell.

Program Azure PowerShell to dobre rozwiązanie do automatyzacji dla administratorów mających doświadczenie z programem PowerShell. Kombinacja przejrzystej składni i zaawansowanego języka skryptów sprawia, że warto go rozważyć, nawet jeśli nie ma się doświadczenia z programem PowerShell. Ten poziom automatyzacji w przypadku zadań, które są czasochłonne i podatne na błędy, pomoże skrócić czas potrzebny na zadania administracyjne i zapewnić wyższą jakość.

## <a name="cleanup"></a>Czyszczenie
Zaaprowizowane i uruchomione maszyny wirtualne generują koszty w subskrypcji. Należy usunąć niepotrzebne maszyny wirtualne, aby uniknąć naliczania niepotrzebnych opłat. Najprostszym sposobem oczyszczenia subskrypcji platformy Azure jest usunięcie powiązanej grupy zasobów. Spowoduje to również usunięcie wszystkich maszyn wirtualnych w tej grupie. Możesz zrobić to w programie PowerShell. Po zakończeniu pracy uruchom następujące polecenie cmdlet programu Azure PowerShell:

```powershell
Remove-AzureRmResourceGroup -Name TrialsResourceGroup
```

Gdy pojawi się monit o potwierdzenie usunięcia, odpowiedz **Tak**. Wykonanie tego polecenia może potrwać kilka minut.