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

E' il primo dei livelli.
Definisce le **caratteristiche elettriche** della comunicazione.
Ad esempio, si definiscono i livelli logici, come è organizzato il canale di comunicazione, etc...

