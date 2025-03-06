
### Vantaggi dei Protocolli a Chiave Pubblica

- Se gli utenti di un sistema sono n, il numero complessivo di chiavi (pubbliche e private) è 2n, anziché
  n(n - 1)/2.
- Non è richiesto alcuno scambio segreto di chiavi tra gli utenti, poiché la chiave pubblica è resa disponibile a tutti.

### Difetti dei Protocolli a Chiave Pubblica

- **Attacchi Chosen Plain-Text:**  
  Il sistema è esposto ad attacchi di tipo chosen plain-text in modo del tutto ovvio. Un crittoanalista può scegliere un numero qualsiasi di messaggi in chiaro, ad esempio:
  - $$ m_1, m_2, \dots, m_h $$
  
  e poi cifrarli utilizzando la funzione pubblica $$ C $$ e la chiave pubblica $$ k[pub] $$ di un destinatario (Dest), ottenendo così i crittogrammi:
  - $$ c_1, c_2, \dots, c_h $$
  
- **Osservazione del Canale:**  
  Spiando sul canale di comunicazione, il crittoanalista può confrontare qualsiasi messaggio cifrato $$ c $$ in transito verso Dest con i crittogrammi di cui è già in possesso.  
  - Se $$ c $$ coincide con uno dei crittogrammi precedentemente scelti e cifrati, il messaggio è automaticamente decifrato.
  - Se $$ c \neq c_i $$ per ogni i, il crittoanalista acquisisce comunque una conoscenza importante: sa che il messaggio $$ c $$ è diverso da quelli che ha scelto.
  
  Questo attacco è particolarmente pericoloso se il crittoanalista sospetta che Dest debba ricevere un messaggio particolare o se il messaggio in questione è breve e ha una struttura prevedibile (ad esempio, un indirizzo Internet o una password scelta ingenuamente).

- **Prestazioni:**  
  I sistemi a chiave pubblica sono molto più lenti di quelli basati su cifrari simmetrici.  
  Stime indicano che il loro rapporto di velocità può variare da due a tre ordini di grandezza.  
  Sebbene si possa obiettare che questo problema sia mitigato dalla crescita costante della potenza di calcolo, l'impatto è ancora significativo in contesti in cui la richiesta di comunicazioni sicure è in continuo aumento.

### Cifrario Proposto da Merkle

- Il primo cifrario asimmetrico, proposto da Merkle, basava la difficoltà di inversione della funzione $$ C $$ sulla risoluzione del problema dello zaino.  
- Benché tale problema sia NP-Hard, il cifrario fu violato per altre vie, evidenziando la delicatezza nel trattare il problema della sicurezza.  
- Successivi cifrari basati su questo problema sono invece rimasti inviolati.

### Cifrario RSA

Il secondo cifrario asimmetrico, proposto da Rivest, Shamir e Adleman (1978) e noto come RSA, fonda la sua sicurezza sulla difficoltà di fattorizzare grandi numeri interi.  
- **Considerazioni:**  
  - Sebbene la fattorizzazione non sia dimostrabilmente NP-Hard, e dunque teoricamente potenzialmente "più semplice" del problema dello zaino, RSA risulta sostanzialmente inviolabile se si usano chiavi sufficientemente lunghe.
  - È il cifrario asimmetrico di più largo impiego.

#### Cifrario RSA: Creazione delle Chiavi

Come possibile destinatario, ogni utente (Dest) esegue le seguenti operazioni:
1. Sceglie due numeri primi molto grandi, $$ p $$ e $$ q $$.
2. Calcola:
   - $$ n = p \cdot q $$
   - $$ \varphi(n) = (p - 1)(q - 1) $$
3. Sceglie un intero $$ e $$, minore di $$ \varphi(n) $$ e tale che $$ \gcd(e, \varphi(n)) = 1 $$.
4. Calcola l’intero $$ d $$ inverso di $$ e $$ modulo $$ \varphi(n) $$.
5. Rende pubblica la chiave $$ k[pub] = (e, n) $$ e mantiene segreta la chiave $$ k[prv] = d $$.

#### Cifrario RSA: Messaggio, Codifica e Decodifica

- **Codifica:**  
  Ogni messaggio viene codificato come una sequenza binaria, interpretata come un numero intero $$ m $$, dove $$ m < n $$. Se necessario, il messaggio viene diviso in blocchi.  
  La codifica avviene con:
  $$
  c = m^e \mod n
  $$
- **Decodifica:**  
  Il destinatario decifra il messaggio con:
  $$
  m = c^d \mod n
  $$

#### Cifrario RSA: Esempio

- Sia:  
  - $$ p = 5 $$, $$ q = 11 $$
  - $$ n = 55 $$, $$ \varphi(n) = 40 $$
