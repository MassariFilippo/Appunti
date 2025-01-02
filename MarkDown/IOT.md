# Appunti IOT

## Architetture Task-Based e la Modellazione dei Sistemi Embedded

Nell'ambito della progettazione di sistemi embedded complessi, uno dei problemi principali è la modellazione e il design del software. La sfida consiste nel trovare metodi appropriati per decomporre e modularizzare il comportamento e le funzionalità del sistema, in modo da gestire la complessità crescente.

### Approccio delle Architetture Task-Based

Un'architettura task-based scompone il comportamento del software embedded in una serie di task concorrenti, dove ogni task rappresenta una specifica unità di lavoro ben definita. Ogni task può essere descritto mediante una Macchina a Stati Finita (FSM) e il comportamento complessivo del sistema è dato dall'interazione e dall'esecuzione parallela di queste FSM. Un esempio è il "LED-Show", dove più LED operano con logiche differenti:

1. **Un LED singolo** lampeggia con un periodo di 500 ms.
2. **Altri tre LED** si accendono e spengono in sequenza, con intervalli di 500 ms.

Questa configurazione può essere rappresentata come un unico task/FSM, ma il modello diventa più semplice se si dividono i comportamenti in due task distinti, riducendo il numero di stati e transizioni.

### Diagramma a Blocchi e Vantaggi della Decomposizione in Task

Ogni task può essere rappresentato come un blocco rettangolare che mostra le variabili di input e output, facilitando così la modularità. Grazie a questa decomposizione, si ottengono i seguenti vantaggi:

- **Modularità**: ogni task è un modulo indipendente, con interfacce definite dagli input/output condivisi con altri task.
- **Riduzione della complessità**: il task singolo è meno complesso rispetto al comportamento globale.
- **Facilità di debugging** e **riutilizzabilità** del codice.

### Sfide della Concorrenza tra Task

Dato che i task operano in parallelo, il loro flusso di controllo logico può sovrapporsi nel tempo. Per gestire questa concorrenza, è necessario implementare meccanismi di coordinamento e interazione basati su variabili e oggetti condivisi.

### Implementazione delle Architetture Task-Based

#### Classe Base Astratta Task

Per rappresentare i task in maniera modulare, si utilizza una classe astratta `Task`, con due metodi principali:

- `init()`: inizializza il task, chiamato una volta.
- `tick()`: incapsula il comportamento del task, richiamato periodicamente.

Ogni task concreto estende questa classe e implementa il proprio comportamento all’interno di `tick()`. In questo modo, i task possono essere gestiti da un loop principale che periodicamente invoca `tick()`.

### Esempio Implementativo: LED-Show su Arduino
Di seguito, una versione implementativa del "LED-Show" su Arduino:

1. **BlinkTask**: rappresenta un LED che lampeggia.
   ```cpp
   class BlinkTask: public Task {
       int pin;
       Light* led;
       enum { ON, OFF } state;
       ...
       void tick() {
           switch (state) {
               case OFF: led->switchOn(); state = ON; break;
               case ON:  led->switchOff(); state = OFF; break;
           }
       }
   };
   ```

2. **ThreeLedsTask**: gestisce tre LED in sequenza.
   ```cpp
   class ThreeLedsTask: public Task {
       int pin[3];
       Light* led[3];
       int state;
       ...
       void tick() {
           led[state]->switchOff();
           state = (state + 1) % 3;
           led[state]->switchOn();
       }
   };
   ```

3. **Main Loop**: gestisce i task con un timer che richiama i metodi `tick` periodicamente.
   ```cpp
   void setup() {
       blinkTask.init();
       threeLedsTask.init();
       timer.setupPeriod(500);
   }
   void loop() {
       timer.waitForNextTick();
       blinkTask.tick();
       threeLedsTask.tick();
   }
   ```

### Scheduler Cooperativo e Gestione di Periodi Diversi

Quando si ha la necessità di gestire task con periodi differenti, è utile implementare uno scheduler cooperativo che tenga traccia dei task da eseguire e li chiami al proprio periodo specifico. Lo scheduler utilizza una strategia **round-robin cooperativa**, con un periodo base pari al massimo comun divisore dei periodi dei task. Ad ogni periodo base, lo scheduler richiama `tick()` per ciascun task.

### Implementazione del Scheduler
Lo scheduler è definito dalla classe `Scheduler`:
   ```cpp
   class Scheduler {
       int basePeriod;
       Task* taskList[MAX_TASKS];
       ...
       void schedule() {
           timer.waitForNextTick();
           for (int i = 0; i < nTasks; i++) {
               if (taskList[i]->updateAndCheckTime(basePeriod)) {
                   taskList[i]->tick();
               }
           }
       }
   };
   ```

