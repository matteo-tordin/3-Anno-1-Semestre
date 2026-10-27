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

