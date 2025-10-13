- Esercizio 1: Scrivete un programma che, ricevuto in input un numero intero $n > 0$, genera in maniera pseudo-casuale n caratteri scegliendoli uniformemente tra $a,b,...,y,z,0,1,...,9$ e li stampa su un file uno per linea (quindi separati tra loro dal carattere a capo `\n`).
	- ```
	  package main
	  
	  import (
	  	"fmt"
	  	"math/rand"
	  	"os"
	  )
	  
	  func main() {
	  
	  	// Crea file
	  	file, err := os.Create("test.txt")
	  
	  	// Se la creazione è andata a buon fine:
	  	if err == nil {
	  
	  		// Inizializza il numero da inserire in input e la pool di caratteri da pigliare
	  		n := 0
	  		chars := "abcdefghijklmnopqrstuvwxyz0123456789"
	  
	  		// Inserisci un valore n in input
	  		fmt.Scan(&n)
	  
	  		// Ripetere n volte il loop
	  		for i := 0; i < n; i++ {
	  
	  			// Seleziona un numero j tra 0 e n
	  			j := rand.Intn(len((chars)))
	  
	  			// Scrivi il carattere in posizione j + un newline nel file
	  			file.WriteString(string(rune(chars[j])) + "\n")
	  
	  		}
	  
	  	}
	  
	  }
	  ```
- Esercizio 2: Considerate un semplice programma che legge una serie di caratteri da un file input, separati dal carattere a capo `(\n)`, li concatena in un’unica stringa (separati da spazi), e stampa la stringa ottenuta su un nuovo file output. Scrivete due versioni del programma: la prima legge un carattere alla volta con un ciclo for, e li concatena uno ad uno a una stringa inizialmente vuota `s` usando l’operatore `+`. La seconda legge tutti i caratteri prima di concatenarli in un’unica stringa usando la funzione `strings.Join`. 
  Paragonate il tempo di esecuzione dei due programmi per un numero crescente di caratteri in input $(1000, 10000, 100000, 1000000)$ usando il pacchetto time. 
  Sapete giustificare la differenza nei tempi di esecuzione in termini di complessità asintotica? 
  Qual'è la complessità di ciascuna delle due versioni dell’algoritmo?
	- Ver. 1
		- ```
		  package main
		  
		  import (
		  	"fmt"
		  	"os"
		  	"time"
		  	"unicode"
		  )
		  
		  func main() {
		  
		  	start := time.Now()
		  
		  	file, err := os.ReadFile("input.txt")
		  
		  	if err == nil {
		  
		  		s := ""
		  
		  		for _, j := range file {
		  
		  			if !unicode.IsSpace(rune(j)) {
		  
		  				s += string(j)
		  
		  			}
		  
		  		}
		  
		  		fmt.Println(s)
		  
		  	}
		  
		  	end := time.Now()
		  
		  	fmt.Println("TEMPO:", end.Sub(start).String())
		  
		  }
		  ```
	- Ver. 2
		- ```
		  package main
		  
		  import (
		  	"fmt"
		  	"os"
		  	"strings"
		  	"time"
		  	"unicode"
		  )
		  
		  func main() {
		  
		  	start := time.Now()
		  
		  	file, err := os.ReadFile("input.txt")
		  
		  	if err == nil {
		  
		  		s_ar := make([]string, len(file))
		  
		  		for i, v := range file {
		  
		  			if !unicode.IsSpace(rune(v)) {
		  
		  				s_ar[i] = string(v)
		  
		  			}
		  
		  		}
		  
		  		fmt.Println(strings.Join(s_ar, ""))
		  
		  	}
		  
		  	end := time.Now()
		  
		  	fmt.Println(end.Sub(start).String())
		  
		  }
		  
		  ```
	- Tempi:
		- |Linee|Ver. 1|Ver.2|
		  |---|
		  |1000|11.2052ms|1.995ms|
		  |10000|41.7819ms|23.9137ms|
		  |100000|1.3905768s|142.3696ms|
		  |1000000|1m46.7185882s|1.622693s|
	- ...
- Esercizio 3:
	- Sia $A$ una slice di $n$ interi, ordinati in ordine crescente. Qual'è il costo asintotico di cancellare il primo elemento di $A$, ottenendo quindi una slice di lunghezza $n − 1$, se si vuole che la slice risultante sia ancora ordinata? E se non si richiede che il risultato sia ordinato?
	- ...
- Esercizio 4:
	- Scrivete un programma che legge un intero $n > 0$ da `stdin`, genera in modo casuale una slice di grandi interi con almeno 50 cifre l’uno e lo stampa. Notate che numeri così grandi non possono essere salvati come `int` nè come `int64`: usate il package Go `math/big`
	  `(https://pkg.go.dev/math/big#pkg-overview)`
	- ...