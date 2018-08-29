Aplikacja i funkcja platformy Azure są teraz kompletne i działają w środowisku lokalnym. W tym module opublikujesz funkcję platformy Azure na platformie Azure w celu jej uruchamiania w chmurze.

> W tym module opublikujesz funkcję z poziomu programu Visual Studio. Jest to doskonały sposób, aby rozpocząć pracę na potrzeby weryfikacji koncepcji, prototypów i uczenia się, ale w przypadku aplikacji o jakości produkcyjnej **nie** powinno się używać tej metody. W zamian należy skorzystać z wdrożenia opartego na elemencie konfiguracji. Więcej informacji na ten temat można znaleźć w [dokumentach dotyczących wdrażania usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).
>
> [![Znajomi: nie pozwalaj znajomym na publikowanie przy użyciu kliknięcia prawym przyciskiem myszy](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)

## <a name="publishing-your-app-to-azure"></a>Publikowanie aplikacji na platformie Azure

Funkcje platformy Azure można publikować na platformie Azure z poziomu programu Visual Studio.

1. Zatrzymaj lokalne środowisko uruchomieniowe usługi Azure Functions, jeśli nadal działa po uruchomieniu w poprzednim module.

2. W eksploratorze rozwiązań kliknij prawym przyciskiem myszy aplikację `ImHere.Functions` i wybierz polecenie *Opublikuj...*.

    ![Klikanie prawym przyciskiem myszy pozycji Opublikuj w aplikacji usługi Functions](../media/8-right-click-publish.png)

3. W oknie dialogowym **Wybieranie miejsca docelowego publikacji** wybierz pozycję *Aplikacja funkcji platformy Azure*, a w obszarze **Azure App Service** wybierz pozycję *Utwórz nową*. Kliknij przycisk **Opublikuj**.

    ![Tworzenie nowej usługi Azure App Service jako docelowej lokalizacji publikowania](../media/8-pick-publish-target.png)

4. Z listy rozwijanej w prawym górnym rogu wybierz konto platformy Azure, jeśli masz więcej niż jedno takie konto i właściwe konto nie zostało wybrane.

5. Nadaj nazwę aplikacji usługi Functions. Ta nazwa musi być globalnie unikatowa wśród wszystkich aplikacji usługi Functions na całej platformie Azure, dlatego użyj nazwy podobnej do „ImHere-\<Twoja_nazwa\>”.

6. Wybierz subskrypcję, w ramach której chcesz utworzyć aplikację usługi Functions.

7. Utwórz nową grupę zasobów dla tej aplikacji usługi Functions, klikając przycisk **Nowy...** obok listy rozwijanej **Grupa zasobów** i nadając jej nazwę, taką jak „ImHere”. Nazwy grup zasobów muszą być unikatowe w ramach Twojej subskrypcji, a nie globalnie unikatowe na platformie Azure. Następnie kliknij przycisk **OK**.

    ![Utworzenie nowej grupy zasobów](../media/8-create-new-resource-group.png)

   Tworzenie nowej grupy zasobów ułatwia jej czyszczenie później. Możesz usunąć grupę zasobów i mieć pewność, że wszystkie elementy utworzone dla tej aplikacji usługi Functions zostaną usunięte w tym samym czasie.

8. Utwórz nowy plan hostingu, klikając przycisk **Nowy...** obok listy rozwijanej **Plan hostingu**. Nazwa planu usługi App Service zostanie domyślnie ustawiona na nazwę aplikacji z ciągiem „Plan” dodanym na końcu. Ustaw pole **Lokalizacja** na najbliższą sobie lokalizację i upewnij się, że **Rozmiar** został ustawiony na wartość użycia. Następnie kliknij przycisk **OK**.

    ![Konfigurowanie planu hostingu](../media/8-configure-hosting-plan.png)

9. Utwórz nowe konto magazynu, klikając przycisk **Nowy...** obok listy rozwijanej **Konto usługi Storage**. Zostanie podana nazwa domyślna. Zachowaj wszystkie wartości domyślne i kliknij przycisk **OK**.

    ![Tworzenie konta magazynu](../media/8-create-storage-account.png)

10. Kliknij pozycję **Utwórz**, aby aprowizować wszystkie zasoby na platformie Azure i opublikować aplikację usługi Azure Functions.

    ![Tworzenie usługi App Service](../media/8-create-app-service.png)

Uruchamianie aprowizowania może potrwać kilka minut. Następujące zasoby zostaną aprowizowane:

* Konto magazynu do przechowywania plików potrzebnych w aplikacji usługi Azure Functions
* Plan usługi App Service umożliwiający zarządzanie zasobami obliczeniowymi wymaganymi przez aplikację usługi Azure Functions
* Usługa App Service, która uruchamia funkcję platformy Azure

Funkcja zostanie teraz opublikowana i będzie dostępna pod adresem https://<nazwa_Twojej_aplikacji>.azurewebsites.net/api/SendLocation.

## <a name="configuring-your-app"></a>Konfigurowanie aplikacji

Funkcja platformy Azure uruchamiana lokalnie używała poświadczeń usługi Twilio przechowywanych w pliku `local.settings.json`. Jak sugeruje nazwa, ten plik jest przeznaczony dla ustawień lokalnych, a nie ustawień platformy Azure. Przed wywołaniem funkcji platformy Azure wewnątrz platformy Azure należy skonfigurować ustawienia `TwilioAccountSid` i `TwilioAuthToken`.

1. Na karcie Publikowanie kliknij opcję **Zarządzaj ustawieniami aplikacji**.

    ![Opcja Zarządzaj ustawieniami aplikacji](../media/8-application-settings-option.png)

2. Kliknij przycisk **Dodaj**, aby dodać nowe ustawienie. Nadaj mu nazwę „TwilioAccountSid” i ustaw wartość identyfikatora SID konta usługi Twilio. Powtórz ten krok dla tokenu uwierzytelniania przy użyciu nazwy „TwilioAuthToken”.

    ![Ustawianie poświadczeń usługi Twilio w ustawieniach aplikacji](../media/8-set-creds-in-app-settings.png)

3. Kliknij przycisk **OK**.

4. Kliknij pozycję **Opublikuj**, aby ponownie opublikować aplikację usługi Azure Functions z nowymi ustawieniami aplikacji.

    ![Przycisk Opublikuj](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a>Wskazywanie platformy Azure w aplikacji mobilnej

1. Na karcie Publikowanie skopiuj **adres URL witryny** przy użyciu przycisku kopiowania obok wartości.

    ![Kopiowanie adresu URL witryny z poziomu karty Publikowanie](../media/8-copy-site-url.png)

2. Otwórz model `MainViewModel` z projektu `ImHere`.

3. Zaktualizuj wartość pola `baseUrl`, aby była adresem URL witryny skopiowanym z karty Publikowanie.

4. Zmień protokół dla tej wartości z `http` na `https`. Adres URL witryny jest zawsze podawany przy użyciu protokołu HTTP, ale w celu wywołania funkcji platformy Azure trzeba użyć protokołu HTTPS.

## <a name="test-it-out"></a>Testowanie działania

1. Ustaw aplikację `ImHere.UWP` jako aplikację uruchamiania i uruchom ją.

2. Wprowadź numer telefonu, a następnie kliknij przycisk **Wyślij lokalizację**.

3. Lokalizacja powinna zostać odebrana w postaci wiadomości SMS.

## <a name="summary"></a>Podsumowanie

W tym module przedstawiono sposób publikowania projektu usługi Azure Functions do platformy Azure z poziomu programu Visual Studio oraz konfigurowania ustawień aplikacji.