2025-02-21 17:01

Status: #baby

Tags: [[Machine Learning]] [[Covariance and Covariance Matrix]]
# Mahalanobis Distance

## Definition of a Distance Metric in the Instance Space
Given an instance space $\mathscr{X}$, a *distance metric* is a function $\text{Dis}: \mathscr{X} \times \mathscr{X} \rightarrow \mathbb{R}$ such that for any $x, y, z \in \mathscr{X}$:

- Distances between a point and itself are zero: $\text{Dis}(x, x) = 0$;
- All other distances are larger than zero: if $x \neq y$ then $\text{Dis}(x, y) > 0$;
- Distances are symmetric: $\text{Dis}(y, x) = \text{Dis}(x, y)$;
- Detours can not shorten the distance: $\text{Dis}(x, z) \leq \text{Dis}(x, y) + \text{Dis}(y, z)$.

If the second condition is weakened to a non-strict inequality – i.e., $\text{Dis}(x, y)$ may be zero even if $x \neq y$ – the function $\text{Dis}$ is called a *pseudo-metric*.

## Mahalanobis Distance
The Mahalanobis distance is a statistical measure that calculates the distance between a point and a distribution in multivariate space. Unlike Euclidean distance, which assumes that variables are uncorrelated and have the same scale, the Mahalanobis distance takes into account the correlations between variables and the different scales of measurement.

> [!abstract] Confronto univariate z-score
> Z-score:
> $$z_i = \frac{x_j-\overline{x}}{σ}$$
> La σ (stdev) è la misura indica quanto i valori di un insieme di dati si discostano, in media, dalla media dell'insieme stesso.
> Dividendo la differenza tra il campione $x$ e la media $\overline{x}$, è dividendola per $σ$, sto andando ad indicare quanto “fuori scala” sia la variazione di $x$ rispetto alla variazione media.
> Mahalanobis distance:
> $$D_M(\mathbf{x}) = \sqrt{(\mathbf{x} - \mathbf{\mu})^T \mathbf{\Sigma}^{-1} (\mathbf{x} - \mathbf{\mu})}$$
> -  $(x-μ)$ è sempre sottrazione dalla media ma su più dimensioni
> - $\mathbf{\Sigma}$ è la misura di varianza ma su più dimensioni


> [!abstract] $\mathbf{\mu}$ e $\mathbf{\Sigma}$ come area di confidenza
> $\mu$ descrive come area di confidenza un intervallo orizzontale, tipicamente sotto una curva
> $\Sigma$ descrive come area di confidenza un’ellisse 

### Definition
The Mahalanobis distance of a point $\mathbf{x} = (x_1, x_2, \ldots, x_p)^T$ from a distribution with mean $\mathbf{\mu} = (\mu_1, \mu_2, \ldots, \mu_p)^T$ and covariance matrix $\mathbf{\Sigma}$ is defined as:

$$
D_M(\mathbf{x}) = \sqrt{(\mathbf{x} - \mathbf{\mu})^T \mathbf{\Sigma}^{-1} (\mathbf{x} - \mathbf{\mu})}
$$

Where:
- $\mathbf{x}$ is a vector of observations.
- $\mathbf{\mu}$ is the mean vector of the distribution.
- $\mathbf{\Sigma}$ is the covariance matrix of the distribution.
- $\mathbf{\Sigma}^{-1}$ is the inverse of the covariance matrix.

### Properties
- **Scale-Invariant**: The Mahalanobis distance is unitless and scale-invariant, making it suitable for comparing distances in spaces with different scales.
- **Correlation-Aware**: Using the covariance matrix has the effect of decorrelating and normalising the features, providing a more accurate measure of distance in the presence of correlated data.
- **Multivariate Normality**: The Mahalanobis distance is particularly useful when the data follows a multivariate normal distribution.

### Applications
- **Outlier Detection**: Identifying observations that are significantly distant from the mean of the distribution.
- **Classification**: Used in algorithms like k-nearest neighbors (k-NN) to classify data points based on their distance from known classes.
- **Multivariate Analysis**: Employed in techniques such as Principal Component Analysis (PCA) and Linear Discriminant Analysis (LDA).

### Example 1

![[mahalanobisEx.png]]

Mahalanobis distance takes into consideration the different correlations between the features. By normalization through ∑ it reduces the distances along the directions of greater spread of the data

In presence of correlated features (in which 𝜎lj is high for the two features of index l and j), consider two data points which are aligned along the direction of maximal spread of data (the longer axis of the ellipsoid, like A and C in the Figure of previous slide)

The two features whose difference is high in the two points give a high contribution in the Euclidean distance; since the two features are correlated (they behave similarly in the two points A and C) we over-emphasize their contribution 

With the Mahalanobis distance, the first feature gives its plain contribution to the distance, but the contribution from the remaining, correlated features is diminished by a term proportional to the covariance between the two features

> [!insight]
>  If we compute the Mahalanobis Distance $MD_i$ for an object $x_i$ to the mean of the data set $\overline{x}$:
> $$
> MD_i = \sqrt{\left( \frac{x_{i1} - \overline{x}_1}{\sigma_1} \right)^2 + \left( \frac{x_{i2} - \overline{x}_2}{\sigma_2} \right)^2 - 2 \rho_{12} \left( \frac{x_{i1} - \overline{x}_1}{\sigma_1} \right) \left( \frac{x_{i2} - \overline{x}_2}{\sigma_2} \right) + \sqrt{1 - \rho_{12}^2}}
> $$

This expression shows that the part of the second variable which is already explained by the first variable is subtracted. In other words, the MD corrects for the correlation within the data. When the two variables in Eq. (5) are uncorrelated ($\rho_{12} = 0$), the equation is reduced to the formula for the ED (for normalized data)

$$
ED_i = (x_{i1} - \overline{x}_1)^2 + (x_{i2} - \overline{x}_2)^2
$$
### Example 2
Consider a bivariate dataset with mean $\mathbf{\mu} = \begin{pmatrix} 3 \\ 4 \end{pmatrix}$ and covariance matrix $\mathbf{\Sigma} = \begin{pmatrix} 1 & 0.5 \\ 0.5 & 1 \end{pmatrix}$. To find the Mahalanobis distance of a point $\mathbf{x} = \begin{pmatrix} 5 \\ 6 \end{pmatrix}$:

1. Compute the difference vector: $\mathbf{x} - \mathbf{\mu} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$.
2. Compute the inverse of the covariance matrix: $\mathbf{\Sigma}^{-1}$.
3. Calculate the Mahalanobis distance using the formula.