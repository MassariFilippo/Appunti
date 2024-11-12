# APPUNTI DI INGEGNERIA DEL SOFTWARE

## Ingegneria del Software

### Che cos'è l’**Ingegneria del Software**?
L’ingegneria del software è la disciplina che si occupa della **realizzazione di sistemi software** complessi, la cui **dimensione** e **complessità** richiedono l'intervento di team di sviluppo dedicati. Questo settore è emerso per affrontare la crescente complessità dei sistemi software, passando da semplici programmi individuali a **sistemi collaborativi** e commerciali, come OS 360 di IBM negli anni '50, fino a moderni standard di qualità come **ISO-9000**.

### Definizioni fondamentali
L’ingegneria del software è definita come un approccio **sistematico** alla **progettazione**, **manutenzione** e **ritiro** di sistemi software. La disciplina mira a produrre software in modo **sistematico** e **strutturato**, rispettando tempi e costi stabiliti. Si fonda su un **corpus di teorie, metodi e strumenti** sia tecnologici che organizzativi per garantire la **qualità** del software prodotto.

## Qualità del Software

### Tipi di Qualità
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

## Software Design e Principi di Progettazione

### Software Design
Il **software design** è il processo che trasforma le specifiche utente in un **insieme di specifiche** per i programmatori, producendo un’**architettura** chiara del software.

### Principi di Progettazione
La progettazione si basa su principi come:
1. **Formalità**: uso di **metodologie standardizzate** per ridurre errori.
2. **Anticipazione dei cambiamenti**: progetta per i requisiti attuali e futuri.
3. **Separazione degli argomenti**: suddivide problemi complessi in elementi più semplici.
4. **Modularità**: scomposizione in moduli funzionali autonomi, che facilita manutenzione e riuso.
5. **Astrazione**: identificazione degli aspetti fondamentali di un problema, ignorando i dettagli.

## Misurazione e Stima dei Costi

### Misurazione dei Costi
Nel ciclo di vita del software, la **misurazione** permette di prevedere tempi di consegna, **costi** e qualità del prodotto. Sebbene le caratteristiche del software rendano ambigue alcune misure, la disciplina ha proposto **metodi e metriche** per agevolare la valutazione.

### Stima dei Costi
I costi del software includono:
- **Risorse di sviluppo** (personale tecnico, supporto, materiali).
- **Metriche dimensionali** (numero di istruzioni o linee di codice) e **funzionali** (es. Function Points).

### Il Metodo dei Function Points
I **Function Points** (FP) rappresentano una metrica per valutare la **dimensione funzionale** del software. Introdotto negli anni '70, il metodo consente di quantificare le funzionalità offerte all’utente, indipendentemente dall’ambiente tecnologico.

-  **Conteggio e Tipi di Function Points
Il conteggio dei Function Points prevede l’identificazione di:
- **Funzioni di tipo dati**: file interni logici ed esterni di interfaccia.
- **Funzioni di tipo transazione**: input, output, e interrogazioni.

-  **Calcolo del Numero di Function Points Non Pesato
Per calcolare il numero di Function Points non pesato, è necessario seguire questi passaggi:
1. **Identificare le funzionalità**: Determinare tutte le funzionalità del sistema, suddividendole in funzioni di tipo dati e funzioni di tipo transazione.
2. **Assegnare un peso a ciascuna funzionalità**: Ogni funzionalità viene classificata in base alla sua complessità (bassa, media, alta) e viene assegnato un peso corrispondente.
3. **Calcolare il totale dei Function Points non pesato**: Moltiplicare il numero di ciascun tipo di funzionalità per il peso assegnato e sommare i risultati.

### Ambito del Conteggio e Confine delle Applicazioni
- **Definizione dell'Ambito del Conteggio**: L’ambito del conteggio definisce le funzionalità che devono essere considerate in un conteggio.
- **Progetti di Sviluppo e Preservazione dei Vecchi Dati**
  - **Progetti di Sviluppo**: Includono tutte le nuove funzionalità che devono essere sviluppate.
  - **Preservazione dei Vecchi Dati**: Includono le attività necessarie per garantire che i dati esistenti siano mantenuti e accessibili.
