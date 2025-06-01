2025-05-20 12:10

Status: #baby 

Tags: [[microservizi]]
# Kubernetes

Kubernetes è un orchestratore di applicazioni a microservizi.
Necessità: robustezza, alta affidabilità (essere quasi sempre accessibili), scalabilità.

Nasce come progetto open source da Google poi donato alla Cloud Native Computing Foundation nel 2014.

semplifica enormemente il deployment sia in locale che in rete, su installazioni on-premises (nella rete aziendale) o su cloud pubblici.

> [!curiosita]
> Il nome "Kubernetes" deriva dalla parola greca che significa "timoniere" o "capitano di una nave" (ed ha sette raggi come citazione ad un personaggio di Star Trek)

Laddove prima il cloud era visto come una rete di computer interconnessi, *con Kubernetes è come se l'astrazione fosse a un livello superiore*: **possiamo immaginare il cloud come un mega computer e Kubernetes come il suo sistema operativo**. Ciò che c'è "sotto" (il numero o il tipo di macchine, Windows o Linux, fisiche o virtuali) è nascosto dall'utente.

Il funzionamento base di un deployment con Kubernetes coinvolge:
1. Le immagini dei container dei servizi (realizzate magari con Docker)3.
2. Un file di configurazione (chiamato manifest), simile a un file YAML di Docker Compose, che specifica lo stato desiderato (desired state)

Kubernetes poi:
- Esegue le applicazioni
- Gestisce la loro interazione con l’ambiente esterno
- Fornisce l’*infrastruttra di gestione dei servizi* o permette di pluggarli all’interno.
- Monitoraggio real time
- Rispondere a eventi in real time (scalare)
- Eseguire load balancing
- Gestire i fallimenti e garantire l’alta disponibilità

> [!important] modello dichiarativo
> l'utente *non istruisce Kubernetes su cosa fare (modello imperativo)*, **esprime lo stato desiderato** nel file di configurazione (manifest) e kubernetes lo attua tramite la **reconciliation**:
> Ad esempio, specificando di volere quattro repliche di un microservizio in parallelo, Kubernetes decide autonomamente come fare per mantenere questo stato. Componenti di Kubernetes osservano continuamente l'andamento e, se l'applicazione devia dallo stato desiderato (es. una replica si blocca), cercano di ripristinarlo (es. riavviando la replica)

