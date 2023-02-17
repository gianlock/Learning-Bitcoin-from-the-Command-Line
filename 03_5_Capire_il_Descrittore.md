# 3.5: Capire il Descrittore

> :information_source: **NOTA:** Avviso ai lettori. Questa sezione è stata aggiunta di recente al corso ed è una prima bozza che potrebbe essere ancora in attesa di revisione.

Potreste aver notato uno strano campo `desc:` nel comando `listunspent` della sezione precedente. Ecco di cosa si tratta (e come può essere usato per trasferire gli indirizzi).

> :warning: **AVVISO SULLA VERSIONE:** Si tratta di un'innovazione di Bitcoin Core v 0.17.0 che ha continuato a essere estesa con Bitcoin Core 0.20.0. La maggior parte dei comandi in questa sezione sono della versione 0.17.0, ma l'aggiornamento di `importmulti` che supporta i descrittori è arrivato con la versione 0.18.0.

## Come Trasferire gli Indirizzi

La maggior parte di questo corso presuppone che si lavori interamente da un singolo nodo in cui si gestisce il proprio portafoglio, inviando e ricevendo pagamenti con gli indirizzi creati da quel portafoglio. Tuttavia, non è necessariamente così che funziona il più ampio ecosistema Bitcoin. È più probabile che si spostino gli indirizzi tra i portafogli e che si creino portafogli per monitorare i fondi controllati da portafogli diversi. 

È qui che entrano in gioco i descrittori. Sono molto utili se si interagisce con software diverso da Bitcoin Core e si ha bisogno di questa funzione di compatibilità: si veda [§6.1](06_1_Inviare_una_Transazione_con_Multisig.md) per un esempio reale di come sia fondamentale avere la funzionalità dei descrittori.

Il trasferimento di indirizzi tra portafogli si basava su `xpub` e `xprv`, che sono ancora supportati. 

> :book: ***Cos'è xprv?*** Una chiave privata estesa. È la combinazione di una chiave privata e di un codice a catena. È una chiave privata da cui può essere derivata un'intera sequenza di chiavi private secondarie.

> :book: ***Cos'è xpub?*** Una chiave pubblica estesa. È la combinazione di una chiave pubblica e di un codice a catena. È una chiave pubblica da cui può essere derivata un'intera sequenza di chiavi pubbliche secondarie.

Il fatto che si possa avere "un'intera sequenza di chiavi...figlio" rivela che "xpub" e "xprv" non sono chiavi standard come quelle di cui abbiamo parlato finora. Sono invece chiavi gerarchiche che possono essere usate per creare intere famiglie di chiavi, basate sull'idea dei portafogli HD.

> :book: ***Cos'è un Wallet HD?*** La maggior parte dei portafogli moderni si basa su [BIP32: Hierarchical Deterministic Wallets](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki). Si tratta di una struttura gerarchica in cui un singolo seme può essere utilizzato per generare un'intera sequenza di chiavi. L'intero portafoglio può quindi essere ripristinato a partire da quel seme, anziché richiedere il ripristino di ogni singola chiave privata.

> :book: ***Cos'è un Path di Derivazione?*** Quando si hanno chiavi gerarchiche, è necessario poter definire le singole chiavi come discendenti di un seme. Per esempio, `[0]` è la chiave 0, `[0/1]` è il primo figlio della chiave 0, `[1/0/1]` è il primo nipote del figlio zero della prima chiave. Alcune chiavi contengono anche un `'` dopo il numero, per indicare che sono state "hardened", il che le protegge da un attacco specifico che può essere usato per ricavare un `xprv` da un `xpub`. Non c'è bisogno di preoccuparsi dei dettagli, a parte il fatto che quei `'` causeranno problemi di formattazione quando si lavora dalla riga di comando.

> :information_source: **NOTA:** un path di derivazione definisce una chiave, il che significa che una chiave rappresenta un path di derivazione. Sono equivalenti. Nel caso di un descrittore, il path di derivazione permette a `bitcoind` di sapere da dove proviene la chiave che segue nel descrittore!

