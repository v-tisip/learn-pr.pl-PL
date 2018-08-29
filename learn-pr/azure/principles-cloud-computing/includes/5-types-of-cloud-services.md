W przypadku przetwarzania w chmurze istnieją trzy główne kategorie. Ważne jest ich zrozumienie, ponieważ są one używane w konwersacji, dokumentacji i szkoleniach.

Poniżej przedstawiono trzy typowe kategorie usług chmury:

- Infrastruktura jako usługa (IaaS)
- Platforma jako usługa (PaaS)
- Oprogramowanie jako usługa (SaaS)

Warto zwrócić uwagę na to, że te kategorie są warstwami umieszczonymi jedna na drugiej. Na przykład usługa PaaS dodaje warstwę na usłudze IaaS, zapewniając poziom abstrakcji. Abstrakcja ma zaletę ukrywania szczegółów, które możesz pominąć, dzięki czemu możesz szybciej przystąpić do kodowania. Jednak ceną, którą trzeba za to zapłacić, jest mniejsza kontrola nad bazowym sprzętem.

![Diagram warstwy](../media-drafts/5-layer-diagram.jpg) TEN OBRAZ WYMAGA PONOWNEGO NARYSOWANIA^^

### <a name="infrastructure-as-a-service-iaas"></a>Infrastruktura jako usługa (IaaS)

Infrastruktura jako usługa jest najbardziej elastyczną kategorią usług w chmurze i ma na celu zapewnienie pełnej kontroli nad sprzętem, na którym będzie działała Twoja aplikacja. Zamiast kupować sprzęt, wynajmujesz go dzięki usłudze IaaS.

Oto kilka przykładów usługi IaaS:

- Maszyny wirtualne
- Zapory
- Dyski twarde
- Moduły równoważenia obciążenia

### <a name="platform-as-a-service-paas"></a>Platforma jako usługa (PaaS)

Platforma jako usługa zapewnia środowisko do kompilowania, testowania i wdrażania aplikacji. Celem usługi PaaS jest jak najszybsze zapewnienie pomocy podczas tworzenia aplikacji bez konieczności martwienia się o zarządzanie bazową infrastrukturą. Na przykład podczas wdrażania aplikacji internetowej przy użyciu usługi PaaS nie trzeba instalować systemu operacyjnego, serwera internetowego ani nawet aktualizacji systemu. 

Przykładem usługi PaaS jest usługa Azure App Service.

### <a name="software-as-a-service-saas"></a>Oprogramowanie jako usługa (SaaS)

Oprogramowanie jako usługa umożliwia dostarczanie aplikacji przez Internet. Aplikacja SaaS najczęściej nosi nazwę aplikacji internetowej, jednak termin aplikacja SaaS wywodzi się z faktu, że aplikacja jest hostowana na serwerze dostawcy usługi SaaS. Dzięki usłudze SaaS nie trzeba martwić się o instalację ani konfigurowanie — wystarczy użyć jej w przeglądarce internetowej lub za pomocą oprogramowania. 

Przykładem aplikacji SaaS jest usługa Microsoft Office 365.

## <a name="summary"></a>Podsumowanie

Usługi IaaS, PaaS i SaaS tworzą umieszczone na sobie warstwy. Poziom wymaganej kontroli nad bazowym sprzętem określi, która kategoria usług będzie dla Ciebie najlepsza.
