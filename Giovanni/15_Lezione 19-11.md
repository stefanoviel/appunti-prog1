# 7Lezione 19-11

## tipi di dato astratto

=> **LISTE**



Tipi di dato sono l'insieme di valori di una variabile

L'*Abstract Data Type* è un modello matematico che include operazioni definite nel modello. Questi esulano dal concetto di linguaggio, ma sono delle cose che possono essere implementati in ogni linguaggio.



### liste con array

se bisognava gestire una sequenza di valori in ingresso, l'unico modo per rappresentarli fino ad ora si usa un array.

Quello che adesso si propone adesso è una situazione a coda. Il concetto importante è che è un insieme dinamico, la coda non rimane costante nel tempo. Questo diventa di difficile rappresentazione con la rappresentazione per un array. Quali requisiti ha bisogno un ADT per gestire meglio questo insieme di segnali (molti tipi di segnali si comportano così).



Un array è possibile, ma l'array è di dimensione fissa, che poi si riempie di buchi, che poi andrebbero riempiti almeno. La struttura dati non è fatta per gestire dei dati dinamici.



**LISTA CONCATENATA**

soluzione alternativa, se l'accesso casuale non è un vincolo stretto (come invece lo è per gli array), allora funzione.

Tanti elementi di memoria disponibili nell'heap, che sono linkati attraverso il linguaggio di programmazione, quindi possono essere anche distanti.

c'è la possibilità di accedere ad un elemento successivo. Ci sono piccole cose che cambiano se sono singolarmente concatenate o se doppiamente concatenate.



VANTAGGI:

* flessibilità di modifica, posso aggiungere/togliere elementi senza creare buchi e senza avere il blocco della dimensione statica
* la lista ci da la possibilità di aumentare e diminuire le dimensioni in base alla necessità
* vantaggio: accesso casuale



SVANTAGGIO:

* onerosità nell'accesso.
* non posso usare un indice, ho bisogno di scorrerli tutti se voglio trovare un determinato elemento al suo interno.
* impossibile avere un accesso casuale.



Che modello matematico dietro questa lista:

-----

sequenza di 0+ elemento con ogni tipo di dato, quindi ogni elemento, anche un astrazione, sarà una cosa che ci può andare.

è un insieme dinamico, quindi posso partire da zero e poi farla decrescere o crescere. 

è un ordine lineare, quindi 0,1,2,3 ..., inoltre l'elemento ha al suo interno le informazioni per accedere all'elemento successivo, quindi 1 non può saltare direttamente a 3, ma deve passare da due (Accesso sequenziale).



La distanza tra inizio e fine varierà nel tempo, proprio perchè questo è un insieme dinamico. 



L'implementazione passa per l'elemento della lista, ovvero uno struct:

```c
typedef struct Telemento{
	Tipoelemento info;
	struct EL *Prossimo;
}Telemento;
```

Struct di EL è quello che ci permette di raggiungere il prossimo elemento della lista, anche se per definizione è una forma di recursione.

Questo è possibile perchè lo struct concatenato è un puntatore, non un intero elemento, quindi non serve al C calcolare quanto spazio gli serve.

Lista singolarmente concatenata, che contiene il suo elemento e l'indirizzo del prossimo elemento (quindi un puntatore all'heap dove è presente il prossimo elemento). 

Io localmente ho le informazioni all'elemento successivo.

![image-20201130102437198](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201130102437198.png)

il simbolo della messa a terra segnala l'ultimo elemento della lista. Questo puntatore viene inizializzato a NULL, cosa molto importante perchè se no non posso trovare la fine e sono in un ciclo infinito.



La TESTA della lista, che può essere NULL anche lei, ma di solito è il puntatore al primo elemento della lista. Per accedere al II elemento della lista l'unico modo è accedere dal secondo.



Per trovare l'ultimo elemento quindi bisogna scorrere tutta la lista e cercare l'elemento che ha il campo 'prox' == NULL.



IMPLEMENTAZIONE:

---

il nucleo è un elemento, creato con uno struct

