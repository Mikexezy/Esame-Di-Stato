#moc

# Indice
```dataview
list from [[]]
```
---

# Routing


Il routing (instradamento) è una funzione del livello Network del modello TCP/IP. Viene svolta da un dispositivo di rete chiamato **router** (o sistema intermedio), che per ottimizzare il percorso dei pacchetti deve conoscere ed eventualmente aggiornare una serie di informazioni. Solo sulla base di queste informazioni il router può avviare il processo di **forwarding**, stabilendo verso quale linea inviare il pacchetto.

---

*Il Router*
Un router è un dispositivo hardware dedicato a far comunicare reti differenti ed eterogenee, instradando i pacchetti nella giusta direzione. È connesso a due o più reti e decide il percorso che i dati devono seguire, basandosi sulle informazioni sullo stato delle reti collegate.

La funzione principale del router è quella di reindirizzare i messaggi tra reti di computer affinché possano raggiungere la destinazione finale. Le due attività fondamentali che svolge sono: la scelta del percorso migliore (routing) e l’invio dei pacchetti sull’interfaccia di uscita corretta (forwarding).

Un router, essendo un computer dedicato al routing, necessita di un sistema operativo. Dal punto di vista hardware deve avere almeno due schede di rete. Un router dotato di una scheda di rete verso la LAN e una verso la WAN può essere configurato come **gateway**, condividendo l’accesso a Internet per tutti i computer della rete locale. In questo caso, l’interfaccia del router che funge da gateway diventa la “via di uscita” degli host dalla LAN.

---

*Routing Table*
È fondamentale che il router costruisca nella propria memoria cache una **tabella di instradamento** (routing table), che gli consenta di memorizzare le informazioni necessarie a identificare il percorso ottimale verso le reti remote. Questa tabella è una lista di tutte le reti raggiungibili, con informazioni sulle modalità di instradamento.

Quando il router esegue il forwarding di un pacchetto, consulta la routing table per cercare l’indirizzo di rete corrispondente all’IP di destinazione.

Ogni riga (entry) della tabella di routing contiene quattro campi:
- l'indirizzo IP della rete raggiungibile (network address),
- l’indirizzo del router successivo (next hop),
- l’interfaccia del router a cui inoltrare il pacchetto (interface),
- la metrica, cioè un valore che rappresenta il costo del percorso. Il router sceglierà il percorso con il costo minore.

---

*Routing Statico e Dinamico*
Il funzionamento del router dipende da come viene creata la routing table. Se viene inserita manualmente dall’amministratore, si parla di routing statico, utilizzabile soprattutto in piccole reti. Se invece la tabella viene costruita automaticamente dal router in base alle informazioni ricevute tramite protocolli di routing, si parla di routing dinamico.

---

*Protocolli di Routing*
La gran parte dei protocolli che regolano il routing dinamico al giorno d'oggi utilizzano questi algoritmi:
- Distance Vector Routing;
- Link State Routing;


# Distance Vector Routing

Il Distance Vector Routing è un algoritmo di routing usato dai router per trovare il percorso migliore verso le varie reti all’interno di una rete più grande

Ogni router **mantiene una tabella di routing**, dove annota:
  
- la **distanza** (in "hop", cioè il numero di router attraversati),

- e la **direzione** (cioè il router successivo) per raggiungere ogni rete.

Periodicamente, **ogni router invia la propria tabella ai router vicini** (i "vicini" sono quelli direttamente connessi). Quando un router riceve le tabelle dai vicini, **confronta i percorsi** e aggiorna la sua tabella se trova un percorso più breve.

Il **Distance Vector Routing** presenta diversi **vantaggi**. Prima di tutto, è un algoritmo **semplice da implementare**: ogni router ha bisogno solo di conoscere i suoi vicini e di scambiare con loro informazioni periodiche sulle distanze verso le varie reti. Questo lo rende adatto a reti **di piccole dimensioni** o con **topologie stabili**, dove le modifiche non sono frequenti. Inoltre, grazie alla sua **bassa complessità**, consuma **poche risorse di calcolo e memoria**, il che è vantaggioso per dispositivi con capacità limitate.

