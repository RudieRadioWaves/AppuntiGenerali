- Svolgiamo ordunque l'[[Analisi]] della moltiplicazione in colonna tra due elementi $a, b \geq 0$
	- Numero di prodotti ad una cifra: lunghezza $a$ $\times$ lunghezza di $b$
	- Numero di somme: numero pari a lunghezza $b$ + riporti
	- [[Pseudocodice]] basato sulle somme iterate (ossia, salvataggio in una variabile di una somma fatta più volte, simulando la moltiplicazione)
		- ```
		  ALGORITMO moltiplicazione_sommeiterate (intero a, intero b) -> intero
		  ```
		- ```
		  	prodotto <- 0
		  	WHILE b > 0 DO 
		      	prod <- prod+a
		  		b <- b-1
		  	return prodotto
		  ```
		- Valutiamo la [[Correttezza]]
			- La variabile $a$ non viene mai modificata, mentre $b$ e $prodotto$ si
				- Si definiscono $b_i, prodotto_i$ come i valori di $b$ e $prodotto$ dopo l'iterazione $i$ (valore che equivale a 0 durante la prima iterazione)
				- Si può dimostrare che $b_i = b - i$ e $prodotto_i = a \times i$
				- Dimostrazione:
					- CASO BASE: $i = 0$
						- Mi aspetto che $b_0 = b$ e $prodotto_0 = 0$ (all'inizializzazione)
						- Applicando il lemma, $b_0 = b - 0 = b$ e $prodotto_0 = a \times 0 = 0$
						- Il caso base è quindi dimostrato
					- INDUZIONE: $i - 1 \rightarrow i$
						- Mi aspetto che $b_i = b_{i - 1}$ e $prodotto_i = prodotto_{i - 1} + a$ (seguendo l'iterazione dell'algoritmo)
						- Applicando il lemma,
							- $b_i = b_{i -1} - 1$ che induttivamente $= b - (i-1) - 1 = b - i$
							- $prodotto_i = prodotto_{i - 1} + a$ che induttivamente $= a \times (i - 1) + a = a \times i$
						- Dimostrato!
				- Sapendo questo, all'iterazione $i = b$, $b_b = 0$ e quindi il ciclo WHILE termina, restituendo $prodotto_b = a \times b$
		- Valutiamo l' [[Efficienza]]
			- Come posso analizzare il tempo usato dal programma?
			- Osserviamo il numero di linee di codice eseguite ad ogni iterazione, legandole ad una quantità di tempo unitaria
				- Con $b = 0$, si eseguono le linee di codice 1, 2 e 5, impiegando quindi tempo 3
				- Con $b > 0$, si eseguono:
					- le linee di codice 1, 5 una volta, impiegando quindi tempo 4
					- le linee 3, 4 una volta per iterazione, ed essendoci $b$ iterazioni impiegano quindi tempo $2b$
					- la linea 2 una volta per iterazione, più una successiva volta per terminare il ciclo, impiegando quindi tempo $b+1$
			- In totale quindi:
				- Il tempo in funzione di $b$ è $3b + 3$, crescendo linearmente in base a $b$
				- Lo spazio impiega solo 3 variabili intere con dimensione costante (in quanto non dipendono dai valori di $a$ e $b$)