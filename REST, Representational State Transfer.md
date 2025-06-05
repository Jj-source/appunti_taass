2025-06-05 14:32

Status: #child 

Tags:
# REST, Representational State Transfer

A differenza di XML Schema che ha un corrispettivo concreto, **REST è più che altro una convenzione**, un modo di utilizzare il protocollo HTTP e le URL per costruire ed esporre le API di un'applicazione disponibile **tramite HTTP**.

*Non ci sono particolari vincoli sul tipo di dati che possiamo inviare, se non quelli stabiliti da HTTP stesso*, che ci permette di specificare il tipo di dato nell'header content-type. La maggior parte delle applicazioni RESTful preferisce il formato JSON per lo scambio di dati, anche se occasionalmente si può trovare anche l'XML (per i file più complessi come immagini o video, si usano encoding basati su stringa come il Base 64, il che però presenta lo svantaggio di aumentare le dimensioni dei dati trasmessi)
##### *Un servizio web che rispetta il paradigma REST è chiamato RESTful*
L'interfaccia API di un servizio RESTful è costituita da *un insieme di URL* (o URI) e dal modo in cui devono essere invocate (i metodi HTTP)

Quando un client effettua una richiesta a un server, utilizza una HTTP request, e la URL della richiesta è tendenzialmente formata da *più segmenti*. Alcuni segmenti possono *identificare il tipo di richiesta*, mentre altri possono essere utilizzati come *parametri* della richiesta. Possiamo avere i cosiddetti path segment per identificare i parametri (come nell'esempio `service/account/23`, dove 23 è un parametro) oppure le query string (la parte dopo il punto di domanda nella URL)

> [!caution] minimizzare l'utilizzo delle query string
> Una delle indicazioni di REST è di minimizzare l'utilizzo delle query string il più possibile

Un'altra caratteristica fondamentale di REST è che è molto *orientato al concetto di risorsa*: L'idea non è tanto eseguire delle funzioni, quanto accedere a delle risorse

L'idea non è tanto eseguire delle funzioni, quanto accedere a delle risorse:
- POST Crearne una nuova
- GET Ottenerne una già esistente
- PUT Aggiornare lo stato di una risorsa esistente
- DELETE Eliminare una risorsa esistente

Affinché un servizio web sia restful, *deve esserci una corrispondenza tra le operazioni esposte dalla sua API e questi metodi HTTP*.

> [!todo] HTTP codes standardizzati
> - una GET generica dovrebbe restituire un array di risorse con un codice di risposta 200 OK
> - Una POST che crea una nuova risorsa di solito restituisce la risorsa creata (magari con un ID assegnato dal server) con un codice 201 Created
> - Una DELETE di solito non restituisce niente e usa come standard la risposta 204 No Content

> [!abstract] microservizi
> Quando parliamo di microservizi su REST, *tendenzialmente ogni microservizio gestisce la propria risorsa*

> [!attention] l'approccio orientato alle risorse potrebbe non coprire tutte le necessità
> Ci potrebbero essere casi in cui vogliamo *invocare dei servizi più in stile RPC (Remote Procedure Call), cioè eseguire una funzione passando dei parametri*. In questi casi, *si utilizzano delle convenzioni per rimanere nel mondo RESTful*.
> Una di queste è che il path segment che identifica l'operazione non sarà più un nome di risorsa, ma un verbo, distinguendolo così dalle URL che accedono direttamente alle risorse. Il metodo HTTP utilizzato in questi casi dipenderà dalla natura dell'operazione: se si tratta di un'elaborazione o un calcolo, si tende ad usare il metodo GET, e i parametri dell'operazione vengono messi nella query string, se invece l'elaborazione prevede anche una manipolazione di risorse, si possono usare altri metodi come POST o PUT, soprattutto se è necessario inviare un body alla richiesta (cosa non prevista da GET e DELETE) per passare oggetti complessi.

Ci sono alcune guideline per la struttura delle URL (o URI) RESTful:
- Devono essere leggibili e intuitive, in modo che quando vediamo una URL dovremmo capire cosa fa
- Bisogna evitare di esporre le estensioni dei file, perché le URL RESTful sono logiche e non devono rivelare la tecnologia utilizzata
- Tutto dovrebbe essere in minuscolo, e si usano trattini o underscore al posto degli spazi
- Le query string andrebbero evitate il più possibile, e se fatte mantenute corte ed univoche.
- gestione di URL non corrispondenti: se una URL ricevuta è un prefisso di qualcosa che potrebbe avere senso (ad esempio, arriva una GET su `/service/account` quando ci si aspetta `/service/account/23` e il servizio non fornisce l'elenco di tutti gli account), invece di mandare un `errore 404 Not Found`, si potrebbe inviare un messaggio più specifico che indichi come proseguire (ad esempio, `Specifica l'ID dell'account`) o che l'operazione richiesta non è supportata
### REST vs SOAP
| Caratteristica                                | REST                                                                                                                                                                            | SOAP                                                                                                                                                             |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tipo                                          | Stile architetturale                                                                                                                                                            | Protocollo strutturato (con WSDL)                                                                                                                                |
| Protocollo di trasporto                       | Usa HTTP                                                                                                                                                                        | Non vincolato a HTTP, può usare altri protocolli                                                                                                                 |
| Formato dei dati di risposta                  | Normalmente JSON, ha sostituito XML, soprattutto con tecnologie server-side basate su JavaScript. JSON è preferito per la sua sinteticità e minor "boilerplate" rispetto a XML. | Tradizionalmente XML, soprattutto nel mondo Java                                                                                                                 |
| Tipo di richiesta                             | Espresso nella URI                                                                                                                                                              | Espresso nell'endpoint                                                                                                                                           |
| Separazione operazione logica/endpoint fisico | Operazione logica e endpoint fisico sono strettamente identificati; una URI RESTful dovrebbe essere logicamente comprensibile.                                                  | Operazione logica separata dall'endpoint fisico (definito nel WSDL); una URI potrebbe essere meno significativa semanticamente.                                  |
| Compatibilità con tecnologie client           | Più adatto ad essere contattato da tecnologie client, inclusi i browser tramite JavaScript                                                                                      | Può essere più complicato e richiedere librerie specifiche                                                                                                       |
| Supporto alla transazionalità                 | Deve essere implementata diversamente                                                                                                                                           | Supporta in automatico la transazionalità delle richieste usando il protocollo Two-Phase Commit                                                                  |
| “Consapevolezza”                              | HTTP, su cui si basa REST, è definito un protocollo "stupido" o "damb" perché non ha una conoscenza intrinseca di servizi o del tipo di dati che vengono trasportati            | Protocollo "intelligente" perché è consapevole di gestire scambi di informazioni tra web service per l'esecuzione di funzionalità e la restituzione di risultati |

# References