Tuttavia, ci sono anche alcuni **svantaggi** importanti. Uno dei principali è la **lentezza nella convergenza**: quando avviene un cambiamento nella rete, come il guasto di un collegamento, i router impiegano **tempo per aggiornare le tabelle** e trovare un nuovo percorso valido. Questo può portare a **temporanei errori di instradamento**. Un altro problema è il cosiddetto **"count to infinity"**, dove i router continuano ad aumentare il numero di hop verso una destinazione irraggiungibile, senza accorgersi che il percorso non esiste più. Infine, il Distance Vector non ha una visione globale della rete, e questo lo rende **meno efficiente** in ambienti complessi o dinamici


# Link State Routing

Il **Link State Routing** è un tipo di algoritmo di routing che, a differenza del Distance Vector, si basa su una **visione completa della rete**. Ogni router non si limita a scambiare informazioni con i vicini, ma **raccoglie dati sulla topologia dell’intera rete** e costruisce una **mappa completa**, che usa per calcolare il percorso più breve verso ogni destinazione.

Ogni router Scopre i propri vicini diretti (link state) ed invia queste informazioni a **tutti gli altri router** della rete tramite messaggi chiamati **LSA (Link State Advertisements)**. Una volta che ogni router ha ricevuto tutte le LSA, può costruire un **grafo della rete** e applicare un algoritmo, di solito **Dijkstra**, per trovare i percorsi ottimali.

Il **Link State Routing** offre numerosi **vantaggi**, soprattutto in reti complesse o dinamiche. Uno dei principali è la **velocità di convergenza**: quando avviene un cambiamento nella rete, come un guasto o l’aggiunta di un nuovo collegamento, i router si aggiornano molto rapidamente grazie alla diffusione delle informazioni tramite i **pacchetti LSA**. Inoltre, ogni router ha una **visione completa della rete**, quindi può calcolare i percorsi migliori in modo molto, questo permette una **gestione più efficiente del traffico**, riducendo il rischio di loop o percorsi sbagliati. Un altro punto a favore è la **maggiore stabilità e affidabilità**, soprattutto in ambienti di grandi dimensioni o soggetti a frequenti cambiamenti.

Tuttavia, ci sono anche alcuni **svantaggi**. Il primo è la **maggiore complessità**: i router devono essere in grado di gestire più dati e di eseguire calcoli più complessi, quindi servono **più risorse di memoria e CPU**. Anche la **configurazione e la manutenzione** del protocollo possono essere più impegnative rispetto ad algoritmi più semplici come il Distance Vector. Inoltre, durante la fase di avvio o in caso di cambiamenti, la **quantità di traffico di aggiornamento** generata dai pacchetti LSA può essere elevata, soprattutto in reti molto estese.

---
*Gli Autonomous System*
Nei primi anni Ottanta, Internet era considerata un’unica rete in cui ogni router possedeva una tabella di instradamento con una voce per ogni rete raggiungibile e l’indirizzo del router da contattare. Questo modello centralizzato non era più sostenibile con la crescita della rete. Si decise quindi di suddividere Internet in più domini chiamati **Autonomous System (AS)**, ciascuno costituito da un insieme di router e LAN organizzati secondo criteri topologici o amministrativi.

Ogni AS è identificato da un numero unico assegnato dall’IANA. I router che collegano diversi AS vengono spesso chiamati **gateway**, poiché svolgono il compito di inoltrare pacchetti da una rete verso l’esterno.

---

*Comunicazione In e Tra AS*
All’interno di un AS, le informazioni di raggiungibilità vengono scambiate tramite uno o più protocolli adattivi, detti **Interior Protocol**. Gli AS tra loro si scambiano informazioni di raggiungibilità attraverso protocolli chiamati genericamente **Exterior Protocol**.

Se un router deve inoltrare un messaggio verso un altro router appartenente allo stesso AS, si parla di comunicazione tra **Interior Router (IR)**, e nella sua tabella sarà presente l'informazione necessaria. Se invece il messaggio è destinato a un router in un altro AS, verrà inoltrato a una coppia di **Exterior Router (ER)**, uno per ciascun AS coinvolto. Ogni ER conosce le reti raggiungibili tramite i link che lo collegano ad altri ER, ma non conosce la struttura interna degli AS esterni.

