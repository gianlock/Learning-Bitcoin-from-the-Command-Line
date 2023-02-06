# 3.3: Configurare il Tuo Wallet

Ora siete pronti per iniziare a lavorare con Bitcoin. Per cominciare, dovrete creare un wallet per inviare e ricevere fondi.

## Creare un Wallet

> :warning: **AVVISO SULLA VERSIONE:** Le nuove versioni di Bitcoin Core, a partire dalla v0.21.0, non creano più automaticamente un wallet predefinito all'avvio. È quindi necessario crearne uno manualmente. Ma se state utilizzando una versione precedente di Bitcoin Core, un nuovo wallet è già stato creato e potete passare a [Creare un Indirizzo](#creare-un-indirizzo).

La prima cosa da fare è creare un nuovo wallet, con il comando `bitcoin-cli createwallet`. Creando un nuovo wallet, si creerà la coppia di chiavi pubbliche e private. La chiave pubblica è la fonte da cui verranno creati i tuoi indirizzi, mentre la chiave privata è quella che ti permetterà di spendere i fondi che riceverai nei tuoi indirizzi. Bitcoin Core salverà automaticamente queste informazioni in un file `wallet.dat` nella cartella `~/.bitcoin/testnet3/wallets`.

Se verifichi la cartella `wallets`, vedrai che attualmente è vuota.
```
$ ls ~/.bitcoin/testnet3/wallets
$
```

Anche se Bitcoin Core non creerà un nuovo wallet per te, all'avvio caricherà comunque un wallet di primo livello senza nome ("") per impostazione predefinita. Potete approfittarne creando un nuovo wallet senza nome.
```
$ bitcoin-cli -named createwallet wallet_name="" descriptors=false

{
  "name": "",
  "warning": ""
}
```

Ora, la tua cartella `wallets` dovrebbe risultare popolata.
```
$ ls ~/.bitcoin/testnet3/wallets
database  db.log  wallet.dat
```

> :book: ***Cos'è un wallet Bitcoin?*** Un wallet Bitcoin è l'equivalente digitale di un portafoglio fisico sulla rete Bitcoin. In esso sono memorizzate le informazioni sulla quantità di bitcoin posseduti e sulla loro posizione (indirizzi), oltre ai modi in cui è possibile spenderli. Spendere denaro fisico è intuitivo, ma per spendere i bitcoin gli utenti devono fornire la corretta _chiave privata_. Lo spiegheremo in modo più dettagliato durante il corso, ma per ora è bene sapere che questa dinamica di chiave pubblica e privata è parte di ciò che rende Bitcoin sicuro e _trustless_. Le informazioni sulla coppia di chiavi vengono salvate nel file `wallet.dat`, oltre ai dati sulle preferenze e sulle transazioni. Per lo più, non ci si dovrà preoccupare della chiave privata: `bitcoind` la userà quando sarà necessaria. Tuttavia, questo rende il file `wallet.dat` estremamente importante: se lo si perde, si perdono le chiavi private, e se si perdono le chiavi private, si perdono i fondi!

Bene, ora avete un wallet Bitcoin. Ma un wallet è poco utile per ricevere bitcoin se prima non si crea un indirizzo.

> :warning: **AVVISO SULLA VERSIONE:** A partire da Bitcoin Core v 23.0, i portafogli con descrittori sono diventati predefiniti. È un'ottima cosa, perché i portafogli con descrittori sono molto potenti, ma al momento non funzionano con i multisigs! Quindi, li disattiviamo con l'argomento "descriptors=false". Vedi [§3.5](03_5_Capire_il_Descrittore.md) per approfondire i descrittori.

## Creare un Indirizzo

La prossima cosa da fare è creare un indirizzo per ricevere i pagamenti. Questo è possibile con il comando `bitcoin-cli getnewaddress`. Ricorda che se vuoi maggiori informazioni su questo comando, devi digitare `bitcoin-cli help getnewaddress`. Attualmente esistono tre tipi di indirizzi: `legacy` e i due tipi di indirizzi SegWit, `p2sh-segwit` e `bech32`. Se non si specifica diversamente, si otterrà quello predefinito, che attualmente è `bech32`.

Tuttavia, per le prossime sezioni utilizzeremo indirizzi `legacy`, sia perché `bitcoin-cli` ha avuto alcuni problemi iniziali con le prime versioni degli indirizzi SegWit, sia perché altre persone potrebbero non essere in grado di inviare a indirizzi `bech32`. È improbabile che questo sia un problema per te, ma per il momento vogliamo che inizi con esempi di transazioni che sono (per lo più) garantite come funzionanti.

