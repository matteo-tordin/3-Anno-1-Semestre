
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


Nella maggior parte delle basi di dati che considereremo in questo corso si userà il **modello** 
**Entity-Relationship** (ER) / UML
Per rappresentarlo si usa il **rettangolo** per l'**entità** e il **rombo** per l'**associazione**.
Gli **attributi** di un'entità si rappresentano con **pallini** vuoti collrgati al rettangolo (pieni se sono identificatori univoci)
Qualsiasi cosa non possa essere rappresentata tramite entità o associazioni può essere scritta a parole tramite regole di vincolo.

Si inizia dall'**analisi dei requisiti**.
Dallo schema ER si passa allo **schema logico** in cui si definiscono le varie **tabelle** collegate tra loro.
Lo schema rimane per lo più invariato. Si possono aggiungere attributi allo schema ER (colonne nella tabella) o associazioni (collegamenti tra tabelle) a seconda delle necessità della base di dati.
Dallo schema logico si passa infine all'**implementazione SQL**.. 

Questo è uno schema di sviluppo **a cascata**. Un **errore** nella parte dell'implementazione SQL va corretto in tutti i **livelli precedenti**. Risulta molto più conveniente prestare grande attenzione alla progettazione concettuale prima di procedere. 


> [!info] Base di Dati
> Una **base di dati** è un **insieme di dati coerenti** e con un preciso significato che rappresenta un **qualche aspetto del mondo** reale.

madonna puttanaccia
dio negrone