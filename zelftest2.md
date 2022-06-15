# Zelftest2

1. >Zoek naar alle bestanden of symlinks met een grootte van 1M of die de
   >voorbije 24u werden gewijzigd.

   ```bash
   ## Onderstaande codefragment in terminal uit te voeren
   mkdir test
   cd test
   mkdir dir
   
   
   mknod pipe p # Om een block specia device aan te maken
   
   # Bestanden aanmaken die > 1M
   head -c $((1024*1024+1)) < /dev/zero > bestand
   head -c $((1024*1024+1)) < /dev/zero > bestand2
   
   # Symbolische links maken
   cp -s dir/bestand link1
   cp -s dir/bestand2 link2
   
   # Pipe aanmaken
   mkfifo pipe2
   
   # Tijdstip van een bestand veranderen
   touch -d '2022101' bestand
   
   ## Opbouw commando
   # find . \( -type f -o -type l \)
   # find . \( -type f -o -type l \) -exec ls -l \{\} \;
   
   # Grootte bestand moet +1 MB zijn
   # -1M = negatief getal = kleinder dan 1 MB
   # +1M = positief getal = groter dan 1 MB
   find . \( -type f -o -type l \) -a \(-size +1M -o -mtime -1 \) -exec ls -l \{\} \;
   
   # L = Link ook gaan volgen, is feitelijk een vorm van backtracking
   Find -L . \( -type f -o -type l \) -a \(-size +1M -o -mtime -1 \) -exec ls -l \{\} \;
   ```
   
2. > Geef hieronder de opdracht of pipeline van opdrachten om de bovenstaande
      > uitvoer te ordenen op basis van het inodenummer (grootste eerst, kleinste
      > laatst).
   
   ```bash
   # -1M = negatief getal = kleinder dan 1 MB
   # +1M = positief getal = groter dan 1 MB
   
   # opzoeken in manpage find
   # %i = inode nummer
   # %p = processnummer
   
   # -k1,1 -> alfanumeriek sorteren bij het eerste veld en eidigen bij het eerste veld
   # -k1n,1n -> numeriek
   # -k1rn,1rn -> reverse numeriek
   # -k1rn,1rn -k2,2 -> reverse numeriek voor eerste sleutel en tweede sleutel alfanumeriek
   
   # je moet doorhebben dat je printf moet gebruiken om de output te manipuleren
   find . \( -type f -o -type l \) -a \( -size -1M -o -mtime -1 \) -printf "%i %p\n" | sort -t " " -k1rn,1rn \ cut -d " " -f2
   ```
   
   
   
3. >Volgens de manpagina van find kan je met de optie -o op twee dingen testen
      >en zal de naam van het object uitgeprint worden wanneer een van de twee
      >voorwaarden voldaan is. Ook kan je haakjes gebruiken om dit te doen (let
      >wel, in BASH moet je die wel escapen met een \ om aan te geven dat die
      >haken voor find bedoeld zijn). Geef een overzicht van alle bestanden in de
      >map /etc die een grootte hebben kleiner dan 10K of groter dan 100K.

   ```bash
   # du -h om de file- en directorygrootte human readble te maken
   find /etc -type f \( -size -10k -o size +100k \) -exec du -h {} \;
   ```

4. >Geef van alle bestanden die zich bevinden in de /etc directory bevinden en
   >die een grootte hebben van minder dan 10K het aantal lijnen. Doe dit op
   >twee manieren:
   >a. Met de optie -exec van find
   >b. Door alle namen via een pipe door te geven naar het commando xargs
   >die dan op iedere bestandsnaam het commando wc uitvoert.

```bash
## Onderstaande codefragment in terminal uit te voeren

find /etc -type f -size -10k - exec wc -l \{\} \;

# minder kindprocessen, er gaat meer gegroepeerd worden
# potentieel risco dat het commandolijn te lang is
find /etc -type f -size -10k - exec wc -l \{\} \+

# xargs gebruiken om het commando op te splitsen
# n1 = neem element per element en pas het commando echo toe
#xargs -n1

#xargs -n1 wc -l

find /etc -type f -size -10k - exec wc -l \{\} \+ | xargs -n1 wc -l

# als diff niets terug geeft weet je dat het iedentiek is, was om de output van twee commando's uit te testen
diff <(find /etc -type f -size -10k - exec wc -l \{\} \;) <(find /etc -type f -size -10k - exec wc -l \{\} \+ | xargs -n1 wc -l)
```

