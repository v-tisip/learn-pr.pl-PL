Do utworzenia maszyny wirtualnej użyliśmy obrazu systemu `Debian`. Platforma Azure oferuje kilka standardowych obrazów maszyn wirtualnych służących do tworzenia maszyny wirtualnej. 

Aby wyświetlić listę dostępnych obrazów, użyj polecenia `az vm image list --output table`. W wyniku uzyskasz najbardziej popularne obrazy, które są częścią listy trybu offline wbudowanej w interfejsie wiersza polecenia platformy Azure. Witryna Azure Marketplace oferuje jednak _setki_ opcji obrazów. 

> [!TIP]
> Pełną listę można uzyskać, dodając do polecenia flagę `--all`. Lista obrazów w witrynie Marketplace jest bardzo długa, dlatego warto ją przefiltrować za pomocą opcji `--publisher` lub `–-offer`.

Niektóre obrazy są dostępne tylko w określonych lokalizacjach. Spróbuj dodać do polecenia flagę `--location [location]`, aby ograniczyć zakres wyników do tych, które są dostępne w regionie, gdzie chcesz utworzyć maszynę wirtualną. Wpisz na przykład następujące polecenie w usłudze Azure Cloud Shell, aby uzyskać listę obrazów dostępnych w regionie `eastus`.

```azurecli
az vm image list --location eastus --output table
```

> [!NOTE]
> Są to standardowe obrazy dostarczane przez platformę Azure. Pamiętaj, że możesz również [utworzyć i przekazać własne obrazy niestandardowe](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images), aby tworzyć maszyny wirtualne na podstawie unikatowych konfiguracji lub mniej typowych wersji lub dystrybucji systemu operacyjnego.