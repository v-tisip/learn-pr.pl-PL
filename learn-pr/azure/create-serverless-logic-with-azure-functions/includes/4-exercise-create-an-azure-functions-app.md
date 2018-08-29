W tym ćwiczeniu utworzymy aplikację funkcji platformy Azure.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com) przy użyciu konta platformy Azure.
1. Wybierz przycisk **Utwórz zasób** znajdujący się w lewym górnym rogu witryny Azure Portal, a następnie wybierz pozycję **Obliczenia > Aplikacja funkcji**.
  ![Tworzenie zasobu aplikacji funkcji](../images/4-create-function-app-blade.png)
1. Wybierz globalnie unikatową nazwą aplikacji. Będzie ona służyć jako podstawowy adres URL usługi. Możesz na przykład nadać aplikacji nazwę **escalator-functions-xxxxxxx**, zastępując znaki x swoimi inicjałami i rokiem urodzenia. Jeśli nazwa nie jest globalnie unikatowa, możesz wypróbować dowolną inną kombinację. Dopuszczalne są znaki od a do z, od 0 do 9 oraz znak -.
1. Wybierz subskrypcję platformy Azure, w ramach której będzie hostowana aplikacja funkcji.
1. Utwórz nową grupę zasobów o nazwie **escalator-functions-group**. Ułatwi to czyszczenie zasobów na późniejszym etapie.
1. Wybierz system operacyjny **Windows**.
1. W polu **Plan hostingu** wybierz **Plan Zużycie**, aby skorzystać z bezserwerowych funkcji platformy Azure.
1. Wybierz lokalizację geograficzną położoną najbliżej Ciebie (lub Twoich klientów).
1. Utwórz nowe konto magazynu i nadaj mu nazwę **escalatorfunctions**.
1. Upewnij się, że usługa Azure Application Insights jest **włączona** i wybierz najbliższy region.
1. Wybierz pozycję **Utwórz**. Wdrażanie potrwa kilka minut. Po jego zakończeniu otrzymasz powiadomienie.
  ![Ustawienia aplikacji funkcji](../images/4-create-function-app-settings.png)

## <a name="verify-your-azure-function-app"></a>Weryfikowanie aplikacji funkcji platformy Azure

1. W witrynie Azure Portal wybierz pozycję **Grupy zasobów** z menu po lewej stronie. Grupa **escalator-functions-group** powinna być widoczna na liście dostępnych grup.
  ![Grupa zasobów](../images/4-resource-group.png)
1. Wybierz grupę **escalator-functions-group**. Powinna zostać wyświetlona lista zasobów podobna do następującej: ![Lista zasobów](../images/4-resource-list.png)
