---
connections:
  - "[[Sistemi e Reti]]"
---

*Firewall*

Il firewall è una linea di difesa che filtra tutti i pacchetti sia in entrata che in uscita da una rete, secondo regole prestabilite che contribuiscono alla sicurezza della rete stessa, questo si può comunemente realizzare tramite un PC, l'apposito software e le Access Control List che servono per configurarlo. I firewall si possono distinguere in 3 categorie in base al livello dello stack TCP/IP in cui operano:

- Application Level Firewall: intercetta le trasmissioni a livello Application valutando il contenuto applicativo dei pacchetti, come i Proxy;
- Packet Filtrer Firewall: lavora a livello Network e Transport, è più veloce dell'Application perché controlla solo l'header e poiché il firewall non gestisce i dati all'interno del pacchetto viene solitamente  impiegato nei punti di origine della connessione a Internet;
- Stateful Packet Inspection Firewall: agisce solo a livello Transport, controlla e analizza tutto il pacchetto dati. Questo tipo di firewall può controllare lo stato di connessione TCP e compilare le informazioni ottenute su una tabella;

---

*ACL*

L'Access Control List o ACL è un insieme di istruzioni da applicare alle interfacce di un router allo scopo di gestire il traffico, si utilizzano le ACL per fornire un livello base di sicurezza e aumentare la performance della rete e decidere quale tipo di traffico può essere trasmesso. Queste vengono elaborate dal router in maniera sequenziale nell'ordine in cui sono state inserite le varie clausole, appena un pacchetto soddisfa una delle condizioni il resto delle ACL non viene preso più in considerazione, il pacchetto viene quindi eliminato o inoltrato secondo le istruzioni.

L'ultima istruzione di un ACL è sempre una negazione implicita 'deny ip any any' che nega qualsiasi tipo di traffico, essa viene inserita automaticamente n ogni ACL, anche se non visibile. Proprio per questo che in un'ACL deve essere presente almeno un permit, diversamente l'unico risultato sarebbe la negazione di qualsiasi traffico per ogni direzione.

Quando le ACL vengono inserite all'interno dell'interfaccia bisogna specificare la direzione, che può essere in uscita o in ingresso sull'interfaccia. Con traffico in entrata si intende il traffico che arriva sul router prima dell'accesso alla tabella di routing, con traffico in uscita si intende il traffico già entrato nel router e sottoposto ad elaborazione per l'inoltro.

Le ACL possono essere:
- Standard ACL (1-99), controllano solo gli indirizzi sorgenti di tutti i pacchetti IP, individuano il traffico a livello 3, in base al solo IP sorgente. A quell'IP sarà pertanto concesso o negato l'accesso a qualsiasi servizio;
- Extended ACL(100-199), controllano entrambi gli indirizzi, sorgente e destinazione, individuano il traffico sino al livello 4, in base ai protocolli TCP o UDP e ai numeri di porta sorgente e di destinazione;

Sia le standard che le numeriche possono essere:
- Numbered (numeriche), con identificativo basato sui numeri da 1 a 99 e da 1300 a 1999 per le standard, da 100 a 199 e da 2000 a 2699 per le extended;
- Named (con nome),  identificate da un nome scelto dall'amministratore;

Su un router si può definire un'ACL per ogni controllo di livello 3 (come IP o Appletalk), per ogni interfaccia logica (ogni interfaccia 'subif' può avere la propria ACL), per ogni direzione (IN o OUT). Per esempio, in un interfaccia Ethernet 0/0 di un router che instrada solo il protocollo IP, possiamo avere per quest'interfaccia al massimo 2 ACL. 

Un altro aspetto molto importante è il posizionamento delle ACL:
- Posizionamento di ACL extended,  devono essere posizionate il più vicino possibile alla sorgente da filtrare, poiché posizionarle lontane dalla sorgente sarebbe inefficiente, in quanto i pacchetti attraverserebbero troppe zone prima di essere bloccati o filtrati;
- Posizionamento di ACL standard, devono essere posizionate il più vicino possibile alla destinazione poiché le ACL standard filtrano i pacchetti solo in base all'indirizzo sorgente, il posizionamento nei pressi dell'interfaccia sorgente potrebbe bloccare del traffico ritenuto valido;

## Configurazione di ACL standard numeriche

	Router(config)#access-list numero_ACL deny|permit ip_sorgente maschera_wildcard

## Configurazione di ACL extended numeriche

	Router(config)#access-list numero_ACL [deny|permit] protocollo ip-sorgente wildcard ip-destinazione wildcard condizione       applicazione