`xpub` e `xprvs` si sono dimostrate insufficienti quando i tipi di chiavi pubbliche si sono moltiplicati nell'ambito dell'[espansione di SegWit](04_6_Creare_una_Transazione_Segwit.md), per cui si è resa necessaria la presenza di "descrittori di output".

> :book: ***Cos'è un descrittore di output?*** Una descrizione precisa di come ricavare un indirizzo Bitcoin dalla combinazione di una funzione e di uno o più input a tale funzione.

L'introduzione di funzioni nei descrittori è ciò che li rende potenti, perché possono essere utilizzati per trasferire tutti i tipi di indirizzi, da quelli Legacy con cui lavoriamo ora a quelli Segwit e multisig che incontreremo più avanti. Una funzione individuale corrisponde a un particolare tipo di indirizzo e si correla a regole specifiche per generare quell'indirizzo.

## Catturare un descrittore

I descrittori sono visibili in diversi comandi, come ad esempio `listunspent` e `getaddressinfo`:
```
$ bitcoin-cli getaddressinfo ms7ruzvL4atCu77n47dStMb3of6iScS8kZ
{
  "address": "ms7ruzvL4atCu77n47dStMb3of6iScS8kZ",
  "scriptPubKey": "76a9147f437379bcc66c40745edc1891ea6b3830e1975d88ac",
  "ismine": true,
  "solvable": true,
  "desc": "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk",
  "iswatchonly": false,
  "isscript": false,
  "iswitness": false,
  "pubkey": "03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388",
  "iscompressed": true,
  "ischange": false,
  "timestamp": 1592335136,
  "hdkeypath": "m/0'/0'/18'",
  "hdseedid": "fdea8e2630f00d29a9d6ff2af7bf5b358d061078",
  "hdmasterfingerprint": "d6043800",
  "labels": [
    ""
  ]
}
```
Qui il descrittore è `pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk`.

## Comprendere un Descrittore

Un descrittore è suddiviso in diverse parti:
```
function([derivation-path]key)#checksum
```
Ecco cosa significa:
* **Function.** La funzione utilizzata per creare un indirizzo da quella chiave. In questo caso è `pkh`, che è l'indirizzo standard P2PKH legacy conosciuto in [§3.3: Configurare il Tuo Wallet](03_3_Configurare_il_Tuo_Wallet.md). Allo stesso modo, un indirizzo P2WSH SegWit userebbe `wsh` e un indirizzo P2WPKH userebbe `wpkh`.
* **Derivation-path.** Descrive la parte di un wallet HD che viene esportata. In questo caso si tratta di un seme con il fingerprint `d6043800` e poi del 18° figlio del figlio 0 del figlio 0 (`0'/0'/18'`) di quel seme. Ci può essere anche un'ulteriore derivazione dopo la chiave: `function([derivation-path]key/more-derivation)#checksum`
   * Vale la pena notare che se si ottiene un path di derivazione senza fingerprint, lo si può inventare. Tuttavia, se ce n'è uno già esistente, è bene che corrisponda, perché se si torna al dispositivo che ha creato il fingerprint, è necessario che sia lo stesso.
* **Key**. La chiave o le chiavi che vengono trasferite. Potrebbe essere qualcosa di tradizionale come una `xpub` o una `xprv`, potrebbe essere solo una chiave pubblica per un indirizzo come in questo caso, potrebbe essere un insieme di indirizzi per una firma multipla, o potrebbe essere qualcos'altro. Questi sono i dati fondamentali: la funzione spiega cosa farci.
* **Checksum**. I descrittori sono pensati per essere trasferibili umanamente. Questa checksum assicura che siano corretti.

