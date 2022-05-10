# Labo Besturingssystemen



> **Handige links:**
>
> Bash cheatsheet :  https://devhints.io/bash
>
> regex: https://regexr.com/



> **Planning/Verloop Labo's:**
>
> - week 1: **Deel 1**: De terminal, Man pages, **Deel 2**: Compileren in de shell
> - week 2: **Deel 7**: Patterns, expansions
> - week 3: **Deel 7**: Redirection & pipes



## Deel I: Inleiding

Lokaal inloggen op een Linux toestel kan op twee manieren gebeuren. Je kan inloggen op de
grafische console of je kan inloggen op een van de vijf a zes tekstuele consoles. Veranderen
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

```bash 
ctrl+D
```

4. > Wanneer je op de commandolijn een aantal woorden intikt, hoe kan je dan het
   > laatste woord verwijderen?

```bash 
ctrl+W
```

5. > In een shell kan je aan “**auto completion**” doen door gebruik te maken van de
   > tab-toets. Tik de letters “les” in, en tik vervolgens op de tab-toets. Je merkt dat er
   > automatisch less verschijnt. Nu kan het zijn dat er nog opdrachten zijn die met
   > less beginnen. Tik nogmaals op de tab-toets om te kijken welke opdrachten er
   > met less beginnen. Een ander handigheidje is “reverse search” om eerder
   > ingetypte commando’s te suggereren tijdens het typen. Gebruik hiervoor
   > “CTRL+r”.

...

6. >Linux telt enkele duizenden opdrachten met elk nog een variabel aantal opties. De opdracht zelf wordt doorgaans beperkt tot enkele letters die de afkorting vormen van een woord dat de functie van de opdracht deels omschrijft. Zo staat het commando “**ls**” voor “list”, “**mkdir**” voor “make directory”, het commando “**wc**” voor “word count”, het commando “**cc**” voor “C-compiler”, het commando “**dd**“ voor “convert and copy”. Bij het laatste voorbeeld is er een conflict omdat de afkorting cc reeds gebruikt wordt voor de C-compiler. Als oplossing heeft men de volgende letter van het alfabet gebruikt.
   >
   > “Auto completion” voor commando’s werd reeds in het vorige punt naar voor gebracht maar geldt ook voor de bijhorende opties. Geef op de commandolijn het commando “**ls** -“ in en gebruik vervolgens de tab-toets. Je merkt dat er een pak opties verschijnen die voorafgegaan worden door twee mintekens. Onder Linux kan je veelal opties op de commandolijn meegeven in twee formaten. Het korte formaat bestaat uit één letter en wordt voorafgegaan door één minteken. Dezelfde optie kan je ook meegeven d.m.v. het lange formaat. In dat geval zal de optie voorafgegaan worden door twee opeenvolgende mintekens. Wanneer je de keuze hebt tussen de twee formaten zal je merken dat de korte variant de voorkeur geniet. 
   >
   >Zo kan het commando “**wc --words --lines /etc/passwd**” ook geschreven worden als “**wc -w -l /etc/passwd**” en zelfs als “**wc -wl /etc/passwd**”. De opdracht toont het aantal lijnen en het aantal woorden uit het bestand /etc/passwd.

...

#### 2. Gebruik van enkele eenvoudige opdrachten

1. >  Met de opdracht man kan je alle info over een welbepaalde opdracht
   > achterhalen. Zo zal de opdracht “**man ls**” de info tonen van de ls-opdracht.
   > Man toont de informatie a.d.h.v. een pager, een programma dat de informatie
   > niet alleen op het scherm toont maar dat ook gebruikersinteractie toelaat. Zo kan
   > je scrollen, zoeken naar bepaalde woorden, etc. Standaard is de pager ingesteld
   > op het commando **less**. Dit betekent dat wanneer je wil weten hoe je voorwaarts
   > moet zoeken in een manpagina, je dit moet gaan zoeken bij het commando **less**
   > en niet bij het commando man. Vraag de manpagina op van het commando **less**
   > en ga na hoe je een tekst die met less wordt getoond kan afsluiten. Hoe kan je
   > voorwaarts zoeken in een manpagina?

Je kan zoeken naar een bepaalde term door deze als volgt mee te geven: /term. 

```bash	
man ls /term #voorwaarts zoeken
man ls ?term #achterwaarts zoeken
```

Dit commando zal naar "term" zoeken in de man page van **ls**. (`n` om naar het volgende en `shift + n`om naar het vorige resultaat te gaan.)

