exclude-from-graph-view:: true

- Scriviamo un algoritmo per la ricerca di un elemento in un array
	- Istanza in input: array $A$, elemento $x$
	- Questione in output: indice $i$ tale che $A[i] = x$, o $-1$ se $A$ non contiene $x$
- Prima soluzione: ricerca sequenziale
	- Scansiono tutto l'array per trovare l'elemento che cerco (o, se non è presente, fino alla fine)
	- ```
	  ALGORITMO ricercaSequenziale(Array A[0, ..., n-1], elemento x) -> indice 
	  ```
	- ```
	  i <- 0
	  WHILE i < n AND A[i] != x DO // si usa la LAZY EVALUATION (quindi non si considera A[i], aiutando a skippare errori di out of range) 
	  	i <- i+1
	  IF i = n 	THEN RETURN -1 // si scrive così e non A[i] != x perchè va out of range
	  			ELSE RETURN i
	  ```
	- Assumendo costo uniforme:
		- Caso migliore: 0 iterazioni (trovo subito)
		- Caso peggiore: n iterazioni (scansiono tutto l'array e non trovo niente)
		- Quindi il tempo è $\Theta(n)$
		- Lo spazio è $\Theta(1)$
- Si può migliorare leggermente per automatizzare la restituzione di -1
	- ```
	  ALGORITMO ricercaSequenziale(Array A[0, ..., n-1], elemento x) -> indice 
	  ```
	- ```
	  i <- n-1
	  WHILE i >= 0 AND A[i] != x DO
	  	i <- i-1
	  RETURN i
	  ```
	- La complessità è identica ma è più leggibile
- ---
- Supponiamo adesso che l'array sia ordinato: la ricerca diventa binaria/dicotomica
	- Funzionamento:
		- Prima confronto l'elemento con quello al centro dell'array
			- Se è uguale, ricerca finita
			- Se è maggiore, sarà nella seconda metà dell'array
			- Altrimenti è nella prima metà dell'array
		- Se non ho trovato l'elemento, applico la ricerca ricorsivamente in una delle due metà dell'array
		- Caso base della ricorsione: array di un elemento
			- Se l'elemento è uguale, allora l'abbiamo trovato
			- Altrimenti l'elemento non è nell'array
- Il vantaggio di questo algoritmo è che le prestazioni sono superiori al metodo precedente
- In pratica, useremo due valori, $sx$ e $dx$ che indicano il range di indici al quale siamo interessati
	- $sx$ indica il primo indice al quale siamo interessati
	- $dx$ indica il primo indice al quale non siamo interessati
	- ```
	  FUNZIONE ricercaRic (Array A, indice sx, indice sx, elemento x) -> indice
	  ```
	- ```
	  IF dx <= sx THEN RETURN -1 // se questo accade, l'array è vuoto
	  ELSE
	  	m <- (sx + dx)/2
	      IF x = A[m] THEN RETURN m
	      ELSE IF x < A[m] THEN
	      	RETURN ricercaRic(A, sx, m, x) // prima metà array
	      ELSE 
	      	RETURN ricercaRic(A, m+1, dx, x) // seconda metà array
	  ```
		- Usare la ricorsione in questo modo è detto "ricorsione in coda"
		-
	- Applichiamo questa funzione:
	- ```
	  ALGORITMO ricercaBinaria (Array A[0, n-1], elemento x) -> indice
	  ```
	- ```
	  RETURN ricercaRic(A, 0, n, x)
	  ```
- Cosa contiene il [[Record di attivazione]] ad ogni chiamata ricorsiva:
	- Puntatore all'array (non lo si copia tutto, sarebbe una perdita di tempo)
	- $sx$
	- $dx$
	- $x$
	- $m$
		- Trovato l'indice finale, esso viene propagato attraverso ogni record
- Valutiamo la complessità in funzione del numero di elementi dell'array:
	- Inizialmente, si compie una prima chiamata e lo spazio di ricerca è tutto l'array ($n$ elementi)
	- Se l'elemento non è stato trovato, si compie una seconda chiamata e lo spazio di ricerca è metà dell'array ($n/2$ elementi)
	- Se l'elemento non è ancora stato trovato, si compie una terza chiamata e lo spazio di ricerca è un quarto dell'array ($n/4$ elementi)
	- ...
	- Alla i-esima chiamata, lo spazio di ricerca è minore di $n / 2^{i-1}$ elementi
		- Per arrivare all'array con un elemento, si pone lo spazio di ricerca uguale a 1
			- Quindi $n / 2^{i-1} = 1$ per $n = 2^{i-1}$, quindi si avranno al più $i = 1 + \log_2 n$ chiamate
		- Da questo, per arrivare all'array vuoto (caso peggiore dove si compie la scansione maggiore possibile ma non si trova niente) si avranno al più $i = 2 + \log_2 n$ chiamate
	- Tempo:
		- Il numero di chiamate è $\Theta(\lg n)$
		- Se i confronti tra $x$ e $A[x]$ costano tempo costante, allora $T(n) = \Theta(\log n)$
	- Spazio:
		- $T(n) = \Theta(\log n)$