Gli accordi tra gestori di diversi AS per definire politiche di transito e raggiungibilità sono chiamati **accordi di peering**.

---

*Il Routing Gerarchico*
Le tabelle di routing di grandi dimensioni possono causare seri problemi: saturano la memoria del router e rallentano le trasmissioni, costringendo la CPU a elaborazioni complesse per calcolare i percorsi ottimali. Inoltre, gli aggiornamenti frequenti delle routing table, dovuti ai continui scambi di informazioni tra numerosi router, aumentano il traffico di rete e riducono le prestazioni complessive.

Quando una rete diventa troppo grande e non è più possibile inserire tutte le destinazioni nelle tabelle dei router, è necessario riorganizzarla. In questi casi si adotta il principio del “divide et impera”. In pratica, invece di mantenere un’unica rete estesa, la si suddivide in più reti di dimensioni più contenute (dette regioni). All’interno di ciascuna regione, la comunicazione avviene secondo protocolli standard. Le connessioni tra regioni sono garantite da router dedicati che, a loro volta, comunicano tra loro come se facessero parte di una rete separata.

Questo approccio prende il nome di **routing gerarchico**. Secondo questo modello, la rete viene suddivisa in regioni interconnesse. Ogni router conosce in dettaglio solo la topologia della propria regione, ma non quella delle altre. Questo comporta un peggioramento delle prestazioni globali, poiché i percorsi non sono ottimizzati a livello interregionale.

---

*I Protocolli di Routing: Interior ed Exterior*
###### Interior Gateway Protocol (IGP)

I protocolli IGP sono utilizzati **all’interno** di un AS per regolare l’instradamento dei pacchetti. Sono chiamati protocolli **intradominio**. Possono essere classificati in base all’algoritmo che utilizzano:

- Distance Vector:
    
    - **RIP** (Routing Information Protocol): usa come metrica il numero di hop.
        
    - **IGRP** (Interior Gateway Routing Protocol): protocollo Cisco, supera i limiti di RIP supportando più metriche (banda, ritardo, carico, affidabilità).
        
    - **EIGRP** (Enhanced IGRP): sempre di Cisco, migliora IGRP pur mantenendone le metriche.
        
- Link State:
    
    - **OSPF (Open Shortest Path First)**.
        
    - **Integrated IS-IS (Intermediate System to Intermediate System)**: standard ISO e poi adottato anche da IETF.
        

###### Exterior Gateway Protocol (EGP)

I protocolli EGP sono utilizzati **tra diversi AS**, per questo si definiscono protocolli **extradominio**. Il principale protocollo utilizzato su Internet è il **BGP (Border Gateway Protocol)**, nella sua versione attuale **BGP-4**. BGP utilizza un algoritmo di tipo **Path Vector**, simile al Distance Vector, ma invece di contare semplicemente gli hop, costruisce un vettore contenente l’elenco degli AS da attraversare per raggiungere una destinazione.

---

# Transport Layer



Lo stack TCP/IP è composto da quattro livelli. È stato sviluppato prima della definizione del modello OSI, che avrebbe dovuto sostituirlo, ma con il tempo si è imposto come lo standard de facto, specialmente su Internet. 

I due protocolli principali della suite TCP/IP sono IP (Internet Protocol), che opera al livello rete, e TCP (Transmission Control Protocol), che appartiene al livello trasporto. Quest'ultimo è responsabile della comunicazione end-to-end tra processi che si trovano su host differenti.

---

*Servizi del Livello Trasporto*  
Il livello di trasporto consente a due processi su host diversi di comunicare direttamente. Questo livello offre un controllo completo end-to-end. Un protocollo di trasporto può gestire più connessioni simultanee verso lo stesso host, distinguendo a quale processo inviare ciascun messaggio grazie a meccanismi basati su porte e socket.

---

*Le Porte e le Socket*
Poiché su un host possono essere attivi più processi che generano richieste, è necessario un sistema per identificare correttamente il destinatario di ogni pacchetto. Per questo vengono utilizzate le porte, numeri a 16 bit assegnati dall'IANA.

Le porte sono suddivise in tre categorie:

- Well Known Ports: da 0 a 1023
    
- Registered Ports: da 1024 a 49151
    
- Dynamic/Private Ports: da 49152 a 65535
    

