<span data-ttu-id="76486-101">W tym momencie aplikacja mobilna jest prostą aplikacją „Witaj świecie”.</span><span class="sxs-lookup"><span data-stu-id="76486-101">At this point, the mobile app is a simple "Hello World" app.</span></span> <span data-ttu-id="76486-102">W tym module dodasz interfejs użytkownika i niektóre elementy podstawowej logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76486-102">In this unit, you add the UI and some basic application logic.</span></span>

<span data-ttu-id="76486-103">Interfejs użytkownika dla aplikacji będzie się składać z:</span><span class="sxs-lookup"><span data-stu-id="76486-103">The UI for the app will consist of:</span></span>

* <span data-ttu-id="76486-104">Kontrolki wprowadzania tekstu umożliwiającej wprowadzenie niektórych numerów telefonów.</span><span class="sxs-lookup"><span data-stu-id="76486-104">A text-entry control to enter some phone numbers.</span></span>
* <span data-ttu-id="76486-105">Przycisku do wysyłania swojej lokalizacji na te numery przy użyciu funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="76486-105">A button to send your location to those numbers using an Azure function.</span></span>
* <span data-ttu-id="76486-106">Etykiety, która wyświetli użytkownikowi komunikat o bieżącym stanie, taki jak o wysyłaniu lokalizacji i pomyślnym wysyłaniu lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="76486-106">A label that will show a message to the user of the current status, such as the location being sent and location sent successfully.</span></span>

<span data-ttu-id="76486-107">Program Xamarin.Forms obsługuje wzorzec projektowania o nazwie Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="76486-107">Xamarin.Forms supports a design pattern called Model-View-ViewModel (MVVM).</span></span> <span data-ttu-id="76486-108">Więcej o MVVM możesz dowiedzieć się w [dokumentacji Xamarin MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), ale kluczową jego cechą jest to, że każda strona (widok) ma model ViewModel, który udostępnia właściwości i zachowanie.</span><span class="sxs-lookup"><span data-stu-id="76486-108">You can read more about MVVM in the [Xamarin MVVM docs](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), but the essence of it is, each page (View) has a ViewModel that exposes properties and behavior.</span></span>

<span data-ttu-id="76486-109">Właściwości modelu ViewModel są „powiązane” ze składnikami interfejsu użytkownika według nazwy, a to powiązanie synchronizuje dane między widokiem a modelem ViewModel.</span><span class="sxs-lookup"><span data-stu-id="76486-109">ViewModel properties are 'bound' to components on the UI by name, and this binding synchronizes data between the View and ViewModel.</span></span> <span data-ttu-id="76486-110">Na przykład właściwość `string` modelu ViewModel o nazwie `Name` może być powiązana z właściwością `Text` kontrolki wprowadzania tekstu w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="76486-110">For example, a `string` property on a ViewModel called `Name` could be bound to the `Text` property of a text-entry control on the UI.</span></span> <span data-ttu-id="76486-111">Kontrolka wprowadzania tekstu wyświetla wartości we właściwości `Name` oraz, jeśli użytkownik zmieni tekst w interfejsie użytkownika, zostanie zaktualizowana właściwość `Name`.</span><span class="sxs-lookup"><span data-stu-id="76486-111">The text-entry control shows the value in the `Name` property and, when the user changes the text in the UI, the `Name` property is updated.</span></span> <span data-ttu-id="76486-112">Jeśli wartość właściwości `Name` zostanie zmieniona w modelu ViewModel, zdarzenie jest zgłaszane, aby poinformować interfejs użytkownika o konieczności aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="76486-112">If the value of the `Name` property is changed in the ViewModel, an event is raised to tell the UI to update.</span></span>

<span data-ttu-id="76486-113">Zachowanie modelu ViewModel jest pokazywane jako właściwości polecenia, przy czym polecenie jest obiektem opakowującym akcję, która jest wykonywana, gdy polecenie jest wywoływane.</span><span class="sxs-lookup"><span data-stu-id="76486-113">ViewModel behavior is exposed as command properties, a command being an object that wraps an action that is executed when the command is invoked.</span></span> <span data-ttu-id="76486-114">Te polecenia są powiązane przez nazwę z kontrolkami, takimi jak przyciski, a naciśnięcie przycisku spowoduje wywołanie polecenia.</span><span class="sxs-lookup"><span data-stu-id="76486-114">These commands are bound by name to controls like buttons, and tapping a button will invoke the command.</span></span>

