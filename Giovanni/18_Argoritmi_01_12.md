# Lezione 01/12/2020

## algortmi di ordinamento

ordinamento degli array spesso è richiesto affinchè siano efficienti poi nei calcoli, o ad esempio nella ricerca dicontomica.



Esempi importanti di algoritmi di ordinamento, molto conosciuti e con analisi della complessità. Questa può essere sia il calcolo del *T(n)* e del *O*, e quindi dove si colloca questo algoritmo.



Il problema dell'ordinamento sorge in alcuni casi, come la ricerca dicotomica, ma utile anche per il problema  della ricerca della mediana.

In particolare vedremo l'InsertionSort e il MergeSort, che tra l'altro rappresentano due macroclassi di complessità di algoritmi.

### Algoritmo Insertion Sort:

efficente per piccole dimensioni dell'array, quindi non da escludere a priori.

concettualmente è come prendere una carta alla volta e posizionarle correttamente in un altro mazzo. 

Il concetto principale è che quando le carte vengono inserite nel mazzo finale siano già in ordine, quindi già correttamente posizionate.

Ho quindi un array che sto scorrendo:
* estraggo il primo e la posziono all'inizio dell'array
* estraggo la seconda carta, se maggiore la metto dopo, se minore la metto prima
* di conseguenza prendo l'ultimo elemento correttamente posizionato e lo confronto con l'elemento che sto per posizionare, e con questo decido dove posizionare la carta correttamente.

![image-20201207115612009](.\image\image-20201207115612009.png)

![image-20201207115753626](.\image\image-20201207115753626.png)



E la complessità di questo algoritmo?

In funzione di T(n) come si comporta l'algoritmo. 

Complessità asintotica dell'algoritmo.

