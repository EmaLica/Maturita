---
Data: 14th June 2023
Descrizione: spiegazione passo passo Entity-Relationship
---
### Teoria modello ER
Un diagramma ER (Entity-Relationship) è **un tipo di diagramma utilizzato per rappresentare la struttura concettuale di un sistema di database**. È una rappresentazione visuale dei concetti e delle relazioni tra gli entità del sistema. 
I diagrammi ER sono ampiamente utilizzati nella **progettazione dei database** per aiutare a identificare le entità, gli attributi e le relazioni chiave che costituiranno lo schema del database. Questi diagrammi sono una parte essenziale del processo di progettazione dei database e **forniscono una rappresentazione chiara e intuitiva delle strutture e delle interconnessioni dei dati nel sistema**.

#### In fase di progettazione:
1. **Analisi dei requisiti** – scopo: individuare e studiare le funzionalità che il sistema dovrà fornire. Raccolta e studio delle funzionalità che il sistema dovrà avere. Comporta l’interazione con gli utenti del sistema e si conclude in una descrizione informale dei requisiti che il sistema dovrà avere
3. **Progettazione** – scopo: (a) strutturare e organizzare i dati (b) caratteristiche dei programmi applicativi. Ha lo scopo di rappresentare la realtà di interesse in termini di una descrizione precisa e completa ma indipendente dai criteri di rappresentazione usati dal sistema informatico scelto per gestire la base di dati (rappresentazione astratta)
4. **Realizzazione** (implementazione): costruzione del sistema
5. **Collaudo**: verifica del corretto funzionamento del sistema

![[Cattura.png]]
#### Entità, relazioni  e attributi
**Entità**: sono classi di oggetti, che hanno tutti le stesse proprietà ed esistono in modo autonomo; ogni entità è un insieme di oggetti (detti anche istanze o occorrenze).
###### Entità deboli
- Le entità deboli devono partecipare ad una relazione con l’entità proprietario e non hanno ragione di esistere senza il proprietario
- Si definisce **entità debole**, l’entità che **non dispone internamente di attributi sufficienti per definire un identificatore**
- In particolare l’identificatore esterno è formato dalla chiave del proprietario e da un discriminatore, un insieme di attributi dell’entità debole che permette di distinguere le entità deboli tra di loro

**Relazioni**: sono legami logici fra due o più entità. Anche una associazione è un insieme, è l’insieme delle correlazioni fra i singoli elementi delle entità coinvolte.
**Attributi**: Descrivono le proprietà elementari di relazioni e entità che sono di interesse. Un’occorrenza di un’entità o di una relazione sono completamente descritti da tutti i suoi attributi (o dall’unione degli attributi delle entità che compongono la relazione).
###### Dominio degli attributi
Il Dominio di un attributo rappresenta **l’insieme dei valori assunti dall’attributo**.
- per l’attributo nome del cliente, il Dominio può essere l’insieme delle stringhe di lunghezza 20 caratteri
- per il numero di conto, può essere l’insieme di tutti i numeri interi positivi
- (tipicamente, interi, caratteri, stringhe, ecc.)

