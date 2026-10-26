
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

## Ottimizzazione

Possiamo comunicare al compilatore di ottimizzare il codice con alcune flag
* -**O0**: ottimizzazione per il tempo di compilazione (standard).
* -**O1**: ottimizzazione per il tempo di esecuzione.
* -**O2**: come O1 ma migliore (aumenta tempo di compilazione)
* -**O3**: come O2 ma migliore (aumenta tempo di compilazione)

## Inlining

Tramite la keyword "inline" si suggerisce al compilatore di sostituire ogni chiamata ad una funzione con le operazioni in essa contenute, **senza eseguire un context switch** ad ogni chiamata.
* Si risparmia l'overhead di una chiamata a funzione
* Si risparmia l'overhead del context switch
* Si risparmia l'overhead del ritorno dalla funzione
* Il compilatore può eseguire ottimizzazioni sul codice che non potrebbe eseguire con la chiamata a funzione.

L'inlining **non si può eseguire** se 
* La funzione contiene loop
* La funzione contiene variabili statiche
* La funzione è ricorsiva
* La funzione ha un tipo di ritorno che non è void
* La funzione contiene istruzioni switch o goto

*E' possibile definire la funzione come inline, ma il compilatore ignorerà la direttiva.*

## Constant folding

Se una variabile non cambia mai valore durante l'esecuzione, può essere sostituita da un valore costante nel codice macchina, risparmiando tempo.

## Dead code elimination

Se vengono eseguiti calcoli a vuoto (ad esempio calcoliamo un valore senza mai usarlo), la riga di codice viene eliminata dal compilatore.

## Branch elimination

Se una istruzione condizionale non ha senso di esistere, viene sostituita da una istruzione senza branch.

## Partial evaluation

Il compilatore può eseguire alcune funzioni e calcolarne direttamente il valore prima di passare al codice macchina.

## Late scheduling

Se un calcolo viene eseguito sempre ma il risultato viene usato solamente in un branch, allora il compilatore può riordinare le istruzioni in modo che l'intero calcolo venga eseguito solo in quel branch.

## Risultato finale

Applicando tutte le tecniche di ottimizzazione viste sopra, si ottiene questo codice

![[Pasted image 20261026153527.png]]

