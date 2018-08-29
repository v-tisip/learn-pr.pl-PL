Funkcja platformy Azure nie działa, dopóki coś nie wyda jej polecenia wykonania. Można na przykład utworzyć funkcję platformy Azure, która przed spotkaniem wysyła do klientów wiadomość SMS z przypomnieniem. Jeśli nie poinformujemy takiej funkcji, kiedy powinna zostać uruchomiona, klienci nigdy nie otrzymają wiadomości. 

W tym dokumencie zapoznasz się z wyzwalaczami na wysokim poziomie i najpowszechniejszymi typami wyzwalaczy.

## <a name="what-is-a-trigger"></a>Co to jest wyzwalacz?

Wyzwalacz to usługa, która definiuje sposób wywoływania funkcji platformy Azure. Na przykład jeśli funkcja ma być wykonywana co 10 minut, można użyć wyzwalacza z czasomierzem.

Każda funkcja musi mieć skojarzony dokładnie jeden wyzwalacz. Jeśli chcesz, aby część logiki była wykonywana pod wieloma warunkami, musisz utworzyć wiele funkcji.

## <a name="what-is-a-binding"></a>Co to jest powiązanie?

Powiązanie to połączenie z danymi w ramach funkcji. Powiązania są opcjonalne i mają formę powiązań wejściowych i wyjściowych. Powiązanie wejściowe to dane odbierane przez funkcję. Powiązanie wyjściowe to dane wysyłane przez funkcję.

W odróżnieniu od wyzwalacza, funkcja może mieć wiele powiązań wejściowych i wyjściowych.

## <a name="types-of-triggers"></a>Typy wyzwalaczy

Usługa Azure Functions obsługuje szeroką gamę typów wyzwalaczy. Oto niektóre z najczęściej używanych typów:

| Typ | Przeznaczenie | 
| --- | --- | 
| **Czasomierz** | Wykonanie funkcji w określonych interwałach. | 
| **HTTP** | Wykonanie funkcji po odebraniu żądania HTTP. |  
| **Obiekt blob** | Wykonanie funkcji po przekazaniu lub zaktualizowaniu pliku w usłudze Azure Blob Storage. | 
| **Kolejka** | Wykonanie funkcji po dodaniu komunikatu do kolejki usługi Azure Storage. | 
| **Cosmos DB** | Wykonanie funkcji po zmodyfikowaniu dokumentu w kolekcji. | 
| **Centrum zdarzeń** | Wykonanie funkcji, gdy centrum zdarzeń odbiera nowe zdarzenie. | 

W tym module skupimy się na typach **czasomierz**, **HTTP** i **obiekt blob**.

## <a name="summary"></a>Podsumowanie

Aby wykonać funkcję platformy Azure, musimy użyć wyzwalacza. Wyzwalacze Czasomierz, HTTP i Obiekt blob są trzema najczęściej używanymi typami wyzwalaczy, które zastosujesz do wykonywania logiki bezserwerowej.
