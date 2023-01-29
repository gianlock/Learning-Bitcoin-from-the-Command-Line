# Intermezzo: Introduzione a Bitcoin

Prima di iniziare a programmare Bitcoin (e Lightning), è necessario avere una conoscenza base di cosa sono e come funzionano. Questa sezione fornisce una panoramica di come funzionano e ha il solo scopo di gettare le basi. Troverai molte altre definizioni nei capitoli successivi.

## Bitcoin

Bitcoin è un protocollo che consente lo scambio di valuta bitcoin. Si basa su un sistema decentralizzato di nodi peer-to-peer che comprende: nodi completi, wallet e minatori. Queste parti lavorando insieme garantiscono la rapidità e l'autenticità delle transazioni. Grazie alla natura decentralizzata del sistema, queste transazioni sono incensurabili e, se ben utilizzate, possono offrire vantaggi come l'anonimato e la non correlazione.

Ovviamente, Bitcoin è il fulcro intorno a cui ruota questo libro, ha ispirato la creazione di altri sistemi come le blockchain e Lightning, che saranno ben spiegati in questo tutorial, ma ha ispirato anche molte altre shitcoin come Ethereum e Litecoin, che non lo saranno.

**_Come viene trasferita la moneta?_** La valuta bitcoin non è una moneta fisica ma una serie infinita di passaggi di proprietà. Quando una persona invia denaro ad un'altra, quel trasferimento viene memorizzato. È la transazione che attesta la proprietà del denaro, non la presenza di una moneta nel portafoglio.

**_A chi puoi inviare monete?_** La stragrande maggioranza delle transazioni di bitcoin comporta l'invio di monete a singole persone (o singoli indirizzi Bitcoin). Tuttavia, è possibile utilizzare metodologie più complesse per inviare bitcoin a gruppi di persone o per eseguire script. Queste varie metodologie hanno nomi come P2PKH, multisig e P2SH.

**_Come vengono memorizzate le transazioni?_** Le transazioni vengono combinate in grandi blocchi di dati, che vengono poi scritti nel registro blockchain. Un blocco è costruito in modo tale da non poter essere sostituito o modificato una volta che i blocchi sucessivi sono stati costruiti successivamente e in correlazione ad esso. Questo è ciò che rende i bitcoin non ripudiabili: il database globale decentralizzato in cui tutto è registrato è effettivamente un database permanente e immutabile.

Tuttavia, il processo di costruzione di questi blocchi è aleatorio, in qualche modo casuale. Data una transazione, non si potrà mai essere certi in quale blocco verrà inserita. Ci possono anche essere cambiamenti nei blocchi se molto recenti, ma solo se _molto_ recenti. Quindi, le transazioni sono autenticate (permanenti e immutabili) solo dopo un po' di blocchi e quindi di tempo.

**_Come sono protette le transazioni?_** I fondi contenuti in una transazione Bitcoin sono protetti da un puzzle crittografico. Questi enigmi sono progettati in modo che possano essere facilmente risolti dalla persona a cui sono stati inviati i fondi. Questo è possibile utilizzando la potenza della crittografia a chiave pubblica. Tecnicamente, una transazione è protetta da una firma che prova che sei il proprietario della chiave pubblica a cui è stata inviata una transazione: questa prova di proprietà è il rompicapo che si sta risolvendo.

I fondi sono ulteriormente protetti con l'uso di funzioni hash. Le chiavi pubbliche non vengono effettivamente memorizzate nella blockchain fino a quando i fondi non vengono spesi: lo sono solo gli hash delle chiavi pubbliche. Ciò significa che anche con il possibile avvento dei computer quantistici, le transazioni Bitcoin rimarrebbero protette da questo secondo livello di crittografia.

**_Come sono create le transazioni?_** Il cuore di ogni transazione Bitcoin è un linguaggio di scripting simile a FORTH che viene utilizzato per bloccare la transazione. Per riutilizzare il denaro, il destinatario fornisce allo script informazioni specifiche che dimostrano che è il destinatario legittimo.

Tuttavia, questi script Bitcoin rappresentano il codice a più basso livello di Bitcoin. Gran parte del lavoro di Bitcoin viene svolto attraverso il deamon Bitcoin `bitcoind`, che viene controllato attraverso comandi RPC. Molti inviano questi comandi RPC attraverso il programma `bitcoin-cli`, che fornisce un'interfaccia semplificata. Tuttavia l'utente medio non avezzo alla programmazione non si preoccupa nemmeno di queste minuzie, ma utilizza portafogli con interfacce ancora più semplificate.

