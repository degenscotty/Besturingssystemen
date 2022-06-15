# Zelftest1: Allerlei info en Commando’s



1. > Leg uit wat het verschil is tussen statisch en dynamisch linken? Enkel de uitleg
   > volstaat.

   Bij **statisch** linken wordt alle code in **één groot uitvoerbaar bestand**
   geplaatst. Bij **dynamisch** linken worden voor alle onbekende symbolen
   **stubs** in de uitvoerbare code voorzien. De code zelf bevindt zich in een
   **externe library** die bij het starten van het proces aan de virtuele
   adresruimte wordt toegevoegd. De dynamische linker zal ervoor zorgen dat
   bij de iedere aanroep van een functie waarvan de code niet beschikbaar is,
   de code uit de bibliotheek zal uitgevoerd worden.
   Het voordeel van dynamisch linken is dat een bibliotheek maar één keer in
   het geheugen moet worden geladen en dat die dan in de adresruimte van
   ieder proces die hem nodig heeft kan ondergebracht worden (cfr. shared
   memory). Het kost wel meer tijd om uit te voeren omdat de dynamisch
   linker bij iedere stub de code in de bibliotheek moet gaan zoeken.

   
   
2. > Hoe kan je een terminal venster leeg maken?

   ````bash
   clear
   ````

   

3. >Hoe kan je met het commando man informatie opvragen over de informatie in het bestand /etc/passwd?

   ```bash
   man 5 passwd
   ```

   

4.  >Met het commando man kan je informatie opvragen over externe Linux/Unix-
    >opdrachten. Hoe kan je best info opvragen over interne opdrachten zoals
    >echo, printf, set, cd, ...

   Met de opdracht help. Bv. help printf | less

   

5. >Welk commando kun je gebruiken om:
   >a. gegevens te sorteren?
   >b. het verschil tussen twee bestanden te bekijken?
   >c. een bestand of directory te zoeken?
   >d. duplicate regels uit een bestand te verwijderen?
   >e. enkel de 10 eerste lijnen uit een bestand op het scherm te tonen?
   >f. enkel de 10 laatste lijnen uit een bestand op het scherm te tonen?
   >g. een string te zoeken in een tekstbestand?
   >h. het aantal lijnen, woorden en karakters van een bestand te tonen?

   **a. sort**
   **b. diff**
   **c. find**
   **d. uniq**
   **e. head**
   **f. tail**
   **g. grep**
   **h. wc**

   
   
6. >De inhoud van de /dev-map bevat bestanden die je in twee groepen kan
   >onderverdelen. Block special device files voor harde schijven en andere
   >“mass storage devices” en character special device files voor de overige
   >randapparatuur waar een device-node voor werd voorzien (niet elk device
   >heeft immers een device node). Wat is het essentiële verschil tussen een
   >block- en character special device files?

   Een block special device heeft meer besturingssysteem nodig aangezien er gebufferd wordt. Bij een character special device gebeurt dit niet. Het heeft dus eigenlijk dus niets te maken met het soort devices wat volgens sommige bronnen het geval is. Het heeft te maken met de manier van programmeren. Block special devices zijn complexer te maken en vandaar dat ze ook schaarser zijn.

   
   
7. >Wat is de betekenis van de twee getallen die naast een device node vermeld
   >staan?

   Het **major** nummer identificeert de device driver die door het OS gebruikt
   moet worden. Het **minor** nummer geeft aan welke instantie er gebruikt van
   maakt.
   Een device node met major nummer 8 en minor nummer 2 moet je lezen als
   “De tweede instantie die gebruik maakt van de door het systeem gekende
   driver met als nummer 8”. Achter de schermen zal er binnen de kernel wel
   ergens een tabel bijgehouden worden waar het major nummer zal gebruikt
   worden als index om zo de device driver te vinden.
   De combinatie van beide is uniek. Het major nummer geeft aan welke driver
   er moet gebruikt worden en het minor nummer identificeert dan weer het
   device dat er gebruik van maakt.

   

8. >Gebruik het commando find om een overzicht te krijgen van zowel de
   >character special device files als de block special device files. Probeer het
   >eerst door twee opdrachten te geven en daarna door de twee opdrachten te
   >groeperen in één opdracht.

   ```bash
   #block special devices
   find /dev -type b
   #character special devices
   find /dev -type c
   #samen in één opdracht...hou er rekening mee dat testen bij het commando
   #find aan elkaar gelinkt worden als een logische EN. Het onderstaande is
   dus #fout.
   find /dev -type b -type c (hier ga je op zoek filesysteemobjecten die een
   character special device zijn EN een block special device. Dit is onmogelijk!
   #Het onderstaande is de juiste oplossing...
   find /dev ! -type f ! -type d !-type l ! -type p ! -type s
   Dus alle objecten die geen bestand zijn EN die geen directory zijn EN die
   geen symlink zijn EN die geen named pipe zijn EN die geen socket zijn.
   ```

   

