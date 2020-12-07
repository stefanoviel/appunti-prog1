## ARCHITETTURA HARDWARE/SOFTWARE DI UN COMPILATORE

#### INDICE:

- archiettura di Von Newman
- Memoria



*Storia del Calcolatore*

* primo è ENIAC, che si programmava con il contatto di fili in modo manuale
* Poi arrivano quelli più sviluppati:
  * MAINFRAME: grandi dimensioni e elevata potenza, di solito condiviso
  * PERSONAL COMPUTER: dotati di monitor e tastiera separati. Dotati di memoria di massa interni o esterni alla memoria centrale. Più economico.
  * LAPTOP: versione portatile del PC, quando quest'ultimo inizia a prendere piede. Poi inizia la miniaturizzazione del laptop, perchè ce n'erano le possibilità. 
  * HANDHELD COMPUTER (SMARTPHONE): anche qui miniaturizzazione dei cellulari.
  * WHERABLE-COMPUTER: tipo smartwatch, che sono complementari i computer e sono piuttosto potente. Particolare attenzione alla sensoristica all'interno di questi oggetti.



Com'è stata possibile la miniaturizzazione? Attraverso la legge di Moore (sotto).

![image-20200930152001573](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930152001573.png)

Poi si lega la quantità di transistor alla velocità del clock. Poi questo dato si fermerà intorno ai 3 ghz. Il problema era per la dissipazione del calore. Nuova strada: multithreading: il clock arriva in più parti della scheda e quindi si passava il segnale di clock a tutti gli organ**i senza latenza e senza mancanze.

![image-20200930152123563](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930152123563.png)



## ORGANIZZAZIONE SOFTWARE DI UN CALCOLATORE:

![image-20200930152539660](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930152539660.png)

Questo è un normale schema di un calcolatore. Tutto si basa su quello che ha sotto e può comunicare solo con i blocchi adiacenti (es. Hardware può accedere solo al sistema operativo). 

L'unico che può operare con l'hardware è il sistema operatore. Noi al momento ci mettiamo nel software applicativo (che non parla assolutamente con il sistema operativo), nel senso che non toccheremo, al momento, di gestione del sistema operativo e altro.



## Architettura Hardware:

![image-20200930152948825](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930152948825.png)

- CPU: central process unit, posto dove avvengono i programmi logici.
- Memoria Centrale: memoria volatile, per esecuzione del programma.
- memoria di massa: memoria dove i dati rimangono anche senza corrente.
- Periferiche: tutto quello che permette l'interazione con il compilatore.
- Bus di sistema: permette il collegamento fra le periferiche e gli oggetti hardware.



### MACCHINA VON NEUMANN:

#### CPU: UNITA' DI ELABORAZIONE

- unità di elaborazione del calcolatore.
  - carica le istruzioni dalla memoria centrale
  - interpreta le istruzioni
  - esegue le istruzioni
- altamente specializzata, perché sa eseguire poche operazioni molto velocemente.
- il lavoro della CPU è scandito dal clock (orologio interno).
  - più elevato è la frequenza degli impulsi più sono le istruzioni riesce a eseguire al secondo.
  
  - si misura in Hz (1 Hz = 1 Ciclo)
  
  - adesso si lavora in parallelo attraverso il clock tipo "condiviso", cioè tutti ottengono lo stesso clock sincronizzato e eseguono contemporaneamente.
  
    ----
  
- FUNZIONAMENTO: 
  - c'è bisogno di qualcosa che organizzi le azioni da fare prima e dopo e le passi alla cpu.
  - le esecuzioni sono, di solo sequenziali. Nel caso sia "parallelabile", cioè i rami dei calcoli si possono spezzare, c'è la necessità di riunire i risultati poi.
  - Utilizza la rappresentazione binaria(ON/OFF), perché così lavora il processore. Per questo negli anni si sono "astratte" forme per rappresentare tutto quello che ci circonda come oggetto binario. (Musica, Foto, Video, ...).
    - Es: Rappresentazione dei Caratteri. ASCII, poi diventata extended-ASCII. 
    - ![image-20200930154216246](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930154216246.png)
    - il BYTE è l'oggetto che viene utilizzato.
    - ci sono standard per tutte le lingue, perché ci sono un sacco di lettere nelle lingue del mondo.
    - Il BYTE:
    - ![image-20200930154322671](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930154322671.png)

