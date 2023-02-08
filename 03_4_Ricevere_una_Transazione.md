# 3.4: Ricevere Una Transazione

Ora sei pronto a ricevere dei satoshi al nuovo indirizzo che hai creato.

## Ricevere Satoshi

Per poter fare qualsiasi altra cosa, è necessario ottenere dei satoshi. Su testnet questo avviene tramite i faucet. Poiché il denaro è tutto finto, basta andare a un faucet, richiedere dei satoshi e questi ti verranno inviati. Si consiglia di utilizzare i faucet all'indirizzo https://testnet-faucet.mempool.co/, https://bitcoinfaucet.uo1.net/ o https://testnet.coinfaucet.eu/en/. Se per qualche motivo non sono disponibili, cercate "bitcoin testnet faucet" e ne troverete altri.

Per utilizzare un faucet, di solito è necessario andare su un sito dedicato, come quelli indicati, e copiare e incollare il proprio indirizzo. Si noti che questo è uno dei casi in cui non è possibile utilizzare le variabili della riga di comando. In seguito, verrà creata una transazione che invierà i satoshi dal faucet al wallet.

> :book: ***Cos'è una transazione?*** Una transazione è uno scambio di bitcoin. Il proprietario di alcuni bitcoin utilizza la sua chiave privata per accedere ad essi, quindi blocca la transazione utilizzando la chiave pubblica del destinatario.

> :link: **TESTNET vs MAINNET:** Purtroppo, non ci sono faucet nella vita reale. Se fossi sulla mainnet, dovresti andare a comprare i bitcoin presso una exchange p2p o un bancomat, oppure dovresti chiedere a qualcuno di inviarteli. La vita su Testnet è molto più semplice.

## Verifica il Saldo

Dopo aver richiesto dei fondi, è possibile verificarli con il comando `bitcoin-cli getbalance`:
```
$ bitcoin-cli getbalance
0.00000000
```
Ma aspetta, non c'è ancora nessun saldo!?

Benvenuti nel mondo della latenza di Bitcoin. Il problema è che la vostra transazione non è ancora stata registrata in un blocco!

> :book: ***Cos'è un blocco?*** Le transazioni vengono trasmesse attraverso la rete e raccolte in blocchi dai miner. Questi blocchi sono protetti da una prova di lavoro matematica, che dimostra che la potenza di calcolo è stata spesa per la creazione del blocco. È questa prova di lavoro (moltiplicata per molti blocchi, ognuno costruito sopra l'altro) a rendere sicuro Bitcoin.

> :book: ***Cos'è un miner?*** Un miner è un partecipante alla rete Bitcoin che lavora per creare blocchi. Si tratta di un lavoro remunerativo: quando un miner crea con successo un blocco, riceve una ricompensa fissa più le commissioni delle transazioni nel suo blocco. Il mining è un grande business. I miner tendono a utilizzare un hardware speciale, accelerato in modo da rendere più probabile la creazione di blocchi. Inoltre, tendono a far parte di pool di mining, in cui i miner sono tutti d'accordo nel dividersi le ricompense quando uno di loro riesce a creare un blocco.

Fortunatamente, `bitcoin-cli getunconfirmedbalance` dovrebbe mostrare il saldo aggiornato finché la transazione iniziale non è stata creata:
```
$ bitcoin-cli getunconfirmedbalance
0.01010000
```
Se anche qui c'è ancora uno zero, probabilmente si sta procedendo troppo velocemente con il tutorial. Aspettate un attimo. Le monete dovrebbero apparire non confermate, quindi passare rapidamente a confermate. Si noti che una moneta può passare da unconfirmedbalance a confirmedbalance quasi immediatamente, quindi assicuratevi di controllarle entrambe. Tuttavia, se il `getbalance` e il `getunconfirmedbalance` mostrano ancora zero dopo dieci minuti, probabilmente c'è qualcosa che non va nel faucet e bisogna sceglierne un altro.

### Ottenere Fiducia nei Propri Satoshi

Puoi usare `bitcoin-cli getbalance "*" [n]`, dove sostituisci `[n]` con un numero intero, per vedere se un saldo confermato è profondo 'n' blocchi.

> :book: ***Cos'è la profondità del blocco?*** Dopo che un blocco è stato creato e confermato, un altro blocco viene creato sopra di esso, e un altro ancora... Poiché si tratta di un processo stocastico, esiste una certa possibilità di inversione quando un blocco è ancora nuovo. Pertanto, un blocco deve essere sepolto da diversi blocchi in una catena prima di potersi sentire totalmente sicuri dei propri fondi. Ognuno di questi blocchi viene creato in media ogni 10 minuti... quindi di solito ci vuole circa un'ora per ricevere una transazione confermata a sei blocchi di profondità, che è la misura della piena fiducia in Bitcoin.

