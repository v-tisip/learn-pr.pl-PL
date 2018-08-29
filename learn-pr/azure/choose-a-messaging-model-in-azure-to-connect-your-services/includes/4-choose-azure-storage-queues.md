Załóżmy, że planujesz architekturę aplikacji do udostępniania muzyki. Chcesz upewnić się, że pliki muzyczne są bezproblemowo przekazywane do internetowego interfejsu API z aplikacji mobilnej.

Rozumiesz, że ta komunikacja powinna mieć formę komunikatu, i musisz wybrać, czy chcesz użyć kolejki usługi Azure Storage lub usługi Service Bus. Obydwa te rozwiązania mogą być używane do przechowywania kolejki komunikatów oczekujących na przetworzenie.

## <a name="delivery-guarantees"></a>Gwarancje dotyczące dostarczania

Systemy kolejkowania zwykle gwarantują dostarczanie każdego komunikatu w kolejce do składnika docelowego. Jednak te gwarancje mogą korzystać z różnych podejść:

- **Co najmniej jednokrotne dostarczanie.** To podejście gwarantuje, że każdy komunikat zostanie dostarczony do co najmniej jednego ze składników, które pobierają komunikaty z kolejki. Należy jednak pamiętać, że w pewnych okolicznościach ten sam komunikat może zostać dostarczony więcej niż raz. Jeśli na przykład istnieją dwa wystąpienia aplikacji internetowej pobierającej komunikaty z kolejki, zazwyczaj każdy komunikat przechodzi tylko do jednego z tych wystąpień. Jeśli jednak jedno wystąpienie przez dłuższy czas przetwarza komunikat, a limit czasu upłynie, komunikat może również zostać wysłany do drugiego wystąpienia. Należy pamiętać o tej możliwości, projektując kod aplikacji internetowej.
- **Co najwyżej jednokrotne dostarczanie.** To podejście nie gwarantuje dostarczenia każdego komunikatu. Istnieje bardzo mała szansa, że nie zostanie on dostarczony. Komunikat nie zostanie jednak dostarczony dwukrotnie, tak jak w przypadku co najmniej jednego dostarczania.
- **Pierwszy na wejściu — pierwszy na wyjściu (FIFO).** W większości systemów obsługi komunikatów komunikaty zazwyczaj opuszczają kolejkę w tej samej kolejności, w której zostały dodane, ale należy rozważyć, czy ta kolejność jest gwarantowana. Jeśli aplikacja rozproszona wymaga, aby komunikaty były przetwarzane dokładnie w prawidłowej kolejności, należy wybrać system kolejki, który oferuje gwarancję FIFO.

## <a name="transactions"></a>Transakcje

Niektóre ściśle powiązane grupy komunikatów mogą powodować problemy, gdy jeden z komunikatów w grupie nie zostanie prawidłowo dostarczony.

Rozważmy na przykład aplikację handlu elektronicznego. Gdy użytkownik kliknie przycisk „Kup”, zostanie wysłany komunikat ze szczegółami zamówienia oraz komunikat ze szczegółami karty kredytowej. Jeśli komunikat dotyczący karty kredytowej nie zostanie dostarczony, zamówienie może zostać wysłane bez płatności.

Aby uniknąć problemów tego typu można zgrupować dwa komunikaty jako transakcję. Powodzenie lub niepowodzenie transakcji odnosi się do pojedynczej jednostki. Jeśli dostarczenie komunikatu ze szczegółami karty kredytowej nie powiedzie się, komunikat ze szczegółami zamówienia również nie zostanie dostarczony.

## <a name="when-to-use-storage-queues"></a>Kiedy stosować kolejki usługi Storage

Kolejki są używane w przypadku komunikatów, ale nie zdarzeń.

Konta usługi Azure Storage obejmują kolejki, które mogą być używane przez aplikacje rozproszone jako proste tymczasowe lokalizacje magazynu na potrzeby komunikatów. Składnik źródłowy może dodać komunikat do kolejki. Składniki docelowe pobierają ten komunikat na początku kolejki do przetworzenia. Kolejki tego typu zwiększają niezawodność wymiany komunikatów, ponieważ w okresach dużego zapotrzebowania komunikaty po prostu czekają, aż ich składnik docelowy będzie gotowy do ich przetworzenia.

Kolejki również są oferowane jako część komunikatów usługi Azure Service Bus. Jeśli chcesz używać kolejki na platformie Azure w przypadku określonej komunikacji, musisz wybrać rozwiązanie do użycia: kolejkę usługi Storage lub kolejkę usługi Service Bus.

Aby dokonać tego wyboru, odpowiedz na następujące pytania:

- Czy potrzebujesz gwarancji co najwyżej jednokrotnego dostarczania?
- Czy potrzebujesz gwarancji FIFO?
- Czy chcesz grupować komunikaty w postaci transakcji?
- Czy chcesz przechowywać komunikaty większe niż 64 KB?

Jeśli odpowiedź na dowolne z tych pytań jest twierdząca, musisz wybrać kolejkę usługi Service Bus.

Dodatkowo zastanów się, czy:

- Czy potrzebujesz dzienników po stronie serwera w przypadku wszystkich wiadomości przechodzących przez kolejkę?
- Czy oczekujesz, że rozmiar kolejki przekroczy 80 GB?

Jeśli odpowiedź na dowolne z tych pytań jest twierdząca, musisz wybrać kolejkę usługi Storage.

## <a name="summary"></a>Podsumowanie

Kolejka to prosta tymczasowa lokalizacja magazynu na potrzeby komunikatów wysyłanych między składnikami aplikacji rozproszonej. Kolejka służy do organizowania komunikatów i bezproblemowej obsługi nieprzewidywalnych wzrostów zapotrzebowania.

Kolejek usługi Azure Storage można użyć, jeśli system kolejek ma być prosty i łatwy do kodowania. W przypadku bardziej zaawansowanych potrzeb należy używać kolejek usługi Azure Service Bus.