```C
struct EL {
	TipoElemento info;
	struct EL *Prossimo;
}EL;

typedef struct EL ELemLista;
typedef ElemLista *ListaDiElem; // puntatore al primo elemento della lista

// inizializzazione di una lista
// questo vuol dire che non abbiamo nessun elemento nella lista

ListaDiElem Lista;
Lista = NULL; // questo è l'ultimo elemento della lista
// ------
// altro modo non raccomandato

#include <stdlib.h>
ListaDiElem Lista; // dichiaro globalmente
void Inizializza(void){
    Lista = NULL;
}

// --- (usa un doppio puntatore)

void initializza(ListaDiElem *ListaPtr){ // passo per inidirizzo la ListaDiElem, che è a sua volta un puntatore all'elemDiLista.
    // devo fare un passaggio per indirizzo, perchè se non lo facessimo non si avrebbe effetto nel programma chiamante
    *ListaPtr = NULL;
    // a questo punto ho un puntatore al puntatore dell'elemento all'interno della lista
    // quindi ho un parametro formale che è un pointer, che porta l'indirizzo di un elemento della lista, che porta al suo interno un elemento con l'indirizzo del prossimo elemento.
    
}

bool IsListaVuota(ListaDiElem Lista){
    // passaggio per valore perchè la lista non va modificata e poi non costa molto, perchè non è un array molto lungo.
    // posso farlo anche per indirizzo con un 'const'
    
    // questa funzione ritorna se la lista è vuota (True), o non vuota (False)
}

bool Ricerca(ListaDiElem Lista, TipoElemento ElemCercato){
    // si passa la testa della lista e l'elemento cercato
    // questa è la funzione più complicata dell'implementazione della lista
    
    // dichiaro un cursore che spazzolerà tutti gli elementi della lista
    ElemLista *Cursore;
    if (Lista != NULL){
    	cursore = Lista;
   		while (cursore != NULL){
        	if (cursore->info == ELemCercato) return True;
            cursore = cursore->prox;
    	}// trovo solo il primo elemento, e riporto true se lo trovo, se lo trovo esco, se non lo trovo aggiorno il cursore
    }
    return False;
    // questo vuol dire che ho spazzolato tutta la lista, perchè sono uscito dal while e sono sicuro di non aver trovato nulla nella lista e quindi posso con una certa sicurezza tornare False.
    // la linghezza della lista cambia, mentre invece nell'array ho un num_elemento fisso. Quindi le considerazioni da fare nell'algoritmo della ricerca in questo caso sono diverse, soprattutto sul tempo che impiegherà.   
}

bool RicercaRecursiva(ListaDiElem Lista, TipoElemento ElementoCercato){
    if (Lista == Null) return false;
    else
        if (Lista->info == ELemCercato)
            return true;
    	else
            return RicercaRicorsiva(Lista->Prox, ElemCercato);
}
// eseguo lo stesso numero di confronti, però avrò un record di attivazione maggiore, molto maggiore, in base a quanto è distante l'elemento.

// altro modo, ritornare l'elemento cercato quando si trova

// Altre funzioni: TestaDiUnaLista, restituisce il valore del campo info del primo elemento -> provare a implementarlo
TipoElemento TestaLista(ListaDiElem Lista);

// altre funzioni: produce come risultato il puntatore alla sottolista ottenuta saltando il primo elemento, senza modificare il paramentro testa della lista, controllando che non sia vuota
ListaDiElem CodaLista(ListaDIElem Lista);

/*		------
	- inserimento
	- eliminazione elemento
	- inserire in testa
  		------
*/

void InsiementoInTesta(ListaDiElem *Lista, TipoElemento Elem){
    // passato per riferimento, in modo che possa modificare la lista
    ElemLista *Punt;
    Punt = malloc(sizeof(ElemLista));
    Punt->info = Elem;
    // questo produce un puntatore che punta a un elemento della lista
    // vogliamo che questo diventi il primo elemento della lista
    // prox deve puntare al primo elemento della lista
    // la testa deve puntare a questo elemento
    Punt->prox = Elem;
    *Lista = Punt;
	// implicitamente ho tolto il link tra testa e primo elemento della lista
    
    // questa operazione non dipende dalla lunghezza della lista, quindi questa è un operazione che dovrei prediligere, perchè ha costo unitario, sempre costante
}

void InserisciInCoda(ListaDiElem *Lista, TipoElemento Elem){
    // funzione ricorsiva: richiamare la funzione ricorsivamente finchè non arrivo alla soluzione base, quindi finché non arrivo all'ultimo elemento. A questo punto posso lagare il penultimo all'ultimo e poi assengnare al nuovo ultimo->prox il valore NULL
    
    ElemLista *Ptr;
    
    if (ListaVuota (*Lista)){
        Ptr = malloc(sizeof(ElemLista));
        Ptr->Prox = NULL;
        Ptr->Info = Elem;
        *Lista = Ptr;
    }
    else InserisciInCoda(&(*Lista)->Prox, Elem);
}

// inserimento in coda avrà un costo variabile in base al numero degli elementi della lista, rispetto al costo unitario dell'inserimento in testa.

/* ListaOrdinata, ovvero il tipodielementi è definita da una relazinoe d'ordine tra gli elementi.Es
 - devo inserire 3 tra ... <=x<= ...
 - nella lista ho i valori:
 	1 2 4 5 7 8 9
 - Posso usare InserisciInTesta o InserisciInCoda per liste ordinate? NO! perchè non rispetta l'ordine
 */

void InserisciInOrdine(ListaDiElem * Lista, TipoElemento Elem){
    // ho bisogno di due variabile di servizio per:
    	// 1. tener traccia dell'Elem
    	// 2. tener traccia del successivo
    	// in questo modo l'ordinamento sarà ottenuto
    ElemLista *Punt, *PuntCorrente, *PuntPrecedente;
    PuntPrecedente = NULL;
    PuntCorrente=*Lista;
    while ((PuntoCorrente != NULL) && (Elem > PuntoCorrente->Info)){
        PuntoPrecedente = PuntoCorrente;
        PuntoCorrente = PuntoCorrente->Prox;
    }
    Punt = malloc(sizeof(ElemLista));
    Punt->Prox = PuntCorrente;
    Punt->Info = Elem;
    if (PuntoPcedente != NULL) PuntoPrecedente->Prox = Punt;
    	else *Lista=Punt;
}

// la cosa più difficile in questo caso è mantenere l'ordine della lista, oppure è saltato qualcosa, se si vuole inserire in testa o in coda, etc. ...


// MAncano ancora qualche funzione: ES. StampadiTuttaLaLista, EliminaElemLista.

/* -- eliminalista --
- si stacca il puntatore
- si fa una free (molto importante, inoltre controlla che il puntatore sia uguale a quello che è stato alloccato)
- la gestione avviene come la ricerca linkata, quando si trova l'elemento bisogna fare cosa all'incontrario rispetto all'inserimento, quindi collegare i puntatori fra loro e poi eliminare l'elemento


	------
ALTRE OPERAZIONI
	------
	
- calcolo della lunghezza della lista
- rovesciamento della lista
- append: concatenazione di due liste (piuttosto facile)

*/
```





**Estensioni a questo concetto**

LISTE DOPPIAMENTE CONCATENATE:

```c
struct EL{
	tipoelemento Info;
	struct EL *Prox;
	struct EL *Prec;
}; 
typedef struct EL ElemLista;
typedef ElemLista *Lista;

// mi costa? si è più grande, ma ho facilitato l'inserimento e la cancellazione
// si possono rifare tutte queste operazioni con liste doppiamente linkate
```

LISTE CIRCOLARI: (sentite nella gestione dell'heap)

```c
// la lista circolare si ha una testa come primo elemento, ma non esiste nessun elemento con el->prox == NULL
// possono essere utili nell'heap
struct EL{
    Tipoelemento Info;
}
```





----

Liste e array si usano per stack e code.

VANTAGGI:

- evitare spreco di memoria o il sottodimensionamento della memoria

- inserimento in testa gratis, inserimento in coda paghi

  