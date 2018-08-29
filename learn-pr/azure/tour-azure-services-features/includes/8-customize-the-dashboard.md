W tym miejscu możesz tworzyć i modyfikować pulpity nawigacyjne, korzystając z interfejsu użytkownika portalu lub bezpośrednio edytując bazowy plik JSON.

## <a name="what-is-a-dashboard"></a>Co to jest pulpit nawigacyjny?

_Pulpit nawigacyjny_ jest konfigurowalną kolekcją kafelków interfejsu użytkownika, wyświetlaną w witrynie Azure Portal. Możesz dodawać, usuwać i rozmieszczać kafelki, aby utworzyć odpowiedni widok, a następnie zapisać ten widok jako pulpit nawigacyjny. Możesz korzystać z wielu pulpitów nawigacyjnych, przełączając się między nimi zgodnie z potrzebami. Możesz nawet udostępniać pulpity nawigacyjne innym członkom zespołu.

Pulpity nawigacyjne pozwalają bardzo elastycznie zarządzać platformą Azure. Możesz utworzyć pulpity nawigacyjne dla określonych ról w organizacji, a następnie sterować dostępem do poszczególnych pulpitów za pomocą kontroli dostępu opartej na rolach (RBAC). Na przykład administrator bazy danych ma pulpit nawigacyjny zawierający widoki usługi SQL Database, a administrator usługi Azure Active Directory korzysta z widoków użytkowników i grup w usłudze Azure AD.

Pulpity nawigacyjne są przechowywane jako pliki w formacie JavaScript Object Notation (JSON). Dzięki temu można je przekazywać i pobierać na inne komputery oraz udostępniać członkom katalogu platformy Azure. Platforma Azure przechowuje pulpity nawigacyjne w grupach zasobów — podobnie jak maszyny wirtualne lub konta magazynu, którymi można zarządzać w portalu.

Pulpity nawigacyjne są plikami w formacie JSON, dlatego można również dostosowywać je programowo, dzięki czemu mogą służyć jako zaawansowane narzędzia administracyjne. Ponadto niektóre typy kafelków mogą korzystać z zapytań i aktualizować się automatycznie po zmianie danych źródłowych.

## <a name="default-dashboard"></a>Domyślny pulpit nawigacyjny

Domyślny pulpit nawigacyjny nazywa się po prostu Pulpit nawigacyjny. Widać go po zalogowaniu się w portalu — zawiera pięć składników Web Part.

![Domyślne składniki Web Part](../images/4-dashboard-default-webparts.png)

Oto domyślne składniki Web Part:

1. Wszystkie zasoby
2. Przewodniki Szybki Start i samouczki
3. Service Health
4. Portal Marketplace
5. Wprowadzenie do platformy Azure

## <a name="creating-and-managing-dashboards"></a>Tworzenie pulpitów nawigacyjnych i zarządzanie nimi

W górnej części pulpitu nawigacyjnego są widoczne kontrolki, które umożliwiają tworzenie, przekazywanie, pobieranie, edytowanie i udostępnianie pulpitów nawigacyjnych. Można również sklonować i usunąć pulpit nawigacyjny, a także wyświetlić go na pełnym ekranie.