2. > Hoe kan je zorgen dat er bij het zoeken in een manpagina geen rekening wordt
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
   >commando read. Er is echter ook een systeemaanroep read aanwezig. Hoe kan je
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
   ls -h #toont hidden files
   ```

6. > Bekijk met “ls /” de inhoud van de hoofddirectory.

   ```bash
   root@localhost ~]# ls /
   bin   dev  home  lib64       media  opt   root  sbin  sys  usr
   boot  etc  lib   lost+found  mnt    proc  run   srv   tmp  var
   ```

7. >In punt 5 en 6 heb je gemerkt dat de uitvoer voorzien wordt van kleuren. Zo
   >worden bv. directories in het donkerblauw gekleurd en symbolische links in het
   >lichtblauw. Dit gedrag is te wijten aan het feit dat er voor ls een alias gedefinieerd
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
   [root@localhost tmp]# cd`
   [root@localhost ~]#
   ```

9. >Een directory aanmaken kan via de opdracht “mkdir”. Maak in je home-directory
   >een directory aan met als naam ‘c’ waar je toekomstige C-programma’s naartoe
   >kan kopiëren.

   ...

10. >Een bestand kopiëren gebeurt via de opdracht “cp”. De eerste parameter is de
    >bron, de tweede de bestemming. Een bestand verplaatsen doe je via de opdracht
    >“mv”.

    ...

    

## Deel II:  Compileren in de Shell

In Linux is het vrij eenvoudig om een C of C++ programma te compileren zonder gebruik te
maken van een IDE. Het enige wat je nodig hebt is een eenvoudige tekstverwerker. In een
grafische omgeving kun je bvb. Visual Studio Code, Atom, Neovim gebruiken. In tekstuele
consoles is nano eenvoudig te gebruiken, terwijl vi en vim ... al wat geavanceerder zijn.
Open in BASH een tekstverwerker (nano, vi, vim, neovim, ...) naar keuze en tik daarin
onderstaand codefragment:

```bash
#include <stdio.h>
int main(){
	printf(“Hello world!”);
	return 0;
}
```

Sla dit bestand vervolgens op als hello.**c** (let op de extensie). Om nu dit bestand te
compileren voer je op de commandolijn “**cc hello.c -o hello**” of “make hello” uit. Na het
succesvol compileren kan je bestand uitvoeren door op de commandolijn “**./hello**” in te
tikken. Bemerk dat je voor het uitvoerbaar bestand de “./” niet mag vergeten!
Wanneer je met de opdracht “file” informatie over het uitvoerbaar bestand opvraagt, zal je
merken dat er gebruikgemaakt wordt van shared libraries en dat het uitvoerbaar bestand
dus niet alle code bevat om de string “Hello world!” naar het scherm te schrijven. Is dit niet
de bedoeling, dan kan je bij het compileren de compileroptie “-static” opgeven (installeer
hiervoor de static versie van de C API via yum install glibc-static). Hierdoor wordt alles
statisch gelinkt en krijg je dus een uitvoerbaar bestand dat alle code bevat om de gegeven
tekst naar het scherm te schrijven.

> **extra:**
>
> Compileren naar assembly (test.s): **cc -S test.c**
>
> Compileren naar Object file (test.o): **cc -c test.c**

**Opdracht**

> Compileer bovenstaand bestand dynamisch en statisch en bekijk het verschil in grootte. De
> grootte van een bestand kan je het gemakkelijkst achterhalen met de opdracht “du” of met
> de opdracht “ls”. Maak in beide gevallen handig gebruik van de optie “**-h**“ om de
> bestandsgrootte in bytes, KB, MB, ... te krijgen.

```bash	
gcc -static test.c #statisch. Grotere bestandsgrootte. Te gebruiken wanneer benodigde libraries niet aanwezig zijn op systeem.
gcc -c test.c #dynamic
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

Soms kan het interessant zijn om te weten welke systeemaanroepen een programma
gebruikt. Bekijk de uitvoer van “strace cat /etc/passwd”. Dit geeft een sequentieel overzicht
van alles wat bij het uitvoeren van “cat /etc/passwd” gebeurt. Wanneer je een overzicht wil
krijgen van welke systeemaanroepen er gebruikt worden en hoeveel keer ze werden
opgeroepen, dan kan je aan strace de optie “-c” meegeven.

**Overige interessante hulpprogramma’s**

**nm**
Met het commando nm kan je symboolinformatie opvragen van uitvoerbare bestanden en
libraries. Wil je weten van welke functies de Linux C API (glibc) de uitvoerbare code bevat?
Voer in een terminal dan nm /lib/libc.so.6 uit en alle lijnen waar een t of T bij vermeld staat
zijn C-functies waarvan je de code via deze bibliotheek kan vinden.

