2025-06-05 14:28

Status: #child

Tags:
# Legacy Code - SW architetture

Vecchie ma in azienda potrebbero esserci, le spolveriamo.
- *Grande eterogeneità* di strumenti, linguaggi, formati di dati e infrastrutture. Immagina un'azienda con sistemi informativi distribuiti su diverse sedi, magari nati in momenti diversi con tecnologie differenti. In questo contesto, è molto comune imbattersi nel legacy software
- Oggi, la maggior parte delle infrastrutture software, sia aziendali che non, si basa su reti che utilizzano il protocollo TCP/IP, e gran parte del software applicativo si appoggia sul protocollo HTTP. Tuttavia, *in passato, non esisteva questa standardizzazione e uniformità di reti e protocolli*. La rete era essenzialmente un cavo, e ciò che veniva trasmesso su quel cavo era gestito in maniera indipendente. Questo portò alla proliferazione di protocolli di rete customizzati.

![[legacy.png]]

Diversi applicativi che girano in un contesto di rete. Al centro quelli su cui si regge il business, il secondo cerchio sono gli applicativi aggiunti per rendere disponibile la digitalizzazione di alcuni servizi ex) per uniTO “f3” che gestisce registrazione ad esami.

![[legacy2.png]]

Tre principali problematiche legate all'integrazione di applicazioni enterprise:
- Data consistency: garantire che i dati siano coerenti in sistemi diversi.
  L'esempio dei registri cartacei e degli statini universitari illustra bene la difficoltà di mantenere la stessa informazione (dati degli studenti, voti degli esami) in due posti diversi (il registro del docente e il libretto dello studente), dove la responsabilità della coerenza ricadeva sul singolo individuo.
  Il problema delle aule che risultavano occupate su un database e libere su un altro evidenzia come la mancanza di integrazione possa portare a incoerenze
- Multistep processes: coordinare attività aziendali che seguono una logica di processo con fasi ben precise e dipendenze tra applicativi.
  L'esempio del nuovo sistema di gestione delle domande di laurea all'Università di Torino: prevede diverse fasi, dall'inserimento della richiesta da parte dello studente, all'approvazione del titolo da parte del docente, all'assegnazione formale, alla presentazione della domanda di laurea vera e propria, fino all'invio dell'elaborato finale e all'approvazione finale del relatore. Ogni fase può coinvolgere diverse applicazioni o moduli software, e il corretto svolgimento dell'intero processo dipende dalla sincronizzazione e dal passaggio di informazioni tra questi diversi componenti
- Composite applications: integrare applicativi separati in un'unica applicazione per fornire un front-end unificato.
  Se implementato male, l'utente si troverà semplicemente di fronte a una serie di pulsanti che lo reindirizzano a diverse applicazioni separate, come spesso accade con alcune applicazioni dell'ateneo (biblioteche, pubblicazioni scientifiche)

Prima ogni dipendente aveva installato i programmi, se volevi usare un programma forse dovevi pure andare dal terminale giusto.
L’architettura client / server risolve questo problema anche.
Si parla di applicativi basati sui dati, non che fanno calcoli o altro.

L'avvento del modello client-server ha rappresentato un punto di partenza per le soluzioni integrate, portando all'idea di **architetture a strati**, tra i principali:
- ***Presentation**: l'interfaccia con cui l'utente interagisce e che presenta i dati*. Il concetto di presentation possa estendersi anche ad applicazioni che offrono servizi ad altre applicazioni, dove la "presentazione" dei dati può avvenire tramite formati come JSON o XML.
- ***Business logic**: la gestione della logica dei dati, la loro consistenza, validazione ed elaborazione*....
- ***Data management**: la gestione della persistenza e della consistenza dei dati*

La suddivisione tra frontend e backend è una distinzione logica basata sul ruolo di un modulo applicativo: orientato all'utente (frontend) o alla gestione dei dati (backend), lo strato di business logic si colloca a metà, con servizi che possono essere più vicini al frontend o al backend a seconda della loro funzione
#### Come si distribuiscono i 3 strati in architetture client-server?
- Si parte da modelli arcaici dove tutto risiedeva sul server e i client erano semplici terminali senza capacità di elaborazione (come i laboratori Unix con terminali collegati a un mainframe)
- L'evoluzione ha portato a client con una limitata capacità di elaborazione per la gestione dell'interfaccia grafica (come gli X terminal)
- Un modello ancora attuale è quello dell'applicazione distribuita, tipico delle applicazioni web moderne, dove il server ospita i dati e parte della logica applicativa, offrendo servizi che vengono utilizzati da un client con piena capacità di elaborazione, in grado di eseguire logica lato client e di gestire la presentazione
- Un altro modello prevede che l'intero applicativo risieda sul client, interagendo con un database centrale unicamente per i dati tramite query SQL. Detta “*fat client*” presentava problemi di manutenzione costosa e sovraccarico del server. Per mitigare sono state introdotte soluzioni come le *stored procedure* (procedure memorizzate sul server che riducono il numero di connessioni di rete, ma limitano la portabilità) e la *replicazione asincrona dei database* (copie dei dati per migliorare scalabilità ed efficienza geografica, con implicazioni sull'integrità transazionale).
##### *Database centralizzato*
Un approccio iniziale per la gestione dei dati è stato quello del database centralizzato, dove tutti gli applicativi fanno riferimento a un unico grande database

   > [!success] PRO
   > appoggiarsi a prodotti consolidati
   > linguaggio standard di interrogazione come SQL
   > standardizzazione
   
> [!failure] Contro
> Limiti di scalabilità

# References
