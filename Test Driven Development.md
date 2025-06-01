2025-02-24 18:12

Status: #baby

Tags: 
# Test Driven Development
## *TDD*
La **Test-Driven Development (TDD)** è una tecnica di sviluppo software basata sull'idea di scrivere i test prima di scrivere il codice effettivo. Segue un ciclo iterativo ben definito chiamato **Red-Green-Refactor**:

1. **Red (Scrivere un test che fallisce)**
    Si scrive un test automatizzato per una funzionalità che ancora non esiste.
    Il test fallisce perché il codice per soddisfare il requisito non è stato ancora scritto.
2. *Green (Scrivere il codice minimo per far passare il test)*
    Si scrive la quantità minima di codice necessaria per far passare il test.
    Il focus è sulla funzionalità, non sulla perfezione del codice.
3. Refactor (Migliorare il codice senza cambiare il comportamento)    
    Si rifattorizza il codice per migliorare la qualità, eliminare duplicazioni o ottimizzare le prestazioni.
    Dopo ogni refactoring, tutti i test devono continuare a passare.
## *Vantaggi del TDD*
- Migliore qualità del codice → Il codice è più pulito, modulare e con meno bug.
- Documentazione automatica → I test fungono da documentazione vivente del comportamento del sistema.
- Migliore design del software → Scrivere i test prima porta a un'architettura più orientata all'usabilità e alla testabilità.
- Minore debugging → Gli errori vengono intercettati precocemente e risolti prima di accumularsi.
- Maggiore sicurezza nelle modifiche → Il refactoring è più sicuro perché i test garantiscono che le funzionalità esistenti non si rompano.
### Framework comuni per il TDD
- Python → `pytest`, `unittest`
- JavaScript/TypeScript → `Jest`, `Mocha`
- Java → `JUnit`, `TestNG`
- C# → `xUnit`, `NUnit`
- Ruby → `RSpec`, `MiniTest`

Il TDD è particolarmente utile in ambienti **Agile** e in **Continuous Integration/Continuous Deployment (CI/CD)**, dove il codice deve essere costantemente modificato e migliorato senza paura di introdurre bug.