**ldd**
Met ldd kan je van ieder uitvoerbaar bestand dat dynamisch gelinkt werkt opvragen van
welke shared libraries het afhankelijk is.

**objdump**
Wil je een uitvoerbaar bestand terug omzetten naar assembleertaal, dan kan je handig
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
> programmeertaal C. Dit commando overloopt alle mogelijke PCI-adressen en gaat na of er
> zich een apparaat bevindt. Bevindt er zich een apparaat, dan wordt het adres (busnummer,
> devicenummer en functienummer) naar het scherm geschreven, samen met het vendorID en
> het deviceID.
> Info en werkwijze
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
gebruik van een **file descriptor**. Een file descriptor is doorgaans een klein positief geheel
getal dat kan verwijzen naar gewone bestanden maar ook naar directories, sockets, pipes, ....
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
geheel getal, de file descriptor dus, teruggeeft of -1 wanneer er een fout optreedt. De eerste
paramater die je moet opgeven is het pad naar het bestand. De tweede parameter bevat
een aantal statusvlaggen die bij het openen van het bestand worden geraadpleegd.
Wanneer je een bestand wil openen om er uitsluitend van te lezen, geef je als flags
“O_RDONLY” op. Wanneer je naar een bestand wil schrijven en er ook van wil lezen is de
flags-parameter gelijk aan “O_RDWR”. Combineren van statusvlaggen gebeurt via de
logische |-operator. Zo kan je een bestand openen om er naar te schrijven en tevens
opgeven dat het moet worden aangemaakt wanneer het niet zou bestaan. De flags-
parameters is in dit geval “O_WRONLY | O_CREAT”. De combinatie “O_WRONLY | O_CREAT
| O_APPEND” betekent dat het bestand zal worden aangemaakt wanneer het niet bestaat,
dat er enkel naar geschreven zal worden en dat alle data die er naartoe wordt geschreven
achteraan zal worden toegevoegd. De O_APPEND vlag verzekert dus dat indien het bestand
reeds zou bestaan, de bestaande inhoud niet zal worden overschreven.
De laatste parameter van de systeemaanroep open is optioneel en is enkel van belang
wanneer de O_CREAT vlag is opgegeven.
Om van een file descriptor te lezen gebruik je de systeemaanroep **read(fd,buffer,count)**.
Buffer is een void-pointer naar een geheugenlocatie waar de gelezen bytes zullen worden
weggeschreven. Count is het aantal bytes die je van de opgegeven file descriptor wil lezen.
De read-systeemaanroep geeft het aantal gelezen bytes terug en -1 wanneer er bij het lezen
een fout optreedt.

Met de **write(fd,buffer,count)** systeemaanroep kan je bytes van een geheugenlocatie naar
een filedescriptor schrijven. De parameters zijn gelijkaardig aan die van de read-
systeemaanroep en ook de return-waarde is hetzelfde, i.e. het aantal weggeschreven bytes
of -1.

Tot slot kan je met de systeemaanroep **close(fd)** een filedescriptor sluiten.

**Opdrachten**

1. > Schrijf een C-programma dat een bestand van ongeveer 10MB aanmaakt met
   > willekeurige lettertekens gelegen in het gesloten interval [a..z].



```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    FILE * fp;
    fp = fopen("output.txt", "w");
    if (fp != NULL)
    {
        for (int i = 0; i < 10000; i++)
        {
            char c = 'a' + rand() % 26;
            fputc(c, fp);
        }
        fclose(fp);
    }
    return 0;
}
```

2. > Tot nog toe werd er niets gezegd over de optimale buffergrootte. De bedoeling is een C-
   > programma te ontwikkelen dat het hierboven aangemaakte bestand verschillende keren
   > inleest en dit met buffergroottes van 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048,
   > 4096 en tot slot 8192 bytes. De uitvoer van het programma moet er ongeveer zo uitzien:

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
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

int main()
{
    FILE *fp = fopen("output.txt", "r");
    int BUF_SIZ = 1;
    if (fp != NULL)
    {
        while (BUF_SIZ < 8192)
        {
            char symbol;
            double start = clock();
            char *buffer = malloc(BUF_SIZ * sizeof(char));
            while ((symbol = getc(fp)) != EOF)
            {
                strcat(buffer, &symbol);
                buffer = realloc(buffer,BUF_SIZ * sizeof(char));
            }
            double time = (clock() - start) / CLOCKS_PER_SEC;
            printf("BUF_SIZ=%d Time=%d", BUF_SIZ, time);
            free(buffer);
            BUF_SIZ *= 2;
        }
        fclose(fp);
    }
    return 0;
}
```

3. > De clock-functie en de macro **CLOCKS_PER_SEC** vind je in de bibliotheek **pthread.h** Doe nu hetzelfde maar voor de write-systeemaanroep. Maak voor iedere verschillende buffergrootte een bestand aan van ongeveer 10MB (cfr. vraag 1). Nadat je de tijd voor een gegeven buffergrootte hebt opgemeten moet je vanzelfsprekend het aangemaakte bestand terug verwijderen. Een bestand verwijderen kan je doen m.b.v. de unlink-
   > systeemaanroep.

```c	
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

