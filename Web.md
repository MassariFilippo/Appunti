# Appunti Tecnologie WEB

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

### Markup
- Un linguaggio di **markup** è un linguaggio (con una specifica sintassi) che consente di annotare un documento fornendone una interpretazione delle sue parti.
- Il termine "markup" deriva dalla tipografia, dove si usava marcare con annotazioni le parti del testo da evidenziare o correggere.

### Tipi di markup
- **Procedurale/Descrittivo:**
  - I linguaggi di markup **procedurali** indicano le procedure di trattamento del testo. Il markup specifica le istruzioni da eseguire per visualizzare una porzione di testo (es. TEX).
  - I linguaggi di markup **descrittivi** identificano strutturalmente il tipo di ogni elemento del contenuto. Esempi: HTML, XML, SGML.

### Metamarkup e XML
- **Metamarkup** fornisce regole di interpretazione del markup, permettendo di definire nuovi linguaggi di markup.
- **XML (Extensible Markup Language):** Linguaggio progettato per lo scambio e la riusabilità di documenti strutturati su Internet.

### XML e Document Publishing
- **Documenti strutturati:** XML è ideale per definire e esprimere documenti strutturati o semi-strutturati in modo indipendente dalla destinazione finale.
- Lo stesso documento XML può essere trasformato per diverse destinazioni (es. Web, smartphone).

### XML e Data Management
- **Uso in W3C:** XML come mezzo per descrivere formati di dati per la comunicazione e memorizzazione (ad es. database basati su formati XML).
- Attuale tendenza: Uso di tecnologie come JSON e MongoDB.

### Well-Formed vs Valid (XML)
- **Well-Formed:** Documenti conformi alle specifiche generiche XML.
- **Valid:** Documenti conformi a una DTD specifica.

### Esempio di file XML valido e ben formattato
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

### Dal primo HTML a HTML5
- La prima versione di HTML viene proposta all'IETF nel 1995 (rfc1866, HTML 2.0).
- La standardizzazione di HTML è stata lenta e inadeguata per l'evoluzione rapida del web.

### Mosaic e Netscape
- **Mosaic (1992):** Primo browser di successo, sviluppato dal NCSA.
- **Netscape Navigator (1994):** Browser che ottenne rapidamente successo e guidò lo sviluppo del web.

### La prima guerra dei browser
- **Microsoft (1995):** Lancio di Internet Explorer (IE) per competere con Netscape.
- Entrambi i browser introdussero piccoli miglioramenti a HTML per migliorare l'esperienza utente.
- **Fine della guerra:** Microsoft vinse distribuendo IE con Windows 95. Netscape rilasciò il codice sorgente del suo browser in open-source, dando vita a Mozilla (Firefox).

### Seconda guerra dei browser
- A partire dal 2004, nuovi browser open source come Firefox iniziarono a erodere la quota di mercato di IE.
- **Google Chrome (2008):** Da aprile 2016, è il browser più utilizzato al mondo.

### W3C e la standardizzazione del Web
- Fondato da Tim Berners-Lee e Robert Cailliau, il W3C è responsabile dello sviluppo degli standard web più importanti (URI, HTTP, CSS, XML).
- W3C ha smesso di evolvere l'HTML e si è concentrato su linguaggi basati su XML, come XHTML.

### WHAT WG e HTML5
- **2004:** Nasce il WHAT WG (Web Hypertext Application Technology) che si occupa di sviluppare HTML, CSS, DOM, e Javascript.
- **2007:** W3C riapre il gruppo di lavoro su HTML e collabora con WHAT WG per creare HTML5.
- **HTML5 (2014):** Pubblicazione della prima specifica di HTML5.

### HTML, the Living Standard
- HTML5 è uno "standard vivente", costantemente aggiornato dal WHAT WG.
- Il processo di aggiornamento continuo è visto come un vantaggio piuttosto che un problema.

### Prospettiva per lo sviluppo in HTML5
- Scrivere codice **ben formato** e **semantico**.
- Separare la presentazione dal contenuto, utilizzando CSS per gli aspetti grafici.
- Garantire che il codice sia **accessibile**.

### Nuovi elementi di HTML5
- **Strutturazione del contenuto:** Elementi come `<article>`, `<section>`, `<header>`, e `<footer>` consentono di strutturare semanticamente il documento.
- **Accessibilità:** Introduzione di nuovi attributi e tecniche per migliorare l'accessibilità delle pagine web.

### Elementi HTML5
- Ogni elemento HTML5 appartiene a una o più categorie:
  - **Metadata:** `<title>`, `<meta>`, `<base>`, `<link>`, `<style>`
  - **Flow:** La maggior parte degli elementi usati nel body del documento
  - **Sectioning:** Divisione del documento in sezioni con ruoli specifici
  - **Phrasing:** Testo del documento e suoi elementi interni
  - **Embedded:** Contenuti come audio, video, e grafici
  - **Interactive:** Elementi per l'interazione con l'utente (es. form)

### Prima pagina HTML5 (esempio)
```html
<!DOCTYPE html>
<html>
<head>
  <title>Nome</title>  <!-- Unico obbligatorio, sancisce il nome che sarà presente nel tab del browser -->
  <meta charset="UTF-8" /> <!-- inserimento di metacaratteri in questo caso il tipo di char utilizzati -->
</head>
<body>
  Content of the document...
</body>
</html>
```

### Metadati in HTML5
- Elementi che descrivono il documento o il suo comportamento:
    - **`<title>`:** Titolo del documento, unico obbligatorio, utile per la search engine optimization (SEO).
        ```html
        <title>Il mio sito web</title> <!-- Titolo che appare nella scheda del browser e nei risultati di ricerca -->
        ```
    - **`<base>`:** Path base del documento.
        ```html
        <base href="https://www.example.com/"> <!-- Definisce l'URL base per tutti i link relativi nel documento, se per esempio avessimo avuto in href nome_file.css avrebbe voluto dire che quella risorsa si trova nella stessa cartella della pagina html -->
        ```
    - **`<link>`:** Relazione con altri documenti (es. molto usato per collegare fogli di stile).
        ```html
        <link rel="stylesheet" href="styles.css"> <!-- Collega un foglio di stile esterno al documento -->
        ```
    - **`<meta>`:** Informazioni per i motori di ricerca.
        ```html
        <meta name="description" content="Descrizione del contenuto della pagina"> <!-- Fornisce una descrizione della pagina per i motori di ricerca -->
        <meta charset="UTF-8"> <!-- Specifica la codifica dei caratteri del documento -->
        ```

