# APPUNTI DI INGEGNERIA DEL SOFTWARE

## Ingegneria del Software

### Che cos'è l’**Ingegneria del Software**?
L’ingegneria del software è la disciplina che si occupa della **realizzazione di sistemi software** complessi, la cui **dimensione** e **complessità** richiedono l'intervento di team di sviluppo dedicati. Questo settore è emerso per affrontare la crescente complessità dei sistemi software, passando da semplici programmi individuali a **sistemi collaborativi** e commerciali, come OS 360 di IBM negli anni '50, fino a moderni standard di qualità come **ISO-9000**.

### Definizioni fondamentali
L’ingegneria del software è definita come un approccio **sistematico** alla **progettazione**, **manutenzione** e **ritiro** di sistemi software. La disciplina mira a produrre software in modo **sistematico** e **strutturato**, rispettando tempi e costi stabiliti. Si fonda su un **corpus di teorie, metodi e strumenti** sia tecnologici che organizzativi per garantire la **qualità** del software prodotto.

## Qualità del Software
Le qualità del software si suddividono in:
- **Qualità interne**: aspetti legati allo **sviluppo** del software, invisibili agli utenti.
- **Qualità esterne**: aspetti legati alle **funzionalità** del prodotto, visibili agli utenti.

Entrambe le qualità sono **interdipendenti**: un software non può avere alta qualità esterna senza adeguate qualità interne.

### Caratteristiche principali della Qualità del Software
1. **Correttezza**: rispetta le specifiche di progetto.
2. **Affidabilità**: l’utente può contare sul software.
3. **Robustezza**: capacità di reagire in modo ragionevole anche a input non previsti.
4. **Efficienza**: utilizzo ottimale delle risorse di calcolo.
5. **Facilità d'uso**: interfaccia intuitiva per l’utente.
6. **Verificabilità**: facilità di valutare la correttezza e le prestazioni.
7. **Riusabilità**: utilizzo del software per creare nuovi sistemi.
8. **Portabilità**: capacità di funzionare su piattaforme diverse.

### Software Design e Principi di Progettazione
Il **software design** è il processo che trasforma le specifiche utente in un **insieme di specifiche** per i programmatori, producendo un’**architettura** chiara del software. La progettazione si basa su principi come:

1. **Formalità**: uso di **metodologie standardizzate** per ridurre errori.
2. **Anticipazione dei cambiamenti**: progetta per i requisiti attuali e futuri.
3. **Separazione degli argomenti**: suddivide problemi complessi in elementi più semplici.
4. **Modularità**: scomposizione in moduli funzionali autonomi, che facilita manutenzione e riuso.
5. **Astrazione**: identificazione degli aspetti fondamentali di un problema, ignorando i dettagli.

### Misurazione dei Costi
Nel ciclo di vita del software, la **misurazione** permette di prevedere tempi di consegna, **costi** e qualità del prodotto. Sebbene le caratteristiche del software rendano ambigue alcune misure, la disciplina ha proposto **metodi e metriche** per agevolare la valutazione.

### Stima dei Costi
I costi del software includono:
- **Risorse di sviluppo** (personale tecnico, supporto, materiali).
- **Metriche dimensionali** (numero di istruzioni o linee di codice) e **funzionali** (es. Function Points).

### Il Metodo dei Function Points
I **Function Points** (FP) rappresentano una metrica per valutare la **dimensione funzionale** del software. Introdotto negli anni '70, il metodo consente di quantificare le funzionalità offerte all’utente, indipendentemente dall’ambiente tecnologico. 

### Conteggio e Tipi di Function Points
Il conteggio dei Function Points prevede l’identificazione di:
- **Funzioni di tipo dati**: file interni ed esterni.
- **Funzioni di tipo transazione**: input, output, e interrogazioni.
Questo metodo può essere utilizzato in **progetti di sviluppo**, **manutenzione evolutiva** e **software esistenti**, permettendo una valutazione continua del software nel tempo.

### Ambito del Conteggio e Confine delle Applicazioni
- **Definizione dell'Ambito del Conteggio**: L’ambito del conteggio definisce le funzionalità che devono essere considerate in un conteggio.
- **Definizione del Confine**: Il confine è la linea di separazione tra le applicazioni che si stanno misurando e le applicazioni esterne o l’utente.
- **Regole per Definire il Confine**:
  - Il confine è stabilito dal punto di vista dell’utente.
  - Tra applicazioni collegate, il confine si basa su aree funzionali distinte per l’utente, indipendentemente dagli aspetti tecnologici.

### Funzioni di Tipo Dati
- **File Interno Logico (ILF)**: È un insieme di dati o informazioni di controllo logicamente collegati, riconoscibili dall’utente e mantenuti all’interno dell’applicazione.
  - Primario compito: contenere dati mantenuti da processi elementari dell'applicazione.