## Configurazione di ACL standard con nome

	Router(config)#ip access-list standard nome_ACL
	Router(config-std-nacl)# [deny|permit] ip-sorgente

## Configurazione di ACL extended con nome

	Router(config)#ip access-list extended nome-ACL
	 Router(config-ext-nacl)# deny-permit protocollo ip_sorgente wildcard_mask
	Ip_destinazione wildcard_mask condizione applicazione

---

*Proxy*

Un proxy è un programma che si frappone tra client e server facendo da tramite, il client si collega al proxy e gli invia la richiesta, il proxy a sua volta si collega al server a cui inoltra la richiesta del client, infine il proxy inoltra la risposta al client. Al suo interno troviamo l'utilizzo di diverse tecniche come NAT e PAT ed essi lavorano a livello Application, il loro compito principale è garantire la connettività e il caching ai client a loro collegati, ai dini dell'efficienza della rete. 

Questo si colloca prossimo al client in modo da permettere un miglioramento delle prestazioni e una riduzione del consumo di banda, e tra i suoi compiti principali vi sono:
- Connettività: permettendo ad una rete privata di accedere a Internet tramite un solo PC;
- Privacy: permettendo di mascherare il vero IP del client;
- Caching: permettendo di immagazzinare per un certo tempo i risultati delle richieste di un client;
- Monitoraggio: permettendo di tenere traccia di tutte le operazioni effettuate; 
- Amministrazione: permettendo di applicare le regole definite dell'amministratore di sistema per determinare quali richieste inoltrate, quali rifiutare e limitare l'ampiezza di banda utilizzata dai client;
- Filtraggio: permettendo di svolgere funzioni di firewall a livello Application, garantendo protezione a scapito della velocità della rete;
- Restrizioni: permettendo di creare una zona neutra o terza zona, nota anche come DMZ, dove il traffico tra le due è fortemente limitato e controllato;

I proxy possono essere utilizzati in diversi modi, a seconda di dove vengono collocati:
- Single Proxy Topology, che è la scelta più semplice poiché utilizza un singolo Proxy Server per servire l'intera rete, è però solo sufficiente per un piccolo gruppo di client;
- Multiple Proxy Vertically Topology, che è la scelta migliore per reti medio-grandi poiché si configurano più proxy, uno primario a cui gli altri si connettono e più secondari che agiscono come fossero dei client di quello primario. Questa è una tecnica che consente a qualsiasi client di avere il filtraggio dei pacchetti personalizzato;
- Multiple Proxy Horizontally Topology, ottimo in quanto bilancia il carico tra i server in base alle richieste dei client, in tal modo le informazioni sul trattamento dei pacchetti personalizzati si distribuiscono ai server di pari livello per riuscire a garantire la risoluzione in locale;

Il proxy si avvale di determinate tecniche come NAT e PAT per nascondere i pacchetti.

---

*NAT e PAT*

Il NAT (Network Address Translation) è una tecnica attuata dal router che sostituisce nell'intestazione di un pacchetto IP quest'ultimo con un altro indirizzo, spesso usato per permettere a una rete locale che usa una classe di indirizzi privata, di accedere a Internet usando un solo indirizzo pubblico. Ovvio che il NAT non è efficace come un firewall, esso usa una tabella con la corrispondenza tra i socket interni ed esterni in uso, quando un client richiede una pagina web a un server esterno, il  suo socket viene traslato e la corrispondenza viene registrata nella tabella, quando la risposta arriva, la tabella permette al router NAT di effettuare la traslazione inversa e inviare i dati.

Il NAT presenta diversi vantaggi:
- Limita il numero di IP pubblici necessari per collegare una LAN a Internet;
- Mantiene inalterata la configurazione degli host;
- Non modifica il funzionamento dei protocolli e delle applicazioni della rete Internet;
- Offre una flessibilità elevata grazie allo spazio molto esteso per gli indirizzi;
- Riduce i costi di accesso ad Internet;
- Garantisce maggior sicurezza per i PC ad Internet;

 Il NAT presenta 3 funzionalità:
 - Static NAT: ha a disposizione un solo IP pubblico e a qualunque pacchetto in uscita assegnerà tale indirizzo;
 - Dynamic NAT:  ha a disposizione un insieme di indirizzi pubblici tra cui sceglierne uno da assegnare ai pacchetti in uscita;
 - PAT (Port Address Translation);

