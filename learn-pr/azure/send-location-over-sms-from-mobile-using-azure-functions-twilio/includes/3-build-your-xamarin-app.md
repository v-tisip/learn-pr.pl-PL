W tym momencie aplikacja mobilna jest prostą aplikacją „Witaj świecie”. W tym module dodasz interfejs użytkownika i niektóre elementy podstawowej logiki aplikacji.

Interfejs użytkownika dla aplikacji będzie się składać z:

* Kontrolki wprowadzania tekstu umożliwiającej wprowadzenie niektórych numerów telefonów.
* Przycisku do wysyłania swojej lokalizacji na te numery przy użyciu funkcji platformy Azure.
* Etykiety, która wyświetli użytkownikowi komunikat o bieżącym stanie, taki jak o wysyłaniu lokalizacji i pomyślnym wysyłaniu lokalizacji.

Program Xamarin.Forms obsługuje wzorzec projektowania o nazwie Model-View-ViewModel (MVVM). Więcej o MVVM możesz dowiedzieć się w [dokumentacji Xamarin MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), ale kluczową jego cechą jest to, że każda strona (widok) ma model ViewModel, który udostępnia właściwości i zachowanie.

Właściwości modelu ViewModel są „powiązane” ze składnikami interfejsu użytkownika według nazwy, a to powiązanie synchronizuje dane między widokiem a modelem ViewModel. Na przykład właściwość `string` modelu ViewModel o nazwie `Name` może być powiązana z właściwością `Text` kontrolki wprowadzania tekstu w interfejsie użytkownika. Kontrolka wprowadzania tekstu wyświetla wartości we właściwości `Name` oraz, jeśli użytkownik zmieni tekst w interfejsie użytkownika, zostanie zaktualizowana właściwość `Name`. Jeśli wartość właściwości `Name` zostanie zmieniona w modelu ViewModel, zdarzenie jest zgłaszane, aby poinformować interfejs użytkownika o konieczności aktualizacji.

Zachowanie modelu ViewModel jest pokazywane jako właściwości polecenia, przy czym polecenie jest obiektem opakowującym akcję, która jest wykonywana, gdy polecenie jest wywoływane. Te polecenia są powiązane przez nazwę z kontrolkami, takimi jak przyciski, a naciśnięcie przycisku spowoduje wywołanie polecenia.

## <a name="create-a-base-viewmodel"></a>Tworzenie podstawowego modelu ViewModel

Wszystkie modele ViewModel implementują interfejs `INotifyPropertyChanged`. Ten interfejs ma pojedyncze zdarzenie, `PropertyChanged`, które służy do powiadamiania interfejsu użytkownika o wszelkich aktualizacjach. To zdarzenie ma argumenty zdarzenia zawierające nazwę właściwości, która uległa zmianie. Tworzenie podstawowej klasy ViewModel implementującej ten interfejs oraz udostępniającej niektóre metody pomocnika jest powszechną praktyką.

1. Utwórz nową klasę w standardowym projekcie platformy .NET `ImHere` o nazwie `BaseViewModel`, klikając prawym przyciskiem myszy projekt, a następnie wybierając pozycję *Dodaj->Klasa...*. Nadaj nowej klasie nazwę „BaseViewModel”, a następnie kliknij przycisk **Dodaj**.

2. Utwórz klasę `public` pochodną od `INotifyPropertyChanged`. Musisz dodać dyrektywę using dla `System.ComponentModel`.

3. Zaimplementuj interfejs `INotifyPropertyChanged`, dodając zdarzenie `PropertyChanged`:

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. Typowym wzorcem dla właściwości modelu ViewModel jest istnienie właściwości publicznej z prywatnym polem zapasowym. W metodzie ustawiającej właściwości pole zapasowe jest sprawdzane z nową wartością. Jeśli nowa wartość różni się do pola zapasowego, pole zapasowe jest aktualizowane i jest zgłaszane zdarzenie `PropertyChanged`. Ta logika jest łatwa do pominięcia w metodzie, należy zatem dodać metodę `Set`. Konieczne będzie dodanie dyrektywy using dla przestrzeni nazw `System.Runtime.CompilerServices`.

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    Ta metoda pobiera odwołanie do pola zapasowego, nową wartość i nazwę właściwości. Jeśli pole nie zostało zmienione, następuje powrót z metody, w przeciwnym razie pole jest aktualizowane i jest zgłaszane zdarzenie `PropertyChanged`. Parametr `propertyName` metody `Set` jest parametrem domyślnym i jest oznaczony za pomocą atrybutu `CallerMemberName`. Gdy ta metoda jest wywoływana z metody ustawiającej właściwość, zwykle ten parametr pozostaje jako wartość domyślna. Następnie kompilator automatycznie ustawi wartość parametru na nazwę właściwości calling.

Pełny kod dla tej klasy znajduje się poniżej.

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

