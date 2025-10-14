exclude-from-graph-view:: true

- Prendiamo il seguente algoritmo:
- ```
  ALGORITMO xx (intero x) -> intero
  ```
- ```
  p <- 1
  FOR i <- 1 TO x DO
  	p <- p * x
  RETURN P
  ```
- Abbiamo $\theta(x)$ per i prodotti e
- Applicando il [[Criterio di costo uniforme]], otteniamo che il tempo è $\theta(x)$, ma anche per un $x$ piccolo (ad esempio, 10) si hanno valori assurdi (come $10^10$) non calcolabili dagli interi
- Cerchiamo un altro approccio usando il [[Criterio di costo logaritmico]]
	- Calcoliamo il tempo:
		- All'iterazione $i$:
			- $p$ contiene $x^{i-1}$ prima dell'assegnamento
			- $p$ contiene $x^{i}$ dopo l'assegnamento
		- Il costo di $p \cdot x$ è $O(\log p + \log x) = \log x^{i- 1} + \log x = (i - 1) \log x$
		- Il costo dell'assegnamento a $p$ è $O(\log p \cdot x)$
		- Quindi il costo dell'$i-$esima iterazione è simile a $c \cdot i\log x + d$
		- Il costo totale dell'algoritmo sarà $e + \sum_{i=1}^x (c \cdot i\log x + d)= e + c\sum_{i=1}^x  (i\log x) + c\sum_{i=1}^x (d) = e + c \cdot \log x \sum_{i=1}^x i + dx = e + c\cdot \log x \frac{x(x+1)}{2} + dx$
			- La parte importante è quella col logaritmo, che detta che il costo finale sarà $\theta(x^2 \log x)$
	- Lo spazio è calcolato in modo simile, e il suo costo finale sarà $\theta(x \log x)$