---
Data: 14th June 2023
Descrizione: 
---
# Sistemi informativi, database, dbms
#### Sistema informativo
Quali sono i suoi compiti?
**1.** Raccolta, acquisizione
**2.** Archiviazione, conservazione
**3.** Elaborazione, trasformazione, produzione
**4.** Distribuzione, comunicazione, scambio
- Componente di una organizzazione che gestisce le informazioni di interesse (cioè utilizzate per il perseguimento degli scopi dell’organizzazione)
- Ogni organizzazione ha un sistema informativo, eventualmente non esplicitato nella struttura
- Il sistema informativo è di supporto ad altri sottosistemi, e va quindi studiato nel contesto in cui è inserito
#### Sistema informatico
- Porzione automatizzata del sistema informativo: la parte del sistema informativo che gestisce informazioni con tecnologia informatica
#### Dato e informazione
**informazione**: notizia, dato o elemento che consente di avere conoscenza più o meno esatta di fatti, situazioni, modi di essere.
**dato**: ciò che è immediatamente presente alla conoscenza, prima di ogni elaborazione; (in informatica) elementi di informazione costituiti da simboli che debbono essere elaborati
#### Database
Un database **è un sistema organizzato per la memorizzazione e la gestione di dati strutturati**, che possono essere **facilmente accessibili, gestiti e aggiornati**. Un database consente di archiviare grandi quantità di informazioni in modo strutturato e coerente, facilitando la ricerca, l'organizzazione e l'analisi dei dati. Un database è costituito da una collezione di dati correlati tra loro, organizzati secondo uno schema predefinito. I **dati sono generalmente organizzati in tabelle**, che **rappresentano entità o concetti specifici**, **e le relazioni** tra le tabelle sono **definite attraverso chiavi primarie e chiavi esterne**. Questa struttura relazionale consente di collegare i dati in modo logico e di recuperare le informazioni in base alle relazioni tra di esse.
#### Dbms
**Il DBMS è un software specifico** che svolge un ruolo di **interfacciamento tra le
applicazioni** utilizzate dall'utente **e la base di dati**, grazie al DBMS, le applicazioni
accedono soltanto alla rappresenta logica di quest'ultima, eliminando quindi il problema della dipendenza fisica. **L'organizzazione fisica** è infatti gestita dal DBMS **in modo trasparente** sia all'utente che al programmatore.

Il DBMS si occupa di implementare il modello logico, manipolare e interrogare la base di dati, controllarne l'integrità e proteggerla (sicurezza). Per fare queste operazioni, esso si serve di diversi linguaggi:

- **DDL** (Data Definition Language): agisce sulla struttura dei “contenitori” (le tabelle)
- **DML** (Data Manipulation Language): permette di inserire, modificare e cancellare i dati
- **DCL** (Data Control Language): fissa i vincoli di integrità, controlla e gestisce gli accessi e i permessi
- **QL**(Query Language): linguaggio per interrogare il database (per leggere i dati)
- **DMCL** (Data Media Control Language): si occupa del controllo dei supporti di memoria fisici e dell’organizzazione fisica della base di dati
## Definizioni sui database relazionali
- **Dominio**: insieme dei valori che possono essere assunti da un attributo (una colonna) di una relazione.
- **Relazione**: prodotto cartesiano di uno o più insiemi. 
- **Tupla**: una tra le possibili combinazioni che fanno parte della relazione.
- **Grado**: numero di attributi di una relazione.
- **Cardinalità**: numero di righe (tuple) di una tabella
- **Chiave**: insieme finito di uno o più attributi che identificano univocamente una tupla. In particolare, la **chiave primaria** può essere semplice o composta da più attributi (da evitare perché onerosa da implementare).
- **Chiave esterna**: attributo o insieme di attributi che coincidono con la chiave primaria di una tupla di un’altra relazione, a cui la tupla in cui è presenta la chiave esterna è associata. Il dominio della chiave primaria della chiave esterna deve essere comune.
## Progettazione di un DB 
La progettazione di un database coinvolge diversi livelli di astrazione, tra cui la progettazione concettuale, logica e fisica. Ognuno di questi livelli ha uno scopo specifico e contribuisce alla creazione di un database ben strutturato e efficiente.
1. **Progettazione Concettuale**: La progettazione concettuale è il primo livello di progettazione e si concentra sulla comprensione dei requisiti del sistema e sulla creazione di un modello concettuale dei dati. Durante questa fase, gli analisti di sistema e gli utenti finali collaborano per identificare le entità, gli attributi e le relazioni chiave che rappresentano il dominio del problema
2. **Progettazione Logica**: La progettazione logica traduce lo schema concettuale in uno schema logico che può essere implementato in un database specifico. Durante questa fase, si definiscono le tabelle, gli attributi, le relazioni e i vincoli di integrità referenziale. Si utilizzano modelli di dati specifici, come il modello relazionale, per rappresentare la struttura dei dati in modo più dettagliato.
3. **Progettazione Fisica**: La progettazione fisica si concentra sull'implementazione concreta dello schema logico all'interno di un DBMS specifico. Durante questa fase, si considerano aspetti come l'ottimizzazione delle prestazioni, la distribuzione dei dati, l'allocazione dello spazio su disco e la gestione delle transazioni.
## Progettazione Concettuale ER
[[Guida Modello Entity-Relationship]]

