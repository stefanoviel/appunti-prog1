### LEZIONE 08_10_2020



- ESEMPIO PRATICO DI UTILIZZO DI ARRAY:

![image-20201008160201008](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008160201008.png)

- gestione dell'array per contenere un insieme di variabili **char**
- utilizzo estensivo del cascade logic del costrutto switch.

- utilizzo della tabella ascii, tutte le cifre dei primi 9 caratteri ascii hanno caratteri adiacenti.
- caratteri come interi in C, si vede bene in **ndigit[c-'0']**
- Rivedere *switch_ContaCaratteri.c*

- deconstruct: rompere l'esecuzione in tante azioni facilmente codificabili.



### ARRAY DINAMICI:

- esiste un altro modo per richiedere memoria in modo non statico?

- cosa usa il C per accedere in modo dinamico alla memoria

- **SIGNIFICA CHE** dichiara la memoria durante l'esecuzione, non durante la compilazione.

  - lato positivo dello statico: no latenza per la memoria, che è richiesta prima dell'inizio dell'esecuzione
  - il lato negativo del dinamico è che durante l'esecuzione la tua memoria viene richiesta al sistema operativo e può negartele o dare memorie non così veloci (es. swap)

- ISO C99 => permette di alloccare dinamicamente un array, cioè un **Variable Length Array**

- ![image-20201008162026361](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008162026361.png)

- PRIMO MODO PER GESTIRE UN ALLOCAZIONE DINAMICA:

  - DA NOTARE che **N non è inizializzata!**
  - ARRAY_S[N] => n viene dichiarato solo dopo lo scanf
  - int ARRAY_D[N] => ho dichiarato questo array solo dopo aver letto il valore dell'array.

- FUNZIONE 

  ```c
  sizeof() //ritorna la dimensione in byte dell'array
  ```

  - questa funzione fa tornare il numero di bytes utilizzati.
  - fa si che io mi calcoli per quella macchina fisica esattamente, in modo da rendere il codice portabile e efficiente in tutti i casi



## ARRAY MULTIDIMENSIONALI:

- esiste la possibilità di fare array multidimensionali

  ```c
  int a[10][5]; //dichiarazione di array con colonne e righe.
  int a[N][M]; // se non si inizializzano N e M il valore è indefinito.
  int a[10][5][20]; // se voglio estendere la dimensionalità della matrice e unisco la sua 3za colonna, che indica la sua 3za dimensione.
  // possono essere dichiarati in fase di definizione
  
  int a[4][5] = {	{2, 5, -8, 7, 6},
                 	{3, 10, 7, 6, 1},
                  {2, 5, -8, 7, 6},
                 	{3, 10, 7, 6, 1},
  		};
  
  ```

- questo è molto utile per capire come il c utilizza una matrice multidimensionale. Raggruppa la matrice a righe, riunendo tutte le colonne della riga. 

- la macchina virtuale del C quindi salva tutte le variabili, in base alla costruzione del suo vettore, in cui le righe sono riordinate.

  ![image-20201008163940096](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008163940096.png)

- ```c
  int matrice[10][10];
  matrice[2][4]=12;
  
  // gestione delle inizializzazioni:
  int a[8] = {5,2,-5, ...};
  float A[3][2]; //3 righe 2 colonne
  
  int B[3][2] = {1,2,3,4,5,6}; // il compilatore raggruppa riga per riga. Lui sa che le colonne sono 2 e ci sono 3 righe. Il compilatore quindi sa come riunire cose e quindi fa 2 gruppi da 3 in automatico.
  
  int D[][] = {1,2,3,4}; //ERR
  
  int F[][2] = {1,2,3,4}; // no numero righe, ma si numero colonne e questa è la cosa necessaria per capire il riempimento dell'array.
  ```

![image-20201008164804213](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008164804213.png)

- inizializzazione logicamente avrà bisogno di più cicli incapsulati, che servono a raccogliere tutti i valore, prima delle righe e poi delle colonne, o in base a cosa ci piace
- i cicli molto utili in questi casi sono il **while** e il **for**
- ESERCIZIO 1:
  - scrivere un programma che verifica se una matrice quadrata è simmetrica, cioè a^ij=a^ji => per ogni i, j
  - vedi progetto8 in programmi a lezione.
