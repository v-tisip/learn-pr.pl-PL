## <a name="creating-key-vaults-for-your-applications"></a>Tworzenie magazynów Key Vault na potrzeby aplikacji

Dobrym rozwiązaniem jest przydzielenie poszczególnym aplikacjom osobnego magazynu dla każdego używanego środowiska wdrażania, takiego jak programowanie, testowanie i produkcja. Wygodne może okazać się udostępnianie wpisów tajnych w aplikacji, ale wpływ dostępu do odczytu magazynu przez osobę atakującą zwiększa się wraz z liczbą wpisów tajnych w magazynie.

> [!TIP]
> Jeśli używasz takich samych nazw wpisów tajnych w różnych środowiskach, jedyną konfiguracją specyficzną dla środowiska, którą trzeba zmienić w aplikacji, jest adres URL magazynu.

Tworzenie magazynu nie wymaga konfiguracji początkowej. Tożsamość użytkownika ma automatycznie przyznawany pełen zestaw uprawnień do zarządzania wpisami tajnymi i natychmiast można rozpocząć dodawanie wpisów tajnych. Po utworzeniu magazynu można dodawać wpisy tajne i zarządzać nimi przy użyciu dowolnego interfejsu administracyjnego platformy Azure, w tym witryny Azure Portal, interfejsu wiersza polecenia platformy Azure i programu Azure PowerShell. W przypadku konfigurowania aplikacji do używania magazynu trzeba przypisać do niej prawidłowe uprawnienia; zobaczymy to w kolejnej sekcji.

## <a name="vault-authentication-and-permissions"></a>Uwierzytelnianie i uprawnienia użytkownika magazynu

Interfejs API usługi Azure Key Vault używa usługi Azure Active Directory do uwierzytelniania użytkowników i aplikacji. Zasady dostępu do magazynu opierają się na *akcjach* i są stosowane do całego magazynu. Na przykład aplikacja z uprawnieniami do **pobierania** (odczytywania wartości wpisów tajnych), **tworzenia listy** (tworzenia listy wszystkich wpisów tajnych) i **ustawiania** (tworzenia lub aktualizowania wartości wpisów tajnych) do magazynu może tworzyć wpisy tajne, wyświetlać listę wszystkich nazw wpisów tajnych oraz pobierać i ustawiać wszystkie wartości wpisów tajnych w tym magazynie.

*Wszystkie* akcje wykonywane w magazynie wymagają uwierzytelniania i autoryzacji &mdash; nie ma możliwości przyznania żadnych praw dostępu anonimowego.

> [!TIP]
> W przypadku udzielania dostępu do magazynu deweloperom i aplikacjom należy przyznać tylko minimalny wymagany zestaw uprawnień. Ograniczenia uprawnień pomagają uniknąć awarii spowodowanych przez usterki kodu i zmniejszyć wpływ kradzieży poświadczeń lub wstrzyknięcia złośliwego kodu do aplikacji.

Deweloperzy będą przeważnie potrzebować tylko uprawnień do **pobierania** i **tworzenia listy** w magazynie środowiska programistycznego. Lider lub starszy deweloper będzie potrzebować pełnych uprawnień do magazynu, aby w razie potrzeby zmieniać i dodawać wpisy tajne. Pełne uprawnienia do magazynów w środowisku produkcyjnym są zazwyczaj rezerwowane dla starszego personelu operacyjnego.

W przypadku aplikacji są zazwyczaj wymagane tylko uprawnienia do **pobierania**. Niektóre aplikacje mogą wymagać uprawnień do tworzenia **listy**, w zależności od sposobu implementowania aplikacji. Aplikacja, którą zaimplementujemy w ramach ćwiczenia w tym module wymaga uprawnienia do **tworzenia listy**, z powodu techniki używanej do odczytywania wpisów tajnych z magazynu.

## <a name="exercise"></a>Ćwiczenie

Mając na uwadze wszystkie problemy z wpisami tajnymi aplikacji, kadra kierownicza poprosiła Cię o utworzenie małej aplikacji startowej, która wyznaczy właściwą ścieżkę działania dla innych deweloperów. Aplikacja musi przedstawiać najlepsze rozwiązania dotyczące jak najprostszego i jak najbezpieczniejszego zarządzania wpisami tajnymi.

Aby rozpocząć, utworzysz magazyn i będziesz przechowywać jeden wpis tajny.

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o nazwie `keyvault-exercise-group` dla wszystkich zasobów w tym ćwiczeniu. Na końcu tego modułu usuniemy tę grupę zasobów, aby wyczyścić wszystkie elementy na raz. Dla wszystkich elementów w tym ćwiczeniu użyjemy lokalizacji `eastus`.

Użyj terminalu usługi Azure Cloud Shell po prawej stronie, aby uruchomić poniższe polecenie interfejsu wiersza polecenia platformy Azure. Spowoduje to utworzenie grupy zasobów w subskrypcji.

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a>Tworzenie magazynu i przechowywanie w nim wpisu tajnego

Następnie utworzymy magazyn i będziemy w nim przechowywać nasz wpis tajny.

**Nazwy magazynów Key Vault muszą być globalnie unikatowe, dlatego musisz wybrać unikatową nazwę**. Nazwy magazynów muszą zawierać od 3 do 24 znaków oraz wyłącznie znaki alfanumeryczne i łączniki.

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

Po zakończeniu zobaczysz dane wyjściowe JSON opisujące nowy magazyn.

Teraz dodaj wpis tajny: nasz wpis tajny będzie miał nazwę **SecretPassword** o wartości **reindeer_flotilla**.

```azurecli
az keyvault secret set --name SecretPassword --value open_sesame --vault-name <your-unique-vault-name>
```

Zanotuj nazwę magazynu &mdash;, ponieważ będziesz jej wkrótce ponownie potrzebować.

Będziemy wkrótce pisać kod dla naszej aplikacji, ale najpierw musimy dowiedzieć się trochę na temat sposobu uwierzytelniania naszej aplikacji w magazynie.