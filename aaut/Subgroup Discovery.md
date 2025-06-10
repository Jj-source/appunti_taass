2025-02-18 21:19

Status: #child 

Tags: [[Machine Learning]]
# Subgroup Discovery

Given a labelled dataset $\{(x, l (x))\}$, find a function:

$$
\hat{g}: D \rightarrow \{\text{true}, \text{false}\}
$$

Such that $\mathcal{G} = \{x\in \mathcal{D}|\hat{g}(x) = true\}$ has a class distribution markedly different from the original population. $\mathcal{G}$ is said to be the extension of the subgroup.

**Example:** In a sales dataset, find a subgroup of people whose propensity to buy a given product is markedly higher than that of the whole population.

In general sub-group discovery algorithms are guided by an evaluation measure. Many different ones exist, but most of them share the following characteristics:
- They prefer larger sub-groups
- they are usually symmetric, i.e., they report the same value for the sub-group and for its complement 