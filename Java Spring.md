2025-04-28 16:18

Status: #baby 

Tags:
# Java Spring

> [!definizioneviola] Server HTTP
> Applicazione che viene eseguita su una macchina detta host e sfrutta (fra le altre cose) i servizi TCP/IP del sistema operativo per ricevere richieste HTTP e rispondere ad esse.

Un Server HTTP deve gestire (almeno ipoteticamente) una *grande quantità di richieste «in parallelo»*. Le richieste giungono in una coda e vengono prese in considerazione nell’ordine di arrivo. è ragionevole assumere che la coda sarà molto raramente vuota. Non si può pensare dunque che la coda sia gestita in modo completamente sequenziale!

 > [!abstract] Modello single-thread asynchronous event loop
 > Le richieste sono prese in carico sequenzialmente da un loop a thread singolo. Le elaborazioni potenzialmente lunghe (I/O o CPU-intensive) devono avvenire in modo asincrono, gestite da thread separati o dal sistema operativo. Esempi: Nginx, HTTP Server basati su Node.js. Questo modello può avere performance più prevedibili sotto alto carico

> [!abstract] multi-thread
> Per ogni richiesta in arrivo, il Server HTTP genera un thread separato e dedicato che gestisce la richiesta, anche in modo sincrono. Esempi: Apache Web, Apache Tomcat

> [!question] Web server?
> L'HTTP Server si riferisce al protocollo di comunicazione. Non è detto che sia usato come Web Server; potrebbe esporre dati di un DB o agire solo da reverse proxy. Un Server è un Web Server se realizza il *"core business" di fornire risorse statiche e dinamiche per il World Wide Web*

Dall’esterno, è possibile rivolgersi all’host usando l’indirizzo IP ad esso assegnato quando è stato inserito in rete, o lo hostname corrispodente a tale IP. *Per contattare uno specifico servizio di livello applicativo* (come ad esempio l’HTTP Server) è necessario conoscere la porta su cui esso è in esecuzione (la maggior parte degli HTTP Server è in esecuzione sulla porta di default 80 o sulla porta 443 se stiamo usando la variante sicura HTTPS).
##### L’unico modo per differenziare i diversi servizi in esecuzione resta dunque la porta

Il suo compito principale è *ascoltare le richieste sulla porta assegnata, elaborarle e fornire una risposta*.

Le sue funzioni includono la fornitura di contenuti statici e dinamici, logging, gestione di host virtuali, autenticazione e autorizzazione, caching, riduzione di banda e riscrittura delle URL.

> [!definizioneviola] framework server-side
> Il ruolo principale dei framework nelle applicazioni server-side è quello di automatizzare parte dei compiti e rendere più uniformi le interfacce. Il framework si frappone fra il «core» dell’applicazione e l’ambiente di esecuzione, facendosi carico di parte dei compiti. Esattamente quali compiti siano gestiti dal framework, come siano gestiti e come sia possibile prevedere al loro interno l’esecuzione di codice personalizzato, è molto dipendente dal framework che si sceglie di usare.

> [!abstract] http
> Il protocollo HTTP è nato per inviare documenti ipertestuali, e, in sostanza, per realizzare il World Wide Web. La funzione più comune (anche se non l’unica) di un Server Web resta quella di fornire contenuti statici e dinamici: per gli utenti di inviare dati al server al fine di «pubblicarli» verso altri utenti (la base, potremmo dire, di quello che è diventato noto come Web 2.0) e le vere e proprie Applicazioni Web, che come abbiamo visto si basano sullo scambio di risorse fra client/browser e server Web.

Talvolta un Server Web ospita più host, ciascuno con il proprio hostname. *Nella maggior parte dei casi un HTTP Server ha un unico indirizzo IP.* Dunque *tutti gli hostname virtuali saranno mappati dal DNS sul medesimo IP*. Per capire qual è la risorsa da fornire, il Server Web dovrà esaminare la richiesta HTTP per stabilire qual era lo hostname utilizzato dal mittente.

