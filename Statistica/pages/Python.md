## Dati e variabili
- ```
  # Assegnazione di variabili
  
  x = 42 		#variabile di tipo intero, senza virgola
  x = 35.0 	#variabile di tipo float, con la virgola
  x = False	#variabile di tipo booleano, valore "binario" (vero o falso)
  ```
- ```
  # Impiego di type() per ottenere il tipo di una variabile
  
  type(x)		#restituisce il tipo di dato di variabile
  type(42)	#restituisce "int" 
  ```
- id:: 68d7cee7-7389-4791-9ca7-1de3fbce0246
  ```
  # Casting di variabili usando 
  
  int("42") #svolge il casting implicito, qualora possibile
  int("a") #qui restituirebbe un'eccezione
  ```
- |**Operazione**|**Simbolo**|
  |--|
  |addizione| `+` |
  |sottrazione|`-`|
  |moltiplicazione|`*`|
  |divisione reale|`/`|
  |divisione intera|`//`|
  |resto/modulo|`%`|
  |elevamento a potenza|`**`|
  |uguale|`==`|
  |diverso|`"!=`|
  |minore|`<`|
  |maggiore|`>`|
  |minore o uguale|`<=`|
  |maggiore o uguale|`>=`|
- ## Tipi di dati strutturati
- Prima di cominciare, definiamo:
	- Operatori: simbolo che specifica quale legge applicare a uno o più operandi, per generare un'espressione (ad esempio tutti quelli listati sopra)
	- Funzioni: unità di organizzazione del codice che permette di raggruppare una sequenza di istruzioni in un unico blocco, impiegata in linguaggi più procedurali
	- Metodi su oggetti/classi: equivalenti delle funzioni nei linguaggi più orientati agli oggetti
- ---
- Lista: struttura dati *eterogenea* ad *accesso posizionale* che è *mutabile*
	- ```
	  # Definire liste:
	  
	  lista_esempio = [	'Elemento 1',
	  					2.0,
	                      3,
	                      False]
	                     
	                     # Si nota che è eterogenea
	  ```
	- ```
	  # Indicizzazione della lista
	  
	  # Per accedere agli elementi della lista, si usa un numero che indica la sua posizione
	  
	  lista_esempio[1] 	#seleziona l'elemento in posizione 1 (ossia al secondo posto)
	  lista_esempio[-2] 	#seleziona l'elemento in posizione -2 (ossia al 0-2 = -2 = penultimo posto)
	  					#(NB. -1 indica quindi l'ultimo elemento)
	  ```
	- ```
	  # Slicing
	  
	  # Creazione di una sotto-lista partendo da una lista esistente
	  
	  lista_esempio[2:4]	#individua la sottolista che va dall'elemento in posizione 2 a quello in posizione 4-1 = 3
	                      #(nb. lista[x:y] indica la sottolista indicando x, il primo elemento da includere, e y, il primo elemento da escludere)
	                      #(nb2. si possono impiegare anche gli indici negativi)
	                  
	  ```
	- ```
	  # Operatori
	  
	  # Operatore "in"
	  # Ritorna True se l'elemento è nella lista, altrimenti ritorna False
	  
	  2.0 in lista_esempio		#restituisce "True"
	  True in lista_esempio 		#restituisce "False"
	  
	  # Operatore "del"
	  # Fornito un indice, elimina l'elemento corrispondente dalla lista. Non restituisce alcun valore
	  
	  del lista_esempio[0] 	#elimina l'elemento in posizione 0 della lista
	  ```
	- ```
	  # Funzioni
	  
	  # Funzione "len"
	  # Restituisce la lunghezza della lista, ossia il numero di elementi nella stessa
	  
	  len(lista_esempio)		#restituisce "3" (o "4" se si considera l'elemento eliminato)
	  ```
	- ```
	  # Metodi
	  
	  # Metodo "lista.sort()"
	  # Riordina gli elementi. Non restituisce alcun valore
	  
	  lista_esempio.sort() 				#riordina seguendo l'ordine di default (nel caso di names, quello alfabetico)
	  lista_esempio.sort(reverse=True) 	#riordina seguento l'ordine di default ma al contrario
	  lista_esempio.insert(4, 'Aquaman')	#inserisci un elemento nella posizione specificata (in questo caso 4)
	  ```
	- ```
	  # Funzione lambda/anonima
	  
	  # Funzione definita specificando direttamente il metodo con il quale i suoi argomenti vengono trasformati
	  
	  lambda x: x*2 					#funzione lambda che raddoppia x
	  successore = lambda x: x + 1 	#una funzione lambda è salvabile in una variabile per essere riutilizzata in seguito
	  successore(9) 					#equivale a 10
	  
	  # Uso delle lambda in sort()
	  
	  lista_esempio.sort(key = lambda n: len(n)) 	#si può definire una funzione lambda per ordinare una lista
	  ```
