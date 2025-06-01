2025-04-28 16:18

Status: #baby 

Tags:
# Java Spring

> [!definizioneviola] Server HTTP
> Applicazione che viene eseguita su una macchina detta host e sfrutta (fra le altre cose) i servizi TCP/IP del sistema operativo per ricevere richieste HTTP e rispondere ad esse.

Dall’esterno, è possibile rivolgersi all’host usando l’indirizzo IP ad esso assegnato quando è stato inserito in rete, o lo hostname corrispodente a tale IP. *Per contattare uno specifico servizio di livello applicativo* (come ad esempio l’HTTP Server) è necessario conoscere la porta su cui esso è in esecuzione (la maggior parte degli HTTP Server è in esecuzione sulla porta di default 80 o sulla porta 443 se stiamo usando la variante sicura HTTPS).
##### L’unico modo per differenziare i diversi servizi in esecuzione resta dunque la porta

Il suo compito principale è *ascoltare le richieste sulla porta assegnata, elaborarle e fornire una risposta*.

Le sue funzioni includono la fornitura di contenuti statici e dinamici, logging, gestione di host virtuali, autenticazione e autorizzazione, caching, riduzione di banda e riscrittura delle URL.

> [!definizioneviola] framework server-side
> Il ruolo principale dei framework nelle applicazioni server-side è quello di automatizzare parte dei compiti e rendere più uniformi le interfacce. Il framework si frappone fra il «core» dell’applicazione e l’ambiente di esecuzione, facendosi carico di parte dei compiti. Esattamente quali compiti siano gestiti dal framework, come siano gestiti e come sia possibile prevedere al loro interno l’esecuzione di codice personalizzato, è molto dipendente dal framework che si sceglie di usare.

> [!abstract] http
> Il protocollo HTTP è nato per inviare documenti ipertestuali, e, in sostanza, per realizzare il World Wide Web. La funzione più comune (anche se non l’unica) di un Server Web resta quella di fornire contenuti statici e dinamici: per gli utenti di inviare dati al server al fine di «pubblicarli» verso altri utenti (la base, potremmo dire, di quello che è diventato noto come Web 2.0) e le vere e proprie Applicazioni Web, che come abbiamo visto si basano sullo scambio di risorse fra client/browser e server Web.

Talvolta un Server Web ospita più host, ciascuno con il proprio hostname. Nella maggior parte dei casi un HTTP Server ha un unico indirizzo IP. Dunque *tutti gli hostname virtuali saranno mappati dal DNS sul medesimo IP*. Per capire qual è la risorsa da fornire, il Server Web dovrà esaminare la richiesta HTTP per stabilire qual era lo hostname utilizzato dal mittente.

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

![[serversidespring.png]]

![[serversidespring2.png]]

Lo sviluppatore in Spring realizza dei request handler, fornendo al framework informazioni su
- A quali tipi di richieste HTTP ciascun handler risponde (ossia: a quale method/route)
- Quali dettagli della richiesta HTTP gli servono per funzionare (ad es.: gli servono i parametri della query string, piuttosto che il body della request, piuttosto che i parametri ottenuti tramite segmenti parametrici della URL)
Il framework si incaricherà di invocare l’handler corretto e fornirgli le informazioni
Richieste.

Come vedremo meglio in seguito, gli handler in Spring sono raggruppati all’interno
Di classi dette «controller». All’interno di Spring (e lontano dall’occhio dello
Sviluppatore) ciascun controller corrisponde di fatto a una servlet di Jakarta.