- **Manutenzione Evolutiva**: Riguarda le modifiche e gli aggiornamenti che migliorano o estendono le funzionalità esistenti di un'applicazione.
- **Applicazione Esistente**: Si riferisce a un'applicazione già in uso che potrebbe richiedere aggiornamenti, correzioni di bug o miglioramenti.

### Funzioni di Tipo Dati
- **File Interno Logico (ILF)**: È un insieme di dati o informazioni di controllo logicamente collegati, riconoscibili dall’utente e mantenuti all’interno dell’applicazione.
- **File Esterno di Interfaccia (EIF)**: Insieme di dati o informazioni di controllo riconoscibili dall’utente, referenziati dall'applicazione ma mantenuti all'interno di un'altra applicazione.

### Funzioni di Tipo Transazione
- **Input Esterno (EI)**: Processo elementare che elabora dati provenienti dall’esterno del confine dell’applicazione.
- **Output Esterno (EO)**: Processo che invia dati fuori dal confine, utilizzando logiche di processo complesse per presentare informazioni.
- **Interrogazione Esterna (EQ)**: Processo che recupera dati da un ILF o EIF senza calcoli complessi e senza creare dati derivati.

### Fattore di Aggiustamento
- **Scopo**: Adatta il totale dei Function Points per rappresentare funzionalità generali del sistema non coperte dalle funzioni dati e transazionali.
- **Calcolo**: Si basa sul Total Degree of Influence (TDI) calcolati su una serie di fattori, con il fattore di aggiustamento che varia tra 0.65 e 1.35.

## Numero Ciclomatico

### Definizione
Il numero ciclomatico è una metrica del software proposta da McCabe nel 1976, che misura la complessità del flusso di controllo di un programma.

### Calcolo del Numero Ciclomatico
Il numero ciclomatico di un grafo fortemente connesso si calcola come:
\[ v(G) = e - n + 2 \]
dove:
- \( e \) è il numero degli archi
- \( n \) è il numero dei nodi

### Teorema di Mills
Secondo il teorema di Mills:
\[ v(G) = d + 1 \]
dove:
- \( d \) è il numero di punti di decisione del programma

### Programmi con Procedure Interne
Se il programma ha procedure interne, il numero ciclomatico totale è la somma dei numeri ciclomatici dei singoli grafi indipendenti:
\[ v(G) = e - n + 2p \]
dove:
- \( p \) è il numero di grafi indipendenti

### Importanza del Numero Ciclomatico
Il numero ciclomatico cattura la complessità del flusso di controllo e sperimentalmente si correla con il numero di errori riscontrati. Si raccomanda che la complessità ciclomatica di un modulo non superi il valore 10.

## Modello Intermedio per Stima dei Costi

### Stima della Dimensione del Software
Basata sul numero di linee di codice o Function Points (FP), utilizzando tabelle di conversione per linguaggi specifici.

### Determinazione della Classe del Software
Le categorie (Organic, Semi-detached, Embedded) differenziano le formule di costo in base alla complessità e dimensione.

### Applicazione degli Stimatori di Costo
Considera proprietà del prodotto, caratteristiche hardware, esperienza del team e specifiche del progetto.

## Produzione del Software

### Processo di Produzione
Consiste nelle fasi per costruire, consegnare e modificare un prodotto. Viene gestito tramite modelli di processo come quelli:
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
  ![immagine in locale](img\Work_flow_rototipazione_evolutiva.PNG)
  - **Prototipo Usa e Getta**: Valida o deriva i requisiti, senza integrazione nel prodotto finale.
  ![immagine in locale](img\work_flow_prototipazione_usa_e_getta.PNG)

### Prototipazione di Interfaccia
- **Importanza**: È impossibile specificare in anticipo il look and feel di una interfaccia utente in maniera efficace, quindi prototipare è essenziale.
- **Sviluppo di GUI**: Lo sviluppo di GUI (Graphical User Interface) sta diventando una attività che prende la maggior parte del costo dello sviluppo del sistema.
- **Generatori di Interfacce Utente**: Possono essere usati per “disegnare” l’interfaccia e simularne la funzionalità.

