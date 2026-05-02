** ALIAS => zadat v konsoli toto: "alias k=kubectl" **
a prida alias do souboru ~/.bashrc

# Hezky a prehledne velikosti adresaru
ncdu

# Prehledne a v tabulce velikosti souboru a adresaru
duf

# Prikaz "fdfind" najde umistneni vsech Dockerfile v systemu!
fdfind '^Dockerfile$'

# parametr -H means "Hidden files"
fdfind -H '\.env'

# I’m thankful for the Linux fuzzy finder tool because it superpowers the command line by making it fast to find whatever I’m looking for
fzf

# EXA showing ICONS!
exa --icons /home/jojovaio/Plocha/


** Diskové Nástroje - Správa, Partition, Oddíly **
--------------------------------------------------

- Hlavní program na partition je samozřejmě "fdisk"

Výborný výpis všech detailů, včetně nainstalovaných operačních systémů

"fdisk -l" je potřeba být ale jako root


- Výborná vychytávka na vypsání všech zařízení v počítači !!!


This command shows all the ATA and SCSI devices detected by your kernel
```
ls /dev|grep '[s|h]d[a-z]'
```

- Zde vypíše všechna připojená zařízení
```
mount|grep ^'/dev'
```

- a zde veškeré CD/DVD mechaniky pokud jich je více, např. "virtuální"
```
ls /dev|grep sr
```

- Zjištění volné kapacity disku !!!
Nejlepší!!!
```
df -TH /
```
nebo např.
```
df -h /dev/sda1
```
- Vypsání UUID (Universally Unique Identifier) disku
Buď
```
1.	ls -l /dev/disk/by-uuid/

Nebo
2.	blkid /dev/sda1
```

** FStab **
-----------
tabulka systémů souborů = nachází se v /etc/fstab

v ní je možno (pokud nefunguje) upravit podle UUID danou oblast(disk)
a nastavit tak, aby system se při bootu do tohoto souboru podíval ;)

 Viz Zde:
```
 /etc/fstab: static file system information.

 Use 'blkid' to print the universally unique identifier for a
 device; this may be used with UUID= as a more robust way to name devices
 that works even if disks are added and removed. See fstab(5).

 <file system> <mount point>   <type>  <options>       <dump>  <pass>
 / was on /dev/sda1 during installation
UUID=979674aa-ef5c-4d11-8929-2ab2e83f170d /               ext4    errors=remount-ro 0       1
 /home was on /dev/sda2 during installation
UUID=6b102316-e5ea-4c63-a202-e3dd6f883a8f /home           ext4    defaults        0       2
 swap was on /dev/sda3 during installation
UUID=36616418-518c-4754-bfd8-79d07d778b11 none            swap    sw              0       0
/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0
```

admin Martinek ;)


** Reset hesel ve Windows XP & Win7 (v Linuxu :o)) **
-----------------------------------------------------

- Nejdrive odpojit daný disk(umount) nebo přes nástroj Gparted

- Potom příkaz
```
ntfs-3g /dev/sda(bacha,zjistit presne daný disk,kde se nachází!) /mnt/widle -o force
```
Nebo parametr -rw místo "force"


- Potom příkaz
```
cd /mnt/widle/Windows/System32/config
```

- No a nakonec
```
chntpw -l SAM

chntpw -u (Uživatel) SAM
```

Hotovo!!!


** Reset Roota V Linuxu!!! **
-----------------------------
- fdisk -l

- Zde vybrat disk, ktery je bootovaci a je na nem linux viz priklad
```
Device		Boot	Start	End	Blocks	Id	System

/dev/sda1	*	1	neco	neco	neco	Linux
```
- mkdir /media/sda1 (pokud se nevytvori naraz nepanikarit, vytvorit

- nejprve "mkdir media" a potom "mkdir media/sda1"

- mount /dev/sda1 /media/sda1

- chroot /media/sda1

- passwd root :)))

* REBOOT a je to!!!


** Zjištění identity uživatele **
---------------------------------
- id, whoami

Vypis nalogovanych uživatelů

- who, w

Výpis logu relací

- last

** BASH Terminál **
-------------------
- Nastaveni "BASH"e
/etc/bash.bashrc

- Historie hledani prikazu
Ctrl + r

- Vymazani terminalu
Ctrl + l

- Pohyb ve vypisu
Shift + PgUp/PgDn

Totální vymazání historie v bashi

cat /dev/null > ~/.bash_history && history -c && exit


** Adresáře, Soubory!!! **
--------------------------
```
cd SAMOTNY PRIKAZ PREPNE DO DOMOVSKEHO ADRESARE!!!

cd - RYCHLY NAVRAT DO PREDCHOZIHO ADRESARE!

cd ~ Přepne do domovského adresáře

cd "adresář" - Vstup do adresáře o úroveň níže

cd .. - Výstup, opuštění z adresáře o úroveň výše

cd / - vleze do kořenového adresáře, tzv. "root"

ll - podrobný výpis (jako dir v DOSu)

ll -a - nejpodrobnější výpis

ls -lt - zobrazi podle casu posledni zmeny a na radek jed.soubory/adresare

ll -rt | tail - zobrazí v opačném pořadí nejnovější soubory

ls -lat - vypise uplne vsechno, na radky a podle casu, nej prikaz!!! ;)

pwd - Zobrazení cesty, kde se nacházím

cksum - zjistí velikost souboru

file - zjistí podrobnosti o souboru

id, finger, whoami - informace o uživatelích

env - Zjistí velikost proměnných v systému (moc jsem nepoužil :/ )

wc -c --bytes "soubor" ("word count" zjistí velikost souboru v bytech)

touch - vytváření novych souborů, možnost jejich změny

Kopirovani Souboru

cp "soubor" "nazev_adresare" (soubor je zkopirovan do adresaře ve stejne urovni jako je soubor)

cp "soubor" ../etc/"adresar" (soubor je zkopirovan do adresáře na vyšší urovni(1.úroveň), tj. přibližuje se do kořenového adresáře, tzv. "rootu" :)

which "soubor"

whereis "název_programu" - ukáže cestu k programu

locate - zjistí výskyty hledaného souboru, podobně jako "find" příkaz

(zjisti velmi podrobne info o souboru/adresáři)
```