Anche IPv6 implementa una forma di NAT con scopi del tutto diversi dal NAT IPv4, con IPv6 non serve risparmiare indirizzi pubblici, ma far comunicare reti IPv6 con reti IPv4 in 3 modi, come ipotizzato da IETF:
- dual-stack: prevede l'utilizzo del doppio stack IP nella pila TCP/IP, per inoltrare pacchetti IPv4 e IPv6. Senza dubbio è la tecnica più semplice da implementare, ma presenta alcuni svantaggi come l'aumento della complessità della rete. È da sottolineare che non risolve il problema del numero degli indirizzi IPv4, in quanto secondo questa tecnica un'interfaccia dev'essere sempre e cmq dotata dei due indirizzi IPv4 e IPv6;
- conversion: è realizzato tramite il protocollo NAT-PT (Network Address Translation - Protocol Translator) che permette la comunicazione tra reti IPv6 e IPv4, questo sistema sfrutta i concetti introdotti dalla tecnologia NAT convertendo l'indirizzo IPv6 in uno IPv4. È sconsigliato il suo utilizzo quando vi è la comunicazione tra un host dual-stack  e un host solo IPv6 o IPv4;
- tunneling per IPv6: incapsula il pacchetto IPv6 in uno IPv4, permettendone così il trasporto su reti IPv4, viene solitamente utilizzata per far fronte ai problemi di incompatibilità  tra le reti IPv4 e IPv6. Con il tunneling si stabilisce un collegamento point-to-point tra due host;

Nel tunneling per IPv6 esistono due modi di agire:
- 4to6: nel tunneling IPv4 di un pacchetto IPv6, i pacchetti IPv6 vengono incapsulati dall'host sorgente in pacchetti IPv4, inviati nel tunnel IPv4 e una volta giunti a destinazione, l'host ricevente li decapsula per riottenere l'indirizzo in IPv6;
- 6to6: il tunneling IPv6 su IPv4 è di difficile realizzazione sulle reti globali per le complicazioni che introduce a livello di routing e quindi il suo utilizzo è limitato ad applicazioni e comunicazioni in reti locali più o meno grosse;

 Per il NAT vale il rapporto 1:1 tra IP del server di destinazione e IP del client. Il router NAT non è in grado di distinguere a quale dei due client locali sono destinati i pacchetti in arrivo dello stesso server remoto, ed è qui che entra in gioco la tecnica PAT.
 
 Il PAT è una tecnica che consente al router di utilizzare un singolo IP per gestire oltre 64.000 connessioni private contemporaneamente, ciò significa che può traslare più IP client per un medesimo IP destinazione cambiando solo la porta. Per il PAT vale il
 rapporto 1:1 tra IP del server di destinazione e IP del client.

---

*DeMilitarized Zone*

Per aumentare di molto la sicurezza di una rete è buona norma dividerla in zone, in base al traffico e alla funzione se se ne identificano diverse, nei casi più semplici vi sono solo due zone che sono attestate sui due lati del firewall:
- zona LAN, ovvero il segmento privato e protetto che comprende tutti gli host e i server i cui servizi sono riservati all'uso interno;
- zona WAN, ovvero la parte esterna a cui appartengono gli apparati di routing che sostengono il traffico da e per la rete locale, Internet e sedi remote dell'azienda;

Vi sono casi in cui è necessaria la creazione di una terza zona detta DMZ (DeMilitarized Zone), che per definizione è un'area in cui sia il traffico LAN che quello WAN sono fortemente limitati e controllati, tale configurazione viene normalmente utilizzata per permettere ai server posizionati sulla DMZ di fornire servizi all'esterno senza compromettere la sicurezza della rete aziendale interna.


Nella DMZ solitamente si colloca la posta elettronica, con l'installazione di un server mail all'interno della rete aziendale che comporta la pubblicazione del servizio SMTP. Praticamente, il server che pubblica il servizio SMTP viene collocato in questa zona ed eventualmente insieme a lui, anche la web mail, l'antispam e l'antivirus, in LAN restano il server che ospita il database delle caselle e gli altri servizi. Un altro caso tipico sono gli Application Server che isolano un database residente in LAN, ma ne offrono un'interfaccia verso l'esterno.

Una DMZ, per esporre all'esterno i servizi di un'azienda, può essere realizzata in due modi:
- vicolo cieco: viene realizzato mediante un firewall con due porte, una verso la LAN e una verso la DMZ, oltre a quella verso la WAN;
- zona cuscinetto: viene creata aggiungendo un secondo firewall che prende il nome di external firewall, esso ha il compito di separare la rete pubblica dalla DMZ. Il primo, l'internal firewall, separa la DMZ dalla zona LAN vera e propria, questo garantisce una sicurezza migliore dei database presenti in LAN;