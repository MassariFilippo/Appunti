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
      - [Cifrari a Chiave Segreta](#cifrari-a-chiave-segreta)
      - [Cifrari a Chiave Pubblica](#cifrari-a-chiave-pubblica)
    - [Funzioni One-Way con Trap-Door](#funzioni-one-way-con-trap-door)
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
- **Cifrari Segreti**: Funzioni di cifratura e decifratura mantenute segrete.
- **Cifrari Pubblici**: Funzioni note a tutti, ma con chiavi segrete per la cifratura e decifratura.

#### Cifrari a Chiave Segreta
- **Funzioni**: C(m; k) per cifratura e D(c; k) per decifratura.
- **Sicurezza**: La chiave deve rimanere segreta; se compromessa, deve essere generata una nuova chiave.

#### Cifrari a Chiave Pubblica
- **Introduzione**: Introdotti da Diffie e Hellman nel 1976, eliminano la necessità di condividere una chiave segreta.
- **Funzionamento**: Utilizzano due chiavi: una pubblica (k[pub]) per cifrare e una privata (k[prv]) per decifrare.
- **Proprietà**: Le funzioni di cifratura e decifratura sono pubbliche, ma solo il destinatario ha accesso alla chiave privata.

### Funzioni One-Way con Trap-Door
- **Definizione**: Facile calcolare C per cifrare, difficile calcolare D per decifrare senza un meccanismo segreto.
- **Esempio**: Moltiplicare due numeri primi è facile, ma fattorizzare il prodotto è difficile senza conoscere uno dei fattori.

### Applicazioni della Crittografia
- **Requisiti Fondamentali**:
  1. **Identificazione**: Verifica dell'identità dell'utente.
  2. **Autenticazione**: Conferma che un messaggio provenga realmente dal mittente.
  3. **Firma Digitale**: Garantisce che il mittente non possa negare l'invio di un messaggio.