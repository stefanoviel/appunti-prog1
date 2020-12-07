## LEZIONE 22-10



**RIASSUNTO VOLTA SCORSA**

il concetto di puntatore si deve vedere come una variabile che invece contenere al suo interno anche l'indirizzo di memoria del contenuto, è essa stessa l'indirizzo di memoria.

se si usa una scrittura del genere: 

```c
x=a;
```

il compilatore eseguirà l'azione di prelevare il contenuto della cella identificata da **a** e memorizzato nella cella di memoria denotata da x.

Nel C infatti il puntatore è proprio quella variabile che contiene un indirizzo di memoria. Quest'ultima è riferito alla locazione di un altra variabile.

Il fatto che il puntatore sia una variabile vuol dire che va appositamente dichiarata e inizializzata. Nel C questo si fa così:

```c
TipoDato *Puntatore;
```

Dove: 

- TipoDato: quale tipo di variabile contiene quello spazio di memoria
- "*": operatore unario di de-referentazione
- Puntatore: identificativo della variabile puntatore.ù



-----

## Lezione di oggi:



La variabile puntatore in C è una variabile, di conseguenza ha right e left value. 

Ha bisogno di un nome, che si chiama TipoDato. Ha l'assterisco di deferenziazione, (de-reference), che serve per dichiarare una variabile che non è solamente la variabile ma un puntatore.

I tipiDati possono essere quelli semplici, come quelli user-defined.

Il puntatore è vero che è solo una variabile di posizione, per così dire. Ma per comprendere cosa contiene quella variabile, necessita di avere una dichiarazione, appunto per capire cosa contiene.

l'operatore * si applica a destra. 

```c
int *totale, *intermedio;
char *stringa;
// si può dichiarare anche:
char* primo;
// esattamente come
char *secondo; // questo decisamente più comprensibile e bello

// si dichiara anche insieme ad altre variabili:
int NumUtenti, *NumChiamate;
```



il puntatore è facilmente utilizzabile con un typedef.

```c
typedef TipoDato *TipoPuntatore;
// tipo dato => quale tipo di variabile può essere referenziata
```



##### Il costrutto puntatore:

Se il tipo del puntatore non è specificato, probabilmente ha un typedef.

```c
typedef int TipoDato;
typedef TipoDato *TipoPuntare;

TipoPuntatore P;
tipoDato x;
```

![image-20201022154400716](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201022154400716.png)

il quadrato rappresenta il puntatore, la freccia invece indica a cosa punta il valore. Sopra il quadrato è presente l'identificatore del puntatore. La freccia arriva in una zona con un solo tipo di dato e poi identificata da un nome.



##### Operatore di Deferenziazione:

- operatore unario per il puntatore

- importante *P => l'asterisco indica che il luogo di memoria identificato con P

  ```c
  *P = x; // assegno il right value di x a *P
  x = *P; // assegno left value di *P ad x
  ```





Esempio: slide 13. In questo esempio nessuna operazione viene fatta sul puntatore, ma se ne legge solo il valore che contengono.



## OPERATORE "&" (= Indirizzo di)

Permette di calcolare un indirizzo di memoria di una data variabile.

```c
typedef TipoDato *TipoPuntatore;
TipoPuntatore P;
TipoDato x;
P = &x; // questo permette alla gestione di indirizzi senza ever la necessità di inserire manualmente a inserire indirizzi
```

In questo modo posso cambiare il right value della variabile puntatore.

Esempio: 

```c
Tipopuntatore P, Q;
TipoDato y = 10;
P = NULL;
Q = NULL;

printf("%d ", y);

P = &y; // inizializzo il puntatore sull'indirizzo di y

P = 14;

printf("%d", y); //14
printf("%d", *P);// 14

y++;

printf("%d", y); //15
Q = P; // sto dicendo che l'indirizzo di memoria che era indicato in P, adesso Q accede all'indirizzo di P, nonché l'indirizzo di y. Adesso ci sono 3 modi per accedere/modificare quella variabile.

printf("%d", *Q);
```

Questo è un modo molto facile cambiare un right value in modo diverso, ma è anche un modo mascherato di cambiare questi valori, caratteristica che può essere molto negativa se usata nel modo sbagliato.



- l'operatore & indica l'indirizzo della cella di memoria che contiene il valore di x.
- si applica solo a oggetti in memoria, quindi variabili e array.
- non si applica a costanti, espressioni e variabili di tipo register.



PERICOLO: 

- con i puntori si crea una grandissima flessibilità
- si crea il problema dell'accesso multiplo
- il codice deve rimanere leggibile e comprensibile in modo molto facile

L'operatore * è inserito nella seconda riga tra le precedenze degli operatori, di autoincremento, sizeof e il casting.



```c
// esempi operatori di autoincremento

int x=1;
int *ip;
ip = &x;
*ip = *ip+10; // vado ad incrementare di 10 il valore che trovo dentro il banco di memoria

*ip += 1; // incrementa la variabile puntata da *ip di uno

++*ip; // prima prende il posto e poi incrementa
(*ip)++; // esattamente la stessa cosa, gli operatori funzionano ugualmente.
// NB: gli operatori * e di autoincremento hanno stessa proprietà, di conseguenza il compilatore avrebbe associato da destra, Di conseguenza il risultato in questo caso è diverso.
```



