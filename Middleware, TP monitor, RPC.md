2025-06-05 14:30

Status: #child

Tags:
# Middleware, TP monitor, RPC

Il middleware viene introdotto come quel *software che si interpone tra diverse applicazioni per garantirne l'integrazione e la coerenza*
Un primo esempio fondamentale di middleware è la **Remote Procedure Call (RPC)**

> [!definizioneviola] RPC
> *Permettere a un applicativo client di invocare una funzione che si trova su un server in modo trasparente, come se fosse una normale chiamata* di funzione locale.
> Per realizzare ciò, si utilizza *un Interface Definition Language (IDL) per definire l'interfaccia tra client e server*.
> Un ambiente di sviluppo compila questa descrizione e genera due componenti di codice: uno **stub client** (che sul client *simula la funzione remota e contiene le chiamate al server*) e uno **stub server** (che *sul server riceve le richieste e invoca la funzione locale*).
> I dati vengono trasferiti tra client e server attraverso processi di marshalling (mantenere la struttura complessa dei dati, inclusi i riferimenti) e serializzazione (tradurre i dati in un formato trasmissibile in rete).
> Al momento dell'invocazione, avvengono diverse fasi: il binding (individuazione del server), il marshalling e la serializzazione dei parametri, l'invio della richiesta, la ricezione, l'unmarshalling e la deserializzazione sul server, l'esecuzione della funzione, e il processo inverso per la restituzione del risultato

*La RPC rappresenta la base concettuale per molti altri middleware*

Un'evoluzione della RPC è il **TP monitor (Transaction Processing monitor)**

> [!definizione] TP Monitor
> Estende le funzionalità della RPC *garantendo proprietà transazionali ACID (Atomicity, Consistency, Isolation, Durability)* alle chiamate remote.
> Interposizione tra l'applicazione client e le risorse (dati o server), offrendo *procedure di accesso transazionale e meccanismi di rollback* in caso di fallimento.
> Oltre alla transazionalità, il TP monitor offre servizi di affidabilità (tramite replica dei servizi su più server), bilanciamento del carico (distribuzione delle richieste tra server), funneling (gestione del flusso di richieste per evitare sovraccarichi), e connection pooling (condivisione di risorse tra più client)
> Per implementare la transazionalità distribuita, un TP monitor può utilizzare meccanismi come il two-phase commit (2PC), che prevede una fase di preparazione e una fase di commit per garantire che una transazione su più database avvenga in modo atomico (o tutto o niente)

> [!abstract] 2-phase commit
> 1. Fase di preparazione (Preparation Phase): Il client (l'applicazione che richiede l'operazione) *invia una richiesta ai diversi server coinvolti*, specificando l'operazione da eseguire e chiedendo loro di prepararsi. I server verificano se sono in grado di eseguire l'operazione e possono anche tentare di eseguirla, sapendo che non devono ancora effettuare il commit finale. Il TP Monitor riceve da ciascun server l'indicazione sulla fattibilità dell'operazione.
> 2. Fase di commit (Commit Phase): *Se tutti i server hanno risposto positivamente (sono pronti), il TP Monitor invia a tutti l'ordine di eseguire il commit dell'operazione. Se anche uno solo dei server rifiuta l'esecuzione, il TP Monitor ordina a tutti di eseguire il rollback*, annullando le operazioni precedentemente tentate.

Il Two-Phase Commit richiede che sia il client che i server supportino questo protocollo, il che implica una gestione dello stato e degli scambi di messaggi

**Object Request Broker (ORB)** rappresenta un'*evoluzione della RPC per i linguaggi di programmazione orientati agli oggetti*. Invece di rendere disponibile una semplice chiamata di funzione, *l'ORB espone un oggetto con tutti i suoi metodi in remoto*.
*Anche in questo caso si utilizza un Interface Definition Language (IDL)*, più complesso rispetto a quello usato con le RPC. L'IDL permette di specificare l'interfaccia dell'oggetto remoto, consentendo al client di fare riferimento a tale interfaccia e invocare i suoi metodi. *L'implementazione effettiva dei metodi risiede su un oggetto sul server, chiamato servant*.
L'ORB funge da *intermediario runtime tra il client e il servant*: sul client, l'ORB *riceve le richieste e le trasforma in messaggi di rete*, inviandoli all'ORB sul server. L'ORB del server *riceve il messaggio e lo trasforma in un'invocazione* del metodo sull'oggetto servant corrispondente
La comunicazione tra gli ORB avviene tramite protocolli specifici:
- GOP (General Interorb Protocol): un protocollo astratto
- IIOP (Internet Interorb Protocol): un'implementazione del GOP su TCP

