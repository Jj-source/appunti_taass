2025-05-20 11:15

Status: #baby 

Tags: [[microservizi]]
# RabbitMQ

RabbitMQ è un message broker basato sul protocollo di messaggistica AMQP (Advanced Message Queuing Protocol)

è considerato un servizio di middleware installato su un host o
, in un'architettura a microservizi, è comune ospitarlo tramite un apposito Docker container.

`rabbitmq:4.1.0-management-alpine`, dove il tag -management indica che include l'utility di gestione web.

RabbitMQ espone diverse porte per la comunicazione con vari protocolli, ma ci concentriamo su 5672 (AMQP) e la 15672 (il tool management).

> [!tip]
> Quando si esegue l'immagine Docker, è utile assegnare un nome al container per facilitare la comunicazione con altri servizi e mappare le porte.

> [!tldr]
> Una caratteristica interessante di RabbitMQ è che è scritto in Erlang, un linguaggio funzionale concorrente sviluppato da Ericsson negli anni '80 per le infrastrutture di telecomunicazione, con caratteristiche come:
> - Processi concorrenti molto leggeri (lightweight)
> - alta tolleranza ai guasti (se un processo va in errore, Erlang (e quindi RabbitMQ) lo lascia "crashare" e ne avvia un altro)
> - Zero down time per gli upgrade
> - Implementazione di pattern di messaggistica resilienti, che sopravvivono a crash e rallentamenti

![[RabbitMQcore.png]]

*Producer e consumer sono solo ruoli, un microservizio può essere entrambi*.
**Exchange**: È il primo punto a cui i producer inviano i messaggi, si può immaginare come uno "scambio ferroviario" o uno snodo
*Routing Key*: Una stringa arbitraria specificata dal producer quando invia un messaggio a un exchange. Dà un'idea di "dove va il messaggio" ed è lo strumento per creare il matching tra producer e consumer.
*Binding Key*: Una stringa usata per collegare una coda a un exchange

Quando un producer invia un messaggio con una routing key, l'exchange lo invia solo alle code il cui binding key corrisponde alla routing key

I messaggi entrano nella coda e vengono gestiti in modo first in, first out (FIFO). Quando un consumer preleva un messaggio, dovrebbe inviare un acknowledgement (ACK) alla coda. Una volta ricevuto l'ACK, la coda elimina il messaggio considerandolo consumato con successo.

> [!info] NACK
> È possibile anche inviare un negative acknowledgement (NACK) in caso di errore durante l'elaborazione del messaggio: si può chiedere a RabbitMQ di ritentare (eventualmente indirizzando il messaggio ad un'altra istanza del servizio) o di metterlo in una dead letter queue

> [!importante]
> Con il sistema di routing key e binding key, RabbitMQ può implementare **sia il point-to-point messaging che il publish and subscribe**. La scelta dipende dalla configurazione: *se una routing key è associata a una sola coda con un solo consumer, si ha point-to-point; se è associata a tante code con tanti binding diversi, si ha publish/subscribe*.

È possibile che più producer scrivano sullo stesso exchange e che più consumer leggano dalla stessa coda. *Se più consumer leggono dalla stessa coda, agiscono come competing consumers* (che riucordiamo è scalabilità, permettendo a più istanze dello stesso servizio di gestire più richieste contemporaneamente)

> [!question] Round Robin e prefetch count
> RabbitMQ distribuisce i messaggi tra i competing consumers usando tendenzialmente il round robin: Se un consumer ha richieste "aperte" (non ancora confermate con ACK), RabbitMQ lo salta. il parametro prefetch count, che un consumer può configurare per sé stesso, indica quante richieste "aperte" può gestire prima di essere saltato nel round robin

Diversi utilizzi delle key:
- Direct Exchange : appena descritto.
- Default Exchange: È un direct exchange predefinito creato automaticamente da RabbitMQ usando il nome della coda come binding key. Questo rende il point-to-point messaging molto semplice, nascondendo l'exchange all'utilizzatore
- Fanout Exchange: **broadcasting puro.** *ignora completamente routing key e binding key*. Tutte le code che si sono legate a un fanout exchange (senza specificare una binding key) ricevono tutti i messaggi inviati a quell'exchange.
- Topic Exchange: un publish/subscribe basato su pattern. Le routing key per i topic exchange devono avere un formato specifico: sequenze di "parole" alfanumeriche (con opzionale trattino) separate da punti. Le binding key possono contenere wild card: l'asterisco (\*) che matcha una singola parola, e l'hash (#) che matcha zero o più parole: Questo permette a un singolo binding di *matchare più routing key*.
  Esempi di convenzioni di naming includono `servizio.azione`, `dominio.entità.operazione`, `environment.servizio.evento`

  > [!esempio]
  > usando un binding key *.payment.* con un topic exchange, un consumer riceverà tutti gli eventi relativi al servizio 'payment', indipendentemente dall'environment (dev, prod, ecc.) e dall'evento specifico

Si può mettere in auto-ack (cioè no ack) ma è rischioso.

Per la gestione degli errori legati a crash dell'intero broker, è fondamentale configurare le code come **durevoli**. Una coda durevole viene ricreata automaticamente quando RabbitMQ si riavvia. Tuttavia, per recuperare anche i messaggi che erano nelle code, il producer deve averli inviati chiedendo che siano persistenti (scritto su disco).

# References
