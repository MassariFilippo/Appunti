<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });</script>

# Virtualizzazione e Integrazione di Sistemi

<div style="page-break-after: always;"></div>

- [Virtualizzazione e Integrazione di Sistemi](#virtualizzazione-e-integrazione-di-sistemi)
  - [La Figura del Systems Integrator](#la-figura-del-systems-integrator)
  - [Scenari di Integrazione](#scenari-di-integrazione)
    - [Integrazione col Mondo dell'Automazione](#integrazione-col-mondo-dellautomazione)
    - [Sistemi a Micro-Servizi](#sistemi-a-micro-servizi)
      - [Applicativi "Monolitici" e "a Micro-Servizi"](#applicativi-monolitici-e-a-micro-servizi)
      - [Esempio di Micro-Servizi in Cloud](#esempio-di-micro-servizi-in-cloud)
      - [Vantaggi dei Micro-Servizi](#vantaggi-dei-micro-servizi)
      - [Problematiche da Considerare](#problematiche-da-considerare)
      - [Progettazione delle Comunicazioni](#progettazione-delle-comunicazioni)
      - [Esempio di Comunicazioni Locali](#esempio-di-comunicazioni-locali)
      - [Problema di Comunicazione](#problema-di-comunicazione)
      - [Soluzione di Integrazione](#soluzione-di-integrazione)
      - [Bus di Messaggi (o Message Broker)](#bus-di-messaggi-o-message-broker)
    - [Sistemi a Micro-Servizi Dispiegati anche in Cloud](#sistemi-a-micro-servizi-dispiegati-anche-in-cloud)
    - [Sistema a Micro-Servizi Principalmente in Cloud](#sistema-a-micro-servizi-principalmente-in-cloud)
      - [Sicurezza nei Sistemi Informatici](#sicurezza-nei-sistemi-informatici)
    - [Directory Service](#directory-service)
      - [Scenario di Integrazione con Autenticazione e Autorizzazione Centralizzate](#scenario-di-integrazione-con-autenticazione-e-autorizzazione-centralizzate)


<div style="page-break-after: always;"></div>

## La Figura del Systems Integrator

- Il termine "sistemista" è obsoleto. Aveva senso quando si trattava di gestire batterie di singoli computer.
- Oggi, il "sistemista" deve progettare e realizzare infrastrutture software per gestire, a livelli architetturali diversi, una molteplicità di entità differenziate che interagiscono continuamente.
- Il termine più corretto per individuare l'attività del sistemista moderno è "Systems Integration and Testing".
- La figura professionale viene definita dall'EUCIP nel seguente documento: [EUCIP Systems Integration and Testing Engineer](http://www.eucip.it/profili/profili-professionali/SystemsIntegrationandTestingEngineerVersion2.4.pdf).
- I numerosi task della figura professionale originano dalla seguente responsabilità di massima:  
  "The Systems Integration and Testing Engineer works within organizations (either as an employee or as an external provider) to ensure that software systems and components are successfully integrated across hardware systems and meet specified requirements."
- Tra le competenze richieste si distingue la conoscenza degli standard software de jure e de facto:  
  "Requirements include a specific knowledge on how interfaces between software modules are built."
- In alcuni casi, si distingue la figura dell'installatore/configuratore/manutentore di sistemi rispetto alla figura del designer di sistemi complessi.
- La figura del Systems Integration Architect si occupa principalmente della progettazione delle infrastrutture software per gestire, a livelli architetturali diversi, una molteplicità di entità differenziate che interagiscono continuamente.
- La realizzazione, installazione e manutenzione è lasciata al Systems Integrator.

Il Systems Integrator deve:
- Progettare e realizzare sistemi complessi,
- Costituiti da molteplici componenti,
- Che interagiscono via rete,
- Mediante interfacce standard.

Egli necessita di competenze che spaziano in molti ambiti dell'informatica, in particolare di conoscenze riguardanti:
- Protocolli di rete.
- Sicurezza nei sistemi di rete.
- Programmazione e scripting.
- IDM (Identity Management Systems, Sistemi di Gestione dell'Identità).
- Sistemi di Provisioning.
- Architetture a MicroServizi e sviluppo.
- Gestione centralizzata di servizi distribuiti.
- Sistemi per Virtualizzazione.
- Amministrazione di specifici sistemi operativi per desktop e server.
- Amministrazione di sistemi cloud privati.

## Scenari di Integrazione
Progettare soluzioni aderendo agli standard (de jure e de facto):
1. Integrazione col mondo dell'automazione.
2. Applicazioni monolitiche vs. Sistemi a micro-servizi.
3. Sistemi a micro-servizi in cloud.
4. Sicurezza.
5. Identity and Access Management (IAM) Directory Service.
6. Dispiegamento (deployment) scalabile mediante virtualizzazione e container.
7. Scenari di rete e ostacoli (firewall).

### Integrazione col Mondo dell'Automazione

- Le macchine automatiche, anche di grandi dimensioni, sono controllate da sistemi che non sono computer, ma PLC.
- L'integrazione con il resto del mondo (Industria 4.0) concerne spesso l'esportazione in tempo reale di dati dai sensori della macchina, su cui si opera con vari sistemi di analisi, big data e intelligenza artificiale. Anche flussi da videocamere sono spesso utilizzati.
- L'integrazione richiede la conoscenza di protocolli di comunicazione specifici per l'ambiente dell'automazione e i meccanismi di sicurezza.
- La gestione di queste macchine, data l'importanza produttiva in ralazione a i costi e tempi di intervento in caso di rottuta, si è orientata fortemente alla manutenzione predittiva per contenere le perdite in caso di rotture non previste.

### Sistemi a Micro-Servizi

#### Applicativi "Monolitici" e "a Micro-Servizi"

Avete sempre visto un'applicazione costituita da un solo pezzo o, al massimo, da due. Si può trattare di un'applicazione in Java, di un servizio web, o di un servizio web combinato con il tier del database, che sono indissolubili. In realtà, gli applicativi moderni nel mondo reale sono costituiti da molteplici componenti separati e personalizzabili, detti micro-servizi, che possono essere eseguiti su uno stesso host oppure su più host distribuiti in rete. Questi componenti interagiscono tra loro scambiandosi messaggi mediante interfacce software e protocolli standard, consentendo il riutilizzo del software. Un'applicazione a micro-servizi lavora, dunque, per moduli disgiunti, più o meno complessi, che comunicano tramite API, in modo tale che i componenti possano essere standardizzati, duplicati a run-time, personalizzati e debuggati singolarmente, anche a run-time aumentando notevolmente la scalabilità e il riuso, inooltre lavorando per api non dovrò interrompere il macro servizio per apportare modifiche al micro. In ultima istanza potrò costantemente monitorare il sistema via codice verificando la saturazione del sistema ed allocando nuove risorse o sostituuendo componenti software che via vai potrebbero andare in down.

#### Esempio di Micro-Servizi in Cloud

Quando parliamo di micro-servizi nel contesto del cloud, un esempio significativo è rappresentato da Microsoft Azure. È importante notare che non tutti i prodotti disponibili su questa piattaforma sono sviluppati da Microsoft; alcuni sono open-source e possono essere installati su macchine virtuali nel cloud.

Le macchine virtuali (VM) possono essere configurate in base alle esigenze specifiche, scegliendo il sistema operativo, la potenza della CPU, la quantità di memoria RAM e lo spazio su disco. Inoltre, il disco virtuale è accessibile da tutte le VM, facilitando la gestione dei dati. Per le esigenze di archiviazione, Azure offre Archive Storage, una soluzione a basso costo per dati che vengono acceduti raramente.

Per quanto riguarda i database, Azure supporta diverse istanze, tra cui database relazionali come MySQL e database documentali come MongoDB. Inoltre, è possibile utilizzare Microsoft Azure CosmosDB, che offre più tipi di API di accesso, sia documentali che relazionali.

Un altro aspetto interessante è la presenza di un distributore di carico web, che consente di gestire picchi di traffico creando nuove VM in tempo reale, il tutto configurabile attraverso regole specifiche utilizzando Kubernetes. Azure offre anche servizi come VPN gateway, DNS, Content Delivery Network, Stream Analytics e Machine Learning, oltre a strumenti per la gestione dell'identità come Active Directory e Multi-factor Authentication. Un secondo tipo di distrubuzione è quello di natura Content Delivery Network ovvero distrubuzione di media come audio o video, qui in focus è concetrato non solo sull'architettura software ma ache sull'infrastruttura hardware ed un uso intelligente di quest'ultima.

Un esempio di integrazione è rappresentato da Microsoft Azure IoT Hub, un gateway centralizzato per la gestione dei messaggi provenienti da vari sensori, utilizzando protocolli come AMQP, MQTT e HTTPS. Inoltre, RabbitMQ è un bus di messaggi che supporta i protocolli AMQP e MQTT, ed è progettato per funzionare in locale ma può essere dispiegato anche su macchine virtuali. CloudAMQP, invece, è una versione di RabbitMQ disponibile in cloud, accessibile anche da fonti esterne.

#### Vantaggi dei Micro-Servizi

La struttura degli applicativi basati su micro-servizi è composta da numerosi componenti disaccoppiati, distribuiti su diversi host o datacenter. Questo approccio consente di considerare l'applicazione nel suo complesso come un sistema integrato. La scomposizione in micro-servizi offre diversi vantaggi:

- **Riusabilità:** I micro-servizi possono essere riutilizzati in diversi applicativi, aumentando l'efficienza dello sviluppo.
- **Scalabilità:** Solo i micro-servizi che necessitano di essere replicati e bilanciati vengono gestiti, ottimizzando l'uso delle risorse.
- **Deployment:** I micro-servizi possono essere distribuiti su una singola macchina o su più macchine, con la possibilità di riconfigurare i servizi di comunicazione per adattarsi a indirizzi diversi, tenendo conto della presenza di firewall e della sicurezza.
- **Cloud:** I micro-servizi sono particolarmente adatti per lo sviluppo di applicativi progettati per il cloud computing, poiché i provider cloud offrono principalmente soluzioni basate su micro-servizi.

#### Problematiche da Considerare

Tuttavia, la necessità di comunicazione tra i micro-servizi presenta alcune sfide. È fondamentale:

- Creare micro-servizi che espongano solo interfacce software e protocolli di comunicazione ampiamente condivisi (standard de facto).
- Progettare le applicazioni in modo che utilizzino esclusivamente questi standard.
- Garantire che la rete di comunicazione consenta il passaggio dei messaggi, oppure implementare infrastrutture e servizi adeguati per superare firewall e NAT.

#### Progettazione delle Comunicazioni

Un aspetto cruciale nella progettazione di un sistema a micro-servizi è la definizione delle comunicazioni tra i vari componenti. È necessario individuare i protocolli di comunicazione standard più adatti allo scenario specifico, scegliendo tra quelli che hanno implementazioni mature e ampiamente diffuse.

#### Esempio di Comunicazioni Locali

Anche un'applicazione che opera su un singolo host può necessitare di comunicare tra diversi micro-servizi. Immaginiamo un'applicazione web in cui gli utenti, tramite un browser, visualizzano le statistiche sui pezzi prodotti da una macchina automatica. Questa applicazione è realizzata utilizzando tecnologie come Nginx, Node.js e Puma, e funziona all'interno di container su un server Linux situato nello stesso stabilimento della macchina.

Gli utenti sono serviti attraverso connessioni persistenti HTML5, con un'istanza del back-end web dedicata a ciascun utente. La macchina automatica, che non è un computer ma un PLC, invia informazioni sui pezzi prodotti al server utilizzando il protocollo standard OPC-UA. Il server gestisce due database: uno relazionale (MySQL) e uno documentale (MongoDB) ovvero DB in cui salviamo dati eterogenei non adatti ad un immagazzinamento tabellare.

Un servizio separato, chiamato OPC client, riceve i dati dalla macchina, li inserisce nel database documentale e aggiorna le statistiche nel database relazionale. Dopo ogni inserimento, l'OPC client informa tutte le istanze del back-end web, che stanno servendo gli utenti, di aggiornare i grafici visualizzati, poiché sono disponibili nuovi dati. Inoltre, un altro software monitora la raggiungibilità di un magazzino e, in caso di problemi, invia notifiche agli utenti connessi al servizio web.

#### Problema di Comunicazione

Una delle sfide principali è come gestire le comunicazioni locali in un contesto "molti a molti", specialmente quando non si conosce a run-time chi siano e quanti siano questi "molti".

![](img/Virtualizzazione/ProbCom.png)

#### Soluzione di Integrazione

Per affrontare questa problematica, si può implementare un bus di messaggi di tipo publish/subscribe orientato ai topic. In questo sistema, ogni entità ricevente si registra e indica a quali topic è interessata. Chi desidera inviare un messaggio pubblica il messaggio stesso, specificando un subject. Il messaggio viene quindi consegnato a tutte le entità che hanno manifestato interesse per quel subject.

![](img/Virtualizzazione/SolCom.png)

#### Bus di Messaggi (o Message Broker)

I bus di messaggi, noti anche come Message Bus o Message Broker, utilizzano diversi protocolli per lo scambio di messaggi. Tra i più comuni ci sono AMQP e MQTT. Questi protocolli definiscono il formato base dei messaggi, che include un body, e offrono diverse modalità di consegna (affidabile, non affidabile, con ricevuta di consegna, ecc.). Inoltre, mantengono i messaggi in code secondo politiche di consegna specifiche e forniscono API per vari linguaggi e sistemi operativi come per esempio time out sul numero di messaggi in coda o TTL.

Le applicazioni di solito sviluppano un proprio strato software per definire il formato interno dei messaggi, spesso optando per un body in formato JSON per semplificare il processo.

Tra le implementazioni più diffuse di bus di messaggi troviamo RabbitMQ, un sistema open-source che supporta sia AMQP che MQTT e può essere installato su vari sistemi operativi. RabbitMQ è in grado di far comunicare entità su macchine fisiche diverse, inclusi ambienti cloud. Esiste anche un servizio pre-installato in cloud, CloudAMQP, accessibile tramite API.

Un altro esempio è Microsoft Azure Service Bus Messaging, che opera nei datacenter di Microsoft Azure, supporta AMQP e MQTT, e offre API per entità che operano su host esterni al cloud, garantendo livelli di sicurezza adeguati.

Va considerato che questi strumenti ovviamenete introducono un ritardo di comunicazione ma contengono decisamente la complessità della comuczionine molti a molti con actor dinamici.

![](img/Virtualizzazione/SolCom2.png)

### Sistemi a Micro-Servizi Dispiegati anche in Cloud

I sistemi a micro-servizi possono essere implementati in modo parziale o completo su infrastrutture cloud. Tuttavia, è raro che un sistema operi esclusivamente in cloud. Infatti, i dati grezzi su cui si basa il sistema sono spesso generati da una varietà di sorgenti distribuite geograficamente, come utenti, dispositivi indossabili, sensori, macchinari e automobili. Questi dati vengono poi raccolti e inviati al cloud per ulteriori elaborazioni.

Di conseguenza, la fase di acquisizione dei dati di solito richiede l'esecuzione di procedure su dispositivi esterni al cloud. I sistemi cloud più avanzati facilitano questa fase di acquisizione, offrendo API e librerie che possono essere eseguite su questi dispositivi esterni. Le fasi successive di elaborazione dei dati, invece, vengono tipicamente gestite nel cloud.

Prendiamo ad esempio un macchinario che produce pezzi in uno stabilimento. Questo macchinario invia statistiche a un server che, in questo caso, non si trova nello stabilimento stesso, ma in un datacenter cloud. Immaginiamo che ci siano molte macchine automatiche in stabilimenti diversi, tutte inviate a questo server cloud. Gli stabilimenti e le macchine potrebbero appartenere a proprietari diversi, mentre il servizio cloud potrebbe essere gestito dal produttore delle macchine. In questo scenario, è fondamentale distinguere i permessi di accesso degli utenti alle informazioni collocate nel cloud, in base alle diverse macchine e alle loro anagrafiche.

### Sistema a Micro-Servizi Principalmente in Cloud

Parliamo di sistemi che controllano dispositivi sparsi per il mondo con numero di client numerosi e risosrse centrali limitate, è inoltre da considerare plausibile che queste macchine comunichino con protocolli diversi e sono gestite da utenti con dipositivi eterogenei, se a questo introduciamo anche propietari diversi la comolessità del sistema risente anche di problemi di tutela dei dati che vanno a rendere il sistema ancor più complesso. 

Per integrare con questi sistemi, possiamo utilizzare una soluzione basata su container Docker, che consente di gestire i micro-servizi in modo efficiente senza dover necessariamente incrementare le risorse hardware a nostra disposizione. I componenti del sistema possono comunicare tra loro attraverso un bus di messaggi, utilizzando protocolli come MQTT. Il server web gestisce le richieste degli utenti, mentre i dati vengono archiviati in database come MySQL e Azure Cosmos DB, che supportano API MongoDB. Inoltre, Azure File Storage e IoT Hub possono essere utilizzati per gestire i dati provenienti dai dispositivi.

In questo contesto, i PLC (Programmable Logic Controllers) delle macchine automatiche inviano dati al server, e gli utenti possono accedere a queste informazioni tramite un'interfaccia web. Un bilanciatore di carico (Load Balancer) e Kubernetes possono essere utilizzati per gestire i container e garantire che il sistema rimanga scalabile e reattivo.

#### Sicurezza nei Sistemi Informatici

La sicurezza è un criterio fondamentale nella progettazione di qualsiasi sistema informatico e non deve essere considerata un aspetto secondario. Spesso, un requisito di progettazione è la centralizzazione delle funzionalità di autenticazione e autorizzazione in un servizio unico. Questa centralizzazione non solo semplifica la gestione, ma rappresenta anche un fattore di sicurezza, poiché limita i punti di attacco e facilita il controllo.

I servizi di directory sono responsabili dell'autenticazione e dell'autorizzazione, e ci sono innumerevoli scenari in cui la sicurezza influisce sulla progettazione dei sistemi. Alcuni aspetti chiave della sicurezza includono:

- **Sicurezza nei mezzi trasmissivi:** Utilizzo di canali wireless, comunicazioni applicative sicure (HTTPS, SSL/TLS) e reti private virtuali (VPN).
- **Autenticazione delle entità:** Utilizzo di certificati X.509.
- **Autenticazione degli utenti:** Implementazione di sistemi di autenticazione multi-fattore.
- **Autorizzazione all'accesso alle risorse:** Gestione delle infrastrutture, dei servizi di directory, dei domini e del DNS.

### Directory Service

Un Directory Service è un sistema centralizzato per la gestione e la fruizione delle informazioni relative a utenti, reti, servizi e applicazioni all'interno di un dominio. In uno scenario di integrazione con autenticazione e autorizzazione centralizzate, il processo di autenticazione avviene attraverso un access token, che fornisce l'identità dell'utente e le impostazioni di sicurezza necessarie per accedere alle risorse e svolgere compiti nel sistema.

Il processo di autenticazione prevede che l'utente fornisca un nome utente e una password. Il sistema operativo confronta queste informazioni con quelle memorizzate nel database appropriato. Se le informazioni corrispondono e l'account utente è abilitato, viene creato un access token per l'utente. In caso contrario, l'accesso al dominio o al computer locale viene negato.

#### Scenario di Integrazione con Autenticazione e Autorizzazione Centralizzate

Un esempio pratico di Directory Service è rappresentato dai laboratori e dai computer del personale amministrativo dell'Università di Bologna (Unibo). Qui, è stato implementato un sistema centralizzato di autenticazione e autorizzazione che utilizza Microsoft Active Directory, distribuito su sistemi Windows Server 2008. Questo sistema gestisce le responsabilità e le funzionalità su cinque campus, distinguendo tra i domini interni unibo.it e studio.unibo.it.

I PC degli studenti appartengono al dominio "studio.unibo.it" e gli studenti si autenticano presso server localizzati nei campus. Possono accedere a servizi condivisi, come file system remoti, forniti da sistemi Windows o Linux attraverso protocolli standard come SMB, CIFS e Samba. Le politiche di sicurezza sono centralizzate, consentendo un join immediato per i PC Windows, mentre i PC Linux utilizzano applicativi e protocolli come LDAP e Samba per accedere alle risorse. È anche possibile avere server basati su Linux (utilizzando applicativi della suite Samba, informalmente noti come Linux Active Directory) e client Windows.