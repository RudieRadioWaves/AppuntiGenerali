exclude-from-graph-view:: true

- Stavolta analizziamo le potenze, ma sotto due punti di vista: iterativamente e ricorsivamente
	- Potenze iterative
		- [[Pseudocodice]]:
		- ```
		  ALGORITMO potenza_iterativa (intero x, intero y) -> intero
		  ```
		- ```
		  power <- 1
		  WHILE y > 0
		  	power <- power * x
		      y <- y - 1
		  RETURN power
		  ```
		- Analizziamo la [[Correttezza]]
			- $x$ non viene mai modificata, mentre $y$ e $power$ si
			- $y_i$ e $power_i$ sono i valori di $y$ e $prodotto$ dopo l'iterazione $i$ (valore che equivale a 0 durante la prima iterazione)
			- Devo dimostrare per induzione che $y_i = y - i$ e che $power_i = x^{(i)}$
			- Dimostrazione:
				- CASO BASE: $i = 0$
					- Se $y = 0$, $power = 1$ in quanto si salta il ciclo completamente
					- Altrimenti, mi aspetto che $y_i = y$ e che $power_i = 1$
					- Applicando il lemma:
						- $y_i = y - 0 = y$
						- $power_i = x^{(0)} = 1$
					- Il caso base è dimostrato
				- INDUZIONE: $i - 1 \rightarrow i$
					- Non considero $y = 0$, in quanto il caso è stato coperto nel caso base
					- Mi aspetto che $y_i = y_{i-1} - 1$ e che $power_i = power_{i-1} \cdot x$
					- Applicando il lemma:
						- $y_i = y_{i-1} - 1$ che induttivamente $= y - (i + 1) = y - i - 1$
						- $power_i = power_{i - 1} \cdot x$ che induttivamente $= x^{i} \cdot x = x^{(i + 1)}$
					- L'induzione è dimostrata
		- Analizziamo l' [[Efficienza]]
			- Diciamo che il numero massimo di iterazioni che il ciclo svolge è $u$
			- Calcoliamo le iterazioni, legandole ad una quantità di tempo unitaria
				- Le linee 1, 5 vengono eseguite una volta sola ciascuna, contribuendo $2$ insieme
				- La linea 2 viene eseguita $u + 1$ volte, in quanto ci sono $u$ iterazioni del ciclo più una in più per uscire dal ciclo
				- Le linee 3 e 4 vengono eseguite $u$ volte ciascuna, contribuendo $2u$ insieme
			- In totale, l'algoritmo impiega $3u + 3$
			- Il numero di iterazione è uguale a $y$, quindi $u = y$
			- Quindi il tempo impiegato è $3y + 3$, linearmente dipendente da $y$
				- Impiegando la [[Notazione asintotica]], si dice che è $\Theta(y)$
			- Inoltre, le variabili utilizzate sono fisse e indipendenti da altri elementi