### Esempio di Sistema Motion-Triggered Lamp

Consideriamo un sistema embedded che accende un LED al rilevamento di un movimento. È progettato come segue:

- Un sensore rileva il movimento (P4) e attiva il LED collegato (P2) quando il movimento è rilevato due volte consecutive (200 ms).
- La luce rimane accesa per 10 secondi dopo l’ultimo rilevamento.
- Un altro LED lampeggia (P3) con un periodo di 200 ms mentre il movimento è rilevato.

I task necessari sono:
1. `DetectMotion`
2. `IlluminateLamp`
3. `BlinkLed`

### Variabili Condivise, Azioni Atomiche e Condizioni di Gara

Quando più task utilizzano variabili condivise, si rischiano condizioni di gara nelle letture/scritture concorrenti. Nella nostra architettura cooperativa, ogni esecuzione di `tick()` è **atomica** per l’intero sistema, ma l’interleaving delle chiamate tra task può introdurre condizioni di gara a livello logico.

### Modalità Sleep per Risparmio Energetico

Con un periodo abbastanza ampio, lo scheduler può sfruttare la modalità sleep per risparmiare energia. Dopo l’esecuzione dei task, il sistema va in sleep fino al prossimo tick del timer.

### Analisi dell’Esecuzione: Utilizzo della CPU e WCET

Nei sistemi FSM sincroni, si suppone che le azioni siano istantanee. Tuttavia, in un sistema reale, bisogna considerare la durata reale delle azioni per evitare eccezioni di overrun. Il parametro di **utilizzo della CPU (U)** è la percentuale di tempo in cui la CPU è utilizzata per eseguire un task, calcolata come:

   \[
   U = \left(\frac{\text{tempo utilizzato dal task}}{\text{tempo totale}}\right) * 100\%
   \]

### Esempio di Calcolo di U con più Task
Per il caso di più task con lo stesso periodo, il WCET totale è la somma dei WCET di ciascun task. Ad esempio, nel caso del LED-Show con `BlinkLed` e `ThreeLeds`, entrambi con periodo 500 ms:

- **WCET** per `BlinkLed` = 3 istruzioni → 0.03 s.
- **WCET** per `ThreeLeds` = 9 istruzioni → 0.09 s.
- **Utilizzo della CPU U** = \( \frac{0.03 + 0.09}{0.5} = 24\% \)

Se il WCET totale superasse il 100%, si verificherebbe un **overrun**, che può essere risolto aumentando il periodo della FSM, ottimizzando il codice, utilizzando un MCU più veloce, o rimuovendo funzionalità.

### Gestione di Task con Periodi Diversi
Per task con periodi diversi, si calcola il WCET sull’**iperperiodo** (minimo comune multiplo dei periodi). Ad esempio, per `BlinkLed` con periodo 300 ms e `ThreeLeds` con periodo 200 ms, l'iperperiodo è 600 ms, in cui `BlinkLed` viene eseguito 2 volte e `ThreeLeds` 3 volte. Il parametro U diventa:

   \[
   U = \frac{(2 \times 20 \text{ms} + 3 \times 90 \text{ms})}{600 \text{ms}} = 55\%
   \]

### Conclusione

L'approccio task-based semplifica la gestione di sistemi embedded complessi grazie a modularità, facilità di debugging e possibilità di riutilizzo. Tuttavia, richiede una gestione attenta delle variabili condivise, del consumo energetico e dell’utilizzo della CPU per evitare overrun e garantire l’affidabilità del sistema.

## Embedded basati su SoC e RTOS

### Introduzione 
- I sistemi embedded basati su **SoC (System-On-a-Chip)** superano i microcontrollori tradizionali, integrando una CPU, memoria sufficiente e componenti per ospitare un sistema operativo, spesso **RTOS (Real-Time Operating System)**.
- **RTOS**: sistema operativo progettato per rispondere a eventi in tempo reale, ottimizzato per sistemi con vincoli temporali stringenti.


### **SoC: System-On-a-Chip**
- **Definizione**: circuito integrato che combina componenti essenziali di un computer o sistema elettronico (CPU, memoria, controller I/O, interfacce di rete, ecc.).
- **Esempi**:
  - BROADCOM BCM2837 (Raspberry Pi 3).
  - ARM Sitara AM335x (BeagleBone, Arduino Tre).
  - ESP8266 e ESP32 (IoT).

- **Architettura di un SoC**
    - **Processori**: microcontroller, microprocessori, DSP.
    - **Memoria**: moduli integrati (ROM, RAM, EEPROM, FLASH).
    - **Interfacce standard**: USB, Ethernet, I²C, SPI.
    - **Connettività**: interfacce radio (Wi-Fi, Bluetooth).
    - **Componenti aggiuntivi**: DAC, ADC, timer, GPIO.

