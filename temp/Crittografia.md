---
connections:
  - "[[Sistemi e Reti]]"
---

*Internet Security*

Con la diffusione di Internet, la sicurezza delle informazioni è diventata una questione fondamentale. È essenziale proteggere i dati sia a livello fisico che durante la loro trasmissione da un nodo all'altro. Per garantire questa protezione, sono state sviluppate diverse misure di sicurezza, note complessivamente come **Internet Security**.

Alla base dell'Internet Security vi è la **Raccomandazione X.800**, che definisce un insieme di requisiti di sicurezza che ogni sistema deve soddisfare:

- Autenticazione: assicurare l'identità dei soggetti coinvolti nella trasmissione;
- Controllo degli Accessi: proibizione dell’uso di una risorsa da parte di soggetti non autorizzati;
- Confidenzialità: protezione della riservatezza dei dati, poiché nessun soggetto terzo vi deve accedere durante la trasmissione;
- Integrità: certezza che i dati non siano stati alterati da soggetti non autorizzati;
- Non ripudiabilità: protezione contro la negazione di un soggetto coinvolto nella trasmissione;

La strategie di sicurezza principali nella trasmissione dei dati si incentrano o sull'oscurazione o sul confinamento. Qualsiasi sia quella adottata, nella progettazione del servizio di sicurezza si deve:

1) Utilizzare un algoritmo per trasformare i dati in chiaro in dati crittografati;
2) Generare le chiavi da utilizzare per crittografare e decrittografare;
3) Sviluppare un metodo per la condivisione sicura delle chiavi;
4) specificare un protocollo che permetta di utilizzare sia l'algoritmo che le chiavi in modo sicuro;

---

*La Crittografia*

La crittografia è l’insieme di tutte le procedure che hanno lo scopo di nascondere il significato di un messaggio tranne che al legittimo destinatario. Alla base vi è un cifrario, che ci permette di trasformare ogni carattere del testo in chiaro. Per cifrare un testo occorrono un algoritmo di cifratura e una chiave per decifrarlo.

Uno dei cardini della teoria della crittografia è il principio di Kerckoffs, secondo il quale la sicurezza di un sistema crittografico è basata esclusivamente sulla conoscenza della chiave.

Esistono molti sistemi di crittografia, si possono classificare in vario modo:

1) Tipo di operazioni usate per cifrare il testo:
	- Crittografia a sostituzione: ogni elemento del testo in chiaro diviene un altro elemento;
	- Crittografia a trasposizione: gli elementi che compongono il testo in chiaro vengono riorganizzati;
2) Modo in cui il testo in chiaro viene elaborato:
	- Crittografia a blocchi:
	- Crittografia a flusso:
3) Numero di chiavi distinte utilizzate:
	- Crittografia a chiave simmetrica:
	- Crittografia a chiave asimmetrica:


---

*Crittografia Simmetrica e Asimmetrica*

La crittografia a chiave simmetrica si basa sull’utilizzo di una sola chiave usata sia per cifrare che per decifrare. La crittografia a chiave asimmetrica o a chiave pubblica nasce per risolvere il problema della distribuzione sicura delle chiavi, essa utilizza due chiavi per ciascun soggetto, una privata nota sola al soggetto, l’altra pubblica, distribuita ai possibili destinatari. 
In genere il numero di chiavi da generare sarà sempre 2 x N dove N è il numero di soggetti che vogliono comunicare, a seconda di come queste coppie vengano impiegate abbiamo 3 diversi possibili utilizzi:

- Confidenzialità: viene utilizzata la coppia di chiavi del destinatario;
- Autenticazione: viene utilizzata solo la coppia di chiavi del mittente;
- Tutte: utilizzando entrambe le coppie di chiavi;

Ovviamente, per poter cifrare un testo con una chiave e poi decifrarlo con una diversa al fine di riottenere il testo di partenza occorre che le due chiavi siano matematicamente correlate, ma non deve essere possibile ricostruire una delle due chiavi sulla base di quella posseduta.

---

*Gli Algoritmi DES e Triple DES*

Il DES (Data Encryption Standard), creato nel 76' su commissione del governo degli Stati Uniti, è un algoritmo molto complicato, le cui basi sono state gettate negli anni 40' quando si dimostrò che per ottenere tale sicurezza l'algoritmo di cifratura deve avere almeno due caratteristiche:

- Confusion: renda confusa la relazione tra testo in chiaro e testo cifrato;
- Diffusion: alteri la struttura del testo in chiaro, tipicamente permutando i caratteri di esso;

Nel DES esse sono soddisfatte attraverso una serie (round) di permutazioni del messaggio e combinazioni del messaggio con la chiave. Esso funziona così:

- Input: il testo in chiaro viene suddiviso in blocchi dalla dimensione di 64 bit, la chiave è a 56 bit, quindi vi sono $2^{56}$ possibili chiavi diverse (se ci facciamo due conti sono una roba come 7,2 milioni di miliardi di possibili chiavi);
- Sequenza di passi:
	1) Viene effettuata una permutazione iniziale del blocco basata su una matrice 8x8 di permutazione casuale. Per esempio se il primo numero della matrice è 60, il 60esimo bit diviene il primo bit del testo permutato, il 9ono diviene il secondo e così via;
	2) Viene suddiviso il testo permutato in due semi blocchi da 32 bit detti $S_i$ (parte alta) e $D_i$ (parte bassa) dell'i-esimo blocco del testo. Questi 2 semi blocchi saranno l'input del primo round col nome di $L_0$ e $R_0$ insieme ad una chiave $K_1$;
	3) Partendo da un'unica chiave da 56 bit vengono generate 16 chiavi $k_1, ......, K_1$ 6 da 48 bit ciascuna. In questa operazione viene usata una matrice di permutazione casuale 8x7, con cui viene rimescolata e compressa la chiave in input (eliminando i bit 9, 18, 22, 25, 35, 38, 43, 54) per ottenere in output una chiave da 48 bit (ogni chiave è associata ad un round);
	4) Inizialmente i 32 bit del semi blocco di destra `R_{i−1}` vengono espansi a 48 bit mediante una matrice di espansione che va semplicemente a ripetere alcuni bit. I 48 bit ottenuti vengono messi nella XOR con la chiave `K_i` (anch’essa di 48 bit), ottenendo una nuova sequenza di 48 bit suddivisa in 8 sotto blocchi da 6 bit ciascuno. Queste 8 stringhe vengono dunque date in ingresso alle 8 S-BO, il cui compito è l’inverso dell’espansione, in quanto comprimono le stringhe in input dando in output 8 stringhe da 4 bit ciascuna (per un totale di 32 bit). Quest’ultima operazione è il punto cruciale della sicurezza dell’intero DES, in quanto introduce il fattore casualità, essendo l’unica **operazione non lineare** in tutto l’algoritmo.
	5) Viene effettuata la permutazione finale, utilizzando un'altra matrice si permutazione e procedendo in modo analogo alla permutazione iniziale;
	6) Vengono invertite le posizioni $S_i$ e $D_i$ per predisporre il blocco cifrato alla successiva decifrazione usando lo stesso algoritmo denominato $DES^{-1}$, esso replica gli stessi passi invertendo però il ruolo di  $S_i$ e $D_i$ e utilizzando le chiavi in ordine inverso, in modo da ritornare al messaggio in chiaro;
- Output: il testo cifrato viene suddiviso in blocchi di dimensione fissa pari a 64 bit;

Il DES è però il più semplice tra gli algoritmi di crittografia, si può ovviare al problema in diversi modi: il primo è il Triple DES, ovvero un algoritmo che richiede tre chiavi di cifratura che vengono utilizzate per applicare tre volte il DES. Esso utilizza chiavi da 192 bit (128 effettivi e 64 di parità). Il processo di cifratura è diviso in tre parti:

- Si applica la prima chiave al testo in chiaro per ottenere quello cifrato (Crypt);
- Si applica la seconda chiave al testo cifrato per decifrarlo, ma visto che si utilizza una chiave diversa dalla corretta il testo in chiaro è a sua volta cifrato (Decrypt);
- Si applica la terza chiave al nuovo testo (Crypt);
Il procedimento inverso che viene utilizzato per decifrare il testo cifrato è l'esatto opposto.

Il secondo metodo per ovviare ai problemi del DES è quello di creare degli algoritmi che derivano dal DES, ma che si diversificano da esso per risolverne le principali problematiche, i principali algoritmi sono:

