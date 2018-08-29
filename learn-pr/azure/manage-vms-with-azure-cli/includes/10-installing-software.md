<span data-ttu-id="b6942-101">Ostatnim zadaniem, które chcemy spróbować wykonać na naszej maszynie wirtualnej jest zainstalowanie serwera internetowego.</span><span class="sxs-lookup"><span data-stu-id="b6942-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="b6942-102">Jednym z najprostszych pakietów do zainstalowania jest pakiet `nginx`.</span><span class="sxs-lookup"><span data-stu-id="b6942-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="b6942-103">Znajdź publiczny adres IP swojej maszyny wirtualnej z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="b6942-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="b6942-104">Pamiętaj, że w celu jego wyszukania możesz użyć polecenia `vm list-ip-addresses`.</span><span class="sxs-lookup"><span data-stu-id="b6942-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

2. <span data-ttu-id="b6942-105">Następnie otwórz połączenie `ssh` z maszyną (tak samo, jak podczas testowania).</span><span class="sxs-lookup"><span data-stu-id="b6942-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="b6942-106">Pamiętaj, że trzeba będzie przekazać nazwę administratora („**aldis**”).</span><span class="sxs-lookup"><span data-stu-id="b6942-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

3. <span data-ttu-id="b6942-107">W przedstawionej powłoce wykonaj następujące polecenie, aby zainstalować serwer internetowy `nginx`.</span><span class="sxs-lookup"><span data-stu-id="b6942-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. <span data-ttu-id="b6942-108">W usłudze Azure Cloud Shell odczytaj domyślną stronę z serwera internetowego z systemem Linux za pomocą polecenia `curl`.</span><span class="sxs-lookup"><span data-stu-id="b6942-108">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="b6942-109">Alternatywnie możesz otworzyć nową kartę przeglądarki i przejść do publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="b6942-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="b6942-110">Zakończy się to niepowodzeniem, ponieważ maszyna wirtualna z systemem Linux nie uwidacznia portu 80 (`http`) przez wbudowaną zaporę.</span><span class="sxs-lookup"><span data-stu-id="b6942-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="b6942-111">Na szczęście interfejs wiersza polecenia platformy Azure oferuje odpowiednie polecenie: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="b6942-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

5. <span data-ttu-id="b6942-112">W usłudze Cloud Shell wpisz poniższe polecenie, aby otworzyć port 80:</span><span class="sxs-lookup"><span data-stu-id="b6942-112">Type the following into Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="b6942-113">Spróbuj ponownie wykonać polecenie `curl`.</span><span class="sxs-lookup"><span data-stu-id="b6942-113">Finally, try `curl` again.</span></span> <span data-ttu-id="b6942-114">Tym razem powinno ono zwrócić dane.</span><span class="sxs-lookup"><span data-stu-id="b6942-114">This time it should return data.</span></span> <span data-ttu-id="b6942-115">Strona będzie także widoczna w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="b6942-115">You can see the page in a browser as well.</span></span>



