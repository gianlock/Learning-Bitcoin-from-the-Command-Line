# 2.2: Configurazione di una Macchina Bitcoin-Core Tramite Altri Metodi

La sezione precedente, [§2.1: Configurazione di un VPS Bitcoin-Core con Bitcoin Standup](02_1_Configurazione_di_un_VPS_Bitcoin-Core_con_StackScript.md), prevedeva la creazione di un _full node_ su un VPS utilizzando uno Stackscript di Linode. Tuttavia, è possibile creare un'istanza di Bitcoin-Core con la metodologia che si preferisce e seguendo i passaggi successivi di questo tutorial.

Di seguito sono riportate altre metodologie di configurazione di cui siamo a conoscenza:

* *[Compilazione dalla Sorgente](A2_0_Compilazione_Bitcoin_dalla_Sorgente.md).* Se preferisci compilare Bitcoin Core a mano, l'argomento è trattato nell'Appendice 2.
* *[Utilizzare GordianServer-macOS](https://github.com/BlockchainCommons/GordianServer-macOS).* Se avete un Mac moderno, potete usare l'applicazione *GordianNode* di Blockchain Commons, alimentata da *BitcoinStandup*, per installare un _full node_ sul vostro Mac.
* *[Utilizzare altri script Bitcoin Standup](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts).* Blockchain Commons offre anche una versione dello script Linode utilizzato che può essere eseguita dalla riga di comando su qualsiasi macchina Debian o Ubuntu. Questo può essere considerato lo script di punta, il che significa che è più probabile che presenti nuove funzioni, come l'installazione di Lightning.
* *[Configurare un nodo Bitcoin su AWS](https://wolfmcnally.com/115/developer-notes-setting-up-a-bitcoin-node-on-aws/).* @wolfmcnally ha scritto un tutorial completo per configurare Bitcoin-Core con Amazon Web Services (AWS).
* *[Configurare un nodo Bitcoin su un Raspberry Pi 3](https://medium.com/@meeDamian/bitcoin-full-node-on-rbp3-revised-88bb7c8ef1d1).* Damian Mee spiega come configurare un _headless full node_ su un Raspberry Pi 3.

Assicurati di installare su una versione aggiornata del vostro sistema operativo, per evitare problemi durante il processo di installazione. Al momento della stesura di questo documento, il corso è stato testato su Debian 11.

## Cosa c'è Dopo?

A meno che non si voglia tornare a una delle altre metodologie per la creazione di un nodo Bitcoin-Core:

   * Passa a "bitcoin-cli" con il [Capitolo Tre: Capire la Tua Configurazione Bitcoin](03_0_Capire_la_Tua_Configurazione_Bitcoin.md).