> [!definizione] Reverse Proxy
> Un Server HTTP che riceve le richieste HTTP (ad es., sulla porta di default), e in base al loro contenuto le reindirizza altrove (ad esempio, al Server Web principale usando il numero di porta abbinato allo hostname contenuto nella richiesta). Il reverse proxy è molto utilizzato anche per gestire siti o applicazioni Web i cui contenuti e servizi sono in realtà erogati da molteplici Server Web; in questo caso, la richiesta specifica sempre il medesimo hostname, ma sarà il reverse proxy che, sulla base del pathname, redirige a un Server Web o a un altro.
> 
> Instead of clients connecting directly to the backend servers, they connect to the reverse proxy, which then forwards their requests to the appropriate server.

Una delle funzionalità che molti Server Web forniscono è quella di permettere o vietare l’accesso ad alcuni pathname/risorse sulla base dell’IP del mittente. Si pensi ad esempio a una rete aziendale: alcune risorse saranno disponibili solo a computer interni alla rete aziendale stessa
In questa circostanza, se i dipendenti in smart working devono poter accedere alle risorse interne, sarà necessario che installino una VPN (virtual private network) che permette di «presentarsi» all’esterno con un diverso IP, per simulare l’appartenenza ad una rete locale (in modo legale: per assumere un IP appartenente a una rete locale, bisogna installare un certificato fornito dal proprietario della rete locale stessa)

Autenticazione != autorizzazione

> [!definizioneviola] bandwidth throttling
> Quando un Server Web eroga dati che possono consumare significativamente l’ampiezza di banda in uscita, può ricorrere al bandwith throttling (letteralmente «strozzatura della banda»). In pratica l’ampiezza di banda occupata da una singola risposta viene ridotta artificialmente, per permettere di suddividere la banda disponibile fra più stream paralleli in uscita.

> [!abstract] Rewrite Emgine
> Non sempre la URL che viene richiesta al Server Web dal client corrisponde al pathname che il server utilizza internamente per reperire la risorsa, si vuole invece che i client possano utilizzare URL «pulite» e evocative di quello che si sta richiedendo. Alcuni Server Web includono un «motore di riscrittura», ossia una componente che applica regole sintattiche per tradurre le URL dalla versione «clean» alla versione «raw».
#### Sessioni
*Il protocollo HTTP è di per sé «stateless»*, non prevede un’idea di stato dello scambio. *Ogni transazione HTTP (richiesta + risposta) è indipendente* dalle altre. L’unico modo di «simulare» l’esistenza di uno stato è ad ogni passo della conversazione riportare tutte le informazioni rilevanti scambiate in precedenza.
Un server HTTP gestisce multiple conversazioni HTTP con diversi client, quindi, *a meno che il client non si renda in qualche modo riconoscibile, non è possibile per il server sapere «a quale punto» della conversazione si trova*, semplicemente perché sarà in punti diversi a seconda dell’interlocutore.
Quindi **è necessario «costruire» uno stratagemma al di sopra del protocollo HTTP** per permettere a client e server in primis di sapere che stanno avendo una conversazione prolungata, e in secondo luogo per mantenere una sorta di «stato» di tale conversazione.

Uno dei modi più semplici per tener traccia di una sessione tramite il protocollo HTTP è attraverso l’uso dei **cookie**. Un cookie è un blocco di dati che il server manda al client nel corso del primo scambio della loro conversazione; ad ogni successivo scambio, il client aggiungerà il cookie alla propria richiesta, in modo che il server identifichi il particolare thread di conversazione che sta avendo con quel client.

![[serversidespring.png]]

![[serversidespring2.png]]

