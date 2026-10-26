
[[lab4 - optimization.pdf|Slide di riferimento]]

## Compilatore gcc

Le tre fasi della compilazione di un codice c sono
* **Preprocessore** (flag -E per fermarsi qui)
* **Compilazione**: traduzione in linguaggio macchina (flag -c per fermarsi al file oggetto)
* **Linking**

Il funzionamento del compilatore **gcc** è il seguente:
Si converte il codice sorgente in un **abstract syntax tree (AST)**, che poi viene tradotto in diversi linguaggi intermedi durante la compilazione:
GENERIC -> GIMPLE -> SSA -> RTL.
Infine, viene generato il codice macchina.

![[Pasted image 20261026144755.png|537]]

## Abstract Syntax Tree

Una rappresentazione ad albero che contiene tutte le informazioni fornite dal codice sorgente, tutto ciò che riguarda il control flow e tutte le informazioni su strutture e tipi di dati.

![[Pasted image 20261026145102.png|448]]


## GIMPLE

E' un tipo di rappresentazione intermedia.
Si definiscono alcune operazioni come "goto" per i salti (e per i loop).
Si definiscono alcuni **basic block**, dei blocchi di codice con una sola entrata e una sola uscita.

## SSA (Static Single Assignment)

Si basa sulla premessa che una variabile sia assegnata una sola volta nel codice.
Una nuova assegnazione genera una nuova variabile.

## RTL (Register Transfer Level)

Si descrive il codice mediante operazioni sui registri, in maniera simile all'assembly, ma senza specificare i registri esatti.

![[Pasted image 20261026145728.png]]


*Vedi esempio sulla funzione di Ackermann.*