Ogni connessione è identificata da una quintupla formata da: protocollo, indirizzo IP del client, indirizzo IP del server, numero di porta del client, numero di porta del server. Questa struttura è detta association. La parte locale dell’associazione (protocollo, IP e porta) è chiamata socket. Le socket permettono di distinguere le comunicazioni tra diversi processi su uno stesso host.

---

*Multiplexing e Demultiplexing* 
Tutti i protocolli del livello trasporto forniscono funzionalità di multiplexing e demultiplexing. Il multiplexing consiste nel raccogliere dati da diverse applicazioni, aggiungere un header e inviarli al livello rete. Il demultiplexing è il processo inverso: ricevere un segmento, esaminarne l’header e consegnare i dati al processo corretto.

---

*I Principali Protocolli di Trasporto*  
I protocolli più usati in questo livello sono UDP (User Datagram Protocol) e TCP (Transmission Control Protocol). Le unità dati per questi protocolli sono rispettivamente il datagramma (TPDU per UDP) e il segmento (TPDU per TCP).

---

*TCP*  
Il TCP è il protocollo più diffuso per il livello trasporto. È connection-oriented e affidabile, ed è utilizzato da applicazioni che necessitano di una trasmissione sicura, come FTP (trasferimento file), SMTP (posta elettronica) e HTTP (pagine web).

Il Segment TCP è composto da un header (20 byte) con al suo interno:

- Numero porta sorgente;
    
- Numero porta destinazione;
    
- Sequenza di numeri;
    
- Acknowledgement number;
    
- Lunghezza header;
    
- checksum, window size;
    
- urgent pointer;
    

Poi troviamo il parametro options e data.

---

*Instaurazione e Abbattimento Sessione TCP*

### Instaurazione di una Connessione TCP – Three-Way Handshake

Affinché possa essere instaurata una connessione TCP tra due host, è necessario che l'host ricevente acconsenta mediante una sequenza composta da tre fasi, nota come Three-Way Handshake:

1. Host 1 invia un segmento TCP con il flag SYN impostato a 1. Viene inoltre generato un numero di sequenza iniziale (sequence number) scelto in modo casuale, indicato con X.
    
2. Host 2, se accetta di stabilire la connessione, risponde con un segmento in cui:
    
    - il flag SYN è impostato a 1 (per iniziare la comunicazione nella direzione opposta),
        
    - il flag ACK è impostato a 1 (per confermare la ricezione),
        
    - l'Ack Number è posto a X + 1 (per confermare il numero di sequenza ricevuto da Host 1),
        
    - viene generato un nuovo numero di sequenza Y, scelto in modo casuale.
        
3. Host 1 risponde con un segmento contenente:
    
    - flag ACK impostato a 1,
        
    - l'Ack Number impostato a Y + 1.
        

A questo punto la connessione è considerata stabilita e si può procedere con la trasmissione dei dati.

### Trasferimento Dati: Affidabilità e Controlli

Durante la fase di trasmissione:

- TCP garantisce una trasmissione affidabile e ordinata dei dati;
    
- sono attivi meccanismi di controllo degli errori, controllo del flusso (flow control) e controllo della congestione (congestion control);
    
- ogni segmento ricevuto viene confermato (ACK) e i numeri di sequenza aiutano a mantenere l'ordine dei dati ed evitare duplicazioni o perdite;
    

### Chiusura della Connessione TCP – Double-Way Handshake

Poiché la connessione TCP è bidirezionale, la chiusura avviene in maniera indipendente per ciascuna direzione. La procedura di chiusura prende il nome di Double-Way Handshake (stretta di mano doppia a due vie), che si compone di quattro fasi:

1. Un host (es. Host 1) invia un segmento TCP con il flag FIN impostato a 1 per indicare la volontà di terminare la trasmissione dal proprio lato.
    
2. Host 2 risponde immediatamente con un segmento contenente:
    
    - flag ACK = 1,
        
    - l'Ack Number = X + 1, dove X è il numero di sequenza del FIN ricevuto.
        
3. Se Host 2 ha ancora dati da trasmettere, continua a farlo. Quando anche lui ha terminato, invia un segmento con FIN = 1 e proprio numero di sequenza Y. Questo passo è suddiviso in due segmenti distinti (ACK e poi FIN) per permettere la chiusura asincrona.
    
