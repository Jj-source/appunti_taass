2025-02-18 18:27

Status: #child

Tags: [[Machine Learning]]
# Classificazione
### Definizione
$$ \hat{c}: \mathcal{X} \rightarrow \mathcal{C} $$
where: $$ \mathcal{C} = \{C_1, C_2, \ldots, C_k\} $$ $\hat{c}$  is an approximation of the true but unknown function $c$.
An example is a pair: $$ (x, c(x)) \in \mathcal{X} \times \mathcal{C} $$ where $x$ is an "instance" and $c(x)$ is the true class of the instance (possibly contaminated by noise).

> **Learning** a classifier → constructing $\hat{c}$ such that it matches c as closely as possible (and not just on the training set, but ideally on the entire instance space )
## Classificazione multi-classe
Partendo da un modello binario:
- One-vs-rest
  Per 3 classi $a, b, c$ hai 3 classificatori
  $a\:\:vs\:\:\{b, c\}$       $b\:\:vs\:\:\{a, c\}$       $c\:\:vs\:\:\{a,bc\}$
- One-vs-one
  Per 3 classi $a, b, c$ hai $3!$ classificatori
  $a\:\:vs\:\:b$  , $b\:\:vs\:\:a$  , $a\:\:vs\:\:c$  , $c\:\:vs\:\:a$  , $b\:\:vs\:\:c$  ,  $c\:\:vs\:\:b$
 
 Per classificare un nuovo esempio, un vettore $w$ è costruito con gli output dei classificatori. La classe predetta sarà quella a cui riga nel classificatore è più vicina a $w$. Distanza → $d (w, c) = \sum_i \frac{(1- c_iw_i)}{2}$
$$
\begin{array}{r|ccc|c}
  & 1 \text{ vs } \{2,3\} & 2 \text{ vs } \{1,3\} & 3 \text{ vs } \{1,2\} & w = (+1, -1, -1) \\
  \hline
C_1 & +1 & -1 & -1 & d(w, C_1) = 0 \\
C_2 & -1 & +1 & -1 & d(w, C_2) = 2 \\
C_3 & -1 & -1 & +1 & d(w, C_3) = 2
\end{array}
$$
##### Issues
- One-vs-rest, i singoli classificatori di solito vedono dataset altamente sbilanciati, anche se il dataset iniziale è bilanciato.
- One-vs-one, il problema sopra descritto è mitigato assegnando l'etichetta 0 agli esempi che non appartengono alle due etichette in fase di valutazione. Questo è particolarmente problematico quando i dati sono scarsi.