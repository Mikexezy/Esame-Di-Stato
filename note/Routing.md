---
connections:
  - "[[Sistemi e Reti]]"
---


Il routing (instradamento) è una funzione del livello Network del modello TCP/IP. Viene svolta da un dispositivo di rete chiamato router (o sistema intermedio), che per ottimizzare il percorso dei pacchetti deve conoscere ed eventualmente aggiornare una serie di informazioni. Solo sulla base di queste informazioni il router può avviare il processo di forwarding, stabilendo verso quale linea inviare il pacchetto.

---

# Il Router

Un router è un dispositivo hardware dedicato a far comunicare reti differenti ed eterogenee, instradando i pacchetti nella giusta direzione. È connesso a due o più reti e decide il percorso che i dati devono seguire, basandosi sulle informazioni sullo stato delle reti collegate.

Le due attività fondamentali che svolge sono: la scelta del percorso migliore (routing) e l’invio dei pacchetti sull’interfaccia di uscita corretta (forwarding).

Un router, essendo un computer dedicato al routing, necessita di un sistema operativo. Dal punto di vista hardware deve avere almeno due schede di rete. Un router dotato di una scheda di rete verso la LAN e una verso la WAN può essere configurato come gateway, condividendo l’accesso a Internet per tutti i computer della rete locale. In questo caso, l’interfaccia del router che funge da gateway diventa la “via di uscita” degli host dalla LAN.

---

# Routing Table

È fondamentale che il router costruisca nella propria memoria cache una tabella di instradamento (routing table), che gli consenta di memorizzare le informazioni necessarie a identificare il percorso ottimale verso le reti remote. Questa tabella è una lista di tutte le reti raggiungibili, con informazioni sulle modalità di instradamento.

Quando il router esegue il forwarding di un pacchetto, consulta la routing table per cercare l’indirizzo di rete corrispondente all’IP di destinazione.

Ogni riga (entry) della tabella di routing contiene quattro campi:
- l'indirizzo IP della rete raggiungibile (network address),
- l’indirizzo del router successivo (next hop),
- l’interfaccia del router a cui inoltrare il pacchetto (interface),
- la metrica, cioè un valore che rappresenta il costo del percorso. Il router sceglierà il percorso con il costo minore.

---

# Routing Statico e Dinamico

Il funzionamento del router dipende da come viene creata la routing table. Se viene inserita manualmente dall’amministratore, si parla di routing statico, utilizzabile soprattutto in piccole reti. Se invece la tabella viene costruita automaticamente dal router in base alle informazioni ricevute tramite protocolli di routing, si parla di routing dinamico.

# Protocolli di Routing

La gran parte dei protocolli che regolano il routing dinamico al giorno d'oggi utilizzano questi algoritmi:
- Distance Vector Routing
- Link State Routing



# Distance Vector Routing

Il Distance Vector Routing è un algoritmo di routing usato dai router per trovare il percorso migliore verso le varie reti all’interno di una rete più grande

Ogni router mantiene una tabella di routing, dove annota:
- la distanza (in "hop", cioè il numero di router attraversati),
- e la direzione (cioè il router successivo) per raggiungere ogni rete.

Periodicamente, ogni router invia la propria tabella ai router vicini (i "vicini" sono quelli direttamente connessi). Quando un router riceve le tabelle dai vicini, confronta i percorsi e aggiorna la sua tabella se trova un percorso più breve.

Il Distance Vector Routing presenta diversi vantaggi. Prima di tutto, è un algoritmo semplice da implementare: ogni router ha bisogno solo di conoscere i suoi vicini e di scambiare con loro informazioni periodiche sulle distanze verso le varie reti. Questo lo rende adatto a reti di piccole dimensioni o con topologie stabili, dove le modifiche non sono frequenti. Inoltre, grazie alla sua bassa complessità, consuma poche risorse di calcolo e memoria, il che è vantaggioso per dispositivi con capacità limitate.

Tuttavia, ci sono anche alcuni svantaggi importanti. Uno dei principali è la lentezza nella convergenza: quando avviene un cambiamento nella rete, come il guasto di un collegamento, i router impiegano tempo per aggiornare le tabelle e trovare un nuovo percorso valido. Questo può portare a temporanei errori di instradamento. Un altro problema è il cosiddetto "count to infinity", dove i router continuano ad aumentare il numero di hop verso una destinazione irraggiungibile, senza accorgersi che il percorso non esiste più. Infine, il Distance Vector non ha una visione globale della rete, e questo lo rende meno efficiente in ambienti complessi o dinamici.

# Link State Routing

Il Link State Routing è un tipo di algoritmo di routing che, a differenza del Distance Vector, si basa su una visione completa della rete. Ogni router non si limita a scambiare informazioni con i vicini, ma raccoglie dati sulla topologia dell’intera rete e costruisce una mappa completa, che usa per calcolare il percorso più breve verso ogni destinazione.

Ogni router scopre i propri vicini diretti (link state) ed invia queste informazioni a tutti gli altri router della rete tramite messaggi chiamati LSA (Link State Advertisements). Una volta che ogni router ha ricevuto tutte le LSA, può costruire un grafo della rete e applicare un algoritmo, di solito Dijkstra, per trovare i percorsi ottimali.

