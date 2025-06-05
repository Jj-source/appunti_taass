2025-06-05 14:35

Status: #child

Tags:
# GraphQL

*Linguaggio di query* che permette di *specificare esattamente quali informazioni ottenere da un'applicazione server*, inclusa la quantità, la struttura e la profondità.

| Caratteristica                                                                 | gRPC                                                                                                                                 | GraphQL                                                                                                                                 |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Tipo                                                                     | Protocollo di comunicazione                                                                                                                | Linguaggio di query                                                                                                   |
| Formato dei dati di risposta                                             | Dipende dall'implementazione, ma comunemente Protobuf                                                                                                                  | JSON                                                                                                                              |
| Orientamento                                                        | Comunicazione tra servizi                                                                                                                  | Ottenimento di dati                                                                                                                              |

![[graphql.png]]

Il server GraphQL espone uno schema che definisce le strutture dati disponibili
Il client invia una query GraphQL tramite HTTP, specificando i dati desiderati, e il server restituisce un oggetto JSON con esattamente quelle informazioni.
Un caso d'uso tipico di GraphQL è la comunicazione tra frontend e backend, spesso nello strato intermedio (BFF).
*A differenza di REST, dove ottenere dati correlati può richiedere multiple richieste HTTP, GraphQL permette di specificare in un'unica query la struttura dei dati desiderati, riducendo l'overhead e il recupero di dati non necessari*

# References
