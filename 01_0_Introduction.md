# Capitolo Uno: Introduzione all'apprendimento di Bitcoin Core (e Linghtning) da riga di comando

## Introduzione

I metodi di pagamento per beni e servizi sono cambiati radicalmente negli ultimi decenni. Laddove una volta tutte le transazioni venivano effettuate tramite contanti o assegni, ora vari metodi di pagamento elettronico sono la norma. Tuttavia, la maggior parte di questi pagamenti elettronici avviene ancora attraverso sistemi centralizzati, dove società, banche o persino istituti finanziari basati su Internet come PayPal tengono lunghi elenchi di transazioni singolarmente correlate e hanno potere di censura sulle transazioni non gradite.

Questi rischi legati alla centralizzazione sono stati i catalizzatori alla base della creazione delle cryptovalute, la quale prima e più di successo è Bitcoin. Bitcoin offre anonimato, rende difficile correlare le transazioni e quasi impossibile la censura da parte di singole entità. Questi vantaggi lo hanno reso una delle valute in più rapida crescita al mondo. Questa crescita, a sua volta, ha creato un mercato attorno a Bitcoin dove sviluppatori e imprenditori creano nuovi servizi per la comunità Bitcoin.

Se sei uno di questi imprenditori o sviluppatori, questo corso fa al caso tuo, in quanto imparerai a programmare in Bitcoin. È un corso introduttivo che gradualmente ti spiegherà tutte le sfumature e caratteristiche di Bitcoin. Potrai inoltre studiare in maniera specifica come usare Bitcoin Core e c-lightining server usando le loro interfacce RPC (chiamata di procedura remota).

Perchè non usare una delle più complete librerie che si trovano nei vari linguaggi di programmazione? Perchè non creare la tua da zero? La risposta è che lavorare con le criptovalute può essere pericoloso. Non ci sono reti di salvataggio. Se accidentalmente paghi commissioni più alte del dovuto, crei una transazione invalida o commetti un qualsiasi numero di potenziali errori, le tue criptovalute saranno perse per sempre. Molta di questa responsabilità, in quanto programmatore, graverà giustamente sulle tue spalle, ma il rischio può essere minimizzato lavorando con le interfacce di criptovaluta più robuste e sicure in circolazione, quelle create dagli stessi team di programmazione cripto: ``bitcoind `` e ``lightningd``.

Gran parte di questo libro parla quindi di come utilizzare script Bitcoin (e Lightning) direttamente da linea di comando. Alcuni capitoli affronteranno temi più complicati con l'utilizzo di linguaggi di programmazzione, ma interagiranno direttamente con i programmi di ``bitcoind`` e ``lightningd`` utilizzando RPC o interagendo con i file che creano. Questo ti consentirà di imparare ad usare una tecnologia testata e solida che ti darà la confidenza necessaria per creare il tuo "Trusted System".

## Competenze richieste

Non è necessario essere particolarmente tecnici per la maggior parte di questo corso. Tutto ciò di cui hai bisogno è la dimistichezza nell'usare i comandi di base su riga di comando UNIX. Se hai familiarità con cose come `ssh`, `cd` e `ls`, il corso ti fornirà il resto.

Una piccola parte di questo corso richiede conoscienze di programmazione e dovresti saltare quelle sezioni se necessario, come discusso nella sezione successiva.

## Panoramica degli argomenti

Questo libro è diviso nelle seguenti lezioni:

| Parte | Descrizione | Competenze |
|-------|---------|---------|
| **Parte Uno: Preparsi per Bitcoin** | Capire le basi di Bitcoin e la configurazione di un server. | Linea di comando | 
| **Parte Due: Utilizzo di Bitcoin-CLI** | Usare Bitcoin-CLI per creare transazioni. | Linea di comando |
| **Parte Tre: Script di Bitcoin** | Espandere il tuo lavoro Bitcoin con gli script. | Concetti di programmazione |
| **Parte Quattro: Privacy** | Migliorare la sicurezza del tuo nodo con Tor | Linea di comando |
| **Parte Cinque: Programmazione con RPC** | Accesso a RPC da C e altri linguaggi. | Programmazione in C |
| **Parte Sei: Usare Lightning-CLI** | Utilizzo di Lightning-CLI per la creazione di transazioni. | Linea di comando |
| **Appendici** | Utilizzo di configurazioni Bitcoin meno comuni. | Linea di comando |

## Come utilizzare questo corso

Da dove puoi iniziare? Questo libro è pensato principalmente per essere letto in sequenza. Basta seguire il collegamento "Cosa c'è dopo?" alla fine di ogni sezione e/o fare clic sui collegamenti delle singole sezioni in ogni pagina del capitolo. L'apprendimento da questo corso sarà più efficace se ti costruirai effettivamente un server Bitcoin (come nel Capitolo 2) e poi eseguirai tutti gli esempi del libro: provare esempi è un'eccellente metodologia di apprendimento.

In base alle tue conoscenze potresti saltare diverse parti di questo libro:

* Se hai già un ambiente Bitcoin pronto per essere utilizzato, passa a [Capitolo 3: Capire la Tua Configurazione_Bitcoin](03_0_Capire_la_Tua_Configurazione_Bitcoin.md).
* Se ti interessa solo lo scripting di Bitcoin, vai a [Capitolo 9: Introduzione Script Bitcoin](09_0_Introduzione_Script_Bitcoin.md).
* Se vuoi informarti esclusivamente sull'uso dei linguaggi di programmazione, vai a [Capitolo 16: Parlare con Bitcoin](16_0_Parlare_con_Bitcoind.md).
* Se al contrario non vuoi fare alcuna programmazione, salta sicuramente i capitoli 15-17 e forse pure i capitoli 9-13. Il resto del corso dovrebbe comunque avere senso senza di loro.
* Se sei interessato solo a Lightning, vai a [Capitolo 19: Capire Configurazione Lightning.md](19_0_Capire_Configurazione_Lightning.md).
* Se vuoi leggere i principali nuovi contenuti aggiunti per la v2 del corso (2020), in seguito alla v1 (2017), leggi [§3.5: Capire il Descrittore](03_5_Capire_il_Descrittore.md), [§4.6: Creare una Trabsazione SegWit](04_6_Creare_una_Transazione_Segwit.md), [Capitolo 7: Ampliare Transazioni Bitcoin PSBTs](07_0_Ampliare_Transazioni_Bitcoin_PSBTs.md), [§9.5: Script di P2WPKH](09_5_Script_di_P2WPKH.md), [§10.5: Scrivere uno Script Segwit](10_5_Scrivere_uno_Script_Segwit.md), [Capitolo 14: Usare Tor](14_0_Usare_Tor.md), [Capitolo 15: Usare i2p](15_0_Usare_i2p.md), [Capitolo 16: Parlare con Bitcoind](16_0_Parlare_con_Bitcoind.md), [Capitolo 17: Programmare con Libwally](17_0_Programmare_con_Libwally.md), [Capitolo 18: Parlare con Bitcoin con altri Linguaggi di Programmazione](18_0_Parlare_con_Bitcoind_Altro.md), [Capitolo 19: Capire la tua configuraizone Lightning](19_0_Capire_Configurazione_Lightning.md), and [Chapter 20: Using Lightning](20_0_Using_Lightning.md).

* If you've already got a Bitcoin environment ready to be used, jump to [Chapter Three: Understanding Your Bitcoin Setup](03_0_Understanding_Your_Bitcoin_Setup.md).
* If you only care about Bitcoin scripting, jump to [Chapter Nine: Introducing Bitcoin Scripts](09_0_Introducing_Bitcoin_Scripts.md).
* If you just want to read about using programming languages, jump to [Chapter Sixteen: Talking to Bitcoin](16_0_Talking_to_Bitcoind.md).
* If you conversely don't want to do any programming, definitely skip chapters 15-17 while you're reading, and perhaps skip chapters 9-13. The rest of the course should still make sense without them.
* If you are only interested in Lightning, zap over to [Chapter Nineteen: Understanding Your Lightning Setup](19_0_Understanding_Your_Lightning_Setup.md).
* If you want to read the major new content added for v2 of the course (2020), following on v1 (2017), read [§3.5: Understanding the Descriptor](03_5_Understanding_the_Descriptor.md), [§4.6: Creating a SegWit Transaction](04_6_Creating_a_Segwit_Transaction.md), [Chapter 7: Expanding Bitcoin with PSBTs](07_0_Expanding_Bitcoin_Transactions_PSBTs.md), [§9.5: Scripting a P2WPKH](09_5_Scripting_a_P2WPKH.md), [§10.5: Scripting a SegWit Script](10_5_Scripting_a_Segwit_Script.md), [Chapter 14: Using Tor](14_0_Using_Tor.md), [Chapter 15: Using i2p](15_0_Using_i2p.md), [Chapter 16: Talking to Bitcoind with C](16_0_Talking_to_Bitcoind.md), [Chapter 17: Programming with Libwally](17_0_Programming_with_Libwally.md), [Chapter 18: Talking to Bitcoind with Other Languages](18_0_Talking_to_Bitcoind_Other.md), [Chapter 19: Understanding Your Lighting Setup](19_0_Understanding_Your_Lightning_Setup.md), and [Chapter 20: Using Lightning](20_0_Using_Lightning.md).

## Why to Use this Course

Obviously, you're working through this course because you're interested in Bitcoin. Besides imparting basic knowledge, it's also helped readers to join (or create) open-source projects and to get entry-level jobs in Bitcoin programming. A number of Blockchain Commons' interns learned about Bitcoin from this course, as have some members of our programming team.

## How to Support this Course

* Please use [Issues](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/issues) for any questions. Blockchain Commons does not have an active support team, and so we can't address individual problems or queries, but we will look over them in time, and use them to improve future iterations of the course.
* Please use [PRs](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/pulls) for any fixes of typos or incorrect (or changed) commands. For command-line or technical changes, it's very helpful if you also use the PR comments to explain why you did what you did, so that we don't have to research it.
* Please Use Our [Community discussions area](https://github.com/BlockchainCommons/Community/discussions) for talking about careers and skills. Blockchain Commons occasionally offers internships, as discussed in our Community repo.
* Please [become a patron](https://github.com/sponsors/BlockchainCommons) if you find this course helpful or if you want to help educate the next generation of blockchain programmers.

## What's Next?

If you'd like a basic introduction to Bitcoin, public-key cryptography, ECC, blockchains, and Lightning, read the [Introducing Bitcoin](01_1_Introducing_Bitcoin.md) interlude. 

Otherwise, if you're ready to dive into the course, go to [Setting Up a Bitcoin-Core VPS](02_0_Setting_Up_a_Bitcoin-Core_VPS.md).
