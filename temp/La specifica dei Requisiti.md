---
connections:
  - "[[TPSIT]]"
---
## Riassunto Esteso: Requisiti Software e Stakeholder

Un requisito è una proprietà richiesta o auspicabile del prodotto. Il documento dei requisiti contiene una descrizione di tutte le proprietà desiderate e include ogni informazione circa la funzionalità, i servizi, le modalità operative e di gestione del sistema da sviluppare. La definizione dei requisiti rappresenta un'analisi completa dei bisogni dell'utente e del dominio del problema, allo scopo di determinare cosa il sistema deve fare.

La raccolta dei requisiti è un processo complesso, che coinvolge membri del team di sviluppo, rappresentanti dell'azienda cliente e, talvolta, consulenti esterni. Gli stakeholder sono tutti coloro che, a vario titolo e livello organizzativo, hanno un interesse nella realizzazione del sistema. Ogni stakeholder può offrire una visione generale del sistema, che l'analista deve poi interpretare e formalizzare in termini tecnici e dettagliati.

È importante considerare anche i fattori esterni al sistema, poiché i requisiti non sono fissi ma possono evolversi durante tutto il ciclo di sviluppo. Errori in questa fase di analisi possono compromettere l'intero progetto. La normativa ISO 13407 (Human-centred design process) fornisce una guida all'identificazione dei requisiti e degli obiettivi di un sistema usabile, considerando:

- le prestazioni richieste dal sistema in relazione agli obiettivi operativi ed economici;
    
- i requisiti normativi e legislativi, incluse le normative su sicurezza e salute;
    
- la comunicazione e cooperazione tra utenti e altri attori rilevanti;
    
- le attività degli utenti, compresa la ripartizione dei compiti;
    
- la progettazione dei flussi di lavoro e dell'organizzazione;
    
- la gestione del cambiamento, incluse attività di formazione e personale coinvolto;
    
- la fattibilità delle operazioni, incluse quelle di manutenzione;
    
- la progettazione dei posti di lavoro e dell'interfaccia uomo-computer.
    

### Classificazione dei Requisiti

I requisiti software si classificano secondo due punti di vista principali:

#### Livello di dettaglio

- **Requisiti utente**: espressi in linguaggio comprensibile al cliente, riflettono le necessità percepite dall'utente finale. Sono presentati al team di sviluppo, che propone soluzioni anche alternative. Sono detti anche "requisiti aperti".
    
- **Requisiti di sistema**: imposti da vincoli tecnici, normativi o infrastrutturali. Sono scritti in linguaggio tecnico, spesso formale o semi-formale, e non lasciano margini all'inventiva. Possono non essere noti all'utente ma ben conosciuti dallo sviluppatore.
    

#### Tipo di requisito

- **Requisiti funzionali**: definiscono le funzionalità e i servizi offerti dal sistema. Devono essere:
    
    - completi (includere tutti i servizi richiesti);
        
    - coerenti (non contenere contraddizioni);
        
- **Requisiti non funzionali**: riguardano le modalità operative e il ciclo di vita del prodotto. Imposti dall'organizzazione o da fattori esterni, sono classificati da Sommerville in:
    
    - requisiti di prodotto;
        
    - requisiti organizzativi;
        
    - requisiti esterni;
        
- **Requisiti di dominio**: dipendono dal contesto specifico del sistema. Esempi includono la riservatezza dei dati, le leggi fisiche o normative settoriali (es. sicurezza sul lavoro). Un esempio tipico è la richiesta di login per accedere ad aree protette.
    

Una seconda classificazione è il modello **FURPS**, che distingue:

- **Functionality**: caratteristiche, funzioni, sicurezza del sistema;
    
- **Usability**: facilità d'apprendimento e d'uso, qualità della documentazione e dell'help;
    
- **Reliability**: accuratezza, frequenza delle failure, recuperabilità, predicibilità del comportamento;
    
- **Performance**: tempi di risposta, risorse impiegate, efficienza complessiva;
    
- **Supportability**: manutenibilità, estendibilità, compatibilità, adattabilità.
    

A questi si aggiungono i cosiddetti **vincoli** o **pseudorequisiti**, che includono:

- vincoli di **implementazione** (strumenti, linguaggi, piattaforme);
    
- vincoli di **interfaccia** (interazioni con altri sistemi);
    
- vincoli di **operazione** (modalità di gestione e amministrazione);
    
- vincoli di **packaging** (modalità di distribuzione);
    
- vincoli **legali** (licenze, regolamenti, certificazioni);
    

### Verifica e Validazione dei Requisiti

I requisiti funzionali sono verificabili tramite collaudi che coinvolgono gli utenti finali. La validazione, che deve avvenire durante tutto il ciclo di sviluppo, implica il controllo dei seguenti criteri:

- **Correttezza**: la specifica riflette esattamente ciò che è richiesto;
    
- **Completezza**: la specifica copre tutti gli scenari previsti;
    
- **Coerenza**: assenza di contraddizioni tra i requisiti;
    
- **Chiarezza**: i requisiti devono essere espressi in modo non ambiguo;
    
- **Realismo**: i requisiti devono essere realizzabili nei limiti imposti;
    
- **Verificabilità**: deve essere possibile testare ogni requisito;
    
- **Tracciabilità**: ogni funzione implementata deve essere collegabile a un requisito preciso.
    

Anche i requisiti di dominio sono verificabili collaudando le interazioni del sistema con software esistenti, sistemi di terze parti e rispetto delle normative. I requisiti non funzionali, invece, sono spesso vaghi e difficili da misurare in modo binario. In questi casi si adottano metriche quantitative per valutare il grado di soddisfazione.
