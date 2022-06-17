# Labo Besturingssystemen



> **Handige links:**
>
> Bash cheatsheet :  https://devhints.io/bash
>
> regex: https://regexr.com/



> **Planning/Verloop Labo's:**
>
> - Labo 1: **Deel 1**: De terminal, Man pages, **Deel 2**: Compileren in de shell
> - Labo 2: **Deel 7**: Patterns, expansions
> - Labo 3: **Deel 7**: Redirection & pipes
> - Labo 4: **Deel 7**: Uitleg Regex + vraag 42-54
> - Labo 5: **Deel 7**: Shellvariabelen, Shellscripting & Arithmetic expansion
> - Labo 6: **Deel 7**: Argumenten van een script/functie, positionele parameters en speciale parameters, Parameter expansion & Arrays
> - Labo 7: **Deel 7**: Structuren: if & While
> - Labo 8: **Deel 7**: De for-lus: 100, 101, 103, 104
> - Labo 9: **Deel 5**: Uitleg nmap + oef 5 **cat**, oef 6 **cp** & oef 7 **watchfile.**
> - Labo 10: **Deel 6:** Processen en POSIX-threads
> - Labo 11: **Deel 6**: Shared memory & threads (oef **6b** & **6c**)
> - Booster 1: Examenvraag vorig jaar : Commando **tee** , vraag **111** & vraag **112**
> - Booster 2: **Zelftest2**
> - Booster 3: Commando **wc -l** met pipes als IPC + Omzettingen binair naar hex/oct

## Deel I: Inleiding

Lokaal inloggen op een Linux toestel kan op twee manieren gebeuren. Je kan inloggen op de
**grafische console** of je kan inloggen op een van de vijf a zes **tekstuele consoles**. Veranderen
van console kan via de toetsencombinaties CTRL-ALT-F1, CTRL-ALT-F2, ... , CTRL-ALT-F7.
Wanneer je Linux draait m.b.v. VirtualBox, dan moet je mogelijks gebruikmaken van de
toetsencombinaties HOSTKEY-F1, HOSTKEY-F2, ..., HOSTKEY-F7 waarbij de HOSTKEY
standaard is ingesteld op de rechter CTRL-toets. Na het opstarten van Linux wordt aan
iedere console een tty (terminal type) gekoppeld of in het geval van een grafische console
een login manager zoals bv. gdm (GNOME Display Manager).
Bij Fedora Linux en aanverwante distributies zal de eerste console ingenomen worden door
de grafische console. De overige tekstuele consoles vind je door te switchen met CTRL-ALT-
Fx. Voor Debian, Ubuntu, ... zal je merken dat de grafische console terug te vinden is op de
zevende terminal. Inloggen op meerdere terminals is mogelijk. Wanneer je correct inlogt op een tekstuele
console kom je terecht in een BASH-shell. Bij het inloggen op de grafische console wordt
naar alle waarschijnlijkheid een desktopomgeving zoals bv. GNOME, KDE, XFCE, ... gestart. In
die desktopomgeving kan je dan allerhande GUI-gebaseerde programma’s starten naar
analogie met MS Windows. Voor deze labo’s is het gebruik van een BASH-shell noodzakelijk. Op een tekstuele console
beschik je onmiddellijk na het inloggen over een BASH-shell en op een grafische console zal je een terminal-emulator moeten starten.



#### 1. De terminal

Log in als gebruiker root met als wachtwoord **e=mc**2** en start wanneer van toepassing in
GNOME de terminal-emulator. Tik in het venster de opdracht “stty -a” in.



1. > Welke toetsencombinatie heb je nodig om een runnend programma (een proces
   > dus) te onderbreken?

```bash 
ctrl+C
```

2. > Hoe kan je een runnend programma pauzeren? (Het hervatten van een
   > programma zullen we later zien)

```bash 
ctrl+Z
```

3. > Wanneer een programma vraagt om gegevens in te typen, met welke
   > toetsencombinatie kan je dan aangeven dat de invoer stopt.
   >
   > Je kan vraag 1 en vraag 3 het best uitproberen m.b.v. het commando “**cat**”. Deze
   > opdracht kopieert alle invoer van het toetsenbord (**standaard invoer**) naar het
   > scherm (**standaard uitvoer)**.
   > Probeer dit nu ook uit met de opdracht “**mail root@localhost**”. Hier zal eerst
   > gevraagd worden om het **onderwerp** van het bericht in te geven, gevolgd door
   > het **bericht** zelf. Wanneer je het **einde** van de **invoer** aangeeft, zal een mail
   > verstuurd worden naar de gebruiker root op het lokale toestel. De gebruiker root
   > kan zijn mail lezen door de opdracht **mail** uit te voeren zonder parameters.
   > Hierdoor kom je terecht in een interactieve omgeving waar je een overzicht krijgt
   > van alle berichten. Bij het intikken van een nummer dat naast een bericht staat,
   > kan je de mail lezen. Het bericht **verwijderen** kan door het ingeven van de letter **d**
   > gevolgd door het **berichtnummer**. De interactieve omgeving verlaten kan door
   > het ingeven van de letter **q**.

```bash 
ctrl+D
```

4. > Wanneer je op de commandolijn een aantal woorden intikt, hoe kan je dan het
   > laatste woord verwijderen?

```bash 
ctrl+W
```

5. > In een shell kan je aan “**auto completion**” doen door gebruik te maken van de
   > **tab-toets**. Tik de letters “les” in, en tik vervolgens op de tab-toets. Je merkt dat er
   > automatisch less verschijnt. Nu kan het zijn dat er nog opdrachten zijn die met
   > less beginnen. Tik nogmaals op de tab-toets om te kijken welke opdrachten er
   > met less beginnen. Een ander handigheidje is “**reverse search**” om **eerder**
   > **ingetypte commando’s te suggereren** tijdens het typen. Gebruik hiervoor
   > “**CTRL+r**”.

...

6. >Linux telt enkele duizenden opdrachten met elk nog een variabel aantal opties. De opdracht zelf wordt doorgaans beperkt tot enkele letters die de afkorting vormen van een woord dat de functie van de opdracht deels omschrijft. Zo staat het commando “**ls**” voor “list”, “**mkdir**” voor “make directory”, het commando “**wc**” voor “word count”, het commando “**cc**” voor “C-compiler”, het commando “**dd**“ voor “convert and copy”. Bij het laatste voorbeeld is er een conflict omdat de afkorting cc reeds gebruikt wordt voor de C-compiler. Als **oplossing** heeft men de **volgende letter van het alfabet** gebruikt.
   >
   > “Auto completion” voor commando’s werd reeds in het vorige punt naar voor gebracht maar geldt ook voor de bijhorende opties. Geef op de commandolijn het commando “**ls** -“ in en gebruik vervolgens de tab-toets. Je merkt dat er een pak opties verschijnen die voorafgegaan worden door twee mintekens. Onder Linux kan je veelal opties op de commandolijn meegeven in **twee formaten**. Het **korte** formaat bestaat uit **één letter** en wordt voorafgegaan door **één minteken**. Dezelfde optie kan je ook meegeven d.m.v. het lange formaat. In dat geval zal de optie voorafgegaan worden door **twee opeenvolgende mintekens**. Wanneer je de keuze hebt tussen de twee formaten zal je merken dat de korte variant de voorkeur geniet. 
   >
   >Zo kan het commando “**wc --words --lines /etc/passwd**” ook geschreven worden als “**wc -w -l /etc/passwd**” en zelfs als “**wc -wl /etc/passwd**”. De opdracht toont het aantal lijnen en het aantal woorden uit het bestand /etc/passwd.

...

#### 2. Gebruik van enkele eenvoudige opdrachten

1. >  Met de opdracht man kan je alle info over een welbepaalde opdracht
   > achterhalen. Zo zal de opdracht “**man ls**” de info tonen van de ls-opdracht.
   > Man toont de informatie a.d.h.v. een pager, een programma dat de informatie
   > niet alleen op het scherm toont maar dat ook gebruikersinteractie toelaat. Zo kan
   > je scrollen, zoeken naar bepaalde woorden, etc. Standaard is de **pager** ingesteld
   > op het commando **less**. Dit betekent dat wanneer je wil weten hoe je voorwaarts
   > moet zoeken in een manpagina, je dit moet gaan zoeken bij het commando **less**
   > en **niet** bij het commando **man**. Vraag de manpagina op van het commando **less**
   > en ga na hoe je een tekst die met less wordt getoond kan afsluiten. Hoe kan je
   > voorwaarts zoeken in een manpagina?

Je kan zoeken naar een bepaalde term door deze als volgt mee te geven: /term. 

```bash	
man ls 
/term #voorwaarts zoeken
?term #achterwaarts zoeken
```

Dit commando zal naar "term" zoeken in de man page van **ls**. (`n` om naar het volgende en `shift + n`om naar het vorige resultaat te gaan.)

2. > Hoe kan je zorgen dat er bij het zoeken in een manpagina **geen** rekening wordt
   > gehouden met het verschil tussen hoofd- en kleine letters?

```bash
-I or --IGNORE-CASE
          Like -i, but searches ignore case even if the  pattern  contains
          uppercase letters.
```

3. >Bekijk de manpagina van het commando man en ga na hoeveel secties er gekend
   >zijn.

```bash	
 	1. Name
 	2. Synopsis
 	3. Description
 	4. Examples
 	5. Overview
 	6. Defaults
 	7. Options
 	8. Exit Status
 	9. Environment
 	10. Files
 	11. See also
 	12. History
 	13. Bugs
```

4. >Wanneer je de opdracht “man read” intikt krijg je de info te zien van het
   >commando read. Er is echter ook een **systeemaanroep** read aanwezig. Hoe kan je
   >aan man meegeven dat je niet de info wenst te zien van het commando read
   >maar wel van de systeemaanroep read?		

```bash	
man 2 read #2 duidt op System Calls

# (1)     User Commands
# (2)     System Calls
# (3)     Library functions
# (4)     Devices
# (5)     File formats
# (6)     Games and Amusements
# (7)     Conventions and Miscellany
# (8)     System Administration and Priveledged Commands
# (L)     Local. Some programs install their man pages into this section instead 
# (N)     TCL commands
```

5. >Met de opdracht “ls” krijg je van een directory een overzicht van alle bestanden
   >en subdirectories te zien. Wanneer je geen directory opgeeft, wordt de huidige
   >werkdirectory genomen. Wat doen de opties -l en -h?

   ```bash 
   ls -l #extra info zoals rechten en aanmaakdatum
   ls -h #-h gaat in combinatie met -l de grootte van het bestand weergeven in kilobytes, megabytes, gigabytes...
   ```

6. > Bekijk met “ls /” de inhoud van de hoofddirectory.

   ```bash
   root@localhost ~]# ls /
   bin   dev  home  lib64       media  opt   root  sbin  sys  usr
   boot  etc  lib   lost+found  mnt    proc  run   srv   tmp  var
   ```

7. >In punt 5 en 6 heb je gemerkt dat de uitvoer voorzien wordt van kleuren. Zo
   >worden bv. **directories** in het **donkerblauw** gekleurd en **symbolische links** in het
   >**lichtblauw**. Dit gedrag is te wijten aan het feit dat er voor ls een **alias gedefinieerd**
   >is die telkens ls vervangt door “ls --color=auto”. Ga met de opdracht “alias” na
   >welke andere aliassen er bestaan.

   ```bash
   [root@localhost ~]# alias
   alias cp='cp -i'
   alias egrep='egrep --color=auto'
   alias fgrep='fgrep --color=auto'
   alias grep='grep --color=auto'
   alias l.='ls -d .* --color=auto'
   alias ll='ls -l --color=auto'
   alias ls='ls --color=auto'
   alias mv='mv -i'
   alias rm='rm -i'
   alias which='(alias; declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
   alias xzegrep='xzegrep --color=auto'
   alias xzfgrep='xzfgrep --color=auto'
   alias xzgrep='xzgrep --color=auto'
   alias zegrep='zegrep --color=auto'
   alias zfgrep='zfgrep --color=auto'
   alias zgrep='zgrep --color=auto'
   ```

8. >Met de opdracht “cd” kan je van werkdirectory veranderen. Wanneer je geen
   >directorynaam opgeeft wordt je home-directory de nieuwe werkdirectory. Voer
   >“cd /tmp” uit en keer daarna terug naar je home-directory.

   ```bash
   [root@localhost tmp]# cd
   [root@localhost ~]#
   ```

9. >Een directory aanmaken kan via de opdracht “**mkdir**”. Maak in je home-directory
   >een directory aan met als naam ‘c’ waar je toekomstige C-programma’s naartoe
   >kan kopiëren.

   ```bash
   [root@localhost ~]# mkdir c
   ```
   
10. >Een bestand kopiëren gebeurt via de opdracht “cp”. De eerste parameter is de
    >**bron**, de tweede de **bestemming**. Een bestand verplaatsen doe je via de opdracht
    >“**mv**”.

    ```bash
    [root@localhost ~]# cp ./tmp.txt ./c
    [root@localhost ~]# mv ./tmp.txt ./c
    ```
    
    

## Deel II:  Compileren in de Shell (werd tussendoor in de labo's/theorie uitgelegd)

In Linux is het vrij eenvoudig om een C of C++ programma te compileren zonder gebruik te
maken van een IDE. Het enige wat je nodig hebt is een eenvoudige tekstverwerker. In een
grafische omgeving kun je bvb. Visual Studio Code, Atom, Neovim gebruiken. In tekstuele
consoles is nano eenvoudig te gebruiken, terwijl vi en vim ... al wat geavanceerder zijn.
Open in BASH een tekstverwerker (nano, vi, vim, neovim, ...) naar keuze en tik daarin
onderstaand codefragment:

```C
#include <stdio.h>
int main(){
	printf("Hello world!");
	return 0;
}
```

Sla dit bestand vervolgens op als hello.**c** (let op de extensie). Om nu dit bestand te
compileren voer je op de commandolijn “**cc hello.c -o hello**” (cc =  c compiler) of “make hello” uit. Na het
succesvol compileren kan je bestand uitvoeren door op de commandolijn “**./hello**” in te
tikken. Bemerk dat je voor het uitvoerbaar bestand de “./” niet mag vergeten!

Wanneer je met de opdracht “**file**” informatie over het uitvoerbaar bestand opvraagt, zal je
merken dat er gebruikgemaakt wordt van shared libraries en dat het uitvoerbaar bestand
dus **niet alle code** bevat om de string “Hello world!” naar het scherm te schrijven. Is dit niet
de bedoeling, dan kan je bij het compileren de compileroptie “**-static**” opgeven (installeer
hiervoor de static versie van de C API via **yum install glibc-static**). Hierdoor wordt alles
**statisch** gelinkt en krijg je dus een uitvoerbaar bestand dat alle code bevat om de gegeven
tekst naar het scherm te schrijven.

> **extra:**
>
> Compileren naar assembly (test.s): **cc -S test.c**
>
> Compileren naar Object file (test.o): **cc -c test.c**

**Opdracht**

> Compileer bovenstaand bestand dynamisch en statisch en bekijk het verschil in grootte. De
> grootte van een bestand kan je het gemakkelijkst achterhalen met de opdracht “du” of met
> de opdracht “**ls**”. Maak in beide gevallen handig gebruik van de optie “**-h**“ om de
> bestandsgrootte in bytes, KB, MB, ... te krijgen.

```bash	
cc -static test.c #statisch. Grotere bestandsgrootte. Te gebruiken wanneer benodigde libraries niet aanwezig zijn op systeem.
cc -c test.c #dynamic


root@localhost c]# ls -l
total 1712
-rwxr-xr-x 1 root root 1713536 Jun 12 09:32 a.out #static
-rwxr-xr-x 1 root root   25136 Jun 12 09:31 test
-rw-r--r-- 1 root root      68 Jun 12 09:31 test.c
-rw-r--r-- 1 root root    1504 Jun 12 09:32 test.o #dynamic
```



## Deel III: Profiler programma’s

Bij het schrijven van programma’s zijn er een aantal zaken waar je toch moet op letten. Zo
mag bv. de geschreven code geen memory leakage vertonen, mag de uitvoeringstijd niet te
groot zijn en moet het aantal systeemaanroepen tot een minimum worden beperkt. Onder
Linux zijn er een aantal profiler programma’s waarmee je uitvoerbare bestanden kan
onderzoeken.

### Valgrind

Valgrind is een tool die in zijn meest eenvoudige vorm onderzoekt of de geschreven
software memory leakage vertoond.

**Opdracht**

> Schrijf een C-programma dat via malloc een tabel van 2000 gehele getallen aanmaakt en
> deze getallen daarna gewoon uitschrijft. Je hoeft bewust het in beslag genomen geheugen
> niet vrij te geven. Compileer het programma en voer het daarna uit d.m.v. “valgrind ./prog”.
> Herschrijf nu het programma waar je het gealloceerde geheugen vrijgeeft en controleer
> opnieuw met valgrind of het programma nog geheugenlekken vertoond.

**Zonder vrijgeven:**

```c
#include <stdio.h>
int main() {
  int numbers = malloc(size_of(int)*2000);
  for(int i = 0; i < 2000; i++)
  {
  	numbers[i] = i:
  }
   for(int i = 0; i < 2000; i++)
  {
  	 printf("%d", i);
  }
  return 0;
}

/*  output:
==3563== HEAP SUMMARY:
==3563==     in use at exit: 8,000 bytes in 1 blocks
==3563==   total heap usage: 2 allocs, 1 frees, 9,024 bytes allocated
==3563== 
==3563== LEAK SUMMARY:
==3563==    definitely lost: 8,000 bytes in 1 blocks
==3563==    indirectly lost: 0 bytes in 0 blocks
==3563==      possibly lost: 0 bytes in 0 blocks
==3563==    still reachable: 0 bytes in 0 blocks
==3563==         suppressed: 0 bytes in 0 blocks
==3563== Rerun with --leak-check=full to see details of leaked memory
==3563== 
==3563== For lists of detected and suppressed errors, rerun with: -s
==3563== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
*/
```

**Met vrijgeven:**

```c
#include <stdio.h>
int main() {
  int numbers = malloc(size_of(int)*2000);
  for(int i = 0; i < 2000; i++)
  {
  	numbers[i] = i:
  }
   for(int i = 0; i < 2000; i++)
  {
  	 printf("%d", i);
  }
  
  free(numbers); //Geeft het geheugen vrij
  return 0;
}

/* output:
==3585== HEAP SUMMARY:
==3585==     in use at exit: 0 bytes in 0 blocks
==3585==   total heap usage: 2 allocs, 2 frees, 9,024 bytes allocated
==3585== 
==3585== All heap blocks were freed -- no leaks are possible
==3585== 
==3585== For lists of detected and suppressed errors, rerun with: -s
==3585== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
*/
```



### Time

Om na te gaan hoeveel CPU-tijd een bepaald programma in beslag heeft genomen kan je de
opdracht “time” gebruiken. Het commando time geeft standaard drie timestamps terug. Het
betreft, de totale tijd tussen het starten en het stoppen van het proces, de CPU-tijd voor het
uitvoeren van code in USER-mode en tot slot de CPU-tijd voor het uitvoeren van code in de
KERNEL-mode. De allereerste tijdsaanduiding is eigenlijk de minst interessante omdat een
proces doorgaans niet in één keer wordt uitgevoerd maar door het besturingssysteem
verschillende keren wordt onderbroken.

**Opdracht**

> Herneem het programma dat je daarnet hebt geschreven en voer het nu uit d.m.v. “time
> ./prog”.

**Met Time**

```bash
#output:
real    0m0.004s
user    0m0.000s
sys     0m0.001s
```

### Strace

Soms kan het interessant zijn om te weten welke **systeemaanroepen** een programma
gebruikt. Bekijk de uitvoer van **“strace cat /etc/passwd**”. Dit geeft een sequentieel overzicht
van alles wat bij het uitvoeren van “cat /etc/passwd” gebeurt. Wanneer je een overzicht wil
krijgen van welke systeemaanroepen er gebruikt worden en hoeveel keer ze werden
opgeroepen, dan kan je aan strace de optie “-c” meegeven.

**Overige interessante hulpprogramma’s**

**nm**
Met het commando nm kan je **symboolinformatie** opvragen van uitvoerbare bestanden en
libraries. Wil je weten van welke functies de Linux C API (glibc) de uitvoerbare code bevat?
Voer in een terminal dan nm /lib/libc.so.6 uit en alle lijnen waar een t of T bij vermeld staat
zijn C-functies waarvan je de code via deze bibliotheek kan vinden.

**ldd**
Met **ldd** kan je van ieder uitvoerbaar bestand dat dynamisch gelinkt werkt opvragen van
welke shared libraries het afhankelijk is.

**objdump**
Wil je een uitvoerbaar bestand terug omzetten naar **assembleertaal**, dan kan je handig
gebruikmaken van objdump met de optie -d (disassembly). Wil je de uitvoer zien in Intel
syntax, voeg dan gerust de optie -M intel toe. Bij een uitvoerbaar bestand is het entrypoint,
het punt waar het besturingssysteem code begint uit te voeren, de subroutine _start. Vanuit
het oogpunt van een programmeur is dit main maar besef dat de eerste instructie die door
het OS zal uitgevoerd worden niet de eerste lijn code uit de main-functie is.



## Deel IV: Een eerste programmeeropdracht

Er zijn een aantal commando’s die “ls” als prefix hebben en die allemaal wel de inhoud van
“iets” naar het scherm schrijven. Net zoals **ls** de inhoud van een directory toont, toont **lspci**
de aanwezige PCI(e)-apparaten, toont **lsusb** de aanwezige USB-apparaten en toont **lsmod** de
modules, of drivers, die momenteel door het systeem gebruikt worden.

**Opdracht**

> De bedoeling is een **eigen versie van het commando “lspci -n”** te programmeren in de
> programmeertaal C. Dit commando **overloopt alle mogelijke PCI-adressen** en gaat na of er
> zich een apparaat bevindt. Bevindt er zich een apparaat, dan wordt het adres (busnummer,
> devicenummer en functienummer) naar het scherm geschreven, samen met het vendorID en
> het deviceID.
> I**nfo en werkwijze**
> Om een register van een bepaald apparaat, aangesloten op de PCI-bus, aan te spreken
> moet je te beschikken over het busnummer, devicenummer, functienummer en tot slot
> het registernummer.
> Het aantal bussen binnen het PCI-systeem kan oplopen tot 256. Om te zoeken naar
> hardware is het dus aangewezen om alle mogelijke bussen af te lopen.
> Een device, of apparaat is een fysiek aangesloten “ding” op het PCI-systeem.
> Voorbeelden hiervan zijn videokaarten, geluidskaarten, onderdelen van de chipset,
> netwerkadapters, etc. Iedere bus kan theoretisch 32 apparaten bevatten.
> Ieder apparaat heeft ten minste één functie en ieder aangesloten apparaat op de PCI-
> bus kan maximum 8 functies hebben, genummerd van 0 tot 7.

