---
connections:
  - "[[TPSIT]]"
---
## Riassunto: Specifica dei Requisiti Software (SRS)

La Specifica dei Requisiti Software (SRS) rappresenta il documento conclusivo della fase di analisi di un progetto software. Il suo obiettivo è raccogliere in maniera strutturata tutte le esigenze funzionali e non funzionali espresse dal committente. Questo documento è un punto di riferimento per garantire una comunicazione chiara e coerente tra analisti, sviluppatori, utenti e cliente. Assicura che tutte le parti coinvolte abbiano una visione condivisa del sistema da realizzare e costituisce la base per pianificare e controllare lo sviluppo.

### Importanza dell'SRS

Redigere un SRS accurato è essenziale per evitare errori che, se scoperti nelle fasi avanzate di sviluppo, possono comportare ritardi significativi e costi elevati. Un requisito ignorato o mal formulato all'inizio può compromettere l'intero progetto. Al contrario, un SRS ben fatto consente di stimare correttamente tempi, risorse e budget, oltre a fungere da base per la validazione e il collaudo del sistema.

### Contenuto dell'SRS

Il documento deve includere le seguenti informazioni:

- analisi dei bisogni e dei requisiti degli utenti;
    
- descrizione del contesto operativo;
    
- elenco delle funzionalità richieste;
    
- definizione dei vincoli tecnici e operativi, come requisiti di performance, sicurezza, affidabilità e compatibilità;
    
- rappresentazione tramite casi d'uso e modelli di sistema.
    

Secondo lo standard IEEE 830-1998, la struttura dell'SRS si articola in:

1. Introduzione;
    
2. Descrizione generale del sistema;
    
3. Requisiti specifici (funzionali e non);
    
4. Modelli e architettura;
    
5. Appendici tecniche.
    

Sommerville propone una classificazione simile, ponendo particolare attenzione alla chiarezza e alla logica interna dei contenuti.

### Ruoli e responsabilità

Il documento distingue chiaramente i diversi attori coinvolti nel progetto:

- **Contractor**: l'organizzazione che fornisce il sistema;
    
- **Customer**: il soggetto che richiede il sistema;
    
- **Supplier**: chi sviluppa concretamente il sistema;
    
- **User**: l'utente finale che interagirà con il software.
    

### Validazione dei requisiti

Affinché sia efficace, un SRS deve essere:

- completo e privo di ambiguità;
    
- verificabile, cioè suscettibile di essere testato;
    
- coerente con i vincoli e le specifiche tecniche;
    
- costantemente validato insieme a clienti e utenti;
    
- facilmente modificabile e aggiornabile;
    
- tracciabile, con requisiti numerati e collegati ad attori, scenari o componenti.
    

### Ambiguità e dettagli

Un linguaggio preciso riduce le interpretazioni errate. Requisiti ben scritti contengono formule misurabili, come ad esempio:

- "Il sistema deve rispondere entro 10 secondi";
    
- "Il tasso di errore non deve superare 1 su 300 richieste";
    
- "Il programma deve avviarsi entro 5 secondi".
    

Questo tipo di formulazioni consente di verificare concretamente se il sistema rispetta o meno i requisiti specificati.

### Convalida delle specifiche

I requisiti possono cambiare nel tempo, anche a causa di nuove esigenze o modifiche organizzative. Per questo motivo, la convalida continua del documento è fondamentale. Gli errori più comuni includono requisiti vaghi o omessi, informazioni incomplete, conflitti interni tra requisiti e richieste irrealistiche. Talvolta, accordi verbali non documentati possono generare ambiguità.

Le checklist risultano molto utili per controllare che ogni aspetto critico sia stato coperto. Ad esempio, aiutano a verificare se sono stati specificati i limiti temporali, le eccezioni, i vincoli hardware o software, e la presenza di modifiche future prevedibili.

### Revisioni e ispezioni

Per migliorare la qualità del documento è essenziale sottoporlo a revisioni frequenti e sistematiche. Questo processo coinvolge tutte le parti interessate: autore del documento, cliente, progettista, esperti di qualità. Le revisioni devono essere pianificate per funzione o area tematica, prevedendo una lettura preliminare individuale e una discussione collettiva per identificare eventuali errori o ambiguità.

### Tecniche di Reading

Il metodo del "reading" è molto efficace per rilevare errori latenti. Si concentra sull'eliminazione di ciò che non deve essere presente. Le buone pratiche prevedono:

- evitare termini generici e poco precisi;
    
- mantenere uno stile narrativo coerente e uniforme;
    
- formulare requisiti oggettivi e verificabili;
    
- usare esempi numerici ove possibile;
    
- assicurare coerenza nella struttura e nei contenuti.
    