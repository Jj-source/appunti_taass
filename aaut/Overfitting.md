2025-02-20 20:50

Status: #baby

Tags: [[Machine Learning]]
# Overfitting
### Definizione
![[overfitting.jpg]]
L'overfitting avviene quando un modello di machine learning è troppo complesso e si adatta eccessivamente ai dati di addestramento, catturando anche il rumore. Questo porta a un'elevata varianza e a un basso bias, compromettendo la generalizzazione su nuovi dati.
### Tecniche di Mitigazione
- **Regolarizzazione**: Aggiungere penalizzazioni alla funzione di costo (es. L1, L2).
- **Dropout**: Disattivare casualmente neuroni durante l'addestramento.
- **Early Stopping**: Interrompere l'addestramento quando le prestazioni su un set di validazione peggiorano.
- **Data Augmentation**: Aumentare i dati di addestramento attraverso trasformazioni.
- **Cross-Validation**: Valutare le prestazioni su diversi sottoinsiemi di dati.

L'obiettivo è bilanciare la complessità del modello con la quantità di dati per migliorare la generalizzazione.