4. Infine, Host 1 conferma con ACK = 1 e Ack Number = Y + 1.
    

---

*Controllo della Congestione in TCP*  
Per individuare una congestione il TCP utilizza dei timer per misurare il tempo trascorso tra l'invio di un segmento e la ricezione del relativo ack. Se questo non arriva entro un determinato quantitativo di tempo si genera un timeout.

TCP ipotizza che la perdita di dati sia per una congestione della rete e agisce di conseguenza, anche se negli ultimi anni sono nate delle versioni di TCP che implementano la possibilità che la perdita di dati sia causata da errori di trasmissione, e quindi intervengono cercando di mantenere le prestazioni di trasmissione alte.

TCP implementa una serie di algoritmi, specificati nella RFC 5681, per il controllo della congestione. Tutti fanno però uso della finestra di congestione, che indica al mittente il massimo numero di byte non riscontrati che si possono ritrovare ancora nella rete. In particolare vale quanto segue:

```
maxWindow = min(FinestraDiCongestione, FinestraDiRicezione)
```

Dove:

- FinestraDiCongestione (congestion window): il max numero di byte che la rete è in grado di trasmettere;
    
- FinestraDiRicezione (advertised window): quanti byte il destinatario è in grado di ricevere;
    
- maxWindow: il minimo tra i due valori delle finestre, che l'host prende come numero max di byte da poter trasmettere.
    

Dei 4 algoritmi utilizzati dal TCP, prendiamo in esame lo slow start e il congestion avoidance, che lavorano assieme durante tutta la sessione TCP:

- al momento della connessione, il mittente imposta la finestra di congestione alla massima quantità di byte che la rete può spedire;
    
- ogni volta che un segmento viene inviato, e ricevuto l'ACK di conferma ricezione, il valore della finestra di congestione viene raddoppiato. Così facendo avviene una crescita esponenziale del numero di byte che possono essere inviati in rete, fino al raggiungimento di una certa soglia (threshold), solitamente impostata a 64Kb;
    
- da questo momento la dimensione della finestra di congestione viene gestita dal congestion avoidance che effettua incrementi di tipo lineare, sommando di volta in volta il valore iniziale della finestra di congestione;
    
- quando si genera un timeout, la soglia viene impostata a metà del valore della finestra di congestione che ha generato il timeout e la finestra di congestione viene riportata al suo valore iniziale.
    

---

*Controllo di Flusso e degli Errori*  
Il protocollo Sliding Window, o finestra scorrevole, è un meccanismo usato dal TCP per garantire un controllo efficiente del flusso dei dati tra mittente e destinatario.

Permette al mittente di inviare più byte consecutivi senza aspettare un acknowledgement (ACK) per ognuno, ma solo entro una certa "finestra" di dati.

La dimensione della finestra dipende da quanto spazio ha il ricevente nel suo buffer: se è pieno, la finestra si restringe; se è libero, si allarga. Questo evita di sovraccaricare il destinatario.

In più, ogni segmento ha un numero di sequenza, così TCP può controllare l’ordine dei pacchetti e accorgersi se ne manca qualcuno. In caso di perdita, vengono ritrasmessi solo i dati mancanti.

---

*UDP*  
UDP (User Datagram Protocol) offre solo le funzionalità di multiplexing/demultiplexing. Il servizio fornito è connectionless e non affidabile. Il datagram UDP si compone di:

- source port number;
    
- destination port number;
    