Il Link State Routing offre numerosi vantaggi, soprattutto in reti complesse o dinamiche. Uno dei principali è la velocità di convergenza: quando avviene un cambiamento nella rete, come un guasto o l’aggiunta di un nuovo collegamento, i router si aggiornano molto rapidamente grazie alla diffusione delle informazioni tramite i pacchetti LSA. Inoltre, ogni router ha una visione completa della rete, quindi può calcolare i percorsi migliori in modo molto, questo permette una gestione più efficiente del traffico, riducendo il rischio di loop o percorsi sbagliati. Un altro punto a favore è la maggiore stabilità e affidabilità, soprattutto in ambienti di grandi dimensioni o soggetti a frequenti cambiamenti.

Tuttavia, ci sono anche alcuni svantaggi. Il primo è la maggiore complessità: i router devono essere in grado di gestire più dati e di eseguire calcoli più complessi, quindi servono più risorse di memoria e CPU. Anche la configurazione e la manutenzione del protocollo possono essere più impegnative rispetto ad algoritmi più semplici come il Distance Vector. Inoltre, durante la fase di avvio o in caso di cambiamenti, la quantità di traffico di aggiornamento generata dai pacchetti LSA può essere elevata, soprattutto in reti molto estese.

---

# Gli Autonomous System

Nei primi anni Ottanta, Internet era considerata un’unica rete in cui ogni router possedeva una tabella di instradamento con una voce per ogni rete raggiungibile e l’indirizzo del router da contattare. Questo modello centralizzato non era più sostenibile con la crescita della rete. Si decise quindi di suddividere Internet in più domini chiamati Autonomous System (AS), ciascuno costituito da un insieme di router e LAN organizzati secondo criteri topologici o amministrativi.

Ogni AS è identificato da un numero unico assegnato dall’IANA. I router che collegano diversi AS vengono spesso chiamati gateway, poiché svolgono il compito di inoltrare pacchetti da una rete verso l’esterno.

---

# Comunicazione In e Tra AS

All’interno di un AS, le informazioni di raggiungibilità vengono scambiate tramite uno o più protocolli adattivi, detti Interior Protocol. Gli AS tra loro si scambiano informazioni di raggiungibilità attraverso protocolli chiamati genericamente Exterior Protocol.

Se un router deve inoltrare un messaggio verso un altro router appartenente allo stesso AS, si parla di comunicazione tra Interior Router (IR), e nella sua tabella sarà presente l'informazione necessaria. Se invece il messaggio è destinato a un router in un altro AS, verrà inoltrato a una coppia di Exterior Router (ER), uno per ciascun AS coinvolto. Ogni ER conosce le reti raggiungibili tramite i link che lo collegano ad altri ER, ma non conosce la struttura interna degli AS esterni.

Gli accordi tra gestori di diversi AS per definire politiche di transito e raggiungibilità sono chiamati accordi di peering.

---

# Il Routing Gerarchico

Le tabelle di routing di grandi dimensioni possono causare seri problemi: saturano la memoria del router e rallentano le trasmissioni, costringendo la CPU a elaborazioni complesse per calcolare i percorsi ottimali. Inoltre, gli aggiornamenti frequenti delle routing table, dovuti ai continui scambi di informazioni tra numerosi router, aumentano il traffico di rete e riducono le prestazioni complessive.

Quando una rete diventa troppo grande e non è più possibile inserire tutte le destinazioni nelle tabelle dei router, è necessario riorganizzarla. In questi casi si adotta il principio del “divide et impera”. In pratica, invece di mantenere un’unica rete estesa, la si suddivide in più reti di dimensioni più contenute (dette regioni). All’interno di ciascuna regione, la comunicazione avviene secondo protocolli standard. Le connessioni tra regioni sono garantite da router dedicati che, a loro volta, comunicano tra loro come se facessero parte di una rete separata.

Questo approccio prende il nome di routing gerarchico. Secondo questo modello, la rete viene suddivisa in regioni interconnesse. Ogni router conosce in dettaglio solo la topologia della propria regione, ma non quella delle altre. Questo comporta un peggioramento delle prestazioni globali, poiché i percorsi non sono ottimizzati a livello interregionale.

---

# I Protocolli di Routing: Interior ed Exterior

### Interior Gateway Protocol (IGP)

I protocolli IGP sono utilizzati all’interno di un AS per regolare l’instradamento dei pacchetti. Sono chiamati protocolli intradominio. Possono essere classificati in base all’algoritmo che utilizzano:

- Distance Vector:
    - RIP (Routing Information Protocol): usa come metrica il numero di hop.
    - IGRP (Interior Gateway Routing Protocol): protocollo Cisco, supera i limiti di RIP supportando più metriche (banda, ritardo, carico, affidabilità).
    - EIGRP (Enhanced IGRP): sempre di Cisco, migliora IGRP pur mantenendone le metriche.
- Link State:
    - OSPF (Open Shortest Path First)
    - Integrated IS-IS (Intermediate System to Intermediate System): standard ISO e poi adottato anche da IETF.

### Exterior Gateway Protocol (EGP)

I protocolli EGP sono utilizzati tra diversi AS, per questo si definiscono protocolli extradominio. Il principale protocollo utilizzato su Internet è il BGP (Border Gateway Protocol), nella sua versione attuale BGP-4. BGP utilizza un algoritmo di tipo Path Vector, simile al Distance Vector, ma invece di contare semplicemente gli hop, costruisce un vettore contenente l’elenco degli AS da attraversare per raggiungere una destinazione.
