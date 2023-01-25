# Capitolo Uno: Introduzione all'apprendimento di Bitcoin Core (e Linghtning) da riga di comando

## Introduzione

I metodi di pagamento per beni e servizi sono cambiati radicalmente negli ultimi decenni. Laddove una volta tutte le transazioni venivano effettuate tramite contanti o assegni, ora vari metodi di pagamento elettronico sono la norma. Tuttavia, la maggior parte di questi pagamenti elettronici avviene ancora attraverso sistemi centralizzati, dove società di carte di credito, banche o persino istituti finanziari basati su Internet come PayPal tengono lunghi elenchi di transazioni singolarmente correlati e hanno potere di censura sulle transazioni non gradite.

Questi rischi legati alla centralizzazione sono stati i catalizzatori alla base della creazione delle cryptovalute, la quale prima e più di successo è Bitcoin. Bitcoin offre anonimato, rende difficile correlare le transazioni e quasi impossibile la censura da parte di singole entità. Questi vantaggi lo hanno reso una delle valute in più rapida crescita al mondo. Questa crescita, a sua volta, ha reso Bitcoin una impresa tra sviluppatori e imprenditori, desiderosi di creare nuovi servizi per la comunità Bitcoin.

Se sei uno di questi imprenditori o sviluppatori, questo corso fa al caso tuo, in quanto imparerai a programmare in Bitcoin. È un corso introduttivo che gradualmente ti spiegherà tutte le sfumature e caratteristiche di Bitcoin. Potrai inoltre studiare in maniera specifica come usare Bitcoin Core e c-lightining server usando le loro interfacce RPC.

Ti starai chiedendo, perchè non usare una delle più complete librerie che si trovano nei vari linguaggi di programmazione? Perchè non creare la tua da zero? La risposta è perchè lavorare con le criptovalute può essere pericoloso. Non ci sono reti di salvataggio. Se accidentalmente paghi delle fee più del dovuto, crei una transazione invalida o commetti un qualsiasi numero di potenziali errori, le tue criptovalute saranno perse per sempre. Molta di questa responsabilità graverà giustamente sulle tue spalle in quanto programmatore, ma il rischio può essere minimizzato lavorando con le interfacce di crittovaluta più robuste e sicure in circolazione, quelle create dagli stessi team di programmazione cripto: ``bitcoind `` e ``lightningd``.

Much of this book thus discusses how to script Bitcoin (and Lightning) directly from the command line. Some later chapters deal with more sophisticated programming languages, but again they continue to interact directly with the ``bitcoind`` and ``lightningd`` daemons by using RPC or by interacting with the files they create. This allows you to stand on the shoulders of giants and use their trusted technology to learn how to create your own trusted systems.

## Required Skill Level

You do not need to be particularly technical for the majority of this course. All you need is the confidence to run basic commands on the UNIX command line. If you're familiar with things like `ssh`, `cd`, and `ls`, the course will supply you with the rest.

A minority of this course requires programming knowledge, and you should skip over those sections if needed, as discussed in the next section. 

## Overview of Topics

This book is broadly divided into the following sections:

| Part | Description | Skills |
|-------|---------|---------|
| **Part One: Preparing for Bitcoin** | Understanding the basics of Bitcoin and setting up a server for use. | Command Line | 
| **Part Two: Using Bitcoin-CLI** | Using the Bitcoin-CLI for creating transactions. | Command Line |
| **Part Three: Bitcoin Scripting** | Expanding your Bitcoin work with scripts. | Programming Concepts |
| **Part Four: Using Tor** | Improving your node security with Tor | Command Line |
| **Part Five: Programming with RPC** | Accessing RPC from C and other languages. | Programming in C |
| **Part Six: Using Lightning-CLI** | Using the Lightning-CLI for creating transactions. | Command Line |
| **Appendices** | Utilizing less common Bitcoin setups. | Command Line |

## How To Use This Course

So where do you start? This book is primarily intended to be read sequentially. Just follow the "What's Next?" Links at the end of each section and/or click through the individual section links on each chapter page. You'll achieve the best understanding from this course if you actually build yourself a Bitcoin server (per Chapter 2) and then run through all the examples over the course of the book: trying out examples is an excellent learning methodology.

If you have different levels of skill or want to learn different things, you might skip to different parts of the book:

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