9.  >Leg uit wat het verschil is tussen een hardlink en een softlink. Wat zijn de
    >voor- en nadelen van beide.

   **Hardlink**
   Een inode bevat alle info over een filesysteemobject. Datum en tijdstip van
   laatste wijziging, de grootte, het uid van de eigenaar, de toegangsrechten,
   enzovoort. Ook bevat de inode een verwijzing naar de datablokken.
   Wanneer je aan een filesysteemobject een extra naam toekent op een
   eventueel andere locatie, dan is dat een hardlink. Ze delen dezelfde inode
   dus wanneer je een hardlink verwijdert wordt de naam verwijderd. Enkel
   wanneer de laatste naam (link) verwijderd wordt, wordt de inode
   verwijderd en dus ook de bijhorende data. Vandaar ook de naam van de
   syscall om iets verwijderen...unlink!
   Een hardlink is dus niet op het eerste zicht zichtbaar. Enkel met “ls -l” kan je
   zien hoeveel hardlinks er zijn.
   Bij het aanmaken van een directory worden automatisch twee hardlinks
   toegevoegd, nl “.” En “..”. De “.” is een hardlink naar de nieuwe map, de “..”
   is een verwijzing naar de bovenliggende map.
   **Symlink, softlink of logische link...**
   Bij een symlink wordt een nieuwe inode aangemaakt met een verwijzing
   naar de naam van het filesysteemobject. Een verwijzing naar de naam, niet
   naar de inode! Dit is duidelijk zichtbaar bij een “ls -l” opdracht aangezien je
   uiterst links lrwxrwxrwx zal terugvinden en uiterst rechts “linknaam ->
   naam”.

   **Hardlinks hebben als nadeel:**

   - Niet mogelijk voor directories. Anders kan je lussen maken in je
     bestandssysteem. Een opdracht zoals find kan het verschil niet zien
     tussen de link en het origineel aangezien er gewoon geen verschil is.
     Een hardlink is een extra naam die je toekent.
     
   - Niet mogelijk over de grenzen van schijfpartities/schijven/USB-
     sticks/etc. Dus een hardlink kan je enkel maar leggen naar objecten
     binnen hetzelfde bestandssysteem.
     
   - Minder zichtbaar voor gebruikers
   

​		**Hardlinks hebben als voordeel:**

- Neemt geen extra plaats in op schijf. Er wordt geen nieuwe inode
  aangemaakt!
  De voordelen van een symlink zijn de nadelen van een hardlink en
  omgekeerd.



10. >Maak in je home-directory een softlink aan naar /etc/passwd en een hardlink
    >naar /etc/group (probeer dit met het commando cp als met het commando
    >ln). Hoe kan je zien of het wel degelijk over een hardlink gaat en niet over een
    >kopie?

    Softlink => cp -s /etc/passwd passwd (of ln -s /etc/passwd passwd)
    Hardlink => cp -l /etc/group group (of ln /etc/group group)

    

11. >Waarom is een pseudo random generator met een beperkt aantal bits geen
    >goede random generator?

    Met weinig bits kan je weinig getallen maken. Meestal gebruik je een
    random generator in combinatie met een modulo bewerking.... Bv. rand()
    %getal. Op die manier is er een terugkoppeling naar alle elementen van [0-
    getal-1] waardoor de getallen vooraan meer kans krijgen op voorkomen.
    Bijvoorbeeld een random generator die een getal genereert tussen 0 en 9
    geeft bij een bewerking zoals rand()%7 de **volgende frequentietabel**

    0 2 (wanneer rand 0 en 7 geeft)
    1 2 (wanneer rand 1 en 8 geeft)
    2 2 (wanneer rand 2 en 9 geeft)
    3 1 (wanneer rand 3 geeft)
    4 1 (wanneer rand 4 geeft)
    5 1 (wanneer rand 5 geeft)
    6 1 (wanneer rand 6 geeft)
    Dus zoals je ziet hebben 0, 1 en 2 een dubbele kans op voorkomen dan de
    overige getallen.
    Wanneer rand() een getal genereert tussen 0 en 100 grenzen inclusief
    krijgen we volgende frequenties bij rand()%7:
    0 15
    1 15
    2 15
    3 14
    4 14
    5 14
    6 14
    Wanneer rand() een getal teruggeeft tussen 0 en 2^16-1 krijgen we voor
    rand()%7 het volgende:
    0 9363
    1 9362
    2 9362
    3 9362
    4 9362
    5 9362
    6 9362
    De hierboven resultaten, behalve de eerste, werden via een script bepaald.
    Zoals je kan zien blijven de elementen vooraan bevoordeeld maar i.p.v

    100% meer kans bij het eerste heb je bij het laatste 9363/9362 nog maar
    meer kans op een 0.
    Een goede random generator heeft minstens 32-bit getallen terug en bij
    voorkeur zelf grotere getallen. Hoe meer bits, hoe meer dat de kans op
    kleinere getallen dezelfde wordt als bij grotere.

    

