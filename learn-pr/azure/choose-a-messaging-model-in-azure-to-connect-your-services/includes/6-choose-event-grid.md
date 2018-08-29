Wiele aplikacji używa zdarzeń, aby powiadamiać rozpowszechnione składniki, że coś się stało lub jakiś obiekt uległ zmianie. Możesz użyć usługi Event Grid, aby ułatwić dystrybucję tych zdarzeń na platformie Azure.

Załóżmy, że masz aplikację do udostępniania muzyki z internetowym interfejsem API uruchamianym na platformie Azure. Gdy nowy plik dźwiękowy zostanie przekazany przez użytkownika, musisz powiadomić wszystkie aplikacje mobilne zainstalowane na urządzeniach użytkowników na całym świecie.

Możesz użyć subskrypcji w usłudze Azure Event Grid, aby to zrobić niezawodnie i szybko.

## <a name="what-is-event-grid"></a>Co to jest usługa Event Grid?

Usługa Event Grid jest usługą, która dystrybuuje zdarzenia ze źródeł, np. kont usługi Azure Blob Storage lub Media Services, do subskrybentów, np. usługi Azure Functions lub elementów webhook.

Źródłem zdarzenia jest dowolny składnik, który może wygenerować zdarzenie. Na przykład użytkownik może dodać nowy plik multimedialny do konta usługi Blob Storage. Spowoduje to wygenerowanie zdarzenia, które może być dystrybuowane przez usługę Event Grid.

Subskrybent zdarzenia to dowolny składnik, który może odbierać zdarzenia od usługi Event Grid. Na przykład usługa Azure Function może wykonać kod, który będzie reagować na nowy plik multimedialny na koncie usługi Blob Storage.

Usługa Event Grid ułatwia łączenie źródeł z wieloma subskrybentami.

![Źródła i subskrybenci usługi Event Grid](../images/6-event-grid.png)

## <a name="event-sources"></a>Źródła zdarzeń

Zdarzenia mogą być wygenerowane przez następujące rodzaje zasobów platformy Azure:

- **Subskrypcje i grupy zasobów platformy Azure.** Subskrypcje i grupy zasobów generują zdarzenia związane z operacjami zarządzania na platformie Azure. Na przykład gdy użytkownik tworzy maszynę wirtualną, to źródło generuje zdarzenie.
- **Konta magazynu.** Konta magazynu mogą generować zdarzenia, gdy użytkownicy dodają obiekty blob, pliki, wpisy tabeli lub komunikaty w kolejce. Możesz użyć kont obiektów blob oraz kont ogólnego przeznaczenia jako źródeł zdarzeń.
- **Usługa Media Services.** Usługa Media Services hostuje multimedialne pliki wideo i audio oraz zapewnia zaawansowane funkcje zarządzania plikami multimedialnymi. Usługa Media Services może generować zdarzenia, gdy na pliku wideo zostanie rozpoczęte lub zakończone zadanie kodowania.
- **Usługa IoT Hub.** Usługa Azure Internet of Things (IoT) Hub komunikuje się z urządzeniami IoT i zbiera dane telemetryczne z tych urządzeń. Usługa może generować zdarzenia za każdym razem, gdy odbierze tego typu komunikację.
- **Zdarzenia niestandardowe.** Zdarzenia niestandardowe można wygenerować przy użyciu interfejsu API REST lub zestawu SDK platformy Azure dla języka Java, GO, .NET, Node, Python i Ruby. Na przykład możesz utworzyć niestandardowe zdarzenie w roli procesu roboczego aplikacji internetowej platformy Azure, kiedy proces odbierze komunikat z kolejki magazynu.

Ta szeroka integracja z różnymi źródłami zdarzeń na platformie Azure gwarantuje, że usługa Event Grids może rozpowszechniać zdarzenia związane niemal z dowolnym zasobem platformy Azure.

## <a name="topics"></a>Tematy

W usłudze Azure Event Grid temat jest kolekcją powiązanych zdarzeń. Podczas publikowania zdarzeń ze źródła podejmuje się decyzję, czy te zdarzenia potrzebują tylko jednego tematu, czy można podzielić je na wiele tematów. Składniki, które odbierają i obsługują zdarzenia, subskrybują tematy, aby określić odbierane zdarzenia.

## <a name="subscriptions"></a>Subskrypcje

Programy obsługi zdarzeń używają subskrypcji, aby poinformować usługę Event Grid, które zdarzenia w temacie chcą odebrać. Ponadto subskrypcja ustala punkt końcowy — jest to lokalizacja, do której usługa Event Grid wysyła powiadomienia o zdarzeniach. Subskrypcja może również filtrować zdarzenia według typu lub tematu, aby upewnić się, że program obsługi zdarzeń odbiera tylko odpowiednie zdarzenia.

## <a name="event-handlers"></a>Programy obsługi zdarzeń

Następujące typy obiektów na platformie Azure mogą odbierać i obsługiwać zdarzenia z usługi Event Grid:

- **Usługa Azure Functions.** Usługa Azure Function zawiera niestandardowy kod, który jest uruchamiany na platformie Azure bez serwera wirtualnego hosta czy kontenera. Użyj usługi Azure Function jako programu obsługi zdarzeń, jeżeli chcesz użyć kodu niestandardowej odpowiedzi na zdarzenie.
- **Elementy webhook.** Element webhook to internetowy interfejs API, którzy wdraża architekturę wypychania.
- **Usługa Logic Apps.** Usługa Azure Logic App hostuje proces biznesowy jako przepływ pracy.
- **Usługa Microsoft Flow.** Usługa Flow również hostuje przepływy pracy, ale jest łatwiejsza w obsłudze dla pracowników nietechnicznych.

## <a name="how-to-choose"></a>Jak wybrać

Użyj usługi Event Grid, jeżeli potrzebujesz tych funkcji i cech:

- **Prostota.** Podłączanie źródeł do subskrybentów w usłudze Event Grid jest bardzo proste.
- **Zaawansowane filtrowanie.** Subskrypcje mają ścisłą kontrolę nad zdarzeniami odbieranymi z tematu.
- **Rozdysponowywanie.** Możesz subskrybować nieograniczoną liczbę punktów końcowych do tych samych zdarzeń i tematów.
- **Niezawodność.** Usługa Event Grid ponawia próby dostarczenia zdarzenia do 24 godzin dla każdej subskrypcji.
- **Płatność za zdarzenie.** Płacisz tylko za liczbę przekazanych zdarzeń.

## <a name="summary"></a>Podsumowanie

Usługa Event Grid jest prostym i wszechstronnym systemem dystrybucji zdarzeń. Użyj jej, aby publikować zdarzenia subskrybentom, którzy będą odbierać te zdarzenia niezawodnie i szybko.