2025-02-20 18:59

Status: #adult 

Tags: [[Alberi]]
# Ranking Tree

## Definizione
Tree models divides the instance space into segments.
They can be turned into rankers by learning an ordering on those segments.

![[AlberiRankers.png]]

## Etichettatura
La scelta dell'etichettatura dipende dal rapporto di costo $c$ tra falsi negativi ($c_{FN}$) e falsi positivi ($c_{FP}$):

1. Calcola il rapporto di costo $c$:
   $c = \frac{c_{FN}}{c_{FP}}$

2. Confronta $c$ con le soglie fornite per determinare l'etichettatura:
   - Scegli $+-+-$ se $\frac{10}{29} < c < \frac{62}{5}$.
   - Scegli $+-++$ se $\frac{62}{5} < c < 25$.
   - Scegli $++++$ se $25 < c$ (predici sempre positivo).
   - Scegli $--+-$ se $\frac{3}{15} < c < \frac{10}{29}$.
   - Scegli $---$ se $c < \frac{3}{15}$ (predici sempre negativo).

Queste soglie aiutano a minimizzare il costo totale delle classificazioni errate in base alla gravità relativa dei falsi positivi e falsi negativi.

##### Può venire applicato il ranking error rate

![[Ranking Error Rate#Ranking Error Rate]]
