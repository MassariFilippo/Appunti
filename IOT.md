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

#### Esempio Implementativo: LED-Show su Arduino

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

#### Implementazione del Scheduler

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

#### Esempio di Calcolo di U con più Task

Per il caso di più task con lo stesso periodo, il WCET totale è la somma dei WCET di ciascun task. Ad esempio, nel caso del LED-Show con `BlinkLed` e `ThreeLeds`, entrambi con periodo 500 ms:

- **WCET** per `BlinkLed` = 3 istruzioni → 0.03 s.
- **WCET** per `ThreeLeds` = 9 istruzioni → 0.09 s.
- **Utilizzo della CPU U** = \( \frac{0.03 + 0.09}{0.5} = 24\% \)

Se il WCET totale superasse il 100%, si verificherebbe un **overrun**, che può essere risolto aumentando il periodo della FSM, ottimizzando il codice, utilizzando un MCU più veloce, o rimuovendo funzionalità.

#### Gestione di Task con Periodi Diversi

Per task con periodi diversi, si calcola il WCET sull’**iperperiodo** (minimo comune multiplo dei periodi). Ad esempio, per `BlinkLed` con periodo 300 ms e `ThreeLeds` con periodo 200 ms, l'iperperiodo è 600 ms, in cui `BlinkLed` viene eseguito 2 volte e `ThreeLeds` 3 volte. Il parametro U diventa:

   \[
   U = \frac{(2 \times 20 \text{ms} + 3 \times 90 \text{ms})}{600 \text{ms}} = 55\%
   \]

### Conclusione

L'approccio task-based semplifica la gestione di sistemi embedded complessi grazie a modularità, facilità di debugging e possibilità di riutilizzo. Tuttavia, richiede una gestione attenta delle variabili condivise, del consumo energetico e dell’utilizzo della CPU per evitare overrun e garantire l’affidabilità del sistema.