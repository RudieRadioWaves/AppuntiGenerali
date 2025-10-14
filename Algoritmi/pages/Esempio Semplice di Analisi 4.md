exclude-from-graph-view:: true

- Stavolta si analizza lo svolgimento di $x^y$
- Osserviamo che $x^y = x^{2 \cdot \frac{y}{2}} = (x^2)^{\frac{y}{2}}$ (se la divisione è con numeri reali)
- Dunque $x^y = \begin{cases}(x^2)^{\frac{y}{2}} \text{ se y è pari e > 0} \\ (x^2)^{\frac{y-1}{2}} \text{ se y è dispari} \\ 1 \text{ se y = 0} \end{cases}$
- Ad ogni "iterazione" elevo la base al quadrato e divido l'esponente per 2. Se la base è dispari, la si "salva"
	- Al termine dell'esecuzione, si moltiplicano tutte le basi salvate
- Formalizzata:
- ```
  ALGORITMO potenza (intero x, intero y) -> intero
  ```
  ```
  power <- 1
  WHILE y > 0 DO
  	IF y è dispari THEN
  		power <- power * x
  	y <- y/2 //divisione intera
  	x <- x*x
  return power
  ```
- Molto simile all'[[Esempio Semplice di Analisi 2]]
- Trascuriamo la dimostrazione della correttezza
- Analizziamo l'efficienza:
	- Tempo:
		- Con un numero di iterazioni $u$:
			- Le linee 1 e 7 vengono eseguite una volta sola ciascuna, quindi contribuiscono 2
			- La linea 2 viene eseguita $u+1$ volte
			- Le linee 3, 5, 6 vengono eseguite $u$ volte ciascuna, quindi contribuiscono $3u$
			- La linea 4 viene eseguita al più $u$ volte, quindi $\leq u$
			- Sommando tutto si ottiene $5u +3$
		- $u = \lfloor \log y \rfloor + 1$
		- Quindi $T(x, y) = 5 (\lfloor \log y \rfloor + 1) + 3 = 5\lfloor \log y \rfloor + 8$
			- E' O-grande di $\log y$ (in quanto ricordiamo la linea 4)
	- Spazio:
		- Tre variabili fisse, e quindi è O-grande di 1 (costante)