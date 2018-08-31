W tym module pokazano, jak utworzyć konto usługi Azure Cosmos DB, którego możesz używać w rzeczywistych scenariuszach, takich jak aplikacje do handlu detalicznego online. Tworząc bazę danych za pomocą inteligentnego klucza partycji, będziesz mieć możliwość skalowania w poziomie wraz ze wzrostem zapotrzebowania na magazyn danych. Omówiono również zapotrzebowanie aplikacji na jednostki żądań oraz sposób ich ustawiania podczas tworzenia konta, aby umożliwić późniejsze skalowanie przepływności w górę, gdy potrzeby użytkowników wzrosną.

## <a name="cleanup"></a>Czyszczenie

Jeśli planujesz kontynuować pracę z modułami w tej ścieżce szkoleniowej, pomiń proces czyszczenia. W przeciwnym razie usuń zasoby, aby uniknąć naliczania opłat za korzystanie z usługi, wykonując następujące kroki:

1. W witrynie Azure Portal wybierz **grupy zasobów** daleko po lewej stronie, a następnie wybierz utworzoną grupę zasobów.  

    Jeśli menu po lewej stronie jest zwinięte, kliknij ![przycisk Rozwiń,](../media/5-create-a-database-and-collection/expand.png) aby je rozwinąć.

   ![Metryki w witrynie Azure Portal](../media/5-create-a-database-and-collection/delete-resources-select.png)

2. W nowym oknie wybierz grupę zasobów, a następnie kliknij pozycję **Usuń grupę zasobów**.

   ![Metryki w witrynie Azure Portal](../media/5-create-a-database-and-collection/delete-resources.png)

3. W nowym oknie wpisz nazwę grupy zasobów, która ma zostać usunięta, a następnie kliknij pozycję **Usuń**.

