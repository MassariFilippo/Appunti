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

