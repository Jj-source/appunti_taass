2025-02-22 09:53

Status: #baby

Tags: [[Machine Learning]]
# Nearest Neighbour Classifier (kNN)

In forma usuale, il k-nearest neighbour prende un voto per ciascuno dei k esemplari più vicini e prevede la classe della maggioranza dei k vicini (pertanto, di solito è conveniente prendere k come numero dispari per evitare pareggi).

> [!warning]
> Il kNN utilizza i dati di addestramento come esemplari, quindi l'addestramento è $O(n)$, ma anche la previsione è $O(n)$ !

$K = 1$ separa perfettamente i dati di addestramento → basso bias ma un'alta varianza (a causa del sovradattamento legato a dati di addestramento rumorosi o non rappresentativi).

> [!info]
> Aumento $k$ → Aumento Bias, diminuzione Variance (il noise avrà meno impatto)

È facilmente adattabile a target a
valori reali e anche a oggetti strutturati (recupero del vicino più vicino). Può anche produrre probabilità quando k > 1.

> [!warning]
> negli spazi ad alta dimensionalità tutto è lontano da tutto e quindi le distanze a coppie sono non informative (maledizione della dimensionalità)

### Bias & Variance

Ricordando il Bias Variance Dilemma

![[Bias Variance#Bias-Variance dilemma]]

Possiamo affermare:

- With lower values of k we have a higher variance (predictions are more susceptible to even little changes in the training set to the position of single instances) and a lower bias (predictions are able to be more adherent to the training set)
- With higher values of k we have a lower variance (predictions are more stable with noise in the training set because little changes in the position of some exemplars might be compensated by the remaining neighbours) but a higher bias (model predictions are more resistant to change in response to change of consistent portions of the training set).
## Distance weighting

KNN Voting can be ==weighted by the reciprocal of the distance== of the test instance to the exemplar.
Since weights decrease exponentially with distance, the effect of increasing k is much smaller than with unweighted voting. 

> [!abstract]
> With weighting → k-nearest neighbours more similar to a global model.
> Without weighting + small k → more similar to an *aggregation of many local models*.

If k-nearest neighbours is used for regression, we could aggregate the k predictions from the k neighbours by performing the average of their values, eventually weighting their values by the distance of the exemplar