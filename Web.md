### Cosa è il Web?
- Definiamolo attraverso l’esperienza:
  - Come lo usiamo
  - Come funziona
  - Cosa fa

### Tecnologie Web
**Tecnologie e tool del corso**:
- Bootstrap
- JQuery
- Atom
- W3School
- HTTP, HTML, URI/URL, CSS, PHP, JS, JSON

### Definizione del Web (da Wikipedia)
- "Il World Wide Web (abbreviato WWW o Web) è uno spazio informativo dove documenti e altre risorse sono identificati da Uniform Resource Locators (URL), interconnessi tramite link ipertestuali e accessibili via Internet."
- Questa definizione deriva da un documento del W3C.
- La prima definizione di WWW risale alla prima pagina web pubblicata il 6 agosto 1991.

### Nascita del Web
- **6 agosto 1991**: Pubblicata la prima pagina web, considerata la data di nascita del WWW.
- Il progetto risale al **1989**.
- Fondamentali per il Web:
  - **Hypermedia**
  - **Accesso universale**
  - **Grande universo di documenti**

### Le 3 tecnologie fondamentali (1990)
- **HTML** (HyperText Markup Language): Formato per le pagine
- **URI** (Uniform Resource Identifier): Identificazione delle risorse
- **HTTP** (Hypertext Transfer Protocol): Interazione C/S sopra TCP
- Anche predisposti:
  - Un editor/browser: **WorldWideWeb.app**
  - Il primo server Web: **httpd**

### Principi Architetturali del WWW
- **Formato**: Accesso al contenuto chiaro e non ambiguo grazie a formati come HTML, PNG, RDF, ecc.
- **Identificazione**: Ogni risorsa è identificata da un URI (Uniform Resource Identifier).
- **Interazione**: Comunicazione tra client e server tramite HTTP (su TCP/IP).

### HTML
- Linguaggio di markup progettato per formattare documenti scientifici con struttura ipertestuale.
- **Markup**: Il contenuto del documento è delimitato da tag (< e >) che ne definiscono struttura e semantica.
- Evoluzione dal **1998** (W3C standard 5.3).

### CSS (Cascading Style Sheets)
- Linguaggio per gestire gli stili e separare la presentazione (CSS) dal contenuto (HTML).
- Supportato dai browser a partire da **IE3** (1996) e **Netscape Communicator 4** (1997).
- Ora siamo alla versione **CSS3**.

### Client e Server nel Web
- Basato su un modello **Client-Server** con protocollo HTTP:
  - **Client (Browser)**: Inizia l’interazione e visualizza documenti HTML.
  - **Server**: Risponde alle richieste del client e può connettersi ad applicazioni server-side.

### Browser
- Il browser è un visualizzatore di documenti ipertestuali e multimediali in HTML.
- Può agire come editor, ma solo localmente.
- Supporta plug-in per formati speciali e integra linguaggi di programmazione come **Javascript**.

### Server
- Il server risponde alle richieste di risorse (pagine, database, ecc.) individuate da un identificatore univoco.
- Funzione primaria: Rispondere alle richieste di pagine dai client.
- Può connettersi a **applicazioni server-side**.

### Statistiche Diffusione Server (Settembre 2023)
- **Top 1M siti**:
  - nginx
  - Apache
  - LiteSpeed

### Prima Domanda
- Nell’architettura del Web:
  1. Le applicazioni web sono eseguite solo sui server ❌
  2. Il client inizia sempre l’interazione con i server ✅
  3. I client possono visualizzare autonomamente tutti i formati ❌
  4. Il server inizia sempre l’interazione con i client ❌

### Evoluzione dell’Architettura del Web
- Il Web è evoluto per fornire:
  - Servizi avanzati agli utenti
  - Strumenti per gli sviluppatori
- Evoluzione su contenuti, dinamicità, sicurezza, distribuzione dei servizi, espressività dei linguaggi, ecc.

### HTTP: Modelli di Interazione
- **Pull**: Il client richiede i contenuti.
- **Push**: Il server invia contenuti non richiesti (webcasting, podcasting, streaming).
- **Polling**: Il client interroga periodicamente il server per nuovi contenuti (es. RSS).

