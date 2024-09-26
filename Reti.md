APPUNTI RETI DI TELECOMUNICAZIONE
# Protocolli di Internet e IP

## Architettura di Internet

L'architettura di Internet è organizzata in strati:

1. Applicazioni (e-mail, ftp, telnet, www)
2. TCP/UDP (Strato di Trasporto)
3. IP (Strato di Rete)
4. Collegamento dati (es. Ethernet, X25, Aloha)
5. Fisico

Questa struttura corrisponde al modello OSI semplificato, con IP che opera al livello di rete (strato 3).

## Internet Protocol (IP) - RFC 791

Caratteristiche principali:
- Funziona a commutazione di pacchetto in modalità connectionless
- Gestisce la trasmissione di datagrammi da sorgente a destinazione attraverso reti eterogenee
- Identifica host e router tramite indirizzi IP di 32 bit
- Frammenta e riassembla i datagrammi quando necessario
- Offre un servizio "best effort" senza garanzie di affidabilità o controllo di flusso

## Struttura degli indirizzi IP

- Lunghezza fissa di 32 bit
- Rappresentazione in formato dotted decimal (es. 137.204.212.1)
- Numero massimo teorico di indirizzi: 2^32 = 4.294.967.296
- Assegnati dalla IANA (Internet Assigned Numbers Authority)

## Formato del pacchetto IP

Il pacchetto IP è composto da:

1. Header (intestazione)
2. Payload (dati utente)

Campi principali dell'header:
- Version (4 bit): versione del protocollo IP (attualmente 4)
- IHL (4 bit): lunghezza dell'intestazione in parole da 32 bit
- Type of Service (8 bit): indica il tipo di servizio richiesto
- Total Length (16 bit): lunghezza totale del datagramma in byte
- Identification (16 bit): identificatore univoco del datagramma
- Flags (3 bit): controllo della frammentazione
- Fragment Offset (13 bit): posizione del frammento nel datagramma originale
- Time to Live (TTL) (8 bit): numero massimo di hop consentiti
- Protocol (8 bit): indica il protocollo di livello superiore
- Header Checksum (16 bit): per il controllo degli errori nell'intestazione
- Source Address (32 bit): indirizzo IP sorgente
- Destination Address (32 bit): indirizzo IP destinazione
- Options (variabile): opzioni aggiuntive
- Padding: bit di riempimento per allineare l'intestazione a 32 bit

## Frammentazione dei datagrammi

- Necessaria quando il datagramma è troppo grande per essere trasmesso su una rete
- Può essere effettuata da qualsiasi apparato di rete con protocollo IP
- I frammenti vengono riassemblati solo dal terminale ricevente
- Il campo "Fragment Offset" indica la posizione del frammento nel datagramma originale
- I campi "Identification", "Flags" e "Fragment Offset" sono usati per gestire la frammentazione

