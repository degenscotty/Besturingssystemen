# Examenvragen besturingssystemen

### Hoofdstuk 1

1. > Wat is het verschil tussen **symmetrische** en **asymmetrische** **multiprocessing**? (p15)

In een **asymmetrische** multiprocessor wordt de kernel van het besturingssysteem altijd uitgevoerd op een bepaalde **master processor**. Deze is verantwoordelijk voor **scheduling** en heeft **volledige controle over het volledige geheugen** en andere bronnen. 

De **andere processoren** kunnen alleen gebruikersprogramma’s en hulpprogramma’s van het besturingssysteem uitvoeren. Heeft een andere processor een dienst nodig (bijvoorbeeld I/O oproep) dan moet die een verzoek sturen naar de master en wachten tot die dienst is uitgevoerd. 



**pro's asymmetrischemultiprocessor :**

- vereist weinig aanpassingen aan een besturingssysteem dat reeds multitasking voor 1 processor mogelijk maakt.

**con's asymmetrischemultiprocessor :**

- master wordt bottleneck voor het ganse systeem.



Bij een **symmetrische** multiprocessor kan de kernel worden uitgevoerd op **elke processor**:

**ofwel** kan de kernel worden opgebouwd als meerdere processen of threads, waardoor gedeelten van de kernel parallel kunnen worden uitgevoerd, door verschillende processoren.

**ofwel** voert elke processor een volledige kopie van het besturingssysteem uit



**pro's symmetrische multiprocessor :**

- Symmetrische multiprocessing biedt  ruime mogelijkheden op het gebied van beschikbaarheid (fouttolerantie) en stapsgewijze uitbreidingsmogelijkheden. (Als een processor uitvalt heeft dit weinig invloed op het systeem, het wordt enkel langzamer.)



**con's symmetrische multiprocessor :**

- stelt hogere eisen aan het besturingssysteem voor communicatie tussen de processoren en het syncen van het aanspreken op bronnen.
- geheugenbeheer veel complexer wanneer processoren aanvullend over een eigen cache bezitten.

