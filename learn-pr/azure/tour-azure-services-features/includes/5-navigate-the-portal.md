Produkty platformy Azure mają rozległą hierarchię. Na przykład załóżmy, że chcesz utworzyć maszynę wirtualną z systemem Linux. Możesz przejść przez następujące poziomy: **Strona główna** **>** **Maszyny wirtualne** **>** **Obliczenia** **>** **Serwer Ubuntu**. Witryna Azure Portal optymalizuje swój interfejs użytkownika, aby tego typu sekwencja nawigacji była intuicyjna. W tym miejscu poznasz kluczowe elementy interfejsu użytkownika, które to umożliwiają. Nauczysz się nawigować po menu i podmenu oraz znajdować i konfigurować usługi, używając bloków.

## <a name="azure-portal-layout"></a>Układ witryny Azure Portal

Witryna Azure Portal to najważniejszy graficzny interfejs użytkownika (GUI) umożliwiający sterowanie platformą Microsoft Azure. W portalu można przeprowadzić większość akcji zarządzania. Zazwyczaj jest on również najlepszym interfejsem do wykonywania pojedynczych zadań lub miejscem, w którym można dokładnie przyjrzeć się opcjom konfiguracji.

Okienko po lewej stronie portalu to okienko zasobów, w którym jest wyświetlana lista najważniejszych typów zasobów. Pamiętaj, że poza wyświetlonymi zasobami na platformie Azure znajduje się dużo więcej ich typów.

## <a name="using-blades-in-azure-portal"></a>Korzystanie z bloków w witrynie Azure Portal

Model nawigacji w witrynie Azure Portal jest oparty na blokach. _Blok_ to wysuwany panel zawierający interfejs użytkownika dla pojedynczego poziomu w sekwencji nawigacji. Na przykład każdy z następujących elementów w tej sekwencji jest przedstawiany przez blok: **Maszyny wirtualne** **>** **Obliczenia** **>** **Serwer Ubuntu**.

Każdy blok w interfejsie użytkownika zazwyczaj zawiera szereg opcji, które można konfigurować. Niektóre z tych opcji powodują wygenerowanie kolejnego bloku, który pojawia się po prawej stronie istniejącego. W nowym bloku każda kolejna opcja, którą można konfigurować, powoduje wyświetlenie następnego bloku itd. Dość szybko możesz skończyć z kilkoma blokami otwartymi jednocześnie. Bloki można również zmaksymalizować tak, aby zajmowały cały ekran.

Gdy spróbujesz zamknąć blok bez zapisania wprowadzonych zmian konfiguracji, zostanie wyświetlony monit.

## <a name="configuring-settings-in-azure-portal"></a>Konfigurowanie ustawień w witrynie Azure Portal

W witrynie Azure Portal jest wyświetlanych kilka opcji konfiguracji, przede wszystkim na pasku stanu w prawym górnym rogu ekranu.

### <a name="notifications"></a>Powiadomienia

Kliknięcie ikony dzwonka powoduje wyświetlenie okienka Powiadomienia. W tym okienku jest wyświetlana lista ostatnio przeprowadzonych akcji wraz z ich stanem.

![Blok Powiadomienia](../images/2-notifications-blade.PNG)

### <a name="cloud-shell"></a>Cloud Shell

Kliknięcie ikony usługi Cloud Shell (>_) spowoduje utworzenie nowej sesji usługi Cloud Shell. Zostanie wyświetlony monit o użycie w tej sesji powłoki Bash systemu Linux lub powłoki PowerShell w systemie Linux.

![Cloud Shell](../images/2-choose-shell.PNG)

### <a name="settings"></a>Ustawienia

Klikając ikonę „koła zębatego”, można zmienić ustawienia witryny Azure Portal. Do tych ustawień należą:

* Godzina wylogowania
* Schemat kolorów
* Motywy o wysokim kontraście
* Powiadomienia wyskakujące (na urządzenie przenośne)
* Dwukrotne kliknięcie w celu zmiany motywu
* Język
* Format regionalny

![Ustawienia portalu](../images/2-settings-blade.PNG)

Po zmianie ustawień kliknij przycisk **Zastosuj**, aby zaakceptować zmiany.

### <a name="feedback-blade"></a>Blok Opinia

Ikona uśmiechniętej buźki powoduje otwarcie bloku **Wyślij do nas swoją opinię**. W tym miejscu możesz wysłać do firmy Microsoft opinię na temat platformy Azure. Pamiętaj, że możesz zdecydować, czy firma Microsoft będzie mogła odpowiedzieć na Twoją opinię za pośrednictwem poczty e-mail.

![Opinia](../images/2-feedback-blade.PNG)

### <a name="help-blade"></a>Blok Pomoc

Kliknij znak zapytania, aby wyświetlić blok **Pomoc**. W tym miejscu możesz wybrać kilka tematów, takich jak:

* Co nowego
* Harmonogram działania dla platformy Azure
* Uruchom przewodnik
* Skróty klawiaturowe
* Pokaż dane diagnostyczne
* Zasady ochrony prywatności i warunki

### <a name="directory-and-subscription"></a>Katalog i subskrypcja

Kliknij ikonę Książka i filtr, aby wyświetlić blok **Katalog i subskrypcja**.

Na platformie Azure możesz mieć więcej niż jedną subskrypcję skojarzoną z jednym katalogiem. W bloku Katalog i subskrypcja możesz zmieniać subskrypcje. W tym miejscu możesz zmienić swoją subskrypcję lub przejść do innego katalogu.

![Katalog](../images/2-directory-blade-1.PNG)

### <a name="profile-settings"></a>Ustawienia profilu

Klikając swoją nazwę w prawym górnym rogu, możesz zmienić ustawienia profilu użytkownika.
Dostępne są następujące opcje:

* Wyloguj się z platformy Azure
* Zmień hasło
* Zmień informacje kontaktowe
* Wyświetl uprawnienia
* Prześlij pomysł do zespołu platformy Azure
* Wyświetl rachunek
* Przełącz katalog (powoduje wyświetlenie bloku Katalog i subskrypcja, jak w poprzedniej sekcji)

![Ustawienia profilu](../images/2-portal-menu.png)

Jeśli teraz klikniesz pozycję **Wyświetl mój rachunek**, platforma Azure przeniesie Cię na stronę **Zarządzanie kosztami i rozliczenia — faktury**, gdzie można przeanalizować miejsca generowania kosztów przez platformę Azure.

![Strona rozliczeń](../images/2-portal-billing.PNG)

## <a name="summary"></a>Podsumowanie

Platforma Azure to duży produkt, a interfejs użytkownika portalu odzwierciedla ten fakt. Podstawowym sposobem, w jaki portal ułatwia nawigowanie po tym złożonym systemie, są bloki wskazujące hierarchię. Bloki pozwalają skupić się na określonym zadaniu, wyraźnie pokazując ścieżkę prowadzącą do tego punktu.