## <a name="create-a-base-viewmodel"></a><span data-ttu-id="76486-115">Tworzenie podstawowego modelu ViewModel</span><span class="sxs-lookup"><span data-stu-id="76486-115">Create a base ViewModel</span></span>

<span data-ttu-id="76486-116">Wszystkie modele ViewModel implementują interfejs `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="76486-116">ViewModels all implement the `INotifyPropertyChanged` interface.</span></span> <span data-ttu-id="76486-117">Ten interfejs ma pojedyncze zdarzenie, `PropertyChanged`, które służy do powiadamiania interfejsu użytkownika o wszelkich aktualizacjach.</span><span class="sxs-lookup"><span data-stu-id="76486-117">This interface has a single event, `PropertyChanged`, which is used to notify the UI of any updates.</span></span> <span data-ttu-id="76486-118">To zdarzenie ma argumenty zdarzenia zawierające nazwę właściwości, która uległa zmianie.</span><span class="sxs-lookup"><span data-stu-id="76486-118">This event has event args that contain the name of the property that has changed.</span></span> <span data-ttu-id="76486-119">Tworzenie podstawowej klasy ViewModel implementującej ten interfejs oraz udostępniającej niektóre metody pomocnika jest powszechną praktyką.</span><span class="sxs-lookup"><span data-stu-id="76486-119">It's common practice to create a base ViewModel class implementing this interface and providing some helper methods.</span></span>

1. <span data-ttu-id="76486-120">Utwórz nową klasę w standardowym projekcie platformy .NET `ImHere` o nazwie `BaseViewModel`, klikając prawym przyciskiem myszy projekt, a następnie wybierając pozycję *Dodaj->Klasa...*. Nadaj nowej klasie nazwę „BaseViewModel”, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="76486-120">Create a new class in the `ImHere` .NET standard project called `BaseViewModel` by right-clicking on the project, and then selecting *Add->Class...*. Name the new class "BaseViewModel" and click **Add**.</span></span>

2. <span data-ttu-id="76486-121">Utwórz klasę `public` pochodną od `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="76486-121">Make the class `public` and derive from `INotifyPropertyChanged`.</span></span> <span data-ttu-id="76486-122">Musisz dodać dyrektywę using dla `System.ComponentModel`.</span><span class="sxs-lookup"><span data-stu-id="76486-122">You'll need to add a using directive for `System.ComponentModel`.</span></span>

3. <span data-ttu-id="76486-123">Zaimplementuj interfejs `INotifyPropertyChanged`, dodając zdarzenie `PropertyChanged`:</span><span class="sxs-lookup"><span data-stu-id="76486-123">Implement the `INotifyPropertyChanged` interface by adding the `PropertyChanged` event:</span></span>

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. <span data-ttu-id="76486-124">Typowym wzorcem dla właściwości modelu ViewModel jest istnienie właściwości publicznej z prywatnym polem zapasowym.</span><span class="sxs-lookup"><span data-stu-id="76486-124">The common pattern for ViewModel properties is to have a public property with a private backing field.</span></span> <span data-ttu-id="76486-125">W metodzie ustawiającej właściwości pole zapasowe jest sprawdzane z nową wartością.</span><span class="sxs-lookup"><span data-stu-id="76486-125">In the property setter, the backing field is checked against the new value.</span></span> <span data-ttu-id="76486-126">Jeśli nowa wartość różni się do pola zapasowego, pole zapasowe jest aktualizowane i jest zgłaszane zdarzenie `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="76486-126">If the new value is different to the backing field, the backing field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="76486-127">Ta logika jest łatwa do pominięcia w metodzie, należy zatem dodać metodę `Set`.</span><span class="sxs-lookup"><span data-stu-id="76486-127">This logic is easy to factor out into a method, so add the `Set` method.</span></span> <span data-ttu-id="76486-128">Konieczne będzie dodanie dyrektywy using dla przestrzeni nazw `System.Runtime.CompilerServices`.</span><span class="sxs-lookup"><span data-stu-id="76486-128">You'll need to add a using directive for the `System.Runtime.CompilerServices` namespace.</span></span>

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    <span data-ttu-id="76486-129">Ta metoda pobiera odwołanie do pola zapasowego, nową wartość i nazwę właściwości.</span><span class="sxs-lookup"><span data-stu-id="76486-129">This method takes a reference to the backing field, the new value, and the property name.</span></span> <span data-ttu-id="76486-130">Jeśli pole nie zostało zmienione, następuje powrót z metody, w przeciwnym razie pole jest aktualizowane i jest zgłaszane zdarzenie `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="76486-130">If the field hasn't changed, the method returns, otherwise, the field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="76486-131">Parametr `propertyName` metody `Set` jest parametrem domyślnym i jest oznaczony za pomocą atrybutu `CallerMemberName`.</span><span class="sxs-lookup"><span data-stu-id="76486-131">The `propertyName` parameter on the `Set` method is a default parameter and is marked with the `CallerMemberName` attribute.</span></span> <span data-ttu-id="76486-132">Gdy ta metoda jest wywoływana z metody ustawiającej właściwość, zwykle ten parametr pozostaje jako wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="76486-132">When this method is called from a property setter, this parameter is normally left as the default value.</span></span> <span data-ttu-id="76486-133">Następnie kompilator automatycznie ustawi wartość parametru na nazwę właściwości calling.</span><span class="sxs-lookup"><span data-stu-id="76486-133">The compiler will then automatically set the parameter value to be the name of the calling property.</span></span>