> [!question] Spring Boot vs Spring
> Spring Boot estende Spring adottando un approccio «dogmatico» rispetto ad alcune scelte architetturali e progettuali su cui Spring è di per sé laico. È proprio la «laicità» di Spring a rendere complessa la configurazione di ogni singolo progetto. Le scelte per certi versi imposte di Spring Boot d’altro canto semplificano, velocizzano e rendono più efficiente la realizzazione di applicazioni, a patto che siano compatibili con codeste scelte.
> - Spring Boot offre dei pacchetti di dipendenze standard che evitano di andare a specificare una per una le librerie che si intende usare; naturalmente è poi sempre possibile andare ad aggiungere dipendenze custom
> - Spring Boot incapsula un’installazione di Tomcat, e la gestisce internamente, dunque un’applicazione Spring Boot è di fatto un’applicazione stand-alone il cui deploy è grandemente semplificato dal fatto che non bisogna fare i conti con la configurazione pre-esistente dell’HTTP server.
> - Spring Boot fornisce modelli di configurazione predefiniti per molte delle funzionalità di Spring, che sono adeguati per la maggior parte dei casi e risparmiano allo sviluppatore di farlo a mano.

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
### Java Annotations
Nel nostro caso avremo a che fare con annotazioni definite nei package inclusi nel progetto tramite il pom.xml.
**puramente dichiarative: non fanno qualcosa, forniscono informazioni sull’elemento annotato.**
Utili per:
- Sviluppatori
- Al compilatore, per effettuare verifiche (es.: @Override; se il metodo così annotato non è effettivamente un override di un omonimo nella classe base, il compilatore segnala un errore)
- A servizi runtime, per attuare determinati comportamenti sugli elementi annotati (**importante!**)

*Il framework Spring* infatti è appunto quel *servizio runtime che, grazie alla Java Reflection API, legge le annotazioni* apposte sulle nostre classi, metodi, parametri, campi, ecc… e *attraverso di esse capisce* come, dove e quando utilizzarli, come invocarne le funzionalità, e come dotarli di comportamenti aggiuntivi forniti da Spring stesso.
#### *Pattern MVC*
![[Javaspring_mvc.png]]

Spring struttura le applicazioni con il pattern Model-View-Controller: l’applicazione è costituita da più controller, ciascuno dei quali è responsabile per rendere «fruibile» una parte del modello (che contiene i dati e la loro logica) tramite una o più viste.

> [!faq] punto di ingresso → controller
  Il punto di ingresso dell’applicazione è sempre uno dei controller: è il controller che riceve la richiesta HTTP e la elabora. In Spring i componenti che svolgono il ruolo di controller sono classi identificate dall’annotazione @Controller

> [!abstract] Controller: compiti
> - Il controller fa da «mediatore» fra una o più view (ossia la presentazione delle informazioni, che include sia il modo in cui sono rappresentate all’esterno, sia le possibili azioni che è possibile operare dall’esterno per chiedere modifiche) e gli aspetti model (ossia la business logic e i repository dati, che detengono le informazioni, la loro strutturazione, i loro vincoli di coerenza, e sanno come effettuare eventuali aggiornamenti ai dati stessi) che sono di sua pertinenza
> - Il controller è dunque responsabile dell’API, che possiamo vedere come la descrizione della view che il controller mette a disposizione

> [!definizioneviola] View
> “punto di vista” (non necessariamente grafico) su un certo sottoinsieme coerenti di dati
> Ogni controller realizza una vista e la descrive tramite API

> [!definizione] Model
> Il model dell’applicazione *contiene la business logic e l’accesso ai dati*, occupandosi anche della loro **persistenza**. Esso conosce i dati e la loro strutturazione, nonché i loro vincoli di coerenza, è dunque in grado di organizzarli e di aggiornarli quando necessario. In Spring i dati in quanto tali sono organizzati in componenti @Repository, strettamente collegati al tema della persistenza.

> [!abstract] accesso ai dati
> I dati possono essere acceduti dai controller così *come sono* (quindi con un’organizzazione DB-like) *oppure tramite la mediazione di servizi di Business Logic* *che aggregano e strutturano i dati,* ne garantiscono la consistenza, li «gestiscono» secondo una «logica d’impresa» specifica, e possono offrire diverse prospettive su di essi.
> Per questa ragione nel model dell’MVC di Spring troviamo anche *i componenti* `@Service`, che permettono al controller di non occuparsi (ad esempio) dei dettagli di come i dati sono rappresentati, e forniscono operazioni di più alto livello
### Inversion of Control
![[Inversion of Control#Pattern architetturale attualmente utilizzato in moltissimi framework.]]

MANCANO CREDO LE ULTIME DUE LEZIONI DI SPRING E LE SLIDE A PARTIRE DALLA 24

# References