*Lo sviluppatore in Spring realizza dei **request handler***, fornendo al framework informazioni su
- A quali tipi di richieste HTTP ciascun handler risponde (ossia: a quale method/route)
- Quali dettagli della richiesta HTTP gli servono per funzionare (ad es.: gli servono i parametri della query string, piuttosto che il body della request, piuttosto che i parametri ottenuti tramite segmenti parametrici della URL)
Il framework si incaricherà di invocare l’handler corretto e fornirgli le informazioni richieste.
### Architettura
![[Java spring_webprofile.png]]
L'architettura di esecuzione di un'applicazione basata su Servlet vede come attori principali il Server HTTP (Tomcat), l'applicazione (una o più istanze) e il Web Container.
*Il **Web Container** funge da interfaccia tra Server e applicazioni*, *gestendo il ciclo di vita* dell'applicazione e delle servlet.
Inoltre è responsabile *di inizializzare gli oggetti servlet* all'avvio o all'installazione dell'app, *gestire le richieste HTTP* per l'app invocando la Servlet appropriata, *gestire eccezioni* (rispondendo con 500) e distruggere gli oggetti servlet allo spegnimento o disinstallazione

Come vedremo meglio in seguito, **gli handler in Spring sono raggruppati all’interno di classi dette «controller»**. All’interno di Spring (e lontano dall’occhio dello sviluppatore) *ciascun controller corrisponde di fatto a una servlet di Jakarta*.

> [!question] Spring Boot vs Spring
> Spring Boot estende Spring adottando un approccio «dogmatico» rispetto ad alcune scelte architetturali e progettuali su cui Spring è di per sé laico. *È proprio la «laicità» di Spring a rendere complessa la configurazione* di ogni singolo progetto. *Le scelte per certi versi imposte di Spring Boot d’altro canto semplificano*, velocizzano e rendono più efficiente la realizzazione di applicazioni, a patto che siano compatibili con codeste scelte.
> - Spring Boot offre dei *pacchetti di dipendenze standard* che evitano di andare a specificare una per una le librerie che si intende usare; naturalmente è poi sempre possibile andare ad aggiungere dipendenze custom
> - Spring Boot *incapsula un’installazione di Tomcat, e la gestisce internamente*, dunque un’applicazione Spring Boot è di fatto un’applicazione stand-alone il cui deploy è grandemente semplificato dal fatto che non bisogna fare i conti con la configurazione pre-esistente dell’HTTP server.
> - Spring Boot fornisce modelli di configurazione predefiniti per molte delle funzionalità di Spring, che sono adeguati per la maggior parte dei casi e risparmiano allo sviluppatore di farlo a mano.
### Servlet
Start
1. Creazione: Il Web Container crea un `ServletContext` (uno per applicazione), un'istanza per ciascuna Servlet, e un `ServletConfig` per ogni istanza (contenente configurazione, spesso da annotazioni `@WebServlet`). Le Servlet e le loro route sono registrate.
2. Inizializzazione: Per ogni Servlet, il Web Container chiama il metodo `init(ServletConfig config)` (della classe base `GenericServlet`), che a sua volta chiama il metodo `init()` (vuoto di default ma sovrascrivibile per logica di inizializzazione). La Servlet è pronta solo dopo il completamento di `init()`
Service
3. Matching & Routing: Il Web Container seleziona la Servlet appropriata per la richiesta HTTP basandosi sull'URL
4. Predisposizione: Vengono creati gli oggetti `HttpServletRequest` e `HttpServletResponse,` derivati da `ServletRequest` e `ServletResponse`
5. Invocazione del servizio: Il Web Container chiama il metodo `service(HttpServletRequest req, HttpServletResponse res)` della Servlet selezionata (implementato nella classe `HttpServlet`). Questo metodo, in base al metodo HTTP della richiesta (GET, POST, ecc.), invoca il corrispondente metodo `doXXX()` (es. `doGet`, `doPost`). I metodi `doXXX()` nella classe base `HttpServlet` non fanno nulla; è responsabilità della Servlet specifica dell'applicazione sovrascriverli per definire la logica di gestione.
Stop
6. Cleaning up: Per ogni Servlet, il Web Container chiama il metodo `destroy()`. Questo metodo, vuoto di default, può essere implementato per rilasciare risorse (es. chiudere connessioni DB) prima della rimozione.
7. Garbage collection: Gli oggetti Servlet e associati vengono eliminati

