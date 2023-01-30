# Capitolo Due: Creazione di un VPS Bitcoin-Core

Per iniziare a usare Bitcoin, è necessario prima di tutto configurare una macchina che esegua Bitcoin. Gli articoli in questo capitolo descrivono come fare, principalmente utilizzando un VPS (Serve Privato Virtuale).

## Obiettivi di questo capitolo

Dopo aver affrontato questo capitolo, uno sviluppatore sarà in grado di:

* Dicirete tra i cinque principali tipi di nodi Bitcoin
* Creare un nodo Bitcoin per lo sviluppo
* Creare un'istanza locale della Blockchain di Bitcoin

Gli obiettivi di supporto includono la capacità di:

* Comprendere la configurazione di base della rete del VPS
* Decidere quali priorità di sicurezza implementare
* Comprendere le differenze tra nodi *pruned* e *unpruned*
* Comprendere le differenze tra nodi Mainnet, Testnet e Regtest
* Interpretare le basi del file di configurazione di Bitcoin

## Tavola dei Contenuti

Non è necessario leggere l'intero capitolo. Decidi se vuoi eseguire uno StackScript per configurare un nodo su un VPS Linode (§2.2); o se vuoi configurarlo su un ambiente differente, come una macchina AWS o un Mac (§2.3). Quindi, salta alla sezione corrispondente. Informazioni aggiuntive sulla nostra configurazione consigliata le puoi trovare in [Appendice I](A1_0_Capire_Bitcoin_Standup.md).

* [Sezione Uno: Configurazione di un VPS Bitcoin-Core con Bitcoin Standup](02_1_Configurazione_di_un_VPS_Bitcoin-Core_con_StackScript.md)
* [Sezione Due: Configurazione di una Macchina Bitcoin-Core Tramite Altri Metodi](02_2_Configurazione_di_un_Bitcoin-Core_Altro.md)