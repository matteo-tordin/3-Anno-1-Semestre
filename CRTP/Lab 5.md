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

Quando una chiamata **fork()** ritorna, i due processi sono identici, e nello stesso punto della loro esecuzione.
L'unica differenza sta nel **valore di ritorno**
* Se viene ritornato **0**, ci troviamo nel **processo figlio**.
* Se il valore di ritorno è il **PID del nuovo processo**, ci troviamo nel **processo padre**.

E' possibile **attendere la terminazione del processo figlio** tramite l'istruzione 
`pid_t wait(pid_t pid, int *status, int options) `

Le uniche **differenze tra padre e figlio** consistono in
* PID
* Utilizzazione delle risorse (i valori sono azzerati per il figlio)
* Segnali in attesa (azzerati)
* Semafori
* Timer
* Operazioni di I/O asincrono
* Memory locks

