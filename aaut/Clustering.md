2025-02-18 18:35

Status: #child 

Tags: [[Machine Learning]] [[Clustering Tree]]
# Clustering

Clustering can be thought of as the task of making sense of data by finding homogeneous groups inside it.

Predictive clustering can be understood as the process of learning a new labelling function from unlabelled data.

A ‘clusterer’ is then a mapping
$$ \hat{q} : \mathcal{X} \rightarrow \mathcal{C}$$
Dove $\mathcal{C} = \{C_1, C_2,\dots, C_k\}$

In descriptive clustering the model learned from the data would instead be a mapping
$$ \hat{q} : \mathcal{D} \rightarrow \mathcal{C}$$
Dove $\mathcal{D}$ è il dataset

# Clustering and distance

![[TypesOfClusters.pdf]]

## DBSCAN
Il DBSCAN (Density-Based Spatial Clustering of Applications with Noise) è un algoritmo di clustering utilizzato nel campo del machine learning e dell'analisi dei dati. A differenza di altri algoritmi di clustering come il K-means, il DBSCAN non richiede di specificare il numero di cluster in anticipo. Invece, si basa sulla densità dei punti per formare i cluster.
### Principi di Funzionamento
1. **Densità**: DBSCAN identifica i cluster come aree ad alta densità di punti separate da aree a bassa densità.
2. **Parametri**:
    - **Epsilon (ε)**: Rappresenta il raggio entro il quale si cerca la densità di punti.
    - **MinPts**: Numero minimo di punti richiesti per formare un cluster.
3. **Tipi di Punti**:
    - **Core Points**: Punti con almeno MinPts punti entro il raggio ε.
    - **Border Points**: Punti che sono raggiungibili da un core point ma non soddisfano la condizione di MinPts.
    - **Noise Points**: Punti che non sono né core né border.
4. **Formazione dei Cluster**:
    - Un cluster è formato da un insieme di core points densamente connessi e dai loro border points.
    - I punti di rumore non appartengono a nessun cluster.
### Vantaggi
- **Non richiede il numero di cluster predefinito**.
- **Robusto al rumore** e può identificare punti anomali.
- **Può trovare cluster di forma arbitraria**.
### Svantaggi
- **Sensibilità ai parametri**: La scelta di ε e MinPts può influenzare notevolmente i risultati.
- **Difficoltà con dati di densità variabile**: Può non performare bene se i cluster hanno densità molto diverse
### DBSCAN params
![[dbscanParams.pdf]]

## K-Means
The K-means problem is to find a partition of a dataset composed by k subsets (or clusters) such that WSS is minimised (or BSS is maximised) → This is understood as the clusters are well cohesive (or well separated)
### K-means algorithm (or Lloyd’s algorithm)
It iterates between partitioning the data by the nearest centroid decision rule and recalculating the centroid of each partition.
It is efficient and converges to a stationary point in finite time (since any iteration reduces the clusters errors) but there is no guarantee that the found solution is really the global minimum → run the algorithm a number of times and select the solution that reduces the within-clusters squared errors.

![[kmeans.pdf]]

Come valutare i clusters?
### WSS (Within-Cluster Sum of Squares)
- **Definizione**: WSS misura la somma delle distanze quadrate tra ciascun punto e il centroide del suo cluster.
- **Obiettivo**: Minimizzare il WSS significa che i punti all'interno di ciascun cluster sono strettamente raggruppati attorno al centroide.
- **Formula**: $$
\text{WSS} = \sum_{k=1}^{K} \sum_{x_i \in C_k} \|x_i - \mu_k\|^2
$$ dove Ck​ è il k-esimo cluster, xi​ è un punto nel cluster, e μk​ è il centroide del cluster.
### BSS (Between-Cluster Sum of Squares)
- **Definizione**: BSS misura la somma delle distanze quadrate tra ciascun centroide di cluster e il centroide globale di tutti i punti.
- **Obiettivo**: Massimizzare il BSS significa che i cluster sono ben separati tra loro.
- **Formula**: $$
\text{BSS} = \sum_{k=1}^{K} n_k \|\mu_k - \mu\|^2
$$ dove nkn è il numero di punti nel cluster k, μk​ è il centroide del cluster k, e μ è il centroide globale di tutti i punti.
### Relazione tra WSS e BSS
- **Equilibrio**: Un buon clustering generalmente minimizza il WSS e massimizza il BSS. Questo equilibrio indica che i punti all'interno dei cluster sono vicini tra loro, mentre i cluster stessi sono ben separati.
- **Metodo del Gomito**: Per determinare il numero ottimale di cluster KK, si può utilizzare il metodo del gomito, che consiste nel tracciare il WSS in funzione del numero di cluster e cercare il "gomito" dove il WSS inizia a diminuire più lentamente.
  
