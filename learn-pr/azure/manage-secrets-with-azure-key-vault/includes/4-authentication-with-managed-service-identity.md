Usługa Azure Key Vault używa usługi **Azure Active Directory** do uwierzytelniania użytkowników i aplikacji próbujących uzyskać dostęp do magazynu. Aby udzielić naszej aplikacji internetowej dostępu do magazynu, najpierw musimy ją zarejestrować w usłudze Azure Active Directory. Zarejestrowanie powoduje utworzenie tożsamości dla aplikacji. Gdy będziemy już mieć tożsamość, możemy do niej przypisać uprawnienia magazynu.

Aplikacje i użytkownicy uwierzytelniają się w usłudze Key Vault przy użyciu tokenu uwierzytelniania usługi Azure Active Directory. Uzyskanie tokenu z usługi Azure Active Directory wymaga wpisu tajnego lub certyfikatu, ponieważ każda osoba mająca token mogłaby przy użyciu tożsamości aplikacji uzyskać dostęp do wszystkich wpisów tajnych w magazynie.

Nasze wpisy tajne aplikacji są bezpieczne w magazynie, ale musimy mieć wpis tajny lub certyfikat poza magazynem, aby uzyskiwać do nich dostęp. Ten problem jest nazywany *problemem ładowania początkowego*, a platforma Azure zapewnia jego rozwiązanie.

## <a name="managed-service-identity"></a>Tożsamość usługi zarządzanej

*Tożsamość usługi zarządzanej* (MSI, Managed Service Identity) to funkcja usługi Azure App Service, której aplikacja może używać w celu uzyskiwania dostępu do usługi Key Vault i innych usług platformy Azure bez konieczności zarządzania nawet jednym wpisem tajnym. Korzystanie z tożsamości MSI jest łatwiejsze i bezpieczniejsze niż samodzielne zarządzanie wpisem tajnym.

Po włączeniu tożsamości MSI platforma Azure aktywuje oddzielną usługę REST przyznającą token specjalnie na potrzeby aplikacji. Gdy aplikacja zażąda tokenu z usługi tokenu MSI, usługa skontaktuje się z usługą Azure Active Directory, aby uzyskać token dla tożsamości MSI, i przekaże go z powrotem do aplikacji w celu użycia w usłudze Key Vault. Najważniejszą częścią tego przepływu pracy jest sposób, w jaki aplikacja uwierzytelnia się w usłudze tokenu MSI &mdash; zamiast wpisu tajnego lub certyfikatu, którym trzeba zarządzać w konfiguracji, aplikacja używa wpisu tajnego bezpiecznie wprowadzanego przez platformę Azure do swoich zmiennych środowiskowych podczas uruchamiania. Nie trzeba zarządzać tą wartością wpisu tajnego ani jej nigdzie przechowywać. Ten wpis tajny oraz punkt końcowy usługi tokenu MSI jest dostępny wyłącznie dla Twojej aplikacji.

Ponadto tożsamość MSI zarejestruje za Ciebie aplikację w usłudze Azure Active Directory i usunie rejestrację, jeśli wyłączysz tożsamość MSI lub usuniesz aplikację.

Tożsamość MSI jest dostępna we wszystkich wersjach usługi Azure Active Directory, w tym w wersji Bezpłatna dołączonej do subskrypcji platformy Azure. Korzystanie z niej w usłudze App Service nie wiąże się z żadnym kosztem ani nie wymaga żadnej konfiguracji. Można ją włączyć lub wyłączyć dla aplikacji w dowolnym czasie.

> [!NOTE]
> Tożsamość MSI nie jest obecnie obsługiwana w przypadku systemu Linux ani internetowych aplikacji kontenera.

Włączenie tożsamości MSI wymaga wydania tylko jednego polecenia interfejsu wiersza polecenia platformy Azure bez żadnej konfiguracji. Wykonamy tę czynność w sekcji 5 podczas konfigurowania aplikacji usługi App Service i wdrażania jej na platformie Azure. Jednak wcześniej skorzystamy z naszej wiedzy o tożsamości MSI w celu napisania kodu naszej aplikacji.