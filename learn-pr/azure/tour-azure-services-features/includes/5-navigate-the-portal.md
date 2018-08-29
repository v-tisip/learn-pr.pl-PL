<span data-ttu-id="3b847-101">Produkty platformy Azure mają rozległą hierarchię.</span><span class="sxs-lookup"><span data-stu-id="3b847-101">Azure products have a deep hierarchy.</span></span> <span data-ttu-id="3b847-102">Na przykład załóżmy, że chcesz utworzyć maszynę wirtualną z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="3b847-102">For example, suppose you needed to create a Linux Virtual Machine.</span></span> <span data-ttu-id="3b847-103">Możesz przejść przez następujące poziomy: **Strona główna** **>** **Maszyny wirtualne** **>** **Obliczenia** **>** **Serwer Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="3b847-103">You might navigate through these levels: **Home** **>** **Virtual machines** **>** **Compute** **>** **Ubuntu Server**.</span></span> <span data-ttu-id="3b847-104">Witryna Azure Portal optymalizuje swój interfejs użytkownika, aby tego typu sekwencja nawigacji była intuicyjna.</span><span class="sxs-lookup"><span data-stu-id="3b847-104">The Azure portal optimizes its UI to make this type of navigation sequence intuitive.</span></span> <span data-ttu-id="3b847-105">W tym miejscu poznasz kluczowe elementy interfejsu użytkownika, które to umożliwiają.</span><span class="sxs-lookup"><span data-stu-id="3b847-105">Here, you will survey the key UI elements that make this possible.</span></span> <span data-ttu-id="3b847-106">Nauczysz się nawigować po menu i podmenu oraz znajdować i konfigurować usługi, używając bloków.</span><span class="sxs-lookup"><span data-stu-id="3b847-106">You will navigate through menus and sub-menus and use blades to find and configure services.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="3b847-107">Układ witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3b847-107">Azure Portal Layout</span></span>

<span data-ttu-id="3b847-108">Witryna Azure Portal to najważniejszy graficzny interfejs użytkownika (GUI) umożliwiający sterowanie platformą Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b847-108">The Azure portal is the main graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="3b847-109">W portalu można przeprowadzić większość akcji zarządzania. Zazwyczaj jest on również najlepszym interfejsem do wykonywania pojedynczych zadań lub miejscem, w którym można dokładnie przyjrzeć się opcjom konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3b847-109">You can carry out the large majority of management actions on the portal and the portal is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

<span data-ttu-id="3b847-110">Okienko po lewej stronie portalu to okienko zasobów, w którym jest wyświetlana lista najważniejszych typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="3b847-110">On the left-hand pane of the portal is the resource pane, which lists the main resource types.</span></span> <span data-ttu-id="3b847-111">Pamiętaj, że poza wyświetlonymi zasobami na platformie Azure znajduje się dużo więcej ich typów.</span><span class="sxs-lookup"><span data-stu-id="3b847-111">Note that Azure has far many more resource types than just those shown.</span></span>

## <a name="using-blades-in-azure-portal"></a><span data-ttu-id="3b847-112">Korzystanie z bloków w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3b847-112">Using Blades in Azure Portal</span></span>

<span data-ttu-id="3b847-113">Model nawigacji w witrynie Azure Portal jest oparty na blokach.</span><span class="sxs-lookup"><span data-stu-id="3b847-113">The Azure Portal uses a blades model for navigation.</span></span> <span data-ttu-id="3b847-114">_Blok_ to wysuwany panel zawierający interfejs użytkownika dla pojedynczego poziomu w sekwencji nawigacji.</span><span class="sxs-lookup"><span data-stu-id="3b847-114">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="3b847-115">Na przykład każdy z następujących elementów w tej sekwencji jest przedstawiany przez blok: **Maszyny wirtualne** **>** **Obliczenia** **>** **Serwer Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="3b847-115">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** **>** **Compute** **>** **Ubuntu Server**.</span></span>