- **File Esterno di Interfaccia (EIF)**: Insieme di dati o informazioni di controllo riconoscibili dall’utente, referenziati dall'applicazione ma mantenuti all'interno di un'altra applicazione.
  - Primario compito: contenere dati referenziati da processi elementari; un EIF per un’applicazione è un ILF in un’altra.

### Esempi di Funzioni di Tipo Dati
- **ILF**:
  - Dati relativi a entità come impiegati, prodotti, clienti.
  - Dati sulle transazioni, come registrazioni di prelievi o spese.
  - Dati di sicurezza dell’applicazione, dati di log e dati di help.
- **EIF**:
  - Dati gestiti da altre applicazioni.
  - Dati di sicurezza, log e help mantenuti esternamente all’applicazione.

### Funzioni di Tipo Transazione
- **Input Esterno (EI)**: Processo elementare che elabora dati provenienti dall’esterno del confine dell’applicazione. Ha il compito di mantenere ILF o modificare il comportamento del sistema.
- **Output Esterno (EO)**: Processo che invia dati fuori dal confine, utilizzando logiche di processo complesse per presentare informazioni.
- **Interrogazione Esterna (EQ)**: Processo che recupera dati da un ILF o EIF senza calcoli complessi e senza creare dati derivati.

### Fattore di Aggiustamento
- **Scopo**: Adatta il totale dei Function Points per rappresentare funzionalità generali del sistema non coperte dalle funzioni dati e transazionali.
- **Calcolo**: Si basa sul Total Degree of Influence (TDI), con il fattore di aggiustamento che varia tra 0.65 e 1.35.
  - **Formula**: \( \text{fattore di aggiustamento} = 0.65 + (TDI \times 0.01) \).

### Numero Ciclomatico
- **Definizione**: È una metrica proposta da McCabe (1976) che misura la complessità del flusso di controllo di un programma.
- **Calcolo del Numero Ciclomatico**:
  - Formula base per un grafo connesso: \( v(G) = e - n + 2 \), dove \( e \) è il numero degli archi e \( n \) dei nodi.
- **Teorema di Mills**: \( v(G) = d + 1 \), con \( d \) pari ai punti di decisione. Se il programma ha procedure, il numero ciclomatico complessivo è la somma dei numeri ciclomatici dei grafi indipendenti.

### Modello Intermedio per Stima dei Costi
1. **Stima della Dimensione del Software**: Basata sul numero di linee di codice o Function Points (FP), utilizzando tabelle di conversione per linguaggi specifici.
2. **Determinazione della Classe del Software**: Le categorie (Organic, Semi-detached, Embedded) differenziano le formule di costo in base alla complessità e dimensione.
3. **Applicazione degli Stimatori di Costo**: Considera proprietà del prodotto, caratteristiche hardware, esperienza del team e specifiche del progetto.

### Produzione del Software
- **Processo di Produzione**: Consiste nelle fasi per costruire, consegnare e modificare un prodotto. Viene gestito tramite modelli di processo come quelli:
  - A cascata
  - Incrementali
  - Evolutivi
  - Agili

### Modelli Prescrittivi
- **Caratteristiche**: Definiscono attività, azioni e prodotti per ingegnerizzare software di alta qualità, creando stabilità e controllo.
- **Attività Comuni**: Comunicazione (raccolta dei requisiti), pianificazione, modellazione, costruzione (testing), e deployment.

### Modello a Cascata (Waterfall)
- **Descrizione**: Approccio sequenziale in cui ogni fase rappresenta l’input della successiva; non adatto a requisiti incerti.
- **Limite**: Non consente modifiche retroattive e non offre una versione funzionante fino alla fine del progetto.

### Modello Incrementale
- **Caratteristiche**: Combina aspetti del modello a cascata, producendo software a incrementi tramite sequenze lineari.
- **Vantaggio**: Permette aggiornamenti frequenti e integrazione graduale di nuove funzionalità.

### Modello RAD (Rapid Application Development)
- **Descrizione**: Modello incrementale che punta a cicli di sviluppo rapidi. Adatto per progetti modulari completabili in meno di tre mesi.
- **Limiti**: Può fallire se l’utente non riesce a seguire il ritmo o se il sistema non è modularizzabile.

### Modelli Evolutivi e Prototipazione
- **Prototipazione**: Versione preliminare del software, usata per chiarire requisiti poco definiti e addestrare l’utente.
- **Benefici**: Rende evidenti ambiguità e migliora la comprensione dei requisiti.
- **Tipologie**:
  - **Prototipazione Evolutiva**: Evoluzione del prototipo nel prodotto finale.
  - **Prototipo Usa e Getta**: Valida o deriva i requisiti, senza integrazione nel prodotto finale.