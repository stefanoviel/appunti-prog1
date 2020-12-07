# LEZIONE 10/11

- gestione dei files in C
- programmazione ricorsiva (metasoluzione di algoritmi, rispetto ad altri modi di mpostare la soluzione)





### FILES in C

concetto di files e come viene implementato nel linguaggio di programmazione.

Il C mette a disposizione una libreria per la gestione Files. Questa libreria poi si appoggia al sistema operativo. Queste cose avvengono fuori dal programma, quindi hanno effetti sul programma ma non sono al suo interno.

![](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110114934736.png)



La cosa importante per la gestione files sono la gestione delle informazioni (lettura e scrittura => gestione informazioni in ingresso e in uscita).

L'obiettivo del C per la gestione files è di garantire un inferfaccia consistente, cioè fornire lo stessa gestione della periferica fisica, incurante della periferica.

Questa astrazione viene chiamata **STREAM** : cioè periferica astratta che viene messa a disposizione. Dall'altra parte c'è il **file**, che è associato alla periferica fisica. 

Noi ci appoggiamo agli stream che manipoleranno le azioni in ingresso e in uscita.

Lo stream prescinde il tipo di periferica: noi non dobbiamo preoccuparci del tipo di interfaccia che ogni periferica richiede, noi dobbiamo solo preoccuparci delle azioni fatte su questa periferica. Queste azioni (FLUSSI) è esattamente lo stesso, la tastiera funziona come la stampante e come l'usb. Il metodo permette di leggere byte e di scriverli, mediati dall'interfaccia, in modo da aprire un flusso con l'interfaccia della periferica.

Lettura scrittura può funzionare con un accesso casuale nel flusso, ma anche in modo manuale. (lettura in maniera lineare = leggere un byte dietro l'altro, e casuale, che si posiziona all'interno dello stream).

Il nostro modo di comunicazione adesso, con una periferica sarà solo la competenza di inizializzare un flusso, e poi interfacciarsi con questo.

I flussi che vengono aperti (se si associano cioè flussi e periferica) saranno associati a una periferica e si scriverà o si leggerà su questo flusso. 

STREAM = sorgente o destinazione dei dati associato a una periferica (file).

I flussi adesso possono essere di due modi:

- **BINARIO**: sequenza di byte in scrittura e sequenza di byte in lettura (nonostante queste sequenze possano essere pacchettizzare in vari formanti)
  - scriviamo o leggiamo bytes, quindi abbiamo una corrispondenza 1:1, tra quello che è rappresentato e quello che viene letto. 
  - nessuna traduzione dell'informazione, nessuna perdita di informazioni dovuti all'aggiunta o scambio di caratteri (di solito di controllo).
- di tipo **TESTO**: sequenza solo di caratteri in lettura/scrittura
  - sequenze di righe con zero o + caratteri delimitata da '\n'
  - codifica dell'informazione: alcuni caratteri potrebbero non aver corrispondenza nella lettura o scrittura (alcuni caratteri di controllo potrebbero non essere scritti e letti, che rendono non equivalente il flusso in ingresso o in uscita)



### Concetto di Files:

- contenitore di informazioni accessibile e manipolabile con operazioni di 'read' e 'write'
- gestiti da sistema operativo (lo stato della periferica, la sua gestione è gestita dal sistema operativo, che poi si occupa anche di esporre una parte di questa periferica al linguaggio di programmazione)
- operazione di associazione di un file e uno stream avviene con una operazione di **open** (cioè la creazione di un flusso tra periferica e programma), a questo punto si possono scambiare informazioni.
- libreria usata è **stdio.h**
- ma se il flusso deve essere aperto, allora perchè il printf funziona se non si apre il flusso? => quando includi la libreria e esegui il programma, allora automaticamente lo apre e lo gestisce.(il programma gestisce l'apertura del flusso e anche la sua chiusura)
- Quasi tutto è astratto per la gestione della periferica (apertura, lettura, scrittura, chiusura sono già stati astratti), ma alcune cose dell'aspetto operativo va conosciuto:
  - accesso sequenziale (tastiera)
  - accesso random
- mentre gli stream operano sempre nella stessa maniera, le periferiche non sono assolutamente simili, infatti possono avere diverse caratteristiche di accesso. Si può quindi calcolare dove posizionarsi e muoversi in maniera manuale, ma solo se è permesso dal tipo di file.
- oltre che per instanziare un flusso, serve una funzione per chiuderlo quando non sono più necessario. Questo serve perchè il sistema operativo gestisce le risorse anche per gestire la periferica, lasciando quindi una periferica libera allora si rilasciano risorse. 
- Se ci dimentichiamo di chiudere files si possono fare danni: la bufferizza, cioè il basso livello, non gestisce un byte dietro l'altro, ma si raggruppano byte e vengono mandati insieme. Quando non viene chiuso lo stream le informazioni che il buffer contiene non vengono scritte, quindi si perdono dati. 
  - **FLUSHING** è la capacità programmatica di gestire un flusso (= tutto quello che contiene la periferica, scaricalo/buttalo), poi lo si chiude.
  - il flush scrive tutti i caratteri che il buffer contiene e li passa al programma (significa che si assicura che tutto quello che c'era da scrivere venga scritto e svolto)
  - per questo si usa prima di chiudere uno stream





### VARIABILE DI TIPO *FILE*

- compare nella parte sinistra della dichiarazione, quando sappiamo che conterrà sicuramente un oggetto di tipo *file* e poi gli si assegna un puntatore, cioè un oggetto che indica quel file.
- questo file è un oggetto che indicherà le modalità di lettura o scrittura che possiede, che consente di sapere informazioni all'interno del file.
- questa variabile contiene un campo di bit per la lettura e scrittura e lo stato della periferica.
- questo oggetto viene gestita dal sistema operativo, la variabile viene instanziata, ma poi tutti questi campi vengono popolati dal sistema operativo.
- FLUSSI STD:
  - vengono instanziali al momento dell'esecuzione di un programma, e vengono aperti tre flussi (stream)
  - *stdout* , *stderr* => periferica video
  - *stdin* => periferica tastiera
  - printf/scanf usano questi flussi.
- ![image-20201110122807433](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110122807433.png)
- schematizzazione di cosa avviene quando un programma apre un flusso per operare su delle periferiche
- nel C c'è la possibilità di accedere a delle funzioni e dei flussi del sistema operativo che altri linguaggi non possiedono.



### OPERAZIONE DI GESTIONE DEI FILES:

```c
FILE *fopen (nomefile, modalità);
// tramite la funz. 'fopen' apri lo strem con un file <nomefile> e con modalità <scrittura, lettura, altro> 
// la funzione accetta un puntatore a file

FILE *fp;
fp = fopen("MioFile", "r"); 
//se il file è nella cartella in cui sto lavorando, mentre invece se ho bisogno di un file in un altra posizione devo selezionare tutto il percorso del file
```

ESEMPIO:

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]){
    FILE *fp;
    char c;
    
    fp = fopen("/tmp/MioFile.txt", "r");
    // devo verificare che il file esista, perchè se non esiste io non riesco a aprire il file
    if (fp == NULL){
        printf("Il file non può essere aperto\n");
        exit(1);
        // il programma deve terminare prima di continuare a lavorare su una cosa che non esiste.
    }
}
```

**Modalità legali di accesso ai files**

- r : lettura

- w : scrittura

- a : scrittura modalità testo alla fine del file(append)

- rb : lettura in modo binario

- ![image-20201110123823219](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110123823219.png)

- se un file è aperto in una modalità non si può usarne un altra, bisogna chiuderlo e reinstanziarlo

- operazione di chiusura: (attenzione a chiudere sempre! (perdita di dati, perdita di files, altri errori))

  ```c
  int fclose (FILE *fp);
  // termina l'associazione tra il flusso e file di una periferica
  // avviene il flush
  ```

- ```c
  //lettura scrittura caratteri:
  int getchar (void);
  int putchar(int c);
  int fget (FILE *fp);
  int fputc (int c, FILE *fp);
  // tutti restituiscono EOF come errore   
  ```

  

**Lettura/Scrittura di stringhe**

```c
char *fgets (char *s, int length, FILE *fp);
// legge i caratteri finchè non trova il EOF, il valore nullo o al più 'length-1'
// il carattere '\n ' viene letto e incluso nella stringa
```

**Operazioni sulla gestione dei files**

```c
int remove (nomeFile);
int rename (vecchionome, nuovonome);
// entrambe queste funzioni dipendono dal sistema operativo, e se non si dispongono i permessi necessari a accedere alle risorse e a modificare lo stato dei file, allora l'azione non è consentita e si restituisce un errore.


```

![image-20201110130101556](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110130101556.png)

![image-20201110130116514](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110130116514.png)



**Lettura/Scrittura Binaria**![image-20201110130202017](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110130202017.png)

![image-20201110130244651](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110130244651.png)

fseek permette di leggere un file a un punto specifico, rewind è una macro funzione di fseek che riporta la lettura all'inizio.

![image-20201110130503620](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201110130503620.png)

il binario potrebbe avere un vantaggio nel senso che occupa meno spazio, mentre invece nel testo ci possono essere dei caratteri strani. 

Quando leggo byte mi devo assicurare che si leggano byte in un certo ordine.