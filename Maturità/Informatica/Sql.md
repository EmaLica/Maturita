---
Data: 3rd June 2023
Descrizione: Spiegazione sql
---
# Alcuni dei comandi più importanti
- `SELECT` - estrae i dati da un database
- `UPDATE` - aggiorna i dati in un database
- `DELETE` - elimina i dati da un database
- `INSERT INTO` - inserisce nuovi dati in un database
- `CREATE DATABASE` - crea un nuovo database
- `ALTER DATABASE` - modifica un database
- `CREATE TABLE` - crea una nuova tabella
- `ALTER TABLE` - modifica una tabella
- `DROP TABLE` - elimina una tabella
- `CREATE INDEX` - crea un indice (chiave di ricerca)
- `DROP INDEX` - elimina un indice

## Query Language
Il linguaggio di interrogazione (Query Language o QL) viene utilizzato per estrarre dati da una o più tabelle all'interno di un database.
**Selezione da una o più tabelle**:
```sql
SELECT colonna1, colonna2, ...
FROM tabella1, tabella2, ...
WHERE condizione;
```
**Operazioni relazionali**:
```text
Le operazioni relazionali comuni utilizzate nelle clausole WHERE includono:

- Uguaglianza: =
- Disuguaglianza: <> o !=
- Maggiore di: >
- Minore di: <
- Maggiore o uguale a: >=
- Minore o uguale a: <=
```
**Funzioni di aggregazione**:
Le funzioni di aggregazione vengono utilizzate per calcolare valori aggregati su un insieme di dati. Alcune funzioni di aggregazione comuni includono:
- COUNT: restituisce il numero di record.
- SUM: restituisce la somma dei valori.
- AVG: restituisce la media dei valori.
- MAX: restituisce il valore massimo.
- MIN: restituisce il valore minimo. Esempio:
```sql
SELECT COUNT(*) AS Numero_Record, SUM(Quantita) AS Totale_Quantita
FROM Tabella
WHERE condizione;
```
**Ordinamento**:
La clausola ORDER BY viene utilizzata per ordinare i risultati in base a una o più colonne. Si può specificare l'ordinamento ascendente (ASC) o discendente (DESC). Esempio:
```sql
SELECT colonna1, colonna2, ...
FROM Tabella
ORDER BY colonna1 ASC, colonna2 DESC;
```
**Raggruppamento**:
La clausola GROUP BY viene utilizzata per raggruppare i risultati in base a una o più colonne. Viene spesso utilizzata in combinazione con le funzioni di aggregazione. Esempio:
```sql
SELECT colonna1, COUNT(*) AS Numero_Record
FROM Tabella
GROUP BY colonna1;
```
## Crud
### Select Statement
```sql
-- sintassi --
SELECT column1, column2, ... 
FROM table_name;

SELECT * FROM table_name;

-- Con DISTINCT non ci saranno doppioni nel risultato --
SELECT DISTINCT Country FROM Customers;

-- COUNT(DISTINCT) restituisce il numero di record distinti e differenti --
SELECT COUNT(DISTINCT Country) FROM Customers;

SELECT colonna1, colonna2
FROM nome_tabella
WHERE condizione;
```
### Insert
```sql
INSERT INTO Prodotti (Nome, Prezzo, Categoria)
VALUES ('Smartphone', 500, 'Elettronica');
```
### Update
```sql
UPDATE Prodotti
SET Prezzo = 600
WHERE Categoria = 'Elettronica';
```
### Delete
```sql
DELETE FROM Clienti
WHERE Stato = 'Inattivo';
```
## Clausole
### Join
Le join sono operazioni utilizzate nel linguaggio SQL per combinare dati provenienti da due o più tabelle basandosi su una condizione di correlazione tra di esse. Le join consentono di ottenere un unico set di risultati che includa dati correlati da più fonti. Ecco i tipi di join più comuni:

1. **INNER JOIN**: Restituisce solo le righe che hanno una corrispondenza tra le tabelle coinvolte nella clausola JOIN. Le righe che non soddisfano la condizione di join vengono escluse dal risultato.
2. **LEFT JOIN (o LEFT OUTER JOIN)**: Restituisce tutte le righe dalla tabella di sinistra (prima tabella menzionata nella clausola JOIN) e le righe corrispondenti dalla tabella di destra (seconda tabella menzionata). Se non c'è corrispondenza, le colonne della tabella di destra conterranno valori NULL.
3. **RIGHT JOIN (o RIGHT OUTER JOIN)**: Restituisce tutte le righe dalla tabella di destra e le righe corrispondenti dalla tabella di sinistra. Se non c'è corrispondenza, le colonne della tabella di sinistra conterranno valori NULL.
4. **FULL JOIN (o FULL OUTER JOIN)**: Restituisce tutte le righe da entrambe le tabelle coinvolte nella clausola JOIN. Se non c'è corrispondenza, le colonne senza corrispondenza conterranno valori NULL.
5. **CROSS JOIN**: Restituisce il prodotto cartesiano tra le righe delle tabelle coinvolte nella clausola JOIN. In altre parole, restituisce tutte le possibili combinazioni tra le righe delle tabelle senza basarsi su una condizione di join.
### View
In SQL, una vista è un oggetto virtuale che rappresenta una visualizzazione specifica di dati all'interno di una o più tabelle. Una vista non contiene dati effettivi, ma è una rappresentazione strutturata dei dati presenti nelle tabelle sottostanti. Le viste consentono di semplificare le query complesse, nascondere la complessità della struttura delle tabelle e fornire una visione personalizzata dei dati per gli utenti.
```sql
CREATE VIEW vista_clienti_ordini AS
SELECT c.id_cliente, c.nome_cliente, SUM(o.importo) AS totale_ordini
FROM clienti c
JOIN ordini o ON c.id_cliente = o.id_cliente
GROUP BY c.id_cliente, c.nome_cliente;
```
### Group by
Supponiamo di avere una tabella "Ordini" con le colonne "Prodotto" e "Quantità". Vogliamo ottenere il numero totale di ordini per ciascun prodotto.
```sql
SELECT Prodotto, COUNT(*) as Numero_Ordini FROM Ordini GROUP BY Prodotto;
--Questo restituirà una lista dei prodotti presenti nella tabella "Ordini" e il numero totale di ordini per ciascun prodotto.--
```
### Having
Utilizzando lo stesso esempio precedente, vogliamo filtrare solo i prodotti con un numero di ordini superiore a 5.
```sql
SELECT Prodotto, COUNT(*) as Numero_Ordini FROM Ordini GROUP BY Prodotto HAVING COUNT(*) > 5;
-- Questo restituirà solo i prodotti che hanno un numero di ordini maggiore di 5.--
```
### Order by
Supponiamo di avere una tabella "Prodotti" con le colonne "Nome" e "Prezzo". Vogliamo ottenere i prodotti ordinati in base al prezzo in ordine crescente.
```sql
SELECT * FROM Prodotti ORDER BY Prezzo ASC;
--Questo restituirà tutti i record della tabella "Prodotti", ordinati in base al prezzo in modo crescente.--
```
### Delete on cascade
Supponiamo di avere due tabelle "Clienti" e "Ordini" collegate da una chiave esterna "ClienteID" nella tabella "Ordini". Vogliamo eliminare un cliente e, automaticamente, eliminare tutti i suoi ordini associati.
```sql
DELETE FROM Clienti WHERE ClienteID = 1;
--Utilizzando la clausola DELETE ON CASCADE nella definizione della chiave esterna tra le tabelle, questa query eliminerà il cliente con ID 1 dalla tabella "Clienti" e automaticamente eliminerà anche tutti i suoi ordini associati dalla tabella "Ordini".--
```
## Vincoli
**Vincolo di chiave primaria**:
```sql
CREATE TABLE prodotti (
  id_prodotto INT,
  nome VARCHAR(50),
  prezzo DECIMAL(10, 2),
  PRIMARY KEY (id_prodotto)
);
```
**Vincolo di chiave esterna**:
```sql
CREATE TABLE clienti (
  id_cliente INT,
  nome VARCHAR(50),
  PRIMARY KEY (id_cliente)
);

CREATE TABLE ordini (
  id_ordine INT,
  id_cliente INT,
  importo DECIMAL(10, 2),
  FOREIGN KEY (id_cliente) REFERENCES clienti(id_cliente)
);
```
**Vincolo di unicità**:
```sql
-- Il vincolo UNIQUE sulla colonna "Email" assicura che ogni valore inserito in quella colonna sia unico all'interno della tabella.--
CREATE TABLE Utenti (
  ID INT,
  Nome VARCHAR(50),
  Email VARCHAR(100) UNIQUE
);
```
**Vincolo di controllo**:
```sql
CREATE TABLE Prodotti (
  ID INT,
  Nome VARCHAR(50),
  Prezzo DECIMAL(10,2),
  Quantita INT,
  CHECK (Prezzo >= 0 AND Quantita >= 0)
);
```
**Vincolo di not null**:
```sql
CREATE TABLE Studenti (
  Matricola INT NOT NULL,
  Nome VARCHAR(50),
  Cognome VARCHAR(50),
  AnnoIscrizione INT
);
```
**Vincolo default**:
```sql
CREATE TABLE persone (
  id INT,
  nome VARCHAR(50) DEFAULT 'Anonimo',
  email VARCHAR(100) DEFAULT 'info@example.com'
);
```
**Vincolo di identità**:
```sql
ALTER TABLE miaTabella
MODIFY id INT AUTO_INCREMENT;
```
**Vincolo index**:
```sql
--Un vincolo INDEX in SQL viene utilizzato per creare un indice su una o più colonne di una tabella al fine di migliorare le prestazioni delle query di ricerca e ordinamento.--
CREATE TABLE Users (
  id INT PRIMARY KEY,
  username VARCHAR(50) NOT NULL,
  email VARCHAR(100) UNIQUE,
  CONSTRAINT idx_UsernameIndex INDEX (username)
);
```