> Iedere functie van een apparaat heeft 256 registers. Registers 0 tot 3F bevatten een
> zee aan informatie over een bepaalde functie van een bepaald apparaat. Registers 40
> tot FF bevatten dan weer merkspecifieke informatie.
> Registers 0 en 1 bevatten het vendorID en registers 2 en 3 bevatten het deviceID.
> Wanneer bijvoorbeeld het vendorID 8086 is en het deviceID 2829 kan je vrij snel
> achterhalen dat het om een SATA AHCI controller gaat van Intel. Deze informatie kan je
> terugvinden in de PCI vendor database ( http://www.pcidatabase.com ).

> Om de PCI-bus af te scannen moet je telkens een 32-bit getal naar het indexregister
> (adres = 0xcf8 ) van het PCI-systeem sturen. Dit 32-bit getal heeft steeds de volgende
> structuur:

1 gereserveerd busnummer Device # Fct # registernummer

| 1    | gereserveerd | busnummer | Device | Fct  | registernummer |
| ---- | ------------ | --------- | ------ | ---- | -------------- |

31																																																																		0

> Je laat het busnummer variëren van 0 tot 255 (8 bit), het devicenummer telkens van 0
> tot 32 (5 bit) en ten slotte het functienummer van 0 tot 7 (3 bit). Het registernummer
> (8 bit) stel je in op 0.

> Het antwoord krijg je door vervolgens een 32-bit getal te lezen van het dataregister
> (adres = 0xcfc). Indien het antwoord uitsluitend 1-bits telt (0xffffffff), is er op die plaats
> geen apparaat aanwezig. In het andere geval ontvang je de inhoud van de eerste vier
> registers (registers 0 tot 3) van de geadresseerde functie. De meest significante 16-bits
> bevatten het deviceID en de minst significante 16-bits het vendorID.



**Opmerkingen**:

• Om rechtstreeks de hardware te kunnen benaderen, moet je in je code daar
expliciet toestemming voor vragen en ook voor krijgen. Bekijk de man-pagina’s
van de systeemaanroepen iopl en ioperm.

• Net zoals de meeste systeemaanroepen geven deze functies -1 terug wanneer
er iets foutloopt en wordt de gehele variabele errno ingesteld. Om de
foutboodschap die bij errno hoort naar het scherm te schrijven gebruik je de
functie perror(...) die naast de string die als parameter wordt meegegeven ook
de stringversie van errno op het scherm toont. Gebruik dus voor het tonen van
foutboodschappen van systeemaanroepen steeds de perror-functie en maak
dus geen gebruik van printf.

• Om een 32-bit getal naar een adres te schrijven kan je gebruikmaken van de
systeemaanroep “outl”. Een 32-bit getal van een adres lezen kan via “inl”.
Bekijk de manpagina van outl/inl voor de juiste syntax. Opgelet, inl en outl zijn
ook gewone Linux-commando’s. Zorg er dus voor dat je de juiste man-pagina
oproept.**

```c
#include <stdio.h>
int main() {
  //todo
  return 0;

}
```



## Deel V: I/O-Systeemaanroepen



Alle systeemaanroepen die een verwijzing nodig hebben naar een open bestand, maken
gebruik van een **file descriptor**. Een file descriptor is doorgaans een **klein positief geheel**
**getal dat kan verwijzen naar gewone bestanden** maar ook naar **directories, sockets, pipes**, ....
Alles wat eigenlijk op het bestandssysteem bestaat kan worden geopend en kan aan een file
descriptor worden gekoppeld. Bij het starten van een programma zullen drie file descriptors
van de shell worden overgeërfd. De drie file descriptors verwijzen respectievelijk naar het
**standaard invoerkanaal**, het **standaard uitvoerkanaal** en het **standaard foutenkanaal**.
Onderstaande tabel geeft een overzicht.

| File descriptor | Doel                    | POSIX-naam    | stdio-stream |
| --------------- | ----------------------- | ------------- | ------------ |
| 0               | Standaard invoerkanaal  | STDIN_FILENO  | stdin        |
| 1               | Standaardnuitvoerkanaal | STDOUT_FILENO | stdout       |
| 2               | Standaard foutenkanaal  | STDERR_FILENO | stderr       |



Een bestand openen gebeurt via de systeemaanroep **open(pathname, flags, mode)** die een
**geheel getal**, de **file descriptor** dus, **teruggeeft** of **-1** wanneer er een **fout** optreedt. De eerste
paramater die je moet opgeven is het **pad** naar het bestand. De tweede parameter bevat
een aantal statusvlaggen die bij het openen van het bestand worden geraadpleegd.
Wanneer je een bestand wil openen om er uitsluitend van te lezen, geef je als **flags**
“**O_RDONLY**” op. Wanneer je naar een bestand wil schrijven en er ook van wil lezen is de
flags-parameter gelijk aan “**O_RDWR**”. Combineren van statusvlaggen gebeurt via de
logische |-operator. Zo kan je een bestand openen om er naar te schrijven en tevens
opgeven dat het moet worden aangemaakt wanneer het niet zou bestaan. De flags-
parameters is in dit geval “**O_WRONLY | O_CREAT”**. De combinatie “**O_WRONLY | O_CREAT**
**| O_APPEND**” betekent dat het bestand zal worden aangemaakt wanneer het niet bestaat,
dat er enkel naar geschreven zal worden en dat alle data die er naartoe wordt geschreven
**achteraan** zal worden **toegevoegd**. De **O_APPEND** vlag verzekert dus dat indien het bestand
reeds zou bestaan, de bestaande inhoud **niet zal worden overschreven**.
De laatste parameter van de systeemaanroep open is optioneel en is enkel van belang
wanneer de **O_CREAT** vlag is opgegeven.
Om van een **file descriptor te lezen** gebruik je de systeemaanroep **read(fd,buffer,count)**.
Buffer is een **void-pointer** naar een **geheugenlocatie** waar de gelezen bytes zullen worden
weggeschreven. Count is het aantal bytes die je van de opgegeven file descriptor wil lezen.
De read-systeemaanroep geeft het aantal gelezen bytes terug en -1 wanneer er bij het lezen
een fout optreedt.

Met de **write(fd,buffer,count)** systeemaanroep kan je bytes van een geheugenlocatie naar
een filedescriptor schrijven. De parameters zijn gelijkaardig aan die van de read-
systeemaanroep en ook de return-waarde is hetzelfde, i.e. het aantal weggeschreven bytes
of -1.

Tot slot kan je met de systeemaanroep **close(fd)** een filedescriptor sluiten.

**samenvatting system calls:**

> **open(pathname, flags, mode)**
>
> **read(fd,buffer,count)**
>
> **write(fd,buffer,count)**
>
> **close(fd)**



**Opdrachten**

1. > Schrijf een C-programma dat een bestand van (ongeveer) 10MB aanmaakt met
   > willekeurige lettertekens gelegen in het gesloten interval [a..z].



```c
#include <unistd.h> //ALTIJD
#include <sys/types.h> //normaal krijg je ze wel op het examen
#include <stdlib.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <time.h>
int main(int argc, char **argv){
	srand(time(0));									//wanneer je willekeurige characters nodig hebt
	int fd = open("largefile", O_WRONLY|O_CREAT);	 //returnt int en opent bestand in write only 
													 //creeërt bestand indien het nog niet bestaat
   
    if(fd<0){ 										//als de returnwaarde < 1 is, is er een fout opgetreden
		perror(argv[0]); 							//geeft de error terug
		return 1; 									//geeft aan aan bash dat er een fout opgetreden is
	}

	int i;
	for(i=0; i< 10*1024*1024; i++){
		char ch = rand()%26 + 'a';				//random char
		if(write(fd, &ch, 1) < 0){ 				//(fd,buffer,mode) //adres van buffer is &ch //1byte
			perror(argv[0]); 					//geeft de error terug omdat hij niks geschreven heeft
			return 1;							//geeft aan aan bash dat er een fout opgetreden is
		}
	}
	
	if(close(fd) < 0){ 							//file descriptor altijd weer sluiten!
		perror(argv[0]);
		return 1;
	}
	
}
```

**Deze aanpak is heel traag omdat er veel I/O opdrachten zijn. Dit kan geoptimaliseerd worden:**

```C
int i,j;
char buffer[1024];
for(i=0; i< 10*1024; i++){
	
    for(j = 0; j < 1024; j++){
		buffer[j] = rand()%26 + 'a';
	}
	
    if(write(fd, buffer, 1) < 0){
		perror(argv[0]); //geeft de error terug omdat hij niks geschreven heeft
		return 1;
	}
}
```



2. > Tot nog toe werd er niets gezegd over de optimale buffergrootte. De bedoeling is een C-
   > programma te ontwikkelen dat het **hierboven aangemaakte bestand verschillende keren**
   > **inleest en dit met buffergroottes van 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048,**
   > **4096 en tot slot 8192 bytes**. De uitvoer van het programma moet er ongeveer zo uitzien:

```bash	
BUF_SIZ= 1 Time=3.60
BUF_SIZ= 2 Time=1.79
BUF_SIZ= 4 Time=0.98
BUF_SIZ= 8 Time=0.48
BUF_SIZ= 16 Time=0.24
BUF_SIZ= 32 Time=0.12
BUF_SIZ= 64 Time=0.06
BUF_SIZ= 128 Time=0.03
BUF_SIZ= 256 Time=0.02
BUF_SIZ= 512 Time=0.01
BUF_SIZ=1024 Time=0.00
BUF_SIZ=2048 Time=0.00
BUF_SIZ=4096 Time=0.00
BUF_SIZ=8192 Time=0.00
```

> Om de tijd tussen het starten het stoppen met lezen op te meten kan je gebruikmaken
> van onderstaande code:

```bash
double start=clock();
...
double time=(clock()-start)/CLOCKS_PER_SEC;
```

```c	
#include <unistd.h> 
#include <sys/types.h> 
#include <stdlib.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <time.h>
#include <pthread.h>
int main(int argc, char **argv){
	
	int fd = open("largefile", O_RDONLY)
	if(fd<0){
		perror(argv[0]); 
		return 1;
	}
	
	int i;
	
	char buffer[8192];								//buffergrootes van 1 -> 8192. Zonder malloc
	for(i = 1; i<8192; i<<1){ 						//left shift == maal 2
		double start=clock();
		
		if(lseek(fd,0, SEEK_SET) < 0;{			 	 //gebruik lseek om de file descriptor terug aan het begin (0) te zetten
            										 //SEEK_SET = absolute waarde meegegeven van adres waar het moet staan
			perror(argv[0]);
			return 1;
		}
		  				
		int n = read(fd,buffer,i);  				//lees altijd i bytes in totdat er geen meer zijn
		while(n > 0){
			n = read(fd,buffer,i);
		}
        
		if(n<0){
			perror(argv[0]);
			return 1;
		}
		printf("BUF_SIZ=%5d Time=%10.2f\n", i, (clock() - start) / CLOCKS_PER_SEC))
	}
	
    
	if(close(fd) < 0){
		perror(argv[0]);
		return 1;
	}
}
```

3. > De clock-functie en de macro **CLOCKS_PER_SEC** vind je in de bibliotheek **pthread.h** Doe nu hetzelfde maar voor de write-systeemaanroep. Maak voor iedere verschillende buffergrootte een bestand aan van ongeveer 10MB (cfr. vraag 1). Nadat je de tijd voor een gegeven buffergrootte hebt opgemeten moet je vanzelfsprekend het aangemaakte bestand terug **verwijderen**. Een bestand verwijderen kan je doen m.b.v. de **unlink**-
   > **systeemaanroep**.
   >
   > **Een leesopdracht is sneller dan een schrijfopdracht.**

```c	


#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <time.h>
#include <pthread.h>

void maak_buffer(char *buffer, int n)
{
    int i = 0;
    for (i = 0; i < n; i++)
    {
        buffer[i] = rand() % 26 + 'a';
    }
    return;
}

int main(int argc, char **argv)
{
    srand(time(0));
    char buffer[8192]; //buffergrootes van 1 -> 8192. Zonder malloc
    int i;
    for (i = 1; i < 8192; i << 1)
    { //left shift == maal 2
        double start = clock();
        printf("%d",i);
        int fd = open("largefile", O_WRONLY | O_CREAT);
        if (fd < 0)
        {
            perror(argv[0]);
            return 1;
        }
        maak_buffer(buffer, i);
        int tot = 0;
        int n = write(fd, buffer, i); 			//lees altijd i bytes in totdat er geen meer zijn
        while (n < (10 * 1024 * 1024 - i))
        {	 
            printf("%d",tot);
            tot += n;
            maak_buffer(buffer, i);
            n = write(fd, buffer, i);
        }

        if (n < 0)
        {
            perror(argv[0]);
            return 1;
        }

        maak_buffer(buffer, i);
        n = write(fd, buffer, i);
        tot += n;
        if (n < 0)
        {
            perror(argv[0]);
            return 1;
        }

        if (close(fd) < 0) 						//bestand sluiten alvorens verwijderen
        {
            perror(argv[0]);
            return 1;
        }

        if (unlink("largefile") < 0) 			//bestand verwijderen
        {
            perror(argv[0]);
            return 1;
        }

        printf("Totaal=%d BUF_SIZ=%5d Time=%10.2f\n", tot, i, (clock() - start) / CLOCKS_PER_SEC);
    }
}
```

4. > Herneem vraag 3 maar voeg aan de flags-parameter de **O_SYNC** vlag toe. Dit laatste zorgt
   > ervoor dat er **noch** in **USER-mode** noch in **KERNEL-mode** zal worden gebufferd en dat de
   > **bytes rechtstreeks naar de schijf zullen worden geschreven.**
   >
   > Ter info, de vaste schijf beschikt om performantieredenen over een bepaalde
   > hoeveelheid write-back-cache-geheugen waar gegevens van I/O- schrijfopdrachten
   > tijdelijk worden bewaard. Dit betekent dat er bij een eventuele spanningsonderbreking
   > wel degelijk gegevens kunnen verloren gaan. Bij programma’s, zoals gegevensbanken,
   > waar gegevensverlies nefast is, wordt er aangeraden om “write-caching” uit te
   > schakelen. Dit kan je doen door in een shell de opdracht “hdparm -W0 /dev/sda” uit te
   > voeren.

```c	
#include <unistd.h> 
#include <sys/types.h> 
#include <stdlib.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <time.h>
#include <pthread.h>

void maak_buffer(char *buffer, int n){
	int i;
	for(i = 0; i < n; i++){
		buffer[i] = rand()%26 + 'a';
    }
}


int main(int argc, char **argv){
	srand(time(0));
	int i;
	char buffer[8192];
	for(i = 1; i<8192; i<<1){
		double start=clock();
	
		int fd = open("largefile", O_WRONLY|O_CREAT|O_SYNC); //dit opent de file in read only
        													//syncronised I/O. buffer iedere keer flushen
	
		if(fd<0){
			perror(argv[0]); 
			return 1;
		}
		maak_buffer(buffer,i);
		
		
		int n = write(fd,buffer,i);
		int tot=0;
	
		while( tot<  (10*1024*1024) - i){ 					//je doet -i omdaje moet controleren op de laatste schrijfopdracht
			tot+= n;
			maak_buffer(buffer,i);
			n = write(fd,buffer,i);
		}
		maak_buffer(buffer,i);
		n = write(fd,buffer,i);
		tot+= n;
		if(n<0){
			perror(argv[0]);
			return 1;
		}
		
		if(close(fd) < 0){ 								//bestand sluiten alovers te verwijderen
			perror(argv[0]);
			return 1;
		}
		
		if(unlink("largefile") < 0 ){
			perror(argv[0]);
			return 1;
		}
		printf("Totaal=%d BUF_SIZ=%5d Time=%10.2f\n",tot, i, (clock() - start) / CLOCKS_PER_SEC);
	}
}
```

5. >Bestudeer gronding de werking van de shell-opdracht cat en schrijf in C een eigen versie
   >van **cat**. Bekijk bv. wat er gebeurt wanneer je de opdracht “cat /etc/passwd - /etc”
   >opgeeft of wanneer cat geen argumenten meekrijgt. Wanneer je een directory opgeeft
   >als argument, geeft cat een foutmelding. Dit gedrag hoef je niet na te bootsen.

```c	
#include <unistd.h>
#include <fcntl.h>
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/mman.h>
#include <string.h>

int main(int argc, char **argv)
{
    unsigned char buffer[BUFSIZ];

    if (argc == 1)
    {                                    //wanneer er geen params zijn meegegeven
        int n = read(0, buffer, BUFSIZ); //lezen standaard invoer
        while (n > 0)
        {
            write(1, buffer, n);
            n = read(0, buffer, BUFSIZ); //n geeft aantal bytes weer
        }
        if (n < 0)
        {
            perror(argv[0]);
            exit(1);
        }
    }
    else 								//wanneer er wel params zijn meegegeven
    {
        int i;
        for (i = 1; i < argc; i++)
        {
            int fd = open(argv[i], O_RDONLY); // bestand Read-only openen
            if (fd < 0)
            { 								// controleren of bestand is geopend.
                perror(argv[i]);
                continue; 					//programma mag door gaan
            }
            int n = read(fd, buffer, BUFSIZ);
            while (n > 0)
            { //buffer van geopende bestand uitschrijven en het volgende deel ervan inlezen naar de buffer
                n = write(1, buffer, n);
                if (n < 0)
                {
                    perror(argv[i]);
                    continue;
                }
                n = read(fd, buffer, BUFSIZ);
            }
            if (n < 0)
            {
                perror(argv[i]);
                continue;
            }

            if (close(fd) < 0)
            {
                perror(argv[i]);
                continue;
            }
        }
    }
    return 0;
}
```

6. >Schrijf een eigen versie van de opdracht **cp** waar twee argumenten op de opdrachtlijn
   >worden verwacht. Het **eerste argument is het bronbestand** en het **tweede het**
   >**doelbestand**. Wanneer de eerste parameter een **directory is, wordt een foutboodschap**
   >**naar het scherm geschreven en stopt het programma met exit-status 1**. **Wanneer het**
   >**tweede argument een directory is, wordt opnieuw gestopt met een passende**
   >**foutboodschap en met exit-status 1.** Om na te gaan of een argument een directory is, kan je gebruikmaken van de
   >systeemaanroep **stat**. Om een programma te stoppen met exit-status 1 maak je best
   >gebruik van de bibliotheekfunctie exit die dan achter de schermen de systeemaanroep
   >_exit aanroept.

   
   
   **Read/Write Oplossing:**
   
   ```bash
   #include <unistd.h>
   #include <fcntl.h>
   #include <sys/types.h>
   #include <sys/stat.h>
   #include <stdio.h>
   #include <stdlib.h>
   
   typedef struct stat sstat;
   
   int main(int argc, char ** argv){
   	if (argc!=3){
   		fprintf(stderr,"Gelieve twee argumenten op te geven\n");
   		exit(1);
   	}
   	
   	int fd_in, fd_out;
   
   	fd_in=open(argv[1],O_RDONLY);
   	if (fd_in<0){
   		perror(argv[1]);
   		exit(1);
   	}
   	
   	sstat s;
   
   	if (fstat(fd_in,&s)<0){
   		perror(argv[1]);
   		exit(1);
   	}
   	
   	fd_out=open(argv[2],O_WRONLY | O_CREAT, s.st_mode);
   	if (fd_out<0){
   		perror(argv[2]);
   		if (close(fd_in)<0){
   			perror(argv[1]);
   		}
   		exit(1);
   	}
   	unsigned char buffer[BUFSIZ];
   	int bytesread=read(fd_in,buffer,BUFSIZ);
   	int byteswritten;
   	
   	while (bytesread>0){
   		byteswritten=write(fd_out,buffer,bytesread);
   		bytesread=read(fd_in,buffer,BUFSIZ);
   	}
   	if (bytesread<0){
   		perror(argv[1]);
   		if (close(fd_in)<0 || close(fd_out)<0){
   			perror(argv[1]);
   		}
   		exit(1);
   	}
   	
   	if (byteswritten<0){
   		perror(argv[2]);
   		if (close(fd_in)<0 || close(fd_out)<0){
   			perror(argv[1]);
   		}
   		exit(1);
   	}
   
   	if (close(fd_in)<0){
   		perror(argv[1]);
   		exit(1);
   	}
   
   	if (close(fd_out)<0){
   		perror(argv[2]);
   		exit(1);
   	}
   
   	return 0;
   }
   ```
   
   
   
   **Memory Mapping (mmap) Oplossing:**
   
   ```c	
   #include <unistd.h>
   #include <fcntl.h>
   #include <sys/types.h> 
   #include <sys/stats.h> 
   #include <stdio.h> 
   #include <stdlib.h>
   #include <sys/mman.h>
   #include <string.h>
   
   int main(int argc, char ** argv){ 
       if (argc!=3){ 
           char fout[]="Geen twee bestanden opgegeven!\n"; 
           write(2,fout,strlen(fout)); 
           exit(1); 
       }
   	
       int fd_in=open(argv[1],O_RDONLY); //file descriptor eerste bestand
      
       if (fd_in<0){
           perror(argv[1]); 
           exit(1); 
       }     
      struct stat s; 
     
       if (fstat(fd_in,&s)<0){ 
          perror(argv[1]);
          exit(1); 
      }
       
      int fd_out=open(argv[2],O_WRONLY|O_CREAT,s.st_mode);	//file descriptor voor het bestand waar naar geschreven moet worden
       												   	//file_name, write only, mode/permissies als bestand niet bestaat
       
     
       if(fd_out<0){
            perror(argv[2]);
            exit(1); 
       }
       
       unsigned char * in=mmap(NULL,s.st_size,PROT_READ ,MAP_PRIVATE,fd_in,0); //s.st_size= grootte i/o bestand
       unsigned char * out=mmap(NULL,s.st_size,PROT_READ | PROT_WRITE, MAP_PRIVATE,fd_in,0);
       
      if(in == MAP_FAILED || out == MAP_FAILED){
          perror(argv[0]);
          exit(1); 
      }
       
      if(close(fd_in)<0){ //file descriptors mogen gesloten worden na memory mapping (mmap)
          perror(argv[1]);
          exit(1);
      }
       
      if(close(fd_out)<0){ //file descriptors mogen gesloten worden na memory mapping (mmap)
          perror(argv[1]);
          exit(1);
      }
          
      int i; 
      for(i=0;i<s.st_size;i++)
      { 
          out[i] = in[i];
      } 
      munmap(in,s.st_size);
      munmap(out,s.st_size);
       
      return 0;
       
   }
   ```
   
7. Schrijf een C-programma met als naam **watchfile**.c dat één argument, een bestand, op de
   opdrachtlijn verwacht. Het programma loopt in een oneindige lus en schrijft telkens een
   boodschap naar het scherm wanneer het bestand dat op de opdrachtlijn werd
   meegegeven werd gewijzigd. Wanneer er geen argument werd opgegeven of het
   argument is geen gewoon bestand wordt een foutboodschap getoond en wordt het
   programma afgesloten met exit-status 1.

```c	
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>
#include <time.h>
#include <string.h>

int main(int argc, char **argv){
	if (argc!=2) // controle op juiste usage (juiste aantal argumenten)
    { 
		char str[] = "Usage: watchfile <filename>";
        write(2, str, strlen(str));
        exit(1);
    }

    int fd=open(argv[1], O_RDONLY); // controle of bestand geopend kan worden
    if (fd<0)
    {
        perror(argv[1]);
        exit(1);
    }

    struct stat s; 

    if(stat(fd,&s)<0)  //stat informatie controleren
    {
        perror(argv[1]);
        exit(1);
    }

    if (! S_ISREG(s.st_mode) ) //S_ISREG is een macro om te testen of het een "regular" bestand is en bv geen directory.
    {
        char str[] = "Error: Meegegeven argument is geen bestand";
        write(2, str, strlen(str));
        exit(1);
    }

    int check = s.st_mtimespec.tv_sec; //modification tijd
    while (1)
    {
        if(fstat(fd,&s)<0) 
        {
            perror(argv[1]);
            exit(1);
        }
        int time=s.st_mtimespec.tv_sec; 
        if (time!=check) //checken of modification tijd is veranderd
        {
            char str[] = "File changed!";
            write(1, str, strlen(str));
            check=time;
        }   
        sleep(1);
    }
    
    return 0;
}
```





## Deel VI: Processen en POSIX-threads

Een **nieuw proces aanmaken** gebeurt met de systeemaanroep **fork()**. De **systeemaanroep**
maakt een nieuw proces aan, het **kind**, dat bijna een exacte kopie is van het proces dat de
systeemaanroep heeft gebruikt, het **ouderproces**. Na het beëindigen van de systeemaanroep
beschik je over **twee processen**, het **kind en het ouderproces,** die beide de uitvoering
**verderzetten** bij het **terugkeren** van de **fork()-systeemaanroep**. Beide processen beschikken
over **dezelfde programmatekst** maar hebben elk hun **eigen kopie van de stapel, de heap, en**
**het datasegment**. Initieel bevat de stapel, de heap, en het datasegment van het kindproces
dezelfde informatie als de overeenkomstige segmenten van het ouderproces. Om in een
programma het onderscheid te kunnen maken tussen het kind en het ouderproces moet je
weten dat de systeemaanroep fork() t**wee verschillende return-waardes heeft**. In het
**kindproces** geeft **fork()** de waarde **0** terug, terwijl in het **ouderproces** het **proces-ID van** het
**nieuwe aangemaakte kindproces** wordt teruggegeven.



**Opdrachten**

1. > Gegeven onderstaande code:

```bash
int main(int argc, char **argv){
...
fork();
fork();
fork();
...
}
```

> Voorspel hoeveel kindprocessen er zullen worden aangemaakt zonder de code uit te
> voeren.

```bash
2^3-1 kindprocessen. =7

fork()

p
\
c1

fork()

	 p
  /	   \
c1		c2
  \
   c3

fork()
			
	--------p-----------
    /	   	\			\
   c1		c2			c4
  /	  \		  \
  c3  c5	  c6
    \
   	c7
```

2. > Schrijf een programma dat **drie kindprocessen** aanmaakt en zorg ervoor dat ieder
   > kindproces zijn **proces-ID** naar het scherm **schrijft** en daarna **stopt**. Het proces-ID kan je
   > m.b.v. de systeemaanroep **getpid()** opvragen en een proces kan je beëindigen met de
   > functie **exit (int exitstatus).** De **exitstatus** van een **correct beëindigd** proces is steeds **0**
   > terwijl een waarde **verschillend** van **0** duidt op een **fout**.

   > In bovenstaande opdracht kan je nog met een eenvoudige if/else-structuur het onderscheid
   > maken tussen wat het **ouderproces** en wat het **kindproces** moet uitvoeren. Het kindproces
   > moet immers alleen maar zijn proces-ID naar het scherm schrijven en zichzelf beëindigen.
   > Wanneer het gaat om meer dan een paar lijnen code, is het interessanter om een nieuw
   > programma te ontwikkelen, eventueel zelfs in een andere programmeertaal, dat je
   > onmiddellijk na de fork()-systeemaanroep uitvoert. Hetzelfde geldt wanneer het kindproces
   > een programma moet uitvoeren dat reeds bestaat en dat dus niet door jou nog moet
   > worden ontwikkeld. 
   >
   > Een nieuw programma uitvoeren gebeurt met de systeemaanroep **execve**(const char*
   > filename, char *const argv[], char *const envp[]). Execve zal het tekstsegment, het
   > datasegment, de stapel en de heap van het huidige **proces** **overschrijven** met de gegevens
   > van het uitvoerbaar bestand filename. **Argumenten voor het nieuwe programma** worden als
   > tweede parameter argv opgegeven. Als laatste parameter envp kan je een **tabel van strings**,
   > in de vorm van naam-waardeparen, doorgeven aan het nieuwe programma.
   > Bemerk dat bij de oplijsting van systeemaanroepen met strace execve op de eerste lijn staat.
   > Concreet wil dit zeggen dat van het shellproces een kopie gemaakt wordt en dat
   > onmiddellijk daarna het proces wordt overschreven met de inhoud van de opdracht die je op
   > de opdrachtlijn hebt ingetikt.
   > Naast het rechtstreeks gebruik van de systeemaanroep **execve**, bestaan er een aantal
   > bibliotheek-functies die allemaal na een aantal tussenstappen execve zullen aanroepen. Deze
   > functies beginnen allemaal met het woord **exec** gevolgd door één of twee letters. Het
   > verschil met execve zit hem in het aantal parameters en de manier waarop de argumenten
   > aan het nieuwe programma worden doorgegeven. Hieronder vind je een overzicht.
   >
   > ![Imgur](https://imgur.com/Io8v4Ky.png)
   
   ```c
   #include <unistd.h>
   #include <sys/types.h>
   #include <stdlib.h>
   #include <sys/stat.h>
   #include <fcntl.h>
   #include <stdio.h>
   #include <time.h>
   #include <pthread.h>
   #include <string.h>
   
   int main(int argc, char **argv)
   {
       int pid = fork();
       if (pid == 0)						//als pid==0 dan ben je bezig in het child proces
       {
           printf("this is child \n");
           return 0;
       }
       else if (pid > 0)					//anders in het parent proces
       {
           printf("this is parent \n");
           sleep(60);						//proces staat vrijwillig proces af aan ander proces = wisselen proces
           return 0;
       }
       else 								//kleiner dan 0. Foutmelding
       {
           perror(argv[0]);
       }
       return 0;
   }
   ```
   
   **Met execv: overschakelen naar ander stukje code binnen kind proces**
   
   ```C
   #include <unistd.h>
   #include <sys/types.h>
   #include <stdlib.h>
   #include <sys/stat.h>
   #include <fcntl.h>
   #include <stdio.h>
   #include <time.h>
   #include <pthread.h>
   #include <string.h>
   
   int main(int argc, char **argv)
   {
       int pid = fork();
       if (pid == 0)							//als pid==0 dan ben je bezig in het child proces
       {
           char * args[]={"ls","-l","/",0}; 	//mee te geven argumenten. argv[0] is "ls".  afsluiten met 0
          	execv("/usr/bin/ls",args);			//path te vinden adhv "whereis ls"
           									//keert niet meer terug wanneer execv succesvol uitgevoerd wordt.
           									//Alles onder execv wordt niet meer uitgevoerd in dat geval.
           return 0;
       }
       else if (pid > 0)						//Parent process
       {
           waitpid(pid,NULL,0);				//wachten tot dat kindproces klaar is
           return 0;
       }
       else 									//kleiner dan 0. Foutmelding
       {
           perror(argv[0]);
       }
       return 0;
   }
   ```
   
   **Examenvraag vorig jaar: Voer base64 uit op elke meegegeven argument(bestand) (theorie les7)**
   
   ```C
   #include <unistd.h> 
   #include <sys/types.h> 
   #include <stdlib.h>
   #include <sys/stat.h>
   #include <fcntl.h>
   #include <stdio.h>
   #include <time.h>
   #include <pthread.h>
   #include <string.h>
   int main(int argc, char **argv){
   	
   	int pids[argc];    								 //maak voor elk argument een kindproces aan.
   
   	for(i = 1; i < argc; i++){
   		pids[i] = fork(); 							//voor elk argument een nieuw kindproces aanmaken
   		if(pids[i] < 0){
   			perror(argv[i]);
   			return 1;
   		}
   		else if (pids[i] == 0){
   			//CHILD
   			char *args[] = {"base64", argv[i],0}; 	//de p in execvp zorgt er voor dase je ook path variabele kan geven
   			if(execvp("base64", args) < 0){ 		//in plaats van het volledige path
   				perror(argv[i]);
   				return 1;
   			}
   		}
   	}
   	
   	for(i = 1; i < argc; i++){
   		waitpid(pids[i],NULL,0); 					//parent proces moet wachten tot elk kind proces klaar is
   	}
   	return 0;
   }
   ```
   
   **oef interprocescommunicatie (pip') (theorie les7)**
   
   ```C
   int main(int argc, char **argv){
   	int fd[2]; 							//de pipe
   	
   	if(pipe(fd) < 0){ 					//maakt de pipe
   		perror(argv[0]);
   		return 1;
   	}
   	
   	int pid=fork(); 					//maak de child
   	if(pid<0){							//bij fout
   		perror(argv[0]);
   		return 1;
   	}
   	else if(pid == 0){ 					
   		close(fd[1]);					//in de child de fd om naar te schrijven sluiten. Enkel nog lees fd gebruiken
   		int ontvangengetal;
   		read(fd[0], &ontvangengetal, sizeof(int));
   		printf("%d", ontvangengetal);
   		return 0;
   	}
   	
   	close(fd[0]);						//in de parent de fd sluiten om te lezen. Kan enkel nog maar de schrijf fd gebruiken
   	int getal = 165465465;
   	write(fd[1], &getal, sizeof(int));
   	waitpid(pid, NULL,0);
   }
   ```
   
   
   
   **Extra oef: Pipe in 2 richtingen (= 2pipes) (theorie les 7, 01:10)** 
   
   ```C
   #include <unistd.h>
   #include <sys/types.h>
   #include <sys/stat.h>
   #include <sys/wait.h>
   #include <fcntl.h>
   #include <stdlib.h>
   #include <stdio.h>
   #include <time.h>
   #include <errno.h>
   
   int main(int argc, char **argv){
   	int fd_PC[2];
   	int fd_CP[2];
   	if (pipe(fd_PC)<0){
   		perror(argv[0]);
   		return 1;
   	}
   	if (pipe(fd_CP)<0){
   		perror(argv[0]);
   		return 1;
   	}
   	int pid=fork();
   	if (pid<0){
   		perror(argv[0]);
   		return 1;
   	}
   	else if (pid==0){
   		close (fd_PC[1]);
   		close( fd_CP[0]);
   		int getal;
   		read(fd_PC[0],&getal,sizeof(int));  
   		close(fd_PC[0]);
   		getal++;
   		write(fd_CP[1],&getal,sizeof(int));
   		close(fd_CP[1]);
   		return 0;
   	
   	}
   	close(fd_PC[0]);
   	close(fd_CP[1]);
   
   	int getal=144;
   	write(fd_PC[1],&getal,sizeof(int));
   	close(fd_PC[1]);
   	read(fd_CP[0],&getal,sizeof(int));
   	close(fd_CP[0]);
   	printf("%d\n",getal);
   	waitpid(pid,NULL,0);
   
   	return 0;
   }
   ```
   
   **Extra oef Parent met 2 childs met pipes tussen (theorie les 7, 01:25)**
   
   ```C
   #include <unistd.h>
   #include <sys/types.h>
   #include <sys/stat.h>
   #include <sys/wait.h>
   #include <fcntl.h>
   #include <stdlib.h>
   #include <stdio.h>
   #include <time.h>
   #include <errno.h>
   
   int main(int argc, char **argv){
   	int fd_PC1[2];
   	int fd_C1C2[2];
   	int fd_PC2[2];
   	if (pipe(fd_PC1)<0){
   		perror(argv[0]);
   		return 1;
   	}
   	if (pipe(fd_C1C2)<0){
   		perror(argv[0]);
   		return 1;
   	}
   	if (pipe(fd_PC2)<0){
   		perror(argv[0]);
   		return 1;
   	}
   
   	int pid=fork();
   	if (pid==0){
   		//CHILD1
   		close(fd_PC1[1]);
   		close(fd_PC2[0]);
   		close(fd_PC2[1]);
   		close(fd_C1C2[0]);
   		int g;
   		read(fd_PC1[0],&g,sizeof(int));
   		g*=2;
   		write(fd_C1C2[1],&g,sizeof(int));
   		return 0;
   	}
   	
   	int pid2=fork();
   	if (pid2==0){
   		//CHILD2
   		close(fd_PC2[1]);
   		close(fd_PC1[0]);
   		close(fd_PC1[1]);
   		close(fd_C1C2[1]);
   		int g,g2;
   		read(fd_PC2[0],&g2,sizeof(int));
   		read(fd_C1C2[0],&g,sizeof(int));
   		printf("%d\n",g*2+g2);
   		return 0;
   	}
   	//PARENT
   	close(fd_PC1[0]);
   	close(fd_PC2[0]);
   	close(fd_C1C2[0]); //parent heeft geen baat bij deze pipe
   	close(fd_C1C2[1]); //parent heeft geen baat bij deze pipe
   	int g,g2;
   	g=144;
   	g2=288;
   	write(fd_PC1[1],&g,sizeof(int));
   	write(fd_PC2[1],&g2,sizeof(int));
   
   	waitpid(pid,NULL,0);
   	waitpid(pid2,NULL,0);
   	return 0;
   }
   ```
   
   **Zelfde oefening als hierboven maar uitgewerkt met semafore ipv pipes (theorie les 9, 01:40)**
   
   ```bash
   #include <sys/mman.h>
   #include <unistd.h>
   #include <stdio.h>
   #include <pthread.h>
   #include <semaphore.h>
   #include <sys/types.h>
   #include <fcntl.h>
   #include <string.h>
   #include <sys/wait.h>
   #include <sys/stat.h>
   #include <stdlib.h>
   
   typedef struct
   {
       int g;
       int g2;
       sem_t P_C1;
       sem_t P_C2;
       sem_t C1_C2;
   } data;
   
   int main(int argc, char **argv)
   {
   
       data *d = mmap(NULL, sizeof(data), PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);
   	//memory map om data tussen processen te delen
       
       sem_init(&d->P_C1, 1, 1);
       sem_init(&d->P_C2, 1, 1);
       sem_init(&d->C1_C2, 1, 1);
   
       int pid = fork();
   
       if (pid < 0)
       {
           printf("pid");
           perror(argv[0]);
           exit(1);
       }
       else if (pid == 0) //Child 1
       {
   
           sem_wait(&d->P_C1); //wachten op data afkomstig van parent semafoor
           d->g *= 2;
           sem_post(&d->C1_C2); //kanaal mag weer openen om data te versturen
           return 0;
       }
   
       int pid2 = fork();
   
       if (pid2 < 0)
       {
           perror(argv[0]);
           exit(1);
       }
       else if (pid2 == 0) //Child 2
       {
           sem_wait(&d->P_C2); //wachten op data afkomstig van deze semaforen
           sem_wait(&d->C1_C2);
           printf("g*2+g2: %d", d->g * 2 + d->g2);
           return 0;
       }
   
       //parent
   
       d->g = 5;
       d->g2 = 7;
   
       sem_post(&d->P_C1);
       sem_post(&d->P_C2);
   
       waitpid(pid, NULL, 0);
       waitpid(pid2, NULL, 0);
   
       sem_close(&d->P_C1);
       sem_close(&d->P_C2);
       sem_close(&d->C1_C2);
   
       return 0;
   }
   ```
   
   
   
   **Vraag die hij (bijna) elk jaar stelt: cmd1 | cmd2. Opdrachten aan elkaar kleven adhv een pipe (theorie les 7, 01:42)**
   
   ```c
   #include <unistd.h>
   #include <sys/types.h>
   #include <sys/stat.h>
   #include <sys/wait.h>
   #include <fcntl.h>
   #include <stdlib.h>
   #include <stdio.h>
   #include <time.h>
   #include <errno.h>
   
   // ls -l / | wc -l  (child 1 | child 2)
   
   int main(int argc, char **argv){
   	int fd_C1C2[2];
   	if (pipe(fd_C1C2)<0){
   		perror(argv[0]);
   		return 1;
   	}
   
   	int pid=fork();
   	if (pid==0){
   		//CHILD1
   		//close(1); //sluit output (write)
   		//dup(fd_C1C2[1]); //schrijffiledescriptor == 1
   		dup2(fd_C1C2[1],1); //kopieert de ene fd naar de andere (oldfd,newfd)
   		close(fd_C1C2[0]);
   		char *args[]={"ls","-l","/",0};
   		execvp("ls",args);
   		return 0;
   	}
   	
   	int pid2=fork();
   	if (pid2==0){
   		//CHILD2
   		//close(0); //sluit input (read)
   		//dup(fd_C1C2[0]);   //leesfiledescriptor == 0
           dup2(fd_C1C2[0],0);
   		close(fd_C1C2[1]);
   		char *args[]={"wc","-l",0};
   		execvp("wc",args);
   		return 0;
   	}
   	//PARENT
   	close(fd_C1C2[0]);
   	close(fd_C1C2[1]);
   	waitpid(pid,NULL,0);
   	waitpid(pid2,NULL,0);
   	return 0;
   }
   ```
   
   
   
   
   
3. >Schrijf een C-programma **writestring**.c dat het **proces-ID** naar het **scherm** schrijft gevolgd
      >door de **string** die als **enige parameter** wordt meegegeven en vervolgens **10 seconden**
      >**wacht** vooraleer te eindigen.
      >
      >**echo $$** om pid op te vragen van huidige terminal.
      >
      >```C
      >#lnclude <stdio.h> 
      >#include <unistd.h> 
      >int main(int argc, char**argv){
      >    if (argc!=2){ 
      >        fprintf(stderr,"Usage writestring string\n"); 
      >        return 1;
      >    }
      >	printf("ppid=%d pid=%d argv[1]=%s\n",getppid(),getpid(),argv[1]); 
      >    sleep(10); //process wissel verplichten
      >    return 0; 
      >}
      >```
      >
      >1. Herschrijf nu opdracht 2 waarbij het kindproces de systeemaanroep **execv**
      >     gebruikt om “writestring hello” uit te voeren.
      >     Opgelet: In het ouderproces moet je wachten tot wanneer het kindproces klaar is,
      >     waarna je nog een boodschap naar het scherm schrijft. Dit doe je door gebruik te
      >     maken van de systeemaanroep waitid of waitpid.
      >
      >   ```c
      >   #include <unistd.h> 
      >   #include <fcntl.h> 
      >   #include <sys/wait. h> 
      >   #include <sys/stat.h> 
      >   #include <stdio.h> 
      >   #include <stdlib.h>
      >   
      >   
      >   int main(int argc, char *argv[] {
      >       int pid=fork();
      >       if(pid==0){
      >           char *args[]={"writestring","writestring hello",(char*)0); 
      >   		if(execv("writestring",args) <0){
      >               perror("writestring");
      >               exit(1);
      >           }
      >   		return 0; 
      >       }
      >       waitpid(pid,NULL,0);
      >   	return 0; 
      >   }
      >   ```
      >
      >2.  Idem als deel 1 maar maak nu gebruik van de systeemaanroep **execl**. De laatste
      >     C-string-parameter moet (char *)0 zijn om het einde van de opsomming aan te
      >     geven. Bemerk dat gewoon 0 schrijven niet voldoende is en zelfs fout is. Wanneer
      >     de grootte van een int verschillend is van de grootte van een char *, zal het aantal
      >     argumenten dat doorgegeven wordt aan execl verkeerd zijn.
      >
      >   ```c
      >   #include <unistd.h> 
      >   #include <fcntl.h> 
      >   #include <sys/wait. h> 
      >   #include <sys/stat.h> 
      >   #include <stdio.h> 
      >   #include <stdlib.h>
      >   
      >   
      >   int main(int argc, char *argv[] {
      >       int pid=fork();
      >       if(pid==0){
      >       	if(execl("writestring","writestring","writestring hello",(char*)0)<0){
      >       	  	perror("writestring");
      >       	  	exit(1);
      >       	}
      >       	return 0; 
      >       }
      >       waitpid(pid,NULL,0);
      >   	return 0; 
      >   }
      >   ```



4. >Schrijf een C++-programma met als naam **watchfiled.cc** dat alle bestanden in de gaten
   >houdt die opgesomd zijn in het tekstbestand watchfile.txt. Telkens wanneer een
   >opgesomd bestand in het tekstbestand wordt gewijzigd, wordt een boodschap naar het
   >scherm geschreven. Het C++-programma loopt in een oneindige lus die telkens het
   >bestand watchfile.txt lijn per lijn inleest en nagaat of het bestand dat zich op een
   >gegeven lijn bevindt reeds in de gaten wordt gehouden. Wanneer dit niet zo is wordt een
   >kindproces aangemaakt dat watchfile (zie Sectie V, opdracht 7) uitvoert op het “nieuwe”
   >bestand.

   ```bash
   #niet te kennen "Dat zijn C++ vragen. Dat ga ik u niet aandoen." ~ Wim
   ```

5. >Pas **watchfiled.cc aan** zodat nu ook rekening wordt gehouden met kindprocessen die
   >beëindigd worden. Een kindproces voert watchfile uit en zal beëindigd worden wanneer
   >het bestand bv. verwijderd of verplaatst wordt. De bedoeling is ook dat de
   >bestandsnaam van het verwijderde/verplaatste bestand in watchfile.txt wordt
   >verwijderd. Controleren of een proces gestopt is, kan met de systeemaanroep waitpid.
   >Bekijk hoe je waitpid kan gebruiken in non-blocking mode ttz. zonder dat de uitvoering
   >wordt gepauzeerd.
   >Wanneer een gebruiker een bestand in watchfile.txt verwijdert zou je eigenlijk het
   >bijhorend kindproces moeten stoppen. Dit hoef je niet te implementeren.

   ```bash
   #niet te kennen "Dat zijn C++ vragen. Dat ga ik u niet aandoen." ~ Wim
   ```

6. >Pas de gegeven code aan zodat het ouderproces het grootste van de gegeneerde
      >getallen bepaalt en vervolgens ieder kindproces op de hoogte brengt wie de winnaar is,
      >ttz. welk proces het grootste getal heeft gegenereerd. De uitvoer met zes kindprocessen ziet er als volgt uit:
      
      (**Labo 11 minuut 30: Examenvraag vorige jaren**)
      
      
      
      ```
      Process 1819 is the winner
      I'm the winner!
      Process 1819 is the winner
      Process 1819 is the winner
      Process 1819 is the winner
      Process 1819 is the winner
      ```
      
      ```c
      #include <unistd.h>
      #include <fcntl.h>
      #include <sys/wait.h>
      #include <sys/stat.h>
      #include <stdio.h>
      #include <stdlib.h>
      #include <time.h>
      
      #define N 6
      
      typedef struct
      {
          int pid;
          int getal;
          int fd_PC[2];
          int fd_CP[2];
      } data;
      
      int main(int argc, char *argv[])
      {
      
          data d[N];
      
          for (int i = 0; i < N; i++)
          { // 6 forks
              if (pipe(d[i].fd_CP) < 0)
              {
                  perror(argv[0]);
                  exit(1);
              }
              if (pipe(d[i].fd_PC) < 0)
              {
                  perror(argv[0]);
                  exit(1);
              }
              d[i].pid = fork();
              if (d[i].pid == 0)
              {
                  close(d[i].fd_CP[0]); // file descriptor sluiten die niet meer gebruikt wordt.
                  close(d[i].fd_PC[1]);
                  srand(getpid());
                  int getal = rand();
                  printf("Child send %d to parent\n", getal);
                  write(d[i].fd_CP[1], &getal, sizeof(int)); // deblokkeert Parent
                  close(d[i].fd_CP[1]);
                  read(d[i].fd_PC[0], &getal, sizeof(int)); // blokkeert Child
                  close(d[i].fd_PC[0]);
                  //printf("Child received %d from parent\n", getal);
                  if (getal == getpid())
                  {
                      printf("Im the winner \n");
                  }
                  else
                  {
                      printf("Process %d is the winner \n", getal);
                  }
                  return 0;
              }
              close(d[i].fd_CP[1]);
              close(d[i].fd_PC[0]);
          }
      
          for (int i = 0; i < N; i++)
          {                                                  // 6 forks
              read(d[i].fd_CP[0], &d[i].getal, sizeof(int)); // blokkeert Parent
              close(d[i].fd_CP[0]);
             //printf("Parent received %d from child %d \n", d[i].getal, d[i].pid);
          }
      
          int index = 0;
          for (int i = 0; i < N; i++)
          {
              if (d[i].getal > d[index].getal) // grootste zoeken
              {
                  index = i;
              }
          }
      
          for (int i = 0; i < N; i++)
          {
              //printf("Parent send %d from child %d \n", index, d[i].pid);
              write(d[i].fd_PC[1], &d[i].pid, sizeof(int)); // deblokkeert Child
              close(d[i].fd_PC[1]);
          }
      
          for (int i = 0; i < N; i++)
          {
              waitpid(d[i].pid, NULL, 0); // vanaf er een fork() is, is er een waitpid nodig.
          }
          return 0;
      }
      ```
      
      
      
      **3 versies: 1 met veel semaforen, 1 met een tabel van datastructuren ipv datastructuur van tabellen & 1 met 2 semafore ipv n * 2 semaforen.**
      
      
      
      **6a**
      
      ```c
      #include <sys/mman.h>
      #include <unistd.h>
      #include <stdio.h>
      #include <pthread.h>
      #include <semaphore.h>
      #include <sys/types.h>
      #include <fcntl.h>
      #include <string.h>
      #include <sys/wait.h>
      #include <sys/stat.h>
      #include <stdlib.h>
      
      #define N 1000
      
      typedef struct {
      	int pids[N];
      	int numbers[N];
      	int winner;
      	sem_t sem_PC[N];
      	sem_t sem_CP[N];
      } data;
      
      int main(int argc, char **argv){
      	data * d=mmap(NULL,sizeof(data),PROT_READ|PROT_WRITE,MAP_SHARED|MAP_ANONYMOUS,-1,0);
      	if (d==MAP_FAILED){
      		perror(argv[0]);
      		exit(1);
      	}
      	for(int i=0;i<N;i++){
      		sem_init(&(d->sem_PC[i]),1,0);
      		sem_init(&(d->sem_CP[i]),1,0);
      		int pid=fork();
      		if (pid==0){
      			//CHILD
      			srand(getpid());
      			d->numbers[i]=rand();
      			sem_post(&(d->sem_CP[i])); //teken geven dat d is ingesteld.
      			sem_wait(&(d->sem_PC[i])); //wachten op signaal van parent om door te gaan.
      			if (d->winner==getpid()){
      				printf("I'm the winner...\n");
      			}
      			else {
      				printf("Process %d is the winner\n",d->winner);
      			}
      			return 0;
      		}
      		d->pids[i]=pid;
      	}
      
      	for(int i=0;i<N;i++){
      		sem_wait(&(d->sem_CP[i])); //wachten op signaal van child om door te gaan
      	}
      
      	int index=0;
      	for(int i=1;i<N;i++){
      		if (d->numbers[i]>d->numbers[index])
      			index=i;
      	}
      	
      	d->winner=d->pids[index];
      
      	for(int i=0;i<N;i++){
      		sem_post(&(d->sem_PC[i])); //signaal geven naar child dat winnaar bekend is.
      	}
      
      
      
      	for(int i=0;i<N;i++){
      		waitpid(d->pids[i],NULL,0);
      	}
      	
      	for(int i=0;i<N;i++){
      		sem_destroy(&(d->sem_CP[i]));
      		sem_destroy(&(d->sem_PC[i]));
      	}
      
      	if (munmap(d,sizeof(data))<0){
      		perror(argv[0]);
      		exit(1);
      	}
      }
      ```
      
      
      
      
      
      
      
      **6b**
      
      ```C
      #include <unistd.h>
      #include <fcntl.h>
      #include <sys/mman.h>
      #include <sys/stat.h>
      #include <sys/wait.h>
      #include <stdio.h>
      #include <stdlib.h>
      #include <string.h>
      #include <pthread.h>
      #include <semaphore.h>
      
      #define N 6
      
      typedef struct {
      	int numbers;
      	int winner;
      	sem_t sem_PC;
      	sem_t sem_CP;	
      } data;
      
      int main(int argc, char **argv){
      	
      	data* d=mmap(NULL,sizeof(data)*N,PROT_READ|PROT_WRITE,MAP_SHARED|MAP_ANONYMOUS,-1,0);
      	int pids[N];
      	if (d==MAP_FAILED){
      		perror(argv[0]);
      		exit(1);
      	}
      	
      	for(int i=0;i<N;i++){
      		sem_init(&(d[i].sem_PC),1,0);
      		sem_init(&(d[i].sem_CP),1,0);
      		pids[i]=fork();
      		if (pids[i]==0){
      			//CHILD
      			srand(getpid());
      			d[i].numbers=rand();
      			sem_post(&(d[i].sem_CP));
      			sem_wait(&(d[i].sem_PC));
      			if (d[i].winner==getpid()){
      				printf("I'm the winner\n");
      			}
      			else {
      				printf("Proces %d is the winner\n",d[i].winner);
      			}	
      			return 0;
      		}
      	}
      	for(int i=0;i<N;i++){
      		sem_wait(&(d[i].sem_CP));
      	}
      	for(int i=0;i<N;i++){
      		printf("Child %d produced %d \n",pids[i],d[i].numbers);
      	}
      	int index=0;
      	for(int i=0;i<N;i++){
      		if (d[i].numbers>d[index].numbers) 
      			index=i;
      	}
      
      	for(int i=0;i<N;i++){
      		d[i].winner=pids[index];
      		sem_post(&(d[i].sem_PC));
      	}
      
      	for(int i=0;i<N;i++){
      		waitpid(pids[i],NULL,0);
      	}
      	for(int i=0;i<N;i++){
      		sem_destroy(&(d[i].sem_PC));
      		sem_destroy(&(d[i].sem_CP));
      	}
      
      	if (munmap(d,sizeof(data)*N)<0){
      		perror(argv[0]);
      		exit(1);
      	}
      	return 0;
      }	
      	
      ```
      
      **6c**
      
      ```bash
      #include <sys/mman.h>
      #include <unistd.h>
      #include <stdio.h>
      #include <pthread.h>
      #include <semaphore.h>
      #include <sys/types.h>
      #include <fcntl.h>
      #include <string.h>
      #include <sys/wait.h>
      #include <sys/stat.h>
      #include <stdlib.h>
      
      #define N 10
      
      typedef struct {
      	int pids[N];
      	int numbers[N];
      	int winner;
      	sem_t sem_PC;
      	sem_t sem_CP;
      } data;
      
      int main(int argc, char **argv){
      	data * d=mmap(NULL,sizeof(data),PROT_READ|PROT_WRITE,MAP_SHARED|MAP_ANONYMOUS,-1,0);
      	if (d==MAP_FAILED){
      		perror(argv[0]);
      		exit(1);
      	}
      	sem_init(&(d->sem_CP),1,0);
      	sem_init(&(d->sem_PC),1,0);
      	for(int i=0;i<N;i++){
      		int pid=fork();
      		if (pid==0){
      			//CHILD
      			srand(getpid());
      			d->numbers[i]=rand();
      			sem_post(&(d->sem_CP));
      			sem_wait(&(d->sem_PC));
      			if (d->winner==getpid()){
      				printf("I'm the winner...\n");
      			}
      			else {
      				printf("Process %d is the winner\n",d->winner);
      			}
      			return 0;
      		}
      		d->pids[i]=pid;
      	}
      	int v;
      	sem_getvalue(&(d->sem_CP),&v);
      	while(v!=N){
      		sem_getvalue(&(d->sem_CP),&v);
      	}
      
      	int index=0;
      	for(int i=1;i<N;i++){
      		if (d->numbers[i]>d->numbers[index])
      			index=i;
      	}
      	
      	d->winner=d->pids[index];
      
      	for(int i=0;i<N;i++){
      		sem_post(&(d->sem_PC));
      	}
      
      
      
      	for(int i=0;i<N;i++){
      		waitpid(d->pids[i],NULL,0);
      	}
      	
      	for(int i=0;i<N;i++){
      		sem_destroy(&(d->sem_CP));
      		sem_destroy(&(d->sem_PC));
      	}
      
      	if (munmap(d,sizeof(data))<0){
      		perror(argv[0]);
      		exit(1);
      	}
      }
      ```
      
      **6d**
      
      ```C
      #include <unistd.h>
      #include <sys/wait.h>
      #include <sys/stat.h>
      #include <fcntl.h>
      #include <stdio.h>
      #include <stdlib.h>
      #include <string.h>
      #include <time.h>
      #include <sys/mman.h>
      #include <semaphore.h>
      #include <pthread.h>
      
      #define N 6
      
      typedef struct {
      	int number;
      	sem_t sem_CP;
      	int winner;
      } data ;
      
      int main (int argc, char **argv){
      	int pids[N];
      	data * d=mmap(NULL,sizeof(data)*N,PROT_READ|PROT_WRITE,MAP_SHARED|MAP_ANONYMOUS,-1,0);
      	
      
      	if (d==MAP_FAILED){
      		perror(argv[0]);
      		exit(1);
      	}
      	sem_t *sem_PC=mmap(NULL,sizeof(sem_t),PROT_READ|PROT_WRITE,MAP_SHARED|MAP_ANONYMOUS,-1,0);
      	
      	if (sem_PC==MAP_FAILED){
      		perror(argv[0]);
      		exit(1);
      	}
      	sem_init(sem_PC,1,0);
      	
      	for(int i=0;i<N;i++){
      		sem_init(&d[i].sem_CP,1,0);
      		pids[i]=fork();
      
      		if (pids[i]==0){
      			srand(getpid());
      			d[i].number=rand();
      			printf("Process %d generated %d\n",getpid(),d[i].number);
      			sem_post(&d[i].sem_CP);
      			sem_wait(sem_PC);
      			if (getpid()==d[i].winner){
      				printf("I'm the winner\n");
      			}
      			else {
      				printf("Process %d is the winner\n",d[i].winner);
      			}
      			return 0;
      		}
      	}
      	for(int i=0;i<N;i++){
      		sem_wait(&d[i].sem_CP);
      	}
      	int index=0;
      	for (int i=0;i<N;i++){
      		if (d[i].number>d[index].number) 
      			index=i;
      	}	
      	
      	for(int i=0;i<N;i++){
      		d[i].winner=pids[index];
      	}
      	
      	for(int i=0;i<N;i++){
      		sem_post(sem_PC);
      	}
      
      	for(int i=0;i<N;i++){
      		//printf("waiting for process %d to finish\n",pids[i]);
      		waitpid(pids[i],NULL,0);
      	}
      	
      	for(int i=0;i<N;i++){
      		sem_destroy(&d[i].sem_CP);
      	}
      	sem_destroy(sem_PC);
      	
      	if (munmap(d,sizeof(data)*N)<0){
      		perror(argv[0]);
      		exit(1);
      	}
      
      
      	return 0;
      }
      ```
      
      
      
      #### Posix threads (pthreads)
      
      >De POSIX Pthreads standaard is de de-facto **standaard** voor het **programmeren** van
      >**multithreaded programma’s** in een POSIX-compatibele omgeving. Deze standaard
      >specificeert de **interface** om **threads** te **creëren** en te **manipuleren**. Als bibliotheek zijn
      >pthreads op de meeste platformen beschikbaar. De voornaamste primitieven zijn het
      >opstarten van een thread(**pthread_create**) en het wachten op een thread(**pthread_join**). De
      >standaard is vanzelfsprekend veel ruimer dan bovenvermelde functies.
      >Voor onderstaande opdrachten zijn de functies pthread_create en pthread_join van groot
      >belang. De syntax van beide functies kan je hieronder vinden:
      >**int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine)**
      >**(void *), void *arg);**
      >
      >**int pthread_join(pthread_t thread, void**** **retval);**

**Opdrachten**



1. >Schrijf een programma dat gebruikmaakt van **vier threads** die elk een verschillend cijfer
   >naar het scherm schrijven. Wanneer een thread het bijhorend cijfer 100 keer naar het
   >scherm heeft geschreven, stopt de thread.

   ```C
   #include <sys/mman.h>
   #include <unistd.h>
   #include <stdio.h>
   #include <pthread.h>
   #include <semaphore.h>
   #include <sys/types.h>
   #include <fcntl.h>
   #include <string.h>
   #include <sys/wait.h>
   #include <sys/stat.h>
   #include <stdlib.h>
   
   typedef struct
   {
       int getal;
       void (*f)(int);
   } arg;
   
   void *worker(void *p)
   {
       arg *a = (arg *)p;
       a->f(a->getal);
       return NULL;
   }
   
   void printgetal(int g)
   {
       int i;
       for (i = 0; i < 100; i++)
       {
           printf("%d", g);
       }
   }
   
   int main(int argc, char **argv)
   {
       pthread_t threads[4];
       int getallen[4];
       for (int i = 0; i < 4; i++)
       {
           arg args[4];
           args[i].getal = i; //per thread een nieuw getal.
           args[i].f = printgetal;
           printf("creating thread %d", i);
           pthread_create(&threads[i], NULL, worker, &args[i]);
       }
   
       for (int i = 0; i < 4; i++)
       {
           pthread_join(threads[i], NULL);
       }
   
       return 0;
   }
   ```
   
   
   
2. > **Genereer 1.000.000 willekeurige reële getallen** die je bijhoudt in een **tabel**. Schijf nu
   > twee functies die zoeken naar respectievelijk het **kleinste getal** en **het grootste getal** en
   > deze getallen als **return-waarde** teruggeven. Schrijf nu een hoofdprogramma dat
   > **gelijktijdig zoekt** naar het **grootste** en het **kleinste** getal in een tabel van 1.000.000 reële
   > getallen. Schrijf beide getallen naar het scherm.

   **Extra uitleg workers: Les8 01:03**
   
   ````C
   #include <pthread.h>
   #include <stdio.h>
   #include <stdlib.h>
   
   
   typedef struct { 							//parameters van de worker
   	double *array;
   	int n;
   	double (*f)(double*, int);
   } arg;
   
   double grootste (double *array, int n){
   	double grootste = array[0]
   	int i;
   	for(i = 1; i < n; i++){
   		if(array[i] > grootste){
   			grootste = array[i];
   		}
   	}
   	return grootste;
   }
   double kleinste(double *array, int n){
   	double kleinste = array[0]
   	int i;
   	for(i = 1; i < n; i++){
   		if(array[i] < kleinste ){
   			kleinste = array[i];
   		}
   	}
   	return kleinste ;
   }
   
   void * worker (void * p){
   	arg *a = (arg*)a;
   	//prinf is de easy oplossing het moet dus anders
   	//printf("%f", a->f(a->array, a->n));
   
   	//dus doe het zo met malloc
   	double *returnwaarde = malloc(sizeof(double));
   	*returnwaarde = a->f(a->array, a->n);
   	return (void*) returnwaarde ; 
   }
   
   void vulop (double * array, int n){
   	int i;
   	for(i = 0; i < n; i++){
   		array[i] = i;
   	}
   }
   
   int main(){
   	double array[1000000];
   	pthread_t tread_kleinse, thread_hoogste;
   
   	vulop(array,1000000);
   	arg arg_kl, arg_gr;
   	
   	arg_kl.array = array;
   	arg_kl.n = 1000000;
   	arg_kl.f = kleinste;
   	
   	arg_gr.array = array;
   	arg_gr.n = 1000000;
   	arg_gr.f = grootste;
   	pthread_create(&thread_kl, NULL, worker,(void*)&arg_kl);
   	pthread_create(&thread_hoogste, NULL, worker,(void*)&arg_gr);
   
   	//lees de returnwaarde
   	double *g,*k;	
   
   	pthread_join(thread_kl, (void**) &k);
   	pthread_join(thread_gr, (void**) &g);
   	printf("grootste %d" , *g);
   	printf("kleinste %d" , *k);
   	
   	free(g);
   	free(k);
   	return 0;
   }
   ````
   
   
   
3. >Multithreading kan ook leiden tot snelheidswinst. Een mooi voorbeeld hiervan is bv. een
      >**matrixvermenigvuldiging**. Om de snelheidswinst op te merken maak je best gebruik van
      >twee vierkante matrices met **1000 rijen** en **1000 kolommen**. Ook gebruik je best vier tot
      >acht threads om de het resultaat te berekenen. Gebruik voor de dimensie en ook voor
      >het aantal threads constanten.
      >Wanneer er bijvoorbeeld acht threads worden gebruikt, kan je het resultaat als volgt
      >berekenen. De eerste thread laat je de 0de, de 8ste, de 16de, ... rij van het resultaat
      >bepalen. De tweede thread ontfermt zich over de 1ste, 9de, 17de, ... rij van het resultaat.
      >Iedere thread berekent dus DIM/8 rijen van het eindresultaat waarbij de rijen op een
      >afstand van het aantal threads van elkaar liggen.
      >Om het opvullen van een matrix vlot te laten verlopen, geef je het element op ide rij en
      >op de jde kolom de waarde i+j. Dit kan eenvoudig worden geprogrammeerd a.d.h.v. een
      >dubbele for-lus. Doe dit voor beide matrices en merk op dat je dus identieke matrices
      >met elkaar vermenigvuldigt.
      >Schrijf ook een programma dat geen Pthreads gebruikt om duidelijk het verschil in
      >snelheid te zien.
      
      ```c
      int matrix[2][2]; // {{1,2},{3,4}};
      int fucntie(int ** matrix) //werkt niet
      int functie( int (* matrix)[2]) //klopt wel
      ```
      
      
      
      ```c
      #include <pthread.h>
      #include <unistd.h>
      #include <stdio.h>
      #include <stdlib.h>
      
      #define N 2000
      
      int A[N][N];
      int B[N][N];
      int C[N][N];
      
      typedef struct {
      	int startrij;
      	int (*a)[N];
      	int (*b)[N];
      	int (*c)[N];
      	void (*f)(int, int (*)[N],int (*)[N],int (*)[N]);
      } arg;
      
      void vermenigvuldig(int startrij, int (*a)[N],int (*b)[N],int (*c)[N]){
      	int i,j,k;
      	for(i=startrij;i<N;i+=6){
      		for (j=0;j<N;j++){
      			int som=0;
      			for(k=0;k<N;k++){
      				som+=a[i][k]*b[k][j];
      			}
      			c[i][j]=som;
      		}
      	}
      }
      
      void *worker(void *p){
      	arg *a=(arg*)p;
      	a->f(a->startrij, a->a,a->b,a->c);
      	return NULL;
      }
      
      
      void schrijf_matrix (int (*m)[N]){
      	int i,j;
      	for(i=0;i<N;i++){
      		for(j=0;j<N;j++){
      			printf("%d ",m[i][j]);
      		}
      		printf("\n");
      	}
      }
      
      void maak_matrix(int (*m)[N]){
      	int i,j;
      	int teller=1;
      	for(i=0;i<N;i++){
      		for(j=0;j<N;j++){
      			m[i][j]=teller++;
      		}
      	}
      }
      
      int main(){
      	pthread_t threads[6];
      	arg args[6];	
      	maak_matrix(A);
      	maak_matrix(B);
      	int i;
      	for (i=0;i<6;i++){
      		args[i].startrij=i;
      		args[i].a=A;
      		args[i].b=B;
      		args[i].c=C;
      		args[i].f=vermenigvuldig;
      		pthread_create(&threads[i],NULL,worker,(void*)&args[i]);
      	}
      	for(i=0;i<6;i++){
      		pthread_join(threads[i],NULL);
      	}
      	schrijf_matrix(C);
      	return 0;
      }	
      
      ```
      
      4. >Omdat iedere aangemaakte thread beschikt over zijn eigen stapel, kunnen ook
         >recursieve functies parallel worden uitgevoerd. 
      
         ```bash
         #Valt weg want nog geen sorteren gezien
         ```
      
         

**Thread synchronisatie**

>Bovenstaande opdrachten hebben één ding gemeenschappelijk, nl. iedere thread loopt
>onafhankelijk van de andere threads. Sommige toepassingen vergen echter dat threads
>onderling moeten kunnen samenwerken en eventueel gebruik moeten maken van dezelfde
>gedeelde bronnen. Soms kan het ook gebeuren dat een bepaald stuk code maar door één
>thread tegelijkertijd mag uitgevoerd worden, een zogenaamde kritische sectie. Om dit te
>kunnen doen bestaan er Mutexen en Semaforen. Het verschil tussen beide is dat mutexen
>een gedeelde bron beschermen en dus fungeren als vergrendelingsmechanisme daar waar
>semaforen dienst doen als signaleringsmechanisme. Doordat semaforen gebruikmaken van
>berichten/signalen, is het gebruik ervan dus veel algemener dan dat van mutexen.



**Gebruik van mutexen**



**Gebruik van POSIX semaforen**



> Er worden twee soorten semaforen onderscheiden, nl. unnamed en named semaforen. Net
> zoals named pipes worden named semaforen gebruikt voor IPC tussen niet gerelateerde
> processen. Voor communicatie tussen threads en gerelateerde processen volstaan unnamed
> semaforen. Wanneer semaforen worden gebruikt voor IPC tussen gerelateerde processen,
> moeten ze worden bijgehouden in een gedeelde virtuele geheugenpagina die kan worden
> aangevraagd via de systeemaanroep mmap. Tussen threads volstaat het wanneer unnamed
> semaforen globaal worden gedeclareerd of op de heap worden geplaatst.
> Een semafoor initialiseren gebeurt via:

```c
#include <semaphore.h>
int sem_init(sem_t *sem, int pshared, unsigned int value);
```

>**pshared** is 0 wanneer de semafoor gedeeld wordt onder threads en is verschillend van nul
>wanneer het gaat om een semafoor die gedeeld wordt onder gerelateerde processen. Dit
>argument geeft onrechtstreeks ook aan waar de semafoor *sem resideert. Bij threads
>volstaat het om een semafoor globaal te declareren of via malloc aan te maken op de heap.
>Voor processen daarentegen moet er gebruikgemaakt worden van een pagina in de virtuele
>adresruimte (zie later).
>
>De werking van een semafoor is vrij eenvoudig. Bij initialisatie wordt aan de semafoor een
>waarde toegekend die niet negatief mag worden. Wanneer een proces of een thread een
>semafoor tegenkomt die een negatieve waarde heeft, wordt de uitvoering stopgezet tot
>wanneer de waarde terug positief wordt. De onderstaande operaties zullen de waarde van
>de semafoor *sem respectievelijk decrementeren en incrementeren.

```c
int sem_wait(sem_t *sem);
int sem_post(sem_t *sem);
```

>Wanneer een semafoor een waarde heeft die gelijk is aan 0, zal de functie sem_wait() de
>uitvoering van de actieve thread of het actieve proces blokkeren tot wanneer de waarde
>strikt positief wordt. In dat geval wordt de waarde van de semafoor door de functie
>sem_wait() gedrecrementeerd.
>Bij een aanroep van de sem_post() functie wordt de waarde van de semafoor
>geïncrementeerd en wordt het proces of de thread die momenteel aan het wachten is
>geactiveerd. Indien er meerdere processen of threads wachtende zijn, bepaalt de scheduler
>welk proces of welke thread de uitvoering mag verderzetten.
>Een unnamed semafoor wordt vernietigd door de onderstaande functie:

```c
int sem_destroy(sem_t *sem);
```

>Een **semafoor** moet worden vernietigd vooraleer dat het geheugen waarin hij resideert
>wordt vrijgegeven. Dit gebeurt bv. wanneer een functie waarin de semafoor werd
>aangemaakt, terugkeert naar de oproepende instantie. Bij het gebruik van een gedeelde
>virtuele geheugenpagina tussen processen, moet de semafoor vernietigd worden wanneer
>er geen enkel proces nog gebruik van maakt en vooraleer het geheugen via de
>systeemaanroep munmap terug wordt vrijgegeven.

**Opdrachten**

1. >Schrijf een programma dat gebruikmaakt van 8 threads voor de verkoop van tickets. Het
   >totaal aantal tickets wordt bijgehouden in een globale variabele waar iedere thread
   >automatisch toegang tot heeft. Iedere thread voert dezelfde functie uit, nl. een functie
   >die door een oneindige lus loopt waar telkens één ticket verkocht wordt. Van zodra alle
   >tickets de deur uit zijn, rapporteert iedere thread het totale aantal tickets dat hij
   >verkocht heeft. Om threadwissels te verzekeren plaats je in de oneindige lus de opdracht
   >sleep(rand()%3) die een delay van 0, 1 of 2 seconden veroorzaakt. Maak gebruik van een
   >mutex om de gedeelde bron, i.e. de globale variabele te beschermen. Bekijk ook wat er
   >gebeurt wanneer de gedeelde bron niet wordt vergrendeld.

   ```bash
   ```

2. >Herneem opdracht 1 maar maak nu gebruik van semaforen om de gedeelde bron te
      >beschermen. Aangezien er maar twee toestanden mogelijk zijn, spreekt men hier van
      >een binaire semafoor.

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   #include <sys/stat.h>
   #include <pthread.h>
   #include <sys/types.h>
   #include <sys/wait.h>
   #include <fcntl.h>
   #include <pthread.h>
   #include <semaphore.h>
   #include <unistd.h>
   
   #define N 10
   
   int tickets=100;
   
   sem_t sem;
   
   
   void* worker(void* p){
   	int verder=1;
   	while (verder){
   		sem_wait(&sem);
   		if (tickets>0) {
   			sleep(rand()%3);
   			tickets--;
   			printf("%d sold 1 ticket\n", gettid());
   		}
   		else verder=0;
   		sem_post(&sem);
   	}
   	return NULL;
   }
   
   int main(){
   	sem_init(&sem,0,1);
   	pthread_t threads[N];
   	int i;
   	for(i=0;i<N;i++){
   		pthread_create(&threads[i],NULL,worker,NULL);
   	}
   	for(i=0;i<N;i++){
   		pthread_join(threads[i],NULL);
   	}
   	sem_destroy(&sem);
   	return 0;
   }
   ```

   **Gebruik van shared memory en memory mapped I/O**
   
   > IPC kan gebeuren d.m.v. pipes, semaforen of shared memory. Om in de virtuele adresruimte
   > van een proces een geheugenmapping aan te maken, wordt gebruikgemaakt van de
   > syteemaanroep mmap.
   
   ```c
   #include <sys/mman.h>
   void *mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);
   int munmap(void *addr, size_t length);
   ```
   
   >De parameter addr is het adres in de virtuele adresruimte waar je de mapping wil plaatsen.
   >Het is aangewezen om als waarde van addr NULL te kiezen waardoor de kernel een geschikt
   >adres zal zoeken voor de gevraagde mapping.
   >De length-parameter is de grootte van de mapping in bytes. Doorgaans zal de kernel dit
   >afronden naar een veelvoud van de paginagrootte (cfr. de return-waarde van
   >sysconf(_SC_PAGESIZE)).
   >Het prot-argument geeft aan welke toegangsrechten er aan de geheugenmapping gekoppeld
   >zullen worden. Mogelijke waarden zijn PROT_NONE, PROT_READ, PROT_WRITE en
   >PROT_EXEC. Bij PROT_NONE is er geen toegang tot de geheugenruimte, bij PROT_READ mag
   >de inhoud gelezen worden, bij PROT_WRITE mag de inhoud gewijzigd worden en tot slot
   >mag bij PROT_EXEC de inhoud uitgevoerd worden.
   
   >De flags-parameter is doorgaans één van onderstaande:
   MAP_PRIVATE
   Maakt een private geheugenmapping aan waarbij eventuele aanpassingen
   onzichtbaar zullen zijn voor andere processen die van dezelfde mapping
   gebruikmaken. Bij een bestandsmapping zullen aanpassingen niet naar het
   onderliggend bestand geschreven worden.
   MAP_SHARED
   Maakt een gedeelde mapping aan. Aanpassingen zullen zichtbaar zijn bij andere
   processen die van dezelfde mapping gebruikmaken. Bij een bestandsmapping zullen
   de aanpassingen naar het onderliggende bestand geschreven worden. Deze zullen
   echter niet onmiddellijk naar het bestandssysteen worden geschreven maar op een
   moment waarop de kernel dit het meest opportuun acht.
   De fd-parameter is de file descriptor die aan de geheugenmapping gekoppeld moet worden.
   
   > Zoals de naam doet vermoeden is de offset-parameter het startpunt van de mapping in het
   > bestand. Wanneer voor de offset de waarde 0 gekozen wordt en als length de grootte van
   > het bestand, wordt een volledige mapping van het bestand bekomen.
   > Mmap geeft bij succes het startadres van de geheugenmapping als return-waarde.
   > Munmap doet het tegenovergestelde van mmap en verwijdert de geheugenmapping
   
   **Bestandmappings**
   
   >Om een bestandsmapping te bekomen moet met de systeemaanroep open een file
   >descriptor gevraagd worden en moet deze vervolgens gebruikt worden bij de
   >systeemaanroep mmap. Na het uitvoeren van mmap mag de file descriptor met close
   >gesloten worden.
   >Het spreekt voor zich dat de toegangsparameters bij het openen van de descriptor en bij de
   >mapping consistent moeten zijn. Het zou onlogisch zijn mocht je bij de mapping
   >PROT_WRITE vermelden, terwijl de fd-parameter bekomen werd met O_RDONLY.
   
   **Memory-mapped I/O**
   
   >Aangezien een bestand in het geheugen kan worden geladen, kunnen een aantal I/O-
   >operaties vervangen worden door geheugenoperaties. Dit heeft volgende voordelen:
   >
   >1. De systeemaanroepen read en write veroorzaken achter de schermen twee
   >     dataoverdrachten. De eerste tussen het bestand en de kernel buffer cache, een
   >     tweede tussen de kernel buffer cache en een buffer in user-space. De tweede
   >     overdracht wordt door gebruik te maken van geheugenmapping overbodig. Bij input
   >     is de data onmiddellijk na de mapping voorhanden en bij output worden de
   >     wijzigingen door de kernel, weliswaar niet ogenblikkelijk, naar het bestand
   >     weggeschreven.
   >2.  Zoals in punt 1 geschetst kan de er wat tijd bespaard worden door het aantal data-
   >     overdrachten te halveren. Bovendien is het ook zo dat er bij een read/write-operatie
   >     data zal bijgehouden worden in twee buffers, nl. één in de kernel en één in user-
   >     space. Bij een geheugenmapping is er enkel nog een buffer nodig in de kernel
   >     waardoor er dus ook op het geheugenverbruik kan bespaard worden.
   >     Performantiewinst is het meest waarschijnlijk bij random I/O-operaties in een groot bestand.
   >     Bij sequentiële toegang zal er weinig tot geen performantiewinst bekomen worden omdat
   >     bij beide technieken het volledige bestand één keer in het geheugen zal worden geladen.
   >     Hierdoor zal het uitsparen van een dataoverdracht en een beetje geheugen niet opwegen
   >     tegen de tijd die verloren gaat aan disk I/O.

**Let wel, het gebruik van virtueel geheugen heeft ook grote nadelen. Voor kleine I/O-
operaties is de kost van memory-mapped I/O aanzienlijk (mapping, unmapping,
paginafouten, aanpassen van de MMU TLB, ...)**



**Opdrachten**

1. >Schrijf een eigen versie van cat waarbij er nu gebruikgemaakt wordt van memory-
   >mapped I/O.

   ```c
   #include <stdio.h>
   #include <stdlib.h>
   #include <sys/stat.h>
   #include <pthread.h>
   #include <sys/types.h>
   #include <sys/wait.h>
   #include <fcntl.h>
   #include <pthread.h>
   #include <semaphore.h>
   #include <unistd.h>
   #include <sys/mman.h>
   
   int main(int argc, char **argv){
   	int fd=open(argv[1],O_RDONLY);
   	if (fd<0){
   		perror(argv[1]);
   		exit(1);
   	}
   	struct stat s;
   	if (fstat(fd,&s)<0){
   		perror(argv[1]);
   		exit(1);
   	}	
   	unsigned char *p=mmap(NULL,s.st_size,PROT_READ,MAP_PRIVATE,fd,0);
   	if (p<0){
   		perror(argv[1]);
   		exit(1);
   	}
   	if (close(fd)<0){ //fd sluiten want niet meer nodig
   		perror(argv[1]);
   		munmap(p,s.st_size); //mapping ondgedaan maken
   		exit(1);
   	}
   	unsigned char *hulp=p; //kopie nemen anders zal de munmap verkeerd pointen
   	int i=0;
   	int total=0;
   	unsigned buffer[BUFSIZ];
   	for(i=0;i<s.st_size-BUFSIZ;i+=BUFSIZ){
   		write(1,hulp,BUFSIZ);
   		total+=BUFSIZ;
   		hulp+=BUFSIZ;
   	}
   	write(1,hulp,s.st_size-total);
   	munmap(p,s.st_size);
   	return 0;
   }
   ```
   
   **Extra oefening uit theorie Les 9 (01:40): Oefening met pipes maar nu adhv semaforen en mmap. Zie Parent met 2 childs met pipes tussen (theorie les 7, 01:25)**
   
   ```C
   #include <stdio.h>
   #include <stdlib.h>
   #include <sys/stat.h>
   #include <pthread.h>
   #include <sys/types.h>
   #include <sys/wait.h>
   #include <fcntl.h>
   #include <pthread.h>
   #include <semaphore.h>
   #include <unistd.h>
   #include <sys/mman.h>
   #include <string.h>
   
   typedef struct {
   	int g;
   	int g2;
   	sem_t semP_C1; //3 semaforen
   	sem_t semC1_C2;
   	sem_t semP_C2;
   } data ;
   
   int main(int argc, char** argv){
   	data* d=mmap(NULL,sizeof(data),PROT_READ | PROT_WRITE, MAP_ANONYMOUS | MAP_SHARED,-1,0);
   	if (d<0){
   		perror(argv[0]);
   		exit(1);
   	}
   	sem_init(&(d->semP_C1),1,0);
   	sem_init(&(d->semC1_C2),1,0);
   	sem_init(&(d->semP_C2),1,0);
   	
   	int pid=fork();
   	if (pid==0){
   		//CHILD1
   		sem_wait(&(d->semP_C1)); //blokkeren
   		d->g*=2;
   		sem_post(&(d->semC1_C2)); //unlocken
   		return 0;
   	}
   	
   	int pid2=fork();
   	if (pid2==0){
   		//CHILD2
   		sem_wait(&(d->semP_C2));
   		sem_wait(&(d->semC1_C2));
   		printf("Het resultaat van g*2+g2 is %d\n",d->g+d->g2);
   		return 0;
   	}
   	
       //parent
   	printf("Geef g....:\n");
   	scanf("%d",&(d->g));
   	sem_post(&(d->semP_C1));
   	
   	printf("Geef g2....:\n");
   	scanf("%d",&(d->g2));
   	sem_post(&(d->semP_C2));
   
   	waitpid(pid,NULL,0); //wachten op child processen
   	waitpid(pid2,NULL,0);
   	sem_destroy(&(d->semP_C1)); //semaforen vernietigen
   	sem_destroy(&(d->semC1_C2));
   	sem_destroy(&(d->semP_C2));
   	
   	munmap(d,sizeof(data));
   	return 0;
   }
   
   
   ```
   
   
   
2. >**Interprocescommunicatie** m.b.v. **semaforen** kwam tot nu toe nog niet aan bod.
      >Schrijf een C-programma dat **200 kindprocessen** aanmaakt die elk een uniek getal
      >genereren. Het pid van het proces dat het grootste getal gegenereerd heeft, alsook
      >het getal zelf, wordt door alle kindprocessen naar het scherm geschreven. Om een
      >nieuw **shared memory** object te maken kan je de systeemaanroep **shm_open**
      >gebruiken. Deze aanroep geeft een getal terug dat je bij mmap kan gebruiken als file
      >descriptor. De initiële grootte van het shared memory object is 0. Om het shared
      >memory object een grootte te geven kan je de systeemaanroep ftruncate gebruiken.

   ```c
   ```



## Deel VII: Programmeren in Bash

### Patterns, expansions en het opzoeken van hulp

Zoals reeds eerder vermeld bevat de shell enkele honderden commando’s met elk nog tal
van command line options. Het is dan ook logisch dat wanneer je meer informatie zoekt over
een welbepaalde opdracht, je dit doet a.d.h.v. het commando man waarbij je de naam van
de opdracht meegeeft als parameter. Als extra parameter kan je ook nog het **sectienummer**
meegeven of de optie -a wanneer je alle man-pagina’s waar de naam die je als parameter
hebt opgegeven wil overlopen. 

Gebruik voor de onderstaande opdrachten de ingebouwde documentatiemogelijkheden om
op de vragen te antwoorden.

**Opdrachten**

1. > Met welk van de commando’s **cp, dd, ln, mktemp, touch** en **cat** kan je **vlug een aantal**
   > **(lege) bestanden aanmaken** waarvan de namen als parameters van het commando
   > worden opgegeven?

```bash
touch file1 file2 file3 file4
#cp & dd -> kopiëren & dd voor “convert and copy”
#ln -> files linken
#mktemp -> temp dir aanmaken
#touch -> bestand aanmaken
#cat -> bestand lezen
```

2. >Wat verschijnt er op het scherm indien je de opdracht head /etc/passwd uitvoert? Zoek
   >nu de verwante opdracht voor het tonen van de laatste lijnen van een bestand. Hoe kan
   >je steeds de laatste lijnen van een bestand op het scherm laten verschijnen wanneer er
   >een ander proces achteraan het bestand lijnen toevoegt?

```bash
head /etc/passwd #eerste (10) lijnen van het bestand
tail /etc/passwd #laaste (10) lijnen van het bestand
```

3. >Waarvoor dient de optie -rf bij de opdracht rm? Maak met een editor een bestand aan  
   >met als naam “-rf”. Hoe kan je het bestand “-rf“ verwijderen?

```bash
touch ./-rf #aanmaak
rm ./-rf -rf #verwijderen
of rm -- -rf (-- = einde opties) #verwijderen

