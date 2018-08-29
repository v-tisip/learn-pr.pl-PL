W tym module zabezpieczono konfigurację wpisu tajnego aplikacji w usłudze Azure Key Vault. Kod naszej aplikacji uwierzytelnia się w magazynie przy użyciu tożsamości usługi zarządzanej i automatycznie ładuje wpisy tajne z magazynu do systemu konfiguracji platformy ASP.NET Core przy uruchamianiu.

## <a name="cleanup"></a>Czyszczenie

Aby wyczyścić swoją subskrypcję platformy Azure, uruchom następujące polecenie w usłudze Azure Cloud Shell w celu usunięcia grupy zasobów zawierającej wszystkie zasoby utworzone w tym module.

```console
az group delete --name keyvault-exercise-group
```

Aby wyczyścić magazyn usługi Cloud Shell, usuń katalog `KeyVaultDemoApp`.

## <a name="next-steps"></a>Następne kroki

Gdyby to była prawdziwa aplikacja, co byłoby dalej?

* Umieszczenie wszystkich wpisów tajnych aplikacji w Twoich magazynach! Nie ma już żadnego powodu, aby trzymać je w plikach konfiguracji.
* Kontynuuj do programowania aplikacji. Środowisko produkcyjne jest już skonfigurowane, dzięki czemu przy przyszłych wdrożeniach w nim nie trzeba powtarzać wszystkich kroków konfiguracji.
* Aby wspierać programowanie, utwórz magazyn środowiska programowania, który będzie zawierać wpisy tajne o tych samych nazwach, ale różnych wartościach. Przyznaj uprawnienia zespołowi programistycznemu i skonfiguruj nazwę magazynu w pliku konfiguracji środowiska programowania aplikacji. Gdy deweloperzy będą uruchamiać aplikację lokalnie, funkcja `AddAzureKeyVault` będzie automatycznie wykrywać lokalne instalacje programu Visual Studio oraz interfejsu wiersza polecenia platformy Azure i używać poświadczeń platformy Azure skonfigurowanych w tych aplikacjach do logowania się i uzyskiwania dostępu do magazynu.
* Utwórz dodatkowe środowiska do celów takich jak testy akceptacyjne użytkowników.
* Rozdziel magazyny pomiędzy różne subskrypcje i/lub grupy zasobów, aby je odizolować.
* Przyznaj dostęp do magazynów w innych środowiskach odpowiednim osobom.

## <a name="further-reading"></a>Dalsze informacje

* [Dokumentacja usługi Key Vault](https://docs.microsoft.com/azure/key-vault/)
* [Więcej informacji o funkcji AddAzureKeyVault i jej opcjach zaawansowanych](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)
* [W tym samouczku](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) zaprezentowano korzystanie z elementu `KeyVaultClient`, w tym ręczne uwierzytelnianie go w usłudze Azure Active Directory za pomocą wpisu tajnego klienta zamiast tożsamości usługi zarządzanej.
* [Dokumentacja usługi tokenu tożsamości usługi zarządzanej](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol) do samodzielnego implementowania przepływu pracy uwierzytelniania