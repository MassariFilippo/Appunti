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