![image-20201022170000134](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201022170000134.png)

in questo caso è un problema, perchè P non sarà più il valore di Q, ma semplicente indica il punto dove punta Q.

**NB**

```c
P = Q != *P = *Q 
```



Problematiche:

![image-20201022170413455](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201022170413455.png)



##### Puntatori e DOT notation:

*Struct*

```c
typedef struct {
	int PrimoCampo;
	char SecondoCampo;
}TipoDato;
TipoDato x, *P;
P = &x;

// adesso come faccio ad accedere alle classi del typedef passando dal *P?
(*P).PrimoCampo = 12; 
// Necessarie le parentesi tonde? NO
*P.PrimoCampo = 12; // questo perchè il Dot ha massima priorità
// esiste una sintassi abbreviata: Puntatore a Struttura:
P -> PrimoCampo = 12; // questo operatore si trova in cima priorità
```

##### Operatore sizeof()

- operatore unario **sizeof()** => resituisce il numero di byte



**Relazione Array e Puntatori in C**

- identificatore dei una variabile di tipo array viene visto dal c come l'indirizzo dell'elemento \[0][0]
  - **a** punta a una parola in memoria, esattamente come un puntatore
  - **a** punta sempre al primo elemento dell'array. è un puntatore fisso, costante, al quale non è possibile assegnare altri valori che già non abbia.



\-- programmino sul ppt per iniziare ad usare cose --

![image-20201022171658870](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201022171658870.png)

nella prima dichiarazione viene associato una memoria che viene assegnato un puntatore. Non modificabile? PROVARE

Nella seconda dichiarazione viene associata una stringa a un certo spazio, modificabile.



#### Principio Minimo:

il concetto è che va dato accesso ai dati il minimo necessario. Io non posso dichiarare una variabile e non proteggerla. Se io voglio una costante, allora quelli devono essere fissi, non esiste che siano modificabili da altro. 

Il concetto di mettere tutte le variabili in globale, non deve esistere, perchè non tutte le variabili devono essere accessibili al mondo.

Keyword **const**

Const != define:

- define avviene al linker, che inserisce la variabile nella tabella dei sinonimi
- const fa una tabella dei sinonimi e dichiara che il const non si può cambiare
  - ha un effetto molto più programmatico sulla parte di programmazione



Proteggiamo il puntatore, nonstante la variabile puntata può cambiare:

```c
int * const ptr = &x; 
```

se invece io voglio un puntatore che contenga una variabile che non cambi mai:

```c
const int * const ptr = &x;
```



#### Aritmetica dei puntatori:

- incremento e decremento del valore all'interno degli indirizzi
- si può incrementare, decrementare, o sommare due indirizzi



- OSS: 

  ```c
  a[i] equivale a *(a+i); // con questo esempio inizio a capire l'artimetica dei puntatori
  // *(a+i) è l'indirizzo che è l'indirizzo di a più i, quindi ne risulta l'elemento num = i, appartenente all'insieme a
  // di conseguenza posso dire che:
  
  	(p = a) == (p = &a[0]);
  	(p = a+1) == (p = &a[1]);
  
  // al contrario non sono ammessi:
  	a = p;
  	a = p+1;
  
  // SOTTRAZIONE:
  
  p-q; // restituisce il numero di elementi che esiste fra p e q, assolutamente non restituisce la loro differenza
  
  // si possono costruire array di puntatori
  const char *semi[4]{
      "Cuori",
      "Picche",
      "Fiori",
  }
  // potevo farlo con una matrice? Si
  // in questo caso però ho un insieme di stringhe con lunghezza variabile
  ```

- SOMMARIO:

- ![image-20201022174052215](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201022174052215.png)





-----

## LE FUNZIONI IN C:

- hanno bisogno di risorse per essere eseguiti
- devono avere tutta la sintassi e le cose necessarie affichè la funzione effettivamente lavori e faccia restituire qualcosa.



- Perchè? 
  - azioni ripetute, con alcune modifiche, per molte cose diverse
  - ho bisogno della stessa funzione per eseguire più istruzioni in un certo ordine e facendo una serie di esecuzioni, in modo che il codice sia riutilizzabile.
  - Riutilizzabilità: ho bisogno di meno righe di codice per eseguire azioni simili tra di noi.
  - Es: libreria per manipolare la stringa, in modo che sia riusabile e copiabile da tutti.
  - Astrazione nell'implementazione dell'algoritmo (incapsulamento) supportata da un interfaccia tra i programmi (distinzione tra il compito da eseguire e come questo venga eseguito)
  - spesso di solito chi progetta i linguaggi di programmazione fa decisioni che però non sono impattanti, infatti esistono librerie di qualsiasi tipo scritte in modo diverso per scopi diversi, o per scopi uguali. Lo scopo è che si possono scrivere le proprie librerie per eseguire comandi dafiniti.
- I **sottoprogrammi** sono asserviti a sottoprogrammi chiamanti (es. il sottop. main chiama il sottop. printf).

