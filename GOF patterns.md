2025-03-04 14:51

Status: #adult 

Tags: [[SAS]]
# GOF patterns
## Comportamentali
> [!success] 1. Observer
> - Nome: Observer
> - Problema: Diversi tipi di oggetti subscriber (abbonato) sono interessati ai cambiamenti di stato o agli eventi di un oggetto publisher (editore). Ciascun subscriber vuole reagire in un suo modo proprio quando il publisher genera un evento. Inoltre, il publisher vuole mantenere un accoppiamento basso verso i subscriber. Che cosa fare?
> - Soluzione: Definisci un’interfaccia subscriber o listener (ascoltatore). Gli oggetti subscriber implementano questa interfaccia. Il publisher registra dinamicamente i subscriber che sono interessati ai suoi eventi, e li avvisa quando si verifica un evento

- Definisce una dipendenza tra oggetti di tipo uno-a-molti: quando lo stato di un oggetto cambia, tale evento viene notificato a tutti gli oggetti dipendenti, essi vengono automaticamente aggiornati
- L’oggetto che notifica il cambiamento di stato non fa alcuna assunzione sulla natura degli oggetti notificati: le due tipologie di oggetti sono disacoppiati
- Il numero degli oggetti affetti dal cambiamento di stato di un oggetto non è noto a priori
- Fornisce un modo per accoppiare in maniera debole degli oggetti che devono comunicare (eventi). I publisher conoscono i subscriber solo attraverso un’interfaccia, e i subscriber possono registrarsi (o cancellare la propria registrazione) dinamicamente con il publisher
Spesso associato al pattern architetturale Model-View-Controller (MVC): le modifiche al modello sono notificate agli osservatori che sono le viste.

![[GOFobserver.pdf]]

> [!success] 2. State
> - Nome: State
> - Problema: Il comportamento di un oggetto dipende da suo stato e i suoi metodi contengono logica condizionale per casi che riflette le azioni condizionali che dipendono dallo stato. C’è un’alternativa alla logica condizionale?
> - Soluzione: Crea delle classi stato per ciascuno stato, che implementano un’interfaccia comune. Delega le operazioni che dipendono dallo stato dall’oggetto contesto all’oggetto stato corrente corrispondente. Assicura che l’oggetto contesto referenzi sempre un oggetto stato che riflette il suo stato corrente

Permette ad un oggetto di modificare il suo comportamento quando cambia il suo stato interno
![[GOFstate.pdf]]

> [!success] 3. Strategy
> - Nome: Strategy
> - Problema: Come progettare per gestire un insieme di algoritmi o politiche variabili ma correlati? Come progettare per consentire di modificare questi algoritmi o politiche?
> - Soluzione: Definisci ciascun algoritmo / politica / strategia in una classe separata, con un’interfaccia comune

L’oggetto contesto, quello a cui va applicato l’algoritmo, è associato a un oggetto strategia, che è l’oggetto che implementa un algoritmo
#### Lati positivi
- Consente la definizione di una famiglia di algoritmi, incapsula ognuno e li rende intercambiabili tra di loro
- Permette di modificare gli algoritmi in modo indipendente dai clienti che fanno uso di essi 
- Disaccoppia gli algoritmi dai clienti che vogliono usarli dinamicamente
- Permette che un oggetto client possa usare indifferentemente uno o l’altro algoritmo 
- è utile dove è necessario modificare il comportamento a runtime di una classe 
- Usa la composizione invece dell’ereditarietà: i comportamenti di una classe non dovrebbero essere ereditati ma piuttosto incapsulati usando la dichiarazione di interfaccia

![[GOFstrategy.pdf]]

> [!success] 5. Visitor
> - Nome: Visitor
> - Problema: Come separare l’operazione applicata su un contenitore complesso dalla struttura dati cui è applicata? Come poter aggiungere nuove operazioni e comportamenti senza dover modificare la struttura stessa? Come attraversare il contenitore complesso i cui elementi sono eterogenei applicando azioni dipendenti dal tipo degli elementi?
> - Soluzione: : Creare un oggetto (ConcreteVisitor) che è in grado di percorrere la collezione, e di applicare un metodo proprio su ogni oggetto (Element) visitato nella collezione (avendo un riferimento a questi ultimi come parametro). Ogni oggetto della collezione aderisce ad un’interfaccia (Visitable) che consente al ConcreteVisitor di essere accettato da parte di ogni Element. Il Visitor analizza il tipo di oggetto ricevuto, fa l’invocazione alla particolare operazione che deve eseguire.

![[GOFvisitor.pdf]] 
## Applicazione di ciò
![[SASdalprogettoalcodice.pdf]]