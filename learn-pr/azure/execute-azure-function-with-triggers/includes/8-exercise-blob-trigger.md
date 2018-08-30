Podczas tego ćwiczenia utworzymy funkcję platformy Azure, która wyświetla nazwę i rozmiar obiektu blob, gdy jest on tworzony lub aktualizowany. 

> [!NOTE]
> Aby wykonać to ćwiczenie, musisz zalogować się w witrynie [Azure Portal](https://portal.azure.com/) przy użyciu prawidłowego konta.

## <a name="create-a-blob-trigger"></a>Tworzenie wyzwalacza obiektu blob

Ponownie kontynuujmy korzystanie z naszej istniejącej aplikacji usługi Azure Functions i dodajmy wyzwalacz obiektu blob.

1. Wskaż pozycję **Funkcje** i wybierz ikonę plus (+).

    ![Wskazywanie pozycji Funkcje i wybieranie ikony plusa](../media-drafts/4-hover-function.png)

1. Wybierz pozycję **Wyzwalacz obiektu blob**.

1. Wybierz język **C#**. 

1. W polu **Nazwa** pozostaw wartość domyślną.

1. W polu **Ścieżka** pozostaw wartość domyślną.

1. Wybierz istniejące konto usługi Azure Storage lub wybierz pozycję **Utwórz**, jeśli chcesz utworzyć nowe konto na platformie Azure.

## <a name="download-storage-explorer"></a>Pobieranie Eksploratora usługi Storage

Teraz, gdy utworzyliśmy wyzwalacz obiektu blob, pobierz Eksploratora usługi Storage, który pozwoli na łatwe utworzenie obiektu blob.

- Pobierz [Eksploratora usługi Storage](http://storageexplorer.com).

## <a name="connect-to-your-azure-storage-account"></a>Nawiązywanie połączenia z kontem usługi Azure Storage

Pobraliśmy już Eksploratora usługi Storage. Zalogujmy się przy użyciu podanych przez nas poświadczeń.

1. W Eksploratorze usługi Storage wybierz ikonę plusa (+) po lewej stronie.

1. Wybierz pozycję **Użyj klucza i nazwy konta magazynu**.

1. Wybierz opcję **Dalej**.

1. Na platformie Azure w obszarze wyzwalacza obiektu blob wybierz pozycję **Zintegruj**.

1. Wybierz pozycję **Dokumentacja**, aby rozszerzyć widok.

1. Skopiuj wartości **Nazwa konta** i **Klucz konta**.

1. W Eksploratorze usługi Storage wklej skopiowane właśnie wartości **Nazwa konta** i **Klucz konta**.

1. Wypełnij pole **Nazwa wyświetlana**. Ta wartość jest nazwą połączenia w Eksploratorze usługi Storage.

1. Wybierz opcję **Dalej**.

1. Wybierz przycisk **Połącz**. 

## <a name="create-a-blob-container"></a>Tworzenie kontenera obiektów blob

Nie jesteśmy połączeni z naszym kontem usługi Azure Storage. Pamiętaj, że nasz wyzwalacz obiektu blob monitoruje tylko lokalizację opisaną w polu **Ścieżka**. Domyślnie ścieżka powinna wyglądać następująco:

> samples-workitems/{name}

Musimy utworzyć kontener o nazwie **samples-workitems**.

1. W Eksploratorze usługi Storage rozwiń swoje konto magazynu. Jego nazwa powinna być zgodna z wartością wprowadzoną w polu **Nazwa wyświetlana** podczas procesu połączenia.

1. Kliknij prawym przyciskiem myszy pozycję **Kontenery obiektów blob** i wybierz pozycję **Utwórz kontener obiektów blob**.

1. Wprowadź ciąg **samples-workitems**.

## <a name="turn-on-your-blob-trigger"></a>Włączanie wyzwalacza obiektu blob

Teraz, gdy utworzyliśmy kontener do monitorowania, uruchomimy naszą funkcję, aby wyświetlić dane wyjściowe podczas tworzenia obiektu blob.

1. Wybierz swój wyzwalacz obiektu blob, aby otworzyć ekran kodu.

1. Wybierz pozycję **Uruchom**.

## <a name="create-a-blob"></a>Tworzenie obiektu blob

Wyzwalacz obiektu blob jest teraz włączony i nasłuchuje działań. Utwórzmy obiekt blob, aby sprawdzić, czy uzyskamy komunikat dziennika.

1. W Eksploratorze usługi Storage wybierz kontener **samples-workitems**.

1. Wybierz pozycję **Przekaż**. 

1. Wybierz pozycję **Przekaż pliki**.

1. Wybierz dowolny plik z komputera.

1. Wybierz pozycję **Przekaż**.

1. Wróć do platformy Azure. Sprawdź, czy w dziennikach znajduje się komunikat informujący o przekazanym pliku.

## <a name="clean-up"></a>Czyszczenie

Aby upewnić się, że za tę funkcję nie zostaną naliczone opłaty, nad oknem dziennika wybierz polecenie **Wstrzymaj**.

![Wstrzymaj](../media-drafts/4-pause-timer.png)


