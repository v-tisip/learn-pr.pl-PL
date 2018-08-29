Maszyny wirtualne muszą mieć rozmiary stosowne do oczekiwanej pracy. Maszyna wirtualna bez odpowiedniej ilości pamięci lub zasobów procesora CPU ulegnie awarii przy zbyt dużym obciążeniu lub będzie działać za wolno, aby było to skuteczne. 

Podczas tworzenia maszyny wirtualnej możesz podać wartość _rozmiaru maszyny wirtualnej_, określającą ilość zasobów obliczeniowych, które będą przeznaczone dla tej maszyny wirtualnej. Obejmuje to procesory CPU i GPU oraz pamięć, które zostaną udostępnione maszynie wirtualnej na platformie Azure.

Platforma Azure oferuje do wyboru zestaw [wstępnie zdefiniowanych rozmiarów maszyn wirtualnych](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) dla systemów Linux i Windows na podstawie oczekiwanego użycia. 

| Typ | Rozmiary | Opis |
|------|-------|-------------|
| Zastosowania ogólne   | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7 | Zrównoważona moc procesora CPU w stosunku do pamięci. Opcja idealna w przypadku tworzenia i testowania, małych i średnich aplikacji oraz rozwiązań dotyczących danych. |
| Optymalizacja pod kątem obliczeń | Fs, F | Duża moc procesora CPU w stosunku do pamięci. Opcja dobra w przypadku aplikacji o średnim ruchu, urządzeń sieciowych i procesów wsadowych. |
| Optymalizacja pod kątem pamięci  | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Duża ilość pamięci na rdzeń. Opcja bardzo dobra w przypadku relacyjnych baz danych, średnich i dużych pamięci podręcznych oraz analizowania w pamięci. |
| Optymalizacja pod kątem magazynu | Ls | Wysoka przepływność dysku i duża liczba operacji we/wy. Opcja idealna w przypadku danych big data oraz baz danych SQL i NoSQL. |
| Optymalizacja pod kątem procesora GPU | NV, NC | Maszyny wirtualne wyspecjalizowane pod kątem intensywnego renderowania grafiki i edytowania materiałów wideo. |
| Wysoka wydajność | H, A8-11 | Maszyny wirtualne z najbardziej wydajnymi procesorami CPU oraz, opcjonalnie, interfejsami sieciowymi zapewniającymi wysoką przepływność (RDMA). | 

Dostępne rozmiary zmieniają się w zależności od regionu, w którym tworzysz maszynę wirtualną. Aby wyświetlić listę dostępnych rozmiarów, użyj polecenia `vm list-sizes`. Spróbuj wpisać następujące polecenie w usłudze Azure Cloud Shell:

```azurecli
az vm list-sizes --location eastus --output table
```

Poniżej przedstawiono skrócony wynik dla regionu `eastus`:

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

Nie określiliśmy rozmiaru, tworząc maszynę wirtualną — więc platforma Azure wybrała dla nas domyślny rozmiar ogólnego przeznaczenia, czyli `Standard_DS1_v2`. Możemy jednak określić rozmiar w ramach polecenia `vm create`, używając parametru `--size`.

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

## <a name="resizing-an-existing-vm"></a>Zmiana rozmiaru istniejącej maszyny wirtualnej
Możemy również zmienić rozmiar istniejącej maszyny wirtualnej w przypadku zmiany obciążenia lub niepoprawnego określenia rozmiaru na etapie tworzenia. Zanim zażądamy zmiany rozmiaru, musimy sprawdzić, czy żądany rozmiar jest dostępny w klastrze, do którego należy nasza maszyna wirtualna. W tym celu można użyć polecenia `vm list-vm-resize-options`:

```azurecli
az vm list-vm-resize-options --resource-group ExerciseResources --name SampleVM --output table
```

Zwróci ono listę wszystkich konfiguracji rozmiarów dostępnych w danej grupie zasobów. Jeśli żądany rozmiar nie jest dostępny w naszym klastrze, ale _jest_ dostępny w regionie, możemy [cofnąć przydział maszyny wirtualnej](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate). To polecenie zatrzyma uruchomioną maszynę wirtualną i usunie ją z bieżącego klastra bez utraty żadnych zasobów. Następnie możemy zmienić jej rozmiar, co spowoduje ponownie utworzenie maszyny wirtualnej w nowym klastrze, w którym wybrana konfiguracja rozmiaru jest dostępna.

Aby zmienić rozmiar maszyny wirtualnej, użyjemy polecenia `vm resize`. Ograniczmy na przykład bieżące zasoby naszej maszyny wirtualnej do absolutnego minimum: 2G pamięci, 1 rdzeń procesora CPU i 4G miejsca na dysku. Wpisz następujące polecenie w usłudze Cloud Shell:

```azurecli
az vm resize --resource-group ExerciseResources --name SampleVM --size "Standard_B1ms"
```

Zmniejszanie zasobów maszyny wirtualnej za pomocą tego polecenia potrwa kilka minut, a gdy wszystko będzie gotowe, polecenie zwróci nową konfigurację JSON.