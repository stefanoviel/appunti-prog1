# Lezione 24/11/2020

Tipi di dati astratti-> **STACK**

- si chiama anche lista LIFO (Last In First Out) o pushdown list
- Last in First out
- il modello matematico che permette di caratterizzare questo tipo di dato, è semplificabile con una lista L dove l'inserimento e l'estrazione degli elementi avviene esclusivamente da un solo lato, ovvero l'alto (*dalla cima, dal top*)

l'unico modo per accedere i libri in questo modo è dalla cima, ovvero dal top, cioè la porta di ingresso all'elemento.

Chiamando lo stack S, dobbiamo poter inserire l'elemento e estrarlo

PILA OPERAZIONI STD:

```c
Push(PILA, elemento); // operazione di inserimento nella pila
Pop(PILA); // estrarre, richiede solo il contenitore da cui va estratto, perchè non c'è ambiguità, posso prenderlo solo dalla cima. Questo può essere visto come una cosa limitante ma invece in alcuni casi è una semplificazione.
```

Di conseguenza si riempie sempre lo stack dal basso e poi lo si svuota in base a cosa si trova per prima dall'alto.

Ci sono operazioni che permettono una migliore/semplificare la gestione delle operazioni:

- restituisci la testa della pila S 'top(s)'
- controllo sa lo stack è vuoto StackIsEmpty(s)
- controlla se lo stack è pieno StackIsFull(s) (solo se lo stack è stato implementato in modo statico)

La notazione *infissa* è la notazione che usa le parentesi, ma che ha di negativo  il fatto che non sia sempre uguale, che ci può essere ambiguità, risolta parzialmente con le parentesi.  Questa ha portato alla necessità di creare alla tabella di priorità.

Si risolve parzialmente questo problema con la notazione postfissa (anche chiamata polacca):

- utile per il calcolatore, la macchina la preferisce, si evita un layer di traduzione del linguaggio.

- apprezzata perché non ha ambiguità, quindi non ha bisogno di usare tabelle di precedenza e associatività

- questa è utile perchè non lascia spazio alla soggettività ma che anche però utilizza uno stack, quindi una struttra dati non semplice.

- ```c
  5 3 + -> 8;
  // sequenza dei valori, dell'operatore da applicare e quindi il risultato.
  ```

- questa operazione è eseguibile solo con lo stack: ogni volta che incontro un valore inserisco nello stack (push(elemento)), e faccio questa cosa con tutti gli elementi.

- a questo punto lo stack ha tutti gli elementi dentro di se,

- infine incontro l'operatore -> facciamo un pop degli operandi necessari per eseguire la somma.

- a questo punto eseguo tutte le operazioni, non ho dubbi non ho ambiguità su cosa devo fare e su cosa viene prima o dopo.

- il risultato viene inserito nello stack, e quindi il valore finale dello stack è il risultato. Questo è l'unico valore che rimane nello stack.

tutto parte con la lettura di caratteri in una stringa, e continuo ad eseguire push con tutti gli elementi della stringa, finché non trovo un operatore. Quando trovo l'operatore eseguo tutto e poi il risultato prende il valore maggiore dello stack, ovvero il valore top.

<img src="C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image\image-20201124115813132.png" alt="image-20201124115813132" style="zoom:80%;" />![image-20201124120340670](C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image\image-20201124120340670.png)

<img src="C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image\image-20201124115813132.png" alt="image-20201124115813132" style="zoom:80%;" />![image-20201124120340670](C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image\image-20201124120340670.png)

Funzione per la conversione:

```c++
void infissa2postfissa(const char* e){
    // Alloca S
    for (int i=0; e[i] != '\0'; ++i){ // se la stringa non è finita continua
        if ((e[i] == "(") || (e[i] == ' ')) continue;
        // se la stringa contiene una parentesi, ignora e vai avanti
        if (e[i] == ')')
            cout << pop(S);
        // se incontri la parentesi tonda estrai e esegui, ritorna il valore finale
        if ((e[i] == '-') || (e[i] == '*') || (e[i] == '+')
           					|| (e[i] == '/'))
            Push(S, e[i]);
        // se contiene un operando inserisci in cima allo stack
        if ((e[i] >= '0') && (e[i] <= '9'))
            cout << e[i];
        // se incontriamo un numero lo stampiamo in output
    }
	// Free S
}
```



Implementazione dello stack, esistono due posizione alternative per l'uso dello stack.

Vantaggi/svantaggi in entrambi i metodi. 

IMPLEMENTAZIONE BASATA SU ARRAY:

Memorai fissa è uno svantaggio perché lo stack cresce nel corso del programma, quindi avere una dimensione fissa ha un certo peso. Inoltre va gestito il fatto che lo spazio finisca.

IMPLEMETAZIONE SULLE LISTE:

può crescere/descrescere indefinitamente, in modo dinamico. Più complicata la gestione logicamente.

**Array**