​	L'algoritmo è efficiente per numeri piccoli. Infatti nel caso medio:
$$
Theta(N^2)
$$
Nel caso peggiore (ovvero quando devo completamente girare l'array):
$$
Theta(N^2)
$$
Come mai costa così? Perché prima devo prendere una carta per N volte, poi bisogna scorrere l'array in cui inserirla (lungo N-j). Per questo avremo due cicli uno annidato all'altro, motivo per cui la complessità è il quadrato di N.

```c++
void InsertionSort(A){
    n = DimensioneArray(A);
    for (int j=1; j<n; ++j){
        // Prendo la carta da inserire
        x = A[j];
        // Secondo indice, quello del ciclo annidato. é anche l'indice superiore, che indica il sottoArray tra 0->(j-1).
        i = j-1;
        /* controllo di non essere alla fine dell'array.
         * Quando trovo il caso in cui x < ElementoArray[i], allora
         * assegno la carta a quel posto
         */
        while( (i >= 0) && (x<A[i])){
            A[i+1] = A[i];
            i = i-1;
        }
        // Prendo la prossima carta.
        A[i+1] = x;
    }
}

/*
 * ANALISI COMPLESSITà, calcolando il contributo della complessità tra tutte le linee.
 */
void InsertionSort(A){
    n = DimensioneArray(A);
    for (int j=1; j<n; ++j){		  // c1*n
        x = A[j];				  	 // c2*(n-1)
        i = j-1;				   	 // c3*(n-1)
        while( (i >= 0) && (x<A[i])){ // c4 * (sommatoria da j=2 a n di tj)
            A[i+1] = A[i];			 // c5 * (Sommatoria da j=2 a n di (tj-1))
            i = i-1;  				// c6 * (Sommatoria da j=2 a n di (tj-1))
        }
        A[i+1] = x;					// c7 * (n-1)
    }							 // ------------------------
}								// La somma di queste complessità porta alla funzione T(n), dove n è il numero di operazioni.

```

### ANALISI COMPLESSITÁ: 

**CASO MIGLIORE**

Nel caso migliore abbiamo per forza che 
$$
t_j = 1
$$
 

perché il primo confronto è già falso, quindi non eseguo mai il corpo istruzioni del while. Si può anche dire che in questo caso *l'Array è ordinato in partenza*. DA questo fatto posso riscrivere l'algoritmo di prima come:

```c++
void InsertionSort(A){
    n = DimensioneArray(A);
    for (int j=1; j<n; ++j){		  // c1*n
        x = A[j];				  	 // c2*(n-1)
        i = j-1;				   	 // c3*(n-1)
        while( (i >= 0) && (x<A[i])){ // c4*(n-1)
            A[i+1] = A[i];			 // 0
            i = i-1;  				// 0
        }
        A[i+1] = x;					// c7 * (n-1)
    }							 // ------------------------
}								// quindi posso calcolare e trovare Omega.
```

Che quindi è rappresentabile:
$$
T(n) = (c1+c2+c3+c4+c7) * n = bn + a = Θ(n)
$$
Questa funzione che esprime la complessità del caso migliore è lineare.

**CASO PEGGIORE:**

Il caso peggiore lo si ha quando ho l'array completamente inverso rispetto a quello per cui devo ordinarlo. Per questo motivo dovrò eseguire tutte le possibili operazioni, che si traduce con:
$$
t_j = n
$$
Da questa relazione possiamo quindi tradurre il caso generale e trovare la complessità del caso peggiore:

```c++

void InsertionSort(A){
    n = DimensioneArray(A);
    for (int j=1; j<n; ++j){		  // c1*n
        x = A[j];				  	 // c2*(n-1)
        i = j-1;				   	 // c3*(n-1)
        while( (i >= 0) && (x<A[i])){ // c4*(sommatoria da j=2 fino a n)
            A[i+1] = A[i];			 // 0
            i = i-1;  				// 0
        }
        A[i+1] = x;					// c7 * (n-1)
    }							 // ------------------------
}								// Posso calcolare


```

Che si traduce in:
$$
T(n) = c_1n+c_2n+c_3(n-1)+c_4\sum_{j=2}^{n} j + c_5\sum_{j=2}^{n}(j-1) + c_6\sum_{j=2}^{n}(j-1) + c_7(n-1)
$$
Poi si sa che:
$$
\sum_{j=2}^{n} j = {n(n+1) \over 2} -1
$$
Quindi nel caso peggiore:
$$
\sum_{j=2}^{n} (j-1) = {n(n+1) \over 2} - n = {n(n-1) \over 2}
$$
Possiamo quindi tornare e sostituire i contributi:
$$
T(n) = c_1n+c_2(n-1)+c_3(n-1)+c_4({n(n+1) \over 2} - 1) + c_5({n(n-1) \over 2})  + c_4({n(n-1) \over 2})  + c_7(n-1)
$$
Che quindi si traduce con:
$$
T(n) = {1 \over 2}(c_4*c_5+c_6)n^2 + (c_1+c_2+c_3+{1 \over 2}c_4 - {1 \over 2}c_5 - {1 \over 2}c_6 + c_7)n -c_2 -c_3-c_4-c_7 \\\\
= c'n^2+b'n+a' \rightarrow Θ(n^2)
$$
Il comportamento asintotico siamo in grado quindi di definirlo.



### CATEGORIE DI ALGORITMI CHE SI COMPORTANO COME L'INSERTIONSORT:

L'InsertionSort è un algoritmo che:

* fa l'ordinamento *sul posto*, usa quindi un solo array senza necessità di array d'appoggio.
* confronta e scambia tra loro elementi consecutivi dell'array.

**Teorema:**

La *complessità nel caso peggiore* per ogni algoritmo di ordinamento che si comporta come l'insertionSort è al massimo:
$$
Θ(n^2)
$$
Algoritmi più efficienti richiedono scambi tra elementi distanti dall'array.



## Algoritmo di MergeSort:

Si comporta nel caso peggiore:
$$
Θ(n * log(n))
$$
Mette insieme due concetti:

1. Ricorsione (solitamente è risolto in questo modo)
2. Divide et Impera (operazione di fusione per unire i sottoarray)

Come funziona:

* si prende l'array e si dividono le due metà (si creano due sotto problemi, da notare la possibilità di ricorsione).
* divido ancora in due sottoarray finché arrivo a una soluzione base, ovvero dimensione 1.
* Arrivato all'array di 1 elemento, allora consegno l'array ordinato. 
* Da questi due array diversi unisco (*merge*) e genero un array che è la somma dell'array di ingresso e li sommo nel corretto ordine.

```c++
// A = Array, p = primoElementoArray, r = FineArray
MergeSort (A, p, r){
	if (p < r){
        // q = metà (senza casting perchè non mi serve perfetta)
        q = Floor( (p+r)/2);
        // genero due sottoarray: inferiore a Q
        MergeSort(A, p, q);
        // superiore a Q
        MergeSort(A, q+1, r);
        // prendo l'ordinato del sottoarray superiore e inferiore e riunisce
        Merge(A, p, q, r);
    }
}
```









