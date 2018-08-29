Ostatnim zadaniem, które chcemy spróbować wykonać na naszej maszynie wirtualnej jest zainstalowanie serwera internetowego. Jednym z najprostszych pakietów do zainstalowania jest pakiet `nginx`.

1. Znajdź publiczny adres IP swojej maszyny wirtualnej z systemem Linux. Pamiętaj, że w celu jego wyszukania możesz użyć polecenia `vm list-ip-addresses`.

2. Następnie otwórz połączenie `ssh` z maszyną (tak samo, jak podczas testowania). Pamiętaj, że trzeba będzie przekazać nazwę administratora („**aldis**”).

3. W przedstawionej powłoce wykonaj następujące polecenie, aby zainstalować serwer internetowy `nginx`.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. W usłudze Azure Cloud Shell odczytaj domyślną stronę z serwera internetowego z systemem Linux za pomocą polecenia `curl`. Alternatywnie możesz otworzyć nową kartę przeglądarki i przejść do publicznego adresu IP.

```azurecli
curl 168.61.54.62
```

Zakończy się to niepowodzeniem, ponieważ maszyna wirtualna z systemem Linux nie uwidacznia portu 80 (`http`) przez wbudowaną zaporę. Na szczęście interfejs wiersza polecenia platformy Azure oferuje odpowiednie polecenie: `vm open-port`. 

5. W usłudze Cloud Shell wpisz poniższe polecenie, aby otworzyć port 80:

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

Spróbuj ponownie wykonać polecenie `curl`. Tym razem powinno ono zwrócić dane. Strona będzie także widoczna w przeglądarce.