12.  >Hoe kan je met het commando head en bijhorende optie 4 bytes uit
     >/dev/random halen en deze bytes gewoon zonder te converteren naar het
     >scherm schrijven?

    ```bash
    head -c 4 /dev/random
    ```

    

13. >Wat is pathname expansion? Wat zijn de verschillende metatekens die je bij
    >pathname expansion kan gebruiken?

    Bash zal een *, een ?, [ ... ] en [!...] proberen om te zetten naar namen van
    bestandsysteemobjecten (bestanden, mappen, links, ...). Dat is pathname
    expansion.

    \* 0 of meer willekeurige tekens
    ? één willekeurig teken
    [ ... ] een karakter uit het bereik dat zich
    tussen de vierkante haken bevindt
    [ ^...] een karakter dat zich niet in het
    bereik bevindt
    [!...] hetzelfde als [ ^...]]

    

14. >Hoe kan je met het commando “ls -l” een overzicht geven van alle
    >bestandsnamen die bestaan uit minstens twee letters gevolgd door een cijfer
    >gevolgd door een willekeurig aantal karakters?

    ```bash
    ls -l ??[1-9]*
    ```

    

    

15. >Wanneer je “echo *” ingeeft, welk proces zorgt dan dat die * wordt omgezet
    >naar bestandsnamen?

    Bash zal dit omzetten. Echo krijgt nooit dat sterretje te zien behalve
    wanneer er zich geen enkel object zich in die map zou bevinden.

    

16. >Maak met touch een bestand aan met als naam passwd in je huidige
    >werkdirectory. Zoek nu met het commando find naar alle bestands- en
    >directorynamen, te beginnen bij /, die beginnen met het woord pass gevolgd
    >door 0 of meerdere willekeurige tekens? Zorg dat find hier het *-teken omzet
    >naar 0 of meerdere willekeurige tekens.

    find / -type f -name “pass*”
    De pass* moet tussen “” staan, anders zal Bash dit omzetten naar passwd

    

17. > Genereer met brace expansion alle hexadecimale getallen van 00 tot FF.

    echo {{0..9},{a..f}}{{0..9},{a..f}}
    Wil je ze onder elkaar? Gebruik dan printf “%s\n” {{0..9},{a..f}}{{0..9},{a..f}}

    

18. >Wat doet het commando sync? Wat wordt er bedoeld met mounten en
    >unmounten?

    Sync zal alle buffers naar I/O-devices gaan flushen. I/O-opdrachten worden
    door hun traag karakter beter gegroepeerd om efficiëntieredenen. Het is
    beter om 1 I/O-opdracht te hebben van 1000 bytes dan 1000 opdrachten
    van 1 bytes! Door het uitstellen van I/O-opdrachten treedt er ook een
    probleem op, nl. de toestand in het geheugen wijkt hoe langer hoe meer af
    van wat er zich in op het I/O-device bevindt! Het OS moet hiermee rekening
    houden en wanneer je wil dat het “nu” gebeurt, gebruik je sync!
    Het commando mount zorgt ervoor dat je een extern bestandssysteem
    koppelt aan een locatie in de hoofddirectory.
    “mount /dev/sdb1 /mnt” zorgt ervoor dat de inhoud van het device
    /dev/sdb1 getoond wordt in de map /mnt.
    Het unmounten gebeurt met de opdracht umount (niet unmount maar
    umount) en zorgt dat je een extern bestandssysteem verwijdert uit de
    hoofddirectory. Bij deze opdracht zullen alle bijhorende I/O-buffers worden
    geflusht.
    “umount /dev/sdb1” zal het device /dev/sdb1 ontkoppelen. Je kan i.p.v. het
    device evengoed het mountpoint of koppelpunt opgeven. “umount /mnt”
    zal na de mount opdracht hierboven ook de ontkoppeling doorvoeren.

