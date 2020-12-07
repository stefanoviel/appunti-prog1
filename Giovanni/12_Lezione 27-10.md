## LEZIONE 27-10

se si usa un pointer che parte all'inizio della stringa, e  poi lo incrementiamo gradualmente per stampare tutti i caratteri. Ma poi il puntatore non punta più la stringa, ma il primo valore all'esterno di essa. Come si fa a questo punto a recuperare la stringa? Si usa una variabile di servizio:

```c
char *stringa = "Il sale della vita";
char *p;
int len = 0;
// variabile ptr p, con il valore di stringa, presa a variabile intermedia.
p = stringa;

while (*p++ != '\0')
	++len;
printf("Lunghezza stringa %s: %d\n", stringa, len)
```



## Funzioni:

- si scorpora il codice in un sottoprogramma chiamante e uno chiamato

  - il chiamante: descrizione in versione sintetica del mio programma

    ```c
    utile = totoMov(entrate) - totMov(uscite);
    ```

    

  - il chiamato/asservito: si fa tutto il lavoro del programma

  - obiettivo: scorporare una parte di esecuzione dal programma principale, e poi definire il parametro "entrate" o "uscite" per eseguire poi il calcolo vero

**Problemi da risolvere**

- sintattico: come faccio a definirlo, come definisco le interfacce(modo unico, modo migliore, modo peggiore), come definisco il chiamante e l'asservito?
- semantico: cosa farà la macchina astratta del C, che invece di eseguire solo il main, chi esegue la funzione, qual'è il modello computazionale



#### Asservimento delle funzioni:

il programma definisce un sottoprogramma, che se definitivo viene invocato (chiamato) => visibilità delle variabili.

 Per fare ciò nel programma, da qualche altra parte devo definire questo programma. In questo devono esserci tutte le variabili, e essere visibili tutte le variabili necessarie, a eseguire i compiti specificati. 

Definizione di un sottoprogramma: scopo e funzioni del sottoprogramma.

Asserzione/Chiamata: sottoprogramma viene eseguito in seguito a una richiesta da un altra.

Esecuzione della funzione: l'invocazione di una funzione C è analoga alla valutazione di un espressione.

Il sottoprogramma chiamante deve poi *rilasciare il risultato* al chiamante.

SOTTOPROGRAMMI: 

- funzioni: restituiscono un valore al chiamante
- procedure: svolgono un compito per il chiamante, ma non restituiscono il valore (definiti con **void**)



#### Struttura di un programma C:

- il main è un programma, il principale

- ```c
  int power(int base, int n){ //questa linea è la testata
  
  }
  ```

  - "int" => tipo del parametro di ritorno

  - "power" => nome

  - "(----)" => argomenti/parametri formali

    - contiene tutti i parametri della funzione, dichiarati con 

      ​							\<tipo>\<nome-parametro>

    - possibilità di avere parametri con struttura molto complessi.

    - "{ --- }" => programma che verrà eseguito quando si esegue la funzione -> corpo della funzione

      - parte dichiarativa locale, contiene variabili necessarie all'esecuzione
      - parte programmatica: algoritmo



**Collegamento tra funzione e chiamante**

1. la funzione non restituisce alcun risultato
2. la funzione termina con **return;** (non ritorna nulla)
3. la funzione termina con **return *espressione*** (il valore dell'espressione viene passato al programma chiamante)
   1. tipo del risultato predefinito o definito dall'utente
   2. non può restituire array
   3. può restituire puntatori (=> cose molto grandi)



**Parametri formali e effettivi**

- parametri *formali*: elencati nella testata 
- parametri *effettivi*: parametri con la quale la funzione viene invocata
  - i parametri formali vengono inizializzati con i valori dei parametri effettivi
  - l'ordine conta



**Dichiarazioni variabili LOCALI**

- si dichiarano le variabili all'interno del programma, necessarie per l'esecuzione del sottoprogramma al cui interno sono state dichiarate



Per invocare una funzione questa deve essere definita prima.

Definizione e dichiarazione non sono sinonimi

**Prototipi di funzione**

- definizione: comprende sia la testata che il corpo
- dichiarazione(o prototipo) comprende solo la testata