- Výstup do souboru
```
prikaz > Presměrování výstupu do souboruv

prikaz >> Presmerovani vystupu do souboru a navazani souboru

prikaz < Přesměrování vstupu ze souboru

prikaz | program - Předání dat programu (tzv. "pajpa" Alt+124)
```

** URČENÍ VELIKOSTI ADRESÁŘU V kB **
```
du -h /adresar

du -sh /adresar

du -h /home/martino | sort -nr | head -n 20 (vypíše 20 adresáře podle velikosti v Kilobytech)
```

** ARCHIVACE & EXTRAHOVANI souborů, adresářů ZIP, TAR, GZ, BZ2 **
-----------------------------------------------------------------
* Zip

(zabalení) compress

** zip -r archive_name.zip directory_to_compress ** 

(rozbalení) extract

** unzip archive_name.zip **


* Tar

(zabalení) compress

** tar -cvf archive_name.tar.gz directory_to_compress **

(rozbalení) extract

- rozbalí do jiného adresáře, pokud chceme :)

** tar -xvf archive_name.tar.gz -C /tmp/extract_here/ **


- Zabalení adresáře do souboru a přidá datum a čas s přesností na sekundy

** tar -cvf nazev_komprimovaneho_souboru$(date +%Y%m%d-%H%M%S).tar nazev_adresare/ **


* Tar.Gz

(zabalení) compress

** tar -zcvf archive_name.tar.gz directory_to_compress **
(rozbalení) extract

- rozbalí do jiného adresáře, pokud chceme :)

** tar -zxvf archive_name.tar.gz -C /tmp/extract_here/ **

* Tar.Bz2
- Metoda comprese, která je náročnější na čas i CPU


(zabalení) compress

** tar -jcvf archive_name.tar.bz2 directory_to_compress **

(rozbalení) extract

- rozbalí do jiného adresáře, pokud chceme :)

** tar -jxvf archive_name.tar.bz2 -C /tmp/extract_here/ **


** Users, Passwords, Groups **
------------------------------
**Jak zjistit a vypsat všechny uživatele podrobně**

**getent passwd**

- hodně "nahuštěné", ale podrobné

**cat /etc/shadow | grep -v '[!||*]'**

- tato se zdá nejlepší, vypíše opravdu všechny uživatele systému

**cat /etc/shadow | cut -d: -f 1**

- vypíše všechny přehledně pod sebou (včetně Oracle, MySQL atd. účtů)

- Vypis zda uživatel se nachazi v souboru /etc/passwd

**grep martinek /etc/passwd**

Vypis vsech skupin

**cat /etc/group**

Zmena hesla uživatelů**

**passwd "jmeno_uzivatele"**

** VIRTUALBOX - pristup na host USB!!! **

**sudo adduser YOURUSERNAME vboxusers** - log out and log in again.

** např.: adduser martino vboxusers **


** Zakládaní a rušení účtů uživatelů **
---------------------------------------

**useradd** - interaktivni programek na vytvoreni noveho uzivatele, vytvoření domovského adresáře

- toto radeji pouzit !!!

* alternativa

**adduser** - založení účtu uživatele bez domovského adresáře, neni interaktivni, je nativni v systemu

**deluser** - smazání účtu


** GENTOO - pridani noveho uzivatele (vytvoreni domovské adresare+shell a pridani do skupin) **
-----------------------------------------------------------------------------------------

**root# useradd -m -G users,wheel,audio -s /bin/bash martino**

**root# passwd martino**

**HOTOVO!** Po vytvoreni tohoto uctu se lze pomoci prikazu "su" prepnout na roota ;)


** Přidání uživatele aby mohl používat příkaz "sudo" /přidání uživatele do "administrátorské" skupiny, popř. jiné/ **

1. nainstalovat apt-get install sudo (pokud neni)

2. usermod -a -G sudo martino /přidá uživatele do skupiny "sudo"/


** Odstranění uživatele ze skupiny(group) "sudo" [uzivatel jako roota pomoci prikazu "sudo"] **
-----------------------------------------------------------------------------------------------

- **gpasswd -d martino sudo** - odstraní uživatele "martino" z "administrátorské" skpiny "sudo"

* Vypis pred ostranenim uzivatele, ktery je ve skupine "sudo"
```
cat /etc/group | grep sudo
sudo:x:27:leonidas
```
* Vypis po pouziti prikazu "gpasswd" pro odstraneni uzivatele ze skupiny "sudo"
```
cat /etc/group | grep sudo
 sudo:x:27
```

** Přístupová práva CHMOD **
----------------------------
- chmod a=rwx "nazev_souboru/adresare"

Oprávnění
```
Hodnota				NAZEV SKUPIN
r(read)	   4	u - user(vlastnik)
w(write)   2	g - group(skupina)
x(eXecute) 1	o - others(ostatní)

a - all(všichni)
```

- např. chmod **u=rwx, g=rx, o=rx "soubor"**, lze zapsat totéž jako **chmod 755 "soubor"**


** Změna vlastníka CHOWN **
---------------------------
- **chown martino file.txt** - změní původniho vlastníka na "martino" :)

- ** sudo chown -R jojovaio AWS/ **  - změní celý adresář rekurzivně (včetně podadresářů a souborů) na uživatele jojovaio

- **chgrp root file.txt** (změní skupina na skupinu správci, rooty)

- **chroot** - **BACHA**, slouží ke změně kořenového adresáře, s tim si moc nehrát!!!
(používá se např. při instalaci Gentoo - abychom se "přepli" do celého kořenového adresáře "/"
viz instalace Gentoo, tzv. "chrootnutí" rootu)

** Procesy a systémové proměnné ENV **
--------------------------------------
** ps aux | grep neco ** - Zobrazi všechny vypisy procesů  a popr. vypise co hledame

** top ** - pravidelně, obnovovany vypis procesu

** ps -e | greb ssh ** => najde a vypíše (pokud existuje) prces ssh

** kill -s 9 -u "nazev_uzivatele" **

(Pošle signál 9-což je kill, všem procesům uživatele danného jmena)

** fg, bg ** - Přesun procesu bud do popředí, nebo do pozadí (foreground, background)

** ps ax | grep martino **

(vypíše všechny procesy pro daneho uživatele)

** ps -ef | grep apache **

(vypíše hezky přehledně všechny procesy tohoto jména)

** ps -fu martino **

(vypíše všechny procesy spjaté s tímto jménem)

