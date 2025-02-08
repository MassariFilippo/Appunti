<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });</script>

# Embedded Systems and Internet of Things

<div style="page-break-after: always;"></div>

- [Embedded Systems and Internet of Things](#embedded-systems-and-internet-of-things)
- [Sistemi Embedded](#sistemi-embedded)
  - [Definizione e Caratteristiche](#definizione-e-caratteristiche)
    - [Definizione di Sistemi Embedded](#definizione-di-sistemi-embedded)
    - [Caratteristiche Principali](#caratteristiche-principali)
  - [Applicazioni dei Sistemi Embedded](#applicazioni-dei-sistemi-embedded)
  - [Sistemi Cyber-Fisici (CPS)](#sistemi-cyber-fisici-cps)
    - [Struttura dei CPS](#struttura-dei-cps)
  - [Architettura dei Sistemi Embedded](#architettura-dei-sistemi-embedded)
  - [Tecnologie della CPU](#tecnologie-della-cpu)
    - [Tipologie di Processori](#tipologie-di-processori)
    - [Processori a Scopo Specifico](#processori-a-scopo-specifico)
      - [Tipologie di PLD](#tipologie-di-pld)
  - [SoC, Microcontrollori, SBC e SBM nell’IoT](#soc-microcontrollori-sbc-e-sbm-nelliot)
    - [Microcontrollore](#microcontrollore)
    - [SoC (System on Chip)](#soc-system-on-chip)
    - [Single-Board Microcontroller (SBM)](#single-board-microcontroller-sbm)
    - [Single-Board Computer (SBC)](#single-board-computer-sbc)
    - [ESP32: SoC vs. SBM](#esp32-soc-vs-sbm)
  - [Confronti Dettagliati](#confronti-dettagliati)
    - [Microcontrollore vs. SoC](#microcontrollore-vs-soc)
    - [SBM vs. SBC](#sbm-vs-sbc)
  - [Esempi di Dispositivi](#esempi-di-dispositivi)
    - [Microcontroller Unit (MCU)](#microcontroller-unit-mcu)
      - [Esempi di Microcontrollori](#esempi-di-microcontrollori)
    - [Microcontrollori vs. Microprocessori](#microcontrollori-vs-microprocessori)
    - [Single-Board Microcontroller](#single-board-microcontroller)
      - [Famiglia Arduino](#famiglia-arduino)
    - [ESP](#esp)
    - [SoC (System-on-a-Chip)](#soc-system-on-a-chip)
      - [Famiglia Raspberry Pi](#famiglia-raspberry-pi)
  - [Sensori e Attuatori](#sensori-e-attuatori)
    - [Sensori](#sensori)
    - [Attuatori](#attuatori)
  - [Protocolli di Comunicazione](#protocolli-di-comunicazione)
- [Microcontrollori](#microcontrollori)
  - [Introduzione](#introduzione)
  - [Componenti Principali](#componenti-principali)
  - [Architetture delle CPU nei Microcontrollori](#architetture-delle-cpu-nei-microcontrollori)
    - [Architettura Von Neumann](#architettura-von-neumann)
    - [Architettura Harvard](#architettura-harvard)
  - [Memoria nei Microcontrollori](#memoria-nei-microcontrollori)
  - [Esempio di Microcontrollore: Arduino Uno](#esempio-di-microcontrollore-arduino-uno)
  - [GPIO - General Purpose Input/Output](#gpio---general-purpose-inputoutput)
    - [GPIO su ATMega328P](#gpio-su-atmega328p)
    - [Parametri Operativi](#parametri-operativi)
  - [Programmazione dei Microcontrollori](#programmazione-dei-microcontrollori)
    - [Caso Arduino](#caso-arduino)
  - [Super Loop](#super-loop)
    - [Vantaggi](#vantaggi)
    - [Svantaggi](#svantaggi)
  - [Ciclo di Esecuzione e Prestazioni](#ciclo-di-esecuzione-e-prestazioni)
  - [Assembly AVR](#assembly-avr)
  - [Conclusione](#conclusione)

<div style="page-break-after: always;"></div>

# Sistemi Embedded

## Definizione e Caratteristiche

### Definizione di Sistemi Embedded
I **sistemi embedded** sono sistemi informatici a scopo speciale, progettati per svolgere una funzione o un compito specifico all'interno di dispositivi o sistemi fisici/elettronici.

### Caratteristiche Principali
- **Interazione con il mondo fisico** tramite sensori e attuatori.
- **Struttura** composta da hardware e software (anche se in alcuni casi il software può mancare).
- **Funzionalità specifica** per un'applicazione particolare.
- **Esecuzione continua**, spesso in loop infinito.
- **Progettazione robusta** e ottimizzata in termini di risorse.
- **Vincoli stringenti** su CPU, memoria e consumo energetico.
- **Metriche di progettazione**:
  - Costo (inclusi i costi NRE - Non-Recurring Engineering)
  - Dimensioni, prestazioni, efficienza energetica
- **Sistemi critici**:
  - Elevata affidabilità e disponibilità
  - Sicurezza e protezione (safety & security)
- **Reattività e real-time**:
  - Devono rispondere agli stimoli dell'ambiente entro un limite di tempo prestabilito.
  - Nei sistemi **hard real-time**, il mancato rispetto della scadenza porta al fallimento del sistema.

## Applicazioni dei Sistemi Embedded

I sistemi embedded trovano applicazione in diversi settori:

- **Elettrodomestici**: dispositivi smart per la casa (es. termostati Nest, serrature Kevo).
- **Automotive**: controllo motore, sistemi di sicurezza.
- **Avionica**: controllo di volo, navigazione.
- **Industria**: automazione industriale, Industry 4.0.
- **Sanità**: dispositivi medici (es. WristOx).
- **Dispositivi mobili e indossabili**: smartwatch, braccialetti fitness.

## Sistemi Cyber-Fisici (CPS)

I **sistemi cyber-fisici (CPS)** integrano computazione con processi fisici e si distinguono dai normali sistemi di elaborazione delle informazioni per:

- **Gestione del tempo**: essenziale per la correttezza del sistema.
- **Concorrenza**: i processi fisici avvengono in parallelo.
- **Reattività** e gestione di eventi asincroni.

### Struttura dei CPS
- **Parte fisica**: dispositivi, sistemi meccanici/biologici, utenti.
- **Parte computazionale**: piattaforme di calcolo con sensori, attuatori e computer.
- **Parte di rete**: meccanismi di connessione tra le piattaforme computazionali.

## Architettura dei Sistemi Embedded

Componenti principali:

- **CPU (Central Processing Unit)**
- **Memoria ROM (Read-Only Memory)**
- **Memoria RAM (Random Access Memory)**
- **Sensori e dispositivi di input**
- **Attuatori e dispositivi di output**
- **Circuiteria specifica per applicazione**
- **Interfacce di comunicazione**

## Tecnologie della CPU

### Tipologie di Processori

1. **Processori general-purpose**: architettura predefinita con un set di istruzioni (ISA); l'esecuzione è definita dal software.
2. **Processori a scopo specifico**: circuiti digitali progettati per un compito specifico (es. **ASIC** - Application-Specific Integrated Circuit).
3. **Processori specifici per applicazioni (ASIP)**: programmabili ma ottimizzati per una classe di applicazioni (es. microcontrollori, SoC, DSP).

### Processori a Scopo Specifico

- **Full-Custom/VLSI**: progettazione completamente personalizzata.
- **Semi-custom (ASIC)**: utilizzo di livelli predefiniti.
- **PLD (Programmable Logic Device)**: dispositivi logici programmabili.

#### Tipologie di PLD

- **PLA (Programmable Logic Array)**: array di porte logiche programmabili.
- **PAL (Programmable Array Logic)**: variante semplificata del PLA.
- **FPGA (Field Programmable Gate Array)**: circuiti integrati programmabili via software, utilizzabili per logiche complesse.
  - **Linguaggi di programmazione**: Verilog, VHDL, LabView.

## SoC, Microcontrollori, SBC e SBM nell’IoT

### Microcontrollore

- Un **microcontrollore (MCU)** è un piccolo computer su un chip con CPU, RAM, memoria flash e I/O integrati.
- Non esegue sistemi operativi complessi, ma codice specifico (bare-metal o RTOS).
- **Esempi**: ATmega328 (Arduino Uno), ESP8266, STM32.

### SoC (System on Chip)

- Un **SoC** è un chip che integra CPU, RAM, storage, connettività e periferiche su un unico circuito integrato.
- Usato in dispositivi embedded, smartphone e hardware IoT.
- **Esempi**: ESP32, ESP8266, Broadcom BCM2837 (Raspberry Pi 3).

### Single-Board Microcontroller (SBM)

- Un **SBM** è una scheda che integra un microcontrollore con circuiti di supporto per alimentazione, GPIO e I/O.
- Non esegue un sistema operativo completo, ma codice specifico.
- **Esempi**: ESP32 DevKit, Arduino Uno.

### Single-Board Computer (SBC)

- Una **SBC** è un computer su un’unica scheda con CPU, RAM, storage e interfacce di comunicazione.
- Supporta sistemi operativi come Linux o Windows IoT.
- Ha più potenza e memoria rispetto a un microcontrollore.
- **Esempi**: Raspberry Pi, NVIDIA Jetson Nano.

### ESP32: SoC vs. SBM

- Il **chip ESP32** standalone è un **SoC** perché integra CPU, RAM, Wi-Fi/Bluetooth e I/O.
- Quando montato su una **scheda di sviluppo** (es. ESP32 DevKit), diventa un **Single-Board Microcontroller (SBM)**.
- **Non** è una **SBC** perché non ha le risorse per eseguire un OS come Linux.

## Confronti Dettagliati

### Microcontrollore vs. SoC

| **Caratteristica**     | **Microcontrollore (MCU)**                               | **SoC (System on Chip)**                                            |
|------------------------|----------------------------------------------------------|---------------------------------------------------------------------|
| **Definizione**        | Un chip con CPU, RAM, memoria flash e I/O, progettato per compiti specifici. | Un chip che integra CPU, GPU (se presente), RAM, storage e periferiche su un unico circuito. |
| **Esempi**             | ATmega328 (Arduino Uno), STM32, PIC                      | ESP32, ESP8266, Broadcom BCM2837 (Raspberry Pi 3)                   |
| **Sistema Operativo**  | Nessuno o RTOS                                           | Può supportare un OS (es. Linux) se ha abbastanza risorse           |
| **Memoria RAM**        | Centinaia di bytes o KB                                  | Da pochi MB a diversi GB                                            |
| **Storage**            | Memoria flash interna (pochi KB o MB)                    | Memoria flash interna o supporto microSD/eMMC                       |
| **Connettività**       | Limitata (es. UART, I2C, SPI)                            | Può includere Wi-Fi, Bluetooth, Ethernet, USB                       |
| **Consumo energetico** | Molto basso, ideale per sistemi a batteria               | Più elevato rispetto a un microcontrollore                          |
| **Esecuzione del codice** | Esegue un singolo programma specifico                | Può eseguire più processi contemporaneamente                        |
| **Uso tipico**         | Automazione, sensori, controllo motori                    | Smartphone, SBC, dispositivi IoT avanzati                            |

### SBM vs. SBC

| **Caratteristica**     | **SBM (Single-Board Microcontroller)**                   | **SBC (Single-Board Computer)**                                     |
|------------------------|----------------------------------------------------------|---------------------------------------------------------------------|
| **Definizione**        | Scheda con microcontrollore e circuiti di supporto per GPIO, alimentazione e I/O. | Computer completo su una scheda, con CPU, RAM, storage e interfacce di comunicazione. |
| **Esempi**             | ESP32 DevKit, Arduino Uno                                | Raspberry Pi, Jetson Nano                                           |
| **Sistema Operativo**  | Nessuno o RTOS                                           | Linux, Windows IoT                                                  |
| **CPU**                | Microcontrollore (Xtensa, AVR, ARM Cortex-M)             | Processore ARM/x86 più potente                                      |
| **RAM**                | Centinaia di KB                                          | 512 MB o più                                                        |
| **Storage**            | Flash interna (pochi MB)                                 | microSD, eMMC, SSD                                                  |
| **Periferiche**        | GPIO, UART, I2C, SPI                                     | USB, HDMI, Ethernet, Wi-Fi                                          |
| **Uso tipico**         | Sensori, automazione, IoT a basso consumo                | Edge computing, AI, server leggeri                                  |

## Esempi di Dispositivi

### Microcontroller Unit (MCU)

I microcontrollori si differenziano dai microprocessori perché integrano su un unico chip tutti i componenti necessari:

- **CPU**, memoria persistente e volatile, canali di I/O, unità di gestione delle interruzioni e altri componenti specializzati.
- Possono essere basati su architettura **CISC** (Von Neumann) o **RISC** (es. MSP430).
- Classificati in **8, 16, 32 bit**.

#### Esempi di Microcontrollori

- **Storici**: Motorola 68000, Intel 8080, Zilog Z80, Intel 8051.
- **Moderni**: Atmel AVR, Texas Instruments MSP430, Microchip PIC16C84, ARM 32-bit, PowerPC.

### Microcontrollori vs. Microprocessori

| **Caratteristica**    | **Microcontrollore** | **Microprocessore** |
|-----------------------|----------------------|---------------------|
| **Max clock speed**   | 200 MHz              | 4 GHz               |
| **Max MegaFLOPS**     | 200                  | 5000                |
| **Consumo energetico**| 1 W                  | 50 W                |

### Single-Board Microcontroller

Le soluzioni single-board integrano un microcontrollore e i circuiti necessari per eseguire compiti di controllo.

- **Arduino** (mercato consumer e maker).
- **XMC Family** (industriale).

#### Famiglia Arduino

- **Arduino UNO**: Microcontrollore a 8 bit, 16 MHz, 2 KB di SRAM, 32 KB di flash memory, 14 pin digitali e 6 pin analogici.
- **Arduino Mega**: 8 bit, 16 MHz, 8 KB di SRAM, 256 KB di flash memory, 54 pin digitali e 16 pin analogici.
- **Arduino Yun**: 32 bit, 400 MHz, 64 MB di RAM, 16 MB di flash memory.
- **Arduino M0**: 32 bit, 48 MHz, 32 KB di SRAM, 256 KB di flash memory.

### ESP

- **ESP8266**: SoC per IoT con processore a 32 bit, 80 MHz, 64 KB di RAM per istruzioni, 96 KB di RAM per dati, 16 pin GPIO, Wi-Fi integrato.
- **ESP32**: Successore dell'ESP8266 con processore dual-core a 32 bit, 160-240 MHz, 520 KB di RAM, 448 KB di ROM, 34 pin GPIO, Wi-Fi e Bluetooth integrati.

### SoC (System-on-a-Chip)

- Integra CPU, memoria, controller I/O e di rete.
- **Esempi**: Broadcom BCM2837 (Raspberry Pi 3), ARM Sitara AM335x (BeagleBone).

#### Famiglia Raspberry Pi

- **Raspberry Pi (2012)**: SoC Broadcom BCM2835, 700 MHz, 256 MB RAM.
- **Raspberry Pi 2 (2015)**: SoC Broadcom BCM2836, 900 MHz quad-core, 1 GB RAM.
- **Raspberry Pi 3 (2016)**: SoC Broadcom BCM2837, 1.2 GHz quad-core, 1 GB RAM.
- **Raspberry Pi 4 (2019)**: SoC Broadcom BCM2711, 1.5 GHz quad-core, 1-4 GB RAM.
- **Raspberry Pi 5 (2023)**: SoC Broadcom BCM2712, 2.4 GHz quad-core, 4-8 GB RAM.

## Sensori e Attuatori

### Sensori

- Dispositivi che misurano fenomeni fisici (temperatura, umidità, accelerazione) o chimici (fumo).
- Possono essere **analogici** o **digitali**.

### Attuatori

- Dispositivi che producono effetti misurabili sull'ambiente.

## Protocolli di Comunicazione

- **I2C**, **SPI**, **JTAG**: Protocolli di comunicazione seriale.
- **CAN-bus**: Protocollo seriale usato nel settore automobilistico.
- **UART**: Protocollo seriale asincrono per la conversione di flussi di bit paralleli in sequenziali.
- **Wireless**: Bluetooth, ZigBee, Z-Wave, LoRaWAN, Wi-Fi.

# Microcontrollori

## Introduzione

I **microcontrollori** sono sistemi integrati costituiti da diversi componenti essenziali che consentono di eseguire compiti specifici in modo autonomo. Sono utilizzati in una vasta gamma di applicazioni, dai dispositivi elettronici di consumo ai sistemi industriali.

## Componenti Principali

Un microcontrollore è composto dai seguenti componenti fondamentali:

- **CPU (Central Processing Unit)**: il cervello del microcontrollore che esegue le istruzioni del programma.
- **Memoria**:
  - **Flash Memory**: memoria non volatile utilizzata per memorizzare il codice del programma.
  - **SRAM (Static RAM)**: memoria volatile per l'archiviazione temporanea dei dati durante l'esecuzione.
  - **EEPROM (Electrically Erasable Programmable Read-Only Memory)**: memoria non volatile per la conservazione di dati persistenti.
- **Porte di I/O Generiche (GPIO)**: pin configurabili come ingressi o uscite per interfacciarsi con altri dispositivi.
- **Convertitori Analogico/Digitale (ADC)**: componenti che convertono segnali analogici in valori digitali.
- **Timer**: utilizzati per operazioni temporizzate e contatori.
- **Bus di Comunicazione Seriali**: protocolli come **SPI**, **I2C**, **UART** per la comunicazione con altri dispositivi.
- **Clock**: fornisce il sincronismo al sistema, determinando la velocità di esecuzione delle istruzioni.
- **Circuito di Alimentazione**: gestisce la tensione e la corrente necessarie al funzionamento del microcontrollore.

## Architetture delle CPU nei Microcontrollori

Le architetture della CPU nei microcontrollori determinano il modo in cui la CPU accede alla memoria e gestisce le istruzioni.

### Architettura Von Neumann

- Segue un ciclo **Fetch-Decode-Execute**:
  1. **Fetch**: preleva l'istruzione dalla memoria.
  2. **Decode**: decodifica l'istruzione prelevata.
  3. **Execute**: esegue l'operazione e aggiorna registri o memoria.
- Utilizza un unico bus per istruzioni e dati, il che può limitare le prestazioni.

### Architettura Harvard

- Distingue tra memoria per le **istruzioni** e memoria per i **dati**, con bus separati.
- Migliora le prestazioni e l'efficienza energetica.
- Utilizzata in microcontrollori come l'**ATMega328P**.
- Memoria **Flash** per il codice (lettura veloce, scrittura lenta).
- Memoria **SRAM** per i dati (lettura e scrittura veloci).
- **EEPROM** per la memorizzazione di dati persistenti.

## Memoria nei Microcontrollori

I microcontrollori utilizzano diversi tipi di memoria, ognuno con caratteristiche specifiche:

| **Tipo di Memoria** | **Caratteristiche**                                                                                                                                     |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Flash**           | Memoria non volatile usata per il codice. Ha una lettura veloce e scrittura lenta. Supporta circa 100.000 cicli di scrittura.                           |
| **SRAM**            | Memoria volatile veloce utilizzata per dati temporanei. Consuma più energia e perde i dati al reset o allo spegnimento del dispositivo.                 |
| **EEPROM**          | Memoria non volatile per dati persistenti. È più lenta e supporta un numero limitato di cicli di scrittura. Utilizzabile tramite librerie specifiche.   |

**Nota**: La quantità di **SRAM** è spesso limitata; è importante ottimizzare l'uso delle variabili per evitare problemi di memoria.

## Esempio di Microcontrollore: Arduino Uno

L'**Arduino Uno** è una scheda di sviluppo basata sul microcontrollore **ATMega328P**, con le seguenti caratteristiche:

- **CPU**: AVR a 8 bit operante a **16 MHz**.
- **Memoria**:
  - **Flash**: 32 KB (0.5 KB utilizzati dal bootloader).
  - **SRAM**: 2 KB.
  - **EEPROM**: 1 KB.
- **Porte di I/O**:
  - **14 pin digitali**, di cui 6 con supporto **PWM** (Pulse Width Modulation).
  - **6 ingressi analogici** per la lettura di segnali analogici.
- **Connettività**:
  - **Porta USB** per programmazione e alimentazione.
  - **Connettore ICSP** (In-Circuit Serial Programming) per programmazione diretta.
  - **Jack di alimentazione** per alimentazione esterna.
  - **Pulsante di reset** per riavviare il microcontrollore.
- **Alimentazione**:
  - **Tensione operativa**: 5V.
  - **Tensione di ingresso raccomandata**: 7-12V attraverso il jack di alimentazione.
  - **Corrente massima per ogni pin I/O**: 40 mA.
  - **Corrente massima sulla linea 3.3V**: 50 mA.

## GPIO - General Purpose Input/Output

I **GPIO** sono pin del microcontrollore che possono essere configurati come ingressi o uscite per interagire con altri dispositivi o sensori.

- **Configurazione dei Pin**:
  - **Input**: per leggere segnali provenienti da sensori o altri dispositivi.
  - **Output**: per controllare attuatori come LED, motori, ecc.
- **Pin Digitali**:
  - Possono assumere valori logici **HIGH (1)** o **LOW (0)**.
  - Utilizzati per segnali discreti e comunicazioni digitali.
- **Pin Analogici**:
  - Possono leggere una gamma continua di valori di tensione (ad es. 0-5V su Arduino).
  - Utilizzati con sensori analogici.
- **Funzioni Multiple**:
  - Alcuni pin possono avere funzioni speciali, come comunicazione seriale, PWM, interruzioni esterne.

### GPIO su ATMega328P

- Il microcontrollore dispone di **23 linee I/O** suddivise in **3 porte**:
  - **Porta B**: comprende i pin digitali 8-13.
  - **Porta C**: include i pin analogici (A0-A5).
  - **Porta D**: comprende i pin digitali 0-7.

### Parametri Operativi

- **Tensione Operativa**:
  - **5V** per Arduino Uno.
  - **3.3V** per dispositivi come ESP32 o Raspberry Pi.
- **Corrente Massima per I/O**:
  - **40 mA** per Arduino Uno.
  - **12 mA** per ESP32.
- **Resistenze di Pull-up**:
  - Utilizzate per garantire che i pin di input non rimangano in stato flottante.
  - Possono essere interne al microcontrollore o aggiunte esternamente.

## Programmazione dei Microcontrollori

La programmazione dei microcontrollori implica la scrittura del codice su un computer e il trasferimento al dispositivo.

- **Processo di Programmazione**:
  - Il codice sorgente viene scritto in un linguaggio di programmazione (ad es. C/C++).
  - Il codice viene compilato in un file eseguibile (linguaggio macchina).
  - Il programma viene caricato nel microcontrollore.
- **Trasferimento del Programma**:
  - **USB**: utilizza un bootloader per la comunicazione seriale.
  - **ICSP (In-Circuit Serial Programming)**: programmazione diretta dei registri di memoria.
- **Esecuzione senza Sistema Operativo**:
  - Il microcontrollore esegue il codice direttamente, senza bisogno di un sistema operativo.
  - Ideal per applicazioni con risorse limitate e tempi critici.

### Caso Arduino

- **Arduino IDE**:
  - Ambiente di sviluppo integrato per scrivere e caricare codice sulle schede Arduino.
  - Basato su **Wiring** e utilizza il compilatore **avr-gcc**.
- **Linguaggio**:
  - Estensione semplificata di **C/C++**.
  - Fornisce funzioni e librerie per l'accesso facilitato alle periferiche.
- **Bootloader**:
  - Software pre-caricato sul microcontrollore che consente la programmazione via USB.
  - Occupa circa **0.5 KB** della memoria Flash.
- **Strumenti Avanzati**:
  - **AVR Libc**: libreria standard per microcontrollori AVR.
  - **avr-objdump**: strumento per l'analisi del codice compilato (disassemblatore).
  - Utili per debugging e ottimizzazione.

## Super Loop

Molti microcontrollori utilizzano una struttura di esecuzione chiamata **Super Loop**, che consiste in un ciclo infinito in cui il programma rimane in esecuzione.

```c
void setup() {
  // Inizializzazione del sistema
}

void loop() {
  // Codice eseguito ripetutamente
}
```

### Vantaggi

- **Semplicità**: facile da capire e implementare.
- **Efficienza**: riduce l'overhead di sistema.
- **Affidabilità**: meno punti di fallimento rispetto a sistemi complessi.

### Svantaggi

- **Precisione Temporale Limitata**: non adatto per applicazioni che richiedono temporizzazioni precise.
- **Bassa Flessibilità**: difficile da scalare o modificare per applicazioni più complesse.
- **Consumo Energetico**: può essere elevato se non sono implementate strategie di risparmio energetico.

## Ciclo di Esecuzione e Prestazioni

La prestazione di un microcontrollore è determinata dalla velocità del suo clock e dall'efficienza nell'eseguire istruzioni.

- **Clock dell'ATMega328P**:
  - Frequenza di **16 MHz**.
  - **1 ciclo macchina** corrisponde a **62.5 nanosecondi**.
- **Esecuzione delle Istruzioni**:
  - La maggior parte delle istruzioni richiede da 1 a 2 cicli macchina.
  - **Tempo di esecuzione prevedibile**, importante per applicazioni **real-time**.

## Assembly AVR

Il codice scritto in alto livello viene compilato in linguaggio macchina comprensibile al microcontrollore.

- **Esempio di Codice Assembly**:

  ```assembly
  00000090 <setup>:
   90: 08 95    ret

  00000092 <loop>:
   92: 08 95    ret
  ```

- **Interpretazione**:
  - Il **label** indica l'indirizzo di memoria della funzione.
  - Il codice esadecimale rappresenta l'istruzione macchina.
  - **ret** è un'istruzione di ritorno da una funzione.

- **Uso Avanzato**:
  - Analizzare il codice assembly può aiutare a ottimizzare le prestazioni.
  - Utile per il debugging a basso livello.

## Conclusione

I microcontrollori sono componenti fondamentali nell'elettronica moderna, permettendo il controllo preciso e autonomo di dispositivi in vari campi. Comprendere la loro architettura, le modalità di programmazione e le caratteristiche operative è essenziale per progettare sistemi efficienti e affidabili.