### Cookies
- Blocchi di dati lasciati dal server al client per ristabilire la sessione in futuro.
- Utilizzati nella gestione delle sessioni.
- Ogni volta che il browser accede al server, invia i cookies per l'identificazione.

### Programmazione del Web
- Applicazioni Web:
  - **Client-side**: Eseguiti nel browser (Javascript).
  - **Server-side**: Eseguiti nel server (PHP).

### JavaScript
- Linguaggio di scripting orientato agli oggetti e agli eventi.
- Introdotto come **LiveScript** e rinominato **JavaScript**.
- Standardizzato da **ECMAScript** (ultima versione ECMA-262, 2022).
- Usato anche **server-side** nello stack MEAN.

### AJAX (Asynchronous JavaScript and XML)
- Tecnologia per applicazioni Web interattive.
- Aggiorna dinamicamente la pagina senza ricaricarla.
- Non necessariamente usa XML, spesso si utilizza **JSON**.

### Java Applet (Deprecate)
- Applicazioni Java incapsulate in pagine web, eseguite nel browser (obsolete dal 2018, rimosse da **Java SE 11**).

### Altri Oggetti Dinamici
- Browser plug-in come **Adobe Flash** e **MS Silverlight** sono stati usati per applicazioni interattive lato client.
- Ora in disuso con l’arrivo di **HTML5**.

### Flash
- YouTube ha sostituito il player Flash con HTML5 nel 2015.
- Supporto Flash disabilitato nei browser, rimosso da Chrome nel 2021.

### Framework di Sviluppo
- Librerie che semplificano l'uso di tecnologie Web.
  - **Server-side**: Facilitano la programmazione a tre livelli.
  - **Client-side**: Si basano su CSS e Javascript.

### Web Solution Stack
- Insieme di componenti software per creare una piattaforma completa:
  1. Sistema operativo
  2. Web server
  3. Database
  4. Linguaggio di programmazione

### LAMP Stack
- **LAMP**: Linux, Apache, MySQL, PHP (anche Perl e Python).
- Tutto open source.

### WAMP Stack
- Variante **Windows** di LAMP:
  - Windows, Apache, MySQL, PHP (anche Perl e Python).

### PHP
- Linguaggio di scripting per pagine web dinamiche lato server.
- Interprete PHP è open source.
- Originariamente **Personal Home Page**, ora **PHP: Hypertext Preprocessor**.

### Architettura PHP
- Il browser invia una richiesta HTTP al server che esegue il codice PHP e restituisce una risposta.

### PHP con JavaScript
- File PHP con codice JS embedded in HTML.
- Esecuzione del codice Javascript lato client.

### WISA
- Stack composto da prodotti Microsoft:
  - Windows, Internet Information Services (IIS), Microsoft SQL Server, ASP.NET.

### MEAN Stack
- Soluzione diversa rispetto a LAMP/WAMP:
  - **MongoDB** (NoSQL database)
  - **Express.js** (Framework server-side JS)
  - **AngularJS** (Framework client-side JS)
  - **Node.js** (Ambiente di esecuzione server-side JS)

### Confronto MEAN vs LAMP/WAMP
- **MEAN** è multipiattaforma, usa **Node.js** (JS lato server) e **MongoDB** (NoSQL), mentre LAMP/WAMP sono legati a sistemi operativi specifici e usano MySQL (DB relazionale).
- MEAN supporta programmazione client e server basata su JS.

### Tecnologie indispensabili
- **HTML5**: Per strutturare e definire il contenuto delle pagine.
- **CSS3**: Per definirne il layout.
- **JS**: Client-side.
- **PHP**: Server-side.

#### Markup
- Un linguaggio di **markup** è un linguaggio (con una specifica sintassi) che consente di annotare un documento fornendone una interpretazione delle sue parti.
- Il termine "markup" deriva dalla tipografia, dove si usava marcare con annotazioni le parti del testo da evidenziare o correggere.

#### Tipi di markup
- **Procedurale/Descrittivo:**
  - I linguaggi di markup **procedurali** indicano le procedure di trattamento del testo. Il markup specifica le istruzioni da eseguire per visualizzare una porzione di testo (es. TEX).
  - I linguaggi di markup **descrittivi** identificano strutturalmente il tipo di ogni elemento del contenuto. Esempi: HTML, XML, SGML.

