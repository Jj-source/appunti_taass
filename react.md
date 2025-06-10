2025-06-08 15:39

Status: #baby 

Tags:
# react

React è una *libreria JavaScript*.


I **componenti** sono i mattoni fondamentali di ogni applicazione React. Permettono di creare tutte le parti visibili delle applicazioni, come bottoni, input o intere pagine. Possono essere riutilizzati più volte, come i mattoncini Lego. Ogni componente React è una *funzione JavaScript che restituisce markup*.

Invece del markup HTML standard, i componenti React restituiscono **JSX**. Il JSX è una sintassi che sembra JavaScript ma in realtà è JavaScript "travestito". È opzionale, ma l'alternativa (`createElement`) è meno pratica, quindi il JSX è ampiamente utilizzato. Poiché il JSX è JavaScript, gli attributi non si scrivono come in HTML; si usa lo **stile camel case**. Ad esempio, l'attributo HTML `class` diventa `className`.

A differenza dell'HTML, che è statico, il vantaggio di usare React è che si possono utilizzare *valori JavaScript dinamici nel JSX*. Per visualizzare dati nel JSX, si usano le parentesi graffe. Queste parentesi accettano direttamente valori come stringhe e numeri. Si possono usare anche per rendere gli attributi dinamici. 

Una funzione JavaScript può restituire solo una cosa, quindi in React un componente può restituire *un solo elemento genitore*. Per risolvere questo problema senza aggiungere un elemento extra come un `div`, si può usare un componente vuoto chiamato **React fragment**.

```React
<>
	<Header>
	<Body>
</>
```
#### Props
Per passare dati da un componente all'altro si usano le **props**. Per creare una prop, si definisce un nome sul componente a cui si vogliono passare i dati e gli si assegna un valore. Le props sono accessibili nei parametri del componente come proprietà su un oggetto. Si possono considerare come attributi personalizzati che si aggiungono a qualsiasi componente. È possibile passare qualsiasi cosa come prop.

`<Component text={'YO'} />`
E poi lo usi
`{props.text}`


Un tipo speciale di prop è la prop **`children`**. Se si usano tag di apertura e chiusura per un componente, si possono passare altri componenti al loro interno. Questi componenti passati sono chiamati "children" e sono accessibili tramite la prop `children` del componente genitore. Questo è utile per la **composition**, che riguarda l'organizzazione ottimale dei componenti React. La prop `children` è particolarmente utile per creare componenti di layout che forniscono una struttura comune ai loro figli.

```
<A>
	</B>
</A>
```
E poi accedi
`{props.children}`

Un'altra prop integrata di React è la prop **`key`**. Non ha funzionalità speciali come suggerisce il nome. La prop `key` è usata da React per distinguere un componente da un altro. Viene solitamente usata quando si crea una lista con la funzione `map`. Una key è semplicemente una stringa o un numero univoco per identificare un componente. React avverte nella console quando è necessario aggiungere una key. Se non si ha un valore univoco, si può usare l'indice corrente dalla funzione map.
#### Rendering
Il processo con cui React visualizza il codice nel browser è chiamato **rendering**. React lo fa automaticamente. È importante capire come funziona perché a volte si può causare un **infinite re-render**, che può bloccare l'applicazione.

Il modo in cui React sa come e quando fare il rendering dell'applicazione è usando il **Virtual DOM (vdom)**. Il **DOM** sta per *Document Object Model* ed è ciò che ogni browser usa per modellare gli elementi HTML di una pagina web. Graficamente, assomiglia a un albero.

Il processo di rendering in React funziona così:

1. Se lo **stato** dell'applicazione cambia, React aggiorna il **Virtual DOM**. *L'aggiornamento del Virtual DOM è più veloce rispetto al DOM reale.*
2. React usa un processo chiamato **diffing** per confrontare il Virtual DOM aggiornato con una versione precedente e vedere cosa è cambiato.
3. Una volta individuate le differenze, React usa un processo chiamato **reconciliation** per *aggiornare il DOM reale solo con le modifiche trovate.*
#### Events
Molti eventi si verificano quando gli utenti interagiscono con un'app, come click, movimenti del mouse e pressioni di tasti. La **gestione degli eventi (event handling)** è il modo in cui si reagisce a questi eventi dell'utente. React ha molti eventi integrati, come `onClick`, `onChange` e `onSubmit`, che sono tra i più usati. Per eseguire un'azione quando un bottone viene cliccato, si aggiungerebbe la prop `onClick` al bottone e la si connetterebbe a una funzione.

Per gestire i dati nelle app React, si usa lo **stato (state)**. Lo stato è come *un'istantanea dell'app in un dato momento*. 
*Non si usano variabili JavaScript standard per gestire lo stato perché non causano il re-render dell'app*. Si usano invece **funzioni speciali** come `useState` e `useReducer`. La funzione `useState` prende un argomento come valore iniziale dello stato e *restituisce un array contenente la variabile di stato e una funzione per aggiornare quello stato.*