![](img\IOT\architettura_SoC.PNG)

- **SoC per IoT**
    - **ESP8266**: processore RISC 32-bit a 80 MHz, 64 KiB RAM istruzioni, Wi-Fi integrato IEEE 802.11 b/g/n.
    - **ESP32**: evoluzione dell’ESP8266, dual-core a 240 MHz, RAM 320 KiB, con Wi-Fi e Bluetooth v4.2, fino a 34 GPIO, ADC e DAC avanzati.

![](img\IOT\architettura_ESP32.PNG)
![](img\IOT\architettura_raspberry.PNG)

### Sistemi Operativi Embedded e RTOS
- I SoC forniscono le risorse necessarie per ospitare sistemi operativi completi, come RTOS, progettati per sistemi embedded.
- Gli **RTOS** ottimizzano la gestione di eventi e risorse, garantendo tempi di risposta deterministici.

- **Ruolo del Sistema Operativo**
    - Orchestrare l’esecuzione dei programmi applicativi.
    - Mediare l’accesso alle risorse hardware.
    - Fornire astrazione, controllo e protezione delle risorse.

- **Obiettivi principali dell’OS**
    1. **Esecuzione e controllo dei programmi**: gestione delle risorse hardware.
    2. **Ottimizzazione**: uso efficace delle risorse.
    3. **Coordinamento**: interazione tra applicazioni, utenti e risorse.


### Architettura a Livelli nei Sistemi Embedded
- La progettazione di un sistema è basata su una struttura gerarchica, composta da moduli che incapsulano funzionalità specifiche, organizzati su più livelli:
  - **Hardware**: circuiti logici, CPU, memoria.
  - **Sistema Operativo**: interfaccia tra hardware e software applicativo.
  - **Software Applicativo**: programmi e applicazioni.

(NON SICURO DELLA POSIZIONE DI QUESTA FORO SULLE SLIDEI CE NE SONO ALTRE DA VALUTARE)

![](img\IOT\overall.PNG)

- **Livelli e Interfacce Principali**
    1. **ISA (Instruction Set Architecture)**:
    - Interfaccia tra hardware e software.
    - Divisa in:
        - **User ISA**: istruzioni accessibili dai programmi utente.
        - **System ISA**: istruzioni privilegiate riservate all’OS.
    2. **ABI (Application Binary Interface)**:
    - Interfaccia che consente l’accesso a risorse hardware e servizi di sistema.
    - Composta da User ISA + System Call Interface.
    3. **System Call Interface**:
    - Funzionalità fondamentali offerte dall’OS ai programmi.
    - Permette il controllo dell’OS e l’accesso sicuro all’hardware.


### API e Mediatore OS
- **API (Application Programming Interface)**:
  - Fornisce una serie di funzioni o primitive OS (system calls) per interfacciarsi con le risorse hardware.
  - Garantisce indipendenza tra software applicativo e hardware.

- **Ruolo di Mediazione dell’OS**
    - Coordina e controlla l’accesso alle risorse hardware richiesto dalle applicazioni.
    - Converte richieste applicative in operazioni eseguibili sull’hardware.
    - Favorisce indipendenza tra applicazioni e hardware.

### Virtualizzazione e Astrazione
- **Macchina Virtuale**: permette di astrarre l’hardware fisico, fornendo un ambiente di esecuzione uniforme per le applicazioni.
- La virtualizzazione consente di suddividere il sistema in livelli più gestibili:
  - **Macchina fisica**: hardware reale.
  - **Macchina virtuale**: strato intermedio tra hardware e software.

### Organizzazione del Sistema Operativo
- **Driver**: gestione periferiche.
- **Gestore della memoria**: allocazione e traduzione della memoria.
- **Scheduler**: gestione della pianificazione dei processi.

### Sistema Operativo come Macchina Virtuale
- Il sistema operativo (OS) nasconde la complessità dell’hardware sottostante, presentando agli sviluppatori una macchina virtuale o astratta:
  - Più semplice rispetto alla macchina fisica.
  - Fornisce un livello superiore di astrazione.
  - Accessibile tramite chiamate di sistema (*system calls*), che fungono da interfaccia della macchina virtuale.

- **Vantaggi**
    1. **Facilità di sviluppo**: gli sviluppatori non devono conoscere i dettagli dell’hardware per accedere alle risorse.
    2. **Portabilità dei programmi**: lo stesso programma può essere eseguito su diverse macchine virtuali, semplificando il passaggio da un OS all’altro.


