2025-02-18 21:56

Status: #child

Tags: [[Machine Learning]]
# Class Probability Estimation

### Definizione
$$ \hat{p}: \mathcal{X} \rightarrow [0,1]^{k} $$
Scriviamo: $$\hat{\mathbf{p}}(x) = \left( \hat{p}_1(x), \dots, \hat{p}_k(x) \right)$$ Dove i-th componente è la probabilità assegnato alla classe $\: C_i\:$ e  $\:\sum_{i=1}^{k} \hat{p}_i(x) = 1\:$

### Squared error
The **squared error** (SE) of the predicted probability vector on an example $x$ is defined as:

$$
SE(x) = \frac{1}{2} \|\hat{p}(x) - I_{c(x)}\|_2^2
$$

$$
= \frac{1}{2} \sum_{i=1}^{k} (\hat{p}_i(x) - I[c(x) = C_i])^2
$$

where $I_{c(x)}$ is a vector having 1 in the position corresponding to label $c(x)$ and 0 in all other positions.

##### Esempio

Assumiamo $\hat{p}_i (x) = (0.7,0.1,0.2)$
E che $c (x) = C_1$ generando $I_{c (x)} = (1,0,0)$
$$
SE(x) = \frac{\|(0.7,0.1,0.2) - (1,0,0)\|_2^2}{2}
$$
$$
= \frac{\|(-0.3,0.1,0.2)\|_2^2}{2}
$$
$$
= \frac{0.09,0.01,0.04}{2} = \frac{0.14}{2} = 0.07
$$

### Mean Squared Error
La media di SE sulle instances del test set
$$
MSE(Te) = \frac{1}{|Te|}\times\sum_{x\in Te}SE(x)
$$
![[Smoothing#Smoothing]]