-r = recursive
-f = force
-rf = combinatie
```

4. >Welke opties moet je toevoegen aan het commando wc om enkel de **grootte** van een bestand te tonen zonder extra informatie?

```bash
-c  of --bytes
```

5. >In Bash zijn er ook Bash-builtin opdrachten zoals **cd, set, pwd, exec, printf** en :  waarvoor  
   >er geen aparte man-pagina’s beschikbaar  zijn. Een overzicht kan je bekomen door man  
   >builtin of door de man-pagina van Bash op te vragen. Zoek informatie op over het  
   >gebruik van de opdrachten cd, set, pwd, exec, printf en :.

```bash	
-cd: change directory
-set: set shell & environment variables instellen
-pwd: print working directory
-exec: uitvoeren van bestand
-printf: printen van een string
-: true command, null command: lukt altijd. heeft geen effect.
```

6. > Wat doet het commando sync?

```bash
synchroniseert gecachete writes (schrijf opdrachten) naar storage om buffers leeg te maken.
```

7. >Hoe kan je met het commando dd een afbeelding maken van een USB-pen? Welke  
   >device-file heb je hiervoor nodig?  Bekijk de uitvoer van de opdracht “fdisk -l

```bash
-dd: converteert en kopieert bestand.
#Benodigde commando:

```
```bash
#uitvoer fdisk -l
[root@localhost c]# fdisk -l

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x9bbdd1fb

Device     Boot    Start      End  Sectors Size Id Type
/dev/sda1  *        2048  2099199  2097152   1G 83 Linux
/dev/sda2        2099200 37750783 35651584  17G 83 Linux
/dev/sda3       37750784 41943039  4192256   2G 82 Linux swap / Solaris


Disk /dev/zram0: 967 MiB, 1013972992 bytes, 247552 sectors
Units: sectors of 1 * 4096 = 4096 bytes
Sector size (logical/physical): 4096 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
```

8. >Hoe kan je met dd een kopie maken van de eerste 512 bytes van de vaste schijf? Bekijk  
   >met het commando strings  welke tekststrings in die 512 bytes verscholen zitten

```bash
head -c 512 /dev/sda < mbr.img
#of
dd if=/dev/sda of=mbr2.img bs=512 count=1

[root@localhost ~]# strings /dev/sda
```

9. >Gebruik het commando find om een lijst van bestanden te krijgen die de afgelopen 24u  
   >nog werden aangepast.

```bash
find / -type f -mtime 1
```

10. > Met het commando wodim kan je van op de opdrachtlijn  een CD/DVD-branden.  Met het  
    > commando **genisoimage** kan je een ISO-bestand aanmaken. Hoe kan je van de inhoud  
    > van de /root directory een ISO-bestand maken?

```bash
genisoimage [options] -o output.iso /root 
```

11. >Bij vraag 10 zal je merken dat de namen van de bestanden/directories werden gewijzigd.
    >Je kunt dit vermijden door de image in Joliet-formaat weg te schrijven.
    >**Naast reguliere expressies** kent Unix ook **patterns** om een verzameling strings te beschrijven.
    >De mogelijkheden van standaard patterns zijn veel **beperkter** dan bv. reguliere expressies en 
    >
    >worden gebruikt zowel in opdrachten als in shellscripts. In recente Bash-versies werden deze
    >patterns uitgebreid. Extended pattern matching kan worden aangezet met de opdracht
    >“shopt –s extglob”. Bij het uitvoeren van een commando met een pattern wordt eerst een lijst met
    >bestandsnamen gegenereerd die aan het opgegeven patroon voldoen. Dit wordt meestal
    >“**Pathname Expansion**” genoemd. Meer uitleg kan je vinden in de man-pagina van Bash
    >onder de rubriek “Pathname Expansion”.

    **Pathname Expansion:**

    - adhv Curly braces
    
    ```bash
    [root@localhost ~]# echo txt{1,2,3,4}
    txt1 txt2 txt3 txt4
    ```
    
    - adhv Wildcard
    
    ```bash
    [root@localhost ~]# ls /etc/l*.conf
    /etc/ld.so.conf     /etc/libuser.conf  /etc/logrotate.conf
    /etc/libaudit.conf  /etc/locale.conf
    ```
    
    
    
    **Maak voor onderstaande opdrachten de volgende lege bestanden aan: a, b, c, d, e, ab.c, a.b,**
    **b.a, b.c, c.d en d.e.**
    
12. >Voer de volgende opdrachten uit:
    >• dir a*.*
    >• dir a*
    >• dir *a
    >• dir a\*
    >Bemerk een belangrijk verschil met reguliere expressies. Bovendien wijkt de uitvoer af
    >van de uitvoer van dezelfde commando’s in Windows.

​		...

13. > Voorspel en controleer de uitvoer van de opdrachten:
    >
    > • printf “%s\n”[abcd]
    > • printf “%s\n” [!abcd]
    > • printf “%s\n” [^abcd]
    > • printf “%s\n” [a-d]
    > • printf “%s\n” [abcd]*[abcd]

    ...

14. > Voer de onderstaande commando’s uit.

    >• printf “%s\n” [a-e]
    >• printf “%s\n” [a/-e]
    >• printf “%s\n” [a\-e]
    >• printf “%s\n” [!\!]*

    >Wat is de bedoeling van het /-teken in deze opdrachten? Wat gebeurt er indien je het
    >verkeerde /-teken gebruikt?

    ```bash
    Het /-teken zorgt dat de string letterlijk geprint wordt en er dus geen pathname extension wordt toegepast.
    
    root@localhost oef12]# printf "%s\n" [a/-e]
    [a/-e]
    [root@localhost oef12]# printf "%s\n" [a-e]
    a
    b
    c
    d
    e
    ```

15. >Hoe kan je een lijst met bestandsnamen bekomen die precies uit één enkel karakter
    >bestaan?

    ```bash
    printf "%s\n" ?
    ```

16. >Vraag een lijst met bestandsnamen die uit precies twee karakters bestaan. Vergelijk de
    >uitvoer met die van de vorige opgave.

    ```bash
    $ printf "%s\n" ??
    ```

**notities** (labo2)

> iode: ls **-i** p /etc/passwd *//iode = metadata van bestand*
> ll: info van dir (of ls -d)

```bash
#2de kollom = aantal hard links naar zelfde file
[root@localhost besturingssystemen]# ll
total 64
-rw-r--r-- 1 root root    27 Mar  9 17:09 35.txt
-rwxr-xr-x 1 root root 25552 May 10 11:57 inlezen_buffer.a
-rw-r--r-- 1 root root   748 May 10 10:12 inlezen_buffer.c
-rw-r--r-- 1 root root     8 Mar  2 16:42 new.txt
drwxr-xr-x 2 root root  4096 May  9 17:30 opdrachten
-rw-r--r-- 1 root root 10000 May 10 09:31 output.txt
-rw-r--r-- 1 root root    24 Mar 23 16:21 scriptje.sh
-rw-r--r-- 1 root root   295 May 10 09:31 write_file.c
```

> hard link (**ln**) : connecteerd bestanden aan elkaar: data up to date. = nieuwe iode aanmaken met verwijzing er naar. bv: 

```bash
ln a b #hard link tussen bestand a en b
```

> hard link naar directory (map) kan niet. 

> **-s** voor symbolic link = nieuwe iode met naam bestand waar men moet naar wijzen

> drivers intanties checken:

```bash
[root@localhost besturingssystemen]# ll /dev/sd*
brw-rw---- 1 root disk 8, 0 May  9 15:28 /dev/sda 
brw-rw---- 1 root disk 8, 1 May  9 15:28 /dev/sda1
brw-rw---- 1 root disk 8, 2 May  9 15:28 /dev/sda2
brw-rw---- 1 root disk 8, 3 May  9 15:28 /dev/sda3
#8: major number = driver die gebruikt wordt 
#3: minor number = zoveelste instantie dat er gebruik van maakt
#major & minor zijn uniek voor elk device
```

> mknod: wordt gebruikt om device node aan te maken



### Redirection, piping en filtering, process substitution en het commando find

>Zoals reeds bij deel V aangehaald werd, zal elk in de shell gestart programma beschikken
>over **drie** **file descriptors**: **standaardinvoer (stdin)**, **standaarduitvoer (stdout)** en
>**standaardfout (stderr)**. Gewone uitvoer wordt steeds naar standaarduitvoer gestuurd terwijl
>eventuele fouten terechtkomen op standaardfout. In de shell waarin je ingelogd bent is
>standaardinvoer **meestal gelijk aan het toetsenbord** (invoer wordt afgesloten met **Ctrl-D**
>voor end of file of eventueel **Ctrl-C** voor terminate), en worden beide uitvoerkanalen met het
>beeldscherm verbonden. **Elk kanaal** heeft een **eigen nummer** waarmee de shell de kanalen identificeert:
>
>**0** standaardinvoer
>**1** standaarduitvoer
>**2** standaardfout

23. >Verwijder de werkbestanden tmp*.txt, indien die reeds zouden bestaan. Voer hiertoe
    >het commando rm -f tmp*.txt uit. Voer daarna achtereenvolgens deze opdrachten uit:
    >
    >• du /etc
    >• du /var > tmp.txt
    >• du /etc 1> tmp.txt
    >• du /var >> tmp.txt
    >• du /etc 1>> tmp.txt
    >• > tmp.txt du /etc
    >• du /var > tmp1.txt > tmp2.txt
    
    > Bekijk na elk commando:
    >
    > - de uitvoer van het commando,
    >
    > - de toestand van de werkbestanden tmp\*.txt (bijvoorbeeld via de commando's wc
    >   tmp\*.txt of ls -l tmp*.txt),*
    >
    > - de inhoud van de werkbestanden tmp.txt (bijvoorbeeld via het commando cat
    >   tmp*.txt of door de bestanden in een teksteditor te openen).
    >   Wat besluit je na het vergelijken van de resultaten van elke tussenstap?

```
Je kan besluiten dat het bestand telkens overschreden wordt omdat er vanuit een andere directory geschreven wordt.
du /var > tmp1.txt > tmp2.txt  -> tmp1 is dus leeg

