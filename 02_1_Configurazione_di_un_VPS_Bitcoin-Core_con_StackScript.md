# 2.1:  Configurazione di un VPS Bitcoin-Core con Bitcoin Standup

Questo documento spiega come configurare un VPS (Server Virtuale Privato) per far girare un nodo Bitcoin su Linode.com, installato utilizzando uno StackScript automatico del [progetto Bitcoin Standup](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts). Dovrai solo eseguire qualche comando e avviare il tuo VPS. Quasi immediatamente dopo l'avvio, troverai il tuo nuovo nodo Bitcoin che scarica felicemente i blocchi.

> :warning: **ATTENZIONE:** Non usare un VPS per gestire un wallet bitcoin con una somma consistente di fondi reali; leggi http://blog.thestateofme.com/2012/03/03/lessons-to-be-learned-from-the-linode-bitcoin-incident/ . È molto bello poter sperimentare transazioni bitcoin reali su un nodo live, senza dover vincolare un server self-hosted su una rete locale. È anche utile aver la possibilità di usare un dispositivo mobile per comunicare via SSH con il tuo VPN per eseguire alcune semplici operazioni con bitcoin. Ma è richiesto un elevato livello di sicurezza per gestire significative quantità di fondi.

* Se vuoi capire come funziona questa configurazione, leggi [Appendice I: Capire Bitcoin Standup ](A1_0_Capire_Bitcoin_Standup.md)durante l'installazione.
* Se, invece, vuoi configurare una macchina diversa da un VPS Linode, come un macchina AWS o un Mac, leggi [§2.2: Configurazione di una Macchina Bitcoin-Core Tramite Altri Metodi](02_2_Configurazione_di_un_Bitcoin-Core_Altro.md)
* Se invece stai già eseguendo un nodo Bitcoin, passa al [Capitolo Tre: Capire la Tua Configurazione Bitcoin](03_0_Capire_la_Tua_Configurazione_Bitcoin.md)

## Per Iniziare con Linode

Linode è un servizio di Cloud Hosting che offre server Linux veloci ed economici con archiviazione SSD. Li utilizzeremo per questo tutorial principalmente perchè i loro StackScript basati su BASH offrono un modo semplice per configurare automaticamente un nodo Bitcoin senza problemi.

### Configurare un Account Linode

Puoi creare un account Linode al seguente link:

```
https://www.linode.com
```

Se preferisci, il link di seguito contiene un codice sconto che ti regala due mesi di utilizzo gratuito (fino a €100), ottimo per imparare Bitcoin: 

<https://www.linode.com/?r=3c7fa15a78407c9a3d4aefb027539db2557b3765>

Dovrai fornire un indirizzo mail e successivamente ricaricare l'importo per i costi futuri da una carta di credito o PayPal.

Una volta terminato, dovresti atterrare sulla pagina <https://cloud.linode.com/dashboard>.

### Prendete in Considerazione la 2FA

La sicurezza del tuo server non sarà completa se qualcuno può accedere al account Linode, quindi considera si abilitare l'Autenticazione a Due Fattori. Puoi trovare questa configurazione nella sezione [My Profile: Password & Authentication page](https://manager.linode.com/profile/auth). Se non lo fai ora, segnatelo in una TODO-list per dopo.

## Creare l'Immagine di Linode Usando uno StackScript

### Caricare lo StackScript

