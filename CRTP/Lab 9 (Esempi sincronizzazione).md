[[Lab9 - synchronization example 2627.pdf|Slide di riferimento]]

Definiamo sincronizzazione come il meccanismo che si assicura che due o più task concorrenti non eseguano simultaneamente una **sezione critica**.

L'uso sbagliato o mancante di sistemi di sincronizzazione porta a due tipi di fallimento:
* **Safety**: i dati sono corrotti o persi (stato inconsistente).
* **Liveness**: deadlock, lost wakeup, starvation (nessun progresso).

Possiamo usare tool esterni o interni al compilatore per **individuare races** all'interno del codice.
* **Helgrind** per la race detection esterna.
* **ThreadSanitizer (TSan)** per la race detection nel compilatore.