- ---
- Tupla: lista *immutabile*
	- ```
	  # Definire tuple: 
	  
	  tupla_esempio 	= (	'Elemento 1',
	  					2.0,
	                      3,
	                      False)
	  ```
	- ```
	   # Operatori e funzioni identici a quelle delle liste, meno quelli che la modificano (ovviamente)
	  ```
- ---
- Stringa: tupla di *caratteri*
	- ```
	  # Definire stringhe
	  
	  name = 'Il nome'
	  name[1] #stampa 'l'
	  ```
	- ```
	  # Operatori e funzioni identici a quelle delle tuple
	  ```
- ---
- Dizionario: insieme di coppie (*chiave, valore*)
	- ```
	  # Definire dizionario
	  
	  dizionario_esempio = {	'nome': "Mario",
	  						'cognome': "Rossi",
	                          'età': 56,
	                          'occupazione': "operaio"}
	  ```
	- ```
	  # Indicizzazione
	  
	  dizionario_esempio['età'] #il valore identificato dalla chiave 'identity' è '56'
	  ```
	- ```
	  # Funzioni
	  
	  dizionario_esempio.items() #restituisce una lista di tuple [(chiave1, elemento1), (chiave2, elemento2)...]
	  ```
	- ```
	  # Operatore "in"
	  
	  name in dizionario_esempio #restituisce "True" se esiste la chiave "name" in "dizionario_esempio", altrimenti ritorna "False"
	  ```
- ---
- Altre funzioni generali:
	- ```
	  # sorted()
	  # Funzione che riordina una struttura dati iterabile. Se si specifica una chiave, ordina in base ad essa; 
	  # può anche svolgere questa operazione in ordine inverso
	  
	  sorted(struttura_dati_iterabile, key=chiave_specificata_per_ordinare, reverse=...) #
	  
	  # sum()
	  # Funzione che somma tutti i valori di una struttura di dati iterabile
	  
	  sum(lista_num)
	  ```
- ## Strutture di controllo
	- ```
	  # Iterazione elementi del dizionario
	  
	  for y in lista:
	  	...
	      f(y) #NB: y deve esistere. Si controlla con un semplice "if"
	      ...
	  ```
	- ```
	  # List comprehension
	  
	  # Procedura di creazione di una lista in maniera intensiva, trasformandone una già esistente
	  # Generalizzata in h = [f(e) for e in l]
	  ```
- ## Importare moduli/package
	- Un modulo è un file che contiene la definizione di una o più funzioni o classi
		- ```
		  # Importare un modulo da una collezione di moduli
		  
		  from collezione import modulo
		  ```
		- ```
		  # Importare un modulo intero
		  
		  import x 
		  ```
		- id:: 68df87d8-a165-4e75-9a26-e4c41eaabf61
		  ```
		  # Dare un diminutivo al modulo 
		  
		  import module as md
		  ```
	- Un package è un file che contiene più moduli in una struttura gerarchica
		- ```
		  # Importare un modulo da un package
		  
		  import package.module
		  ```
