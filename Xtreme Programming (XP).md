2025-02-27 14:19

Status: #baby 

Tags: [[Programmazione Agile]] [[SAS]]
# Xtreme Programming (XP)

![[XtremeProgramming.png]]

Extreme Programming (XP) è una *metodologia agile di sviluppo software* che enfatizza la collaborazione, la flessibilità e la qualità del codice attraverso pratiche rigorose. È stata sviluppata da Kent Beck negli anni '90 per migliorare l'efficacia dei team di sviluppo in contesti di alta variabilità e requisiti mutevoli.
### Principi chiave di XP
1. **Comunicazione** – Favorire il dialogo continuo tra i membri del team.
2. **Semplicità** – Scrivere il codice più semplice possibile che funzioni.
3. **Feedback** – Ricevere rapidamente riscontri dai test e dagli stakeholder.
4. **Coraggio** – Essere pronti a modificare il codice senza paura, grazie ai test automatizzati.
5. **Rispetto** – Collaborazione e fiducia reciproca tra i membri del team.
### Pratiche principali
- **Sviluppo iterativo e incrementale** – Rilasci frequenti di nuove funzionalità in brevi cicli di sviluppo.
- **Test-Driven Development (TDD)** [^1] – Scrivere i test prima del codice per garantire qualità e manutenibilità.
- **Pair Programming** – Due sviluppatori lavorano insieme sulla stessa porzione di codice per ridurre errori e migliorare la progettazione.
- **Continuous Integration** – Il codice viene integrato frequentemente per evitare problemi di merge e rilevare bug rapidamente.
- **Refactoring** – Migliorare continuamente la qualità del codice senza alterarne il comportamento.
- **User Story** – Requisiti descritti in modo semplice e comprensibile per il team.
- **Metafore di progetto** – Un linguaggio condiviso per descrivere il sistema in termini comprensibili a tutti.
- **Sustainable Pace (40-hour workweek)** – Evitare straordinari eccessivi per garantire efficienza a lungo termine.
- **Proprietà collettiva del codice** – Tutti nel team possono modificare qualsiasi parte del codice.
### Quando usare XP?
XP è ideale in contesti con:
- Requisiti che cambiano frequentemente.
- Team piccoli e altamente collaborativi.
- Necessità di alta qualità e tempi di sviluppo brevi.

> [!warning]
> Se il progetto richiede una documentazione dettagliata e rigidamente strutturata, XP potrebbe non essere la scelta migliore.
## Fasi
Extreme Programming (XP) segue un ciclo di sviluppo iterativo e incrementale, organizzato in **fasi ben definite**

> [!check] 1. *Pianificazione (Planning)*
> **Definire i requisiti e stabilire le priorità**. Coinvolge il team di sviluppo e il *cliente*.

- **User Stories**: descrizioni semplici e concise di funzionalità dal punto di vista dell’utente finale. Servono a comunicare in modo chiaro ciò che deve essere sviluppato senza scendere nei dettagli tecnici.

> Come \[tipo di utente], voglio \[azione/obiettivo] in modo da \[beneficio/valore].

Esempio:

> Come cliente, voglio poter recuperare la mia password in modo da accedere al mio account anche se la dimentico.

- **Assegnazione delle priorità**: Il cliente decide quali storie sono più importanti.
- **Stima dello sforzo**: Il team stima il tempo necessario per implementare ogni storia utente.
- Suddivisione in iterazioni: Si pianificano cicli brevi (1-2 settimane) in cui verranno sviluppate e rilasciate le funzionalità.
  
> [!check] 2. Progettazione (Design)
> L'obiettivo è mantenere il design il più semplice possibile e flessibile per future modifiche.

- Metafore di progetto: Si definisce *un linguaggio condiviso* per descrivere il sistema in modo intuitivo.
- Progettazione minima: Si evitano design complessi in anticipo, sviluppando solo ciò che è necessario per l'iterazione in corso.
- **Spike solutions**: Quando c'è incertezza tecnica, si creano piccoli prototipi per testare possibili soluzioni.
- **Refactoring**: Il codice viene continuamente migliorato senza modificarne il comportamento.
  
> [!check] 3. *Sviluppo (Coding)*
> È la fase in cui si scrive effettivamente il codice, seguendo le pratiche XP per garantire qualità e manutenibilità.

- **Pair Programming**: Due sviluppatori lavorano insieme su una stessa funzionalità, migliorando la qualità del codice e riducendo errori.
- **Test-Driven Development (TDD)**: Si scrivono prima i test e poi il codice necessario per farli passare.
- **Proprietà collettiva del codice**: Tutti nel team possono modificare qualsiasi parte del codice.
- **Continuous Integration**: Il codice viene integrato e testato frequentemente per evitare conflitti e individuare errori tempestivamente.
  
> [!check]   4. *Test (Testing)*
> La qualità è un principio fondamentale in XP, e il testing è parte integrante dello sviluppo.

- **Test unitari automatici**: Ogni porzione di codice deve avere test automatici che ne verificano il corretto funzionamento.
- **Test di accettazione**: Il cliente definisce test per verificare se una funzionalità soddisfa i requisiti.
  Sono *basati sulle user stories* e definiti prima di scrivere il codice, per guidare l’implementazione. Non devono essere solo test tecnici, ma facilmente leggibili da chiunque.
  Esempio per la User Story sulla password dimenticata:
  
>   5. **Given** che un utente ha un account registrato.
>   6. **When** l'utente clicca su "Password dimenticata" e inserisce la sua email.
>   7. **Then** il sistema invia un'email con un link per reimpostare la password.

- **Refactoring continuo**: Dopo ogni test superato, il codice viene migliorato per essere più leggibile e mantenibile.
  
> [!check] 5. *Rilascio (Release)*
> Al termine di ogni iterazione, il software viene rilasciato e il cliente può testarlo.

- **Deploy frequente**: Il software viene consegnato regolarmente, spesso alla fine di ogni iterazione.
- **Feedback del cliente**: Il cliente prova il software e fornisce indicazioni per miglioramenti o nuove funzionalità.
- **Pianificazione delle iterazioni successive**: Il team aggiorna il piano in base al feedback ricevuto.
  
> [!check] 6. *Manutenzione (Maintenance)*
> XP prevede un miglioramento continuo del software per garantire stabilità e adattabilità ai nuovi requisiti.

# References

[^1]: ![[Test Driven Development#Tdd]]