### Flags per la frammentazione:
- Bit 0: sempre 0
- Bit 1 (DF - Don't Fragment): 
  - 0 = si può frammentare
  - 1 = non si può frammentare
- Bit 2 (MF - More Fragments):
  - 0 = ultimo frammento
  - 1 = frammento intermedio

### Calcolo del Fragment Offset:
- Il datagramma è diviso in blocchi di 8 byte (64 bit)
- L'offset è calcolato in unità di 8 byte dall'inizio del datagramma originale

## Time to Live (TTL)

- Imposta un limite al numero di hop che un pacchetto può attraversare
- Valore iniziale tipico: 64 (massimo 255)
- Decrementato di 1 ad ogni hop
- Se raggiunge 0, il pacchetto viene scartato

## Riassemblaggio dei datagrammi

- I frammenti possono arrivare fuori sequenza o con tempi diversi
- Il riassemblaggio avviene solo al terminale di destinazione
- Utilizza i campi Identification, Flags e Fragment Offset per ricostruire correttamente il datagramma originale

#Istradamento IP

### Internet e il Modello di Instradamento IP
   - **Instradamento a pacchetto**: Internet utilizza la commutazione a pacchetto per trasmettere dati.
   - Esistono più percorsi per raggiungere una destinazione. Il routing (instradamento) avviene pacchetto per pacchetto, e i router decidono quale percorso seguire.

### Componenti della Rete
   - **Network IP**: Internet è costituita da tante reti isolate (Network IP). Ogni network IP è un'isola, che contiene host (calcolatori terminali).
   - **Router**: Collegano le isole e permettono la comunicazione tra reti diverse. Funzionano fino al livello 3 del modello OSI.

### Tecnologie di Implementazione
   - **Wi-Fi**: Wireless a breve distanza.
   - **ADSL/xDSL**: Connessioni via cavo a media distanza.
   - **Ethernet**: Connessioni cablate locali.
   - **GPRS/EDGE/LTE**: Connessioni radio fornite da operatori pubblici.

### Indirizzo IP
   - L'indirizzo IP è composto da due parti:
     - **Net ID**: Identifica la rete.
     - **Host ID**: Identifica l'host all'interno della rete.
   - La distinzione tra Net ID e Host ID è determinata dalla **Netmask**.

### Routing e Instradamento
   - **Direct Delivery**: Quando l'IP sorgente e destinatario sono sulla stessa rete.
   - **Indirect Delivery**: Se l'IP destinatario è su un'altra rete, il pacchetto viene inviato a un router intermedio.
   - **Tabella di Instradamento**: Ogni nodo (host o router) ha una tabella che contiene informazioni su destinazioni possibili, netmask, gateway, e interfacce.
   - **Longest Prefix Match**: Per selezionare il percorso corretto, il nodo confronta l'indirizzo di destinazione con la netmask più lunga disponibile nella tabella.

### Protocolli ARP e Risoluzione degli Indirizzi
   - **ARP (Address Resolution Protocol)**: Utilizzato per trovare l'indirizzo fisico (MAC) di un host a partire dall'indirizzo IP. Il processo coinvolge:
     1. Un messaggio broadcast ARP request.
     2. La risposta dell'host con il proprio indirizzo MAC.
   - **Cache ARP**: Ogni host mantiene una tabella di cache con le corrispondenze IP-MAC.

### Subnetting
   - Esempio di **Netmask**: 
     - **Net-ID**: 192.168.1.0/24 indica una rete con Net-ID di 24 bit.
     - Può essere suddivisa in sottoreti usando la netmask per identificare la parte Net e Host dell'indirizzo.

### Routing Aggregato
   - La **semplificazione delle tabelle di routing** avviene aggregando più network in un’unica voce, riducendo la complessità per i router.

### Uso del Gateway
   - **Gateway**: Il nodo che connette due network IP. È responsabile dell'instradamento dei pacchetti verso la destinazione finale.

### Esempi di Tabelle di Routing
   - La tabella di routing contiene campi come:
     - **Destination**: L'indirizzo IP o la rete da raggiungere.
     - **Netmask**: La maschera di rete che separa Net ID da Host ID.
     - **Gateway**: L'indirizzo IP del router da usare.
     - **Interface**: L'interfaccia di rete attraverso cui inviare il pacchetto.

# Classless vs Classfull IP
- **Indirizzi IP e Netmask**:
  - Gli indirizzi IP pubblici devono essere unici su Internet e identificano sorgente e destinazione nel datagramma IP.
  - La **netmask** è locale a ciascun nodo, utilizzata per determinare la porzione di indirizzo che rappresenta la rete e l'host. Non viene trasportata nel datagramma, ma è parte della tabella di routing del nodo.
  - Inizialmente, la divisione tra Net-ID e Host-ID era assoluta, mentre successivamente si è passati a un approccio più flessibile (Classless).

### Classi di indirizzi IP (Classfull)
- Durante le fasi iniziali di Internet, gli indirizzi IP erano suddivisi in **classi**:
  - **Classe A**: grandi reti (da 0.0.0.0 a 127.255.255.255).
  - **Classe B**: reti di medie dimensioni (da 128.0.0.0 a 191.255.255.255).
  - **Classe C**: piccole reti (da 192.0.0.0 a 223.255.255.255).
  - **Classe D**: indirizzi multicast (da 224.0.0.0 a 239.255.255.255).
  - **Classe E**: sperimentale (da 240.0.0.0 a 255.255.255.255).
  - **Indirizzi riservati**: ad esempio, 127.x.x.x per loopback e 255.255.255.255 per broadcast.

### Subnetting
- La **subdivisione in sottoreti (subnetting)** consente di frammentare una rete principale in reti più piccole (subnet) per assegnarle a diverse sotto-amministrazioni all'interno di un'organizzazione.
  - La **subnet mask** permette di personalizzare l'assegnazione dell'indirizzo IP, suddividendo l'Host-ID in due parti: una parte per la subnet e l'altra per l'host.
  - **Esempio**: L'Università di Bologna utilizza una rete di classe B (137.204.0.0) e divide l'Host-ID per creare 254 sottoreti di classe C, utilizzando la netmask 255.255.255.0.

### CIDR (Classless InterDomain Routing)
- Con la diffusione di Internet, la suddivisione rigida in classi si è dimostrata inefficiente, portando alla creazione di CIDR (**RFC 1519**).
  - CIDR elimina la logica delle classi nei router e consente la **definizione variabile della dimensione del Net-ID**.
  - Le tabelle di routing includono le netmask per una gestione più flessibile delle reti.
  - **Obiettivi**:
    - Ottimizzazione dello spazio di indirizzi IP.
    - Aggregazione delle informazioni di routing (supernetting).
    - Gestione di reti di classe A e B limitate e della crescita delle tabelle di routing.

### Supernetting
- Il **supernetting** consente di unire più reti contigue per ridurre le voci nelle tabelle di routing. Ad esempio:
  - Un'organizzazione ha bisogno di circa 2000 indirizzi IP: invece di una rete di classe B (64k indirizzi), è preferibile combinare 8 reti di classe C (2048 indirizzi).
  - Supernetting consente di rappresentare queste reti come una singola super-rete: es. 194.24.0.0/21, con netmask 255.255.248.0.
- **Operazioni duali**:
  - Subnetting riduce la parte Host-ID per estendere il Net-ID.
  - Supernetting estende l'Host-ID per aggregare reti con Net-ID simili.

### Protocolli di Controllo e ICMP
- **IP** è un protocollo **best effort**, non garantisce la consegna corretta dei datagrammi e si appoggia a protocolli affidabili di livello superiore come **TCP**.
  - Tuttavia, è necessario un protocollo per gestire situazioni anomale e segnalare errori: **ICMP (Internet Control Message Protocol)**.
  - ICMP segnala errori come:
    - **Destination Unreachable (Type 3)**: quando un gateway non può raggiungere la rete o l'host.
    - **Time Exceeded (Type 11)**: quando il Time-to-Live (TTL) di un datagramma si azzera.
    - **Redirect (Type 5)**: un router segnala all'host sorgente una via più ottimale.
  - ICMP non corregge gli errori, ma fornisce informazioni per diagnosticare problemi di rete.

### Comandi utili: PING e TRACEROUTE
- **PING**:
  - Verifica se un host è raggiungibile inviando pacchetti ICMP di tipo "echo" e ricevendo "echo reply".
  - Opzioni: definire il numero di pacchetti, timeout, dimensione pacchetti, ecc.
- **TRACEROUTE**:
  - Mostra il percorso dei pacchetti verso una destinazione, utilizzando pacchetti ICMP con TTL crescente. Mostra il nome DNS e l'indirizzo IP dei nodi intermedi.

# **Gestione della numerazione IP: DHCP**
- **DHCP (Dynamic Host Configuration Protocol)** consente la configurazione dinamica e automatica di un indirizzo IP per un host, assegnando:
  - Indirizzo IP, netmask, gateway predefinito, server DNS, ecc.
- **Processo DHCP**:
  - **DHCPDISCOVER**: l'host cerca un server DHCP inviando un messaggio di richiesta in broadcast.
  - **DHCPOFFER**: i server DHCP rispondono proponendo un indirizzo IP.
  - **DHCPREQUEST**: l'host accetta una delle offerte e richiede l'indirizzo IP.
  - **DHCPACK**: il server DHCP conferma la configurazione con un messaggio di risposta.