int main()
{
    #todo
    return 0;
}
```

4. > Herneem vraag 3 maar voeg aan de flags-parameter de O_SYNC vlag toe. Dit laatste zorgt
   > ervoor dat er noch in USER-mode noch in KERNEL-mode zal worden gebufferd en dat de
   > bytes rechtstreeks naar de schijf zullen worden geschreven.
   > Ter info, de vaste schijf beschikt om performantieredenen over een bepaalde
   > hoeveelheid write-back-cache-geheugen waar gegevens van I/O- schrijfopdrachten
   > tijdelijk worden bewaard. Dit betekent dat er bij een eventuele spanningsonderbreking
   > wel degelijk gegevens kunnen verloren gaan. Bij programma’s, zoals gegevensbanken,
   > waar gegevensverlies nefast is, wordt er aangeraden om “write-caching” uit te
   > schakelen. Dit kan je doen door in een shell de opdracht “hdparm -W0 /dev/sda” uit te
   > voeren.

```c	
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

int main()
{
    #todo
    return 0;
}
```

5. >Bestudeer gronding de werking van de shell-opdracht cat en schrijf in C een eigen versie
   >van cat. Bekijk bv. wat er gebeurt wanneer je de opdracht “cat /etc/passwd - /etc”
   >opgeeft of wanneer cat geen argumenten meekrijgt. Wanneer je een directory opgeeft
   >als argument, geeft cat een foutmelding. Dit gedrag hoef je niet na te bootsen.

```c	
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

int main()
{
    #todo
    return 0;
}
```

6. >Schrijf een eigen versie van de opdracht cp waar twee argumenten op de opdrachtlijn
   >worden verwacht. Het eerste argument is het bronbestand en het tweede het
   >doelbestand. Wanneer de eerste parameter een directory is, wordt een foutboodschap
   >naar het scherm geschreven en stopt het programma met exit-status 1. Wanneer het
   >tweede argument een directory is, wordt opnieuw gestopt met een passende
   >foutboodschap en met exit-status 1. Om na te gaan of een argument een directory is, kan je gebruikmaken van de
   >systeemaanroep stat. Om een programma te stoppen met exit-status 1 maak je best
   >gebruik van de bibliotheekfunctie exit die dan achter de schermen de systeemaanroep
   >_exit aanroept.

   ```c	
   #include <stdio.h>
   #include <stdlib.h>
   #include <pthread.h>
   #include <string.h>
   
   int main()
   {
       #todo
       return 0;
   }
   ```

7. Schrijf een C-programma met als naam watchfile.c dat één argument, een bestand, op de
   opdrachtlijn verwacht. Het programma loopt in een oneindige lus en schrijft telkens een
   boodschap naar het scherm wanneer het bestand dat op de opdrachtlijn werd
   meegegeven werd gewijzigd. Wanneer er geen argument werd opgegeven of het
   argument is geen gewoon bestand wordt een foutboodschap getoond en wordt het
   programma afgesloten met exit-status 1.

```c	
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

int main()
{
    #todo
    return 0;
}
```





## Deel VI: Processen en POSIX-threads

## Deel VII: Programmeren in Bash

### Patterns, expansions en het opzoeken van hulp

Zoals reeds eerder vermeld bevat de shell enkele honderden commando’s met elk nog tal
van command line options. Het is dan ook logisch dat wanneer je meer informatie zoekt over
een welbepaalde opdracht, je dit doet a.d.h.v. het commando man waarbij je de naam van
de opdracht meegeeft als parameter. Als extra parameter kan je ook nog het sectienummer
meegeven of de optie -a wanneer je alle man-pagina’s waar de naam die je als parameter
hebt opgegeven wil overlopen. 

Gebruik voor de onderstaande opdrachten de ingebouwde documentatiemogelijkheden om
op de vragen te antwoorden.

**Opdrachten**

1. > Met welk van de commando’s cp, dd, ln, mktemp, touch en cat kan je vlug een aantal
   > (lege) bestanden aanmaken waarvan de namen als parameters van het commando
   > worden opgegeven?

```bash
touch
#cp & dd -> kopiëren
#ln -> files linken
#mktemp -> temp dir aanmaken
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