​	

19. >Welke filedescriptoren worden er gebruikt voor standaard invoer, standaard
    >uitvoer en het standaardfoutenkanaal? Wat is het essentiële verschil tussen
    >de twee uitvoerkanalen?

    0 => stdin
    1 => stdout
    2 => stderr
    Persoonlijk vind ik de naam stderr niet zo goed gekozen. Eigenlijk is het een
    tweede uitvoerkanaal dat gewoon niet gebufferd wordt. Omdat fouten zo

    snel mogelijk naar scherm moeten worden geschreven en niet moeten
    worden opgespaard is dat ook de reden waarom men in eerste instantie dat
    tweede kanaal in het leven heeft geroepen vanwaar ook de naam die men
    eraan gegeven heeft.
    Er zijn een aantal commando’s die beide uitvoerkanalen gebruiken om de
    uitvoer op te splitsen.
    “strace ls -l” bijvoorbeeld zal stdout gebruiken voor de uitvoer van ls, terwijl
    de syscalls die gegeneerd worden door ls -l door strace zullen worden
    weggeschreven naar stderr.

    

20. >Waarvoor dient /dev/null? Hoe kan je de gebufferde uitvoer van een
    >willekeurige opdracht naar /dev/null schrijven? Hoe kan je de niet-gebufferde
    >uitvoer van een willekeurige opdracht naar /dev/null schrijven? Hoe kan je
    >ervoor zorgen dat ze nu allebeide naar /dev/null worden gestuurd?

    Dit speciale device dient als prullenbak voor als je niet geïnteresseerd bent in
    de uitvoer van een opdracht.
    De gebufferde uitvoer kan je naar /dev/null sturen door bv.
    ls -l > /dev/null
    De niet-gebufferde uitvoer kan je naar /dev/null schrijven door:
    du /proc 2>/dev/null
    Allebei naar /dev/null kan door:
    du /proc >/dev/null 2>&1
    Die ampersand voor de 1 moet er staan om aan te geven dat het om een
    filedescriptor gaat en niet zozeer over een bestand met als naam 1.

    Twijfel je over de locatie van 2>&1? Volg dan de onderstaande regel:

    - Schrijf eerst wat je naar /dev/null wil sturen (fouten of gewone uitvoer)
      en zet dit onmiddellijk na de opdracht.
      “du /proc > /dev/null
    - Wanneer je het erna schrijft is de omleiding van de filedescriptor reeds
      gebeurd en zal je dus het andere kanaal naar dezelfde locatie sturen.
      “du /proc > /dev/null 2>&1”
    - Schrijf je het ervoor, dan is de omleiding nog niet gebeurd en zal je dus
      van niet-gebufferde uitvoer gebufferde uitvoer maken.
      “du /proc 2>&1 >/dev/null”

    

21. >Wanneer is het handig om gebufferde uitvoer om te zetten naar niet-
    >gebufferde uitvoer? Wanneer is het nodig om niet-gebufferde uitvoer naar
    >gebufferde uitvoer om te zetten?

    Gebufferd => niet-gebufferd?
    Wanneer je bv. een foutmelding naar het scherm wil schrijven:
    echo “fout!” 1>&2”
    Niet-gebufferd => gebufferd
    Bij het gebruik van een pipe voor interprocescommunicatie wordt enkel de
    gebufferde uitvoer doorgegeven naar de invoer van de volgende opdracht
    in de pipeline.
    du /proc 2>&1 >/dev/null | wc -l (de fouten worden geteld want de
    gewone uitvoer wordt weggegooid maar daarvoor werd de foutenuitvoer
    eerst gebufferd gemaakt)

    

22. > Wat is een pipe? Wat wordt doorgelaten en wat niet?

    Een pipe is een achter de schermen niet meer of niet minder dan een queue
    en wordt gebruikt om de uitvoer van een opdracht als invoer van een
    andere opdracht te kunnen gebruiken. De gebufferde uitvoer wordt
    doorgestuurd, de niet-gebufferde niet.
    grep root /etc/passwd | wc -l
    De uitvoer van grep wordt doorgestuurd wc.
    Een alternatieve schrijfwijze is bv.
    wc -l < <(grep root /etc/passwd)
    Deze schrijfwijze is wat men process substitution noemt.

    

