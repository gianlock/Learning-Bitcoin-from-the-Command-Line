# 3.1: Verificare la Tua Configurazione Bitcoin

Prima di iniziare a sperimentare con Bitcoin, è necessario verificare che tutto sia configurato correttamente.

## Crea i tuoi alias

Suggeriamo di creare alcuni alias per facilitare l'utilizzo di Bitcoin.

Lo puoi fare inserendoli nel tuo `.bash_profile`, `.bashrc` o `.profile`.
```
cat >> ~/.bash_profile <<EOF
alias btcdir="cd ~/.bitcoin/" #linux default bitcoind path
alias bc="bitcoin-cli"
alias bd="bitcoind"
alias btcinfo='bitcoin-cli getwalletinfo | egrep "\"balance\""; bitcoin-cli getnetworkinfo | egrep "\"version\"|connections"; bitcoin-cli getmininginfo | egrep "\"blocks\"|errors"'
EOF
```
Dopo aver inserito questi alias, è possibile eseguire `source .bash_profile` per aggiungerli o semplicemente uscire e rientrare.

Nota che questi alias includono scorciatoie per l'esecuzione di `bitcoin-cli`, per l'esecuzione di `bitcoind` e per accedere alla directory di Bitcoin. Questi alias hanno come scopo principale quello di semplificare la vita dell'utente. Ti consigliamo di creare altri alias per facilitare l'uso di comandi (e argomenti) frequenti e per ridurre al minimo gli errori. Gli alias di questo tipo possono essere ancora più utili se si ha una configurazione complessa in cui si eseguono regolarmente comandi associati alla Mainnet, alla Testnet, _e_ alla Regtest, come spiegheremo più avanti.

Detto questo, l'uso di questi alias in _questo_ documento potrebbe accidentalmente sviare dalle dalle informazioni centrali su Bitcoin, quindi l'unico alias usato direttamente qui è `btcinfo` perché racchiude comandi molto più lunghi e complessi. Per il resto, mostreremo i comandi completi; adattateli all'uso che ne farete.

## Eseguire Bitcoind

Inizierai la tua esplorazione della rete Bitcoin con il comando `bitcoin-cli`. Tuttavia, bitcoind deve essere in funzione per utilizzare bitcoin-cli, poiché bitcoin-cli invia comandi JSON-RPC a bitcoind. Se si utilizza la nostra configurazione standard, bitcoind dovrebbe essere già attivo e funzionante. Si può verificare guardando la lista dei processi.
```
$ ps auxww | grep bitcoind
standup    455  1.3 34.4 3387536 1392904 ?     SLsl Jun16  59:30 /usr/local/bin/bitcoind -conf=/home/standup/.bitcoin/bitcoin.conf
```
Se non è in esecuzione, occorre eseguire `/usr/local/bin/bitcoind -daemon` a mano e inserirlo nel crontab.

## Verifica i tuoi blocchi

Dovresti aver scaricato l'intera blockchain prima di iniziare a smanettare. Basta eseguire l'alias `bitcoin-cli getblockcount` per vedere se è stata scaricata tutta. 
```
$ bitcoin-cli getblockcount
1772384
```
Questo ti dice cosa è stato scaricato; dovrai quindi verificarlo con un servizio online che ti indichi l'altezza attuale del blocco.

> :book: ***Cos'è l'altezza del blocco?*** L'altezza del blocco è la distanza che separa un determinato blocco dal blocco di genesi. L'altezza del blocco attuale è l'altezza del blocco più recente aggiunto alla blockchain.

