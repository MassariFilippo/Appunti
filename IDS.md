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

### Numero Ciclomatico

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
  ![immagine in locale](img\IDS\Work_flow_rototipazione_evolutiva.PNG)
  - **Prototipo Usa e Getta**: Valida o deriva i requisiti, senza integrazione nel prodotto finale.
  ![immagine in locale](img\IDS\work_flow_prototipazione_usa_e_getta.PNG)

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
![immagine in locale](img\IDS\Schema_MDD.PNG)

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

![immagine locale](img\IDS\fasi_UP.PNG)

## Verifica del software

La fase di verifica del software è finalizzata a controllare che il sistema sviluppato sia conforme alle specifiche di progetto. Questo processo non si limita al prodotto finale, ma accompagna ogni fase del progetto e dello sviluppo del software, assicurando la coerenza del prodotto con i requisiti originali. Le tecniche di verifica del software possono essere suddivise in due categorie principali:

- **Dinamiche o di testing**: queste tecniche verificano il corretto funzionamento del sistema attraverso prove sperimentali che valutano il comportamento del software in una varietà di situazioni rappresentative. Si tratta delle tecniche di verifica più utilizzate nella pratica.
- **Statiche o di analisi**: mirano a verificare il funzionamento del sistema esaminando la struttura dei moduli e il codice sorgente. A differenza delle tecniche dinamiche, le verifiche statiche possono essere applicate in ogni fase del ciclo di vita del software.

### Testing

Il testing è una delle operazioni più critiche per la verifica del software. Tuttavia, come osservato da Dijkstra nel 1972, "le operazioni di testing possono individuare la presenza di errori nel software ma non possono dimostrarne la correttezza". L’obiettivo del testing è quindi verificare il comportamento del sistema in un insieme di casi abbastanza ampio da garantire, con una buona probabilità, che il sistema risponderà correttamente anche nelle situazioni non testate.

Poiché un **testing esaustivo** (cioè verificare il sistema in tutte le possibili circostanze) è impraticabile, è essenziale selezionare criteri per individuare i casi di test più significativi ovvero le un sottoinsieme significativo dei casi d'uso. 
Le operazioni di testing si dividono in due tipologie principali:

- **Testing in the small**: riguarda l’esame di singoli moduli o porzioni specifiche di codice che risultano particolarmente complesse o rilevanti per il corretto funzionamento del sistema. Questo tipo di testing è detto **white-box**, in quanto richiede accesso diretto al codice, e in particolare al flusso di controllo, che viene utilizzato per identificare un insieme significativo di input da somministrare al software. Attraverso alcuni **criteri di copertura**, si selezionano i test case utili per garantire una rappresentatività degli input e coprire efficacemente le varie parti del codice. I principali criteri di copertura includono:
  (NON CAPITE, VERIFICARE LA CORRETTEZZA)
  - **Criterio di copertura dei programmi (statement test)**: consiste nel selezionare un insieme di test tali che, eseguendo il programma su tutti i casi di test selezionati, ogni istruzione elementare del programma venga eseguita almeno una volta. Questo criterio si basa sull’idea che un errore nel codice non può essere rilevato se la parte di codice che lo contiene non viene eseguita almeno una volta. È applicabile solo conoscendo la struttura interna del codice, quindi fa parte del white-box testing.

  - **Criterio di copertura delle decisioni (branch test)**: prevede la selezione di un insieme di test in modo che, durante l’esecuzione del programma, ogni ramo o percorso decisionale del grafo di controllo venga attraversato almeno una volta. Questo criterio si focalizza sul flusso di controllo e richiede che per ogni condizione presente nel codice sia utilizzato un test che produca sia un esito TRUE sia un esito FALSE. Anche questo tipo di verifica si basa sulla conoscenza della struttura interna del codice e rientra nel white-box testing.

  - **Criterio di copertura delle decisioni e delle condizioni**: questo criterio è ancora più rigoroso rispetto al precedente e richiede che ogni arco del grafo di controllo sia percorso, e che tutti i possibili risultati delle condizioni composte siano valutati almeno una volta. Ogni condizione composta deve quindi essere testata per generare esiti TRUE e FALSE, permettendo un’analisi più dettagliata delle combinazioni logiche presenti nel codice. Anche in questo caso, la verifica è possibile solo conoscendo la struttura interna del codice ed è una tecnica di white-box testing.