## Proprietà delle tabelle relazionali
Le tabelle relazionali sono una componente fondamentale dei database relazionali e possiedono le seguenti proprietà:

1. **Struttura tabellare**: I dati sono organizzati in tabelle con righe (tuple) e colonne (attributi).
2. **Identificatore unico**: Ogni tabella ha una chiave primaria che identifica in modo univoco ogni record.
3. **Attributi**: Le colonne rappresentano gli attributi dei dati e hanno un nome e un tipo di dato associato.
4. **Relazioni tra tabelle**: Le tabelle possono essere collegate tra loro attraverso relazioni utilizzando chiavi primarie e chiavi esterne.
5. **Integrità dei dati**: I vincoli di integrità garantiscono la coerenza e l'integrità dei dati, come l'unicità dei record e le relazioni tra le tabelle.
6. **Normalizzazione**: Le tabelle possono essere normalizzate per eliminare ridondanze e migliorare l'organizzazione dei dati.
7. **Query e manipolazione dei dati**: Le tabelle consentono l'esecuzione di operazioni di interrogazione e manipolazione dei dati tramite comandi DML come SELECT, UPDATE, INSERT e DELETE.

## Integrità dei dati
L'integrità dei dati nel database è garantita attraverso diverse regole e meccanismi:

- La chiave primaria garantisce l'unicità di ogni record all'interno di una tabella, prevenendo l'inserimento di duplicati.
- Le chiavi esterne stabiliscono relazioni tra tabelle e assicurano la coerenza dei dati. Le chiavi esterne fanno riferimento alle chiavi primarie di altre tabelle, evitando relazioni inconsistenti o orfane.
- I vincoli di integrità referenziale definiscono le regole per le relazioni tra le tabelle, come ad esempio l'obbligatorietà di una corrispondenza tra le chiavi primarie e le chiavi esterne.
- Le regole di dominio specificano i tipi di dati ammissibili per gli attributi, come numeri interi o stringhe di una certa lunghezza. Queste regole impediscono l'inserimento di dati non validi o incoerenti.
- Le regole di convalida consentono di definire criteri specifici che i dati devono soddisfare, come ad esempio un campo "Età" maggiore di 18. Le regole di convalida verificano che i dati rispettino tali criteri prima di essere inseriti o modificati.
## Regole di inserzione

## Vincoli di integrità 
I vincoli sono regole o restrizioni che vengono applicate alle tabelle o ai dati di un database per garantire l'integrità dei dati. Alcuni esempi di vincoli comuni includono:
1. **Vincolo di chiave primaria**: Impone l'unicità e l'identificazione univoca di ogni record in una tabella.
2. **Vincolo di chiave esterna**: Stabilisce una relazione tra due tabelle, garantendo che i valori di un attributo facciano riferimento a valori validi in un'altra tabella.
3. **Vincolo di unicità**: Assicura che i valori di un attributo o di un insieme di attributi siano unici all'interno della tabella.
4. **Vincolo di controllo**: Definisce una condizione che deve essere soddisfatta per ogni record nella tabella.
5. **Vincolo di not null**: Impedisce l'inserimento di valori NULL per un attributo, garantendo che l'attributo abbia sempre un valore valido.
## Dipendenze funzionali
Una dipendenza funzionale può essere espressa come A -> B, dove A e B sono insiemi di attributi. Questa notazione indica che il valore di B è determinato dal valore di A. In altre parole, se si conosce il valore di A, allora si può determinare univocamente il valore di B.

Esistono diversi tipi di dipendenze funzionali:

1. **Dipendenza funzionale completa (FD)**: Si verifica quando il valore di ogni attributo nella tabella è determinato dal valore di ogni altro attributo. Ad esempio, se si ha una tabella con gli attributi "Nome" e "Età", il nome determina in modo completo l'età delle persone, e viceversa.
2. **Dipendenza funzionale parziale (PD)**: Si verifica quando il valore di un attributo è determinato solo da un sottoinsieme degli attributi della tabella. Ad esempio, se si ha una tabella con gli attributi "Nome", "Cognome" e "Codice Postale", il codice postale dipende solo dal nome e non dal cognome.
3. **Dipendenza funzionale transitiva**: Si verifica quando il valore di un attributo è determinato da un altro attributo attraverso una catena di dipendenze funzionali. Ad esempio, se si ha una tabella con gli attributi "Nome", "Città" e "Stato", e si conosce il nome di una persona, si può determinare la città in cui vive e, di conseguenza, lo stato.