> [!bug] Requisiti computazionali
> L'architettura ORB è descritta come "piuttosto pesantina" a causa della complessità necessaria per far funzionare il meccanismo

> [!note]
> Un'idea interessante di CORBA (architetture storiche che hanno proposto ORB), che all'epoca non ebbe grande successo ma che è riemersa in seguito, era la possibilità per un client di scoprire dinamicamente in rete oggetti che implementavano l'interfaccia del servizio desiderato. Questo meccanismo si basava su un registro che pubblicava l'identità degli oggetti disponibili. L'obiettivo era di disaccoppiare il servizio richiesto dalla sua specifica implementazione e persino dall'indirizzo di rete del server, offrendo una sorta di "mirror" di servizi tra cui scegliere dinamicamente

Esisteva anche l'**Object Transaction Monitor (OTM)**, un sistema di middleware che *combinava le funzionalità del TP Monitor e di un ORB*, *garantendo le proprietà ACID non sulle operazioni ma sulle invocazioni di metodi di oggetti.*

Il **Message Oriented Middleware (MOM)** è un altro tipo di middleware che permette a *diverse applicazioni su una stessa rete locale* aziendale di comunicare in modo *asincrono* tramite l'invio di *messaggi*. A differenza della comunicazione diretta client-server, il MOM funge da intermediario che smista i messaggi.

> [!important] Fire and forget
> La comunicazione asincrona con MOM implica che il mittente invia un messaggio con la modalità *"fire and forget"* (manda e dimentica), senza attendere una risposta immediata. La risposta, se prevista, arriverà in un momento successivo sotto forma di un altro messaggio → **forte disaccoppiamento tra mittente e destinatario** Il mittente non necessita di conoscere l'API o l'interfaccia del destinatario; invia semplicemente un messaggio

Esistono due tipi principali di MOM:
- Point-to-point: Il messaggio ha un destinatario specifico. Una variante prevede che, una volta letto, il messaggio venga consumato e non sia più disponibile
- Publish/subscribe: Il messaggio è in broadcast su un canale, e tutti gli iscritti al canale possono riceverlo. È importante notare che, in genere, i messaggi non vengono recapitati a chi si iscrive a un topic dopo l'invio del messaggio.

JMS (Java Messaging System) è un esempio di tecnologia MOM che implementa il modello publish/subscribe.
Con i MOM, si introduce il concetto di *tecnologie push*, dove *il gestore dei messaggi può "spingere" il messaggio verso il ricevente, senza che quest'ultimo debba interrogare attivamente la coda*. Questo è legato al *paradigma* **event-driven**, in cui i servizi non aspettano di essere invocati, ma reagiscono a degli eventi (in questo caso, l'arrivo di un messaggio)

> [!definizione] message broker
> Un gestore di code di messaggi, specialmente nel modello publish/subscribe, viene definito **message broker** quando è in grado di eseguire logica applicativa sui messaggi che lo attraversano

Un message broker può, ad esempio, *trasformare i messaggi (cambiare formato dati o protocollo), effettuare il rerouting* dei messaggi (dirigerli verso canali diversi in base al contenuto), e *garantire la persistenza* dei messaggi, aumentando l'affidabilità e prevenendo la perdita di dati.

L'evoluzione dei modi di comunicazione tra applicazioni, da sistemi più accoppiati (tightly coupled) a quelli meno accoppiati (loosely coupled).

- Conversational: Scambi di informazioni con *sequenze hardcoded* all'interno dei programmi, con una perfetta sincronizzazione per l'intero scambio
  
- Request/Reply: *Scambio sincrono e hardcoded, ma costituito da una singola richiesta e una singola risposta*.
  > [!warning] 
  > Anche se le richieste HTTP sono asincrone dal punto di vista del trasporto, a livello concettuale spesso implementano un modello request/reply.
  
- Direct Message Passing: Il client invia un messaggio al server senza attendere una risposta, risultando in uno scambio tendenzialmente asincrono. *A differenza del request/reply, nel message passing non c'è una distinzione intrinseca tra richiesta e risposta; è simmetrico*.
- Message Queuing: *Introduce un **intermediario** (una coda di messaggi* gestita). Il mittente invia il messaggio al gestore della coda, e il destinatario deve esplicitamente richiedere al gestore se ci sono messaggi per lui. Questo aumenta il disaccoppiamento, permettendo anche che il destinatario non sia disponibile al momento dell'invio. Tuttavia, la coda è generalmente associata a un destinatario specifico
- Publish and Subscribe: Il mittente pubblica un messaggio su un certo "topic" (argomento), e *chiunque sia sottoscritto a quel topic può ricevere* i messaggi. La coda di messaggi diventa accessibile a più mittenti e più destinatari, simile a una "chat di gruppo" tra servizi.

# References