----



#### MEMORIA CENTRALE:

- è una memoria che deve essere velocissima, ma volatile(una volta che il programma finisce, o non c'è più il diritto di avere dello spazio o non c'è proprio lo spazio).

- accoglie la memoria e i dati per far funzionare i programmi.

- concettualmente è composta da sequenze di celle ognuna della quali contiene delle parole, **word**

  - ad ogni cella si può accedere specificandone l'indirizzo. Questo serve per leggere o scrivere il valore al suo interno.

  - ogni Word è creata da una quantità di bit che dipende dalla macchina

    ![image-20200930155410000](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930155410000.png)

- la memoria centrale di solito è realizzata da una **RAM** (Random Access Memory), memoria ad accesso casuale. 

  - Random: non devo attraversare tutti gli indirizzi per sapere quello che sto cercando(ogni cosa è accessibile). Rende il tempo di accesso indipendente dalla località di memoria. 
  - prima bisognava aspettare che il nastro magnetico arrivasse alla tua località.

- Memoria Volatile: il contenuto si perde quando si spegne la macchina.

  - Tutte le memorie sono ad accesso dinamico ma possono essere DRAM o SRAM ( particolari non necessari).

- **ROM**: READ-ONLY MEMORY

  - caratteristiche simili alla RAM
  - accesso molto veloce
  - si tratta di memorie permanenti su cui però non si può scrivere
  - Tipicamente usato per memorizzare dati e programmi che servono al momento dell'accensione dell'elaboratore, prima del caricamento del BIOS
  - BIOS (Basic Input-Output System)



### MEMORIA CENTRALE:

![image-20200930160038403](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930160038403.png)

- Come è fatta la memoria centrale: appare come una lista di parole, un mattoncino orizzontale che è creato da 16 bit (H=16bit).
- posso memorizzare tanti valore binari quanti 2^16
- gli indirizzi sono assegnati da 0 a 1023, per avere 1024 indirizzi.
- non si può rappresentare in memoria cose più grandi di 2^16 e non si può eccedere a 1024.
  - Ma se si eccede? Ci sono i registri (chiamati così per distinguerli) nella CPU:
    -  AR (Address register), almeno di 10 bit
    - Registro dati (DR): spostare da memoria a CPU, elementi di supporto al calcolo. Contiene di solito dati da leggere o da scrivere.



#### UNITA' DI ELABORAZIONE: cpu

![image-20200930160755314](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930160755314.png)

* Program Counter: ti dà gli indirizzi dove andare a prendere la prossima istruzione

* Registro Istruzioni (INTR): segnala il funzionamento periferiche.

* CIR: registro istruzione corrente

* Registri: luoghi di memoria per eseguire operazioni varie

* Registro di Stato (SR): rappresenta tutte le periferiche a cui è collegato e per ottenere un immagine dello stato. Parole che identifica stati, es. attesa, errore...

* ALU esegue le operazioni aritmetico logiche

* In basso il collegamento a tutte le altre componenti dell'architettura: Bus di sistema.

* Unità di controllo (CU): capacità di controllare cosa sta succedendo. Da questa unità può provenire il segnale prelievo di un comando, etc.

  ![image-20200930161315407](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930161315407.png)

* Organizzazione della segnaletica: chi comanda, chi da segnali e chi è più importante. Si usa la coppia **MASTER/SLAVE** => master, unità di controllo di solito, gli altri invece sono slave.

* il Bus sul quale si lanciano i segnali: Bus Dati, Bus Indirizzi, Bus Controlli. (come avere tre corsie che dividono anche semanticamente le informazioni trasmesse).

* FUNZIONAMENTO: 

  ![image-20200930161607002](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930161607002.png)