** env ** - výpis systémových proměnných, důležitá funkce pro nastavení systému!!!

** ps -fe | grep martinek | sort -k3 **

- vypíše všecny procesy pro daneho uživatele a setřídí podle 3.sloupce



** CRON - časové spouštění úloh **
----------------------------------
** at ** - spustí jednorázově, ukončí se Ctrl + d

** atq ** - Vypis mazání úloh

** cron ** - Démon pro pravidelné spouštění programů, atd

** crontab ** - editace,mazání, výpis crontabu

** crontab -e ** - nastavení Cronu viz níže příklad

** crontab -u martino -l **

(vypíše naplánované úlohy pro tohoto uživatele)
```
SHELL=/bin/bash

PATH=/sbin:/bin:/usr/sbin:/usr/bin

MAILTO=root

 Home=/

 For details see man 4 crontabs

 Example of job definition

 .---------------- minute (0 - 59)

 |  .------------- hour (0 - 23)

 |  |  .---------- day of month (1 - 31)

 |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...

 |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat

 |  |  |  |  |

 *  *  *  *  * user-name command to be executed
```


** Konkretni Priklad nastavení crontabu! **

** 30 14 * * sun "Ahoj lidi!" **

- Napíše každou neděli, v pul třetí odpoledne "Ahoj lidi!"

** Další příklad **

** 0 0, 8, 10, 16, 18 * * 1-5 **

- Zkontroluje, kteří zaměstnanci jsou přihlášeni v systému 

od 8:00 - 10:00 do 16:00 - 18:00 od Pondělí do Pátku (1 - 5)


** SED - pokročilejší práce se soubory! **
------------------------------------------
** DIFF ** - Porovnani souboru

** diff -w soubor1.txt soubor2.txt **
- porovnani dvou souboru, ignoruje mezery

** diff -by soubor1.txt soubor2.txt **
- ignoruje mezery a prazdna mista

** diff -iy soubor1.txt soubor2.txt **
- porovna soubory a ignoruje CaseSensitive :)

** SED (Stream EDitor) **
** sed -e 's/+00/g' "vstupni_soubor" > "vystupni_soubor" **

- Nahradí všechny znaky "+" za 00 v celém souboru :

** sed -e '/ˆ *$/d' "vstupni_soubor" > "vystupni_soubor" **

- v souboru smaže prázdné řádky, nebo řádky obsahující jen mezery

** sudo sed -i 's/jirm10/grep07/g' * **

- nahradí "grep07" za "jirm10" ve VŠECH SOUBORECH v daném adresáři!


** FIND - command **
--------------------

- Hledání souboru pomocí "find"

** find / -name '*menu*' **

- najde v kořenovém adresáři všechny výskyty začínající na "menu"


** GREP - vyhledávání řetězců, vzorků v souborech atd.**
--------------------------------------------------------

** grep -i 'slovo' "soubor" **

- vypíše "slovo" v "souboru"

** grep -n 'neco' "soubor" **
- najde na kolikatém řádku nějaký výraz 'neco')


** CUT - "ořezávácí" příkaz pro přehledný výstup **
---------------------------------------------------

** cut -f 4,6 "soubor" | cat **

- vypíše 4. a 6. sloupec v souboru, musí byt ale odděleny aspoň tabulátorem, mezerou

** cut -f1 -d: /etc/passwd | sort **

- **f1** je 1.sloupec, **d:** oddelovac znaku dvojtecka, **sort** - setridi



** CAT - výpis souborů **
-------------------------

** cat soubor **

- vypíše obsah souboru na obrazovku


** Less - command **
--------------------

** ls -l | less **

- vypíše pokud je delší vypis na obrazovku, tak aby byl text postupně zobrazen

- umožňuje pohyb ve výstupu či souboru


** Head - command **
--------------------

** head soubor1 soubor2 **

- vypíše prvích 10 rádků z obou souborů


** Tail - command **
--------------------

** tail soubor **

- vypíše posledních 10 řádků ze souboru


** ASCII, HexDump, CStocs - kódování textu **
---------------------------------------------

- speciální příkazy pro kódování/formátování textu

** recode -f cp1250..uft8 "soubor" **

- dokáže odstranit diakritiku ze souboru

** cstocs cp1250 utf-8 < "soubor" **

** HD nebo Hexdump ** - vypíše v ASCII


** --->>> Linux Síťařina ;) <<<--- **
-------------------------------
** ip a (zobrazí veškerá síťová zařízení) **

** ip r (zobrazí gateway) **

** ifconfig -a (zobrazí veškerá síťová zařízení) **

** ifconfig eth0 192.168.1.9 netmask 255.255.255.0 up **

** route add default gw 192.168.1.1 **

- nastavi IP adresu a masku podsítě a gateway

** route add -net 192.168.9.0 netmask 255.255.255.0 gw 10.0.0.4 **

- nastavi IP a masku a vychozi branu-gateway

** route -n ** (základní routovací tabulka)

** route -CFvne ** (hodně podrovná routovací tabulka)

** angry IP scanner ** "propingne" vsechny pocitace v zadaném subnetu/siti

** ping ** - dostupnost cíle

** traceroute ** - cesta k cílové statnici z různých IP adrres, různé TTL (TimeToLive)

** mtr -t ** grafický traceroute

** nmap (Nmap/Zenmap GUI) ** - nejlepší nástroj na sniffování a skenování portů!!! :)

** netstat ** - vypis aktivních síťových spojení

** tcpdump ** - sledování síťového provozu, různé filtry, různé úrovně detailnosti informací

** etheral ** - sledování síťového provozu on-line grafické prostředí, textová verze

** wireshark ** - SUPER program na zachytávání paketů v síťi s GUI a podrobnou analýzou paketů aj.!!!

** ethtool ** - hw nastavení síťových karet

** pathping ** - kromě prostých statistik zobrazuje také podrobné informace o všech prvcích, jimiž testovací paket prošel

** etherwake ** - probouzení díky WOL (MagicPaket)


** Připojení Vzdálenených Sharu, Namapování **
----------------------------------------------
** mount -t cifs -o username="uziv.jm." //leonidas/downloads /mnt/ **

- musi byt nainstalovan "cifs" - **apt-get install cifs-utils**, jinak zkusit použit smbfs, misto cifs


** Wi-Fi **
-----------

- Připojení k Wi-Fi pomocí příkazové řádku z terminálu, bez grafického prostředí (menší machrovinka ;))

