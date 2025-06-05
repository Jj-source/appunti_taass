2025-02-22 17:00

Status: #baby

Tags: [[Università]] [[Object Oriented Analysis (OOA)]]
[[SAS]]
# Project & People Management

## Gestione di un progetto

- difficoltà nel comprendere le tempistiche
- troppi livelli gerarchici
- attività duplicate
- cattiva comunicazione
- mancanza funzione di controllo: verificare procedimento corretto ed avere piano B.

Punti chiave
1. definire
2. pianificare: sapere quali sono i passaggi chiave e quali sono le dipendenze tra essi. Individuare i task (e sottotask) che compongono il progetto.
3. schedulare: prese le attività del punto 2 si assegnano
- tempistiche
- vincoli di precedenza
  Così diventa possibile stimare il tempo e le risorse necessarie al progetto.
4. controllare

Nell'approccio tradizionale / monolotico l'esecuzione di un progetto è un momento completamente separato dalla pianificazione.
# Xtreme Programming

Molto importante la fiducia tra i membri del gruppo.
(come? premiare i meritevoli, celebrare i successi, suddividere correttamente le responsabilità).

[[Xtreme Programming (XP)]]

# Unified Process UP

[[Unified Process UP#Unified Process UP]]
# People Management
*Project Manager*
Attua funzione di monitoraggio, controlla che tutto vada come il gruppo ha deciso.
#### Stumenti
- meetings
- performance review, non per dare voti ma per riflettere su cosa ha funzionato di più e cosa meno (quindi un momento di riflessione anche per il manager)
- assunzioni
#### approccio estrattivo
"estrarre più risorse possibili dalla miniera"
ottenere il massimo da ciò che possono produrre i tuoi schiavi
(il manager dovrebbe ugualmente spremersi)
-> breve periodo
#### approccio generativo
"un albero da frutto mica puoi spremerlo e farlo morire"
fai fiorire il tuo giardino e cura il benessere dei tuoi schiavi-piante.
-> lungo periodo

Accettabile un 80% generativo ed un 20% estrattivo in prossimità di scadenze

# Lezione 2
### Time and Effort
- Time: tempo tra l'inizio e la fine del progetto
- Effort: forza lavoro comulativa necessaria a finire il progetto

ex) 5 pittori che dipingono una casa in 3 giorni:
Tempo = 3 giorni
Effort = 15 person-days (5 painters * 3 days)
## Action planning model

| Phase                                | Action Planning                                             | Planning outcome                                              |
| ------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------- |
| Obiettivi (perché)                   | Quali sono gli obiettivi? Le priorità?                      | Definizione obiettivi e priorità                              |
| Tasks (cosa)                         | Quali sono i tasks                                          | identificazione tasks per raggingere obiettivi                |
| Procedure per implementazione (come) | Come viene posto in azione il piano? Con che metodi?        | meccanismi e procedure, *Testing e le procedure di controllo* |
| Schedule (come)                      | Quando sarà completato il piano? le fasi?                   | Timetable                                                     |
| Stima dei costi (come)               | /                                                           | Budget                                                        |
| Follow-up e review (quando)          | Come sarà valutato il piano? Quali meccanismi di controllo? | follow up e review                                            |
### Planning
- Determina priorità
- Prepara a risolvere i conflitti, se può previenili
- Scrivere i piani
- Modifica e mantieni i piani attraverso meccanismo di controllo e revisione -> che metriche ti dai? molto difficile  

! puoi usare librerie dummies per sostituire temporaneamente pezzi di codice
# Gestire un progetto
## Definire il progetto
### Definire gli obiettivi
Motivo del progetto, caratteristiche del risultato
Scope:
- prodotto: funzionalità
- progetto: il lavoro da fare per produrre il prodotto

Limitazioni: fattori limitanti del progetto come tempo, budget, risorse

*Educated guesses* relative alle tempistiche ("gli ordini dei materiali non impiegheranno più di 30 giorni" "non pioverà più del 15% del tempo")

> [!tip]
> ciò che vogliono da noi alle review è che capiamo i limiti e ciò che ha funzionato della nostra pianificazione iniziale
### Creare e Strutturare i Tasks
*codice di outline* per i task -> facilitare documentazione (ex: task 1.4.1)

Due approcci:
- Top-Down: si parte dal macro per dividere in singoli compiti
- Bottom-up: si parte dai singoli compiti atomici e li si accorpa in task più grossi
  
**! non fare micromanaging**, non task troppo piccoli, il livello di dettaglio dev'essere coerente con la qualità di pianificazione e controllo desiderata

! includere stesura di rapporti, review, attività di coordinazione

> [!abstract] Milestones
> Sono i punti in cui c'è qualche consegna, per un cliente (esterna) o tra sviluppatori (interna) per controllare come procede il lavoro (come momento di confluenza) e sono da inserire *all'inizio ed alla fine di una serie di task*
> per noi: le due project review e la consegna
## Strumenti
### GANTT chart
![](https://www.productplan.com/uploads/2019/11/Gantt-chart.png)
### Pert chart
![](https://powerslides.com/wp-content/uploads/2020/08/PERT-Chart-Template-2.jpg)

puoi applicarci il minimal path algoritmo he prende in input la durata stimata delle task e le dependencies tra task e ti trova i cammini critici tra le task

cammini critici: sequenza delle attività che vincolano il progetto (se ritarda una, ritarda tutto)

-> parallelizzare e rendere indipendenti i task
(**high coesion e low coupling**)

> [!info] Software
trello +gantt chart + calendar,timeline,time tracking
jetbrains + YouTrak
### 3 major problems
- incertezza: sia di ciò che vuole il committente che può cambiare idea nel tempo, che delle tecnlogie che in fretta possono diventare obsolete
- irreversibility: Consuming less resource by not committing early, Requirements could be economically reversible
- Complexity: Dealing with one requirement at a time, Keeping the project under control
## Evoluzione del software engineering
L'iteratività permette di intercettare i nuovi requisiti (funzionali (dei clienti) e tecnologici) ed inglobarli nel progetto.
### Cascata
![](https://static.html.it/app/uploads/documenti/guide/img/antipattern/fig01.png)
### Incrementale
![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/39/Iterative_development_model.svg/1200px-Iterative_development_model.svg.png)
! refactoring: facilita il processo di re-ingenierizzazione del software
### Spirale
![](https://www.bdtask.com/blog/assets/plugins/ckfinder/core/connector/php/uploads/images/what%20is%20spiral%20model%20for%20software%20development.jpg)
Ripete le fasi espandendosi.
Avere più release permette di notare prima i problemi.
### Xtreme Programming (XP)
  
[[Xtreme Programming (XP)#Xtreme Programming (XP)]]
### Gestione iterativa
![[iterative.png]]
![[iterative.pdf]]

![[Progettex.pdf]]

![[umlex.png]]

