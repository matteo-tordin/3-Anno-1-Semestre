
[[2a.Semiconduttori.pdf |Slide di riferimento]]

I **semiconduttori** sono materiali caratterizzati da una **resistività** tra i 10^-3 e i 10^5 $\ohm \cdot cm$.

Nella tavola periodica, si collocano tra gli **elementi di transizione** tra metalli e non metalli, attorno ai **gruppi III , IV e V**.

Possono essere a elemento **singolo**, oppure **composti** da più elementi, che in genere sono **simmetrici rispetto al gruppo IV** (come GaAs, InP, CdTe, etc...).

Un semiconduttore senza impurità è detto **intrinseco**.

---

L'**atomo** di silicio è caratterizzato da **14 protoni e 14 neutroni** nel nucleo. I suoi elettroni sono divisi nei livelli 1s (x2), 2s (x2), 2p (x6, due per ogni asse x,y,z), 3s (x2) e 3p (x2).
Al **livello più esterno** sono dunque presenti **4 elettroni** su 8 posti massimi. Questi si dicono elettroni **di valenza** e determinano le proprietà dell'atomo.

Il **reticolo cristallino** del silicio prevede che ogni atomo formi **legami con altri 4 atomi** formando una struttura tetraedrica. Ogni **legame** è composto da **due elettroni**.
Alla temperatura di 0K, la struttura cristallina è perfettamente intatta.
Alzando la temperatura (ad esempio ambiente a 300K), l'energia fornita agli elettroni può superare quella del legame, che si rompe. 
A questo punto l'**elettrone si libera**, lasciando al suo posto una **lacuna di carica +q**.

---

In un semiconduttore intrinseco, la densità di lacune "p" equivale alla densità di elettroni liberi "n". Tale quantità è detta **densità di portatori intrinseci**, e vale:

$$n_{i} = BT^3 \exp\left( -\frac{E_{G}}{kT} \right)$$

In cui $E_{G}$ è l'**energy gap** (energia per rompere il legame), T è la temperatura, B è una costante dipendente dal materiale, k è la costante di Boltzmann.
Si misura in $cm^{-3}$.
Nel caso del silicio, si ha $n_{i} \approx 2 \cdot 10^{23}cm^{-3}$.

È possibile **drogare** un semiconduttore **aggiungendo atomi di altri elementi**.
Esistono due tipi di drogaggio:
* **Tipo p**: atomi del III gruppo (es. boro) -> aumenta le lacune.
* **Tipo n**: atomi del V gruppo (es. fosforo) -> aumenta gli elettroni liberi.


In condizioni di **equilibrio termodinamico**, il **tasso di generazione** (liberazione di elettrone e formazione di lacuna) è una funzione crescente della temperatura: $$G = f_1(T)$$
Lo stesso vale per il **tasso di ricombinazione** (elettrone si ricongiunge alla lacuna): $$R=n\cdot p \cdot f_{2}(T)$$
All'equilibrio, i due tassi devono essere uguali. Si ha quindi $$f_{1}(T) = n \cdot p \cdot f_{2}(T) \Rightarrow \frac{f_1(T)}{f_{2}(T)} = n \cdot p = n_{i}^2$$
Da cui si ricava la **legge di azione di massa**   $n \cdot p = n_{i}^2$

Si considera un **semiconduttore drogato di tipo n**, con  $N_{D} \gg n_{i}$
Si formano $N_{D}$ ioni positivi (+q) che liberano ciascuno un elettrone (-q).
La carica totale in equiibrio deve essere nulla, quindi
$$-qn+qp+qN_{D}=0$$
Sfruttando la legge di azione di massa otteniamo $$n -p-N_{D}=0 \Rightarrow n-\frac{n_{i}^2}{n}-N_{D}=0$$Risolvendo per n, e con un $N_{D}$ sufficientemente grande, si ottiene che
$$n\approx N_{D}$$
$$p \approx \frac{n_{i}^2}{N_{D}}$$

Facendo il ragionamento contrario, per un **semiconduttore drogato di tipo p** con $N_{A} \gg n_{i}$
si ottiene
$$p\approx N_{A}$$
$$n\approx \frac{n_{i}^2}{N_{A}}$$

È possibile drogare un semiconduttore con elementi di tipo p e di tipo n insieme. 
In tal caso si avranno **portatori maggioritari e minoritari** a seconda della quantità.
*Ad esempio se $N_{D} > N_{A}$ si considera semplicemente il materiale come drogato di tipo n con $N_{D}'=N_{D}-N_{A}$.*

---

In un semiconduttore in **equilibrio** gli elettroni liberi si muovono in maniera casuale in ogni direzione. Lo **spostamento medio è nullo**.
In presenza di un **campo elettrico**, si aggiunge al movimento casuale una **forza elettrica** che spinge gli elettroni in direzione opposta al campo e le lacune in direzione del campo.

Gli elettroni si spostano con velocità  $v_{n} = -\mu_{n}E$
Le lacune si spostano con velocità $v_{p} = \mu_{p}E$
In cui le due costanti di proporzionalità sono dette **mobilità** (maggiore di circa 3 volte per gli elettroni).

Consideriamo un conduttore di area "A" e lunghezza "dx".
Il numero di portatori che attraversano tale sezione è 
$$n\cdot A\cdot dx$$$$p\cdot A\cdot dx$$
Da cui le due correnti di elettroni e lacune valgono
$$I_{n}=\frac{-q\cdot n\cdot A\cdot dx}{dt} = -q\cdot n\cdot A\cdot v_{n}$$
$$I_{p}=\frac{q\cdot p\cdot A\cdot dx}{dt} = q\cdot p\cdot A\cdot v_{p}$$
Ricaviamo le densità dividendo per l'area:
$$J_{n} = -q\cdot n\cdot v_{n}=q\cdot n\cdot\mu_{n}E$$
$$J_{p} = q\cdot p\cdot v_{p}=q\cdot p\cdot\mu_{p}E$$
Definiamo quindi **corrente di deriva** la grandezza
$$J_{drift}=q(n\mu_{n}+p\mu_{p})E$$

Dalla corrente di deriva possiamo calcolare la **resistività** del semiconduttore:
$$\rho=\frac{E}{J_{drift}}=\frac{1}{q(\mu_{n}n+\mu_{p}p)}$$