<span data-ttu-id="76486-134">Pełny kod dla tej klasy znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="76486-134">The full code for this class is below.</span></span>

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a><span data-ttu-id="76486-135">Tworzenie modelu ViewModel strony</span><span class="sxs-lookup"><span data-stu-id="76486-135">Create a ViewModel for the page</span></span>

<span data-ttu-id="76486-136">`MainPage` będzie mieć kontrolkę wprowadzania tekstu dla numerów telefonów i etykietę do wyświetlania komunikatu.</span><span class="sxs-lookup"><span data-stu-id="76486-136">The `MainPage` will have a text-entry control for phone numbers and a label to display a message.</span></span> <span data-ttu-id="76486-137">Te kontrolki będą powiązane z właściwościami modelu ViewModel.</span><span class="sxs-lookup"><span data-stu-id="76486-137">These controls will be bound to properties on a ViewModel.</span></span>

1. <span data-ttu-id="76486-138">Utwórz klasę o nazwie `MainViewModel` w standardowym projekcie platformy .NET `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="76486-138">Create a class called `MainViewModel` in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="76486-139">Ustaw tę klasę jako publiczną, która pochodzi od `BaseViewModel`.</span><span class="sxs-lookup"><span data-stu-id="76486-139">Make this class public and derive from `BaseViewModel`.</span></span>

3. <span data-ttu-id="76486-140">Dodaj dwie właściwości `string`, `PhoneNumbers` i `Message`, każdą z polem zapasowym.</span><span class="sxs-lookup"><span data-stu-id="76486-140">Add two `string` properties, `PhoneNumbers` and `Message`, each with a backing field.</span></span> <span data-ttu-id="76486-141">W metodzie ustawiającej właściwość użyj metody klasy bazowej `Set`, aby zaktualizować wartość i zgłosić zdarzenie `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="76486-141">In the property setter, use the base class `Set` method to update the value and raise the `PropertyChanged` event.</span></span>

   ```cs
    string message = "";
    public string Message
    {
        get => message;
        set => Set(ref message, value);
    }

    string phoneNumbers = "";
    public string PhoneNumbers
    {
        get => phoneNumbers;
        set => Set(ref phoneNumbers, value);
    }
   ```