Questi criteri permettono di coprire in modo significativo le possibili esecuzioni del codice, riducendo la probabilità che errori sfuggano al controllo durante le fasi di verifica ma sono fallacei e dipendono dalla struttura del codice e dalla posizione dell'errore in esso.

- **Testing in the large**: si concentra sull’intero sistema e verifica la funzionalità complessiva, assicurandosi che tutte le componenti interagiscano correttamente per soddisfare i requisiti stabiliti. Poiché in sistemi complessi si presenta un’enorme quantità di situazioni possibili, l’uso di tecniche white-box diventa impraticabile a causa dell’esplosione combinatoria delle variabili da testare. Per questo motivo, il testing in the large adotta un approccio black-box: il sistema viene trattato come una "scatola nera" in cui l’attenzione si sposta sull’analisi dei rapporti input-output senza considerare l’implementazione interna.

  L’insieme di test viene definito a partire dalle specifiche di progetto, le quali determinano i valori di input e i relativi output attesi. In questa fase, il **diagramma UML dei use case** risulta essenziale: esso definisce i casi d’uso del sistema, descrivendo tutte le interazioni previste con gli utenti e permettendo di identificare e progettare i test case per ciascuno di questi scenari d’uso.

  Ad esempio, se il sistema deve elaborare una fattura strutturata e inserirla in un archivio ordinato per data, si devono eseguire diversi test per coprire i possibili casi. Supponendo che la fattura venga inserita in ordine di arrivo quando esistono più fatture con la stessa data, alcuni test di input-output potrebbero includere:

    - Fattura con data odierna
    - Fattura con data passata per cui esistono altre fatture
    - Fattura con data passata senza altre fatture presenti
    - Fattura il cui cliente non è stato ancora inserito in archivio

  Questi test verificano il comportamento esterno del sistema in condizioni realistiche senza necessità di accedere alla logica interna.

  **Tipi di testing in the large**:
  
  - **Test di modulo**: verifica se un modulo del sistema è stato implementato correttamente in base al suo comportamento esterno, garantendo che le funzioni fornite siano conformi alle specifiche.
  - **Test d’integrazione**: verifica come i vari moduli e sottosistemi interagiscono tra loro, simulando gli input dei moduli che alimentano il sottosistema in analisi. Il test d’integrazione è utile per:
    1. Anticipare la scoperta di errori già nelle fasi iniziali di sviluppo, riducendo il costo delle correzioni.
    2. Semplificare la ricerca degli errori circoscrivendoli a porzioni specifiche del sistema.
    3. Permettere il rilascio graduale di sottoparti autonome e funzionanti, migliorando la continuità operativa del progetto.
  - **Test di sistema**: verifica il comportamento dell’intero sistema in base alle specifiche esterne, accertando che tutti i moduli e componenti funzionino correttamente in sinergia e rispondano ai requisiti dell’applicazione completa.

### Analisi del Software

L'analisi di un software consiste nell’ispezionare il codice per comprenderne le caratteristiche e funzionalità, permettendo la verifica di un insieme di esecuzioni piuttosto che di singoli casi, come nel testing. Questo processo si basa su modelli della realtà e può essere applicato sia al codice che allo pseudocodice. Tuttavia, l’analisi è soggetta a errori interpretativi, derivanti dalla soggettività di chi la conduce. Esistono due principali metodi di analisi del codice: **Code walk-through** e **Code inspection**.

### Code Walk-Through

Il **code walk-through** è un’analisi informale condotta da un piccolo team (3-5 persone), che seleziona porzioni di codice specifiche e valori di input per simulare su carta il comportamento del programma. L'analisi, della durata di poche ore, mira esclusivamente a individuare problemi, senza includere i manager per mantenere un clima collaborativo. La documentazione del codice è fornita dal progettista in anticipo, e lo scopo è cercare eventuali errori senza necessariamente risolverli.

### Code Inspection

Nella **code inspection**, un team analizza specifiche classi di errori nel codice, verificando la presenza di problematiche come variabili non inizializzate, cicli infiniti, letture di dati non allocati e deallocazioni improprie di memoria. A differenza del walk-through, si cerca un tipo specifico di errore piuttosto che simulare esecuzioni generiche.

### Analisi del Flusso dei Dati

Un tipo specifico di code inspection è l’**analisi di flusso dei dati**, che si concentra sull’evoluzione dei valori associati alle variabili durante l'esecuzione del programma. Attraverso questo metodo, ogni comando viene categorizzato come:
- **Definizione (d)**: l’inizializzazione di una variabile.
- **Uso (u)**: la lettura del valore della variabile.
- **Annullamento (a)**: l’eliminazione del valore associato a una variabile.