4. >Welke opties moet je toevoegen aan het commando wc om enkel de grootte van een  
   >bestand te tonen zonder extra informatie?

```bash
-c  of --bytes
```

5. >In Bash zijn er ook Bash-builtin opdrachten zoals cd, set, pwd, exec, printf en :  waarvoor  
   >er geen aparte man-pagina’s beschikbaar  zijn. Een overzicht kan je bekomen door man  
   >builtin  of door de man-pagina van Bash op te vragen. Zoek informatie op over het  
   >gebruik van de opdrachten cd, set, pwd, exec, printf en :.

```bash	
-cd: change directory
-set: set shell & environment variables
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
```

8. >Hoe kan je met dd een kopie maken van de eerste 512 bytes van de vaste schijf? Bekijk  
   >met het commando strings  welke tekststrings in die 512 bytes verscholen zitten

```bash
head -c 512 /dev/sda < mbr.img
#of
dd if=/dev/sda of=mbr2.img bs=512 count=1
```

9. >Gebruik het commando find om een lijst van bestanden te krijgen die de afgelopen 24u  
   >nog werden aangepast.

```bash
find / -type f -mtime 1
```

10. > Met het commando wodim kan je van op de opdrachtlijn  een CD/DVD-branden.  Met het  
    > commando genisoimage kan je een ISO-bestand aanmaken. Hoe kan je van de inhoud  
    > van de /root directory een ISO-bestand maken?

```bash
genisoimage [options] -o output.iso /root 
```

11. >Bij vraag 10 zal je merken dat de namen van de bestanden/directories werden gewijzigd.
    >Je kunt dit vermijden door de image in Joliet-formaat weg te schrijven.
    >Naast reguliere expressies kent Unix ook patterns om een verzameling strings te beschrijven.
    >De mogelijkheden van standaard patterns zijn veel beperkter dan bv. reguliere expressies en 
    >
    >worden gebruikt zowel in opdrachten als in shellscripts. In recente Bash-versies werden deze
    >patterns uitgebreid. Extended pattern matching kan worden aangezet met de opdracht
    >“shopt –s extglob”. Bij het uitvoeren van een commando met een pattern wordt eerst een lijst met
    >bestandsnamen gegenereerd die aan het opgegeven patroon voldoen. Dit wordt meestal
    >“Pathname Expansion” genoemd. Meer uitleg kan je vinden in de man-pagina van Bash
    >onder de rubriek “Pathname Expansion”.

    ...

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
    
    ```

15. >Hoe kan je een lijst met bestandsnamen bekomen die precies uit één enkel karakter
    >bestaan?

    ```bash
    
    ```

...



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
>over drie file descriptors: standaardinvoer (stdin), standaarduitvoer (stdout) en
>standaardfout (stderr). Gewone uitvoer wordt steeds naar standaarduitvoer gestuurd terwijl
>eventuele fouten terechtkomen op standaardfout. In de shell waarin je ingelogd bent is
>standaardinvoer meestal gelijk aan het toetsenbord (invoer wordt afgesloten met Ctrl-D
>voor end of file of eventueel Ctrl-C voor terminate), en worden beide uitvoerkanalen met het
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

- de uitvoer van het commando,
- de toestand van de werkbestanden tmp\*.txt (bijvoorbeeld via de commando's wc
  tmp\*.txt of ls -l tmp*.txt),
- de inhoud van de werkbestanden tmp.txt (bijvoorbeeld via het commando cat
  tmp*.txt of door de bestanden in een teksteditor te openen).
  Wat besluit je na het vergelijken van de resultaten van elke tussenstap?

```
Je kan besluiten dat het bestand telkens overschreden wordt omdat er vanuit een andere directory geschreven wordt.
/var > tmp1.txt > tmp2.txt  -> tmp1 is dus leeg

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
De inhoud van het best tmp.txt blijft hetzelfde doorheen het proces. 
>| kan gebruikt worden om de noclobber optie te overriden. 
-C doet het zelfde als noclobber. 
+C zorgt er voor dat je het terug kan aanpassen.
```



25. >Foutmeldingen worden via een apart kanaal weergegeven, zodat er onderscheid  
    >gemaakt kan worden tussen gewone uitvoer en foutteksten. Voer achtereenvolgens  
    >volgende commando's uit en controleer de inhoud van het bestanden tmp*.txt*
    >
    >•  du /etc  
    >•  du /etc 1>tmp.txt  
    >•  du /etc 2>>tmp.txt  
    >•  du /etc >tmp1.txt 2>tmp2.txt  

