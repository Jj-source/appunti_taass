2025-02-20 17:35

Status: #adult

Tags: [[Machine Learning]] [[Alberi]]
# Purezza

![[Purezza.png]]

Un modo iniziale per calcolare la purezza di una partizione di $n$ esempi $\{n^+, n^-\}$ può essere espressa tramite l’**empirical probability**
$$\dot{p} = \frac{n^+}{n^+ + n^-}$$
### Minority class:
$$
min\{\dot{p}, 1-\dot{p}\} 
$$
$$
1-max\{\dot{p_i}\} \:\:,\: i>2 
$$
or the error rate as it would be measured with the **proportion of misclassified examples** if all the examples in the leaf node were labelled with the majority class
### Entropy:
![[Entropy#Definizione]]
### Gini index:
$$
2\dot{p}(1-\dot{p}) 
$$
$$
\sum_i \dot{p}_i (1-\dot{p_i}) \:\:\:,\:\: i>2
$$
it is the **expected error if the examples in the leaf node were labelled randomly**: positive with probability $\dot{p}$, negative with probability $(1-\dot{p})$. The probability of a false positive is $\dot{p}(1-\dot{p})$ and the probability of a false negative is $(1-\dot{p})\dot{p}$.

> [!help] Why Gini index is the expected error
> Examples in the population are positive with probability $p$ and negative with probability $(1-p)$
> 
> They are labelled randomly and independently of their true label.
> 
> When we extract an example, it is positive with probability $p$.
> If we label it as negative we commit an error of false negative (FN). This error occurs with probability $(1-p)$.
> Overall probability of this error: $p(1-p)$
> 
> There is $(1-p)$ probability that we extract a negative example.
> If we label it as positive we commit an error of false positive (FP). 
> This error occurs with probability $p$.
> Overall probability of this error: $(1-p)p$
> 
> Total probability of error (FN+FP)= $p(1-p)+(1-p)p=2p(1-p)$

> [!caution]
> Il Gini Index, come l’Entropia, è sensibile alle fluttuazioni nella class distribution.
> $\sqrt{Gini}$ non lo è

![[giniex.png]]