> overschrijven
>> append
```

24. >Verwijder eerst het werkbestand tmp.txt. Voer daarna volgende opdrachten  uit:  
    >•  set -o  noclobber  
    >•  echo test > tmp.txt  
    >•  echo test > tmp.txt  
    >•  echo test >| tmp.txt  
    >•  set +o noclobber  
    >•  echo test > tmp.txt  
    >•  set -C # hoofdletter verplicht!  
    >•  echo test > tmp.txt
    >•  echo test >| tmp.txt  
    >•  set +C  
    >•  echo test > tmp.txt

    >Wat besluit je uit de uitvoer van de verschillende tussenstappen? Waar vind je
    >informatie terug over de shell-variabele noclobber?

```
De -o noclobber informatie zorgt er voor dat bestanden niet meer overschreven kunnen worden.
 
>| kan gebruikt worden om de noclobber shell variabele te overriden. 
set -C doet het zelfde als set -o  noclobber. 
+C zorgt er voor dat je het terug kan aanpassen. (zelfde als set +o noclobber)

De informatie over de shell-variabele noclobber kan teruggevonden worden in de Bash Builtin Commands.
man set
/noclobber
```



25. >Foutmeldingen worden via een apart kanaal weergegeven, zodat er onderscheid  
    >gemaakt kan worden tussen gewone uitvoer en foutteksten. Voer achtereenvolgens  
    >volgende commando's uit en controleer de inhoud van het bestanden tmp*.txt*
    >
    >•  du /etc  
    >•  du /etc 1>tmp.txt  
    >•  du /etc 2>>tmp.txt  
    >•  du /etc >tmp1.txt 2>tmp2.txt  

```bash
•  du /etc  #uitvoer naar scherm
•  du /etc 1>tmp.txt  #gebufferde uitvoer naar tmp.txt
•  du /etc 2>>tmp.txt  #gaat fouten van commando du gaan appenderen naar tmp.txt
•  du /etc >tmp1.txt 2>tmp2.txt #gebufferde uitvoer naar tmp1.txt & niet gebufferde uitvoer (fouten) naar tmp2.txt
```

26. > Je kunt ook omleiden naar de vuilnisbak (/dev/null). Verklaar de uitvoer bij uitvoering
    >van volgende opdrachten:
    >
    >• du /etc > /dev/null
    >• cat /dev/null

```bash
du /etc > /dev/null #uitvoer wegschrijven naar prullenbak
cat /dev/null #prullenbak is leeg
```

27. > Ga na wat het effect is van cat /dev/null > test.txt

```bash
Maakt bestand leeg. (want prullenbak is leeg)
```

28. >Veronderstel dat een of ander programma continu informatie wegschrijft in een
    >logbestand (dat hierdoor onbeperkt en continu in grootte toeneemt), en dat niemand
    >geïnteresseerd is in dit logbestand. Hoe kun je vermijden dat je periodiek het bestand
    >moet legen of verwijderen?

```bash
ln -s /dev/null datum.txt #soft link dat verwijst naar/dev/null als oplossing
```

29. > Bekijk verdere mogelijkheden met de opdrachten:
    >• du /etc >tmp.txt 2>&1
    >• du /etc 2>&1 >tmp.txt
    >• du /etc &>tmp.txt
    >• du /etc 2>tmp.txt >tmp.txt
    >• exec 3>tmp.txt ; du /etc >&3 2>&1 ; exec 3>&-

```bash	
du /etc >tmp.txt 2>&1 #schrijf weg naar gebufferde kanaal &1 (& = file descriptor. Anders zou het schrijven naar bestand "1")
du /etc 2>&1 >tmp.txt #fouten naar scherm op gebufferde manier en naar tmp.txt
du /etc &>tmp.txt
du /etc 2>tmp.txt >tmp.txt
exec 3>tmp.txt ; du /etc >&3 2>&1 ; exec 3>&- #zelf file descriptor aanmaken (fd 3)

#&1 = naar scherm, gebufferd. &2 = naar scherm, niet gebufferd.

# '>' is output redirection  (output naar bestand ipv scherm) -> file terug leeg en dan toevoeging (overschrijven)
# '>>' regels toevoegen (append)
# '0>' standaardinvoer
# '1>' standaarduitvoer
# '2>' standaardfout
# '&1' file descriptor 1 (= standaard uitvoer)
# '&2' file descriptor 2 (= fouten kanaal)
```

30. >Verwijder eerst het werkbestand tmp.txt, indien dit reeds zou bestaan. Vergelijk daarna
    >telkens de uitvoer en de inhoud van tmp.txt bij uitvoering van volgende
    >commandoregels. Vergeet de spaties niet!
    >• du /etc ; du /var
    >• du /etc ; du /var > tmp.txt
    >• ( du /etc ; du /var ; ) > tmp.txt
    >• { du /etc ; du /var ; } > tmp.txt

    ```bash
    du /etc ; du /var #meerdere opdrachten gescheiden door ";"
    du /etc ; du /var > tmp.txt 
    ( du /etc ; du /var ; ) > tmp.txt #groep opdrachten met redirection op toegepast ( child process )
    { du /etc ; du /var ; } > tmp.txt #groep opdrachten met redirection op toegepast { huidige shell }
    ```

    >In UNIX wordt heel dikwijls de **standaarduitvoer** van het ene commando **gebruikt als**
    >**standaardinvoer** van het volgende. Deze gecombineerde vorm van invoer- en uitvoer-
    >redirection wordt **piping** genoemd. Men bekomt dit door tussen de twee betreffende
    >opdrachten een verticale streep (**|**) te plaatsen. Dit kan een willekeurig aantal keer op
    >dezelfde commandolijn herhaald worden. Hierbij worden de opdrachten steeds van links
    >naar rechts uitgevoerd.
    >
    >**Enkel de standaarduitvoe**r kan worden doorgepipet naar het volgende commando; de
    >foutuitvoer blijft op het scherm. Je kunt dit tenietdoen door vooraf de foutuitvoer om te
    >leiden naar standaarduitvoer d.m.v. redirection.
    >Een probleem dat veelvuldig optreedt is dat je **na het |-teken werkt in een subshell**. Het
    >**omdraaien** van de volgorde is bij het |-teken helaas **onmogelijk**. Een alternatief voor dat
    >probleem is **process substition**.
    >Wanneer we **process substitution** vergelijken met piping moeten we besluiten dat het
    >eerste de voorkeur geniet. Je kan in het onderstaande voorbeeld er voor kiezen om de wc-
    >opdracht als eerste te vermelden en dan pas de ls-opdracht. Zeker bij scripting is dit soms
    >minder schrijf- of prutswerk.
    >wc -l << (ls ~) //Process substitution (= alternatief pipes, omdraaien volgorde)
    >ls ~ | wc -l     //Gewoon piping (stdout wordt gebruikt als stdin)
    >
    >**Let wel, bij beide oplossingen worden evenveel kindprocessen aangemaakt en wordt ook**
    >**een pipe gebruikt als IPC (inter process communication). Er is dus geen enkele vorm van performantiewinst door gebruik**
    >**te maken van process substitution!**
    >Maak bij onderstaande opdrachten zoveel mogelijk gebruik van process substitution.
    >UNIX kent vele utilities zoals **head, tail, grep, uniq, sort en awk**, die hun input, meestal
    >tekststrings, uit de standaardinvoer halen, op deze data één of andere manipulaties
    >uitvoeren, en de resultaten van deze manipulatie naar standaarduitvoer schrijven. Deze
    >programma's worden filters genoemd. Filterprogramma's worden dikwijls in een keten van
    >pipes geschakeld, zoals in volgend voorbeeld. Vergelijk de uitvoer van
    >ps -A
    >en
    >ps -A | grep bash
    
    

31. >Hoe kan je ervoor zorgen dat de uitvoer van het commando **printf** "dit is een fout" niet
    >als standaarduitvoer, maar als standaardfout wordt geïnterpreteerd? De tekst moet dus
    >wel op het scherm getoond worden, maar mag niet doorgepipet worden naar een
    >volgend commando.

```bash
printf "hello" >&2 #niet gebufferd, wel weergegeven op het scherm.
```

32. >Enkel de standaarduitvoer wordt normaal doorgepipet naar het volgende commando.
    >Hoe kan je (met een wc-filter) het aantal foutmeldingen vragen bij het commando du
    >/etc?

```bash
du /proc 2>&1 > /dev/null | wc -l
```

33. >Hoe kun je met behulp van de head- en tail-commando's enkel de N-de lijn van een
    >bestand tonen, voor een willekeurige N? Zorg er voor dat geen uitvoer wordt
    >geproduceerd indien het gevraagde lijnnummer groter is dan het aantal lijnen in het
    >bestand.

```bash
head -3 /etc/passwd | tail -1
```

34. >Met behulp van de eenvoudige opdracht dos2unix kun je de **<CR><LF>**-sequenties in een
    >bestand dat door een Windowstoepassing is aangemaakt, vervangen door enkele <LF>-
    >lijnscheidingstekens, zoals dit op UNIX verwacht wordt. Hoe kun je met behulp van de tr
    >opdracht hetzelfde effect bereiken? Welke zijn de nadelen van deze benadering?

```bash
tr a-z A-Z < /etc/passwd #tr - translate or delete characters
```

35. > Het commando uniq -d *bestandsnaam* is bedoeld om alle lijnen te tonen die meerdere
    >keren voorkomen in een bestand. Echter, indien men dit commando toepast op een
    >bestand met als inhoud
    >*het*
    >*is*
    >*mooi*
    >*het*
    >*geweest*
    >*is*
    >dan wordt geen enkele lijn getoond. Hoe komt dit?
    >Zoek een eenvoudige oplossing hiervoor, door gebruik te maken van een pipe.

```bash
sort 35.txt | uniq -dc 
#-d (repeated) only print duplicate lines, one for each group
#-c (count) prefix lines by the number of occurrences
```

36. > Het filter-commando **grep** toont alle lijnen van een bestand die aan een bepaald **patroon**
    > voldoen. **Op welke drie verschillende manieren** (drie verschillende opties, met betrekking
    > op de interpretatie van regular expressions) kan dit patroon opgegeven worden? 
    >
    > Let erop dat het patroon door het grep-commando moet worden geïnterpreteerd en niet
    > door de shell. Gebruik de drie mogelijkheden om alle lijnen van een bestand te zoeken
    > die een woord bevatten uit de lijst: BEGIN END IF ENDIF
    > In de man-pages van grep vind je een extra sectie over regular expressions.
    
    **[Regex]:**
    
    ```
    ^begin van lijn
    $einde van lijn
    .willekeurig teken
    		?mag voorkomen maar moet niet
    		+1ofmeer
    		*0ofmeer
    [bereik] (kan gevolgd worden door ?of+of*)
    [^alles behalve bereik] (kan gevolgd worden door ?of+of*)
    {2} komt 2x voor
    {2,3} komt min 2x en max 3x voor
    ^[1-9] [0-9]*$ testen of het een getal voorstelt met 2 cijfers. * wijst op of meerder occurences van [0-9]
    ```
     ```bash
    drie verschillende manieren:
    
    -G, --basic-regexp (= grep)
    	Interpret  PATTERNS  as  basic  regular  expressions. This is the default.
    
    -E, --extended-regexp (= egrep)
    	Interpret PATTERNS as extended regular expressions
    
    -F, --fixed-strings (= fgrep)
    	Interpret PATTERNS as fixed strings, not regular expressions.
     ```
    
37. >Installeer emacs (yum install emacs) en wijzig de werkdirectory naar
    >/usr/share/emacs/versienummer/etc/tutorials. Voorspel de uitvoer van volgende
    >commando's en test ze dan uit op de Emacs tutorial:
    >• grep -E 'C\-[a-z] *' TUTORIAL
    >• grep -E '(C\-[a-z] *){2}' TUTORIAL
    >• grep '\(C\-[a-z] *\)\{2\}' TUTORIAL
    >Het patroon moet tussen enkele of dubbele aanhalingstekens staan, zodat de shell de
    >speciale tekens niet interpreteert, maar het patroon ongewijzigd doorgeeft aan het grep-
    >commando.

    ```bash
    grep -E 'C\-[a-z] *' TUTORIAL 
    grep -E '(C\-[a-z] *){2}' TUTORIAL
    grep '\(C\-[a-z] *\)\{2\}' TUTORIAL
    
    #1.-E=extended regex (Hoofdletter C, gevolgd door minteken, gevolgd door letter A-Z, gevolgd door 0 of meerdere spaties)
    #2. Zelfde als het voorgaande maar 2x na elkaar.
    #3. 
    #(grep = general regular expression parser)
    ```

38. > Wat is de uitvoer van volgend commando?
        > `grep -E '^.*$' TUTORIAL`
        > Wat zijn de twee verschillen met
        > `grep -E '^\.*$' T*`

    ```bash
    grep -E '^.*$' TUTORIAL #Alle lijnen
    grep -E '^\.*$' T* #Begin, gevolgd door een punt, 1 of meerdere keren
    ```

39. > Zoek de opties van het grep-commando die het gedrag van grep als volgt wijzigen:
    > • Er worden enkel lijnen getoond die **niet** aan het patroon voldoen.
    > • Deze patronen worden in een configuratiebestand opgeslagen, **één lijn per**
    > **patroon**

    ```bash
    # -v -> inverse: regex omdraaien
    # -f -> ontvang pattern van file, 1 per lijn
    ```

    

40. >Voorspel de uitvoer die je bij de volgende commando's verwacht en voer daarna pas de
    >commando's effectief uit, om te controleren dat je prognose correct was.

    > 1. grep -E '^$' TUTORIAL | wc -l
    > 2. grep -Ev '^$' TUTORIAL
    > 3. grep -E 'margin|direction' TUTORIAL | nl
    > 4. nl TUTORIAL | grep -E 'margin|direction'
    > 5. grep -E '^-+$' TUTORIAL | uniq -d
    > 6. grep -E '^-+$' TUTORIAL | sort | uniq -d
    > 7. grep -E '\--+' TUTORIAL | grep -Ev '^-+$'

    > Een aantal van deze commando's zijn syntactisch correct, maar bevatten logische
    > fouten. Welke? 

    ```bash
    1. grep -E '^$' TUTORIAL | wc -l 			#Alle lege lijnen. Output doorsluizen naar wordcount -l (aantal matches tellen)
    2. grep -Ev '^$' TUTORIAL 		 			#Alles behalve lege lijnen
    3. grep -E 'margin|direction' TUTORIAL | nl	#Alle lijnen die ofwel het woord margin, ofwe het woord direction bevatten.
    											#nl nummert iedere lijn. niet de juiste lijnnummeres die we verwachten.
    4. nl TUTORIAL | grep -E 'margin|direction'	#betere optie om lijnnummers weer te geven
    5. grep -E '^-+$' TUTORIAL | uniq -d		#Enkel lijnen met mintekens. uniq -d toont enkel de unieke lijnen.
    6. grep -E '^-+$' TUTORIAL | sort | uniq -d #Altijd sort gebruiken bij uniq! anders werkt het niet zoals gewenst.
    7. grep -E '\--+' TUTORIAL | grep -Ev '^-+$'#Deel1: Minstens 2 mintekens. 
    											#Deel2: Zoekt naar lijnen met die niet 1 of meerdere mintekens bevatten
    											#De combinatie zorgt er voor dat er geen matches zijn.
    											
    Een aantal van deze commando's zijn syntactisch correct, maar bevatten logische
    fouten. Welke? 
    
    3, 5 & 7 zijn niet ok.
    ```



41. >Welke van onderstaande constructies kun je gebruiken indien de uitvoer van de
    >opdracht te lang is om op één scherm getoond te worden?
    >• du /
    >• du / | less
    >• du / | more
    >• du / | cat
    >Welk commando is zinloos en waarom?

    ```bash
    du /
    du / | less #scrollable, beter dan more
    du / | more #vergelijkbaar met less. less is beter.
    du / | cat #zinloos
    ```

42. >Bekijk hoeveel keer je het commando man in het verleden (voor de huidige inlogsessie)
    >reeds gebruikt hebt. Gebruik hiervoor het bestand .bash_history uit je home-directory en
    >de commando's wc en grep.

```bash
[root@localhost ~]# grep -E  "^man" .bash_history | wc -l
6
```

43. >In het bestand /etc/passwd worden de velden gescheiden door een :-teken. Het **eerste**
    >veld bevat de **gebruikersnaam** en het **derde veld** het **gebruikersID**, terwijl het **vierde veld**
    >het **nummer van de primaire groep** is waartoe de gebruiker behoort.
    >Sorteer het passwd-bestand met behulp van het **sort** commando, met het nummer van
    >de primaire groep als sleutel. Zorg ervoor dat het sort commando enkel sorteert op het
    >veld met de primaire groep (en niet op het restant van de lijn), en dit veld alfabetisch
    >(niet-numeriek) sorteert. Bij deze sortering moet bijvoorbeeld gelden: 1 < 100 < 12. Geef
    >de volledige commandolijn waarmee je deze opdracht hebt uitgevoerd. Voer dit
    >commando vervolgens uit, waarbij je de uitvoer omleidt naar het bestand ~/passwd.
    >Doe nu hetzelfde met het group-bestand. Dit bestand bevat onder meer als eerste veld
    >de groepsnaam, terwijl het nummer van de groep nu in het derde veld staat. Sorteer
    >opnieuw volgens dezelfde criteria, met het nummer van de groep als sleutel. Leid de
    >uitvoer nu om naar het bestand ~/group.

```bash
sort -t : -k1,1 /etc/passwd #eerste veld
sort -t : -k1.2,1.2 /etc/passwd #eerste veld, 2de char
sort -t : -k4,4 /etc/passwd > passwd #4de veld wegschrijven naar passwd
sort -t : -k3,3 /etc/group > group #3de veld wegschrijven naar group

