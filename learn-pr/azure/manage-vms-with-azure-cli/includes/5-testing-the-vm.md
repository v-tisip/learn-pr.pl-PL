Gdy tworzysz maszynę wirtualną, ma ona przypisywany publiczny adres IP, który jest dostępny przez Internet, oraz prywatny adres IP używany w ramach centrum danych platformy Azure. Korzystając z narzędzia `ssh`, możemy szybko sprawdzić, czy maszyna wirtualna z systemem Linux działa i jest gotowa do użytku. Pamiętaj, że nasza nazwa administratora to `aldis`, musimy więc to określić.

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> Nie potrzebujemy hasła, ponieważ tworząc maszynę wirtualną, wygenerowaliśmy parę kluczy SSH. Podczas pierwszego przechodzenia przez powłokę maszyny wirtualnej zostanie wyświetlony monit dotyczący autentyczności hosta. 
> 
> Jest to spowodowane tym, że korzystamy bezpośrednio z adresu IP, a nie z nazwy hosta. Wybranie opcji „tak” spowoduje, że adres IP zostanie zapisany jako poprawny host dla połączenia i pozwoli na kontynuowanie połączenia.

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

Następnie zostanie wyświetlona powłoka zdalna umożliwiająca wprowadzanie poleceń systemu Linux.

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

Wprowadź kilka poleceń w ramach testów, a gdy skończysz, wyloguj się z konta (wpisz `logout` lub `exit` w powłoce).