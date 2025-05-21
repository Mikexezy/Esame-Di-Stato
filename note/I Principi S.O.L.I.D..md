---
connections:
  - "[[TPSIT]]"
---
## Introduzione

I principi SOLID sono una raccolta di linee guida fondamentali per la progettazione orientata agli oggetti. L'acronimo deriva dalle iniziali dei cinque principi formulati da Robert C. Martin. Questi principi aiutano a sviluppare software comprensibile, flessibile e manutenibile.

## S - Single Responsibility Principle (principio di responsabilità singola)

Una classe deve avere una sola responsabilità, ovvero un solo motivo per essere modificata. In questo modo il codice diventa più leggibile e semplice da aggiornare o testare.

## O - Open/Closed Principle (principio aperto/chiuso)

Un modulo, una classe, una funzione deve essere aperto all'estensione ma chiuso alla modifica. Questo si ottiene introducendo un'astrazione. Il concetto è rendere il codice estendibile attraverso nuove classi o metodi senza alterare il codice già esistente.

## L - Liskov Substitution Principle (principio di sostituzione di Liskov)

Questo principio afferma che un oggetto di una classe derivata deve poter sostituire un oggetto della classe base senza alterare il funzionamento del programma. Si applica al polimorfismo e alla progettazione con classi e interfacce.

## I - Interface Segregation Principle (principio di segregazione delle interfacce)

Questo principio afferma che è meglio creare interfacce più piccole e specifiche piuttosto che una sola interfaccia grande. I client non devono essere costretti a implementare metodi che non usano.

## D - Dependency Inversion Principle (principio di inversione delle dipendenze)

Le classi ad alto livello non devono dipendere da classi a basso livello, ma entrambe devono dipendere da astrazioni. Le astrazioni non devono dipendere dai dettagli, ma i dettagli devono dipendere dalle astrazioni. Questo consente di separare le responsabilità e di cambiare le classi concrete senza modificare le classi che le usano.

## Conclusione

I principi SOLID offrono un modello efficace per progettare codice di qualità, ridurre la complessità e migliorare la manutenibilità. La loro applicazione porta vantaggi significativi nello sviluppo software, soprattutto su larga scala.