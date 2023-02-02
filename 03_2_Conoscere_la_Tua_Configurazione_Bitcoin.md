# 3.2: Conoscere la Tua Configurazione

Prima di iniziare a sperimentare con Bitcoin, ti consigliamo di comprendere al meglio la tua configurazione.

## Conosci la Directory di Bitcoin.

Per cominciare, bisogna capire dove viene memorizzato il tutto: la directory `~/.bitcoin`.

La directory principale contiene solo il file di configurazione e la directory di testnet:
```
$ ls ~/.bitcoin
bitcoin.conf  testnet3
```
Le guide all'installazione del [Capitolo Due: Configurazione di un Bitcoin-Core VPS](02_0_Configurazione_di_un_VPS_Bitcoin-Core.md) hanno presentato un file di configurazione standardizzato. [§3.1: Verificare la Tua Configurazione Bitcoin](03_1_Verificare_la_Tua_Configurazione_Bitcoin.md) ha suggerito come modificarlo per supportare setup più avanzati. Se sei interessato a saperne di più sul file di configurazione, puoi consultare [Jameson Lopp's Bitcoin Core Config Generator].(https://jlopp.github.io/bitcoin-core-config-generator/).

Tornando alla tua directory ~/.bitcoin, vedrai che la cartella testnet3 contiene tutte le componenti essenziali:
```
$ ls ~/.bitcoin/testnet3
banlist.json   blocks	  debug.log	     mempool.dat	peers.dat
bitcoind.pid  chainstate  fee_estimates.dat  onion_private_key	wallets
```
Non è consigliabile intervenire sulla maggior parte di questi file e directory, in particolare sulle directory `blocks` e `chainstate`, che contengono tutti i dati della blockchain, e sulle informazioni contenute nella directory `wallets`, che contiene il wallet personale. Tuttavia, è bene prestare attenzione al file `debug.log`, a cui fare riferimento in caso di problemi con la configurazione.

> :link: **TESTNET vs MAINNET:** Se si usa la mainnet, allora _tutto_ sarà collocato nella directory principale `~/.bitcoin`. Queste diverse configurazioni sono elegantemente sovrapponibili, quindi se si utilizzano mainnet, testnet e regtest, vedrai che `~/.bitcoin` contiene il file di configurazione e i dati della mainnet, la directory `~/.bitcoin/testnet3` contiene i dati della testnet e la directory `~/.bitcoin/regtest` contiene i dati della regtest.

## Conoscere i Comandi di Bitcoin-cli

La maggior parte del lavoro iniziale sarà svolto con il comando `bitcoin-cli`, che offre una facile interfaccia con `bitcoind`. Se si desiderano maggiori informazioni sul suo utilizzo, basta lanciarlo con l'argomento `help`. Senza altri argomenti, mostra tutti i comandi possibili:
```
$ bitcoin-cli help
== Blockchain ==
getbestblockhash
getblock "blockhash" ( verbosity )
getblockchaininfo
getblockcount
getblockfilter "blockhash" ( "filtertype" )
getblockhash height
getblockheader "blockhash" ( verbose )
getblockstats hash_or_height ( stats )
getchaintips
getchaintxstats ( nblocks "blockhash" )
getdifficulty
getmempoolancestors "txid" ( verbose )
getmempooldescendants "txid" ( verbose )
getmempoolentry "txid"
getmempoolinfo
getrawmempool ( verbose )
gettxout "txid" n ( include_mempool )
gettxoutproof ["txid",...] ( "blockhash" )
gettxoutsetinfo
preciousblock "blockhash"
pruneblockchain height
savemempool
scantxoutset "action" ( [scanobjects,...] )
verifychain ( checklevel nblocks )
verifytxoutproof "proof"

== Control ==
getmemoryinfo ( "mode" )
getrpcinfo
help ( "command" )
logging ( ["include_category",...] ["exclude_category",...] )
stop
uptime

== Generating ==
generatetoaddress nblocks "address" ( maxtries )
generatetodescriptor num_blocks "descriptor" ( maxtries )

== Mining ==
getblocktemplate ( "template_request" )
getmininginfo
getnetworkhashps ( nblocks height )
prioritisetransaction "txid" ( dummy ) fee_delta
submitblock "hexdata" ( "dummy" )
submitheader "hexdata"

== Network ==
addnode "node" "command"
clearbanned
disconnectnode ( "address" nodeid )
getaddednodeinfo ( "node" )
getconnectioncount
getnettotals
getnetworkinfo
getnodeaddresses ( count )
getpeerinfo
listbanned
ping
setban "subnet" "command" ( bantime absolute )
setnetworkactive state

== Rawtransactions ==
analyzepsbt "psbt"
combinepsbt ["psbt",...]
combinerawtransaction ["hexstring",...]
converttopsbt "hexstring" ( permitsigdata iswitness )
createpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime replaceable )
createrawtransaction [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime replaceable )
decodepsbt "psbt"
decoderawtransaction "hexstring" ( iswitness )
decodescript "hexstring"
finalizepsbt "psbt" ( extract )
fundrawtransaction "hexstring" ( options iswitness )
getrawtransaction "txid" ( verbose "blockhash" )
joinpsbts ["psbt",...]
sendrawtransaction "hexstring" ( maxfeerate )
signrawtransactionwithkey "hexstring" ["privatekey",...] ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
testmempoolaccept ["rawtx",...] ( maxfeerate )
utxoupdatepsbt "psbt" ( ["",{"desc":"str","range":n or [n,n]},...] )

== Util ==
createmultisig nrequired ["key",...] ( "address_type" )
deriveaddresses "descriptor" ( range )
estimatesmartfee conf_target ( "estimate_mode" )
getdescriptorinfo "descriptor"
signmessagewithprivkey "privkey" "message"
validateaddress "address"
verifymessage "address" "signature" "message"

== Wallet ==
abandontransaction "txid"
abortrescan
addmultisigaddress nrequired ["key",...] ( "label" "address_type" )
backupwallet "destination"
bumpfee "txid" ( options )
createwallet "wallet_name" ( disable_private_keys blank "passphrase" avoid_reuse )
dumpprivkey "address"
dumpwallet "filename"
encryptwallet "passphrase"
getaddressesbylabel "label"
getaddressinfo "address"
getbalance ( "dummy" minconf include_watchonly avoid_reuse )
getbalances
getnewaddress ( "label" "address_type" )
getrawchangeaddress ( "address_type" )
getreceivedbyaddress "address" ( minconf )
getreceivedbylabel "label" ( minconf )
gettransaction "txid" ( include_watchonly verbose )
getunconfirmedbalance
getwalletinfo
importaddress "address" ( "label" rescan p2sh )
importmulti "requests" ( "options" )
importprivkey "privkey" ( "label" rescan )
importprunedfunds "rawtransaction" "txoutproof"
importpubkey "pubkey" ( "label" rescan )
importwallet "filename"
keypoolrefill ( newsize )
listaddressgroupings
listlabels ( "purpose" )
listlockunspent
listreceivedbyaddress ( minconf include_empty include_watchonly "address_filter" )
listreceivedbylabel ( minconf include_empty include_watchonly )
listsinceblock ( "blockhash" target_confirmations include_watchonly include_removed )
listtransactions ( "label" count skip include_watchonly )
listunspent ( minconf maxconf ["address",...] include_unsafe query_options )
listwalletdir
listwallets
loadwallet "filename"
lockunspent unlock ( [{"txid":"hex","vout":n},...] )
removeprunedfunds "txid"
rescanblockchain ( start_height stop_height )
sendmany "" {"address":amount} ( minconf "comment" ["address",...] replaceable conf_target "estimate_mode" )
sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount replaceable conf_target "estimate_mode" avoid_reuse )
sethdseed ( newkeypool "seed" )
setlabel "address" "label"
settxfee amount
setwalletflag "flag" ( value )
signmessage "address" "message"
signrawtransactionwithwallet "hexstring" ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
unloadwallet ( "wallet_name" )
walletcreatefundedpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime options bip32derivs )
walletlock
walletpassphrase "passphrase" timeout
walletpassphrasechange "oldpassphrase" "newpassphrase"
walletprocesspsbt "psbt" ( sign "sighashtype" bip32derivs )

== Zmq ==
getzmqnotifications
```
È possibile anche digitare `bitcoin-cli help [comando]` per ottenere informazioni più dettagliate su quel comando. Ad esempio:
```
$ bitcoin-cli help getmininginfo
...
Returns a json object containing mining-related information.
Result:
{                              (json object)
  "blocks" : n,                (numeric) The current block
  "currentblockweight" : n,    (numeric, optional) The block weight of the last assembled block (only present if a block was ever assembled)
  "currentblocktx" : n,        (numeric, optional) The number of block transactions of the last assembled block (only present if a block was ever assembled)
  "difficulty" : n,            (numeric) The current difficulty
  "networkhashps" : n,         (numeric) The network hashes per second
  "pooledtx" : n,              (numeric) The size of the mempool
  "chain" : "str",             (string) current network name (main, test, regtest)
  "warnings" : "str"           (string) any network and blockchain warnings
}

Examples:
> bitcoin-cli getmininginfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id": "curltest", "method": "getmininginfo", "params": []}' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
> :book: ***Cos'è RPC?*** `bitcoin-cli` è solo un'interfaccia pratica che consente di inviare comandi a `bitcoind`. Più precisamente, è un'interfaccia che consente di inviare comandi RPC (o Remote Procedure Protocol) al `bitcoind`. Spesso il comando `bitcoin-cli` e il comando RPC hanno nomi e interfacce identici, ma alcuni comandi `bitcoin-cli` forniscono invece scorciatoie per richieste RPC più complesse. Generalmente, l'interfaccia `bitcoin-cli` è molto più pulita e semplice rispetto al tentativo di inviare comandi RPC a mano, usando `curl` o qualche altro metodo. Tuttavia, ha anche delle limitazioni rispetto a ciò che è possibile fare in definitiva.

## Opzionale: Conoscere le Info Bitcoin

Una serie di comandi di bitcoin-cli possono fornire ulteriori informazioni sui dati di bitcoin. I più generali sono:

`bitcoin-cli -getinfo` restituisce informazioni da RPC differenti (facile da usare)

```diff
$ bitcoin-cli -getinfo

! Chain: test
Blocks: 1977694
Headers: 1977694
Verification progress: 0.9999993275374796
Difficulty: 1

+ Network: in 0, out 8, total 8
Version: 219900
Time offset (s): 0
Proxy: N/A
Min tx relay fee rate (BTC/kvB): 0.00001000

@@ Wallet: ""@@
Keypool size: 1000
Unlocked until: 0
Transaction fee rate (-paytxfee) (BTC/kvB): 0.00000000

# Balance: 0.02853102

- Warnings: unknown new rules activated (versionbit 28)

```

Altri comandi per ottenere informazioni su blockchain, mining, rete, portafoglio ecc.

```
$ bitcoin-cli getblockchaininfo
$ bitcoin-cli getmininginfo
$ bitcoin-cli getnetworkinfo
$ bitcoin-cli getnettotals
$ bitcoin-cli getwalletinfo
```
Ad esempio, `bitcoin-cli getnetworkinfo` fornisce una serie di informazioni sulla propria configurazione e sul suo accesso a diverse reti:
```
$ bitcoin-cli getnetworkinfo
{
  "version": 200000,
  "subversion": "/Satoshi:0.20.0/",
  "protocolversion": 70015,
  "localservices": "0000000000000408",
  "localservicesnames": [
    "WITNESS",
    "NETWORK_LIMITED"
  ],
  "localrelay": true,
  "timeoffset": 0,
  "networkactive": true,
  "connections": 10,
  "networks": [
    {
      "name": "ipv4",
      "limited": false,
      "reachable": true,
      "proxy": "",
      "proxy_randomize_credentials": false
    },
    {
      "name": "ipv6",
      "limited": false,
      "reachable": true,
      "proxy": "",
      "proxy_randomize_credentials": false
    },
    {
      "name": "onion",
      "limited": false,
      "reachable": true,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    }
  ],
  "relayfee": 0.00001000,
  "incrementalfee": 0.00001000,
  "localaddresses": [
    {
      "address": "45.79.111.171",
      "port": 18333,
      "score": 1
    },
    {
      "address": "2600:3c01::f03c:92ff:fecc:fdb7",
      "port": 18333,
      "score": 1
    },
    {
      "address": "4wrr3ktm6gl4sojx.onion",
      "port": 18333,
      "score": 4
    }
  ],
  "warnings": "Warning: unknown new rules activated (versionbit 28)"
}
```
Sentiti libero di fare riferimento a uno qualsiasi di questi comandi e di usare "bitcoin-cli help" se vuoi maggiori informazioni sul funzionamento di uno di essi.

## Riepilogo: Conoscere la Tua Configurazione Bitcoin

La directory `~/.bitcoin` contiene tutti i file, mentre `bitcoin-cli help` e una serie di comandi info possono essere usati per ottenere maggiori informazioni sul funzionamento della configurazione e di Bitcoin.

## Cosa c'è Dopo?

Continua il capitolo "Capire la Tua Configurazione Bitcoin" con [§3.3: Configurare il Tuo Wallet](03_3_Configurare_il_Tuo_Wallet.md).
