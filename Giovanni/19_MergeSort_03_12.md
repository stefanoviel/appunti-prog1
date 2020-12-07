# Lezione 03/12/2020

continuazione lezione 01/12/2020



## Algoritmo MergeSort:

```c++
// Array = A, indice destro = p, indice sx = r
MergeSort(A, p, r){
	if(p<r){
		// trovo il punto centrale -> DIVIDE
        q = Floor((p+r)/2);
        // Sottoinsieme sx -> Chiamata ricorsiva (IMPERA)
        MergeSort(A, p, q);
        // Sottoinsieme dx -> Chiamata ricorsiva (IMPERA)
        MergeSort(A, q+1, r);
        // Unisce i due sottoinsieme -> Funzione principale
        Merge(A, p, q, r);
	}
    // caso base
}

// Vettore A, indici p, w, r = dx, centrale, sx
Merge(A, p, q r){
    // Sottoarray sinistro
    n1 = q-p+1;
    // Sottoarray destro
    n2 = r-q;
    // tutti questi elementi tra p-q-r sono ordinati!
    int j, i;
    // Riempio gli array
    for (i=0; i<n1; ++i){ L[i] = A[p+i]; }
    for (j=0; j<n2; ++j){ R[j] = A[q+1]; }
    // Valore sentinella
    L[n1] = R[n2] = MAXINT;
   // aggiorno intanto che faccio i confronti
    i=j=0;
    // r - p+1 passi
    for(int k=p, k<=r; ++k){ 
        if ( L[i] <= R[j] ){
            A[k] = L[i];
            i++;
        } else{
            A[k] = R[j];
            j++;
        }
    }
}
```

 ## Tempi di esecuzione del Merge:

Principalmente si prende in considerazione il tempo della funzione Merge():
$$
T_{merge}(n) = Θ(n) \\
Θ(n) = Θ(r-p+1)
$$
Quindi nel caso peggiore, l'algoritmo di MergeSort è 
$$
Θ(n log(n))
$$
Ma da dove arriva? Con la complessità delle funzioni ricorrenti:
$$
T(n) =
\bigg \{
\begin{array}{}
Θ(1) \text{ Se } n \leq c \\
aT({n \over b}) + D(n) + C(n)  \\
\end{array}\\
$$
Dove:

*  c: costante piccola
* a : numero sottoproblemi generato dal passo *divide*
* 1/b : dimensione dei sottoproblemi rispetto a quello a quello originale
* D(n) : Tempo/Risorse impiegato per dividere i problemi in sottoproblemi (operazione di Floor)
* C(n) : Tempo impiegato per ricombinare le sottosoluzioni

Nel caso di MergeSort l'equazione di ricorrenza ha i seguenti parametri:
$$
a = 2 \\
b=2\\
T_{MergeSort}(n) = 
\bigg \{
\begin{array}{}
Θ(1) \text{ Se } n \leq c \\
2T({n \over 2}) + D(n) + C(n)  \\
\end{array}\\
$$
Il Termine *divide* ovver D(n), corrisponde al calcolo della metà (=Floor)
$$
D(n) = Θ(1) \text { (è un valore costante)}\\
\text{Impera: } = 2T({n \over 2}) \\
C(n) : \text {Operazione combinazione/fusione} \\
C(n) = Θ(n)
$$
Si può quindi scrivere che: (sapendo che a=b=2)
$$
T_{MergeSort}(n) = 
\bigg \{
\begin{array}{}
Θ(1) \text{ Se } n \leq c \\
2T({n \over 2}) + Θ(n) \\
\end{array}\\
$$


e ricordando che nell'operazione sopra:
$$
Θ(n) \leftarrow C(n) = Θ(n) \\
Θ(n) \leftarrow D(n) = Θ(1)
$$


Ma nel caso dell'InsertionSort avevo un polinomio, quindi riuscivo a trovare la complessità statica totale. Le equazioni di ricorrenza si possono risolvere vari modi, come la sostituzione e l'albero di ricorsione.

**Metodo dell'albero di ricorsione**
$$
T_{MergeSort}(n) = 
\bigg \{
\begin{array}{}
C \text{ Se } n = 1 \\
2T({n \over 2}) + Cn \text{ Se n>1} \\
\end{array}\\
$$
Questo è possibile perché il significato di *Θ(1)* è che si approssima a una funzione lineare, che vuol dire una funzione costante. Di conseguenza si può sostituire *Θ(1)* con *C* e *Θ(n)* con *Cn*. Così si ottengono termini espliciti.

Si risolve attraverso alberi:

![Untitled Diagram](.\image\Untitled Diagram.jpg)

E si continua in questo modo finché non si è trovato il caso di base, che costa c, di conseguenza l'ultimo 'piano' di rami dell'albero sono n foglie che costano ognuna C. (*n\*C*)

Poi dovremmo calcolare il numero di livelli che impiego ad arrivare al caso base e il rispettivo costo.

Avremo quindi 3 problemi:

1. Calcolare il numero di livelli
2. Calcolare il numero delle foglie
3. calcolare il costo di *Ci* (costi di ciascun livello)

Se risolviamo 1, 2, 3 troviamo *T(n)* sommando i costi di tutti i livelli, inclusi i costi delle foglie.

**Costo di ciascun livello**
$$
C_1 \rightarrow Cn \\
C_2 \rightarrow C(n/2) + C(n/2) = Cn \\
C_3 \rightarrow C(n/4) + C(n/4) + C(n/4) + C(n/4) = C(n) \\
$$
in generale:
$$
C_i = 2^i * c\big({n \over 2^i}\big) = cn \\
C_{NumLivel.} := cn
$$
Quindi il costo di ciascun livello del MergeSort è *Cn*. Di conseguenza:
$$
T(n) = \sum_{i}^{NumLivel} C_i
$$
Calcolo dei numero dei livelli viene fatto per *induzione*: (si conosce la soluzione per un caso base e si risolve per un caso generico).

IPOTESI: 
$$
NumLivelli = log_2(n+1)
$$
 da questo, il CASO BASE:
$$
n = 1 \\
NumLivelli = 1 = 0+1 \rightarrow OK!
$$
CASO INDUTTIVO:
$$
n = 2^i \\
NumLivelli = log(2^i+1) = i+1
$$
Noi sappiamo che ogni volta che passiamo di livello, moltiplichiamo per due nel livello successivo, quindi:
$$
ProssimoN : n=2^{i+2} \\
n = 2^{i+1} \\
(i+1) +1 = log_2(2^{i+1}) + 1
$$
 Che quindi dimostra la formula per il caso bersaglio che stavamo cercando.

Con questo possiamo descrivere il caso induttivo. Da questo ragionamento arriviamo nell'ultimo caso, nel quale dobbiamo sommare tutti le somme parziali dei livelli:
$$
\sum_i^{NulLivelli}C_i \\
T(n) = cn * NumLivelli = cn * (logn +1) \\
 = cnlog(n) + cn = - (nlog(n))
$$
E con questa si dimostra come il MergeSort ha complessità costante, sia nel caso peggiore che nel caso migliore e vale:
$$
Θ(nlog(n)) 
$$

----

Ricapitolando: **Gli algoritmi di ordinamento** sono dipendenti:

1. dal tipo di elementi da ordinare
2. dal verso di ordinamento: crescente o decrescente

i metodi basati su confronti e scambi sul posto che ordinano una sequenza di N numeri non può fare meglio che Θ(N^2). 

Es. BubbleSort o InsertionSort

Mentre con gli algoritmi basati sui confronti si può arrivare nel caso *peggiore* Θ(nlog(n)). Ad es: MergeSort o QuickSort.

**Si può dimostrare** che tutti i metodi per confronto hanno metodo ottimale al massimo come *nlog(n)*. 

Per andare oltre, quindi abbandonando il metodo dei confronti, si può arrivare a complessità inferiore a *nlog(n)*. Ad esempio il CountingSort, RadixSort o il BucketSort.

## Risoluzione della complessità della ricorsione con la sostituizione: (applicato all'algoritmo MergeSort)

La complessità di questa funzione è:
$$
T_{MergeSort}(n) = 
\bigg \{
\begin{array}{}
Θ(1) \text{ Se } n \leq c \\
2T({n \over 2}) + Θ(n) \\
\end{array}\\
$$


Voglio dimostrare che *T(n) = Θ(nlog(n))*.

Dimostrare per induzione che:
$$
T(n) = cn*log(n) \text{ per } c < 0 
$$
Assumo il CASO BASE:
$$
T(1) = Θ(1)
$$
e il CASO INDUTTIVO:

Assumo che la diseguaglianza valga per n<k. Che quindi
$$
T(n) \leq cn*log(n)
$$
Dimostrare che questa sopra vale per n=k, in particolare n=K/2.
$$
T({k \over 2}) \leq c{k \over 2}log({k \over 2})
$$
La ricorsione ci dice che:
$$
T(k) = 2T({k \over 2}) + k \\
T(k) \leq 2c({k \over 2})log({k \over 2}) + k \\
T(k) \leq ck(log(k)-log(2)) + k \\
T(k) \leq cklog(k) - ck + k \\
T(k) \leq cklog(k) + k(1-c) \\
T(k) \leq cKlog(k) +(1-c)k \\
T(k) \leq cklog(k) \\
\text{ per } c \geq 1
$$
Questo vuol dire che l'assunto vale per k>n, rispetto all'ipotesi che era più ristretta.

Esercizio dopo il 1:34 in AlgoMergeSortEqRicorrenza.









