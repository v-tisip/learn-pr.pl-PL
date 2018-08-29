W tym ćwiczeniu utworzysz i skonfigurujesz niestandardowy pulpit nawigacyjny.

## <a name="create-a-new-dashboard"></a>Tworzenie nowego pulpitu nawigacyjnego

1. W witrynie Azure Portal kliknij przycisk **Nowy pulpit nawigacyjny**.

2. W oknie **Mój pulpit nawigacyjny** zmień nazwę na **Pulpit nawigacyjny klienta**.

## <a name="add-and-configure-the-clock-tile"></a>Dodawanie i konfigurowanie kafelka zegara

1. Przeciągnij zegar z galerii kafelków i upuść go w obszarze roboczym. Umieść zegar w prawym górnym rogu w dostępnym obszarze.

2. W bloku edycji zegara zmień lokalizację na **Czas pacyficzny (Stany Zjednoczone i Kanada)**.

3. W obszarze **Format godziny** kliknij pozycję **24 godziny**.

4. Kliknij przycisk **Gotowe**.

5. Powtórz cztery powyższe kroki, wybierając pozycję **Czas wschodni (Stany Zjednoczone i Kanada)**. Masz teraz dwa zegary. Pierwszy wyświetla godzinę na zachodnim wybrzeżu, a drugi — na wschodnim.

## <a name="resize-a-tile"></a>Zmienianie rozmiaru kafelka

1. W okienku galerii kafelków kliknij pozycję **Wszystkie zasoby**, a następnie upuść kafelek w lewym górnym rogu obszaru roboczego nowego pulpitu nawigacyjnego.

2. Kliknij kafelek, a następnie kliknij prawym przyciskiem myszy wielokropek i wybierz polecenie **6x6**.

3. Kliknij szary narożnik w prawej dolnej części kafelka, a następnie zmień rozmiar kafelka, wybierając 3,5 punktu w pionie i 6 punktów w poziomie. Zwróć uwagę na to, że gdy upuścisz narożnik, jego rozmiar zostanie zmieniony na 4x6.

4. W galerii kafelków kliknij kafelek **Grupy zasobów** i przeciągnij go do obszaru roboczego. Umieść go pod kafelkiem **Wszystkie zasoby**.

5. W galerii kafelków kliknij kafelek **Kondycja usługi** i przeciągnij go do obszaru roboczego. Umieść go po prawej stronie kafelka **Wszystkie zasoby**.

6. Dodaj następujące kafelki i dopasuj ich rozmieszczenie:

    * Pomoc i obsługa techniczna
    * Szybkie zadania
    * Portal Marketplace
    * Co nowego

7. Po dodaniu kafelków kliknij pozycję **Zakończono dostosowywanie**. Pojawi się pulpit nawigacyjny **Pulpit nawigacyjny klienta**.

## <a name="clone-a-dashboard"></a>Klonowanie pulpitu nawigacyjnego

Teraz utworzysz bardzo podobny pulpit nawigacyjny dla innych klientów.

1. Kliknij przycisk **Klonuj**.

2. Zmień nazwę pulpitu nawigacyjnego z **Klon Pulpit nawigacyjny klienta** na **Pulpit nawigacyjny administratora usługi Azure AD**.

3. Na kafelku **Grupy zasobów** kliknij ikonę kosza, aby usunąć kafelek.

4. Dodaj następujące kafelki z galerii:

    * Tożsamość organizacji
    * Użytkownicy i grupy
    * Podsumowanie działań użytkownika
    * Witamy w centrum administracyjnym usługi Azure AD

5. Dostosuj położenie tych kafelków, a następnie kliknij pozycję **Zakończono dostosowywanie**.

## <a name="share-a-dashboard"></a>Udostępnianie pulpitu nawigacyjnego

Teraz warto udostępnić ten pulpit nawigacyjny innym użytkownikom. Aby to zrobić, wykonaj następujące czynności:

1. Upewnij się, że jest wybrany pulpit nawigacyjny administratora usługi Azure AD, a następnie kliknij pozycję **Udostępnij**.

2. W bloku **Udostępnianie i kontrola dostępu** upewnij się, że zaznaczono opcję **Opublikuj w grupie zasobów „pulpity nawigacyjne”**.

3. W polu **Lokalizacja** wybierz wartość odpowiadającą swojej lokalizacji geograficznej. Zwykle jest to najbliższe centrum danych.

4. Kliknij pozycję **Opublikuj**, a następnie zamknij blok **Udostępnianie i kontrola dostępu**.

5. Kliknij pozycję **Pulpit nawigacyjny administratora usługi Azure AD** i wybierz pozycję **Pulpit nawigacyjny klienta**.

6. Zwróć uwagę, że na kafelku **Wszystkie zasoby** pojawił się zasób udostępnionego pulpitu nawigacyjnego, a na kafelku **Grupy zasobów** pojawiła się grupa zasobów pulpitów nawigacyjnych.

7. Powtórz kroki od 1 do 3, aby udostępnić pulpit nawigacyjny klienta.

## <a name="edit-a-dashboard-file"></a>Edytowanie pliku pulpitu nawigacyjnego

Aby pobrać i zmodyfikować plik pulpitu nawigacyjnego, wykonaj następujące czynności:

1. Kliknij pozycję **Pobierz**.

2. Otwórz Eksploratora Windows i przejdź do folderu Pobrane.

3. Znajdź plik **Pulpit nawigacyjny klienta.json** i kliknij go dwukrotnie.

4. W edytorze plików wyszukaj tekst „ClockPart”.

