Teraz nadszedł czas na uruchomienie aplikacji na platformie Azure. Musimy utworzyć aplikację usługi Azure App Service, skonfigurować ją przy użyciu tożsamości MSI i konfiguracji naszego magazynu oraz wdrożyć nasz kod.

## <a name="exercise"></a>Ćwiczenie

### <a name="create-the-app-service-plan-and-app"></a>Tworzenie aplikacji i planu usługi App Service

Tworzenie aplikacji usługi App Service jest procesem dwuetapowym: najpierw należy utworzyć *plan*, a następnie *aplikację*.

Nazwa *planu* musi być unikatowa tylko w ramach subskrypcji, aby można było stosować nazwę używaną przez nas: **keyvault-exercise-plan**. Nazwa aplikacji musi być globalnie unikatowa, więc musisz wybrać własną.

W usłudze Azure Cloud Shell uruchom następujące polecenie:

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a>Dodawanie konfiguracji do aplikacji

W przypadku wdrażania na platformie Azure będziemy korzystać z najlepszego rozwiązania w usłudze App Service, które polega na umieszczaniu konfiguracji w ustawieniach aplikacji, a nie w pliku konfiguracji.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a>Włączanie tożsamości usługi zarządzanej

Włączanie tożsamości usługi zarządzanej aplikacji wymaga jednego wiersza kodu:

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Z wynikowych danych wyjściowych JSON skopiuj wartość **principalId**. PrincipalId to unikatowy identyfikator nowej tożsamości aplikacji w usłudze Azure Active Directory. Będziemy z niego korzystać w następnym kroku.

### <a name="grant-access-to-the-vault"></a>Udzielanie dostępu do magazynu

Teraz musisz udzielić aplikacji uprawnień tożsamości do pobierania i wyświetlania listy wpisów tajnych z magazynu w środowisku produkcyjnym. Użyj wartości **principalId** skopiowanej w poprzednim kroku jako wartości identyfikatora **object-id** w poleceniu poniżej.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a>Wdrażanie aplikacji i jej wypróbowywanie

Konfiguracja została ustawiona i wszystko jest gotowe do wdrażania. Poniższe polecenia spowodują opublikowanie witryny w folderze `pub`, spakowanie jej w pliku `site.zip` i wdrożenie pliku ZIP w usłudze App Service.

> [!NOTE]
> Jeśli jeszcze nie znajdujesz się w katalogu KeyVaultDemoApp, musisz do niego wrócić za pomocą polecenia `cd`.

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Po uzyskaniu wyniku wskazującego na to, że witryna została wdrożona, otwórz adres `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` w przeglądarce. Powinna pojawić się wartość wpisu tajnego **reindeer_flotilla**.

Twoja aplikacja jest gotowa i wdrożona.