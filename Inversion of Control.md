2025-04-28 17:15

Status: #baby 

Tags:
# Inversion of Control
#### Pattern architetturale attualmente utilizzato in moltissimi framework.

> [!abstract] Controllo diretto
> Immaginiamo due componenti software X e Y (classi, moduli, o anche altro). X ha bisogno dei servizi di Y.
> → è responsabilità dello sviluppatore creare un’istanza di Y (anche, volendo, nel codice di X stesso) e passarla a X perché possa utilizzarla.

> [!abstract] Controllo rovesciato
> Esiste un framework che mantiene tutti i servizi[^1] (come Y) le cui funzionalità possono essere richieste da altri, e li fornisce a chi dichiara di necessitarne. 

> [!important] Astrazione
> il framework potrebbe anche **esporre versioni astratte** dei servizi, il che gli permette di *fornirne implementazioni diverse a seconda del contesto*, nonché di modificarne l’implementazione senza «scossoni» per le classi che li utilizzano, o di *fornirne versioni «mock» quando si sta effettuando il testing*. 

Il controllo rovesciato spesso viene realizzato tramite un meccanismo detto dependency injection.

> [!abstract] Dependency Injection
> Il componente che vuole usare determinati servizi lo dichiara, ad esempio specificandoli come parametri formali del proprio costruttore. Poiché è il framework a costruire il componente, nel momento in cui lo fa il framework gli passa le istanze dei servizi che ritiene appropriate e che ha già creato in precedenza. Questo meccanismo è appunto la «iniezione delle dipendenze». Esso permette un **minore accoppiamento fra l’utilizzatore e il fornitore di un servizio.**
# References

[^1]: in questo contesto il termine «servizio» è usato in senso astratto e non va identicicato con i @Service di Spring Boot, che possono beneficiare della dependency injection in entrambi i ruoli
