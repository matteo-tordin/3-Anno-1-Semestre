[[Lab9 - synchronization example 2627.pdf|Slide di riferimento]]

Definiamo sincronizzazione come il meccanismo che si assicura che due o più task concorrenti non eseguano simultaneamente una **sezione critica**.

L'uso sbagliato o mancante di sistemi di sincronizzazione porta a due tipi di fallimento:
* **Safety**: i dati sono corrotti o persi (stato inconsistente).
* **Liveness**: deadlock, lost wakeup, starvation (nessun progresso).

Possiamo usare tool esterni o interni al compilatore per **individuare races** all'interno del codice.
* **Helgrind** per la race detection esterna.
* **ThreadSanitizer (TSan)** per la race detection nel compilatore.

Consideriamo come esempio il problema del produttore-consumatore.
L'idea della sincronizzazione è di produrre dei periodi definiti di attività per ciascun thread, in modo da evitare la lettura di dati non pronti o la sovrascrittura di dati non letti.

Usiamo due funzioni per realizzare l'**attesa**:

```
int pthread_cond_wait(pthread_cond_t *restrict cond, pthread_mutex_t *restrict mutex);

int pthread_cond_timedwait(pthread_cond_t *restrict cond, pthread_mutex_t *restrict mutex, const struct timespec *restrict abstime);
```

La differenza sta nel fatto che la seconda contenga un timeout massimo.

Tali funzioni **vanno chiamate dopo aver bloccato il mutex e all'interno di un ciclo while**.
La loro chiamata si occupa automaticamente del rilascio di tale mutex e del bloccaggio del processo sulla condizione indicata.

Usiamo due funzioni per realizzare la **segnalazione** di una condizione:

```
int pthread_cond_signal(pthread_cond_t *cond); 

int pthread_cond_broadcast(pthread_cond_t *cond);
```

La differenza sta nel fatto che signal sveglia almeno un thread in attesa, mentre broadcast si usa quando ogni thread in attesa deve vedere il cambiamento.