#UPG: user private groups: Groep waarbij gebruiker enigste lid is.
#-t = field seperator (: in dit geval)
#-k = key
```

44. >Gebruik het commando join met aangepaste opties om op basis van de daarnet
    >**gecreëerde** bestanden **~/passwd** en ~/group een lijst af te drukken met op elke lijn enkel
    >drie velden: de gebruikers-ID, de volledige gebruikersnaam en de naam van de primaire
    >groep waartoe de gebruiker behoort. Geef de volledige commandolijn waarmee je deze
    >opdracht hebt uitgevoerd. Hoeveel uitvoerregels zijn er? Hoe heb je dit aantal geteld?
    >Vergelijk met het aantal regels in het passwd bestand. Indien deze aantallen niet
    >overeenkomen heb je ofwel bij deze vraag, ofwel bij de vorige een fout gemaakt.

```bash	
join -t : -1 4 -2 3 /etc/passwd /etc/group #We nemen het 4de veld van het 1ste bestand en het 3de veld van het 2de bestand
join -t : -1 4 -2 3 -o "1.1 1.3 2.1" passwd group | less #-o is een uitvoerlijn. 
														 #1.1 gebruikersnaam, 1.3 userid & 2.1 naam primaire groep
						 
#combinatie 43+44:
join -t : -1 4 -2 3 -o "1.3 1.1 2.1"
 < (sort -t : -k4,4 /etc/passwd)  #gecreëerde bestanden ~/passwd
 < sort( -t : -k3,3 /ectd/group)  #gecreëerde bestanden ~/group
```

45. >Sorteer het /etc/passwd bestand, met behulp van het sort commando. Gebruik als
    >**primaire sleutel** het **vierde veld** van het bestand. Zorg ervoor dat je in **numerieke**
    >volgorde sorteert (12 < 100). Regels met gelijke numerieke waarden voor het vierde veld
    >moeten gesorteerd worden met het **vijfde veld** als **secundaire sleutel**, waarbij **geen**
    >**onderscheid** mag gemaakt worden tussen **hoofdletters en kleine letters**, en voor de
    >
    >sorteervolgorde nu de **omgekeerd alfabetische** volgorde moet genomen worden. Geef
    >de volledige commandolijn waarmee je deze opdracht hebt uitgevoerd.

```bash
sort -t : -k4n,4n -k5fr,5fr < /etc/passwd

-n, --numeric-sort
             compare according to string numerical value
-f, --ignore-case
             fold lower case to upper case characters
-r, --reverse
			 reverse the result of comparisons
             
#-k4n,4n betekent sorteren op veld (key) 4, numeriek
#-k5fr,5fr betekent sorteren op veld (key) 5, ignore case, reverse (=omgekeerd alfabetisch)
```

46. >Gebruik het cut commando met aangepaste opties om van het bestand /etc/passwd alle
    >**gebruikersnamen** te tonen. Geef opnieuw de volledige commandolijn waarmee je deze
    >opdracht hebt uitgevoerd.

```bash
cut -d : -f 1 /etc/passwd #cut met : als delimiter en enkel field 1 (gebruikersnaam)

-d, --delimiter=DELIM
              use DELIM instead of TAB for field delimiter
-f, --fields=LIST
              select only these fields;  also print any line that contains  no
              delimiter character, unless the -s option is specified
              
[root@localhost ~]# cut -d : -f 1 /etc/passwd
root
bin
daemon
adm
...
```

47. >Het commando **tee** bestandsnaam neemt de **standaardinvoer**, geeft de invoer
    >**ongewijzigd** door aan de **standaarduitvoer**, en kopieert de standaardinvoer tegelijkertijd
    >naar het **opgegeven bestand**. Gecombineerd met een pipe laat dit je toe de uitvoer van
    >een programma terzelfdertijd op het **beeldscherm** te bekijken, en te **loggen** voor later
    >gebruik. Hoe kun je ervoor zorgen dat de uitvoer van een programma tegelijkertijd op
    >het beeldscherm verschijnt, en wordt toegevoegd aan een bestaand bestand, zonder dat
    >de oude inhoud van dat bestand wordt overschreven?
    >Het commando **find** zoekt in alle subdirectory's vanaf een opgegeven directory naar alle
    >bestanden die aan bepaalde criteria voldoen (naam, grootte ...) en toont alle gewenste
    >informatie van alle bestanden die voldoen. Dit commando heeft heel veel mogelijkheden
    >door het toevoegen van aangepaste opties. Leer de goede opties op te zoeken in de man-
    >pages. Het commando genereert dikwijls veel foutmeldingen, die je bij voorkeur omleidt.
    >
    >**tee**: Read from standard input and write to standard output and files
    >
    >bv. **echo ok | tee f1 f2 f3** (schrijft "ok" (afkomstig van standaard invoer adhv pipe) naar f1,f2 & f3)
    
    **Dit was een examenvraag vorig jaar**
    
    

```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char **argv) {
    /* 1. alle bestanden openen en de fildescriptor bijhouden in een array */

    int *fds = malloc(sizeof(int) * (argc - 1)); //aantal output files tellen: elke opgegeven parameter is een file
    int teller = 0;
    for (int i = 1; i < argc; i++) {
        if (strcmp(argv[i], "-") == 0) { //check of dat er een minteken is meegegevens
            fds[teller++] = 1;			//fd voor standaard uitvoer meegeven
            continue;
        }
        fds[teller] = open(argv[i], O_WRONLY | O_CREAT); // bestanden aanmaken indien ze niet bestaan
        if (fds[teller] < 0) { 							
            perror(argv[i]);
            continue;
        }
        teller++;
    }
    fds[teller++] = 1; //stdin naar stdout schrijven

    /* 2. inlezen van stdin en wegschrijven naar elke uitvoer filedescriptor */

    char buffer[BUFSIZ]; 							//BUFSIZ is ideale grootte voor I/O opdrachten

    int n = read(0, buffer, BUFSIZ);
    while (n != 0) {
        for (int i = 0; i < teller; i++) {  		
            write(fds[i], buffer, n);				//schrijf naar elk bestand
        }
        n = read(0, buffer, BUFSIZ);
    }
    if (n < 0) {
        perror(argv[0]);
    }

    /* alle bestanden sluiten */
    for (int i = 0; i < teller; i++) {
        if (fds[i] == 1) {
            continue;
        }
        if (close(fds[i]) < 0) {
            perror(argv[i]);
        }
    }
    free(fds); //geheugen terug vrij maken
    return 0;
}
```

48. > Zoek naar alle bestanden in de /etc directory tree waarvan de naam begint met pass.

```bash
find /etc -type f -name 'pass*'

/etc/pam.d/passwd
/etc/passwd-
/etc/passwdqc.conf
/etc/passwd
/etc/authselect/password-auth

-type:
              c		 File is of type c:
              b      block (buffered) special
              c      character (unbuffered) special
              d      directory
              p      named pipe (FIFO)
              f      regular file
              l      symbolic link; this is never true if the -L option or the
                     -follow  option is in effect, unless the symbolic link is
                     broken.  If you want to search for symbolic links when -L
                     is in effect, use -xtype.
              s      socket
              D      door (Solaris)


```

49. >Je kunt ook meerdere testen combineren. Hoe vraag je alle subdirectory's (geen
    >bestanden) waarvoor de naam begint met sh?

```bash
find . -type d -name "sh*" #in de volledige dir structuur naar directories (-type d) gaan zoeken die starten met "sh".
./.local/share
```

50. >Gebruik het find-commando om een lijst te bekomen van alle **bestanden** in de **/usr**
    >directory tree met een bestandsgrootte van minstens **1 megabyte**. Bij het uitprinten (één
    >lijn per bestand) moet je het **volledig pad** van de gevonden bestanden laten voorafgaan
    >door de **grootte** van het bestand. Geef de volledige commandolijn waarmee je deze
    >opdracht hebt uitgevoerd. Let er ook op dat je enkel bestanden in de lijst opneemt en
    >**geen directory's**.

```bash
find /usr -type f -size +1M -exec du -h {} \; #commando du uitvoeren voor elk gevonden object. {} = object in kwestie
strace 2>&1 find /usr -type f -size +1M -exec du -h {} \+ > /dev/null; #+ gaat concatineren
find /usr -type f -size +1M -printf "%s %p\n" | sort -t " " -k1nr,1nr | cut -d " " -f2 #geformatteerde output

#\; object per object \+ verzameling van objecten (concat)
```

51. >Gebruik het **find**-commando om een **lijst** te bekomen van alle **bestanden** in je
    >**persoonlijke map**, die gedurende de **laatste twee weken gewijzigd** werden. Bij het
    >uitprinten (**één lijn per bestand**) moet je het **volledig pad** van de gevonden bestanden
    >laten voorafgaan door het **tijdstip** van de laatste wijziging. Geef de volledige
    >commandolijn waarmee je deze opdracht hebt uitgevoerd. Let er ook op dat je enkel
    >**bestanden** in de lijst opneemt en geen directory's.

```bash	
find /usr -type f -mtime 14 -exec du -h {} \;

-mtime n
              File's data was last modified n*24 hours ago.  See the  comments
              for -atime to understand how rounding affects the interpretation
              of file modification times.

find ./besturingssytemen/ -type f -mtime 0 -exec du --time {}  

4	2022-06-11 17:41	./besturingssytemen/f3
4	2022-06-11 17:41	./besturingssytemen/f1
4	2022-06-11 17:41	./besturingssytemen/f2
```

52. >Gebruik het find-commando om een lijst te bekomen van alle **subdirectory's** van /usr
    >waarin zich C- of C++-headerbestanden (bestanden met suffix **.h**) bevinden. Gebruik een
    >commandolijn van de gedaante
    >find ... | sort | uniq
    >
    >**Let erop dat enkel de namen van de directory's weergegeven worden.**
    >
    >sort: sorteert output op bepaalde key.
    >
    >cut: toon specifieke deel van output op basis van key.
    >
    >uniq: diplicated lijnen worden gemerged naar eerste voorkomen

```bash
find /usr -type f -name "*.h" | rev | cut -d / -f 2 | rev | uniq -u

#rev: reverse de output
#cut -d / -f 2 : cutten op delimeter / en veld 2 (de subdirectory naam) nemen
#rev: terug reversen 
#uniq -u : enkel unieke lijnen tonen
```

53. >Geef een lijst van alle directory's waar je als gewone gebruiker geen toegang toe hebt.
    >Tip: gebruik cut en de foutuitvoer van het commando find.

```bash
find / -type d 2>&1 > /dev/null | cut -d ‘ -f 2 | cut -d ‘ -f 1
```

54. Toon alle bestanden van de map /etc die rwx-rechten hebben voor de huidige gebruiker.

````bash
 ls -l /etc | sort -t : -k1,1 | grep "rwx" 
 #geen enkele files. 
 #sort is optioneel
 
 #voorbeeld dat wel een output heeft
[root@localhost ~]# ls -l /etc | sort -t : -k1,1 | grep "rw-rw"
-rw-rw-r--.  1 root root        19 Feb 25  2021 locale.conf
-rw-rw-r--.  1 root root        28 Feb 25  2021 vconsole.conf
-rw-rw-r--.  1 root root       615 Feb 25  2021 fstab
````



### Shellvariabelen

> Bij het ingeven van een commando in bash gebeurt er een fork() =  clone = terminal maakt **kindproces** aan. Parent en kind beschikken over zelfde code. code van kind proces wordt overschreven met ingegeven commando.
>
> Ronde haakjes forceren een **fork()** = **kindproces**. bv `( exec ls )` .

55. >Naast gekende shellvariabelen, zoals PATH, kun je **zelf shellvariabelen toevoegen**. Tenzij
    >je de declare-opdracht gebruikt, zijn ze steeds van het type string. Er wordt onderscheid
    >gemaakt tussen hoofdletters en kleine letters. Voer de volgende commando's uit:
    >• printf “PATH %s\n” $PATH
    >• printf “dag %s\n” $dag
    >• dag=jan
    >• printf “dag %s\n” $dag
    >• set

```bash
#PATH (windows) = environment variables
#PATH (Linux) = wanneer er een commando wordt ingegeven en deze niet wordt teruggevonden in de history, dan wordt er gezocht op volgend path:

[root@localhost ~]# echo $PATH
/root/.local/bin:/root/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin

#${BASH_CMDS[@]} = commando om te checken waar alle recent aangeroepen commando's zich bevinden:
[root@localhost ~]# echo ${BASH_CMDS[@]}
/usr/bin/ls

#${!BASH_CMDS[@]} =  toont recent gebruikte commando's
[root@localhost ~]# echo ${!BASH_CMDS[@]}
ls
```



56. >Definieer zelf de variabele date met een willekeurige datum als inhoud. Wat is het
    >verschil tussen $date, $(date) en ${date}? Onderzoek dit met behulp van het commando
    >echo. Je kunt bijvoorbeeld je eerste script schrijven met de volgende regels:
    >**date="18/5/2016"**
    >**echo '$date:' $date**
    >**echo '${date}:' ${date}**
    >**echo '$(date):' $(date)**
    >De enkele aanhalingstekens garanderen dat de tekst letterlijk wordt doorgegeven aan
    >het echo-commando.
    >Merk op dat de variabele date niet gekend is in de shell die het script heeft opgestart. Elk
    >script wordt namelijk uitgevoerd in een nieuwe shell, met zijn eigen variabelenlijst,
    >instellingen ...

```bash
#code wordt enkele geïnterpreteerd wanneer zaken tussen dubbele quotes staan. Bij single quotes zullen de zaken letterlijk genomen worden.

root@localhost ~]# var = "het is mooi weer"
bash: var: command not found...
[root@localhost ~]# var="het is mooi weer"
[root@localhost ~]# echo $var
het is mooi weer
[root@localhost ~]# echo "var=$var"
var=het is mooi weer
[root@localhost ~]# echo 'var=$var'
var=$var

[root@localhost ~]# echo ${var}iable 	#manier om variabelen tussen strings weer te geven
het is mooi weeriable

[root@localhost ~]# date="datum"
[root@localhost ~]# echo "date=$(date)" #command substitution
date=Wed May 11 03:06:51 PM CEST 2022
```

57. >Bash ondersteunt vanaf versie 3 de mogelijkheid tot **indirecte adressering**: je kunt de
    >inhoud van een variabele opvragen door haar naam in een tweede variabele te stoppen,
    >die je invult in **${!varnaam}**. Dit is vergelijkbaar met pointers in C en C++. Vul de inhoud
    >van de variabele een willekeurig op, en geef aan de variabele twee als inhoud de string
    >'een'. Voorspel het resultaat van
    >echo ${een}
    >echo ${twee}
    >echo ${!twee}
    >echo ${$twee}
    >In oudere versies van Bash kun je dit gedrag simuleren d.m.v. de opdracht eval. Hoe?

```bash
[root@localhost ~]# een=1
[root@localhost ~]# echo ${een}
1
[root@localhost ~]# twee=een
[root@localhost ~]# echo ${twee}
een
[root@localhost ~]# echo ${!twee}
1

[root@localhost ~]# eval $twee=17 #Met eval kan je de waarden van variabelen (adhv pointers) aanpassen.
[root@localhost ~]# echo $een
17

[root@localhost ~]# echo {1..10} #brace expension
1 2 3 4 5 6 7 8 9 10

[root@localhost ~]# echo {1..$een}
{1..17}
[root@localhost ~]# eval echo {1..$een} #Eerst wordt eval uitgevoerd, daarna de brace expension
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

#variable verwijderen: unset variable_name
```

58. >Bekijk de inhoud van de shellvariabelen **PS1, PS2, SHLVL, RANDOM, SECONDS** en **PWD**,
    >en zoek de betekenis ervan op in info bash of man bash, sectie Shell Variables.
    >Vraag de inhoud van deze variabelen eerst interactief op (met echo) en schrijf vervolgens
    >een script om de inhoud van deze variabelen op het scherm te tonen. Kan je de
    >verschillen verklaren?

```bash
#PS1 = primary prompt
[root@localhost ~]# echo $PS1
[\u@\h \W]\$

#PS2 = secondary prompt, wordt gebruikt bij incompleet commando
[root@localhost ~]# echo $PS2
>

#SHLVL = shell level. om te kijken of dat je in een subshell aan het werken bent of niet.
[root@localhost ~]# echo $SHLVL
1
[root@localhost ~]# bash
[root@localhost ~]# echo $SHLVL
2
[root@localhost ~]# exit
exit
[root@localhost ~]# echo $SHLVL
1

#RANDOM = geeft random getal terug tussen 1-(2^15-1). Af te raden.
#mogelijke examenvraag: script om bytes om te zetten naar getal.

head -c 8 /dev/random | od -An -tu8

head -c 8 /dev/random #random cijfer van 8 bytes.
| An -tu8 #omzetten naar leesbaar cijfer
```

59. > Hoe kun je commentaar toevoegen in een script?

    ```bash
    #
    ```

60. >Hoe kun je de variabele PATH zodanig wijzigen dat je bij het aanroepen van een
    >shellscript (dat zich in de actieve directory bevindt), niet steeds naar de actieve directory
    >moet verwijzen?
    >Zorg ervoor dat je oplossing werkt in eender welke directory. Het script moet dus steeds
    >gezocht worden in de werkdirectory, zonder telkens de waarde van PATH aan te passen.

```bash
huidige map bijvoegen (path variabele uitbreiden): . (punt) toevoegen.
. is een hardlink naar huidige map
.. is een hardlink naar bovenliggende map
```

61. > Hoe kun je ervoor zorgen dat wanneer bij de cd-opdracht een relatieve padnaam (dus
    >niet beginnend met /) als argument opgegeven wordt, niet alleen de huidige
    >werkdirectory als prefix uitgeprobeerd wordt, maar ook een aantal vaste directory's?

```bash
CDPATH="/usr:/" #eerst zoeken in /usr, daarna in / (hoofd directory)
#op deze manier zal het cd commando altijd zoeken vanaf /usr
#als het opgegeven path niet gevonden wordt, dan wordt er verder gezocht in / (hoofd directory)
```

62. >Hoe kun je met eenzelfde opdracht regelmatig heen en terug schakelen tussen twee
    >mappen als actieve directory?

```bash
cd - #terugkeren naar vorige map
```

63. >Je kunt met het commando **read** tegelijkertijd meerdere variabelen inlezen via het
    >**standaard invoerkanaal**. Test dit uit met:
    >read a b c d
    >Kan je dit aanpassen zodat de gegevens **uit** een bestand gelezen worden?
    >Probeer dit ook eens met een script op te lossen, en merk op dat de variabelen enkel in
    >het script bestaan!

```bash
[root@localhost ~]# read a b c d
het is mooi weer
[root@localhost ~]# echo $a
het

#alles dat niet meer in een variabele past wordt in de laatste variabele gestoken.
#bv:  Het is mooi weer vandaag:
#var1:het
#var2:is
#var3: mooi weer vandaag  

