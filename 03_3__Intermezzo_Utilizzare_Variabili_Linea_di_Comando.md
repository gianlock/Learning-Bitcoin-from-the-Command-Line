# Intermezzo: Utilizzare Variabili della Linea di Comando

La sezione precedente ha mostrato una serie di istruzioni da riga di comando utilizzate senza offuscamento o interferenze. Tuttavia, spesso questo non è il modo migliore per eseguire Bitcoin dalla riga di comando. Poiché si ha a che fare con variabili lunghe, complesse e illeggibili, è facile commettere un errore se si copiano tali variabili (o, satoshi forfend, se si digitano a mano). Poiché queste variabili possono fare la differenza tra ricevere o perdere denaro reale, non si vuole commettere errori. Per queste ragioni, consigliamo vivamente di utilizzare le variabili della riga di comando per salvare indirizzi, firme o altre lunghe stringhe di informazioni ogni volta che è opportuno farlo.

Se si usa `bash`, si possono salvare le informazioni in una variabile come questa:
```
$ VARIABLE=$(command)
```
Si tratta di una semplice sostituzione di comando, l'equivalente di ``VARIABLE=`command` ``. Il comando all'interno delle parentesi viene eseguito e poi assegnato alla _VARIABLE_.

La creazione di un nuovo indirizzo risulterebbe quindi come segue:
```
$ unset NEW_ADDRESS_1
$ NEW_ADDRESS_1=$(bitcoin-cli getnewaddress "" legacy)
```
Questi comandi cancellano la variabile NEW_ADDRESS_1, per essere certi, e poi la riempiono con i risultati del comando `bitcoin-cli getnewaddress`.

Si può quindi utilizzare il comando `echo` della shell per visualizzare il (nuovo) indirizzo:
```
$ echo $NEW_ADDRESS_1
mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE
```
Poiché l'indirizzo è stato inserito in una variabile, ora è possibile firmare facilmente un messaggio per quell'indirizzo, senza preoccuparsi di sbagliare a digitare l'indirizzo. Naturalmente, anche la firma deve essere salvata in una variabile!
```
$ NEW_SIG_1=$(bitcoin-cli signmessage $NEW_ADDRESS_1 "Hello, World")
$ echo $NEW_SIG_1
IPYIzgj+Rg4bxDwCyoPiFiNNcxWHYxgVcklhmN8aB2XRRJqV731Xu9XkfZ6oxj+QGCRmTe80X81EpXtmGUpXOM4=
```
Il resto di questo corso utilizzerà questo stile di salvataggio delle informazioni nelle variabili quando è conveniente.

> :book: ***Quando non è pratico utilizzare variabili sulla linea di comando?*** Le variabili della riga di comando non sono pratiche se si ha bisogno di usare le informazioni da qualche altra parte che non sia la riga di comando. Ad esempio, salvare la propria firma potrebbe non essere utile se la si deve inviare a qualcun altro in un'e-mail. Inoltre, alcuni comandi futuri produrranno oggetti JSON invece di semplici informazioni, e le variabili non possono essere usate per catturare tali informazioni... almeno non senza _un po'_ di lavoro in più.

## Riepilogo: Utilizzare Variabili della Linea di Comando

Le variabili della shell possono essere utilizzate per contenere lunghe stringhe di Bitcoin, riducendo al minimo le possibilità di errore.

## Cosa c'è Dopo?

Continua "Capire la Tua Configurazione Bitcoin" con [§3.4: Ricevere Una Transazione](03_4_Ricevere_una_Transazione.md).