- JAKO PRVNI VEC SE MUSI VYPNOUT "network-manager"

** /etc/init.d/network-manager stop **


/ WEP Key /
```
- ifconfig wlan0 up

- iwlist scan

- ifconfig wlan0 essid "Wi-Fi network" WEP klíč

- Hotovo!!!
```

/ WPA Key /

- Vytvoření konfiguráku (pokud neexistuje)
```
network = {
ssid = "Wi-Fi Network"
proto = WPA
key_mgmt = WPA-PSK
psk = "heslo"
priority = 5
}
```

- Nastavení přístupových práv pro tento soubor:

- ** chmod go-rwx etc/"konfigurak_wifi.conf" ** nebo ** chmod 600 etc/... **

- Připojení k síťi s WPA, WPA2

** wpa_supplicant -i wlan0 -c /etc/cesta ke konfiguraku -B **

- "c" je nazev souboru, "B" je beh na pozadi "Background"

- Hotovo!!!


POZOR a teď je potřeba pokud je u předešlých kroků 4 krok OK,

- spustit DHCP client - ** dhclient wlan0 **

- ukončení připojení pomocí:
** wpa_cli reconnect, disconnect, terminate **

- kompletní odpojení, musí se znovu fyzicky připojit

** wpa_cli status ** - zobrazí info o připojení


** SSH (Secure SHell) **
------------------------

** ssh root@IP** - připojí uživatele "root" se zadanou IP adresou přes sshčko

** POZOR! Pokud se vyskytne tato hláška: **
```
Unable to negotiate with IP(A.B.C.D) port 22: no matching key exchange method found.
Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1
```

- Je potřeba přidat "matching key exchange method" do /etc/ssh/ssh_config
pod posledni radek toto
```
KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,
ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1
Ciphers 3des-cbc,blowfish-cbc,aes128-cbc,aes128-ctr,aes256-ctr
```
- po ulozeni do "ssh_config" aktualizovat prikazem

** ssh-keygen -A **

- pokud to ješte zobrazí tuto hlášku

```
Unable to negotiate with IP(A.B.C.D) port 22: no matching host key type found. Their offer: ssh-dss
```

- tak přidat třeba na předposlední konec řádku ještě toto:
```
HostkeyAlgorithms +ssh-dss
```

- při dalším přihlášení se zobrazí nejspíš toto, ale je to OK! :)
```
The authenticity of host 'lubuntu (A.B.C.D)' can't be established.
ECDSA key fingerprint is SHA256:hZqV3iuaQt+hEXyP6hoqIyzaPOnhQmb7z+m2I8vyhVg.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'lubuntu,A.B.C.D' (ECDSA) to the list of known hosts.
```
- potvrdit volbou "yes" a všechno je v pořádku a při příštím přihlášení se nic už neobjeví!



** SSH nastavení CERTIFIKÁTŮ (veřejný /public key/ a privátní /private key/ klíče)**

Na lokalní mašině, odkud se chceme připojovat spustíme:

** ssh-keygen ** (nastavime tzv. "passphrase" - nastavit silne heslo!!! )

- Pokud potrebujeme zmenit "passphrase" potom, pouzijme tento prikaz

** ssh-keygen -p **

- vše se uloží do /home/martino/.ssh/id_rsa


** Kopírování přes SSH se vzdálených strojů **

** ssh-copy-id -i ~/.ssh/id_rsa.pub root@lubuntu ** (nebo pouzit cestu /home/martino/.ssh/id_rsa)

- Instalace veřejného klíče na server/vzdálený počítač

- Nyní zkusit funkčnost na serveru

** ssh martino@lubuntu **

- ale pres "passphrase" !!!

* pozn. - přístup přes hesla lze zakazat/zamknout: ** passwd -l martino **

- parametr -l lock, zamknout, čili se pak na vzdalene pocitace lze dostat
pouze pres "passphrase" ;)



** Smbclient **
---------------
smbclient -L //IP -U="user ID"

(Zobrazí veškeré sdílené prostředky)

smbclient \\\\IP\\share (c$, x$ např.)

(připojení na hostitelský počítač/server)

smbclient -U "uživ.jm." \\\\IP\\share (c$, x$ např.)

(připojení na hostitelský počítač/server s použitím uživ.jm. a hesla)


- Po připojení lze použít příkazy pro kopírování (GET) nahrání (PUT) zobrazení (LS)


** SFTP (Secure File Transfer Protocol) **
------------------------------------------

** sftp://martino@martino-zorin-18/martino **

(vzdálené připojení, přenos souborů, opět lze využít přikazy LS, PUT, GET)


** SCP (Secure Copy) **
-----------------------

- Například, chci stáhnout soubor se vzdáleného počítače do lokálního počítače

 ** scp martino@lubuntu:/sambashare/readme.txt	/home/martino/Downloads **

- kopírování souboru pomocí scp<soubor>

 ** scp "soubor" martino@martino-zorin-18:/home/martino **

```
POZOR - funguje pouze mezi počítači, které mají nainstalován openssh-server,
```

jinak se musí použít putty, nebo WinSCP

- nelze přenášet soubory mezi 2 vzdalenými počítači, alespoň 1 musí být lokální

- Autentizace, odstraneni znamych hostu podle IP se provede:

** ssh-keygen -f "/root/.ssh/known_hosts" -R IP **


** RDP (Remote Desktop Protocol) **
-----------------------------------

** rdp:/ IP serveru **

rdesktop IP poče


** Nslookup **
--------------

** nslookup -q=MX atlas.cz **

Zjistí DNS adresu a IP poštovního SMTP serveru atlas.cz

POP3 - příchozí pošta port č. 110

SMTP odchozí pošta port č. 25

IMAP - pro BlackBerry např.


** FIREWALL v LINUXU **
-----------------------

- nachází se v /sbin/iptables

** iptables -L ** - výpis pravidel

** iptables -L -v -n --line **

- vypíše podrobné porty IPTables

** iptables -A INPUT -p tcp -s 192.168.0.0/16 --dport 22 -j ACCEPT **

- přidej pravidlo, že na portu č.22 tcp pro dané IP adresy přijímej pakety!!!

** Grafické firewally v linuxu - Vyatta nebo Untangle **


