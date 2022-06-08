# Examenvragen besturingssystemen

### Hoofdstuk 1

1. > Wat is het verschil tussen **symmetrische** en **asymmetrische** **multiprocessing**?

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

- Symmetrische multiprocessing biedt  ruime mogelijkheden op het gebied van beschikbaarheid (fouttolerantie) en stapsgewijze uitbreidingsmogelijkheden.



**con's symmetrische multiprocessor :**

- stelt hogere eisen aan het besturingssysteem voor communicatie tussen de processoren en het syncen van het aanspreken op bronnen.
- geheugenbeheer veel complexer wanneer processoren aanvullend over een eigen cache bezitten.

![Imgur](https://imgur.com/acPC69G.png)



2. > Wat moet je voorzien om op een Unix-systeem Windows applicaties te kunnen uitvoeren?

   Je hebt Virtuele machines nodig om Windows-Toepassingen uit te voeren op een computer waarop Linux is geïnstalleerd.
   
   
   
3. > Bespreek hoe je op Windows een Unix-applicatie kan uitvoeren? Wat wordt in deze context bedoeld met een subsysteem? 
   
   De omgevingssusbsystemen zorgen voor de interactie met de gebruiker en voor een API set. NT (Windows **N**ew Technology) kan hierdoor toepassingen ondersteunen die geschreven zijn voor uiteenlopende besturingssystemen zoals Linux (**W**indows **S**usbsystem for **L**inux = **WSL**).
   
   
   
   **subsysteem:**

   Een Subsysteem is een interface om een vreemd systeem op een host te kunnen runnen. Zo zorgt WSL dat Windows een Linux besturingssysteem kan draaien.
   
   
   
4. > Geef drie mogelijke ontwerpen van kernels. Bespreek bij elk hun voor- en nadelen en of ze nog gebruikt worden.

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

   **2. Gelaagde kernel:**

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

   3. **Micro kernel:**

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

5. > Gegeven onderstaande figuur: Geef van elke component in de “executive” aan wat de werking ervan is.

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

6. > Wat is het verschil tussen een programma en een proces? Wat zijn de vorige definities van een proces

7. > Waarom is het model met twee procestoestanden actief en niet actief niet interessant? Wat is het probleem dat je hier zal tegenkomen? 

8. >  Geef alle toestanden waarin een thread zich kan bevinden? Bespreek wanneer een thread van de ene toestand in de andere zal terechtkomen. 

   
