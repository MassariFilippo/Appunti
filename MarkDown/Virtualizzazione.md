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
    - [Sistema a Micro-Servizi Principalmente in Cloud](#sistema-a-micro-servizi-principalmente-in-cloud)
      - [Sicurezza nei Sistemi Informatici](#sicurezza-nei-sistemi-informatici)
    - [Directory Service](#directory-service)
      - [Autenticazione in Canali Wireless](#autenticazione-in-canali-wireless)
      - [Autorizzazione all'Uso di Applicazioni (Single Sign-On)](#autorizzazione-alluso-di-applicazioni-single-sign-on)
    - [Dispiegamento di Servizi Scalabili e Isolati mediante Virtualizzazione e Containerizzazione](#dispiegamento-di-servizi-scalabili-e-isolati-mediante-virtualizzazione-e-containerizzazione)
      - [Virtualizzazione](#virtualizzazione)
      - [Containerizzazione](#containerizzazione)
      - [Container vs. Virtual Machine](#container-vs-virtual-machine)
      - [Cloud e Categorie di Servizi Cloud](#cloud-e-categorie-di-servizi-cloud)
      - [PaaS vs. IaaS](#paas-vs-iaas)
      - [Piattaforme di Gestione di Cloud Privati](#piattaforme-di-gestione-di-cloud-privati)
      - [Multitenancy](#multitenancy)
    - [Progettazione delle Comunicazioni in Reti Protette da NAT e Firewall](#progettazione-delle-comunicazioni-in-reti-protette-da-nat-e-firewall)
      - [Virtual Private Network (VPN)](#virtual-private-network-vpn)
      - [Esposizione di Porte Remote mediante SSH Remote Port Forwarding](#esposizione-di-porte-remote-mediante-ssh-remote-port-forwarding)
  - [Sincronizzazione degli Orologi](#sincronizzazione-degli-orologi)
    - [Importanza della Sincronizzazione nella Sicurezza](#importanza-della-sincronizzazione-nella-sicurezza)
    - [Tipi di Clock](#tipi-di-clock)
    - [Meccanismi di Sincronizzazione](#meccanismi-di-sincronizzazione)
    - [Meccanismo Three-Way di Sincronizzazione](#meccanismo-three-way-di-sincronizzazione)
    - [Problemi e Limitazioni](#problemi-e-limitazioni)
    - [Sincronizzazione dei Clock Fisici](#sincronizzazione-dei-clock-fisici)
    - [Sincronizzazione Esterna dei Clock Fisici](#sincronizzazione-esterna-dei-clock-fisici)
    - [NTP (Network Time Protocol)](#ntp-network-time-protocol)
  - [Crittografia](#crittografia)
    - [Crittografia a Chiave Segreta (Simmetrica)](#crittografia-a-chiave-segreta-simmetrica)
    - [Crittografia a Chiave Pubblica (Asimmetrica)](#crittografia-a-chiave-pubblica-asimmetrica)
    - [Funzioni Hash Crittografiche](#funzioni-hash-crittografiche)
    - [Integrità di Messaggi e Firma Digitale](#integrità-di-messaggi-e-firma-digitale)
    - [Ricezione del Messaggio con MAC](#ricezione-del-messaggio-con-mac)
    - [Crittografia a Chiave Segreta vs. Crittografia a Chiave Pubblica](#crittografia-a-chiave-segreta-vs-crittografia-a-chiave-pubblica)
  - [Kerberos](#kerberos)
    - [Strategie di Kerberos](#strategie-di-kerberos)
    - [Requisiti di Tempo in Kerberos](#requisiti-di-tempo-in-kerberos)
    - [Applicabilità di Kerberos](#applicabilità-di-kerberos)


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

### Sistema a Micro-Servizi Principalmente in Cloud

Parliamo di sistemi che controllano dispositivi distribuiti a livello globale, caratterizzati da un elevato numero di client e risorse centrali limitate. È plausibile che queste macchine comunichino utilizzando protocolli diversi e siano gestite da utenti con dispositivi eterogenei. Inoltre, la presenza di proprietari diversi aumenta la complessità del sistema, rendendo necessaria una particolare attenzione alla tutela dei dati.

Per integrare questi sistemi, possiamo adottare una soluzione basata su container Docker, che consente di gestire i micro-servizi in modo efficiente senza dover necessariamente aumentare le risorse hardware disponibili. I componenti del sistema possono comunicare tra loro attraverso un bus di messaggi, utilizzando protocolli come MQTT. Il server web gestisce le richieste degli utenti, mentre i dati vengono archiviati in database come MySQL e Azure Cosmos DB, che supportano API MongoDB. Azure File Storage e IoT Hub possono essere utilizzati per gestire i dati provenienti dai dispositivi.

In questo contesto, i PLC (Programmable Logic Controllers) delle macchine automatiche inviano dati al server, e gli utenti possono accedere a queste informazioni tramite un'interfaccia web. Un bilanciatore di carico (Load Balancer) e Kubernetes possono essere impiegati per gestire i container, garantendo che il sistema rimanga scalabile e reattivo.

È necessario introdurre nuove componenti per offrire servizi a interfacce e gestire i componenti cloud dinamici. L'IoT Hub funge da interfaccia di comunicazione con le macchine automatiche, che operano con logiche implementative e protocolli di comunicazione eterogenei. Questo componente si interfaccia con un host del sito produttivo, evitando di esporre le macchine al pubblico e gestendo la loro comunicazione interna, che spesso non è complessa.

Il Load Balancer, responsabile dell'interfaccia con gli utenti, smista il traffico e tiene traccia delle richieste per istanziare o eliminare i container Docker quando necessario. È fondamentale garantire la sicurezza delle comunicazioni, spesso realizzata tramite certificati predefiniti con scadenze stabilite.

![](img/Virtualizzazione/ArchitetturaIotCloud.png)

#### Sicurezza nei Sistemi Informatici

La sicurezza è un criterio fondamentale nella progettazione di qualsiasi sistema informatico e non deve essere considerata un aspetto secondario. Spesso, un requisito di progettazione è la centralizzazione delle funzionalità di autenticazione e autorizzazione in un servizio unico. Questa centralizzazione non solo semplifica la gestione, ma rappresenta anche un fattore di sicurezza, poiché limita i punti di attacco e facilita il controllo.

I servizi di directory sono responsabili dell'autenticazione e dell'autorizzazione, e ci sono innumerevoli scenari in cui la sicurezza influisce sulla progettazione dei sistemi. Alcuni aspetti chiave della sicurezza includono:

- **Sicurezza nei mezzi trasmissivi:** Utilizzo di canali wireless (server Radius), comunicazioni applicative sicure (HTTPS, SSL/TLS) e reti private virtuali (VPN).
- **Autenticazione delle entità:** Utilizzo di certificati X.509.
- **Autenticazione degli utenti:** Implementazione di sistemi di autenticazione multi-fattore.
- **Autorizzazione all'accesso alle risorse:** Gestione delle infrastrutture, dei servizi di directory, dei domini e del DNS.

### Directory Service

Un Directory Service è un sistema centralizzato progettato per la gestione e la fruizione delle informazioni relative a utenti, reti, servizi e applicazioni all'interno di un dominio. In uno scenario di integrazione con autenticazione e autorizzazione centralizzate, il processo di autenticazione avviene tramite un access token, che fornisce l'identità dell'utente e le impostazioni di sicurezza necessarie per accedere alle risorse e svolgere compiti nel sistema.

Il processo di autenticazione inizia quando l'utente fornisce un nome utente e una password. Il sistema confronta queste informazioni con quelle memorizzate nel database appropriato. Se le informazioni corrispondono e l'account utente è abilitato, viene creato un access token per l'utente, che include i diritti di utilizzo. In caso contrario, l'accesso al dominio o al computer locale viene negato. 

Questo servizio prevede dunque che si salvino i dati di configurazione delle macchine della rete, questo sistema permentte di asseganre routine di gestione ed esecuzione legate a specifiche situazioni con il grande vantaggio di poter apportare modifiche per macro gruppi in maniera centralizzata per tutte la macchine che fanno parte del dominio attraverso un certificato datogli durante il join fatto tra macchian e dominio.

Un esempio pratico di Directory Service è rappresentato dai laboratori e dai computer del personale amministrativo dell'Università di Bologna (Unibo). Qui è stato implementato un sistema centralizzato di autenticazione e autorizzazione che utilizza **Microsoft Active Directory**, distribuito su sistemi Windows Server 2008, sui sistemi Linux trovaimo il fratello quasi equivalente **Samba**. Questo sistema gestisce le responsabilità e le funzionalità su cinque campus, distinguendo tra i domini interni unibo.it e studio.unibo.it.

I PC degli studenti appartengono al dominio "studio.unibo.it" e gli studenti si autenticano presso server localizzati nei campus. Possono accedere a servizi condivisi, come file system remoti, forniti da sistemi Windows o Linux attraverso protocolli standard come SMB, CIFS e Samba. Le politiche di sicurezza sono centralizzate, consentendo un join immediato per i PC Windows, mentre i PC Linux utilizzano applicativi e protocolli come LDAP e Samba per accedere alle risorse. È anche possibile avere server basati su Linux, utilizzando applicativi della suite Samba, informalmente noti come Linux Active Directory, e client Windows.

#### Autenticazione in Canali Wireless

Per l'autenticazione nell'accesso a punti di accesso WiFi e alle reti retrostanti, si utilizza un server RADIUS data la sua capacità di interfacciarsi con una grande varietà di protocolli anche molto datati, in conformità con gli standard WPA2 e 802.1x. Lo standard WPA2 per la sicurezza nelle reti wireless prevede l'uso di 802.1x per gestire l'autenticazione, offrendo ottima sicurezza e grande flessibilità, poiché consente di gestire vari metodi di autenticazione.

IEEE 802.1x è uno standard per l'autenticazione e l'autorizzazione in rete, sviluppato inizialmente per reti cablate, e si basa sul protocollo EAP (Extensible Authentication Protocol) per l'autenticazione. Questo standard prevede tre entità principali:
- **Authenticator:** richiede l'autenticazione prima di offrire il servizio (è l'access point).
- **Supplicant:** desidera accedere al servizio e deve essere autenticato (è il terminale wireless).
- **Authentication Server:** verifica le credenziali del supplicant a nome dell'authenticator (nel nostro caso, il server RADIUS).

L'autenticazione avviene tramite il protocollo EAP, che consente di negoziare diversi metodi di autenticazione, tra cui EAP-MD5, EAP-TLS, EAP-TTLS e PEAP. Durante il processo di autenticazione, l'authenticator ha un ruolo passivo, occupandosi solo di ricevere i messaggi dal supplicant, contenuti nel protocollo EAP, e di inoltrarli al server RADIUS, e viceversa.

![](img/Virtualizzazione/AutenticazioneRadius.png)

#### Autorizzazione all'Uso di Applicazioni (Single Sign-On)

Il **Single Sign-On (SSO)** è un meccanismo che consente a un utente di accedere a più applicazioni con una sola richiesta di credenziali, l'iserimento di crdenziali molteplici volte va non solo ad interrompere il flusso lavorativo ma ci espone anche a livello di sicurezza. L'implementazione del SSO può variare a seconda di diversi fattori, tra cui la posizione del computer dell'utente (se si trova nello stesso dominio dei server delle applicazioni o meno), il sistema operativo in uso (Microsoft o altro) e se le applicazioni sono basate su web.

Tra i sistemi di SSO per **servizi web**, uno dei più utilizzati è **Shibboleth**, anche se negli anni ha preso piede **OpenAutentication (O-Aut)**. Il SSO consente l'autorizzazione all'uso di più applicazioni con una sola richiesta di credenziali utente, basandosi su protocolli come Kerberos e marche temporali. **Shibboleth** si basa su HTTP POST e su SAML v2.0 (Security Assertion Markup Language). Questo sistema consente di gestire l'autenticazione degli utenti attraverso diversi web server e applicazioni, semplificando l'accesso e migliorando l'esperienza utente grazie all'utilizzo di token rinnovabili. L'**Identity and Access Management (IAM)** contiene parte della librera Shibboleth, implementazione di u **SAML v2.0 (Security Assertion Markup Language)**, che viene posta in cumunicazione con la restate parte della libreria contenuta nel web-server.

![](img/Virtualizzazione/SsoShibboleth.png)

Per servizi **non web-based** si utilizza **Kerberos**, specialmente in contesti in cui le macchine operano tutte sulla stessa rete, dove è possibile assumere un livello di sicurezza maggiore. Nonostante Kerberos presenti alcune vulnerabilità (ad esempio, la possibilità che script richiedano o trasportino credenziali in chiaro), il suo utilizzo risulta accettabile se il dominio di applicazione è strettamente controllato. Questo sistema si basa su scadenze (**marche temporali**) temporali che richiedono una sincronia tra tutte le macchine non capillare al microsecondo ma sufficiente a garantire il servizio.

![](img/Virtualizzazione/SsoKerberos.png)

### Dispiegamento di Servizi Scalabili e Isolati mediante Virtualizzazione e Containerizzazione

Di seguito il testo riorganizzato, corretto e con le parole importanti evidenziate:

#### Virtualizzazione

La **virtualizzazione** è il processo di creazione di una rappresentazione virtuale, basata su software, di risorse fisiche. Questa tecnologia consente di virtualizzare applicazioni, server, storage e reti. In particolare, la virtualizzazione del server permette di eseguire un **sistema operativo** isolato all'interno di una **macchina virtuale (VM)**, che non è fisica ma viene realizzata tramite uno strato software chiamato **Virtual Machine Monitor** o **Hypervisor**.

Esistono diversi modi per realizzare la virtualizzazione del server, distinti in base a vari fattori:

- **Livello di esecuzione:** Gli hypervisor possono operare a livello **hardware** o **software**, sfruttando le funzionalità offerte da un eventuale sistema operativo sottostante. Se l'hypervisor si appoggia direttamente sull'hardware, esso può svolgere anche compiti tipici del sistema operativo, fornendo un'interfaccia trasparente. La differenza risiede nelle funzionalità aggiuntive eventualmente offerte dall'hypervisor.

- **Funzionalità fornite:** Gli hypervisor possono fornire le stesse funzionalità dell'hardware o funzionalità diverse. Nel secondo caso, è necessario modificare il sistema operativo ospitato per adeguarlo alle nuove capacità.

- **Modalità di esecuzione:** Le modalità con cui vengono eseguite le istruzioni del sistema operativo ospitato possono variare, influenzando l'efficienza e l'isolamento dell'ambiente virtuale.

La virtualizzazione offre il vantaggio di **isolamento**, in quanto consente di eseguire un'applicazione all'interno del sistema operativo della macchina virtuale in maniera indipendente dalle altre applicazioni. Tuttavia, presenta anche alcuni svantaggi, quali la necessità di eseguire l'intero sistema operativo all'interno della VM per isolare ed eseguire una specifica applicazione e la dipendenza dell'applicazione dalla versione, configurazione e dai software presenti nel sistema operativo ospitato.

#### Containerizzazione

La tecnologia dei container sposta l'attenzione dalla virtualizzazione del server alla virtualizzazione dell'applicazione. I container creano un **contesto di esecuzione virtualizzato** per le applicazioni, senza dover virtualizzare l'intero server (hardware e sistema operativo), usa dunque il **Kernel** del SO sottostante. I container realizzano un sottoinsieme delle risorse offerte da un sistema operativo e mettono a disposizione queste risorse alle applicazioni eseguite al loro interno.

I container isolano ulteriormente le applicazioni all'interno del sistema operativo ospitato, astrando in parte dal sistema operativo e dalla macchina virtuale in cui gira. Questo approccio rende l'applicazione dipendente dal container, ma non dalla versione e configurazione del sistema operativo ospitato nella macchina virtuale. È importante notare che i container sfruttano pesantemente il sistema operativo sottostante, riutilizzando la maggior parte delle sue funzionalità per minimizzare il peso del container e rendere più agile la sua esecuzione.

#### Container vs. Virtual Machine

Un'applicazione può essere inserita in un container all'interno di un sistema operativo oppure sopra un sistema operativo all'interno di una macchina virtuale. 

![](img/Virtualizzazione/containerVSvm.png)

Il cambio di contesto da VM a VM è estrmamente più pesante che quello da processo a processo, ben più leggero invece è il passaggio da container a container.

#### Cloud e Categorie di Servizi Cloud

Il cloud di un provider è essenzialmente un insieme di datacenter, ognuno dei quali fornisce micro-servizi. I micro-servizi più essenziali consistono in macchine virtuali, per le quali è possibile richiedere specifiche tipologie di CPU, caratteristiche hardware, quantità di memoria e spazio su disco. Su queste basi vengono poi costruiti micro-servizi più complessi, alcuni dei quali consentono di gestire la ridondanza dei dati e il recupero da guasti verso altri datacenter.

I servizi cloud si distinguono per il livello di componibilità e per la capacità di scalare in modo trasparente per l'utente. Possiamo classificare i servizi cloud in tre categorie principali:

- **SaaS (Software as a Service):** Un servizio applicativo che non richiede all'utente di conoscere né il sistema operativo né l'host su cui opera. Un esempio è Google Documents, dove gli utenti possono modificare documenti senza preoccuparsi dell'infrastruttura sottostante.
  
- **PaaS (Platform as a Service):** Fornisce API di sviluppo per comporre servizi più complessi, senza che l'utente debba preoccuparsi del sistema operativo o dell'host. Un esempio è CosmosDB, un database scalabile in modo trasparente.

- **IaaS (Infrastructure as a Service):** Fornisce un'infrastruttura su cui installare servizi, come macchine virtuali e connessioni di rete. In questo caso, la scalabilità deve essere gestita aumentando la potenza o il numero delle istanze.

#### PaaS vs. IaaS

Per chiarire la differenza tra PaaS e IaaS, consideriamo un esempio pratico. Supponiamo di dover costruire un servizio web. Abbiamo due opzioni:

- **PaaS:** Affidarci a un servizio PaaS fornito da un provider, che garantisce di servire fino a 1000 utenti contemporaneamente, con un costo base e un costo aggiuntivo per ogni richiesta utente che supera le 2000 richieste al giorno. In questo caso, dobbiamo scrivere le funzioni del server utilizzando le API di Nginx, senza preoccuparci della scalabilità. Un esmpio potrebbe essere un DB installato e gestito in un server remoto che io, attraverso delle api configuro e sfrutto per delle query.

- **IaaS:** Costruire il servizio web partendo da componenti IaaS, istanziando le macchine virtuali, collocando i container contenenti Nginx su di esse e istanziando un bilanciatore di carico Kubernetes che, all'occorrenza, avvia nuove macchine virtuali e container con Nginx.

![](img/Virtualizzazione/paasVSiass.png)

#### Piattaforme di Gestione di Cloud Privati

Un privato che desidera costruire un proprio datacenter per realizzare un sistema cloud può farlo grazie a specifiche architetture software che consentono di utilizzare le risorse di più macchine fisiche, rendendole disponibili parzialmente su richiesta. Queste architetture sono conosciute come Piattaforme di Gestione del Cloud (**Cloud Management Platform**). Tra le principali architetture troviamo **OpenStack** e **OpenNebula**.

In un datacenter gestito tramite OpenStack, ad esempio, si possono avere diversi componenti come il **Cloud Controller (CLC)**, il **Walrus (storage controller)**, il **Cluster Controller (CC)** e il **Node Controller (NC)**. Questi componenti lavorano insieme per fornire un'infrastruttura cloud efficiente e scalabile.

![](img/Virtualizzazione/cloudPrivati.png)

Le esigenze per cui si potrebbe voler avere un cloude privato sono molteplici ma per lo più fanno tutte riferiento a probemi di privacy o di gestione della sicurezza.

#### Multitenancy

La multitenancy consente di condividere dinamicamente le risorse hardware tra diversi clienti, questa esigenza emerge dal fatto che gestico dati di macro utenti diversi che non vanno fatti aderire l'uno con l'altro. Ogni applicazione cliente opera in una propria macchina virtuale, garantendo isolamento per motivi di sicurezza e privacy. Questo approccio permette di pianificare l'uso delle risorse condivise, consentendo a un'applicazione di essere multithreaded in una macchina virtuale, mentre i dati e i profili degli utenti possono risiedere in altre macchine virtuali.

### Progettazione delle Comunicazioni in Reti Protette da NAT e Firewall

#### Virtual Private Network (VPN)

Le Virtual Private Network (VPN) consentono di creare una rete privata, simile a una LAN, tra host che possono trovarsi anche a grande distanza geografica. Esistono due principali tipologie di VPN:

- **Site-to-Site VPN:** Queste VPN vengono instaurate tra due reti, ad esempio tra due sedi distaccate di una stessa azienda, per utilizzare una rete privata unica.
- **Remote Access VPN:** Questa tipologia consente il collegamento di un singolo computer a una rete privata tramite VPN.

![](img/Virtualizzazione/vpn.png)

Tuttavia, l'uso delle VPN presenta un problema di sicurezza: se un computer esterno, collegato a una rete di un dominio tramite VPN, viene compromesso, c'è il rischio che l'intera rete del dominio venga messa in pericolo.

#### Esposizione di Porte Remote mediante SSH Remote Port Forwarding

Immaginiamo un server 0 che si trova dietro un NAT e espone un servizio sulla sua porta locale 44444, ma nessuno riesce a raggiungerlo dato che non espone ip pubblici. Un altro server, chiamato server 1, ha un indirizzo IP pubblico e un demone SSH attivo, fungendo da relay. In questo scenario, l'utente Joe è un utente del server 1. Il server 0 espone la sua porta locale 44444 come porta 55555 del server 1 utilizzando il comando **SSH**. Con **iptables**, il server 1 ridirige le connessioni in arrivo sulla porta webport verso la sua porta 55555. In questo modo, viene instaurata una connessione tra il client e il server 0 passando attraverso il server 1.

Ecco un esempio di comando SSH per realizzare questa configurazione:

```
ssh -R public_IPaddr:55555:localhost:44444 joe@public_IPaddr
```

![](img/Virtualizzazione/ssh.png)

- **Es: Video Controllo da Remoto con Superamento Firewall** (LEZIONE NON SEGIUTA!!!!!)

Consideriamo un sistema in cui diverse macchine automatiche, dotate di videocamera, si trovano in stabilimenti diversi. Gli utenti, sparsi nel mondo e con dispositivi vari, desiderano visualizzare le immagini delle macchine. Non ci sono vincoli sui dispositivi, quindi si utilizza video streaming basato su HTTP. Tuttavia, è necessario controllare l'identità dell'utente tramite un server centrale, e potrebbero esserci NAT e firewall davanti ai plant e agli utenti (reti private).

Il sistema di live streaming crea video in tempo reale e consente la visualizzazione da remoto. Sono coinvolti quattro attori software:
- **Media Server:** Acquisisce flussi audio e video dalle videocamere e li codifica. In alcuni casi, la videocamera stessa può avere funzionalità avanzate per questa operazione.
- **Utenti:** Possono accedere al flusso video tramite un browser, sia all'interno che all'esterno del plant.
- **Servizio di Signalling:** Gestisce la comunicazione tra i vari componenti del sistema.
- **Servizio di Distribuzione dei Contenuti:** Può essere centralizzato in cloud, fungendo da relay per i flussi video del media server, oppure decentralizzato, attivando una connessione diretta tra l'utente e il media server.

![](img/Virtualizzazione/videoRemoto.png)

Tuttavia, la presenza di NAT, in particolare di tipo simmetrico, può rendere impossibile il collegamento diretto tra i due end-system, richiedendo un intermediario. 

![](img/Virtualizzazione/Nat.png)

Per superare le limitazioni imposte dal NAT, si possono adottare diverse strategie:

1. **Collegamento mediante Intermediario in Cloud:** Un servizio con indirizzo IP pubblico opera come relay per i flussi video, duplicando i flussi e rimanendo sempre nel percorso dei dati. Questo approccio, sebbene efficace, utilizza una notevole quantità di banda.

![](img/Virtualizzazione/intermediarioCloud.png)

2. **Collegamento mediante Server TURN:** In questo caso, il canale di signalling (del quale non esistono standar dùe dunque è implemetato in maniera eterogenea) serve a concordare tra browser e media server le credenziali temporanee di accesso al server TURN e a stabilire le porte da utilizzare per i flussi video. Browser e media server tentano di stabilire un canale diretto tra loro; se non ci riescono, stabiliscono un canale indiretto che passa costantemente dal server TURN.

![](img/Virtualizzazione/turn1.png)

![](img/Virtualizzazione/turn2.png)

La probabilità di instaurare una connessione diretta tra due end-system è ridotta quando entrambi sono protetti da NAT simmetrici. Studi stimano che gli end-system protetti da NAT simmetrici rappresentino tra il 16% e il 23% del totale, a seconda che si tratti di sistemi desktop o mobile. È importante considerare che alcuni firewall bloccano il traffico UDP, quindi è consigliabile utilizzare protocolli di trasporto basati su HTTP, se possibile.

![](img/Virtualizzazione/liveEvent.png)

Il costo del servizio di live streaming di Azure è composto da cinque componenti principali:
1. Costo di instaurazione del channel (1 per ciascuna videocamera): gratuito.
2. Costo del servizio di streaming dal channel, basico, senza codifica: 0.835 €/ora, con un massimo di 600 Mbps, tariffa a consumo.
3. Costo della codifica in cloud: non utilizzato, poiché la codifica avviene in locale.
4. Costo della banda entrante in Azure: gratuito.
5. Costo della banda uscente da Azure verso gli utenti: 0.074 € per GB per consumi entro i 10 TB/mese.

Considerando il costo mensile per lo streaming di una videocamera, ipotizzando che da Azure esca un flusso di 1.6 Mbps verso ciascun utente e che lo streaming venga utilizzato ogni giorno da un solo utente per un totale di X ore giornaliere, il costo mensile può essere calcolato come segue:

$$
COSTO\_MENSILE(X) = X \times \left[30 \, \text{gg} \times 0.835 \, \text{€/h} + \left(\frac{1.6 \, \text{Mbps}}{8 \times 1000} \times 3600 \, \text{s} \times 30 \, \text{gg} \times 0.074 \, \text{€/GB}\right)\right]
$$

Per un'ora giornaliera di video inspection su una videocamera, il costo sarà:

$$
COSTO\_MENSILE(1 \, \text{ora al giorno}) = 26.6484 \, €
$$

## Sincronizzazione degli Orologi 
Nei sistemi distribuiti, molti processi operano su computer differenti e comunicano scambiandosi messaggi. Di norma, ogni computer utilizza il proprio orologio locale, il che significa che non esiste una “visione temporale” condivisa. La sincronizzazione degli orologi ha l’obiettivo di garantire che, pur operando in ambienti fisicamente separati, tutti i processi abbiano la medesima nozione del tempo. Questa sincronizzazione è fondamentale per diverse ragioni: ad esempio, può servire a determinare l’istante esatto in cui si verifica un evento, misurare l’intervallo di tempo tra due eventi o stabilire l’ordine relativo degli eventi, come avviene con l’utilizzo dei clock logici (ad esempio, quelli proposti da Lamport).

### Importanza della Sincronizzazione nella Sicurezza
In molti sistemi distribuiti, specialmente in quelli in cui la sicurezza è essenziale, i protocolli fanno uso di marcature temporali (timestamp) per concedere l’accesso a risorse in maniera limitata nel tempo. Ad esempio, protocolli come SSL/TLS e Kerberos utilizzano i timestamp per assicurare che le credenziali o i ticket abbiano una validità breve, limitando così la finestra di attacco in caso di compromissione. Nel caso di Kerberos, è cruciale che gli orologi dei server siano sincronizzati accuratamente; altrimenti, se vi sono differenze troppo marcate, i client non potranno autenticarsi correttamente e il sistema rischia di non funzionare.

### Tipi di Clock  
Ogni computer è dotato di due tipi principali di orologi, che svolgono funzioni complementari:

- **Clock Hardware (o CMOS/ Digital Clock):** Questo orologio è realizzato attraverso un contatore digitale alimentato da una batteria e continua a contare il tempo anche se il computer è spento. All’accensione, il sistema operativo legge il valore del clock hardware per inizializzare il clock software. Sebbene il clock hardware sia generalmente affidabile, può essere influenzato da variazioni nella tensione o nella temperatura – per questo, è basato su un oscillatore al quarzo che garantisce una frequenza relativamente stabile. In molti sistemi, è possibile visualizzare o modificare il clock hardware (ad esempio, utilizzando il comando “hwclock” su Linux).

- **Clock Software (o System Clock):** 
  Il clock software è gestito dal sistema operativo ed è in funzione solo quando il computer è acceso. Durante il processo di avvio, il sistema operativo imposta il clock software utilizzando il valore del clock hardware. Successivamente, il sistema operativo aggiorna il clock software tramite incrementi periodici, generalmente noti come tick. Durante tali aggiornamenti, è possibile applicare un offset per correggere eventuali deviazioni, in modo da mantenere il sistema sincronizzato rispetto a fonti esterne, come i server NTP.

### Meccanismi di Sincronizzazione

- **Meccanismo di Sincronizzazione Semplice:** Una strategia basilare per sincronizzare gli orologi prevede che un dispositivo, indicato come “master”, invii periodicamente un messaggio che contiene il proprio timestamp attuale. Il dispositivo “slave”, ricevendo questo messaggio, aggiorna il proprio orologio con il valore indicato. Tuttavia, poiché il messaggio impiega un certo tempo per raggiungere il destinatario, il valore ricevuto corrisponde a un istante passato. Ciò introduce un piccolo errore, noto come errore di fase, dovuto al ritardo di trasmissione.

- **Meccanismo Round-Trip Time (RTT) di Sincrinizzazione:** Per ridurre l’errore di sincronizzazione dovuto al ritardo di rete, si possono adottare algoritmi che misurano il round-trip time (RTT). In pratica, il master invia un messaggio e attende una risposta dal slave, così da misurare il tempo totale impiegato per l’invio e il ritorno del messaggio. Supponendo che il ritardo sia simmetrico, il ritardo effettivo per un solo verso può essere approssimato come la metà dell’RTT.  
Ad esempio, in alcuni algoritmi (come l’algoritmo di Berkeley) il dispositivo slave invia il proprio timestamp (T₁) in una richiesta; il master riceve tale messaggio, registra il proprio orario di ricezione (T₂) e spedisce una risposta, includendo sia T₂ che l’istante di spedizione (T₃). Quando il slave riceve la risposta (all’istante T₄), può calcolare il delay come:  

  D = ((T₄ – T₁) – (T₃ – T₂)) / 2

Successivamente, il dispositivo slave aggiorna il proprio orologio applicando tale delay, riducendo l’errore introdotto dal ritardo di rete. Un’altra formula utile è quella per calcolare l’offset, cioè la differenza tra il tempo del master e quello dello slave, che può essere approssimato come:  

  Offset ≈ ((T₂ – T₁) + (T₃ – T₄)) / 2

![](img/Virtualizzazione/sincroClock.png)

Attraverso questi calcoli, è possibile regolare il clock dello slave per avvicinarlo il più possibile a quello del master.

### Meccanismo Three-Way di Sincronizzazione

Nel meccanismo three-way di sincronizzazione, il processo inizia con il **master** che invia una richiesta contenente il proprio timestamp, indicato come **T₁**. Questo messaggio viene inviato allo **slave**, il quale, al momento della ricezione, registra il proprio timestamp come **T₂**. Successivamente, lo slave prepara una risposta includendo il valore ricevuto, ovvero **T₁**, insieme al suo timestamp di ricezione (**T₂**) e al timestamp al momento dell'invio della risposta (**T₃**).

Una volta che il master riceve la risposta dallo slave (al tempo **T₄**), egli stima il ritardo di trasmissione (**Delay D**) approssimandolo come metà del **round-trip time (RTT)**. La formula utilizzata per calcolare il ritardo è la seguente:

  D = RTT/2 = ((T₄ – T₁) – (T₃ – T₂)) / 2

Successivamente, il master stima l’**offset** (O), cioè la differenza temporale tra il suo orologio e quello dello slave, con la formula:

  O = ((T₂ – T₁) + (T₃ – T₄)) / 2

Questo offset indica di quanti secondi bisogna rallentare il clock dello slave. Una volta calcolati delay e offset, il master invia al slave un messaggio contenente questi dati, che funge da ordine per aggiornare il proprio orologio. Ricevuto il messaggio, lo slave modifica il proprio orologio, applicando la correzione, cioè impostando il nuovo valore del clock secondo:

  T_slave' = T_slave – O

![](img/Virtualizzazione/3way1.png)

- **Esempio**

- Supponiamo che:
  - Il clock del **master** sia indietro di 1 secondo rispetto a quello dello **slave**.
  - Il tempo di trasmissione per ogni messaggio sia costante, pari a circa 0.5 secondi.
  - Il tempo impiegato (T₃ – T₂) per elaborare e rispondere al messaggio sia di 1 secondo.

In questo caso, possiamo calcolare il **round-trip time (RTT)** come segue:

  RTT = ((T₄ – T₁) – (T₃ – T₂))  
  Supponendo T₁ = 1.0, T₄ = 3.0, T₂ = 2.5, T₃ = 3.5,  
  RTT = (3.0 – 1.0) – (3.5 – 2.5) = 2.0 – 1.0 = 1.0 secondo.

Da qui, il **Delay D** risulta:

  D = RTT/2 = 1.0 / 2 = 0.5 secondi.

Successivamente, l'**offset O** si calcola come:

  O = ((T₂ – T₁) + (T₃ – T₄)) / 2  
  O = ((2.5 – 1.0) + (3.5 – 3.0)) / 2  
  O = (1.5 + 0.5) / 2 = 1.0 secondo.

Questo significa che, per allinearsi al clock del master, lo slave deve rallentare il proprio orologio di 1 secondo.

Nel seguito del processo, al momento T₅ il master invia il messaggio di aggiornamento, contenente il valore dell’offset (O = 1.0, insieme al delay D = 0.5). Successivamente, quando lo slave riceve questo messaggio all’istante T₆ (ad esempio T₆ = 6.5), esso aggiorna il proprio clock:

  T_slave' = T₆ – O = 6.5 – 1.0 = 5.5

Così, lo slave corregge il proprio orologio per sincronizzarlo con quello del master.

### Problemi e Limitazioni
Nonostante le tecniche avanzate, la sincronizzazione degli orologi nei sistemi distribuiti presenta alcune problematiche. In primo luogo, i ritardi di trasmissione tra i dispositivi possono variare notevolmente, impedendo di avere una vista istantanea e globale dei tempi. Inoltre, anche se tutti i clock fossero inizializzati allo stesso istante, il fenomeno del drift – ovvero la differenza nel ritmo di avanzamento di ciascun orologio – richiede correzioni continue per mantenere la precisione. Infine, la presenza di componenti malfunzionanti o “faulty” può rendere ancora più difficile ottenere una sincronia perfetta.

### Sincronizzazione dei Clock Fisici

Nei sistemi distribuiti non basta avere un ordinamento temporale privo di ambiguità; in molte applicazioni è fondamentale conoscere il tempo reale in cui avvengono gli eventi. Per questo motivo, oltre ai cosiddetti clock logici – che garantiscono solo un ordinamento degli eventi – è necessario fare riferimento ai **clock fisici**, che siano essi hardware o software, in quanto essi forniscono un’**approssimazione del tempo reale**. Nei sistemi complessi è auspicabile disporre di più clock fisici, ma questo porta a dover affrontare tre problematiche principali:

1. **Definire un tempo ufficiale e i mezzi per ottenerlo:**  
   L’obiettivo è stabilire una base comune, come rappresentata dal **UTC (Universal Coordinated Time)**.

2. **Sincronizzazione diretta con la fonte ufficiale:**  
   È necessario stabilire metodi per sincronizzare direttamente gli orologi con i detentori del tempo ufficiale, ad esempio tramite **WWV**, una stazione radio a onde corte che trasmette segnali temporali.

3. **Sincronizzazione degli orologi tra loro:**  
   I sistemi devono essere in grado di coordinarsi internamente, utilizzando ad esempio il **Network Time Protocol (NTP)** per mantenere gli orologi in linea tra di loro. 

Spesso in certi sistemi non basta disporre di un ordinamento temporale per determinare l’ebrezza degli eventi; ciò che conta è il tempo effettivo in cui si verificano. I clock fisici – che siano realizzati in hardware o gestiti via software – forniscono una stima del tempo reale, mentre i clock logici si limitano a ordinare gli eventi. Per una gestione efficiente e ridondante dei sistemi distribuiti è preferibile che siano presenti diversi clock fisici. Tuttavia ciò introduce tre sfide:
 
- Stabilire un tempo ufficiale (es. **UTC**) e definire i mezzi fisici per ottenerlo.
- Determinare come sincronizzare direttamente gli orologi con i detentori del tempo ufficiale (ad esempio tramite **WWV**).
- Coordinare e sincronizzare gli orologi tra loro, per cui si utilizza solitamente il **NTP (Network Time Protocol)**.

La base di riferimento per il tempo ufficiale a livello globale è il **UTC**.  
- Numerosi laboratori in tutto il mondo dispongono di orologi atomici, molti dei quali basati sul cesio 133, e comunicano periodicamente al **Bureau International de l’Heure (BIH)** di Parigi il loro numero di tick.  
- Il BIH esegue una media di tali valori per produrre il **Tempo Atomico Universale (TAI)**. Il giorno del TAI risulta leggermente più corto, di circa 3 microsecondi, rispetto al giorno solare; per compensare questa differenza viene applicato un tempo di compensazione, dando origine all’UTC – il riferimento internazionale che coincide, a piccole approssimazioni, con il tempo medio di Greenwich (**GMT**).

Per mettere a disposizione l'UTC agli utenti che richiedono un tempo preciso, esiste una stazione radio a onde corte, nota come **WWV**, che trasmette un segnale (un beep) ogni secondo UTC.  
- Naturalmente, il segnale viaggia attraverso l’atmosfera e introduce dei ritardi; per compensare ciò è necessario conoscere con precisione la distanza tra il trasmettitore e il ricevitore, in modo da calcolare il ritardo di propagazione. 

Quando due processi, ad esempio c e c′, sono considerati sincronizzati al tempo T se la differenza tra i loro clock è inferiore a un delta stabilito (|c(T) – c′(T)| < δ), si affrontano due sistemi:
 
- **Sincronizzazione interna:**  
  In assenza di una fonte esterna, più clock fisici paritetici si sincronizzano tra di loro per minimizzare la massima differenza interna, creando così quasi un clock comune.

- **Sincronizzazione esterna:**  
  Quando esiste una sorgente di tempo reale, l’obiettivo è che i clock degli host siano quanto più vicino possibile a questa fonte.

Nei casi di sincronizzazione esterna, ci si focalizza sull’allineare il clock di uno o più host con il tempo ufficiale fornito, ad esempio, da una sorgente NTP.

### Sincronizzazione Esterna dei Clock Fisici

Un **time server process** è il componente responsabile della sincronizzazione degli orologi. Esso può leggere il **clock hardware (HC)** dell’host al tempo t, mentre il **clock software (SC)** viene infatti definito via software come: 

  SC(t) = HC(t) + A(t)

dove A(t) è la funzione di correzione che dipende dal tempo. La sfida consiste nel determinare A(t) in maniera adeguata, anche in presenza di malfunzionamenti nei sistemi, che possono riguardare processori, clock o link di comunicazione. Questo problema è affrontato dal protocollo **NTP**, che garantisce che anche se alcuni sistemi responsabili del tempo risultano difettosi, l’algoritmo continui a funzionare.

### NTP (Network Time Protocol)

Per sincronizzare l’orario tra i server e i client esiste il **Network Time Protocol (NTP)**.  
- Numerosi server NTP pubblici permettono di sincronizzare gli orologi: in una LAN, NTP può raggiungere la precisione al millisecondo, mentre in una WAN la precisione tipica è entro decine di millisecondi.
- I server NTP sono organizzati in livelli detti **stratum**:  
  - I server primari, classificati come **stratum 1**, si sincronizzano direttamente con fonti esterne (GPS, orologi atomici, WWV).  
  - I server pubblici di **stratum 2** si sincronizzano con quelli di stratum 1 e forniscono il tempo ai client.
  
Ad oggi è possibile trovare liste di server NTP dello stratum 2, da utilizzare per una sincronizzazione efficace. Nel contesto di sistemi più complessi, ad esempio quando si configura un servizio di directory, è comune impostare i server Kerberos per interrogare più server NTP di stratum 2.

**Architettura e Formato dei Dati NTP** 
 
Ogni computer possiede un orologio hardware che, sebbene scarsamente preciso, fornisce un tick a intervalli variabili.  
- Speciali ricevitori permettono di ottenere il segnale orario da fonti esterne come WWV o il GPS.  
- Non è economico equipaggiare ogni sistema con tali ricevitori; invece, alcuni computer, agendo come **server primari**, si sincronizzano direttamente con queste fonti e propagano il tempo agli altri sistemi, organizzando così una gerarchia (o albero) di sincronizzazione suddivisa in strati (stratum).

I messaggi NTP utilizzano formati di dati appositamente progettati per rappresentare il tempo. Esistono vari formati:
  
- **NTP Date Format:**  
  Un formato a 128 bit, diviso in due parti da 64 bit ciascuna, in cui i 64 bit iniziali rappresentano i secondi e i successivi 64 bit rappresentano la frazione di secondo. Questo formato include anche la suddivisione in “Ere” per coprire lunghe scale temporali.

- **NTP Timestamp Format:**  
  Un formato più compatto a 64 bit, in cui 32 bit memorizzano i secondi e 32 bit la frazione di secondo. È utilizzato nei pacchetti NTP per trasmettere i timestamp.

- **NTP Short Format:**  
  Un formato a 32 bit, utilizzabile quando sono necessari minori dettagli temporali.

L’obiettivo primario di NTP non è “settare” il clock di un client a un valore fisso, ma **aggiustarlo** (con il termine inglese “adjust”) applicando periodicamente una correzione alla funzione di aggiustamento A(t) del clock software. Questo processo richiede che, inizialmente, il clock del client non sia disallineato di oltre 68 anni rispetto al server, affinché la correzione sia possibile e significativa.

**Flusso dei Messaggi NTP**

Un client NTP mantiene una lista di server da cui richiedere il tempo. A intervalli regolari:
  
- Il client invia una richiesta a ciascun server, includendo il proprio timestamp di origine (T₁).  
- Il server risponde includendo i timestamp relativi alla ricezione (T₂) e alla trasmissione (T₃) del messaggio.  
- Il client, al ricevere la risposta, annota il proprio istante di ricezione (T₄) e calcola, per ciascun server, l’**offset** e il **delay** tramite i meccanismi di round-trip già descritti.  
- Dopo aver raccolto più campioni, il client scarta quelli con dati devianti e usa una media pesata degli offset per determinare la correzione da applicare al proprio clock.

I pacchetti NTP sono incapsulati in UDP e sono strutturati secondo la RFC 5905 (NTP versione 4). Essi contengono informazioni quali:
  
- **Leap Indicator (LI):** Avvisa di un imminente leap second.  
- **Version Number (VN):** Indica la versione del protocollo.  
- **Mode e Stratum:** Specificano il ruolo del mittente (client, server, broadcast, ecc.) e il livello gerarchico.  
- Altri campi contengono i vari timestamp (Reference, Origin, Receive e Transmit) e informazioni sui ritardi e dispersioni.

## Crittografia

La **crittografia** è una scienza antichissima che si occupa di codificare e decodificare informazioni. Le sue origini risalgono a epoche storiche come quella di Sparta. Il processo di crittografia implica due fasi fondamentali: 

- **Codificare:** trasformare un testo in chiaro in un testo codificato.
- **Decodificare:** riportare il testo codificato al suo stato originale, ovvero il testo in chiaro.

Entrambi i processi si basano su un **algoritmo** e una **chiave**. Ad esempio, un semplice metodo di codifica potrebbe essere quello di "shiftare" una stringa di un certo numero di posizioni. È importante notare che l'algoritmo utilizzato è pubblico, mentre la sicurezza del sistema dipende da due fattori principali:

1. **Segretezza della chiave:** Solo le parti autorizzate devono conoscere la chiave utilizzata per la codifica e la decodifica.
2. **Robustezza dell’algoritmo:** Un algoritmo forte rende più difficile per un attaccante decifrare il messaggio senza la chiave.

### Crittografia a Chiave Segreta (Simmetrica)

Nella crittografia a chiave segreta, la stessa chiave viene utilizzata sia per la codifica che per la decodifica. Questo richiede che solo il mittente e il destinatario conoscano la chiave segreta. I vantaggi di questo approccio includono:

- **Segretezza, autenticazione e integrità:** La chiave condivisa garantisce che solo le parti autorizzate possano accedere alle informazioni.
- **Velocità:** Gli algoritmi come **DES (Data Encryption Standard)**, **Triple-DES** e **AES (Advanced Encryption Standard)** sono generalmente veloci e possono essere implementati in modo efficiente.

Tuttavia, ci sono anche svantaggi significativi:

- **Distribuzione della chiave:** È necessario scambiare la chiave segreta in modo sicuro tra le parti, il che rappresenta un punto critico, poiché non esistono soluzioni generali affidabili per questo scambio.
- **Scalabilità:** Per n utenti, sono necessarie n*(n-1)/2 chiavi diverse, il che può diventare ingombrante in sistemi con molti utenti.

### Crittografia a Chiave Pubblica (Asimmetrica)

La crittografia a chiave pubblica utilizza due chiavi distinte: una per la codifica e una per la decodifica. In questo modello, il mittente e il destinatario non condividono una chiave segreta. Ogni utente possiede una coppia di chiavi:

- **Chiave privata:** Un segreto personale che deve essere custodito.
- **Chiave pubblica:** Un'informazione che può essere diffusa a chiunque.

Queste chiavi possono essere utilizzate per codificare o decodificare i messaggi. In particolare, un messaggio codificato con una chiave può essere decodificato solo con l'altra chiave. Un esempio comune di algoritmo di crittografia asimmetrica è **RSA**, che utilizza chiavi di dimensioni comprese tra 1024 e 2048 bit. È importante notare che chiavi inferiori a 2048 bit non sono più considerate sicure.

I vantaggi della crittografia a chiave pubblica includono:

- **Nessuna necessità di scambiare chiavi segrete:** Solo le chiavi pubbliche devono essere comunicate, il che semplifica il processo.
- **Segretezza, autenticazione, integrità e non ripudiabilità:** Queste proprietà sono garantite dalla struttura stessa del sistema.

Tuttavia, ci sono anche svantaggi:

- **Lentezza:** Gli algoritmi di crittografia asimmetrica sono generalmente più lenti rispetto a quelli simmetrici.
- **Verifica dell'identità:** È necessario garantire che la chiave pubblica di un utente sia effettivamente quella dell'utente stesso, per evitare attacchi di impersonificazione.

### Funzioni Hash Crittografiche

Le funzioni hash crittografiche, note anche come **one-way hash** o **funzioni digest**, sono progettate per prendere in input una stringa (messaggio) di lunghezza variabile e produrre una stringa (digest) di lunghezza fissa. Queste funzioni soddisfano la proprietà di non reversibilità, il che significa che deve essere computazionalmente impossibile trovare due messaggi distinti che producano lo stesso hash.

In sintesi, una funzione hash crittografica MD(m) produce un riassunto digitale del messaggio m. Le proprietà fondamentali di queste funzioni includono:

1. **Unicità:** Ogni messaggio deve generare un hash unico.
2. **Non reversibilità:** Dato un hash, non deve essere possibile risalire al messaggio originale.
3. **Resistenza alle collisioni:** È impossibile trovare due messaggi distinti che producano lo stesso hash.

Queste caratteristiche rendono le funzioni hash crittografiche strumenti essenziali per garantire la sicurezza e l'integrità dei dati in vari contesti, come la firma digitale e la verifica dell'integrità dei messaggi.

La **Message Authentication Code (MAC)** è una tecnica che consente di autenticare parzialmente l'origine di un messaggio, riconoscendo il mittente e garantendo l'integrità del messaggio stesso. Questa tecnica combina l'uso della crittografia, sia a chiave pubblica che a chiave segreta, con le funzioni hash crittografiche. 

Quando tra mittente e destinatario esiste una chiave segreta per la crittografia simmetrica, si utilizza la funzione hash insieme alla crittografia simmetrica. Questa rappresenta la vera tecnica MAC. Al contrario, se il mittente dispone di una chiave pubblica (parte di una coppia di chiavi pubblica e privata), si può utilizzare la funzione hash insieme alla crittografia asimmetrica, dando vita alla **firma digitale**.

### Integrità di Messaggi e Firma Digitale

Quando si desidera spedire un messaggio **m**, la tecnica della firma digitale mediante MAC prevede le seguenti operazioni:

1. **Applicazione della Funzione Hash:**  
   Prima di inviare il messaggio, si applica una funzione hash crittografica per creare un riassunto (digest) del messaggio stesso, ottenendo **MD(m)**.

2. **Codifica del Riassunto:**  
   Il digest del messaggio viene quindi codificato:
   - Utilizzando la chiave segreta **K** condivisa tra mittente e destinatario, si ottiene **MAC = E_K(MD(m))**.
   - Oppure, utilizzando la chiave privata del mittente, si ottiene **MAC = K^-(MD(m))**.

3. **Creazione del Messaggio Finale:**  
   Il codice di autenticazione del messaggio (MAC) viene concatenato al messaggio originale. Il messaggio spedito sarà quindi formato da **(m, MAC)**, ovvero **(m, K^-(MD(m)))** o **(m, E_K(MD(m)))**.

### Ricezione del Messaggio con MAC

Alla ricezione del messaggio con il formato **(m', MAC)**, il destinatario deve seguire questi passaggi:

1. **Separazione del Messaggio e del MAC:**  
   Il destinatario separa il messaggio **m'** dal MAC.

2. **Decodifica del MAC:**  
   Il MAC viene decodificato:
   - Utilizzando la chiave pubblica del mittente, si ottiene **K^+(K^-(MD(m))) = MD(m)**.
   - Oppure, utilizzando la chiave segreta condivisa, si ottiene **D_K(E_K(MD(m))) = MD(m)**.

3. **Verifica dell'Integrità:**  
   Se la decodifica produce errori, significa che il mittente non è quello dichiarato nel messaggio. Se la decodifica va a buon fine, il digest ottenuto è il digest del messaggio originale **MD(m)**. A questo punto, il destinatario calcola il digest del messaggio ricevuto **MD(m')** e confronta i due valori. Se **MD(m) == MD(m')**, il messaggio ricevuto è autentico e proviene dal mittente dichiarato.

### Crittografia a Chiave Segreta vs. Crittografia a Chiave Pubblica

La tecnica MAC è applicabile solo se mittente e destinatario conoscono una chiave segreta. In questo caso, il destinatario può verificare che, se riesce a decodificare il messaggio, questo proviene dall'altro (o da sé stesso). Tuttavia, non può dimostrare a osservatori esterni che l'altro ha realmente spedito il messaggio, il che implica che mancano segretezza e non ripudiabilità. Pertanto, le proprietà garantite sono:

- **Integrità**
- **Autenticazione**

D'altra parte, la firma digitale è applicabile solo se il mittente possiede una chiave pubblica/privata. In questo caso, chiunque può leggere il messaggio e riconoscere chi lo ha spedito, verificandone l'integrità. Le proprietà garantite dalla firma digitale includono:

- **Integrità**
- **Autenticazione**
- **Non ripudiabilità**

Tuttavia, manca la segretezza, poiché il messaggio è accessibile a chiunque. 

In generale, sia la MAC che la firma digitale sono più rapide rispetto alla codifica dell'intero documento, poiché non è necessario codificare tutto il messaggio, ma solo il digest.

## Kerberos

Kerberos è un sistema di autenticazione sviluppato nel 1983 grazie alla collaborazione tra il **Massachusetts Institute of Technology (MIT)**, **IBM** e **DEC**. Il nome "Kerberos" deriva dalla mitologia greca, dove era il nome del cane a tre teste che custodiva le porte dell'inferno. Questo simbolismo è significativo, poiché le tre teste rappresentano i tre obiettivi principali di Kerberos:

- **Autenticazione:** Verificare l'identità di un client o di un servizio.
- **Autorizzazione:** Consentire a un client autenticato di utilizzare un particolare servizio.
- **Cifratura:** Garantire che terze parti non possano ascoltare i contenuti delle comunicazioni.

Attualmente, esistono due versioni di Kerberos, che utilizzano protocolli diversi e non sono compatibili tra loro: la **versione 4**, sviluppata alla fine degli anni '80, e la **versione 5**, emanata nella RFC 1510 nel 1993 e stabilizzata nella RFC 4120 nel 2005, che offre maggiore sicurezza e supporto per ambienti multidominio.

La necessità di controllare l'accesso degli utenti che richiedono servizi da reti diverse ha portato allo sviluppo di Kerberos. I requisiti di autenticazione in una rete aperta devono essere:

- **Sicuri:** Proteggere le informazioni sensibili.
- **Affidabili:** Garantire che le identità siano verificate correttamente.
- **Scalabili:** Supportare un numero crescente di utenti e servizi.
- **Trasparenti:** Non richiedere complicate configurazioni da parte degli utenti.

Kerberos funge da **server fidato di gestione delle chiavi** (Trusted Key Server System), fornendo un servizio di autenticazione centralizzato basato su chiavi private (simmetriche). Questo sistema è separato dal servizio stesso, consentendo agli utenti di accedere a servizi distribuiti senza dover riporre fiducia nei server fornitori di servizio. Idealmente, gli utenti non devono fidarsi delle workstation nella rete in cui opera Kerberos, ma devono fidarsi del server di autenticazione centralizzato.

L'autenticazione nel sistema Kerberos si basa su un nuovo modello di fiducia, che differisce dal tradizionale modello a due parti. In quest'ultimo, le due entità devono avere fiducia reciproca. In Kerberos, invece, le due parti si fidano solo di una terza parte, il **KDC (Key Distribution Center)**, che funge da garante dell'identità di ciascuna parte.

All'interno di un **realm** (dominio di sicurezza), i "principal" sono sia utenti che servizi che possono autenticarsi tramite Kerberos. La struttura del nome di un principal è: **Primary/instance@NOMEREALM**, dove "Primary" rappresenta il nome dell'utente o del servizio e "instance" rappresenta la qualifica dell'utente. Ogni client e server condivide con il KDC una chiave (o password) crittografica, e il KDC si occupa di presentare un principal a un altro principal mantenendo la segretezza reciproca.

Kerberos si basa su alcune assunzioni fondamentali:

- Le password non devono essere "facili" da indovinare.
- Le workstation devono essere sicure, senza keylogger o software simili.
- La rete è considerata insicura, il che implica che Kerberos deve essere in grado di resistere a vari tipi di attacchi. Tuttavia, è preferibile utilizzare Kerberos all'interno di un dominio controllato.

### Strategie di Kerberos

Kerberos implementa diverse strategie per garantire la sicurezza:

- **Single Sign-On (SSO):** La password è richiesta e utilizzata solo una volta durante la sequenza di login.
- **Sicurezza delle Password:** Le password non vengono mai trasmesse in chiaro, rendendo il sistema resistente agli attacchi di sniffing.
- **Uso di Chiavi Private:** La comunicazione avviene esclusivamente tramite chiavi private, senza l'uso di crittografia a chiave pubblica.
- **Ambiente Sicuro per il KDC:** Ogni dominio di sicurezza di Kerberos deve operare in un ambiente fisico sicuro che ospiti il KDC.
- **Protocollo di Autenticazione:** Kerberos estende il protocollo di Needham-Schroeder per la distribuzione delle chiavi.

### Requisiti di Tempo in Kerberos

La sicurezza di Kerberos è anche legata all'uso di **timestamp** (marche temporali) nei ticket. È cruciale che gli orologi dei server Kerberos siano regolati con precisione. I ticket hanno una scadenza breve per prevenire attacchi di forza bruta e di replica. Se gli orologi non sono sincronizzati entro un intervallo ragionevole, Kerberos può presentare errori fatali e smettere di funzionare. I client che tentano di autenticarsi da una macchina con un orologio non accurato falliranno il tentativo di autenticazione presso il KDC a causa della differenza di ora.

### Applicabilità di Kerberos

Kerberos non è facilmente applicabile in tutti i contesti, poiché utilizza un protocollo di comunicazione specifico tra l'entità che richiede un servizio e quella che lo fornisce. Le applicazioni devono essere modificate per supportare Kerberos, un processo noto come "kerberizzazione". Alcune applicazioni che già supportano Kerberos includono:

- AFS, NFS, Coda File System
- Apache (mod_auth_kerb) e Apache 2 (libapache-mod-auth-kerb)
- Cisco routers e switches
- Client di posta elettronica come Eudora e Mulberry
- Sistemi operativi come Mac OS X e Microsoft Windows
- OpenSSH e moduli di autenticazione pluggable (PAM)
- Samba e Netatalk
- Qualsiasi software che utilizzi il framework SASL


**Perché Usare Kerberos e LDAP Insieme?**

Kerberos è progettato per l'autenticazione e fornisce un sistema di **Single Sign-On (SSO)**. D'altra parte, **LDAP** (Lightweight Directory Access Protocol) può essere utilizzato per l'autenticazione, l'autorizzazione e i servizi di nomi, ma non offre SSO. L'**Active Directory** è un servizio di directory kerberizzato con un'interfaccia LDAP, quindi è vantaggioso utilizzare Kerberos per l'autenticazione e LDAP per l'autorizzazione e i servizi di nomi.


**Panoramica di Kerberos e Realms**

Un ambiente Kerberos è composto da:

- Un server Kerberos (KDC)
- Un numero di client, tutti registrati con il server e che condividono chiavi con esso.
- Server applicativi che condividono chiavi con il server.

Questo insieme di componenti è definito un **realm**, che tipicamente rappresenta un singolo dominio amministrativo.