### Sistema Operativo come Gestore delle Risorse
- **Gestione delle risorse**:
  - Condivisione delle risorse tra più programmi, eventualmente in esecuzione concorrente.
  - Protezione e sicurezza per evitare interferenze tra programmi.
- **Funzioni principali**:
  1. Ottimizzazione dell’accesso (*scheduling*).
  2. Sicurezza e protezione dei dati.
  3. Gestione multi-utente e multi-programmazione.

### Virtualizzazione delle Risorse
- **Memoria virtuale**: ogni programma vede uno spazio di memoria lineare e teoricamente illimitato.
- **File system virtuale**: accesso uniforme ai file indipendentemente dal loro tipo o posizione (locale o remota).

- **Esecuzione dei Programmi**
    - **Multi-programmazione**:
    - Permette di caricare più programmi in memoria centrale e di eseguirli per ottimizzare l’uso della CPU.
    - Se un programma è in attesa di un’operazione I/O, la CPU viene assegnata a un altro programma.
    - **Time-sharing**:
    - Estende la multi-programmazione consentendo l’esecuzione concorrente di programmi che richiedono interazione con l’utente.
    - La CPU è condivisa tra i programmi in base a specifici algoritmi di scheduling.


### Sistemi Embedded e RTOS
- **Caratteristiche generali**:
  - Compattezza, efficienza, affidabilità.
  - Determinismo e prevedibilità (soprattutto nei sistemi hard real-time).
- **Differenze rispetto agli OS desktop**:
  - Un RTOS è progettato per eseguire una singola applicazione, solitamente multi-threaded.
- **Esempi**:
  - Open-source: FreeRTOS, eCos, RT Linux.
  - Commerciali: VxWorks, QNX, Windows IoT Core.


### Sistemi Real-Time
- **Classificazione**:
  - **Hard real-time**: le scadenze temporali devono essere rigorosamente rispettate (es. sistemi di sicurezza critici).
  - **Soft real-time**: le scadenze possono essere violate occasionalmente, ma devono essere gestite.
- **Determinismo**:
  - Essenziale per prevedere il tempo massimo necessario per completare un’azione.
  - Il sistema deve garantire tempi di latenza e di cambio contesto noti.


### Funzioni del Kernel di un RTOS
1. **Gestione dei task**:
   - Scheduling preemptivo per massimizzare l’uso della CPU.
   - Supporto per multi-threading e sincronizzazione (semafori, mutex).
2. **Gestione della memoria**:
   - Allocazione e deallocazione dinamica.
3. **Gestione I/O**:
   - Accesso controllato alle periferiche.
4. **Sicurezza e protezione**:
   - Prevenzione di problemi come il priority inversion.


### Scheduling nei Sistemi Real-Time
1. **Algoritmi principali**:
   - **Rate Monotonic (RM)**: assegna priorità fisse, dove i task con periodo più breve hanno priorità più alta.
   - **Earliest Deadline First (EDF)**: priorità dinamiche basate sulle scadenze temporali più vicine.
2. **Categorie di task**:
   - **Periodici**: rilasciati a intervalli regolari.
   - **Aperiodici**: rilasciati a tempi arbitrari.
   - **Sporadici**: come gli aperiodici, ma con scadenze rigide.
3. **Parametri temporali**:
   - Tempo di rilascio (r): quando il task è pronto per l’esecuzione.
   - Tempo di esecuzione (e): tempo massimo necessario per completare il task.
   - Scadenza (D): limite massimo entro cui il task deve essere completato.
   - Tempo di risposta (res): intervallo tra rilascio e completamento.

- **Vantaggi dell’RTOS**
    1. **Miglioramento della reattività**:
    - Evita il polling continuo sfruttando il cambio di contesto.
    2. **Facilitazione dello sviluppo**:
    - Fornisce un’astrazione che semplifica l’accesso all’hardware.
    3. **Modularità**:
    - Permette lo sviluppo modulare delle applicazioni.
    4. **Portabilità**:
    - Le applicazioni sono indipendenti dall’hardware sottostante grazie all’interfaccia RTOS.

- **Quando un RTOS non è necessario**
    - Applicazioni semplici basate su *super-loop*.
    - Applicazioni a singolo scopo o singolo task (es. dimensioni < 32 KiB).

## Internet of Things (IoT)  

### Definizione e Origini
- Il termine **Internet of Things (IoT)** è stato introdotto nel 1999 da Kevin Ashton, durante progetti sull'RFID al MIT.  
  - Obiettivo iniziale: digitalizzare automaticamente il mondo fisico (oggetti, identificazioni, misurazioni, eventi) tramite sensori che inviano dati in tempo reale a Internet, evitando errori manuali.   
- L'IoT ha un impatto significativo non solo sul piano tecnico ma anche sulla società, contribuendo a trasformazioni in vari settori.   