Di seguito viene mostrato che le nostre transazioni sono state confermate una volta, ma non due:
```
$  bitcoin-cli getbalance "*" 1
0.01010000
$  bitcoin-cli getbalance "*" 2
0.00000000
```
Ovviamente, ogni dieci minuti circa questa profondità aumenterà.

Naturalmente, nella rete di prova, nessuno si preoccupa di quanto siano affidabili i vostri fondi. Potrai spendere i tuoi fondi non appena saranno confermati.

## Verificare il Proprio Wallet

Il comando `bitcoin-cli getwalletinfo` fornisce ulteriori informazioni sul saldo del portafoglio:
```
$ bitcoin-cli getwalletinfo
{
  "walletname": "",
  "walletversion": 169900,
  "balance": 0.01010000,
  "unconfirmed_balance": 0.00000000,
  "immature_balance": 0.00000000,
  "txcount": 2,
  "keypoololdest": 1592335137,
  "keypoolsize": 999,
  "hdseedid": "fdea8e2630f00d29a9d6ff2af7bf5b358d061078",
  "keypoolsize_hd_internal": 1000,
  "paytxfee": 0.00000000,
  "private_keys_enabled": true,
  "avoid_reuse": false,
  "scanning": false
}
```

## Scoprire l'ID della Transazione

I satoshi sono entrati nel tuo portafoglio tramite una transazione. È possibile scoprire il transactionid (txid) con il comando `bitcoin-cli listtransactions`:
```
$ bitcoin-cli listtransactions
[
  {
    "address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",
    "category": "receive",
    "amount": 0.01000000,
    "label": "",
    "vout": 1,
    "confirmations": 1,
    "blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",
    "blockheight": 1772396,
    "blockindex": 73,
    "blocktime": 1592600085,
    "txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",
    "walletconflicts": [
    ],
    "time": 1592599884,
    "timereceived": 1592599884,
    "bip125-replaceable": "no"
  },
  {
    "address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",
    "category": "receive",
    "amount": 0.00010000,
    "label": "",
    "vout": 0,
    "confirmations": 1,
    "blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",
    "blockheight": 1772396,
    "blockindex": 72,
    "blocktime": 1592600085,
    "txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",
    "walletconflicts": [
    ],
    "time": 1592599938,
    "timereceived": 1592599938,
    "bip125-replaceable": "no"
  }
]

```
Vengono mostrate due transazioni (`8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9`) e (`ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36`) per un importo specifico (`0. 01000000` e `0,00010000`), entrambi ricevuti (`receive`) nello stesso indirizzo del nostro wallet (`mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE`). Questa è una cattiva pratica di utilizzo delle chiavi: dovreste usare un nuovo indirizzo per ogni singolo Bitcoin che ricevete. In questo caso, ci siamo spazientiti perché il primo rubinetto non sembrava funzionare.

È possibile accedere a informazioni simili con il comando `bitcoin-cli listunspent`, ma mostra solo le transazioni in cui i satoshi non sono stati spesi. Queste sono chiamate UTXO e saranno di vitale importanza quando si invieranno i satoshi nel mondo Bitcoin:
```
$ bitcoin-cli listunspent
[
  {
    "txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",
    "vout": 0,
    "address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",
    "label": "",
    "scriptPubKey": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",
    "amount": 0.00010000,
    "confirmations": 1,
    "spendable": true,
    "solvable": true,
    "desc": "pkh([d6043800/0'/0'/1']02fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9ba)#62rud39c",
    "safe": true
  },
  {
    "txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",
    "vout": 1,
    "address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",
    "label": "",
    "scriptPubKey": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",
    "amount": 0.01000000,
    "confirmations": 1,
    "spendable": true,
    "solvable": true,
    "desc": "pkh([d6043800/0'/0'/1']02fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9ba)#62rud39c",
    "safe": true
  }
]
```
Nota che i bitcoin non sono solo un insieme omogeneo di contanti infilati in tasca. Ogni singola transazione ricevuta o inviata viene inserita nel registro immutabile della blockchain, in un blocco. Puoi vedere queste singole transazioni quando guardi i tuoi satoshi non spesi. Ciò significa che la spesa in bitcoin non è così anonima come si potrebbe pensare. Sebbene gli indirizzi siano abbastanza privati, le transazioni possono essere esaminate mentre entrano ed escono dagli indirizzi. Questo rende la privacy vulnerabile all'analisi statistica. Inoltre, introduce una potenziale non-fungibilità dei bitcoin, in quanto è possibile risalire a una serie di transazioni, anche se non è possibile risalire a un "bitcoin" specifico.

