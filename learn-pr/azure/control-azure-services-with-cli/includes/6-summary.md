## <a name="module-summary"></a>Podsumowanie modułu
W tym module użyto interfejsu wiersza polecenia platformy Azure do utworzenia grupy zasobów i wdrożenia aplikacji internetowej za pomocą niewielkiego zestawu poleceń. Te polecenia można łączyć w skrypcie powłoki jako część rozwiązania do automatyzacji.

Interfejs wiersza polecenia platformy Azure jest dobrym wyborem dla każdego nowego użytkownika wiersza polecenia platformy Azure oraz skryptów. Jego prosta składnia i zgodność międzyplatformowa zmniejszają ryzyko wystąpienia błędów podczas wykonywania regularnych i powtarzalnych zadań.

## <a name="cleanup"></a>Czyszczenie
Uruchamianie aplikacji internetowej powoduje naliczanie kosztów względem Twojej subskrypcji. Aby uniknąć niepotrzebnych opłat, możesz usunąć zbędne zasoby. Najprostszym sposobem oczyszczenia subskrypcji platformy Azure jest usunięcie grupy zasobów. Spowoduje to również usunięcie wszystkich zasobów w grupie. Po zakończeniu tego modułu uruchom następujące polecenie cmdlet programu Azure PowerShell:

    ```azurecli
    az group delete --resource-group popupResGroup
    ```

Gdy pojawi się prośba o potwierdzenie usunięcia, odpowiedz **Tak**. Wykonywanie polecenia może potrwać kilka minut i zakończy się po usunięciu zasobów. 