
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