![[Every React Concept Explained in 12 Minutes.jpeg]]

I **componenti controllati (controlled components)** utilizzano valori di stato per avere un comportamento più prevedibile. In un componente controllato, il valore digitato in un input, ad esempio, viene inserito nello stato e controllato da una variabile di stato. Cambiando lo stato che lo controlla, si cambia il comportamento del componente.
#### Hooks
Le funzioni come `useState` sono esempi di **React hooks**. Gli hooks permettono di *"agganciare" funzionalità* come lo stato all'interno dei componenti funzione. Ci sono cinque tipi principali di hooks:

- Hooks di stato (`useState`, `useReducer`) per gestire lo stato.
- Hooks di contesto (`useContext`) per usare dati passati tramite React context.
- Hooks di ref (`useRef`) per referenziare elementi come elementi HTML.
- Hooks di effetto (`useEffect`) per connettersi a sistemi esterni come le API del browser.
- Hooks di performance (`useMemo`, `useCallback`) per migliorare le prestazioni evitando lavori non necessari. 

La maggior parte delle volte si utilizzeranno probabilmente solo tre: `useState`, `useEffect` e `useRef`.

![[reactpurity.jpeg]]
La **purezza (purity)** è un termine usato per descrivere come dovrebbero funzionare i componenti React. Un componente React puro significa che *lo stesso input dovrebbe sempre restituire lo stesso output*. Per mantenere un componente puro, dovrebbe solo restituire il suo JSX e *non modificare oggetti o variabili esistenti al di fuori del componente* prima del rendering. La modifica di variabili esterne durante il rendering può portare a output incorretti quando il componente viene utilizzato più volte.

Per evitare errori legati alla purezza e altri problemi, si può usare lo **strict mode**. Lo strict mode è un componente speciale che avvisa degli errori durante lo sviluppo. Di solito si avvolge il componente principale dell'app nello strict mode.

![[reacteffects.jpeg]]
A volte è necessario "uscire" da React per interagire con sistemi esterni, come le API del browser o fare richieste a un server. Queste azioni sono chiamate **effetti (effects)** o side effects. Gli effetti possono essere gestiti all'interno degli event handlers. *Se un effetto non può essere eseguito in un event handler, si usa l'hook* **`useEffect`**. Un pattern comune è recuperare dati quando i componenti vengono caricati usando `useEffect`.

![[reactref.jpeg]]
Similmente agli effetti, a volte si vuole *interagire direttamente con il DOM reale*. Per referenziare un elemento DOM effettivo si usa un **ref**. Si crea un ref con l'hook **`useRef`** e si ottiene l'accesso all'elemento DOM usando la prop `ref` su un elemento React. Per alcuni compiti, come focalizzare un input, è più semplice referenziare l'elemento DOM effettivo piuttosto che tentare di farlo "alla React".

![[reactctx1.jpeg]]

![[reactctx2.jpeg]]

Il **context** è un modo potente per *passare dati* tra i componenti dell'app senza doverli passare come prop attraverso molti livelli (prop drilling). La maggior parte delle app React ha molti componenti nidificati, e il context permette di "saltare" l'albero dei componenti e usare i dati a qualsiasi livello. Per usare il context: 

![[reactctx3.jpeg]]

1. Si crea il context in un componente genitore.
2. Si avvolge il componente genitore in un componente speciale chiamato **context provider**.
3. Si inseriscono i dati che si vogliono passare sul provider.
4. Si accede a quei dati in qualsiasi componente figlio con l'hook **`useContext`**.

![[reactportals.jpeg]]
I **portals** sono simili al context, ma per i componenti. Permettono di *spostare componenti React in qualsiasi elemento HTML selezionato nel DOM*. I portals sono utili per componenti che non possono essere visualizzati correttamente a causa degli stili del loro componente genitore, come modali, menu a tendina e tooltip. Per creare un portal si usa la funzione **`createPortal`**, passandogli il componente e l'elemento HTML di destinazione.

**Suspense** è un componente speciale che aiuta a gestire il caricamento di un componente o dei suoi dati. È utile per componenti che impiegano tempo a recuperare dati. Offre una migliore esperienza utente mostrando un componente di fallback (come uno spinner di caricamento) finché i dati non sono disponibili. Suspense è utile anche per il lazy loading di componenti, che permette di caricarli solo quando necessario.

Poiché le app React sono basate su JavaScript, *gli errori che si verificano durante il rendering possono bloccare completamente l'app*. Gli **error boundaries** sono componenti che permettono di catturare questi errori critici e mostrare un componente di fallback all'utente. Ad esempio, per evitare che l'app si blocchi a causa di un errore di rendering, si aggiunge un error boundary per visualizzare un messaggio più utile all'utente.

# References

https://www.youtube.com/watch?v=wIyHSOugGGw