2025-02-18 21:19

Status: #adult 

Tags: [[Machine Learning]]
# Association Rules

Given an unlabelled dataset $D$, find a set of rules $\{b \rightarrow h\}$ such that the itemset $b \cup h$ is frequent and that $h$ is likely to hold whenever $b$ holds.

Here, $b$ and $h$ are sets of attribute/value pairs.
Here's the text formatted in Markdown with inline math expressions enclosed in single dollar signs:

To mine association rules, we first need to identify frequent itemsets (the ones with high support). Once we know that itemset $\{i1, i2, i3\}$ is frequent, then all the following rules are frequent:

- $i1 \rightarrow i2, i3$
- $i2 \rightarrow i1, i3$
- $i3 \rightarrow i1, i2$
- $i1, i2 \rightarrow i3$
- $i1, i3 \rightarrow i2$
- $i2, i3 \rightarrow i1$

Among those rules, we want to select those satisfying some measure. For instance, if we use “confidence” then we would select those for which $\frac{supp(b\:\cup\:h)}{supp(b)}$ is high.
##### Esempio
| spesa | product 1 | product 2 | product 3 |
|-------|-----------|-----------|-----------|
| 1     | Bread     | Milk      | Water     |
| 2     | Bread     | Milk      |           |
| 3     | Water     | Bread     | Ham       |
| 4     | Water     | Eggs      |           |
| 5     | Bread     | Milk      |           |
If we set 0.6 as our support threshold (i.e., an itemset is frequent whenever it appears in 60% of the transactions), the following frequent itemsets can be extracted:

- $\{Bread\}$ (supp: 0.8)
- $\{Milk\}$ (supp: 0.6)
- $\{Water\}$ (supp: 0.6)
- $\{Bread, Milk\}$ (supp: 0.6)

Allowing one to generate the following rules:

- $Bread \rightarrow Milk$ (conf: $0.6/0.8 = 0.75$)
- $Milk \rightarrow Bread$ (conf: $0.6/0.6 = 1$)