### Modello a Spirale
- **Descrizione**: Fa crescere incrementalmente il grado di definizione e implementazione del sistema, riducendo il livello di rischio e producendo un insieme di milestone per garantire la fattibilità delle soluzioni intraprese.
1. Customer communication: Colloquio tra
cliente e team di sviluppo
2. Planning: Raccolta requisiti e definizione
piano di progetto
3. Risk analysis: Stima e prevenzione dei
rischi tecnici e di gestione
4. Engineering: Modellazione e
progettazione
5. Construction & release: Realizzazione,
collaudo e installazione
6. Costumer evaluation: Rilevazione delle
reazioni da parte del cliente 

### MDD (Model-Driven Development)
Tipo di sviluppo in cui si creano modelli formali del software che vengono poi fatti evolvere mentre il sistema viene progettato e implementato. I modelli diventano la guida del processo di sviluppo; infatti, MDD prevede l’uso di strumenti per la generazione automatica del codice e dei test case a partire dai modelli.
![immagine in locale](img\Schema_MDD.PNG)

### I modelli agili

I modelli agili sono stati ideati per superare le limitazioni dei modelli prescrittivi tradizionali, che, basati su una disciplina rigida, non tengono conto della complessità e della fragilità degli sviluppatori di software. I modelli agili presentano alcune caratteristiche distintive:

- **Soddisfazione del cliente**: mirano a garantire una soddisfazione elevata del cliente e una consegna incrementale anticipata del software.
- **Team di sviluppo**: prevedono team compatti e molto motivati, facilitando un ambiente di lavoro coeso e orientato agli obiettivi.
- **Metodi informali**: adottano metodi di lavoro informali, promuovendo una maggiore flessibilità e adattabilità.
- **Prodotti di ingegneria minimali**: producono solo i minimi prodotti necessari per l'ingegneria del software.
- **Semplicità di sviluppo**: incoraggiano un approccio semplice e lineare al processo di sviluppo.
- **Comunicazione continua**: enfatizzano l'importanza della comunicazione costante tra sviluppatori e utenti per garantire che le esigenze siano sempre allineate.

### Extreme Programming (XP)

Extreme Programming (XP) è uno dei modelli di processo agile più diffusi, nato nel 1999. XP adotta un approccio orientato agli oggetti e si basa su quattro attività strutturali principali: pianificazione, design, programmazione e testing.

**Pianificazione**

Durante la fase di pianificazione, il team XP utilizza le **user story**, brevi descrizioni delle funzionalità del software, come elementi fondamentali per definire le esigenze:

- Ogni user story viene valutata dal cliente, che ne assegna un valore per indicare la priorità.
- I progettisti stimano il costo di ogni user story in termini di settimane di sviluppo.
- Se una user story richiede più di tre settimane di sviluppo, il cliente viene invitato a frammentarla.
- Cliente e progettisti decidono insieme quali user story inserire nella release successiva, ordinandole per valore o rischio decrescenti.

**Design**

La fase di design in XP è volta alla massima semplicità e scoraggia la progettazione di funzionalità non necessarie:

- Si incoraggia l’uso di schede CRC (Classe-Responsabilità-Collaborazione) per definire le responsabilità e le interazioni delle classi.
- Se emerge un problema di design, si sviluppa immediatamente un prototipo operativo (spike solution) da valutare.
- Il design promuove il **refactoring**, ossia la ripulitura e riorganizzazione del codice senza alterarne il comportamento esterno.
- L'architettura viene considerata un elemento transitorio, da adattare alle necessità del momento.

**Programmazione**

XP prevede una tecnica chiamata **pair programming**, dove due persone collaborano alla stessa workstation per sviluppare il software. Questa pratica:

- Facilita la risoluzione immediata dei problemi.
- Garantisce una verifica di qualità in tempo reale grazie alla collaborazione continua tra i membri del team.

**Testing**

La fase di testing inizia già prima della programmazione con la definizione degli **unit test**, test automatizzati per ogni componente singolo:

- Questi test vengono implementati con strumenti che ne permettono l'automazione.
- A ogni modifica del software, si esegue un test di regressione (dato che l'implementazione di nuove funzionalità potrebbe compromettere vecche funzionalità implementate) per garantire che il sistema continui a funzionare correttamente.

### Misurazione della velocità del progetto

Dopo il primo rilascio, il team XP calcola la **velocità del progetto**, che rappresenta il numero di user story completate nella prima release. La velocità del progetto è uno strumento fondamentale che consente di:

- Stimare le date di consegna e le pianificazioni delle release successive.
- Identificare eventuali sottovalutazioni delle user story, consentendo di modificare il contenuto delle future release o di rivedere le date di consegna.

### Unified Process

Unified Process (UP) è un modello di sviluppo del software creato da Booch, Rumbaugh e Jacobson, gli stessi autori di UML. Si tratta di un processo:

- **Guidato dai casi d’uso**: utilizza i casi d'uso come base per identificare e definire i requisiti del sistema.
- **Centrato sull’architettura**: pone l'architettura come fondamento dello sviluppo.
- **Iterativo e incrementale**: prevede cicli di sviluppo ripetuti, ognuno dei quali aggiunge funzionalità al sistema.
- **Model-based e component-based**: focalizzato sui modelli e sull'uso di componenti riutilizzabili.
- **Object-oriented**: adotta la programmazione orientata agli oggetti come base metodologica.
- **Configurabile**: il processo può essere adattato alle specifiche esigenze del progetto.

### Un modello di UP

UP è organizzato in modo tale da definire **CHI, COSA e QUANDO** per ogni attività.

- **CHI**: definisce i ruoli e le responsabilità, assegnando a ogni ruolo il comportamento specifico e le responsabilità, che possono essere svolte da individui o gruppi.
- **COSA**: definisce il comportamento del ruolo, espresso in termini di attività (cosa fare) e manufatti (cosa produrre).
- **QUANDO**: rappresenta i flussi di lavoro, cioè sequenze di attività correlate che vengono eseguite da ruoli specifici per produrre i manufatti del processo.

**Manufatti**

UP prevede la produzione di vari set di manufatti, ciascuno contenente elementi essenziali per il progetto:

- **Set di gestione**:
  - Elaborati di pianificazione, come il software development plan e lo studio economico.
  - Elaborati operazionali, come gli stati di avanzamento e le descrizioni delle versioni.
- **Set dei requisiti**:
  - Documento di visione, modello dei casi d’uso e modello di business.
- **Set di progettazione**:
  - Modello di design, modello architetturale e modello di test.
- **Set di implementazione**:
  - Codice sorgente ed eseguibili, insieme ai file di dati.
- **Set di rilascio agli utenti**:
  - Script di installazione, documentazione per l’utente e materiale formativo.

**Flussi di lavoro**

I flussi di lavoro in UP non seguono una sequenza rigida, ma si svolgono iterativamente nel corso del progetto:

- **Requisiti**: definizione delle funzionalità e dei requisiti di sistema.
- **Analisi**: raffinamento e strutturazione dei requisiti.
- **Progettazione**: sviluppo dell’architettura e del design del sistema.
- **Implementazione**: sviluppo e costruzione del software.
- **Test**: verifica che l’implementazione rispetti i requisiti definiti.
- **Deployment**: configurazione e distribuzione del sistema nell'ambiente di produzione.
- **Gestione configurazione**: mantenimento delle versioni del sistema.
- **Gestione progetto**: pianificazione e gestione dell’intero processo iterativo.
- **Ambiente**: definizione delle infrastrutture e strumenti di sviluppo necessari.

**Fasi**

Le fasi del processo UP sono sequenziali e rappresentano milestone significative per gli stakeholder del progetto:

- **Inception (avvio)**: definizione degli obiettivi del progetto, analisi della fattibilità, stima di costi e rischi, valutazione del mercato e confronto con prodotti concorrenti.
- **Elaboration**: pianificazione del progetto e definizione delle caratteristiche funzionali, strutturali e architetturali.
- **Construction**: sviluppo del prodotto attraverso iterazioni, testing e preparazione della documentazione.
- **Transition**: consegna del sistema agli utenti finali, includendo attività di marketing, installazione, configurazione, formazione, supporto e manutenzione.

Ogni fase può includere una o più iterazioni, determinate dalle scelte del Project Manager e dai rischi del progetto.

**Milestone**

Ogni fase prevede una milestone (punto cardine) che rappresenta il completamento di obiettivi chiave e consegan di relativo materiale:

- **Inception**: documentazione della fattibilità del progetto.
- **Elaboration**: specifica dei requisiti software e architettura consolidata e verificata.
- **Construction**: versione del sistema in pre-produzione (Beta).
- **Transition**: rilascio del sistema in produzione per gli utenti finali.

![immagine locale](img\fasi_UP.PNG)