#### Metamarkup e XML
- **Metamarkup** fornisce regole di interpretazione del markup, permettendo di definire nuovi linguaggi di markup.
- **XML (Extensible Markup Language):** Linguaggio progettato per lo scambio e la riusabilità di documenti strutturati su Internet.

#### XML e Document Publishing
- **Documenti strutturati:** XML è ideale per definire e esprimere documenti strutturati o semi-strutturati in modo indipendente dalla destinazione finale.
- Lo stesso documento XML può essere trasformato per diverse destinazioni (es. Web, smartphone).

#### XML e Data Management
- **Uso in W3C:** XML come mezzo per descrivere formati di dati per la comunicazione e memorizzazione (ad es. database basati su formati XML).
- Attuale tendenza: Uso di tecnologie come JSON e MongoDB.

#### Well-Formed vs Valid (XML)
- **Well-Formed:** Documenti conformi alle specifiche generiche XML.
- **Valid:** Documenti conformi a una DTD specifica.

#### Esempio di file XML valido e ben formattato
```xml
<?xml version="1.0" ?>
<!DOCTYPE tesi SYSTEM "tesi.dtd">
<tesi sessione='II'>
  <titolotesi>Linguaggi di Markup</titolotesi>
  <autore>Pinco Pallino</autore>
  <relatore>Paola Salomoni</relatore>
  <capitolo>
    <numero>1</numero>
    <titolo>Introduzione</titolo>
    <paragrafo>...</paragrafo>
  </capitolo>
</tesi>
```

#### Dal primo HTML a HTML5
- La prima versione di HTML viene proposta all'IETF nel 1995 (rfc1866, HTML 2.0).
- La standardizzazione di HTML è stata lenta e inadeguata per l'evoluzione rapida del web.

#### Mosaic e Netscape
- **Mosaic (1992):** Primo browser di successo, sviluppato dal NCSA.
- **Netscape Navigator (1994):** Browser che ottenne rapidamente successo e guidò lo sviluppo del web.

#### La prima guerra dei browser
- **Microsoft (1995):** Lancio di Internet Explorer (IE) per competere con Netscape.
- Entrambi i browser introdussero piccoli miglioramenti a HTML per migliorare l'esperienza utente.
- **Fine della guerra:** Microsoft vinse distribuendo IE con Windows 95. Netscape rilasciò il codice sorgente del suo browser in open-source, dando vita a Mozilla (Firefox).

#### Seconda guerra dei browser
- A partire dal 2004, nuovi browser open source come Firefox iniziarono a erodere la quota di mercato di IE.
- **Google Chrome (2008):** Da aprile 2016, è il browser più utilizzato al mondo.

#### W3C e la standardizzazione del Web
- Fondato da Tim Berners-Lee e Robert Cailliau, il W3C è responsabile dello sviluppo degli standard web più importanti (URI, HTTP, CSS, XML).
- W3C ha smesso di evolvere l'HTML e si è concentrato su linguaggi basati su XML, come XHTML.

#### WHAT WG e HTML5
- **2004:** Nasce il WHAT WG (Web Hypertext Application Technology) che si occupa di sviluppare HTML, CSS, DOM, e Javascript.
- **2007:** W3C riapre il gruppo di lavoro su HTML e collabora con WHAT WG per creare HTML5.
- **HTML5 (2014):** Pubblicazione della prima specifica di HTML5.

#### HTML, the Living Standard
- HTML5 è uno "standard vivente", costantemente aggiornato dal WHAT WG.
- Il processo di aggiornamento continuo è visto come un vantaggio piuttosto che un problema.

#### Prospettiva per lo sviluppo in HTML5
- Scrivere codice **ben formato** e **semantico**.
- Separare la presentazione dal contenuto, utilizzando CSS per gli aspetti grafici.
- Garantire che il codice sia **accessibile**.

#### Nuovi elementi di HTML5
- **Strutturazione del contenuto:** Elementi come `<article>`, `<section>`, `<header>`, e `<footer>` consentono di strutturare semanticamente il documento.
- **Accessibilità:** Introduzione di nuovi attributi e tecniche per migliorare l'accessibilità delle pagine web.