L’analisi riduce sequenze di comandi a successioni di queste operazioni per ogni variabile, permettendo di identificare anomalie come l’uso di valori non definiti e definizioni non utilizzate. Per esempio, in una procedura `swap` che utilizza la variabile locale `x`, la sequenza risultante per `x` potrebbe essere **auu**, dove il valore viene usato senza essere definito in precedenza. Errori simili emergono quando sequenze di operazioni non seguono le regole.

### Esempio di Analisi di Flusso dei Dati

Consideriamo il seguente programma `swap`:

```plaintext
1. procedure swap(x1, x2: real)
2. var x: real;
3. begin
4. x2 := x;
5. x2 := x1;
6. x1 := x;
7. end;
```

La sequenza delle operazioni per `x` è `auu` (annullamento, uso, uso), evidenziando che `x` è utilizzata senza definizione previa. La sequenza per `x2` risulta `ddd`, indicando definizioni consecutive senza uso intermedio, che suggerisce un’assegnazione superflua.

### Regole Generali di Validità delle Sequenze di Flusso

Per prevenire anomalie, si applicano le seguenti regole generali:
1. **Uso preceduto da definizione**: ogni uso di una variabile deve essere preceduto da una sua definizione, senza annullamenti intermedi.
2. **Definizione seguita da uso**: ogni definizione deve essere seguita da un uso, prima di un’altra definizione o annullamento.

Sequenze come `aduduu` e `duadudu` rispettano queste regole, mentre `aduddu` e `dauduu` no, indicando la presenza di anomalie.

### Eccezioni nelle Sequenze di Flusso

Non tutte le sequenze apparentemente anomale indicano errori: ad esempio, una sequenza `au` potrebbe apparire in un generatore di numeri casuali, mentre una sequenza `dd` potrebbe essere giustificata da strutture programmatiche più complesse che usano lo stesso valore in diverse esecuzioni. 

Questa analisi approfondisce le relazioni tra i valori delle variabili e i comandi del programma, contribuendo all’identificazione di problemi di utilizzo delle variabili, a vantaggio della sicurezza e robustezza del codice.

## Certificazione

### Sistema di Controllo della Qualità in Europa

La Comunità Europea regola la qualità nei vari settori produttivi attraverso due classi di norme:

1. **Regole Tecniche**  
   Emanate da enti statali tramite leggi, decreti e regolamenti, queste norme sono obbligatorie e devono rispettare le direttive comunitarie.

2. **Norme Tecniche Consensuali**  
   Queste norme sono sviluppate da enti di normazione riconosciuti (nazionali come UNI e CEI, europei come EN, e internazionali come ISO e IEC) e coinvolgono rappresentanti governativi e industriali. La loro applicazione è facoltativa, salvo disposizioni legali che ne rendano obbligatoria l’adozione. Un esempio è la famiglia **ISO 9000**, destinata alla gestione e assicurazione della qualità.

### ISO 9000: Obiettivi Principali

La famiglia ISO 9000 comprende norme per:

- **Gestione della Qualità**  
  Fornisce una guida alle aziende per sviluppare o migliorare un sistema di qualità, con l'obiettivo di ottimizzare processi e attività aziendali.

- **Assicurazione della Qualità**  
  Stabilisce i requisiti per permettere ai clienti di valutare l’idoneità del sistema qualità del fornitore, in relazione alla capacità di soddisfare le esigenze stabilite.

### Certificazione e Accreditamento

- **Certificazione**  
   La certificazione è il riconoscimento ufficiale, rilasciato da un ente accreditato, che attesta la conformità di un prodotto, processo o sistema qualità ai requisiti di una specifica norma.

- **Accreditamento**  
   È il riconoscimento formale che un laboratorio o un organismo certificatore possiede la competenza necessaria per svolgere prove specifiche o certificazioni.

### Processo di Certificazione ISO 9000

La certificazione ISO 9000 può coprire intere aziende o solo alcune porzioni; l'estensione viene decisa dall'organismo di certificazione in accordo con l'azienda. Gli elementi e processi inclusi nella certificazione sono documentati nel **manuale qualità**, che descrive sia i processi soggetti al sistema di qualità sia la documentazione di supporto.

### Fasi della Certificazione

- **Verifica Ispettiva**  
   È una fase cruciale in cui i valutatori, sulla base del manuale qualità, visitano l'azienda e verificano l'applicazione delle procedure aziendali. Durante l’ispezione, vari responsabili aziendali (direzione, ufficio acquisti, laboratori, ecc.) vengono intervistati e le unità produttive vengono ispezionate.