### Codifica dei caratteri
- **ASCII:** Codifica a 7 bit, definita nel 1961, standardizzata ISO nel 1972.
- **ISO 8859/1 (Latin 1):** Standard a 8 bit per i caratteri latini.
- **Unicode e ISO/IEC 10646:** Standard per la codifica di alfabeti non latini. Utilizzano schemi di codifica a più byte (UCS-2 e UCS-4).

### UCS e UTF
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
**Elementi di blocco e Elementi in linea**

### Elementi di blocco
Gli elementi di blocco occupano l'intera larghezza disponibile del loro contenitore e iniziano su una nuova riga. Sono utilizzati per strutturare il layout della pagina.

### Esempi di elementi di blocco:
- `<div>`: Un contenitore generico per contenuti di blocco.
- `<p>`: Un paragrafo di testo.
- `<h1>` - `<h6>`: Intestazioni di vari livelli.
- `<ul>` e `<ol>`: Liste non ordinate e ordinate.
- `<li>`: Un elemento di lista.
- `<table>`: Una tabella.
- `<header>`, `<footer>`, `<section>`, `<article>`: Elementi semantici per la struttura della pagina.

```html
<div>
    <h1>Intestazione</h1>
    <p>Questo è un paragrafo di testo.</p>
</div>
```

### Elementi in linea
Gli elementi in linea occupano solo lo spazio necessario per il loro contenuto e non iniziano su una nuova riga. Sono utilizzati per stilizzare parti di testo all'interno di elementi di blocco.

### Esempi di elementi in linea:
- `<span>`: Un contenitore generico per contenuti in linea.
- `<a>`: Un collegamento ipertestuale.
- `<strong>`: Testo in grassetto.
- `<em>`: Testo in corsivo.
- `<img>`: Un'immagine.
- `<br>`: Un'interruzione di riga.
- `<code>`: Un frammento di codice.

```html
<p>Questo è un <strong>testo in grassetto</strong> e questo è un <em>testo in corsivo</em>.</p>
<p>Visita il nostro <a href="https://www.example.com">sito web</a> per maggiori informazioni.</p>
```

### Sectioning
Tali elementi dividono la pagina in parti semanticamente diberse assumono dunque un ruolo strutturale.
### `<article>`
- **Descrizione**: Rappresenta un contenuto autonomo e indipendente che potrebbe essere distribuito separatamente, come un articolo di giornale, un post di blog, un commento, o un widget.
- **Esempio**:
    ```html
    <article>
        <h2>Titolo dell'articolo</h2>
        <p>Contenuto dell'articolo...</p>
    </article>
    ```

### `<section>`
- **Descrizione**: Utilizzato per raggruppare contenuti tematicamente correlati, tipicamente con un'intestazione.
- **Esempio**:
    ```html
    <section>
        <h2>Sezione del sito</h2>
        <p>Contenuto della sezione...</p>
    </section>
    ```

### `<header>`
- **Descrizione**: Contiene l'intestazione di una sezione o di una pagina, spesso include titoli, sottotitoli, loghi, e strumenti di navigazione.
- **Esempio**:
    ```html
    <header>
        <h1>Intestazione del sito</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
            </ul>
        </nav>
    </header>
    ```

### `<footer>`
- **Descrizione**: Contiene il piè di pagina di una sezione o di una pagina, spesso include informazioni di contatto, copyright, e link a documenti correlati.
- **Esempio**:
    ```html
    <footer>
        <p>&copy; 2023 Il Mio Sito Web</p>
        <nav>
            <ul>
                <li><a href="#privacy">Privacy</a></li>
                <li><a href="#terms">Terms</a></li>
            </ul>
        </nav>
    </footer>
    ```

### `<nav>`
- **Descrizione**: Rappresenta una sezione della pagina destinata alla navigazione, contenente link a altre sezioni della stessa pagina o a pagine diverse.
- **Esempio**:
    ```html
    <nav>
        <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>
    ```

### `<aside>`
- **Descrizione**: Contiene contenuti tangenzialmente correlati al contenuto principale, come barre laterali, note a margine, o pubblicità.
- **Esempio**:
    ```html
    <aside>
        <h2>Barra Laterale</h2>
        <p>Contenuto della barra laterale...</p>
    </aside>
    ```

**Heading**
Tag per evidenziare i titoli indentati che vanno per livelli da 1 a 6

**Parsing**
Tag che rappresentano del testo.

### Esempio 1: Tag di Paragrafo
```html
<p>Questo è un paragrafo di testo.</p>
```

### Esempio 2: Tag di Line Break
```html
<p>Questa è una linea di un paragrafo di testo.<br/>
Questa è una linea di un paragrafo di testo.</p>
```

### Esempio 3: Tag di Enfasi
```html
<strong>Questo testo è in grassetto.</strong>
<em>Questo testo è in corsivo.</em>
```

### Esempio 4: Tag di Link
```html
<a href="https://www.example.com">Questo è un link</a>
```

### Esempio 5: Tag di Lista
```html
<ul>
    <li>Elemento della lista 1</li>
    <li>Elemento della lista 2</li>
</ul>
```

### Esempio 6: Tag di Immagine
```html
<img src="immagine.jpg" alt="Descrizione dell'immagine">
```

### Esempio 7: Tag di Divisione
```html
<div>
    <h2>Intestazione della sezione</h2>
    <p>Questo è un paragrafo all'interno di un div.</p>
</div>
```

### Esempio 8: Tag di Sezione Principale
```html
<main>
    <h1>Contenuto Principale</h1>
    <p>Questo è il contenuto principale della pagina.</p>
</main>
```

### Esempio 9: Tag di Span
```html
<p>Questo è un <span style="color: red;">testo evidenziato</span> all'interno di un paragrafo.</p>
```

### Esempio 10: Tag di Sub e Sup
```html
<p>Questo è un testo con un indice inferiore <sub>2</sub> e un esponente <sup>2</sup>.</p>
```

**Embedded e Fallback**

### Embedded e Fallback

L'elemento **embedded** in HTML5 permette di incorporare contenuti multimediali come immagini, audio, video, e altri oggetti direttamente nelle pagine web. Il **fallback** è una tecnica utilizzata per fornire contenuti alternativi nel caso in cui il browser non supporti il formato originale.

### Esempi di elementi embedded con fallback:

1. **Immagine (`<img>`)**
    ```html
    <!-- Figura con immagine e didascalia -->
    <figure>
        <!-- Immagine con testo alternativo per il fallback -->
        <img src="immagine.jpg" alt="Descrizione dell'immagine">
        <!-- alt, insieme ad src, è obbligatorio e riporta il testo sulla pagina in caso non fosse possibile caricare la foto, nel caso l'immagine fosse puramente decorativa alt si lascia vuoto per non appesantire il file -->
        <!-- longdesc specifica una descrizione lunga dell'immagine contenuta in un file txt esterno associato al file html, è deprecato ma ancora in uso in alcuni contesti -->
        <figcaption>Descrizione dell'immagine</figcaption>
    </figure>
    <!-- Il tag <figure> viene utilizzato per raggruppare l'immagine e la sua didascalia, migliorando la semantica e l'accessibilità del contenuto -->
    ```
    DA QUI ALLA FINE DELLE RISORSE MULTIMEDIALI NON HO SEGUTO LA REGISTRAZIONE PERCHE' ASSENTE

2. **Audio (`<audio>`)**
    ```html
    <!-- Audio con fallback per browser che non supportano l'elemento audio -->
    <audio controls>
      <source src="audio.mp3" type="audio/mpeg">
      <source src="audio.ogg" type="audio/ogg">
      Il tuo browser non supporta l'elemento audio.
    </audio>
    ```

3. **Video (`<video>`)**
    ```html
    <!-- Video con fallback per browser che non supportano l'elemento video -->
    <video controls>
      <source src="video.mp4" type="video/mp4">
      <source src="video.ogg" type="video/ogg">
      Il tuo browser non supporta l'elemento video.
    </video>
    ```

4. **Embed (`<embed>`)**
    ```html
    <!-- Embed di un file PDF con fallback -->
    <embed src="documento.pdf" type="application/pdf" width="600" height="400">
    ```

5. **Object (`<object>`)**
    ```html
    <!-- Object con fallback per browser che non supportano l'elemento object -->
    <object data="documento.pdf" type="application/pdf" width="600" height="400">
      <p>Il tuo browser non supporta l'elemento object. <a href="documento.pdf">Scarica il PDF</a>.</p>
    </object>
    ```

