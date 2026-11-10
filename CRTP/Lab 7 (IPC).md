[[lab7 - sockets.pdf|Slide di riferimento]]

 I sistemi distribuiti sono utili perché
 * Offrono **maggiore potenza di calcolo**, in quanto è possibile usare più macchine comunicanti tra loro.
 * Danno la possibilità di **distribuire i dati**, e permettono di elaborarli in un luogo (quello dove vengono collezionati) prima di essere inviati ad un server centrale per il resto dell'elaborazione.
 * Permettono di **evitare il single point of failure**, ovvero permettono al sistema di rimanere operativo anche se una delle macchine che lo compongono dovesse fallire.

Si noti che, utilizzando un sistema distribuito, si aggiunge latenza nel trasferimento di informazioni.

## Modello OSI

Si suddivide la comunicazione in 7 livelli, i primi 3 dei quali sono i **media layers**, mentre gli ultimi 4 sono **host layers**.
IMMAGINE

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

Attualmente la comunicazione Ethernet ha superato tecnologie LAN come Token Ring, FDDI, ARCNET.
L'alternativa wireless ad Ethernet è il WiFi.


