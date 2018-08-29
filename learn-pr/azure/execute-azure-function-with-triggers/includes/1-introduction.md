Wyobraź sobie scenariusz, w której bardzo popularny salon fryzjerski ma cykliczny problem: klienci często nie zgłaszają się w umówionych terminach. Terminy to zarezerwowane przedziały czasu. Jeśli klient nie zgłosi się w terminie, salon traci pieniądze. Aby rozwiązać ten problem, salon zwraca się z prośbą o pomoc do Ciebie, dewelopera oprogramowania. W celu poprawienia sytuacji decydujesz się na wysyłanie wiadomości SMS z przypomnieniem. Codziennie rano wysyłasz wiadomość SMS do każdego klienta, który w danym dniu ma omówiony termin.

Jako deweloper platformy Azure chcesz rozwiązać ten problem za pomocą funkcji platformy Azure. Wiesz już, jak zaimplementować logikę w celu wysyłania wiadomości SMS. Teraz musisz dowiedzieć się, jak wysyłać wiadomości o określonej godzinie. Na szczęście usługa Azure Functions obsługuje funkcję _wyzwalaczy_. Wyzwalacze są używane do określenia sposobu wykonywania funkcji platformy Azure.

## <a name="learning-objectives"></a>Cele szkolenia
> [!div class="checklist"]
> * Ustalenie, który wyzwalacz najlepiej zaspokoi Twoje potrzeby biznesowe.
> * Utworzenie wyzwalacza czasomierza w celu wywoływania funkcji zgodnie z ustalonym harmonogramem.
> * Utworzenie wyzwalacza HTTP w celu wywoływania funkcji po odebraniu żądania HTTP.
> * Utworzenie wyzwalacza obiektu blob w celu wywoływania funkcji, gdy obiekt blob jest tworzony lub aktualizowany w usłudze Azure Storage.