### Elementi Principali  
1. **“Things” (oggetti fisici)**:  
   - Tipicamente sistemi embedded dotati di sensori e attuatori.  
2. **Connettività e Comunicazione**:  
   - Uso di protocolli specifici come MQTT e CoAP per comunicare tramite Internet.  
   - Sfida nell'interoperabilità: l’IoT è considerato un sistema di sistemi.  
3. **Aspetti Critici**:  
   - **Sicurezza**: Identità, autenticazione e autorizzazione.  
   - **Privacy e proprietà dei dati**: Protezione delle informazioni sensibili.   

### Smart Things
- Gli oggetti smart combinano oggetti fisici, sensori e connessione Internet.  
- **Esempi di oggetti smart**:  
  - Interruttori WeMo, termostati Google Nest, smartwatch Fitbit.  
- Gli oggetti sono "incantati" (enchanted), secondo la visione di David Rose, integrando tecnologia avanzata in oggetti comuni.  

### Il Ruolo degli Smartphone nell'IoT
- Gli smartphone possono essere:  
  - **Sistemi embedded**: Dotati di sensori per raccogliere dati e inviarli a Internet.  
  - **Controller universali**: Interfacce utente per gestire dispositivi smart.  
  - **Unità di controllo**: Governano dispositivi vicini tramite Bluetooth e connessioni con dispositivi indossabili.   

### 5 Fasi dell’Evoluzione
1. **Prodotti base**: Dispositivi semplici come un condizionatore.  
2. **Prodotti smart**: Dispositivi programmabili, come un condizionatore con programmazione automatica.  
3. **Prodotti connessi**: Dispositivi controllabili via Internet, con manutenzione predittiva basata sui dati raccolti.  
4. **Sistemi di prodotti**: Dispositivi che collaborano (es. termostati che comunicano con tapparelle e pavimenti riscaldati).  
   - **Standard e piattaforme**:  
     - Iniziative come il Web of Things (WoT).  
     - Piattaforme come Apple HomeKit, Amazon Echo, e Samsung SmartThings.  
5. **Sistemi di sistemi**: Collaborazione tra elettrodomestici, sistemi di sicurezza, automobili e dispositivi medici.  

### Dall’IoT all’IoT Industriale e Aziendale  
- **Industry 4.0**  
  - La quarta rivoluzione industriale si basa sull’integrazione di sensori, Big Data e sistemi in tempo reale per ottimizzare la produzione e i processi aziendali.  
  - **Differenze tra Enterprise IoT e Industrial IoT (I-IoT)**:  
    - **Enterprise IoT**: Termine generico per applicazioni IoT nel contesto aziendale.  
    - **I-IoT**: Specifico per il settore manifatturiero e industriale.  

### Architettura e Sistemi SCADA  
- **Sistemi SCADA**: Supervisory Control and Data Acquisition (SCADA): Sistemi industriali per monitorare e controllare processi su larga scala.  
  - **Elementi principali**:  
    - **RTU (Remote Terminal Units)**: Rilevano e digitalizzano i dati dai sensori.  
    - **PLC (Programmable Logic Controller)**: Supervisionano la raccolta dati e controllano i dispositivi.  
    - **MTU (Master Terminal Unit)**: Server di controllo che elabora e archivia i dati.  
    - **HMI (Human-Machine Interface)**: Interfaccia per operatori umani.  
    - **Historian**: Software per l'archiviazione e analisi di dati temporali.  

- **PLC e Standard IEC 61131-3**: Programmazione dei PLC tramite linguaggi standard come:  
  - **Diagrammi Ladder** (visuale).  
  - **Blocchi funzionali** (visuale).  
  - **Testo strutturato** (testuale).  
  - **Grafici sequenziali** (per programmi complessi). 

### Standard OPC: Open Platform Communication
- L'OPC è uno **strato software** che facilita l'interazione tra le sorgenti di dati industriali e i sistemi esterni.  
- Funzioni principali:  
  - Traduce i protocolli specifici di **PLC** (Programmable Logic Controller) o **DCS** (Distributed Control Systems), come Modbus e Profibus, in un'interfaccia standard.  
  - Agisce come mediatore per sistemi SCADA e simili, convertendo richieste OPC generiche in richieste specifiche per i dispositivi, e viceversa.  
  - Espone **tag**, serie temporali, eventi e sequenze di eventi (SOE) ai sistemi che implementano l'interfaccia OPC.  

### Specifiche OPC 
1. **OPC Classic**:  
   - Introdotto nel 1995.  
   - Basato su Windows, utilizza tecnologie come OLE e DCOM.  