#uit bestand:
[root@localhost ~]# read a b c d < /etc/passwd
[root@localhost ~]# echo $a
root:x:0:0:root:/root:/bin/bash
[root@localhost ~]# echo $b
[root@localhost ~]# echo $c
```

64. >Achterhaal de waarde van de bijzondere variabele **IFS** (**I**nternal **F**ield **S**eperator). Merk op dat echo $IFS je niet veel
    >wijzer maakt; echo "$IFS" (met aanhalingstekens) verraadt echter al dat er een newline-
    >karakter in de waarde staat. De eigenlijke waarde van IFS kun je vinden met
    >**grep ^IFS < <(set)**
    >Zoals je weet uit vorige oefeningen, zorgt $' ' hierin voor interpretatie van de escapes.
    >**Standaard** bevat IFS dus een **spatie**, een **tab** en een **regeleinde**. Deze karakters worden
    >door read gebruikt voor het **splitsen** van **invoervelden**, ongeveer zoals o.a. de operator
    ><< in C++ en de Scanner-klasse in Java.
    >Je kunt de waarde van IFS ook (tijdelijk) wijzigen, hetzij door een functie te gebruiken,
    >hetzij door de IFS-variabele vóór het commando in te stellen. Gebruik het commando
    >read om een aantal variabelen in te lezen gesplitst op spaties, dubbelepunten en
    >komma's. Ga de werking na met read

```bash
[root@localhost ~]# grep ^IFS < <(set)
IFS=$' \t\n' #splitst default op spaties, tabs & newlines
```

65. >Het wijzigen van IFS kan voor verwarring zorgen. Voer volgend script uit (zet het in een bestand):
    >IFS=':'
    >x=ik:ben:groot
    >echo x = $x
    >echo x = "$x"
    >echo x = '$x'
    >grep -E ^x= < <(set)
    >grep -E ^x < <(set)
    >declare -p x
    >declare -p ${!x*}

```bash
[root@localhost ~]# bash ifs.sh
x = ik ben groot
x = ik:ben:groot
x = $x
x=ik:ben:groot
x=ik:ben:groot
declare -- x="ik:ben:groot"
declare -- x="ik:ben:groot"
[root@localhost ~]# grep ^IFS < <(set)
IFS=$' \t\n'
```

66. >Je kunt de standaarduitvoer van een commando ook toekennen aan een variabele.
    >Daarbij maak je gebruik van **command substitution**. Dit is vooral **zinvol** wanneer de
    >**uitvoer van een commando uit slechts één regel bestaat**. Indien je slechts een deel van
    >de uitvoer aan de variabele wilt toekennen, dan kun je proberen dit er met cut uit te
    >halen.
    >Voorspel de inhoud van de variabele t na volgende commando's:
    >
    >1. t=$(du /etc/passwd)
    >2. t=$(cut -f1 < <(du /etc/passwd))
    >3. t=$(cut -f1 < <(wc -l /etc/passwd))
    >4. t=$( cut -d " " -f2 < <(wc -l /etc/passwd))
    >5. t=$(wc -l < /etc/passwd)
    >6. tab=( $(wc -l /etc/passwd) )
    >7. echo ${tab[1]}

```bash
t=$(du /etc/passwd) #uitvoer van commando komt in variable t = command substitution
t=$(cut -f1 < <(du /etc/passwd))
t=$(cut -f1 < <(wc -l /etc/passwd))
t=$( cut -d " " -f2 < <(wc -l /etc/passwd))
t=$(wc -l < /etc/passwd)
tab=( $(wc -l /etc/passwd) ) #er wordt een tabel aangemaakt
echo ${tab[1]}				 #inhoud tabel wordt uitgeschreven


[root@localhost ~]# echo ${tab[0]}
47
[root@localhost ~]# echo ${tab[1]}
/etc/passwd
```

### Arithmetic expansion



67. >**Normaal** worden alle variabelen door de shell als **strings** beschouwd. Toch kun je met
    >behulp van een specifiek intern commando **rekenkundige bewerkingen** op variabelen
    >toepassen. Dit laat je niet alleen toe om optellingen (+), aftrekkingen (-),
    >vermenigvuldigingen (*), gehele delingen (/ en %) en machtsverheffingen (**) uit te
    >voeren, maar ook om bitoperaties (<<, >>, &, |, ^, ! en ~) of logische testoperaties (&&
    >en ||) toe te passen. Zoek dit specifiek commando op in info bash of man bash; lees de
    >secties Arithmetic Expansion en Arithmetic Evaluation.
    >Pas het gevonden commando toe om het product van twee variabelen, x en y in een
    >variabele z te stoppen.
    >Welk intern (builtin) commando kun je hiervoor als alternatief gebruiken?

    ```bas
    [root@localhost ~]# echo $((7*5))
    35
    ```

    

68. >Hoe kun je in een script, met behulp van de variabele **SECONDS**, de uitvoeringstijd
    >bepalen van een groep commando's? Pas dit bijvoorbeeld toe om de **uitvoeringstijd** (in
    >seconden) te **bepalen** van de **tijdrovende instructie**
    >**ls -lR / > /dev/null 2>&1**

```bash
#!/bin/bash

echo $SECONDS
ls -lR / > /dev/null 2>&1
echo $SECONDS
```

```bash
[root@localhost ~]# bash seconds.sh 
0
44
```



### Argumenten van een script/functie, positionele parameters en speciale parameters

>Bij het uitvoeren van een shellscript kun je **argumenten** opgeven. Het script zal deze
>argumenten toekennen aan de positionele parameters $1, $2 enz (of ${1}, ${2} enz). In elk
>script beschik je steeds over de **positionele parameters**. Als de argumentenlijst leeg is dan
>bestaan de positionele parameters nog steeds, maar ze hebben een lege inhoud. Je kunt de
>positionele parameters slechts op twee manieren wijzigen:
>
>- a. Met **set --** argumentenlijst worden de opeenvolgende waarden uit de argumentenlijst
>  een voor een toegewezen aan de positionele parameters. Het gebruik van het
>   dubbele streepje wordt hierbij aangeraden om problemen met opties (d.w.z.
>   argumenten die met een streepje beginnen) te vermijden.
>- b. Omdat set -- ... de oorspronkelijke positionele parameters overschrijft, is het
>  doorgaans **beter** om een **array** te gebruiken om operaties op positionele parameters
>   uit te voeren.
> - c. Met **shift n** wordt de **inhoud** van alle **positionele parameters** i **vervangen** door de
>  oorspronkelijke inhoud van parameters i + n. Hierbij gaan de eerste n waarden
>   verloren. De standaardwaarde van n is 1; **standaard wordt dus één plaats**
>   **opgeschoven**.



69. > Hoe kun je in een shellscript het dertiende argument aanspreken?

    ```bash
    ${13} #vanaf $10 met accolades
    
    # $# om het aantal parameters te checken 
    # $@ alle parameters in 1 string
    ```

    

70. >Veronderstel dat een variabele x als **waarde** de index van een **positionele parameter**
    >bevat. Hoe kun je de waarde van deze **positionele parameter** bekomen?

```bash
#${!x}

#script
#!/bin/bash
echo ${@} #alle params printen
x=2
echo "$2"
echo ${!x}

#output
[root@localhost bash]# bash pos.sh een twee drie
een twee drie
twee
twee
```

71. >Gebruik het script dat 3 argumenten verwacht. Hoe kun je bij het aanroepen van dit
    >script enkel het eerste en derde argument opgeven?

```bash
bash 71.sh 1 "" 3
```

72. >In Bash zijn speciale variabelen gedefinieerd, waarvan men in shellscripts gebruik kan
    >maken. Lees de sectie Special Parameters in man bash. Zo staat **$0** voor de **naam van het**
    >**script**, **$$** voor het (unieke) proces-ID of **PID** van het script en **$#** voor het aantal
    >argumenten ervan.
    >Schrijf een script dat zijn eigen naam en proces-ID uitschrijft, evenals zijn totale aantal
    >argumenten, gevolgd door het eerste en het laatste argument.

```bash
#!/bin/bash
aantal=$#
echo naam:${0} pid:$$ aantal params:$aantal
echo eerste:${1} en laatste:${!aantal}                                     
```

```bash
[root@localhost ~]# bash para.sh a b c d e f g
naam:para.sh pid:3299 aantal params:7
eerste:a en laatste:g
```

73. >Verder bevatten de shellvariabelen $* en $@ alle argumenten van het script als één
    >string. Hoe kun je deze gebruiken om, na bijvoorbeeld één of meerdere shift-opdrachten,
    >weer de oorspronkelijke toestand van de positionele parameters te bekomen?

```bash
#!/bin/bash
temp="$@" 	#Initiele parameters bewaren
while [[ -n "$1" ]];
do
        echo $1
        shift
done
set -- $temp #Parameters terug resetten na het shiften. (positionele parameters terug invullen)
```

```bash
[root@localhost ~]# bash 73.sh {0..5}
0
1
2
3
4
5
```

74. >Tussen **$*** en **$@** bestaat een subtiel verschil, dat men in shellscripts dikwijls nuttig kan
    >aanwenden, vooral in **combinatie** met **for- en while-lussen**. Maak de volgende twee
    >scripts:
    >74a 74b
    >Roep vervolgens 74a op met minimum twee argumenten.
    >
    >**Verschil $* en $@**:
    >
    >***** Expands  to  the positional parameters, starting from one.  When the expansion is
    >
    >**not within double quotes**, each positional parameter expands to a  separate  word
    >
    >In contexts where it is performed, those words are subject to further word split‐
    >
    >ting and pathname expansion.  When the expansion occurs within double quotes,  it
    >
    >expands  to a single word with the value of each parameter separated by the first
    >
    >character  of  the  IFS  special  variable.   That  is,  "$*"  is  equivalent  to
    >
    >**"$1c$2c..."**, where c is the first character of the value of the IFS variable.  If
    >
    >IFS is unset, the parameters are separated by spaces.  If IFS is null, the 
    >
    >param‐eters are joined without intervening separators.
    >
    >**Geen dubbele quotes? woord voor woord** $1c $2c...
    >
    >**Wel dubbeke quotes? 1 woord -> aan elkaar geplakt ** "$1c$2c..."
    >
    >
    >
    >**@**      Expands  to the positional parameters, starting from one.  In contexts where word
    >
    > **splitting** is performed, this expands each  positional  parameter  to  a  separate
    >
    > word; if not **within double quotes**, these words are subject to word splitting.  In
    >
    >contexts where word splitting is not performed, this expands  to  a  single  word
    >
    >with  each  positional parameter separated by a space.  When the expansion occurs
    >
    >within double quotes, each parameter expands to a separate word.  That  is,  "$@"
    >
    >is  equivalent  to  "**$1" "$2"** ...  If the double-quoted expansion occurs within a
    >
    >word, the expansion of the first parameter is joined with the beginning  part  of
    >
    >the  original  word,  and  the expansion of the last parameter is joined with the
    >
    >last part of the original word.  When there are no  positional  parameters,  "$@"
    >
    >and $@ expand to nothing (i.e., they are removed).



```bash
#!/bin/bash

IFS=-
echo "$*"
IFS=$' \r\n'

for i in "$@"; do #dubbele quotes zijn nodig wanneer er spaties staan tussen argumenten (bijna altijd dus)
        echo $i
done
```

```bash
[root@localhost ~]# bash 74.sh a "hello world"
a-hello world
a
hello world
```

75. >Wat geldt voor scripts, geldt ook voor functies. Een functie heeft dus net zoals een script
    >een **exit-status**. De return-opdracht zal bij een bash-functie echter de exit-status
    >beïnvloeden en dus in tegenstelling tot wat je verwacht niet de teruggeefwaarde
    >bepalen. Wil je iets teruggeven, gebruik dan bij het aanroepen van een functie **command**
    >**substitution** en binnen de functie echo/printf. Schrijf een niet-recursieve functie die de
    >faculteit van een getal dat als parameter wordt meegegeven, teruggeeft.

```bash
#!/bin/bash
#exit status van een proces (functie) is altijd een getal tussen 0 en 255

faculteit(){
	res=1
	for((i=$1;i>1;i--));do
		((res*=i))
	done
	echo $res
}

echo Faculteit van $1 is $(faculteit $1) #command substitutie
```

```bash
[root@localhost ~]# bash 75.sh 5
Faculteit van 5 is 120
```

76. >Een functie kan ook uitvoerparameters simuleren. Schrijf een functie wissel die twee
    >scriptparameters van waarde omwisselt.

```bash
#!/bin/bash

wissel(){
	local temp1=$1
	local temp2=$2
	eval "$1=${!temp2} $2=${!temp1}"
}

a=7
b=12

wissel a b  #opgelet, hier geen $-tekens gebruiken!
printf "%d %d \n" $a $b
```



### Parameter expansion

>In de volgende oefeningen leren we een aantal **interessante bewerkingen** om **parameters** te
>**manipuleren**. Het begrip parameter slaat op alle positionele parameters en op alle
>variabelen (shellvariabelen of andere). De reeds gekende positionele parameters $1, $2 enz.
>vormen een belangrijke uitzondering: deze kunnen enkel worden gewijzigd d.m.v. set.
>Verdere mogelijkheden zoek je op in de sectie Parameter Expansion van man bash.



77. >De bijzondere notaties ${variabele=waarde} en ${variabele-waarde} bieden een snelle
    >oplossing voor het toewijzen of opvragen van een waarde aan een variabele indien die
    >nog niet gedefinieerd zou zijn.
    >Indien een **variabele** wel **gedefinieerd** is, **maar leeg**, dan biedt deze notatie geen
    >oplossing. Welk alternatief heb je hiervoor, dat beide situaties aankan? Schrijf deze zo
    >compact mogelijk.

```bash
#!/bin/bash
x=""
: ${x:=7} #als variabele x niet bestaat (leeg is), dan is x gelijk aan 7
echo $x
```

78. >Schrijf een shellscript dat de **laatste aantal lijnen** van het bestand .bash_history in je
    >home directory naar standaarduitvoer uitschrijft. De waarde van aantal wordt als enige
    >argument meegegeven. Indien deze waarde ontbreekt, moeten er **10** lijnen
    >uitgeschreven worden. Gebruik het commando **tail**.
    >
    >Met een goed gekozen delimiter kun je een string in stukken **splitsen**. In een aantal
    >toepassingen is dit niet voldoende of minstens zeer onhandig.
    >Bash kent een beperkt aantal stringoperatoren. Deze stringoperatoren laten o.a. toe de
    >lengte van variabelen/parameters te bepalen, en substrings die beantwoorden aan bepaalde
    >patterns uit variabelen/parameters te verwijderen. De patterns zijn beperkt (helaas zonder
    >regular expressions), maar mogen ook variabelen bevatten.
    >
    >**Bash v1-compatibele manipulaties**
    >${#variabele} geeft de **lengte** van de waarde van de variabele in karakters
    >${variabele#pattern} **verwijdert de kortst mogelijke substring** **vooraan** de variabele
    >die aan het pattern voldoet
    >${variabele##pattern} **verwijdert de langst mogelijke substring** **vooraan** de variabele
    >die aan het pattern voldoet
    >${variabele%pattern} **verwijdert de kortst mogelijke substring** **achteraan** de
    >variabele die aan het pattern voldoet
    >${variabele%%pattern} **verwijdert de langst mogelijke substring** **achteraan** de
    >variabele die aan het pattern voldoet
    >**Vereisen minimaal Bash v2**
    >${variabele:offset} geeft de **deelstring** vanaf positie offset.
    >${variabele:offset:length} geeft de **deelstring** vanaf positie offset met length tekens.
    >${variabele/pattern/string}
    >geeft de string die ontstaat als je in de variabele de eerste en
    >langste substring die aan pattern voldoet, vervangt door
    >string.
    >${variabele//pattern/string} **geeft** de **string** die ontstaat als je in de variabele alle
    >substrings die aan pattern voldoen, vervangt door string.
    >${variabele/#pattern/string} **geeft** de **string** die ontstaat als je de langste substring vooraan
    >de variabele, die aan pattern voldoet, vervangt door string.
    >${variabele/%pattern/string}
    >geeft de string die ontstaat als je de langste substring
    >achteraan de variabele, die aan pattern voldoet, vervangt
    >door string.
    >**Vereisen minimaal Bash v4**
    >${variabele^} converteert de eerste letter van de string naar uppercase
    >${variabele,} converteert de eerste letter van de string naar lowercase
    >
    >${variabele^^} converteert de volledige string naar uppercase
    >${variabele,,} converteert de volledige string naar lowercase
    >Alle uitleg hierover vind je in info bash of man bash, sectie Parameter Expansion.

```bash
#!/bin/bash
tail -n ${1:-10} ~/.bash_history #als param 1 niet bestaan, neem dan 10 als waarde
```

79. >Vul een variabele x op met de waarde /usr/share/emacs/24.5/etc/tutorials/TUTORIAL.nl.
    >Met welke stringoperatoren kun je x opsplitsen in een directorypad en een
    >bestandsnaam? Los dit op twee manieren op.
    >Hoe kun je deze twee substrings toekennen aan de variabelen dir en file?

```bash
#!/bin/bash
x="/usr/share/emacs/24.5/etc/tutorials/TUTORIAL.nl"
printf "directory=%s bestandsnaam=%s\n" ${x%/*} ${x##*/}


