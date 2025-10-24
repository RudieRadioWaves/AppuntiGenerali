- "Selection" = "selezione" di una parte dell'array ordinata o da ordinare
- ```
  ALGORITMO selectionSort(array A[0, ..., n-1)]
  ```
- ```
  FOR k <- 0 TO n-1 DO
  	// ricerca la posizione m del minimo tra gli elementi del da posizione k a n-1
      m <- k
      FOR j <- k+1 TO n-1 DO
      	IF A[j] < A[m] THEN
          	m <- j
      scambia A[m] con A[k]
  ```