6. **Canvas (`<canvas>`)**
    ```html
    <!-- Canvas con fallback per browser che non supportano l'elemento canvas -->
    <canvas id="myCanvas" width="200" height="100">
      Il tuo browser non supporta l'elemento canvas.
    </canvas>
    <script>
      var canvas = document.getElementById('myCanvas');
      var context = canvas.getContext('2d');
      context.fillStyle = 'blue';
      context.fillRect(10, 10, 150, 75);
    </script>

**Elemento `<a>`**
  - Consente di inserire àncore nel documento, ovvero punti di partenza di un link.
  - La destinazione si specifica con un URI attraverso l’attributo `href`.
  - Nelle precedenti versioni di HTML, con `<a>` si realizzavano anche i punti di arrivo di un link (raggiungibili con `#` come frammento interno di un URI), usando l’attributo `name`. Questa soluzione in HTML5 è stata superata: al suo posto si usa l’attributo `id`, associandolo a qualunque elemento.

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
- Caratteri riservati:
  - **%**: Utilizzato per codificare caratteri speciali in un URI.
  - **/**: Separatore di directory o path in un URI.
  - **.**: Indica l'estensione di un file o separa i componenti di un nome di dominio.
  - **#**: Utilizzato per identificare un frammento all'interno di una risorsa.
  - **?**: Inizia la query string in un URI.
  - **+**: Rappresenta uno spazio in una query string codificata.
  - **\***: Carattere jolly utilizzato in vari contesti, come nei pattern di ricerca.
  - **!**: Utilizzato in vari contesti, come nei pattern di ricerca o nei linguaggi di programmazione.
    
**URI Reference**
- Un URI assoluto contiene tutte le parti necessarie.
- Un URI reference è un URI relativo che si riferisce a un URI di base.
 
**URI Shortener**
- Strumenti come bit.ly e goo.gl accorciano gli URL lunghi, utili per piattaforme come Twitter.

**Struttura delle tabelle**
- Le tabelle HTML5 sono realizzate con l'elemento `<table>`, organizzate per righe `<tr>`.
- Celle di dati (`<td>`) e di intestazione (`<th>`).
- Esempi con intestazioni orizzontali e verticali, e utilizzo di `rowspan` e `colspan`.

**Esempio di tabella**
- Tabella con nome, email e telefono, ottimizzata per evitare ripetizioni tramite `rowspan`.

**Esempio con scope**
- Utilizzo dell’attributo `scope` per rendere le tabelle più accessibili.  
- Scope incolonna e scope per righe.

```html
<table>
  <thead>
    <tr>
      <th>Nome</th>
      <th>Email</th>
      <th>Telefono</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Mario Rossi</td>
      <td>mario.rossi@example.com</td>
      <td>+39 123 456 7890</td>
    </tr>
    <tr>
      <td>Luigi Bianchi</td>
      <td>luigi.bianchi@example.com</td>
      <td>+39 098 765 4321</td>
    </tr>
    <tr>
      <td colspan="3">
        <div>
          <p>Informazioni aggiuntive:</p>
          <ul>
            <li>Mario è un cliente VIP.</li>
            <li>Luigi ha richiesto una chiamata di follow-up.</li>
          </ul>
        </div>
      </td>
    </tr>
  </tbody>
</table>
```
 
**Liste in HTML5**
- Tipi di liste:
  - **Non ordinate (`<ul>`)**: Utilizzate per elenchi di elementi senza un ordine specifico.
  - **Ordinate (`<ol>`)**: Utilizzate per elenchi di elementi con un ordine specifico.
  - **Di definizioni (`<dl>`)**: Utilizzate per elenchi di termini e le loro definizioni.

**Esempi di strutture di liste**

1. **Lista non ordinata**
    ```html
    <ul>
      <li>Elemento 1</li>
      <li>Elemento 2</li>
      <li>Elemento 3</li>
    </ul>
    ```

2. **Lista ordinata**
    ```html
    <ol>
      <li>Primo elemento</li>
      <li>Secondo elemento</li>
      <li>Terzo elemento</li>
    </ol>
    ```

3. **Lista di definizioni**
    ```html
    <dl>
      <dt>Termine 1</dt>
      <dd>Definizione del termine 1</dd>
      <dt>Termine 2</dt>
      <dd>Definizione del termine 2</dd>
    </dl>
    ```

**Liste annidiate**
- Esempio di liste annidiate:
    ```html
    <ul>
      <li>Elemento 1
        <ul>
          <li>Sotto-elemento 1.1</li>
          <li>Sotto-elemento 1.2</li>
        </ul>
      </li>
      <li>Elemento 2
        <ol>
          <li>Sotto-elemento 2.1</li>
          <li>Sotto-elemento 2.2</li>
        </ol>
      </li>
    </ul>
    ```
 
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

## WEB Design

### Web Design
1. **Concetti di base**: Il web design implica la pianificazione e creazione di un sito web. 
Il designer cura aspetti tecnici, grafici, e l'esperienza utente, incluse accessibilità e coinvolgimento.
2. **Elementi principali**: 
   - **Tipografia** (scelta dei font e codifica del testo),
   - **Colore** (schemi e codifica RGB, psicologia dei colori),
   - **Layout** (disposizione degli elementi),
   - **Responsive e Mobile First** (priorità al design per dispositivi mobili).

### Tipografia
- **Glifi e Font**: Un font è un insieme di glifi con caratteristiche grafiche simili. 
Esistono font **serif** (con grazie) e **sans-serif** (senza grazie), con ulteriori varianti di peso e inclinazione.
- **Famiglie di Font**: Comprendono vari stili di un carattere, distinguibili per 
peso (es. bold), inclinazione (italic), e presenza di grazie.

### Colori
- **Schema di Colori**: Codificati in RGB per il web. Gli schemi includono monocromatico, analoghi e complementari (incluso schema triadico e tetradico).
- **Codifica esadecimale**: Colori rappresentati da una terna di valori (es. #000000 per nero).
- **Color Wheel**: Utilizzata per creare combinazioni armoniche; include colori primari (rosso, verde, blu) e secondari.

### Accessibilità e Daltonismo
- **Accessibilità cromatica**: Importante per inclusività, tenendo conto dei vari tipi di daltonismo (protanopia, deuteranopia, tritanopia).

### Layout di Pagina e Mobile First
- **Mobile First**: Si basa sul principio del *progressive enhancement*, progettando prima per dispositivi mobili, successivamente adattando ai desktop.
- **Graceful Degradation**: Al contrario, parte da layout per desktop adattandoli poi per il mobile, ma oggi è meno utilizzato rispetto al *mobile first*.

## Usabilità

### **Introduzione a User Experience (UX) e Usabilità**
   - **Human-Computer Interaction (HCI)**: integra aspetti ergonomici e psicologici per facilitare l'uso delle tecnologie.
   - **Obiettivi del Corso**: Definire concetti principali e individuare le best practices per la creazione di siti e servizi usabili.

### **Concetto di Usabilità**
   - Origina dagli anni '60 nell'ergonomia delle interazioni uomo-artefatto.
   - **ISO 9241** definisce l'usabilità come la capacità di un prodotto di consentire agli utenti di raggiungere obiettivi con efficacia, efficienza e soddisfazione.
   - Importanza del modello mentale dell'utente, che deve allinearsi a quello progettuale (user vs. design model).

### **Verso la User Experience (UX)**
   - **Evoluzione dell'usabilità**: da necessità tecnica per esperti a requisito per l'uso quotidiano.
   - **Donald Norman** nel 1988 introduce il concetto di UX, andando oltre la pura funzionalità.
   - **Dimensioni della UX**:
     - **Pragmatica**: funzionalità e usabilità.
     - **Estetica/Edonica**: piacere visivo ed emotivo.
     - **Simbolica**: aspetti sociali e di identità.

### **Differenze tra Usabilità e UX**
   - **Metafora**: una superstrada è usabile (funzionale e semplice), mentre una strada di montagna offre un’esperienza più emozionante ma meno semplice.
   - L'usabilità si concentra sull’efficacia e semplicità, la UX include anche emozioni e aspetti esperienziali.

### **Processi di UX Design**
   - **Ciclo di Design UX**:
     - **Studio** delle necessità utente,
     - **Design** dell'interfaccia e del sistema,
     - **Valutazione** tramite prototipi e redesign.
   - **Tecniche di UX**:
     - **Personas e Scenarios**: descrizioni dettagliate di utenti tipo e situazioni d’uso.
     - **Experience Prototypes**: test prima dello sviluppo.
     - **Mock-up**: rappresentazioni visive dell’interfaccia per test senza sviluppo effettivo.

### **Strumenti di UX Design**
   - **Mock-up Software**: strumenti come Balsamiq Mockup (disponibile per il corso) e Figma.
   - **UX Prototyping**: simula l'interazione utente per valutare le reazioni prima dello sviluppo completo.

### **Focus Group e Test con gli Utenti**
   - **Focus Group**: raccolgono opinioni su prototipi con gruppi di utenti (8-12 partecipanti).
   - **Obiettivi**: esplorare vantaggi/svantaggi di proposte e definire il target utente; si differenziano dai test perché analizzano ciò che gli utenti dicono, non come effettivamente operano.

### **Esempi Pratici di Applicazione**
   - **Caso myUnibo**: app per studenti Unibo, con servizi come gestione libretto, orari, esami e miglioramenti suggeriti (es. accesso a risorse e informazioni in tempo reale).
   - **Sviluppo di Personas**: creazione di personaggi tipo, come “Martina”, studentessa che usa l’app per gestire la carriera universitaria e partecipare alla vita accademica.

### **Conclusioni sulla UX**
   - La UX rappresenta un approccio centrato sull’utente e sul contesto d’uso, fondamentale per creare applicazioni funzionali ed emozionanti.
   - L'importanza di iterare continuamente il processo di design per ottenere il miglior compromesso tra usabilità ed esperienza complessiva dell’utente.

## Uso colore

Sistemi Multimediali AA 2015/16 1 1
Colore
Lezione due
Sistemi Multimediali AA 2015/16
2
Luce
• Con luce si indica quella parte dello
spettro elettromagnetico visibile
dall'occhio umano, compresa,
all’incirca tra 400 e 700 nanometri
di lunghezza d'onda, ovvero tra 750
e 428 THz di frequenza.
• L'occhio umano ha limiti nella
visione della luce, ovvero consente
di percepire la radiazione
elettromagnetica compresa tra
violetto e rosso
2
Sistemi Multimediali AA 2015/16 3
3
Colori dello spettro
• I colori dello spettro e le relative
lunghezze d’onda sono: – Violetto 380–450 nm – Blu 450–495 nm – Verde 495–570 nm – Giallo 570–590 nm – Arancione 590–620 nm – Rosso 620–750 nm
• La massima sensibilità dell'occhio
la si ha attorno ai 555 nm (540
THz), in corrispondenza del colore
verde.
Sistemi Multimediali AA 2015/16
4
Higher energy
…
Sistemi Multimediali AA 2015/16
5
Occhio e rètina
• La rètina è la membrana più interna
dell'occhio ed è composta da cellule
sensibili alle radiazioni luminose
(fotorecettori). Attraverso il nervo ottico
invia al cervello le informazioni visive da
interpretare.
• Tra le cellule che compongono la retina
esistono due tipi di fotorecettori:
– i coni, responsabili della visione a colori
ma sensibili solo a luci piuttosto intense;
– i bastoncelli, che sono particolarmente
sensibili a basse intensità di luce ma non
ai colori.
5
Sistemi Multimediali AA 2015/16 6
6
Coni
• I coni si suddividono in tre differenti tipologie
responsabili della visione di tre colori primari
(Red-Green-Blue, Rosso-Verde-Blu): – i coni S (short) presentano il
massimo assorbimento alle
lunghezze d'onda del blu; – i coni M (medium), sono
sensibili alle lunghezze
d'onda del verde; – I coni L (long) sono sensibili
alle lunghezze d'onda del rosso.
• Insieme compongono il mosaico retinico.
Sistemi Multimediali AA 2015/16
7
7
Coni
• I coni operano soprattutto in
condizione di luce piena, mentre i
bastoncelli permettono la visione
anche quando la luce è scarsa. I
coni sono presenti maggiormente
in una zona centrale della retina
detta fòvea.
• Questa differente densità di
fotorecettori è responsabile della
visione nitida nel punto di
fissazione e della visione sfumata e
poco definita nella zona periferica
del campo visivo.
Sistemi Multimediali AA 2015/16 8
8
Percezione della luce
• Anche per i bastoncelli è possibile definire una curva di
sensibilità, traslata rispetto a quella dei coni e più ampia.
• I bastoncelli sono molto
più sensibili (rispetto ai
coni) e reagiscono
un insieme ampio di
lunghezze d’onda,
ma producono un
impulso nervoso "in
bianco e nero"
(nell’accezione televisiva
del termine).
Sistemi Multimediali AA 2015/16 9
9
Percezione del colore
• La fisiologia dei coni e dei bastoncelli non spiega in modo
esaustivo la percezione del colore. Per spiegare in modo
più completo come viene percepito il colore occorre
considerare: – Come il segnale è recepito nel suo complesso e
trasmesso dalla retina al cervello attraverso il nervo
ottico. – Come questo è elaborato dal cervello e, ovviamente,
in questa fase intervengono aspetti di tipo psicologico.
• Accanto ai meccanismi di compressione del segnale, sono
stati ipotizzati e sperimentati (ma non del tutto ancora
verificati) meccanismi percettivi di codifica dei segnali
opponenti.
Sistemi Multimediali AA 2015/16 10
Segnali opponenti
• Esiste un livello di elaborazione successivo (non completamente
spiegato dal punto di vista fisiologico) che trasforma i tre segnali
provenienti dai coni in: – un canale specializzato nella visione alternativa del giallo e
del blu. Quando l'eccitazione combinata dei tre tipi di coni
produce la visione del blu, è inibita la visione del giallo, e
viceversa; – un canale specializzato nella visione alternativa del rosso e
del verde. Quando l'eccitazione combinata dei tre tipi di coni
produce la visione del rosso, è inibita la visione del verde e
viceversa; – un canale specializzato nella visione della componente di
bianco o di nero. Questo canale non è basato su meccanismi
antagonisti, come i due precedenti, ma sul presupposto di
un'eguale stimolazione dei tre tipi di coni.
10
Sistemi Multimediali AA 2015/16 11 11
Segnali opponenti
Sistemi Multimediali AA 2015/16 12
Segnali opponenti
• Il modello a segnali opponenti spiega: – l'esistenza di due coppie di colori complementari, giallo col blu, e rosso col verde – Il fatto che i colori che formano ciascuna
coppia non possano essere visti
simultaneamente nello stesso posto; – lo status del giallo, che sembra godere di
proprietà analoghe a quelle dei colori
primari rosso, verde e blu; – l'esistenza di colori “puri”, che vengono
percepiti come non contaminati da
sfumature di nessun altro colore (blu,
giallo, verde e rosso). – la visione di colori consecutivi.
12
Sistemi Multimediali AA 2015/16 13
Daltonismo
• Col termine daltonismo si intende la cecità ai colori, ovvero
l'inabilità a percepire (del tutto o in parte) i colori.
• Prende il nome dal chimico inglese John Dalton che pubblicò (nel
1794) un articolo intitolato "Extraordinary facts relating to the
vision of colors" scritto dopo essersi reso conto della propria cecità
cromatica.
• E’ una condizione prevalentemente di origine genetica: – Circa l’8% della popolazione maschile è daltonico. – Lo 0,4% della popolazione femminile è daltonico.
13
Sistemi Multimediali AA 2015/16 14
Daltonismo
• Col termine daltonismo si intende la cecità
ai colori, ovvero l'inabilità a percepire (del
tutto o in parte) i colori.
• Prende il nome dal chimico inglese John
Dalton che pubblicò (nel 1794) un articolo
intitolato "Extraordinary facts relating to
the vision of colors" scritto dopo essersi
reso conto della propria cecità cromatica.
• La cecità ai colori può essere totale
(acromasia o acromatopsia) oppure parziale
(discromatopsia o di dicromatismo)
14
Sistemi Multimediali AA 2015/16 15
Tipi di daltonismo
PROTANOPIA
VISIONE
NORMALE DEUTERANOPIA TRITANOPIA
Sistemi Multimediali AA 2015/16 16
Visione tetracromatica
• Secondo studi recenti, sembrerebbe che alcune donne
abbiano sviluppato la presenza di una quarta tipologia di
cono, ovvero potessero contare su una visione
tetracromatica.
• Dagli studi effettuati non tutti gli individui con 4 tipi di
coni sarebbero in grado di avere una effettiva percezione
tetracromatica, ma è stata individuata almeno una donna
in grado di vedere effettivamente attraverso 4 tipi di
recettore (https://research.ncl.ac.uk/tetrachromacy/)
Sistemi Multimediali AA 2015/16 17
Colore
• La percezione del colore si realizza con la consapevolezza
dell’osservatore e il riconoscimento del colore, per
associazione con un termine che identifica la classe di tutti
gli oggetti di quel colore o di un colore somigliante.
• Non esistono, ad oggi, risposte esaustive ai processi
psicologici che governano la nostra capacità di analisi e
sintesi successive alla percezione dei colori,
ma esistono alcuni fenomeni
noti che caratterizzano questo
tipo di percezione.
17
Sistemi Multimediali AA 2015/16 18
Contesto
• Il contesto in cui uno colore
viene presentato ne guida
l’interpretazione percettiva.
– I due quadrati marroni, sono
esattamente dello stesso colore.
– I due quadrati azzurri sono
esattamente delle stesse
dimensioni
18
Sistemi Multimediali AA 2015/16 19
Metamerismo
• Metamerismo è la condizione percettiva (non
patologica) in cui due oggetti appaiono di colore identico
se posti in un medesimo contesto(tipicamente di
illuminazione) e, invece, di colore diverso se in un
successivo diverso contesto
19
Sistemi Multimediali AA 2015/16 20
20
Qualità percettiva
• Nella percezione del colore vengono
considerati molte caratteristiche, le tre
principali sono: – Tonalità
Brillantezza (e luminosità) – Saturazione
Sistemi Multimediali AA 2015/16 21
Tonalità
• Tonalità (hue) o tinta è un colore "puro",
ovvero caratterizzato da una singola lunghezza
d'onda all'interno dello spettro visibile della
luce.
• Nell'esperienza comune la tonalità è la qualità
percettiva che fa attribuire un nome piuttosto
che un altro ad un certo colore.
21
Sistemi Multimediali AA 2015/16 22
Brillantezza e luminosità
• Brillantezza (brightness) o brillanza è la quantità totale di
luce che una sorgente luminosa appare emettere (o che
appare riflessa da una superficie).
• La luminosità (lightness o value) è la quantità di luce
proveniente da un oggetto, a paragone della quantità di
luce proveniente da una superficie bianca sottoposta alla
medesima illuminazione (valutazione contestuale).
22
Sistemi Multimediali AA 2015/16 23
Saturazione
• La saturazione (saturation) o purezza è
l'intensità di una specifica tonalità.
• Una tinta molto satura ha un colore vivido e
squillante; al diminuire della saturazione, il
colore diventa più debole e tende al grigio.
• Se la saturazione viene azzerata il colore si
trasforma in una tonalità di grigio.
23
Sistemi Multimediali AA 2015/16 24
24
Sintesi additiva
• La mescolanza additiva di stimoli di colore
(detta anche sintesi o mescolanze additiva) è
la mescolanza di stimoli di colore che: – arrivano all'occhio invariati, – entrano nell'occhio simultaneamente o in rapida
successione, – incidono sulla stessa area di retina, anche in forma
di mosaico.
Sistemi Multimediali AA 2015/16 25
Sintesi additiva: esempio
• Un esempio classico è quello di due fasci di luce
colorata (rossa e verde) proiettati sulla parete bianca
di una stanza buia in modo che ci sia un’area di
sovrappossizione.
25
Sistemi Multimediali AA 2015/16 26
Sintesi o mescolanza additiva
• L’effetto che si ottiene è che i due stimoli luminosi (luce
rossa e luce verde) vengono riflessi dalla parete e
giungono simultaneamente e immutati all'occhio, dove
incidono sulla stessa area di retina.
• Dal punto di vista fisico non avviene alcuna interferenza
tra i due fasci luminosi ma il sistema visivo percepisce il
colore risultante dalla mescolanza dei due stimoli come
giallo.
• Il giallo è, in questo caso, un
colore prodotto dalla mescolanza
additiva del rosso e del verde.
Sistemi Multimediali AA 2015/16 27
Mescolanza additiva
• Si parla di mescolanza additiva in media spaziale o
temporale quando la sovrapposizione degli stimoli
luminosi monocromatici è approssimata nel tempo
o nello spazio. – I punti (o pixel) di un monitor
sono l’esempio classico di
mescolanza in media spaziale. – Il disco di Newton è un
esempio di media temporale.
•
27
Sistemi Multimediali AA 2015/16 28
28
Sintesi o mescolanza additiva
Sistemi Multimediali AA 2015/16 29
29
Sistemi sottrattivi
• Nel caso della mescolanza additiva si considera la luce
emessa da una sorgente per irraggiamento (come nel
caso di una lampadina, del sole, di un semaforo, ecc..) o
riflessione (come nel caso di qualsiasi oggetto che non
emette luce propria).
• Se consideriamo invece la luce assorbita, Possiamo dire
che il colore di un oggetto è il risultato di una sottrazione
di lunghezze d’onda che sono assorbite dall’oggetto.
Ovviamente questo è equivalente a considerare il
risultato delle lunghezze d’onda riflesse, mescolate
additivamente.
Sistemi Multimediali AA 2015/16 30
Sistemi sottrattivi
• Assumendolo illuminato da luce bianca,
contenente tutte le lunghezze d’onda visibili,
un oggetto ci appare nero poiché,
approssimativamente, le assorbe tutte; un
oggetto giallo assorbe tutte le lunghezze
d’onda del blu, riflettendo il rosso e il
verde, e così via.
• Queste considerazioni conducono ad
affermare che ogni colore percepibile
può essere ricondotto alla sottrazione,
opportunamente modulata, di una terna di
stimoli.
Sistemi Multimediali AA 2015/16 31
31
Sintesi o mescolanza sottrattiva
• Dunque: – la mescolanza di colori additiva se avviene nell'occhio
(a causa di meccanismi percettivi). – la mescolanza sottrattiva avviene prima di raggiungere
l'occhio (a causa di meccanismi fisici).
• L’esempio classico è
quello degli inchiostri delle
stampanti (per esempio giallo
e ciano) che si mescolano
sulla carta per formare il
verde.
Sistemi Multimediali AA 2015/16 32
32
Sintesi o mescolanza sottrattiva
Sistemi Multimediali AA 2015/16 33
Colori primari
• I singoli colori che, quando sovrapposti o
mescolati in media spaziale o temporale,
producono la percezione di un ulteriore
colore, sono detti colori primari.
• Il numero assoluto dei colori primari è
potenzialmente infinito. Tuttavia, poiché i
coni sono di 3 tipi e sono rispettivamente
sensibili al rosso, al verde e al blu, questi tre
colori sono generalmente indicati come
colori primari per la sintesi additiva.
• I primari additivi sono quindi rosso (red),
verde (green) e blu (blue).
Sistemi Multimediali AA 2015/16 34
34
Colori primari
• Anche in mescolanza sottrattiva si può: – Limitare il numero dei colori primari a 3 – Scegliere i primari per produrre il
maggior numero possibile di colori.
• Con questi obiettivi sono usati come
primari in sintesi sottrattiva ciano (cyan),
magenta (magenta) e giallo (yellow) sono
usati tipicamente come primari nella
mescolanza sottrativa.
• Notare che essendo una mescolanza fisica
di sostanze, non è così semplice usare solo
colori primari
Sistemi Multimediali AA 2015/16 35
35
Colore digitale
• Con rappresentazione digitale del colore, si
intende la codifica delle proprietà relative al colore
in termini numerici.
• Questo tipo di rappresentazione è utilizzata tutti i
sistemi digitali forniscono o acquisiscono
informazioni di tipo visivo: personal computer, le
stampanti, i telefoni cellulari, tablet, le fotocamere
o telecamere digitali, e i televisori (delle ultime
generazioni).
Sistemi Multimediali AA 2015/16 36
Colore digitale
• La corrispondenza tra colore e numeri può essere realizzata
1,2 o 3 coordinate: – Lineare: è assegnato un codice a ogni colore – Bidimensionale: i colori sono organizzati
su un piano e riferiti con coppie di
numeri – Tridimensionale: i colori sono organizzati
nello spazio e riferiti con terne di numeri
Sistemi Multimediali AA 2015/16 37
Pantone: codifica bidimensionale
• Il sistema Pantone è stato ideato negli anni cinquanta
per poter catalogare i colori e associarli ad una codifica
per la stampa.
• ogni codice Pantone è composto da due campi,
entrambi definiti in modo arbitrario: – nel primo campo può essere presente una parola (es. RED) o
un numero di due cifre che si riferisce alla famiglia di
appartenenza (es. 18 per la famiglia dei Rossi). – Il secondo campo indica quello specifico tipo di colore nella
classe specificata
Sistemi Multimediali AA 2015/16 38
Pantone color of the year
• Ogni anno, a partire dal 2000, Pantone ha scelto un
colore come colore dell’anno.
• Quest’anno i colori Pantone sono due:
Sistemi Multimediali AA 2015/16 39
39
Colore digitale
• Sono, in generale, possibili, conversioni: – dei segnali luminosi in segnali elettrici, come accade
nelle macchine fotografiche digitali o negli scanner. – dei segnali elettrici in operazioni meccaniche come
accade nelle stampanti. – dei segnali elettrici in segnali luminosi come accade
nei monitor dei computer, nei display dei dispositivi
mobili e nei televisori.
• In questi casi, la codifica è tridimensionale,
basata o su sintesi additiva o sottrattiva
Sistemi Multimediali AA 2015/16 40
40
Spazi colorimetrici
• Gli spazi colorimetrici digitali fanno riferimento ai due
sistemi di sintesi che conosciamo: – Sintesi additiva: per esempio, il monitor funziona sulla
base della sintesi additiva, poiché ogni pixel dello schermo
è in realtà costituito di tre piccolissimi punti, uno rosso,
uno verde e uno blu, così vicini da essere percepiti come
un unico colore all’interno dell’occhio – Sintesi sottrattiva: per esempio le stampanti a getto
d’inchiostro operano spruzzando un punto della carta con
più colori diversi, che sulla superficie bianca si
amalgamano in sintesi sottrattiva, formando un colore per
mescolanza.
Sistemi Multimediali AA 2015/16 41
41
RGB
• Lo spazio colorimetrico RGB descrive la corrispondenza
tra colori e terne di numeri compresi tra 0 e 255
• Ogni terna è la codifica numerica di tre colori primari,
detti componenti RGB del colore: – il rosso (red), – il verde (green), – e il blu (blue).
• Sulla base di questo effetto, monitor e
televisori producono il colore di ogni singolo
punto dello schermo, sfruttando la mescolanza additiva in media spaziale di tre
emettitori monocromatici contigui,
uno per il rosso, uno per il verde e uno per il blu.
Sistemi Multimediali AA 2015/16 42
RGB: esempio
• Per esempio questo colore è codificato
dalla terna (80,200,130) in cui: – 80 è la componente rossa, – 200 è la componente verde, – 130 è la componente blu.
Sistemi Multimediali AA 2015/16 43
Altri spazi additivi
• RGB è definito in base a criteri
percettivi ma non tiene conto
dell’uso dei colori da parte
dell’utente e rende complesse
attività.
• Per esempio: – per schiarire un colore occorre aggiungere la stessa quantità
a tutte e tre le componenti RGB, – per rendere più scuro un colore occorre togliere lo stesso
valore a tutte e tre le componenti.
• Per questo sono stati studiati altri spazi additivi, più
adatti in fase di selezione dei colori, tra i quali vediamo
HSL e HSV.
Sistemi Multimediali AA 2015/16 44
HSL
• HSL è un modello additivo cilindrico,
orientato ad una prospettiva
percettiva che considera un colore in
termini di tinta, sfumatura e tono.
• Il colore è definito da:
– H (tonalità, hue), viene misurata da un
angolo intorno all'asse verticale, con il
rosso a 0°, il verde a 120° e il blu a 240°
– S (saturazione, saturation): va da zero,
sull'asse del modello, a una sua
superficie.
– L (luminosità, lightness): 0 rappresenta
il nero, 1 rappresenta il bianco
Sistemi Multimediali AA 2015/16 45
HSV
• HSV è un modello additivo, simile a
HSL, che sostituisce la componente L
con un valore (V, value), con lo scopo
di avere colori puri in corrispondenza
del valore 1.
• Si utilizza sia una rappresentazione
cilindrica che conica.
Sistemi Multimediali AA 2015/16 46
46
Altri spazi additivi: YUV
• Un ulteriore spazio colorimetrico additivo, alternativo
rispetto ad RGB è YUV (indicato a volte come Y’UV), nato
in seguito agli studi effettuati per la realizzazione dei primi
televisori a colori.
• Per mantenere compatibilità con le trasmissioni in B/N e
contemporaneamente ridurre la quantità di informazioni
(a livello elettronico, di segnali trasmessi, elaborati
e ricevuti), fu studiato un sistema che codifica il
colore nelle sue componenti di: – luminanza (indicata con Y e definito
anche Luma) e – crominanza o cromaticità (codificata
dalla coppia U, V).
Sistemi Multimediali AA 2015/16 47
YUV
• In particolare, Y codifica la luminosità (e non il colore) del
colore, mentre U e V sono, rispettivamente, le codifiche di B–
Y (Blue – luma) ed R–Y (Red – luma).
• Questa codifica: – è funzionale al mantenimento della compatibilità con i
segnali in B/N, che utilizzano in sostanza solo il segnale Y; – è funzionale alla riduzione della quantità di informazioni
mediante compressione, poiché la componente di
luminanza Y (percettivamente più importante) può essere
mantenuta per intero applicando riduzioni alle
informazioni contenute nelle componenti di crominanza.
47
Sistemi Multimediali AA 2015/16 48
48
Spazi sottrattivi: CMY
• Oltre agli spazi colorimetrici digitali additivi, esistono anche
spazi sottrattivi, utilizzati prevalentemente per la stampa. In
questo contesto infatti, la colorazione avviene per sintesi
sottrattiva, attraverso la combinazione di inchiostri che
formano colori sulla carta per mescolanza delle componenti
primarie.
• Il più semplice spazio colorimetrico digitale sottrattivo è CMY,
uno spazio in tricromia basato sui tradizionali colori primari
usati per la sintesi sottrattiva. In questo caso ogni terna è la
codifica numerica di tre colori primari con valori da 0 a 255: – il ciano (cyan), – il magenta (magenta), – e il giallo (yellow).
Sistemi Multimediali AA 2015/16 49
Spazi sottrattivi: CMYK
• In generale l’efficacia della sintesi
sottrattiva dipende da principi fisici/chimici
di mescolanza tra sostanze.
• In particolare la composizione del nero
nella sintesi sottrattiva (che corrisponde
alla contemporanea presenza di tutti i
pigmenti dei colori primari ) non è
soddisfacente dal punto di vista tipografico.
• Per questa ragione si fa uso di un ulteriore
spazio colorimetrico sottrattivo,
denominato CMYK, che utilizza codifiche
dei colori ciano, magenta, giallo e del nero
e viene, per questo, indicato anche come
spazio colorimetrico in quadricromia.
49
Sistemi Multimediali AA 2015/16 50
Conversione
• Ovviamente esistono algoritmi di conversione da
un sistema all’altro.
• Per esempio per passare da RGB a CMG, le
formule sono: – C = 1 - ( R / 255 ) – M = 1 - ( G / 255 ) – Y = 1 - ( B / 255 )
• Viceversa per passare da CMG a RGB si usano: – R = ( 1 - C ) * 255 – G = ( 1 - M ) * 255 – B = ( 1 - Y ) * 255
Sistemi Multimediali AA 2015/16 51
Quanti colori?
• Le codifiche a base tre sono basate sull’uso
di 3 byte per codificare ciascun colore
(complessivamente ogni sistema codifica
potenzialmente 224 colori, ovvero
16.777.216 colori). Questa situazione è
indicata come Truecolor.
• Alcuni formati/sistemi sono basati su
numero inferiore di colori, tipicamente
codificato da un solo byte. Questi sistemi
definiscono una palette, ovvero un
insieme prefissato di colori truecolor a cui
sono associati i numeri da 0 a 255 usati per
la codifica.
Sistemi Multimediali AA 2015/16 52
Quanti colori
• Verso la fine degli anni novanta furono messi a
punto sistemi in grado di visualizzare più di 8
bit per canale (12 o 16).
• In realtà sembra che 10 bit per canale siano
sufficienti per raggiungere i limiti assoluti della
vista umana in quasi tutte le circostanze.
• Quindi, in molti ambiti, i sistemi con più di 8 bit
sono stati abbandonati. Restano in voga in
alcuni contesti (per esempio gli scanner) in cui
esistono apparati in grado di riconoscere più di
8 bit per canale (solitamente 10, a volte 12).
• La scelta del numero di colori rappresenta una
forma di quantizzazione.
Sistemi Multimediali AA 2015/16 53
53
Contrasto
• Per assicurare che il testo (scritto con il colore di
primo piano, o foreground) sia leggibile su uno
sfondo colorato (background), occorre verificare
che tra i due colori ci sia sufficiente contrasto.
• Esistono due diversi tipi di contrasto: – il contrasto cromatico, prodotto dal
diverso chroma dei colori, – il contrasto nella luminosità, prodotto
dalla diversa brightness dei colori.
• L’esistenza di un contrasto sufficiente è
fondamentale per gli utenti che hanno difficoltà
visive e in particolare il contrasto della luminosità
è necessario agli utenti che hanno forme di
daltonismo
Sistemi Multimediali AA 2015/16 54
Gestione digitale del colore
• L’esistenza di sistemi di codifica non garantisce che il colore
digitale sia «fedele». Se provate a scattare una fotografia e
a riprodurla su diversi dispositivi vi accorgerete che la
riproduzione è probabilmente diversa dall’originale.
• La gestione del colore (color management) consiste nel
mantenere il colore uguale su periferiche diverse (non va
confuso col fotoritocco).
Sistemi Multimediali AA 2015/16 55
Di che colore è il vestito?
• Avrete forse seguito su
Facebook la discussione sul
vestito (#TheDress)
• La maggior parte delle
persone lo vede
una minoranza lo vede.
blu nero
bianco oro
Sistemi Multimediali AA 2015/16 56
Come è codificata l’immagine?
• I colori usati nella
codifica dell’immagine
digitale sono quasi tutti
riconoscibili
(singolarmente) come
sfumature di blu e di
nero
Sistemi Multimediali AA 2015/16 57
Come è codificata l’immagine?
• Per esempio Google
quando ricerca foto
simili, individua foto di
abiti blu scuro o blu e
nero
• Ma perché la
maggioranza
lo vede oro e bianco?
Sistemi Multimediali AA 2015/16 58
Perché?
• Potremmo pensare che sia un classico problema di
gestione digitale del colore: il colore viene riprodotto
diversamente da apparati diversi e quindi chi lo vede,
sta effettivamente osservando colori differenti.
• In realtà non è così, persone
che hanno visualizzato il
vestito con lo stesso apparato
hanno valutato diversamente
i colori
• Potrebbe essere una questione legata alla quantità di
coni recettori del blu, che varia da persona a persona,
ma questa variabilità non giustifica una percentuale di
percezioni errate così alta.
Sistemi Multimediali AA 2015/16 59
Perché?
• Se non si tratta del sistema di riproduzione, né
della retina, si tratta del cervello.
• Provando a ritoccare l’immagine si scopre che
è un fenomeno legato alla luminosità: – Rendendo l’immagine
più luminosa è di
sicuro bianco e oro – Rendendola più scura
è certamente blu e
nero
Sistemi Multimediali AA 2015/16 60
Una questione di ombra..
Sistemi Multimediali AA 2015/16 61
Color Constancy
• Color constancy: noi percepiamo che il colore di un
oggetto rimane costante, anche quando cambiano le
condizioni di illuminazione.
• Il quadrato che sembra
arancione nella faccia verticale del cubo è esattamente
dello stesso colore di quello
che pare marrone nella
faccia orizzontale.
Sistemi Multimediali AA 2015/16 62
Color Constancy
• Il nostro cervello interpreta le condizioni di
luce e di conseguenza interpreta il colore.
• Il fatto che nel caso del vestito non si veda
qualche colore di riferimento (come per
esempio il colore della pelle) o quello del
contesto aumenta la
confusione.
• É una illusione ottica legata
alla percezione dei colori nel
contesto, e ne esistono
numerore altre.
Sistemi Multimediali AA 2015/16 63
Riferimenti
• Libro: capitolo 5 (Color)
• Risorse on line sulla piattaforma