- **Visite di Sorveglianza**  
   Dopo la certificazione, l’organismo effettua visite periodiche di controllo (da 1 a 4 volte l’anno) per assicurarsi che l’azienda continui a rispettare i requisiti.

![immagine locale](img\IDS\workflow_ISO_9000_certificazione.PNG)

### Non Conformità

La **non conformità** è definita come il "non soddisfacimento dei requisiti specificati" e può riferirsi alla mancanza di una caratteristica di qualità o di un elemento del sistema qualità. Durante le verifiche, le non conformità riscontrate si classificano in:

- **Non Conformità ai Requisiti della Norma**: requisiti della norma non rispettati.
- **Non Conformità Documentale**: mancanza di procedure documentate o non rispetto delle procedure formalizzate.
- **Non Conformità nell’Attuazione delle Procedure**: le procedure non sono applicate correttamente.

![immagine locale](img\IDS\documenti_progetto.PNG)

## Manutenzione Software

### Tipi di manutenzione
La manutenzione software comprende vari interventi per migliorare o adattare i sistemi, assicurandone la funzionalità e prolungandone il ciclo di vita. Le principali tipologie di manutenzione sono:

1. **Manutenzione Correttiva**
   - **Obiettivo**: Correggere malfunzionamenti derivanti da errori di analisi, progettazione, codifica e test.
   - **Cause**:
     - **Errori**: Derivano da attività umane e possono insorgere in qualsiasi fase dello sviluppo.
     - **Difetti**: Problemi nel programma che causano risultati errati.
     - **Malfunzionamenti**: Riguardano il sistema nel suo complesso, compromettendo funzionalità e affidabilità.
   - **Costi**: Elevati (fino al 40% dei costi di manutenzione), specialmente se i difetti non vengono risolti alla radice.
   - **Risultati**: Riduzione dell'affidabilità e aumento dell'entropia del programma, ma ripristino della qualità originaria.

2. **Manutenzione Adattiva**
   - **Obiettivo**: Mantenere inalterato il livello di servizio del sistema in risposta a mutamenti dell'ambiente operativo.
   - **Esempi**:
     - Aggiornamenti di calcoli per imposte e tariffe.
     - Modifiche nei listini prezzi.
   - **Costi**: Significativi (20-30%), spesso classificati come costi di sviluppo.
   - **Risultati**: Conservazione della qualità senza aumento del valore informativo del sistema.

3. **Manutenzione Perfettiva**
   - **Obiettivo**: Aumentare qualitativamente le funzionalità o le caratteristiche tecniche del sistema.
   - **Esempi**:
     - Ottimizzazione delle prestazioni.
     - Introduzione di nuove interfacce o funzionalità.
     - Modifiche strutturali.
   - **Costi**: Generalmente inclusi nei costi di sviluppo.
   - **Risultati**: Miglioramento del valore informativo e usabilità del sistema, ma con potenziale aumento della complessità e rischio di degradazione della qualità.

4. **Manutenzione Evolutiva**
   - **Obiettivo**: Migliorare qualitativamente e quantitativamente il sistema, adattandolo a nuove esigenze.
   - **Esempi**:
     - Aggiunta di funzioni avanzate.
     - Transizione a interfacce grafiche o a DBMS relazionali.
     - Potenziamento delle capacità di reporting.
   - **Costi**: Elevati e spesso occulti fino alla fase operativa.
   - **Risultati**: Maggiore potenza e funzionalità, ma anche aumento dell’entropia e rischio di riduzione della robustezza, a meno di un’attenta pianificazione.

### Manutenibilità del Sistema: L'Importanza dell'Architettura

La manutenibilità di un sistema è determinata dalla qualità della sua architettura originale, progettata per facilitare interventi successivi e adattamenti. Alcuni esempi includono:

- **Automobili**: Architettura modulare e smontabile per interventi facili, con funzioni stabili nel tempo.
- **Hi-Fi**: Struttura a moduli, ma con componenti strettamente integrati e difficilmente aggiornabili.
- **Case**: Architettura non modulare con elementi nascosti (tubi, cavi), progettate per un impianto fisso piuttosto che per frequenti modifiche.

Spesso i programmi software sono progettati come case (non modulari), ma devono essere manutenuti come automobili, rendendo essenziale un’architettura che ne faciliti l’adattamento e la lunga durata.