- ---
	- Potenze ricorsive
		- Algoritmo basato su questa equazione: $x^y = \begin{cases}1 \text{ se } y = 0 \\ (x^{\frac{y}{2}})^2 \text{ se } y > 0, y \text{ è pari} \\ (x^{\frac{y - 1}{2}})^2 \cdot x \text{ se } y \text{ è dispari}\end{cases}$
		- [[Pseudocodice]]:
		- ```
		  ALGORITMO potenza_ricorsiva (intero x, intero y) -> intero
		  ```
		- ```
		  if y = 0 THEN
		  	RETURN 1
		  ELSE 
		  	power <- potenza_ricorsiva(x, y/2) #divisione intera
		      power <- power * power
		      IF y è dispari THEN
		      	power <- power * x
		      RETURN power
		  ```
		- Analizziamo la [[Correttezza]]
			- $x$ non viene mai modificata, mentre $y$ e $power$ si
			- Dimostro che $\forall x, y \leq 0$, `potenza(x, y)` restituisce $x^y$
			- Utilizziamo sempre l'induzione su $y$
				- CASO BASE: $y = 0$
					- Restituisce 1
					- $x^y = x^0 = 1$, quindi è corretto
				- INDUZIONE: ipotizziamo sia vera per tutti i valori $< y$, vediamo se è vera per $y$
					- Caso $y$ pari
						- `potenza(x, y/2)` che, per ipotesi induttiva, $=x^\frac{y}{2}$
						- $(x^\frac{y}{2})^2 = x^y$
						- $y$ è pari, quindi abbiamo terminato
					- Caso $y$ dispari
						- `potenza(x, y/2)` che, per ipotesi induttiva, $=\lfloor x^\frac{y}{2} \rfloor= x^{\frac{y-1}{2}}$
						- $(x^{\frac{y-1}{2}})^2 = x^{y-1}$
						- $y$ è dispari, quindi $x^{y-1} \cdot x = x^y$
		- Analizziamo l' [[Efficienza]]
			- Tempo
				- Il tempo impiegato è definito come la funzione $T(x, y)
				- Caso $y = 0$
					- Vengono eseguite le righe 1, 2 e basta, quindi $T(x, y) = 2$
				- Caso $y > 0$
					- Vengono eseguite le linee 1, 4, 5, 6, 8, che portano insieme tempo = 5
					- La linea 7 viene eseguita se $y$ è dispari, portando tempo $\leq 1$
					- La linea 4 è una chiamata ricorsiva; il tempo è quindi $T(x, \lfloor \frac{y}{2} \rfloor)$
					- $T(x, y) \leq 6 + T(x, \lfloor \frac{y}{2} \rfloor)$
				- Quindi $T(x, y) = / \leq \begin{cases}2 \text{ se } y = 0 \\ 6 + T(x,  \lfloor \frac{y}{2} \rfloor) \text{ altrimenti} \end{cases}$
					- Un'equazione definita in termini di se stessa è detta "equazione di ricorrenza"
				- Risolviamola (supponendo $y$ pari per semplicità):
					- $T(x, y) \leq 6 + T(x, \frac{y}{2}) = 6 + 6 + T(x, \frac{y}{2^2}) = 6 + 6 + 6 + T(x, \frac{y}{2^3}) = ... = 6K  + T(x, \frac{y}{2^K})$
					- Scegliamo un K pratico, che mi riconduce al caso base: $K = 1 + \log y$ è tale che $\lfloor \frac{y}{2^K} \rfloor = \lfloor \frac{1}{2} \rfloor= 0$
					- $6(1 + \log y)  + T(x, 0) = 6 + 6 \log y + 2 = 8 + 6 \log y$
					- $T(x, y) \leq  8 + 6 \log y$
				- Quindi $T(x, y) = / \leq \begin{cases}2 \text{ se } y = 0 \\ 8 + 6 \log y  \text{ altrimenti} \end{cases}$
					- (NB: per calcolare queste cose, a volte si faranno approssimazioni non molto "matematiche", ad esempio supporre $y$ pari)
					- Impiegando la [[Notazione asintotica]], si dice che è $O(\log y)$
				- Siccome il tempo cresce in maniera logaritmica, è più efficiente del primo (che cresceva in maniera lineare)
			- Spazio:
				- 3 variabili fisse per [[Record di attivazione]]
				- Lo spazio utilizzato equivale al numero di variabili moltiplicato per il record di attivazione, ossia all'altezza dello [[Stack di ricorsione]]
				- Definiamola come $H(x, y)
				- $H(x, y) = \begin{cases}1 \text{ se } y = 0 \\ 1 + H(x,  \lfloor \frac{y}{2} \rfloor) \text{ altrimenti} \end{cases}$
				- Risolvendo questa equazione si ottiene che $H(x, y) = 2 + \log(y)$
				- Dunque lo spazio usato è $3 \cdot (2 + \log(y))$
					- Impiegando la [[Notazione asintotica]], si dice che è $O(\log y)$