23. >Tel hoeveel fouten het commando “du /proc” oplevert en maak hierbij
    >gebruik van een pipe?

    ```bash
    du /proc 2>&1 >/dev/null | wc -l
    ```

    

24. >Gegeven “strace shuf -i 1-10 -n 5”. Strace schrijft de uitvoer van het
    >commando shuf naar stdout. De systeemaanroepen die het commando shuf
    >aan het besturingssysteem heeft gericht worden naar stderr gestuurd.
    >Herschijf de bovenstaande opdracht zodat nu uitvoer van shuf naar /dev/null
    >wordt gestuurd en waarbij de systeemaanroepen kunnen worden overlopen
    >door een pipe naar het commando less.

    ```bash
    strace shuf -i 1-10 -n5 2>&1 >/dev/null|less
    ```

    

25. >Open de manpagina van de opdracht tr. Maak ook een bestand aan met
    >uitsluitend leestekens en kleine letters. Hoe kan je met tr alle tekst uit dit
    >bestand omzetten naar een hoofdletters? Het commando tr kent geen
    >bestandparameters waardoor je met input en output redirection zal moeten
    >werken. Bemerk ook dat het een slecht idee is om binnen een proces van een
    >bestand te lezen en er ook naartoe te schrijven. Maak dus gebruik van een
    >tijdelijk bestand dat je na tr met de opdracht cp naar het originele bestand
    >kopieert (en waardoor dus het oorspronkelijk bestand overschreven wordt).

    ```bash
    tr a-z A-Z < bestand > tempfile
    cp tempfile bestand
    ```

    

26.  > Hoe wordt het regeleinde aangegeven in Windows en hoe wordt dit gedaan
     >in Linux? Het gebruik van het Linux-formaat in Windows geeft problemen,
     >dewelke? Het gebruik van het DOS-formaat geeft dan weer nog grotere
     >problemen in Linux. Waarom?

    In Windows wordt het regeleinde gegeven via de combinatie carriage return
    newline of in POSIX-notatie “\r\n”. In Linux wordt een regeleinde gegeven
    door een newline of kortweg “\n”.
    Wanneer je een bestand opent in Windows (in een primitieve editor) dat in
    Linux werd gemaakt dan zal je zien dat door het ontbreken van de carriage
    return lijnen onder mekaar worden gezet maar dat er niet noodzakelijk aan
    het begin van de lijn zal begonnen worden.
    De layout zal er bv. zo uitzien.
    .......................................
    ...........................
    ........................
    Wanneer je scriptbestanden aanmaakt in Windows en die zomaar
    overneemt in Linux dan krijg je foutmeldingen wanneer de scriptaal het
    regeleinde (\n dus) neemt als einde van een opdrachtlijn. Wanneer het

    einde van de opdracht gegeven wordt door een kommapunt “;” dan is dit
    minder een probleem.
    De reden van de problemen is dat de carriage return dan als deel van de
    opdracht genomen wordt en dat kan leiden tot foutmeldingen die weinig
    begrijpbaar zijn want een “\r” is nu eenmaal een onzichtbaar teken.

    

27. >Gebruik het commando od om de inhoud van het bestand /etc/passwd
    >hexadecimaal, in groepjes van 1 byte, op het scherm te tonen. Doe hetzelfde
    >met het commando xxd en vergelijk de uitvoer van beide commando’s. Bekijk
    >uitvoerig de manpagina’s van beide opdrachten!

    od -tx1 /etc/passwd
    xxd -g1 /etc/passwd

    

28. >Bij vraag 12 werd er gevraagd om 4 bytes (32 bits) te lezen van /dev/random.
    >Zet die uitvoer met het commando od nu om naar een decimaal getal. Hoe
    >zet je het om naar een strikt positief getal? (unsigned dus)

    head -c4 /etc/random | od -td4
    De uitvoer van de opdracht hierboven is niet zo goed omdat de adresprefix
    er nog voor staat. Dit kan je weglaten door de optie -An toe te voegen.
    head -c4 /etc/random | od -An -td4
    Voor een unsigned int:
    head -c4 /etc/random | od -An -tu4

    

29. >Gebruik het commando cut (zie manpage) om alle gebruikersnamen (1e veld)
    >uit het wachtwoordenbestand te halen?

    ```bash
    cut -d : -f1 /etc/passwd
    ```

    

30. >Hoe kan je het bestand /etc/passwd sorteren op het eerste veld? Zie de
    >manpage van sort.

    ```bash
    sort -t : -k1,1 /etc/passwd
    ```

    
