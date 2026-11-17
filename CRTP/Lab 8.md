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