2. **OPC-UA (Unified Architecture)**:  
   - Definito nel 2005 secondo lo standard **IEC 62451**.  
   - Architettura orientata ai servizi (Service-Oriented Architecture, SOA).  
   - Compatibile con dispositivi piccoli e non solo su Windows.  

### Il Dispositivo Edge 
- Situato fisicamente in fabbrica, il dispositivo edge collega:  
  - **Dati industriali** tramite server OPC.  
  - **Cloud** tramite gateway IoT. Il Cloud Computing è un modello di erogazione di servizi IT che consente l'accesso on-demand a un pool condiviso di risorse computazionali configurabili (ad esempio, reti, server, storage, applicazioni e servizi) che possono essere rapidamente fornite e rilasciate con uno sforzo minimo di gestione o interazione con il fornitore di servizi. Questo modello offre diversi vantaggi, tra cui scalabilità, flessibilità, efficienza dei costi e accessibilità globale.
- I dispositivi edge sono fondamentali per l’implementazione dell'IIoT e si adattano a diversi approcci industriali.  

### IoT e Cloud
- **Caratteristiche Principali del Cloud nell'IoT**  
  - **Capacità di invio dati** direttamente o indirettamente su Internet.  
  - **Gestione di Big Data e Big Streams**:  
    - Necessaria per i sensori che generano grandi volumi di dati non archiviabili localmente.  
  - **Servizi offerti dal cloud**:  
    - Gestione dispositivi.  
    - Archiviazione e analisi dati offline.  
    - Sistemi aperti per lo scambio dati tra applicazioni, incluse le mobile app.  

### Modelli di Cloud Computing  
  1. **IaaS** (Infrastructure as a Service):  
    - Risorse virtualizzate come server, rete e storage.  
  2. **PaaS** (Platform as a Service):  
    - Runtime di esecuzione, database, server web, IDE.  
  3. **SaaS** (Software as a Service):  
    - Applicazioni come CRM, suite per ufficio, email.

![](img\IOT\livelli_cloud.PNG)  

### Domini Applicativi e Sfide dell'IoT
- **Applicazioni e Smart City**  
  - **Domini applicativi**: Logistica, smart home, eHealth, smart city.  
  - **Smart City**:  
    - Utilizzo di infrastrutture IoT e servizi cloud per ottimizzare i servizi urbani (Urban OS).  
- **Sfide Critiche**  
  1. **Sicurezza**: Protezione dei dispositivi e delle comunicazioni.  
  2. **Privacy**: Garanzia della protezione dei dati personali.  
  3. **Interoperabilità**: Standard e architetture di riferimento per l’integrazione a livello applicativo.  


### Web of Things (WoT)
- **Definizione e Obiettivi**  
  - Il **Web of Things (WoT)** integra i dispositivi IoT nel Web, fornendo API RESTful.  
    - Abilita l'interoperabilità a livello applicativo.  
    - Supporta protocolli sottostanti come Zigbee, Bluetooth, 6LoWPAN.  

- **Topologie di Rete nel WoT**  
  1. **Star Topology**:  
    - Nodo centrale che connette tutti gli altri dispositivi.  
  2. **Mesh Topology**:  
    - Nessun nodo centrale; i dispositivi inoltrano i messaggi creando una rete estesa e resiliente.  

- **Vantaggi del WoT**  
  - Maggiore semplicità di programmazione.  
  - Integrazione rapida di dati e servizi.  
  - Soluzioni ottimizzate per dispositivi embedded con basso consumo energetico.  

### Mobile e Wearable Computing nell'IoT  

- **Mobile Computing**  
  - **Dispositivi mobili**: Smartphone e tablet.  
    - Interfacce per interagire con dispositivi IoT.  
    - Raccolta e analisi di dati tramite sensori.  

- **Wearable Computing**  
  - **Dispositivi indossabili**: Smartwatch, smartglasses.  
    - Tipicamente connessi a dispositivi mobili tramite Bluetooth.  
    - Estensione dell’interazione con ambienti fisici tramite realtà aumentata (AR) o mista (XR).  

## Comunicazione nei Sistemi M2M e IoT

- **Ruolo della comunicazione**:
  - Fondamentale per consentire lo scambio di dati tra dispositivi e sottosistemi.
- **Tipologie di connessione**:
  - **Cablate**: utilizzano moduli come shield/board con porte Ethernet e supporto per protocollo 802.11.
  - **Wireless**: impiegano moduli trasmettitori/ricevitori integrati o USB dongle.
- **Interfaccia microcontrollore-modulo**:
  - Avviene tramite **porta seriale**.