> :book: ***Perché tutti questi importi di bitcoin sono in frazioni?*** I bitcoin vengono prodotti lentamente e quindi sono relativamente pochi quelli in circolazione. Di conseguenza, ogni bitcoin sulla mainnet ha un valore piuttosto elevato (~ €21.500 al momento in cui scriviamo). Ciò significa che di solito si lavora in frazioni. Infatti, gli 0,0101 in monete di Testnet varrebbero circa €200 se fossero sulla mainnet. Per questo motivo, sono apparsi nomi per piccole quantità di bitcoin, tra cui millibitcoin o mBTC (un millesimo di bitcoin), microbitcoin o bit o μBTC (un milionesimo di bitcoin) e satoshi (un centomilionesimo di bitcoin).

## Esaminare la Tua Transazione

È possibile ottenere ulteriori informazioni su una transazione con il comando `bitcoin-cli gettransaction`:
```
$ bitcoin-cli gettransaction "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9"
{
  "amount": 0.01000000,
  "confirmations": 1,
  "blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",
  "blockheight": 1772396,
  "blockindex": 73,
  "blocktime": 1592600085,
  "txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",
  "walletconflicts": [
  ],
  "time": 1592599884,
  "timereceived": 1592599884,
  "bip125-replaceable": "no",
  "details": [
    {
      "address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",
      "category": "receive",
      "amount": 0.01000000,
      "label": "",
      "vout": 1
    }
  ],
  "hex": "0200000000010114d04977d1b0137adbf51dd5d79944b9465a2619f3fa7287eb69a779977bf5800100000017160014e85ba02862dbadabd6d204fcc8bb5d54658c7d4ffeffffff02df690f000000000017a9145c3bfb36b03f279967977ca9d1e35185e39917788740420f00000000001976a9141b72503639a13f190bf79acf6d76255d772360b788ac0247304402201e74bdfc330fc2e093a8eabe95b6c5633c8d6767249fa25baf62541a129359c202204d462bd932ee5c15c7f082ad7a6b5a41c68addc473786a0a9a232093fde8e1330121022897dfbf085ecc6ad7e22fc91593414a845659429a7bbb44e2e536258d2cbc0c270b1b00"
}
```
Il comando `gettransaction` fornisce informazioni dettagliate sulle transazioni presenti nel tuo portafoglio, come questa, che ci è stata inviata.

Si noti che `gettransaction` ha due argomenti opzionali:
```
$ bitcoin-cli help gettransaction
gettransaction "txid" ( include_watchonly verbose )

Get detailed information about in-wallet transaction <txid>

Arguments:
1. txid                 (string, required) The transaction id
2. include_watchonly    (boolean, optional, default=true for watch-only wallets, otherwise false) Whether to include watch-only addresses in balance calculation and details[]
3. verbose              (boolean, optional, default=false) Whether to include a `decoded` field containing the decoded transaction (equivalent to RPC decoderawtransaction)
```
Impostando questi due valori true o false, si può scegliere di includere nell'output gli indirizzi di sola osservazione (che non ci interessano) o di visualizzare un output più dettagliato (che ci interessa).