### Bitcoin — In Breve

Un modo per pensare a Bitcoin è come _una sequenza di transazioni indivisibili_. Ogni transazione è autenticata da un mittente con la soluzione di un precedente puzzle crittografico memorizzato come script. La nuova transazione viene bloccata dal destinatario con un nuovo enigma crittografico, anch'esso memorizzato come script. Ogni transazione è registrata in un libro mastro globale e immutabile.

## Crittografia a chiave Pubblica

La crittografia a chiave pubblica è un sistema matematico per proteggere i dati e dimostrarne la proprietà attraverso una coppia asimmetrica di chiavi collegate: la chiave pubblica e la chiave privata.

È importante per Bitcoin (e per la maggior parte dei sistemi blockchain) perché è la base della crittografia che protegge i fondi della criptovaluta. Una transazione Bitcoin viene tipicamente inviata ad un indirizzo che è un hash della chiave pubblica. Il destinatario è quindi in grado di recuperare il denaro rivelando la chiave pubblica e quella privata.

**_Cos'è una chiave Pubblica?_** Una chiave pubblica è la chiave che viene data ad altre persone. In un tipico sistema a chiave pubblica, un utente genera una chiave pubblica e una chiave privata, poi dà la chiave pubblica a tutti. I destinatari possono criptare le informazioni con la chiave pubblica, ma non possono decifrarle con la stessa chiave pubblica a causa dell'asimmetria della coppia di chiavi.

**_Cos'è una chiave Privata?_** Una chiave privata è la chiave collegata a quella pubblica in una coppia di chiavi. In un tipico sistema a chiave pubblica, un utente tiene al sicuro la sua chiave privata e la usa per decifrare i messaggi che sono stati crittografati con la chiave pubblica corrispondente.

**_Che cos'è una Firma?_** Un messaggio (o più comunemente un hash di un messaggio) può essere firmato con una chiave privata, creando appunto una firma. Chiunque possieda la chiave pubblica corrispondente può quindi convalidare la firma, verificando che il firmatario possiede la chiave privata associata alla chiave pubblica in questione. _SegWit_ è un formato specifico per la memorizzazione di una firma sulla rete Bitcoin che incontreremo più avanti.

**_Che cos'è una funzione Hash?_** Una funzione di hash è un algoritmo spesso utilizzato nella crittografia. È un modo per mappare una grande quantità arbitraria di dati in una piccola quantità fissa di dati. Le funzioni hash utilizzate in crittografia sono unidirezionali e resistenti alle collisioni, il che significa che un hash può essere collegato in modo affidabile ai dati originali, ma i dati originali non possono essere rigenerati dall'hash. Gli hash consentono quindi la trasmissione di piccole quantità di dati per rappresentare grandi quantità di dati, il che può essere importante per l'efficienza e i requisiti di archiviazione.

Bitcoin sfrutta la capacità di un hash di mascherare i dati originali, il che consente di nascondere la chiave pubblica di un utente, rendendo le transazioni resistenti al calcolo quantistico.

### Crittografia a chiave pubblica - In breve

Si può pensare alla crittografia a chiave pubblica come: _Un metodo per proteggere i dati in modo che solo una persona autorizzata possa accedervi e che la persona autorizzata possa dimostrare di avere tale accesso._

## ECC

ECC è l'acronimo di Crittografia a Curve Ellittiche. È una tipologia di crittografia a chiave pubblica basata sull'utilizzo di curve ellittiche definite su campi finiti. È più complessa e più difficile da spiegare rispetto alla crittografia a chiave pubblica classica (che utilizza i numeri primi), ma presenta alcuni vantaggi interessanti.

L'ECC non verrà trattato con molta attenzione in questo tutorial. Questo perché il corso è incentrato sull'integrazione con i server Bitcoin Core e Lightning, della crittografia se ne occuperanno loro. In effetti, l'intento di questo tutorial è quello di non farvi preoccupare di aspetti molto tecnici come quello della crittografia, che verranno trattati dagli esperti.