** NAT - LINUX jako ROUTER ;) **
--------------------------------
```
* na poč. A a B nastavit IP ve stejné podsíťi (např. 192.168.1.1-1.2)

* na poč. A: iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE

* na poč. A: echo 1 > /proc/sys/net/ipv4/ip-forward

* na poč. B: route add default gw "IP adresa poč. A + maska"

* nastavit v /etc/resolv.conf zapsat nameserver což je DNS, adresu Wi-fi routeru, např.192.168.9.1
a tam ji přidat

* Ověření jestli běží INTERNET a HOTOVO! ;)))

- Zrušení výše uvedeného nastavení a navrácení do původního stavu

** iptables -t nat -F **

** echo 0 > /proc/sys/net/ipv4/ip-forward **

- jinak v /etc/hosts je soubor, kde jsou uloženy IP hostname
```


** Netstat & ss - command **
-----------------------------
** netstat -tulpn | grep :22 ** (SSH)

- vypíše podobný výpis vše na portu 22, nejlepší funkce!

** ss -tulpn | grep vnc **

- to samé použitím "ss" zjistí zda běží "vnc" služba

** netstat -na | grep :22 **

- Vypsání všech portů č. 22 na kterých počítač naslouchá

nebo

** netstat -ln | grep :22 **

** netstat -lntp **

- vypíše naslouchající v IP adrese procesy s ID cislem, jmenem a cestou k procesu/programu

** netstat -ntp | grep :22 **

- vypíše IP všech naslouchajícíh zařízení na portu č.22


** NETCAT (TCP Swiss-Army-Knife :) **
-------------------------------------

** Přesun souboru z jednoho počítače na druhý **

* Oba počítače se musí "vidět" /nastavit sit aby se "pingly"/

* Cílový počítač
  ** nc -l 80 **

* Zdrojový počítač odešle zprávu ** echo ahoj | nc IP 80 **

** Přesun souborů **

- Zdroj:
** cat "soubor" | nc -q0 IP 80 **

- Cíl:
** nc -l 80 **

** Psaní na vzdálenem PC - velice COoL parádička! **

- Zdroj:
** nc -l 1234 (lib.port) **

- Cíl:
** nc IP 1234 **


** pv ** - monitoruje progres přenosu dat skrz pajpu (chce to nainstalovat)

- Zde použití

- Zdroj: ** nc -l 1234(lib.port) > "soubor" **

- Cíl: ** cat "soubor" | nc IP 1234 | pv -b **



** Email In Linux **
--------------------

- To add content to the body of the mail while running the command you can use the following options. If you want to add text on your own:

echo “This will go into the body of the mail.” | mail -s “Hello world” you@youremailid.com

And if you want mail to read the content from a file

mail -s “Hello world” you@youremailid.com < /home/calvin/application.log

Some other useful options in the mail command are


-s subject (The subject of the mail)
-c email-address (Mark a copy to this “email-address”, or CC)

-b email-address (Mark a blind carbon copy to this “email-address”, or BCC)


Here’s how you might use these options

echo “Welcome to the world of Calvin n Hobbes” | mail -s “Hello world” calvin@cnh.com -c hobbes@cnh.com -b susie.derkins@cnh.com


Read more at http://www.simplehelp.net/2008/12/01/how-to-send-email-from-the-linux-command-line/#cuTlJAXBdBKOIhiw.99


** OSTATNí LINUXOVÉ DISTRIBUCE (ZÁKLAD BALÍČKOVACÍHO SYSTÉMU) **
----------------------------------------------------------------
** Debian **

** apt-get update, install, remove (dpkg -i, -r, -l) **

- Pridani "add-apt-repository" do Debianu "Jessie" a dalsi/ => ** apt-get install software-properties-common **


** RedHat **

