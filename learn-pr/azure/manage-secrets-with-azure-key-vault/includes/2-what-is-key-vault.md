Usługa Azure Key Vault jest *magazynem wpisów tajnych*: scentralizowaną usługą w chmurze do przechowywania wpisów tajnych aplikacji. Usługa Key Vault pomaga zapobiegać powyższym scenariuszom przez przechowywanie wpisów tajnych aplikacji w jednej centralnej lokalizacji i zapewnienie bezpiecznego dostępu, kontroli uprawnień oraz rejestrowania dostępu.

Pojedynczy magazyn jest zasobem platformy Azure z własnymi zasadami konfigurowania i zabezpieczeń, który można utworzyć przy użyciu dowolnych standardowych narzędzi zarządzania platformy Azure, takich jak witryna Azure Portal lub interfejs wiersza polecenia platformy Azure. Dostęp do wpisów tajnych oraz zarządzanie magazynem realizowane jest za pośrednictwem interfejsu API REST. Każdy magazyn ma unikatowy adres URL, pod którym hostowany jest jego interfejs API.

> [!IMPORTANT]
> **Usługa Key Vault została zaprojektowana do przechowywania wpisów tajnych konfiguracji dla aplikacji serwerowych.** Nie jest przeznaczona do przechowywania danych należących do użytkowników aplikacji i nie powinna być używana w części aplikacji po stronie klienta. Znajduje to odzwierciedlenie w charakterystyce jej wydajności, interfejsie API i modelu kosztów.
>
> Dane użytkowników powinny być przechowywane gdzie indziej, na przykład w usłudze Azure SQL Database z funkcją Transparent Data Encryption lub na koncie magazynu z szyfrowaniem usługi Storage. Wpisy tajne używane przez aplikację do uzyskiwania dostępu do tych magazynów danych można przechowywać w usłudze Key Vault.

## <a name="what-is-a-secret-in-key-vault"></a>Co to jest wpis tajny w usłudze Key Vault?

W usłudze Key Vault wpisem tajnym jest para ciągów nazwa-wartość. Nazwy wpisów tajnych muszą składać się z od 1 do 127 znaków, zawierać wyłącznie znaki alfanumeryczne i łączniki oraz być unikatowe w ramach magazynu. Wartość wpisu tajnego może być dowolnym ciągiem UTF-8 o rozmiarze do 25 KB.

> [!TIP]
> Same nazwy wpisów tajnych nie muszą być traktowane jako tajne. Można przechowywać je w konfiguracji aplikacji, jeśli Twoja implementacja będzie je wywoływać. To samo dotyczy nazw i adresów URL magazynów.

> [!NOTE]
> Usługa Key Vault obsługuje poza ciągami dwa dodatkowe rodzaje wpisów tajnych &mdash; *klucze* i *certyfikaty* &mdash; i udostępnia przydatne funkcje specyficzne dla ich zastosowań. Ten moduł nie zawiera omówienia tych funkcji i koncentruje się na ciągach wpisów tajnych, takich jak hasła i parametry połączenia.