- ## Moduli importanti
	- Collections: da esso si prende *defaultdict*, che è comodo per la creazione di dizionari
		- ```
		  dizionario_zero = defaultdict(int) #siccome ho specificato int, tutti i valori saranno messi a zero
		  ```
	- Numpy: introduce funzioni utili e gli *array* (liste di tipo omogeneo)
		- ```
		  import numpy as np
		  	
		  np.argmax(lista_esempio) 					#trova l'argomento che si ripete più volte nella lista_esempio (frequenza assoluta massima)
		  
		  np.arange(start, end, gap) 					#genera un array di che parte da "start", arriva a "end" e va avanti di "gap" in "gap" 
		  
		  array_esempio = np.array(lista_esempio) 	#array generato da una lista omogenea
		  array_esempio.transpose()				 	#fornisce una vista trasposta dell'array ("lo gira" di 90 gradi)
		  x, y = array_esempio 						#assegno a x, y i valori delle due "righe" dell'array trasposto
		  
		  np.round(x, num_cifre_decimali)				#arrotonda x ad avere un numero determinato di cifre decimali
		  
		  #NB: si possono eseguire operazioni aritmetiche sull'array:
		  array_esempio * 2
		  ```
	- Pandas: introduce *serie* e *dataframe*
		- ```
		  import pandas as pd
		  
		  # Serie 
		  
		  serie_esempio = pd.Series(valori_serie, index = indice_serie) 	#introduce una serie, una specie di lista con un indice e funzioni specifiche 
		  
		  serie_esempio['indice_esempio'] 									#indicizzabile tramite nome
		  serie_esempio.iloc[x] 												#indicizzabile tramite posizione
		  
		  serie_esempio['indice_esempio_1':'indice_esempio_2']				#creazione slice tramite nomi
		  serie_esempio[x:y]	 												#creazione slice tramite posizione
		  
		  serie_esempio.iloc[[x, y, ..., z]] 									#prende tutti gli elementi nelle posiz
		  serie_esempio[[list_comprehension]]						 			#seleziona tutti gli elementi nei quali la comprehension restituisce "True"
		  #ESEMPIO:
		  	
		  serie_esempio[condizione booleana che coinvolge serie_esempio]		#seleziona tutti gli indici che soddisfano la condizione
		  #ESEMPIO:
		  serie_esempio[serie_esempio > 5]
		  
		  freq_esempio = serie_esempio.value_counts() 						#restituisce una serie nella quale:
		  																	#indice = valori osservati, 
		                                                                  	#valori = frequenze assolute (ordine non crescente)
		                                                                  	
		  serie_esempio.sort_index()											#riordina la serie in base all'indice
		  serie_esempio.index 												#restituisce gli indici della serie
		  
		  serie_esempio.apply(funzione_lambda)								#modifica tutti gli elementi della serie in base alla funzione lambda
		  
		  # Dataframe
		  
		  dataframe_esempio = pd.read_csv('data.csv', sep=";", index_col = 0)	#un dataframe è una collezione di serie con lo stesso indice
		  																	#i dataframe verranno generati leggendo CSV
		  dataframe_esempio['Colonna'] 										#restituisce una lista leggendo una colonna
		  dataframe_esempio['Colonna 1':'Colonna 2']							#restituisce un sub-dataframe sliceato
		  dataframe_esempio[x:y]												#come sopra
		  dataframe_esempio.loc['Riga']										#restituisce una serie
		  dataframe_esempio.loc['Riga', 'Colonna 1':'Colonna 2']				#restituisce una serie con solo gli attributi tra le due colonne
		  #NB: si può usare anche iloc con numeri
		  dataframe_esempio.at['Riga', 'Colonna']								#seleziona l'attributo alla posizione specificata
		  #NB: si può usare anche iat con numeri
		  dataframe_esempio.sort_values(by='Colonna', ascending=...)			#ordina in base ai valori Colonna e de/crescente
		  dataframe_esempio.sort_index()										#ordina in base all'indice
		  
		  # dataframe_esempio[f(dataframe_esempio['Colonna'])] ove f restituisce un valore booleano
		  
		  # Altro
		  
		  # Analisi frequenza dataframe
		  pd.crosstab(index=dataframe_esempio['Colonna'], colonne=['C1', 'C2', ...], colnames=['Etichetta per tabella'], normalize=assoluta_o_relativa)
		  #NB: se si vuole una frequenza assoluta si usa normalize=False, altrimenti =true
		  #NB2: si può fare una selezione facendo, ad esempio, index=dataframe_esempio['Colonna']=='Valore'
		  
		  elemento_esempio.head(x) 											#prende i primi x elementi di un elemento iterabile 
		  elemento_esempio.tail(x) 											#prende gli ultimi x elementi di un elemento iterabile
		  ```
	- Pyplot: permette di disegnare *grafici*
		- ```
		  import matplotlib.pyplot as plt
		  
		  plt.bar(x, y)												#genera un grafico a barre partendo da un indice x e da valori y 
		  															#(presumibilmente frequenze)
		  freq_esempio.plot.bar() 									#genera un grafico a barre partendo da una serie che usa pandas
		  #NB: anche i dataframe funzionano bene con .plot.bar(), ponendo se si vuole l'argomento legend a False
		  
		  plt.plot(index=dati, marker='o di solito', color='colore') 	#genera un grafico poligonale
		  
		  #NB: plot e plot.bar hanno anche gli argomenti color e alpha
		  
		  plt.vlines(indice, 0, valori) 								#grafico a barre molto molto sottili
		  
		  # ISTOGRAMMA
		  valore.hist(bins=numero_bins)								#genera istogramma (numero bins=numero suddivisione intervalli)
		  															#usando arange
		  
		  plt.xlim((x1,x2)) 			#limita il grafico orizzontalmente
		  plt.ylim((y1,y2)) 			#limita il grafico verticalmente
		  plt.show() 					#comando finale di ogni grafico generato con plt
		  ```
	- CSV: permette di importare file *csv* (comma separated values)
		- ```
		  import csv
		  
		  with open('data.csv', 'r') as file: 								#apre il file in lettura
		    reader = csv.reader(file, delimiter=';', quotechar='"') 			#salva i contenuti del file specificando delimitatori e caratteri di virgole
		    data = list(reader)[1:] 											#salva il file come lista, tralasciando le intestazioni dei campi
		  ```