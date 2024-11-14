# APPUNTI RETI DI TELECOMUNICAZIONE
## Protocolli di Internet e IP

### Architettura di Internet

L'architettura di Internet è organizzata in strati:

1. Applicazioni (e-mail, ftp, telnet, www)
2. TCP/UDP (Strato di Trasporto)
3. IP (Strato di Rete)
4. Collegamento dati (es. Ethernet, X25, Aloha)
5. Fisico
Questa struttura corrisponde al modello OSI semplificato, con IP che opera al livello di rete (strato 3).

### Internet Protocol (IP) - RFC 791

Caratteristiche principali:
- Funziona a commutazione di pacchetto in modalità connectionless
- Gestisce la trasmissione di datagrammi da sorgente a destinazione attraverso reti eterogenee
- Identifica host e router tramite indirizzi IP di 32 bit
- Frammenta e riassembla i datagrammi quando necessario
- Offre un servizio "best effort" senza garanzie di affidabilità o controllo di flusso

### Struttura degli indirizzi IP

- Lunghezza fissa di 32 bit
- Rappresentazione in formato dotted decimal (es. 137.204.212.1)
- Numero massimo teorico di indirizzi: 2^32 = 4.294.967.296
- Assegnati dalla IANA (Internet Assigned Numbers Authority)

### Formato del pacchetto IP

Il pacchetto IP è composto da:
1. Header (intestazione)
2. Payload (dati utente)

### Campi principali dell'header IP

- **Prima riga (identificazione)**
  - **Version (4 bit)**: versione del protocollo IP (attualmente 4)
  - **IHL (Internet Header Length) (4 bit)**: lunghezza dell'intestazione in parole da 32 bit
  - **Type of Service (8 bit)**: indica il tipo di servizio richiesto (continua ad essere un problema non risolto)
  - **Total Length (16 bit)**: lunghezza totale del datagramma in byte (fino a 65,535 byte)