- length (nell'UDP-Lite, viene sostituito dal checksum coverage length);
    
- checksum;
    
- data;
    

---

*UDP-Lite*  
UDP-Lite è una versione modificata di UDP che permette di accettare pacchetti anche se parzialmente corrotti.

A differenza di UDP normale, dove un errore in un singolo byte fa scartare tutto il pacchetto, con UDP-Lite si può decidere di proteggere solo una parte dei dati con il checksum.

Questo è utile per applicazioni come streaming video, audio o VoIP, dove è meglio ricevere qualcosa, anche se imperfetto, piuttosto che perdere tutto il pacchetto.

In pratica, UDP-Lite migliora la tolleranza agli errori in contesti dove la velocità è più importante dell’integrità completa dei dati.

---

*Confronto tra UDP e TCP* 
TCP e UDP hanno in comune alcune caratteristiche tipiche dei protocolli del livello Transport:

- le funzionalità di multiplexing/demultiplexing
    
- l’impiego delle porte
    

TCP è il protocollo da preferire quando è richiesta integrità dei dati e affidabilità. UDP è invece preferibile quando le prestazioni sono più importanti del ricevere i dati in modo perfetto, senza alcuna perdita.


---

# DHCP e DNS



Il principale protocollo usato per la configurazione degli host è il DHCP (Dynamic Host Configuration Protocol). Per la gestione della rete si usa invece il protocollo SNMP (Simple Network  Management Protocol).

---

# Il DHCP

Quando nelle reti si diffusero la tecnologia wireless e l’uso di computer portatili, in ambito IETF fu definito il protocollo DHCP (Dynamic Host Configuration Protocol), la cui specifica si trova in RFC 2131.

Tramite DHCP, oltre all’indirizzo IP, un host può ricevere altri parametri di configurazione: 

- subnet mask
- default gateway: per esempio l’indirizzo IP del router che connette la subnet alla rete Internet. A questo sono inviati i pacchetti IP aventi indirizzo di rete del destinatario diverso da quello del mittente;
- DNS Server preferito;
- DNS Server alternativo;

---
*Configurazione Modalità*
L’amministratore di rete può configurare, per ogni subnet e per ogni host, la modalità con cui il DHCP Server risponderà alle richieste dei client scegliendo fra 3 diversi tipi di configurazione.

- Configurazione manuale: è possibile assegnare un indirizzo IP specifico a un host, inserendolo manualmente nel DHCP Server; di regola si utilizza per macchine come router e server che si trovano stabilmente in una rete o per host che necessitano di un indirizzo permanente;
- Configurazione automatica: il DHCP Server assegna in modo automatico un indirizzo IP permanente a ogni host che si collega alla rete (si differenzia dalla configurazione dinamica per l’assenza del tempo di lease);
- Configurazione dinamica: il DHCP Server assegna un indirizzo IP a un host per un tempo limitato (tempo di lease) in base alla lease length policy stabilita. Allo scadere del tempo di lease il client può richiederne il rinnovo o richiedere l’assegnazione di un nuovo indirizzo;

---

*L'Architettura Client Server DHCP*
Un solo DHCP Server è solitamente in grado di soddisfare le esigenze operative relative all’assegnazione degli indirizzi IP e al setting dei parametri di configurazione sui client della rete locale. In condizioni normali il carico che deriva da queste attività non è particolarmente pesante. 

Un DHCP Server può anche essere configurato per servire più subnet, per due scopi:

- fault-tolerance: per cui in genere è opportuno inserire un secondo DHCP Server come backup, così da mantenere il servizio sempre attivo;
- bilanciamento del carico di lavoro: così da diminuire i tempi di risposta del server. In tal caso, alla richiesta di un client per l’assegnazione di un indirizzo IP possono rispondere più di un DHCP Server;

Quando un DHCP Server è responsabile dell’indirizzamento su una subnet diversa dalla propria è necessario introdurre un relay agent (agente di ritrasmissione), ossia una macchina che non è né un server né un client, ma svolge un ruolo di intermediario occupandosi di facilitare la comunicazione tra client e server attraverso più reti.

---

*La Comunicazione tra DHCP Client e DHCP Server*
I messaggi di trasporto tra DHCP Client e DHCP Server sono di due tipi: richieste (request) e risposte (reply). Il protocollo di trasporto utilizzato è UDP e utilizza le porte 67 per il server e 68 per il client.

---

*Il Pacchetto DHCP*
- op (operation code)
- htype (hardware type)
-  hlen (Hardware address length)
-  hops (Hops count)
- Transaction ID (xid)
- Seconds (secs)
- Flags (flags)
- Client IP address (ciaddr)
- ‘Your’ (client) IP address (yiaddr)
- Server IP address (siaddr)
- Gateway IP address (giaddr)
- Client hardware address (chaddr)
- Server host name (sname)
- Boot file name (file)
- Options;

---

*Assegnazione degli Indirizzi*
La comunicazione tra il nuovo host e il server, al fine di ottenere i dati per la configurazione di rete, avviene 4 fasi:

1) Ricerca del DHCP Server: quando un nuovo host si connette alla rete, per ottenere un IP, invia un messaggio di broadcast chiamato DHCP Discover. Questo messaggio viene inviato a tutti i dispositivi sulla rete locale, perché l’host non conosce ancora l’indirizzo del server DHCP che possa assegnargli una configurazione IP;
2) Offerta al DHCP Client: quando il server DHCP riceve il messaggio di Discover, risponde con un messaggio chiamato DHCP Offer che contiene una proposta di configurazione per il client: un indirizzo IP disponibile, la subnet mask, il gateway, i DNS e altre informazioni utili;
3) Richiesta al DHCP Server: dopo aver ricevuto le offerte, il client sceglie una delle proposte  e invia un messaggio chiamato DHCP Request, con cui il client comunica al server DHCP che ha accettato l’offerta. Anche questo messaggio è un broadcast, così che anche gli altri server DHCP sappiano che la loro offerta è stata rifiutata;
4) Conferma al DHCP Client: infine, il server DHCP riceve la richiesta e risponde con un messaggio chiamato DHCP  ACK, con cui il server conferma l’assegnazione dell’indirizzo IP al client e ribadisce tutte le informazioni necessarie per la configurazione della rete;

