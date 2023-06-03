---
Data: 3rd June 2023
Descrizione: Spiegazione query sql
---
## Alcuni dei comandi più importanti

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

###### Select Statement
```sql
-- sintassi --
SELECT column1, column2, ... 
FROM table_name;

SELECT * FROM table_name;

-- Con DISTINCT non ci saranno doppioni nel risultato --
SELECT DISTINCT Country FROM Customers;

-- COUNT(DISTINCT) restituisce il numero di record distinti e differenti --
SELECT COUNT(DISTINCT Country) FROM Customers;
```

###### Where Clause
```sql
SELECT column1, column2, ...  
FROM table_name 
WHERE condition;

WHERE Country='Mexico';
WHERE CustomerID=1;
```