## <a name="create-a-viewmodel-for-the-page"></a>Tworzenie modelu ViewModel strony

`MainPage` będzie mieć kontrolkę wprowadzania tekstu dla numerów telefonów i etykietę do wyświetlania komunikatu. Te kontrolki będą powiązane z właściwościami modelu ViewModel.

1. Utwórz klasę o nazwie `MainViewModel` w standardowym projekcie platformy .NET `ImHere`.

2. Ustaw tę klasę jako publiczną, która pochodzi od `BaseViewModel`.

3. Dodaj dwie właściwości `string`, `PhoneNumbers` i `Message`, każdą z polem zapasowym. W metodzie ustawiającej właściwość użyj metody klasy bazowej `Set`, aby zaktualizować wartość i zgłosić zdarzenie `PropertyChanged`.

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

4. Dodaj właściwość tylko do odczytu command o nazwie `SendLocationCommand`. To polecenie będzie mieć typ `ICommand` z przestrzeni nazw `System.Windows.Input`.

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. Dodaj konstruktor do klasy, a w tym konstruktorze zainicjuj polecenie `SendLocationCommand` jako nowe `Command` z przestrzeni nazw `Xamarin.Forms`. Konstruktor dla tego polecenia pobiera `Action` w celu uruchomienia po wywołaniu polecenia, więc utwórz metodę `async` o nazwie `SendLocation` i przekaż funkcję lambda, która oczekuje (`await`) na wywołanie do konstruktora. Treść metody `SendLocation` zostanie zaimplementowana w późniejszych jednostkach w tym module. Musisz dodać dyrektywę using dla przestrzeni nazw `System.Threading.Tasks`, aby można było zwrócić `Task`.

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

Poniżej przedstawiono kod dla tej klasy.

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

## <a name="create-the-user-interface"></a>Tworzenie interfejsu użytkownika

Interfejsy użytkownika programu Xamarin.Forms można zbudować przy użyciu języka XAML.

1. Otwórz plik `MainPage.xaml` z projektu `ImHere`. Strona zostanie otwarta w edytorze języka XAML.

    UWAGA — projekt `ImHere.UWP` zawiera także plik o nazwie `MainPage.xaml`. Upewnij się, że edytujesz plik, który znajduje się w standardowej bibliotece platformy .NET.

2. Przed powiązaniem kontrolek z właściwościami w modelu ViewModel musisz ustawić wystąpienie modelu ViewModel jako kontekst powiązania strony. Dodaj następujący fragment w języku XAML wewnątrz najwyższego poziomu `ContentPage`.

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. Usuń zawartość `StackLayout` i dodaj wewnątrz pewne wypełnienie, aby poprawić wygląd interfejsu użytkownika.

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. Dodaj kontrolkę `Editor`, której użytkownik może użyć do dodawania numerów telefonów do `StackLayout` za pomocą `Label` powyżej, aby opisać przeznaczenie kontrolki wprowadzania. Stos podrzędny `StackLayout` realizuje kontrolę w poziomie albo pionie w kolejności, w której kontrolki są dodawane, więc dodanie najpierw `Label` umieści ją powyżej `Editor`. Kontrolki `Editor` są kontrolkami wprowadzania wielowierszowego, umożliwiając użytkownikowi wprowadzanie wielu numerów telefonów, po jednym w każdym wierszu.

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    Właściwość `Text` w elemencie `Editor` jest powiązana z właściwością `PhoneNumbers` w elemencie `MainViewModel`. Składnia dla powiązania służy ustawieniu wartości właściwości na `"{Binding <property name>}"`. Nawiasy klamrowe informują kompilator języka XAML, że ta wartość jest szczególna i powinna być traktowana inaczej niż prosty `string`.

5. Dodaj `Button`, aby wysyłać `Editor` do lokalizacji użytkownika poniżej.

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    Właściwość `Command` jest powiązana z poleceniem `SendLocationCommand` modelu ViewModel. Po naciśnięciu przycisku polecenie zostanie wykonane.

6. Dodaj `Label`, aby wyświetlić komunikat o stanie poniżej `Button`.

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

Pełny kod tej strony znajduje się poniżej.

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

Uruchom aplikację, aby zobaczyć nowy interfejs użytkownika. Jeśli chcesz teraz zweryfikować powiązania, możesz to zrobić, dodając punkty przerwania do właściwości lub metody `SendLocation`.

![Interfejs użytkownika nowej aplikacji](../media/3-new-ui.png)

## <a name="summary"></a>Podsumowanie

W tym module pokazano, jak utworzyć interfejs użytkownika dla aplikacji przy użyciu języka XAML wraz z modelem ViewModel w celu obsługi logiki aplikacji. Przedstawiono również sposób powiązania modelu ViewModel z interfejsem użytkownika. W następnym module dodasz lokalizację wyszukiwania do modelu ViewModel.