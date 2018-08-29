Wyobraź sobie, że pracujesz w firmie, która przetwarza dane z kamer monitorujących ruch drogowy. Strumienie wideo są w wyznaczonych okresach analizowane, kategoryzowane i przetwarzane w celu zidentyfikowania twarzy i tablic rejestracyjnych. Te informacje są następnie przekazywane do usługi Azure Data Lake, gdzie zostaje wygenerowany przeszukiwalny indeks.

Strumienie wideo używają różnych koderów i rozdzielczości. Musisz uruchomić kilka własnościowych pakietów oprogramowania w systemie Windows, aby przeprowadzić wstępne przetwarzanie i zakodować je we wspólnym formacie wideo. Ponieważ nowe formaty pojawiają się regularnie, korzystne jest wykonywanie przetwarzania wideo na maszynach wirtualnych. Własnościowe pakiety można wtedy dodać lub zaktualizować bez zatrzymywania całego systemu.

Aby administrować oprogramowaniem do kodowania na maszynach wirtualnych z systemem Windows, należy połączyć się z interfejsem użytkownika.

W tym module dowiesz się, jak utworzyć maszynę wirtualną z systemem Windows i nawiązać z nią połączenia za pomocą protokołu RDP (Remote Desktop Protocol).

## <a name="learning-objectives"></a>Cele szkolenia
> [!div class="checklist"]
> * Utworzenie maszyny wirtualnej z systemem Windows za pomocą witryny Azure Portal.
> * Poznanie opcji, które są dostępne dla maszyn wirtualnych na platformie Azure.
> * Nawiązanie połączenia z uruchomioną maszyną wirtualną z systemem Windows za pomocą programu Podłączanie pulpitu zdalnego systemu Windows.

## <a name="prerequisites"></a>Wymagania wstępne

- Znajomość środowiska usług Azure Cloud Services.
- Znajomość maszyn wirtualnych.