È possibile farlo osservando un blocknet explorer, come [il Blockcypher Testnet explorer](https://live.blockcypher.com/btc-testnet/). Il numero più recente corrisponde al tuo `getblockcount`? Se sì, sei aggiornato.

Se desideri un alias per guardare tutto in una volta, il seguente funziona attualmente per Testnet, ma potrebbe anche cambiare in futuro:
```
$ echo "alias btcblock='echo \$(bitcoin-cli -testnet getblockcount)/\$(curl -s https://blockstream.info/testnet/api/blocks/tip/height)'" >> .bash_profile
$ source .bash_profile 
$ btcblock
1804372/1804372
```

> :link: **TESTNET vs MAINNET:** Ricordati che questa esercitazione presuppone in generale che si stia utilizzando la testnet. Se invece si utilizza la mainnet, è possibile recuperare l'altezza del blocco corrente con: `curl -s https://blockchain.info/q/getblockcount`. È possibile sostituire l'ultima metà dell'alias `btcblock` (dopo `/\$(`)) con questo link.

Se non si è aggiornati, ma il proprio `getblockcount` sta aumentando, non c'è problema. Il tempo totale di download può richiedere da un'ora a diverse ore, a seconda della vostra configurazione.

## Opzionale: Conoscere i tipi di server

> **TESTNET vs MAINNET:** Quando si configura il nodo, si sceglie di crearlo come nodo Mainnet, Testnet o Regtest. Sebbene questo documento presuma una configurazione testnet, vale la pena di capire come si può accedere e utilizzare gli altri tipi di configurazione, anche sulla stessa macchina! Tuttavia, se si è alle prime armi, si può passare oltre, perché non è necessario per una configurazione di base.

Il tipo di configurazione è controllato principalmente attraverso il file ~/.bitcoin/bitcoin.conf. Se si sta eseguendo in testnet, probabilmente contiene questa riga:
```
testnet=1
```
Se si sta eseguendo in regtest, probabilmente contiene questa riga:
```
regtest=1
```
Tuttavia, se si desideri eseguire diversi tipi di nodi contemporaneamente, è necessario omettere il flag testnet (o regtest) dal file di configurazione. Ogni volta che si esegue bitcoind o bitcoin-cli si può scegliere se utilizzare la mainnet, la testnet o la regtest.

Ecco un insieme di alias che semplificherebbe il tutto, creando un alias specifico per avviare e arrestare bitcoind, per accedere alla directory bitcoin e per eseguire bitcoin-cli, per la mainnet (che non ha flag aggiuntivi), la testnet (che è -testnet) o la regtest (che è -regtest).
```
cat >> ~/.bash_profile <<EOF
alias bcstart="bitcoind -daemon"
alias btstart="bitcoind -testnet -daemon"
alias brstart="bitcoind -regtest -daemon"

alias bcstop="bitcoin-cli stop"
alias btstop="bitcoin-cli -testnet stop"
alias brstop="bitcoin-cli -regtest stop"

alias bcdir="cd ~/.bitcoin/" #linux default bitcoin path
alias btdir="cd ~/.bitcoin/testnet" #linux default bitcoin testnet path
alias brdir="cd ~/.bitcoin/regtest" #linux default bitcoin regtest path

alias bc="bitcoin-cli"
alias bt="bitcoin-cli -testnet"
alias br="bitcoin-cli -regtest"
EOF
```
Per una complessità ancora maggiore, si potrebbe fare in modo che ciascuno dei propri alias "start" utilizzi il flag -conf per caricare la configurazione da un file diverso. Questo va ben oltre lo scopo di questo tutorial, ma lo proponiamo come punto di partenza per quando le vostre sperimentazioni su Bitcoin raggiungeranno il livello successivo.

## Riepilogo: Verificare la Tua Configurazione Bitcoin

Prima di iniziare a sperimentare con bitcoin, devi assicurarti che i tuoi alias siano impostati, che il tuo bitcoind sia in funzione e che i tuoi blocchi siano scaricati. Se si è un utente avanzato, si può anche impostare l'accesso a configurazioni alternative di Bitcoin.

## Cosa c'è Dopo?

Continua il capitolo "Capire la Tua Configurazione Bitcoin" con [§3.2: Conoscere la Tua Configurazione Bitcoin](03_2_Conoscere_la_Tua_Configurazione_Bitcoin.md).