![Dostosowywanie kontrolek pulpitu nawigacyjnego](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a>Wybieranie pulpitu nawigacyjnego

Po lewej stronie jest wyświetlana kontrolka listy rozwijanej Wybierz pulpit nawigacyjny. Kliknięcie tej kontrolki pozwala wybrać pulpit nawigacyjny z zestawu pulpitów zdefiniowanych na koncie. Dzięki tej kontrolce możesz łatwo zdefiniować wiele pulpitów nawigacyjnych przeznaczonych do różnych celów, a następnie w prosty sposób przełączać się między nimi, aby wykonać określone zadanie.

Pamiętaj o tym, że wszystkie utworzone pulpity nawigacyjne są prywatne i dostępne tylko dla Ciebie. Aby upublicznić pulpit nawigacyjny w przedsiębiorstwie, musisz go udostępnić. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą udostępniania/anulowania udostępniania pulpitów nawigacyjnych w dalszej części tego modułu.

### <a name="create-a-new-dashboard"></a>Tworzenie nowego pulpitu nawigacyjnego

Aby utworzyć nowy pulpit nawigacyjny, po prostu kliknij pozycję **Nowy pulpit nawigacyjny**. Pojawi się obszar roboczy pulpitu nawigacyjnego bez kafelków. Możesz teraz dodać kafelki, co zostało szczegółowo opisane w sekcji Edytowanie pulpitu nawigacyjnego za pomocą interfejsu użytkownika w dalszej części tego modułu. Gdy skończysz dodawać i dostosowywać kafelki, zmień nazwę pulpitu nawigacyjnego. Następnie kliknij pozycję **Zakończono dostosowywanie**, aby zapisać pulpit nawigacyjny i przełączyć się do niego.

### <a name="upload-and-download"></a>Przekazywanie i pobieranie

Przyciski **Przekaż** i **Pobierz** umożliwiają pobranie bieżącego pulpitu nawigacyjnego jako pliku JSON i dostosowanie go, a następnie rozpowszechnienie go i przekazanie z powrotem. Inne osoby również mogą przekazać ten plik do witryny Azure Portal, aby zastąpić swój bieżący pulpit nawigacyjny.

Po kliknięciu przycisku **Pobierz** bieżący pulpit nawigacyjny zostanie pobrany do domyślnego folderu Pobrane. Aby wyświetlić kod JSON, otwórz pobrany plik.

![Kod JSON pulpitu nawigacyjnego](../images/7-dashboard-json-code.PNG)

Kod możesz edytować ręcznie, aby na przykład zmienić rozmiary kafelków, a następnie przekazać go ponownie na platformę Azure, klikając przycisk **Przekaż**.

### <a name="edit-a-dashboard"></a>Edytowanie pulpitu nawigacyjnego

Aby uzyskać więcej informacji, zobacz temat Edytowanie pulpitu nawigacyjnego za pomocą interfejsu użytkownika.

### <a name="shareunshare-a-dashboard"></a>Udostępnianie/anulowanie udostępniania pulpitu nawigacyjnego

Nowy zdefiniowany pulpit nawigacyjny jest prywatny i widoczny tylko na Twoim koncie. Aby pulpit nawigacyjny stał się widoczny dla innych użytkowników, musisz go udostępnić. Jednak podobnie jak w przypadku innych zasobów platformy Azure, musisz określić grupę zasobów (lub użyć istniejącej grupy zasobów), w której będą przechowywane udostępnione pulpity nawigacyjne. Jeśli nie masz takiej grupy, platforma Azure utworzy grupę zasobów „pulpity nawigacyjne” we wskazanej przez Ciebie lokalizacji. Jeśli masz grupę zasobów, możesz przechowywać w niej pulpity nawigacyjne.

![Udostępnianie i kontrola dostępu 1](../images/7-share-dashboards-default.PNG)

Po udostępnieniu szablonu pojawi się drugi blok **Udostępnianie i kontrola dostępu**.

![Udostępnianie i kontrola dostępu 2](../images/7-share-dashboards-access-control.PNG)

Po kliknięciu pozycji **Zarządzaj użytkownikami** możesz określić, którzy użytkownicy mają dostęp do tego pulpitu nawigacyjnego.

### <a name="switching-to-a-shared-dashboard"></a>Przełączanie się do udostępnionego pulpitu nawigacyjnego

Aby przełączyć się do udostępnionego pulpitu nawigacyjnego, kliknij listę pulpitów nawigacyjnych, a następnie kliknij pozycję **Przeglądaj wszystkie pulpity nawigacyjne**.

![Przeglądanie wszystkich pulpitów nawigacyjnych](../images/7-browse-dashboards.PNG)

Pojawi się blok Wszystkie pulpity nawigacyjne z wyświetlonymi nazwami wszystkich udostępnionych pulpitów nawigacyjnych. Aby zastosować dany pulpit nawigacyjny w witrynie Azure Portal, po prostu go kliknij.

![Udostępnione pulpity nawigacyjne](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a>Wyświetlanie pulpitu nawigacyjnego na pełnym ekranie

Jeśli chcesz zmaksymalizować powierzchnię pulpitu nawigacyjnego, kliknij przycisk **Pełny ekran**, aby wyświetlić bieżący pulpit nawigacyjny bez żadnych menu przeglądarki. Jeśli jakieś kafelki wykraczają poza granice ekranu, w jego prawej i dolnej części pojawią się suwaki.

Po zakończeniu pracy w trybie pełnoekranowym naciśnij klawisz Escape lub kliknij przycisk **Zamknij widok pełnoekranowy** widoczny obok nazwy pulpitu nawigacyjnego w górnej części ekranu.

### <a name="clone-a-dashboard"></a>Klonowanie pulpitu nawigacyjnego

Sklonowanie pulpitu nawigacyjnego powoduje po prostu utworzenie jego kopii o nazwie „Klon (nazwa pulpitu nawigacyjnego)” i wybranie jej jako bieżącego pulpitu nawigacyjnego. Klonowanie pozwala również łatwo tworzyć pulpity nawigacyjne, które mają zostać udostępnione. Jeśli na przykład wygląd jakiegoś pulpitu nawigacyjnego w dużej części spełnia Twoje wymagania, po prostu go sklonuj, wprowadź odpowiednie zmiany, a następnie udostępnij ten pulpit.

### <a name="delete-a-dashboard"></a>Usuwanie pulpitu nawigacyjnego

Usunięcie pulpitu nawigacyjnego powoduje, że nie widać go na liście dostępnych pulpitów nawigacyjnych. Pojawi się monit o potwierdzenie usunięcia pulpitu nawigacyjnego. Nie ma możliwości odzyskania usuniętego pulpitu nawigacyjnego.

## <a name="edit-a-dashboard-through-the-user-interface"></a>Edytowanie pulpitu nawigacyjnego za pomocą interfejsu użytkownika

Chociaż pulpit nawigacyjny można edytować, pobierając plik JSON, zmieniając wartości w tym pliku i przekazując go z powrotem na platformę Azure, taka metoda projektowania interfejsu użytkownika nie jest bardzo intuicyjna. Aby skonfigurować bieżący pulpit nawigacyjny przy użyciu graficznego interfejsu użytkownika, kliknij przycisk **Edytuj** lub kliknij prawym przyciskiem myszy pulpit nawigacyjny i wybierz polecenie **Edytuj**. Pulpit nawigacyjny zostanie przełączony do trybu edycji.

![Edytowanie pulpitu nawigacyjnego](../images/7-edit-dashboard.PNG)

Po lewej stronie pojawi się galeria kafelków z liczbą kafelków widoczną w dolnej części. Galerię kafelków można odfiltrować według następujących kryteriów:

* Ogólne
* Typ
* Wyszukiwanie
* Grupa zasobów
* Tag

![Galeria kafelków](../images/7-tile-gallery.png)

Poszczególne opcje możesz dodatkowo doprecyzować, wybierając kategorię, na przykład Azure Active Directory, Internet of Things, Microsoft Intune itd.

Dodawanie kafelków polega po prostu na wybraniu kafelka z listy po lewej stronie, a następnie przeciągnięciu go i upuszczeniu w obszarze roboczym. Następnie możesz dostosować położenie i rozmiar kafelka lub zmienić wyświetlane dane.

Obszar roboczy w trybie edycji jest podzielony na kwadraty. Każdy kafelek musi znajdować się w co najmniej jednym kwadracie. Kafelki są przyciągane do najbliższego największego zestawu separatorów kafelków. Kafelki, które się nakładają, są przenoszone. Zmniejszenie kafelka powoduje, że układ otaczających go kafelków też się zmieni.

### <a name="change-tile-sizes"></a>Zmienianie rozmiarów kafelków

Rozmiar niektórych kafelków jest stały i możesz go zmienić tylko programowo. Jednak kafelki z szarym narożnikiem w prawej dolnej części możesz edytować, przeciągając i upuszczając wskaźnik narożnika.

![Kafelek o zmiennym rozmiarze](../images/7-resizable-tile.png)

Możesz również kliknąć prawym przyciskiem myszy menu kontekstowe i określić rozmiar.

![Rozmiar kafelka](../images/7-tile-size.png)

Aby utworzyć pulpit nawigacyjny, po prostu przeciągnij kafelki z galerii kafelków do obszaru roboczego i dostosuj ich położenie.

### <a name="change-tile-settings"></a>Zmienianie ustawień kafelków

Ustawienia niektórych kafelków można edytować. Na przykład po przeciągnięciu kafelka zegara do obszaru roboczego jest otwierany kafelek **Edytuj zegar**. Możesz wtedy ustawić strefę czasową i format wyświetlania— 12- lub 24-godzinny.

![Edytowanie zegara](../images/7-edit-clock.png)

W przypadku wielonarodowych lub transkontynentalnych przedsiębiorstw możesz dodać kolejne zegary z różnymi strefami czasowymi.

### <a name="accepting-your-edits"></a>Akceptowanie zmian

Gdy rozmieścisz kafelki w odpowiedni sposób, kliknij przycisk **Zakończono dostosowywanie** lub kliknij prawym przyciskiem myszy i wybierz polecenie **Zakończono dostosowywanie**.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>Edytowanie pulpitu nawigacyjnego za pomocą pliku JSON

Możesz również zmodyfikować pulpit nawigacyjny, zmieniając plik JSON. Ta metoda umożliwia zmianę ustawień w szerszym zakresie, ale zmiany są widoczne dopiero po przekazaniu pliku z powrotem na platformę Azure.

![Ustawienia JSON](../images/7-json-code.png)

Aby w powyższym przykładzie zmienić rozmiar kafelka, zmodyfikuj zmienne colSpan i rowSpan, a następnie zapisz plik i przekaż go na platformę Azure. Możesz również rozpowszechnić plik wśród innych użytkowników.

## <a name="reset-a-dashboard"></a>Resetowanie pulpitu nawigacyjnego

Dowolny pulpit nawigacyjny możesz zresetować do domyślnego stylu. W trybie edycji kliknij prawym przyciskiem myszy i wybierz polecenie **Resetuj do stanu domyślnego**. Pojawi się okno dialogowe z monitem o potwierdzenie zresetowania pulpitu nawigacyjnego.

## <a name="summary"></a>Podsumowanie

Pulpity nawigacyjne są elastycznym narzędziem do zarządzania różnymi aspektami usług platformy Azure za pośrednictwem portalu. Ułatwiają one monitorowanie stanu usług. Możliwość ich udostępniania pomaga zagwarantować, że wszyscy członkowie zespołu mają dostęp do tych samych danych oraz stały wgląd w stan krytycznych składników.