programmazione 22/09



operazione assegnazione è un assegnazione semplice che assume il valore di destra.

Alcuni operatore sono normali matematici mentre altri sono più specifici. Gli operator si compongono anche, es maggiore/uguale

Come avviene l'esecuzione di un espressione: bisogna creare una variabile che poi prende il valore dell'espressione di destra.



LAZY EVALUATION:

- per calcolare un espressione si deve calcolare tutto l'albero sintattico, che parte dall'alto, dalla cosa più piccola e poi scende fino in fondo
- si calcola senza valutare tutto l'albero sintattico
- processo che rende il programma più veloce e più snella
- si sfrutta questa cosa tenendo conto, quando si scrive l'espressione che è presente questo meccanismo





Assegnazioni combo: no performance migliori, ma migliora la leggibilità del codice

​	x += y ==> x = x+y 

 -=, *=; /=; %= 

operatori di convenienza ? sono utilizzati per una migliore comprensione del programma 

++ -- => operatori unari, cioè si applicano a un solo elemento

x++ => incrementa il right value ma in due modi diversi: DESTRA

*prima si valuta il valore di x e poi si incrementa di 1 il valore di x*

++x => *prima si fa l'auto incremento e poi viene denominato*

allo stesso modo x--; --x



variabili che hanno valori variabili nel corso del programma:

+ true, false (boolean)
+ numeriche
+ stringhe
+ predefinite

variabili dichiarati costanti, se si prova a cambiare valore a queste variabili costanti risulta u errore. 

come si dichiarano costanti? 

**const** tipo identificatore = espressione;



const è un qualificatore, cioè modifica il significato della variabile, in questo caso indica che il valore non può essere cambiato nel corso del programma.



stampa di caratteri e stringhe

- printf("a")
- printf(a)
- printf("a=", a)
- la stringa è una sequenza di carattere che dovrebbe trattata come oggetto unitario non decomponibile.



codifica caratteri: prima si usava ASCII, poi si sono aggiunti un sacco di caratteri anche inmolte lingue diverse, standard UTF-8 => informazioni a 4 bytes con lo standard UNICODE





_Operazione Logiche: Algebra di Boole_

3 operazioni NOT, AND, OR

NOT unario, AND e OR binario => not A, A and B, A or B

Si applicano solo a oggetti che possono avere solo il valore binario (vero (bit=1) o falso(bit=0))

- NOT
  - NOT A opposto del valore di A (se a=vero, adesso valore falso)
- AND:
  - A and B = vero => se e solo se a e b sono veri
- A or B: vero se almeno uno dei due è vero



PROPRIETà:

- COMMUTATIVA:
  - A or B = B or A
  - A and B = B and A
- DISTRIBUTIVA:
  - A and (B or C) = (A and B) or (A and C)
  - A or (B and C) = (A or B) and (A or C)

operatori e tabelle di verità:

i possibili valori di questa tabella sono indicati tutti i possibili valori



NOT (A)

| A    | NOT(A) |
| ---- | ------ |
| 0    | 1      |
| 1    | 0      |
|      |        |

| A    | B    | A and B | A OR B |
| ---- | ---- | ------- | ------ |
| 0    | 0    | 0       | 0      |
| 0    | 1    | 0       | 1      |
| 1    | 0    | 1       | 1      |
| 1    | 1    | 1       | 1      |



CALCOLO DI ESPRESSIONI LOGICHE:

regole di precedenza:

1. valuta NOT
2. valuta AND
3. valuta OR	



| X    | Y    | NOT X | NOT Y | Y OR NOT X | NOT Y AND(Y OR NOT X) |
| ---- | ---- | ----- | ----- | ---------- | --------------------- |
| 1    | 0    | 0     | 1     | 0          | 0                     |
| 0    | 1    | 1     | 0     | 1          | 0                     |
| 0    | 0    | 1     | 1     | 1          | 1                     |
| 1    | 1    | 0     | 0     | 1          | 0                     |





Per casa tabella di 3 variabili binarie nella tabella di verità su ppt

Dimostrare l'equivalenza, cioè che sono due espressioni con la stessa tabella di verità, non nel senso di tutti i passaggi intermedi, ma l'ultima che rappresenta l'espressione in interezza. Se queste due sono uguali, allora le due variabili hanno la stessa tabella di verità.

dimostrare le leggi di DE morgan

1.  A and B = NOT ((NOT A ) OR (NOT B))
2. A OR B = NOT((NOT A) AND (NOT B))

IN LOGICA: contraddizione  e tautologia

- contraddizione: espressione sempre falsa (A AND (NOT A))
- tautologia: espressioni sempre vere