- IDEA (International Data Encryption Algorithm), con blocchi a 64 bit e chiavi a 128, sviluppato dal Poli di Zurigo e pubblicato nel 91'. Viene raccomandato per la sua grande robustezza e tutt'oggi è ancora inviolato;
- AES (Advanced Encryption Standard), con blocchi a 128 bit e chiavi a 128, 192 e 256 bit, sviluppato come standard del governo USA. Si tratta di un algoritmo molto veloce, relativamente semplice da implementare, richiede poca memoria e offre un buon livello di protezione. Interessante notare come esso si basa su una rete a sostituzione e permutazione e non è una rete di Feistel;
- CAST (Carlisle Adams and Stafford Tavares), con blocchi da 64 o 128 bit e chiavi a 128 e 256 bit, ne esistono due versioni: CAST-128 e CAST-256;

---

*L'algoritmo RSA*

RSA è un algoritmo di crittografia asimmetrica inventato nel 1977. La sua particolarità è l’uso di due chiavi diverse: una pubblica per cifrare i messaggi e una privata per decifrarli. Questo sistema è considerato sicuro perché, anche conoscendo la chiave pubblica, è estremamente difficile risalire a quella privata. La sicurezza dell’algoritmo si basa sulla difficoltà di fattorizzare un numero molto grande ottenuto moltiplicando due numeri primi. Tuttavia, rispetto agli algoritmi simmetrici, l’RSA è molto più lento e consuma più risorse. Per questo motivo, oggi si tende a usare l’RSA solo per proteggere lo scambio della chiave simmetrica, e poi si usa quest’ultima per cifrare realmente i dati, ottenendo così sia sicurezza che velocità. Vediamo ora in modo schematico come funziona RSA.

Generazione delle chiavi:
- Si scelgono due numeri primi grandi, p e q.
- Si calcola n = p × q.
- Si calcola ϕ(n) = (p − 1)(q − 1).
- Si sceglie un numero e, di solito 65537, che sia coprimo con ϕ(n).
- Si calcola d, cioè l’inverso di e modulo ϕ(n).
- Le chiavi risultanti sono:
  - Chiave pubblica: (e, n)
  - Chiave privata: (d, n)

Crittografia:
- Si prende il messaggio m (convertito in numero).
- Si calcola c = m^e mod n usando la chiave pubblica.
- Il risultato c è il messaggio cifrato.

Decrittografia:
- Si prende il messaggio cifrato c.
- Si calcola m = c^d mod n usando la chiave privata.
- Il risultato m è il messaggio originale.

In sintesi, RSA è molto sicuro ma lento, quindi oggi viene usato soprattutto per scambiare le chiavi simmetriche, affidando la cifratura dei dati veri e propri ad algoritmi più rapidi.

---

*La Firma Digitale e gli Enti Certificatori*

Fina dal 97', la firma digitale ha valore giuridico, in quanto è l'equivalente elettronico della tradizionale firma autografata su carta. Essa è basata su un sistema a chiavi asimmetriche, siccome di per se non è in grado di garantire la reale identità del firmatario è previsto l'intervento di terze parti fidate, i certificatori che verificano l'identità di un soggetto e la corrispondenza con la titolarità della chiave pubblica e attestano tali informazioni mediante l'emissione del certificato digitale.

l file che viene firmato digitalmente dev’essere certificato dall’ente certificatore prima del
suo invio. Il nostro ordinamento prevede l’utilizzo di 3 formati per produrre file firmati digitalmente:

- pkcs#7 (noto come p7m), è un formato in uso dal 1999 ed è quello che le Pubbliche Amministrazioni sono obbligate ad accettare;
- PDF, sottoscritto con protocollo d’intesa tra Adobe e il CNIPA (Centro Nazionale per l’Informatica nella Pubblica Amministrazione) il 16 febbraio 2006, al fine di introdurre la possibilità di utilizzare il formato di firma digitale definito nelle specifiche PDF, attraverso la RFC 3778;
- XML, è il formato più diffuso nei settori bancario e sanitario, questo linguaggio è molto diffuso nella gestione elettronica dei flussi di dati;

Per generare una firma digitale c’è bisogno di un kit di firma digitale composto dal dispositivo sicuro e dal software di firma. L’algoritmo di apposizione della firma digitale prevede la creazione di un’impronta (message digest) attraverso la funzione di hash.