Un **Kubernetes Cluster** è fatto di nodi, dove ogni nodo corrisponde tendenzialmente a una macchina. (Per il progetto del corso si userà MiniKube, un'installazione locale con un solo nodo)

I nodi si dividono in due ruoli (un nodo può avere entrambi):
1. **Control Plane Nodes**: Eseguono le parti di Kubernetes che servono a monitorare e gestire gli altri nodi. Ne serve almeno 1!
   I servizi cloud se ne fanno carico da soli.
2. **Worker Nodes** su cui girano effettivamente i microservizi containerizzati

![[Kubernetes_controlnode.png]]
I componenti principali di un Control Plane Node sono:
- API Server: Il frontend del control plane. Espone una REST API per interagire con il control plane (da altri nodi o dall'amministratore).
- Cluster Store: Un database NoSQL basato su coppie chiave-valore (di default etcd), usato per mantenere persistenti lo stato e la configurazione del cluster e dei nodi gestiti dal control plane.
- Controller Manager: Il supervisore di tutti i moduli del control plane che si occupano della state reconciliation. *Cerca di far corrispondere lo stato osservato del cluster e dei container con lo stato desiderato*. 
  I controller sono i mattoni base di Kubernetes; ci sono controller per quasi tutto: Monitorano lo stato, vedono se si discosta dal desired state e intraprendono azioni per riportarvelo. Sono i controller che rendono le applicazioni dispiegate tramite Kubernetes self-healing (si riparano da sole). Ad esempio, un controller si occupa di creare repliche di un container o farlo ripartire se si è fermato.
- Scheduler: Resta in ascolto dei task da eseguire (deployment di container) e li assegna ai worker nodes. possono esserci regole sofisticate che stabiliscono preferenze, attrazioni o repellenze tra container o nodi.

La *High Availability (HA)* è un principio fondamentale per il control plane: se il control plane cade, non funzionano più non solo l'applicazione, ma tutte quelle che girano sul cluster
→ si possono usare più Control Plane Nodes: uno è il leader, e se il leader cade, un altro deve diventare leader. 

I nodi multipli dovrebbero essere posizionati in diversi failure domains (aree che potrebbero fallire insieme). 

È importante avere un numero dispari di Control Plane Nodes perché le decisioni sulla reconciliation vengono prese a maggioranza
Avere un numero pari potrebbe portare allo *split brain*, dove due gruppi di nodi prendono decisioni diverse senza una maggioranza chiara. 

Se un nodo non ottiene la maggioranza, va in read only mode. Le applicazioni continuano a funzionare, ma non è più possibile modificarne il desired state (scalare, fare load balancing, ecc.).

Per la maggior parte delle applicazioni, tre Control Plane Nodes sono sufficienti; cinque sono considerati per situazioni estreme ("paranoico").

I Worker Nodes contengono:
- *Kubelet: Il runtime di Kubernetes* sul singolo nodo worker. Registra il nodo nel cluster e comunica con l'API server del control plane per riportare sull'andamento dell'esecuzione.
- *Container Runtime: È ciò che esegue effettivamente i container*. Fino a poco tempo fa era Docker per default, ma ora Kubernetes permette di usare diversi runtime (purché implementino la Container Runtime Interface) e di default usa containerd (lo stesso usato da Docker)
- Cube Proxy: Gestisce gli aspetti di rete. Ogni unità applicativa (vedremo: i pod) all'interno di un worker node ha un IP virtuale. Il kube proxy gestisce la comunicazione, reindirizzando il traffico in arrivo sulla macchina fisica ai pod interni tramite i loro IP virtuali.
### POD
L'unità atomica di scheduling in Kubernetes è il Pod.

> [!definizione] Pod
> Un pod è un wrapper intorno a uno o più container. Di fatto, un pod è un ambiente di esecuzione. Offre un ulteriore livello di isolamento rispetto al container stesso

> [!summary] 
> Quando si chiede a Kubernetes di eseguire qualcosa, si chiede di eseguire un pod

> [!important]
> *Container all'interno dello stesso pod* si vedono come *"local"* (sulla stessa macchina) e condividono risorse come lo spazio su disco (tramite volumi montati)

![[Kubernetes_pod.png]]

L'IP viene assegnato al pod, non ai singoli container al suo interno.

Quando Kubernetes replica un microservizio, replica l'intero pod, non solo il container.

Quando un pod viene dispiegato, resta in stato pending finché tutto al suo interno non è in esecuzione.... Solo allora può ricevere richieste.
Un pod può terminare (con successo o fallimento) o restare in esecuzione indefinitamente

*Quando ha senso avere più container nello stesso pod?* Questo non è frequente e per l'uso nel progetto del corso probabilmente non accadrà
Idealmente, un microservizio corrisponde a un container e i microservizi sono loosely coupled (non condividono risorse)!
*Un caso è con l'uso di un Service Mesh*. Il service mesh (utilizzato per gestire problemi come il rallentamento o il fallimento della rete nelle comunicazioni sincrone, ad esempio REST) inietta un proxy davanti a ogni microservizio. Questo proxy (un container aggiuntivo) fa parte dello stesso pod del microservizio principale: ogni pod conterrebbe due containers!

> [!summary] Deployment
> Fornisci l’immagine del container ed il manifest yaml per il desired state e fa tutto lui

> [!abstract]
> Quando si aggiorna l'immagine del servizio a una nuova versione con zero downtime, Kubernetes crea nuovi pod con la nuova immagine, li mette in esecuzione e solo quando sono pronti sostituisce i vecchi pod

> [!importante]
> *self-healing (autoguarigione) e scalabilità, sono proprietà del Deployment non del Pod*. Un pod, da solo, o funziona o non funziona. È il deployment che, vedendo che un pod non funziona o che c'è bisogno di più pod per scalare, tira su nuove repliche del pod

# References
