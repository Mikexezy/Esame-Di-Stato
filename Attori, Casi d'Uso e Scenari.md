---
connections:
  - "[[TPSIT]]"
---
## Riassunto Esteso: Casi d'Uso, Scenari e User Stories

I requisiti funzionali rappresentano i comportamenti attesi di un sistema informatico e descrivono ciò che il sistema deve fare in termini di servizi e risposte agli stimoli esterni. Uno degli strumenti più diffusi per descrivere i requisiti funzionali è il **caso d'uso** (_use case_), largamente impiegato nel modello di sviluppo orientato agli oggetti e formalizzato tramite il linguaggio UML.

### Casi d'Uso e Attori

Un **caso d'uso** descrive una sequenza di azioni che il sistema compie per fornire un servizio a un attore, ovvero un'entità esterna che interagisce con il sistema. Gli attori possono essere:

- **Primari**: iniziano l'interazione con il sistema per ottenere un determinato risultato.
    
- **Secondari**: supportano il sistema nel fornire il servizio ma non iniziano l'interazione.
    

Ogni caso d'uso deve essere:

- scritto dal punto di vista dell'attore;
    
- delimitato da confini chiari (inizio e fine dell'interazione);
    
- auto-contenuto, ossia descrivere una sequenza logica completa;
    
- focalizzato su comportamenti osservabili e misurabili.
    

Viene spesso utilizzata una descrizione narrativa per evidenziare come il sistema risponde a determinati eventi.

### Scenari: Definizione e Tipologie

Ogni caso d'uso è composto da uno o più **scenari**, che rappresentano varianti specifiche del comportamento del sistema. Gli scenari descrivono interazioni concrete tra attori e sistema e aiutano ad esplorare più a fondo le possibili situazioni operative.

Le principali tipologie di scenario sono:

- **As-is**: fotografano la situazione attuale, utile per identificare criticità e inefficienze.
    
- **Visionary**: mostrano come il sistema dovrebbe funzionare in futuro, una volta implementato.
    
- **Evaluation**: utilizzati nei test, descrivono situazioni da simulare per verificare il corretto funzionamento.
    
- **Training**: finalizzati alla formazione degli utenti, illustrano casi pratici d'uso.
    

Per costruire scenari validi è necessario analizzare le attività svolte dagli utenti, i dati in gioco e le interazioni possibili.

### Diagrammi dei Casi d'Uso e Relazioni

I **diagrammi dei casi d'uso UML** sono strumenti grafici che rappresentano attori, casi d'uso e le relazioni tra di essi. Gli attori sono visualizzati come omini stilizzati, mentre i casi d'uso sono ellissi con il nome del caso al centro. Le linee che li collegano rappresentano le interazioni.

Tra i casi d'uso possono esistere relazioni che aiutano a semplificare e strutturare meglio il diagramma:

- **Inclusione (<>)**: permette di riutilizzare una sequenza comune di azioni in più casi d'uso. È utile quando diversi casi condividono uno stesso sotto-processo.
    
- **Estensione (<>)**: definisce comportamenti opzionali che si attivano solo in certe condizioni. Aiuta a mantenere i diagrammi ordinati e a evitare ridondanze.
    

Queste relazioni rendono il modello più modulare e favoriscono il riutilizzo e la chiarezza.

### Documentazione di un Caso d'Uso

Ogni caso d'uso viene documentato seguendo una struttura standard che garantisce uniformità e facilita la lettura da parte degli stakeholder:

- **Nome**: identificativo del caso.
    
- **Descrizione**: obiettivo generale e funzione svolta.
    
- **Attori coinvolti**: elenco di attori primari e secondari.
    
- **Scenario principale**: flusso regolare delle operazioni.
    
- **Estensioni (variazioni)**: eventuali alternative, eccezioni o errori.
    
- **Precondizioni**: condizioni necessarie prima di iniziare il caso.
    
- **Postcondizioni**: risultati attesi alla fine del caso.
    
- **Requisiti speciali**: vincoli tecnici o normativi.
    
- **Autore/data**: persona che ha scritto il caso e data di redazione.
    

Questa documentazione è utile per lo sviluppo, il collaudo e la manutenzione del sistema.

### Le User Stories nel Modello Agile

Nel contesto **agile**, i requisiti vengono descritti mediante **user stories**, una forma sintetica e flessibile per rappresentare le esigenze dell'utente. Ogni user story si compone di tre parti:

1. **Situazione (as)**: chi compie l'azione (es. utente, amministratore);
    
2. **Motivazione (I want)**: cosa vuole fare;
    
3. **Aspettativa (so that)**: quale beneficio si aspetta.
    

Le user stories non sono casi d'uso completi ma ne rappresentano un'estensione semplificata, utile a evidenziare le funzionalità attese in termini di valore per l'utente.

Ogni story deve essere:

- chiara e comprensibile,
    
- realizzabile entro una o due iterazioni,
    
- collegata a criteri di accettazione condivisi.
    

Le user stories vengono raccolte nel **backlog**, uno strumento fondamentale del metodo agile, e sono considerate **partizioni verticali** perché includono una funzionalità completa dal punto di vista dell'utente. Tuttavia, per motivi pratici, si tende spesso a organizzarle **orizzontalmente** secondo criteri di efficienza e facilità di implementazione.

Questo approccio favorisce una gestione più dinamica e iterativa dei requisiti durante tutto il ciclo di sviluppo.