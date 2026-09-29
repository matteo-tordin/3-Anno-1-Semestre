
## Dati e informazioni

> [!info] Dato
> Un **dato** è la **rappresentazione di un evento** attraverso una **sequenza di simboli**.

Deve essere
* **Non interpretato**
* **Salvato su un supporto**

Consideriamo come esempio il seguente caso (prezzo di alcune azioni):

| max    | min    | id    | hh  | mm  | ss  |
| ------ | ------ | ----- | --- | --- | --- |
| 219.05 | 218.15 | 05023 | 11  | 52  | 17  |
Questi non sono più semplici dati, in quanto sono stati interpretati specificando il significato di ogni valore. 

> [!info] Informazione
> L'**informazione** è un **insieme di dati** sottoposto ad un processo di **interpretazione**.

## Il modello Entry-Relationship

Nella maggior parte delle basi di dati che considereremo in questo corso si userà il **modello** 
**Entity-Relationship** (ER) / UML
Per rappresentarlo si usa il **rettangolo** per l'**entità** e il **rombo** per l'**associazione**.
Gli **attributi** di un'entità si rappresentano con **pallini** vuoti collrgati al rettangolo (pieni se sono identificatori univoci)
Qualsiasi cosa non possa essere rappresentata tramite entità o associazioni può essere scritta a parole tramite regole di vincolo.

Consideriamo la seguente rappresentazione di un'entità "Utente":

![[Utente ER.svg]]

Notiamo che gli attributi possono avere diverse caratteristiche:
* **Attirbuto identificatore**: Uno o più attributi che definiscono univocamente un'entità. Si indicano scurendo il pallino che li identifica.
* **Vincoli numerici**: Si possono fornire vincoli sul numero di valori per ogni attributo. 
	(0,1) indica che il valore può essere unico o non esserci affatto.
	(1,n) indica che deve esserci almeno un valore.
* **Attributi composti**: Un attributo formato da altri attributi. Nella rappresentazione logica si scomporrà in una serie di attributi semplici.

Prendiamo ora un caso con attributi e associazioni:

![[Studente-Insegnamento ER.svg]]

Da cui si evince che
* Alcuni **attributi identificatori** funzionano solo se **combinati** (il solo nome del corso potrebbe non essere univoco, così come il corso di laurea).
* Le **associazioni possono avere attributi**. Il voto con cui uno studente supera l'esame di un insegnamento non è un attributo né dello studente né dell'insegnamento, ma del legame che c'è tra i due.
* Le associazioni accettano vincoli numerici in entrambi i sensi: uno studente può seguire da 0 a n corsi, ma un corso necessita di almeno uno studente che lo segua per essere inserito nella base di dati.

## Progettazione di una base di dati

Si inizia dall'**analisi dei requisiti**.
Dallo schema ER si passa allo **schema logico** in cui si definiscono le varie **tabelle** collegate tra loro.
Lo schema rimane per lo più invariato. Si possono aggiungere attributi allo schema ER (colonne nella tabella) o associazioni (collegamenti tra tabelle) a seconda delle necessità della base di dati.
Dallo schema logico si passa infine all'**implementazione SQL**.. 

Questo è uno schema di sviluppo **a cascata**. Un **errore** nella parte dell'implementazione SQL va corretto in tutti i **livelli precedenti**. Risulta molto più conveniente prestare grande attenzione alla progettazione concettuale prima di procedere. 