Per prima cosa, riavvia `bitcoind` in modo che il nuovo wallet senza nome sia impostato come predefinito e caricato automaticamente.
```
$ bitcoin-cli stop
Bitcoin Core stopping # wait a minute so it stops completely
$ bitcoind -daemon
Bitcoin Core starting # wait a minute so it starts completely
```

A questo punto è possibile creare un indirizzo. È possibile richiedere un indirizzo `legacy` con il secondo argomento di `getnewaddress` o con l'argomento `addresstype`.
```
$ bitcoin-cli getnewaddress -addresstype legacy
moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B
```
Nota che questo indirizzo inizia con una "m" (o talvolta con una "n") per indicare un indirizzo Legacy di testnet. Sarebbe un "2" per un indirizzo P2SH o un "tb1" per un indirizzo Bech32.

> :link: **TESTNET vs MAINNET:** L'indirizzo equivalente della mainnet inizierebbe con "1" (per Legacy), "3" (per P2SH) o "bc1" (per Bech32).

Prendete nota dell'indirizzo. Dovrete fornirlo a chi vi invierà i fondi.

> :book: ***Cos'è un indirizzo Bitcoin?*** Un indirizzo Bitcoin è letteralmente dove si riceve il denaro. È come un indirizzo e-mail, ma per i fondi. Tecnicamente, si tratta di una chiave pubblica, anche se i diversi schemi di indirizzo la gestiscono in modo diverso. Tuttavia, a differenza di un indirizzo di posta elettronica, un indirizzo Bitcoin dovrebbe essere considerato monouso: usatelo per ricevere fondi solo _una volta_. Quando volete ricevere fondi da qualcun altro o in un altro momento, generate un nuovo indirizzo. Questo è consigliato soprattutto per migliorare la privacy dell'utente. L'intera blockchain è immutabile, il che significa che gli explorer possono esaminare lunghe catene di transazioni nel tempo, rendendo possibile determinare statisticamente chi sei tu e i tuoi contatti, a prescindere da quanto tu sia attento. Tuttavia, se si continua a riutilizzare lo stesso indirizzo, questo diventa ancora più facile. Creando il tuo primo indirizzo Bitcoin, hai anche iniziato a riempire il tuo wallet Bitcoin. Più precisamente, avete iniziato a riempire il file `wallet.dat` nella vostra directory `~/.bitcoin/testnet3 /wallets`.

Con un singolo indirizzo in mano, si può passare direttamente alla sezione successiva e iniziare a ricevere fondi. Tuttavia, prima di arrivare a questo punto, discuteremo brevemente degli altri tipi di indirizzi che incontrerete in futuro e parleremo di alcuni altri comandi del wallet che potresti voler usare in futuro.

### Conoscere gli Indirizzi Bitcoin

Esistono tre tipi di indirizzi Bitcoin che si possono creare con il comando RPC `getnewaddress`. In questo caso si utilizzerà un indirizzo `legacy` (P2PKH), mentre si passerà a un indirizzo SegWit (P2SH-SegWit) o Bech32 in [§4.6: Creare una Transazione Segwit](04_6_Creare_una_Transazione_Segwit.md).

Come già detto, la base di un indirizzo Bitcoin è una chiave pubblica: qualcuno invia fondi alla vostra chiave pubblica e voi usate la vostra chiave privata per riscattarli. Semplice? Ma mettere in giro la propria chiave pubblica non è del tutto sicuro. Al momento, se qualcuno possiede la vostra chiave pubblica, non può recuperare la vostra chiave privata (e quindi i vostri fondi); questa è la base della crittografia, che utilizza una funzione di trap-door per garantire che si possa passare solo dalla chiave privata a quella pubblica, e non viceversa. Ma il problema è che non sappiamo cosa ci riserverà il futuro. Sappiamo però che i sistemi di crittografia finiscono per essere violati dall'inarrestabile progresso della tecnologia, quindi è meglio non mettere in rete chiavi pubbliche grezze, per proteggere le transazioni dal futuro.

Le transazioni Bitcoin tradizionali creavano indirizzi P2PKH che aggiungevano un ulteriore passaggio crittografico per proteggere le chiavi pubbliche.

