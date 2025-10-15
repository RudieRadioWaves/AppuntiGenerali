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