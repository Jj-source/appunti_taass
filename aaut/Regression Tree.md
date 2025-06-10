2025-02-20 21:34

Status: #adult

Tags: [[Alberi]]
# Regression Tree

> [!idea]
La varianza di una variabile bouleana con probabilità $\dot{p}$ è $\dot{p}(1-\dot{p})$, cioè metà del Gini Index[^1]. Di conseguenza potremmo interpretare il goal del tree learning come la minimizzazione della class variance nelle foglie

Siccome i target values sono ora continui, sostituiamo le misure di impurità con la **Varianza**.
$$ Var(Y) = \frac{1}{|Y|}\sum_{y\,\,\in\,Y}(y-\overline{y})^2$$

![[regTreeEx.pdf]]

[^1]: ![[Purezza#Gini index]]