![Imgur](https://imgur.com/acPC69G.png)



2. > Wat moet je voorzien om op een Unix-systeem Windows applicaties te kunnen uitvoeren? (p12)

   Je hebt **Virtuele machines** nodig om Windows-Toepassingen uit te voeren op een computer waarop Linux is geïnstalleerd.
   
   
   
   **AchtergrondInfo:**
   
   Om **systeemaanroepen** te kunnen uitvoeren moet de processor overschakelen naar **kernelmodus**. Dit gebeurt via een verzameling van bibliotheek routines met een gestandaardiseerde interface (bijvoorbeeld POSIX-standaard). Bij Windows is dit de enige mogelijkheid bij UNIX kan een systeemaanroep rechtstreeks vanuit een programma in C of C++ worden gegenereerd. Programma’s die voor systeemaanroepen louter beroep doen op de op een gestandaardiseerde API set kunnen dan ook uitgevoerd worden op andere besturingssystemen die de systeemaanroepen ter beschikking stelt met dezelfde API. Op deze manier heeft ieder besturingssysteem zijn eigen implementatie van de API. Zo zorgt de POSIX-standaard voor het uitvoeren van programma’s zonder het aan te passen aan een specifiek platform. Het **besturingssysteem** **verbergt** alle **complexiteit** en biedt een **eenvoudige gebruiksvriendelijke interface** aan, wat ook wel een **virtuele machine** wordt genoemd.
   
   
   
   *![img](https://lh6.googleusercontent.com/jFi9ZK_iPGYn3zPjWbpNLYqh-aKk09UpZdFXMcKRrxVFE1ao5m7PM2lTb3gn1djqkbrjmBj2OPVqDwv7uwjlMadhfG5p_Tqgnhh88XiAKKdF8TrDEL0Dpjra8Czj1QdOzt4LLP3UcNwpYyaKjw)*
   
3. > Bespreek hoe je op Windows een Unix-applicatie kan uitvoeren? Wat wordt in deze context bedoeld met een subsysteem?  (p20)
   
   De omgevingssusbsystemen zorgen voor de interactie met de gebruiker en voor een API set. NT (Windows **N**ew **T**echnology) kan hierdoor toepassingen ondersteunen die geschreven zijn voor uiteenlopende besturingssystemen zoals Linux (**W**indows **S**usbsystem for **L**inux = **WSL**).
   
   
   
   **subsysteem:**

   Een Subsysteem is een interface om een vreemd systeem op een host te kunnen runnen. Zo zorgt WSL dat Windows een Linux besturingssysteem kan draaien.
   
   
   
4. > Geef vier mogelijke ontwerpen van kernels. Bespreek bij elk hun voor- en nadelen en of ze nog gebruikt worden. (p16)

   **1. Monolitsche kernel:**

![img](https://lh5.googleusercontent.com/aBIQVSLXnUbCuKsdFuCfGwN1DHdFs4cPF1U3naXs67PDsyMTG-ItftH5yAC-m4TO5tY4c-kpdA5IFzzeRxRmfBkxTE3dsqC34r9Lf4kO0qraZKn3MMLewcacg3rJ18v2NLtRA6xdMa3AXXUP_A)

   - tot voor kort het meest gebruikte ontwerp
   - weinig aandacht voor structuur
      **voordelen:**
   - volledige kernel wordt uigevoerd in dezelfde gedeeelde geheugenruimte, zonder restricties voor toegang tot hardware
   - vrijwel elke procedure binnen de kernel kan een andere oproepen
   - zeer efficient
      **nadelen:**
   - gesloten voor uitbreiding. Nood aan fouten verbeteren en nieuwe functies toevoegen. Nood aan een meer modulair ontwerp.

 **2. Modulaire kernel:** 



![img](https://lh3.googleusercontent.com/InwZz3xPn8P72n-kbTckY1vNxTd8O6Xi78D_uhhJnG-xioTAMbDtl_FK2lYzZYVUy2kVUFQXXkpe9G1myTTrY437XD1zbARXy1jQpFb76avJkHkii28Gm2bkkc5Tfe96C1TEN6WxgSbLwNerRw)

Ontwikkelaars zijn afgestapt van de doorgedreven gelaagde of microkernel benaderingen. In veel moderne systemen gebruikt men verschillende modules, maar vermijdt men problemen met het definiëren van lagen en communicatie ertussen. Elke module wordt monolitisch geïmplementeerd en staat in voor specifieke functionaliteiten.

   **3. Gelaagde kernel:**

![img](https://lh6.googleusercontent.com/TJ7Xh4CCT3LJss9ITT26jUGx52mz6UdLKQuFhoNIHWjQwiVbiR4CESheyVcTileY2-ZKvtCbl9YNmHuUJ6Mv2baYfrRwXssXMsp6Lx0CZgurm5SXEZ4BZ2NsvRdoWlyXCNeJ9WbOAXd2oeKOEw)

   - verschillende modules (lagen)
   - interfaces tussen lagen
   - elk niveau voert een deel van de functies van het besturingssysteem uit
   - interactie met hardware op het onderste niveau
   - UI op het hoogste niveau
      **nadelen:**
   - Elke laag heeft toegang tot hardware. Eventuele fout in 1 laag kan de integriteit van het volledig systeem in gevaar brengen.
   - verandering in ene laag vergt aanpassingen aan andere lagen dankzij tussenliggende lagen.
   - beveiliging is lastig te bouwen in dit model

   4. **Micro kernel:**

![img](https://lh3.googleusercontent.com/DVZmwD1WnQ0qZxw68VTnkeg7LUNyOIucCmxEkNk18cpXRu930eysvY9YxS45sUCbPx9z0IDZihK6FqI8eC61wakoFDi7Q74MVm9RfQisZ1MQWPzqueBPD6P97xqnobk6y7urOQnpOb4B-DyAGQ)

   - aka client-server-model
   - enkel essentiële functies toewijzen aan kernel. Kernel wordt zo klein mogelijk gehouden.
   - andere diensten worden verzorgd door processen (servers). Deze worden in gebruikersmodus uitgevoerd.
   - server processen hebben geen rechtsreekte toegang tot hardware. Ze werken samen door berichten door te sturen via kernel.
   - servers (modules) kunnen gelijk wanneer toegevoegd/verwijderd worden.
   - bestaande functionaliteiten kunnen weggelaten worden om gereduceerde implementaties te creeëren.
   - dankzij OO technieken kunnen servers modulair uitgebreid worden zonder de integriteit van het OS in gevaar te brengen.
   - alle harware afhankelijkheid bevindt zich in micro kernel.
   - zeer geschikt voor gedistribueerde omgevingen.

     **nadelen:**

   - mircrokernel systemen blijken in praktijk te weinig performant. Berichtuitwissel belast het systeem te veel waardoor een systemcall langer duurt.

5. > Gegeven onderstaande figuur: Geef van elke component in de “executive” aan wat de werking ervan is. (p20)

![img](https://lh3.googleusercontent.com/AxHqYJph7WnRQYFglNKHVYyFvV3VUqYUJxaUrCjWVfqu9C1Kt_WTA63f13kv-237xqRuwhRLBwWtUidsODkuOw69Ag2gv3PB37beQPl3WHn2ee0EY4hiTu1klefrGtvqLWSXHGUiuDWc_aalCg)

**Executive** = deel van het NT besturingssysteem dat in kernelmodus wordt uitgevoerd. Heeft volledige toegang tot systeemgegevens en hardware. De executive is opgebouwd met een gelaagde structuur.



**Hardware Abstraction Layer (HAL):**

Voert een **vertaling** uit tussen **algemene opdrachten** en **instructies eigen aan een specifieke processor**. De **hogere niveaus** zijn eerder **afhankelijk** van **HAL-interfaces** dan van specifieke hardware. De HAL biedt ook ondersteuning voor symmetrische multiprocessing. 

**Microkernel:**

Beheert de **scheduling** en **synchronisatie** van processen. Het handelt **traps** en **interrupts** af. Het zorgt ook voor herstel na een stroomonderbreking. De microkernel is **altijd in het geheugen geladen** en **kan nooit door andere componenten onderbroken worden**.



**Executive diensten:**

= NT-modules die in kernelmodus uitgevoerd worden. De I/O-manager verwerkt de verzoeken.

- **I/O-manager:** 

Verwerkt I/O-verzoeken.

- **Cache Manager:**

Beheert de schijfcache. (File system cache op de figuur)

- **Security Reference Monitor**:

Verantwoordelijk voor controleren van alle toegang. Kijken naar permissies.

- **Object Manager:** 

Maakt en verwijdert objecten.

- **Process Manager:**

Beheert proces- en threadobjecten. Het schedulen gebeurd door microproces.

- **Virtual Memory Manager:**

Voert vertaling uit tussen virtuele en fysieke geheugenadressen (MMU) en bevat hierdoor hardwareafhankelijke code.


### Hoofdstuk 2

6. > Wat is het verschil tussen een programma en een proces? Wat zijn de vorige definities van een proces? (p28)

      Een **proces** is een uitvoering van een afzonderlijk programma (=actieve entiteit). Aan een proces worden ook bronnen toegekend (vb ruimte in hoofdgeheugen, secundaire adresruimte,..). 

      Een **programma** is een verzameling van instructies (= een passieve entiteit).

      Een besturingssyteem met multitasking geeft aan elk proces op ieder ogenblik de illusie van een induviduele programmateller, die bepaalt wat de volgende instructie is die de processor voor dat programma moet uitvoeren.

   

7. > Waarom is het model met twee procestoestanden actief en niet actief niet interessant? Wat is het probleem dat je hier zal tegenkomen? (p30)

      Het model is **te eenvoudig**. Sommige processen in de toestand niet-actief zijn gereed om te worden uitgevoerd, terwijl anderen wachten, bijvoorbeeld op de voltooiing van een I/O-bewerking. De scheduler moet in de wachtrij **telkens opnieuw op zoek gaan naar een proces** dat niet moet wachten. Stel dat een process wacht op data van de harde schijf om ingeladen te worden, dan zou het een verspilling zijn van processortijd om gewoon actief te wachten. Daarom is het aangewezen om de toestand **niet-actief** op te **splitsen** in "**ready**" en "**blocked**.

   Stel dat een process wacht op data van de harde schijf om ingeladen te worden, dan zou het een verspilling zijn van processortijd om gewoon actief te wachten. Het is dan handig om nog een extra status toe te voegen namelijk “**blocked**” waarbij dat process niet meer gekozen kan worden uit de prioriteitswachtrij. Blocked processen kunnen **ready** worden dan door een trigger, vb een IO-aanvraag of een kindproces.

   

    Hierdoor kan een procestoestandsdiagram worden opgesteld met **vijf toestanden**.

   ![img](https://lh6.googleusercontent.com/O3AZcB13s4jX_T9GdQroFmbTxHFdqeky1r6VA00WrkFbIXMKComc-41NIpQZo3l36J0Bg0p3kVE9v7f993AVOHoWKVNVFjLY7nFQce2KQuCD7Ulfk0gf2rp2k5gsGAkFbo_0JGnp3bsIsO_4Zg)

8. >  Geef alle toestanden waarin een thread zich kan bevinden? Bespreek wanneer een thread van de ene toestand in de andere zal terechtkomen. (p30)

**Nieuw (new)**

- Nieuw → Gereed: Een nieuw proces wordt toegevoegd aan de lijst van uitvoerbare processen.

**Gereed (ready)**

- Gereed → Actief: De scheduler kiest één van de processen in de toestand 'gereed' om uit te voeren.

**Actief (running)**

- Actief → Einde: Het proces word afgebroken of het geeft zelf aan dat het voltooid is.
- Actief → Gereed: Als het proces te lang bezig is (indien threshold van besturingssysteem), wordt het onderbroken. Het proces kan dit ook bijvoorbeeld doen met **sleep()**.
- Actief → Geblokkeerd: Een proces wordt geblokkeerd als hij vraagt om iets waarop hij moet wachten. (meestal in de vorm van een system call naar I/O of wachten op een kindproces.)

**Geblokkeerd (blocked)**

- Geblokkeerd → Gereed: Als het ding waarop het proces aan het wachten was klaar is.

**Einde (exit)**



![img](https://lh6.googleusercontent.com/O3AZcB13s4jX_T9GdQroFmbTxHFdqeky1r6VA00WrkFbIXMKComc-41NIpQZo3l36J0Bg0p3kVE9v7f993AVOHoWKVNVFjLY7nFQce2KQuCD7Ulfk0gf2rp2k5gsGAkFbo_0JGnp3bsIsO_4Zg)





6. >Voor processen hebben we een model met 7 toestanden, dewelke? Teken het toestandsdiagram en
      >geef aan hoe en wanneer er van toestand zal worden gewisseld. (p32)

      - **New**: Processen die gecreëerd zijn door het besturingssysteem, maar nog niet toegevoegd zijn aan de lijst met uitvoerbare processen.

      - **Ready:** Processen die uitgevoerd kunnen worden van zodra de scheduler hen daartoe de gelegenheid geeft.
      - **Running**: Enkel het proces dat wordt uitgevoerd, bevindt zich in deze toestand. By systemen met slechts 1 processor kan er maar 1 proces zich in deze toestand bevinden. Bij een systeem met meerdere processoren kunnen er uiteraard meerdere processen zich in deze toestand bevinden.
      - **Blocked**: Processen die wachten op het optreden van een bepaalde gebeurtenis, dikwijls het voltooien van I/O-bewerkingen.
      - **Exit**: Processen die door het besturingssysteem vrijgegeven zijn uit de verzameling van uitvoerbare processen.

      Door invoering van swapping moeten in het procestoestandsdiagram 2 aanvullende toestanden worden toegevoegd.

      - **Blocked/Suspended:** Processen die wachten op een bepaalde gebeurtenis, worden onderbroken (suspended).
      - **Ready/Suspended:** Wanneer die "gebeurtenis" optreedt, dan is het onderbroken proces niet meer geblokkeerd en kan het beschikbaar zijn voor uitvoering.

      **![img](https://lh3.googleusercontent.com/mSqzSFaZlacflLZtqa4jEgV0jr2NjaavJTuVQJu5V--CJkgeEeR18E_aZUu_-8JK37sEQ-gnzoXVMyWc6i0YBql3kljwvE91Rx_HmFdXbYkHF8czont0t64u9_fwS3_cGEwdW5y3WQhOLedpPw)**

      

7. > Wat wordt er bedoeld met het **procesbeeld**? Geef aan hoe dit er uitziet en beschrijf ook wat er zich
      > in elk deel bevindt. Het PCB mag je hier buiten beschouwing laten. (p33)

      **Procesbeeld** (= Proces Image):  Verzameling bestaande uit het **programma**, de **gegevens** en de **stackgebieden** van een proces. Voor uitvoering van het proces gaan we er vooralsnog van uit dat het gehele procesbeeld in het hoofdgeheugen geladen wordt. Bij een onderbroeken toestand wordt het procesbeeld als een aaneengesloten blok in het secundaire geheugen opgeslagen.

      **Delen:** 
   
   In gewone **gebruikersmodus** ga je gebruik maken van de **User Stack**, om bijvoorbeeld lokale variabelen in op te slaan, voor het aanroepen van functies en procedures en voor het doorgeven van attributen aan die functies en procedures.
   
   Als je **kernel** dingen wil uitvoeren ga je die uitvoeren in kernel mode en ga je daarvoor de **Kernel Stack** gebruiken. 
   
   In de gedeelde adresruimte  (**Shared Adress Space**) worden dingen geplaatst die gedeeld worden zoals bijvoorbeeld de C-API.



![img](https://lh6.googleusercontent.com/82V7KBNpd4tP_1zOze0a9cslcMHGyuQjzqeYpxmu4Wz5xszWcaUJEfzDVnPreomG6JLzQ6bKhfxUgggIRPTXXXspUelxuq0tKUbRZ6o48qAY0pUiVAHN0al8eCyydWJUaiys7dti6FZ3LCCppg)





11. > De info in het PCB kan je in drie categorieën onderverdelen. Dewelke? Bespreek ook wat er zich zoal
    > in elk deel van het PCB bevindt. (p34)

    **PCB** (= Process Control Block): Informatie in verband met het beheer van processen. Wordt aan het proces beeld toegevoegd.
    
    
    
    ![img](https://lh6.googleusercontent.com/heWxG8_6iqWVUQfxHCdC2OrctwWm7jvcGBmqMTr4mKPYRWQtPEzQ-cSP9yupHLC97aVNpQqbOW_L6ys7AvX_nZFuiYaItGOt8gwAYAFpV13GkJHX8idTZgIL-Cw1dqTxTTaKc4185J0YVVphsA)
    
    **Categoriën:**
    
    1. **Process Identificatie:** Unieke code voor elk proces (pid). Wordt meestal gebruikt als index in de primaire procestabel.
    
    **hoe?** Er wordt een soort boomstructuur gemaakt, Het parentproces verwijst naar het laatst aangemaakte kindproces. Dat kindprocess verwijst dan naar het voorlaatste nieuwe kindproces etc.: 
    
    os = Older Sibling, 
    
    ys = Younger Sibling
    
    kindprocess verwijst ook naar zijn parent.
    
    ![img](https://lh3.googleusercontent.com/JxKkczr5oyO9LRdQlEQD4vCMV6UodXzfAwE9rR1FZ_HnnLfvsIzCRE7YtS-s0BFPU3tN--68OhmxCXTWtx2RGbwYhE2Da_CgOi8-YO0lAE_jHFANajopX5qIjbyhlLzWLxrnkfD4SiUrvjvIiA)
    
    1. **Processor Toestand Informatie**: Bestaat uit de inhoud van alle processor registers. Wanneer een proces actief is bevindt deze informatie zich in de registers van de processor. Wanneer het proces onderbroken wordt zal de informatie in dit deel van de PCB opgeslaan worden.
    2. **Procesor Besturings Informatie:** Bevat aanvullende informatie die het besturingssysteem nodig heeft voor het beheren van diverse processen.



12. > Welke stappen moet het besturingssysteem ondernemen om een nieuw proces aan te maken? (p36)

    1. Toewijzing unieke PID.
    2. Toewijing ruimte voor alle elementen van het procesbeeld.
    3. Installatie PCB. in het bijzonder van de procesbesturingsinformatie.
    4. Instelling juiste koppelingen. Bv. plaatsing van het proces in de wachtrij gereed of gereed-onderbroken.
    5. (Eventueel) aanmaken of uitbreiden andere gegevensstructuren.

    

13. >Welke opportuniteiten kan het besturingssysteem gebruiken om van proces te wisselen? Bespreek
    >
    >zo gedetailleerd mogelijk op welke momenten de **scheduler** aan bod kan komen. Geef bij elke
    >
    >mogelijke opportuniteit ook aan of er van **proces zal/kan/moet gewisseld worden** en geef zo
    >
    >mogelijk ook een aantal **voorbeelden** om je antwoord te staven. (p36)
    
    1. **Interrupts**: Worden veroorzaakt door een gebeurtenis die zich buiten het op dat moment actieve proces afspeelt. Er wordt dan eerst overgeschakeld naar kernelmodus en de **besturing overgedragen aan een routine voor interruptafhandeling**, behorend tot het OS. Deze voert specifieke code uit voor de verwerking van het type interrupt dat is opgetreden.
    
       **Soorten Interrupts:**
    
       - *Klokinterrupt*: Actieve proces heeft de maximaal toegestane tijdsduur bereikt en moet preëmptief onderbroken worden. Om deze interrupts te genereren wordt gebruik gemaakt van een teller en een klok. Zodra de teller op 0 komt te staan treedt de interrupt op.
       - *I/O-interrupts*: Verwittigen het OS dat een I/O gebeurtenis is uitgevoerd. Het OS moet alle processen die op deze gebeurtenis wachten in de toestand gereerd of gereed-onderbroken brengen en kan beslissen het huidig actief proces preëmtief te onderbreken.
       - *Paginafouten:* Worden veroorzaakt door verwijzingen naar geheugenelementen, die ondertussen door het OS tijdelijk uit het hoofdgeheugen verwijederd zijn.
    
    2. **Trap (Exception):** Fout of uitzonderingsconditie die wordt gegenereerd binnen het op dat moment actieve proces. Bijvoorbeeld een gebruikersprogramma in gebruikersmodus die een actie wilt uitvoeren dat enkele mogelijk is in kernelmodus. Dit geval genereerd een trap (exceptie). Fatale fouten leiden tot beeïndiging van het proces en het activeren van een proceswissel.
    
    3. **De verzameling systeemaanroepen (software-interrupts**): Interface tussen OS en gebruikersprogramma's. Omdat gebruikers-programma's niet rechtstreeks geprivilegieerde instructies kunnen uitvoeren, communiceren ze met het besturingssyteem adhv system calls.
    
       **Soorten System Calls:**
    
       - **Berichtgestuurd**: Bij OS met microkernel of client/server architectuur is de interface tussen gebruikersprocesse en serverprocessen gebaseerd op het uitwisselen van berichten.
       - **Proceduregestuurd**: Elke system call komt overeen met een biblitheekprocedure, die de parameters van de system call op een bepalade plaats, bijvoorbeeld de proces registers, plaatst en vervolgs een trap instructie genereert.
    
14. > Wat is het verschil tussen een synchrone en asynchrone interrupt?

    Interrups kunnen gegroepeerd worden gebaseerd op hun herkomst. **Synchrone** interrupts komen voor bij het uitvoeren van een **instructie** (bijvoorbeeld een segmentation fault na deling door nul). Een **asynchrone** interrupt wordt gegenereerd door iets **extern**, bijvoorbeeld IO die beschikbaar komt. 

    De naamgeving komt van: een **synchrone** interrupt moet je steeds onmiddelijk afhandelen, segfaults, pagefaults (opgevraagd geheugen is niet beschikbaar). Je moet dus onmiddelijk zo’n fout fixen. Bij **asynchrone**, bijvoorbeeld IO, kan het wel **even wachten**.

15. > Geef een aantal voorbeelden die aanleiding zullen geven tot het **wisselen van proces**. Geef een aantal voorbeelden die wellicht geen aanleiding zullen geven tot een proceswissel.

    - Bij een IO-interrupt kan het dat een meer prioritair proces gedeblokkeerd wordt (= proces wissel)
    - Bij een KLOK intterupt zal het ENKEL gewisseld worden ALS Quantum op is.
    - Bij paginafouten zal het proberen de pagina’s in het geheugen laden en dan ook altijd van process wisselen .
    - Traps gaan meestal over fouten, als het een oplosbare fout is is het geen probleem als ze niet oplosbaar is zal gewisseld worden en zal het oude proces simpelweg afgesloten wordenBij een systemcall zijn er geen regels
    
    
    
16. > Hoe zal men bij een microkernel-architectuur een systeemaanroep afhandelen? (p38)
    
    **Berichtgestuurd**. Bij OS met microkernel of client/server architectuur is de interface tussen gebruikersprocessen en serverprocessen gebaseerd op het uitwisselen van berichten. Na het tot stand brengen van een kanaal en het versturen van een aanvraagbericht, laat het gebruikersproces zich door het besturingssysteem blokkeren tot wanneer het antwoord beschikbaar is. 
    
    
    
17. > Hoe zal men bij een monolithisch kernelontwerp een systeemaanroep afhandelen? (p38)
    
    In een meer klassiekere benadering (monolithisch kernelontwerp) gebeurt dit **Proceduregestuurd**: Elke system call komt overeen met een biblitheekprocedure, die de parameters van de system call op een bepalade plaats, bijvoorbeeld de proces registers, plaatst en vervolgs een trap instructie genereert.
    
    
    
18.  > Waarom hebben software interrupts een veel lagere prioriteit dan hardware interrupts? (p39)

    Het uitvoeren van system calls ten behoeve van één toepassing is minder dringend dan het vroeg genoeg bedienen van een I/O-Controller vooraleer interne buffers overlopen en gegevens verloren gaan.
    
    
    
19. >Er wordt steeds gezegd dat wanneer een proces tegen een I/O-bewerking aanloopt, het proces
    >geblokkeerd wordt. Hoe kan het besturingssysteem dat weten? (p37)

    **I/O-interrupts** verwittigen het besturingssysteem dat een I/O-gebeurtenis is uitgevoerd. Het OS moet alle processen, die op deze gebeurtenis wachten, in de toestand gereed of gereed-onderbroken brengen. Het OS kan beslissen het huidig actief proces preëmptief onderbreken ten gunste van een ander proces met bijvoorbeeld een hogere prioriteit.
    
    
    
20. >Bespreek de stappen bij het afhandelen van een interrupt wanneer de scheduler ervoor opteert om
    >de uitvoering **verder te zetten binnen het reeds actieve proces**. Wat wordt er hier bedoeld met een
    >moduswissel en een contextwissel? (p40)

    **stappen:**
    
    1. Terugschakelen naar gebruikersmodus. (=**moduswisseling**)
    2. Processortoestandsinformatie herstellen in de registers. (= **Contextwissel**, wisselen van de info van de registers.)
    
    
    
21. > Bespreek de stappen bij het afhandelen van een interrupt wanneer de scheduler ervoor opteert om
    > de uitvoering **niet** verder te zetten binnen het reeds actieve proces. Welke stappen zijn nodig om
    > een proceswissel door te voeren. (p40-41)

    Het OS zal in dit geval softwarematige aanpassingen moeten aanbrengen aan de omgeving. Dit proces zorgt voor overhead omdat het systeem tijdens het overschakelen geen nuttig werk kan uitvoeren.
    
    **stappen:**
    
    1. Opslaan context van de processor (processortoestandsinformatie).
    2. Processorbesturingsinformatie van het PCB van het tot op dat moment actieve proces bijwerken.
    3. PCB van het proces verplaatsen naar juiste wachtrij
    4. Selectie volgend actief proces
    5. Bijwerken PCB van het proces.
    6. Bijwerken gegevensstructuren voor het geheugenbeheer.
    7. Terugschakelen naar gebruikersmodus en het laden van processortoestandsinformatie van het PCB van het geselecteerde proces in de registers. Hiermee wordt de context teruggebracht naar hoe ze was op het moment dat het geselecteerde proces het laatst uit toestand actief werd gewisseld.



22. >Wat zijn de nadelen van een procesloze kernel? Welke delen van een Unix- en een Windows kernel
    >zijn procesloos? (p41)

    **nadelen:**
    
    - Het veelvoudig optreden van context- en proceswisselingen vormt een bottleneck.
    
    **Procesloze Delen:**
    
    -  
    
    
    
23. >Hoe wordt er van binnen een Unix besturingssysteem doorgaans van proces gewisseld? Hoe komt
    >het dat dit vrij efficiënt verloopt? (p41-42)
    
    Indien een proceswisseling moet uitgevoerd worden, dan wordt binnen het proces zelf de **context opgeslagen**, een **ander proces geselecteerd**, en de **besturing overgedragen aan een routine voor proceswisseling** waarvan de uitvoering plaatsvindt buiten alle processen.
    
    Het verloopt vrij efficiënt omdat: Vrijwel alle software van het OS uitgevoerd wordt in de context van een **gebruikersproces** en er dus minder proces wisselingen voorkomen die een bottleneck zouden vormen.


24. >Hoe wordt er binnen een microkernelgeoriënteerd besturingssysteem van proces gewisseld? Wat
    >zijn hier de voor- en nadelen (p42)
    
    De belangrijkste OS functiess worden gestructureerd als aparte processen, uitgevoerd in de kernelmodus. Ook hier zorgt een kleine hoeveelheid code voor de proceswisseling, uitgevoerd buiten alle processen om. 
    
    **Nadeel**: overhead door veel meer proceswisselingen.
    
    **Voordeel:** OS kan beschouwd worden als een verzameling van verschillende modules, met onderlingen eenvoudig interfaces. De processen die deze modules uitvoeren, kunnen met aangepaste prioriteit worden verweven met andere processen. Sommige van deze processen moeten bovendien niet in kernelmodus uitgevoerd worden. Ook kan in een systeem met meerdere processoren, of zelf in een gedistribueerd systeem, een deel van de OS processen toegekend worden aan specifieke processoren.    
    
    

25. > Wat is de herdefinitie van een proces en de definitie van een thread? (p43)

**Proces**: eenheid voor de eigendom van bronnen

- ruimte in het hoofdgeheugen
- secundaire adresruimte
- andere bronnen

**Thread**: eenheid van verdeling van processorinstructies



26. >Geef het procesbeeld van een multithreaded proces met drie threads. Welke delen worden er over
    >de grenzen van een thread gedeeld? (p43-44)

    Er is nog steeds een PCB en gebruikersadresruimte op procesniveau. Voor elke thread zijn er afzonderlijke stacks en een afzonderlijke besturingsblok, waarin ondermeer de contextinfo opgeslagen wordt.

    Threads kunnen zich zoals processen in verschillende toestanden bevinden. Scheduling wordt uitgevoerd per individuele thread. De OS scheduler maakt bij selectie voor het volgende actieve thread geen onderscheid of threads al dan niet tot hetzelfde proces behoren. De meeste toestandsinformatie wordt daarom bijgehouden op thread niveau.

    Alle threads **delen** de toestand en de bronnen van dat proces: Threads hebben gedeelde toegang tot dezelfde geheugengegevens en dezeflde bestanden. Ook programmacode wordt automatisch gedeeld. Het voordeel van gedeelde code is dat toepassingen meer actieve threads kunnen hebben binnen dezelfde adresruimte, waardoor de processor waarschijnlijk beter bezig kan gehouden worden.

**![img](https://lh6.googleusercontent.com/QrC4gsmJUlzYbbmg6csy2tANu76Xar39YdooEvDKXJlnsU5CK5YIKWQ_qdAjgMoUMQRO9y0lQFxxnzyqdgeVg9E4iznHx3C0qRETk4wOClCaD3kwdA_r8mvz5UJd2rxdHo-v4NetIyLnNcDOTg)**



27. >Geef voor- en nadelen van multithreading. Welke zijn de mogelijke implementaties (enkel
    >vernoemen volstaat)? (p45-46)

    **Voordelen:**

    - Alle threads delen de toestand en de bronnen van dat proces: Threads hebben gedeelde toegang tot dezelfde geheugengegevens en dezeflde bestanden. Ook programmacode wordt automatisch gedeeld. Het voordeel van gedeelde code is dat toepassingen meer actieve threads kunnen hebben binnen dezelfde adresruimte, waardoor de processor waarschijnlijk beter bezig kan gehouden worden.
    - Interprocescommunicatie tussen threads van eenzelfde proces kan eenvoudig op gedeeld geheugengebruik worden gebaseerd, zonder tussenkomst van de kernel. 
    - Het creëren en wisselen van threads binnen een proces vraagt aanzienlijk minder overhead dan de overeenkomstige handelingen op processen.
    - Blokkeert één thread op een gebeurtenis, dan hoeft het proces daarom niet noodzakelijk geblokkeerd te worden: andere threads binnen hetzelfde proces kunnen immers nog geactiveerd worden.
    - Programma gaat verder wanneer een deel ervan bezig is met een langdurige bewerking.

    **Nadelen:**

    - Indien men in threads gebruik maakt van hulpfuncties (bv. van een bibliotheek), dan moeten die reëntrant uitgevoerd zijn. Dit betekent ondermeer dat elke simultane uitvoering van de functie enkel een beroep mag doen op een aparte verzameling lokale variabelen om de toestand van de functie bij te houden.

    **Mogelijk implementaties:**

    - User-level threads
    - Kernel-level threads
    - Combinatie van de twee.

    

28. > Wat zijn de voor- en nadelen met user level threading? (p46)

**Voordelen:**

- Kunnen worden ondersteund op elk besturingssysteem
- Threadwisselingen kunnen efficiënter worden uitgevoerd omdat het proces voor het beheren van de threads niet moet overschakelen naar de kernelmodus van de processor
- Het schedulingalgoritme kan specifiek aan de toepassing worden aangepast

**Nadelen:**
- Voert één thread een blokkerende systeemaanroep uit alle threads van het proces worden tegelijkertijd geblokkeerd
- Op elk moment kan maar één enkele thread actief zijn binnen een proces  geen gebruik van multiprocessing



29. > Wat zijn de voor- en nadelen van kernel level threading? (p47)

    

**Voordelen:**

- Worden door het besturingssysteem zelf beheerd
- Scheduling door de kernel wordt uitgevoerd op basis van threads
- Een geblokkeerde thread blokkeert andere thread binnen hetzelfde proces niet
- Thread pools zorgen er voor dat een aanvraag sneller afgehandeld worden. Anders zou er elke keer een nieuw thread aangemaakt en afgebroken moeten worden

**Nadelen:**

- De besturing van de ene naar de andere thread vereist een modus- en contextwisseling. Het aantal kernel-level threads wordt hierdoor vaak gelimiteerd.



30. >Wat is het verschil tussen coöperatieve- en preempted multitasking? Wanneer kan een proces
    >preemptief worden onderbroken? (p51, theorieles week4: 01:19)

**Coöperatieve multitasking:** Op systemen zonder timeslicing moet een thread vrijwillig de controle over de processor afgeven (met de yield methode) om andere threads een kans te geven.

**preempted multitasking**: Bij preempted multitasking wordt er gebruik gemaakt van **timeslicing** waarbij threads onderbroken kunnen worden. Bijgevolg kunnen threads met een lagere prioriteit actief worden voor een thread met een hogere prioriteit. een thread wordt gewisseld na een bepaalde tijd, het wordt dus preemptief onderbroken wanneer deze tijd verstreken wordt.

Een proces moet **preemptief** onderbroken worden:

- Bij een Klokinterrupt
- Bij een I/O-interrupt



31. > Geef het procestoestandsdiagram van een klassiek Unix besturingssysteem en bespreek elke
    > toestandsovergang (cfr. vraag 9). Waarom is dit niet geschikt voor realtime-applicaties?

    

    **procestoestandsdiagram:**

![img](https://lh5.googleusercontent.com/oh9RkWW-cGsqiEM4rZU8MabCtjFasif9uEwCdczj-s7Nn7bgd4GeerG4s0N2_7M4HzDFj61J018OMKUr1wtBoyQvFPYq52f_zjDwKVoM_4xahmaADXUBcvKrpkVFfANCt107ht5o7hxYvUn51g)



**Verschil tussen preempted en ready to run (Oplossing prof):**

Er wordt onderscheid gemaakt tussen de twee toestanden (Ready to Run en Preempted). 

In essentie vormen beide één toestand hetgeen wordt aangegeven door de streepjeslijn die de toestanden
verbindt. Het onderscheid wordt gemaakt op de wijze waarop een proces in de toestand preemted
binnenkomt. Wordt een proces uitgevoerd in kernelmode (als gevolg van een interrupt) dan zal er
een moment aanbreken (na interruptafhandeling) waarop de kernel zijn werk heeft voltooid en de
besturing kan teruggegeven worden aan het gebruikersprogramma. Net voordat dat gebeurt, wordt
zoals steeds, de scheduler aangeroepen om te kijken of er preemptief moet worden onderbroken
ten gunste van een proces met een hogere prioriteit. Wanneer er preemptief moet worden
gewisseld, wordt het actieve proces naar de toestand preempted gebracht. Het proces in de
toestand preempted en de processen in de toestand ready to run vormen één wachtrij van gerede
processen.
Een proces kan enkel preemptief onderbroken worden wanneer er gewisseld wordt van kernel- naar
gebruikersmode. Een proces kan echter niet preemptief worden onderbroken terwijl het in
kernelmode wordt uitgevoerd (een interrupt wordt in Unix afgehandeld binnen de context van dat
huidige actieve proces). **Dit maakt klassieke Unix ongeschikt voor realtime applicaties.**





32. > Een proces in een Windows heeft drie zaken? Benoem ze en bespreek waarvoor ze dienen. (p56)

    - **Access token**: = primary token. Staat in voor de beveiliging. Bevat een kopie van de beveiligingsidentificatiecode.
    - **Virtuele adresruimte:** Wordt door de Virtual memory manager module van de Executive beheerd.
    - **Objectlable met handles** naar andere objecten, ondermeer naar elke thread die het proces omvat.

    

33. >Geef het toestandsdiagram van een Windows thread? Bespreek de toestanden en de mogelijke overgangen. (p58)

    

    ![img](https://lh5.googleusercontent.com/S5c4ATN-yjxRZQtKGPEdsb6i0QsMNdT-JvfcHvws9b2iys77d9dg4PcNz25shVZvUibiKwgwG_cKnA_H_K5g6gzKX6TTl421ms459fsp2JciiiuP-bBPZWLUhXppJXYtm-HZAyajlNGAFX2ndA)

    Een NT-thread kan zich in zes verschillende **toestanden** bevinden:

    - **ready**
    - **running**
    - **terminated**
    - **stand-by**: Hier bevindt zich de ready thread met hoogste prioriteit
    - **waiting**: Wordt bereikt indien een thread geblokkeerd wordt op een gebeurtenis (bijvoorbeeld een I/O-handeling), of wanneer een thread, vrijwillig of op verzoek van een andere thread, zichzelf onderbreek.
    - **transition**: Zijn na het wachten de (geheugen)bronnen nog steeds beschikbaar, dan gaat de thread rechtstreeks naar de toestand gereed, zoniet naar de overgang transition.

    

    **De mogelijke overgangen**:

    - Pick to run (Ready → Standby)
    - Switch (Standby → Running)
    - Preempted (Running → Ready)
    - Terminate (Running → terminated)
    - Blocked/suspend (Running → Waiting)
    - Unblock/resume, resource available (Waiting → Ready)
    - Unblock, resource not available (Waiting → Transition)
    - Resource available (Transition → Ready)



34. >Geef het toestandsdiagram van een besturingssysteem dat gebruikmaakt van **user level threads** en
    >een **lichtgewichtproces** (cfr. **Solaris**). Wat zijn de verschillende toestanden en de mogelijke
    >overgangen? Bespreek wanneer er van toestand zal worden **gewisseld** en geef ook aan in **welke**
    >**toestand** de user-level thread en het lichtgewichtproces zich moeten bevinden om uitgevoerd te
    >worden. (p55)



![img](https://lh5.googleusercontent.com/4WkWvNN5G-bA88-3XMzivW1yNL1lxAKObeMc-c-gNV7IPAz9gzWhvffPoenDJAQ7fWn2HRvOpPRjoGZ8QgWSghLI2xiJ360UsKFM9jukgFIToU4MAzXBbaMIeOSB0UX6AD4jQN-D1y-24T4zcA)

**Verschillende toestanden:**

- **Runnable**
- **Sleeping**
- **Active**
- **Stopped**

**Overgangen:**

- Active -> Sleeping: Door een primitieve voor synchronistatie , waardoor de toestand sleeping wordt aangenomen tot wanneer de synchronisatievoorwaarde voldaan is.
- Active -> Stopped: Door een ander actieve user-level thread
- Active -> Runable: Het user-level thread wordt preëmptief onderbroken wanneer een andere thread met hoger prioriteit runnable wordt.
- Een actief User-level thread kan zichzelf ook preëmptief onderbreken en de controle overdragen aan een andere uitvoerbare user-level thread met gelijke prioriteit.

Indien de user-level thread niet gebonden is aan een enkel lichtgewicht proces, dan wordt die enkel in de **actieve toestand** effectief aan het lichtgewicht proces gekoppeld.



35. > Bespreek onderstaande figuur. Hoe worden de verschillende componenten aan elkaar gekoppeld (p48)

    **Combinatie user-level en kernel-level threads**

**![img](https://lh3.googleusercontent.com/tT-8q36GYPHuFL4SK-HrhmUx9sRJhFtIsrjVyZy9WVAClRxXbNIg7dQ8HmA7V-jfOL-4JeJO1aQph5mylQzXDnPgRlM2goVwl-odxjG21_2uiHG3uIcYQ3-lBYrfjvZtlaZ5zCj4N57HKRZtLg)**

Sommige besturingssystemen, zoals Windows, en enkele Unix varianten , waaronder Solaris, **combineren user-level en kernel-level threads.** Ze baten hierbij de voordelen van beide benaderingen.

Verschillende user-level threads worden gegroepeerd **gekoppeld** aan een (kleiner of gelijk) aantal kernel-level threads. In dit gecombineerde systteem moet de user-level threadbibliotheek communiceren met de kernel. Dit gebeurt meestal via lightweight processen (gegevensstructuren). Voor die bibliotheek ziet een lightweight proces er uit als een virtuele processor, waaraan een user-level thread kan **gekoppeld** worden. Het OS gebruikt het lightweight proces om er een kernel-level thread aan te koppelen.



36. >Bespreek elke gegeven situatie en geef ook aan waar ze ideaal voor geschikt zijn, m.a.w. waar en
    >wanneer zullen ze worden gebruikt. (p49)

    **![img](https://lh3.googleusercontent.com/-aC9qksDF10gIJshI7iGREBqSgYXri4N7K6sG2i5fF45edvpkmwSL3WyUe45TUJhHDn4LMJhV6479SRiVkU5bafbGcislCwBcHT8zJCu4DMQZ5HyYmBh-LDNJIANJfZSKexrtY7YRcrlJ1fu_Q)**

    

- **Proces 1:** Heeft één user-level thread, die gebonden is aan één lichtgewicht proces. Deze optie gaan nomen worden indien gelijktijdigheid binnen een proces niet vereist is.
- **Proces 2:** Meerdere user-level threads, die allemaal gebonden zijn aan hetzelfde lightweight proces. Dit is een efficiënte oplossing voor programma's met een logische parallelliteit.
- **Proces 3**: Meerdere user-level threads, gekoppeld aan een (kleiner of gelijk) aantal  lightweight processen. Goede oplossing indien threads geblokkeerd kunnen worden.
- **Proces 4**: Meerdere user-level threads, die elk in een 1-op-1 relatie gebonden zijn met lightweight processen. Dit kan nuttig zijn bij CPU-gebonden toepassingen.
- **Proces 5:** Gelijkaardig aan proces 3 maar bindt aanvullend nog één user-level een lightweight proces, dat bovendien gebonden is aan een spcifieke processor. Dit is bijvoorbeeld aangewezen voor toepassingen met een realtime component.



### Hoofdstuk 3



37. >Waarom krijg je bij het schrijven van data naar een filedescriptor die geopend werd met de O_SYNC-
    >vlag een heel trage verwerkingssnelheid (2 redenen)? (Oplossing prof)

    Wanneer je de vlag niet meegeeft zal een proceswissel niet steeds noodzakelijk zijn. Het proces
    roept via een software-interrupt de systeemaanroep aan, er treedt een **modewissel** en
    **contextwissel** op (cfr. de CPU-registers worden, in Linux althans, op de kernelstack bewaard) en de
    code van de systeemaanroep wordt in kernelmode uitgevoerd. Zonder de O_SYNC-vlag leidt dit
    veelal tot een zuivere geheugenoperatie door het wegschrijven van 1 of meerdere bytes van de
    user-buffer naar de kernel-buffer. De tijd die hiervoor nodig is is zeer beperkt en na de
    systeemaanroep is een proceswissel dus niet steeds aan de orde. Wanneer de kernelbuffer echter
    vol komt, moet er een **I/O-operatie** gestart worden en zal het gebruikersproces moeten worden
    geblokkeerd tot wanneer alle bytes uit de userbuffer werden gekopieerd.
    Bij het zetten van de O_SYNC-vlag heb je dus naast meer **I/O-operaties** ook steeds een extra
    **proceswissel** wat het vertragend effect nog versterkt. Iedere write-systeemaanroep wordt verplicht
    om een I/O-operatie te starten en het bijhorende proces te blokkeren tot wanneer de bijhorende
    I/O-interrupt het geblokkeerde proces deblokkeert

​	

38. >Wat zijn de voor- en nadelen van (kernel/user) buffering? In de kernel wordt er default
    >gebruikgemaakt van buffering en in het gebruikersprogramma stel je het zelf in. Bemerk dat
    >wanneer je opeenvolgende schrijfopdrachten doet met slechts 1 byte, je per definitie geen buffering
    >gebruikt. (Oplossing prof)

**Voordelen:**

- Buffering **beperkt** het aantal **I/O-opdrachten** naar de schijf. De blokgroottes die naar schijf worden
  geschreven zijn niet bepalend voor de schijfprestaties, het aantal lees/schrijfoperaties per seconde
  daarentegen wel. 
- Buffering zorgt dat lees/schrijfopdrachten plaatsvinden op een geheugenbuffer en wanneer die
  dreigt vol te lopen zal het OS die moeten flushen. Er wordt dus van heel veel kleine I/O-opdrachten
  één grote I/O-opdracht gemaakt die dan daadwerkelijk naar schijf zal worden geschreven.

**Nadelen:**

- Het nadeel is wel dat je ten eerste **geheugen** zal moeten **toekennen** om die buffers te voorzien en
- Dat er ook wel wat **werkt** kruipt in het constant **in de gaten houden van de buffergrootte** zodat
  die tijdig kan worden leeggemaakt (bij schrijven) of opgevuld (bij lezen). Buffering vereist ook
  complexe algoritmes die de buffers op juiste moment moeten aanvullen of leegmaken



39. >Wanneer zal de systeemaanroep read resulteren in een geblokkeerd proces en wanneer niet. Idem
    >voor een write-systeemaanroep. Geef nog een aantal andere systeemaanroepen die doorgaans een
    >proces zullen blokkeren en dus bijgevolg een proceswissel zullen veroorzaken. (Oplossing prof)

    Wanneer de buffer net moeten worden opgevuld, zal het OS het proces moeten **blokkeren** tot
    wanneer de achterliggende I/O-opdracht de buffer terug aangevuld heeft. Wanneer de buffer nog
    voldoende gevuld is zal het OS onmiddellijk de leesopdracht kunnen beantwoorden **zonder** te
    moeten wisselen van proces.
    
    **Waitpid**, **read** en bv. **write** (bij een volle buffer die moet geflusht worden) zijn voorbeelden van
    systeemaanroepen die een **geblokkeerd** proces en dus een **proceswissel** zullen **veroorzaken**.
    
    
    
40. > Geef een kort C-codefragment waarmee je een zombie-proces aanmaakt. Wanneer een proces een zombieproces wordt, welk deel van het proces houdt de kernel dan nog in het geheugen bij en waarom? (Oplossing prof)
    
       ```C
       int main(){
       	int pid;
       	if ( (pid=fork())<0){
       		perror(argv[0]);
       		exit(1);
       	}
       	else if (pid==0){
       		//child
       		exit(0);
       	}
       	//parent
       	sleep(60);
       	//niet wachten, geen waitpid dus
       }
       ```

​	

Wanneer een proces klaar is komt het in Unix in de status **zombie** terecht vooraleer het wordt
afgebroken. Het proces kan echter uitsluitend worden afgebroken wanneer de parent zijn **exit-**
**status** leest. Doet de parent dit niet, wordt het proces niet volledig beëindigd en **blijft** het in de
toestand **zombie**. Als de parent zelf beëindigd wordt, wordt het kind naast een zombie ook een
**orphan** dat **geadopteerd** wordt door het **init-proces**. Het init-proces zal de exit-status van het kind
lezen waardoor vervolgens ook het kindproces kan worden ontmanteld.
De **exit-status** van een proces wordt in Linux bijgehouden in het PCB (process control block) dat dus
zolang het in de status “zombie” vertoefd in het geheugen blijft.
Bij een daemon-proces zal je dus bij het niet correct lezen van de exit-statussen van de kinderen een
ganse waslijst met zombie-processen maken die op zich 0% CPU tijd krijgen (dus geen probleem
voor de scheduler) en ook 0% geheugen toegewezen krijgen. Iedere zombie neemt wel een plaats in
de globale procestabel in beslag en bovendien blijft de volledige procesbesturingsinformatie achter
in het geheugen! Dit is dus niet onschuldig!



41. >Na de systeemaanroep fork kan de uitvoering worden verdergezet in ofwel het kind ofwel de ouder.
    >In welke van de twee zal de uitvoering hoogstwaarschijnlijk worden verdergezet en waarom?
    >Wanneer zal dit niet het geval zijn? (Oplossing prof)

Wanneer je een systeemaanroep aanroept wordt er naar kernelmode geschakeld om de software
interrupt (systeemaanroep) af te handelen. Hierna komt de scheduler (ook in kernelmode) aan bod
om te kijken of er door de interrupt-afhandeling geen meer prioritaire processen werden
gedeblokkeerd en zich dus in de toestand “gereed” bevinden. Dit is hier onmogelijk want de enige
manier dat er preemptief van proces kan worden gewisseld is wanneer er na het afhandelen van de
systeemaanroep processen gedeblokkeerd werden met een hogere prioriteit. **Dus zal de uitvoering**
**gewoon worden verdergezet in het proces dat aan zet was voor de onderbreking,** de **parent** dus. Er
is slechts één manier waarbij het kind als eerste aan bod zou kunnen komen en dat is dat bij het
aanroepen van de systeemaanroep alle toegewezen tijd door de parent werd opgebruikt. Dan en
**enkel dan zal het kind als eerste aan bod komen**.



42. > Linux kent geen fork-systeemaanroep. Hoe komt het dat je hem wel kan gebruiken? (Oplossing prof)

    Linux gebruikt de glibc-POSIX API. Die staat in voor de **vertaling** van courante Unix-
    systeemaanroepen naar Linux-specifieke systeemaanroepen.

    

43. > In welke situatie maak je gebruik van een named pipe en kan je dus geen unnamed pipe gebruiken? (Oplossing prof)

**Unamed** pipes of anonieme pipes kan je **uitsluitend** **gebruiken** voor **IPC** (interprocescommunicatie)
tussen processen met verwantschap (ouder, kind, broer, kleinkind, ...). Bij processen zonder
verwantschap moet je gebruikmaken van een **named** pipe, i.e. een object op het bestandssysteem
dat je een naam moet geven (vandaar ook de naam)



44. >Zijn POSIX-threads (of pthreads genoemd) kernel level threads of user level threads? Hoe kom je tot
    >dit besluit? (Oplossing prof)

Linux kent uitsluitend tasks en maakt eigenlijk geen onderscheid tussen threads en processen. Bij
het gebruik van POSIX-threads merk je op dat er achter de schermen een clone-systeemaanroep
wordt gebruikt en waar dus een nieuw proces mee wordt aangemaakt waarbij alles gedeeld wordt
behalve dan de userstack. Ook wanneer je kijkt met de opdracht top -H zie je hier twee processen
staan waarbij het dus **eerder** aanleunt bij de definitie van **kernelthreads** **dan** bij de definitie van **user**
**level threads**. 

Ter info bij user level threads is het besturingssysteem niet op de hoogte van het
gebruik van threads. De scheduler kan dus onmogelijk een user level thread voor uitvoering
selecteren. Alle beheer van user level threads komt dus terecht bij de applicatie zelf. Het proces
moet dus de nodige code bevatten om zelf te switchen tussen threads. Blokkeert één user level
thread op een I/O-bewerking, dan blokkeert het volledige proces. Ook al kunnen andere threads
binnen dat proces wel verder doen.



### Hoofdstuk 4



45. > Aan welke vier randvoorwaarden moet ieder geheugenbeheersysteem voldoen? (p109)

	1. Om de efficiëntie van de processor en van de I/O-voorzieningen te verhogen, is het noodzakelijk dat zoveel mogelijk processen in het hoofdgeheugen geladen zijn. Er is in praktijk nooit voldoende hoofdgeheugen om alles bij te houden. Daarom is het nodig om gegevens naar en uit het secundair gegeheugen te **swapppen**. Swappen is echter een langzame bewerking. Swappen verhoogt tijd nodig voor proceswisseling en is dus een complexe taak voor het geheugenbeheersysteem. Tegenwoordig wordt er meer gebruikt gemaakt van het concept **virtueel geheugen**.
	2. Hardware van de processor en software van het OS moeten de verwijzingen in de code van het programma op een of andere wijze **vertalen** in adressen van het fysieke geheugen, die overeenkomen met de huidige locatie van het programma in het hoofdgeheugen.
	3. Enerzijds mogen processen **niet zonder toestemming** geheugenlocaties van andere processen kunnen **lezen** of **schrijven**. Dergelijke instructies moeten afgebroken worden van zodra ze uitgevoerd worden. Anderzijds moet dit beveiligingsmechanisme voldoende flexibel zijn om verschillende processen toegang te kunnen geven tot gedeelde stukken van het hoofdgeheugen. Ook is het dikwijls noodzakelijk dat dat processen die samenwerken dezelfde gegevensstucturen delen.
	4. Zowel het hoofdgeheugen als het secundaire geheugen zijn doorgaans georganiseerd als een ééndimensionale adresruimte. De meeste Programm'aas daarintegen zijn logisch ingedeeld in modules, met andere karakteristieken. Het is de taak van het geheugenbeheer en van de computerhardware om deze modules te **vertalen** naar een ééndimensionale adresruimte.



46. > Bespreek de werking van vaste partitionering (vaste grootte en verschillende grootte). Wat zijn de voor- en nadelen van dit systeem? Hoe zal het besturingssysteem procesbeelden gaan plaatsen in een systeem met vaste partitionering? (p110)



**Vaste partitionering** is de eenvoudigste techniek om de rest van het hoofdgeheugen te beheren. Het hoofdgeheugen wordt verdeeld in **gebieden met vaste begrenzing.**



**Voordelen:**

- Systemen met vaste partitionering vereisen nauwelijks OS software. Het OS moet enkel in een tabel bijhouden welke partities nog beschikbaar zijn en welke reeds bezet zijn.
- Gelijke grootte: Bieden een grotere flexibiliteit. Men kan elk proces toewijzen aan de kleinste partitie waarin het past. Het geheugenbeeld van het OS ligt nu dichter bij de werkelijke behoeften van de processen. Voor elke partitie is wel eens scheduling wachtrij nodig. In deze benadering wordt verspilling uiteraard geminimaliseerd.



**Nadelen**:

- Het aantal partities die werd ingesteld bij het genereren van het systeem beperkt echter het aantal actieve processen.
- Het vergt dat het maximale geheugen dat een proces zal vereisen, op voorhand gekend is.
- Vaste grootte: Hoofdgeheugen weinig efficiënt gebruikt. = **Interne Fragmentatie**
- Vaste grootte: **Procesbeeld** kan nog steeds te groot zijn om in één partitie te passen. In dat geval moet het gebruikersprogramma zelf overlaytechnieken inbouwen, zodat zich altijd maar een deel van het programma in de toegewezen partitie bevindt.



47. > Bespreek de werking van dynamische partitionering. Wat zijn de voor- en nadelen? Welke zijn de
    > verschillende plaatsingsalgoritmen en bespreek de werking en functie van elk algoritme. (p111)



**Dynamische partitionering** probeert de beperkingen van vaste partitionering op te lossen door een variabel aantal partities met een variabele grootte te gebruiken. 



**Voordelen**:

Het creeërt een geheugenbeeld dat meer aan de eisen van processen voldoet. Wanneer een proces wordt overgebracht naar het hoofdgeheugen krijgt het precies de benodigde hoeveelheid geheugen. 



**Nadelen**:

Processen die zich niet meer in de toestand gereed bevinden, worden uit het hoofdgeheugen geswapt om plaats te maken voor beschikbare processen, in de toestand gereed-onderbroken. Aangrenzende vrije partities kunnen hierbij worden samengevoegd. Dit leidt tot **extern fragmentatie**. Het geheugen buiten de partities worden steeds meer gefragmenteerd en steeds minder benut. In het ergste geval wordt er een blok verspild tussen elke twee opeenvolgende procassen.



48. > Hoe gebeurt adresvertaling bij dynamische partitionering? (p114)

Wanneer het proces in het hoofdgeheugen wordt geladen, geswapt of verschoven, worden de aan het proces toegekende absolute begin- en eindadressen geladen in het **basisregister** en het **begrenzingsregister** van de processorregister, als onderdeel van de contextwisseling. Tijdens de uitvoering worden enkel relatieve adressen aangewend. Elk adres ondergaat hierbij 2 bewerkingen: een **optelling** om het overeenkomstige fysiek adres te bekomen, en een **vergelijking** met de begrenzingregister. Wanneer het adres niet binnen de begrenzing ligt, dan wordt een **interrupt** gegenereerd naar het OS.



49. >Bij dynamische partitionering kan je voor het geheugengebruik een bitmap of een gelinkte lijst
    >bijhouden (maak een schets)? Hoe gebeurt dit en wat zijn de voor- en nadelen van beide systemen? (p115)

Bij het gebruik van **bitmaps** wordt het geheugen verdeeld in kleine allocatie-eenheden van gelijke grootte. Bij elke allocatie-eenheid hoort een bit die aangeeft of de eenheid vrij is of bezet. Hoe kleiner de allocatie-eenheid is, des te groter wordt de bitmap.

![img](https://lh4.googleusercontent.com/4ciH29yqT78whRu8Odm92SFqQq90PpUPcTcQIq8C85BEKBo5s9mxPaHlP91rfXToE2g_zyWBV1EgZboUjCwLRjbRfslhO-cL4jnsTdzBEyfN4_yd_I2SO7nLQ9_dschNqOwROOQI0FyUVRV3IQ)

**nadelen:** 

- Als de allocatie-eenheid te groot wordt gekozen, **versplit elk proces veel geheugen** in zijn laatst gealloceerde eenheid.
- Wanneer een nieuw proces, N aaneensluitende allocatie-eenheden vereist, dan moet het geheugen-beheersysteem immers in de bitmap op zoek gaan naar een rij van N opeenvolgende nullen. Dit is een **tijdverslindend proces**.

**Gelinkte lijsten** vormen een alternatieve manier om de vrije allocatie-eenheden bij te houden. Het geheugen wordt voorgesteld als een gekoppelde lijst segmenten die ofwel in gebruikt zijn door een proces, ofwel beschikbaar zijn.

![img](https://lh5.googleusercontent.com/9Gj6SuGZ_Lm4zpUt_C7tJMYHfToBGk9FUjk8ALqaI3msjucJUZcxf9ydqYIhs2h-wkXdssUjLbnBoJo7Dv305zfCeeql-ShYDknMgEAAHjFQkebHhnJ1OFr6-3renx81m7vXLsZSPEYOcSOWzg)

**voordelen**: 

- indien voor het vrije en gebruikte geheugen aparte lijsten worden bijgehouden, kunnen deze lijsten worden gesorteerd op grootte. 

**nadelen**:
- bijwerken lijsten complex en duur. 

De blijkbaar meest efficiënte oplossing, voorgesteld door donald Knuth, plaatst zowel aan het begin als aan het einde van elk geheugenblok informatie met de status en grootte van het blok, en neemt enkel de vrije geheugenblokken op in de dubbel gelinkte lijst.



50. >Bespreek de werking van paginering (zonder virtueel geheugen). Wat is het verschil tussen
    >paginering en vaste partitionering? Hoe gebeurt de adresvertaling bij paginering (maak een schets)?  (p118)

Bij de **paginering** verdeelt men het hoofdgeheugen in frames (stukken met een gelijke, relatief kleine grootte) en alle **procesbeelden in pagina’s ter grootte van de frames**. De procespagina’s worden toegewezen aan frames van het hoofdgeheugen. Kleinere processen vereisen minder frames, grotere processen vereisen er meer. Het besturingssysteem houdt een lijst van vrije frames bij, en een pagina table voor elk proces (in het procesbeeld van het proces zelf). Deze bevat de framelocatie van elke pagina van het proces: elke ingang in de paginatabel bevat het nummer van het frame in het hoofdgeheugen dat de corresponderende pagina bevat.

![img](https://lh6.googleusercontent.com/7jQN3iEGtnryZalWRjl-OSC8ZBqVZScxssG3wgU-5u4iyAcBzpaV8Sprhb4aq4m_SVDcpPm2ldUMYv5UoEIXzZXcEhUxtKDL7xE7bcHXCaKeG_DHEy_27z-6u1_rKtiY52rTtFasXVc44Iy-OQ)

**paginering** vs **vaste partitionering:** 

- Partities bij paginering zijn kleiner.Processen bij paginering bezetten verschillende partities die niet aaneengesloten hoeven te zijn.
- Bij paginering is geen externe fragmentatie.
- Bij paginering wordt de interne fragmentatie beperkt tot een fractie voor de laatste pagina van het proces.

**adresvertaling bij paginering:** 
- Door de MMU (memory management unit) 
- Voor de grootte van de pagina’s en frames wordt een macht van 2 gekozen. Hierdoor kunnen logische adressen beschouwd blijven worden als relatieve adressen, verwijzend naar de oorsprong van het programma. 

51. >Bespreek de werking van segmentatie (zonder virtueel geheugen)? Wat is het verschil tussen
    >dynamische partitionering en segmentatie? Waarom wordt dit model voor de gebruiker bewust
    >zichtbaar wordt gehouden. Geef een voorbeeld waar je handig gebruik kan maken van segmenten. 
    >
    >Hoe gebeurt de adresvertaling bij segmentatie (maak een schets)? (p119)

**Segmentatie** lijkt op **dynamisch partitionering**, zoals **paginering** lijkt op **vaste partitionering**. Bij segmentatie worden de blokken **niet uniform** verdeeld in blokken. Elk logisch adres bestaat uit twee onafhankelijke dimensies: een segmentnummer en een relatieve positie binnen het segment. Het hoofdgeheugen blijft 1-dimensionale, lineaire, rij adressen, vertrekkend van 0. De koppeling tussen het tweedimensionale en eendimensionale geheugen beeld gebeurt aan de hand van een segmenttabel. Het besturingssysteem houdt een segmenttabel bij voor elk proces, die de fysieke locatie van elk segment van het proces bevat. **In tegenstelling tot dynamische partitionering** kunnen processen bij segmentatie meerdere partities in het hoofdgeheugen bezetten, die niet aaneengesloten hoeven te zijn.Segmentatie **vermijdt interne fragmentatie, maar is onderhevig aan externe fragmentatie,** een verschijnsel dat hier checker-boarding wordt genoemd.

![img](https://lh5.googleusercontent.com/opf8K6dgOF2SP4k-wdjAekv94QE0LpuyZhGTKP1WjQr_m27ezHoh80S7olNQpKoKm4Me2blvaf8-QVe_z-O430aw1EElGsnBmW5tiPdPXqCtJk7kGHp8IOoPbzYPRRHfjHR1xg5f1YH04TI-cg)

52. >Bespreek de stappen die moeten ondernomen worden wanneer bij adresvertaling wordt vastgesteld
    >dat een deel van het proces zich niet in het geheugen bevindt? (p121)
    
    Tot nu toe hebben we verondersteld dat het gehele proces in het hoofdgeheugen moet geladen en uitgevoerd worden. Gebruik makend van partitionering of segmentatie kan deze eis versoepeld worden. De uitvoering van een proces kan tijdelijk worden verder gezet indien de pagina's (of segmenten) met de volgende op te vragen instructies en gegevenslocaties zich in het hoofdgeheugen bevinden, ook al zijn andere pagina's of segmenten van het procesbeeld niet aanwezig. Dit concept noemt men **virtueel geheugen.**
    
    Het deel van een proces dat zich op een bepaald moment werkelijk in het hoofdgeheugen (dat nu reeël geheugen wordt genoemd) bevindt , wordt de **residente set** van het proces genoemd.
    
    Het gebruik van virtueel geheugen zorgt voor **overhead**. Telkens naar een **logisch adres** gerefereerd wordt dat **zich niet in het hoofdgeheugen bevindt,** moet niet alleen het OS tweemaal (na de paginafout, en na de interrupt (zie hieronder)) de controle overnemen , maar moet eveneens een ander stuk uitgestapt worden.

**(nummers verwijzen naar nummers uit de figuur)**

1. Op basis van de paginatabel kan de processor vaststellen of alle geheugen verwijzingen betrekking hebben op de locaties die zich in de residente set bevinden. 
2. Wordt er een logisch adres tegengekomen dat zich niet in het hoofdgeheugen bevindt, dan genereert de processor een interrupt die een geheugentoegang fout aangeeft.
3. Het besturingssysteem neemt op dat ogenblik de besturing over, en plaatst een I/O verzoek om het stuk van het procesbeeld met het virtuele adres dat de toegangsfout veroorzaakte, binnen te halen in het hoofdgeheugen. 
4. Is het gewenste stuk eenmaal binnengehaald in het hoofdgeheugen, dan wordt opnieuw een interrupt gegeneerd
5. .Het besturingssysteem kan hierdoor de paginatabellen bijwerken.
6. En het betrokken proces terug in de gereed wachtrij plaatsen.



**![img](https://lh3.googleusercontent.com/2TyS2YEi7Nwc2_xD1leDHuu1rhUQh_S9fosPDJhN8TOsD71E_Nkg6SqfiEG7M3kcCyV0bENQuemGLnreAjEq5HFWADVxT3D2koFyeMRj59IZ8W9TqVNrbYiqvLpC1tpAcaDHI2thYZbAquOfqA)**

53. >Wat zijn de drie voordelen van het gebruik van virtueel geheugen? Wat is het nadeel van het gebruik
    >van virtueel geheugen? (p122)

**Voordelen:**

- Omdat de processen slechts partieel in het hoofdgeheugen geladen worden, is er ruimte voor meer processen. Hierdoor is de kans groter dat minstens één proces zich in de toestand gereed bevindt.
- Het wordt mogelijk dat de geheugen hoeveelheid die elk individueel proces aanspreekt groter is dan het totale hoofdgeheugen. Voor wat de programmeur betreft, wordt het hoofdgeheugen enkel beperkt door de beschikbare schijfruimte. Hij moet zich niet langer zorgen maken over het beschikbaar fysiek geheugen. Hij hoeft ook niet langer na te denken over overlay- of andere benaderingen.
- Het laden van het volledige proces is duidelijk een verspilling als er slechts enkele stukken effectief gebruikt worden vooraleer het programma wordt onderbroken en terug uit het hoofdgeheugen geswapt wordt. Het geheugen wordt efficiënter benut door slechts enkele stukken in te laden. Zorgt voor heel wat overhead. Telkens er naar een logisch adres gerefereerd wordt dat zich niet in het hoofdgeheugen bevindt, moet niet alleen het besturingssysteem tweemaal de controle overnemen, maar moet eveneens een ander stuk uitgeswapt worden.

**Nadelen**:

- Zorgt voor heel wat overhead. Telkens er naar een logisch adres gerefereerd wordt dat zich niet in het hoofdgeheugen bevindt, moet niet alleen het besturingssysteem tweemaal de controle overnemen, maar moet eveneens een ander stuk uitgeswapt worden.

54. >Welke twee parameters moet het besturingssysteem in de gaten houden om te zien of er bij het
    >gebruik van virtueel geheugen te veel dan wel te weinig paginafouten optreden? Wat wordt er
    >bedoeld met “**thrashing**”?  **Hoe** kan het besturingssysteem oordeelkundig **inschatten** welke pagina’s
    >in de toekomst nodig zullen zijn en welke niet? (p122)

- gemiddelde tijd tussen 2 paginafouten **(L)**
- gemiddelde tijd die nodig is om pagina te vervangen **(S)**

**Trashing**: De processor besteedt meer tijd aan het swappen van stukken dan aan het uitvoeren van instructie. Het is essentieel dat besturingssystemen **op basis van de historiek in het recente verleden**, oordeelkundig kunnen inschatten welke stukken niet meer en welke stukken waarschijnlijk wel nog gebruikt zullen worden in de nabije toekomst.



> Vraag 55 en verder heeft de prof laten vallen.



### Theorie lessen

**Les 1:** Inleiding + basisbegrippen computerarchitectuur + functie & kenmerken van moderne besturingssystemen

**Les 2:**  multitasking  + kernel architectuur + uitleg basis comando's find

**Les 3:**  Hoofdstuk 2 processenbeheer

**Les 4:**  Vervolg proceswissel + threads + demo multithreaded applicatie via pthread (01:10)

**Les 5:** Uitleg Labo Deel V: I/O-Systeemaanroepen

**Les 6:** Uitleg Labo Deel VI: Processen en POSIX-threads (pthreads)

**Les 7:**  Vervolg processen: demo base64, demo interprocescommunicatie (adhv pipe)

**Les 8:** Threads: Mutithreading (met workers) + Inter thread communicatie

**Les 9:** Mutexen, Semaforen , shared memory (mmap) & interprocescommunicatie  (adhv semaforen)

**Les 10:** Hoofdstuk 4 geheugenbeheer





### Begrippen

**Besturingssysteem**: Meer eenvoudige, gelaagde interface naar gebruikers en programmeurs toe. Beheert bronnen (processor, geheugen & I/O apparaten)

**Kernel**: Core, Centrale deel van besturingsssysteem

**Subsysteem**: Een Subsysteem is een interface om een vreemd systeem op een host te kunnen runnen. Zo zorgt WSL dat Windows een Linux besturingssysteem kan draaien.

**NT**: New technology (Windows)

**Executive**: Deel van het NT besturingssysteem dat in kernelmodus wordt uitgevoerd. Heeft volledige toegang tot systeemgegevens en hardware. 

**System Call**: Een **systeemaanroep**, of **system call**, is een verzoek van een computerprogramma aan het besturingssysteem om een bepaalde taak uit te voeren voor het programma. Alle systeemaanroepen samen vormen de interface (de API) van het besturingssysteem of de kernel.

