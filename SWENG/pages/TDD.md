- AKA Test Driven Development
- Tecnica di progettazione di software che guida verso il design più semplice
- E' test-first (ossia, il primo passo da svolgere è creare il test che controlla che il codice sia corretto) e si avanza passo passo
	- Facendo questo creo scelte di design e consolido le specifiche
- Funziona seguendo questi passi:
	- Scrivere un test che fallisce (se non fallisce, vuol dire che è inutile)
	  logseq.order-list-type:: number
	- Farlo passare (nella maniera più semplice possibile)
	  logseq.order-list-type:: number
		- NB: Anche gli altri test devono continuare a passare, ossia non deve causare regressioni
		- NB2: Se entro un tempo breve continua a non funzionare, si riparte da capo
	- Refactor
	  logseq.order-list-type:: number
	- Ripeti ogni 2-10 min
	  logseq.order-list-type:: number