Una Servlet è dunque un'istanza di una classe che eredita da `HttpServlet`. La gerarchia chiave include l'*interfaccia Servlet* (che definisce `init, service, destroy`), la *classe astratta GenericServlet* (che fornisce un'implementazione base di `init`), e la classe `HttpServlet` (che implementa service per instradare alle chiamate `doXXX` basate sul metodo HTTP)

> [!attention]
> Perché un XML sia ben formato devono essere rispettati i seguenti vincoli: un tag XML deve essere una sequenza di caratteri alfanumerici fra parentesi angolari: <...> ; per ogni tag che scelgo di usare, il corrispondente tag di chiusura è ; un tag può chiudersi solo se tutti gli altri tag aperti al suo interno sono già stati chiusi, dunque l'XML (così come HTML) ha una struttura ad albero ; deve esserci un unico tag radice che contiene tutti gli altri
### Creazione Progetto
![[springboot_structure.png]]

![[springboot_pom.png]]

La *gestione delle dipendenze* è un tema rilevante nei progetti server-side basati su Java indipendentemente dal fatto che usino semplicemente il Jakarta Web Profile piuttosto che Spring o Spring Boot (così come d’altra parte lo è nei progetti client-side indipendentemente dal fatto che usino un framework o l’altro o nessuno).
Uno degli asset di Spring Boot sono i **dependency starter**, ossia dei *«pacchetti di dipendenze» che corrispondono alle necessità più comuni* delle applicazioni «enterprise» realizzate con Java, e che possono essere richiesti in blocco tramite il pom.xml, senza dover indicare uno per uno tutti i package necessari.

![[JavaSpring_main.png]]
##### Senza Spring Boot
Se non usassimo Spring Boot, ma solo Spring, o solo il Jakarta Web Profile, *la nostra applicazione non avrebbe una «main class» che fa da punto di ingresso dell’applicazione stessa*. Sarebbe un insieme di classi che vengono istanziate dal Web Container (nel caso di una Jakarta EE) o dall’ambiente di esecuzione di Spring. Gli oggetti ottenuti dall’istanziazione verrebbero poi invocati quando necessario (ad esempio, quando c’è da gestire una richiesta HTTP).
Per eseguire l’applicazione sarebbe necessario
- installare Tomcat sul nostro computer
- compilare e «impacchettare» (bundle) il file .class così ottenuti
- effettuare il «rilascio» (deploy) del pacchetto in Tomcat, in modo che Tomcat possa eseguirlo all’interno del Web Container tramite la sua JVM
##### Con SPringBoot
Spring Boot ci risparmia tutto questo. Ci sono sempre le «classi operative» che vengono istanziate dall’ambiente di esecuzione di Spring, ed è sempre vero che le istanze ottenute vengono invocate quando necessario da quello stesso ambiente. Tuttavia *c’è anche una main class che invoca le opportune librerie di Spring affinché eseguano una versione embedded di Tomcat con l’applicazione già rilasciata (deployed) al suo interno*. Pertanto *è possibile effettuare un semplice run* dell’applicazione come faremmo con una qualsiasi applicazione Java.

```Java
@SpringBootApplication
public class MyApplication
{
  public static void main(String[] args)
  {
    SpringApplication.run(MyApplication.class, args);
  }
}
```
#### Java Annotations
Nel nostro caso avremo a che fare con annotazioni definite nei package inclusi nel progetto tramite il pom.xml. **Puramente dichiarative: non fanno qualcosa, forniscono informazioni sull’elemento annotato.**
Utili per:
- Sviluppatori
- Al compilatore, per effettuare verifiche (es.: @Override; se il metodo così annotato non è effettivamente un override di un omonimo nella classe base, il compilatore segnala un errore)
- A servizi runtime, per attuare determinati comportamenti sugli elementi annotati (**importante!**)

*Il framework Spring* infatti è appunto quel *servizio runtime che, grazie alla Java Reflection API, legge le annotazioni* apposte sulle nostre classi, metodi, parametri, campi, ecc… e *attraverso di esse capisce* come, dove e quando utilizzarli, come invocarne le funzionalità, e come dotarli di comportamenti aggiuntivi forniti da Spring stesso.
#### *Pattern MVC*
![[Javaspring_mvc.png]]

Spring struttura le applicazioni con il pattern Model-View-Controller: l’applicazione è costituita da **più controller**, ciascuno dei quali è responsabile per **rendere** «fruibile» una parte del modello (che contiene i dati e la loro logica) tramite una o più viste.

> [!faq] punto di ingresso → controller
  **Il punto di ingresso dell’applicazione è sempre uno dei controller**: è il controller che riceve la richiesta HTTP e la elabora. In Spring i componenti che svolgono il ruolo di controller sono classi identificate dall’annotazione @Controller

> [!abstract] Controller: compiti
> - Il controller fa da «mediatore» fra una o più view (ossia la presentazione delle informazioni, che include sia il modo in cui sono rappresentate all’esterno, sia le possibili azioni che è possibile operare dall’esterno per chiedere modifiche) e gli aspetti model (ossia la business logic e i repository dati, che detengono le informazioni, la loro strutturazione, i loro vincoli di coerenza, e sanno come effettuare eventuali aggiornamenti ai dati stessi) che sono di sua pertinenza
> - Il controller è dunque responsabile dell’API, che possiamo vedere come la descrizione della view che il controller mette a disposizione

> [!definizioneviola] View
> “punto di vista” (non necessariamente grafico) su un certo sottoinsieme coerenti di dati
> Ogni controller realizza una vista e la descrive tramite API

> [!definizione] Model
> Il model dell’applicazione *contiene la business logic e l’accesso ai dati*, occupandosi anche della loro **persistenza**. Esso conosce i dati e la loro strutturazione, nonché i loro vincoli di coerenza, è dunque in grado di organizzarli e di aggiornarli quando necessario. In Spring i dati in quanto tali sono organizzati in componenti @Repository, strettamente collegati al tema della persistenza.

Per dare risposta dal controller , ci metti il tipo che vuoi `ResponseEntity<Persona>` 
> [!abstract] accesso ai dati
> I dati possono essere acceduti dai controller così *come sono* (quindi con un’organizzazione DB-like) *oppure tramite la mediazione di servizi di Business Logic* *che aggregano e strutturano i dati,* ne garantiscono la consistenza, li «gestiscono» secondo una «logica d’impresa» specifica, e possono offrire diverse prospettive su di essi.
> Per questa ragione nel model dell’MVC di Spring troviamo anche *i componenti* `@Service`, che permettono al controller di non occuparsi (ad esempio) dei dettagli di come i dati sono rappresentati, e forniscono operazioni di più alto livello

![[Java Spring_db.png]]
![[Java Spring_db2.png]]

> [!definizioneviola] ORM (Object-relational mapping)
> Tecnica per mappare le strutture relazionali del DB (tabelle, record, colonne) a costrutti della programmazione orientata agli oggetti (classi, istanze, campi) -> *interagire col DB manipolando oggetti invece di scrivere query SQL dirette*.
> JPA (Jakarta Persistence API) è una specifica (parte di Jakarta EE) per l'ORM in Java:
> - le tabelle del DB sono mappate a classi Java dette Entities, annotate con `@Entity`. ***Istanza entity == record***
>   I campi della classe corrispondono alle colonne, annotati con `@Column` per configurare dettagli come nome, nullabilità e unicità

> [!definizione] JPA
> JPA (Jakarta Persistence API) è parte di Jakarta EE ed è una specifica che descrive come gestire dati relazionali a partire da Java. *non implementa un servizio di ORM, è piuttosto una specifica dell’interfaccia di programmazione che un ORM per Java dovrebbe rispettare*

Hibernate è il provider di JPA preferito da Spring Boot

- I @RestController hanno la responsabilità di gestire le richieste HTTP e le risposte
- I @Service hanno la responsabilità di attuare i servizi di business logic, ossia le vere e proprie funzionalità dell’applicazione, solitamente attuando qualche forma di I/O sullo strato di persistenza dei dati
- I @Repository hanno la responsabilità di garantire la corretta persistenza dei dati a loro affidati. Ogni @Repository gestisce una entità ben precisa. I @Repository non sanno nulla delle funzionalità di business logic


> [!importante] CORS (Cross-Origin Resource Sharing)
> L’origine di un’applicazione client-side è il Server HTTP che l’ha fornita.
> CORS si verifica quando un'applicazione client-side, servita da un'origine (Server HTTP) specifica, *tenta di richiedere risorse da un'applicazione server-side su un'origine diversa* (es. Porta diversa, anche su localhost in sviluppo).
> Quando si verifica una richiesta di questo tipo, il browser, *prima di far partire l’effettiva fetch* che compare nel codice dell’app client-side, effettua al server una richiesta detta ***preflight***, che usa l’HTTP method OPTIONS, per verificare se il server permette l'accesso dalla specifica origine, con il metodo HTTP e gli header richiesti.
> Il server risponde con header che indicano cosa è permesso.
> Per default, i server bloccano le richieste cross-origin (politica noCORS). *In fase di sviluppo, un approccio semplice è usare l'annotazione `@CrossOrigin` su controller o handler Spring* per consentire richieste da qualsiasi origine verso quegli endpoint

Nella preflight request, il browser descrive la richiesta effettiva che vorrebbe effettuare attraverso tre header
- Access-Control-Request-Method: quale sarà l’HTTP method della richiesta
- Origin: qual è l’origine dell’applicazione client-side che effettuerà la richiesta
- Access-Control-Request-Headers: specifica gli HTTP header della richiesta che verrà effettuata
#### Sessione JSPRING
[[Java Spring#Sessioni]]

Usare i cookies. Specifichiamo poi che si tratta di un cookie http-only, ossia che il browser e il codice dell’applicazione client-side non hanno accesso ai contenuti del cookie, e che il cookie deve essere secure ossia cifrato.

l’applicazione client-side deve collaborare: deve infatti mandare indietro il cookie ad ogni richiesta HTTP che invia all’app server-side, ma se siamo in una situazione cross-origin, per default le credenziali non vengono inviate al server. Per ottenere che vengano inviate, dobbiamo specificare nelle RequestOptions della fetch l’opzione credentials: "include"
##### Filtrare le richieste
Quando c’è la necessità di eseguire operazioni preliminari sulle richieste HTTP che pervengono ad una app server-side, è utile implementare un **filtro**, ossia una *funzione che verrà chiamata appunto per ogni richiesta HTTP prima di inoltrarla ad uno specifico request handler*.

- una classe che implementa l’interfaccia Filter
- ed è annotata con @Component
- 
L’interfaccia Filter richiede di implementare il metodo: 
```Java
public void doFilter(ServletRequest servletRequest,
	ServletResponse servletResponse,
	FilterChain filterChain) 
	throws IOException, ServletException
```

![[Java Spring_auth.png]]

versione particolarmente semplificata (e per nulla sicura) in cui username e password viaggiano in chiaro come query parameters nella richiesta HTTP. È possibile realizzare una Basic Auth un poco più sicura inserendo username e password nel body della richiesta (quindi, effettuando una POST anziché una GET) ed usando, per la connessione, il protocollo HTTPS anziche HTTP standard.

# References