![[bsswssEx.png]]
### Disadvantage of K-Means
K-means has the disadvantage that it is biased towards clusters of globular shape, and of the same sizes. Here clusters are too high and it breaks them in half.

![[kmeansDisadvantage.png]]
## Silhouette
La Silhouette è una metrica utilizzata per valutare la qualità del clustering, ovvero quanto bene i punti sono assegnati ai rispettivi cluster. Questa metrica misura la similarità di un punto rispetto al proprio cluster rispetto agli altri cluster.
### Definizione
**Silhouette Score**: Per ogni punto, il Silhouette Score è calcolato come:
$$
  S (i) = \frac{b (i) - a (i)}{\max (a (i), b (i))}
$$
-  $a (i)$ è la distanza media tra il punto $i$ e tutti gli altri punti nello stesso cluster (coesione).
- $b (i)$ è la distanza media tra il punto $i$ e tutti i punti del cluster più vicino (separazione).

Il Silhouette Score varia tra -1 e 1:
- Un valore vicino a 1 indica che il punto è ben assegnato al proprio cluster.
- Un valore vicino a 0 indica che il punto è vicino al confine di decisione tra due cluster.
- Un valore vicino a -1 indica che il punto potrebbe essere assegnato al cluster sbagliato.
### Interpretazione
- **Media del Silhouette Score**: Per valutare la qualità complessiva del clustering, si calcola la media dei Silhouette Scores di tutti i punti. Un valore medio alto indica un buon clustering.
- **Utilizzo**: La Silhouette è utile per determinare il numero ottimale di cluster e per confrontare diversi algoritmi di clustering.

La Silhouette è una metrica intuitiva e facile da interpretare, che aiuta a capire quanto i cluster siano ben definiti e separati tra loro.
# Hierarchical Clustering
Il Hierarchical Clustering è un metodo di clustering che costruisce una gerarchia di cluster. A differenza di altri metodi come il K-means, non richiede di specificare in anticipo il numero di cluster. Esistono due approcci principali per il clustering gerarchico:
### Approcci
1. **Agglomerativo (Bottom-Up)**:
   - **Processo**: Inizia con ogni punto come un singolo cluster e iterativamente unisce i cluster più simili fino a quando tutti i punti non appartengono a un unico cluster.
   - **Metodi di Linkage**: Determinano come calcolare la distanza tra i cluster. I più comuni sono:
     - **Single Linkage**: Distanza minima tra due punti in cluster diversi.
     - **Complete Linkage**: Distanza massima tra due punti in cluster diversi.
     - **Average Linkage**: Distanza media tra tutti i punti nei due cluster.
     - **Centroid Linkage**: Distanza tra i centroidi dei cluster.

2. **Divisivo (Top-Down)**:
   - **Processo**: Inizia con tutti i punti in un unico cluster e iterativamente lo divide in cluster più piccoli fino a quando ogni punto non è un cluster singolo.
   - **Menor utilizzo**: Questo approccio è meno comune rispetto a quello agglomerativo.
### Vantaggi
- **Non richiede il numero di cluster predefinito**.
- **Produce un dendrogramma**, che è una rappresentazione grafica utile per determinare il numero ottimale di cluster.
- **Flessibile**: Può gestire cluster di forme e dimensioni diverse.
### Svantaggi
- **Computazionalmente intensivo**: Soprattutto per grandi dataset, poiché richiede il calcolo di una matrice di distanza completa.
- **Sensibilità al metodo di linkage**: La scelta del metodo di linkage può influenzare notevolmente i risultati.
### Dendrogramma
![[dendrogramma.png]]
- **Visualizzazione**: Un dendrogramma è un diagramma ad albero che mostra l'ordine e i livelli di fusione o divisione dei cluster.
- **Interpretazione**: Tagliando il dendrogramma a un certo livello, si può determinare il numero di cluster.

Il Hierarchical Clustering è utile quando si desidera esplorare la struttura dei dati a diversi livelli di granularità e quando non si conosce a priori il numero di cluster.