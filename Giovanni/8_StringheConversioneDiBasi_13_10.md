



## LEZIONE 13/10

 -- continuazione lezione sulle stringhe --

Approfondimento lettura e scrittura dei caratteri.

```c
scanf("%d", &c); // lo scan usa il "<paramatro>" per capire cosa leggere
printf("stampa il carattere %c e il numero del carattere %d", c, c);
    // in questo caso stampa il primo printf con il carattere, mentre il secondo restituisce il codice ASCII del carattere, cioè il valore intero del carattere.
    // il codice funziona anche con il carattere \n e poi restituisce anche il suo valore ASCII del carattere \n.
    
    // ciclo while per stampare tutto, cioè stampa fino al valore nullo \0
i = 0;
while (stringa[i]){// questo avviene perchè ci sarà un while (0) alla fine. In C, 0=Falso
    printf("valore stringa %c", i);
    i++;
}

printf(stringa); //funziona, ma ci si aspettava che si rompesse. Per funzionare allora funziona, ma se si valuta la correttezza del linguaggio e formale allora il comando è sbagliato. In questo caso il compilatore lascia un "warning" cioè avvisa, ma compie anche un best-guest, cioè inserisce quello che ritiene più giusto.
```

### OPERAZIONI E CONVERSIONE TRA BASI DIVERSE:

- base decimale: uso di 10 cifre, 0-9.
- base binaria: rappresenta il modo fisico in cui la memoria e la cpu lavorano.
  - mi perdo qualcosa se rappresento in base binaria qualcosa prima rappresentato in base 10.
  - ![image-20201013122920820](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013122920820.png)





##### sistema decimale:

- si usano le dieci cifre
- valore dipende dalla posizione (notazione posizionale)
- cifre più significative verso sinistra, destra meno significative
- ![image-20201013123043132](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123043132.png)
- il pedice (10), indica la natura del numero, decimale in questo caso.



##### sistema binario

- si usano solo due cifre (1-0)

- valore posizionale della cifre

- più significative andando verso sinistra (More Significal BIt), il  valore di destra è meno significativa (Less Significal Bit)

- ![image-20201013123347825](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123347825.png)

- come prima il pedice (2) indica la natura binaria del numero.

- per passare da base binaria a decimale: 

  ![image-20201013123555457](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123555457.png)





##### sistema ottale:

![image-20201013123655412](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123655412.png)





![image-20201013123737807](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123737807.png)



##### sistema esadecimale:

- uso di 16 basi: 0-9 + ABCDF
- ![image-20201013123825951](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123825951.png)
- per trasformalo in base decimale l'algoritmo è sempre la conversione sul concetto di base posizionale esponenziale.
- ![image-20201013123935599](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013123935599.png)





### Conversione dei valori:

- dato valore in base decimale a valore binario:
- ![image-20201013124154661](C:\Users\giova\AppData\Roaming\Typora\typora-user-images\image-20201013124154661.png)
- in questo algoritmo il più significativo è l'ultimo risultato, che va stampato per primo 
- la conversione restituisce il valore (10011)



-- casissimo alla fine, durante la dimostrazione --

​		dimostrazione dell'algoritmo da decimale a binario e viceversa.

```c
// ultimo file in c99, è presente il tipo di variabile bool
#include <stdbool.h>
_Bool = True;
```

anche la conversione da decimale a ottale avviene con un algoritmo molto simile a quello visto prima, si raccolgono i resti della divisione, poi si raccolgono i resti.

algoritmo da decimale a base esadecimale è anche questo identico a quelli visti prima.  