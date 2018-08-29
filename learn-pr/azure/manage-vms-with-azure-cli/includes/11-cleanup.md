Utworzyliśmy nową maszynę wirtualną systemu Linux, zmieniliśmy jej rozmiar, zatrzymaliśmy ją i uruchomiliśmy oraz zaktualizowaliśmy konfigurację przy użyciu interfejsu wiersza polecenia platformy Azure.

## <a name="cleanup"></a>Czyszczenie

Teraz, gdy skończyliśmy pracę z maszyną wirtualną i już jej nie potrzebujemy, trzeba usunąć zasoby. Czyszczenie jest ważne ze względu na zasoby obliczeniowe i magazynowe, które nadal będą rozliczane w ramach Twojego konta. 

Możesz usunąć poszczególne zasoby za pomocą polecenia `delete`, ale najłatwiejszym sposobem na usunięcie wszystkich zasobów jest użycie polecenia `az group delete`. W interfejsie wiersza polecenia platformy Azure uruchom następujące polecenie:

```azurecli
az group delete --name ExerciseResources --no-wait
```

Odpowiedz „tak” na wyświetlony monit, lub użyj parametru `--yes`, aby odpowiedzieć na niego automatycznie.

To polecenie usuwa wszystkie zasoby skojarzone z grupą zasobów i gwarantuje cofnięcie ich przydziału w odpowiedniej kolejności. Parametr `--no-wait` zapobiega blokowaniu interfejsu wiersza polecenia platformy Azure podczas usuwania. Pozostaw go wyłączonego, oczekując na usunięcie zasobów. Możesz też użyć polecenia `az group wait -n ExerciseResources --deleted` dalej w swoim skrypcie, aby poczekać na zakończenie usuwania.


## <a name="further-reading"></a>Dalsze informacje

* [Omówienie interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [Dokumentacja poleceń interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
