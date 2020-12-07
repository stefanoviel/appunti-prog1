# Lezione 17/11

## analisi e tempi di esecuzione:



Solitamente si programmava staticamente, quindi nota a priori. Molto spesso però soprattutto quando bisognava avere degli input, si doveva stimare una quantità. Questo però lascia alcuni problemi, se più roba => crash, se troppo poco => mi becco una serie di cose che non mi servono e che non uso, ma che hanno della memoria a lor assegnata.

Non potevo neanche rilasciare la memoria quando mi accorgevo di avere un array vuoto, perchè non avevo una strategia di gestione della memoria.

Come si risolve? **Programmazione a Tipi di dati dinamici**

questo consiste nel creare oggetti nuovi, che non si possono prevedere in struttura statica del programma. 



Il controllo nel C si ottiene attraverso una libreria di funzioni, che implementa una strategia di allocazione dinamica, ovvero un'allocazione e de-allocazione della memoria disciplinata.

Di solito alloca all'inizio del programma e viene de-alloccata alla fine dell'esecuzione del programma. Per molte istruzioni e variabili questo continua a essere così (stack).

```c
#include <stdlib.h>
```



Questa libreria nativa copre la gestione della memoria dinamica, e quindi gestisce l'interfaccia del sistema operativo. 



```c
void * malloc(size_t size);
// prende solo un parametro formale: size_t -> int unsign.
// size -> valore in int della quantità di memoria.

int *P;
P = malloc(sizeof(int)); // questa è un operazione che è resa portabile, infatti da il numero di bytes della variabile di tipo int
//  è portabile perchè ogni macchina che lo esegue in base alle caratteristiche ha una quantità che viene alloccata diversa.
```

Questa crea una parte di memoria in indirizzo del puntatore che torna la funzione, e su questa parte di memoria si assegna/viene restituito un puntatore a questa zona di memoria che contenga size-bytes.

Programma diventa quindi portabile. Quando la memoria viene creata si crea un puntatore e lo si associa ad esso.



