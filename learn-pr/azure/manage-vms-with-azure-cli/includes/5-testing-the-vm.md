<span data-ttu-id="b917e-101">Gdy tworzysz maszynę wirtualną, ma ona przypisywany publiczny adres IP, który jest dostępny przez Internet, oraz prywatny adres IP używany w ramach centrum danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b917e-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="b917e-102">Korzystając z narzędzia `ssh`, możemy szybko sprawdzić, czy maszyna wirtualna z systemem Linux działa i jest gotowa do użytku.</span><span class="sxs-lookup"><span data-stu-id="b917e-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="b917e-103">Pamiętaj, że nasza nazwa administratora to `aldis`, musimy więc to określić.</span><span class="sxs-lookup"><span data-stu-id="b917e-103">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="b917e-104">Nie potrzebujemy hasła, ponieważ tworząc maszynę wirtualną, wygenerowaliśmy parę kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="b917e-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="b917e-105">Podczas pierwszego przechodzenia przez powłokę maszyny wirtualnej zostanie wyświetlony monit dotyczący autentyczności hosta.</span><span class="sxs-lookup"><span data-stu-id="b917e-105">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="b917e-106">Jest to spowodowane tym, że korzystamy bezpośrednio z adresu IP, a nie z nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="b917e-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="b917e-107">Wybranie opcji „tak” spowoduje, że adres IP zostanie zapisany jako poprawny host dla połączenia i pozwoli na kontynuowanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="b917e-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="b917e-108">Następnie zostanie wyświetlona powłoka zdalna umożliwiająca wprowadzanie poleceń systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b917e-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="b917e-109">Wprowadź kilka poleceń w ramach testów, a gdy skończysz, wyloguj się z konta (wpisz `logout` lub `exit` w powłoce).</span><span class="sxs-lookup"><span data-stu-id="b917e-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>