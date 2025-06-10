2025-02-21 17:09

Status: #baby

Tags: [[Machine Learning]] [[Mahalanobis Distance]]
# Covariance and Covariance Matrix

Covariance is a statistical measure that describes the extent to which two random variables change together. It provides insight into the direction of the linear relationship between two variables.

## Definition

The covariance between two random variables $X$ and $Y$ is defined as:

$$
\text{Cov}(X, Y) = \mathbb{E}[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])]
$$

Where:
- $\mathbb{E}[X]$ and $\mathbb{E}[Y]$ are the expected values (means) of $X$ and $Y$, respectively.
- $\mathbb{E}[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])]$ is the expected value of the product of the deviations of $X$ and $Y$ from their respective means.
## Covariance Matrix
For a set of $p$ random variables $X_1, X_2, \ldots, X_p$, the covariance matrix $\mathbf{\Sigma}$ is a $p \times p$ matrix where each element $\Sigma_{ij}$ represents the covariance between $X_i$ and $X_j$:

$$
\mathbf{\Sigma} = \begin{pmatrix}
\text{Cov}(X_1, X_1) & \text{Cov}(X_1, X_2) & \cdots & \text{Cov}(X_1, X_p) \\
\text{Cov}(X_2, X_1) & \text{Cov}(X_2, X_2) & \cdots & \text{Cov}(X_2, X_p) \\
\vdots & \vdots & \ddots & \vdots \\
\text{Cov}(X_p, X_1) & \text{Cov}(X_p, X_2) & \cdots & \text{Cov}(X_p, X_p)
\end{pmatrix}
$$

L’elemento $\sigma_{ij}$ , che rappresenta la covarianza tra le caratteristiche i e j, è calcolato come: $$ \sigma_{ij} = \frac{1}{n}\sum_{k=1}^n (X_{ki}-\overline{X_i}) (X_{kj}-\overline{X_j})$$
- $X_{ki}$ è il valore della variabile i per l’osservazione k
- $\overline{X_i}$ è la media dei valori della variabile i.

## Interpretazione

Se $i\neq j$ :
- $\sigma_{ij} > 0$ , *correlazione positiva*, le variabili aumentano o diminuiscono insieme
- $\sigma_{ij} < 0$, *correlazione negativa*, quando una variabile aumenta l’altra diminuisce
- $\sigma_{ij} = 0$, nessuna correlazione
## Properties

- **Symmetric**: The covariance matrix is symmetric, i.e., $\Sigma_{ij} = \Sigma_{ji}$.
- **Diagonal Elements**: The diagonal elements $\Sigma_{ii}$ represent the variance of $X_i$, i.e., $\text{Cov}(X_i, X_i) = \text{Var}(X_i)$.
- **Positive Semi-Definite**: The covariance matrix is positive semi-definite, meaning all its eigenvalues are non-negative.
## Relation to Variance
Variance is a special case of covariance where the two variables are the same. Specifically, the variance of a random variable $X$ is the covariance of $X$ with itself:

$$
\text{Var}(X) = \text{Cov}(X, X)
$$

Thus, the diagonal elements of the covariance matrix represent the variances of the individual variables.
## Applications

- **Multivariate Analysis**: Used in techniques such as Principal Component Analysis (PCA) and Linear Discriminant Analysis (LDA).
- **Portfolio Theory**: In finance, the covariance matrix is used to assess the risk of a portfolio of assets.
- **Regression Analysis**: Helps in understanding the relationships between dependent and independent variables.

### $\mathbf{\sigma}$ e $\mathbf{\Sigma}$ come area di confidenza

> [!abstract] $\mathbf{\sigma}$ e $\mathbf{\Sigma}$ come area di confidenza
> $\sigma$ descrive come area di confidenza un intervallo orizzontale, tipicamente sotto una curva
> $\Sigma$ descrive come area di confidenza un’ellisse
> 
> ![[Bell-Curve-with-Conf.webp]]
> ![[Error-Ellipse-P-Rotated.webp]]

# References
https://thekalmanfilter.com/covariance-matrix-explained/