###### Classificazione degli attributi
**Semplici**: se possono assumere un solo valore
- es. il nome di un cliente
**Multipli**: se prevedono la possibilità di più valori
- es. l’attributo esami sostenuti per uno studente
- L’uso degli attributi multipli è spesso deprecato in quanto non è ben rappresentabile in una base di dati che adotta il metodo relazionale. Al posto degli attributi multipli è incoraggiata la definizione di nuove entità e relazioni tra di esse
**Composti**: quando è possibile scomporli in più elementi
- es. l’indirizzo, che può essere scomposto in via, n. civico, CAP, città
**Opzionali**: quando questi possono non avere un valore definito
- es. n. patente associato ad una persona (che potrebbe non avere la patente)
![[Cattura 1.png]]
![[Cattura 2.png]]
#### Cardinalità delle relazioni
**Per ogni entità** che partecipa a una relazione è possibile **indicare il num. min e max di legami che le sue istanze possono avere** con istanze delle altre entità partecipanti alla medesima relazione
![[Cattura 3.png]]
Esempi:
0:1
0:N
1:1
1:N
#### Associazioni a molte entità
Le associazioni possono collegare più di due entità, per esempio il concetto di pubblicazione, intesa come libro scritto da un certo scrittore per una certa casa editrice, potrebbe essere rappresentato come:
![[Cattura 4.png]]
#### Identificatori
ogni entità è un insieme di oggetti aventi le stesse proprietà, è però necessario poter identificare in modo univoco ciascuna istanza di un’entità (anziché parlare di “persone” talvolta occorre parlare dello specifico “sig. Rossi”)
A. **Identificatore interno**: sottoinsieme di attributi che costituiscono una chiave per l’entità
B. **Identificatore esterno**: quando non è sufficiente utilizzare un sottoinsieme di attributi ma l’entità partecipa a una relazione con cardinalità (1,1), i suoi elementi possono essere identificati tramite tale relazione.
![[Cattura 5.png]]
#### Generalizzazioni o Gerarchie
- Gli **attributi** (proprietà) **del Padre sono ereditati dai Figli**
- Non vanno quindi replicati nello schema, sarebbe un errore! NOTA: Non è vero il viceversa!
- Il **legame logico** che unisce la classe degli attributi comuni (padre) con le sottoclassi specializzate (figli) è la **gerarchia di specializzazione**
Possono essere di due tipi:
- **Totali**
- **Parziali**
![[Cattura 9.png]]
![[Cattura 6.png]]
#### Relazioni ricorsive ![[Cattura 7.png]]![[Cattura 8.png]]
#### Attributi sulle relazioni
- Una relazione può avere degli attributi
- La rappresentazione grafica è la stessa delle entità
![[Immagine 2023-06-19 163500.png]]
#### Vincoli di integrità
- Il modello E-R include una serie di costrutti che permettono di definire dei *vincoli di integrità* sui costrutti già visti
- Queste in altre parole **sono delle proprietà** che occorrenze di **entità e relazioni devono soddisfare** per essere considerate valide
	- Cardinalità delle relazioni
	- Cardinalità degli attributi
	- Identificatori delle entità
	- Generalizzazioni

#### Cardinalità delle relazioni
I **vincoli di cardinalità sulle relazioni** vengono rappresentati con una coppia di numeri **(min, max)** Impone un limite minimo ed un limite massimo al numero di entità a cui un’altra entità può essere associata.
-  0 e 1 per la **cardinalità minima**:
	-  0 ="è opzionale"
	-  1 ="è obbligatoria“

-  1 e N per la **cardinalità massima**:
	- N = “non pone alcun limite”
#### Cardinalità degli attributi
Nel definire il modello concettuale dei dati, può essere utile, sul piano pratico, fornire ulteriori classificazioni per gli attributi, ad esempio, è importante sapere se un **attributo può assumere o meno valori nulli** (ossia non avere valori).
Classificazione:
- **Opzionali**: se la cardinalità minima è 0 (es. n. patente)
- **Monovalore**: se la cardinalità massima è 1 (es.cod_fiscale)
- **Multivalore**: se la cardinalità massima è n (es.telefono)

#### Collassi
Ci sono tre metodi per eliminare le gerarchie:
- **mantenimento delle entità con associazioni**
- **collasso verso l’alto**
- **collasso verso il basso**

Prendiamo come esempio il seguente schema E-R:
![[db31.jpg]]
###### Mantenimento con associazioni
**Tutte le entità vengono mantenute**. Le **entità figlie** vengono **messe in associazione con l’entità padre** e sono identificate esternamente tramite l’associazione. La cardinalità (0,1) indica che per tale associazione l’ entità padre può avere zero o una entità figlio. Mentre (1,1) che l’ entità figlio può avere un solo padre.
![[db32 1.jpg]]
###### Verso l'alto
Il collasso **verso l’alto** riunisce **tutte le entità figlie nell’entità padre**. Otterremo una cosa di questo tipo:
![[db33.jpg]]
E1 ed E2 vengono eliminate e le loro proprietà vengono aggiunte all’entità padre . Gli attributi obbligatori per le entità figlie divengono opzionali per il padre , indicato dalla cardinalità (0,1), con la conseguenza che si avrà una certa percentuale di valori nulli. All’ entità ottenuta viene aggiunto un ulteriore attributo (selettore) che specifica se una istanza di E appartiene a una delle sotto entità.

