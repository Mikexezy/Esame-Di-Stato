---
connections:
  - "[[Sistemi e Reti]]"
---
# Spanning Tree Protocol

Le reti locali moderne sono suddivise in segmenti più piccoli collegati tramite switch o router. Questo permette di isolare il traffico, ridurre i domini di collisione e migliorare la banda disponibile per ogni dispositivo. Per garantire affidabilità, spesso si introducono collegamenti ridondanti, ma questi possono causare loop nella rete e generare broadcast storm, cioè un sovraccarico di traffico che rallenta o blocca la rete. Per evitare questi problemi si usa il protocollo STP (Spanning Tree Protocol), definito dallo standard IEEE 802.1.

STP costruisce una topologia logica ad albero che lascia attivi solo i collegamenti necessari tra due dispositivi e di conseguenza disattiva quelli ridondanti a livello logico (ma non fisico), da usare solo in caso di guasto.

Ogni switch invia messaggi chiamati BPDU (Bridge Protocol Data Unit) per:
- selezionare lo switch root (radice dell’albero)
- calcolare il percorso più breve verso la root
- eleggere il designated switch (quello più vicino alla root su ogni segmento)
- scegliere la root port per ogni switch (la porta con il percorso migliore verso la root)

Le porte coinvolte nello Spanning Tree sono le designated port (attive nel traffico) e le altre porte bloccate per prevenire i loop. Gli stati possibili di una porta STP sono:
- blocking: riceve solo BPDU
- listening: partecipa alla costruzione della topologia
- learning: impara gli indirizzi MAC
- forwarding: invia e riceve traffico
- disabled: disattivata manualmente

Il problema principale dell'STP classico è il tempo di convergenza (30–50 secondi), troppo lungo per le moderne LAN. Per migliorarlo, nel 2001 è stato introdotto il Rapid Spanning Tree Protocol (RSTP), standard IEEE 802.1w, che riduce significativamente i tempi di riconfigurazione della rete.

# Le Reti Locali Virtuali

Per migliorare l'efficienza e la gestione delle reti, oltre a separare i domini di collisione, è utile anche dividere la rete in più domini di broadcast. Un dominio di broadcast è un gruppo di dispositivi che riceve un messaggio broadcast inviato da uno di essi. In una configurazione base, tutti gli host collegati a uno switch appartengono allo stesso dominio di broadcast. Tuttavia, in reti con molti dispositivi, i messaggi broadcast possono generare traffico eccessivo. Per evitare questo problema, si utilizzano due soluzioni:

- VLAN (Virtual LAN): creano sottoreti logiche all'interno della rete fisica, permettendo di suddividere i domini di broadcast senza modificare la topologia fisica
- Switch Layer 3: integrano funzionalità di routing, permettendo la comunicazione tra VLAN diverse senza bisogno di router esterni

Le VLAN offrono vari vantaggi come migliorare le prestazioni e la sicurezza della rete, semplificano l'aggiunta, lo spostamento e la gestione degli host e riducono i costi.

Una VLAN può essere creata in vari modi:
- per gruppi di porte: in base alla porta dello switch a cui è collegato un dispositivo (metodo più comune)
- per indirizzi MAC: in base all’indirizzo fisico del dispositivo (meno usato perché difficile da gestire)
- per protocolli: in base al protocollo di rete utilizzato

Esistono due tipi di collegamenti nelle VLAN:
- access link: collegamento che fa parte di una sola VLAN, usato per connettere dispositivi finali
- trunk link: collegamento punto-punto tra switch o altri apparati, trasporta traffico di più VLAN (fino a 4096)

In una configurazione con VLAN e trunking, le porte di uno switch possono essere configurate come:

- Access port  
  - Collegate a dispositivi finali (PC, stampanti, telefoni IP)  
  - Appartengono a una sola VLAN  

- Trunk port  
  - Collegate ad altri switch, router o server  
  - Trasportano traffico di più VLAN contemporaneamente  

In alcuni casi, è possibile configurare le porte con modalità dinamiche (es. Dynamic Trunking Protocol su switch Cisco), ma per motivi di sicurezza e controllo si preferisce la configurazione manuale.

Per semplificare la gestione centralizzata delle VLAN in reti complesse si usa il VTP (VLAN Trunking Protocol), che sincronizza le configurazioni tra switch. Gli switch VTP possono operare in tre modalità:
- VTP server: gestisce e distribuisce le configurazioni VLAN
- VTP client: riceve e applica le configurazioni dai server
- VTP transparent: inoltra le informazioni VTP ma non modifica la propria configurazione
