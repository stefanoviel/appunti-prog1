## LEZIONE 15-10-2020

cambiare da base Esa a Oct => prima in binario e poi in ottale

l'ultimo bit lo attacco agli altri gruppi in modo da creare dei gruppi di bit tutti da 3. 

![image-20201015154501158](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201015154501158.png)

raggruppo fino a che posso, poi aggiungo zero. in questa maniera riesco sempre a costruire triplette.

![image-20201015154728645](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201015154728645.png)



## Rappresentazione delle informazioni:

rappresentazioni di informazioni che poi il calcolatore è capace di utilizzare. Per farlo si usano opportune rappresentazioni, chiamate codifiche.



Informazione di alto livello => valore reale.

Rappresentazione => dove si elabora la codifica.

Dati => valore che il compilatore vede e sa elaborare.



Per fare ciò si usa la **codifica** e la decodifica: algoritmi che permettono la rappresentazione di informazioni.

Viceversa si deve saper decodificare ciò che è stato memorizzato, quindi ci deve essere un processo di decodifica che valuti il dato e lo renda comprensibile all'uomo.

Come si fa a collegare la macchina fisica (hardware=basso livello), alto livello(livello applicativo).

Attraverso il programma ad esempio si può dichiarare che tipo di dato e quindi come un certo dato va utilizzato e letto,  si comprende la codifica che si utilizza e anche come questo valore deve venir essere utilizzato. 

Come si fa a codificare il numero in una sequenza di bit? 

esistono varie codifiche che includono una grande varietà di oggetti, ad es. le informazioni a 16bit(2byte), che servono per i numeri o le lettere.

codifica di valori come: **Interi positivi**

con 8 bit: ci sono 256 combinazioni, usate per gli interi da 0-255

di solito si usano almeno 4 byte: (32 bit) per rappresentare un intero positivo, range compreso fra o e 4 miliardi circa. In realtà quindi quando ci riferiamo a un intero positivo, non includiamo tutti gli interi positivi, ma solo il sottoinsieme dei positivi che contiene questi casi.



**Interi relativi **

- la reppresentazione con il segno: uso 7 bit per il suo valore, l'8 indica il positivo (0) o negativo(1)
- rappresentazione **modulo e segno**: perchè divido la parola tra l'elemento di sinistra e tutti gli altri.

*Interi relativi* seconda soluzione 

- problema con la codifica precedente: introdotto una codifica ridondante, infatti se codifico lo zero, ho due codifiche per zero+ e zero-. Questa rappresentazione quindi è ambigua e non riesco a rappresentare 2^8 valori, ma solo 2^8-1.



**Codifica Interi Relativi** 

<img src="C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201015161557737.png" alt="image-20201015161557737"  />

- usando il MSB come segno, allora con quello posso capire il segno, poi lo levo e capisco subito il suo valore. problema che le cifre sono asimmetriche, da una parte si arriva a 7, mentre dall'altra arrivo a -8
- molto facile trovare l'inverso di un numero, infatti basta invertire gli zero con l'uno e viceversa.



**Numeri Frazionari**

- *virgola fissa*: numero di bit assegnati alla parte intero e quella decimale fissi => ci sono molti lati negativi:
  - 1001.1001 (la virgola non esiste fisicamente, ma è una cosa ideale)
  - prendo e taglio a metà con la virgola fissa. 
  - la notazione posizionale mi permette di avere la parte razionale e la parte intera
  - SVANTAGGIO: se ho un segnale che ha bisogno di più cifre intere che razionali non posso farlo con questa codifica. Se il valore cresce io non posso spostare la virgola e quindi il mio valore decimale rimane inutilizzato mentre intero è molto limitato. Se inizio a modificare la virgola, con il metodo della virgola fissa creo solo un casino, perchè la codifica non è esplicita.
- *virgola mobile:* valori mobili assegnati al numero, che abbia più o meno cifre intorno alla sua virgola.
  - poi diventato standard nel 32 bit.
  - esistono codifiche per la lunghezza delle parole. Precisione singola a 32 bit.
  - il primo bit, indica il segno; i successivi 8 bit indicano l'esponente del valore; il resto è mantissa, cioè il valore reale contiene tutto quello che è a destra della virgola.

 manca un pezzo



## TIPO DI DATO:

- il tipo è un insieme di valori che può assumere, i cui elementi possono fare/ essere l'oggetto di operazioni. in base all'oggetto di cui ho bisogno e in base a che operazioni devo eseguire con quei dati allora dichiaro tipo di dati diversi, in base allo scopo e alla funzione.

