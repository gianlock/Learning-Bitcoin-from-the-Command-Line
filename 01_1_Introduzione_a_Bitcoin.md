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

**_Cosa sono i campi finiti?_** Un campo finito è un insieme finito di numeri, in cui i risultati di tutte le addizioni, sottrazioni, moltiplicazioni e divisioni sono compresi nello stesso campo finito. Un modo semplice per creare un campo finito è attraverso l'uso di una funzione modulo.

**_Come viene definita una curva ellittica su un campo finito?_** Una curva ellittica definita su campo finito possiede i punti della curva tracciati da un campo finito specifico. Questo assume la forma: `y`<sup>`2`</sup> `% GrandezzaCampo = (x`<sup>`3`</sup>` + ax + b) % GrandezzaCampo` Il campo finito usato per la curva ellittica secp256k1 è: `2`<sup>`256`</sup>` - 2`<sup>`32`</sup>` - 2`<sup>`9`</sup>` - 2`<sup>`8`</sup>` - 2`<sup>`7`</sup>` - 2`<sup>`6`</sup>` - 2`<sup>`4`</sup>` - 1`.

**_Come vengono utilizzate le curve ellittiche nella crittografia?_** Nella crittografia a curva ellittica, un utente seleziona un numero molto grande (256 bit) come chiave privata. Quindi aggiunge un punto base impostato sulla curva a se stesso tante volte. (In secp256k1, il punto base è `G = 04 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798 483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A695D48FFBD 483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A695D48FFBD', che antepone alle due parti della tupla uno "04" per indicare che il punto dati è in formato non compresso. Se preferisci una definizione geometrica lineare, è il punto "0x79BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798,0x483ADA7726A3C4655DA4FBFC0E1108A8FD17B448A68554199C47D08FFB10D4B8") Il numero risultante è la chiave pubblica. Varie formule matematiche possono quindi essere utilizzate per dimostrare la proprietà della chiave pubblica, data la chiave privata. Questa è una funzione a senso unico: è facile passare dalla chiave privata alla chiave pubblica e quasi impossibile passare dalla chiave pubblica alla chiave privata.

Questa particolare proprietà spiega perché i campi finiti vengono utilizzati nelle curve ellittiche: garantisce che la chiave privata non diventi troppo grande. Si noti che il campo finito per secp256k1 è leggermente inferiore a 256 bit, il che significa che tutte le chiavi pubbliche saranno lunghe 256 bit, proprio come lo sono le chiavi private.

**_Quali sono i vantaggi dell'ECC?_** Il vantaggio principale dell'ECC è di consertire un livello di sicurezza della classica crittografia a chiave pubblica con una chiave molto più piccola. Una chiave pubblica a curva ellittica a 256 bit corrisponde a una chiave pubblica tradizionale (RSA) a 3072 bit.

### ECC - In Breve

Possiamo pensare all'ECC come: _un modo di usare la crittografia a chiave pubblica che sfrutta chiavi molto piccole e matematica complessa._

## Sulle Blockchain

La Blockchain è la generalizzazione del metodo utilizzato da Bitcoin per creare un registro globale distribuito. Come tante altre criptovalue alternative, Bitcoin è una blockchain, ognuna delle quali vive sulla propria rete e scrive sulla propria catena. Anche le sidechain come Liquid sono blockchain. Le blockchain non hanno il bisogno di avere a che fare con il mondo della finanza. Ad esempio, ci sono state molte discussioni sull'utilizzo di blockchain per proteggere le identità auto-sovrane.

Sebbene tu debba comprendere le basi di come funziona una blockchain per capire come funzionano le transazioni in Bitcoin, non avrai bisogno di andare oltre. Poiché le blockchain sono diventate una vasta categoria di tecnologie, questi concetti di base saranno probabilmente applicabili a molti altri progetti in questo settore. Tuttavia, i comandi di programmazione appresi in questo libro non lo saranno, poiché specifici per Bitcoin (e Lightning).

**_Perché si chiama chain (catena)?_** Ogni blocco nella blockchain memorizza un hash del blocco precedente. Questo collega il blocco attuale fino al primo blocco originale (Blocco Genesi), attraverso una catena ininterrotta. È un modo per creare un ordine assoluto tra dati potenzialmente in conflitto. Poichè ogni blocco è costruito al di sopra di quello precedente attraverso un algoritmo di Proof-of-Work (Prova di Lavoro), più blocchi verranno costruiti, più la catena sarà computazionalmente sconveniente da ricorstruire. Questo rende una blockchain irreversibile e quindi sicura.

**_Cos'è un Fork?_** Occasionalmente vengono creati due blocchi nello stesso momento. Questo crea temporaneamente un fork di un blocco, dove entrambi i blocchi potrebbero essere quelli "reali". Di tanto in tanto, un fork potrebbe espandersi fino a diventare lungo due, tre o anche quattro blocchi, ma abbastanza rapidamente si determinerà che solo uno dei fork è quello accettato, mentre l'altro sarà considerato "orfano". Questo fa parte del processo stocastico di creazione dei blocchi e dimostra perché diversi blocchi devono essere costruiti nella blockchain prima che possa essere considerato valido e non ripudiabile.

### Blockchain — In Breve

Un modo di pensare alla blockchain è: _una serie di blocchi di dati immutabili, retroattivamente riconducibili_. Un altro modo è: _una serie di blocchi collegati per ordinare in modo assoluto i dati che potrebbero essere in conflitto_.

## La Blockchain fa al caso mio?

Se vuoi effettuare transazioni in bitcoin, allora ovviamente Bitcoin è giusto per te. Tuttavia, il termine blockchain è in voga al giorno d'oggi e non è la bacchetta magica per risolvere ogni tipo di problema tecnico. Detto questo, ci sono molte situazioni specifiche in cui la blockchain è una spanna sopra le tecnologie concorrenti.

Le blockchain _saranno_ probabilmente utili se:

  * Gli utenti non si fidano l'uno dell'altro.
    * Oppure: Gli utenti sono presenti in diversi paesi.
  * Gli utenti non si fidano delle autorità centrali.
    * E: Gli utenti vogliono controllare il proprio futuro.
  * Gli utenti vogliono una tecnologia trasparente.
  * Gli utenti vogliono condividere qualcosa.
    * E: Gli utenti desiderano che ciò che viene condiviso sia registrato in modo permanente.
  * Gli utenti vogliono una transazione rapida e definitiva.
    * Ma: Gli utenti non hanno bisogno di una transazione immediata e definitiva.

Le blockchain _non saranno_ probabilmente utili se:

  * Gli utenti sono fidati:
    * es.: le transazioni avvengono all'interno di un'azienda o organizzazione.
    * es.: le transazioni sono controllate da un'autorità centrale.
  * La segretezza è necessaria:
    * es.: Le informazioni devono essere segrete.
    * es.: Le transazioni devono essere segrete.
    * es.: Gli utilizzatori devono essere segreti.
    * A meno che: Una metodologia per la segretezza crittografica è attentamente considerata, analizzata e testata.
  * Gli utenti hanno bisogno di una transazione immediata e definitiva.
    * es.: in meno di 10 minuti su una rete simile a Bitcoin, in meno di 2,5 minuti su una rete simile a Litecoin, in meno di 15 secondi su una rete simile a Ethereum

Si noti che per alcune di queste situazioni possono ancora esistere soluzioni all'interno dell'ecosistema Bitcoin. Ad esempio, i canali di pagamento stanno rapidamente affrontando le questioni della liquidità e della definitività del pagamento.

## Lightning

Lightning è un layer-2 (protocollo di secondo livello) che interagisce con Bitcoin per consentire agli utenti di scambiare i propri bitcoin "off-chain" (esternamente alla blockchain principale). Rispetto l'utilizzo diretto di Bitcoin presenta sia vantaggi che svantaggi.

Lightning è anche l'argomento secondario di questo tutorial. Sebbene si occupi principalmente di interagire direttamente con Bitcoin (e con `bitcoind`), dedica una certa attenzione a Lightning perché è una tecnologia emergente che probabilmente diventerà un'alternativa diffusa a Bitcoin. Questo libro adotta lo stesso approccio a Lightning e a Bitcoin: insegna come interagire direttamente con un deamon Lightning da riga di comando.

A differenza di Bitcoin, esistono diverse varianti di Lightning. Questo tutorial utilizza l'implementazione [c-lightning](https://github.com/ElementsProject/lightning) come server Lightning attendibile.

**_Cos'è un protocollo di livello 2?_** Un protocollo layer-2 è un protocollo costruito sopra il protocollo principale o "blockchain madre". In questo caso, Lightning opera sopra Bitcoin, interagendo con esso tramite smart contracts.

**_Cos'è un canale Lightning_** Un canale Lightning è una connessione tra due utenti Lightning. Ciascuno degli utenti blocca un certo numero di bitcoin sulla blockchain Bitcoin utilizzando un multi-sig firmato da entrambi. I due utenti possono quindi scambiare bitcoin attraverso il loro canale Lightning senza mai scrivere sulla blockchain principale. Solo quando vorranno chiudere il loro canale regoleranno i loro bitcoin in base alla divisione finale delle monete.

**_Cos'è una rete Lightning?_** L'intreccio di una serie di canali Lightning crea la rete Lightning. Ciò consente a due utenti senza un canale Lightining di scambiare tra loro bitcoin : il protocollo collega i due utenti creando una catena di canali e scambia le monete utilizzando transazioni bloccate nel tempo.

**_Quali sono i vantaggi di Lightning?_** Lightning consente di effettuare transazioni più veloci con commissioni inferiori. Questo rende reale la possibilità di micropagamenti finanziati da bitcoin. In aggiunta Lightning, in quanto off-chain, offre una migliore privacy in quanto solo il primo e l'ultimo stato della transazione verranno riportati nel ledger Bitcoin (libro mastro immutabile di Bitcoin).

**_Quali sono gli svantaggi di Lightning?_** Lightning è ancora una tecnologia molto nuova e non testata a fondo come Bitcoin. Non si tratta solo di una questione di implementazione tecnologica, ma anche di capire se il protocollo stesso può essere sfruttato in modo inaspettato.

### Lightning - In Breve

Possiamo pensare a Lightning come: _un modo per trasferire bitcoin utilizzando canali off-chain tra coppie di persone, in modo che solo un primo e un ultimo stato debbano essere scritti sulla blockchain_.

## Sommario: Presentazione di Bitcoin

Bitcoin è un sistema peer-to-peer che consente il trasferimento di fondi attraverso transazioni bloccate da puzzle crittografici. Questi enigmi dipendono dalla crittografia a curva ellittica a chiave pubblica. Generalizzando le idee alla base del Bitcoin, si ottiene la blockchain, una tecnologia in continua crescita e innovazione. Quando si espandono le idee alla base di Bitcoin, si ottengono protocolli di livello 2 come Lightning, che ampliano il potenziale della valuta.

## Cosa c'è dopo?

Avanza verso "Prepararsi a Bitcoin" con [Capitolo 2: Configurazione di un Bitcoin-Core VPS](02_0_Configurazione_di_un_Bitcoin-Core_VPS.md).