5. Przy pierwszym wystąpieniu tekstu ClockPart zmień wartość elementu rowSpan na 1.

6. Przy drugim wystąpieniu tekstu ClockPart również zmień wartość elementu rowSpan na 1.

7. Przy drugim wystąpieniu tekstu ClockPart zmień wartość elementu Y z 2 na 1.

8. Zapisz plik Pulpit nawigacyjny klienta.json, a następnie zamknij edytor kodu.

9. Na pulpicie nawigacyjnym platformy Azure kliknij pozycję **Przekaż**.

10. W oknie dialogowym **Otwieranie** przejdź do folderu Pobrane, a następnie kliknij dwukrotnie plik **Pulpit nawigacyjny klienta.json**.

11. Zwróć uwagę, że rozmiar zegarów jest równy wysokości jednego wiersza, a dolny zegar został przesunięty w górę o jeden wiersz.

## <a name="select-a-shared-dashboard"></a>Wybieranie udostępnionego pulpitu nawigacyjnego

Załóżmy, że nie podobają Ci się mniejsze zegary i chcesz używać wcześniejszej wersji udostępnionego pulpitu nawigacyjnego klienta. Możesz to zrobić, edytując plik i przekazując go ponownie lub korzystając z udostępnionej wersji. W tym celu wykonaj następujące czynności:

1. Kliknij strzałkę w dół obok pozycji **Pulpit nawigacyjny klienta**.

2. Kliknij pozycję **Przeglądaj wszystkie pulpity nawigacyjne**.

3. W bloku **Wszystkie pulpity nawigacyjne** w obszarze **TYP** wybierz pozycję **Udostępnione pulpity nawigacyjne**.

4. Kliknij pozycję **Pulpit nawigacyjny klienta**.

5. Zamknij blok **Wszystkie pulpity nawigacyjne**.

6. Zwróć uwagę na zmianę wyglądu zegarów — powróciły one do swego pierwotnego rozmiaru.

## <a name="switch-to-full-screen"></a>Wyświetlanie na pełnym ekranie

1. Kliknij strzałkę w dół obok pozycji **Pulpit nawigacyjny klienta**. Widać jeszcze jeden pulpit nawigacyjny klienta bez wyświetlanego symbolu udostępniania. Gdy klikniesz tę wersję pulpitu nawigacyjnego klienta, zegary znów zostaną pomniejszone.

2. Przełącz się z powrotem do udostępnionego pulpitu nawigacyjnego klienta.

3. Kliknij przycisk **Pełny ekran**. Zwróć uwagę, że nie widać menu przeglądarki ani pasków.

4. Kliknij pozycję **Zamknij widok pełnoekranowy**, aby powrócić do normalnego ekranu.

## <a name="unshare-a-dashboard"></a>Anulowanie udostępniania pulpitu nawigacyjnego

Możesz anulować udostępnianie pulpitu nawigacyjnego, aby uniemożliwić jego wybieranie. Aby to zrobić, wykonaj następujące czynności:

1. Kliknij przycisk **Anuluj udostępnianie**. Zostanie wyświetlony blok **Udostępnianie i kontrola dostępu**.

2. Kliknij przycisk **Cofnij publikowanie**.

3. W oknie z komunikatem potwierdzającym kliknij przycisk **OK**.

4. Kliknij strzałkę w dół obok pozycji **Pulpit nawigacyjny klienta**.

5. Kliknij pozycję **Przeglądaj wszystkie pulpity nawigacyjne**.

6. W bloku **Wszystkie pulpity nawigacyjne** w obszarze **TYP** wybierz pozycję **Udostępnione pulpity nawigacyjne**.

7. Teraz pulpitu nawigacyjnego klienta nie ma na liście dostępnych pulpitów nawigacyjnych.

8. Zamknij blok „Wszystkie pulpity nawigacyjne”.

## <a name="delete-a-dashboard"></a>Usuwanie pulpitu nawigacyjnego

1. Upewnij się, że wybrano pulpit nawigacyjny administratora usługi Azure AD.

2. Kliknij przycisk **Usuń**.

3. W oknie komunikatu **Potwierdzenie** zaznacz pole wyboru, aby potwierdzić, że chcesz zrezygnować z wyświetlania tego pulpitu nawigacyjnego, a następnie kliknij przycisk **OK**.

## <a name="reset-a-dashboard"></a>Resetowanie pulpitu nawigacyjnego

1. Upewnij się, że wybrano pulpit nawigacyjny klienta.

2. Kliknij pozycję **Edytuj**.

3. Kliknij prawym przyciskiem myszy obszar roboczy, a następnie kliknij polecenie **Resetuj do stanu domyślnego**.

4. W oknie komunikatu **Zresetować pulpit nawigacyjny do stanu domyślnego?** kliknij przycisk **Tak**.

5. Spowoduje to zresetowanie kafelków na pulpicie nawigacyjnym klienta do wyglądu domyślnego.

6. Kliknij pozycję **Zakończono dostosowywanie**.

7. Kliknij swoją nazwę użytkownika w prawym górnym rogu portalu.

8. Kliknij pozycję Wyloguj się.

9. Zamknij przeglądarkę.

## <a name="summary"></a>Podsumowanie

Wiesz już, jak tworzyć, edytować i udostępniać pulpity nawigacyjne, zmieniać je za pośrednictwem plików JSON, anulować ich udostępnianie oraz resetować je do stanu domyślnego. Jak widać, pulpity nawigacyjne udostępniają bardzo wiele możliwości, dzięki którym można utworzyć wydajne interfejsy dla różnych ról w organizacji.