**_Cos'è una Curva Ellittica?_** Una curva ellittica è una curva geometrica descritta dall'equazione `y`<sup>`2`</sup> = `x`<sup>`3`</sup>` + ax + b`. Una curva ellittica specifica viene scelta selezionando valori specifici di "a" e "b". La curva deve quindi essere attentamente esaminata per determinare se funziona bene per la crittografia. Ad esempio, la curva secp256k1 utilizzata da Bitcoin è definita come `a=0` e `b=7`.

Qualsiasi linea che interseca una curva ellittica lo farà in 1 o 3 punti... e questa è la base della crittografia a curva ellittica.

**_What are Finite Fields?_** A finite field is a finite set of numbers, where all addition, subtraction, multiplication, and division is defined so that it results in other numbers also in the same finite field. One simple way to create a finite field is through the use of a modulo function.

**_How is an Elliptic Curve Defined Over a Finite Field?_** An elliptic curve defined over a finite field has all of the points on its curve drawn from a specific finite field. This takes the form: `y`<sup>`2`</sup> `% field-size = (x`<sup>`3`</sup>` + ax + b) % field-size` The finite field used for secp256k1 is `2`<sup>`256`</sup>` - 2`<sup>`32`</sup>` - 2`<sup>`9`</sup>` - 2`<sup>`8`</sup>` - 2`<sup>`7`</sup>` - 2`<sup>`6`</sup>` - 2`<sup>`4`</sup>` - 1`.