<span data-ttu-id="3b847-116">Każdy blok w interfejsie użytkownika zazwyczaj zawiera szereg opcji, które można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="3b847-116">Each blade within the UI typically contains a number of configurable options.</span></span> <span data-ttu-id="3b847-117">Niektóre z tych opcji powodują wygenerowanie kolejnego bloku, który pojawia się po prawej stronie istniejącego.</span><span class="sxs-lookup"><span data-stu-id="3b847-117">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="3b847-118">W nowym bloku każda kolejna opcja, którą można konfigurować, powoduje wyświetlenie następnego bloku itd.</span><span class="sxs-lookup"><span data-stu-id="3b847-118">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="3b847-119">Dość szybko możesz skończyć z kilkoma blokami otwartymi jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="3b847-119">Pretty soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="3b847-120">Bloki można również zmaksymalizować tak, aby zajmowały cały ekran.</span><span class="sxs-lookup"><span data-stu-id="3b847-120">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="3b847-121">Gdy spróbujesz zamknąć blok bez zapisania wprowadzonych zmian konfiguracji, zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="3b847-121">If you try to close a blade without saving any configuration changes that you have made, then you will receive a prompt.</span></span>

## <a name="configuring-settings-in-azure-portal"></a><span data-ttu-id="3b847-122">Konfigurowanie ustawień w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3b847-122">Configuring Settings in Azure Portal</span></span>

<span data-ttu-id="3b847-123">W witrynie Azure Portal jest wyświetlanych kilka opcji konfiguracji, przede wszystkim na pasku stanu w prawym górnym rogu ekranu.</span><span class="sxs-lookup"><span data-stu-id="3b847-123">The Azure portal displays several configuration options, mostly in the status bar to the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="3b847-124">Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="3b847-124">Notifications</span></span>

<span data-ttu-id="3b847-125">Kliknięcie ikony dzwonka powoduje wyświetlenie okienka Powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="3b847-125">Clicking the bell icon displays the Notifications pane.</span></span> <span data-ttu-id="3b847-126">W tym okienku jest wyświetlana lista ostatnio przeprowadzonych akcji wraz z ich stanem.</span><span class="sxs-lookup"><span data-stu-id="3b847-126">This pane lists the last actions that have been carried out, along with their status.</span></span>

![Blok Powiadomienia](../images/2-notifications-blade.PNG)

### <a name="cloud-shell"></a><span data-ttu-id="3b847-128">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="3b847-128">Cloud Shell</span></span>

<span data-ttu-id="3b847-129">Kliknięcie ikony usługi Cloud Shell (>_) spowoduje utworzenie nowej sesji usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="3b847-129">If you click the Cloud Shell icon (>_), you will create a new cloud shell session.</span></span> <span data-ttu-id="3b847-130">Zostanie wyświetlony monit o użycie w tej sesji powłoki Bash systemu Linux lub powłoki PowerShell w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="3b847-130">You are prompted to use either Linux Bash or PowerShell on Linux in that session.</span></span>

![Cloud Shell](../images/2-choose-shell.PNG)

### <a name="settings"></a><span data-ttu-id="3b847-132">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="3b847-132">Settings</span></span>

<span data-ttu-id="3b847-133">Klikając ikonę „koła zębatego”, można zmienić ustawienia witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3b847-133">Clicking on the "gear" icon to change Azure Portal settings.</span></span> <span data-ttu-id="3b847-134">Do tych ustawień należą:</span><span class="sxs-lookup"><span data-stu-id="3b847-134">These settings include:</span></span>

