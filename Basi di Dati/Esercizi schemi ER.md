
## 1 - Studenti e corsi di laurea

Per ogni stutende nome, cognome, matricola, data di nascita.
Per ogni corso id, denominazione, anno.
Ogni studente deve essere iscritto ad un solo corso di laurea.
Un corso può esistere anche senza studenti iscritti.

![[Studenti e corsi.svg]]

## 2- Esami

Per ogni stutende nome, cognome, matricola.
Per ogni corso id, denominazione, anno, cfu.
Uno studente può superare più insegnamenti.
Per ogni esame superato bisogna registrare data, voto, eventuale lode.

![[Esami.svg]]

NOTA: Lo schema ER proposto è detto **intensionale**. Una vista **estensionale** prevede una rappresentazione tramite insiemi matematici, in cui non sono inclusi gli attributi, come questa:

![[Esami-estensionale.svg|700]]

E' importante sottolineare che gli **insiemi non prevedono ripetizioni** dei propri elementi. Il che significa che anche le coppie studente-corso possono essere registrate una volta soltanto (e quindi non è possibile per esempio registrare due appelli per lo stesso studente).

## 3- Libri, autori, editori

Per ogni libro isbn, titolo, anno, pagine.
Per ogni autore codice, nome, cognome, data di nascita.
Per ogni editore codice, nome, città.
Ogni autore può scrivere più libri ed essere aggiunto alla base di dati anche senza che ci siano libri associati ad esso.
Ogni libro deve essere scritto da almeno un autore.
Ogni editore può pubblicare più libri ed essere aggiunto alla base di dati anche senza che ci siano libri associati ad esso.
Ogni libro deve essere pubblicato da un solo editore.

![[Libri.svg]]

NOTA: Nel caso di un campo come la città, in cui il testo è limitato ad una quantità finita di valori, le possibili opzioni sono
* Vincolare i valori tramite un'enumerazione.
* Promuovere l'attributo città ad una nuova entità.
Si rischia altrimenti di avere valori differenti per la stessa città (ad esempio "Padova" e "padova").

## 4 - Dipendenti azienda

NOTA: Se volessi indicare un minimo di valori da inserire maggiore di 1 ma arbitrario, si può indicare con la dicitura "(n,m)" (il dipartimento esiste se sono presenti alcuni dipendenti, ma non uno).

![[Dipendenti azienda.svg]]

Essendo l'impegno un valore percentuale, non deve superare il 100%. Per risolvere questo problema posso
* Sommare le percentuali di impegno di un dipendente prima di inserire un dato, eventualmente impedendolo.
* *boh l'ho perso*

## Medici e pazienti


![[Medici e pazienti.svg]]

Si potrebbe promuovere la specializzazione ad entità per evitare i problemi già analizzati riguardanti i campi di testo (alternativamente si può usare l'enumerazione).

Sarebbe possibile realizzare una relazione tra 3 entità siccome una visita ha sempre un medico e un paziente assegnati ad essa. Il risultato finale sarebbe lo stesso. 