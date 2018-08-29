W tym ćwiczeniu tworzona jest funkcja platformy Azure wywoływana co 20 sekund przy użyciu wyzwalacza czasomierza.

> [!NOTE] 
> Aby wykonać to ćwiczenie, musisz zalogować się w witrynie [Azure Portal](https://portal.azure.com/) przy użyciu prawidłowego konta.

## <a name="create-an-azure-function"></a>Tworzenie funkcji platformy Azure

Zacznijmy od utworzenia funkcji platformy Azure w portalu.

1. W lewym obszarze nawigacji wybierz pozycję **Utwórz zasób**.

1. Wybierz polecenie **Obliczenia**.

1. Znajdź i wybierz pozycję **Aplikacja funkcji**. Możesz również skorzystać z paska wyszukiwania, aby zlokalizować szablon.

    ![Wybieranie aplikacji funkcji](../media/4-click-function-app.png)

1. Wpisz unikatową **nazwę aplikacji**.

1. Wybierz pozycję **Subskrypcja**.

1. Utwórz nową **grupę zasobów**.

1. Wybierz **system operacyjny** **Windows**.

1. Wybierz **plan Zużycie** jako **plan hostingu**. Opłaty są naliczane za każde wykonanie funkcji. Zasoby są przydzielane automatycznie na podstawie obciążenia aplikacji.

1. Wybierz **lokalizację**.

1. Utwórz nowe konto usługi **Storage**. Ta wartość jest wymagana, ale nie będziemy z niej korzystać.

1. Wyłącz usługę **Application Insights**.

1. Wybierz pozycję **Utwórz**.

## <a name="create-a-timer-trigger"></a>Tworzenie wyzwalacza czasomierza

Teraz utworzymy wyzwalacz czasomierza w ramach funkcji platformy Azure.

1. Po utworzeniu funkcji platformy Azure wybierz pozycję **Wszystkie zasoby** w lewym obszarze nawigacji.

1. Zlokalizuj i wybierz funkcję platformy Azure.

1. W nowym bloku wskaż pozycję **Funkcje** i wybierz ikonę plus (+).

    ![Wskazywanie pozycji Funkcje i wybieranie ikony plusa](../media/4-hover-function.png)

1. Wybierz pozycję **Czasomierz**.

1. Wybierz język **CSharp**.

1. Wybierz pozycję **Utwórz tę funkcję**.

## <a name="configure-the-timer-trigger"></a>Konfigurowanie wyzwalacza czasomierza

Mamy funkcję platformy Azure z logiką drukowania komunikatu w oknie dziennika. Ustawimy harmonogram czasomierza, tak aby funkcja była wywoływana co 20 sekund.

1. Wybierz pozycję **Integracja**.

1. Wprowadź następującą wartość w polu **Harmonogram**:

    ```
    */20 * * * * *
    ```

1. Wybierz pozycję **Zapisz**.

## <a name="start-the-timer"></a>Uruchamianie czasomierza

Po skonfigurowaniu czasomierza można go uruchomić.

1. Wybierz pozycję **TimerTriggerCSharp1**. 

    > [!NOTE]
    > Nazwa **TimerTriggerCSharp1** jest nazwą domyślną. Jest wybierana automatycznie po utworzeniu wyzwalacza.

1. Wybierz pozycję **Uruchom**. 

Teraz co 20 sekund w oknie dziennika powinien być wyświetlany komunikat.

## <a name="clean-up"></a>Czyszczenie

Aby upewnić się, że opłaty za tę funkcję nie są naliczane, nad oknem dziennika wybierz polecenie **Wstrzymaj**, aby zatrzymać czasomierz.

![Wstrzymaj](../media/4-pause-timer.png)


