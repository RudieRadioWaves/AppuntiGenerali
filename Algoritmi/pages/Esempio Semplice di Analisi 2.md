exclude-from-graph-view:: true

- Analizziamo il metodo delle moltiplicazioni "alla russa":
	- Prerequisiti: saper dividere e moltiplicare per due, saper sommare (ideale per i computer e il codice binario)
	- Passo 1: Svolgo ripetutamente queste operazioni: moltiplico per due il moltiplicando $a$ e divido per due il moltiplicatore $b$ (tralasciando il resto). Quando $b$ è 1, mi fermo.
		- |Moltiplicando $a$|Moltiplicatore $b$|
		  |---|---|
		  | 19 | 114 |
		  | 38 | 57|
		  | 76 | 28 |
		  | 152 | 19 |
		  |304 | 7|
		  |608|3|
		  |1216|1|
	- Passo 2: Osservo tutti i numeri ottenuti. Tutte le volte che $b$ è dispari, prendo $a$.
		- 38, 304, 608, 1216
	- Passo 3: Sommo tutti gli $a$ presi, ottenendo il prodotto.
		- 38 + 304 + 608 + 1216 = 2166
	- (Si può anche svolgere l'analisi dei numeri durante il passo 1)
- Dunque, si può dire che
	- $a \cdot b = \begin{cases}2a \cdot \frac{b}{2} \text{ se } b \text{ pari} \\ 2a \cdot \frac{b - 1}{2} + a \text{ se } b \text{ dispari} \\ a \text{ se } b = 1 \end{cases}$
- [[Pseudocodice]]:
	- ```
	  ALGORITMO moltiplicazione_russa (intero a, intero b) -> intero
	  ```
	- ```
	  prod <- 0
	  WHILE b > 0 DO
	  	IF b è dispari THEN
	      	prod <- prod + a
	      b <- b/2
	      a <- a*2
	  return PROD
	  ```
	- Verifichiamo la [[Correttezza]]
		- Definiamo $a_i, \ b_i, \ prod_i$ come i valori di $a, \ b, \ prod$ dopo l'iterazione $i$
		- Bisogna dimostrare che $a_i b_i + prod_i = a \cdot b$; come nel primo esempio applico l'induzione su $i$
		- Dimostrazione
			- CASO BASE: $i = 0$
				- $a_0 = a$, $b_0 = b$, $prod_0 = 0$
				- $a_0 b_0 + prod_0 = a \cdot b + 0 = ab$
			- INDUZIONE: $i - 1 \rightarrow i$
				- $a_i = 2a_{i-1}$
				- $b_i = \lfloor \frac{b_{i-1}}{2}\rfloor = \begin{cases}b_i = \frac{b_{i-1}}{2} \text{ se } b_{i-1} \text{ è pari} \\ b_i = \frac{b_{i-1}-1}{2} \text{ se } b_{i-1} \text{ è dispari} \end{cases}$
				- $prod_i = \begin{cases}prod_{i - 1} \text{ se } b_{i-1} \text{ è pari} \\ prod_{i - 1} + a_{i-1} \text{ se } b_{i-1} \text{ è dispari} \end{cases}$
				- Analizziamo $a_i b_i + prod_i$ in diversi casi:
					- Se $b_{i-1}$ è pari: $a_i b_i + prod_i = 2a_{i-1} \frac{b_{i-1}}{2} + prod_{i-1} = a_{i-1} b_{i-1}+ prod_{i-1}$
					- Se $b_{i-1}$ è dispari: $a_i b_i + prod_i = 2a_{i-1} \frac{b_{i-1}-1}{2} + prod_{i-1} + a_{i-1} = a_{i-1} (b_{i-1} - 1)+ prod_{i-1} = a_{i-1} b_{i-1} - a_{i-1} + prod_{i - 1} + a_{i-1} =  a_{i-1} b_{i-1}+ prod_{i-1}$
				- In entrambi i casi, $a_i b_i + prod_i = a_{i-1} b_{i-1}+ prod_{i-1}$ che per induzione $= a \cdot b$
			- Dunque, abbiamo verificato che è corretto.
	- Verifichiamo l'[[Efficienza]].
		- Tempo:
			- Calcolo delle iterazioni:
				- Definiamo l'ultima iterazione come $u$
				- Le linee 1, 7 vengono eseguite una volta sola ciascuna, quindi insieme contribuiscono 2 unità di tempo
				- Le linee 2 viene ripetuta $u + 1$ volte ($u$ volte per iterare attraverso le $u$ iterazioni e l'ultima per uscire dal ciclo)
				- Le linee 3, 5 e 6 vengono ripetute $u$ volte ciascuna, quindi quindi insieme contribuiscono $3u$ unità di tempo
				- La linea 4 viene eseguita a volte si, a volte no, quindi si dice che contribuisce *al più* $u$ volte ($\leq u$)
				- Sommando tutto, otteniamo $\leq 5u + 3$
			- Come dipende $u$ da $b$?
				- Osserviamo la grandezza di $b$ e il numero di iterazioni relativo
					- $b = 0 \implies u = 0$, in quanto il calcolo si blocca subito
					- $b = 1 \implies u = 1$ iterazione prima di terminare (divido 1 volta sola prima di raggiungere un numero < 1)
					- $b = 2 \implies u = 2$ iterazioni prima di terminare (divido 2 volte). Questo vale anche per $b = 3$
					- $b = 4 \implies u = 3$ iterazioni prima di terminare (divido 3 volte). Questo vale anche per $b = 4, 5, 6, 7$
					- E così via...
				- Possiamo vedere che la relazione è $u = \lfloor \log b\rfloor + 1$
			- Quindi il tempo $T(a, b) \leq 5(\lfloor \log b\rfloor + 1) + 3 = 5\lfloor \log b\rfloor + 8$
				- Possiamo vedere che la crescita è indipendente da $a$ e che è logaritmica dipendente da $b$
				- Comparata alla crescita lineare del [primo esempio]([[Esempio Semplice di Analisi 1]]) è molto più veloce
		- Spazio:
			- Identico al primo esempio (impiega solo 3 variabili intere con dimensione costante)