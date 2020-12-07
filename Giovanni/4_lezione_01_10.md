Appunti 01/10/2020



il programma fornisce un dato sicuramente sbagliato. Questo succede perchè la variabile diventa più grande di quanto sia lo spazio precedentemente allocato. Il compilatore/programma non fornisce errori.



## STRUTTURE DI CONTROLLO:

- ```c
  while, for, do-while
  ```

  



##### 1. CICLO FOR:

​	![image-20201001161025025](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201001161025025.png)

- il ciclo continua finché l'espressione è vera, però c'è una variabile di controllo che viene modificata ogni ciclo.

- Dopo ogni esecuzione del blocco di istruzioni si aggiornano le variabili del ciclo. Infine il ciclo riparte, si ricontrollano le variabili e poi se è corretta si continua, se no si stoppa.

- ```c
  for (inizio; expr; aggiorna){
      istruzioni;}
  ```

- all'inizio si dichiara la variabile del ciclo, si scrive l'espressione che deve essere valutata e poi una funzione che aggiorna la variabile ogni volta che il ciclo lavora.

- QUESTO CONSTRUTTO E' UTILE PER:

  - quando il numero di iterazioni è noto, diversamente dal while che non so per quante volte io debba ripetere l'espressione.
  - è una maniera più compatta di scrivere un ciclo while, nel caso sopra, perché permette di non dover aumentare il contatore nel testo dell'espressione del while, ma include tutto nella stessa riga.
  - leggibilità è migliore del while.

- si possono anche fare modifiche di variabile alle variabili del ciclo all'interno della dichiarazione. SCONSIGLIATO.





##### 2. COSTRUTTO DO-WHILE:

![image-20201001163241832](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201001163241832.png)

- il blocco viene eseguito e poi il while valuta un espressione.
- la differenza tra il while normale ritorna sempre alla migliore leggibilità e alla scrittura delle minor righe possibile





##### 3. CONSTRUTTO SWITCH

- semplifica una catena di if-else. Migliora la leggibilità e la compattezza del codice.

  ![image-20201001165340129](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201001165340129.png)

- v1 è un intero

- default: parola chiave opzionale. Se tutti i casi sono sbagliati allora si esegue questo blocco istruzioni. Se non viene inserito e non viene positivo neanche un valore all'interno dello switch, allora nulla viene eseguito.

- il valore intero serve perchè si continua a eseguire mano a mano che il valore **int** aumenta.

- La parola **break**(opzionale) permette di fermare il codice alla fine del costrutto che si è appena eseguito. Serve per fermare l'esecuzione dello switch.

  ![image-20201001170051365](C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image-20201001170051365.png)

- se non si inserisce il break allora avviene al cosiddetta esecuzione a cascata.

  - positivo se i valori devono tutti passare da alcuni blocchi di istruzione.
  - negativo se l'esecuzione a cascata non è voluta.

- l'espressione che viene valutata deve essere _int_ lecito perchè venga eseguito.





#### 4. ISTRUZIONE BREAK:

- si può usare nei cicli while, for, do, switch.
- provoca l'immediata uscita dall'istruzione
- l'esecuzione del programma continua con l'istruzione successiva
- l'istruzione del break è sconsigliata per motivi di leggibilità del codice



#### 5. ISTRUZIONE CONTINUE:

- il flusso di esecuzione ha dei salti. Nel continue all'interno del ciclo che si prende in considerazione si salta al ciclo successivo.
- usabile in while, for, do. Non applicabile a switch.



##### ASPETTI E CARATTERISTICHE NECESSARIE PER LE STRUTTURE DI CONTROLLO

- esistono cose non codificabili con questi diagrammi di flusso?

- esistono strutture che riescono a codificare qualsiasi algoritmo?

- esistono strutture di controllo più potenti di queste?

- TEOREMA DI BOEHM E JACOPINI:

  - se puoi fare sequenze di istruzioni

  - se hai un modo per selezionare (if-else)

  - se hai un modo per creare un ciclo

  - Allora si può codificare qualsiasi cosa.

    ![image-20201001172950551](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201001172950551.png)



## GLI ARRAY:

- MACCHINA ASTRATTA:

  - contiene il bus di sistema virtuale che consente di connettere ad es. lo stdin o stdout.
  - la macchina astratta permette di avere una serie di risorse: memoria che contiene le variabili e poi una cpu virtuale che permette l'esecuzione di processi logici.

- c'è bisogna di avere una zona in memoria centrale un posto dove io possa raccogliere una serie di oggetti simili, che vanno raggruppati.

- se si vogliono rappresentare luoghi in 3dimensioni o vettori, allora gli array servono a rappresentare l'insieme delle componenti.

- solitamente le informazioni rilevanti vengono aggregati a contenitori fatti di elementi più semplici.

- poi per accedere a un particolare elemento all'interno dell'array si usa un indice **a[i]** (le parentesi quadre hanno alta precedenza tra gli operatori e associano da destra a sinistra)

- questo oggetto poi deve avere una dimensione. Infatti quando dichiaro una variabile semplice e indico il tipo di variabile che voglio, allora qualcuno mi allocca una certa quantità di memoria. 

- Tutti gli elementi sono contenuti in sequenze di celle consecutive e omogenee.

- COME FUNZIONA IN C: per accedere agli elementi a[numero], l'indice più basso è l'indice = 0.

- a[i]

  - ho un oggetto che si chiama "a"
  - poi guarda tra le parentesi quadre e guarda nell'insieme di valori di a.
  - bisogna calcolare il i-esimo elemento, con un massimo che poi vedremo.
  - una volta che so valutare dove si trova, allora poi verrà restituita il right value della variabile, cioè quello contiene l'insieme a all'indirizzo [i]

- Come fa la macchina astratta a accedere alle celle dell'array?

  - ```c
    x = a[0];
    x = a[1];
    ```

    

  - prima di tutto preleva l'elemento dall'array

  - il compilatore deve calcolare l'indirizzo

  - il right value viene assegnato alla prima variabile x.

  - poi continua l'esecuzione e il valore di x cambia con il valore di a[1]