## Queries
### Semplice
Questa query seleziona i nomi, i cognomi e le email degli utenti dalla tabella "utenti" che hanno un'età superiore a 30 anni.
```sql
SELECT nome, cognome, email
FROM utenti
WHERE età > 30;
```
### Media
Questa query calcola il prezzo medio dei prodotti per ogni categoria dalla tabella "prodotti" e restituisce solo le categorie che hanno più di 5 prodotti. Utilizza la funzione di aggregazione AVG per calcolare il prezzo medio e la clausola HAVING per filtrare i risultati in base al conteggio dei prodotti.
```sql
SELECT categoria, AVG(prezzo) AS prezzo_medio
FROM prodotti
GROUP BY categoria
HAVING COUNT(*) > 5;
```
### Difficile
Questa query seleziona l'ID, il nome e l'email degli utenti dalla tabella "utenti" che non hanno effettuato alcun ordine a partire dal 1° gennaio 2022. Utilizza una **subquery** per ottenere l'elenco degli utenti che hanno effettuato ordini dopo la data specificata e li esclude dalla query principale utilizzando la clausola NOT IN.
```sql
SELECT utente_id, nome, email
FROM utenti
WHERE utente_id NOT IN (
  SELECT utente_id
  FROM ordini
  WHERE data_ordine >= '2022-01-01'
);
```
### Con JOIN
Questa query seleziona il nome del cliente, il numero dell'ordine e la data dell'ordine dalla tabella "ordini" e "clienti". Utilizza la clausola JOIN per unire le due tabelle in base all'attributo "cliente_id" nella tabella "ordini" e all'attributo "id" nella tabella "clienti". La clausola WHERE filtra solo gli ordini con stato "Consegnato", mentre la clausola ORDER BY ordina i risultati in base alla data dell'ordine in ordine decrescente.
```sql
SELECT c.nome, o.numero_ordine, o.data_ordine
FROM ordini o
JOIN clienti c ON o.cliente_id = c.id
WHERE o.stato = 'Consegnato'
ORDER BY o.data_ordine DESC;
```