* 3 fasi: Fetch, Interpretazione (traduzione in binario), Esecuzione (sequenza segnali di controllo per eseguire l'istruzione)

- tipologia di istruzioni: 

  - aritmetiche
  - controllo
  - di trasferimento dei dati: (dai registri, dalla memoria centrale, ...)

- ESEMPIO:

  - istruzione assegnazione: c <= a+b

    - Leggi i valori di a:

      ![image-20200930164350621](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930164350621.png)

      - variabile associata a un indirizzo. 
      - In Address Register (AR) ci deve essere l'informazione di A in 123
      - Sul Bus funzione di READ (ARANCIONE)
      - Il dato va su DATA REGISTER, quindi DR = 42
      - Bus sistema informazioni(GREEN) da segnale di OK 

    - CAMBIARE valore di C:

      - si scrive (BLU) nell'indirizzo 123
      - code OK (GREEN)

  ![image-20200930164844459](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930164844459.png)



* esiste anche nel corpo umano il concetto di memoria a lungo termine, breve termine. Questo però non si può assimilare al cache che viene creata.
  * chunking aumenta la capacità di memoria: modo per velocizzare l'accesso alla memoria => nel computer ci sono tecniche di comprensione





#### 	CONCETTO DI PERIFERICA

* come si fa a parlare con tante periferiche? Non si può creare un linguaggio/codice per ogni periferica

  ![image-20200930165456592](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930165456592.png)

* quando si manda un messaggio alla periferica, un codificatore di indirizzi che gli permette poi di parlare con la cpu. Nel tempo sono state create interfacce di vario tipo (USB: universal Serial Bus)

* GESTIONE DELLE PERIFERICHE:

  * come faccio ad accerdervi?
    1. POLLING: il programma continua a chiedere se è disponibile
       * svantaggi: il controllo avviene anche quando non serve
       * gestione molto semplice, perchè quando aggancio una periferica, essendo un esecuzione deterministica e quindi so di essere pronto.
       * sincrono => con un ciclo di esecuzioni e azioni
    2.  INTERRUPT: il segnale di notifica venga quando la periferica è pronta
       * non ho a che fare con un ciclo
       * essendo un elemento non sincrono, non aspettato, devo sapere gestire eventi asincroni e saperli mettere in coda (quindi gestione più complicata).
       * asincrono => opero sulla base dell'effettiva necessità



 ## CENNI AL SISTEMA OPERATIVO:

* il sistema operativo parla in maniera esclusiva con l'hardware (se si riesce a accedervi in altro modo probabilmente ha un problema).

* E' il modo per dare accesso ai programmi alle risorse del calcolatore. Logicamente la traduzione da programma a calcolatore viene ad alto livello perché al programma non interessa la gestione degli indirizzi o dei registri, ma semplicemente le sue funzioni. Di conseguenza le funzionalità dell'hardware avvengono ad alto livello.

  * il sistema operativo usa quindi astrazione

* [CAPITOLO 13 del libro di testo.]SOURCE

* Il sistema operativo fornisce funzionalità di alto livello e maschera le caratteristiche specifiche di ogni processore.

* AT&T UNIX presentation 1982 Featuring Kernigham => spiegano perché hanno creato UNIX, perché si capiscono che esigenze avessero al tempo.

  ![image-20200930171019756](C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image\image-20200930171019756.png)

* una caratteristica del sistema operativo era la possibilità di servire più di un utente: quando un utente lavora l'altro aspetta? Adesso no. Si usa il multitasking, gli utenti non si mettono in fila ma ognuno ha la propria fila a disposizione

* MACCHINA:

  ![image-20200930171344955](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930171344955.png)

* KERNEL SISTEMA OPERATIVO: (cuore dell'OS)

  * gestione periferiche (ingresso e uscita informazioni).
  * gestione memoria (Fornisce la memoria, _non_ la fornisce (possibile), la da di un certo tipo).
  * gestione dei processi

* Sopra c'è la gestione dei file system, dei comandi e dei programmi

* PROCESSO:

  * il programma è un entità statica: così è

  * questa entità statica ha un esecuzione che fa partire un fetch => questo crea un processo.

  * Quando si avvia un programma si prende un codice e si da in pasto a questa catena che è un entità dinamica. La catena viene quindi eseguita all'interno di un processo.

  * il processo contiene:

    * codice eseguibile del programma (E)
    * stato di esecuzione del programma (S)
    * quindi il processo viene definito in maniera univoca da (E, S) => dato questo programma, il processo è in questo luogo e in questo stato (esecuzione, attesa, ...) => il registro va a valorizzare questo stato del processo.

  * CHI ESEGUE IL PROCESSO:  il processore virtuale che si comporta similmente a un processore reale

    ![image-20200930172036451](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930172036451.png)

  * ogni processore virtuale permette che venga eseguito il processo e il bus di sistema permette di comunicare con il disco. Per cui il processore non ha accesso immediato al disco, ma è mediato dal bus di sistema.

  * CICLO DI VITA DEL PROCESSO: lo stato cambia dalla nascita alla morte, infatti di solito tutti i processi hanno un termine.

    ![image-20200930172919627](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930172919627.png)

    * il processore può avere un processo in esecuzione, pronto per essere eseguito o in attesa. 

    * quando gli si da il go, cioè può decidere di farlo partire e gli fornisce un tempo, scaduto questo può decidere di fornirgliene altro o terminarlo. TIME-SHARING

    * questo viene detto SCHEDULING che anche se può sembrare parallelo è sequenziale. 

      * soluzione tipica: Round-robin (a turno). Si usa con processi con la stessa priorità di esecuzione, cioè tutti hanno lo stesso diritto di essere eseguiti.
      * in realtà poi lavora con la gestione priorità, perchè alcuni processi hanno più importanza di altri.

    * CICLO DI VITA DI UN PROCESSO:

      * inzia l'esecuzione, il processo viene reso pronto.

      * quando il primo processo è pronto va aggiungersi alla coda

      * quando raggiunge il suo turno viene eseguito

        1. Può succedere che il sistema fermi l'esecuzione, cioè non fornisca più altri slot di tempo.

        * il programma torna in coda.	

        2. Avviene un interruzione interna (I/O) => processo in attesa, quando pronto torna in coda.

        3. Fine esecuzione/Errore

      * GESTORE DELLA MEMORIA:

        * partiziona la memoria tra i vari processi che la richiedono
        * l'os deve prendere decisioni, alcune volte gravi, mentre altre volte riesce a mediare.
          * se c'è la necessità di andare oltre i limiti fisici della memoria centrale, quindi dichiara la memoria virtuale:
            * ci guadagna chi chiede memoria, perché gli viene fornita
            * ci perdi in velocità perché crea memoria più lenta, nonché quella più spaziosa
        * Innanzitutto protegge/separa le zone alloccate, in modo che non si sovrascrivano.
        * MEMORIA VIRTUALE o SWAP
        * GESTIONE DELLE PERIFERICHE
        * INTERPRETE COMANDI





## THE C PROGRAMMING LANGUAGE:

processo/Catena di lavoro che parte dal nostro programma e fare in modo che diventi un identità e quindi un processo.

Si passa dallo pseudocodice, e poi si arriva all'esecuzione di istruzioni.

REALIZZAZIONE DI PROGRAMMI:

- Realizzazione Hardware: programmare dispositivo fisici/logici. Linguaggio coincide con il linguaggio macchina.
- Realizzazione Firmware: linguaggio che usa un insieme comune di istruzioni mediante assembly. Livello di programmazione molto basso.
- Realizzazione Software: si usa un linguaggio intermedio che simula funzionalità della macchina fisica. Permette maggiore **flessibilità** (inteso come numero di programmi realizzabili), ma **meno efficente**



##### MACCHINA FISICA:

- esegue le istruzioni scritte nel suo linguaggio, cosiddetto _codice macchina_ (fetch, code, execute). Non esiste il sistema operativo.
- Linguaggio macchina esistono e sono inscindibili.

##### COSA VOGLIO DA UN SISTEMA OPERATIVO:

- gestire in maniera simbolica le aree di memoria, in modo astratto. Voglio che oltre il nome che ci assegno, ci siano le informazioni quali l'indirizzo o l'assegnamento degli indirizzi che vengano assegnate.
- astrarre oggetti o istruzioni complesse in alto livello



##### DIFFUSIONE DEI LINGUAGGI E DECISIONE DI FARE C:

- ci sono tantissimi linguaggi disponibili che sono stati creati o sono particolarmente apprezzati per specifici utilizzi.

- l'insieme dei linguaggi che studieremo permette una comprensione del funzionamento della maggior parte dei linguaggi.

- PERCHE' IL C:

  - allocazione dinamica, e altri aspetti che normalmente si utilizzano in alto livello, ma in C si usa il basso livello
  - gestione della memoria che è molto manuale
  - il C è richiesto/apprezzato dalle aziende
  - ha un posizionamento con l'astrazione che è di alto livello per certi aspetti, ma anche di basso. Questo lo rende molto utile ad esempio negli embedded  system.

- IL LINGUAGGIO C:

  - inventato nel 1972 da Brian Kernighan e Dennis Ritchie ai Bell Telephone Laboratories

    ![image-20200930234742890](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20200930234742890.png)

  - 