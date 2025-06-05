2025-06-05 14:36

Status: #child

Tags:
# Jakarta (JEE)

> [!abstract]
> Insieme di specifiche, framework e librerie Java progettate per lo sviluppo di applicazioni aziendali di livello enterprise. Caratteristiche come sicurezza, persistenza dei dati, scalabilità e affidabilità.

Storicamente, *le applicazioni JEE* venivano *eseguite in un livello intermedio tra un web server* (che gestiva le richieste HTTP tramite servlet o altre tecnologie) *e un backend* che includeva database e sistemi legacy, l’**application server**, il cui compito era quello di *erogare i servizi necessari per l'esecuzione delle applicazioni JEE*, spesso *costituite dagli* **Enterprise Java Beans** (EJBs).

![[jee.png]]

> [!caution]
> In molti casi, il web server e l'application server erano implementati nello stesso prodotto software, come ad esempio WebSphere di IBM e JBoss/Wildfly → eri vincolato al fornitore dell’application server (per sviluppare il JEE dovevi avere un server che supportasse quella logica applicativa).
> Inoltre il deploy non era standardizzato (*oggi Docker e Kubernetes hanno notevolmente semplificato*)

> [!tip] API
> Emerge l'idea che un'applicazione dovesse esporre una Application Programming Interface (API), concepita per essere utilizzata da altri programmi

Componenti di JEE:
- **JDBC** (Java Database Connectivity) e **JPA** (Jakarta Persistence API): J*DBC fornisce l'accesso ai database, mentre JPA è un'astrazione ORM* (Object-Relational Mapping) che si occupa di *tradurre le operazioni sugli oggetti Java in query SQL specifiche per il database sottostante*, semplificando notevolmente lo sviluppo
- **Enterprise Java Beans (EJBs)**: Sono *oggetti Java che forniscono servizi a runtime* e rappresentano un elemento fondamentale per la modularizzazione delle applicazioni aziendali. Hanno fatto diffondere nel mondo Java i seguenti concetti:
	- *Inversion of Control* (IoC): Invece che essere l'oggetto utilizzatore a creare direttamente l'istanza del servizio di cui ha bisogno, con l'IoC è il framework (in questo caso l'application server) a creare e gestire le istanze dei servizi
	  [[Inversion of Control]]
	  
	- *Dependency Injection* (DI): *Il framework "inietta" (fornisce) le dipendenze (gli oggetti di servizio) all'interno degli oggetti che ne fanno richiesta a runtime.* Questo approccio *aumenta l'indipendenza tra gli oggetti e rende il codice più flessibile e testabile*. Framework moderni come Spring utilizzano massicciamente questi concetti. In Spring, ad esempio, gli sviluppatori dichiarano le dipendenze, e il framework si occupa di creare e fornire gli oggetti necessari. 
	  
> [!definizioneviola] IoC & Dependency Injection
> Supponiamo che al componente X serva il componente Y
> - Controllo diretto: X crea un’istanza di Y
> - Controllo rovesciato: il framework crea un’istanza di Y e la «inietta» a tutti coloro che la richiedono, fra cui X
> - Dependency injection: X «chiede» un oggetto Y nel suo costruttore, il framework glielo passa

- *Servlet*: Sono oggetti Java che rimangono in attesa di richieste HTTP e possono utilizzare gli EJB per elaborare le risposte
- *Java Server Pages* (JSP): Sono una tecnologia per la creazione di pagine web dinamiche lato server, integrandosi con gli EJB per visualizzare i dati elaborati
- Java Messaging Service (JMS): È una specifica per un Message Oriented Middleware (MOM) integrato in Jakarta EE, che consente la comunicazione asincrona e disaccoppiata tra diverse applicazioni
Sono inoltre presenti specifiche per autenticazione, autorizzazione e gestione della posta elettronica, fornendo un set completo di strumenti per lo sviluppo di applicazioni aziendali
#### Beans
![[Screenshot from 2025-04-23 15-18-28.png]]

