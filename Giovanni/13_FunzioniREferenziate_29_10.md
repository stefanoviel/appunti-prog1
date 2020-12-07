## LEZIONE 29-10



```c
int x = 0;
int f1(int p);
void f2();

main(){
    f2();
}
int f1(int p){
    return p+x;
}
void f2(){
    printf("%d", f1(x));
}
```

Fa una macchina astratta per ogni funzione, posso pensare di avere una macchina dedicata a ogni esecuzione di funzione.

Come si fa a usare una memoria lineare per un flusso di funzioni non lineare?

**Modello di esecuzione  è il concetto di ambiente**

a questo ambiente viene alloccato e quindi messo a disposizione, quando la funzione viene istanziata, e poi viene rilasciato libero quando ha finito l'uso delle risorse prese.

Vedremo che in realtà una sola macchina virtuale può eseguire questo comportamento.



![image-20201029162606113](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201029162606113.png)

costruisco una pila, in cui i pezzi sono in contatto tra di loro. Quando ho finito di usare ogni singolo ambiente io posso rilasciare mano a mano che scendo, quindi mano a mano che eseguo. La memoria viene quindi gestita con questa pila (**STACK**) che fa riferimento alla struttura LIFO (last in first out). 

Quando una funzione viene invocata si crea una copia delle variabili che  vengono passate dalla funzione chiamante. Risultato viene poi riportato. La copia permette di avere tutte le informazioni necessarie al funzionamento, utile perchè main lascia la funzione e il suo posto viene occupato dalla funzione chiamata. Nel C l'unico modo per passare valori è attraverso la copia.

Svantaggio di questo metodo è che la copiatura avviene molto lentamente per le grosse strutture di dati, e ancora di più se queste azioni avvengono molto velocemente. Senza contare che grandi usi di memoria per dati ingombranti, come ad esempio interi databases non si può replicare più di poche volte perchè la memoria limitata finirebbe.

Uno dei modi per passare i parametri da funzione a funzione è l'uso dei puntatori, utilizzando infatti il punto di riferimento della memoria il puntatore permette di implementare cambiamenti in memoria su strutture non connesse al main. In questo modo prima che la funzione termini e quindi venga distrutto tutto il suo contenuto, la struttura viene riportata direttamente  all'indirizzo della variabile che vogliamo cambiare.

![image-20201029170916817](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201029170916817.png)

Questo è importantissimo, infatti permette la modifica e l'accesso a ambienti non visibili alla funzione. Un altro lato positivo è che così non ho copiato tutto il vettore V, ma solo il suo indirizzo. Con questa implementazione quindi siamo riusciti a diminuire lo spazio in memoria necessario all'esecuzione del programma, siamo riusciti a modificare un valore appartenente al main. Il lato negativo è che nel caso di un errore nella gestione del puntatore si possono creare gravi problemi di accesso a sezioni di memoria non normalmente accessibili.

Adesso si scopre il perchè della & nella funzione scanf: perchè dall'altra parte richiede un puntatore che deve essere modificato e quindi incapsulare il valore della tastiera e lo inserisce nella variabile.

Il vantaggio di usare i puntatori in C consente nel fatto che si possono passare qualsiasi tipo di dato. Infatti usando uno struct allora posso gestire tutti i parametri formali e passo una struttura solo con un puntatore.

```c
void swap(int *X, int *Y){
    int temp;
    
    temp = *X;
    *X = *Y;
    *Y = temp;    
} 
```



![image-20201029174726552](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201029174726552.png)



## AMBITI DI VISIBILITA'

Visto = denotato dal suo identificatore.

Ambiente **globale**, cioè esterno a tutte le macchine del processo. Main e tutte le altre funzioni possono accedervi. 

Se invece la dichiarazione avviene nella **parte dichiarativa locale** allora le variabili sono visibili ovunque all'interno della funzione. Tutte le funzioni che sono contenute in un blocco interno diventano visibili anche nel blocco che la contiene.

Può avere **side effect - effetti collaterali**: l'esecuzione di una funzione non è più confinato all'interno del suo ambiente e interessa variabili di altre funzioni.

L'uso di variabili globali è solitamente sconsigliato.

Concetto di blocco: posto compreso tra due graffe.



***Ciclo di vita delle variabili***

- allocate una sola volta e poi distrutte
- **static**: persistenti all'interno e all'esterno di invocazioni di funzioni.
- **dinamic** (o automatiche) dichiarate esplicitamente dal programmatore.