Scarica lo [Script Standup Linode](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/Scripts/LinodeStandUp.sh) dalla [repo Bitcoin Standup Scripts](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts). Questo script semplicemente automatizza tutte le istruzioni di configurazione del VPS Bitcoin. Se vuoi essere particolarmente prudente, leggi lo script con attenzione. In alternativa, potete copiare questo StackScript nella [pagina Stackscripts](https://cloud.linode.com/stackscripts?type=account) del vostro account Linode e selezionando [Create New Stackscript](https://cloud.linode.com/stackscripts/create). Assegnali un nome (noi abbiamo usato 'Bitcoin Standup'), poi copia e incolla lo script. Selezionate Debian 11 come immagine di destinazione e poi "Salva".

### Configurazione Iniziale

Ora sei pronto per creare un nodo basato sullo Stackscript.

1. Nella [pagina StackScript](https://cloud.linode.com/stackscripts?type=account), clicca su "..." alla destra del nuovo script e scegli "Deploy New Linode".
2. Inserite un hostname breve e uno completo 
   * **_Short Hostname_.** scegliete un nome per il VPS. Ad esempio, "miobtctest".
   * **_Fully Qualified Hostname_.** Se intendi includere questo VPS come parte di una rete con record DNS completi, digita il nome dell'host con il relativo dominio.Ad esempio, "miobtctest.miodominio.com". Altrimenti, basta ripetere l'hostname breve e aggiungere ".local", ad esempio "miobtctest.local".
3. Inserisci la password per l'utente "standup".
4. Compila le opzioni avanzate necessarie.
   * **_X25519 Public Key_.** Si tratta di una chiave pubblica da aggiungere all'elenco dei client autorizzati a Tor. Se non la utilizzerai, chiunque ottenga il codice QR del vostro nodo potrà accedervi. Otterrai questa chiave pubblica da qualsiasi client si utilizzi per connettersi al proprio nodo. Ad esempio, se si usa [FullyNoded 2](https://github.com/BlockchainCommons/FullyNoded-2), si può andare nelle sue impostazioni e selezionare "Export Tor V3 Authentication Public Key" da usare qui.
   * **_Installation Type_.** Si tratta di scegliere tra "_Mainnet_" o "_Pruned Mainnet_" se stai configurando un nodo per l'utilizzo e "_Testnet_" o "_Pruned Testnet_" se, invece, stai solo sperimentando. La maggior parte di questa esercitazione presuppone che abbiate scelto "_Pruned Testnet_", ma dovreste essere in grado di seguirla anche con le altre tipologie. Leggi la [Synopsis](#synopsis-tipi-installazione-bitcoin) per maggiori informazioni su queste opzioni. (Nota che se stai pensando di provare i capitoli su relativi a Lightning, dovrai utilizzare un noto _Unpruned_, poiché lavorare con i nodi _Pruned_ su Lightning è problematico. Vai al capitolo [§19.1](19_1_Verificare_Configurazione_Lightning.md#compiling-the-source-code) per le specifiche.)
   * **_SSH Key_.** Copia qui la chiave SSH del tuoi computer locale; questo ti permetterà di effettuare automaticamente il login via SSH al tuo account standup. Se non hai mai configurato una chiave SSH sul tuo computer, puoi seguire questa guida su [Github](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/). Si consiglia di aggiungere la chiave SSH nel LISH di Linode (Linode Interactive Shell) accedendo alla sezione "Linode Home Page / My Preferences / LISH Settings /  LISH Keys". L'uso di una chiave SSH consente di accedere al server in modo più semplice e sicuro.
   * **_SSH-Allowed IPs_.** Si tratta di un elenco di IP separato da virgole a cui sarà consentito l'accesso al VPS tramite SSH. Per esempio "192.168.1.15,192.168.1.16". Se non inserisci alcun IP, *il tuo VPS non sarà molto sicuro*. Sarà costantemente bombardato da aggressori che cercheranno di entrare e potrebbero riuscirci.
5. Seleziona una Immagine
   * **_Target Image_.** Se avete seguito le istruzioni, questo vi permetterà di selezionare solo "Debian 11".(anche se versioni precedenti di questo Stackscript funzionavano e potrebbero ancora funzionare con Debian 9 o 10).
6. Scegli una regione per localizzare il tuo Linode.

*Le domande rimanenti hanno tutte a che fare con la dinamica di implementazione del VPS e dovrebbero essere lasciate così come sono, con un'unica eccezione: sposta lo Swap Disk da 256MB a 512MB, per assicurarti di avere abbastanza memoria per scaricare la blockchain.*

### Scegliere Altre Opzioni di Standup

Blockchain Commons sta attualmente ampliando i suoi script di standup per Bitcoin con opzioni per installare Lightning e altre applicazioni Bitcoin di rilievo. Dai un'occhiata a tutte le opzioni extra e vedi se sono cose con cui ti piacerebbe sperimentare. In particolare, se stai considerando di configurare Lightning, ti suggeriamo di installarla, perchè renderà il [Capitolo 19](19_0_Capire_Configurazione_Lightning.md) e [Capitolo 20](20_0_Usare_Lightning.md) molto più semplici.

### Scegli un Piano Linode

Dovrai ora scegliere un piano Linode.


Linode sceglierà di default i piani Dedicated-CPU, ma è possibile selezionare il più economico Shared-CPU. Un Linode con Shared-CPU di 4GB sarà sufficiente per la maggior parte dei setup, incluso: _Pruned Mainnet_, _Pruned Testnet_, ed anche _non-Pruned Testnet_. Queste configurazioni usano meno di 50GB di memoria e 4GB di  They all use less than 50G of storage and 4GB di RAM sono una quantità adeguata.

Se invece vuoi avere una _non-Pruned Mainnet_ nel tuo VPS, è necessario installare un Linode con un disco superiore a 500G(!), che attualmente è il Linode 32GB, che ha 640GB di spazio di archiviazione e 32GB di RAM e costa circa $160 al mese. Noi *non* consigliamo questa soluzione.

La tabella seguente mostra i requisiti minimi:

| Setup | RAM | Archiviazione | Piano Linnode |
|-------|--------|---------|---------|
| _Mainnet_ | 2GB | 280GB | Linode 16GB |
| _Pruned Mainnet_ | 2GB | ~5GB | Linode 4GB |
| _Testnet_ | 2GB | ~15GB | Linode 4GB |
| _Pruned Testnet_ | 2GB | ~5GB | Linode 4GB |
| _Regtest_ | 2GB | ~ | Linode 4GB |

Nota che potrebbero esserci modi per ridurre entrambi i costi.

* Per le macchine che suggeriamo come **Linode 4GB**, potreste essere in grado di ridurle a un Linode 2GB. Alcune versioni di Bitcoin Core hanno funzionato bene a quelle dimensioni, altre hanno occasionalmente raggiunto il limite di RAM e poi si sono riprese, altre ancora hanno continuamente raggiunto il limite di RAM. Ricordati di aumentare lo spazio di scambio per massimizzare le probabilità di funzionamento. Usalo a tuo rischio e pericolo.
* Per la _Unpruned Mainnet_, per cui suggeriamo il piano **Linode 16GB**, probabilmente puoi cavartela con un Linode 4 GB, ma aggiungere [_Block Storage_](https://cloud.linode.com/volumes) sufficiente per scaricare l'intera blockchain. Questa è certamente una soluzione migliore a lungo termine, poiché lo spazio di archiviazione della blockchain di Bitcoin aumenta continuamente se non si abilita il _prune_, mentre i requisiti della CPU non aumentano (o non nella stessa misura). Uno spazio di 640GB costerebbe $64/mese, che combinato con un piano Linode 4GB arriverebbe a $84, invece di $160, e soprattutto potete continuare a espanderla. Non documentiamo completamente questa configurazione per due motivi (1) non suggeriamo la configurazione _unpruned Mainnet_ e quindi sospettiamo che sia una configurazione molto meno comune; e (2) non abbiamo testato come i volumi di Linodes si comportino con le loro SSD in termini di prestazioni e utilizzo. Ma la documentazione completa è disponibile alla pagina Block Storage. Dovrai configurare Linode, eseguire il suo stackscript, ma poi interromperlo per spostare la memorizzazione della blockchain su un nuovo volume prima di continuare.

Se stai eseguendo un'implementazione che prevede transazioni di Bitcoin reali, potresti prendere in considerazione un Linode con CPU dedicata, che tende a costare il 50% in più rispetto al Linode con CPU condivisa. In generale abbiamo trovato le CPU condivise del tutto sufficienti, ma per un'implementazione più ampia, potresti voler prendere in considerazione livelli di affidabilità più elevati.

### Setup Finale

L'ultima cosa che devi fare è immettere una password di _root_. (Se ti sei perso qualcosa, te lo diranno in questo momento!)

Clicca "_Deploy_" per inizializzare i tuoi dischi e per preparare il tuo VPS. Tutte le attività in coda dovrebbero terminare il meno di un minuto. Al termine dovresti vedere nella sezione "_Host Job Queue_", dei pulsanti di "_Success_" che riportano "_Disk Create from StackScript - Setting password for root… done._" e "_Create Filesystem - 256MB Swap Image_".

Potrai ora cambiare nome del tuo VPS Linode da quello assegnato di default `linodexxxxxxxx`.  Vai al tab _Settings_, e cambia l'etichetta per renderla più comprensibile. Per esempio potresti rinominarlo `bitcoin-testnet-pruned` per differenziarlo da un altro VPS nel tuo account.

## Login al Tuo VPS

Se controlli il pannello di controllo di Linode, dovresti vedere il nuovo computer avviarsi. Quando il lavoro ha raggiunto il 100%, sarete in grado di accedere.

Per prima cosa, è necessario l'indirizzo IP. Cliccate sulla scheda "Linodes" e dovreste vedere un elenco del vostro VPS, il fatto che sia in esecuzione, il suo "piano", il suo indirizzo IP e alcune altre informazioni.

Vai nella tua console locale e accedi all'account `standup` usando quell'indirizzo:

```
ssh standup@[IP-ADDRESS]
```

Per esempio:

```
ssh standup@192.168.33.11
```

Se hai configurato il tuo VPS per utilizzare una chiave SSH, l'accesso dovrebbe essere automatico (eventualmente richiedendo la password SSH per sbloccare la chiave). Se non è stata configurata una chiave SSH, sarà necessario digitare la password dell'utente1.

### Aspetta Qualche Minuto

C'è un piccolo intoppo: *il vostro StackScript è in esecuzione in questo momento*. Lo script BASH viene eseguito al primo avvio del VPS. Ciò significa che il VPS non è ancora pronto.

Il tempo totale di esecuzione è di circa 10 minuti. Quindi, fate una pausa, prendete un caffè o rilassatevi per qualche minuto. Ci sono due parti dello script che richiedono un po' di tempo: l'aggiornamento di tutti i pacchetti Debian e il download del codice Bitcoin. Non dovrebbero volerci più di 5 minuti ciascuno, il che significa che se tornate dopo 10 minuti, sarete probabilmente pronti a partire.

Se si è impazienti, si può andare avanti con `sudo tail -f /standup.log` che mostrerà l'attuale progresso dell'installazione, come descritto nella prossima sezione.

## Verifica la Tua Installazione

Saprai che lo stackscrpit è stato completato quando la `tail` di `standup.log` dirà qualcosa di simile a quanto segue:

```
/root/StackScript - Bitcoin is setup as a service and will automatically start if your VPS reboots and so is Tor
/root/StackScript - You can manually stop Bitcoin with: sudo systemctl stop bitcoind.service
/root/StackScript - You can manually start Bitcoin with: sudo systemctl start bitcoind.service
```

A questo punto, la vostra home directory dovrebbe avere questo aspetto:

```
$ ls
bitcoin-22.0-x86_64-linux-gnu.tar.gz  keys.txt  SHA256SUMS  SHA256SUMS.asc
```

Questi sono i diversi file utilizzati per installare Bitcoin sul vostro VPS. *Nessuno* di essi è necessario. Li abbiamo lasciati nel caso in cui vogliate fare ulteriori verifiche. Altrimenti, potete eliminarli:

```
$ rm *
```

### Verifica la Configurazione di Bitcoin

Per assicurarsi che la release di Bitcoin scaricata sia valida, lo StackScript controlla sia la firma che il checksum SHA. È necessario verificare che entrambi i test siano corretti:

```
$ sudo grep VERIFICATION /standup.log
```

Se vedi qualcosa di simile a quanto segue, dovrebbe essere tutto a posto:

```
./standup.sh - SIG VERIFICATION SUCCESS: 9 GOOD SIGNATURES FOUND.
./standup.sh - SHA VERIFICATION SUCCESS / SHA: bitcoin-22.0-x86_64-linux-gnu.tar.gz: OK
```

Se uno di questi due controlli riporta invece "ERRORE DI VERIFICA", allora c'è un problema.

Il log contiene anche ulteriori informazioni sulle firme, se si vuole essere sicuri di sapere *chi* ha firmato la release di Bitcoin:

```
$ sudo grep -i good /standup.log
./standup.sh - SIG VERIFICATION SUCCESS: 9 GOOD SIGNATURES FOUND.
gpg: Good signature from "Andrew Chow (Official New Key) <achow101@gmail.com>" [unknown]
gpg: Good signature from "Ben Carman <benthecarman@live.com>" [unknown]
gpg: Good signature from "Antoine Poinsot <darosior@protonmail.com>" [unknown]
gpg: Good signature from "Stephan Oeste (it) <it@oeste.de>" [unknown]
gpg: Good signature from "Michael Ford (bitcoin-otc) <fanquake@gmail.com>" [unknown]
gpg: Good signature from "Oliver Gugger <gugger@gmail.com>" [unknown]
gpg: Good signature from "Hennadii Stepanov (hebasto) <hebasto@gmail.com>" [unknown]
gpg: Good signature from "Jon Atack <jon@atack.com>" [unknown]
gpg: Good signature from "Wladimir J. van der Laan <laanwj@visucore.com>" [unknown]
```

Dal momento che è tutto programmato, è possibile che ci sia stata una piccola modifica che ha fatto sì che i controlli dello script non funzionassero correttamente. (Questo è successo alcune volte nel corso del tempo in cui è stato creato lo script che è diventato Standup). Ma è anche possibile che qualcuno stia cercando di incoraggiarvi a eseguire una copia falsa del demone Bitcoin. Quindi, *sii sicuro di sapere cosa è successo prima di usare Bitcoin!*

### Leggere i Log

Si consiglia di leggere tutti i log di configurazione, per assicurarsi che non sia successo nulla di imprevisto durante l'installazione.

È meglio consultare il log standard di StackScript, che contiene tutti i risultati, compresi gli errori:

`$ sudo more /standup.log`

Si noti che è del tutto normale vedere *alcuni* errori, in particolare quando si esegue il complicatissimo software gpg e quando varie operazioni cercano di accedere al dispositivo inesistente `/dev/tty`.

Se invece si vuole guardare un insieme più piccolo di informazioni, tutti gli errori dovrebbero essere presenti:

`$ sudo more /standup.err`

Contiene ancora una discreta quantità di informazioni che non sono errori, ma è una lettura più veloce.

Se tutto sembra a posto, congratulazioni, avete un nodo Bitcoin funzionante su Linode!

## Cosa Abbiamo Fatto

Sebbene l'immagine Debian 11 predefinita che stiamo utilizzando per il tuo VPS sia stata modificata da Linode per essere relativamente sicura, il tuo nodo Bitcoin installato tramite lo StackScript Linode è impostato con un livello di sicurezza ancora più elevato. Potresti trovare questo limitante, o non essere in grado di fare cose che ti aspettavi. Ecco alcune note al riguardo:

### Servizi Protetti

L'installazione del VPS Bitcoin è minima e non consente quasi nessuna comunicazione. Ciò avviene attraverso un semplice firewall (`ufw`), che blocca tutto tranne le connessioni SSH. È inoltre possibile una sicurezza aggiuntiva per le porte RFC, grazie ai servizi nascosti installati da Tor.

**Modificare UFW.** Probabilmente dovresti lasciare UFW nella sua fase super-protetta! Non è consigliabile utilizzare una macchina Bitcoin per altri servizi, perché tutti aumentano la vostra vulnerabilità! Se decidete diversamente, ci sono diverse [guide a UFW](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands) che vi permetterà di aggiungere servizi. Come annunciato, è semplice. Per esempio, per aggiungere i servizi di posta è sufficiente aprire la porta della posta: `sudo ufw allow 25`. Ma non fatelo.

**Modificare Tor.** Potresti decidere di proteggere meglio servizi come SSH. Leggi il [Capitolo 14: Usare Tor](14_0_Usare_Tor.md) per più informazioni su Tor.

### Shell Protette

Se hai impostato "SSH-allowed IPs", l'accesso SSH (e SCP) al server è fortemente limitato. `/etc/hosts.deny` impedisce a chiunque di accedere. *Non si consiglia di modificarlo*. `/etc/hosts.allow` consente invece l'accesso a indirizzi IP specifici. È sufficiente aggiungere altri indirizzi IP in un elenco separato da virgole se si desidera consentire un numero maggiore di accessi.

Ad esempio:

```
sshd: 127.0.0.1, 192.128.23.1
```

### Aggiornamenti Automatici

Debian è anche impostata per aggiornarsi automaticamente, in modo da rimanere al passo con le più recenti patch di sicurezza.

Se per qualche motivo volessi cambiare questa impostazione (*non lo suggeriamo*), puoi fare così:

```
echo "unattended-upgrades unattended-upgrades/enable_auto_updates boolean false" | debconf-set-selections
```

*Per saperne di più su ciò che fa lo stackscript Bitcoin Standup, leggi [Appendice I: Capire Bitcoin Standup](A1_0_Capire_Bitcoin_Standup.md).*

## Giocare con Bitcoin

Quindi ora probabilmente vuoi giocare con Bitcoin!

Ma aspetta, il tuo demone Bitcoin probabilmente sta ancora scaricando i blocchi. Il comando `bitcoin-cli getblockcount` vi dirà l'avanzamento attuale:

```
$ bitcoin-cli getblockcount
1771352
```

Se è diverso ogni volta che si digita il comando, è necessario attendere prima di utilizzare Bitcoin. Attualmente sono necessarie da 1 a 6 ore per una configurazione  _pruned_, a seconda della vostra macchina.

Ma una volta che il numero si è stabilizzato, sei pronto a continuare!

Tuttavia, potrebbe essere il momento di bere qualche altro caffè. Ma presto il tuo sistema sarà pronto per l'uso e potrai iniziare a sperimentare.

## Riepilogo: Configurazione manuale di un VPS Bitcoin-Core

La creazione di un VPS Bitcoin-Core con gli script Standup ha reso l'intero processo rapido, semplice e (si spera) indolore.

## Cosa c'è Dopo?

Hai alcune opzioni per il prossimo passo:

* Leggi [StackScript](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/Scripts/LinodeStandUp.sh) per approfondire la tua configurazione.
* Leggi cosa fa lo StackScript nell' [Appendice I](A1_0_Capire_Bitcoin_Standup.md).
* Scegli una metodologia completamente diversa in [§2.2: Configurazione di una Macchina Bitcoin-Core Tramite Altri Metodi](02_2_Configurazione_di_un_Bitcoin-Core_Altro.md).
* Passa a "bitcoin-cli" con il [Capitolo Tre: Capire la Tua Configurazione Bitcoin](03_0_Capire_la_Tua_Configurazione_Bitcoin.md).

## Synopsis: Tipi di Installazione di Bitcoin

**_Mainnet_.** Questo scaricherà l'intera blockchain di Bitcoin. Si tratta di 450 GB di dati (che aumentano ogni giorno).

**_Pruned Mainnet_.** Questo ridurrà la blockchain che si sta memorizzando agli ultimi 550 blocchi. Se non state facendo mining o gestendo altri servizi Bitcoin, questo dovrebbe essere sufficiente per la convalida.

**_Testnet__.** Questo permette di accedere a una blockchain Bitcoin alternativa in cui i Bitcoin non hanno effettivamente valore. È destinato alla sperimentazione e ai test.

**_Pruned Testnet_.** Questi sono solo gli ultimi 550 blocchi di _Testnet_ ... perché anche la blockchain di _Testnet_ è piuttosto grande.

**Private Regtest_.** Questa è la modalità per i test di regressione, che consente di eseguire un server Bitcoin completamente locale. Consente di eseguire test ancora più approfonditi. Non c'è bisogno del _pruning_ in questo caso, perché si parte da zero. Si tratta di una configurazione molto diversa, ed è trattata nell' [Appendice 3](A3_0_Usare_Bitcoin_Regtest.md).