${variabele##pattern} verwijdert de langst mogelijke substring vooraan de variabele
${variabele%pattern} verwijdert de kortst mogelijke substring achteraan de variabele die aan het pattern voldoet
```

80. >Vul een variabele x op met de regel "dit is een <b>eenvoudige</b> en <b>nuttige</b>
    >oefening". Gebruik de stringoperatoren om de woorden eenvoudige en nuttige uit de
    >variabele te halen. Probeer dit op twee methodes.

    ```bash
    #!/bin/bash
    x='dit is een <b>eenvoudige</b> en <b>nuttige</b> oefening'
    
    #met Bash v1
    temp=${x%%</*} 			#verwijdert de langst mogelijke substring achteraan de variabele die aan het pattern </* voldoet
    						#verwijdert dus "</b> en <b>nuttige</b> oefening" => "dit is een <b>eenvoudige"
    echo $temp
    
    
    vet1=${temp#*>}			#verwijdert de kortst mogelijke substring vooraan de variabele die aan het pattern *> voldoet
    						#verwijdert dus "dit is een <b>" => "eenvoudige"
    echo $vet1
    
    
    rest=${x##*$vet1}		#verwijdert de langst mogelijke substring vooraan de variabele die aan het pattern *eenvoudige voldoet	.
    						#verwijder dus "dit is een <b>eenvoudige" => "</b> en <b>nuttige</b> oefening'"
    echo $rest
    
    temp=${rest%</*}		#verwijdert de kortst mogelijke substring achteraan de variabele die aan het pattern </* voldoet
    vet2=${temp##*>}		#verwijdert de langst mogelijke substring vooraan de variabele die aan het pattern *> voldoet
    echo "$vet1 *** $vet2"
    
    #vanaf Bash v2
    temp=${x/<\/b>*/""}		#geeft de string die ontstaat als je in de variabele de eerste en langste substring die aan pattern </b> voldoet, vervangt door string "".
    vet1=${temp/*<b>/""}		#geeft de string die ontstaat als je in de variabele de eerste en langste substring die aan pattern *<b> voldoet, vervangt door string "".
    temp=${x/*<b>/""}		
    vet2=${temp/<\/b>*/""}
    echo "$vet1 *** $vet2"
    ```
    
    
    
81. > Indien je in de stringoperatoren de variabele $@ of $* gebruikt, kun je op een relatief
    >eenvoudige manier de laatste positionele parameter opvragen met:
    >**echo ${@:$#:1}**
    >Hoe vraag je op een analoge manier de voorlaatste positionele parameter op?

```bash
#!/bin/bash

${@: -1:1} #laatste param
${@: -2:1} #lvooraatste param

echo "Laatste: ${@:$#:1}"  #van $@ (alle positionele parameters) vertrek je van offset $# (index van laatste pos par) en neem je 1 pos

echo "Voorlaatste: ${@:$#-1:1}"
echo "Twee laatste: ${@:$#-1:2}"
echo "Andere manier voorlaatste: ${@: -2:1}"  # Spatie niet vergeten! . Betekent: van $@ (alle positionele parameters) vertrek je van offset -2 (index van voorlaatste pos par) en neem je 1 pos par
echo "Foute manier voorlaatste: ${@:-2:1}"  # verklaring zie hieronder
echo "Foute manier voorlaatste verduidelijking: ${onbestaandevar:-2:1}"  # zonder spatie heb je ${var:-value} wat betekent "gebruik $variabele; indien niet gedefinieerd of leeg, gebruik waarde"
```



82. >Los vorige vraag op door gebruik te maken van:
    >
    >1. het mechanisme van indirecte adressering en
    >2. de opdracht eval.
    
    

```bash
#!/bin/bash

#1
x=$(($#-1))
echo ${!x}

#2
eval echo '$'$(($#-1))
```



### Arrays

83. >Vanaf versie 2 kent Bash arrays of tabellen. Helaas kunnen deze in Bash v2 en Bash v3
    >enkel met niet-negatieve (64-bit) integers geïndexeerd worden. Bash v4 laat associatieve
    >arrays toe, vergelijkbaar met de hashes van Perl. Lees de sectie Arrays in man bash of
    >info bash. Om de mogelijkheden van (niet-associatieve) arrays verder uit te diepen, maak
    >je een array waarbij de gebruikte indices elkaar niet numeriek opvolgen, bijvoorbeeld:
    >data=( 0 1 2 3 4 )
    >data[20]=20
    >declare -p data # ter controle
    >grep ^data= < <(set) # alternatieve controle
    >Vraag volgende informatie op, telkens met één statement:
    >• **alle getallen van deze array**
    >• **het aantal getallen in de array**
    >• **het getal met index 2 uit de array**
    >• **het getal met index 5 uit de array** (is leeg in ons voorbeeld)
    >• **het getal met index 20 uit de array** (=20)
    >Pas deze vragen eveneens toe op de builtin array **BASH_VERSINFO**.

```bash
#!/bin/bash
data=(0 1 2 3 4)
data[20]=20
echo Alle getallen: ${data[@]}
echo Aantal getallen: ${#data[@]}
echo Getal met index 2: ${data[2]}
echo Getal met index 5: ${data[5]}  
echo Getal met index 20: ${data[20]}
```

84. >Getallen op een bepaalde positie (≠ index) in een array a kun je opvragen door de
    >volledige array a[@] door te geven aan de slice-operatie ${variable:offset:length}.
    >Herneem de vorige oefening en bepaal in één statement
    >• het getal op positie 2 in de array
    >• het getal op positie 5 in de array
    >• het getal op positie 20 in de array (onbestaand)
    >• het laatste getal uit de array

```bash
#!/bin/bash
data=(0 1 2 3 4)
data[20]=20
echo "Fout: $data[1]"
echo "Juist: ${data[1]}"

echo Alle getallen: ${data[@]}
echo Aantal getallen: ${#data[@]}
echo Getal met index 2: ${data[2]}
echo Getal met index 5: ${data[5]}  
echo Getal met index 20: ${data[20]}

echo Getal op positie 2: ${data[@]:2:1}
echo Getal op positie 5: ${data[@]:5:1}
echo Getal op positie 20: ${data[@]:20:1}
echo Laatste getal: ${data[@]:${#data[@]}-1:1}  # of ${data[@]: -1:1}
```

85. >Je kunt een array ook initialiseren met de uitvoer van een commando. Wat is de inhoud
    >van regel indien je volgende toekenning uitvoert (zonder IFS te wijzigen)?
    >regel=( $(wc /etc/passwd) )

```bash
#!/bin/bash
regel=($(wc /etc/passwd))
echo "regel[0]: ${regel[0]}"
echo "regel[1]: ${regel[1]}"
echo "regel[@]: ${regel[@]}"
declare -p regel #toont info over variabele (wat er in zit)
grep ^regel= < <(set) #geeft ook value van de variable weer
```

86. > Hoe vraag je de bestaande indices van een array op? Hoe genereer je hieruit een tweede
    > array, geïndexeerd door opeenvolgende gehele getallen en met als waarden de indices
    > van een eerste? Pas toe op de array uit vorige oefening, en op de builtin array
    > BASH_VERSINFO.

```bash
#!/bin/bash
data=(a b c d e)
data[20]=z
echo data: ${data[@]}
echo indices: ${!data[@]}
indices=(${!data[@]})
echo indices in een array: ${indices[@]}
echo
echo BASH_VERSINFO: ${BASH_VERSINFO[@]}
echo BASH_VERSINFO indices: ${!BASH_VERSINFO[@]}
```

87. >Schrijf een script met als naam weekdag dat als enig argument een getal meekrijgt (0
    >t.e.m. 6) en de corresponderende weekdag (in het Nederlands) uitschrijft. De waarde 0
    >komt hierbij overeen met zondag.
    >Met welke parameter kun je dit script gebruiken om de weekdag van vandaag te
    >bekomen?

```bash
#!/bin/bash
dagen=( zondag maandag dinsdag woensdag donderdag vrijdag zaterdag )
echo ${dagen[$1]}

#met als parameter $(date '+%w')
```





### Herhalingsinstructies Output van een commando verwerken in een script



Dikwijls bestaat de uitvoer van een commando uit één regel, waarvan je slechts het deel, dat
je nodig hebt in je script wilt opslaan in een variabele. Dit kan op diverse manieren:
• Gebruik **cut** met een gepaste **delimiter**. Deze kan echter slechts uit één teken
bestaan. Standaard is de delimiter voor dit commando een tabkarakter.
• Sla de volledige regel op in een variabele en gebruik **stringoperatoren** om het
interessante deel af te zonderen.
• Gebruik de opdracht **read**, die – op basis van IFS – een regel opsplitst en de delen
ervan aan **variabelen** toekent. De inputregel moet hierbij komen van
standaardinvoer. Indien de invoer doorgepipet wordt, dan zijn de variabelen enkel
gekend in de nieuwe shell.
• Gebruik **arrays** om de alle delen van de regel op te slaan in arrayelementen – alweer
op basis van IFS – en verwijs met de juiste indices naar de gewenste delen.
De variabele IFS is standaard ingesteld op whitespace, dus spaties, tabs en regeleinden. Je
kunt deze echter ook zelf wijzigen, zowel interactief als binnen een script; in dit laatste geval
is de wijziging enkel van kracht binnen het script.



**Om niet telkens de standaardwaarde $' \t\n' opnieuw te moeten typen, zou je IFS**
**eventueel kunnen kopiëren naar een hulpvariabele. Een betere oplossing bestaat er in om**
**een aparte functie te voorzien of om de IFS-variabele enkel te wijzigen voor de huidige**
**regel. Op die manier kan je enkele geheugenreferenties uitsparen!**



In een script kunnen if-testen dikwijls vervangen worden door alternatieven op basis van de
**&&- en/of ||**-operatoren. Maak daar nuttig gebruik van om je code bondig te houden.



89. >Ontwikkel een shellscript dat als (enige) parameter een **bestandsnaam** heeft. Als output
    >moet het script het **gemiddelde aantal karakters per regel en het gemiddelde aantal**
    >**woorden per regel uitschrijven**. Gebruik de output van het commando **wc** en probeer
    >met de diverse methodes die hierboven aangehaald werden (behalve de tweede) om
    >deze output op te **splitsen**.
    >Opgelet: de shell behandelt alle getallen als integers. Niettemin kun je er, met behulp
    >van wat wiskunde, voor zorgen dat delingen correct worden afgerond. Hoe?



```bash
#!/bin/bash

if (($#!=1));then 						#geen bestand opgegeven of te veel paramters.
	echo geen parameter meegegeven! >&2 #file descriptor 2. Foutmelding
	exit 1
fi

if [[ ! -f "$1" ]]; then
	echo $1 is geen bestand >&2
    exit 1
fi

#array( $(wc "$1") )
read lijnen woorden kars naam < <(wc "$1")
echo gemiddeld aantal woorden per lijn: $((woorden/lijnen))
echo gemoddeld aantal karakters per lijn: $((kars/lijnen))
```



90. >Wat moet je doen opdat de read-instructie lijnen niet alleen in woorden zou opsplitsen
    >op basis van spaties, tabs en regeleinden, maar ook op basis van **:-tekens**?

```bash
IFS=: read a b > /etc/passwd
```



91. >Ontwikkel een script om de **gebruikersnaam** (veld 1 van /etc/passwd) te bepalen aan de
    >hand van een **gebruikers-ID** (veld 3 van /etc/passwd) dat je als (enige) parameter aan het
    >script meegegeven hebt.
    >Je kunt de output van het commando grep zowel met **cut**, **read** als met een **array**
    >analyseren.

```bash
#!/bin/bash
if (($#!=1));then
	echo Fout bij parameters! >&2
	exit 1
fi

if [[ "$1" =~ "^[0-9]+$" ]]; then
	echo $1 stelt geen getal voor >&2
	exit 1
fi

grep -E "^.*:x:$1" /etc/passwd | cut -d : -f1 	#begin lijn, gevolgd door 0 of meer random tekens, 
							   					#gevolgd door :, gevolgd door x, gevolgd door :, 
							   					#gevolgd door getal $1, gevolgd door :.
```



### Lussen: while en until

Met een lus kan je een bepaald deel van het script herhalen zolang de exit status van een
commando waar is. Je kunt hierbij het test-commando gebruiken, maar ook een read-
commando, of om het even welk ander commando, of zelfs gegroepeerde commando's
(tussen ronde haakjes of accolades, of een pipe).
Als de exit status gelijk is aan 0 (waar), worden de opdrachten tot de afsluitende done
uitgevoerd, waarna de voorwaarde-opdracht weer aan de beurt is. Wanneer de lus niet
doorlopen wordt, is de exit status van de lus 0. Wanneer de lus wel doorlopen wordt, is de
exit-status van de lus gelijk aan de exit status van de laatste opdracht die binnen de while-lus
uitgevoerd werd. De until-lus is functioneel gelijk aan de while-lus, maar de exit status van
de voorwaarde wordt geïnverteerd.

**while**

```bash
while *commando* ; do  (zolang exitstatus 0 is)
...
done
```
**for**
```bash
for i in ... ; do
...
done
```
**testen**
```bash
testen op getallen: ((i<10))
testen op string [[ "$i" == "hallo"]]
testen of het een bestand is [[ -f "$1"]]
testen als var niet bestaat [[ -z "$1"]]
testen als var wel bestaat [[ -n "$1"]]
```
**if**
```bash
if *commando*
then ...
elif *commando*
then ...
fi
```

**Examenvragen vorige jaren:**

```bash
Schrijf eigen versie van commando du
Schrijf eigen versie van commando wc -l
```



92. >Ontwikkel een script dat het commando **tail** n simuleert. Als eerste argument moet een
    >bestandsnaam opgegeven worden en als tweede argument mag het aantal regels
    >opgegeven worden. Ontbreekt het tweede argument, dan worden de 10 laatste regels
    >weergegeven. Realiseer dit op twee manieren:
    >• Gebruik een while-lus met een read-commando om het bestand te overlopen en
    >een array om de gegevens cyclisch op te slaan.
    >• Gebruik geen array, maar bepaal vooraf het aantal lijnen van het bestand.

    

```bash
#!/bin/bash



#(( $# >= 1 )) || { echo verkeerd aantal parameters >&2 ; exit 1 ; }
if (($#!=1 && $#!=2));then 
	echo verkeerd aantal parameters >&2
	exit 1
fi


#[[ -f "$1" ]] || { echo $1 is geen bestand  >&2  ; exit 1 ; } 
if [[ ! -f "$1" ]];then 
	echo $1 is geen bestand >&2
	exit 1
fi



aantal=${2-10}				#${parameter-value}: gebruik parameter $2 als die bestaat, zoniet gebruik value 10
tel=0
while IFS='' read lijn ; do		# while lus om file in te lezen regel per regel in $lijn, IFS='' zorgt dat witruimte vooraan niet wordt weggelaten
    tot[tel % aantal]=$lijn		# $lijn kopieren naar array tot op positie: tel modulo aantal
    (( tel++ ))
done < "$1"


(( aantal <= tel )) || aantal=$tel	# als aantal>tel (maw er zijn minder lijnen in de file dan gevraagd), wordt aantal ingesteld op aantal lijnen in file (huidige teller)

i=0				
while (( i < aantal )) ; do		#while lus om de aantal lijnen, opgeslagen in tot, weer te geven
    echo "${tot[(tel + i) % aantal]}"
    (( i ++ ))
done
```



93. >Hoe kun je met behulp van de while- of until-lus een aantal commando's oneindig lang
    >laten uitvoeren? Onderbreek de uitvoering met Ctrl+C.

```bash
while : ; do : ; done
```

94. >Het bestand ping.out bevat de output van een Windows batch file:
    >ping -n 1 AL005951
    >ping -n 1 AL005952
    >...
    >Indien toestel xxxxxxxx actief is, wordt het commando ping beantwoord met regels van
    >de vorm:
    >**Pinging xxxxxxxx [141.96.126.137] with 32 bytes of data:**
    >**Reply from 141.96.126.137: bytes=32 time=1322ms TTL=124**
    >Je kunt niet-actieve toestellen herkennen aan het feit dat het commando niet wordt
    >beantwoord zoals bij actieve. De **foutboodschappen** die dan gegenereerd worden zijn
    >divers. Maak een Bash-script dat uit ping.out een inventaris opmaakt van **alle niet-**
    >**actieve toestellen** (één lijn per toestel). Het script moet ook een samenvattende regel
    >weergeven die zowel het aantal actieve als het totaal niet-aantal toestellen vermeldt.
    >Zorg ervoor dat het script onafhankelijk is van de precieze foutboodschappen die niet-
    >actieve toestellen produceren. Construeer twee oplossingen, al dan niet gebruikmakend
    >van associatieve arrays (enkel beschikbaar in Bash v4).

```bash
#!/bin/bash

declare -A array #associatieve array (=dictonaiy) = hash table

while read lijn; do
	if [[ "$lijn" =~ ^Pinging ]]; then #als lijn start met "Pinging"
		read pinging comp rest <<< "$lijn" #lezen van string <<<, lezen van bestand <	
		array["$comp"]="request timed out" #sleutel moet sowiso een waarde bevatten
	fi
	if [[ "$lijn" =~ ^Reply ]]; then
		unset array["$comp"] #laatstse keer da comp variabele is ingevuld er uit gooien.
	fi
done < ping.out

for i in ${!array[@]}; do
	echo $i ${array[$i]} #request timed out
done
```

95. >Gebruik (enkel) het bestand /etc/passwd om voor alle **groepsnummers** het aantal
    >**gebruikers** met **hetzelfde primaire groepsnummer** te **tellen**. Realiseer dit op twee
    >manieren:
    >• Gebruik een while-lus met een read-commando om het bestand te overlopen
    >en arrays om de gegevens op te slaan.
    >• Sla eerst de gegevens geordend op in een tijdelijk bestand, en verwerk
    >vervolgens dit bestand.

```bash
#!/bin/bash

declare -A array #associatieve array = hash table

cd #zorgen dat we op het juiste pad zitten

while read lijn; do
    IFS=':' 
    read naam x uid gid rest <<< "$lijn"
    if [[-z ${array[$gid]} ]]; then
        array[$gid]=1
    else
        ((array[$gid]++))
    fi
done < /etc/passwd

for i in ${!array[@]}; do
    echo $i ${array[$i]};
done
```

96. >Gebruik de bestanden **/etc/group** en **/etc/passwd** om een overzicht te maken van alle
    >groepen, gevolgd door de volledige lijst van gebruikers die deze groep als primaire groep
    >hebben. Gebruik een while-lus met een read-commando om het bestand /etc/group te
    >overlopen en grep om de gebruikers op te sporen

```bash
#!/bin/bash

while IFS=: read naam x gid rest ; do
	array=( $(grep -E "^.*:x:.*:$gid:" /etc/passwd | cut -d : -f1) )
	echo "$naam: ${array[@]}"
	unset array #tabel terug leegmaken om geheugen vrij te maken
done < /etc/group
```



### De for-lus

> **extra info:**

> **declare -a array**:  declaratie numeriek geassocieerde array  (array=() werkt ook)
> **declare -A array**:  declaratie string geassocieerde array 
>
> **[[ -n "${ array["$i"] }" ]]** checken of inhoud non-zero is
>
> **[[ -z "${ array["$i"] }" ]]** checken of inhoud 0 (zero/leeg) is
>
> **$** staat voor "vervang door"



100. >Ontwikkel een script dat **alle parameters uitschrijft** die **meer dan één keer**
     >**voorkomen in de argumentenlijst** van het script. De volgorde waarin de minstens dubbel
     >voorkomende parameters worden uitgeschreven heeft geen belang (sorteren mag),
     >maar je moet er wel voor zorgen dat parameters die meer dan twee keer voorkomen
     >toch slechts eenmaal weggeschreven worden. Laat als eerste parameter ook eventuele
     >opties -i of -I (van ignore case) toe, die desgewenst aangeven dat er geen onderscheid
     >mag gemaakt worden tussen hoofdletters en kleine letters.
     
     > Extra info oefening 100:
     >
     > **cmd1 && cmd2** : als cmd1 niet lukt zal cmd2 niet uitgevoerd worden. = Logische AND voor exit statusen.
     >
     > **cmd1 || cmd2** : als cmd1 niet lukt zal cmd2 WEL uitgevoerd worden. 
     >
     > **&&** heef prioriteit boven **||**
     >
     > **${i,,}** -> ,, = to_lowercase
     >
     > **${i,}** -> , =enkel Eerste letter to_lowercase
     >
     > **${i^^}** -> ^^ = to_uppercase
     >
     > **${i^}** -> ^ =enkel Eerste letter to_uppercase
     >
     > *meer info? man bash -> /parameter expansion*
     
     

```bash
#!/bin/bash

declare -A params #string geindexeerde tabel = dictionary

if [[ "$1" == "-i" || "$1" == "-I" ]]; then
	ic=1
fi

for i in "$@" ; do
	if ((ic==1)); then
    	[[ -z ${params["${i,,}"]} ]] && param["${i,,}"]=1 || ((params["${i,,}"]++)) 
    fi
    else
        [[ -z ${params["$i"]} ]] && param["${i}"]=1 || ((params["${i}"]++))
done  

for i in "${params[@]}";do
	(($params["$i"] > 1)) && echo $i
done
```



101. >Ontwikkel een script dat een beperkte versie van het commando **wc** simuleert. Het
     >script moet het **aantal regels** en de **bestandsnaam** afdrukken **van elk bestand dat als**
     >**parameter meegegeven wordt**. Het script mag enkel interne Bash-instructies (if, for,
     >case, let, while, read enz.) gebruiken, en behalve echo geen externe commando's; het
     >gebruik van **awk, sed, perl en wc in het bijzonder is niet toegelaten**. Je zult bijgevolg elk
     >bestand regel voor regel moeten inlezen en deze tellen. Het script moet bovendien een
     >samenvattende regel weergeven met het **totale aantal regels**. **Indien geen enkele**
     >**parameter meegegeven wordt, neem je alle bestanden in de huidige werkdirectory in**
     >**beschouwing**. Los dit zo beknopt mogelijk op met de speciale notaties voor shell-
     >variabelen



````bash
#!/bin/bash

tot_lijnen=0
tot_woorden=0
tot_kars=0

files=( ${@:-*} ) #korte notatie van 
				#if [[ -z "$@" ]]; then 
					#files=( $@ ) 
				#else 
					#files=( * ) 
				#fi

for file in "${files[@]}";do
	#[[ -f "$file" ]] && continue; 	#check of bestand bestaat. korte notatie
    								#&& = Als eerste commando true is zal het 2de ook uitgevoerd worden.
   
   if [[ ! -f "$file" ]];then  #lange versie
   		echo $file is geen bestand
   		continue
   	fi
   	
    lijnen=0
    woorden=0
    kars=0
    while read lijn; do
    	((lijnen++))
    	temp=( $lijn )
    	((woorden+=${#temp[@]}))
    	unset temp #tijdelijke table vernietigeng
    	((kars=kars${#lijn}+1)) #+1 voor \n character
    done < "$file"
    ((tot_lijnen+=lijnen))
    ((tot_woorden+=woorden))
    ((tot_kars+=kars))
    printf "%4d %4d %4d %s" $lijnen $woorden $kars "$file"
done	

printf "%4d %4d %4d %s" $tot_lijnen $tot_woorden $tot_kars $total
````



103. >Enerzijds kun je met behulp van het commando **ps -e** informatie opvragen over alle
     >processen die actief zijn. De **vier kolommen** in de output tonen respectievelijk het
     >proces-ID (**PID**), de **TTY** device file van de (pseudo-)terminal, de **CPU** time, en het
     >**commando** dat het proces opgestart heeft. Anderzijds kun je met behulp van het
     >commando kill -**KILL** pid een proces met willekeurig proces-ID afbreken. Ontwikkel een
     >**script** dat **alle processen afbreekt** waarvan het commando **één van de strings bevat die**
     >**als parameters bij het oproepen** van het script meegegeven wordt. Indien **geen enkele**
     >**parameter** meegegeven wordt, moet het script een **gesorteerde lijst weergeven van alle**
     >**unieke commandonamen** van actieve processen. Behalve de interne instructies (if, for,
     >case, let, while, read enz.) mag je ook de externe commando's grep, sort en uniq
     >gebruiken. Om problemen te vermijden, **schrijf je bij het testen de kill-opdracht uit naar**
     >**standaarduitvoer i.p.v.** deze daadwerkelijk uit te voeren.

     ```bash
     #!/bin/bash
     
     trap 'ls; exit 1' SIGINT #signaal handler. Voer b 'ls; exit 1' uit bij SIGINT signaal
     
     if (($#==0)); then
     	declare -A array
     	eerste=0
     	while read pid tty time cmd;do
     		((eerste==0)) && { eerste=1 ; continue ; }
     		array["$cmd"]=1
     	done < <(ps -e)
     	for i in ${!array[@]}; do
     		echo $i
     	done | sort
     fi
     
     else 
     	eerste=0
     	while read pid tty time cmd;do
     		((eerste==0)) && { eerste=1 ; continue ; }
     		for i in "$@";do
     			[[ "$cmd" =~ $i ]] && echo kill $pid 
     			#kill -9 om te forcen. Dan wordt signaal 9 verstuurd naar het proces met als PID $pid.
     		done
     	done < <(ps -e)
     fi
     ```
     
104. > **WAS EEN VRAAG OP HET EXAMEN VORIG JAAR**
          >
          > Ontwikkel een script dat (zonder getopt te gebruiken) alle **opties die aan het script**
          > **worden meegegeven naar standaarduitvoer wegschrijft**, één per regel. Je moet dus alle
          > karakters die voorkomen in parameters die beginnen met een minteken verzamelen, en
          > deze één voor één verwerken. Bekommer je niet om opties die meerdere keren zouden
          > voorkomen. Voor de argumentenlijst **-Ec -rq /etc/passwd -a** moet het script dus als
          > uitvoer **E, c, r, q** en a produceren.

```bash
#!/bin/bash

while [[ -n "$1" ]]; do #zolang $1 bestaat
	case "$1" in
		-?*)  while read -N1 kar; do										#-teken gevolgd door 1 of meerdere random chars
					[[ "$kar" != $'\n' && "$kar" != "-"  ]] && echo $kar
				done <<< "$1"
				;; #=break
		[!-]*) echo ongeldige optie >&2 									#begint niet met het minteken (is dus geen optie)
			   exit 1
			   ;;
	esac #einde case
	shift #$1 wordt $2
done
```



**handige functies**

```c
int dimension = atoi(argv[1]); //( = Asci To Integer) zet string om naar int
[[ $x =~ "^.$"]] //checken of variabele voldoet aan reguliere expressie
```





**De opdrachten break en continue**



>Lussen kunnen vroegtijdig afgebroken worden met behulp van de instructie **break**. Als de
>shell op een break stuit, dan wordt de huidige for-, while-, of until-lus beëindigd en gaat de
>verwerking verder bij de eerste opdracht na done.
>De **continue**-instructie heeft een vergelijkbare functie. Deze zorgt ervoor dat de volgende
>iteratie van de huidige lus onmiddellijk begint. Als je lussen genest hebt en meer dan één lus
>wilt afbreken, dan kun je break en continue een numerieke parameter meegeven, die duidt
>op het aantal geneste lussen; break 1 en break zijn bijgevolg equivalent.



111. > Ontwikkel een script dat een recursieve versie van het UNIX commando **wc** simuleert. Behalve de interne instructies (if, for, case, let, while, read enz.) mag je ook de externe commando's **echo**, **wc** en **find** gebruiken. Het script kan opgeroepen worden met 0 tot 3 opties (-l, -w en -c, niet noodzakelijk in die volgorde), gevolgd door een willekeurig aantal parameters. Indien er geen enkele optie meegegeven wordt, wordt aangenomen dat alle drie de opties werden vermeld. De parameters kunnen zowel bestandsnamen als namen van directory's zijn; worden geen parameters meegegeven, dan neemt het script de werkdirectory in beschouwing. De optie -l staat voor het afdrukken van het aantal regels,
     -w voor het aantal woorden en -c voor het aantal karakters. Deze aantallen worden
     berekend.
     • voor elk bestand dat als parameter meegegeven wordt,
     • voor elk bestand in de tree van een directory die als parameter meegegeven
     wordt en
     • tot slot voor alle bestanden samen.

```bash
#!/bin/bash

# wordcount recursief schrijven
#trap { rm -f $temp; exit 1; } SIGINT # proberen

function printerr() {
    echo "Usage wc [-l] [-w] [-c] [file|directory] [file2|directory2] ..." >&2 # naar error uitvoer
}

while [[ -n "$1" ]]; do
# hier wordt veronderstelt dat de opties als eerst komen en nadien de bestanden
    case "$1" in
            -l) lijnen=1
                ;;
            -w) woorden=1
                ;;
            -c) kars=1
                ;;
            [^-]*)  break # nu kom je naam van file tegen #[[ ! -f "$1" && ! -d "$1" ]] && {printerr; exit 1; }
                ;;
            -*) printerr # oproepen functie -> geen haakjes
                exit 1
                ;;
    esac
    shift
done

[[ -z $woorden && -z $lijnen && -z $kars ]] && { kars=1; woorden=1; lijnen=1; }

#echo $@
bestanden=${@:-.} # mag geen parameters meer bevatten

temp=$(mktemp 'XXXXXX')

for i in $bestanden; do
    [[ -f "$i" ]] && wc "$i" >> $temp #bij bestanden
    [[ -d "$i" ]] && find "$i" -type f -print0 |xargs -n 1 -0 wc >> $temp #directories. alle bestanden ophalen met find
done

#cat $temp

totaal_lijnen=0
totaal_woorden=0
totaal_chars=0

while read lijn woord chars bestand; do
    ((totaal_lijnen+=lijn))
    ((totaal_woorden+=woorden))
    ((totaal_chars+=chars))
    [[ -n "$lijnen" ]] && printf "%7d" $lijn
    [[ -n "$woorden" ]] && printf "%7d" $woord
    [[ -n "$kars" ]] && printf "%7d" $chars
    printf "%10s\n" $bestand
done < "$temp"

# formatering van de tekst -> printf
[[ -n "$lijnen" ]] && printf "%7d" $totaal_lijnen
[[ -n "$woorden" ]] && printf "%7d" $totaal_woorden
[[ -n "$kars" ]] && printf "%7d" $totaal_chars
printf "%10s\n" total

rm $temp
```



112. >Het bestand pagefile.out bevat de uitvoer van een Windows batch file:
     >dir \\AL005951\c$\pagefile.sys
     >dir \\AL005952\c$\pagefile.sys
     >
     >...
     >Elk van de 2.901 dir-opdrachten werd beantwoord met regels van de vorm:
     >C:\WINDOWS\system32>dir \\AL005951\c$\pagefile.sys
     >Volume in drive \\AL005951\c$ is WINNT
     >Volume Serial Number is D0A0-4386
     >Directory of \\AL005951\c$
     >02/08/00 02:12 146.800.640 pagefile.sys
     >1 File(s) 146.800.640 bytes
     >577.850.880 bytes free
     >De regel met de woorden bytes free vermeldt de beschikbare ruimte op het volume C:.
     >Maak een script dat een tekstbestand genereert met de namen van alle toestellen die
     >minder dan 80 MB vrij hebben op de C: schijf, één per regel.

```bash
#!/bin/bash


while read -r lijn; do # -r negeert de backslash \
    array=($lijn)
    if [[ ${array[0]} =~ ^Directory ]]; then
        comp=${array[-1]}
        comp=${comp%c$}
        comp=${comp//\\/}
        echo $comp;
    fi
    if [[ ${array[2]} =~ "free" ]]; then
        grootte=${array[0]//./}
        if((grootte<80*1024*1024)); then #80 mb
            echo $comp
        fi
    fi
done < pagefile.out

```



## Extra oefeningen booster sessie 3



> Schrijf een C-programma 2.c dat van een **aantal bestanden** de **hexadecimale** uitvoer naar het scherm **schrijft**. De namen van de bestanden worden via de opdrachtlijn meegegeven. Met het minteken, dat slaat op standaard invoer, hoef je geen rekening te houden.
>
> De hexadecimale uitvoer bekom je door elke byte van ieder invoerbestand om te zetten naar twee hexadecimale cijfers. Alle hexadecimale tekens worden na mekaar naar het scherm geschreven.  Wanneer de gebruiker op de opdrachtlijn â€œ./2 bestand1 bestand2â€ intikt, wordt in de veronderstelling dat deze bestanden bestaan, de inhoud van de bestanden bestand1 en bestand2 in hexadecimale vorm naar het scherm geschreven. Wanneer een bestand niet bestaat, wordt er een foutboodschap getoond.

**Invoer omzetten naar binair:**

```c
int main(int argc, char **argv)
{
    unsigned char in = 0x5a;
    unsigned char out[8]; //8 characters

    for (int i = 0; i < 8; i++)
    {
        out[7 - i] = '0' + in % 2; //2=binair
        in /= 2;
    }
    write(1,out,8);
    return 0;
}
```

**Invoer omzetten naar hexadecilaal:**

```c
int main(int argc, char **argv)
{
    unsigned char in = 0x5a;
    unsigned char out[2]; //2 characters

    char omz[16] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};

    out[0] = omz[in % 16]; //16=hexadecimaal
    out[1] = omz[in / 16];

    write(1, out, 2);

    return 0;
}
```

**Omzetten naar octaal**

```c
int main(int argc, char **argv)
{
    unsigned char in = 0x5a;
    unsigned char out[3];  //3 characters

    for (int i = 0; i < 3; i++)
    {
        out[2 - i] = '0' + in % 8; //8=octaal
        in /= 8;
    }
    write(1,out,3);
    return 0;
}
```

**Oplossing**

```bash
#include <unistd.h>
#include <sys/wait.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <sys/mman.h>
#include <semaphore.h>
#include <pthread.h>

int main(int argc, char** argv){
	unsigned char in[BUFSIZ];
	unsigned char out[BUFSIZ*2];
	char omz[16]={'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f'};
	for(int i=1;i<argc;i++){
		int fd=open(argv[i],O_RDONLY);
		if (fd<0){
			perror(argv[i]);
			continue;
		}
		int n=read(fd,in,BUFSIZ);
		while (n>0){
			int teller=0;
			for(int i=0;i<n;i++){
				unsigned char byte=in[i];
				out[teller]=omz[byte/16];
				out[teller+1]=omz[byte%16];
				teller+=2;
			}
			write(1,out,teller);
			n=read(fd,in,BUFSIZ);
		}
		if (n<0){
			perror(argv[i]);
			continue;
		}
		if (close(fd)<0){
			perror(argv[i]);
			continue;
		}
	}
	
	return 0;
}
```





**Opgave 2**



![Imgur](https://imgur.com/ZfYzsgh.png)

```bash
#!/bin/bash

declare -A array

function printErr(){
	echo "Usage ..." >&2
}

function test_s(){
	[[ -n ${array["-s"]} ]] && { printErr ; exit 1 ; }
	array["-s"]=1
}

function test_k(){
	[[ -n ${array["-k"]} ]] && { printErr ; exit 1 ; }
	array["-k"]=1
}

function test_f(){
	[[ -n ${array["-f"]} ]] && { printErr ; exit 1 ; }
	array["-f"]=1
	[[ ! -f "$1" ]] && { printErr ; exit 1 ; } 
}	

function test_p(){
	[[ -n ${array["-p"]} ]] && { printErr ; exit 1 ; }
	array["-p"]=1
	[[ ! $1 =~ ^[0-9]+%$ ]] && { printErr ; exit 1 ; } 
}	

while [[ -n "$1" ]]; do
       case "$1" in 
	       -s|--size) test_s
		          ;;
	       -f|--file) shift
		          test_f "$1"			   	
		          ;;
	       -k|--key) test_k
		          ;;
	       -p)  shift
		    test_p "$1"
		          ;;
	       [^-]*) printErr
		      exit 1
		      ;;
	       -?*) while read -N1 kar;do
		       [[ "$kar" == "-" || "$kar" == $'\n' ]] && continue
		       case $kar in 
			       s)    test_s
			             ;;
			       k)    test_k
				     ;;
			       f)    [[ ! "$1" =~ f$ ]] && { printErr ; exit 1 ; }
				     shift
				     test_f "$1"   
				     ;;
			       p)    [[ ! "$1" =~ p$ ]] && { printErr ; exit 1 ; }
				     shift
				     test_p "$1"
				     ;;
		       esac
		    done <<< "$1" 
		      ;;
       esac
       shift
done	
```