Le dipendenze funzionali sono importanti perché possono essere utilizzate per progettare e ottimizzare il database. Consentono di identificare le chiavi primarie, normalizzare il database per ridurre la ridondanza dei dati e stabilire vincoli di integrità referenziale per mantenere la coerenza dei dati.

## Normalizzazione
La normalizzazione è un processo di progettazione dei database relazionali che mira a ridurre la ridondanza dei dati e a migliorare l'integrità dei dati. La normalizzazione viene eseguita in diverse fasi, rappresentate dalle normal forms (forme normali). Le forme normali più comuni sono:

1. **Prima forma normale (1FN)**: La 1FN richiede che ogni attributo di una tabella abbia un singolo valore atomico. Ciò significa che non ci dovrebbero essere valori multipli, separati da virgole o altro delimitatore, in una singola cella dell'attributo. Inoltre, ogni tabella deve avere una chiave primaria che identifica in modo univoco ogni record.
2. **Seconda forma normale (2FN)**: La 2FN richiede che una tabella sia in 1FN e che ogni attributo non chiave dipenda completamente dalla chiave primaria. In altre parole, se un attributo dipende solo da una parte della chiave primaria, dovrebbe essere spostato in una tabella separata. Ciò riduce la ridondanza dei dati e facilita l'aggiornamento e la gestione dei dati.
3. **Terza forma normale (3FN)**: La 3FN richiede che una tabella sia in 2FN e che non ci siano dipendenze funzionali transitive tra gli attributi non chiave. Ciò significa che se un attributo A dipende da un attributo B, che a sua volta dipende dalla chiave primaria, allora A dovrebbe essere spostato in una tabella separata. La 3FN contribuisce a eliminare la ridondanza dei dati e a migliorare la struttura del database.
È importante notare che **esistono anche altre forme normali**, come la forma normale di **Boyce-Codd (BCNF)** e la forma normale di quarta **(4NF)** e quinta **(5NF)**.
La normalizzazione è un processo iterativo, in cui si analizzano le dipendenze funzionali e si suddividono le tabelle in base a tali dipendenze per ottenere una struttura ottimale del database. Il risultato finale è un database ben strutturato, senza ridondanze e con relazioni corrette tra le tabelle, che facilita la gestione dei dati e migliora le prestazioni del sistema.

# DDL, DML E QL
#### Data Definition Language
La Data Definition Language (DDL) è un linguaggio utilizzato per definire la struttura e le caratteristiche di un database. La DDL consente di creare, modificare ed eliminare oggetti come tabelle, domini e vincoli di integrità referenziale.
**Creazione tabelle**:
```sql
CREATE TABLE Utenti (
    ID INT PRIMARY KEY,
    Nome VARCHAR(50),
    Email VARCHAR(100) UNIQUE,
    DataNascita DATE
);
```
**Modifica tabelle**:
```sql
-- aggiungo un nuovo attributo alla tabella --
ALTER TABLE Utenti
ADD Telefono VARCHAR(20);
```
**Eliminare tabelle**:
```sql
-- per definire un dominio "Stato" che può assumere i valori "Attivo" o "Inattivo", si può utilizzare il comando CREATE DOMAIN --
DROP TABLE Utenti;
```
**Definizione di domini**:
```sql
CREATE DOMAIN Stato AS VARCHAR(10) CHECK (VALUE IN ('Attivo', 'Inattivo'));
```
**Vincoli di integrità referenziale**: I vincoli di integrità referenziale definiscono le relazioni tra tabelle e garantiscono la coerenza dei dati. Ad esempio, si può specificare che un attributo in una tabella deve fare riferimento a un valore presente in un'altra tabella. La DDL permette di definire questi vincoli. Ad esempio, per aggiungere un vincolo di integrità referenziale tra la tabella "Ordini" e la tabella "Clienti", in modo che l'attributo "ClienteID" in "Ordini" faccia riferimento a un valore presente in "Clienti", si può utilizzare il comando ALTER TABLE:
```sql
ALTER TABLE Ordini
ADD CONSTRAINT FK_Ordini_Clienti
FOREIGN KEY (ClienteID) REFERENCES Clienti(ID);
```
#### Data Manipulation Language
Il linguaggio di manipolazione dei dati (Data Manipulation Language o DML) è utilizzato per inserire, cancellare e aggiornare i record delle tabelle all'interno di un database.
**Inserimento**:
```sql
INSERT INTO Prodotti (Nome, Prezzo, Categoria)
VALUES ('Smartphone', 500, 'Elettronica');
```
**Cancellazione**:
```sql
DELETE FROM Clienti
WHERE Stato = 'Inattivo';
```
**Aggiornamento**:
```sql
UPDATE Prodotti
SET Prezzo = 600
WHERE Categoria = 'Elettronica';
```
#### Query Language [[Sql]]
Il linguaggio di interrogazione (Query Language o QL) viene utilizzato per estrarre dati da una o più tabelle all'interno di un database.