#### Elementi HTML5
- Ogni elemento HTML5 appartiene a una o più categorie:
  - **Metadata:** `<title>`, `<meta>`, `<base>`, `<link>`, `<style>`
  - **Flow:** La maggior parte degli elementi usati nel body del documento
  - **Sectioning:** Divisione del documento in sezioni con ruoli specifici
  - **Phrasing:** Testo del documento e suoi elementi interni
  - **Embedded:** Contenuti come audio, video, e grafici
  - **Interactive:** Elementi per l'interazione con l'utente (es. form)

#### Prima pagina HTML5 (esempio)
```html
<!DOCTYPE html>
<html>
<head>
  <title>Nome</title>
  <meta charset="UTF-8" />
</head>
<body>
  Content of the document...
</body>
</html>
```

#### Metadati in HTML5
- Elementi che descrivono il documento o il suo comportamento:
  - **<title>:** Titolo del documento
  - **<base>:** Path base del documento
  - **<link>:** Relazione con altri documenti (es. fogli di stile)
  - **<meta>:** Informazioni per i motori di ricerca

#### Codifica dei caratteri
- **ASCII:** Codifica a 7 bit, definita nel 1961, standardizzata ISO nel 1972.
- **ISO 8859/1 (Latin 1):** Standard a 8 bit per i caratteri latini.
- **Unicode e ISO/IEC 10646:** Standard per la codifica di alfabeti non latini. Utilizzano schemi di codifica a più byte (UCS-2 e UCS-4).

#### UCS e UTF
- **UTF-8:** Codifica a lunghezza variabile che consente di usare i caratteri di UCS senza consumare troppa memoria.
  
**Commenti**
- I commenti nel codice HTML sono inseriti tra `<!--` e `-->`.
- Esempio:  
  `<!-- Questo è un commento. I commenti non sono visualizzati dal browser -->`

**Elemento `<a>`**
- L'elemento `<a>` consente di inserire àncore, ovvero punti di partenza di un link.
- La destinazione si specifica con un URI attraverso l'attributo `href`.
- Nelle versioni precedenti di HTML, l'attributo `name` si usava per i punti di arrivo, ma è stato superato da `id` in HTML5.
 
**Esempio di utilizzo di `<a>`**
```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/news">News</a></li>
    <li><a href="http://www.google.it">Google</a></li>
    <li><a href="#articolo">Articolo</a></li>
  </ul>
</nav>

<article id="articolo">
  <p>Testo dell'articolo...</p>
</article>
```
 
**Risorsa**
- Una risorsa è qualsiasi struttura oggetto di scambio tra applicazioni nel Web.
- Le risorse possono essere:
  - In un file system relazionale
  - In un database
  - Il risultato dell’elaborazione di un’applicazione
  - Risorse non elettroniche o concetti astratti
 
**URI (Uniform Resource Identifier)**
- Gli URI identificano nomi e indirizzi di oggetti su Internet.
- Forniscono un meccanismo di accesso unificato alle risorse di dati.

**URI, URL e URN**
- URL (Uniform Resource Locator): contiene informazioni per accedere a una risorsa.
- URN (Uniform Resource Name): etichettatura permanente della risorsa.
  
**Sintassi degli URI**
- Gli URI sono divisi in diverse parti: schema, authority, path, query, fragment.
- Authority contiene userinfo, host e port.  
- Path rappresenta il percorso alla risorsa.  
- Query e fragment aggiungono ulteriori specificazioni.
 
**Esempio URI per FTP**
```ftp://[user[:password]@]host[:port]/path]```
- Accesso anonimo se manca l’utente.
- La porta di default è la 21.

**Caratteri ammessi negli URI**
- Caratteri non riservati: alfanumerici e punteggiatura specifica.
- Caratteri riservati: `%`, `/`, `.`, `#`, `?`, `+`, `*`, `!`.
  
**URI Reference**
- Un URI assoluto contiene tutte le parti necessarie.
- Un URI reference è un URI relativo che si riferisce a un URI di base.
 
**URI Shortener**
- Strumenti come bit.ly e goo.gl accorciano gli URL lunghi, utili per piattaforme come Twitter.
 