**_How Are Elliptic Curves Used in Cryptography?_** In elliptic-curve cryptography, a user selects a very large (256-bit) number as his private key. He then adds a set base point on the curve to itself that many times. (In secp256k1, the base point is `G = 04 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798 483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A6855419 9C47D08F FB10D4B8`, which prefixes the two parts of the tuple with an `04` to say that the data point is in uncompressed form. If you prefer a straight geometric definition, it's the point "0x79BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798,0x483ADA7726A3C4655DA4FBFC0E1108A8FD17B448A68554199C47D08FFB10D4B8") The resultant number is the public key. Various mathematical formula can then be used to prove ownership of the public key, given the private key. As with any cryptographic function, this one is a trap door: it's easy to go from private key to public key and largely impossible to go from public key to private key.

This particular methodology also explains why finite fields are used in elliptic curves: it ensures that the private key will not grow too large. Note that the finite field for secp256k1 is slightly smaller than 256 bits, which means that all public keys will be 256 bits long, just like the private keys are.

**_What Are the Advantages of ECC?_** The main advantage of ECC is that it allows the same security as classic public-key cryptography with a much smaller key. A 256-bit elliptic-curve public key corresponds to a 3072-bit traditional (RSA) public key.

### ECC - In Short

One way to think of ECC is: _a way to enable public-key cryptography that uses very small keys and very obscure math._

## About Blockchains

Blockchain is the generalization of the methodology used by Bitcoin to create a distributed global ledger. Bitcoin is a blockchain as are any number of alt-coins, each of which lives on its own network and writes to its own chain. Sidechains like Liquid are blockchains too. Blockchains don't even need to have anything to do with finances. For example, there have been many discussions of using blockchains to protect self-sovereign identities.

Though you need to understand the basics of how a blockchain works to understand how transactions work in Bitcoin, you won't need to go any further than that. Because blockchains have become a wide category of technology, those basic concepts are likely to be applicable to many other projects in this growing technology sector. The specific programming commands learned in this book will not be, however, as they're fairly specific to Bitcoin (and Lightning).

**_Why Is It Called a Chain?_** Each block in the blockchain stores a hash of the block before it. This links the current block all the way back to the original "genesis block" through an unbroken chain. It's a way to create absolute order among possibly conflicting data. This also provides the security of blockchain, because each block is stacked atop an old one makes it harder to recreate the old block due to the proof-of-work algorithms used in block creation. Once several blocks have been built atop a block in the chain, it's essentially irreversible.

**_What is a Fork?_** Occasionally two blocks are created around the same time. This temporarily creates a one-block fork, where either if the current blocks could be the "real" one. Every once in a while, a fork might expand to become two blocks, three blocks, or even four blocks long, but pretty quickly one side of the fork is determined to be the real one, and the other is "orphaned". This is part of the stochastic process of block creation, and demonstrates why several blocks must be built atop a block before it can be considered truly trustworthy and non-repudiable.

### Blockchain — In Short

One way to think of blockchain is: _a linked series of blocks of unchangeable data, going back in time_. Another way is: _a linked series of blocks to absolutely order data that could be conflicting_.

## Is Blockchain Right for Me?

If you want to transact bitcoins, then obviously Bitcoin is right for you. However, more widely, blockchain has become a popular buzz-word even though it's not a magic bullet for all technical problems. With that said, there are many specific situations where blockchain is a superior technology.

Blockchains probably _will_ be helpful if:

  * Users don't trust each other.
    * Or: Users exist across various borders.
  * Users don't trust central authorities.
    * And: Users want to control their own destinies.
  * Users want transparent technology.
  * Users want to share something.
    * And: Users want what's shared to be permanently recorded.
  * Users want fast transaction finality.
    * But: Users don't need instant transaction finality.

Blockchains probably _will not_ be helpful if:

  * Users are trusted:
    * e.g.: transactions occur within a business or organization.
    * e.g.: transactions are overseen by a central authority.
  * Secrecy is required:
    * e.g.: Information should be secret.
    * e.g.: Transactions should be secret.
    * e.g.: Transactors should be secret.
    * Unless: A methodology for cryptographic secrecy is carefully considered, analyzed, and tested.
  * Users need instant transaction finality.
    * e.g.: in less than 10 minutes on a Bitcoin-like network, in less than 2.5 minutes on a Litecoin-like network, in less than 15 seconds on an Ethereum-like network

Do note that there may still be solutions for some of these situations within the Bitcoin ecosystem. For example, payment channels are rapidly addressing questions of liquidity and payment finality.

## About Lightning

Lightning is a layer-2 protocol that interacts with Bitcoin to allow users to exchange their bitcoins "off-chain". It has both advantages and disadvantages over using Bitcoin on its own.

Lightning is also the secondary focus of this tutorial. Though it's mostly about interacting directly with Bitcoin (and the `bitcoind`), it pays some attention to Lightning because it's an upcoming technology that is likely to become a popular alternative to Bitcoin in the near future. This book takes the same approach to Lightning as to Bitcoin: it teaches how to interact directly with a trusted Lightning daemon from the command line.

Unlike with Bitcoin, there are actually several variants of Lightning. This tutorial uses the standard-compliant [c-lightning](https://github.com/ElementsProject/lightning) implementation as its trusted Lightning server.

**_What is a Layer-2 Protocol?_** A layer-2 Bitcoin protocol works on top of Bitcoin. In this case, Lightning works atop Bitcoin, interacting with it through smart contracts.

**_What is a Lightning Channel?_** A Lightning Channel is a connection between two Lightning users. Each of the users locks up some number of bitcoins on the Bitcoin blockchain using a multi-sig signed by both of them. The two users can then exchange bitcoins through their Lightning channel without ever writing to the Bitcoin blockchain. Only when they want to close out their channel do they settle their bitcoins, based on the final division of coins.

**_What is a Lightning Network?_** Putting together a number of Lightning Channels creates the Lightning Network. This allows two users who have not created a channel between themselves to exchange bitcoins using Lightning: the protocol forms a chain of Channels between the two users, then exchanges the coins through the chain using time-locked transactions.

**_What are the Advantages of Lightning?_** Lightning allows for faster transactions with lower fees. This creates the real possibility of bitcoin-funded micropayments. It also offers better privacy, since it's off-chain with only the first and last states of the transaction being written to the immutable Bitcoin ledger.

**_What are the Disadvantages of Lightning?_** Lightning is still a very new technology and hasn't been tested as thoroughly as Bitcoin. That's not just a question of the technological implementation, but also whether the design itself can be gamed in any unexpected ways.

### Lightning - In Short

One way to think of Lightning is: _a way to transact bitcoins using off-chain channels between pairs of people, so that only a first and final state have to be written to the blockchain_.

## Summary: Introducing Bitcoin

Bitcoin is a peer-to-peer system that allows for the transfer of funds through transactions that are locked with puzzles. These puzzles are dependent upon public-key elliptic-curve cryptography. When you generalize the ideas behind Bitcoin, you get blockchains, a technology that's currently growing and innovating. When you expand the ideas behind Bitcoin, you get layer-2 protocols such as Lightning, which expand the currency's potential.

## What's Next?

Advance through "Preparing for Bitcoin" with [Chapter Two: Setting Up a Bitcoin-Core VPS](02_0_Setting_Up_a_Bitcoin-Core_VPS.md).