5. >Bij het bovenstaande heb je wellicht geen rekening gehouden met
   >bestandsnamen die spaties bevatten. Bij find kan je vragen om de
   >bestandsnamen af te sluiten met een null-karakter i.p.v. een newline (\n)
   >door middel van de optie -print0. Gebruik nu opnieuw xargs met bijhorende
   >parameters om op iedere null-terminated bestandsnaam “wc -l” toe te
   >passen.

   ```bash
   ## Onderstaande codefragment in terminal uit te voeren
   
   # prnten met 0-terminated karakter
   find . -type f -printf0 
   find . -type f -10k -printf0 | xargs -0 -n1 wc -l
   ```

   

6. >Gebruik het commando shuf om 16 getallen te genereren tussen 10 en 50 en
   >gebruik xargs om die uit te schrijven in een raster van 4 bij 4.

   ```bash
   ## Onderstaande codefragment in terminal uit te voeren
   
   shuf -i 10-50 -n 16
   
   #head -c 64 /dev/urandom | od -An -tud8 # meer supplesse
   # r = mag meermaals voorkomen
   # echo moet daar niet staan, default optie bij xargs
   # n = het aantal kolommen
   shuf -i 10-50 -n 6 -r | xargs -n 4 echo
   
   #Rekenen in shell (ter info, wordt semi-verwacht te kunnen)
   
   `echo scale=2 \; $(shif -i 10-50 -n2|paste -s -d "/"|bc`
   ```

7. > Zelfde vraag als hierboven maar doe dit nu met printf (2 karakter per getal)
      > en command substitution. Je zal zien dat dit een betere uitlijning geeft
      > wanneer je “%2d” gebruikt voor ieder getal.

   ```bash
   shuf -i 10-50 -n 6 -r | xargs -n 4 printf "%2d %2d %2d %2d\n"
   ```

   

8. > Hoe worden lijneindes aangegeven in Windows en hoe gebeurt dit in
   > Unix/Linux? Waarom is het belangrijk om te werken met
   > tekstbestanden/scripts/... die regeleindes hebben overeenkomstig het
   > besturingssysteem? Geef enkele voorbeelden waar het fout kan gaan.

```bash
#!/bin/bash

# Voorbeeld wrm het problemen geeft voor dos2unix om bestanden vanop een windows naar een linux pc te processen.
# In essentie komt het er op neer dat ieder bestand dat door een windows-toepassing wordt aangemaakt 
# of bewerkt, een "CR" "LF" (Cariage Return) (Line Feed) heeft op het einde van iedere lijn. Bij Linux is dat enkel \n

while read lijn; do
    echo $lijn
done < /etc/password



```

**Door het commando `tr` te gebruiken**

```bash
tr -d '\r' < 8.sh | bash
```



9. > Geef de reguliere expressie om te testen of een lijn een getal bevat. Geef nu
   > de reguliere expressie om te testen of een lijn uitsluitend een getal bevat.
   > Maak een testbestand aan waar je enkele lijnen naartoe wegschrijft die
   > voldoen en die niet voldoen. Test vervolgens met het commando grep uit of
   > de reguliere expressie die je hebt uitgedacht, voldoet.

```bash
grep -E "^[0-9]+$" bestand.txt
```

10. >Een geldig e-mailadres voldoet aan de volgende regel “naam@domeinnaam”
    >waarbij zowel de naam als de domeinnaam kan bestaan uit verschillende
    >delen gescheiden door punten. De (domein)naam bestaat uitsluitend uit
    >letters en/of cijfers. Test opnieuw uit of een regel van een tekstbestand
    >uitsluitend een geldig e-mailadres bevat (dus tussen het begin en het einde
    >van de regel bevindt zich een e-mailadres).

    ```bash
    grep -E "([a-zA-Z0-9]+\.?)+[^.@]@([a-zA-Z0-9]+\.?)+[^.@]$" 
    ```

    

11. > Waarvoor dient in een script de shebang-lijn? (i.e. #!/bin/bash)?

    Dient om aan te geven wat de interpreter is

12. > Wat is het type van iedere variabele in BASH?

    String

13. >Wanneer is het handig of zelfs noodzakelijk om bij het uitschrijven van een
    >variabele de variabelenaam tussen accolades te plaatsen?

    ```bash
    naam= wim
    echo -e "de${naam}is"
    ```

    

14. >Schrijf een BASH-script dat een getal inleest (geen controle nodig) en de
    >derdemacht van dat getal naar het scherm schrijft (via arithmetic expansion).
    >
    >Een intermezzo....de magie van process substition...
    >Bij interprocescommunicatie wordt meestal gebruikgemaakt van de verticale
    >streep en voldoet een opdrachtregel aan de volgende syntax:
    >opdracht1 | opdracht2 | opdracht3
    >De uitvoer van opdracht1 wordt via een anonieme pipe naar het invoerkanaal
    >van het proces waar opdracht2 in uitgevoerd wordt. Hetzelfde met de uitvoer
    >van opdracht2 naar de invoer van opdracht3.
    >Hoe handig deze syntax is, er is één groot nadeel aan verbonden. Dat is dat
    >iedere opdracht na de verticale streep uitgevoerd wordt in een subshell van
    >de huidige shell. Dus wanneer bv. variabelen wil gaan inlezen via de
    >opdrachtlijn:
    >echo 1 2 3 | read a b c
    >echo $a
    >kom je er altijd op uit dat als je de inhoud van de variabele a wil uitschrijven
    >dat die precies niet bestaat. Dat is niet abnormaal aangezien je nu zou
    >moeten weten dat het inlezen en dus ook het toekennen is gebeurd in een
    >subshell en niet in de shell waar je de oorspronkelijke “echo 1 2 3” hebt laten
    >uitvoeren.
    >
    >Om dit wel mogelijk te maken zou je maar al te graag de volgorde van de
    >opdrachten omdraaien en dat kan wanneer je gebruikmaakt van process
    >substitution. De syntax is complexer als met de verticale streep maar is veel
    >flexibeler te gebruiken. De bovenstaande opdracht kan als volgt worden
    >geschreven:
    >read a b c < <**(echo 1 2 3)**
    >Het in het vetgedrukte gedeelte is proces substitution.
    >Het eerste <-teken staat voor input redirection onmiddellijk gevolgd door een
    >spatie, gevolgd door een <(opdracht). Let op, dit is aan elkaar geschreven en
    >er kan zeker geen spatie staan tussen het <-teken en de openende ronde
    >haak aangezien een <-teken omringd door spaties in BASH duidt op input
    >redirection.
    >Wat er achter de schermen gebeurt is hetzelfde als met de verticale streep. Er
    >worden twee kindprocessen aangemaakt die via een tijdelijke pipe met elkaar
    >data uitwisselen. Hierbij wordt de <(opdracht) vervangen door een tijdelijk
    >bestand dat zich in de /dev map bevindt en dat eigenlijk een gateway is naar
    >de leesfiledescriptor van de pipe. Dus net zoals met I/O kan je eenvoudigweg
    >via een bestand toegang krijgen tot een structuur in de kernel.
    >Even terzijde maar **>(opdracht)** kan ook. Hier zal je dus een tijdelijk bestand
    >zien verschijnen in de /dev map dat een gateway is naar schrijffiledescriptor
    >van de pipe.
    >Enkele voorbeelden:
    >ls <(:) >(:) #hier zie je de tijdelijke bestanden voor interprocescommunicatie
    >grep -E “^pass” <(ls -lR /etc)
    >grep -E “^pass” < <(ls -lR /etc)
    >De laatste twee opdrachten geven identieke uitvoer. Bij de eerste opdracht
    >zal **<(ls -lR)** vervangen worden door een tijdelijk bestand dat zich in de /dev-
    >map bevindt en waarvan grep gewoon van leest. Bij de tweede opdracht
    >wordt er gewerkt met input redirection waarbij de invoer voor het
    >
    >commando grep komt van het tijdelijke bestand in de /dev-map. Onnodig om
    >te zeggen dat de input redirection onnodig is!
    >Heb je bv. een kopie gemaakt van een map, dan kan je heel eenvoudig
    >controleren of de inhoud van het origineel en van de kopie hetzelfde is. Dit
    >kan door: **diff <(ls -lR origineel) <(ls -lR kopie)**
    >Zoals onmiddellijk duidelijk wordt is dit met de verticale strepen heel wat
    >lastiger om niet te zeggen onmogelijk! Hier worden achter de schermen drie
    >kindprocessen aangemaakt en leest diff van zowel het ene kind (ls -lR
    >origineel) als van het tweede kind (ls -lR kopie). Beide ls-processen hebben
    >een pipe naar het commando diff en voor iedere pipe wordt een tijdelijk
    >bestand voorzien waardoor diff kan lezen van die pipes alsof het van reguliere
    >bestanden leest.

```bash
read -r getal
echo $(( getal**3 ))
```



15. >Het commando read splitst op basis van de inhoud van de IFS-variabele. Zijn
    >er meer variabelen dan dat er elementen zijn, dan zullen de overtollige
    >variabele leeg zijn. Zijn er minder variabelen dan dat er elementen zijn dan zal
    >de laatste variabele het restant van de lijn bevatten.
    >IFS-wijzigen om bv. read te laten splitsen op basis van iets anders dan
    >whitespace kan gewoon door de volgende constructie:
    >IFS=. read a b c d <<< string
    >De <<< is string input redirection en betekent dus dat je van plan bent om
    >niet van een bestand te lezen maar van een string.
    >IFS=. read a b c d <<< “192.168.16.16”
    >echo $a
    >Wanneer je IFS een waarde toekent vóór een commando dan zal IFS enkel en
    >alleen gewijzigd zijn voor dat commando en dus niet voor de rest van het
    >script! Dus dan gaat het om een wijziging in de context van dat commando.
    >Schrijf een script dat een IPv4-adres inleest en dat daarna dat IPv4-adres
    >opsplitst in vier variabelen. Daarna check je of ieder van deze variabelen
    >
    >bestaat en of dat het een getal voorstelt en of dat dat getal binnen de
    >grenzen [0-255] ligt. Indien deze voorwaarde niet voldaan is, dan is het geen
    >geldig IPv4-adres! Het script eindigt met een passende foutboodschap
    >wanneer er geen geldig IPv4 adres werd ingelezen. (Met een reguliere
    >expressie testen op de geldigheid van een IPv4-adres is niet eenvoudig maar
    >de constructie hierboven maakt het makkelijker)

```bash
#!/bin/bash

while read ip; do
	if [[ "$ip" =~ \.$ ]];then
		echo "$ip" is een fout IP-adres! >&2
		continue
	fi
	IFS=. array=( $ip )
	if (( ${#array[@]} != 4 ));then
	       echo "$ip" is een fout IP-adres >&2
	       continue
       	fi
	for i in ${array[@]};do
		#wanneer juist => als het een getal is EN als het 0<=getal<=255
		#wanneer foutboodschap => als het geen geen getal is OF het is niet gelegen tussen 0<=getal<=255
		if [[ ! "$i" =~ ^[0-9]*$ ]] || ((i>255 || i<0)); then
			echo "$ip" stelt geen geldig IP-adres voor! >&2
			continue
		fi
	done

	unset array
done < "$1"

```



16. >Schrijf nu hetzelfde script als hierboven maar geef het IP-adres als een
    >parameter mee met het script. Als de parameter niet wordt meegegeven, dan
    >wordt verondersteld dat het IP-adres dat je moet checken 192.168.16.8 is.

    ```bash
    #!/bin/bash
    
    ip=${1:-192.168.16.8}
    	if [[ "$ip" =~ \.$ ]];then
    		echo "$ip" is een fout IP-adres! >&2
    		continue
    	fi
    	IFS=. array=( $ip )
    	if (( ${#array[@]} != 4 ));then
    	       echo "$ip" is een fout IP-adres >&2
    	       continue
           	fi
    	for i in ${array[@]};do
    		#wanneer juist => als het een getal is EN als het 0<=getal<=255
    		#wanneer foutboodschap => als het geen geen getal is OF het is niet gelegen tussen 0<=getal<=255
    		if [[ ! "$i" =~ ^[0-9]*$ ]] || ((i>255 || i<0)); then
    			echo "$ip" stelt geen geldig IP-adres voor! >&2
    			continue
    		fi
    	done
    
    	unset array
    
    ```

    

17. >Gebruik stringoperatoren om alle klinkers uit een woord te vervangen door
    >een punt. (probeer dit ook eens uit via de externe opdracht tr

    ```bash
    tr [aeiouyAEIOY] . <<< "hallo wim" # input redirection -> h.all. w.m
    
    tekst="halle wim"
    echo ${tekst//[aeoiuy]/.} # -> h.all. w.m
    ```

    

18. >Hoe kan je van een getal dat de bestandsgrootte in bytes voorstelt en waarbij
    >digit grouping gebruikt wordt, bv. 131.273.678, één getal maken en dat getal
    >in kilobytes naar het scherm schrijven.

    ```bash
    #besproken bij pagefile.out (vorige week)
    ```

    

19. >Schrijf in C een eigen versie van het commando du. De bestandsgrootte kan je
    >opvragen met de syscall stat.

    ```c
    #include <sys/stat.h>
    #include <stdio.h>
    #include <dirent.h>
    #include <fcntl.h>
    
    #define PATH_MAX 4096
    
    void checkDir(const char *);
    
    void loopDir(DIR *, const char *);
    
    struct stat st;
    
    void loopDir(DIR *dir, const char *base) {
        struct dirent *ent;
    
        while ((ent = readdir(dir)) != NULL) {
            if (ent->d_name[0] == '.') {
                continue;
            }
    
            char fname[PATH_MAX];
            snprintf(fname, sizeof(fname), "%s/%s", base, ent->d_name);
    
            stat(fname, &st);
    
            if (!S_ISREG(st.st_mode)) { // is een regulier bestand
                printf("%llu\t%s\n", st.st_blocks, fname);
            } else { // is een directory
                checkDir(fname);
            }
        }
    }
    
    void checkDir(const char *dirName) {
        DIR *dir = opendir(dirName);
        if (dir != NULL) {
            loopDir(dir, dirName);
            closedir(dir);
        } else {
            stat(dirName, &st);
            printf("%llu\t%s\n", st.st_blocks, dirName);
        }
    }
    
    int main(int argc, char *argv[]) {
        if (argc == 1) {
            checkDir(".");
        }
        for (int i = 1; i < argc; ++i) {
            checkDir(argv[i]);
        }
        return 0;
    }
    ```
    
20. >Schrijf in C een eigen versie van het commando “wc -l” dat van de laatste 100
    >bytes van de bestanden die meegegeven worden op de commandolijn het
    >aantal lijnen bepaalt. In BASH zou je dit als volgt schrijven .... tail -c 100
    >bestand1 bestand2| wc -l. Doe dit zonder pipe en zonder execve syscalls
    >maar dus louter met open/read/write/close/...!

    ```c
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
    
    int main(int argc, char **argv){
    	for (int i=1;i<argc;i++){
    		int fd=open(argv[i],O_RDONLY);
    		if (lseek(fd,-100,SEEK_END)<0){ //juist positioneren
    			perror(argv[i]);
    			continue;
    		}
    		unsigned char buffer[100];
    		int n=read(fd,buffer,100);
    		if (n<0){
    			perror(argv[i]);
    			continue;
    		}
    		int teller=0;
    		for(int j=0;j<n;j++){
    			if (buffer[j]=='\n'){
    				teller++;
    			}
    		}	
    		printf("%d %s\n",teller,argv[i]);
    		if (close(fd)<0){
    			perror(argv[i]);
    			continue;
    		}
    	}
    	return 0;
    }
    ```

    

21. > Doe nu hetzelfde als vorige vraag waar je wel gebruikmaakt van
    > kindprocessen en een pipe als IPC. Gebruik ook execve of gelijkaardige
    > syscalls om de programma’s aan te roepen.

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
    
    int main(int argc, char **argv){
    	int fd[2];
    	if (pipe(fd)<0){
    		perror(argv[0]);
    		exit(1);
    	}
    	int pid=fork();
    	if (pid==0){
    		//tail -c 100 argv[1] argv[2] ...
    		close(fd[0]);
    		//dup2(fd[1],1);
    		close(1);
    		dup(fd[1]);
    		char* argv2[argc+2];
    		int teller=0;
    		char *hulp[]={"tail","-c","100",0};
    		argv2[teller++]=hulp[0];
    		argv2[teller++]=hulp[1];
    		argv2[teller++]=hulp[2];
    
    		for(int i=1;i<argc;i++) {
    			argv2[teller++]=argv[i];
    		}
    		argv2[teller]=0;
    		if (execvp("tail",argv2)<0){
    			perror(argv[0]);
    			exit(1);
    		}
    		return 0;
    	}
    	int pid2=fork();
    	if (pid2==0){
    		//wc -l
    		close(fd[1]);
    		close(0);
    		dup(fd[0]);
    		if (execlp("wc","wc","-l",(char*) 0)<0){
    			perror(argv[0]);
    			exit(1);
    		}
    		return 0;
    	}
    	close(fd[0]);
    	close(fd[1]);
    	waitpid(pid,NULL,0);
    	waitpid(pid2,NULL,0);
    	return 0;
    }
    
    ```

    

22. > Gegeven volgende situatie:
    >
    > ![Imgur](https://imgur.com/t3eWRBF.png)
    >
    > C1 en C2 zijn kindprocessen van P. C3 is een kindproces van C1.
    > De werking is als volgt: 
    >
    > Zowel de parent P als child C3 genereren een willekeurig
    > getal. De parent stuurt zijn getal naar C1 en child C3 stuurt zijn willekeurig getal
    > naar C2. Child C2 vermenigvuldigt het ontvangen getal van C3 met twee en stuurt
    > dat getal door naar C1. C1 telt het getal van de parent P samen met het getal
    > ontvangen van child C2 en schrijft de som naar het scherm.
    > Schrijf een volledig C-programma dat alle processen aanmaakt en ervoor zorgt dat
    > C1 de som van g1 en g2*2 naar het scherm schrijft.

     ```bash
     ```

    



