# Capitolo Uno: Introduzione all'apprendimento di Bitcoin Core (e Linghtning) da riga di comando

## Introduzione

I metodi di pagamento per beni e servizi sono cambiati radicalmente negli ultimi decenni. Laddove una volta tutte le transazioni venivano effettuate tramite contanti o assegni, ora vari metodi di pagamento elettronico sono la norma. Tuttavia, la maggior parte di questi pagamenti elettronici avviene ancora attraverso sistemi centralizzati, dove società, banche o persino istituti finanziari basati su Internet come PayPal tengono lunghi elenchi di transazioni singolarmente correlate e hanno potere di censura sulle transazioni non gradite.

Questi rischi legati alla centralizzazione sono stati i catalizzatori alla base della creazione delle criptovalute, la prima e più importante delle quali è Bitcoin. Bitcoin offre anonimato, rende difficile correlare le transazioni e quasi impossibile la censura da parte di singole entità. Questi vantaggi lo hanno reso una delle valute in più rapida crescita al mondo. Questa crescita, a sua volta, ha attratto imprenditori e sviluppatori da tutto il mondo, pronti a creare nuovi servizi per la comunità Bitcoin.

Se sei uno di questi imprenditori o sviluppatori, questo corso fa al caso tuo, in quanto imparerai a programmare in Bitcoin. È un corso introduttivo che gradualmente ti spiegherà tutte le sfumature e caratteristiche di Bitcoin. Potrai inoltre studiare in maniera specifica come usare Bitcoin Core e c-lightining server usando le loro interfacce RPC (Remote Procedure Call, Chiamata di procedura remota).

Perché non usare una delle più complete librerie che si trovano nei vari linguaggi di programmazione? Perché non creare la tua da zero? La risposta è che lavorare con le criptovalute può essere pericoloso. Non ci sono reti di salvataggio. Se accidentalmente paghi commissioni più alte del dovuto, crei una transazione invalida o commetti un qualsiasi numero di potenziali errori, le tue criptovalute saranno perse per sempre. Molta di questa responsabilità, in quanto programmatore, graverà giustamente sulle tue spalle, ma il rischio può essere minimizzato lavorando con le interfacce di criptovaluta più robuste e sicure in circolazione, quelle create dagli stessi team di programmazione cripto: ``bitcoind `` e ``lightningd``.

Gran parte di questo libro parla quindi di come utilizzare script Bitcoin (e Lightning) direttamente da linea di comando. Alcuni capitoli affronteranno temi più complicati con l'utilizzo di linguaggi di programmazione, ma interagiranno direttamente con i programmi di ``bitcoind`` e ``lightningd`` utilizzando RPC o interagendo con i file che creano. Questo ti consentirà di imparare ad usare una tecnologia testata e solida che ti darà la confidenza necessaria per creare il tuo "Trusted System".

## Competenze richieste

Non è necessario essere particolarmente tecnici per la maggior parte di questo corso. Tutto ciò di cui hai bisogno è la dimestichezza nell'usare i comandi di base su riga di comando UNIX. Se hai familiarità con cose come `ssh`, `cd` e `ls`, il corso ti fornirà il resto.

Una piccola parte di questo corso richiede conoscenze di programmazione e dovresti saltare quelle sezioni se necessario, come discusso nella sezione successiva.

## Panoramica degli argomenti

Questo libro è diviso nelle seguenti lezioni:

| Parte | Descrizione | Competenze |
|-------|---------|---------|
| **Parte Uno: Prepararsi per Bitcoin** | Capire le basi di Bitcoin e la configurazione di un server. | Linea di comando | 
| **Parte Due: Utilizzo di Bitcoin-CLI** | Usare Bitcoin-CLI per creare transazioni. | Linea di comando |
| **Parte Tre: Script di Bitcoin** | Espandere il tuo lavoro Bitcoin con gli script. | Concetti di programmazione |
| **Parte Quattro: Privacy** | Migliorare la sicurezza del tuo nodo con Tor | Linea di comando |
| **Parte Cinque: Programmazione con RPC** | Accesso a RPC da C e altri linguaggi. | Programmazione in C |
| **Parte Sei: Usare Lightning-CLI** | Utilizzo di Lightning-CLI per la creazione di transazioni. | Linea di comando |
| **Appendici** | Utilizzo di configurazioni Bitcoin meno comuni. | Linea di comando |

## Come utilizzare questo corso