###### Verso il basso
**Si elimina l’entità padre trasferendone gli attributi su tutte le entità figlie**. Una associazione del padre è replicata, tante volte quante sono le entità figlie la soluzione è interessante in presenza di molti attributi di specializzazione (con il collasso verso l’alto si avrebbe un eccesso di valori nulli).
![[db35.jpg]]

Si noti che **se la gerarchia è parziale non si può fare il collasso verso il basso**.

#### Proprietà fondamentali di una relazione
- tutte le **tuple** devono avere lo **stesso grado** ( = numero di attributi)
- gli **attributi** devono essere **atomici** (= non ulteriormente scomponibili)
- **ciascuna tupla** deve essere **unica** (ciò è garantito se è presente una chiave primaria)
- non è rilevante l’ordine con cui le tuple compaiono nella tabella

#### Regole di derivazione del modello logico
- ogni entità e ogni associazione molti a molti diventano una relazione
- ogni attributo di un'entità o di un’associazione molti a molti diventa un attributo ( = colonna) della relazione corrispondente
- l’identificatore univoco dell’entità diventa chiava primaria della relazione corrispondente
- l’associazione uno a uno può essere rappresentata come un'unica relazione, oppure come due relazioni separate; nel secondo caso, una di esse conterrà la chiave esterna che fa riferimento all’altra relazione
- l’associazione uno a molti comporta la presenza di una chiave esterna nell’entità debole (lato N), che fa riferimento all’entità forte (lato 1)
- la relazione corrispondente a un’associazione molti a molti contiene le chiavi esterne che si riferiscono agli identificatori univoci delle entità coinvolte, e gli attributi dell’associazione stessa

# Analisi passo per passo
## Esercizio base di dati
Si vuole realizzare una base di dati per una società che eroga corsi, di cui
vogliamo rappresentare i dati dei partecipanti ai corsi e dei docenti. Per i
partecipanti (circa 5000), identificati da un codice, si vuole memorizzare il
codice fiscale, il cognome, l’età, il sesso, il luogo di nascita, il nome dei loro
attuali datori di lavoro, i posti dove hanno lavorato in precedenza insieme al
periodo, l’indirizzo e il numero di telefono, i corsi che hanno frequentato (i
corsi sono in tutto circa 200) e il giudizio finale. Rappresentiamo anche i
seminari che stanno attualmente frequentando e, per ogni giorno, i luoghi e le
ore dove sono tenute le lezioni. I corsi hanno un codice, un titolo e possono
avere varie edizioni con date di inizio e fine e numero partecipanti. Se gli
studenti sono liberi professionisti, vogliamo conoscere l’area di interesse e, se
lo possiedono, il titolo. Per quelli che lavorano alle dipendenze di altri, vogliamo
conoscere invece il loro livello e la posizione ricoperta. Per gli insegnanti (circa
300), rappresentiamo il cognome, l’età, il posto dove sono nati, il nome del
corso che insegnano, quelli che hanno insegnato nel passato e quelli che possono
insegnare. Rappresentiamo anche tutti i loro recapiti telefonici. I docenti
possono essere dipendenti interni della società o collaboratori esterni.

### Regole generali
Dobbiamo arrivare a:
(a) **Costruire un glossario dei termini**
(b) **Raggruppare i requisiti in insiemi omogenei** (dopo aver analizzato
i requisiti ed eliminato le ambiguità presenti)

Per ottenere tutto questo procediamo secondo le seguenti regole generali
1) **Scegliere** il corretto **livello di astrazione**: meglio evitare termini troppo generici
2) **Standardizzare** la struttura delle frasi (stesso stile sintattico). 
3) **Evitare frasi contorte**
4) Individuare sinonimi/omonimi e unificare i termini (docente / insegnante)
5) Rendere esplicito il riferimento tra termini (es indirizzo e num telefono relativi a chi?)
6) **Costruire il glossario**
![[Immagine 2023-06-19 174929.png]]

