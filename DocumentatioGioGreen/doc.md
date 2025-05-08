## 1. Analisi dei Requisiti

### 1.1 Intervista

#### a. Stakeholder coinvolti:
- **Admin**: gestisce il catalogo prodotti (piante, vasi, prodotti chimici, substrati), crea sconti, invia notifiche e monitora le statistiche di vendita.
- **Utente registrato**: acquista prodotti e gestisce i suoi ordini, valuta i prodotti, riceve notifiche, aggiorna i suoi dati personali.
- **Utente ospite**: può esplorare il sito, ma per effettuare ordini è richiesta la registrazione/autenticazione.

#### b. Domande chiave emerse:
- Quali tipologie di prodotti saranno gestite?
- Quali attributi specifici possiede ogni tipo di prodotto?
- Come avviene l’inserimento e la gestione dei prodotti?
- Ogni prodotto può avere sconti, taglie e quantità disponibili?
- In che modo vengono gestiti gli ordini? Quali dati richiede la spedizione/fatturazione?
- Quali modalità di pagamento sono previste?
- L’utente può valutare i prodotti acquistati e con quali modalità?
- Come si gestiscono le notifiche per utenti e admin?
- Cosa contiene l’area personale di ciascun tipo di utente?

---

### 1.2 Rilevamento delle Ambiguità e Correzioni Proposte

**Ambiguità individuate:**
- **Gestione scorte**: cosa succede se la quantità di prodotto arriva a zero? Si può impostare un prodotto come “non disponibile”?
- **Gestione delle taglie**: tutti i prodotti hanno taglie o solo alcuni? Se un vaso ha più taglie, si tratta sempre dello stesso prodotto o di varianti?
- **Valutazione prodotti**: chi può inserire una valutazione? Solo chi ha acquistato il prodotto?
- **Tipi di pagamento**: quali? (Carta di credito, PayPal, bonifico, alla consegna, ecc.)
- **Gestione notifiche**: quali azioni generano notifiche per l’utente? (solo ordine effettuato o anche spedizione, ecc.)
- **Ruoli utente**: Esiste la possibilità di definire altri ruoli oltre ad admin e utente?

**Proposte di chiarimento:**
- Permettere all’admin di impostare un prodotto come “non disponibile” e gestire il rifornimento scorte.
- Stabilire quali prodotti usano il campo taglia e, in caso di varianti, gestirle come sottoprodotti o varianti.
- Limitare l'inserimento di valutazioni ai soli utenti che hanno realmente acquistato il prodotto.
- Elencare le tipologie di pagamento implementate.
- Dettagliare le possibili azioni per notifiche (ordine ricevuto, spedito, consegnato, ecc.).
- Prevedere esplicitamente un attributo “ruolo” per eventuali estensioni future.

---

### 1.3 Definizione delle Specifiche in Linguaggio Naturale

- Il sito consente la **vendita di piante, vasi, prodotti chimici e substrati**.  
- **Gli utenti** possono registrarsi, navigare il catalogo prodotti, aggiungere prodotti al carrello, acquistare selezionando quantità desiderate (se disponibili) e applicando eventuali sconti.  
- **Ogni prodotto** ha un nome, una descrizione, una taglia, una quantità disponibile, un prezzo e può essere associato a uno sconto.  
- **Le piante** includono anche la specie; **i vasi** includono forma e materiale.  
- Durante l’acquisto, l’utente inserisce i dati per **spedizione**, **fatturazione** e **pagamento**, scegliendo tra più modalità disponibili.
- L’utente, dopo l’acquisto, può **valutare i prodotti** con un sistema a stelle e testo descrittivo.
- Nell’area personale, l’utente trova gli **ordini effettuati**, le notifiche (ad esempio conferma dell’ordine) e i propri dati personali.
- Un **admin** può inserire nuovi prodotti, creare e gestire sconti, inviare notifiche agli utenti, visualizzare la lista degli utenti e consultare le statistiche di vendita dalla propria area riservata.

---

### 1.4 Estrazione dei Concetti Principali

**Entità principali**:
- **Prodotto** (con sottotipi: Pianta, Vaso, Prodotto Chimico, Substrato)
- **Utente** (con sottotipi: Cliente, Admin)
- **Carrello**
- **Ordine**
- **Valutazione**
- **Sconto**
- **Notifica**
- **Dati di spedizione**
- **Dati di fatturazione**
- **Pagamento**

**Attributi chiave**:
- Prodotto: nome, descrizione, taglia, quantità, prezzo, sconto (opzionale), (specie per piante; forma e materiale per vasi)
- Utente: nome, cognome, email, password, ruolo, dati spedizione e fatturazione associati
- Ordine: data, lista prodotti, totale, stato, tipo pagamento, riferimenti spedizione/fatturazione
- Sconto: percentuale/valore, validità
- Valutazione: stelle, testo, riferimenti prodotto/utente
- Notifica: testo, data, stato lettura, destinatario
