---
connections:
  - "[[PON Informatica]]"
source:
  - PON
---
# Esercizio 1

| Matricola | NomeStudente | Corso      | DocenteCorso  | Aule         |
| --------- | ------------ | ---------- | ------------- | ------------ |
| 101       | Marco Rossi  | Matematica | Prof. Bianchi | Aula1, Aula2 |
| 102       | Lucia Neri   | Storia     | Prof. Verdi   | Aula3        |


### Normalizzazione

Aule(AulaID {PK}, Denominazione, CorsoID {FK}, MStudente {FK})
Corso(CorsoID {PK}, NomeMateria, Docente)
Studente(Matricola {PK}, Nome, Cognome)


### Opzione 1
![[Quarta Lezione PON.png]]

### Opzione 2
![[Quarta Lezione PON 2.png]]

---

# Esercizio 2

| IDVendita | Data     | IDCliente | NomeCliente   | CittàCliente | IDProdotto | NomeProdotto | PrezzoUnitario | Quantità | CategoriaProdotto |
| --------- | -------- | --------- | ------------- | ------------ | ---------- | ------------ | -------------- | -------- | ----------------- |
| 5001      | 24/10/01 | c100      | Mario Bianchi | Milano       | p10        | Penna blu    | 1.00           | 10       | Cancelleria       |
| 5001      | 24/10/01 | c100      | Mario Bianchi | Milano       | p20        | Quaderno     | 2.00           | 5        | Cartoleria        |
> Prima forma normale


Vendita(IDVendita {PK}, Data, IDCliente {FK}, IDProdotto {FK})
Cliente(IDCliente {PK}, NomeCliente, CittàCliente)
Prodotto(IDProdotto {PK}, NomeProdotto, PrezzoUnitario, Categoria)
DettaglioVendita(IDDettaglio {PK}, Quantità, IDVendita {FK})