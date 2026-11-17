[[lab8 - datagrams.pdf|Slide di riferimento]]

## User Datagram Protocol (UDP)

Abbiamo visto che la connessione tramite socket può essere di due tipi
* **Stream**: un pipe di dati ordinati con verifica della connessione (3-way handshake). Vedi funzionamento del protocollo TCP.
* **Datagram**: comunicazione di pacchetti senza connessione. Non è detto che il pacchetto arrivi intatto, o arrivi in generale. L'ordine dei pacchetti non è controllato.

Un **socket datagram** può essere gestito solamente tramite le chiamate
* `recvfrom()` per ricevere pacchetti.
* `sendto()` per inviare pacchetti.

**Non è richiesta alcuna connessione** esplicita tra le due macchine.

Un **header UDP** è significativamente più semplice della sua controparte TCP.
E' composto da
* Porta di partenza
* Porta di destinazione
* Lunghezza
* Checksum

NOTA: nonostante non si effettui alcuna connessione (handshake), è comunque possibile eseguire una chiamata `connect()` "fasulla" che imposta semplicemente la destinazione dei pacchetti nel socket.

## MSG_CONFIRM

Possiamo usare la flag `MSG_CONFIRM` per bypassare la verifica del MAC del ricevente.
* **Vantaggi**: Miglioramento (marginale) delle performance della rete.
* **Svantaggi**: Se il device fosse sostituito da un altro con lo stesso IP ma MAC diverso, continuerebbe a ricevere pacchetti in quanto non si esegue alcuna verifica.

Conviene usare tale flag nel momento in cui si sta rispondendo ad un messaggio appena ricevuto (e quindi siamo certi che il MAC sia corretto).
Tale flag può essere usato per confermare all'altra parte la ricezione di un messaggio.

## UDP VS TCP

Una connessione **UDP può ricevere (e rispondere a) datagrammi da molti client**, senza la necessità di creare una diversa connessione per ciascuno di essi.

Inoltre, UDP risulta **più rapido** in quanto non è presente alcun overhead per handshake e verifica dell'ordine dei pacchetti.
E' particolarmente **utile nei sistemi real time**, in cui il delay indefinito causato dalla perdita di un pacchetto TCP può non essere accettabile.

## Socket Options

E' possibile usare una chiamata a `setsockopt()` per impostare alcune funzioni di un socket.

### SO_REUSEADDR

Permette ad una **coppia indirizzo/porta** di subire un **bind più volte** nello stesso sistema.
Ci sono due scenari per questa funzione:
1) Un server rimane connesso ad un client che non ha invocato close(). Il socket rimane aperto. Se si prova a ricreare la connessione, si va in contro ad errore.
2) Un server crea un processo figlio per gestire una connessione ad un client. Il server termina, mentre il figlio continua a gestire la richiesta.

### SO_KEEPALIVE (TCP)

Immaginiamo di avere un server con una serie di client connessi.
Se i **client perdono la connessione momentaneamente** (diciamo per un guasto), riproveranno a **ristabilire la connessione tutti nello stesso momento**.
Si generano nuove connessioni.

Il server non si rende conto di aver perso la connessione ai socket (che sono rimasti idle).
Per un periodo, le **risorse dedicate ai client saranno duplicate** (creerà nuovi socket).

Il flag SO_KEEPALIVE permette di di inviare **messaggi ai socket idle al fine di verificare la connessione**.
Ci sono 3 casi:
* Il peer risponde che la connessione è corretta.
* Il peer risponde che non conosce la connessione (era rimasto l'endpoint del server ma il client ha terminato la connessione). Si termina la connessione.
* Non viene ricevuta alcuna risposta. In tal caso si riprova, e in caso non si riceva niente si termina la connessione.

## SO_LINGER (TCP)

Si usa per definire **cosa fare alla terminazione della connessione**.

DA SISTEMARE

## SO_OOBINLINE (TCP)

Esistono dei **pacchetti Out-of-Bounds** nel TCP che possono essere spediti appena psosibile, invece di rispettare l'ordinamento.
Si usa di solito per **segnali urgenti** (allarmi).

Il flag permette di controllare questi pacchetti OOB.
* Se **attivo**, i dati OOB possono essere ricevuti insieme agli altri dati dello stream.
* Se **disattivo**, i dati OOB devono essere recuperati tramite chiamate come `recv(MSG_OOB)`.

### SO_ERROR

Permette di recuperare messaggi di errore ed error status di un socket.

DA SISTEMARE

## SO_TYPE

DA SISTEMARE


## Flag per send e recieve

DA SISTEMARE


## Nonblocking I/O

Nell'ambito della IPC la **connessione** può essere vista **come una risorsa condivisa** per sincronizzare un canale send-recieve.
* E' possibile bloccare l'input di un socket se non c'è nessun dato da leggere (**input lock**).
* E' possibile bloccare l'output di un socket se i dati non possono essere inviati immediatamente (**output lock**)

Nel **TCP** ci sono molte **più attese**, mentre in UDP ci si ferma solo per aspettare un messaggio dal sender.
In ogni caso, il **processo si deve interrompere**.

![[Pasted image 20261117133846.png]]

Analizziamo alcune **strategie per ottenere una connessione non bloccante**:

### Polling

Possiamo settare nel file descriptor del socket il flag `O_NONBLOCK`.

Equivalentemente, possiamo settare il flag `MSG_DONTWAIT` nel socket.

### Polling with delay

Possiamo usare le socket options `SO_RCVTIMEO` e `SO_SNDTIMEO` per impostare dei timeout per ricezione e invio di messaggi.

Il processo **continua a bloccarsi**, ma lo fa per un **tempo massimo definito**.

### Select

Una volta creato un socket con `O_NONBLOCK`, possiamo usare le funzioni `select()`, `poll()`, `epoll()` per far **attendere il processo fino a che il kernel non nota un cambio nel socket** (nel suo file).

La chiamata select avvisa il chiamante nel caso di
* nuovi dati da leggere
* eccezioni nel file descriptor

Richiede alcuni parametri:
DA SISTEMARE fino a 39

### Epoll

DA FINIRE