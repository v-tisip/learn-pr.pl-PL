Tworzona przez Ciebie aplikacja to międzyplatformowa aplikacja mobilna komunikująca się z funkcją platformy Azure w celu udostępnienia Twojej lokalizacji. W ramach tej sekcji utworzysz pustą aplikację mobilną za pomocą programu Visual Studio i zainstalujesz pakiet NuGet, który udostępnia interfejs API umożliwiający pobieranie lokalizacji użytkownika.

## <a name="create-the-xamarinforms-project"></a>Tworzenie projektu platformy Xamarin.Forms

1. W programie Visual Studio wybierz pozycję *Plik -> Nowy -> Projekt...*.

2. W drzewie po lewej stronie wybierz pozycję *Visual C# -> Wiele platform*, a następnie pozycję *Aplikacja mobilna (Xamarin.Forms)* z panelu w środku.

3. Podaj nazwę „ImHere” dla rozwiązania.

4. Wybierz odpowiednią lokalizację dla rozwiązania.

    > Jeśli korzystasz z tego modułu lokalnie w systemie Windows i planujesz kompilowanie dla systemu Android, upewnij się, że ścieżka jest możliwie krótka. Zestawu Android SDK dotyczą ograniczenia długości ścieżki, więc ścieżka katalogu głównego powinna być możliwie krótka.

5. Kliknij przycisk **OK**.

    ![Okno dialogowe Nowe rozwiązanie](../media-drafts/2-new-solution-dialog.png)

6. Z okna dialogowego **Nowa aplikacja międzyplatformowa** wybierz szablon *Pusta aplikacja*.

7. W ramach tego modułu będzie kompilowana aplikacja UWP, więc anuluj zaznaczenie systemów iOS i Android oraz pozostaw zaznaczoną platformę UWP.

    > Jeśli korzystasz z niego lokalnie, możesz pozostawić system Android zaznaczony, ponieważ zestaw Android SDK został zainstalowany jako część pakietu roboczego *Tworzenie aplikacji mobilnych przy użyciu platformy .NET* programu Visual Studio. Jeśli chcesz także kompilować dla systemu iOS, musisz wykonać parowanie z agentem kompilacji systemu macOS. Więcej informacji na ten temat zawiera [dokumentacja platformy Xamarin dla systemu iOS](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/).

8. Dla pozycji *Strategia udostępniania kodu* wybierz opcję **.NET Standard**.

9. Kliknij przycisk **OK**.

    ![Okno dialogowe konfigurowania nowego rozwiązania](../media-drafts/2-configure-solution-dialog.png)

Program Visual Studio utworzy dwa projekty — aplikację UWP o nazwie `ImHere.UWP` i bibliotekę platformy .NET Standard o nazwie `ImHere`. Aplikacje platformy Xamarin.Forms składają się z dwóch części — co najmniej jeden projekt aplikacji specyficzny dla platformy i co najmniej jedna biblioteka platformy .NET Standard. Projekty aplikacji specyficzne dla platformy zawierają kod specyficzny dla platformy wymagany do uruchomienia na niej aplikacji. Te projekty następnie uruchamiają aplikację platformy Xamarin.Forms, która jest zdefiniowana w międzyplatformowej bibliotece platformy .NET Standard. Aplikację kompiluje się do kodu międzyplatformowego, a w czasie wykonywania wszelkie utworzone interfejsy użytkownika są tłumaczone na odpowiednie składniki interfejsu użytkownika specyficzne dla platformy.

## <a name="adding-xamarinessentials"></a>Dodawanie pakietu Xamarin.Essentials

Platformy UWP, Android i iOS udostępniają wiele podobnych możliwości, które wykorzystują system operacyjny i sprzęt. Mimo tych podobieństw interfejsy API różnią się znacznie. Używanie tych interfejsów API z poziomu kodu międzyplatformowego wymaga napisania kodu specyficznego dla platformy w projektach aplikacji i ujawnienia go dla bibliotek platformy .NET Standard. [Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/) to pakiet NuGet, który udostępnia międzyplatformowe abstrakcje dla pewnej liczby tych interfejsów API, w tym interfejsów API geolokalizacji, które będą używane w aplikacji do pobierania lokalizacji użytkownika.

1. Kliknij prawym przyciskiem myszy rozwiązanie `ImHere` w Eksploratorze rozwiązań programu Visual Studio i wybierz pozycję *Zarządzaj pakietami NuGet dla rozwiązania...*.

2. Wybierz kartę **Przeglądaj** i wyszukaj pozycję „Xamarin.Essentials”. Ten pakiet NuGet jest obecnie dostępny w wersji wstępnej, więc zaznacz pole *uwzględnij wersję wstępną*.

3. Wybierz pakiet NuGet **Xamarin.Essentials**.

4. Zaznacz wszystkie projekty na liście projektów po prawej stronie.

5. Kliknij przycisk **Instaluj**, aby zainstalować pakiet NuGet. Musisz zaakceptować licencję, aby kontynuować.

    ![Dodawanie pakietu NuGet Xamarin.Essentials do wszystkich projektów w rozwiązaniu](../media-drafts/2-add-essentials-nuget.png)

    > Jeśli korzystasz z tego modułu w środowisku lokalnym, a platformą docelową ma być system Android, musisz przeprowadzić dodatkową konfigurację. Aby uzyskać więcej informacji, zobacz [Wprowadzenie do platformy Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/get-started?context=xamarin%2Fios&tabs=windows%2Candroid).

## <a name="building-and-running-the-app"></a>Kompilowanie i uruchamianie aplikacji

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt `ImHere.UWP` i wybierz polecenie *Ustaw jako projekt startowy*.

2. Ustaw konfigurację kompilacji na **Debugowanie**, platformę na **x86**, a urządzenie na potrzeby uruchamiania na **Komputer lokalny**.

    ![Ustawianie konfiguracji debugowania dla architektury x86 pod kątem uruchamiania na urządzeniu lokalnym](../media-drafts/2-debug-configuration.png)

3. Rozpocznij debugowanie aplikacji.

    ![Uruchomiona aplikacja](../media-drafts/2-debuging-app.png)

## <a name="summary"></a>Podsumowanie

W ramach tej sekcji utworzono nową międzyplatformową aplikację mobilną platformy Xamarin.Forms i dodano pakiet NuGet Xamarin.Essentials. Następnie dowiesz się, jak utworzyć interfejs użytkownika i logikę aplikacji mobilnej.