### Passo base
Individuare i **concetti più rilevanti e rappresentarli** in uno schema scheletro![[1.png]]
### Passo di decomposizione
**Se necessario effettuare una decomposizione dei requisiti** con riferimento ai concetti presenti nello schema scheletro
Con riferimento a questo schema, decidiamo di analizzare separatamente le specifiche riguardanti i partecipanti, quelle riguardanti i corsi e quelle riguardanti i docenti e procedere a macchia d’olio per includere i concetti non considerati nello schema scheletro.

### Passo iterativo
*da ripetere, per tutti i sotto-schemi (se presenti) finche’ ogni specifica è stata rappresentata*
1. raffinare i concetti presenti sulla base delle loro specifiche
2. Aggiungere nuovi concetti allo schema per descrivere specifiche non ancora descritte.

###### Partecipanti
![[2.png]]
###### Docenti
![[3.png]]
###### Corso
![[4.png]]

### Passo di integrazione
**Integrare i vari sottoschemi** in uno schema generale facendo riferimento allo schema scheletro![[5.png]]
## Raffinamento
### Analisi delle ridondanze
**Si eliminano** (o eventualmente si mantengono giustificandole) **le
ridondanze**:
- **Attributi derivabili** (calcolabili) da altri attributi della stessa entità,
di altre entità, da operazioni di conteggio delle occorrenze o, infine,
dalla composizione di altre associazioni

**Nell’esempio** precedente c’è un **solo dato ridondante**: l’attributo Numero di
partecipanti in Edizione Corso la cui presenza porta svantaggi sia in termini di
memoria che di efficienza, di conseguenza viene eliminato.

### Eliminazione delle gerarchie
Nel nostro schema d’esempio, **supponiamo** per quanto riguarda la gerarchia dei docenti **che non ci siano operazioni che richiedano distinzioni tra collaboratori esterni ed interni**, perciò scegliamo questa soluzione e **aggiungiamo il campo tipo all’entità genitore**.
Si procede per la eliminazione di tutte le gerarchie. 
Nel caso della gerarchia partecipante **&rarr;** Sostituzione della generalizzazione con associazioni.
![[6.png]]

## Verso il modello logico
### Regole generali
Ecco un riassunto delle regole per ottenere lo schema relazionale equivalente a uno schema ER ristrutturato:

1. **Associazioni molti a molti**:
    - Creare una tabella per ogni entità coinvolta, con lo stesso nome e gli stessi attributi dell'entità.
    - Creare una tabella per l'associazione, con lo stesso nome dell'associazione e gli attributi dell'associazione, inclusi gli identificatori delle entità coinvolte come chiave primaria.
2. **Associazioni ricorsive**:
    - Aggiungere all'entità un attributo che rappresenti la relazione, dello stesso tipo della chiave primaria dell'entità stessa.
    - Ad esempio, se c'è un'associazione "coordina" tra i dipendenti, aggiungere all'entità "Dipendente" l'attributo "coordinatore" che conterrà la matricola del dipendente che coordina.
3. **Associazioni ternarie molti a molti**:
    - Creare una nuova tabella che abbia le chiavi primarie delle tre entità coinvolte come colonne, insieme agli attributi dell'associazione ternaria.
4. **Associazioni uno a molti**:
    - Aggiungere alla tabella dell'entità "a molti" la chiave primaria dell'entità "uno".
    - La chiave primaria dell'entità "uno" diventa una chiave esterna (FK) nella tabella dell'entità "a molti". Se l'associazione ha attributi, questi vengono migrati nella tabella "a molti".
5. **Associazioni uno a uno**:
    - Se la seconda entità ha molti attributi che potrebbero rimanere vuoti, trattare l'associazione 1:1 come un'associazione 1:N.
    - Creare una tabella con gli attributi dell'associazione e utilizzare la chiave primaria dell'entità "uno" come chiave esterna nella tabella.

### Schema logico finale![[7.png]]