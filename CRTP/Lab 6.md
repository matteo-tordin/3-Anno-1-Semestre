[[lab6 - parallel processing.pdf|Slide di riferimento]]

Consideriamo il classico problema SPSC (Single Producer Single Consumer).

## SPSC sleep-wakeup cicle

Consideriamo un esempio con sleep e wakeup per sincronizzare i due.

#### Problema 1: lost wakeup (race condition)
Se i processi effettuano un context switch nel momento sbagliato, può verificarsi il problema del **lost wakeup**, che provoca un deadlock.

*Vedi esempio alla [[lab6 - parallel processing.pdf#page=5|slide 5]].*


## SPSC circular buffer

Usiamo ora un buffer circolare per regolare la comunicazione tra producer e consumer.

Definiamo:
* **Race condition:** dipende dal **timing delle operazioni**.
* **Data race:** dipende dall'accesso in **scrittura senza mutua esclusione** alla stessa area di memoria.

#### Problema 2: Publish before write (race condition)
Se il produttore aggiorna l'indice e poi aggiorna le memoria, può accadere che il consumatore legga la memoria prima che essa sia aggiornata.

La soluzione è eseguire le operazioni in questo ordine:
In scrittura
1) scrivere il dato
2) aggiornare l'indice

Mentre in lettura
1) leggere il dato
2) rilasciare lo slot

*Vedi esempio alla slide 8.*

#### Problema 3: Reordering and caching (data race)

Le operazioni possono essere riordinate, oppure il processore può caricare un indice nei registri senza sapere che sta venendo modificato. 
Questo porta ad errori nell'esecuzione nonostante sua rispettato l'ordine delle istruzioni nel codice sorgente.

La soluzione è usare operazioni atomiche e la semantica di memoria

*Vedi slide 9*


#### Problema 4: Torn index update

Si verifica quando le operazioni di aggiornamento di un indice più lungo di una word viene spezzato in più operazioni in memoria.
Il consumatore potrebbe leggere nel momento sbagliato, ottenendo un valore errato.

Si devono usare oggetti atomici per gestire la memoria condivisa.

#### Problema 5: Two producers