> :book: ***Cos'è un indirizzo Legacy (P2PKH)?*** Si tratta di un indirizzo Legacy del tipo utilizzato dalla prima rete Bitcoin. Lo utilizzeremo negli esempi delle prossime sezioni. È chiamato indirizzo Pay to PubKey Hash (o P2PKH) perché l'indirizzo è un hash a 160 bit di una chiave pubblica. L'utilizzo di un hash della propria chiave pubblica come indirizzo crea un processo a due fasi in cui per spendere i fondi è necessario rivelare sia la chiave privata che la chiave pubblica, aumentando di conseguenza la sicurezza futura. Questo tipo di indirizzo rimane importante per ricevere fondi da persone con software wallet non aggiornati.

Come descritto più dettagliatamente in [§4.6: Creare una Transazione Segwit](04_6_Creare_una_Transazione_Segwit.md), le _Block Size Wars_ (guerre sulla dimensione dei blocchi) della fine degli anni '10 hanno portato a un nuovo tipo di indirizzo: SegWit. Questo è il tipo di indirizzo attualmente preferito e a questo punto dovrebbe essere pienamente integrato in Bitcoin-Core, ma comunque lo lasciamo per il §4.6.

SegWit significa semplicemente " segregated witness" (testimone segregato) ed è un modo per separare le firme della transazione dal resto della transazione per ridurre le dimensioni della transazione stessa. Alcuni indirizzi SegWit si intrufoleranno in alcuni dei nostri esempi prima del §4.6 come indirizzi di modifica, che vedreai come indirizzi che iniziano con "tb". Questo va bene perché `bitcoin-cli` supporta completamente il loro utilizzo. Ma non li useremo comunque.

Esistono due indirizzi di questo tipo:

> :book: ***Cos'è un indirizzo P2SH-SegWit (aka Nested SegWit)?*** Si tratta della prima generazione di SegWit. L'indirizzo SegWit è racchiuso in un hash Script per garantire la compatibilità con il passato. Il risultato è che le transazioni sono più piccole di circa il 25% (con una rispettiva riduzione delle commissioni di transazione).

> :book: ***Cos'è un indirizzo Bech32 (aka Native SegWit, aka P2WPKH)?*** Questa è la seconda generazione di SegWit. È completamente descritta in [BIP 173](https://en.bitcoin.it/wiki/BIP_0173). Crea transazioni ancora più piccole, ma soprattutto presenta alcuni vantaggi nella creazione di indirizzi meno inclini all'errore umano e ha una correzione implicita degli errori. Non è *compatibile* all'indietro come lo era P2SH-SegWit, e quindi alcune persone potrebbero non essere in grado di inviare a questo tipo di indirizzo.

Esistono altri tipi di indirizzi Bitcoin, come il P2PK (che paga una chiave pubblica nuda, deprecato a causa della sua futura insicurezza) e il P2SH (che paga uno Script Hash, utilizzato dagli indirizzi Nested SegWit di prima generazione; lo vedremo meglio tra qualche capitolo).

## Opzionale: Firmare un Messaggio

A volte potresti avere la necessità di dimostrare che controlli un indirizzo Bitcoin (o meglio, che ne controlli la chiave privata). Questo è importante perché permette di sapere che si stanno inviando fondi alla persona giusta. Questo può essere fatto creando una firma con il comando `bitcoin-cli signmessage`, nella forma `bitcoin-cli signmessage [indirizzo] [messaggio]`. Ad esempio:
```
$ bitcoin-cli signmessage "moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B" "Hello, World"
HyIP0nzdcH12aNbQ2s2rUxLwzG832HxiO1vt8S/jw+W4Ia29lw6hyyaqYOsliYdxne70C6SZ5Utma6QY/trHZBI=
```
Si otterrà in risposta la firma.

> :book: ***Cos'è una firma?*** Una firma digitale è una combinazione di un messaggio e di una chiave privata che può essere sbloccata con una chiave pubblica. Poiché esiste una corrispondenza uno-a-uno tra gli elementi di una coppia di chiavi, lo sblocco con una chiave pubblica dimostra che il firmatario è in possesso della chiave privata corrispondente.

Un'altra persona può quindi utilizzare il comando `bitcoin-cli verifymessage` per verificare la firma. Inserisce l'indirizzo in questione, la firma e il messaggio:
```
$ bitcoin-cli verifymessage "moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B" "HyIP0nzdcH12aNbQ2s2rUxLwzG832HxiO1vt8S/jw+W4Ia29lw6hyyaqYOsliYdxne70C6SZ5Utma6QY/trHZBI=" "Hello, World"
true
```
Se tutti corrispondono, l'altra persona sa che può tranquillamente trasferire fondi alla persona che ha firmato il messaggio inviandolo all'indirizzo.

