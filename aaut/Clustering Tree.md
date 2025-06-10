2025-02-20 21:47

Status: #child

Tags: [[Alberi]] [[Clustering]]
# Clustering Tree

## Dissimilarity as Distance

We introduce an abstract function $Dis : X \times X \mapsto R$  
that measures the dissimilarity of two instances $x_1$ and $x_2$ in $X$.

The higher $Dis(x_1, x_2)$ the less similar $x_1$ and $x_2$ are.

The dissimilarity of a set (or cluster) of instances in $D$ can be measured by:
$$
  Dis(D) = \frac{1}{|D|^2} \sum_{x_1 \in D} \sum_{x_2 \in D} Dis(x_1, x_2)
$$
The lower $Dis(D)$ the better will be the cluster of instances in $D$.

$BestSplit(D,F)$ is implemented with a weighted average of $Dis(D_j)$, where $D_j$ is one of the partitions obtained after the split at the parent node:
$$
  Dis(\{D_1, ..., D_l\}) = \sum_{j=1}^{l} \frac{|D_j|}{|D|} \cdot Dis(D_j)
$$
If an object $x_i$ is described by $d$ numerical features in a space $X \subseteq R^d$,  each object can be described by a vector of $d$ components, $x_i = \langle x_{i1}, x_{i2}, ..., x_{ij}, ..., x_{id} \rangle$  where $x_{ij}$ represents the value of the feature $j$ in object $i$.

The dissimilarity $Dis(x_1, x_2)$ can be computed by a function of their distance:
$$
Dis(\mathbf{x_1}, \mathbf{x_2}) = (\mathbf{x_1} - \mathbf{x_2})^2 = \sum_{i=1}^{d} [x_{1j} - x_{2j}]^2
$$
The variance of the feature $j$ in a set of $N$ objects is:
$$
Var_j(D) = \frac{1}{N} \sum_{i=1}^{N} [x_{ij} - \bar{x}_{.j}]^2
$$
The sum of the variances of all the features can be interpreted as the average squared Euclidean distance between vectors in a $d$ -dimensional space:
$$
\sum_{j=1}^{d} Var_j(D) = \frac{1}{N} \sum_{j=1}^{d} \sum_{i=1}^{N} [x_{ij} - \bar{x}_{.j}]^2 = \frac{1}{N} \sum_{i=1}^{N} [\mathbf{x}_i - \bar{\mathbf{x}}]^2
$$
## Clustering Tree
We will learn a clustering tree by allowing feature with discrete values to be considered for the split conditions in the tree

![[clustTreeEx.pdf]]

> [!attention]
> Smaller clusters tend to have a lower dissimilarity and provoke overfitting

It is recommended setting aside a pruning set to remove the splits (in lower levels of the tree) if they do not improve the cluster cohesion (dissimilarity does not decrease) on the pruning set.

Furthermore, single examples (outliers) can dominate in the computation of the dissimilarity. It might be beneficial to remove them and recompute the measure Dis.

How do we label each cluster?

We choose the **best representative instance**
(It might be that instance that has the lowest total dissimilarity with all the other instances of the same cluster, called *the medoid*)