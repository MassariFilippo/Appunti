<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });</script>

# Crittografia

<div style="page-break-after: always;"></div>

- [Crittografia](#crittografia)
  - [Introduzione alla Crittografia](#introduzione-alla-crittografia)
    - [Dilemma Etico](#dilemma-etico)
    - [Crittologia](#crittologia)
    - [Cifratura e Decifratura](#cifratura-e-decifratura)
    - [Ruolo del Crittoanalista](#ruolo-del-crittoanalista)
    - [Tipologie di Cifrari](#tipologie-di-cifrari)
      - [Cifrari per Uso Ristretto](#cifrari-per-uso-ristretto)
      - [Cifrari per Uso Generale](#cifrari-per-uso-generale)
      - [Cifrari a Chiave Segreta o Simmetrici](#cifrari-a-chiave-segreta-o-simmetrici)
      - [Spazio delle Chiavi e Attacchi Esaustivi](#spazio-delle-chiavi-e-attacchi-esaustivi)
    - [La Chiave Pubblica](#la-chiave-pubblica)
      - [Funzionamento della Chiave Pubblica](#funzionamento-della-chiave-pubblica)
    - [Funzioni One-Way con Trap-Door](#funzioni-one-way-con-trap-door)
      - [Esempio di Funzione One-Way](#esempio-di-funzione-one-way)
    - [Applicazioni della Crittografia](#applicazioni-della-crittografia)
  - [Complessità computazionale](#complessità-computazionale)
    - [Tabella delle cifre di alcune funzioni](#tabella-delle-cifre-di-alcune-funzioni)
    - [Facile vs Difficile](#facile-vs-difficile)
  - [Cifrari e sicurezza](#cifrari-e-sicurezza)
    - [Modello Matematico della Crittografia](#modello-matematico-della-crittografia)
  - [Cifrario Perfetto (Shannon)](#cifrario-perfetto-shannon)
    - [Dimostrazione del numero minimo di chiavi in un cifrario perfetto](#dimostrazione-del-numero-minimo-di-chiavi-in-un-cifrario-perfetto)
    - [One-Time Pad](#one-time-pad)
      - [Funzionamento:](#funzionamento)
      - [Esempio](#esempio)
      - [Dimostrazione della Perfezione del One-Time Pad](#dimostrazione-della-perfezione-del-one-time-pad)
      - [Minimalità dell’insieme delle chiavi](#minimalità-dellinsieme-delle-chiavi)
      - [Limiti del One-Time Pad](#limiti-del-one-time-pad)


<div style="page-break-after: always;"></div>

## Introduzione alla Crittografia
- **Definizione**: La crittografia è l'arte della "scrittura nascosta", utilizzata per proteggere le comunicazioni.
- **Contesto**: Esistono due gruppi opposti: chi desidera comunicare in privato e chi cerca di intercettare queste comunicazioni, sia per curiosità, investigazione legittima, o scopi malevoli.

### Dilemma Etico
- **Buoni vs Cattivi**: La distinzione tra chi è "buono" e chi è "cattivo" è complessa e dipende dal contesto. Chi cifra le comunicazioni può essere visto come buono, ma anche chi cerca di intercettarle può avere motivazioni legittime.

### Crittologia
- **Definizione**: La crittologia comprende sia la crittografia (cifratura) che la crittoanalisi (decifratura).
- **Obiettivo**: Proteggere la comunicazione tra un mittente (Mitt) e un destinatario (Dest) su un canale insicuro.

### Cifratura e Decifratura
- **Processo**: 
  - Cifratura: Trasformazione di un messaggio in chiaro (m) in un crittogramma (c) tramite una funzione C.
  - Decifratura: Recupero del messaggio originale (m) dal crittogramma (c) tramite una funzione D.
- **Relazione**: D(C(m)) = m; C e D sono funzioni inverse.
- Si deduce che C debba essere iniettiva.

### Ruolo del Crittoanalista
- **Obiettivi**: Il crittoanalista può cercare di scoprire, alterare o disturbare la comunicazione.
- **Tipi di Attacchi**:
  - **Cipher Text Attack**: Analisi di crittogrammi noti.
  - **Known Plain-Text Attack**: Conoscenza di coppie di messaggi in chiaro e crittogrammi.
  - **Chosen Plain-Text Attack**: Scelta di messaggi in chiaro da cifrare.
  - **Man in-the-middle Attack**: Intercettazione e modifica dei messaggi tra due utenti.

### Tipologie di Cifrari
La crittografia si divide in diverse categorie a seconda dell'uso e della segretezza delle funzioni di cifratura e decifratura. Le principali tipologie di cifrari sono:

#### Cifrari per Uso Ristretto
Questi cifrari sono utilizzati in contesti sensibili, come le comunicazioni diplomatiche o militari. In questo caso, sia le funzioni di cifratura (C) che di decifratura (D) sono mantenute segrete in ogni loro aspetto. Questo approccio garantisce un alto livello di sicurezza, poiché solo le parti autorizzate conoscono i metodi utilizzati per proteggere le informazioni.

#### Cifrari per Uso Generale
A differenza dei cifrari per uso ristretto, in quelli per uso generale le funzioni di cifratura e decifratura sono pubblicamente note. In questo scenario, viene utilizzata una chiave segreta (k) diversa per ogni coppia di utenti. La chiave è inserita come parametro nelle funzioni C e D. Anche se un intruso conosce le funzioni e ha accesso a un crittogramma (c) carpito su un canale insicuro, non può estrarre informazioni utili sul messaggio originale (m) senza conoscere la chiave segreta.

#### Cifrari a Chiave Segreta o Simmetrici
Nei cifrari a chiave segreta, la cifratura e la decifratura avvengono tramite le funzioni:
- C(m; k) per la cifratura
- D(c; k) per la decifratura

È necessario un canale sicuro per lo scambio della chiave. Mantenere segreta la chiave è più semplice rispetto a mantenere segreto l'intero processo di cifratura e decifratura. Tutti gli utenti possono utilizzare le funzioni pubbliche C e D, a condizione di scegliere chiavi diverse. Se un crittoanalista riesce a ottenere una chiave, è sufficiente generarne una nuova per mantenere la sicurezza delle comunicazioni.

#### Spazio delle Chiavi e Attacchi Esaustivi
Lo spazio delle chiavi (KEY) deve essere ampio per garantire la sicurezza. Se il crittoanalista conosce o può indovinare lo spazio delle chiavi, può tentare un attacco esaustivo, verificando ogni possibile chiave k per decifrare il messaggio.

### La Chiave Pubblica
Nel 1976, la crittografia ha subito una svolta significativa con l'introduzione della crittografia a chiave pubblica da parte di Diffie e Hellman, e indipendentemente da Merkle. Questo sistema elimina la necessità di condividere una chiave segreta tra mittente e destinatario.

#### Funzionamento della Chiave Pubblica
Nella crittografia a chiave segreta, due utenti utilizzano la stessa chiave (k) per cifrare e decifrare i messaggi. Al contrario, nella crittografia a chiave pubblica, si utilizzano due chiavi diverse: 
- k[pub] per la cifratura (pubblica e nota a tutti)
- k[prv] per la decifratura (privata e nota solo al destinatario)

Le funzioni C e D sono di pubblico dominio e identiche per tutti gli utenti. Questo rende la cifratura accessibile a chiunque, mentre la decifratura è riservata a chi possiede la chiave privata. I sistemi a chiave pubblica sono definiti asimmetrici, mentre quelli a chiave segreta sono simmetrici.

### Funzioni One-Way con Trap-Door
In un sistema a chiave pubblica, la funzione di cifratura C deve avere una proprietà nota come "one-way con trap-door". Questo significa che calcolare C per cifrare un messaggio deve essere facile, mentre calcolare D per decifrare deve essere difficile, a meno che non si conosca un meccanismo segreto (trap-door) che semplifichi il calcolo.

#### Esempio di Funzione One-Way
Un esempio classico è il prodotto di due numeri primi p e q. Calcolare il loro prodotto n è semplice, ma fattorizzare n per ottenere p e q è difficile, a meno che non si conosca uno dei due numeri.

### Applicazioni della Crittografia
La segretezza delle comunicazioni è fondamentale, ma non è l'unica caratteristica richiesta ai sistemi crittografici moderni. Tre requisiti importanti nelle applicazioni su rete sono:

1. **Identificazione**: Permette al sistema di verificare l'identità di chi richiede accesso ai suoi servizi.
2. **Autenticazione**: Consente al destinatario di accertare che un messaggio sia stato effettivamente inviato dal mittente e che non sia stato modificato durante la trasmissione.
3. **Firma Digitale**: Garantisce che il mittente non possa negare la paternità di un messaggio inviato, permettendo al destinatario di dimostrare a terzi che il messaggio è stato effettivamente inviato.

## Complessità computazionale

### Tabella delle cifre di alcune funzioni
| n        | log2(n) | n  | n^2  | n^5  | 2^n       | n!          |
|----------|---------|----|------|------|-----------|-------------|
| 1        | 1       | 1  | 1    | 1    | 1         | 1           |
| 100,000  | 2       | 6  | 11   | 26   |  30 103   | 500 001     |
| 500,000  | 2       | 6  | 12   | 29   |  150 515  | 2 849486    |
| 1,000,000| 2       | 7  | 13   | 31   | 301 030   | 6 000 001   |

- Prima colonna valore dell'input altre colonne numero di cifre per rappresentare l'output.

| n    | log2(n) | n   | n^2       | n^5          | 2^n       |
|------|---------|-----|-----------|--------------|-----------|
| 10   | 3       | 10  | 100       | 100,000      | 1,024     |
| 100  | 6       | 100 | 10,000    | 10^10        | x         |
| 1000 | 9       | 1000| 1,000,000 | 10^15        | y         |

Dove:
- x = 1.2676506002282294 × 10^30
- y = 1.0715086071862673 × 10^300

- Prima colonna lunghezza dell'input altre colonne passi per arrivare all'output.

Secondo alcune stime, il Sole si spegnerà tra 4 miliardi di anni, ovvero tra 1.26 × 10^23 microsecondi.

- **Fattorizzazione di numeri**
  - **Input**: $n = p_1^{k_1} \cdot \ldots \cdot p_m^{k_m}$
  - **Output**: $p_1, k_1, \ldots, p_m, k_m$
  - Numero di cifre di n in base b: $\log_b(n)$
  - Miglior algoritmo noto: **$T(n) = e^{\left( \frac{64}{9} \right)^{1/3} \cdot (\ln(n) \cdot \ln(\ln(n)))^{2/3}}$**
  - Se n ha 3000 cifre binarie, **$T(n) \approx 9.31 \times 10^{50}$**, un tempo inaccettabile con la tecnologia attuale.

- **Elevamento a potenza e Logaritmo**
  - **Elevamento a potenza**: dati $b$ e $c$, calcolare $a = b^c$.
  - **Logaritmo**: dati $a$ e $b$, calcolare $c$ tale che $a = b^c$.
  - Nei numeri reali, il logaritmo è facile da calcolare.
  - Sia $p$ un numero primo.
  - $Z_p = \{1, \ldots, p-1\}$ è il gruppo degli interi modulo $p$ con moltiplicazione.
  - Dati $a, b, c \in Z_p$:
    - $a = b^c \mod p$ (facile)
    - Dato $a$ e $b$, trovare $c$ è difficile.
  
  **Esempio:**
  - $p = 17$
  - $Z_{17} = \{1, \ldots, 16\}$
  - $13 = 3^4 \mod 17$ (facile)
  - Dato $13$ e $3$, trovare $4$ è difficile (logaritmo discreto).

### Facile vs Difficile
- **Facile**: problemi risolvibili in tempo polinomiale.
- **Difficile**: problemi che richiedono tempo esponenziale e per cui non si conoscono algoritmi polinomiali.
- **Impossibile**: problemi senza soluzione algoritmica.

Alcune equazioni, come le **equazioni diofantee**, non hanno algoritmi risolutivi.
Esempio:
$$3x^2 - 7y^2 - z^3 = 18$$
$$7y^2 + 8z^2 = 0$$
Non esiste un algoritmo generale per risolvere queste equazioni per numeri interi.

## Cifrari e sicurezza

Esistono cifrari che offrono sicurezza assoluta, ma il loro costo è proibitivo, limitandone l'uso a comunicazioni estremamente riservate detti **cifrari inviolabili**. Mentre i **cifrari pratici** sono cifrari non perfetti, ma sufficientemente sicuri ed efficienti, vengono impiegati nelle comunicazioni quotidiane.

### Modello Matematico della Crittografia
La comunicazione tra Mitt (mittente) e Dest (destinatario) è modellata come un processo stocastico:
- $M$ è una variabile aleatoria che rappresenta il messaggio inviato.
- $C$ è la variabile aleatoria che rappresenta il crittogramma trasmesso.
- $Pr(M = m)$ indica la probabilità che venga inviato il messaggio $m$.
- $Pr(M = m | C = c)$ rappresenta la probabilità a posteriori che $m$ sia stato inviato dato il crittogramma $c$.
- **Scenario peggiore**: Il crittoanalista che ha intercettato c è in possesso di tutta l’informazione possibile sul sistema tranne la chiave
segreta. In particolare egli conosce la distribuzione di probabilità con cui Mitt genera i messaggi, il cifrario utilizzato e lo spazio Key delle chiavi.

## Cifrario Perfetto (Shannon)
Un cifrario è perfetto se: $$Pr(M = m | C = c) = Pr(M = m)$$. Questo implica che osservare $C$ non fornisce alcuna informazione su $M$. Ne risulta che il numero di chiavi $N_k$ deve essere almeno pari al numero di messaggi $N_m$: Se $N_m > N_k$, esiste almeno un messaggio $m$ che non può essere ottenuto, violando la perfezione del cifrario.

### Dimostrazione del numero minimo di chiavi in un cifrario perfetto  

Consideriamo un sistema crittografico in cui:  
- **Nm** è il numero totale di messaggi possibili, ovvero quelli per cui la probabilità di essere inviati non è nulla: $Pr(M = m) > 0$.  
- **Nk** è il numero totale di chiavi disponibili nel sistema.  

- **Assunzione per assurdo**
Supponiamo, per assurdo, che il numero di messaggi sia maggiore del numero di chiavi:  
$$
Nm > Nk
$$  
Questo significa che abbiamo più messaggi possibili di quanti siano gli elementi nello spazio delle chiavi segrete.  

- **Analisi della decifrabilità**
Quando un crittogramma $c$ viene intercettato, sappiamo che esso può essere stato generato cifrando diversi messaggi con le diverse chiavi. Se abbiamo **Nk** chiavi, allora il numero massimo di messaggi che possiamo ottenere decifrando $c$ con tutte le chiavi possibili è al massimo **Nk**.  

Tuttavia, poiché abbiamo assunto che **Nm > Nk**, questo significa che esistono più messaggi possibili di quanti ne possiamo effettivamente ottenere dalla decifratura di qualsiasi crittogramma.  

- **Contraddizione** 
Dato che **Nk** è minore di **Nm**, esisterà almeno un messaggio $m$ tale che **non** può essere ottenuto a partire da un dato crittogramma $c$. In termini matematici, significa che la probabilità condizionata di $m$ dato $c$ è nulla:  
$$
Pr(M = m | C = c) = 0
$$  
Ma, per definizione di un **cifrario perfetto**, la probabilità condizionata $Pr(M = m | C = c)$ deve essere esattamente uguale alla probabilità a priori $Pr(M = m)$, ovvero la conoscenza del crittogramma **non** deve alterare la probabilità di ogni messaggio.  

Dal momento che abbiamo trovato un caso in cui questa proprietà non vale, abbiamo raggiunto una contraddizione.  

- **Conclusione** 
Poiché l’assunzione $Nm > Nk$ porta a una contraddizione con la definizione di cifrario perfetto, ne segue che per avere un cifrario perfetto dobbiamo avere almeno altrettante chiavi quanti sono i messaggi possibili:  
$$
Nk \geq Nm
$$  
Questo risultato dimostra che, in un cifrario perfetto, lo spazio delle chiavi deve essere **almeno grande quanto** lo spazio dei messaggi, rendendo il suo utilizzo pratico estremamente oneroso in termini di gestione delle chiavi.

### One-Time Pad
Un cifrario perfetto ideato da Mauborgne e Vernam nel 1917, usato in comunicazioni segrete.

#### Funzionamento:
- **Generazione della chiave**: una sequenza casuale $k$ lunga almeno quanto il messaggio.
- **Cifratura**: $c_i = m_i \oplus k_i$ per ogni bit $i$.
- **Decifratura**: $m_i = c_i \oplus k_i$, poiché $k_i \oplus k_i = 0$.

#### Esempio
| msg  | 0 | 1 | 1 | 0 | 0 | 1 |
|------|---|---|---|---|---|---|
| key  | 1 | 1 | 0 | 1 | 0 | 1 |
| c    | 1 | 0 | 1 | 1 | 0 | 0 |
| key  | 1 | 1 | 0 | 1 | 0 | 1 |
| msg  | 0 | 1 | 1 | 0 | 0 | 1 |

#### Dimostrazione della Perfezione del One-Time Pad

- **Assunzioni**  
Per semplificare l’analisi, assumiamo che:  
- Tutti i messaggi abbiano la stessa lunghezza $n$ bit.  
- Tutte le possibili sequenze di $n$ bit siano messaggi validi.  

Il **One-Time Pad** è un sistema crittografico che utilizza una chiave generata in modo completamente casuale, lunga quanto il messaggio, e usata una sola volta. Dimostreremo che è un **cifrario perfetto**, ovvero soddisfa la proprietà:  

$$
Pr(M = m \mid C = c) = Pr(M = m)
$$  

che implica che la conoscenza del crittogramma **non fornisce alcuna informazione** sul messaggio originale.  

- **Espansione della probabilità condizionata**  
Utilizziamo la definizione di probabilità condizionata per riscrivere l’uguaglianza da dimostrare:  

$$
Pr(M = m \mid C = c) = \frac{Pr(M = m, C = c)}{Pr(C = c)}
$$  

dove $Pr(M = m, C = c)$ è la probabilità che il messaggio sia $m$ e il crittogramma sia $c$, mentre $Pr(C = c)$ è la probabilità che il crittogramma assuma il valore $c$.  

- **Probabilità congiunta $Pr(M = m, C = c)$**
L’evento $\{ M = m, C = c \}$ descrive la situazione in cui l’utente mittente ha scelto il messaggio $m$ e lo ha cifrato ottenendo $c$.  

Nel One-Time Pad, la cifratura è definita come:  
$$
C = M \oplus K
$$  
dove $K$ è una chiave segreta, generata in modo completamente casuale e lunga $n$ bit.  

Poiché il **XOR** ha la proprietà di essere una funzione **biunivoca**, ogni chiave diversa genera un crittogramma diverso per lo stesso messaggio. Dato che la chiave viene scelta in modo uniforme tra $2^n$ possibili valori, ogni chiave ha probabilità:  
$$
Pr(K = k) = \frac{1}{2^n}
$$  

Fissato un messaggio $m$, la probabilità di ottenere un determinato crittogramma $c$ è quindi anch’essa:  
$$
Pr(C = c) = \frac{1}{2^n}
$$  

e questa probabilità è **costante e indipendente da** $m$.  

- **Indipendenza tra $M$ e $C$**
  
Dal momento che ogni crittogramma è generato con probabilità costante indipendentemente dal messaggio, gli eventi $M = m$ e $C = c$ sono **statisticamente indipendenti**, quindi:  

$$
Pr(M = m, C = c) = Pr(M = m) \cdot Pr(C = c)
$$  

Sostituendo nella formula iniziale:  

$$
Pr(M = m \mid C = c) = \frac{Pr(M = m) \cdot Pr(C = c)}{Pr(C = c)}
$$  

semplificando $Pr(C = c)$, otteniamo:  

$$
Pr(M = m \mid C = c) = Pr(M = m)
$$  

che dimostra che il One-Time Pad è un **cifrario perfetto**, poiché il crittogramma non fornisce alcuna informazione sul messaggio originale.  

#### Minimalità dell’insieme delle chiavi

Affinché un cifrario sia perfetto, abbiamo visto nella dimostrazione precedente che il numero di chiavi deve essere **almeno pari al numero di messaggi possibili**.  

Nel caso del One-Time Pad:  
- Il numero di messaggi possibili di $n$ bit è $2^n$.  
- Il numero di chiavi possibili è anch’esso $2^n$.  

Poiché il numero di chiavi non può essere inferiore al numero di messaggi per mantenere la perfetta segretezza, e nel One-Time Pad è **esattamente** pari al numero di messaggi, possiamo concludere che il One-Time Pad utilizza il **numero minimo di chiavi necessario** per garantire la perfezione crittografica.

#### Limiti del One-Time Pad
- **Sicurezza massima**, ma **gestione complessa**.
- Le chiavi devono essere lunghe quanto il messaggio.
- Una chiave può essere usata **una sola volta** per mantenere la sicurezza.

