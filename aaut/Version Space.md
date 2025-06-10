2025-02-18 23:02

Status: #adult

Tags: [[Machine Learning]]
# Version Space

Hypothesis $h$ is a conjunction of constraints on attributes
Each constraint can be:
- A specific value: e.g. Water=Warm
- A don’t care symbol representing any value: e.g. Water=?
- No value allowed (null hypothesis): e.g. Water=Ø

|  Sky  | Temp | Humid |  Wind  | Water | Forecast |
| :---: | :--: | :---: | :----: | :---: | :------: |
| Sunny |  ?   |   ?   | Strong |   ?   |   Same   |

- Target function $c: EnjoySport X \rightarrow \{0,1\}$

|  Sky  | Temp | Humid |  Wind  | Water | Forecast | EnjoySport |
| :---: | :--: | :---: | :----: | :---: | :------: | :--------: |
| Sunny |  ?   |   ?   | Strong |   ?   |   Same   |     …      |

- Goal of the learning: determinare le ipotesi $h$ in $\mathcal{H}$ tali che $h (x) = c (x)$ per tutti gli $x$ in $\mathcal{D}$


> [!definizioneviola] Definition of Version Space
> A hypothesis $h$ is consistent with a set of training examples $D$ of the target concept if and only if $h(x) = c(x)$ for each training example $<x, c(x)>$ in $D$.
> $$\text{Consistent}(h, D) := \forall\:<x,c(x)>\:\in D, \, h(x) = c(x)$$
> The Version Space, $VS_{H,D}$, with respect to hypothesis space $H$ and training set $D$, is the subset of hypotheses from $H$ consistent with all training examples:
> $$VS_{H,D} = \{h \in H \mid \text{Consistent}(h, D)\}$$

###### Assunzioni necessarie
1. Che esista nel hypothesis space $\mathcal{H}$ un’ipotesi che descriva il target concept
2. Che il training data non contenga errori
###### General to specific
Let $h_j$ and $h_k$ be boolean-valued functions defined over $X$. Then $h_j$ is more general than or equal to $h_k$ (written $h_j \geq h_k$) if and only if

$$
\forall x \in X : [ (h_k(x) = 1) \Rightarrow (h_j(x) = 1)]
$$

> [!definizione] Vapnik– Chervonenkis (VC) dimension
> Measure of the capacity (complexity, expressive power, richness, or flexibility) of a model (i.e, a set of functions that can be learned from instances) by a binary classification algorithm, defined as the cardinality of the largest set of points that the algorithm can shatter (distinguish by separating them in two distinct regions of the instance space).

### Algoritmo Find-S
1. Initialize $h$ to the most specific hypothesis in $\mathcal{H}$.
2. For each positive training instance $x$:
   - For each attribute constraint $a_i$ in $h$:
     - If the constraint $a_i$ in $h$ is satisfied by $x$, then do nothing.
     - Else, replace $a_i$ in $h$ by the next more general constraint that is satisfied by $x$.
3. Output hypothesis $h$.

> [!info] Bias
The hypothesis space H contains the target concept c and all instances are negative instances unless the opposite is entailed by its knowledge entailed by the most specific hypothesis learnt
##### Results
- It will output the most specific hypothesis within H that is consistent with the positive training examples
- The output hypothesis will also be consistent with the negative examples
##### Complaints
- it is unable to determine whether it has found the only hypothesis consistent with the training examples
- Can’t tell when training data is inconsistent, as it ignores negative training example.
### Algoritmo List-Then Eliminate
1. $\text{VersionSpace} \leftarrow$ a list containing every hypothesis in $\mathcal{H}$.
2. For each training example $<x, c(x)>$:
   - Remove from $\text{VersionSpace}$ any hypothesis that is inconsistent with the training example $h(x) \neq c(x)$.
3. Output the list of hypotheses in $\text{VersionSpace}$.

> [!info] Bias
The hypothesis space H contains the target concept c. It allows classification if all the members of VS agree. Otherwise, it refuses to classify.
##### Results
- It will output the most specific hypothesis within H that is consistent with the positive training examples
- The output hypothesis will also be consistent with the negative examples
##### Complaints
- It is unable to determine whether it has found the only hypothesis consistent with the training examples
- Can’t tell when training data is inconsistent, as it ignores negative training examples

## Rappresentazione del Version Space
The general boundary, $G$, of version space $VS_{H,D}$ is the set of maximally general members.

- The specific boundary, $S$, of version space $VS_{H,D}$ is the set of maximally specific members.
- Every member of the version space lies between these boundaries:

$$
VS_{H,D} = \{h \in H \mid (\exists s \in S)(\exists g \in G)(g \geq h \geq s)\}
$$

where $x \geq y$ means $x$ is more general or equal to $y$.

![[VersionSpace.png]]
### Candidate Elimination Algorithm
- Generalizzazione ($G$): ipotesi più generali coerenti con esempi positivi.
- Specializzazione ($S$): ipotesi più specifiche coerenti con esempi negativi.
- Inizializzazione: $G$ è l'ipotesi più generale, $S$ la più specifica.
- Per esempi positivi: rimuovi da $G$ ipotesi non coerenti, espandi $S$.
- Per esempi negativi: rimuovi da $S$ ipotesi non coerenti, riduci $G$.
- Version space finale: ipotesi coerenti con tutti gli esempi.

![[VersionSpaceAlgo.png]]

## Criticità

Assenza parziale o totale di inductive bias!

![[Inductive Leap#Inductive Bias]]