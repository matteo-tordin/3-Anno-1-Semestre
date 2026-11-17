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
1) Un server rimane connesso ad un client che non ha invocato close().
2) Un server crea un processo figlio per gestire una connessione ad un client. Il server termina, mentre il figlio continua a gestire la richiesta.

### SO_KEEPALIVE (TCP)

Immaginiamo di avere un server con una serie di client connessi.
Se i **client perdono la connessione momentaneamente** (diciamo per un guasto), riproveranno a **ristabilire la connessione tutti nello stesso momento**.

Se il sever