Ecco come appaiono questi dati quando si imposta `include_watchonly` a `false` e `verbose` a `true`.
```
$ bitcoin-cli gettransaction "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9" false true
{
  "amount": 0.01000000,
  "confirmations": 3,
  "blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",
  "blockheight": 1772396,
  "blockindex": 73,
  "blocktime": 1592600085,
  "txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",
  "walletconflicts": [
  ],
  "time": 1592599884,
  "timereceived": 1592599884,
  "bip125-replaceable": "no",
  "details": [
    {
      "address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",
      "category": "receive",
      "amount": 0.01000000,
      "label": "",
      "vout": 1
    }
  ],
  "hex": "0200000000010114d04977d1b0137adbf51dd5d79944b9465a2619f3fa7287eb69a779977bf5800100000017160014e85ba02862dbadabd6d204fcc8bb5d54658c7d4ffeffffff02df690f000000000017a9145c3bfb36b03f279967977ca9d1e35185e39917788740420f00000000001976a9141b72503639a13f190bf79acf6d76255d772360b788ac0247304402201e74bdfc330fc2e093a8eabe95b6c5633c8d6767249fa25baf62541a129359c202204d462bd932ee5c15c7f082ad7a6b5a41c68addc473786a0a9a232093fde8e1330121022897dfbf085ecc6ad7e22fc91593414a845659429a7bbb44e2e536258d2cbc0c270b1b00",
  "decoded": {
    "txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",
    "hash": "d4ae2b009c43bfe9eba96dcd16e136ceba2842df3d76a67d689fae5975ce49cb",
    "version": 2,
    "size": 249,
    "vsize": 168,
    "weight": 669,
    "locktime": 1772327,
    "vin": [
      {
        "txid": "80f57b9779a769eb8772faf319265a46b94499d7d51df5db7a13b0d17749d014",
        "vout": 1,
        "scriptSig": {
          "asm": "0014e85ba02862dbadabd6d204fcc8bb5d54658c7d4f",
          "hex": "160014e85ba02862dbadabd6d204fcc8bb5d54658c7d4f"
        },
        "txinwitness": [
          "304402201e74bdfc330fc2e093a8eabe95b6c5633c8d6767249fa25baf62541a129359c202204d462bd932ee5c15c7f082ad7a6b5a41c68addc473786a0a9a232093fde8e13301",
          "022897dfbf085ecc6ad7e22fc91593414a845659429a7bbb44e2e536258d2cbc0c"
        ],
        "sequence": 4294967294
      }
    ],
    "vout": [
      {
        "value": 0.01010143,
        "n": 0,
        "scriptPubKey": {
          "asm": "OP_HASH160 5c3bfb36b03f279967977ca9d1e35185e3991778 OP_EQUAL",
          "hex": "a9145c3bfb36b03f279967977ca9d1e35185e399177887",
          "reqSigs": 1,
          "type": "scripthash",
          "addresses": [
            "2N1ev1WKevSsdmAvRqZf7JjvDg223tPrVCm"
          ]
        }
      },
      {
        "value": 0.01000000,
        "n": 1,
        "scriptPubKey": {
          "asm": "OP_DUP OP_HASH160 1b72503639a13f190bf79acf6d76255d772360b7 OP_EQUALVERIFY OP_CHECKSIG",
          "hex": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",
          "reqSigs": 1,
          "type": "pubkeyhash",
          "addresses": [
            "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE"
          ]
        }
      }
    ]
  }
}
```
Ora è possibile vedere le informazioni complete sulla transazione, compresi tutti gli ingressi ("vin") e tutte le uscite ("vout"). Una cosa interessante da notare è che, sebbene abbiamo ricevuto .01 BTC nella transazione, altri .01010143 sono stati inviati a un altro indirizzo. Probabilmente si trattava di un cambio di indirizzo, un concetto che verrà approfondito nella prossima sezione. È abbastanza tipico che una transazione abbia più ingressi e/o più uscite.

Esiste un altro comando, `getrawtransaction`, che consente di esaminare le transazioni non presenti nel proprio portafoglio. Tuttavia, richiede un nodo unpruned e `txindex=1` nel file `bitcoin.conf`. A meno che non si abbia una seria necessità di informazioni non presenti nel proprio portafoglio, probabilmente è meglio usare un explorer Bitcoin per questo genere di cose...

## Opzionale: Usare un Block Explorer

Anche guardare le informazioni dettagliate di una transazione può essere un po' scoraggiante. L'obiettivo principale di questo tutorial è insegnare come gestire le transazioni grezze dalla riga di comando, ma siamo felici di parlare di altri strumenti quando sono pertinenti. Uno di questi strumenti è un block explorer, che può essere utilizzato per esaminare le transazioni da un broswer in un formato molto più intuitivo.

Attualmente, il nostro block explorer preferito è [https://mempool.space/](https://mempool.space/) o [https://blockstream.info/](https://blockstream.info/).

Si può utilizzare per cercare le transazioni relative a un indirizzo:

[https://mempool.space/testnet/address/mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE/](https://mempool.space/testnet/address/mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE/)

Si può anche utilizzare per esaminare le singole transazioni:

[https://mempool.space/testnet/tx/8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9/](https://mempool.space/testnet/tx/8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9/)

Un block explorer non fornisce in genere più informazioni di un'analisi a riga di comando di una transazione grezza; fa solo un buon lavoro per evidenziare le informazioni importanti e mettere insieme i pezzi del puzzle, comprese le spese di transazione che stanno dietro a una transazione - un altro concetto che tratteremo nelle prossime sezioni.

## Riepilogo: Ricevere Una Transazione

I faucet ti daranno satoshi sulla testnet. Arrivano come transazioni grezze, che possono essere esaminate con `gettransaction` o con un block explorer. Una volta ricevuta una transazione, la si può vedere nel proprio saldo e nel proprio wallet.

## Cosa c'è Dopo?

Per un approfondimento su come vengono descritti gli indirizzi, in modo che possano essere trasferiti o trasformati in parti di una firma multipla, guarda [§3.5: Capire il Descrittore](03_5_Capire_il_Descrittore.md).

Ma se questo è troppo dettagliato, continua con il [Capitolo Quattro: Inviare Transazioni Bitcoin](04_0_Inviare_Transazioni_Bitcoin.md).