* <span data-ttu-id="3b847-135">Godzina wylogowania</span><span class="sxs-lookup"><span data-stu-id="3b847-135">Logout time</span></span>
* <span data-ttu-id="3b847-136">Schemat kolorów</span><span class="sxs-lookup"><span data-stu-id="3b847-136">Color scheme</span></span>
* <span data-ttu-id="3b847-137">Motywy o wysokim kontraście</span><span class="sxs-lookup"><span data-stu-id="3b847-137">High contrast themes</span></span>
* <span data-ttu-id="3b847-138">Powiadomienia wyskakujące (na urządzenie przenośne)</span><span class="sxs-lookup"><span data-stu-id="3b847-138">Toast notifications (to a mobile device)</span></span>
* <span data-ttu-id="3b847-139">Dwukrotne kliknięcie w celu zmiany motywu</span><span class="sxs-lookup"><span data-stu-id="3b847-139">Double-click to change theme</span></span>
* <span data-ttu-id="3b847-140">Język</span><span class="sxs-lookup"><span data-stu-id="3b847-140">Language</span></span>
* <span data-ttu-id="3b847-141">Format regionalny</span><span class="sxs-lookup"><span data-stu-id="3b847-141">Regional format</span></span>

![Ustawienia portalu](../images/2-settings-blade.PNG)

<span data-ttu-id="3b847-143">Po zmianie ustawień kliknij przycisk **Zastosuj**, aby zaakceptować zmiany.</span><span class="sxs-lookup"><span data-stu-id="3b847-143">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="3b847-144">Blok Opinia</span><span class="sxs-lookup"><span data-stu-id="3b847-144">Feedback Blade</span></span>

<span data-ttu-id="3b847-145">Ikona uśmiechniętej buźki powoduje otwarcie bloku **Wyślij do nas swoją opinię**.</span><span class="sxs-lookup"><span data-stu-id="3b847-145">The smiley face icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="3b847-146">W tym miejscu możesz wysłać do firmy Microsoft opinię na temat platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3b847-146">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="3b847-147">Pamiętaj, że możesz zdecydować, czy firma Microsoft będzie mogła odpowiedzieć na Twoją opinię za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="3b847-147">Note that you can specify whether Microsoft can respond to your feedback by email.</span></span>

![Opinia](../images/2-feedback-blade.PNG)

### <a name="help-blade"></a><span data-ttu-id="3b847-149">Blok Pomoc</span><span class="sxs-lookup"><span data-stu-id="3b847-149">Help Blade</span></span>

<span data-ttu-id="3b847-150">Kliknij znak zapytania, aby wyświetlić blok **Pomoc**.</span><span class="sxs-lookup"><span data-stu-id="3b847-150">Click the question mark to show the **Help** blade.</span></span> <span data-ttu-id="3b847-151">W tym miejscu możesz wybrać kilka tematów, takich jak:</span><span class="sxs-lookup"><span data-stu-id="3b847-151">Here you choose from a number of topics, including:</span></span>

* <span data-ttu-id="3b847-152">Co nowego</span><span class="sxs-lookup"><span data-stu-id="3b847-152">What's new</span></span>
* <span data-ttu-id="3b847-153">Harmonogram działania dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b847-153">Azure roadmap</span></span>
* <span data-ttu-id="3b847-154">Uruchom przewodnik</span><span class="sxs-lookup"><span data-stu-id="3b847-154">Launch guided tour</span></span>
* <span data-ttu-id="3b847-155">Skróty klawiaturowe</span><span class="sxs-lookup"><span data-stu-id="3b847-155">Keyboard shortcuts</span></span>
* <span data-ttu-id="3b847-156">Pokaż dane diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="3b847-156">Show diagnostics</span></span>
* <span data-ttu-id="3b847-157">Zasady ochrony prywatności i warunki</span><span class="sxs-lookup"><span data-stu-id="3b847-157">Privacy + terms</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="3b847-158">Katalog i subskrypcja</span><span class="sxs-lookup"><span data-stu-id="3b847-158">Directory and Subscription</span></span>

