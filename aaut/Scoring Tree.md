2025-02-20 18:55

Status: #adult

Tags: [[02 - Tags/Alberi|Alberi]]
# Scoring Tree

```mermaid
graph TD
    A[Viagra] -->|0| B[lottery];
    A -->|1| C["ŝ(x) = +2"];
    B -->|0| D["ŝ(x) = -1"];
    B -->|1| E["ŝ(x) = +1"];
```

> Variante dei Decision Tree utilizzata per assegnare punteggi o valori a diverse opzioni o scenari. Ogni percorso attraverso l'albero rappresenta una sequenza di decisioni che portano a un punteggio finale

Si poggia sullo scoring classifier

![[Loss Function & Margin#Scoring classifier]]

Da uno Scoring Tree si ottiene facilmente un **Ranking Classifier** ordinando le foglie in base al punteggio dato.

Può venir applicato il ranking error rate:

![[Ranking Error Rate#Ranking Error Rate]]