# Examenvragen besturingssystemen



1. > Wat is het verschil tussen **symmetrische** en **asymmetrische** **multiprocessing**?

In een **asymmetrische** multiprocessor wordt de kernel van het besturingssysteem altijd uitgevoerd op een bepaalde *master processor*. Deze is verantwoordelijk voor scheduling en heeft volledige controle over het volledige geheugen en andere bronnen. De *andere processoren* kunnen alleen gebruikersprogramma’s en hulpprogramma’s van het besturingssysteem uitvoeren.

Bij een **symmetrische** multiprocessor kan de kernel worden uitgevoerd op *elke processor* (elke processor voert een volledige kopie van het besturingssysteem uit *****) oftewel kan de kernel worden opgebouwd als meerdere processen of threads. Symmetrische multiprocessing biedt echter ruime mogelijkheden op het gebied van beschikbaarheid (fouttolerantie) en stapsgewijze uitbreidingsmogelijkheden.

***** Deze mogelijkheid stelt hogere eisen aan het besturingssysteem voor communicatie tussen de processoren en het syncen van het aanspreken op bronnen.

![Imgur](https://imgur.com/acPC69G.png)



2. > Wat moet je voorzien om op een Unix-systeem Windows applicaties te kunnen uitvoeren?

   

3. > Bespreek hoe je op Windows een Unix-applicatie kan uitvoeren? Wat wordt in deze context bedoeld
   > met een subsysteem?

4. > Geef vier mogelijke ontwerpen van kernels. Bespreek bij elk hun voor- en nadelen en of ze nog
   > gebruikt worden.