2025-02-18 20:54

Status: #child

Tags: [[Machine Learning]] 
# Loss Function & Margin

### Scoring classifier
$$ \hat{s}: \mathcal{X} \rightarrow \mathbb{R}^{k} $$
Output is a vector: $$\hat{\mathbf{s}}(x) = \left( \hat{s}_1(x), \dots, \hat{s}_k(x) \right)$$ Dove $\hat{s}_1 (x)$ è lo score assegnato alla classe $C_i$ per l’istanza $x$ 
### Margin
Assume to have to deal with a binary classifier. If we take the true class $\:\:c(x)\:\:$ as $\:\:+1\:\:$ for positive examples and $\:\:-1\:\:$ for negative examples. Assume also that we have a scoring classifier assigning a positive score $\:\:\hat{s}(x) > 0\:\:$ to positive examples and a negative score $\:\:\hat{s}(x) < 0\:\:$ to negative examples, then:

$$Z (x) = c (x) \hat{s}(x) =
\begin{cases} 
+|\hat{s}(x)|, & \text{if } x \text{ is correctly classified} \\
-|\hat{s}(x)|, & \text{if } x \text{ otherwise}
\end{cases}
$$

Is called the **margin** assigned by the scoring classifier to the example.

### Loss Function
We would like to reward large positive margins, and penalise large negative ones. This is achieved by means of a so-called **loss function** $\:\:L : \mathbb{R} \rightarrow [0, \infty)\:\:$ which maps each example's margin $\:\:z (x)\:\:$ to an associated loss $\:\:L (z (x))\:\:$.

We will assume that $\:\:L (0) = 1\:\:$ which is the loss incurred by having an example on the decision boundary. We furthermore have $\:\:L (z) \geq 1\:\:$ for $\:\: z < 0 \:\:$, and usually also $\:\: 0 \leq L(z) < 1\:\:$ for $\:\: z > 0\:\:$.

![Loss Function Graph](classificationlosses.png)

- **Incorrectly classified examples**: \( z < 0 \)
- **Correctly classified examples**: \( z > 0 \)
