Pomyślnie utworzono aplikację mobilną dla wielu platform przy użyciu platformy Xamarin i funkcji platformy Azure z powiązaniem usługi Twilio.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Po zakończeniu pracy z tą aplikacją usługi Azure Functions można usunąć wszystkie zasoby utworzone w ramach tego samouczka z witryny Azure Portal.

1. W programie Visual Studio wybierz pozycję *Widok->Cloud Explorer*.

2. Z listy rozwijanej w górnej części tego panelu wybierz pozycję *Grupy zasobów*.

3. Rozwiń subskrypcję, która była używana do utworzenia tej grupy zasobów. Kliknij prawym przyciskiem myszy grupę zasobów „ImHere”, a następnie wybierz pozycję *Otwórz w portalu*.

    ![Otwieranie grupy zasobów w portalu z okna eksploratora chmury](../media-drafts/9-open-resource-group-in-portal.png)

4. W razie potrzeby zaloguj się do witryny Azure Portal w przeglądarce.

5. Portal otworzy się na grupie zasobów „ImHere”. Kliknij przycisk **Usuń grupę zasobów**.

    ![Usuwanie grupy zasobów](../media-drafts/9-delete-resource-group.png)

6. Wprowadź nazwę grupy zasobów, aby potwierdzić usunięcie, a następnie kliknij przycisk **Usuń**.

    ![Wprowadzanie nazwy grupy zasobów, aby potwierdzić usunięcie](../media-drafts/9-confirm-delete-resource-group.png)

## <a name="summary"></a>Podsumowanie

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:
> [!div class="checklist"]
> * Tworzenia aplikacji platformy Xamarin.Forms dla wielu platform, która używa rozwiązania Xamarin.Essentials.
> * Tworzenia międzyplatformowego interfejsu użytkownika przy użyciu języka XAML z logiką aplikacji w modelu ViewModel oraz tworzenia powiązania właściwości w modelu ViewModel z interfejsem użytkownika.
> * Wykrywania lokalizacji użytkownika.
> * Tworzenia funkcji platformy Azure z wyzwalaczem HTTP, a następnie uruchamianie ich lokalnie.
> * Wywoływania funkcji platformy Azure z aplikacji mobilnej z przekazywaniem danych w formacie JSON.
> * Tworzenia powiązania funkcji platformy Azure z usługą Twilio, aby wysłać wiadomość SMS.
> * Publikowania funkcji platformy Azure na platformie Azure.
