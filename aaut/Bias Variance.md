2025-02-18 18:20

Status: #child 

Tags: [[Machine Learning]]
# Bias Variance

![[biasVariance.jpg]]

**BIAS**: l’errore sistematico che il modello compie perchè non è in grado di adattarsi completamente ai dati
**VARIANCE**: sensibilità del modello a variazioni nei dati

### Bias-Variance dilemma

> [!tldr] Bias-Variance dilemma
> Aumentando la capacità del modello:
> $\text{Bias} \downarrow, \quad \text{Variance} \uparrow$
> Riducendo la capacità del modello:
> $\text{Bias} \uparrow, \quad \text{Variance} \downarrow$

### Bias and Variance formula in relation with regression loss

$Bias^2(\hat{f}) = \left( f - \mathbb{E}[\hat{f}] \right)^2$
Distanza della media di $\hat{f}$ dalla $f$

$Var(\hat{f}) = \mathbb{E}\left[\left ( \hat{f} - \mathbb{E}[\hat{f}] \right)^2\right]$
Fluttuazioni di $\hat{f}$ attorno alla sua media