- classificazione: 

  - built-in (predefiniti): interi, caratteri, tipi strutturati (array, struct).
  - user-defined: definiti dal programmatore, creati a piacere.
  - ogni linugaggio offre diversi tipi diversi predefiniti o semplici.

- i tipi sono utili per interpretare una serie di bit in memoria, e in base al qualificatore viene inteso come num. intero o lettera. Questo cambia moltissimo all'utente, ma invece è la stessa cosa a livello basso.

- i tipi sono importanti perchè permettono di comunicare quanta memoria si mette a disposizione, e quindi so anche se sto usando 16 bit o 32 bit, quanta richiesta di memoria posso fare 

- possono catturare qualche errore di tipo, senza causare un errore durante l'esecuzione.

  - aspetto formale e sintattico: a un tipo si associano oggetti e operazioni, e il tipo mi permette di segnalare che cosa sia una certa quantità di memoria. se poi nel programma viene usato come una cosa diversa dal dichiarato causa un errore, che invece viene preso direttamente al compilatore (statycally typed)
  - permesso di casting => la possibilità di programmaticamente forzare un tipo su altro tipo.
  - normalmente il tipo di solito si mantiene per il programma

- tipi predefiniti: 

  - **int**:
    - concetto matematico numero intero
    - ha operatori come +-*/, %==!=><>=<=
    - normalmente usa una parola di memoria (1byte, normalmente, ma poi cambia anche da macchina fisica)
  - float
  - double (float con doppia precisione sui frazionari, di conseguenza la sua lunghezza dovrebbe essere il doppio di quella del float)
  - char

- ulteriore modo per caratterizzare il tipo di valori, usando: 

  - short: **lunghezza** <= spazio di **int** <= **long **
  - modificano la quantità di memoria riservata per la variabile

- **signed** & **unsigned**: senza segno o con il senso, ad esempio se ho bisogno di un contatore, allora posso evitare di avere il bit che si occupa del segno. 

  - **unsigned int**, ma **int** considera già con il segno, quindi senza senso specificare che debba essere **signed**

  - importante perchè se una variabile non ha il segno, il primo bit varrà un numero, invece che segno come invece sarebbe stato se segnata:

    ![image-20201015171916756](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201015171916756.png)

- ```c
  #include <limits.h>
  // racchiude i valori minimi e massimi della mia variabile
  // dichiara il valore massimo e minimo del valore della variabile in una certa architettura
  sizeof(nomevariabile); // restituisce il numero di byte
  // es. char = 1, in generale restituisce il numero di byte assegnati a una variabile passata al costrutto.
  // anche se il valore unsigned viene decrementato di uno, riceverò un valore positivo, nonstante fosse stato inizializzato a zero.
  unsigned long int x;
  printf("%d", x); // print valore intero della variabile e con il rispettivo sengno, anche se dichiarata unsigned. QUesto avviene perchè converte il valore da long a int.
  
  ```

- differenza float/double: float (6cifre di precisione), double (15 cifre di precisione). Lo spazio dato dalla memoria sarà: float < double < long double

  - rischioso usare un if(a==b) in cui a,b float, perchè con una variabile del genere e con un uguaglianza con questa precisione, la condizione potrebbe non risultare mai corretta.
  - in questo caso creare una variabile EPSILON che segnala un intorno e togliere quel valore alla variabile float. Così facendo le probabilità di avere un if positivo aumentano

- il char viene usato come un **unsigned int** e quindi ha senso a scrittura 'A', 'B' in cui si usa il valore numerico del carattere ASCII.



## Conversioni di Tipo:

- il tipo permette di fare un controllo sulla variabile, ma può essere che poi mi serve la variabile ma in un altro tipo.
- c'è un meccanismo per permettere la corretta conversione tra variabili che non sono uguali, o che non sono compatibili. La conversione deve essere automatica, cioè io non devo farmi carico del pensiero della conversione.
- il C pensa da solo alla conversione, ma bisogna essere al corrente di questa conversione, in modo da assicurare che non avvengano perdite di valori in un variabile.
- come funziona il C con le variabili. **Assegnamento**
  - il valore dell'espressione dei destra viene convertito al tipo che sta a sinistra del =
  - la conversione automatica è comoda perchè permette la conversione tra tipi diversi. NEGATIVO: si va a perdere informazioni oltre la virgola.
  - 