4. <span data-ttu-id="76486-142">Dodaj właściwość tylko do odczytu command o nazwie `SendLocationCommand`.</span><span class="sxs-lookup"><span data-stu-id="76486-142">Add a read-only command property called `SendLocationCommand`.</span></span> <span data-ttu-id="76486-143">To polecenie będzie mieć typ `ICommand` z przestrzeni nazw `System.Windows.Input`.</span><span class="sxs-lookup"><span data-stu-id="76486-143">This command will have a type of `ICommand` from the `System.Windows.Input` namespace.</span></span>

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. <span data-ttu-id="76486-144">Dodaj konstruktor do klasy, a w tym konstruktorze zainicjuj polecenie `SendLocationCommand` jako nowe `Command` z przestrzeni nazw `Xamarin.Forms`.</span><span class="sxs-lookup"><span data-stu-id="76486-144">Add a constructor to the class, and in this constructor, initialize the `SendLocationCommand` as a new `Command` from the `Xamarin.Forms` namespace.</span></span> <span data-ttu-id="76486-145">Konstruktor dla tego polecenia pobiera `Action` w celu uruchomienia po wywołaniu polecenia, więc utwórz metodę `async` o nazwie `SendLocation` i przekaż funkcję lambda, która oczekuje (`await`) na wywołanie do konstruktora.</span><span class="sxs-lookup"><span data-stu-id="76486-145">The constructor for this command takes an `Action` to run when the command is invoked, so create an `async` method called `SendLocation` and pass a lambda function that `await`s this call to the constructor.</span></span> <span data-ttu-id="76486-146">Treść metody `SendLocation` zostanie zaimplementowana w późniejszych jednostkach w tym module.</span><span class="sxs-lookup"><span data-stu-id="76486-146">The body of the `SendLocation` method will be implemented in later units in this module.</span></span> <span data-ttu-id="76486-147">Musisz dodać dyrektywę using dla przestrzeni nazw `System.Threading.Tasks`, aby można było zwrócić `Task`.</span><span class="sxs-lookup"><span data-stu-id="76486-147">You'll need to add a using directive for the `System.Threading.Tasks` namespace to be able to return a `Task`.</span></span>

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

<span data-ttu-id="76486-148">Poniżej przedstawiono kod dla tej klasy.</span><span class="sxs-lookup"><span data-stu-id="76486-148">The code for this class is shown below.</span></span>

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using Xamarin.Forms;

namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a><span data-ttu-id="76486-149">Tworzenie interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="76486-149">Create the user interface</span></span>

<span data-ttu-id="76486-150">Interfejsy użytkownika programu Xamarin.Forms można zbudować przy użyciu języka XAML.</span><span class="sxs-lookup"><span data-stu-id="76486-150">Xamarin.Forms UIs can be built using XAML.</span></span>

1. <span data-ttu-id="76486-151">Otwórz plik `MainPage.xaml` z projektu `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="76486-151">Open the `MainPage.xaml` file from the `ImHere` project.</span></span> <span data-ttu-id="76486-152">Strona zostanie otwarta w edytorze języka XAML.</span><span class="sxs-lookup"><span data-stu-id="76486-152">The page will open in the XAML editor.</span></span>

    <span data-ttu-id="76486-153">UWAGA — projekt `ImHere.UWP` zawiera także plik o nazwie `MainPage.xaml`.</span><span class="sxs-lookup"><span data-stu-id="76486-153">NOTE - The `ImHere.UWP` project also contains a file called `MainPage.xaml`.</span></span> <span data-ttu-id="76486-154">Upewnij się, że edytujesz plik, który znajduje się w standardowej bibliotece platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="76486-154">Make sure you're editing the one in the .NET standard library.</span></span>

2. <span data-ttu-id="76486-155">Przed powiązaniem kontrolek z właściwościami w modelu ViewModel musisz ustawić wystąpienie modelu ViewModel jako kontekst powiązania strony.</span><span class="sxs-lookup"><span data-stu-id="76486-155">Before you can bind controls to properties on a ViewModel, you have to set an instance of the ViewModel as the binding context of the page.</span></span> <span data-ttu-id="76486-156">Dodaj następujący fragment w języku XAML wewnątrz najwyższego poziomu `ContentPage`.</span><span class="sxs-lookup"><span data-stu-id="76486-156">Add the following XAML inside the top-level `ContentPage`.</span></span>

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. <span data-ttu-id="76486-157">Usuń zawartość `StackLayout` i dodaj wewnątrz pewne wypełnienie, aby poprawić wygląd interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="76486-157">Delete the contents of the `StackLayout` and add some padding inside it to help make the UI look better.</span></span>

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. <span data-ttu-id="76486-158">Dodaj kontrolkę `Editor`, której użytkownik może użyć do dodawania numerów telefonów do `StackLayout` za pomocą `Label` powyżej, aby opisać przeznaczenie kontrolki wprowadzania.</span><span class="sxs-lookup"><span data-stu-id="76486-158">Add an `Editor` control that the user can use to add phone numbers to the `StackLayout`, with a `Label` above to describe what the entry control is for.</span></span> <span data-ttu-id="76486-159">Stos podrzędny `StackLayout` realizuje kontrolę w poziomie albo pionie w kolejności, w której kontrolki są dodawane, więc dodanie najpierw `Label` umieści ją powyżej `Editor`.</span><span class="sxs-lookup"><span data-stu-id="76486-159">`StackLayout`'s stack child controls either horizontally or vertically in the order in which the controls are added, so adding the `Label` first will put it above the `Editor`.</span></span> <span data-ttu-id="76486-160">Kontrolki `Editor` są kontrolkami wprowadzania wielowierszowego, umożliwiając użytkownikowi wprowadzanie wielu numerów telefonów, po jednym w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="76486-160">`Editor` controls are multi-line entry controls, allowing the user to enter multiple phone numbers, one per line.</span></span>

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    <span data-ttu-id="76486-161">Właściwość `Text` w elemencie `Editor` jest powiązana z właściwością `PhoneNumbers` w elemencie `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="76486-161">The `Text` property on the `Editor` is bound to the `PhoneNumbers` property on the `MainViewModel`.</span></span> <span data-ttu-id="76486-162">Składnia dla powiązania służy ustawieniu wartości właściwości na `"{Binding <property name>}"`.</span><span class="sxs-lookup"><span data-stu-id="76486-162">The syntax for binding is to set the property value to `"{Binding <property name>}"`.</span></span> <span data-ttu-id="76486-163">Nawiasy klamrowe informują kompilator języka XAML, że ta wartość jest szczególna i powinna być traktowana inaczej niż prosty `string`.</span><span class="sxs-lookup"><span data-stu-id="76486-163">The curly braces will tell the XAML compiler that this value is special and should be treated differently from a simple `string`.</span></span>

