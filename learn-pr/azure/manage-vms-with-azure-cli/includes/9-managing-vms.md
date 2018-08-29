Jednym z głównych zadań wykonywanych w stosunku do działających maszyn wirtualnych jest ich uruchamianie i zatrzymywanie.

## <a name="stopping-a-vm"></a>Zatrzymywanie maszyny wirtualnej

Uruchomioną maszynę wirtualną możemy zatrzymać za pomocą polecenia `vm stop`. Musisz przekazać nazwę i grupę zasobów lub unikatowy identyfikator maszyny wirtualnej:

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

Możemy sprawdzić, czy została ona zatrzymana, próbując wysłać polecenie ping do publicznego adresu IP, przy użyciu elementu `ssh` lub polecenia `vm get-instance-view`. To końcowe podejście powoduje zwrócenie tych samych danych podstawowych jako `vm show`, ale obejmuje szczegółowe informacje o samym wystąpieniu. Spróbuj wpisać poniższe polecenie w usłudze Azure Cloud Shell, aby wyświetlić bieżący stan działania maszyny wirtualnej:

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/') == `true`].displayStatus" -o tsv
```

To polecenie powinno zwrócić wynik `VM stopped`.

## <a name="starting-a-vm"></a>Uruchamianie maszyny wirtualnej

Odwrotną czynność możemy wykonać za pomocą polecenia `vm start`.

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

To polecenie uruchomi zatrzymaną maszynę wirtualną. Możemy to zweryfikować przy użyciu zapytania `vm get-instance-view`, które powinno teraz zwrócić wartość `VM running`.

## <a name="restarting-a-vm"></a>Ponowne uruchamianie maszyny wirtualnej

Na koniec możemy można ponownie uruchomić maszynę wirtualną, jeśli wprowadzono zmiany, które wymagają ponownego uruchomienia przy użyciu polecenia `vm restart`. Możesz dodać flagę `--no-wait`, jeśli chcesz, aby interfejs wiersza polecenia platformy Azure był zwracany natychmiast bez oczekiwania na ponowne uruchomienie maszyny wirtualnej.