- ESERCIZIO 3:
  - esercizio iniziale di analizzatore di testo, che: 
    - parola-cercata$paro-sostituire#inizio stringa parole%
  - identificare dallo pseudo codice e poi passare al codice c:
    - validazione degli input, con inserimento delle parole e poi dell'effettiva stringa da analizzare delimitata con #--%



### DESCRIVERE UNA MATRICE CHE NON RIESCE COMPLETAMENTE A STARE IN MEMORIA:

- se la memoria e le risorse ci sono, si può usare la matematica per calcolare le due matrici, ma se non c'è memoria bisogna spacchettare il calcolo.

- ![image-20201008171936067](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008171936067.png)

  - la loro moltiplicazione darà risultato a una matrice di NxM

  - una soluzione possibile è parallelizzare i programmi, e quindi suddividere il processo in più processi, in modo da far più veloce.

  - posso ad esempio dividere la matrice in tanti pezzi:

    ![image-20201008172207438](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008172207438.png)

  - in base alla memoria che dispongo ho necessità di dividere la matrice in molti più quadratini, questo permette di lasciare la memoria intatta, avendo comunque però lo spazio necessario a eseguire la moltiplicazione .

  - ci sono alcune matrici "magiche" in cui tutte le righe, colonne e diagonali siano il valore 34

    - esercizio: verificare che una data matrice è magica
    - esercizio 2: data una matrice magica M, è possibile trovarne un altra con lo stesso numero magico. Quante?
      - simmetrie
      - rotazioni



### 	LE STRINGHE:

- nel C non si è mai data una gestione elegante delle stringhe come negli altri linguaggi di medio o alto livello.

- il C non è nato per gestire di base le stringhe.

- la **stringa** è una sequenza di caratteri (**char**) => esiste un tipo per le stringhe? Il C vede la stringa come sequenza di caratteri, ovvero come sequenza di char, non esiste il tipo stringa

- per includere il valore di stringa è stato scelto il carattere nullo come delimitatore della stringa e ne delimita la fine  '\0' (carattere ASCII null). Questo è il vincolo che il C impone.

- il valore 'null' serve nella gestione delle stringhe per capire quando una data stringa finisce. Le librerie che sono fornite per la gestione delle stringhe presuppongono che siano delimitate dal valore nullo.

- Questo impone subito un vincolo in termini di risorse, nel senso che ogni stringa di fatto utilizza n+1 char, perchè l'ultimo da standard è '\0'

- ```c
  char mia_stringa[] = "Ciao a tutti!" // semplificazione per rappresentare una stringa, che principalmente inserisce i singoli caratteri all'interno dell'array.
      // con questa dichiarazione il compilatore aggiunge il carattere \0 in fondo alla stinga automaticamente.
      // conteggia i char tra i doppi apici e poi aggiunge il null a destra.
      // questo semplifica perchè inizializza la memoria, mette il null e pure inserisce i caratteri.
  
  char mia_stringa[] = {'c', 'i', 'a', ..., '\0'}; // schema della dichiarazione statica dell'array. Molto più pesante perchè servono tutti gli apici e poi devo ricordarmi il carattere nullo alla fine
  
  char frase[20] = "Mario Rossi"; //specifico il valore dell'array, con indice 20. Noi dobbiamo tener conto che in questa sequenza bisogna calcolare n+1 elementi, perchè l'ultimo è \0. Se chiedi 20 caratteri di una stringa i caratteri utilizzabili sono 19. Se riempi tutti i 20 spazi, allora diventa un array di char, non è più una stringa.
  ```

  ![image-20201008173817542](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201008173817542.png)

- Visualizzazione delle stringhe:

  ```c
  char mia_stringa[] = "Ciao a tutti!";
  printf("%s", mia_stringa); // non si poteva strampare un array, perchè non si conoscevano i limiti, mentre invece in questo momento si possono stampare tutti i caratteri senza possibilità di doppi sensi, infatti c'è il carattere nullo. Se non c'è torna ad essere un array di caratteri e quindi non posso di nuovo più stampare un array con 
  printf("%c", array_di_char)
      
  // c'è anche la possibilità di gestire le stringhe in input
  printf("%s", stringa); // il carattere nullo viene inserirto automaticamente.
  ```

- se creiamo stringhe in maniera corretta, validandole e quindi facendo in modo che le stringhe siano delimitate nel modo corretto, allora ci sono possibilità di gestione delle stringhe. => librerie.

- 