```c
#define StackMAx 20 // dichiarazione della massima dimensione dello stack

struct Tipostack {
    int N; // numero di elementi presenti nello stack al momento
    int s[StackMAx]; // elementi presenti nello stack
}Tipostack;

typedef struct TipoStack STack; // Alias per sopra
typedef struct Tipostack *StackPtr; // Passaggio per riferimento

// True/False se lo stack è empty
bool StackIsEmpty(StackPtr p){
    return (p->N == 0);
}
// True/False se Stack vuoto
bool StackIsFull(StackPtr p){
    return (p->N == MAXP);
}
// Funzione Push, inserisce nello stack e aumenta la dimensione
void Push(StackPtr, Tipoelemento Elem){
    if (StackIsFull(p)){
        exit();
    }
    p->s[p->N] = Elem;
    p->N=p->N+1;
}
// Funzione Pop, estrae dallo stack e riduce la dimensione, torna il valore dell'elemento nello stack
int Pop(StackPtr p){
    if (StackIsEmpty(p)){
        exit();
    }
    p->N = p->N-1;
    return p->s[p->N];
}

// Come faccio a cercare/accedere un elemento in mezzo, come faccio? Rimuovere la prima occorrenza e rimuoverla?

/* Rimuovere la prima occorrenza, true/false se rimosso
 * Problema del Treno:
 * 		- faccio Pop finché non trovo il valore
 * 		- quando trovo il valore, lo rimuovo
 * 		- se il valore != valore cercato, vengono aggiunti in un secondo stack
 * 		- quando ho eseguito l'eliminazione di quello cercato
 * 		- ricompongo lo stack
 * 
 * 	IMPORTANTE RICORDARE CHE PUSH E POP COSTANO POCO, QUINDI MOLTO UTILI E UTILIZZABILI
 */
```



**Lista**

```c++
struct TipoElemento;
struct StackNodo{
    TipoElemento info;
    struct StackNode *next;
}StackNodo;

typedef StackNodo Nodo;
typedef StackNodo* NodoPtr;

// inserire in testa alla lista
void Push(nodoPtr p, TipoElemento Elem){
    // alloco un nuovo elemento
    NodoPtr punt;
    
    if ( !(punt = new NodePtr(sizeof(Nodo)) ){
        // gestisco un errore allocazione
        exit();
    }
    // punt nuovo elemento
    punt->info = Elem; 
    // punt-> next diventa la testa, puntando alla vecchia testa
    punt->next = p;
    // il nuovo elemento diventa nuova testa
    p = punt;   
}
// prende la testa e la estrae/elimina, ritorna l'elemento estratto
TipoElemento Pop(NodoPtr p){
    // inizializzo un nodo temporaneo
    NodePtr tmpPtr = p;
    // creo un elemento e ci assegno il valore di p
    TipoElemento value = p->info;
    // creo la nuova testa
    p = p->next;
    // elimino il Ptr temporaneo
    delete [] tmpPtr;
    // restituisco il valore dell'elemento estratto
    return value;        
    
}
        
/*
 * IMPLEMENTAZIONE SEMPLICE E POCO COSTOSA:
 * - l'operazione di pop e push hanno importanza perchè l'operazione non dipende dalla lunghezza dello stack, ma si esegue sempre in un tempo unitario.
 * => indipendentemente dalla lunghezza dello stack le operazioni pop e push si eseguono sempre con la stessa velocità.
 */
        
  // return true/false se lo stack è pieno o no
 bool StackIsEmpty(NodePtr p);
 // controlla se nullo se no stampa finchè (p->next == NULL)
 void StampaStack(NodePtr p);

        
```



Le operazioni di push e pop dipendono dalla dimensione dello stack? NO.

e nel caso di implementazione con array? NO.

# Tipi di dati astratti: CODA

Chiamata anche FIFO (first in first out), ma anche lista o queue.

Il concetto di coda non vale come quello nella vita reale, infatti non tutti si comportano in maniera constante, coerente. 

La coda ha due accessi: **coda** e **testa** (uscita e ingresso). 

Questo caratterizza fondamentalmente lo stack dalla coda.

A questo punto abbiamo due strutture:

- inserimento => avviene solamente dal lato della coda
- estrazione => avviene solamente da lato della testa

esistono due operazioni formali che permettono l'inserimento e la rimozione. 

```c
Enqueue(Q, E); // PUT, inserisci
// Coda Q e elemento E
Dequeue(Q); // GET, estrai dalla testa della coda Q
// poi ci sarà altre funzioni complementari
void CheckIfEmpty(Q);
void PrintQueue(Q);
```

Inserisco dall'alto finché io continuo a inserire, attraverso l'operazione PUT. Poi invece serve il GET, che prendere dal primo elemento inserito, 

![image-20201204163212779](C:\Users\giova\Documents\1_UNI\programmazione1\appunti\image\image-20201204163212779.png)

Per gestire una coda quindi abbiamo due punti da gestire, il fronte e la coda.



Due implementazioni, con liste e con array.

**LISTE LINKATE**

```c++
typedef struct EL{
    int val;
    // elemento che va inserito nella lista
}EL;
// Elemento base della lista
typedef struct Tnodo{
    TipoElemento EL;
    Tnodo* next;
}Tnodo;

typedef struct EL ElemLista;

struct queue{
    EL *Head;
    EL *Tail;
}

// per rendere il codice leggibile definisco gli Alias
typedef struct queue Queue;
typedef Queue *QueuePtr;

// Prototipi di queste funzioni:
void Enqueue(QueuePtr qP, TipoElemento El);
TipoElemento Dequeue(QueuePtr qP);
bool checkIfEmpty(QueuePtr qP);

/* primo inserimento, devo modificarli entrambi
 * Head-Tail -> Tnodo inserito
 * aggiungo un altro
 * head -> Tnodo -> Tnodo2 -> NUll, con Tail -> Tnodo2
 * 
 */
```



**ARRAY**

continua in 26/11/2020