<span data-ttu-id="3b847-159">Kliknij ikonę Książka i filtr, aby wyświetlić blok **Katalog i subskrypcja**.</span><span class="sxs-lookup"><span data-stu-id="3b847-159">Click the Book and Filter icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="3b847-160">Na platformie Azure możesz mieć więcej niż jedną subskrypcję skojarzoną z jednym katalogiem.</span><span class="sxs-lookup"><span data-stu-id="3b847-160">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="3b847-161">W bloku Katalog i subskrypcja możesz zmieniać subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="3b847-161">In the Directory and Subscription blade, you can change between subscriptions.</span></span> <span data-ttu-id="3b847-162">W tym miejscu możesz zmienić swoją subskrypcję lub przejść do innego katalogu.</span><span class="sxs-lookup"><span data-stu-id="3b847-162">Here, you can change your subscription, or change to another directory.</span></span>

![Katalog](../images/2-directory-blade-1.PNG)

### <a name="profile-settings"></a><span data-ttu-id="3b847-164">Ustawienia profilu</span><span class="sxs-lookup"><span data-stu-id="3b847-164">Profile Settings</span></span>

<span data-ttu-id="3b847-165">Klikając swoją nazwę w prawym górnym rogu, możesz zmienić ustawienia profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3b847-165">If you click on your name in the top right-hand corner, you can then change your profile settings.</span></span>
<span data-ttu-id="3b847-166">Dostępne są następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="3b847-166">Options include:</span></span>

* <span data-ttu-id="3b847-167">Wyloguj się z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b847-167">Sign out of Azure</span></span>
* <span data-ttu-id="3b847-168">Zmień hasło</span><span class="sxs-lookup"><span data-stu-id="3b847-168">Change password</span></span>
* <span data-ttu-id="3b847-169">Zmień informacje kontaktowe</span><span class="sxs-lookup"><span data-stu-id="3b847-169">Change contact information</span></span>
* <span data-ttu-id="3b847-170">Wyświetl uprawnienia</span><span class="sxs-lookup"><span data-stu-id="3b847-170">View permissions</span></span>
* <span data-ttu-id="3b847-171">Prześlij pomysł do zespołu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b847-171">Submit an idea to the Azure team</span></span>
* <span data-ttu-id="3b847-172">Wyświetl rachunek</span><span class="sxs-lookup"><span data-stu-id="3b847-172">View your bill</span></span>
* <span data-ttu-id="3b847-173">Przełącz katalog (powoduje wyświetlenie bloku Katalog i subskrypcja, jak w poprzedniej sekcji)</span><span class="sxs-lookup"><span data-stu-id="3b847-173">Switch directory (shows the Directory + Subscription blade as in the previous section)</span></span>

![Ustawienia profilu](../images/2-portal-menu.png)

<span data-ttu-id="3b847-175">Jeśli teraz klikniesz pozycję **Wyświetl mój rachunek**, platforma Azure przeniesie Cię na stronę **Zarządzanie kosztami i rozliczenia — faktury**, gdzie można przeanalizować miejsca generowania kosztów przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="3b847-175">If you now click **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

![Strona rozliczeń](../images/2-portal-billing.PNG)

## <a name="summary"></a><span data-ttu-id="3b847-177">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3b847-177">Summary</span></span>

<span data-ttu-id="3b847-178">Platforma Azure to duży produkt, a interfejs użytkownika portalu odzwierciedla ten fakt.</span><span class="sxs-lookup"><span data-stu-id="3b847-178">Azure is a large product and the portal UI reflects this.</span></span> <span data-ttu-id="3b847-179">Podstawowym sposobem, w jaki portal ułatwia nawigowanie po tym złożonym systemie, są bloki wskazujące hierarchię.</span><span class="sxs-lookup"><span data-stu-id="3b847-179">The primary way that the portal helps you navigate this complexity is with blades to indicate hierarchy.</span></span> <span data-ttu-id="3b847-180">Bloki pozwalają skupić się na określonym zadaniu, wyraźnie pokazując ścieżkę prowadzącą do tego punktu.</span><span class="sxs-lookup"><span data-stu-id="3b847-180">Blades let you focus on a specific task while clearly indicating the path you took to reach that point.</span></span>