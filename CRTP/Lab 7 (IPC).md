[[lab7 - sockets.pdf|Slide di riferimento]]

 I sistemi distribuiti sono utili perché
 * Offrono **maggiore potenza di calcolo**, in quanto è possibile usare più macchine comunicanti tra loro.
 * Danno la possibilità di **distribuire i dati**, e permettono di elaborarli in un luogo (quello dove vengono collezionati) prima di essere inviati ad un server centrale per il resto dell'elaborazione.
 * Permettono di **evitare il single point of failure**, ovvero permettono al sistema di rimanere operativo anche se una delle macchine che lo compongono dovesse fallire.

Si noti che, utilizzando un sistema distribuito, si aggiunge latenza nel trasferimento di informazioni.

## Modello OSI

Si suddivide la comunicazione in 7 livelli, i primi 3 dei quali sono i **media layers**, mentre gli ultimi 4 sono **host layers**.

![[Pasted image 20261110154116.png|461]]

### Phisical layer

E' il **primo livello**.
Definisce le **caratteristiche elettriche** della comunicazione.
Ad esempio, si definiscono i livelli logici, come è organizzato il canale di comunicazione, etc...

### Data link layer

E' il **secondo livello**.
Definisce **come l'informazione viene trasferita**. Nel caso della comunicazione via internet si usano
* **Logical Link Control (LLC)**
* **Media Access Control (MAC)**

Nel caso di dati condivisi tramite Ethernet, il frame del livello 2 contiene i dati binari e le seguenti informazioni:

![[Pasted image 20261110130834.png]]

* Il **preambolo** serve per sincronizzare ricevitore e trasmettitore e per eliminare qualsiasi bias elettrostatico presente nel canale.
* Il **MAC di destinazione** è l'indirizzo del ricevitore del frame.
* Il **MAC di sorgente** è l'indirizzo del trasmettitore del frame.
* La **lunghezza del pacchetto** contiene le informazioni sulla dimensione del segmento di dati.
* **LLC**.
* **Dati** del pacchetto (massimo 1500 byte).
* **CRC** (Cyclic Redundancy Check) che individua eventuali errori di comunicazione. Viene calcolato dal trasmettitore e poi ricalcolato dal ricevitore e confrontato.
* **Gap tra frame** (la distanza minima da rispettare tra due frame consecutivi).

Attualmente la comunicazione Ethernet ha superato tecnologie cablate LAN come Token Ring, FDDI (usato per la fibra ottica), ARCNET.
L'alternativa wireless ad Ethernet è il WiFi.

I layer MAC e quello fisico (PHY) sono resi tra loro indipendenti da alcune **interfacce di collegamento**, che usano un protocollo standardizzato per qualsiasi cosa si connetta ad esse.
E' quindi possibile cambiare il cavo di comunicazione senza cambiare il layer MAC, ma solamente quello PHY.

#### Network

E' il **terzo livello**.
Si tratta del livello di **trasporto**.
Nel nostro caso, consideriamo il **protocollo internet IP** e il **protocollo di trasmissione TCP**.
Insieme compongono il **protocollo TCP/IP**.

![[Pasted image 20261110133215.png|463]]


Il protocollo **IP** definisce le funzionalità necessarie per la trasmissione di pacchetti attraverso uno o più reti.

*Per vedere i contenuti del layer IP vedi [[lab7 - sockets.pdf#page=14|slide 14]].*

Il protocollo **TCP** garantisce la **correttezza** e la **consegna in ordine** di un flusso di dati.

*Per vedere i contenuti del layer RCP vedi [[lab7 - sockets.pdf#page=16|slide 16]].*


Per garantire la consegna dei pacchetti, si esegue una **3-way handshake**: 
1) Il client invia una richiesta di connessione, accendendo il bit **SYN**.
2) Il server accetta la richiesta, accendendo **SYN** e **ACK**.
3) Il client risponde con **ACK** per comunicare al server di aver ricevuto il suo segnale.
A questo punto la connessione è operativa.

All'interno del pacchetto sono definiti anche tutti i frame dei livelli inferiori.
Il **TCP/IP stack** contiene le informazioni del livello TCP, sopra a quelle del livello IP, a loro volta sopra quelle del livello Ethernet.

![[Pasted image 20261110133944.png|383]]


## Socket

I socket sono **strutture dati del sistema operativo** che fungono da **endpoint di una rete di comunicazione**.

I socket sono degli **pseudo file** che rappresentano una connessione ad una rete.
Una volta creato il socket, le **scritture** su tale file sono trasformate in pacchetti e inviate nella rete, mentre è possibile reperire i pacchetti ricevuti tramite **letture** al file.

Esistono diverse tipologie di socket:
* **Stream socket**: utilizzati per il protocollo TCP. Permettono la trasmissione assicurata e senza errori di un flusso di dati.
* **Datagram socket**: utilizzati per il protocoloo UDP. L'ordine di arrivo, così come l'arrivo stesso, non sono garantiti.
* **Raw socket**: permettono l'invio di pacchetti IP senza nessun layer di trasporto.


### Codice per creare e usare socket

La richiesta di **creazione** di un socket avviene tramite l'operazione
`int socket(int domain, int type, int protocol);`

* **domain** specifica il dominio degli indirizzi (ad esempio, AF_INET corrisponde a IPv4, mentre AF_INET6 corrisponde a IPv6).
* **type** specifica il tipo di socket richiesto (SOCK_STREAM, SOCK_DGRAM, SOCK_RAW).

Il protocollo può essere lasciato a 0 e verrà determinato automaticamente a seconda del tipo.

Dopo la creazione si esegue il **bind** del socket

