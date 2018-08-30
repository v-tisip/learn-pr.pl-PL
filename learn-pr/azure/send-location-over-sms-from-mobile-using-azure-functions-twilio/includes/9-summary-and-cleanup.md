<span data-ttu-id="72f95-101">Pomyślnie utworzono aplikację mobilną dla wielu platform przy użyciu platformy Xamarin i funkcji platformy Azure z powiązaniem usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="72f95-101">You've successfully created a cross-platform mobile app using Xamarin and an Azure function with a Twilio binding.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="72f95-102">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="72f95-102">Clean up resources</span></span>

<span data-ttu-id="72f95-103">Po zakończeniu pracy z tą aplikacją usługi Azure Functions można usunąć wszystkie zasoby utworzone w ramach tego samouczka z witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="72f95-103">When you're done working with this Azure Functions application, you can delete all resources created during the tutorial from the Azure portal.</span></span>

1. <span data-ttu-id="72f95-104">W programie Visual Studio wybierz pozycję *Widok->Cloud Explorer*.</span><span class="sxs-lookup"><span data-stu-id="72f95-104">From Visual Studio, select *View->Cloud Explorer*.</span></span>

2. <span data-ttu-id="72f95-105">Z listy rozwijanej w górnej części tego panelu wybierz pozycję *Grupy zasobów*.</span><span class="sxs-lookup"><span data-stu-id="72f95-105">From the drop-down at the top of this panel, select *Resource Groups*.</span></span>

3. <span data-ttu-id="72f95-106">Rozwiń subskrypcję, która była używana do utworzenia tej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="72f95-106">Expand the subscription that you used to create the resource group.</span></span> <span data-ttu-id="72f95-107">Kliknij prawym przyciskiem myszy grupę zasobów „ImHere”, a następnie wybierz pozycję *Otwórz w portalu*.</span><span class="sxs-lookup"><span data-stu-id="72f95-107">Right-click on the "ImHere" resource group and select *Open in Portal*.</span></span>

    ![Otwieranie grupy zasobów w portalu z okna eksploratora chmury](../media-drafts/9-open-resource-group-in-portal.png)

4. <span data-ttu-id="72f95-109">W razie potrzeby zaloguj się do witryny Azure Portal w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="72f95-109">Log into the Azure portal in your browser, if necessary.</span></span>

5. <span data-ttu-id="72f95-110">Portal otworzy się na grupie zasobów „ImHere”.</span><span class="sxs-lookup"><span data-stu-id="72f95-110">The portal will open on the "ImHere" resource group.</span></span> <span data-ttu-id="72f95-111">Kliknij przycisk **Usuń grupę zasobów**.</span><span class="sxs-lookup"><span data-stu-id="72f95-111">Click the **Delete Resource Group** button.</span></span>

    ![Usuwanie grupy zasobów](../media-drafts/9-delete-resource-group.png)

6. <span data-ttu-id="72f95-113">Wprowadź nazwę grupy zasobów, aby potwierdzić usunięcie, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="72f95-113">Enter the name of the resource group to confirm the deletion and click **Delete**.</span></span>

    ![Wprowadzanie nazwy grupy zasobów, aby potwierdzić usunięcie](../media-drafts/9-confirm-delete-resource-group.png)

## <a name="summary"></a><span data-ttu-id="72f95-115">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="72f95-115">Summary</span></span>

<span data-ttu-id="72f95-116">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="72f95-116">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="72f95-117">Tworzenia aplikacji platformy Xamarin.Forms dla wielu platform, która używa rozwiązania Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="72f95-117">Create a cross-platform Xamarin.Forms app that uses Xamarin.Essentials.</span></span>
> * <span data-ttu-id="72f95-118">Tworzenia międzyplatformowego interfejsu użytkownika przy użyciu języka XAML z logiką aplikacji w modelu ViewModel oraz tworzenia powiązania właściwości w modelu ViewModel z interfejsem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72f95-118">Create a cross-platform UI using XAML with application logic in a ViewModel, as well as bind properties in a ViewModel to the UI.</span></span>
> * <span data-ttu-id="72f95-119">Wykrywania lokalizacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72f95-119">Detect the user's location.</span></span>
> * <span data-ttu-id="72f95-120">Tworzenia funkcji platformy Azure z wyzwalaczem HTTP, a następnie uruchamianie ich lokalnie.</span><span class="sxs-lookup"><span data-stu-id="72f95-120">Create an Azure function with an HTTP trigger and run it locally.</span></span>
> * <span data-ttu-id="72f95-121">Wywoływania funkcji platformy Azure z aplikacji mobilnej z przekazywaniem danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="72f95-121">Call an Azure function from a mobile app, passing data as JSON.</span></span>
> * <span data-ttu-id="72f95-122">Tworzenia powiązania funkcji platformy Azure z usługą Twilio, aby wysłać wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="72f95-122">Bind an Azure function to Twilio to send an SMS message.</span></span>
> * <span data-ttu-id="72f95-123">Publikowania funkcji platformy Azure na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="72f95-123">Publish an Azure function to Azure.</span></span>
