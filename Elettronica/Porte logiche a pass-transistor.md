
[[3d.Logica Pass Transitor.pdf|Slide di riferimento]]

Il concetto di **pass-transistor** (**pass-T**) è quello che si avvicina di più all'uso del MOS come interruttore.
Si tratta di un'alternativa alla logica statica complementare.

Nella **logica statica complementare** gli **ingressi** sono **collegati solo ai gate** dei transistor.
Nella logica **pass-transistor** gli **ingressi** sono **collegati sia al gate che al source/drain**.

DA SISTEMARE fino a slide 6

## Implementazione di funzioni complesse

Sfruttiamo il **teorema di Shannon**:
Ogni funzione logica a N variabili F(A,B,C,...) può essere espressa come 
FORMULA
IMMAGINE

## Caratteristiche statiche

Consideriamo la caratteristica di trasferimento di una porta **AND** realizzata tramite **pass-T NMOS**:

![[Pasted image 20261105150055.png|476]]

Nemmeno realizzandola tramite **pass-T PMOS** la situazione cambierebbe:

![[Pasted image 20261105150159.png|489]]


Questo è dato dal fatto che
* Un **NMOS** è **efficiente** solo nel trasmettere il **valore logico basso**.
* Un **PMOS** è **efficiente** solo nel trasmettere il **valore logico alto**.

Generalmente, **si preferisce** sempre l'uso di **NMOS** rispetto ai PMOS perché sono **più rapidi**.

## Connessioni in cascata di pass-T

DA SISTEMARE

Dunque, il **valore di uscita** di una porta **pass-T** **può pilotare** solamente il **source/drain** di una seconda porta, ma **non il gate**.

Se collegassimo una porta pass-T ad un invertitore CMOS, la tensione trasmessa dalla prima non sarà perfetto, ma sarà ad esempio $V_{DD}-V_{T}$ nel caso di un valore alto trasmesso da un pass-T NMOS.
Questo non è un problema dal punto di vista logico, in quanto l'inverititore rispetta la probabilità di rigenerazione del segnale, attenuando l'errore.
Il problema è che in questo modo il PMOS non è spento. Questo genera un consumo statico.


## Ottimizzazione dei valori logici

### Level restorer

DA SISTEMARE 

### Transmission gate (TG)

Mettiamo un NMOS e un PMOS in parallelo, pilotati da un segnale A.
* Se A è basso, sono entrambi spenti. L'interruttore è aperto.
* Se A è alto, sono entrambi accesi. L'interruttore è chiuso.

In questo modo, qualsiasi sia l'ingresso riusciamo a trasmetterlo perfettamente all'uscita.
* Se l'ingresso è basso, entrambi i MOS inziano a scaricare l'uscita. Quando il PMOS si spegne, l'NMOS continua a scaricare da solo.
* Se l'ingresso è alto, entrambi i MOS iniziano a caricare l'uscita. Quando l'NMOS si spegne, il PMOS continua a caricare da solo.


## Tempo di propagazione

DA SISTEMARE
Il tempo di propagazione di una porta pass-T dipende dalla somma di tutte le capacità di uscita, oltre alla capacità di carico.
Si ha dunque
FORMULA
In cui $C_{F}=C_{OUT}+c_{L}$.

Il **collegamento in cascata** peggiora notevolmente rispetto alla logica statica complementare.
Infatti, in quel caso l'impedenza è infinita, dunque non passa corrente.

Nel caso del pass-T, la corrente passa. Una connessione in cascata diventa una **rete di Elmore**
DA SISTEMARE


## Ottimizzazione delle prestazioni

Se tutte le resistenze e le capacità sono uguali, usando la formula di Elmore troviamo $$t_{p}=0,69\cdot RC\cdot \frac{{N(N+1)}}{2}$$
E dunque **dipende quadraticamente da N**.

Per ottimizzare, la soluzione è dividere gli N MOS in serie in K gruppi da M elementi, intervallati da un buffer CMOS.

Ora, ogni gruppo ha un tempo di propagazione dato dalla somma del tempo degli M MOS e del buffer: $$t_{pass-T}=0,69\cdot RC\cdot \frac{{M(M+1)}}{2} + t_{BUF}$$
Da cui, il tempo totale di propagazione diventa
FORMULA

Ottimizzando tramite la derivata si calcola il numero M ideale:
FORMULA

Generalmente, si trova un M che si aggira tra 4 e 5.


## Consumo dinamico delle porte logiche

DA SISTEMARE


DA FINIRE fino a 