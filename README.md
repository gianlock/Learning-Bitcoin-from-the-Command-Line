# Imparare Bitcoin dalla Linea di Comando 2.2.0
### _di Christopher Allen e Shannon Appelcline_
### _tradotto da gianlock e_

![](https://www.blockchaincommons.com/images/projects/lbtc-screen.png)

Imparare Bitcoin dalla Linea di Comando è un tutorial per lavorare con Bitcoin (e Lightning) che insegna le interazioni dirette con i server stessi, così come i metodi più solidi e sicuri per iniziare a lavorare con questa criptovaluta.

> NOTA: Questa è una bozza in continuo progresso, così che possa ricevere qualche feedback dai primi utenti che la revisioneranno. Non è ancora pronta all'uso.

_Questo tutorial assume che tu abbia una qualche minima conoscenza di base su come utilizzare l'interfaccia a linea di comando. Se così non fosse, ci sono molti tutorial disponibili, e io ne ho uno per gli utenti Mac: https://github.com/ChristopherA/intro-mac-command-line._

## Traduzioni

* [Inglese](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line) — versione originale
* [Portuguese](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/tree/portuguese-translation/pt/README.md) — traduzione v2.0.1
* [Spanish](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/tree/spanish-translation/es/README.md) - traduzione v2.0.1

Se desideri fare la tua traduzione, per favore guarda [Contributing](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/tree/master#contributing), qui sotto.

## Tavola dei Contenuti

### PARTE UNO: PREPARARSI PER BITCOIN

**Stato:** Finito. Aggiornato per 0.20.

* [1.0: Introduzione alla Programmazione con Bitcoin Core e Lighnting](01_0_Introduzione.md)
    * [Intermezzo: Introduzione a Bitcoin](01_1_Introduzione_a_Bitcoin.md)
* [2.0: Configurazione di un Bitcoin-Core VPS](02_0_Configurazione_di_un_VPS_Bitcoin-Core.md)
  * [2.1: Configurazione di un VPS Bitcoin-Core con Bitcoin Standup](02_1_Configurazione_di_un_VPS_Bitcoin-Core_con_StackScript.md)
  * [2.2: Configurazione di una Macchina Bitcoin-Core Tramite Altri Metodi](02_2_Configurazione_di_un_Bitcoin-Core_Altro.md)

### PARTE DUE: UTILIZZO DI BITCOIN-CLI

**Status:** Finito. Aggiornato per 0.20.

* [3.0: Capire la Tua Configurazione Bitcoin](03_0_Capire_la_Tua_Configurazione_Bitcoin.md)
  * [3.1: Verificare la Tua Configurazione Bitcoin](03_1_Verificare_la_Tua_Configurazione_Bitcoin.md)
  * [3.2: Conoscere la Tua Configurazione Bitcoin](03_2_Conoscere_la_Tua_Configurazione_Bitcoin.md)
  * [3.3: Configurare il Tuo Wallet](03_3_Configurare_il_Tuo_Wallet.md)
    * [Intermezzo: Utilizzare Variabili della Linea di Comando](03_3__Intermezzo_Utilizzare_Variabili_Linea_di_Comando.md)
  * [3.4: Ricevere Una Transazione](03_4_Ricevere_una_Transazione.md)
  * [3.5: Capire il Descrittore](03_5_Capire_il_Descrittore.md)
* [4.0: Inviare Transazioni Bitcoin](04_0_Inviare_Transazioni_Bitcoin.md)
  * [4.1: Inviare Monete nel Modo Semplice](04_1_Inviare_Monete_Modo_Semplice.md)
  * [4.2: Creare una Transazione Grezza](04_2_Creare_una_Transaction_Grezza.md)
     * [Intermezzo: Usare JQ](04_2__Intermezzo_Usare_JQ.md)
  * [4.3: Creare una Transazione Grezza con Argomenti Denominati](04_3_Creare_una_Transazione_Grezza_con_Argomenti_Denominati.md)
  * [4.4: Inviare Monete con Transazioni Grezze](04_4_Inviare_Coins_con_una_Transazione_Grezza.md)
     * [Intermezzo: Usare Curl](04_4__Intermezzo_Usare_Curl.md)
  * [4.5: Inviare Monete con Transazioni Grezze Automatizzate](04_5_Inviare_Monete_con_Transazioni_Grezze_Automatizzate.md)
  * [4.6: Creare una Transazione Segwit](04_6_Creare_una_Transazione_Segwit.md)
* [5.0: Monitorare le Transazioni Bitcoin](05_0_Monitorare_le_Transazioni_Bitcoin.md)
  * [5.1 Monitorare le Transazioni Bloccate](05_1_Controllare_le_Tranzazioni_Bloccate.md)
  * [5.2: Reinviare una Transazione con RBF](05_2_Reinviare_una_Transazione_con_RBF.md)
  * [5.3: Coprire una Transazione con CPFP](05_3_Coprire_una_Transaction_con_CPFP.md)
* [6.0: Espandere le Transazioni Bitcoin con Multisigs](06_0_Ampliare_Transazioni_Bitcoin_Multisigs.md)
  * [6.1: Inviare una Transazione con un Multisig](06_1_Inviare_una_Transazione_con_Multisig.md)
  * [6.2: Spendere una Transazione con un Multisig](06_2_Spendere_una_Transazione_con_Multisig.md)
  * [6.3: Inviare & Spendere una Multisig Automatizzata](06_3_Inviare_una_Multisig_Automatizzata.md)
* [7.0: Espandere le Transazioni Bitcoin con PSBTs](07_0_Ampliare_Transazioni_Bitcoin_PSBTs.md)
  * [7.1: Creare una Transazione Bitcoin Parzialmente Firmata](07_1_Creare_una_Transazione_Bitcoin_Parzialmente_Firmata.md)
  * [7.2: Usare una Transazione Bitcoin Parzialmente Firmata](07_2_Usare_una_Transazione_Bitcoin_Parzialmente_Firmata.md)
  * [7.3: Integrazione con gli Hardware Wallets](07_3_Integrazione_con_Hardware_Wallets.md)
* [8.0: Espandere le Transazioni Bitcoin in Altri Modi](08_0_Ampliare_Transazioni_Bitcoin_Altro.md)
  * [8.1: Inviare una Transazione con un Locktime](08_1_Inviare_una_Transazione_con_Locktime.md)
  * [8.2: Inviare una Transazione con Dati](08_2_Inviare_una_Transazione_con_Dati.md)

### PARTE TRE: SCRIPT DI BITCOIN

**Stato:** Finito. Aggiornato per 0.20 e btcdeb.

* [9.0: Introduzione agli Script di Bitcoin](09_0_Introduzione_Script_Bitcoin.md)
  * [9.1: Capire le Basi delle Transazioni](09_1_Capire_le_Basi_delle_Transazioni.md)
  * [9.2: Eseguire uno Script Bitcoin](09_2_Eseguire_uno_Script_Bitcoin.md)
  * [9.3: Testare uno Script Bitcoin](09_3_Testare_uno_Script_Bitcoin.md)
  * [9.4: Script di un P2PKH](09_4_Script_di_P2PKH.md)
  * [9.5: Script di un P2WPKH](09_5_Script_di_P2WPKH.md)
* [10.0: Incorporare Script Bitcoin in Transazioni P2SH](10_0_Incorporare_Script_Bitcoin_in_Transazioni_P2SH.md)
  * [10.1: Capire le Basi del P2SH](10_1_Capire_le_Basi_del_P2SH.md)
  * [10.2: Costruire la Struttura del P2SH](10_2_Costruire_la_Struttura_del_P2SH.md)
  * [10.3: Eseguire uno Script Bitcoin con P2SH](10_3_Eseguire_uno_Script_Bitcoin_con_P2SH.md)
  * [10.4: Script di un Multisig](10_4_Script_di_Multisig.md)
  * [10.5: Scrivere uno Script Segwit](10_5_Scrivere_uno_Script_Segwit.md)
  * [10.6: Spendere una Transazione P2SH](10_6_Spendere_una_Transazione_P2SH.md)
* [11.0: Valorizzare il Timelock con gli Script Bitcoin](11_0_Valorizzare_Timelock_con_Script_Bitcoin.md)
  * [11.1: Capire le Opzioni del Timelock](11_1_Capire_Opzioni_Timelock.md)
  * [11.2: Usare CLTV negli Script](11_2_Usare_CLTV_negli_Script.md)
  * [11.3: Usare CSV negli Script](11_3_Usare_CSV_negli_Script.md)
* [12.0: Espandere gli Script di Bitcoin](12_0_Espandere_Script_Bitcoin.md)
  * [12.1: Usare i Condizionali di uno Script](12_1_Usare_Condizionali_Script.md)
  * [12.2: Usare Altri Comandi di uno Script](12_2_Usare_Altri_Comandi_Script.md)
* [13.0: Progettazione di Script Bitcoin Reali](13_0_Progettazione_Script_Bitcoin_Reali.md)
  * [13.1: Scrivere Puzzle Script](13_1_Scrivere_Puzzle_Script.md)
  * [13.2: Scrivere Script Multisig Complessi](13_2_Scrivere_Script_Multisig_Complessi.md)
  * [13.3: Espandere Bitcoin con gli Script](13_3_Espandere_Bitcoin_con_Script.md)

### PARTE QUATTRO: PRIVACY

**Stato:** Finito.

* [14.0: Usare Tor](14_0_Usare_Tor.md)
  * [14.1: Verificare la Tua Configurazione Tor](14_1_Verificare_Configurazione_Tor.md)
  * [14.2: Cambiare il Tuo Servizio Nascosto di Bitcoin](14_2_Cambiare_Servizio_Nascosto_Bitcoin.md)
  * [14.3: Aggiungere Servizi Nascosti SSH](14_3_Aggiungere_Servizi_Nascosti_SSH.md)

* [15.0: Usare i2p](15_0_Usare_i2p.md)
  * [15.1: Bitcoin Core come Servizio I2P (Invisible Internet Project)](15_1_Servizio_i2p.md)

### PARTE CINQUE: PROGRAMMAZIONE CON RPC

**Stato:** Finito.

* [16.0: Parlare con Bitcoind in C](16_0_Parlare_con_Bitcoind.md)
  * [16.1: Accedere a Bitcoind in C con Librerie RPC](16_1_Accedere_Bitcoind_con_C.md)
  * [16.2: Programmare Bitcoind in C con Librerie RPC](16_2_Programmare_Bitcoind_con_C.md)
  * [16.3: Ricevere Notifiche in C con Librerie ZMQ](16_3_Ricevere_Notifiche_Bitcoind_con_C.md)
* [17.0: Programmare Bitcoin con Libwally](17_0_Programmare_con_Libwally.md)
   * [17.1: Configurare Libwally](17_1_Configurare_Libwally.md)
   * [17.2: Usare BIP39 con Libwally](17_2_Usare_BIP39_con_Libwally.md)
   * [17.3: Usare BIP32 con Libwally](17_3_Usare_BIP32_con_Libwally.md)
   * [17.4: Usare PSBTs con Libwally](17_4_Usare_PSBTs_con_Libwally.md)
   * [17.5: Usare Script con Libwally](17_5_Usare_Script_con_Libwally.md)
   * [17.6: Usare Altre Funzioni con Libwally](17_6_Usare_Altre_Funzioni_con_Libwally.md)
   * [17.7: Integrare Libwally e Bitcoin-CLI](17_7_Integrare_Libwally_e_Bitcoin-CLI.md)
* [18.0: Parlare con Bitcoind in Altri Linguaggi](18_0_Parlare_con_Bitcoind_Altro.md)
  * [18.1: Accedere a Bitcoind in Go](18_1_Accedere_Bitcoind_in_Go.md)
  * [18.2: Accedere a Bitcoind in Java](18_2_Accedere_Bitcoind_in_Java.md)
  * [18.3: Accedere a Bitcoind in Node JS](18_3_Accedere_Bitcoind_in_NodeJS.md)
  * [18.4: Accedere a Bitcoind in Python](18_4_Accedere_Bitcoind_in_Python.md)
  * [18.5: Accedere a Bitcoind in Rust](18_5_Accedere_Bitcoind_in_Rust.md)
  * [18.6: Accedere a Bitcoind in Swift](18_6_Accedere_Bitcoind_in_Swift.md)

### PARTE SEI: USARE LIGHTNING-CLI

**Stato:** Finito.

* [19.0: Capire la Tua Configurazione Lightning](19_0_Capire_Configurazione_Lightning.md)
  * [19.1: Verificare la Tua Configurazione c-lightning](19_1_Verificare_Configurazione_Lightning.md)
  * [19.2: Conoscere la Tua Configurazione c-lightning](19_2_Conoscere_Configurazione_Lightning.md)
     * [Intermezzo: Accedere a un Second Nodo Lightning](19_2__Intermezzo_Accedere_a_Secondo_Nodo_Lightning.md)
  * [19.3: Creare un Canale Lightning](19_3_Creare_un_Canale.md)
* [20.0: Usare Lightning](20_0_Usare_Lightning.md)
  * [20.1: Generare una Rechiesta di Pagamento](20_1_Generare_Richiesta_Pagamento.md)
  * [20.2: Pagare una Invoice](20_2_Pagare_una_Invoice.md)
  * [20.3: Chiudere un Canale Lighnting Channel]((20_3_Chiudere_un_Canale.md))
  * [20.4: Espandere la Rete Lightning](20_4_Espandere_Rete_Lightning.md)

### APPENDICI

**Stato:** Finito.

* [Appendici](A0_Appendici.md)
  * [Appendice I: Capire Bitcoin Standup](A1_0_Capire_Bitcoin_Standup.md)
  * [Appendice II: Compilazione di Bitcoin dalla Sorgente](A2_0_Compilazione_Bitcoin_dalla_Sorgente.md)
  * [Appendice III: Usare Bitcoin Regtest](A3_0_Usare_Bitcoin_Regtest.md)

## Stato - Beta

v2.1.0 of **Imparare Bitcoin dalla Linea di Comando** è completo di tutte le funzionalità ed è stato completamente modificato e integrato. E' pronto per l'apprendimento.

Stiamo considerando cosa potremmo includere in una [v3.0](../TODO-30.md) odel corso. Se volessi supportare in qualche modo il lavoro, diventa un [GitHub Sponsor](https://github.com/sponsors/BlockchainCommons) o supportaci sul nostro [BTCPay Server](https://btcpay.blockchaincommons.com/), e facci sapere che il motivo è stato **Imparare Bitcoin**.

## Origine, Autori, Copyright & Licenze

Salvo diversa indicazione (che sia in questo [/README.md](./README.md) o nei commenti di testa del file) i contenuti di questo repository sono coperta da Copyright © 2020 della Blockchain Commons, LLC, sotto licenza [CC-BY](./LICENSE-CC-BY-4.0.md).

## Supporto Finanziario

*Imparare Bitcoin dalla Linea di Comando* è un progetto di [Blockchain Commons](https://www.blockchaincommons.com/). Siamo orgogliosamente una corporazione di utilità sociale "senza scopo di lucro" impegnati nell'open source e nello sviluppo libero. Il nostro lavoro si basa interamente sulle donazione e le partnership collaborative con persone come te. Ogni contributo sarà utilizzato per lo sviluppo di strumenti, tecnologie, e tecniche aperte a tutti che sosterranno e faranno avanzare le infrastrutture di sicurezza della blockchain e di internet e promuoveranno un web aperto.

Per supportare finanziariamente ulteriori sviluppi di *Imparare Bitcoin dalla Linea di Comando* e altri progetti, considera di diventare un mecenate di Blockchain Commons attraverso una donazione ricorrente mensile come [GitHub Sponsor](https://github.com/sponsors/BlockchainCommons). Puoi supportare Blockchain Commons con bitcoin sul nostro [BTCPay Server](https://btcpay.blockchaincommons.com/).

## Contribuzioni

Incoraggiamo contributi pubblici attraverso issue e pull request! Consulta [CONTRIBUIRE.md](./CONTRIBUIRE.md) per maggiori dettagli sul nostro processo di sviluppo. Tutti i contributi su questo repository richiedono un [Accordo di Licenza da Contributore](./CLA.md) firmato tramite GPG.

Se volessi tradurre Imparare Bitcoin in un'altra lingua, consulta in aggiunta [TRADUZIONE.md](./TRADUZIONE.md).

### Discussioni

Il miglior luogo per parlare di Blockchain Commons e i suoi progetti è nell nostra area GitHub _Discussions_.

[**Blockchain Commons Discussions**](https://github.com/BlockchainCommons/Community/discussions). Per sviluppatori, interni, e mecenati di Blockchain Commons, usate l'area di discussione della [repository _Community_](https://github.com/BlockchainCommons/Community) per parlare di questioni generali relative a Blockchain Commons , al programma interno, o argomenti diversi dal [Sistema Gordiano](https://github.com/BlockchainCommons/Gordian/discussions) o dagli [standard dei wallet](https://github.com/BlockchainCommons/AirgappedSigning/discussions), ciascuno dei quali ha la propria area di discussione.

### Altre Domande & Problemi

In quanto comunità open-source, open-development, Blockchain Commons non ha le risorse per fornire supporto diretto ai nostri progetti. Considerate l'area di discussione come un  luogo dove potreste trovare risposte alle vostre domande. In alternativa, usate le funzionalità di questa repository [issues](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/issues). Putroppo, non possiamo fare promesse sui tempi di risposta.

Se la tua società necessitasse di supporto per l'utilizzo dei nostri progetti, sentiti libero di contattarci direttamente per conoscere le opzioni. Potremmo essere in grado di offrirti un contratto per il supporto da parte di uno dei nostri contributori, o potremmo indirizzarti verso qualcuno che possa offrirti un contratto per il supporto di cui hai bisogno.

### Crediti

Le persone seguenti hanno contribuito direttamente a questa repository. Potete aggiungere il vostro nome qui partecipando. Il primo passo è leggere la documentazione per scoprire come [CONTRIBUIRE.md](./CONTRIBUIRE.md).


| Nome              | Ruolo                | Github                                            | Email                                 | Impronta Digitale GPG                                    |
| ----------------- | ------------------- | ------------------------------------------------- | ------------------------------------- | -------------------------------------------------- |
| Christopher Allen | Autore Principale | [@ChristopherA](https://github.com/ChristopherA) | \<ChristopherA@LifeWithAlacrity.com\> | FDFE 14A5 4ECB 30FC 5D22  74EF F8D3 6C91 3574 05ED |
| Shannon Appelcline |  Autore Principale | [@shannona](https://github.com/shannona) | \<shannon.appelcline@gmail.com\> | 7EC6 B928 606F 27AD |


Ulteriori contributori sono riportati sotto:

| Ruolo                | Nomi                                    |
| ------------------- | ---------------------------------------- |
| ***Contributori:*** | [gg2001](https://github.com/gg2001) (Sezioni Go, Node.js), [gorazdko](https://github.com/gorazdko) (sezione Rust), [Javier Vargas](https://github.com/javiervargas) (Sezioni C, Java, Lightning, Tor), [jodobear](https://github.com/jodobear) (Appendice: Compilare Bitcoin, sezione Python), [Prayank](    https://github.com/prayank23) (Sezioni i2p)                               |
| ***Revisori:***    | Glen Willem [@gwillem](https://github.com/gwillem) |
| ***Sponsor:***     | Blockstream Corporation                  |

### Crediti di Traduzione

Grazie ai volontari che trascorrono molto tempo a scrivere e revisionare le traduzioni in altre lingue del corso originale in inglese.

#### Traduzione Portoghese

| Nome              | Ruolo                | Github                                            | 
| ----------------- | ------------------- | ------------------------------------------------- | 
| Namcios | Traduttore & Revisore | [@namcios](https://github.com/namcios) | 
| Korea | Traduttore & Revisore | [@KoreaComK](https://github.com/KoreaComK) | 
| Luke Pavsky | Traduttore & Revisore | [@lukedevj](https://github.com/lukedevj) | 
| hgrams | Traduttore & Revisore | [@hgrams](https://github.com/hgrams) | 

#### Traduzione Spagnola

 Nome | Ruolo | GitHub |
| ---------- | -------- | ------------ |
| Ian Culp | Traduttore & Revisore | [@icculp](https://github.com/icculp) |
| Maxi Goyheneche | Traduttore | [@maxcrowar](https://github.com/maxcrowar) |
| Said Rahal | Traduttore | [@srahalh](https://github.com/srahalh) |
| César A. Vallero | Traduttore & Revisore | [@csralvall](https://github.com/csralvall) |
| Javier Vargas | Traduttore & Revisore | [@javiervargas](https://github.com/javiervargas) |

#### Traduzione Italiana

 Nome | Ruolo | GitHub |
| ---------- | -------- | ------------ |
| Gian | Traduttore & Revisore | [@gianlock](https://github.com/gianlock) |
| Brik | Traduttore & Revisore | [@enricobrik](https://github.com/enricobrik) |

## Divulgazione Responsabile

Vogliamo che tutti i nostri software siano sicuri per chiunque. Se hai scoperto una vulnerabilità di sicurezza, apprezziamo il vostro aiuto nel comunicarcelo in modo responsabile. Purtroppo, al momento non siamo in grado di offrire un'offerta di bug bounty.

Chiediamo la vostra massima fiducia e impegno a non divulgare informazioni o danneggiare alcun utente, i loro dati, o della nostra comunità di sviluppatori. Vi preghiamo di darci un periodo di tempo ragionevole per risolvere il problema e pubblicare la fix. Non frodate i nostri utenti o noi nel processo di scoperta. Promettiamo di non avanzare azioni legali contro ricercatori che evidenziano un problema, a patto che facciano del loro meglio per seguire queste linee guida.

### Riportare una Vulnerabilità

Vi preghiamo di segnalare casi sospetti di vulnerabilità di sicurezza in privato via mail a ChristopherA@BlockchainCommons.com (non usate questa mail per richieste di supporto). Vi preghiamo di NON creare issue visibili pubblicamente per casi di sospette vulnerabilità di sicurezza.

La seguente chiave può essere usata per comunicare informazioni sensibili agli sviluppatori:

| Nome| Impronta Digitale                                       |
| ----------------- | -------------------------------------------------- |
| Christopher Allen | FDFE 14A5 4ECB 30FC 5D22  74EF F8D3 6C91 3574 05ED |

Puoi importare una chiave eseguendo il seguente comando con l'impronta digitale sopra riportata: `gpg --recv-keys "<fingerprint>"`. Assicurati di inserire l'impronta digitale contenente gli spazi tra virgolette.
