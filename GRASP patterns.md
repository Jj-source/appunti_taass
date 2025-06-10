2025-03-04 14:19

Status: #adult

Tags: [[SAS]]
# GRASP patterns

> [!summary]
> L’approccio complessivo al fare la modellazione per la progettazione OO si basera sulla metafora della *progettazione guidata dalle responsabilita* (RDD), ovvero pensare a come assegnare le responsabilita a degli oggetti che collaborano.

Le *responsabilita di fare* di un oggetto comprendono:
- fare qualcosa esso stesso, come per esempio creare un oggetto o eseguire un calcolo
- chiedere ad altri oggetti di eseguire azioni
- controllare e coordinare le attivita di altri oggetti
  
Le *responsabilita di conoscere* di un oggetto comprendono:
- conoscere i propri dati privati incapsulati
- conoscere gli oggetti correlati
- conoscere cose che puo derivare o calcolare

Le responsabilita sono assegnate alle classi di oggetti durante la progettazione a oggetti, aiutandosi con i pattern GRASP.

> [!important] Low Representational Gap (LRG)
> Inoltre, nella fase di progettazione, vale sempre il principio LRG, **Low Representational Gap**, o salto rappresentazionale basso, *tra il modo in cui si pensa al dominio e una corrispondenza diretta con gli oggetti software*
## I pattern

> [!success] 1. Creator
> - Nome: Creator (Creatore)
> - Problema: Chi crea un oggetto A? Ovvero, chi deve essere responsabile della creazione di una nuova istanza di una classe?
> - Soluzione: Assegna alla classe B la responsabilita di creare un’istanza della classe A se una delle seguenti condizioni e vera (piu sono vere meglio e):
> 	- B “contiene” o aggrega con una composizione oggetti di tipo A
> 	- B registra A2
> 	- B utilizza strettamente A 
> 	- B possiede i dati per l’inizializzazione di A, che saranno passati ad A al momento della sua creazione (pertanto B e un Expert rispetto alla creazione di A)

Ex) nel monopoli, la classe (campo da gioco) sarà creator della classe (casella)

> [!success] 2. Information Expert
> - Nome: Information Expert (Esperto delle Informazioni)
> - Problema: Qual è un principio di base, generale, per l’assegnazione di responsabilità agli oggetti?
> - Soluzione: Assegna una responsabilità alla classe che possiede le informazioni necessarie per soddisfarla, all’esperto delle informazioni, ovvero alla classe che possiede le informazioni necessarie per soddisfare la responsabilità

Ex) nella transazione del supermercato, la classe (vendità) sarà expert della classe (SalesLineItem) che contiene.
Nel monopoly, board è esperto di square (poichè li aggrega e ne conosce le caratteristiche)

> [!success] 3. Low Coupling
> - Nome: Low Coupling
> - Problema: Come ridurre l’impatto dei cambiamenti? Come sostenere una dipendenza bassa, un impatto dei cambiamenti basso e una maggiore opportunità di riuso?
> - Soluzione: Assegna le responsabilità in modo tale che l’accoppiamento (non necessario) rimanga basso. Usa questo principio per valutare le alternative.

![[lowCouplingEx.pdf]]

Il problema infatti non è l’accoppiamento alto di per s’è, ma l’accoppiamento alto con elementi per certi aspetti instabili, per esempio nell’interfaccia, nell’implementazione o per loro pura e semplice presenza

Una classe o componente con un accoppiamento basso non è influenzata dai cambiamenti nelle altre classi e componenti, è semplice da capire separatamente dalle altre classi e componenti, è conveniente da riusare

> [!success] 4. High Coesion
> - Nome: High Coesion
> - Problema: Come mantenere gli oggetti focalizzati, comprensibili e gestibili e, come effetto collaterale, sostenere Low Coupling?
> - Soluzione: Assegna le responsabilità in modo tale che la coesione rimanga alta. Usa questo principio per valutare alternative.

Stesso esempio del Low Coupling
→ Sono due patterns di **progettazione modulare**

Livelli di coesione:
- Coesione *di dati*: una classe implementa un tipo di dati (molto buona)
- Coesione *funzionale*: gli elementi di una classe svolgono una singola funzione (buona o molto buona) 
- Coesione *temporale*: gli elementi sono raggruppati perch´e usati circa nello stesso tempo (es. controller, a volte buona a volte meno)
- Coesione *per pura coincidenza*: es. una classe usata per raggruppare tutti i metodi il cui nome inizia per una certa lettera dell’alfabeto (molto cattiva)
  
> [!summary]
>  In generale, un elemento ha coesione alta se ha responsabilità (funzionali) altamente correlate e se “non svolge troppo lavoro”. Un elemento ha coesione bassa se fa molte cose scorrelate o se svolge troppo lavoro

La coesione è una misura di quanto sono correlate le responsabilità di un elemento software.
- Coesione molto bassa: una classe è la sola responsabile di molte cose in aree funzionali molto diverse
- Coesione bassa: una classe ha da sola la responsabilità di un compito complesso in una sola area funzionale
- Coesione alta: una classe ha responsabilità moderate in un’area funzionale e collabora con altre classi per svolgere i suoi compiti
- Coesione moderata: una classe ha, da sola, responsabilità in poche aree diverse, che sono logicamente correlate al concetto rappresentato dalla classe, ma non l’una all’altra
  Esempio: una classe Company che è completamente responsabile di conoscere i suoi dipendenti e conoscere le proprie informazioni finanziarie, queste non sono aree correlate anche se entrambe sono logicamente legate al concetto di una Company

> [!success] 5. Controller
> - Nome: Controller
> - Problema: Qual è il primo oggetto oltre lo strato UI che riceve e coordina (“controlla”) un’operazione di sistema?
> - Soluzione: Assegna la responsabilità a un oggetto che rappresenta una delle seguenti scelte:
> 	1. **facade controller** rappresenta il “sistema” complessivo, un “oggetto radice”, un dispositivo all’interno del quale viene eseguito il software, un punto di accesso al software o un sottosistema principale (variante del facade controller)
> 	2. **controller di caso d’uso** rappresenta uno scenario di un caso d’uso all’interno del quale si verifica l’operazione di sistema (un controller di caso d’uso o controller di sessione)

> [!caution]
> Nota: *le classi dello strato UI* (le classi “finestre”, “viste” e “documenti”) **non sono Controller**, non devono svolgere i compiti associati agli eventi di sistema, ma normalmente ricevono questi eventi e li delegano a un controller

> [!idea]
> Utilizzare la stessa classe controller per tutti gli eventi di sistema di un unico caso d’uso, in questo modo il controller può conservare le informazioni sullo stato del caso d’uso.

I *facade controller* Sono adatti quando non ci sono “troppi” eventi di sistema o quando l’interfaccia utente UI non può reindirizzare i messaggi per gli eventi di sistema a più controller alternativi.
I *controller di caso d’uso* Lo si sceglie quando la collocazione delle responsabilità in un facade controller porta a progetti con coesione bassa o accoppiamento alto, ovvero quando il facade controller diventa “gonfio” di eccessive responsabilità

![[graspEsempi.pdf]]