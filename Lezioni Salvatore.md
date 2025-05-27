---
connections:
  - "[[Informatica]]"
---
## Modello E/R

![[ProvaEsame1.png]]

- [ ] Viaggiatori
- [ ] Percorsi
- [x] Utenti
- [x] Autisti 
- [x] Viaggi
- [ ] Passeggero 
- [x] Prenotazioni
- [x] Feedback

![[modelloERSalvatore.png]]

## Utenti

- UtentiCF {PK}
- Nome
- Cognome
- Fotografia
- TipoDiUtente
- DocumentoIdentità
- Telefono
- Email
- Password


## Autisti

- NumeroPatente {PK}
- UtentiID {FK}
- ScadenzaPatente


## Automobili

- AutomobileID {PK}
- NumeroPatente {FK}
- Modello
- Marca


## Viaggi

- ViaggioID {PK}
- CittàPartenza
- CittàArrivo
- OrarioPartenza
- DataPartenza
- AutistaID {FK}
- Costo
- StatoPrenotazione


## Prenotazioni

- PrenotazioneID {PK}
- PasseggeroID {FK}
- AutistaID {FK}


Feedback

- FeedbackID {PK}
- MittenteID {FK}
- DestinatarioID {FK}
- Messaggio
- Voto

---

## Modello Logico

Lo saltiamo per velocità, 1 linea primary key, 2 linee foreign key

---

## Modello Fisico

| Entità  | Parametro         | Vincolo                   | Formato   | Dimensione |
| ------- | ----------------- | ------------------------- | --------- | ---------- |
| Utenti  | UtentiCF          | Primary Key               | Small Int | //         |
|         | Nome              | Not Null                  | Varchar   | 50         |
|         | Cognome           | Not Null                  | Varchar   | 20         |
|         | Fotografia        | Not Null                  | Varchar   | //         |
|         | TipoDiUtente      | Enum("Utente", "Autista") | Varchar   | 7          |
|         | DocumentoIdentità | Not Null                  | Varchar   | 7          |
|         | Telefono          | Not Null                  | Varchar   | 10         |
|         | Email             | Not Null                  | Varchar   | 50         |
|         | Password          | Not Null                  | Varchar   | 30         |
| Autisti | ...               | ...                       | ...       | ...        |
|         | ...               | ...                       | ...       | ...        |

---

![[ProvaEsame2.png]]

## Prima Query

```SQL
SELECT u.Nome, u.Cognome, v.OrarioPartenza, a.* , v.Costo
FROM Utenti as u, Viaggi as v, Automobili as a, Autisti as au
WHERE a.NumeroPatente = au.NumeroPatente
AND au.UtentiID = u.UtentiCF
AND v.AutistaID = au.NumeroPatente
AND v.CittàPartenza = ["cittàP"]
AND v.CittàArrivo = ["cittàA"]
AND v.DataPartenza = ["dataP"]
AND v.StatoPrenotazione = "Chiuso"
ORDER BY v.OrarioPartenza ASC
```