Da dove puoi iniziare? Questo libro è pensato principalmente per essere letto in sequenza. Basta seguire il collegamento "Cosa c'è dopo?" alla fine di ogni sezione e/o fare clic sui collegamenti delle singole sezioni in ogni pagina del capitolo. L'apprendimento da questo corso sarà più efficace se ti costruirai effettivamente un server Bitcoin (come nel Capitolo 2) e poi eseguirai tutti gli esempi del libro: provare esempi è un'eccellente metodologia di apprendimento.

In base alle tue conoscenze potresti saltare diverse parti di questo libro:

* Se hai già un ambiente Bitcoin pronto da utilizzare, passa a [Capitolo 3: Capire la Tua Configurazione Bitcoin](03_0_Capire_la_Tua_Configurazione_Bitcoin.md).
* Se ti interessa solo lo scripting di Bitcoin, vai a [Capitolo 9: Introduzione agli Script Bitcoin](09_0_Introduzione_Script_Bitcoin.md).
* Se vuoi informarti esclusivamente sull'uso dei linguaggi di programmazione, vai a [Capitolo 16: Parlare con Bitcoind](16_0_Parlare_con_Bitcoind.md).
* Se al contrario non vuoi fare alcuna programmazione, salta sicuramente i capitoli 15-17 e forse pure i capitoli 9-13. Il resto del corso dovrebbe comunque avere senso senza di loro.
* Se sei interessato solo a Lightning, vai a [Capitolo 19: Capire la tua Configurazione Lightning.md](19_0_Capire_Configurazione_Lightning.md).
* Se vuoi leggere i principali nuovi contenuti aggiunti per la v2 del corso (2020), in seguito alla v1 (2017), leggi [§3.5: Capire il Descrittore](03_5_Capire_il_Descrittore.md), [§4.6: Creare una Transazione SegWit](04_6_Creare_una_Transazione_Segwit.md), [Capitolo 7: Espandere le Transazioni Bitcoin PSBTs](07_0_Ampliare_Transazioni_Bitcoin_PSBTs.md), [§9.5: Script di un P2WPKH](09_5_Script_di_P2WPKH.md), [§10.5: Scrivere uno Script Segwit](10_5_Scrivere_uno_Script_Segwit.md), [Capitolo 14: Usare Tor](14_0_Usare_Tor.md), [Capitolo 15: Usare i2p](15_0_Usare_i2p.md), [Capitolo 16: Parlare con Bitcoind in C](16_0_Parlare_con_Bitcoind.md), [Capitolo 17: Programmare Bitcoin con Libwally](17_0_Programmare_con_Libwally.md), [Capitolo 18: Parlare con Bitcoind in Altri Linguaggi](18_0_Parlare_con_Bitcoind_Altro.md), [Capitolo 19: Capire la tua configurazione Lightning](19_0_Capire_Configurazione_Lightning.md) e [Capitolo 20: Usare Lightning](20_0_Usare_Lightning.md).

## Perché seguire questo corso

Ovviamente, stai seguendo questo corso perché sei interessato a Bitcoin. Oltre ad acquisire conoscenze di base, questo corso ha anche aiutato i lettori a creare progetti open source e a ottenere lavori di livello base nella programmazione Bitcoin. Un certo numero di stagisti di Blockchain Commons ha imparato a conoscere Bitcoin da questo corso, così come alcuni membri del nostro team di programmazione.

## Come supportare questo corso

* Si prega di utilizzare [Issues](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/issues) per ogni domanda. Blockchain Commons non ha un team di supporto attivo, quindi non possiamo affrontare singoli problemi o domande, ma li esamineremo in tempo e li utilizzeremo per migliorare le future iterazioni del corso.
* Usate [PRs](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/pulls) per eventuali correzioni di errori di battitura o comandi errati/modificati. Per modifiche su argomenti tecnici o riga di comando, è molto utile utilizzare i commenti PR per spiegare le motivazioni, in modo da non doverlo ricercare.
* Usate [Community discussions area](https://github.com/BlockchainCommons/Community/discussions) per parlare di competenze e carriera. Blockchain Commons offre occasionalmente stage, come discusso nel nostro repository della community.
* Per favore [diventa un patreon](https://github.com/sponsors/BlockchainCommons) se trovi utile questo corso o se vuoi aiutare a educare la prossima generazione di programmatori blockchain.

## Cosa c'è dopo?

Se desideri un'introduzione di base a Bitcoin, crittografia a chiave pubblica, ECC, blockchain e Lightning, leggi l'intermezzo [Introduzione a Bitcoin](01_1_Introduzione_a_Bitcoin.md). 

In alternativa, se sei pronto per immergerti nel corso, vai a [Configurazione di un VPS Bitcoin-Core](02_0_Configurazione_di_un_Bitcoin-Core_VPS.md).