** yum update, install, remove (rpm -i, rpm -qa | grep "nazev_balicku" ** - najde a vypise

- u RedHat ještě jedna "specialia" například instalace balíčku "gparted"

se dá provést i takto (preferovaný způsob)

* dnf download gparted
* sudo rpm -i gparted-downloaded-package-name.rpm --nodeps
* sudo gparted

- DŮLEŽITÉ!!! Nastavení pro "mirror list" pro Centos8 (RedHat)

** http://mirror.centos.org/centos/8/BaseOS/x86_64/os/ **


** REPO - odstranění probémů u CENTOS 8 (RedHat) **
```
root@centos8:/home/centosuser:-] yum update
CentOS Linux 8 - AppStream                                                         0.0  B/s |   0  B     00:00
Errors during downloading metadata for repository 'appstream'
- Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStre                                                                                 am&infra=stock [Could not resolve host: mirrorlist.centos.org]
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: Curl error (6): Couldn                                                                                 't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock [Could not                                                                                  resolve host: mirrorlist.centos.org]
```

** Uzitecne Prikazy Na Zjisteni Informaci Repo!!! **

** yum repolist **

** find / -name 'mirror*' **

** cat /etc/*-release **

** grep -rH enabled=1 /etc/yum.repos.d/* **

** find /var -name mirrorlist -exec cat {} \; **


** Solution!!! **

/under ROOT/

 1) root@centos8: sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS*

 2) root@centos8: sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS*

 3) root@centos8:/etc/yum.repos.d:-] yum clean all
```
Warning: failed loading '/etc/yum.repos.d/CentOS-Linux-Sources.repo', skipping.
21 files removed

root@centos8:/etc/yum.repos.d:-] yum update
Warning: failed loading '/etc/yum.repos.d/CentOS-Linux-Sources.repo', skipping.
CentOS Linux 8 - AppStream                                                         2.6 MB/s | 8.4 MB     00:03
CentOS Linux 8 - BaseOS                                                                                                                                             2.3 MB/s | 4.6 MB     00:02
CentOS Linux 8 - Extras                                                                                                                                              17 kB/s |  10 kB     00:00
Dependencies resolved.
```

** OpenSUSE ** - zypper update, install, remove (yast - "graficke" DOS prostredi)

** Gentoo ** - "emerge --sys" (update), "emerge --ask _nazev_co_chceme_instalovat_(zepta se Yes/No)"

** Debian ** vypis vsech nainstalovanych baliku obsahujici nazev "java"

** dpkg --list | grep java **

** dpkg --list ** - vypíše všechny nainstalované balíčky


** FreeBSD (čistý free UNIX :) **
- Při instalaci FreeBSC se nastaví IP adresa, DNS a vzdálený ssh přístup!

- Vytvoření nového uživatele "adduser" a potom se systém zeptá na další detaily

- SSH přístup pro FreeBSD - pokud mi nelze se vzdalene prihlasit jako root (defaulne to neni povoleno) tak to lze

provést tak, že v editoru vi upravit takto: vi /etc/group (upravit řádek "wheel:*:0"root,"nazev_uzivatele")

a to samé platí pro vzdálené přihlášení pokud nefunguje přepnutí příkazem "su"

- pw => správa účtů, např pw add group adminuser - vytvoří v souboru skupinu adminuser


** Instalace balíků **

** pkg_add -r "nazev_programu" ** (nainstaluje program)

** pkg_deinstall "nazev_programu" ** (odinstalace programu)

** pkg_info ** (informace o balíčcích)


- Instalace programů se provádí tzv. z "portů"

čili kompilace z portů cd /usr/ports

make search name="jmeno_programu"

make install (vlastni instalace hledaného programu)

make clean (vycisteni prac. plochy aktualniho programu a jeho závislostí)


napr. portinstall mc - instalace midnight commanderu


portupgrade - nastaveni, cd /usr/pors/ports-mgmt/portupgrade

make install clean



** GRAFICKÉ NADSTAVBY pro FreeBSD **

** Kports **

** DesktopBSD **



** JAVA Instalace a Adobe Flash Playeru (AUTOMATICKA) **
--------------------------------------------------------
```
apt-get install openjdk-7-jre (JDK - Java Development Kit)

dpkg --list | grep jdk (vypis nainstalovanych balicku "jdk")

update-java-alternatives -L (vypise alternativy Javy)

java -version
```


** MANUALNI INSTALACE ORACLE Java (100% funkcni) **

1. stahnout nejnovější verzi z webu www.oracle.com -> downloads -> Java for Developers -> Java SE (Standard Edition)

- stahnout Java Platform a JDK Docs - stažení vhodných balíků z webu
(v mém případě Ubuntu 64-bit, tedy "Linux x64.tar")

2. po stažení rozbalit: tar -xvf *.tar soubor do adresáře "jvm"  /usr/lib/jvm/ na mem poci to vypadalo takto
```
lrwxrwxrwx   1 root root    20 lis  4 20:44 java-1.8.0-openjdk-amd64 -> java-8-openjdk-amd64
-rw-r--r--   1 root root  2600 dub 13  2016 .java-1.8.0-openjdk-amd64.jinfo
drwxr-xr-x   5 root root  4096 čen 28 14:10 java-8-openjdk-amd64
```

(TARGET - CILOVY ADRESAR s JAVA) (LINK_NAME - NAZEV LINKU)
3. vytovorit "link"(odkaz): ln -s java-8-openjdk-amd64/ java-1.8.0-openjdk-amd64

(nalinkuje, resp.vytvoří symbolický odkaz na tuto Javu, vytvoří tzv. softlink)

potom

4. update-alternatives --config java (aktualizace pro system ze mame novou JAVA)

5. Hotovo, Jede To, Svisti To! :D
```


** Záložky FIREFOX v Linuxu **
------------------------------
- Kde najdu oblíbené(favorites) ve Firefoxech?

- Windows7 -> Users/Uzivatel/Data Aplikaci/Mozilla/Firefox/Profiles/0ovf8kht/bookmarks



** BASH Scripting! **
---------------------
Obcas se stane, ze skript vytvoreny ve windows nelze spustit kvuli "formatovacim" znakum...

ŘEŠENÍ: ** cat -A script.sh ** (zobrazi skryte formatovaci znaky)
```
pozn.: x0D je hexadecimalni reprezentace znaku Carriage Return (navrat voziku),
ktery je ridicim znakem ASCII s desitkouvou hodnotou 13.
Tento znak se pouziva k oznaceni konce radku a v mnoha OS
se chape jako ekvivalent stisknuti klavesy "Enter"
Ridici kod ^M a oznacuje se jako konec radku, nekdy evivalent
klavesy Enter.
```

I. Parametr -A , který je aliasem pro parametry -vET nám zobrazí „neviditelné“ znaky.
Mimo svých ^M tu ještě vidím znak ^I, který zastupuje tabulátor, a také $, který indikuje konec řádku.
Už tedy vidím, co nevidím a můžu se pustit do odstraňování. Mám ověřené dvě metody. První z nich používá sed,
je jednodušší (obzvlášť pokud potřebujete opravit větší množství souborů), ale nemusí být vždy a všude účinná.

** sed -i 's/\x0D$//' script.sh **

II. 0x0D je ASCII hodnota znaku CR. Sed jednoduše prošmejdí soubor a všechny CR na koncích řádků vymaže.
Druhá metoda je nepatrně složitější, ale zato mě zatím nezklamala. Soubor otevřete ve vi či nějakém podobném
vi-like editoru a přikažte mu

** :e ++ff=dos **

** :setlocal ff=unix **

** :wq **

Pokud váš soubor doprasil mac, na prvím řádku nahraďte dos macem.
Samozřejmě lze touto metodou konvertovat i nazpátek.


** Programovani & Kompilace zdrojáků! **
----------------------------------------

- Jak Prelozit Java Zdrojak

** javac "nazev_souboru.java"	**					

- Spusteni *.jar souboru

** java -jar "nazev_jar_souboru.jar" **

```
kompilace pomoci gcc, g++ v C nebo C++ (soubory *.c *.cpp *.o apod.)
po stahnuti "zdrojaku" rozbalit a bud zkusit "make" nebo podivat se jestli neni
nekde nejdrive ".configure" nebo jiny navod. Pokud nic takoveho neni, potom
provest (u jednoho souboru)
```

** gcc -c "nazev_souboru.c" (nejdrive zkompiluje) **

potom

** gcc -o "lib_nazev" "nazev_souboru.o" ** (vytvori spustitelny binarni tvar)

a nebo rovnou zkompilovat a prevest do spustitelneho tvaru

** gcc "nazev_souboru.c" -o "lib_nazev" **

- vytvoreni spustitelneho souboru z vice zdrojovych souboru

** gcc *.c -o "lib_nazev" **

(spise pouzit g++ kvuli knihovnam, zalezi na typu zdrojaku atd.)

** g++ *.c (*.cpp) -o "lib_nazev" **

- priklad pokrocilejsi kompilace s pripojenim knihoven viz "graficky balicek" nebo grafika v Linuxu...

** g++ KruhovyFraktal.cpp -w -o fraktal -lgrap **

- dal jsem parametr -w , fakt me ta "ukecanost" stvala :)

** spuštění skriptu, spustitelný soubor **
- Pokud jsme v "ceste"(adresari) spustitelneho souboru, ktery chceme spustit, tak jednoduse takto:

** ./nazev_skriptu/"spust.soubor" **

- s teckou pred lomitkem a tabulatorem doplnim nazev souboru a Enter ;)

- nebo zadat "cestu" s nazvem spust.souboru, pokud jsem mimo "cestu" k souboru

** /home/martino/Dokumenty/PROGRAMOVANI/binarne **
(bez tecky ;)


** Linux System - Runlevels, BootSystem! **
-------------------------------------------
- Vytvoříme script například ** nas.sh **  s obsahem
```
#!/bin/sh

smbmount -o username=jmeno,password=_heslo_ //192.168.1.100/data/ /home/obyvak/NAS_Server

* Script nas.sh je třeba nahrát do /etc/init.d/

a umožnit jeho spouštění
* sudo chmod +x nas.sh

Následně stačí jen použít příkaz který provede vše potřebné za nás.
* update-rc.d nas.sh defaults

Do rulevelu 2,3,4 a 5 umístí příkaz start a do 0 a 6 stop.
Po restartu bude script spuštěn
tento můj script mountuje síťový disk jako složku v adresáři	/home/obyvak
```

** odstraneni skriptu pri startu systemu! **

** update-rc.d "nazev_skriptu.sh" remove **


** GRUB zmena startu systemu = MANUALNI **
------------------------------------------

fgrep menuentry /boot/grub/grub.cfg

- Zobrazí informace o "bootu"

- Označit např. "Windows 7 (loader) (on /dev/sda2)"

vim /etc/default/grub

- Změna, počítá se od "nuly" takže když je poslední položka
třeba Windows a je pátá od shora tak je de facto čtvrtá!!!

 Grub_Default=0

na zkopírovaný, označený systém

GRUB_DEFAULT="Windows 7 (loader) (on /dev/sda2)"

- popřípadně přidat komentář, poté uložit

sudo update-grub

zobrazeni vsech HLÁŠEK pri start systemu,bootu bash
journalctl -b


start systemu do textoveho prostredi! (se všemi službami pochopitelně)
* disable the X server => vim /etc/default/grub, finding the line

* GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

zmenit nebo pridat a zakomentovat predchozi

* GRUB_CMDLINE_LINUX_DEFAULT="text"

* update-grub
* update-grub2 (radeji take)

** start do textoveho rezimu pro unixove system napr. FreeBSD! **
* vypsat cat /etc/inittab

* vim v řádku id:3:initdefault: a uložit

start z prikazove radky do grafickeho prostredi!

** startx **

** Start do Grafickeho prostredi pro UNIX **

** xinit & ** (musi byt za xinit mezera!)

pro Gnome

** gnome& **

pro KDE

** kde& **

Spusteni grafickeho "Exploreru" pres prikazovy radek

** xdg-open . **


** Service - command & Systemctl **
-----------------------------------

* Sluzby v debianu

* List services
ls /etc/init.d/

 * Start service
/etc/init.d/{SERVICENAME} start

 * Stop service
/etc/init.d/{SERVICENAME} stop

 * Enable service
cd /etc/rc3.d
ln -s ../init.d/{SERVICENAME} S95{SERVICENAME}
(the S95 is used to specify order. S01 will start before S02, etc)

 * Disable service
rm /etc/rc3.d/*{SERVICENAME}

V OSTATNICH DISTRO lze pouzit prikaz "service --status-all"
service stop|start atd.

** Zjisteni, jake mam v Linuxu GUI (graficke prostredi - KDE, Gnome, LXDE ...) **

** echo $XDG_CURRENT_DESKTOP ** nebo ** echo $GDMSESSION **


** Datum a Čas v Linuxu **
--------------------------

- prikaz "date"
- nastaveni datumu a casu (jak je někdy duležitý :D !)

** date -s "11/4/2016 22:57:03" **


** VIM - VIMproved editor **
----------------------------

SUPER NASTAVENI BAREV V EDITORU VIM :o)

** :highlight Normal ctermfg=grey ctermbg=darkblue **

- nebo další cool nastavení

** :highlight Normal ctermfg=grey ctermbg=black **

**:w** uloží

**:q** ukončí

**ZZ** okamžitě vyskočí z editoru

**i** - klávesa aktivuje editaci

**a** - aktivuje editaci vedle znaku

- pro více info "man vim" :)


** Kopírování Celého Textu Ve Vim! **

** Ctrl-v ** - přepnutí do visuálního výběru

- kurzorem vybrat část textu a buď:

** y ("yank") ** zkopíruje výběr

** c ("cut") ** vyjme část text

** d ("delete")** vybranou část smaže

* Esc - zrušení Visual Modu

** p ("paste") ** vloží výber kde se nachází kurzor (už ale ne ve visual modu!)


** Remote Desktop(Gui) Vnc **
-----------------------------

** Install X11vnc, LXDE, VPN programs **

** apt-get install x11vnc ** - zatím nejlepší řešení a fungovalo nejlíp!

- nebo

** apt-get install xorg lxde-core tightvncserver **


Start VNC to create config file

** tightvncserver :1 **

Then stop VNC

** tightvncserver -kill :1 **


Edit config file to start session with LXDE

** nano ~/.vnc/xstartup **


Add this at the bottom of the file

```
lxterminal &
/usr/bin/lxsession -s LXDE &
```
Restart VNC

- případně vypnutí encryption
 ** gsettings set org.gnome.Vino require-encryption false **

** tightvncserver :1 **


- Pokud je černá obrazovka tak zkusit instalovat grafické UI Xfce

** yum install epel-release **
** yum groupinstall xfce **

přidat do

- /home/<user>/.vnc/xstartup and change the exec entry (usually line 4)
- from etc/X11/xinit/xinitrc to startxfce4, as shown below

```
#!/bin/sh 
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec startxfce4
vncserver -kill $DISPLAY
```

- restart VNC, případně celej komp ;)


** NASTAVENÍ FIREWALLu pro VNC **
---------------------------------
firewall-cmd --list-all (vypsání celé konfigurace)

sudo firewall-cmd --add-service vnc-server
sudo firewall-cmd --remove-service vnc-server

sudo firewall-cmd --zone=public --add-port=7777/tcp
sudo firewall-cmd --zone=public --remove-port=7777/tcp

sudo firewall-cmd --list-all-zones

sudo firewall-cmd --reload

firewall-cmd --add-port=5901/tcp
firewall-cmd --add-port=5901/tcp --permanent

- Odstranění (Permanentní) Portů
firewall-cmd --remove-port=5901/tcp
firewall-cmd --runtime-to-permanent


** Security Linux!!! **
-----------------------

** SELinux has 3 modes **

- Enforcing mode
This is the default mode. It blocks and logs actions that are against defined 		policy.

- Permissive mode
Allows actions to take place and logs the events in detail. This mode is useful 	when testing SELinux features. Changing modes between enforcing and permissive 		does not require a system reboot.

- Disabled mode
Allows for all actions and does not log any activity. Changing to this mode 	requires a system reboot for it to apply. Learn more on disabling SELinux.

- Dá se použít příkaz
** setenforce ( usage: setenforce [ Enforcing | Permissive | 1 | 0 ] ) **
ale raději použít TOTO!

** sestatus ** (vypíše status - mělo by být "enabled")
pokud ne, tak

vim /etc/selinux/config
- změnit řádek SELINUX=enforcing (default mode, viz výše)
- řádek by měl být SELINUXTYPE=targeted (ten neměnit!)

reboot


** NASTAVENÍ SELinux a Firewall pro Sambu **

SELinux
* setsebool -P samba_export_all_ro=1 samba_export_all_rw=1
* semanage fcontext -a -t samba_share_t "/sambashare(/.*)?"
* restorecon /sambashare/

Firewall

* firewall-cmd --add-service=samba --zone=public --permanent

* firewall-cmd --reload

* výpis všech povolených služeb ve firewallu
- firewall-cmd --list-all

** Client List Sharu **
zkusit třeba: net share
nebo
smbclient -L localhost
smbclient -L //raspberrypi

* Poznámka:

* otevření portů ve Firewallu, aby šlo namapovat vzdálené share
* umožnění smbd službě "file sharing" a "printing services", které poslouchají
* na portech TCP 139 a 445
* nmbd služba poskytuje NetBIOS over IP naming služby klientů a poslouchá na UDP portu 137


** Raspberry Pi 3B **
---------------------
* všechny předchozí kroky jsou shodné, až kromě nastavení firewallu
ten se nastavuje

- ufw status
- ufw allow 139/tcp
- ufw allow 445/tcp

* odepření služeb

- ufw deny 139/tcp
- ufw deny 445/tcp

* restart služby
```
/etc/init.d/samba restart

[ ok ] Restarting nmbd (via systemctl): nmbd.service.

[ ok ] Restarting smbd (via systemctl): smbd.service.

[ ok ] Restarting samba-ad-dc (via systemctl): samba-ad-dc.service.
```

** Ufw Firewall Přidání/Smazání Pravidla **
-------------------------------------------

ufw - základní firewall
(delete allow/deny/reject)

- ufw allow 1194/udp

- ufw delete allow 1194/udp

Rule deleted
Rule deleted (v6)


** Linux Perfomance/Výkon Linux systému **
------------------------------------------

Zjištění výkonu systému v Linuxu

příkaz ** "top" **

** lscpu **

** cat /proc/meminfo **

** cat /proc/cpuinfo **

** mpstat (musí se instalovat sysstat) **


** Restart, Konfigurace služeb (Daemon) **
------------------------------------------

* Přehled všech aktivních služeb (popřípadně se nacházejí v /etc/init.d/apache2 restart)

- ** service --status-all ** nebo ** systemctl -a **

* Doporučené použití pro start/stop/restart konkrétní služby

- ** /etc/init.d/apache2 restart **

```
root@raspberrypi:/home/pi# /etc/init.d/apache2 restart
[ ok ] Restarting apache2 (via systemctl): apache2.service.
```

*Použití "Systemctl" Pro Konfiguraci Služeb*
* vypíše všechny služby, které jsou "enable"


- ** systemctl list-unit-files | grep enabled **

* vypíše všechny služby, které jsou "running"


- ** systemctl | grep running **

* restartuje službu apache2 (apache2.service)


- ** systemctl restart apache2 **


* Podrobný Výpis Služby (Status)*
- ** /etc/init.d/apache2 status **
```
● apache2.service - LSB: Apache2 web server
Loaded: loaded (/etc/init.d/apache2)
```

** KWallet - DEAKTIVACE TÝHLE VOTRAVNÝ SLUŽBY!!! **
---------------------------------------------------

* editace souboru ~/.kde/share/config/kwalletrc : přidání do [Wallet] sekce pouze jeden řádek:
```
Enabled=false
```
Toto znemožní zobrazování žádostí "kwallet popups"

* pokud config je v této cestě, potom je postup stený => ** ~/.config/kwalletrc **

Hotovo !!!


** | Linux Hardware | **
------------------------

** dmesq ** - zobrazí výpis jádra

** dmesq | tail ** - vypíše posledních 10 řádek jádra s hlášky

** dmesq | grep eth ** - vypíše všeee co hlásí s tímto zařízením

** uname -a ** - vypíše všechny informace o systému včetně 32/64bit verze

Jak zjistit verzi Debianu?

** lsb_release -a **

- Nastroj na disky,zobrazeni disku,deleni atd.

** fdisk -l ** (vypíše vsechna zařízení)

** lspci ** - info o sběrnici PCI

** lsusb ** - info o USB zařízeních

** cat /proc/version ** - zjištění verze jádra (jestli je Debian atd.)

** eject ** - vysune CD z mechaniky

** poweroff ** - vypne počítač

** časované vypnutí - shutdown -P -t secs: 10 **

- Vypnutí systému bez použití příkazu "poweroff" a to příkazem shutdown -P (velké p!)

a mezera cislo (v celých to jsou minuty)

** mount | grep ˆ'/dev' ** - vypíše všechna připojená zařízení

** ls /dev | grep sr ** - vypíše všechna CD/DVD i virtuální

** dd if = /dev/dvd of=dvd.iso ** jestli je DVD vytvoří bitovou kopii
