
W tym ćwiczeniu użyjesz interfejsu wiersza polecenia platformy Azure na maszynie lokalnej do utworzenia grupy zasobów, a następnie do wdrożenia w niej aplikacji internetowej. 

### <a name="steps-to-create-a-resource-group"></a>Kroki tworzenia grupy zasobów
1. Otwórz powłokę bash w systemie Linux lub macOS bądź otwórz okno wiersza polecenia lub programu PowerShell, jeśli pracujesz w systemie Windows.

1. Uruchom interfejs wiersza polecenia platformy Azure, a następnie uruchom polecenie logowania.

    ```bash
    az login
    ```
    Jeśli w przeglądarce internetowej nie zostanie wyświetlona strona logowania platformy Azure, postępuj zgodnie z instrukcjami wiersza polecenia, a następnie wprowadź kod autoryzacji na stronie [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

1. Utwórz grupę zasobów.

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. Sprawdź, czy grupa zasobów została pomyślnie utworzona, wyświetlając listę wszystkich grup zasobów w tabeli.

    ```bash
    az group list --output table
    ```
1. Opcjonalnie sprawdź w witrynie Azure Portal, czy zasób został utworzony. Otwórz przeglądarkę internetową, zaloguj się do witryny Azure Portal, a następnie przejdź do sekcji **Grupy zasobów** (zobacz poniżej). Nowa grupa zasobów powinna zostać wyświetlona na liście.

![Używanie witryny Azure Portal do wyświetlania listy grup zasobów](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a>Procedura tworzenia planu usług
W przypadku korzystania z usługi Web Apps w ramach usługi Azure App Service płacisz za zasoby obliczeniowe platformy Azure używane przez aplikację, co jest zależne od planu usługi App Service skojarzonego z usługami Web Apps. Za pomocą planów usług określany jest region używany na potrzeby centrum danych aplikacji, liczba używanych maszyn wirtualnych i warstwa cenowa.

1. Utwórz plan usługi App Service, w ramach którego zostanie uruchomiona Twoja aplikacja. Nazwy aplikacji i planu muszą być unikatowe, dlatego zmień ciąg „12345” na losową liczbę. Następujące polecenie nie określa warstwy cenowej lub szczegółów wystąpienia maszyny wirtualnej, więc domyślne zostanie użyty plan **Podstawowy** i jedno **małe** wystąpienie maszyny wirtualnej.

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. Sprawdź, czy plan usług został pomyślnie utworzony, wyświetlając listę wszystkich planów w tabeli.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Procedura tworzenia aplikacji internetowej
Następnym krokiem jest utworzenie aplikacji internetowej w ramach swojego planu usług. Kod można wdrożyć w tym samym czasie, ale w tym przykładzie zrobimy do w oddzielnych krokach.

1. Utwórz aplikację internetową, pamiętając o zmianie ciągu „12345” na wcześniej użytą losową liczbę.
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. Sprawdź, czy aplikacja została pomyślnie utworzona, wyświetlając listę wszystkich aplikacji w tabeli.

    ```bash
    az webapp list --output table
    ```

1. Zwróć uwagę na parametr **DefaultHostName**; będzie on potrzebny później.

### <a name="steps-to-deploy-code-from-github"></a>Procedura wdrażania kodu z repozytorium GitHub
1. Ostatnim krokiem jest wdrożenie kodu z repozytorium GitHub do aplikacji internetowej, ponownie pamiętając o zmianie ciągu „12345” na wcześniej użytą losową liczbę.
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Skopiuj następujący adres URL do przeglądarki, aby wyświetlić aplikację internetową.
http://popupapp12345.azurewebsites.net

1. Zostanie wyświetlona strona z informacją „HelloWorld!”

1. Zamknij okno przeglądarki.

## <a name="summary"></a>Podsumowanie
W ćwiczeniu przedstawiono typowy wzorzec na potrzeby interaktywnej sesji wiersza polecenia platformy Azure. Najpierw użyto standardowego polecenia, aby utworzyć nową grupę zasobów. Następnie użyto zestawu poleceń do wdrożenia zasobu (w tym przykładzie jest to aplikacja internetowa) w tej grupy zasobów. Ten zestaw poleceń można w łatwy sposób połączyć w skrypt powłoki i wykonywać za każdym razem, gdy konieczne jest utworzenie takiego samego zasobu.