5. <span data-ttu-id="76486-164">Dodaj `Button`, aby wysyłać `Editor` do lokalizacji użytkownika poniżej.</span><span class="sxs-lookup"><span data-stu-id="76486-164">Add a `Button` to send the user's location below the `Editor`.</span></span>

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    <span data-ttu-id="76486-165">Właściwość `Command` jest powiązana z poleceniem `SendLocationCommand` modelu ViewModel.</span><span class="sxs-lookup"><span data-stu-id="76486-165">The `Command` property is bound to the `SendLocationCommand` command on the ViewModel.</span></span> <span data-ttu-id="76486-166">Po naciśnięciu przycisku polecenie zostanie wykonane.</span><span class="sxs-lookup"><span data-stu-id="76486-166">When the button is tapped, the command will be executed.</span></span>

6. <span data-ttu-id="76486-167">Dodaj `Label`, aby wyświetlić komunikat o stanie poniżej `Button`.</span><span class="sxs-lookup"><span data-stu-id="76486-167">Add a `Label` to show the status message below the `Button`.</span></span>

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

<span data-ttu-id="76486-168">Pełny kod tej strony znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="76486-168">The full code for this page is below.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ImHere"
             x:Class="ImHere.MainPage">
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
        <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                Command="{Binding SendLocationCommand}" />
        <Label Text="{Binding Message}"
               HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

<span data-ttu-id="76486-169">Uruchom aplikację, aby zobaczyć nowy interfejs użytkownika.</span><span class="sxs-lookup"><span data-stu-id="76486-169">Run the app to see the new UI.</span></span> <span data-ttu-id="76486-170">Jeśli chcesz teraz zweryfikować powiązania, możesz to zrobić, dodając punkty przerwania do właściwości lub metody `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="76486-170">If you want to validate the bindings at this point, you can do so by adding breakpoints to the properties or the `SendLocation` method.</span></span>

![Interfejs użytkownika nowej aplikacji](../media-drafts/3-new-ui.png)

## <a name="summary"></a><span data-ttu-id="76486-172">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="76486-172">Summary</span></span>

<span data-ttu-id="76486-173">W tym module pokazano, jak utworzyć interfejs użytkownika dla aplikacji przy użyciu języka XAML wraz z modelem ViewModel w celu obsługi logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76486-173">In this unit, you learned how to create the UI for the app using XAML, along with a ViewModel to handle the applications logic.</span></span> <span data-ttu-id="76486-174">Przedstawiono również sposób powiązania modelu ViewModel z interfejsem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="76486-174">You also learned how to bind the ViewModel to the UI.</span></span> <span data-ttu-id="76486-175">W następnym module dodasz lokalizację wyszukiwania do modelu ViewModel.</span><span class="sxs-lookup"><span data-stu-id="76486-175">In the next unit, you add location lookup to the ViewModel.</span></span>