Se un black hat stesse inventando le firme, il risultato sarebbe invece negativo:
```
$ bitcoin-cli verifymessage "FAKEV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B" "HyIP0nzdcH12aNbQ2s2rUxLwzG832HxiO1vt8S/jw+W4Ia29lw6hyyaqYOsliYdxne70C6SZ5Utma6QY/trHZBI=" "Hello, World"
error code: -3
error message:
Invalid address
```

## Opzionale: Scaricare il wallet

Potrebbe sembrare pericoloso avere tutte le proprie chiavi private irriproducibili in un unico file. Ecco a cosa serve `bitcoin-cli dumpwallet`. Permette di fare una copia del proprio wallet.dat:
```
$ bitcoin-cli dumpwallet ~/mywallet.txt
```
Il file `mywallet.txt` nella vostra home directory conterrà un lungo elenco di chiavi private, indirizzi e altre informazioni. Si badi bene, non si vorrebbe mai mettere questi dati in un file di testo semplice su una configurazione Bitcoin con fondi reali!

È possibile recuperarlo con `bitcoin-cli importwallet`.
```
$ bitcoin-cli importwallet ~/mywallet.txt
```
Ma questo richiede un nodo _unpruned_!
```
$ bitcoin-cli importwallet ~/mywallet.txt
error code: -4
error message:
Importing wallets is disabled when blocks are pruned
```

## Opzionale: Visualizzare le Chiavi Private

A volte potresti voler dare un'occhiata alle chiavi private associate ai tuoi indirizzi Bitcoin. Forse si vuole essere in grado di firmare un messaggio o spendere bitcoin da un'altra macchina. Forse si vuole semplicemente fare un backup di alcune chiavi private importanti. È possibile farlo anche con il file di dump, poiché è leggibile dall'uomo.
```
$ bitcoin-cli dumpwallet ~/mywallet.txt
{
  "filename": "/home/standup/mywallet.txt"
}
```
È più probabile che si voglia solo esaminare la chiave privata associata a un indirizzo specifico. Questo può essere fatto con il comando `bitcoin-cli dumpprivkey`.
```
$ bitcoin-cli dumpprivkey "moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B"
cTv75T4B3NsG92tdSxSfzhuaGrzrmc1rJjLKscoQZXqNRs5tpYhH
```
È quindi possibile salvare la chiave in un luogo sicuro, preferibilmente non collegato a Internet.

È anche possibile importare qualsiasi chiave privata, da un dump di un portafoglio o da un dump di una chiave individuale, come segue:
```
$ bitcoin-cli importprivkey cW4s4MdW7BkUmqiKgYzSJdmvnzq8QDrf6gszPMC7eLmfcdoRHtHh
```
Anche in questo caso, è necessario un nodo _unpruned_. Ci vorrà un po' di tempo, perché `bitcoind` deve rileggere tutte le transazioni passate, per vedere se ce ne sono di nuove a cui prestare attenzione.

> :information_source: **NOTA:** Molti portafogli moderni preferiscono i [codici mnemonici] (https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) per generare i semi necessari a creare le chiavi private. Questa metodologia non è utilizzata in `bitcoin-cli`, quindi non sarà possibile generare comode liste di parole per ricordare le chiavi private.

_Hai digitato spesso l'indirizzo Bitcoin che hai generato, mentre firmavi i messaggi e ora per scaricare le chiavi. Se pensi che sia una seccatura, siamo d'accordo. È anche soggetto a errori, un argomento che affronteremo nella prossima sezione._

## Riepilogo: Configurare il Tuo Wallet

Per ricevere fondi è necessario creare un indirizzo. Il tuo indirizzo è memorizzato in un portafoglio, di cui puoi fare il backup. È anche possibile fare molte altre cose con un indirizzo, come scaricare la sua chiave privata o usarla per firmare i messaggi. Ma in realtà, la creazione dell'indirizzo è tutto ciò che occorre fare per ricevere fondi Bitcoin.

## Cosa c'è Dopo?

Fai un passo indietro da "Capire la Tua Configurazione Bitcoin" con [Intermezzo: Utilizzare Variabili della Linea di Comando](03_3__Intermezzo_Utilizzare_Variabili_Linea_di_Comando.md).