### Connessione Internet nei Dispositivi Embedded
- **Modalità principali**:
  1. **Connessione indiretta**:
     - Comunicazione tramite un nodo intermediario che funge da gateway.
     - Tecnologie: ZigBee, Bluetooth.
  2. **Connessione diretta**:
     - Modulo ricevitore/trasmettitore montato direttamente sul dispositivo.
     - Tecnologie: 3G/4G/5G, Wi-Fi.
- **Protocolli di riferimento**:
  - **IP**, **TCP/IP**, **UDP/IP**.

### Architettura ISO-OSI e Internet Stack
- Struttura a strati per standardizzare la comunicazione.
- Nello stack Internet, IP funge da "collo di bottiglia" permettendo l'interoperabilità tra protocolli superiori e inferiori.

### Comunicazioni Wireless
- **Principi di base**:
  - Utilizzano segnali elettromagnetici in frequenza radio (RF).
  - Classificazione:
    - **Terrestre**: basata su infrastrutture a terra.
    - **Satellitare**: basata su infrastrutture in orbita terrestre.
- **Categorie principali**:
  - **Short Range**: decine di metri (Bluetooth, Visible Light Communication).
  - **Medium Range**: centinaia di metri (Wi-Fi, WPAN).
  - **Long Range**: distanze superiori a 1 miglio (reti cellulari, LPWA).

### Topologie di Rete Wireless
- **Tipologie utilizzate**:
  - **Punto a Punto (P2P)**.
  - **Stella**.
  - **Albero (Tree)**.
  - **Mesh**: comunicazione ridondante e resiliente.

### Tecnologie Wireless
#### Wi-Fi
- Standard: **IEEE 802.11x**.
- Caratteristiche principali:
  - Velocità: fino a 54 Mbps.
  - Distanza: ~150 metri.
  - Frequenza: 5 GHz.
- Limiti:
  - Elevato consumo energetico, non ideale per sistemi embedded.

#### Reti Cellulari (pre-5G)
- Tecnologie: GPRS, 3G, WiMax, LTE (4G).
- Caratteristiche:
  - Velocità: da 80 Kbps (GPRS) a vari Mbps (3G/4G).
  - Portata: chilometri.
  - Frequenze: 800-1900 MHz.
- Consumo elevato e latenza incompatibile alle necessità, poco adatte per IoT.

#### 5G
- Progettato per IoT:
  - Velocità: fino a 10 Gbps.
  - Bassa latenza: 1-10 ms.
  - Affidabilità e flessibilità elevate.
  - Ideale per sensori, wearable e applicazioni IoT.

#### Bluetooth (BT)
Bluetooth è uno standard largamente adottato per la trasmissione di dati in reti personali wireless (WPAN). La sua flessibilità e basso consumo energetico lo rendono ideale per applicazioni su dispositivi di consumo e IoT.  

- **Caratteristiche Generali**
  - **Standard**: **IEEE 802.15.1**, inizialmente sviluppato da Ericsson nel 1994 e formalizzato dal Bluetooth Special Interest Group (SIG), che include Sony Ericsson, IBM, Intel, Toshiba e Nokia.
  - **Ambito di applicazione**: 
    - Ampiamente utilizzato in dispositivi come smartphone, tablet, laptop, stampanti, fotocamere digitali.
    - Ideale per la comunicazione a breve distanza (fino a decine di metri).  
  - **Obiettivi principali**:  
    - Ridotto consumo energetico.  
    - Comunicazione a basso costo.  
    - Facilità di connessione dinamica.  

- **Tecnologia e Prestazioni**
  - **Frequenza operativa**: 2,45 GHz (banda libera).  
  - **Tecnica di trasmissione**: **Frequency hopping** (cambi di frequenza 1.600 volte al secondo per ridurre le interferenze).  
  - **Velocità**:
    - Versioni 1.1 e 1.2: fino a 723,1 kbit/s.
    - Versione 2.0: modalità ad alta velocità fino a 3 Mbit/s (ma con maggiore consumo energetico).  
    - Versioni successive ottimizzano il consumo energetico con segnali più corti rispetto al Bluetooth 1.2.  

- **Classi di Dispositivi**
  - **Classi BT**:
    - I dispositivi Bluetooth si dividono in quattro classi, basate su consumo energetico e portata:
      - **Classe 1**: Alta potenza, portata fino a 100 metri.  
      - **Classe 2**: Potenza intermedia, portata di circa 10 metri (la più comune).  
      - **Classe 3**: Bassa potenza, portata ridotta a pochi metri.  

- **Topologie di Rete**
  - **Piconet**:
    - Architettura **master-slave**.
    - Un master può gestire fino a 7 dispositivi slave.  
    - La comunicazione è sincronizzata con il clock del master.
  - **Scatternet**:
    - Interconnessione tra più piconet.  
    - Un dispositivo slave può partecipare a più piconet contemporaneamente.  
    - Un master di una piconet può essere slave in un'altra.  
    - Possibilità di formare reti più grandi e flessibili.  