---

*Problematiche di Sicurezza*
Il DHCP utilizza i protocolli UDP e IP che sono intrinsecamente insicuri. Sono due i principali problemi di sicurezza:

- DHCP Server non autorizzati: un DHCP Server abusivo potrebbe inserirsi e inibire gli host o configurarli per azioni fraudolente; 
- DHCP Client non autorizzati: un host potrebbe danneggiare la rete, oppure esaurire gli indirizzi a disposizione e bloccare nuovi accessi;

Per ovviare al problema si possono implementare meccanismi di sicurezza ai livelli più bassi, inoltre si potrebbe usare IPsec per rendere sicuro il livello Network.

---

# Il  DNS

Il DNS consente agli utenti della rete di usare dei nomi al posto dell’indirizzo IP. È un database distribuito usato dagli applicativi del TCP/IP per il mapping tra nomi e indirizzi IP. Il DNS è formato da 3 componenti principali:

- Domain Name Space, specifica la struttura ad albero dei nomi di dominio ed è suddiviso in 3 tipi di domini:
	- domini radice;
	- domini intermedi;
	- domini foglia;

- Name Server, un processo applicativo con il ruolo di server che contiene informazioni su alcune parti del Name Space chiamate zone;
- Resolver, un programma con il ruolo di client che ottiene informazioni dal Name Server;

---

*Come Funziona il DNS*
L’albero gerarchico del DNS è realizzato mediante base di dati distribuita, cosa che garantisce il funzionamento della rete. Se tutte le informazioni fossero memorizzate su un unico server e questo si guastasse si fermerebbe infatti tutta la rete Internet.

Lo spazio dei nomi del DNS è stato suddiviso in zone disgiunte, ognuna con un Name Server principale (DNS primario) e dei Name Server secondari (DNS secondario) che attingono al principale.

I client che accedono ai Name Server sono i resolver. Se il Resource Record è authoritative per la zona richiesta, il DNS Server risponderà direttamente, in caso contrario farà una ricerca nello spazio dei nomi. Questo processo si chiama risoluzione dei nomi.

---

*Problematiche di Sicurezza del DNS*
Il DNS dal punto di vista della sicurezza è critico sotto vari punti di vista:
- non è autenticato: l'informazione richiesta potrebbe arrivare non dal DNS Server corretto ma da un'altra macchina;
- è molto lento, quindi è possibile che qualcuno intercetti la richiesta destinata a un DNS Server e risponda la suo posto che qualcuno intercetti la richiesta destinata a un DNS Server e risponda al suo posto (spoofing);
- non offre meccanismi per proteggere l'integrità delle informazioni distribuite;

Proprio per il ruolo critico che il DNS ricopre nell'internet, l'ICANN ha evidenziato la necessità di stabilire metriche e modalità per il controllo del DNS, individuando 5 indicatori importanti: coerenza, integrità, velocità, disponibilità e robustezza.


---

# La Crittografia