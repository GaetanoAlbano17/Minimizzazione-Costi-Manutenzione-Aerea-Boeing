# TRACCIA:
![Traccia file]([(https://github.com/GaetanoAlbano17/Minimizzazione-Costi-Manutenzione-Aerea-Boeing/blob/main/Traccia_Progetto_Boeing.pdf])


# Minimizzazione-Costi-Manutenzione-Aerea-Boeing
Progetto per l'esame di 'Modelli e Metodi di Ottimizzazione e Statistica'
# SOLUZIONE
Il progetto riguarda la localizzazione ottimale di centri di manutenzione aerea nell’area euro-asiatica per l’azienda Boeing.
La traccia del problema fornisce informazioni sulla distribuzione geografica degli aeroporti principali e sul numero atteso di aeromobili che richiederanno manutenzione presso ciascun aeroporto.
L’obiettivo è quello di minimizzare i costi complessivi, considerando il costo di costruzione dei centri e il costo di servizio.
Nel seguito del progetto verranno descritti indici, parametri, variabili, vincoli e funzione obiettivo del modello matematico, e, inoltre, verrà ricercata una soluzione ottimale utilizzando il mezzo Risolutore di Excel.
Per risolvere il seguente problema, innanzitutto definiamo il numero dei centri di servizio e di aeroporti. Useremo ‘i’ e ‘j’ come indici per il problema:
## Indici
𝑖≤𝑛=𝑁𝑢𝑚𝑒𝑟𝑜 𝑑𝑒𝑖 𝑐𝑒𝑛𝑡𝑟𝑖 𝑑𝑖 𝑠𝑒𝑟𝑣𝑖𝑧𝑖𝑜 (𝑑𝑎 1 𝑎 5)

𝑗≤𝑚=𝑁𝑢𝑚𝑒𝑟𝑜 𝑑𝑖 𝑎𝑒𝑟𝑜𝑝𝑜𝑟𝑡𝑖 (𝑑𝑎 1 𝑎 12)

## Parametri del problema

Definiamo adesso i parametri fondamentali per lo sviluppo del problema, a partire da latitudine e longitudine dell’aeroporto j, il raggio terrestre, il numero atteso di aviogetti/anno dall’aeroporto j, la costante di proporzionalità tra distanza e costo, i costi delle costruzioni nell’area Europea o Asiatica e la capienza dei centri.

- 𝛿𝑗: rappresenta la latitudine dell’aeroporto j
La latitudine è una coordinata geografica che indica la distanza di un punto dalla linea dell’equatore, misurata in gradi. Questo parametro è utilizzato per calcolare la distanza geodetica tra un centro di servizio ed un aeroporto.

- φj: rappresenta la longitudine dell’aeroporto j
La longitudine è una coordinata geografica che indica la posizione est-ovest di un punto rispetto al meridiano di riferimento, solitamente tra il meridiano di Greenwich. Utilizziamo questo parametro per calcolare la distanza geodetica tra un centro di servizio e un aeroporto.

- r: rappresenta il raggio terrestre
Questo parametro indica la lunghezza approssimativa del raggio della Terra ed è utilizzato nella formula per calcolare la distanza geodetica tra i centri di servizio e gli aeroporti.
Nel nostro problema, r = 6371 Km

- 𝐴𝑗: rappresenta numero atteso di aviogetti/anno dall’aeroporto j
Questo parametro indica il numero di aviogetti previsti per essere serviti da un determinato aeroporto durante un anno. Viene utilizzato nei vincoli che regolano la manutenzione sugli aviogetti.

- α: rappresenta la costante di proporzionalità (euro/km)
Questo parametro indica la relazione tra la distanza geodetica tra un centro di servizio e un aeroporto ed il costo associato a quella distanza. È utilizzato nella funzione obiettivo al fine di calcolare i costi totali dell’operazione.
Nel nostro caso α = 50 euro/Km

- 𝐶1: rappresenta il costo di costruzione tra 20◦W e 40◦E (area europea)
Questo parametro indica il costo associato alla costruzione di un centro di servizio nell’area europea. È utilizzato nella funzione obiettivo per calcolare i costi totali dell’operazione.
Nel nostro caso 𝐶1=300 𝑚𝑖𝑙𝑖𝑜𝑛𝑖 𝑑𝑖 𝑒𝑢𝑟𝑜.

- 𝐶2: rappresenta il costo di costruzione tra 40◦E e 160◦E (area asiatica)
Questo indica il costo associato alla costruzione di un centro di servizio nell’area asiatica. È utilizzato nella funzione obiettivo per calcolare i costi totali dell’operazione.
Nel nostro caso 𝐶2=150 𝑚𝑖𝑙𝑖𝑜𝑛𝑖 𝑑𝑖 𝑒𝑢𝑟𝑜.

- P: rappresenta la capienza dei centri (rappresentata in numero di aviogetti)
Questo parametro limita la somma dei flussi di aviogetti da tutti gli aeroporti verso un centro di servizio. È utilizzato come vincolo per assicurare che un centro non superi la sua massima capacità.
Nel nostro caso, P = 60.

## Variabili del problema
Ora definiamo le variabili del problema, fondamentali per la risoluzione, lo studio dei vincoli successivo e la descrizione della funzione obiettivo.
Avremo variabili dedicate a latitudine e longitudine, al numero di aviogetti per i centri e per gli aeroporti, alla distanza geodetica tra centri e aeroporti, e, infine, alla variabile ‘z’ destinata al capire in quali condizioni di costruzioni siamo (quindi in quale area geografica).

𝑥𝑖: rappresenta la variabile utilizzata per la latitudine del centro i (90◦S ≤ 𝑥𝑖≤ 90◦N), quindi (-90◦ ≤ 𝑥𝑖<=90°);

𝑦𝑖: rappresenta la variabile utilizzata per la longitudine del centro i (20◦W ≤ 𝑦𝑖≤ 160◦E), quindi (-20° <= 𝑦𝑖<= 160°);

𝑤𝑖𝑗: rappresenta il numero di aviogetti destinati al centro i e provenienti dall’aeroporto j (0 ≤ 𝑤𝑖𝑗 ≤ 𝐴𝑗);

𝑑𝑖𝑗: distanza geodetica tra il centro i e l’aeroporto j (𝑑𝑖𝑗≥ 0);

𝑧𝑖 che vale 1 se il centro i è costruito tra 20◦W e 40◦E, 0 altrimenti.

## Funzione obiettivo
Importante, successivamente, è formulare la funzione obiettivo, decisiva nell’intento di decidere dove localizzare i centri di manutenzione minimizzando i costi dell’operazione.
La funzione obiettivo suddetta, è incentrata su un problema di minimizzazione.

min Σ(𝐶1∗𝑧𝑖+𝐶2∗(1−𝑧𝑖)+ α∗Σ𝑤𝑖𝑗∗𝑑𝑖𝑗)𝑗≤𝑚𝑖≤𝑛

Quindi, sostituendo i valori noti:

min Σ(300∗𝑧𝑖+150∗(1−𝑧𝑖)+ 50∗Σ𝑤𝑖𝑗∗𝑑𝑖𝑗)𝑗≤𝑚𝑖≤𝑛

La funzione obiettivo è una funzione di minimizzazione che combina i costi di costruzione dei centri di servizio, il costo di servizio (dipendente dalla distanza) e il flusso di aviogetti tra centri e aeroporti. L’obiettivo è quello di minimizzare i costi totali dell’operazione, considerando sia costi di costruzioni che costi di servizio.

## Vincoli progetto:
Importante è successivamente la parte dedicata ai vincoli di progetto, per gestire le varie situazioni e richieste del progetto.
I vincoli a cui tener conto per sviluppare il progetto sono legati alle distanze, alla capienza dei centri, alla manutenzione sugli aviogetti, al definire z. Poi, è importante tener conto dei domini delle variabili.

#### Vincolo sulle distanze
𝑑𝑖𝑗=2𝑟∗asin√sin2(𝑥𝑖− 𝛿𝑗2)+cos𝑥𝑖∗cos𝛿𝑗∗sin2(𝛾𝑖− 𝜑𝑗2) ,∀ i≤n,∀ j≤m
Il vincolo sulle distanze rappresenta la formula per calcolare la distanza geodetica tra centro di servizio i e aeroporto j. La formula utilizza latitudine, definita come x, e longitudine, definita come y, per calcolare la distanza sulla superficie terrestre utilizzando la formula definita nella traccia del problema.

#### Vincolo sulla capienza dei centri
Σ𝑤𝑖𝑗≤𝑃 ∀𝑖≤𝑛𝑗 ≤ 𝑚

Quindi:

Σ𝑤𝑖𝑗≤60 ∀𝑖≤𝑛𝑗 ≤ 𝑚

Il vincolo suddetto impone che la somma di tutti i flussi di aviogetti da tutti gli aeroporti al centro di servizio non debbano superare la capienza massima del centro. L’obiettivo è quello che non arrivino più aviogetti di quelli gestibili.

#### Vincolo sulla manutenzione sugli aviogetti
Σ𝑤𝑖𝑗=𝐴𝑗 ∀𝑗≤𝑚𝑖≤ 𝑛

Questo vincolo impone che la somma di tutti i flussi di aviogetti da tutti gli aeroporti al centro di servizio sia uguale al numero atteso di aviogetti da servire nell’aeroporto.
𝐴𝑗, da problema, rappresenta il numero di aviogetti dei vari aeroporti j.
Viene garantito, grazie a ciò, che tutti gli aviogetti provenienti da un certo aeroporto ricevano la manutenzione necessaria.

#### Vincolo sulla variabile z
𝑦𝑖−40°≤360°∗ 𝑧𝑖 ∀𝑖≤𝑛 𝑦𝑖−40°≥−360°∗(1− 𝑧𝑖) ∀𝑖≤𝑛

Questo vincolo definisce la variabile z come una variabile binaria, fondamentale nell’indicare se il centro di servizio sia costruito nell’area europea (tra 20°W e 40°E) o nell’area asiatica (tra 40°E e 160°E).

Il primo vincolo afferma che se 𝑧𝑖 è uguale a 1 (quindi il centro è costruito nell’area europea), allora la longitudine 𝑦𝑖 deve essere maggiore o uguale a 40°.

Il secondo vincolo afferma che se 𝑧𝑖 è uguale a 0 (il centro è costruito nell’area asiatica), allora la longitudine 𝑦𝑖 deve essere maggiore o uguale a -320°.
In questo modo i vincoli assicurano che i centri di manutenzione vengano correttamente localizzati nelle rispettive aree geografiche.
𝑦𝑖−40 rappresenta la differenza tra la longitudine del centro e il valore di riferimento (40°) che corrisponde al limite tra l’area europea e l’area asiatica.
Vediamo 360° che rappresenta l’intervallo completo di un cerchio in gradi. La longitudine tra due punti è espressa in gradi ed un giro completo intorno alla terra corrisponde a 360 gradi.

## Domini delle variabili
𝑥𝑖∈[−90,90]

yi∈[−20,160]

𝑑𝑖𝑗≥0

0≤𝑤𝑖𝑗 ≤𝐴𝑗 ∀ 𝑖≤𝑛,𝑗≤𝑚,𝑤𝑖𝑗 𝑖𝑛𝑡𝑒𝑟𝑜

𝑧𝑖∈{0,1} ∀ 𝑖≤𝑛

Per affrontare al meglio il problema, ho deciso di utilizzare Excel, in modo da risolvere il problema di ottimizzazione con lo strumento Risolutore.
Dopo aver affrontato il problema in maniera scritta per derivare dal testo i vari possibili parametri e vincoli del problema, ho innanzitutto riportato i dati del problema (messi in tabella nelle varie colonne dedicate ad Aeroporto, Latitudine, Longitudine e numero di aviogetti annuo) sul foglio di calcolo. Per la latitudine Sud e longitudine Ovest ho posto valori negativi, anche se, ovviamente, per le funzioni seno e coseno (rispettivamente dispari e pari) non sarebbe cambiato niente.

Posti valori inizialmente casuali sulle variabili da trovare, ho innanzitutto dato valori possibili alle latitudini e longitudine dei centri. È stato poi fondamentale ricavare i valori delle distanze geodetiche tra i centri ‘i’ e gli aeroporti ‘j’.
Per il calcolo della distanza geodetica sulle celle ho utilizzato funzioni trigonometriche presenti in Excel, basandomi sulla formula precedentemente definita: 𝑑𝑖𝑗=2𝑟∗asin√sin2(𝑥𝑖− 𝛿𝑗2)+cos𝑥𝑖∗cos𝛿𝑗∗sin2(𝛾𝑖− 𝜑𝑗2) Ovviamente, ho svolto lo stesso calcolo per ogni 𝑑𝑖𝑗(centri ‘i’ da 1 a 5, Aeroporti ‘j’ da 1 a 12).

Per il vincolo sulla capienza dei centri, ho posto minore di 60 la somma, per ogni centro, di tutti gli aviogetti provenienti dagli aeroporti j.

Successivamente, ho posto poi anche un vincolo dedicato alla manutenzione degli aviogetti, in previsione che la somma degli aviogetti per ogni centro fosse uguale al numero di aviogetti, dati da testo, per ogni aeroporto.
Una tabella, inoltre, è stata destinata al vincolo per z, in cui abbiamo posto le due condizioni precedenti: 𝑦𝑖−40°≤360°∗ 𝑧𝑖 ∀𝑖≤𝑛

𝑦𝑖−40°≥−360°∗(1− 𝑧𝑖) ∀𝑖≤𝑛

Inoltre, nella tabella delle variabili, imponiamo che, se parliamo di un centro costruito nell’area europea, z varrà 1, altrimenti, d’altro caso, sarà uguale a 0.

Viene infatti inserita nella cella dedicata alle 𝑧𝑖 una condizione in cui se ci trova tra i -20° e 40° si parla di centro in Europa, altrimenti in Asia.
Fondamentale, infine, la funzione obiettivo, che andremo a minimizzare.

La formula generale per la cella che ho utilizzato è stata: =SOMMA(E19*B148;E19*B149;E19*B150;E19*B151;E19*B152;F19*(1-B148);F19*(1-B149);F19*(1-B150);F19*(1-B151);F19*(1-B152);G19*SOMMA(MATR.SOMMA.PRODOTTO(B28:B39;B88:B99);MATR.SOMMA.PRODOTTO(B40:B51;B100:B111);MATR.SOMMA.PRODOTTO(B52:B63;B112:B123);MATR.SOMMA.PRODOTTO(B64:B75;B124:B135);MATR.SOMMA.PRODOTTO(B76:B87;B136:B147))) (ovviamente si poteva abbreviare e rendere più semplice)

Da qui, utilizzando il Risolutore, ho posto i vari vincoli definiti da problema, definendo i vari domini di applicazione, ottenendo questi risultati:

È stata ottenuta una soluzione ottimale, con una funzione obiettivo di valore 1050 (mln di euro).

Dal risolutore, 3 posizioni dedicate ai centri sono state identificate in Asia, considerando anche i costi rispetto all’Europa (150 mln contro i 300 mln europei).

Sono stati individuati due centri di manutenzione in Europa, probabilmente in considerazione dei clienti Boeing in quell’area, nonostante il costo più elevato.
È stato quindi trovato un buon compromesso tra i costi di costruzione dei centri ed i costi di servizio legati alle distanze geodetiche tra gli aeroporti e i centri.
Sono state determinate le coordinate di latitudine e longitudine dei centri di manutenzione, le assegnazioni dei flussi di aviogetti tra gli aeroporti e i centri, ed anche lo stato di costruzione dei centri in base all’area geografica.

Le decisioni prese sulla localizzazione dei centri di manutenzione si basano sulle informazioni fornite nella traccia, come i costi di costruzione differenziati tra l’area europea e quella asiatica, il numero atteso di aviogetti per gli aeroporti e la distanza geodetica come metrica di costo di servizio.

I risultati ottenuti forniscono una base solida per la decisione sulla localizzazione dei centri di manutenzione, consentendo di massimizzare l’efficienza operativa e minimizzare i costi complessivi.
La soluzione considera in modo accurato le distanze geodetiche e tiene conto delle specifiche esigenze dei clienti di Boeing.

È importante tenere a mente del fatto che i risultati ottenuti dipendono dalle condizioni iniziali, dai vincoli e dalla formulazione. Nel complesso, la soluzione ottenuta fornisce una guida per la
decisione sulla localizzazione dei centri di manutenzione aerea, consentendo di prendere decisioni informate e strategiche per garantire un servizio di manutenzione efficiente ed economicamente vantaggioso.
