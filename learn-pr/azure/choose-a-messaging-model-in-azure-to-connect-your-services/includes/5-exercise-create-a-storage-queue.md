W tym ćwiczeniu utworzysz nowe konto usługi Storage w ramach subskrypcji platformy Azure. Następnie użyjesz usługi Azure Cloud Shell, aby utworzyć nową kolejkę, dodać do niej komunikat, a następnie odczytać komunikat i usunąć go z kolejki.

Te same działania wykonują składniki w aplikacji rozproszonej. Aplikacja mobilna może na przykład dodać komunikat do kolejki, gdzie oczekuje on na pobranie i przetworzenie przez usługę internetową.

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Ponieważ kolejki usługi Storage są częścią konta usługi Storage ogólnego przeznaczenia platformy Azure, należy rozpocząć od utworzenia konta usługi Storage:

1. W przeglądarce przejdź do witryny [Azure Portal](http://portal.azure.com) i zaloguj się przy użyciu swoich zwykłych poświadczeń.
1. W lewym górnym rogu kliknij pozycję **Wszystkie usługi**.
1. Przewiń w dół do sekcji **Storage**, a następnie kliknij przycisk **Konta magazynu**.
1. W lewym górnym rogu bloku**Konta magazynu** kliknij polecenie **Dodaj**.

    ![Tworzenie konta magazynu](../images/5-create-a-storage-account-1.png)

1. W polu tekstowym **Nazwa** wpisz unikatową nazwę konta magazynu.
1. W obszarze **Model wdrożenia** upewnij się, że wybrano opcję **Resource Manager**.
1. Na liście rozwijanej **Rodzaj konta** wybierz pozycję **Magazyn (ogólnego przeznaczenia wersja 2)**.
1. Na liście rozwijanej **Lokalizacja** wybierz pobliski region.
1. Wybierz pozycję **Magazyn lokalnie nadmiarowy (LRS)** z listy rozwijanej **Replikacja**.
1. W obszarze **Wydajność** wybierz opcję **Standardowa**.
1. W obszarze **Warstwa dostępu** wybierz pozycję **Chłodna**.
1. W obszarze **Wymagany bezpieczny transfer** wybierz pozycję **Wyłączony**.
1. W obszarze **Subskrypcja** wybierz swoją subskrypcję.

    ![Tworzenie konta magazynu](../images/5-create-a-storage-account-2.png)

1. W obszarze **Grupa zasobów** wybierz polecenie **Utwórz nową**, a następnie w polu tekstowym wpisz nazwę **MusicSharingResourceGroup**.
1. W obszarze **Sieci wirtualne** wybierz pozycję **Wyłączone**, a następnie kliknij polecenie **Utwórz**.

    ![Tworzenie konta magazynu](../images/5-create-a-storage-account-3.png)

Na platformie Azure zostanie utworzone nowe konto magazynu i nowa grupa zasobów.

## <a name="create-a-queue"></a>Tworzenie kolejki

Po utworzeniu konta usługi Storage możesz dodać do niego nową kolejkę. Należy utworzyć kolejkę przy użyciu poleceń programu PowerShell:

1. W prawym górnym rogu portalu kliknij link **Cloud Shell**.

    ![Uruchamianie usługi Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. Na ekranie **Witamy w usłudze Azure Cloud Shell** kliknij przycisk **PowerShell (Linux)**.
1. Jeśli pojawi się ekran **Nie masz zainstalowanego magazynu**, kliknij przycisk **Utwórz magazyn**.
1. Aby uzyskać konto magazynu, po wyświetleniu wiersza polecenia `PS Azure` wpisz następujące polecenie, zastępując nazwę `<storageaccountname>` unikatową nazwą Twojego konta magazynu, i naciśnij przycisk Enter:

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. Aby uzyskać kontekst konta magazynu, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $context = $storageaccount.Context
    ```

1. Aby utworzyć nową kolejkę, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>Dodawanie komunikatu do kolejki

Po utworzeniu kolejki na koncie magazynu możesz dodać do niej komunikat.

1. Aby utworzyć nowy komunikat, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. Aby dodać nowy komunikat do nowej kolejki, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. W witrynie Azure Portal w obszarze nawigacji po lewej stronie kliknij pozycję **Wszystkie zasoby**.
1. Na liście zasobów kliknij wcześniej utworzone konto magazynu.
1. W bloku konta magazynu kliknij pozycję **Eksplorator usługi Storage (wersja zapoznawcza)**.
1. W Eksploratorze usługi Storage w obszarze **KOLEJKI** kliknij pozycję **musicsharingmessages**. W Eksploratorze usługi Storage zostanie wyświetlony dodany komunikat.

## <a name="retrieve-and-remove-the-message"></a>Pobieranie i usuwanie komunikatu

Docelowy składnik komunikatu w kolejce usługi Storage musi pobrać komunikat znajdujący się na początku kolejki, przetworzyć go, a następnie usunąć z kolejki, tak aby nie mogły go pobrać inne składniki:

1. Aby pobrać komunikat znajdujący się na początku kolejki w usłudze Azure Cloud Shell, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. Aby wyświetlić komunikat, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $retrievedMessage.AsString
    ```

1. Aby wyświetlić wszystkie właściwości komunikatu, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $retrievedMessage
    ```

1. Aby usunąć komunikat z kolejki, wpisz następujące polecenie i naciśnij przycisk Enter:

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. Aby odświeżyć wyświetlaną kolejkę w bloku Konto magazynu w witrynie Azure Portal, kliknij przycisk **Przegląd**, a następnie kliknij pozycję **Eksplorator usługi Storage**.
1. W obszarze **KOLEJKI** kliknij pozycję **musicsharingmessages**. W Eksploratorze usługi Storage zobaczysz, że kolejka jest pusta, ponieważ jedyny komunikat został usunięty.

## <a name="cleanup"></a>Czyszczenie

Aby usunąć wszystkie zasoby utworzone w tym ćwiczeniu, wprowadź następujące polecenie w usłudze Azure Cloud Shell. 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a>Podsumowanie

Utworzono konto usługi Storage w ramach subskrypcji platformy Azure i utworzono na nim nową kolejkę. Użyto również programu PowerShell, aby symulować działania składników aplikacji rozproszonej poprzez dodanie komunikatu do kolejki, a następnie pobranie go i usunięcie.

Kolejki konta usługi Azure Storage są dobrym rozwiązaniem, gdy chcesz przekazywać komunikaty pomiędzy składnikami aplikacji rozproszonej. Jeśli chcesz publikować zdarzenia, kolejki usługi Storage nie są dobrym rozwiązaniem.