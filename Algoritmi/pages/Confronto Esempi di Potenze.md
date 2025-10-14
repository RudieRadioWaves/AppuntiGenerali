exclude-from-graph-view:: true

- Analizziamo le risorse impiegate dagli algoritmi di potenze visti qui: [[Esempio Semplice di Analisi 3]] e [[Esempio Semplice di Analisi 4]]
- | | $T(x, y)$ | $S(x, y)$ |
  |---|---|---|
  |Prodotti iterati| $\theta(y)$ | $\theta(1)$ | 
  |Potenze ricorsive|$\theta(\log y)$ | $\theta(\log y)$ | 
  |Potenze "alla russa" |$\theta(\log y)$ | $\theta(1)$ |
- Il miglior algoritmo è palesemente l'ultimo, in quanto usa meno tempo e meno spazio di tutti gli altri