Guarda [Bitcoin Core's Info on Descriptor Support](https://github.com/bitcoin/bitcoin/blob/master/doc/descriptors.md) per maggiori informazioni.

## Esaminare un Descrittore

Puoi esaminare un descrittore con il comando RPC `getdescriptorinfo`:
```
$ bitcoin-cli getdescriptorinfo "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk"
{
  "descriptor": "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk",
  "checksum": "4ahsl9pk",
  "isrange": false,
  "issolvable": true,
  "hasprivatekeys": false
}
```
Nota che restituisce un checksum. Se si riceve un descrittore senza checksum, si può verificarlo con questo comando:
```
$ bitcoin-cli getdescriptorinfo "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)"
{
  "descriptor": "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk",
  "checksum": "4ahsl9pk",
  "isrange": false,
  "issolvable": true,
  "hasprivatekeys": false
}
```
Oltre a fornire il checksum, questo comando verifica anche la validità del descrittore e fornisce informazioni utili, come ad esempio se un descrittore contiene chiavi private.

Uno dei vantaggi di un descrittore è la possibilità di derivare un indirizzo in modo regolare. Questo viene fatto con il comando RPC `deriveaddresses`.
```
$ bitcoin-cli deriveaddresses "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk"
[
  "ms7ruzvL4atCu77n47dStMb3of6iScS8kZ"
]
```
Noterai che ritorna all'indirizzo di partenza (come dovrebbe).

## Importare un Descrittore

Ma la cosa veramente importante di un descrittore è che lo si può importare su un'altra macchina (remota). Questo viene fatto con l'RPC `importmulti`, utilizzando l'opzione `desc`:
```
remote$ bitcoin-cli importmulti '[{"desc": "pkh([d6043800/0'"'"'/0'"'"'/18'"'"']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk", "timestamp": "now", "watchonly": true}]'
[
  {
    "success": true
  }
]
```
Innanzitutto, si può notare il primo uso veramente brutto delle virgolette. Ogni `'` nel percorso di derivazione deve essere sostituito con `'"'"'`. Ci si aspetta di doverlo fare se si manipola un descrittore che contiene un percorso di derivazione. (L'altra opzione è quella di sostituire la `'` con una `h` per hardened, ma questo cambierà il checksum, quindi se si preferisce questa soluzione per la sua facilità d'uso, si dovrà ottenere un nuovo checksum con `getdescriptorinfo`).

In secondo luogo, si noterà che l'abbiamo contrassegnata come "watchonly". Questo perché sappiamo che si tratta di una chiave pubblica, quindi non possiamo spendere con essa. Se non avessimo inserito questo flag, `importmulti` ci avrebbe detto qualcosa come: `Mancano alcune chiavi private, gli output saranno considerati watchonly. Se ciò è intenzionale, specificare il flag watchonly.`.

> :book: ***Cos'è a watch-only address?*** Un indirizzo di watch-only consente di osservare le transazioni relative a un indirizzo (o a un'intera famiglia di indirizzi, se si utilizza un `xpub`), ma non di spendere fondi su tali indirizzi.

Utilizzando `getaddressesbylabel`, possiamo ora vedere che il nostro indirizzo è stato importato correttamente nella nostra macchina remota!
```
remote$ bitcoin-cli getaddressesbylabel ""
{
  "ms7ruzvL4atCu77n47dStMb3of6iScS8kZ": {
    "purpose": "receive"
  }
}
```
## Riepilogo: Capire il Descrittore

I descrittori consentono di passare chiavi pubbliche e private tra i wallet, ma soprattutto permettono di definire in modo preciso e corretto gli indirizzi e di ricavare indirizzi di molti tipi diversi da un formato di descrizione standardizzato.

> :fire: ***Qual è il potere dei descrittori?*** I descrittori consentono di importare ed esportare semi e chiavi. È un'ottima cosa se si vuole passare da un portafoglio all'altro. Come sviluppatore, inoltre, consentono di costruire il tipo preciso di indirizzi che si è interessati a creare. Ad esempio, lo utilizziamo in [FullyNoded 2](https://github.com/BlockchainCommons/FullyNoded-2/blob/master/Docs/How-it-works.md) per generare un multi-sig da tre semi. 

Faremo un uso reale dei descrittori nel capitolo [§7.3](07_3_Integrating_with_Hardware_Wallets.md), quando importeremo gli indirizzi da un hardware wallet.

## Cosa c'è dopo?

Avanza attraverso "bitcoin-cli" con il [Capitolo Quattro: Inviare Transazioni Bitcoin](04_0_Inviare_Transazioni_Bitcoin.md).
