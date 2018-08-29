Jeśli chcesz zrozumieć, jakie problemy mogą wystąpić podczas zarządzania wpisami tajnymi konfiguracji aplikacji, zapoznaj się z historią Steve’a, starszego dewelopera.

Steve pracował w firmie dostarczającej karmę dla zwierząt od kilku tygodni. Zajmował się eksplorowaniem szczegółów firmowej aplikacji internetowej &mdash; aplikacji internetowej platformy .NET Core, która używała usługi Azure SQL Database do przechowywania informacji o zamówieniach oraz interfejsów API innych firm do rozliczania kart kredytowych i mapowania adresów klientów &mdash; gdy przypadkowo wkleił parametry połączenia bazy danych zamówień na forum publicznym.

Kilka dni później dział księgowości zauważył, że firma dostarczała mnóstwo karmy, za którą nikt nie płacił. Ktoś użył parametrów połączenia do uzyskania dostępu do bazy danych, odtworzył schemat i złożył zamówienia, nie używając witryny internetowej.

Gdy Steve zdał sobie sprawę ze swojego błędu, szybko zmienił hasło bazy danych, aby zablokować osobę atakującą włamującą się do witryny internetowej. Zalogował się on bezpośrednio na serwerze aplikacji i zmienił konfigurację aplikacji, zamiast ponownie przeprowadzić wdrożenie, ale serwer nadal wyświetlał żądania zakończone niepowodzeniem.

Steve zapomniał, że na różnych serwerach uruchomiono wiele wystąpień aplikacji, i zmienił tylko konfigurację jednego z nich. Konieczne było pełne ponowne wdrożenie, co spowodowało kolejne 30 minut przestoju.

Wyciek parametrów połączenia bazy danych, klucza interfejsu API lub hasła usługi może mieć katastrofalne skutki. Potencjalne efekty to kradzież lub usunięcie danych, szkody finansowe, przerwy w działaniu aplikacji oraz nieodwracalne szkody dla zasobów firmy i jej reputacji. Niestety wartości wpisów tajnych często trzeba wdrażać w wielu miejscach równocześnie i zmieniać je w niekorzystnym czasie. I trzeba je *gdzieś* przechowywać. Zobaczmy, jak możemy zabezpieczyć cały ten proces dzięki usłudze Azure KeyVault.

## <a name="learning-objectives"></a>Cele szkolenia
> [!div class="checklist"]
> * Zrozumienie, jakie typy informacji można przechowywać w usłudze Azure KeyVault
> * Utworzenie magazynu Azure KeyVault
> * Uwierzytelnienie za pomocą usługi Azure KeyVault
> * Uzyskanie dostępu do wpisów tajnych w usłudze Azure KeyVault