**Domanda 1:**  
Quale elemento è semanticamente corretto per il link `<a href="#primaparte">`?
- `<span id="primaparte">`
- `<a name="primaparte">`
- `<section id="primaparte">`
- `<br name="primaparte"/>`

**Struttura delle tabelle**
- Le tabelle HTML5 sono realizzate con l'elemento `<table>`, organizzate per righe `<tr>`.
- Celle di dati (`<td>`) e di intestazione (`<th>`).
- Esempi con intestazioni orizzontali e verticali, e utilizzo di `rowspan` e `colspan`.

**Esempio di tabella**
- Tabella con nome, email e telefono, ottimizzata per evitare ripetizioni tramite `rowspan`.


**Esempio con scope**
- Utilizzo dell’attributo `scope` per rendere le tabelle più accessibili.  
- Scope incolonna e scope per righe.
 
**Esempio reale**  
- Esempio di una tabella reale con thead, td, e div nidificati.
 
**Liste in HTML5**
- Tipi di liste: non ordinate (`<ul>`), ordinate (`<ol>`), e di definizioni (`<dl>`).
- Esempi di strutture di liste.
 
**Liste annidiate**  
- Esempio di liste annidiate.
 
### Elemento `<form>`
- **Attributo action**: specifica l'URL del server che riceverà i dati del form
- **Attributo method**:
    - **GET**: dati inviati come query string nell'URL (es. ?nome=valore&nome2=valore2)
    - **POST**: dati inviati nel corpo della richiesta HTTP, non visibili nell'URL

### Elementi comuni dei form e loro attributi
- **`<input>`**:
    - **Attributo type**: determina il tipo di input (text, password, radio, etc.)
    - **Attributo name**: identifica il campo nel form
    - **Attributo value**: valore predefinito del campo
- **`<textarea>`**:
    - **Attributi rows e cols**: per definire le dimensioni
- **`<select>` e `<option>`**:
    - **Attributo multiple**: per consentire selezioni multiple
    - **Attributo selected**: per l'opzione predefinita

### Tipi di `<input>` in dettaglio
- **text**: `<input type="text" name="nome" placeholder="Inserisci il tuo nome">`
- **password**: `<input type="password" name="pwd">`
- **radio**:
    ```html
    <input type="radio" name="genere" value="m"> Maschio
    <input type="radio" name="genere" value="f"> Femmina
    ```
- **checkbox**: `<input type="checkbox" name="interessi" value="sport"> Sport`
- **file**: `<input type="file" name="documento">`

### Nuovi tipi di input in HTML5
- **email**: `<input type="email" name="email">`
- **number**: `<input type="number" min="1" max="10" step="1">`
- **range**: `<input type="range" min="0" max="100">`
- **date**: `<input type="date">`
- **color**: `<input type="color">`

### Elementi per migliorare l'usabilità
- **`<datalist>`**:
    ```html
    <input list="browsers">
    <datalist id="browsers">
        <option value="Chrome">
        <option value="Firefox">
    </datalist>
    ```
- **`<fieldset>` e `<legend>`**:
    ```html
    <fieldset>
        <legend>Dati personali</legend>
        <!-- campi del form -->
    </fieldset>
    ```

### Accessibilità nelle form
- **Uso di `<label>`**:
    ```html
    <label for="nome">Nome:</label>
    <input type="text" id="nome" name="nome">
    ```
- **Attributi di accessibilità**:
    - **required**: campo obbligatorio
    - **autofocus**: focus automatico all'apertura della pagina
    - **autocomplete**: suggerimenti basati su input precedenti

### Validazione e elaborazione dei form
- **Validazione lato client** con attributi HTML5 (required, pattern, min, max)
- **Importanza della validazione lato server** per la sicurezza

### Best practices per la scrittura di codice HTML
- **Uso di DOCTYPE appropriato**: `<!DOCTYPE html>`
- **Corretta nidificazione degli elementi**
- **Uso di attributi semantici** come `role`

### Strumenti per la verifica del codice
- **Validator W3C**: controllo della sintassi HTML
- **AChecker**: verifica conformità alle linee guida di accessibilità

### Esempi pratici
- **Form di registrazione** con campi per nome, email, password
- **Tabella HTML accessibile** con uso corretto di `<th>`, `<td>`, e attributi `scope`

