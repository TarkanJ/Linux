** Jak checknout jestli je Linux Server is Hacked **
----------------------------------------------------

```
lastlog 
```

- zkontroluje pokusy o přihlášení


```
sudo cat /var/log/auth.log | grep "Failed"
```

- tento příkaz kontroluje soubor auth.log, kde Linux zaznamenává pokusy o přihlášení. Pokud se v krátkém období vyskytne mnoho neúspěšných pokusů o přihlášení, mohlo by to znamenat útok hrubou silou.


```
top (htop - better graphical look! <3)
```

- zkontroluje běžící procesy a kolik zabírají paměti


```
ps aux
```

- kontrola všech běžících procesů, včetně cesty k procesum


```
sudo lsof -i -P -n
```

- tento příkaz vypíše všechny otevřené porty a s nimi spojené procesy. Neznámé nebo otevřené porty mohou být známkou neoprávněného přístupu.

```
netstat -tulnp
```

- hledejte připojení na neobvyklých portech nebo cizí IP adresy, které se zdají být mimo vaše místo.
- můžete také použít příkaz iftop pro přehled o využití šířky pásma v reálném čase:

```
sudo iftop
```

- tento nástroj pomáhá monitorovat síťový provoz a detekovat jakékoli neobvyklé přenosy dat nebo podezřelé IP adresy.

```
sudo find / -type f -mtime -1
```

- zkontrolujte nově upravené soubory pomocí příkazu find

- zobrazí se soubory, které byly upraveny za posledních 24 hodin. Jakékoli neočekávané úpravy mohou naznačovat, že do systému byl přidán škodlivý skript nebo zadní vrátka.

```
find -type f -mtime -15 -ls

```

- Tato funkce vyhledá všechny soubory, které byly upraveny za posledních 15 dní. Toto číslo můžete samozřejmě změnit tak, aby odráželo období, které je pro váš případ použití realističtější. Můžete také použít hodnotu +15 pro všechny soubory, které byly upraveny před 15 dny (například 5. března, pokud příkaz spustíte 20. března). To je užitečné, pokud máte podezření na kompromitaci v určitý den.

```
find /var/log/ -type f -mtime -15 -ls
```

- Často je také užitečné zkontrolovat konkrétní složku – například složku protokolů, abyste zjistili, zda některá z nich nebyla upravena nebo aktualizována

- Pro další zkoumání můžete zkontrolovat časové razítko konkrétního souboru pomocí příkazu stat. Například:

```
stat /var/log/malware.sh

sudo aide --check
```

- Pro sledování integrity souborů zvažte použití nástrojů, jako je AIDE (Advanced Intrusion Detection Environment), které pomáhají detekovat neoprávněné úpravy souborů:

```
dpkg --get-selections
```

- Seznam všech nainstalovaných balíčků (dpkg pro Debian, rpm pro RED HAT,

RPM based)
----------

```
rpm -qa
```

- Hledejte balíčky, které jste nenainstalovali nebo nepoznáváte. Může se jednat o malware nebo neoprávněné nástroje.


```
sudo cat /etc/crontab
sudo ls /etc/cron.d/
```
- Zkontrolujte výstup, zda neobsahuje neznámé položky, které nepatří správcům systému ani vašemu legitimnímu softwaru.
- Pro úlohy cron specifické pro uživatele použijte:

```
crontab -l
```

Protokoly k prohlížení:

```
Auth.log: Tento protokol uchovává záznamy o událostech souvisejících s ověřováním,
```

- včetně přihlášení a aktivity příkazu sudo.

```
sudo cat /var/log/auth.log
```

- Syslog: 

Tento protokol ukládá obecné aktivity systému a může obsahovat informace o
neobvyklém chování.

```
sudo cat /var/log/syslog
```
