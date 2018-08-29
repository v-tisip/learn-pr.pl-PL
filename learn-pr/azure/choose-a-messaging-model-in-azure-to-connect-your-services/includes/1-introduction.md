Wiele aplikacji składa się z programów działających na kilku różnych komputerach lub urządzeniach. W takich rozproszonych aplikacjach między składnikami muszą być przesyłane komunikaty w różnych sieciach i na dużych odległościach. Nawet na tym samym serwerze lub w tym samym centrum danych luźno połączone architektury wymagają mechanizmów umożliwiających komunikację między składnikami. Niezawodna obsługa komunikatów jest często krytycznym problemem.

Załóżmy, że pracujesz w firmie zajmującej się oprogramowaniem, która opracowuje aplikację do udostępniania muzyki. Muzycy mogą przekazywać skomponowane utwory na Twoja platformę użyciu frontonu internetowego lub aplikacji mobilnej. Mogą także słuchać utworów innych członków i dodawać komentarze. Aplikacja składa się z witryny internetowej, która działa u Twojego usługodawcy internetowego, z aplikacji mobilnej, która jest uruchamiana na urządzeniach mobilnych użytkowników, internetowego interfejsu API, który działa na platformie Azure, i usługi Azure SQL Database, gdzie są przechowywane dane.

Zauważasz, że w czasie wysokiego zapotrzebowania niektóre pliki muzyczne nie są pomyślnie przekazywane, a niektóre komentarze nie są publikowane. Testy pokazują, że te problemy są spowodowane przez porzucone komunikaty między składnikami frontonu i internetowym interfejsem API. Zamierzasz rozwiązać te problemy przy użyciu jednej lub kilku następujących technologii platformy Azure: kolejki usługi Storage oraz usługi Event Hub, Event Grid i Service Bus.

W tym module dowiesz się, jak wybrać właściwą technologię obsługi komunikatów na platformie Azure dla każdego zadania komunikacji w aplikacji rozproszonej.

## <a name="learning-objectives"></a>Cele szkolenia

- Opisanie zdarzeń i komunikatów oraz wyzwań, które należy rozwiązać w aplikacji rozproszonej.
- Zidentyfikowanie scenariuszy, w których kolejka usługi Azure Storage jest najlepszą technologią obsługi komunikatów dla aplikacji.
- Zidentyfikowanie scenariuszy, w których usługa Azure Event Grid jest najlepszą technologią obsługi komunikatów dla aplikacji.
- Zidentyfikowanie scenariuszy, w których usługa Azure Event Hub jest najlepszą technologią obsługi komunikatów dla aplikacji.
- Zidentyfikowanie scenariuszy, w których usługa Azure Service Bus jest najlepszą technologią obsługi komunikatów dla aplikacji.
