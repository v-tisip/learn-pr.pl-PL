## <a name="motivation"></a>Motywacja
Interfejs wiersza polecenia platformy Azure umożliwia pisanie poleceń i ich natychmiastowe wykonywanie. Pamiętaj, że w tym przykładzie tworzenia oprogramowania ogólnym celem jest wdrażanie nowych kompilacji do testowania aplikacji internetowej. Pierwszym krokiem jest utworzenie grupy zasobów. Pamiętaj, że celem jest tutaj utworzenie tych zasobów przy użyciu lokalnej instalacji interfejsu wiersza polecenia platformy Azure. 

W tym rozdziale pokażemy, jak za pomocą interfejsu wiersza polecenia platformy Azure zalogować się do subskrypcji platformy Azure i utworzyć nowy zasób.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Jakimi zasobami platformy Azure można zarządzać przy użyciu interfejsu wiersza polecenia platformy Azure?
Interfejs wiersza polecenia platformy Azure umożliwia sterowanie niemal każdym aspektem każdego zasobu platformy Azure. Możesz pracować z grupami zasobów, magazynem, maszynami wirtualnymi, usługą Azure Active Directory (Azure AD), kontenerami, uczeniem maszynowym itd.

Polecenia w interfejsie wiersza polecenia dzielą się na grupy i podgrupy. Każda grupa reprezentuje usługę oferowaną przez platformę Azure, a podgrupy dzielą polecenia dla tych usług na logiczne grupy. Na przykład grupa **storage** zawiera m.in. podgrupy **account**, **blob**, **storage** i **queue**.

Jak w takim razie znaleźć potrzebne polecenia? Jednym ze sposobów jest użycie polecenia **az find**. Na przykład jeśli chcesz znaleźć polecenia, które mogą ułatwić zarządzanie **obiektem blob** magazynu, użyj następującego polecenia wyszukiwania:

```bash
az find -q blob
```

Jeśli już znasz nazwę potrzebnego polecenia, bardziej przydatny może być argument **--help** dla tego polecenia. Pozwala on uzyskać szczegółowe informacje na temat polecenia, a w przypadku grupy poleceń — listę dostępnych poleceń podrzędnych. Tak więc w naszym przykładzie magazynu listę podgrup i poleceń umożliwiających zarządzanie magazynem obiektów blob można uzyskać w następujący sposób:

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Sposób tworzenia zasobu platformy Azure
Podczas tworzenia nowego zasobu platformy Azure zazwyczaj trzeba wykonać trzy kroki: nawiązać połączenie z subskrypcją platformy Azure, utworzyć zasób i sprawdzić, czy tworzenie zakończyło się pomyślnie (patrz poniżej).

![Procedura tworzenia zasobu za pomocą interfejsu wiersza polecenia platformy Azure](../media-drafts/4-create-resources-overview.png)

Każdy krok odnosi się do innego polecenia interfejsu wiersza polecenia platformy Azure.

### <a name="connect"></a>Połączenie
Ponieważ pracujesz z lokalną instalacją interfejsu wiersza polecenia platformy Azure, zanim możliwe będzie wykonywanie poleceń platformy Azure konieczne jest przeprowadzenie uwierzytelniania przy użyciu polecenia **login** interfejsu wiersza polecenia platformy Azure. 

```bash
az login
```

Interfejs wiersza polecenia platformy Azure zazwyczaj uruchamia domyślną przeglądarkę w celu otwarcia strony logowania platformy Azure. Jeśli to nie działa, postępuj zgodnie z instrukcjami wiersza polecenia i wprowadź kod autoryzacji na stronie [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

Po pomyślnym zalogowaniu nastąpi połączenie z subskrypcją platformy Azure. 

### <a name="create"></a>Przycisk Utwórz
Przed utworzeniem nowej usługi platformy Azure często konieczne jest utworzenie nowej grupy zasobów, dlatego użyjemy grup zasobów jako przykładu, aby pokazać sposób tworzenia zasobów platformy Azure z poziomu interfejsu wiersza polecenia.

Polecenie interfejsu wiersza polecenia platformy Azure **group create** powoduje utworzenie grupy zasobów. Musisz określić nazwę i lokalizację. Nazwa musi być unikatowa w ramach Twojej subskrypcji. Lokalizacja określa, gdzie będą przechowywane metadane dla Twojej grupy zasobów. Do określania lokalizacji służą ciągi, takie jak „Zachodnie stany USA”, „Europa Północna” lub „Indie Zachodnie”. Można również użyć odpowiedników w postaci pojedynczych słów, takich jak westus, northeurope lub westindia. Podstawowa składnia jest następująca:

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a>Weryfikuj
W przypadku wielu zasobów platformy Azure interfejs wiersza polecenia platformy Azure udostępnia polecenie podrzędne **list** umożliwiające wyświetlenie szczegółowych informacji o zasobie. Na przykład polecenie interfejsu wiersza polecenia Azure **group list** powoduje wyświetlenie listy grup zasobów platformy Azure. W tym przypadku przydaje się ono do sprawdzenia, czy tworzenie grupy zasobów zakończyło się pomyślnie:

```bash
az group list
```

Aby uzyskać bardziej zwięzły widok, można sformatować dane wyjściowe jako prostą tabelę:

```bash
az group list --output table
```