- **Session Bean**: Sono *responsabili dell'implementazione della logica di business* e possono essere di tre tipi (dichiarati tramite *Java Annotations* come `@Stateless, @Stateful, @Singleton`):
	- Stateless: Non mantengono uno stato tra le diverse invocazioni. L'application server può fornire la stessa istanza a più client, rendendoli efficienti in termini di risorse
	- Stateful: Mantengono uno stato specifico per ogni client. L'application server crea un'istanza separata per ogni client, conservando le informazioni relative alla sessione di quel particolare utente
	- Singleton: Esiste una sola istanza per tutta l'applicazione. L'application server ne crea una sola e la condivide tra tutti i client che ne hanno bisogno, seguendo il design pattern Singleton. L'application server è responsabile della creazione e della gestione del ciclo di vita di queste istanze. 
- *Message-Driven Bean* (MDB): Sono componenti che vengono attivati dalla ricezione di un messaggio da un sistema di messaggistica (come JMS). L'application server crea un'istanza del MDB quando arriva un messaggio, lo fa elaborare e poi lo distrugge.

Gli EJB possono essere utilizzati in due modi principali:
- *Localmente*: All'interno della stessa applicazione. Un oggetto client può richiedere l'uso di un EJB semplicemente dichiarando una variabile di istanza del tipo dell'EJB e utilizzando l'annotazione `@EJB`. Il framework si occuperà di iniettare un'istanza dell'EJB nella variabile senza che il programmatore debba crearla manualmente
- *Remotamente*: Da altre applicazioni in esecuzione sullo stesso application server. In questo caso, è necessario un meccanismo più complesso che coinvolge un naming directory service. L'application server funge da object request broker e potenzialmente da TP monitor, gestendo le invocazioni remote e il bilanciamento del carico tra i diversi Bean

*L'application server mette a disposizione gli EJB all'interno di un EJB container*, in modo simile al web container per le servlet. *L'EJB container fornisce l'ambiente di esecuzione (basato su una Java Virtual Machine) e gestisce il ciclo di vita degli EJB* in base alla loro tipologia (stateless, stateful, singleton). Ad esempio, per un EJB stateless, il container può riutilizzare le istanze tra diverse richieste, mentre per un EJB stateful deve creare una nuova istanza per ogni client. Per un EJB singleton, il container ne mantiene una sola istanza per tutta l'applicazione.
#### Jakarta Messaging API (JMS)
*JMS realizza il concetto di MOM all'interno di Jakarta EE*, consentendo la **comunicazione asincrona e disaccoppiata** tra applicazioni. Questo significa che *il mittente e il destinatario* di un messaggio *non devono essere in esecuzione contemporaneamente e non devono conoscere i dettagli implementativi l'uno dell'altro*. La comunicazione avviene tramite code (Queues) per la messaggistica point-to-point (un messaggio ha un solo consumatore) e topic per la messaggistica publish/subscribe (più sottoscrittori possono ricevere i messaggi).

Per utilizzare JMS è necessario un provider JMS che gestisce le code e i topic. 
I client JMS (qualsiasi oggetto Java) possono connettersi al provider e inviare o ricevere messaggi. Gli oggetti chiave di JMS includono i messaggi stessi, le destinazioni (code o topic) e le Connection Factory, che vengono utilizzate per creare connessioni e sessioni per l'invio e la ricezione di messaggi.

Nel modello point-to-point (code), il mittente invia un messaggio a una coda e un solo ricevente lo consumerà, segnalando al sistema una volta processato. Nel modello publish/subscribe (topic), il publisher invia un messaggio a un topic e tutti i sottoscrittori (subscriber) interessati lo ricevono. Tuttavia, *a differenza di alcuni MOM generali, in JMS il sottoscrittore deve essere attivo* (sottoscritto e in esecuzione) *per ricevere i messaggi inviati al topic*. Se un sottoscrittore è offline, non riceverà i messaggi inviati durante la sua assenza.

[[Java Spring#Java Spring]]
# References
