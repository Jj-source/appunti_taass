2025-02-21 16:58

Status: #baby

Tags: 
# Distance Metrics

### Definition of a Distance Metric in the Instance Space
Given an instance space $\mathscr{X}$, a *distance metric* is a function $\text{Dis}: \mathscr{X} \times \mathscr{X} \rightarrow \mathbb{R}$ such that for any $x, y, z \in \mathscr{X}$:

- Distances between a point and itself are zero: $\text{Dis}(x, x) = 0$;
- All other distances are larger than zero: if $x \neq y$ then $\text{Dis}(x, y) > 0$;
- Distances are symmetric: $\text{Dis}(y, x) = \text{Dis}(x, y)$;
- Detours can not shorten the distance: $\text{Dis}(x, z) \leq \text{Dis}(x, y) + \text{Dis}(y, z)$.

If the second condition is weakened to a non-strict inequality – i.e., $\text{Dis}(x, y)$ may be zero even if $x \neq y$ – the function $\text{Dis}$ is called a *pseudo-metric*.
### Minkowski Distance
If $\mathscr{X}=\mathbb{R}^{d}$, the Minkowski distance of order $p>0$ is defined as
$$
\operatorname{Dis}_{p}(\mathbf{x}, \mathbf{y})=\left(\sum_{j=1}^{d}\left|x_{j}-y_{j}\right|^{p}\right)^{1 / p}=\|\mathbf{x}-\mathbf{y}\|_{p}
$$

> [!important] Norma
> $\|\mathbf{z}\|_{p}=\left(\sum_{j=1}^{d}\left|z_{j}\right|^{p}\right)^{1 / p}$ is the $p$ -norm (sometimes denoted $L_{p}$ norm) of the vector $\mathbf{z}$.
> We will often refer to $\mathrm{Dis}_{p}$ simply as the $p$ -norm.

### Euclidian Distance
The 2-norm refers to the familiar Euclidean distance

$$
\operatorname{Dis}_{2}(\mathbf{x}, \mathbf{y})=\sqrt{\sum_{j=1}^{d}\left(x_{j}-y_{j}\right)^{2}}=\sqrt{(\mathbf{x}-\mathbf{y})^{\mathrm{T}}(\mathbf{x}-\mathbf{y})}
$$

Which measures distance 'as the crow flies'.
### Manhattan Distance
The 1-norm denotes Manhattan distance, also called cityblock distance:
$$
\operatorname{Dis}_{1}(\mathbf{x}, \mathbf{y})=\sum_{j=1}^{d}\left|x_{j}-y_{j}\right|
$$

This is the distance if we can only travel along coordinate axes.

### Chebyshev Distance

> [!hint] If we now let $p$ grow larger, the distance will be more and more dominated by the largest coordinate-wise distance
> 
> 

from which we can infer that $\operatorname{Dis}_{\infty}(\mathbf{x}, \mathbf{y})=\max _{j}\left|x_{j}-y_{j}\right|$; this is also called Chebyshev distance.

### Hamming & Levenshtein Distance
You will sometimes see references to the 0-norm (or $L_{0}$ norm) which counts the number of non-zero elements in a vector. The corresponding distance then counts the number of positions in which vectors $\mathbf{x}$ and $\mathbf{y}$ differ. This is not strictly a Minkowski distance; however, we can define it as
$$
\operatorname{Dis}_{0}(\mathbf{x}, \mathbf{y})=\sum_{j=1}^{d}\left(x_{j}-y_{j}\right)^{0}=\sum_{j=1}^{d} I\left[x_{j} \neq y_{j}\right]
$$

under the understanding that $x^{0}=0$ for $x=0$ and 1 otherwise.

1. If $\mathbf{x}$ and $\mathbf{y}$ are binary strings, this is also called the Hamming distance. → number of bits that need to be flipped to change $\mathbf{x}$ into $\mathbf{y}$.
2. For non-binary strings of unequal length this can be generalised to the notion of edit distance or Levenshtein distance → minimum number of operations of insertion, deletion and substitution of one character required to change $x$ into $y$.
### Jaccard Similarity
In some cases, in which the features are sparse, zeros represent the absence of something.
Hamming distance accounts for the zeros as well as the ones.
**Jaccard does not** and it is more appropriate in sparse problems.

> P= 1 0 0 0 0 0 0 0 0 0
> Q= 0 0 0 0 0 0 1 0 0 1
> 
> Hamming (p, q) =(M 11+M 00)/(M 11+M 00+M 01+M 10) =7/10=0.7
> 
> Jaccard (p, q) =(M 11+M 00)/(M 11+M 00+M 01+M 10) =0/3=0
