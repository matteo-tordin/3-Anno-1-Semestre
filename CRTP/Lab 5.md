[[lab5 - parallel processing.pdf|Slide di riferimento]]


## Parallel processing e scheduling

Il [[2. Parallel processing|parallel processing]] si ottiene nel sistema operativo scambiando continuamente il processo in esecuzione all'interno di una CPU.

Lo **scheduler** si occupa dello scambio dei processi in esecuzione.

Ogni volta che il processo in esecuzione cambia, avviene un **context switch**:
Vengono salvati:
* I registri **program counter** e **stack pointer**
* I descrittori dei file aperti dal processo
* La page table relativa al processo
* Le strutture dati del sistema operativo per la gestione del processo.

Le informazioni salvate in un context switch sono salvate in un **Process Control Block (PCB)**, che risiede **nella memoria del kernel**.

I processi sono organizzati per **priorità**. Un processo ad alta priorità verra scelto dallo scheduler prima di altri.

I principali algoritmi di scheduling sono
* **First In First Out (FIFO)**
* **Round Robin (RR)**


## Processi in Linux

La creazione di processi in Linux avviene tramite una chiamata a sistema: **fork()**.
Tale chiamata genera un **clone del processo chiamante**, replicandone la memoria e le strutture dati associate, compresi i registri del processore.
Tali processi (**padre e figlio**) sono eseguiti in due **spazi di memoria differenti**.


## Layout di memoria di un processo

La memoria assegnata ad un processo si divide in
* **Stack:** Contiene le variabili private e gli argomenti delle routine attive. Solitamente il processore ha un registro designato che punta alla cima dello stack.
* **Text:** Contiene le istruzioni macchina del processo. E' un'area di sola lettura.
* **Data:** Contiene le variabili statiche e globali. Si divide di solito in **data** per le variabili inizializzate e **bss** per quelle non inizializzate.
* **Heap:** Contiene le strutture allocate dinamicamente (con malloc() in c o con l'operatore new in c++).

E' possibile osservare le regioni di memoria utilizzate da un processo (in Linux, tramtite il comando `cat maps` chiamato dalla cartella del processo `/proc/<PID>` ).
Ogni riga di `/proc/<PID>/maps` corrisponde ad un segmento contiguo di memoria. Contiene
* Indirizzo del segmento
* Permessi
* Offset (solo se si tratta di un file con mmap(), altrimenti vale 0)
* Device (major e minor number del device dove vive il file)
* Inode (numero dei file)
* Pathname (percorso del file)


## PCB in Linux

Nel kernel Linux, i processi sono salvati in una lista doppiamente concatenata di **task_struct**.
Il primo elemento di tale lista è **init_task**, con PID = 0.

## Fork in Linux

Quando una chiamata **fork()** ritorna, i due processi sono identici, e nello stesso punto della loro esecuzione.
L'unica differenza sta nel **valore di ritorno**
* Se viene ritornato **0**, ci troviamo nel **processo figlio**.
* Se il valore di ritorno è il **PID del nuovo processo**, ci troviamo nel **processo padre**.

E' possibile **attendere la terminazione del processo figlio** tramite l'istruzione 
`pid_t wait(pid_t pid, int *status, int options) `

Le uniche **differenze tra padre e figlio** consistono in
* PID
* Utilizzazione delle risorse (i valori sono azzerati per il figlio)
* *Segnali*
* *Semafori*
* *Timer*
* *Operazioni di I/O asincrono*
* *Memory locks*

La memoria del processo padre non viene immediatamente copiata dal figlio.
La page table del figlio punterà ancora alle pagine del padre, che verranno marcate come **Copy on Write (CoW)**.


## Memoria condivisa tra fork

Possiamo sfruttare la **memoria virtuale** per **condividere memoria tra padre e figlio**.
`int shmget(key_t key, size_t size, int shmflg)`
* Key è una chiave
* Size è la dimensione desiderata della regione di memoria condivisa.
* Smhflg sono i flag relativi al modo in cui tale memoria verrà utilizzata.

La **chiave** di tipo **key_t** è necessaria in Unix per richiedere risorse.
Può essere generata tramite la funzione **ftok()**, che richiede un path e un intero e genera una chiave basandosi su questi valori. La chiave generata sarà uguale per ogni chiamata con gli stessi argomenti.
Altrimenti, tramite **IPC_PRIVATE**, si genera una chiave univoca ogni volta, garantendo che nessun altro processo possa avere la stessa chiave.


## Threads

Sono sostanzialmente affini ai processi nel senso che rappresentano flussi indipendenti di esecuzione.
La differenza risiede nel fatto che i thread condividano l'area di memoria del processo di cui fanno parte, oltre agli stessi file e devices.
Sono pertanto detti **processi leggeri (lightweight processes)**.

Ogni thread possiede un program counter (che viene inizializzato al momento della sua esecuzione all'indirizzo dove risiedono le sue istruzioni) e un proprio stack pointer.

La gestione dei thread in Linux avviene tramite la libreria **pthread**.

Aumentare il numero di thread aumenta le prestazioni del sistema, ma fino ad un certo punto. 
Sopra ad un determinato valore. l'overhead del context switch ricomincia a peggiorarle.

![[Pasted image 20261027134939.png|298]]