- Scelto:
  - $$ e = 7 $$ (che è primo con 40)
  - $$ d = 23 $$ (poiché $$ 23 \cdot 7 \equiv 1 \mod 40 $$)
- Le chiavi sono:
  - $$ k[pub] = (7, 55) $$
  - $$ k[prv] = 23 $$
- Codifica:  
  $$ c = m^7 \mod 55 $$
- Decodifica:  
  $$ m = c^{23} \mod 55 $$

#### Cifrario RSA: Correttezza

Per qualunque intero $$ m < n $$ si ha:
$$
(m^e \mod n)^d \mod n = m
$$  
La dimostrazione si basa su:
- Se $$ p $$ e $$ q $$ non dividono $$ m $$, si usa il teorema di Eulero.
- Se uno dei due (ad esempio $$ p $$) divide $$ m $$ ma non l’altro, si dimostra che $m^e$ comunque, elevato alla potenza $$ d $$, restituisce $$ m $$ modulo entrambi e quindi modulo $$ n $$.
- Nota: $$ p $$ e $$ q $$ non possono entrambi dividere $$ m $$ perché altrimenti $$ m $$ sarebbe maggiore o uguale a $$ n $$, in contrasto con la condizione sui blocchi.

### Generazione di un Primo Grande

- **Distribuzione dei Numeri Primi:**  
  La probabilità che un numero casuale $n$ sia primo è approssimativamente:
  $$
  \Pr(n \text{ è primo}) \approx \frac{1}{\log n}
  $$
- **Idea:**  
  Si genera un numero $$ n $$ a caso e si verifica la sua primalità. Se è primo, si interrompe il processo; altrimenti, si ripete.

#### Test di Primalità

- Fino a qualche tempo fa non si conoscevano algoritmi efficienti.  
- Attualmente esistono algoritmi in tempo polinomiale (sebbene poco efficienti in pratica), come il test basato sul teorema di Fermat:
  $$
  a^{n-1} \mod n = 1 \quad \text{per } 0 < a < n \quad (\text{se } n \text{ è primo})
  $$
- **Test di Primalità Probabilistico:**  
  1. Genera un intero $a$ casuale tra 1 e $n-1$.
  2. Calcola $x = a^{n-1} \mod n$.
  3. Se $x = 1$, si dichiara che $n$ è prime; altrimenti, $n$ è composto.
  4. Iterare il test $k$ volte per ridurre la probabilità di errore.

### Come Generare $e$ e $d$

- **Scelta di $e$:**  
  Il numero $e$ deve essere scelto casualmente tale da essere primo con $\varphi(n)$; l'algoritmo di Euclide verifica questa condizione.
  
- **Calcolo di $d$:**  
  Utilizzando l’algoritmo di Euclide Esteso, si trova l’inverso moltiplicativo di $e$ modulo $\varphi(n)$.

### Operazioni di Codifica e Decodifica

La codifica e decodifica RSA richiedono il calcolo di potenze modulari, ossia di espressioni della forma:
$$
a^b \mod c
$$
con $a$, $b$ e $c$ interi molto grandi.

- **Metodo "Stupido":**  
  Moltiplicare $a$ per se stesso $b$ volte, riducendo modulo $c$ ad ogni passaggio.  
  Questo approccio diretto è inefficiente per esponenti molto lunghi.
  
- **Metodo Ottimizzato:**  
  Utilizzare l'espansione binaria dell'esponente e la tecnica di "esponenziazione rapida", che comporta un numero di operazioni lineare rispetto alla lunghezza binaria dell'esponente.

### Algoritmo di Euclide e quello Esteso

#### Algoritmo di Euclide per il Massimo Comune Divisore (MCD)

Euclide-gcd(a, b):
1. if b == 0 then return a
2. else return Euclide-gcd(b, a mod b)

- Costo: O(log b).

#### Algoritmo di Euclide Esteso

Euclide-esteso(a, b):
1. if b == 0 then return (a, 1, 0)
2. else:
      (d, x, y) = Euclide-esteso(b, a mod b)
      return (d, y, x - floor(a/b)*y)

- Costo: O(log b).  
Questo algoritmo fornisce anche i coefficienti dell'identità di Bézout, utilizzati per trovare l'inverso moltiplicativo di $a$ modulo $b$.

### Cifrari Ibridi

I cifrari asimmetrici sono notoriamente lenti, mentre i cifrari simmetrici richiedono chiavi segrete condivise.  
I sistemi cifrari ibridi combinano i due approcci:
- **Ruolo dell'Asimmetrica:**  
  Utilizzata per lo scambio sicuro della chiave segreta.
- **Ruolo della Simmetrica:**  
  Utilizzata per la cifratura effettiva delle comunicazioni a causa della sua maggiore velocità.

In questo modo si sfruttano i vantaggi di entrambi i sistemi garantendo comunicazioni sicure e performanti.