- **Tipi di Connessione**
  - **Connessione orientata**: Richiede l'instaurazione di una connessione prima di inviare dati.  
  - **Connessione senza stato**: Non richiede connessione; i pacchetti vengono inviati direttamente conoscendo l'indirizzo del ricevitore.  
  - **Tipologie specifiche**:
    - **ACL** (Asynchronous ConnectionLess): Trasmissione dati best-effort.  
    - **SCO** (Synchronous Connection Oriented): Trasmissione in tempo reale, adatta a dati multimediali.

- **Stack del Protocollo**
  - Organizzato in strati, simile all'architettura ISO/OSI.  
  - Include livelli fisici e data-link come minimo.  
  - **RFCOMM**:
    - Protocollo utilizzato per emulare porte seriali RS-232, consentendo una connessione senza soluzione di continuità con dispositivi compatibili.

- **Profili Bluetooth**
  Per facilitare l'adozione e l'uso, sono stati definiti profili applicativi come:
    - **GAP** (Generic Access Profile).  
    - **SDAP** (Service Discovery Application Profile).  
    - **SPP** (Serial Port Profile).  
    - **HSP** (Headset Profile).  
    - **FTP** (File Transfer Profile).  
    - Altri, per applicazioni specifiche come intercomunicazione, trasferimento file, sincronizzazione, etc.

- **Sicurezza**
  - Algoritmo **SAFER+** per l'autenticazione dei dispositivi e la generazione di chiavi per la crittografia dei dati.

- **Evoluzione di Bluetooth**
  - **Versione 4.0 (Bluetooth Smart)**:
    - Include:
      - **Classic Bluetooth**: Versioni precedenti.  
      - **Bluetooth High Speed**: Basato su Wi-Fi.  
      - **Bluetooth Low Energy (BLE)**: Specificamente progettato per IoT.  
    - Caratteristiche BLE:
      - Consumo energetico ridotto.  
      - Comunicazione più reattiva.  
      - Implementazioni: 
        - **Single-mode** (solo stack BLE).  
        - **Dual-mode** (integrazione con funzioni Classic).
  - **Bluetooth 5**:
    - Disponibile dal 2016, ottimizzato per IoT.
    - Portata quadruplicata a pari consumo.
    - Velocità raddoppiata fino a 2 Mbps in modalità low-power.

- Bluetooth Low Energy (BLE)
  - Evoluzione di BT, introdotta con **Bluetooth 4.0**.
  - Caratteristiche:
    - Minore consumo energetico.
    - Comunicazione ottimizzata per IoT.
    - Presenta la capacità di aggiornare i collegamenti in maniera dinamenica
  - Versione **Bluetooth 5**:
    - Area di trasmissione quadruplicata con lo stesso consumo.
    - Velocità raddoppiata fino a 2 Mbps.

![](img\IOT\bt.PNG)

### Standard IEEE 802.15.4
- Standard per WPAN a basso costo e bassa velocità.
- Caratteristiche:
  - Frequenza: 2.4 GHz, 900 MHz, 868 MHz.
  - Velocità: fino a 250 kbps.
  - Portata: 100 m - 1 Km.
- Applicazioni:
  - Automazione domestica e industriale.
  - Reti di sensori wireless.
- Implementazioni:
  - **ZigBee**: basso consumo, ideale per IoT.
  - **6LoWPAN**: ottimizzazione IPv6 per reti a bassa potenza.

### ZigBee
- Basato su IEEE 802.15.4.
- Dispositivi:
  - **Coordinator**: unico per rete, gestisce sicurezza e configurazione.
  - **Router**: instrada dati tra dispositivi.
  - **End Device**: limitate capacità di comunicazione.
- Topologie:
  - **Stella**, **Albero**, **Mesh**.

### Thread Protocol
- Protocollo IPv6 per WPAN in **mesh network**.
- Progettato per:
  - Automazione domestica e connettività cloud.
  - Sicurezza, affidabilità e basso consumo.

### Matter
- Standard aperto per la connettività smart home e IoT (dal 2022).
- Supporto da giganti come Amazon, Apple e Google.
- Obiettivo: interoperabilità tra dispositivi smart, sostituendo protocolli proprietari.

### Protocolli di Livello Applicativo
- **Tipologie**:
  - **Generici**: SCADA, UDP/TCP.
  - **Specifici per IoT**:
    - **MQTT**: leggero, basato su pubblicazione/sottoscrizione.
    - **CoAP**: ottimizzato per reti a bassa potenza e perdita.