- **Seconda riga (controllo di dimensione e segmentazione del pacchetto)**
  - **Identification (16 bit)**: identificatore univoco del datagramma (dato che un pacchetto potrebbe essere diviso in rete)
  - **Flags (3 bit)**: controllo della frammentazione (spiegati sotto)
  - **Fragment Offset (13 bit)**: posizione del frammento nel datagramma originale (indica la posizione del primo byte rispetto all'inizio)

- **Terza riga (controllo dell'errore)**
  - **Time to Live (TTL) (8 bit)**: numero massimo di hop consentiti (a livello funzionale potrebbe anche non esistere più perché la rete è molto efficiente ed i pacchetti non girano più a caso per essa, oggi vengono usati come strumenti di controllo)
  - **Protocol (8 bit)**: indica il protocollo di livello superiore
  - **Header Checksum (16 bit)**: per il controllo degli errori nell'intestazione

- **Quarta riga**
  - **Source Address (32 bit)**: indirizzo IP sorgente

- **Quinta riga**
  - **Destination Address (32 bit)**: indirizzo IP destinazione

- **Sesta riga opzionale (quasi mai usata)**
  - **Options (variabile)**: opzioni aggiuntive
  - **Padding**: bit di riempimento per allineare l'intestazione a 32 bit

### Frammentazione dei datagrammi

- Necessaria quando il datagramma è troppo grande per essere trasmesso su una rete
- Può essere effettuata da qualsiasi apparato di rete con protocollo IP
- I frammenti vengono riassemblati solo dal terminale ricevente
- Il campo "Fragment Offset" indica la posizione del frammento nel datagramma originale
- I campi "Identification", "Flags" e "Fragment Offset" sono usati per gestire la frammentazione

### Flags per la frammentazione:
- Bit 0: sempre 0
- Bit 1 (DF - Don't Fragment): 
  - 0 = si può frammentare
  - 1 = non si può frammentare (nel caso fosse a 1 e fosse necessario frammentarlo lo distruggo)
- Bit 2 (MF - More Fragments):
  - 0 = ultimo frammento (aiuta a riordimare i paccheti in arrivo, è tecnicamente superfluo ma ci risparmia il calcolo di vedere quanto era lungo)
  - 1 = frammento intermedio

### Calcolo del Fragment Offset:
- Il datagramma è diviso in blocchi di 8 byte (64 bit)
- L'offset è calcolato in unità di 8 byte dall'inizio del datagramma originale (non ho bisogno di mappare tutti i bit ma posso mapparli a blocchi di 8 byte per ridurre a 13 il numero di bit necessari a tenerne traccia, ciò implica che la frammentazione non potrà mai scendere sotto i 64 bit perché non sarei più in grado di ricomporre il pacchetto)

### Time to Live (TTL)

- Imposta un limite al numero di hop che un pacchetto può attraversare
- Valore iniziale tipico: 64 (massimo 255)
- Decrementato di 1 ad ogni hop
- Se raggiunge 0, il pacchetto viene scartato

### Riassemblaggio dei datagrammi

- I frammenti possono arrivare fuori sequenza o con tempi diversi
- Il riassemblaggio avviene solo al terminale di destinazione
- Utilizza i campi Identification, Flags e Fragment Offset per ricostruire correttamente il datagramma originale

## Istradamento IP

### Internet e il Modello di Instradamento IP
- **Instradamento a pacchetto**: Internet utilizza la commutazione a pacchetto per trasmettere dati.
- Esistono più percorsi per raggiungere una destinazione. Il routing (instradamento) avviene pacchetto per pacchetto, e i router decidono quale percorso seguire.

### Componenti della Rete
- **Network IP**: Internet è costituita da tante reti isolate (Network IP). Ogni network IP è un'isola che contiene host (calcolatori terminali). Questi host devono essere necessariamente in grado di comunicare tra di loro; il caso più estremo è un solo host (calcolatore) che parla con se stesso.
- **Router**: Detti anche Gateway, collegano le isole e permettono la comunicazione tra reti diverse. Funzionano fino al livello 3 del modello OSI. In molti casi, il trasferimento di dati compie un percorso che passa per più gateway e probabilmente anche per più network. Due router connessi che a loro volta connettono altrettante network IP possono essere visti,

### Tecnologie di Implementazione
   - **Wi-Fi**: Wireless a breve distanza. (dal punto di vista dell'ip è un tipo di comunicazione 1a1 che passa per il centro stella e viene poi smistata )
   - **ADSL/xDSL**: Connessioni via cavo a media distanza.
   - **Ethernet**: Connessioni cablate locali.
   - **GPRS/EDGE/LTE**: Connessioni radio fornite da operatori pubblici.

### Indirizzo IP
   - L'indirizzo IP, usato per raggiungere una specifica network al dilà dell'plementazione su cui lavora, è composto da due parti:
     - **Net ID**: Identifica la rete (network ip), parte di sinistra dell'indirizzo
     - **Host ID**: Identifica l'host all'interno della rete (singolo calcolatore), parte destra dell'indirizzo.
   - La distinzione tra Net ID e Host ID è determinata dalla **Netmask**.

### Routing e Instradamento
- **Direct Delivery**: Quando l'IP sorgente e destinatario sono sulla stessa rete. Supponendo di essere in collegamento Ethernet in un network IP, inseriremo l'IP in un indirizzo di livello 2 contenente il MAC del calcolatore da raggiungere. Il MAC è fondamentale perché evita che tutti i calcolatori debbano ricevere tutti i pacchetti e verificare se l'IP è il loro, cosa che renderebbe gli host incapaci di fare qualsiasi altra cosa data la mole di lavoro. Questo MAC viene reperito grazie a una tabella contenuta nel calcolatore che mette in relazione IP con MAC. Se non è presente, lo richiede partendo dall'IP che vuole raggiungere grazie al protocollo ARP, che fa una richiesta broadcast. Questo scambio è una consegna diretta.

![immagine locale](img\Reti\direct_delivery.PNG)

- **Indirect Delivery**: Se l'IP destinatario è su un'altra rete, il pacchetto viene inviato a un router intermedio. A livello 1, l'IP di destinazione sarà quello del calcolatore obiettivo, ma a livello 2, il MAC sarà quello del gateway della propria rete. Poiché il gateway è un router, non scarterà il pacchetto nonostante l'IP di destinazione non corrisponda al proprio; invece, lo instraderà verso un altro router. Il primo e l'ultimo scambio, tra l'host spedente e il rispettivo router e tra l'host ricevente e il rispettivo router, sono scambi diretti. Tutti gli scambi intermedi sono indiretti e devono essere completati entro il limite di 255 hop imposto dal TTL. La decisione nei passaggi indiretti è simile a quella nei passaggi diretti: il router utilizzerà il protocollo ARP (pacchetti broadcast a livello data link) per ottenere l'indirizzo del gateway successivo, ovvero l'unico altro calcolatore della loro rete, per passargli il pacchetto. In questi casi, è opportuno avere un indirizzo IP /30, in modo tale che, tolti i 2 indirizzi proibiti, ne restino 2 per i 2 gateway della rete. Per determinare se è possibile effettuare una consegna diretta, si utilizza la tabella di instradamento IP. Grazie a essa, è possibile inviare una richiesta ARP, nella speranza di una ARP reply, attraverso l'interfaccia corretta e agli indirizzi che contengono l'IP dell'host, evitando una richiesta ARP broadcast che appesantirebbe eccessivamente l'infrastruttura di rete. In caso di mancanza di reply, dato che l'IP è un protocollo best effort, si scarta il pacchetto e si segnala l'errore.

![immagine locale](img\Reti\indirect_delivery.PNG)

- **Tabella di Instradamento**: Ogni nodo (host o router) ha una tabella che contiene informazioni sulle destinazioni possibili, netmask, gateway e interfacce. Le righe della tabella rappresentano le singole istanze di instradamento, mentre le colonne contengono le opzioni di instradamento. Tipicamente, la tabella ha cinque colonne principali:
  - **Destination**: Contiene gli indirizzi IP o i gruppi di IP raggiungibili.
  - **Netmask**: Indica la netmask che permette di interpretare correttamente l'IP.
  - **Gateway**: L'IP del gateway successivo a cui fare riferimento.(Se si dovesse essere già un host finale ci possono esere più possibilità come per esempio il proprio ip, la scritta self ecc)
  - **Interface**: L'interfaccia di rete attraverso cui inviare il pacchetto.(Mi dice da dove fare la richiesta Arp qualora fosse necessarai)
  - **Metric**: Rappresenta il costo del percorso, utilizzato per determinare il percorso migliore quando sono disponibili più opzioni.
Questa struttura permette ai nodi di instradare i pacchetti in modo efficiente, scegliendo il percorso ottimale basato sulle informazioni disponibili nella tabella di instradamento.

!CHIEDERE SPEIEGAZIONE DI COME FARE LA ARP UNA VOLTA CHE SI ARRIVA AL GATWAY DELLA NETWORK IP GIUSTA!

- **Utilizzo della Tabella di Instradamento da parte dei Gateway**: I gateway utilizzano la tabella di instradamento per determinare il percorso ottimale per ogni pacchetto. La tabella contiene informazioni su destinazioni, netmask, gateway e interfacce. Quando un pacchetto arriva al gateway, questo esamina l'indirizzo IP di destinazione e lo confronta con le voci nella tabella di instradamento. Il gateway seleziona la voce con la netmask più lunga che corrisponde all'indirizzo di destinazione (Longest Prefix Match) e inoltra il pacchetto attraverso l'interfaccia appropriata. Questo processo evita il sovraccarico della rete con broadcast inutili, poiché il gateway invia il pacchetto solo all'interfaccia specifica che conduce verso la destinazione finale. In questo modo, i pacchetti vengono instradati in modo efficiente e preciso, riducendo il traffico di rete e migliorando le prestazioni complessive. Se non trova una corrispondenza, scarta il pacchetto e comunica un errore. Per trovare la corrispondenza migliore, avendo l'IP di destinazione, il gateway procede con il processo di table lookup durante il quale, partendo dalla netmask con valore più grande e andando a decrescere, prende la netmask e fa l'AND bit a bit con l'IP di destinazione del datagramma e lo confronta con l'IP di destinazione della singola riga. Qualora il risultato fosse uguale, la corrispondenza è trovata (abbiamo trovato il ricevente); altrimenti, continua con le altre righe e tiene il risultato più simile che quindi avvicina di più all'host finale.

- **Longest Prefix Match**: Per selezionare il percorso corretto, il nodo confronta l'indirizzo di destinazione con la netmask più lunga disponibile nella tabella.

### Protocolli ARP e Risoluzione degli Indirizzi
   - **ARP (Address Resolution Protocol)**: Utilizzato per trovare l'indirizzo fisico (MAC) di un host a partire dall'indirizzo IP. Il processo coinvolge:
     1. Un messaggio broadcast ARP request.
     2. La risposta dell'host con il proprio indirizzo MAC.
   - **Cache ARP**: Ogni host mantiene una tabella di cache con le corrispondenze IP-MAC.

## Classless VS Classfull

### Subnetting
- Esempio di **Netmask**: Una netmask è composta da 32 bit che sono in locale e rimangono affibiati al singolo calcolatore, tutti i calcolatori della stessa network avranno la stessa netmask, con tutti 1 a sinistra e tutti 0 a destra. Il punto in cui avviene il cambio rappresenta la separazione tra Net-ID e Host-ID nell'indirizzo IP. Per la parte di host, indipendentemente dalla dimensione, gli indirizzi con tutti 0 e tutti 1 non vengono assegnati e sono riservati a compiti specifici. Quindi, si perdono 2 indirizzi: quello con tutti 0 identifica la network ID senza la parte di host, mentre con tutti gli 1 è riservato al gateway predefinito.
  - **Net-ID**: 192.168.1.0/24 indica una rete con Net-ID di 24 bit.
  - Può essere suddivisa in sottoreti usando la netmask per identificare la parte Net e Host dell'indirizzo.

### Routing Aggregato
La **semplificazione delle tabelle di routing** avviene aggregando più network in un’unica voce, riducendo la complessità per i router. Questo processo è noto come **supernetting** o **route aggregation**.

### Come si aggregano le reti
1. **Identificazione delle reti contigue**: Per aggregare le reti, è necessario che queste siano contigue, ovvero che gli indirizzi IP siano consecutivi.
2. **Calcolo della supernet**: Si determina una nuova netmask che copra tutte le reti contigue. Ad esempio, se si hanno le reti 192.168.1.0/24 e 192.168.2.0/24, si può aggregarle in una singola rete 192.168.0.0/22.
3. **Aggiornamento delle tabelle di routing**: Le voci delle singole reti vengono sostituite da una voce unica che rappresenta la supernet.

### Vantaggi del Routing Aggregato
- **Riduzione delle voci nelle tabelle di routing**: Aggregando le reti, si diminuisce il numero di voci che i router devono gestire, semplificando il processo di instradamento.
- **Miglioramento delle prestazioni**: Con meno voci da esaminare, i router possono prendere decisioni di instradamento più rapidamente, migliorando le prestazioni complessive della rete.
- **Minore utilizzo di memoria**: Le tabelle di routing più piccole richiedono meno memoria, liberando risorse per altre operazioni.
- **Scalabilità**: La rete diventa più scalabile, poiché l'aggiunta di nuove reti contigue può essere gestita facilmente attraverso l'aggiornamento della supernet esistente.
- **Riduzione del traffico di aggiornamento**: Con meno voci da aggiornare, si riduce il traffico di aggiornamento delle tabelle di routing tra i router, migliorando l'efficienza della rete.

### Uso del Gateway
   - **Gateway**: Il nodo che connette due network IP. È responsabile dell'instradamento dei pacchetti verso la destinazione finale.

### Esempi di Tabelle di Routing
   - La tabella di routing contiene campi come:
     - **Destination**: L'indirizzo IP o la rete da raggiungere.
     - **Netmask**: La maschera di rete che separa Net ID da Host ID.
     - **Gateway**: L'indirizzo IP del router da usare.
     - **Interface**: L'interfaccia di rete attraverso cui inviare il pacchetto.

### Classless vs Classfull IP
- **Indirizzi IP e Netmask**:
  - Gli indirizzi IP pubblici devono essere unici su Internet e identificano sorgente e destinazione nel datagramma IP.
  - La **netmask** è locale a ciascun nodo, utilizzata per determinare la porzione di indirizzo che rappresenta la rete e l'host. Non viene trasportata nel datagramma, ma è parte della tabella di routing del nodo.
  - Inizialmente, la divisione tra Net-ID e Host-ID era assoluta, mentre successivamente si è passati a un approccio più flessibile (Classless).

### Classi di indirizzi IP (Classfull)
- Durante le fasi iniziali di Internet, gli indirizzi IP erano suddivisi in **classi**:
  - **Classe A**: grandi reti (da 0.0.0.0 a 127.255.255.255) ed andavano letti come se avessero un netmask /8.
  - **Classe B**: reti di medie dimensioni (da 128.0.0.0 a 191.255.255.255) ed andavano letti come se avessero un netmask /16.
  - **Classe C**: piccole reti (da 192.0.0.0 a 223.255.255.255) ed andavano letti come se avessero un netmask /24.
  - **Classe D**: indirizzi multicast (da 224.0.0.0 a 239.255.255.255), riservati al multicast.
  - **Classe E**: sperimentale (da 240.0.0.0 a 255.255.255.255), riservati a casi sperimentali.
  - **Indirizzi riservati**: ad esempio, 127.x.x.x per loopback e 255.255.255.255 per broadcast.
- Dunque, la netmask dell'indirizzo era implicita nella classe dell'indirizzo stesso. Tuttavia,
 questo approccio presentava limitazioni significative, come la scarsa flessibilità nella gestione 
 degli indirizzi IP e l'inefficienza nell'allocazione degli indirizzi. Per risolvere questi problemi, 
 è stato introdotto il **Classless Inter-Domain Routing (CIDR)**, che permette una gestione più efficiente 
 e flessibile degli indirizzi IP, eliminando la rigida suddivisione in classi e utilizzando netmask variabili.
- Con CIDR, la netmask è specificata esplicitamente utilizzando la notazione **slash** (ad esempio, /24), 
permettendo una suddivisione più granulare e ottimizzata degli indirizzi IP.
- Inoltre, CIDR facilita l'aggregazione delle rotte (supernetting), riducendo la complessità delle tabelle di 
routing e migliorando l'efficienza della rete.
- Per esempio, un indirizzo IP come 192.168.1.0/24 indica che i primi 24 bit dell'indirizzo sono utilizzati per 
identificare la rete, mentre i restanti 8 bit sono utilizzati per identificare gli host all'interno di quella rete.
- Questa flessibilità consente di adattare meglio la dimensione delle reti alle esigenze specifiche, evitando 
sprechi di indirizzi IP e migliorando la scalabilità della rete.

### Subnetting
- La **subdivisione in sottoreti (subnetting)** consente di frammentare una rete principale in reti più piccole 
(subnet) per assegnarle a diverse sotto-amministrazioni all'interno di un'organizzazione.
  - La **subnet mask** permette di personalizzare l'assegnazione dell'indirizzo IP, suddividendo 
  l'Host-ID in due parti: una parte per la subnet e l'altra per l'host.
  - **Esempio**: L'Università di Bologna utilizza una rete di classe B (137.204.0.0) e divide 
  l'Host-ID per creare 254 sottoreti di classe C, utilizzando la netmask 255.255.255.0.

### CIDR (Classless Inter-Domain Routing)
- Con la diffusione di Internet, la suddivisione rigida in classi si è dimostrata inefficiente, 
portando alla creazione di CIDR (**RFC 1519**).
  - CIDR elimina la logica delle classi nei router e consente la 
  **definizione variabile della dimensione del Net-ID**.
  - Le tabelle di routing includono le netmask per una gestione più flessibile delle reti.
  - **Obiettivi**:
    - Ottimizzazione dello spazio di indirizzi IP.
    - Aggregazione delle informazioni di routing (supernetting).
    - Gestione di reti di classe A e B limitate e della crescita delle tabelle di routing.
- Oggi, la distinzione tra host e net è locale a tal punto che dipende dal punto in cui si guarda, 
punto nel quale è contenuta la netmask di riferimento per quella specifica istanza. Dunque, 
uno stesso indirizzo ha rilevanza diversa in punti diversi della rete.
  - **Esempio**: Un indirizzo IP come 192.168.1.0/24 può essere visto come una singola rete 
  in un contesto, mentre in un altro contesto, con una netmask diversa, può rappresentare una 
  parte di una rete più grande o essere suddiviso in sottoreti più piccole.
  - Questo approccio flessibile permette una gestione più efficiente e scalabile degli indirizzi IP, 
  adattandosi meglio alle esigenze specifiche delle diverse reti.

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
  - Mostra il percorso dei pacchetti verso una destinazione, utilizzando pacchetti ICMP con TTL crescente. 
  Mostra il nome DNS e l'indirizzo IP dei nodi intermedi.

### **Gestione della numerazione IP: DHCP**
- **DHCP (Dynamic Host Configuration Protocol)** consente la configurazione dinamica e automatica di un indirizzo IP per un host, assegnando:
  - Indirizzo IP, netmask, gateway predefinito, server DNS, ecc.
- **Processo DHCP**:
  - **DHCPDISCOVER**: l'host cerca un server DHCP inviando un messaggio di richiesta in broadcast.
  - **DHCPOFFER**: i server DHCP rispondono proponendo un indirizzo IP.
  - **DHCPREQUEST**: l'host accetta una delle offerte e richiede l'indirizzo IP.
  - **DHCPACK**: il server DHCP conferma la configurazione con un messaggio di risposta.

## Pianificazione di numerazione IP

### Progettazione di Reti Aziendali

- **Esempio di rete aziendale**: Tre siti aziendali (S1, S2, S3) devono essere interconnessi con una rete a maglia completa. 
Gli indirizzi di classe C assegnati sono basati su 196.200.96.0/24. Con questa rete ho più IP del necessario, 
dato che ho 256 IP, ma con una /25 ne avrei avuti 128 e sarei stato troppo di misura.

- **Soluzione 1**: Non avendo una sola rete fisica, non possiamo avere consegna diretta. 
Dovremmo usare dei gateway con una rete "comune" di collegamento tra questi ultimi. Avendo una /24, 
posso ottenere 4 reti /26, dunque 62 IP per blocco. Questa soluzione provoca un grande spreco nel 
blocco usato per il collegamento (uso 3 numeri per i gateway e i restanti 58 non servono a niente). 
Inoltre, se devo crescere, sarò in difficoltà perché se creo una nuova sede essa necessiterà di un nuovo 
blocco che non ho modo di creare. Se aumento i terminali nelle sedi già esistenti, posso arrivare solo a 62.

![immagine locale](img\Reti\rete_azz_sol_1.PNG)

- **Soluzione 2**: Potrei valutare netmask a grandezza differenziata. Ricordiamoci che più divido, 
più mi mangio numeri, dato che per ogni divisione il primo e l'ultimo numero sono non utilizzabili. 
Creerò dunque 2 reti /26 (metà degli indirizzi), 3 reti /27 (3/4 dei restanti indirizzi), 
1 rete /28 (1/2 dei restanti indirizzi) e /30 con le quali completerò gli indirizzi. Così facendo, 
le 2 reti /26 saranno usate per 2 sedi, 1 rete /27 per la terza sede e 3 reti /30 per i 3 gateway, 
mantenendo disponibili tutti gli altri indirizzi per il futuro.
Se possibile, un'unica rete per tutti i gateway è preferibile a questa seconda soluzione, perché se 
dobbiamo fisicamente creare l'infrastruttura urbana, è più facile da realizzare. Fossero state 3 isole, forse 
fisicamente sarebbero state più comode 3 reti.

![immagine locale](img\Reti\rete_azz_sol_2.PNG)

## Protocollo ICMP (Internet Control Message Protocol)

### ICMP
  - **Struttura pacchetto ICMP**:
    1. **IP Header**: Intestazione del protocollo IP.
    2. **Message Type**: Tipo di messaggio ICMP (8 bit).
    3. **Message Code**: Codice del messaggio ICMP (8 bit).
    4. **Checksum**: Controllo degli errori per l'intestazione ICMP (16 bit).
    5. **Additional Fields**: Campi aggiuntivi specifici per il tipo di messaggio ICMP.
    6. **Data**: Dati del messaggio ICMP.

- **Tipi di messaggi ICMP**:
  - **Destination Unreachable (Type 3)**: Notifica l'inaccessibilità di host o sottorete.
    - **Code 0**: Network Unreachable
    - **Code 1**: Host Unreachable
    - **Code 2**: Protocol Unreachable
    - **Code 3**: Port Unreachable
    - **Code 4**: Fragmentation Needed and Don't Fragment was Set
    - **Code 5**: Source Route Failed
    - **Code 11**: Destination Network Unreachable for Type of Service
  - **Time Exceeded (Type 11)**: Notifica il superamento del TTL o il timeout per il riassemblaggio dei frammenti.
  - **Echo/Echo Reply (Type 8/0)**: Utilizzati per determinare lo stato di raggiungibilità di un host.
  - **Timestamp Request/Reply (Type 13/14)**: Misura il tempo di transito nella rete.

## Comandi di Rete

### PING
 Verifica la raggiungibilità di un host inviando pacchetti di tipo ICMP Echo Request.
  - Parametri principali: `-n` (numero di pacchetti), `-t` (ping continuo), `-a` (risoluzione DNS), 
  `-l` (dimensione del pacchetto).
### TRACEROUTE
 Identifica il percorso seguito dai pacchetti verso una destinazione tramite la gestione del TTL.
  - **Come funziona**: Traceroute invia pacchetti con un valore TTL (Time To Live) inizialmente impostato a 1. 
  Ogni router lungo il percorso decrementa il TTL di 1. Quando il TTL raggiunge 0, il router scarta il pacchetto 
  e invia un messaggio ICMP "Time Exceeded" al mittente. Traceroute incrementa quindi il TTL e invia un nuovo pacchetto, 
  ripetendo il processo fino a raggiungere la destinazione finale. Questo permette di identificare ogni hop (router) 
  lungo il percorso.
  - Parametri principali: `-m` (TTL massimo), `-q` (numero di query per hop), `-w` (timeout per risposta).

## Gestione della numerazione

### Gestione degli Indirizzi IP
- **DHCP (Dynamic Host Configuration Protocol)**: Automatizza l'assegnazione dinamica di IP, netmask, gateway e DNS. Processo chiave:
  - **DHCPDISCOVER** → **DHCPOFFER** → **DHCPREQUEST** → **DHCPACK**.
  - Il processo inizia con un messaggio broadcast di livello 2 (come ARP) chiamato **DHCPDISCOVER**, 
  inviato sulla rete per cercare un server DHCP. I server DHCP rispondono con un messaggio **DHCPOFFER**, 
  proponendo i parametri di configurazione. L'host seleziona una delle offerte e invia un **DHCPREQUEST** 
  al server scelto. Il server risponde con un **DHCPACK**, confermando i parametri di configurazione.

## Filtraggio dei Pacchetti
### Metodologie di Filtraggio dei Datagrammi
- Le metodologie di filtraggio dei datagrammi sono tecniche utilizzate per controllare il traffico di rete 
in base a criteri predefiniti. Questi criteri possono includere indirizzi IP, numeri di porta, protocolli e 
altre informazioni contenute nei pacchetti. In questo contesto, i gateway fungono da punti di controllo per 
il traffico di rete, applicando le regole di filtraggio per garantire che solo il traffico autorizzato possa 
attraversare la rete. Queste metodologie sono fondamentali per implementare firewall e altre soluzioni di sicurezza 
di rete, garantendo che solo il traffico autorizzato possa attraversare i confini della rete.
  - **Packet Filter**: Controlla l'accesso a determinati servizi o indirizzi in base alle regole 
  impostate sugli IP, protocolli o porte. È detto instradamento selettivo e opera a livello IP basando 
  le sue decisioni sulla natura dell'IP stesso come il TTL, i tipi di indirizzi ecc. Il vantaggio è che 
  a livello di gateway basta implementare il filtro a livello software, ma esistono situazioni in cui i 
  filtri a livello IP non sono sufficienti.
  ![immagine locale](img\Reti\packet_filter.PNG)
  - **Stateful Packet Inspection (SPI)**: Monitora lo stato delle connessioni e adatta dinamicamente le regole 
  di filtraggio. Adattando opportunamente il software, si può andare più a fondo nel pacchetto guardando, per 
  esempio, il tipo di protocollo, attuando così filtri semanticamente più efficaci. Ciò viola il protocollo OSI 
  dato che vado a leggere dati più profondi del livello IP.
  ![immagine locale](img\Reti\packet_inspection.PNG)
  - **Application Layer Gateway (Proxy)**: Monitora le connessioni applicative (ad esempio, FTP, HTTP, SIP), 
  garantendo controllo e sicurezza a livello applicativo. In questo caso, il gateway agisce come un host che 
  scompone il pacchetto fino al livello applicativo e poi lo reinstrada se non è destinato a lui. A differenza 
  dei normali gateway con implementazioni specifiche, un proxy a livello applicativo è più complesso sia a livello 
  hardware che software.
  ![immagine locale](img\Reti\proxy.PNG)
  ![immagine locale](img\Reti\proxy_2.PNG)

Le tre differenti versioni vengono adottate a necessità dato che la prima è la più leggera a 
livello computazionale e la più facile da implementare ma quella meno efficace, e viceversa per la terza.

### Firewall
Il firewall o portatagliafuoco ci difende combinando le tecnologie precedentemente descritte:
- **Packet Filter**: Filtra i pacchetti seguendo le politiche stabilite.
  - Filtri: Generalmente configurati staticamente.
  - La maggioranza delle configurazioni non permettono pacchetti per porte "non-standard" 
  (Internet Assigned Numbers Authority – IANA).
- **Stateful Packet Inspection**:
  - Mantiene il contesto dei pacchetti sia nel trasporto che nello strato applicativo.
  - Adatta dinamicamente le specifiche dei filtri.
- **Application Layer Gateway (trasparente o proxy esplicito)**:
  - Monitora le connessioni: Analizza il contenuto dei protocolli applicativi.
  - A scapito della sicurezza di comunicazione end-to-end.
  - Adatta dinamicamente le specifiche dei filtri.
- **Per ogni strato (layer) dello stack possono essere applicate politiche (policies) differenti**.
- Protezione Host: funge da filto software/hardware per accessi indesiderati dall'esterno della rete. 
(sevono architetture di difesa più complesse). Dunque si potrebbero usare configurazioni di packet filter 
e proxy per migliorare la sicurezza della rete. Un'architettura di difesa multilivello può includere:

1. **Packet Filter**: Filtra i pacchetti in base a regole predefinite sugli indirizzi IP, protocolli e porte. 
È il primo livello di difesa e agisce a livello di rete.
2. **Stateful Packet Inspection (SPI)**: Monitora lo stato delle connessioni e adatta dinamicamente le regole 
di filtraggio. Fornisce un controllo più approfondito rispetto ai semplici packet filter.
3. **Application Layer Gateway (Proxy)**: Monitora e controlla le connessioni a livello applicativo, 
garantendo un controllo dettagliato sui protocolli specifici come HTTP, FTP, e SIP. Questo livello può 
bloccare attacchi che sfruttano vulnerabilità a livello applicativo.

Combinando queste tecnologie, si ottiene una protezione più robusta contro una vasta gamma di minacce, 
migliorando la sicurezza complessiva della rete.

## Network Address Translation (NAT)

### NAT
E' un gateway con funzione di paket filter che si interpone tra 2 networ e può cambiare il contenuto dei pacchetti 
in partivolare gli indirizzi sia ip che di porta.
Viene definito a livello concettuale ma non a livelli fisico/implementativo dato che ci sono molteplici modi di farlo.
- **Funzioni**: Maschera gli indirizzi IP interni, permettendo a reti private di accedere a reti pubbliche. 
- I tipi di NAT principali:
  - **Basic NAT - Conversione di indirizzo**: Converte solo gli indirizzi IP. Si trova tra 2 network e funge da gateway e modifica gli 
  indirizzi sorgente modificando IP e porta per poi reindirizzare al destinatario per poi fare il 
  contrario al ritorno grazie a una tabella delle conversioni. Questo permette di rendere il flusso monodirezionale, 
  ovvero chi è dietro al basic NAT comunica con l'esterno solo se ha richiesto qualcosa da fuori, 
  dunque costruito in questa maniera permette di essere uno strumento di protezione anche se è stato 
  concepito per risparmiare numeri.
  - **Port Address Translation (PAT) (VERIFICARE CHE SIA QUESTO IL NOME)**: Tecnica utilizzata nei router per mappare più indirizzi IP privati su un singolo 
  indirizzo IP pubblico, utilizzando numeri di porta univoci per distinguere le connessioni. Questo processo consente a 
  più dispositivi all'interno di una rete locale (LAN) di condividere un singolo indirizzo IP pubblico per accedere a Internet.
  Quando un dispositivo all'interno della rete locale invia un pacchetto verso Internet, il router sostituisce l'indirizzo 
  IP privato del dispositivo con l'indirizzo IP pubblico del router e assegna un numero di porta univoco. 
  Quando il pacchetto di risposta ritorna, il router utilizza il numero di porta per determinare a quale dispositivo 
  interno inoltrare il pacchetto. PAT è una forma di Network Address Translation (NAT) ed è particolarmente 
  utile per conservare gli indirizzi IP pubblici, che sono una risorsa limitata. Inoltre, offre un livello aggiuntivo 
  di sicurezza, poiché gli indirizzi IP privati non sono visibili dall'esterno della rete locale. Qui effettivamente 
  vado a risparmiare indirizzi IP poiché possiamo internamente vedere più indirizzi come fossero lo stesso, 
  così facendo però riduco i possibili flussi distinguibili a 2^16 dato che vengono distinti dalle porte. 
  (VERIFICARE SE SEMANTICAMENTE CORRETTO)
  - **Full Cone NAT, Restricted Cone NAT, Symmetric NAT**: Definiscono il tipo di traffico permesso.

### Considerazioni sui Firewall
- **Protezione degli host**: Il firewall può essere software (per accessi domestici) o hardware (per reti aziendali).
- **Politiche di sicurezza**:
  - **Default deny**: Blocca tutto eccetto ciò che è esplicitamente permesso.
  - **Default permit**: Permette tutto eccetto ciò che è esplicitamente bloccato.

## IPV6

### Problematiche dell’indirizzamento IP

- **Mobilità**
  - **Indirizzi riferiti alla rete di appartenenza**: Gli indirizzi IP sono legati alla rete a cui appartengono. Se un host viene spostato in un’altra rete, il suo indirizzo IP deve cambiare.
  - **Configurazione automatica con DHCP**: Il Dynamic Host Configuration Protocol (DHCP) permette la configurazione automatica degli indirizzi IP, facilitando la gestione degli indirizzi in reti dinamiche.
  - **Mobile IP**: Mobile IP è una tecnologia che permette agli utenti di spostarsi tra diverse reti mantenendo lo stesso indirizzo IP, garantendo la continuità delle sessioni di rete.

- **Sicurezza**
  - **Scarsa protezione del datagramma IP**: L'intestazione dei datagrammi IP è in chiaro, rendendo vulnerabili i dati in transito.
  - **IPSec**: Il protocollo IPSec può essere applicato anche a IPv4 per migliorare la sicurezza delle comunicazioni, fornendo autenticazione e cifratura dei dati.

- **Dimensioni delle reti prefissate**
  - **Subnetting e CIDR**: Il subnetting e il Classless Inter-Domain Routing (CIDR) sono tecniche utilizzate per suddividere le reti in sottoreti più piccole e per ottimizzare l'uso degli indirizzi IP.

- **Esaurimento degli indirizzi IPv4**
  - **Reti IP private e NAT**: A causa dell'enorme diffusione di Internet, il numero di indirizzi IPv4 disponibili è insufficiente. Le reti IP private e il Network Address Translation (NAT) sono soluzioni temporanee per mitigare questo problema.

### IPv6

- **Supportare molti miliardi di host**: IPv6 è stato progettato per supportare un numero molto maggiore di indirizzi rispetto a IPv4.
- **Semplificare il routing**: IPv6 mira a rendere il routing più efficiente e scalabile.
- **Offrire meccanismi di sicurezza**: IPv6 include nativamente il supporto per IPSec, migliorando la sicurezza delle comunicazioni.
- **Offrire qualità di servizio (QoS)**: IPv6 fornisce meccanismi per garantire la qualità del servizio, essenziale per applicazioni multimediali.
- **Gestire bene multicast e broadcast**: IPv6 migliora la gestione del multicast e del broadcast rispetto a IPv4.
- **Consentire la mobilità**: IPv6 supporta la mobilità degli host, permettendo agli utenti di spostarsi tra diverse reti senza cambiare indirizzo IP.
- **Evoluzione futura e compatibilità**: IPv6 è progettato per consentire future evoluzioni e garantire la compatibilità con le versioni precedenti.


(MANCANO 24 MIN DELLA LEZIONE DEL 16 OTTOBRE POICHè NON HO TROVATO LE SLIDE)

## Routing

### Funzioni di IP
- **Indirizzamento**: L'IP fornisce un sistema di indirizzamento univoco per identificare dispositivi sulla rete.
- **Frammentazione**: L'IP può dividere i pacchetti di dati in frammenti più piccoli per adattarsi alla dimensione 
massima del pacchetto supportata dai vari segmenti della rete.
- **Instradamento**:
  - Decidere che percorso un datagramma deve seguire per raggiungere la destinazione.
  - Utilizza le PCI dei datagrammi, in particolare l'indirizzo di destinazione.
  - Determina il comportamento della funzione di commutazione nei nodi.
  - Il problema dell'instradamento è più generale rispetto al protocollo di livello 3.

### Algoritmi e protocolli di instradamento
- **Instradamento**: scelta del percorso.
  - Spesso significa scegliere il prossimo router (next hop).
- **Algoritmo di instradamento**:
  - Obiettivi: semplicità, robustezza, stabilità, efficienza.

### Tabella di instradamento
- I nodi di commutazione utilizzano tabelle predisposte localmente.
- **Algoritmi senza tabella e con tabella**:
  - **Senza tabella**: Flooding, Random, Deflection routing, Source routing.
  - **Con tabella**:
    - **Instradamento fisso e centralizzato**: Utilizzato per sistemi estremamente statici, dove i dati rimangono invariati per un tempo molto più lungo della singola comunicazione. Questo metodo risulta sempre uguale dal punto di vista dell'utente.
    - **Instradamento dinamico a distanza minima**: I percorsi vengono aggiornati periodicamente per adattarsi ai cambiamenti della rete dunque risulta più dinaico del precedente.

### Flooding
- Flooding è una tecnica di instradamento in cui ogni nodo della rete ritrasmette ogni pacchetto ricevuto su tutte le sue porte, eccetto quella da cui il pacchetto è arrivato. Questo metodo garantisce che tutte le possibili strade vengano percorse, assicurando che almeno una copia del pacchetto raggiunga la destinazione.
- Garantisce:
  - **Affidabilità**: Flooding garantisce che il pacchetto raggiunga la destinazione anche se alcuni percorsi sono interrotti.
  - **Percorso più breve**: Il primo pacchetto che raggiunge la destinazione lo fa percorrendo il percorso più breve disponibile.
  - **Semplicità**: L'algoritmo è semplice da implementare poiché non richiede tabelle di instradamento complesse.
- Contro:
  - **Proliferazione dei pacchetti**: La rete può essere sovraccaricata da un numero eccessivo di pacchetti duplicati, causando congestione.
  - **Inefficienza**: L'invio di pacchetti su tutte le porte può risultare inefficiente in termini di utilizzo della larghezza di banda.
- UTilizzato:
  - **Broadcasting**: Flooding è utile per inviare messaggi di broadcast, dove l'obiettivo è raggiungere tutti i nodi della rete.
  - **Scenari di emergenza**: In situazioni in cui è cruciale che il messaggio raggiunga la destinazione, indipendentemente dall'efficienza.

### Soluzioni per il Flooding
- Non ritrasmettere il pacchetto da dove è arrivato.
- Identificazione dei pacchetti (indirizzo sorgente + numero di sequenza).
- Uso di un TTL per evitare pacchetti infiniti.
È importante ricordare che all'aumentare di queste soluzioni il protocollo si complica, andando via via a perdere di utilità a causa del suo complicarsi.

### Instradamento dinamico e statico
- **Statico**: percorsi predefiniti all'inizializzazione.
- **Dinamico**: percorsi aggiornati periodicamente per adattarsi ai cambiamenti.

### Random e Deflection Routing
- **Random Routing**: Il prossimo hop è scelto casualmente. Questo metodo è molto inefficiente e raramente utilizzato.
- **Deflection Routing**: Il pacchetto viene inviato sulla linea con meno pacchetti in attesa. Questo metodo è stato 
studiato per reti a griglia (Manhattan), dove si dimostra essere una buona soluzione.
  - **Problemi**: I pacchetti possono arrivare fuori sequenza o entrare in cicli infiniti.

### Store-and-Forward
Il pacchetto viene verificato, memorizzato e confrontato con la tabella di instradamento. 
Dopo l'elaborazione, si seleziona un'uscita e il pacchetto viene inserito in coda. 
Tutto questo avviene in una coda che gestisce l'elaborazione.

### Shortest Path Routing
L'instradamento a percorso più breve implica l'associazione di una lunghezza a ciascun 
collegamento e la ricerca dei percorsi a costo minimo utilizzando algoritmi come Bellman-Ford e 
Dijkstra. Questo può essere implementato in modo centralizzato o distribuito, sia in maniera sincrona che asincrona. 
Quando i nodi di rete vengono accesi, conoscono solo la configurazione delle loro interfacce, che può essere statica 
o dinamica tramite DHCP. Con queste informazioni, popolano la tabella di instradamento iniziale. Per implementare il 
routing a percorso più breve (shortest path) verso qualsiasi destinazione, devono utilizzare uno o più protocolli di 
routing per scambiarsi informazioni e apprendere la topologia della rete, e uno o più algoritmi per il calcolo dei 
percorsi più brevi basati sulle informazioni ottenute.

### Teoria dei grafi e rappresentazione della rete
- Le reti possono essere rappresentate come grafi orientati o non orientati.
- Il peso degli archi rappresenta il costo del collegamento.

### Routing Distance Vector
Basato sull'algoritmo Bellman-Ford, ogni nodo invia un vettore con le distanze agli altri nodi. 
Questo metodo è piuttosto datato e presenta diversi problemi, ma su piccoli sistemi questi non emergono, 
rendendolo interessante in casi specifici, ovvero con dati statici, privi di variazioni in corso d'opera, 
e in cui possiamo conoscere l'intera struttura, cosa oggi impossibile dato che la rete è dinamica e distribuita. 
In questo metodo, ogni nodo ha una lista con la distanza dagli altri nodi. Inizialmente, questa lista è composta 
solo dalla distanza da se stesso, ovvero 0. Successivamente, i nodi (router) condivideranno con i nodi a cui sono 
direttamente collegati i propri dati detti **Distance vector**, aggiornando così le tabelle dei vicini. Questo processo continua finché non 
si reperiscono informazioni da tutti i nodi, passando per i vicini e ottenendo i percorsi migliori nel sistema.
- **Problemi**:
  - **Cold start e convergenza lenta**: La convergenza si raggiunge dopo un numero di iterazioni pari al numero di nodi. 
  Questo comporta una lenta convergenza su reti grandi, poiché gli aggiornamenti tra nodi non possono essere inviati 
  continuamente, ma devono lasciare che anche i messaggi circolino, ritardando così la convergenza.
  - **Conteggio all'infinito**: In alcuni casi, si potrebbe tentare di convergere all'infinito. 
  Ad esempio, se ci sono tre router in fila e si rompe il collegamento tra due di essi, gli altri due potrebbero 
  scambiarsi aggiornamenti di distanza dal terzo all'infinito. Questo li porta a convincersi reciprocamente che 
  per raggiungere il terzo router debbano usare l'altro a cui sono collegati, finendo per passarsi all'infinito 
  pacchetti e aggiornamenti di distanza, andando a bruciare capacità computazionale. Per ovviare, si sceglie una 
  distanza tra nodi superata la quale si considera la distanza come infinita ed implementare un Triggered Update,
  ovvero un aggiornamento istantaneo del distance vector qualora ci fosse una variazione di distanza.
  - **Bouncing effect**: Situazione in cui un router si "convince" che sia opportuno mandare i propri pacchetti 
  a un altro router che poi glieli rimanderà. Questo è solitamente dovuto a una rottura e, fino a quando non viene 
  inviato un aggiornamento, i router si rimpallano i pacchetti.
- **Soluzioni**
  - **Split Horizon**: evitare di informare un nodo su una destinazione raggiungibile solo tramite esso, 
  inviando distance vector differrnziati in cui ometto tutte le distanze da nodi che vedono il ricevente come gateway.
  - **Triggered Update**: inviare aggiornamenti immediatamente in caso di modifica.
Queste solozioni non sono definitive in quanto avendo una rete con dei cicli vanno 
a perdere di efficacia, dunque si è reso indispensabile trovare un' alternativa alla soluzione del routing distance vector.

### Routing Link State
In questa nuova soluzione, si separano nettamente il protocollo e l'algoritmo. 
Abbiamo una logica in cui, tramite uno specifico protocollo, i nodi scoprono altri nodi, 
estrapolano informazioni da questi ultimi e condividono tali informazioni con altri nodi. 
Questo processo permette a tutti i nodi di avere una visione completa della rete.
Solo a questo punto si utilizzano algoritmi di routing come Dijkstra per scoprire i percorsi più rapidi. 
Questo approccio comporta un maggiore utilizzo di memoria e una maggiore complessità computazionale. 
Tuttavia, se ogni nodo conosce tutta la rete, sarà in grado di reagire opportunamente in caso di guasto.

#### Vantaggi del Routing Link State
- **Convergenza rapida**: Poiché ogni nodo ha una visione completa della rete, le modifiche nella topologia 
vengono propagate rapidamente.
- **Percorsi ottimali**: Utilizzando algoritmi come Dijkstra, i percorsi calcolati sono generalmente più efficienti.
- **Maggiore affidabilità**: La conoscenza completa della rete permette di gestire meglio 
i guasti e le variazioni nella topologia.

#### Svantaggi del Routing Link State
- **Maggiore utilizzo di memoria**: Ogni nodo deve memorizzare una copia completa della topologia della rete.
- **Maggiore complessità computazionale**: Gli algoritmi di calcolo dei percorsi, come Dijkstra, 
richiedono più risorse computazionali.
- **Overhead di comunicazione**: La necessità di scambiare informazioni di stato tra i nodi può generare 
un significativo overhead di comunicazione.

#### Processo di Routing Link State
1. **Scoperta dei vicini**: Ogni nodo scopre i nodi vicini tramite messaggi di "Hello Packet".
2. **Misurazione della distanza dai vicini**: Calcolo della distanza dai vicini tramite un messaggio "Echo Packet".
3. **Scambio di informazioni**: I nodi scambiano informazioni di stato tramite pacchetti di Link State Advertisement (LSA) 
contenenti:
  - La lista dei propri vicini
  - Il peso del loro collegamento
I pacchetti LSA sono trasmessi con il flooding (simile al broadcast con alcune attenzioni in più), 
facendo attenzione a non rimandarli da dove sono già provenuti, a scartare pacchetti già visti o 
temporalmente più vecchi di altri già ricevuti.
4. **Dijkstra** : A questo pinto abbiamo il nostro grafo su cui applicare Dijkstra:
    1. **Inizializzazione**:
      - Assegna una distanza iniziale di 0 al nodo sorgente e di infinito a tutti gli altri nodi.
      - Crea un insieme di nodi non visitati.
    2. **Selezione del nodo corrente**:
      - Seleziona il nodo non visitato con la distanza minore (inizialmente il nodo sorgente).
    3. **Aggiornamento delle distanze**:
      - Per ogni nodo adiacente al nodo corrente, calcola la distanza totale dal nodo sorgente passando per il nodo corrente.
      - Se questa distanza è minore della distanza attualmente registrata per il nodo adiacente, aggiorna la distanza.
    4. **Marcatura del nodo come visitato**:
      - Una volta esaminati tutti i nodi adiacenti, marca il nodo corrente come visitato (non sarà più considerato).
    5. **Ripetizione**:
      - Ripeti i passaggi 2-4 fino a quando tutti i nodi sono stati visitati o la distanza minore tra i nodi non visitati è infinita.
    6. **Costruzione del percorso**:
      - Una volta completato l'algoritmo, la distanza registrata per ogni nodo rappresenta la distanza minima dal nodo sorgente.
      - È possibile ricostruire il percorso più breve tracciando indietro dai nodi di destinazione al nodo sorgente utilizzando le distanze registrate.

#### Esempi di Protocolli Link State
- **OSPF (Open Shortest Path First)**: Un protocollo di routing link state ampiamente utilizzato nelle reti IP.
- **IS-IS (Intermediate System to Intermediate System)**: Un altro protocollo di routing link state utilizzato principalmente nelle reti di grandi dimensioni.

In sintesi, il routing link state offre una soluzione robusta e efficiente per il calcolo dei percorsi in reti complesse, a scapito di un maggiore utilizzo di risorse di memoria e computazionali.

### Router IP
- **Funzioni dei router**:
  - **Routing**: Determina il percorso ottimale per i pacchetti di dati attraverso la rete utilizzando algoritmi e 
  tabelle di instradamento volto allo scambio di informazioni in maniera ottimale.
  - **Forwarding**: Inoltra i pacchetti di dati ricevuti verso la loro destinazione finale basandosi sulle 
  informazioni contenute nella tabella di forwarding.
  - **Switching**: Gestisce il trasferimento dei pacchetti tra le diverse interfacce del router, garantendo un 
  flusso di dati efficiente, ovvero l'istaradamento fisico sull'opportuna interfaccia.
  - **Trasmissione**: Invio fisico dei pacchetti di dati attraverso la rete utilizzando i protocolli di livello inferiore, 
  come Ethernet o Wi-Fi.

### Classificazione dei Router
 - **SOHO (Small Office/Home Office)**:
    - **Descrizione**: Router progettati per piccoli uffici o ambienti domestici.
    - **Caratteristiche**: Solitamente offrono funzionalità di base come NAT, firewall, e supporto per connessioni Wi-Fi.
    - **Prestazioni**: Capacità di gestire un numero limitato di dispositivi e traffico moderato. Velocità di throughput tipicamente tra 100 Mbps e 1 Gbps.

  - **Access Router**:
    - **Descrizione**: Router utilizzati per connettere dispositivi finali a una rete più ampia.
    - **Caratteristiche**: Supportano funzionalità avanzate come QoS (Quality of Service), VPN (Virtual Private Network), e gestione delle VLAN (Virtual Local Area Network).
    - **Prestazioni**: Progettati per gestire un numero maggiore di dispositivi rispetto ai router SOHO, con throughput che può variare da 1 Gbps a 10 Gbps.

  - **Enterprise Router**:
    - **Descrizione**: Router destinati a grandi aziende e organizzazioni.
    - **Caratteristiche**: Offrono funzionalità avanzate di sicurezza, gestione del traffico, 
    e supporto per protocolli di routing complessi come OSPF e BGP.
    - **Prestazioni**: Capacità di gestire un elevato volume di traffico e numerosi dispositivi. 
    Velocità di throughput tipicamente superiori a 10 Gbps, con supporto per connessioni multiple ad alta velocità.

  - **Backbone Router**:
    - **Descrizione**: Router utilizzati nelle dorsali di rete per instradare il traffico tra diverse reti.
    - **Caratteristiche**: Progettati per alta affidabilità e prestazioni, con supporto per protocolli di routing avanzati e capacità di gestire grandi volumi di traffico.
    - **Prestazioni**: Velocità di throughput estremamente elevate, spesso superiori a 100 Gbps. Capacità di gestire migliaia di connessioni simultanee e instradare traffico su lunghe distanze.

### Tabelle di Routing e Forwarding
- **Routing table**: Conosciuta anche come RIB (Routing Information Base), contiene i prefissi di routing, 
i next hop, e le metriche. È quindi un insieme di dati grezzi su cui si basano i calcoli di instradamento. 
Queste informazioni derivano da una serie di protocolli o canali considerati affidabili, sia in termini assoluti 
che relativi rispetto ad altri.
- **Forwarding table**: Nota anche come FIB (Forwarding Information Base), è ottimizzata per l'inoltro rapido 
dei datagrammi. Su di essa si basa lo scambio di pacchetti, ed è generata a partire dalla RIB. Da quest'ultima 
si estraggono, tra tutte le informazioni considerate affidabili, quelle più utili all'inoltro dei pacchetti. 
Questo processo avviene grazie alla funzione chiamata **Route Selection Process**, che seleziona le rotte migliori per la FIB. 
Contestualmente, la produzione della FIB genera anche dati di output per i protocolli, consentendo di decidere 
quali informazioni comunicare agli altri nodi. Questo meccanismo offre una notevole flessibilità nel recepire, 
filtrare e inviare informazioni in base alle esigenze specifiche di ogni singolo router. 

## Instradamento nell’Internet globale

### Instradamento (Routing) nell’Internet globale
  - **Routing gerarchico**: In Internet, il routing è organizzato gerarchicamente in **sistemi autonomi (AS)**, 
  ciascuno identificato da un numero progressivo. Ogni AS gestisce autonomamente le proprie politiche di routing, 
  risolvendo internamente i problemi e importando solo le soluzioni identificate all'esterno. Questo approccio è 
  necessario per gestire la rete in modo efficiente, data la diversità degli oggetti operanti in rete.
  - **Protocolli di routing**:
    - **Interior Gateway Protocol (IGP)**: Gestisce il routing all’interno di un AS.
    - **Exterior Gateway Protocol (EGP)**: Gestisce il routing tra AS diversi, ad esempio tramite i protocolli EGP e BGP.

### Sistemi Autonomi (AS)
   - Definizione: Un AS è un insieme di router gestiti da un’unica amministrazione 
   e usa un unico protocollo di routing. Con CIDR, un AS è 
   identificato da un insieme di prefissi IP gestiti in modo unitario. 
   In sintesi estrema potremmo dire che è l'insieme di un prefisso di network.
   - **Esempi di AS**: GARR (rete italiana degli enti di ricerca), infatti l'Unibo da sola non 
   è un AS ma passa attraverso il GARR come tante altre università finendo per risultare un unico AS.
  - Un AS svolge compiti di import e di export rispettivamente:
    - **Import**: L'AS riceve e accetta le rotte pubblicizzate da altri AS ritenuti affidabili, 
    aggiornando le proprie tabelle di routing per includere queste nuove rotte.
    - **Export**: L'AS pubblicizza le proprie rotte e le rotte apprese da altri AS verso i 
    suoi vicini che, qualora lo ritenessero affidabile, permetterebbero loro di aggiornare le proprie 
    tabelle di routing con queste informazioni. 
  (RADb sito per sperimentare questo genere di cose)

### Internet Service Provider (ISP)
Organizzazione che fornisce servizi per l'utilizzo di Internet e che solitamente si registra come AS.
   - **Classificazione**:
     - **Tier 1**: ISP con copertura globale, non necessariamente tutto il mondo, ma grandi coperture su intere 
     **internet region**, ovvero porzioni di aree geografiche coperte da una connessione internet, 
     senza necessità di acquistare connettività.
     - **Tier 2**: Acquista connettività da Tier 1.
     - **Tier 3**: ISP locali che acquistano connettività da Tier 2 o altri ISP locali.
  - **Peering e interconnessione**: Il peering tra ISP non implica pagamenti diretti; è una relazione neutrale. 
  Gli IXP facilitano l’interconnessione tra ISP. Gli ISP nelle loro zone di pertinenza hanno dei POP (Points of Presence) 
  che sono punti di raccolta collegati tra loro da maglie. Tali POP si trovano in punti strategici come città e snodi 
  commerciali. Se ci sono più ISP in una stessa internet region, i POP saranno in posizioni limitrofe per entrambi gli ISP. 
  Tuttavia, non è quasi mai possibile farli comunicare direttamente, poiché gli ISP si propongono come AS (Autonomous Systems) 
  e quindi sarà necessario far avvenire la comunicazione in un punto di "contatto" che talvolta potrebbe essere molto distante 
  dal POP geograficamente più vicino. Tale collegamento unico deve essere molto robusto data la sua unicità. Esso è fornito da 
  compagnie dette **Internet Exchange** che forniscono tale infrastruttura detta **Internet Exchange Point** (IXP).

   (MANCA REGISTRAZIONE DELLA LEZIONE DEL 28 OTTOBRE)

### Protocollo RIP (Routing Information Protocol)

- **Caratteristiche**:  
  RIP è un protocollo di routing di tipo **distance vector**, il che significa che le sue decisioni di routing si basano sulla 
  distanza in termini di hop count. Utilizza messaggi di tipo **Request** per richiedere informazioni di routing e **Response** 
  per inviare aggiornamenti agli altri router della rete. Questi aggiornamenti vengono inviati periodicamente, come risposta a 
  una richiesta esplicita e quando un'informazione di routing cambia (triggered update). RIP è semplice da configurare e gestire, 
  ma presenta limiti significativi. Non supporta il **Classless Inter-Domain Routing (CIDR)**, che consente un uso più 
  efficiente degli indirizzi IP, e ha problemi di sicurezza poiché le informazioni di routing vengono trasmesse in chiaro. 
  Inoltre, in reti di grandi dimensioni, il tempo necessario per convergere può diventare critico, portando a potenziali 
  loop di routing e inefficienze.

- **Struttura del pacchetto**:
  I pacchetti RIP hanno una lunghezza variabile fino a 512 byte e sono strutturati su parole da 32 bit:
  - **Command**: Indica se il pacchetto è una richiesta (Request) o una risposta (Response).
  - **Version**: Specifica la versione del protocollo RIP utilizzata.
  - **Zero**: Campo riservato, impostato a zero.
  - **Address Family Identifier (AFI)**: Indica il tipo di indirizzo contenuto nel campo di indirizzo IP.
  - **IP Address**: L'indirizzo IP della rete di destinazione.
  - **Metric**: Il numero di hop necessari per raggiungere la rete di destinazione.

  Ogni pacchetto RIP può contenere fino a 25 voci di routing, ciascuna delle quali descrive una singola rotta.

- **Tabella di routing**:
  Ogni tabella di routing contiene:
  - **Indirizzo di destinazione**: Un indirizzo IP a 32 bit.
  - **Distanza dalla destinazione (metrica)**: In termini di hop-count (ogni link ha peso = 1). La distanza massima (∞) per RIP 
  è pari a 16, al fine di limitare il conteggio all’infinito, rendendolo adatto per reti relativamente piccole.
  - **Next-hop**: Il router vicino a cui inviare i datagrammi per la destinazione.
  - **Timeout**: Se una route non viene aggiornata dopo un certo numero di secondi (default 180 s), la sua distanza è posta 
  all’infinito (si ipotizza una perdita di connettività).
  - **Garbage-collection timer**: Se dopo ulteriori secondi (default 120 s) la route non viene aggiornata, viene eliminata 
  del tutto dalla tabella.

- **Aggiornamento delle tabelle di routing con RIP**:
  I router RIP inviano periodicamente aggiornamenti delle loro tabelle di routing a tutti i router vicini. 
  Quando un router riceve un aggiornamento, confronta le nuove informazioni con la propria tabella di routing. 
  Se trova una rotta più breve o una nuova rotta, aggiorna la propria tabella di conseguenza. Questo processo continua 
  finché tutte le tabelle di routing nella rete non sono sincronizzate.

- **Problematiche del Protocollo RIP**
  Il protocollo RIP presenta diverse problematiche che ne limitano l'efficacia e la sicurezza, 
  specialmente nelle reti di grandi dimensioni:
  - **Split Horizon**: RIP utilizza la tecnica dello split horizon per prevenire loop di routing. 
  Tuttavia, le risposte (RESPONSE) inviate dalle diverse interfacce possono variare, complicando la gestione delle tabelle 
  di routing.
  - **Triggered Update**: RIP supporta gli aggiornamenti immediati (triggered update) per ridurre il tempo di convergenza. 
  In questi aggiornamenti, non è necessario includere tutte le voci della tabella di routing, ma solo quelle appena modificate.
   Questo può portare a una maggiore efficienza, ma anche a una complessità aggiuntiva nella gestione degli aggiornamenti.
  - **Mancanza di Supporto per CIDR**: RIP non supporta il **Classless Inter-Domain Routing (CIDR)**, limitando la flessibilità 
  nella gestione degli indirizzi IP e portando a un uso inefficiente dello spazio di indirizzamento.
  - **Sicurezza**: RIP è considerato un protocollo insicuro. Chiunque trasmetta datagrammi dalla porta UDP 520 viene 
  considerato come un router autorizzato. Questo può portare a vulnerabilità significative, come nel seguente esempio di 
  malfunzionamento indotto:
    - Un router non autorizzato trasmette messaggi indicando una distanza di 0 tra se stesso e tutti gli altri nodi della rete.
    - Dopo un certo periodo, tutti i percorsi ottimali convergono su questo router non autorizzato, causando potenziali 
    disservizi e problemi di sicurezza.

### RIP versione 2
RIP versione 2 introduce miglioramenti significativi rispetto alla versione 1, affrontando alcune delle sue 
limitazioni principali. Le modifiche includono:
  - **Supporto per Subnetting e CIDR**: RIP v2 supporta il subnetting e il Classless Inter-Domain Routing (CIDR), permettendo una gestione più efficiente degli indirizzi IP.
  - **Autenticazione**: RIP v2 include meccanismi di autenticazione per migliorare la sicurezza delle informazioni di routing. Questo aiuta a prevenire l'inserimento di informazioni di routing non autorizzate.
  - **Trasporto di Maschere di Sottorete**: RIP v2 trasporta le maschere di sottorete insieme agli indirizzi IP, consentendo una maggiore flessibilità nella configurazione delle reti.
  
  - **Struttura dei Pacchetti RIP v2**:
  I pacchetti RIP v2 mantengono una struttura simile a quella della versione 1, ma con alcune aggiunte:
    - **Command**: Indica se il pacchetto è una richiesta (Request) o una risposta (Response).
    - **Version**: Specifica la versione del protocollo RIP utilizzata (2 per RIP v2).
    - **Zero**: Campo riservato, impostato a zero.
    - **Address Family Identifier (AFI)**: Indica il tipo di indirizzo contenuto nel campo di indirizzo IP.
    - **Route Tag**: Campo aggiuntivo per identificare le rotte esterne.
    - **IP Address**: L'indirizzo IP della rete di destinazione.
    - **Subnet Mask**: La maschera di sottorete associata all'indirizzo IP.
    - **Next Hop**: L'indirizzo IP del prossimo hop verso la destinazione.
    - **Metric**: Il numero di hop necessari per raggiungere la rete di destinazione.

Questi miglioramenti rendono RIP v2 più adatto per l'uso in reti moderne, 
offrendo maggiore flessibilità e sicurezza rispetto alla versione precedente.

### Open Shortest Path First (OSPF)
**Open Shortest Path First (OSPF)** è un **protocollo di routing** largamente adottato, standardizzato nella versione 2 (RFC 2328), e tra i più diffusi nell’ambito delle **reti interne (IGP)**. È di tipo **link-state** e usa pacchetti **Link State Advertisement (LSA)** per condividere informazioni di rete con altri router. OSPF è incapsulato direttamente nel **protocollo IP**, con un protocol number di valore 89 per distinguere i pacchetti OSPF dagli altri.

### Struttura Gerarchica e Aree di OSPF
OSPF semplifica il **routing** in reti complesse suddividendole in **aree**, interconnesse tramite un’**area backbone** (Area 0). Questa suddivisione crea una struttura **gerarchica** che riduce il carico sui router e consente la **comunicazione tra aree** tramite router specifici. I principali tipi di router in OSPF includono:
- **Internal Router**, interni a un’area specifica
- **Area Border Router (ABR)**, che collegano più aree
- **Backbone Router**, che gestiscono le connessioni con l’area centrale
- **AS Boundary Router (ASBR)**, responsabili della comunicazione con **Autonomous Systems (AS)** esterni utilizzando protocolli **EGP**

### Tipi di Route
OSPF gestisce vari tipi di **route**:
- **Route intra-area**: informazioni di routing interne all’area
- **Route inter-area**: aggiornamenti tra aree diverse
- **Route esterne**: route da altri protocolli o AS, inoltrate tramite l’**ASBR**

### Tipologie di Aree
Le aree di OSPF possono assumere configurazioni diverse per ottimizzare il routing:
- **Area normale**: accetta tutte le route
- **Stub area**: utilizza un **default route** per destinazioni esterne, con minori requisiti di memoria
- **Totally stub area**: consente solo route interne e il default route
- **Not So Stubby Area (NSSA)**: permette di importare alcune route esterne, mantenendo limitata la propagazione

### Funzionalità Avanzate di OSPF
OSPF offre funzionalità aggiuntive per migliorare l’efficienza della rete:
- **Bilanciamento del carico**: ripartisce il traffico su percorsi multipli di uguale costo
- **Autenticazione**: protegge lo scambio di informazioni con **password** o **crittografia**
- **Quality of Service (QoS)**: seleziona percorsi in base al **Type of Service**, consentendo livelli di servizio differenziati

### Tipologie di Reti Supportate
OSPF supporta **reti punto-punto** e **reti multi-accesso**, tra cui **Broadcast Multi-Access (LAN 802)** e **Non-Broadcast Multi-Access** (ad esempio, X.25, ATM). In queste reti, utilizza una struttura a **stella virtuale** per ridurre le connessioni necessarie. In reti multi-accesso, si usano due ruoli chiave:
- **Designated Router (DR)**, per ottimizzare la comunicazione. Qui i nodi si accorderanno su che debba essere considerato 
il disegnato in modo tale da usarlo come centro ed evitare di sovraccaricare gli altri con un flusso inutilmente elevato di pacchetti.
- **Backup Designated Router (BDR)**, per garantire **affidabilità** dato che di fatto il diseganto non ha alcuna peculiarità rispetto agli altri.

### Identificatori e Priorità dei Router
Ogni router OSPF ha un **Router ID** univoco e può avere una **priorità** (da 0 a 255) per determinare l’elezione del DR, tolti coloro che hanno priorità scelto si va a sciegliere chi ha la priorità più alta e lo si elegge. Nelle reti multi-accesso, il **DR** coordina le comunicazioni e ottimizza lo scambio di informazioni tra router **adiacenti** ovvero tutti quei router connessi in maniaera diretta e che utilizzano effettivamente tale connessione per comunicsre, se non lo facessere nonostante siano collegati direttamente sarebbero detti **vicini**.

### Struttura del Pacchetto OSPF

Il pacchetto OSPF è composto da diverse sezioni chiave, ciascuna con un ruolo specifico nel protocollo:

1. **Header OSPF**:
  - **Version**: La versione del protocollo OSPF.
  - **Type**: Il tipo di pacchetto OSPF (Hello, Database Description, Link State Request, Link State Update, Link State Acknowledge).
  - **Packet Length**: La lunghezza totale del pacchetto OSPF.
  - **Router ID**: L'identificatore univoco del router che invia il pacchetto.
  - **Area ID**: L'identificatore dell'area OSPF da cui proviene il pacchetto.
  - **Checksum**: Un valore di controllo per verificare l'integrità del pacchetto.
  - **Authentication Type**: Il tipo di autenticazione utilizzato.
  - **Authentication**: I dati di autenticazione.

2. **Dati Specifici del Tipo di Pacchetto**:
  - **Hello Packet**: Contiene informazioni sui vicini, l'intervallo Hello, e il Dead Interval.
  - **Database Description Packet**: Include una descrizione del database di stato dei collegamenti.
  - **Link State Request Packet**: Richiede informazioni specifiche sullo stato dei collegamenti.
  - **Link State Update Packet**: Trasporta aggiornamenti sullo stato dei collegamenti.
  - **Link State Acknowledge Packet**: Conferma la ricezione degli aggiornamenti sullo stato dei collegamenti.

Questa struttura modulare consente a OSPF di gestire efficacemente la comunicazione e la sincronizzazione delle informazioni di routing tra i router.

### Protocolli di Comunicazione in OSPF
OSPF utilizza tre **sottoprotocolli** principali:
- **Hello**: scopre i router vicini e far sapere della propria presenza agli altri, avvia l’elezione del DR e del BDR e costantemente verifica la presenza dei vicini
- **Exchange**: sincronizza i database di **link-state** tra router adiacenti ed avviene solo all'inizio
- **Update**: diffonde le informazioni di routing in tutta la rete via flooding, così facendo si vaa costruire debtro ad ogni router la mappa intera della rete.

I **pacchetti principali** di OSPF includono:
- **Hello** (Tipo 1), per rilevare i vicini
- **Database Description** (Tipo 2), per descrivere il database
- **Link State Request** (Tipo 3) e **Link State Update** (Tipo 4) per l’aggiornamento delle informazioni di routing
- **Link State Acknowledge** (Tipo 5), per confermare la ricezione

### Stub Area e Routing verso l’Esterno
Le **stub area** sono progettate per ottimizzare le risorse di rete in configurazioni con un solo punto di uscita. Il routing verso l’esterno si basa su un **default route**, riducendo la dimensione delle **tabelle di routing** e il carico sui router di bordo, ideali per le aree con basse risorse di memoria.

### Multicast e IP Multicast
   - **Multicast** rappresenta una soluzione efficace per la trasmissione di dati a più destinatari simultaneamente, 
   riducendo il carico di traffico di routing. A differenza del broadcast, che invia informazioni a tutti i nodi della rete, 
   il multicast consente di inviare pacchetti solo ai gruppi specifici di destinatari che si sono registrati per riceverli. 
   Questo approccio è particolarmente utile in applicazioni come lo streaming video e le videoconferenze.  
   - **Indirizzi multicast**: Gli indirizzi IP multicast sono assegnati a un intervallo specifico, compreso tra 224.0.0.0 e 
   239.255.255.255. Questi indirizzi permettono l'identificazione di gruppi multicast e sono utilizzati dai router per 
   instradare i pacchetti solo ai nodi interessati, contribuendo così a una gestione più efficiente della larghezza di banda.

### Internet Group Management Protocol (IGMP)
   - L'**Internet Group Management Protocol (IGMP)** è un protocollo fondamentale per la gestione dei gruppi multicast. 
   Consente agli host di comunicare con i router multicast, dichiarando la loro appartenenza a specifici gruppi. 
   Attraverso IGMP, gli host possono anche abbandonare i gruppi a cui non desiderano più partecipare. Questo processo è 
   cruciale per mantenere l'efficienza della rete, poiché garantisce che solo gli host interessati ricevano i dati multicast.  
   - IGMP opera in diverse versioni, ciascuna con miglioramenti rispetto alla precedente, per gestire meglio la congestione e 
   ottimizzare l'uso delle risorse di rete. Inoltre, il protocollo facilita la comunicazione tra i router e gli host, 
   consentendo un aggiornamento dinamico delle informazioni sui gruppi multicast attivi nella rete.

## Exterior Gateway Protocols (EGP)

### Protocolli EGP

I protocolli di tipo EGP si distinguono dai protocolli di tipo IGP per le loro finalità e logiche operative:
- All’interno di un Autonomous System (AS), si mira principalmente all’ottimizzazione dei percorsi.
- Nel routing tra AS, si devono considerare soprattutto le politiche di instradamento:
  - Ogni AS preserva la propria autonomia e indipendenza dalle decisioni di altri.
  - Alcuni AS limitano il transito del traffico da altri AS attraverso le loro reti, ciò può dipendere da diversi fattori come per esempio dinamiche geopolitiche o più generalmente da accordi tra AS rendendo dunque lo shorter path non prioritario.
  - In determinati contesti, si seguono accordi internazionali per la gestione del traffico.
  
Due protocolli principali di tipo EGP utilizzati in Internet sono:
- **Exterior Gateway Protocol (EGP)**, molto vecchio e praticamente abbandonato.
- **Border Gateway Protocol (BGP)**

## Border Gateway Protocol (BGP)

### BGP
sviluppato per sostituire EGP e attualmente è disponibile nella versione 4 (RFC 1771). I router BGP utilizzano connessioni TCP (porta 179), chiamate sessioni BGP, per uno scambio affidabile delle informazioni di routing:
- **Sessioni BGP esterne (eBGP)** tra router in AS diversi.
- **Sessioni BGP interne (iBGP)** tra router nello stesso AS.
  
BGP scambia informazioni di raggiungibilità per reti IP secondo lo schema *classless* (CIDR), permettendo un instradamento flessibile e dettagliato.

### BGP e Path Vector
BGP utilizza un protocollo di tipo *Path Vector*, un’evoluzione del distance vector, che offre:
- **Elenco degli AS nel percorso**: Contiene l'elenco esaustivo degli AS da attraversare per raggiungere uno specifico AS, risolvendo i cicli e permettendo politiche di routing più efficaci. 
La necessità di conoscere nel dettaglio tutte le path ha portato a un problema di grandezza delle tabelle. La frammentazione degli indirizzi ha reso necessario conservare in memoria "fette" di indirizzi sempre più frammentate, portando a tabelle con righe nell'ordine di quasi 10^6. Questo comporta una lettura di tali tabelle per l'instradamento di ogni singolo pacchetto. Inoltre, il fenomeno della crescita esponenziale della banda dei collegamenti aggrava la situazione. La combinazione di aumento esponenziale della grandezza delle tabelle e del numero di pacchetti trasportati per secondo rischia di mettere in crisi l'infrastruttura di collegamento.
  
- **Politiche di routing**:
  - **Export policies**: permette il transito solo verso destinazioni consentite.
  - **Import policies**: esclude percorsi che coinvolgono AS non conformi alle politiche di routing o non considera le informazioni da esso ricevute.

Questo approccio richiede maggiore larghezza di banda per il routing e memoria nei router per memorizzare i path vector.

### Scambio di Path Vector
Ogni path vector scambiato con i vicini include i seguenti attributi:
- **Origin**: indica l’origine del percorso (IGP, EGP o incomplete).
- **AS path**: elenca gli AS da attraversare per raggiungere una destinazione.
- **Next hop**: specifica l’indirizzo del router di bordo dell’AS che deve essere utilizzato come prossimo passo verso la destinazione.
Questi attributi possono avere diverse caratteristiche:
- **Well-known**: attributi che devono essere riconosciuti da tutti i router BGP.
  - **Mandatory**: attributi well-known che devono essere presenti in ogni aggiornamento BGP.
  - **Discretionary**: attributi well-known che possono essere presenti o meno in un aggiornamento BGP.
- **Optional**: attributi che non devono essere necessariamente riconosciuti da tutti i router BGP.
  - **Transitive**: attributi optional che devono essere trasmessi anche se non riconosciuti.
  - **Non-transitive**: attributi optional che non devono essere trasmessi se non riconosciuti.

### Formato dei Messaggi BGP
I messaggi BGP sono strutturati in un formato specifico per garantire la corretta comunicazione tra i router. Ogni messaggio BGP inizia con un header comune, seguito da campi specifici a seconda del tipo di messaggio. L'header comune include:
- **Marker (16 byte)**: Campo utilizzato per la sincronizzazione e la sicurezza.
- **Length (2 byte)**: Lunghezza totale del messaggio BGP, compreso l'header.
- **Type (1 byte)**: Tipo di messaggio BGP (Open, Update, Notification, Keepalive).
A seconda del tipo di messaggio, l'header è seguito da campi specifici:
- **Open**: Include l'ID dell'AS, il numero di versione BGP, il tempo di hold, l'ID del router e i parametri opzionali.
- **Update**: Contiene informazioni sulle rotte da aggiungere o rimuovere, inclusi i prefissi IP e gli attributi del percorso.
- **Notification**: Fornisce dettagli sugli errori riscontrati e chiude la connessione.
- **Keepalive**: Messaggio semplice utilizzato per mantenere attiva la connessione senza trasmettere nuove informazioni di routing.
Questa struttura modulare consente a BGP di gestire in modo efficiente e sicuro la comunicazione tra router in diverse reti autonome.

### BGP: Tipi di Messaggi
I messaggi di BGP includono un header comune (marker, length, type) e possono assumere i seguenti tipi:
- **Open**: inizia una connessione BGP e include identificazione dell’AS, timeout e autenticazione.
- **Update**: trasmette il path vector e relativi attributi.
- **Notification**: notifica errori e chiusura della connessione.
- **Keepalive**: conferma la connessione attiva senza nuove informazioni di routing.

## Ifrastruutura regionale italiana
In Italia, l'infrastruttura degli Autonomous Systems (AS) è distribuita tra reti private, reti pubbliche e diversi punti di interscambio fondamentali per il traffico Internet nazionale e internazionale. Gli AS italiani sono numerosi e variano per dimensione e scopo: dai provider di servizi Internet (ISP) alle reti aziendali, fino alle reti gestite dalle pubbliche amministrazioni. Due strutture cardine che facilitano l'interconnessione e migliorano l'efficienza del traffico Internet in Italia sono il **Milan Internet Exchange (MIX)** e la rete **LEPIDA**.

### Il Ruolo del MIX
Il Milan Internet Exchange (MIX) è uno dei più importanti punti di interscambio di traffico Internet in Italia e uno dei maggiori a livello europeo. Situato a Milano, MIX permette l’interconnessione diretta tra AS di vari operatori, riducendo la latenza e ottimizzando il routing del traffico Internet a livello nazionale e internazionale. MIX è una struttura neutrale e indipendente che offre servizi di peering pubblico e privato, consentendo ai provider di scambiarsi traffico direttamente. Ciò riduce la necessità di instradare il traffico verso AS esteri, favorendo una maggiore autonomia della rete italiana e migliorando l’efficienza di trasmissione tra reti locali. Questo snodo è particolarmente importante per garantire la connettività tra le grandi reti italiane e l’infrastruttura globale di Internet.

### La Rete LEPIDA
LEPIDA è una rete regionale di proprietà pubblica, gestita dalla società Lepida S.p.A., che supporta il sistema di interconnessione digitale per le pubbliche amministrazioni dell’Emilia-Romagna. Nasce con l’obiettivo di interconnettere le amministrazioni pubbliche regionali, migliorando la qualità dei servizi digitali rivolti ai cittadini e garantendo la sicurezza e la gestione diretta delle reti di pubblica utilità. LEPIDA opera anche come AS e stabilisce connessioni con altri AS nazionali e internazionali, facilitando l'accesso a risorse e servizi pubblici in tutta Italia. Grazie a LEPIDA, la Regione Emilia-Romagna gode di un’infrastruttura autonoma e indipendente, riducendo la dipendenza da operatori privati e aumentando la resilienza della rete regionale.

In questo scenario, MIX e LEPIDA contribuiscono a una maggiore autonomia e resilienza della rete italiana. Il MIX facilita l'interconnessione tra grandi reti commerciali e nazionali, mentre LEPIDA supporta un’infrastruttura dedicata alla pubblica amministrazione, assicurando una comunicazione efficiente e sicura per il settore pubblico e migliorando il servizio per i cittadini e le imprese a livello regionale.

## Virtualizzazione di Rete

### Virtualizzazione di Rete
La virtualizzazione di rete permette la creazione di versioni virtuali di infrastrutture di computazione, memorizzazione e reti, realizzando componenti che si comportano come sistemi software indipendenti dall'hardware fisico. Questo approccio garantisce vantaggi significativi come la condivisione delle risorse fisiche e il disaccoppiamento tra progetto software e hardware, migliorando flessibilità, mobilità e scalabilità. Tuttavia, la virtualizzazione comporta criticità legate alla sicurezza e all'isolamento dei sistemi che condividono lo stesso hardware fisico.

### Obiettivo e Tecniche della Virtualizzazione di Rete
La virtualizzazione di rete risponde alla crescente complessità dei requisiti di servizio dell’utenza, consentendo di realizzare topologie o funzionalità su infrastrutture esistenti, altrimenti difficili da modificare. Questo approccio spesso si basa su "reti overlay", ovvero reti logiche sovrapposte all'infrastruttura fisica per creare funzionalità aggiuntive, le network IP nel loro piccolo ne sono un esempio. Tra le tecnologie che consentono questo tipo di virtualizzazione troviamo VLAN (IEEE 802.1Q), GRE (RFC 1701), VXLAN (RFC 7348) e VPN, che rappresentano alcune delle soluzioni per segmentare, incapsulare e isolare il traffico di rete virtuale.

### Reti Overlay: VLAN, GRE e VXLAN
- **VLAN**: Le Virtual Local Area Network (VLAN) creano domini di broadcast separati all'interno della stessa rete fisica, migliorando sicurezza e prestazioni. VLAN statiche e dinamiche permettono una gestione ottimizzata delle risorse, mentre l'uso del protocollo IEEE 802.1Q facilita l'instradamento su più switch.
- **GRE (Generic Routing Encapsulation)**: GRE permette l'incapsulamento di pacchetti su protocollo IP, creando un overlay di routing che separa logica e rete fisica, se analizzassimo dunque il pacchetto non vedremmo l'originale indirizzo IP ma quello che gli abbiamo attribito. Il GRE ho un header specifico che gli permette di specificare il protocollo contenuto ed altri parametri opzionali. Grazie al GRE potrò creare dei tunnel fittizi che vanno a modellare la topologia della rete, così facendo posso astrarre una rete fittizia che non varia al variare, dovuto per esempio ad una rottura, della rete fisica.
- **VXLAN (Virtual eXtensible LAN)**: VXLAN, ampiamente usato nel cloud computing, consente l'incapsulamento di traffico Layer 2 in pacchetti UDP, garantendo un isolamento scalabile con identificatori unici per ciascun segmento. Creado un tunnel VXLAN ottengo la fusione di 2 LAN distinte dato che grazie al tunnel esse risponderanno alla stessa ARP request. 
Il tunnel VXLAN funziona incapsulando i frame Ethernet in pacchetti UDP, che vengono poi trasmessi attraverso una rete IP. Ogni segmento VXLAN è identificato da un VXLAN Network Identifier (VNI), che consente di isolare il traffico tra diversi segmenti. I dispositivi che terminano i tunnel VXLAN, noti come VXLAN Tunnel Endpoints (VTEP), aggiungono e rimuovono l'incapsulamento VXLAN. Quando un frame Ethernet entra in un VTEP, viene incapsulato in un pacchetto UDP con un header VXLAN e inviato attraverso la rete IP. Il VTEP di destinazione rimuove l'incapsulamento e inoltra il frame Ethernet alla rete locale.
Nonostante i vantaggi, l'uso di VXLAN può introdurre alcuni problemi di prestazione:
- **Overhead di Incapsulamento**: L'aggiunta di header VXLAN e UDP aumenta la dimensione dei pacchetti, riducendo l'efficienza della trasmissione e aumentando il carico sulla rete.
- **Latenza**: L'incapsulamento e il decapsulamento dei pacchetti richiedono tempo di elaborazione aggiuntivo, che può aumentare la latenza end-to-end.
- **Fragmentazione dei Pacchetti**: L'aumento della dimensione dei pacchetti può causare la frammentazione, che a sua volta può ridurre le prestazioni e aumentare il rischio di perdita di pacchetti.

### Reti Private Virtuali (VPN) e la Sicurezza del Tunneling

Le **VPN** sono reti sovrapposte su reti pubbliche che garantiscono connessioni sicure attraverso il **tunneling cifrato** e l'**autenticazione**. Esistono principalmente due tipologie di VPN: le **Roadwarrior VPN** e le **VPN Net-to-Net**:
- **Roadwarrior VPN**: Questo tipo di VPN è configurato per offrire accesso sicuro a utenti singoli che si collegano da punti remoti, creando connessioni sicure punto-punto verso un server VPN dedicato capace di gestire una rete a stella tra client molteplici. Tuttavia, questa configurazione, se utilizzata da un elevato numero di dispositivi, può comportare un overhead significativo poiché richiede un tunnel per ogni dispositivo. Lo si può utilizzare per emulare un'altra posizione geografica grazie al fatto che, se il server si trova in un'internet region diversa dalla propria, il ricevente è convinto che i propri messaggi arrivino da quell'internet region. Questa metodologia è funzionale solo se gli host si trovano de-localizzati sulla rete; se invece sono co-localizzati ci sarà un grande spreco di computazione.
- **Net-to-Net VPN**: Le Net-to-Net VPN collegano intere LAN o reti IP tramite un unico tunnel cifrato, sfruttando un canale sicuro su rete pubblica, agendo sui gateway di uscita dalla nostra network IP e quelli di ingresso dell'host ricevente. I pacchetti vengono criptati nel tunnel, mentre l’indirizzamento IP reale può essere mascherato, garantendo così privacy e sicurezza nelle connessioni tra sedi aziendali distribuite. Questo tipo di VPN è particolarmente adatto per reti aziendali, poiché consente di ridurre il numero di connessioni dirette necessarie.

### Il Ruolo di IPsec per la Sicurezza delle VPN
Lo standard IPsec (Internet Protocol Security) è il principale protocollo per la cifratura e autenticazione dei dati trasmessi su reti pubbliche tramite VPN. Offre due modalità principali: **Transport Mode** (che protegge solo i dati dell'utente) e **Tunnel Mode** (che protegge l'intero pacchetto IP). Gli elementi principali di IPsec sono:
- **IKE (Internet Key Exchange)**: È il protocollo di negoziazione che autentica i partecipanti alla VPN, negoziando algoritmi crittografici e chiavi, utilizzando UDP che supporta porta sorgente e destinazione 500, ciò comporta che se sulla path troviamo una NAT si potrebbe incappare in una problematica data dal cambio di porta.
- **AH (Authentication Header)** e **ESP (Encapsulating Security Payload)**: AH assicura autenticità, integrità dei pacchetti e identità del mittente, mentre ESP include anche la riservatezza attraverso la cifratura icapsulando il pacchetto e dunque esponedolo a frammentazione durante il trasporto dato che ne aumenta le dimensioni. Con ESP Transoprt cifro solo il contenuto mentre con ESP Tunnel cifro l'intero pacchetto comprensivo di IP.
Grazie a queste caratteristiche, le VPN realizzate con IPsec garantiscono alti livelli di sicurezza e sono la soluzione preferita per interconnettere reti aziendali che devono trasmettere dati sensibili su Internet, offrendo riservatezza, autenticazione e una protezione costante dei dati attraverso reti pubbliche.

## Mezzi Trasmissivi

### Legge di Edholm
La **Legge di Edholm** prevede che la larghezza di banda delle reti di telecomunicazione raddoppi ogni 18 mesi.

### Attenuazione
L'attenuazione è la riduzione della potenza del segnale man mano che si propaga attraverso un mezzo trasmissivo. L'attenuazione è misurata in decibel per kilometro (dB/km). L'attenuazione è un parametro critico nella progettazione delle reti di telecomunicazione, poiché influisce sulla qualità e sulla distanza massima di trasmissione del segnale. 
- L'**attenuazione sul rame** crese esponenzialmente con la lunghezza del collegamento e con la radice della frequeza del seganle, avrà dunque un fattore di dispersione olto altro che si quantifica con la formula:
  \[ A = 10 \log_{10} \left(\frac{P_t}{P_r}\right) = a \sqrt{f} L \]
  Per limitare l'attenuazione di usa la tecnica del **twined pair** che considte del arrotolare a spirale le coppie per contenere la dimendione del campo generatoe dunque la sua dispersione, ne esistono di 2 tipi: **STP** schemati da un conduttore e **UTP** non schermati.
  I **Coassiali** permettono di raggiungere distaze maggiori, si copriranno distanze connesse da ripetitori (nodi semplificati) che collegano più tratte.
- L'**attenuazione delle Radio comunicazioni** è la diminuzione della potenza del segnale radio mentre si propaga attraverso l'aria o altri mezzi. Questo fenomeno è influenzato da vari fattori, tra cui la distanza tra il trasmettitore e il ricevitore, la frequenza del segnale, le condizioni atmosferiche e la presenza di ostacoli fisici come edifici o montagne. Ad esempio, l'attenuazione cresce in maniera polinomiale con il quadrato della frequenza, e le antenne diventano più efficaci quando la frequenza aumenta.

  La propagazione ionosferica è un fenomeno in cui le onde radio vengono riflesse o rifratte dalla ionosfera, uno strato dell'atmosfera terrestre carico di particelle ionizzate. Questo tipo di propagazione permette alle onde radio di coprire distanze molto maggiori rispetto alla propagazione diretta, rendendola utile per le comunicazioni a lunga distanza, come quelle utilizzate nelle trasmissioni radio a onde corte.

  Attualmente, l'utilizzo della ionosfera è stato superato grazie ai satelliti in orbita geostazionaria, che svolgono lo stesso lavoro ad un'altezza maggiore e con una portata più ampia. Tuttavia, poiché le orbite geostazionarie sono limitate, si possono utilizzare satelliti non stazionari che orbitano più vicino alla Terra. Questi satelliti sono più facili da installare ma non rimangono fissi, quindi è necessario averne un numero maggiore per garantire una copertura continua.

### Telefonia Cellulare

- L'obiettivo iniziale della telefonia cellulare era incrementare il numero di terminali per ridurre i costi elevati della tecnologia e delle infrastrutture, rendendo il servizio più accessibile a un numero crescente di utenti.
- **Sviluppo delle Celle**: per aumentare l’efficienza e ridurre i costi, le reti cellulari sono state organizzate in celle, piccole aree coperte ciascuna da un’antenna. Questa struttura permette di servire molti utenti all'interno di un'area circoscritta, migliorando la capacità complessiva della rete e permettendo un uso efficiente delle frequenze disponibili.
- **Gestione della Copertura**: ogni cella è progettata per supportare un certo numero di chiamate simultanee, e le celle sono posizionate in modo da garantire che, anche se un utente si sposta da una cella all’altra, il servizio rimanga continuo. Le celle si sovrapporrano dunque in alcuni punti, questo va però ad evitare che si formino degli spazi non coperti.

![immagine locale](img\Reti\celle_di_copertura_cellulare.PNG)

### Fibra Ottica

- La fibra ottica ha rivoluzionato le reti di telecomunicazione, sostituendo progressivamente il rame nella rete di trasporto a partire dagli anni 2000. Con una larghezza di banda significativamente superiore, la fibra ottica supporta la trasmissione di grandi quantità di dati su lunghe distanze con una minima perdita di segnale, migliorando drasticamente la qualità e l'affidabilità delle comunicazioni.
- **Caratteristiche**: le fibre ottiche sono sottili filamenti di vetro o plastica che trasportano dati sotto forma di impulsi luminosi. La fibra offre un'elevata capacità di trasporto dati e una bassa attenuazione, rendendola ideale per le tratte di lunga distanza. Negli anni, la tecnologia della fibra ha permesso di superare i limiti fisici delle trasmissioni terrestri e transoceaniche, anche in condizioni complesse come il fondo marino.
- **Innovazioni**: grazie alla tecnica del **multiplexing a lunghezza d'onda** (WDM), è possibile trasmettere simultaneamente più flussi di dati su diverse frequenze di luce all'interno dello stesso cavo in fibra ottica. Questo approccio sfrutta la scarsa selettività della fibra rispetto al colore della luce, permettendo a una singola fibra di trasportare diversi flussi di dati ad alta velocità, aumentando così la capacità totale di trasmissione senza necessità di nuovi cavi.

### Manutenzione e Sicurezza della Fibra Ottica

- **Giunzione e Allineamento**: le fibre ottiche devono essere giuntate con estrema precisione per evitare perdite di segnale e dispersione della luce, che potrebbero compromettere la qualità della trasmissione. Le giunzioni possono essere permanenti o temporanee, ma in entrambi i casi è fondamentale un allineamento perfetto tra i segmenti di fibra per garantire un'efficienza ottimale.
- **Problemi di Sicurezza nelle Lunghe Tratte**: nelle tratte di lunga distanza, specialmente nelle trasmissioni transoceaniche, emergono problemi di sicurezza e manutenzione. Le lunghe distanze e la difficoltà di accesso rendono complicato il monitoraggio e la protezione delle fibre da potenziali danni o manomissioni. Per garantire sicurezza e affidabilità, sono necessari sistemi di sorveglianza avanzati e misure di protezione che preservino l'integrità del segnale su queste distanze estese.