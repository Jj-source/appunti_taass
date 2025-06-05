2025-06-05 14:34

Status: #child 

Tags:
# Google Remote Procedure Call (gRPC)

In alcuni casi può essere più opportuno *orientare l'API di un servizio all'esecuzione di una funzione, richiamando il concetto di Remote Procedure Call (RPC) a un livello più alto* rispetto al passato.

> [!definizioneviola] gRPC
> Protocollo di comunicazione **free open source** ed un'implementazione di RPC progettata *specificamente per la comunicazione tra microservizi* (a differenza di REST, nato per esporre API consumabili anche da browser). Si basa su HTTP2 e non è adatto per la comunicazione diretta tra client (browser) e server, in quanto richiederebbe un'implementazione GRPC all'interno del browser

> [!idea]
> Un servizio client invoca una funzione su un servizio server come se fosse una funzione locale, ricevendo una risposta (Simple RPC)
##### GRPC è uno dei sistemi di comunicazione diretta tra servizi, in particolare tra microservizi, insieme a REST
A volte ha senso che un servizio invochi direttamente un altro usando REST (se l'altro servizio esiste già con un'API REST), mentre altre volte, costruendo servizi ad hoc per interagire tra loro, può essere più sensato usare gRPC.

Per comunicazioni asincrone e più "loose" tra cluster di servizi indipendenti, si preferisce il message broker.

gRPC oltre alla *simple RPC* supporta altri stili di comunicazione: *server-side streaming* (il server invia continuamente dati al client), *client-side streaming* (il client invia continuamente dati al server) e *streaming bidirezionale* (entrambi inviano e ricevono stream di dati indipendenti)

![[grpc.png]]
Per l'esecuzione è necessario implementare il servizio specifico e un server gRPC in ascolto su una porta TCP.
Dal lato client, è necessaria una componente che riceve le comunicazioni (channel) e un client gRPC che permette l'invocazione della funzione remota. *Gran parte del lavoro "tedioso" è gestito da gRPC stesso tramite eseguibili e librerie*. Il programmatore deve descrivere il servizio e come deve essere invocato tramite i **Protocol Buffers**, che fungono da Interface Description Language (IDL).

> [!definizione] Protocol Buffers
> *Formato di serializzazione dei dati binario* (più efficiente per la trasmissione dei dati rispetto al json usato da REST), a cui si accompagna un linguaggio di specifica.
> **definisce la struttura dei messaggi** (tipi di dati) che vengono **scambiati tra client e server**.
> Utilizzando il compilatore protoC per uno specifico linguaggio, a partire dalla descrizione dello schema vengono dichiarati i tipi di dati corrispondenti, creati gli strumenti per costruire gli oggetti e generato il codice per la serializzazione e deserializzazione.

 ! *differenza fondamentale rispetto a REST*, che tipicamente usa formati testuali come XML o JSON.
 Mentre JSON non ha uno schema, i Protocol Buffers sono più simili a XML in quanto definiscono uno schema che struttura e vincola i tipi di dati scambiati
 
![[grpccode.png]]

Lo stesso linguaggio dei Protocol Buffers viene usato per descrivere un *servizio GRPC come una* *collezione di procedure* (RPC), ognuna definita con la keyword rpc, il nome della procedura, il tipo di messaggio in input e il tipo di messaggio in output.
I quattro tipi di comunicazione GRPC si ottengono combinando la possibilità per la procedura di inviare/ricevere un singolo messaggio o uno stream di messaggi.

> [!done] Language indipendent
> Per sviluppare servizi GRPC in un determinato linguaggio, è necessario scaricare il compilatore e le librerie specifiche.
> Il file .proto (il formato del Protocol Buffer schema) è l'IDL per GRPC. Il compilatore genera degli "stub" sia per il client che per il server, all'interno dei quali è possibile utilizzare classi, funzioni e moduli di libreria per implementare la logica del servizio

![[grpcaschiutettura+.png]]

In un'architettura GRPC, laddove un servizio vuole usare le funzionalità di un altro, *deve contenere un GRPC client* (ad esempio, il servizio "orders" ha un GRPC client per comunicare con "product catalog").
Per quanto riguarda il frontend (browser, mobile), *in un'architettura REST si può avere un API Gateway che riceve le richieste e le indirizza al servizio appropriato senza ulteriore complessità, invece con gRPC i browser **non** sono in grado di effettuare direttamente richieste gRPC*. *È necessario uno **strato intermedio*** che traduca le richieste provenienti dal frontend (tipicamente REST) in chiamate gRPC verso i microservizi. Questo strato intermedio può includere altri microservizi dedicati alle richieste web e mobile. Quando l'API Gateway assume questo ruolo più complesso, si parla di *Backend For Frontend (BFF)*.

# References
