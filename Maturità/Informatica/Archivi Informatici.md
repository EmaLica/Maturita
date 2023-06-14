---
Data: 13th June 2023
Descrizione: archivi sequenziali, lista, accesso diretto, invertiti, albero
---
## Cos'è un archivio
**Un archivio è una collezione di dati organizzati e strutturati** in modo da consentire l'efficiente gestione, l'accesso e l'elaborazione delle informazioni in esso contenute. Gli archivi sono spesso utilizzati per **conservare dati persistenti nel tempo**.
## Archivi Sequenziali
Per archivio sequenziale **si intende una organizzazione di dati su memoria di massa in cui le registrazioni possono essere pensate come disposte in blocchi contigui** e in cui ogni elemento, eccetto l'ultimo, ne ha uno e uno solo che lo segue.
- Negli archivi sequenziali è sempre possibile definire un ordine fisico di registrazione, facendo riferimento alla successione fisica delle registrazioni sul supporto di memoria.
- Si parla, invece, di ordine logico tra le registrazioni quando, su uno o più campi, è possibile definire un criterio di ordinamento.
- Quando l’ordine logico coincide con l'ordine fisico, l’archivio verrà detto sequenziale ordinato, altrimenti sequenziale non ordinato o seriale.
#### Supporti di memorizzazione
Il tipo di supporto di memorizzazione a disposizione condiziona il metodo di accesso ad un record posto all'interno dell'archivio principale.
Infatti, se nel caso dei **nastri magnetici** è possibile **accedere ad una registrazione solo dopo aver elaborato la precedente (metodo di accesso sequenziale)**, con i **dischi** si può utilizzare anche una modalità che rende praticamente indipendente il tempo di accesso dalla posizione occupata dal record sul supporto di memoria **(metodo di accesso diretto)**.
#### Operazioni 
**creazione e caricamento**
Nel caso degli archivi sequenziali queste operazioni risultano molto elementari, in quanto consistono semplicemente nella generazione di un archivio vuoto e in un ciclo di caricamento in cui i singoli record vengono registrati in modo sequenziale. Nel caso in cui si voglia lavorare con archivi sequenziali ordinati, sarà necessario far seguire questa fase da una di ordinamento o ricorrere ad un inserimento ordinato.
**ricerca**
Se si effettuano interrogazioni e aggiornamenti su di un archivio, una delle operazioni più frequenti è quella di ricerca di una registrazione. Naturalmente la tecnica varierà in rapporto al tipo di supporto usato e al fatto che esista o meno un ordinamento.
- completa
Si tratta del metodo più semplice, che può essere applicato in tutte le situazioni e consiste nella scansione dell'intero archivio fino al raggiungimento del record cercato o alla fine dell’archivio. La tecnica di ricerca completa è l'unica applicabile agli archivi sequenziali non ordinati.
- sequenziale
Questo tipo di ricerca viene generalmente applicato agli archivi sequenziali ordinati e rappresenta un’ottimizzazione del metodo precedente, in quanto la ricerca termina quando si trova l’elemento cercato oppure lo si supera.
- binaria
Questo metodo di ricerca può essere applicato solo ad archivi ordinati, memorizzati su un supporto ad accesso diretto. Esso consiste nel riapplicare la ricorsivamente la ricerca binaria nella metà dell’archivio in cui si suppone sia presente l’elemento cercato, dimezzando così ad ogni iterazione il
campo di ricerca. L'algoritmo presentato si riferisce ad archivi privi di record vuoti, poiché altrimenti occorre scandire sequenzialmente l’archivio verso l’inizio o la fine per individuare la prima registrazione
occupata. E' evidente quindi che l’efficienza dell'algoritmo diminuisce in funzione del fattore di riempimento ovvero, del rapporto tra il numero di record occupati e il numero totale di record che compongono l'archivio.
- interpolata
Se si deve ricercare un nome in una rubrica telefonica, di solito non la si apre a metà ma in un punto che si valuta vicino a quello in cui si dovrebbe trovare il nome voluto. In pratica, si tratta di un'ottimizzazione del metodo precedente, in cui ad ogni passo, invece di dimezzare semplicemente il campo di ricerca, lo si riduce maggiormente applicando un'apposita funzione di interpolazione
**inserimento**
L'inserimento in archivi non ordinati è relativamente semplice, poiché è sufficiente aggiungere il nuovo elemento in coda o nel primo record fisico logicamente libero. Tuttavia, in archivi ordinati, l'operazione è più complessa in quanto richiede la ricerca della posizione corretta, lo spostamento delle registrazioni successive per creare spazio e infine l'inserimento effettivo dei nuovi dati.
Un'alternativa per gli archivi ordinati potrebbe essere quella di creare un sotto-archivio temporaneo per memorizzare le nuove registrazioni acquisite durante un certo periodo di tempo. Successivamente, si potrebbe eseguire periodicamente una ristrutturazione dell'archivio principale, che coinvolgerebbe l'inserimento delle registrazioni dal sotto-archivio temporaneo nella posizione corretta.
**aggiornamento**
L'operazione di modifica in un archivio consiste nel cambiare i valori di uno o più campi di un record esistente, ad eccezione della chiave. Nell'organizzazione sequenziale su supporto ad accesso diretto, questa operazione si divide in due fasi: la ricerca del record da modificare e la riscrittura del record con le modifiche apportate. La fase di ricerca coinvolge la localizzazione del record desiderato all'interno dell'archivio, solitamente attraverso l'utilizzo della chiave di ricerca. Una volta individuato il record, si passa alla fase di riscrittura, in cui i valori dei campi interessati vengono modificati secondo le specifiche richieste.
**cancellazione**
Se si vuole mantenere una corrispondenza reale tra struttura logica e struttura fisica, per cancellare una registrazione occorre effettuare la riscrittura dell’archivio, tralasciando il record eliminato, in modo da ottenere una nuova organizzazione priva di spazi vuoti. Dato che questa operazione è onerosa si può pensare di sostituire la cancellazione fisica con una logica, ponendo un'apposita marca o nel campo chiave o in un apposito campo del record da eliminare. In questo caso è sufficiente provvedere periodicamente alla ristrutturazione dell'archivio,
sulla base delle politiche di gestione prestabilite in fase di progettazione.
**ordinamento**
l metodi di ordinamento di un archivio possono essere logicamente suddivisi in due grandi categorie:
- metodi di ordinamento interni, applicabili con efficienza accettabile solo a registrazioni completamente residenti in memoria centrale;
- metodi di ordinamento esterni, applicabili a sequenze di registrazioni disposte su memoria di massa.
uno dei metodi più usati per effettuare l'ordinamento esterno di dati disposti su file
sequenziali: 
La tecnica si può riassumere nei seguenti passi:
- si divide l'archivio in sottoarchivi di dimensioni tali che ciascuno di essi possa risiedere completamente in memoria centrale
- si carica ciascuno dei sottoarchivi in memoria centrale, lo si ordina mediante un metodo interno, lo si riscrive su memoria di massa
- si fondono i sottoarchivi ordinati ottenendo un unico archivio ordinato.
*Algoritmi di fusione:*
- fusione parallela
![[parallela.png]]
- fusione a coppie
![[coppie.png]]

## Archivi a liste
In molte applicazioni risulta particolarmente importante poter mantenere costantemente aggiornato ed ordinato un archivio, anche a scapito della velocità di interrogazione dello stesso. Come abbiamo visto, la struttura sequenziale non risponde efficacemente a tale tipo di richieste, poiché le operazioni di modifica risultano spesso laboriose e richiedono l'esecuzione di operazioni aggiuntive
per mantenere inalterata l'originale struttura logica dell'archivio. La struttura di lista lineare, meglio si presta per l’implementazione di archivi in cui, pur volendo
conservare una organizzazione logicamente sequenziale, sono previste molteplici operazioni di inserimento e cancellazione.
#### Richiami sulla struttura di lista
Ricordiamo che per lista lineare si intende una successione di elementi tali che ognuno, tranne il primo e l’ultimo, abbia un solo successore ed un sol predecessore.
Ciò è quanto avviene negli archivi sequenziali facendo riferimento alla successione fisica delle registrazioni.
Esiste un metodo alternativo di memorizzazione che consiste nell’assegnare agli elementi un ordinamento fisico arbitrario, garantendo nel contempo la consequenzialità logica tra gli stessi.
Si costruisce così una lista definita come una successione di elementi che occupano sul supporto di massa posizioni qualsiasi, in modo però che ciascuno di essi sia legato al successivo mediante un puntatore. In una struttura così fatta, ogni registrazione è costituita da due parti: la prima informativa (chiave e attributi) e l'altra di collegamento (puntatore all'elemento successivo).

![[lista.png]]
#### Operazioni 
**ricerca**
La ricerca di una registrazione in una struttura a liste è molto semplice: si parte dal primo elemento della lista, individuata attraverso il puntatore esterno, e si effettua una scansione sequenziale delle registrazioni, seguendo i puntatori. Ci si trova quindi nulla stessa condizione già esaminata per gli archivi sequenziali ordinati e di conseguenza l’algoritmo di ricerca è del tutto analogo.
**inserimento**
Per inserire un nuovo elemento in una lista è sufficiente porre nel suo campo puntatore l'indirizzo dell’elemento destinato a seguirlo e aggiornare il campo puntatore dell’elemento precedente con l’indirizzo dell’elemento aggiunto.
**cancellazione**
Per eliminare un elemento dalla lista, è sufficiente modificare il puntatore dell'elemento precedente in modo che punti all'elemento successivo, ignorando così l'elemento da eliminare. Tuttavia, l'elemento eliminato rimane fisicamente presente nella memoria, ma non è più accessibile. Questo rappresenta un problema poiché lo spazio occupato da elementi eliminati non può essere recuperato. Pertanto, è necessario implementare un meccanismo che permetta di recuperare la memoria occupata dagli elementi eliminati in modo da poterla riutilizzare per nuovi inserimenti.
- Una soluzione per gestire la memoria occupata dagli elementi eliminati è quella di utilizzare una lista libera. In questa organizzazione, tutti i blocchi di memoria vuoti sono collegati in una lista chiamata lista libera, che rappresenta l'archivio vuoto. Quando si desidera inserire un nuovo elemento nella lista, si preleva un blocco dalla lista libera e si inseriscono i dati desiderati. Allo stesso modo, quando si elimina un elemento, il blocco corrispondente viene restituito alla lista libera, diventando disponibile per futuri inserimenti.
- Un approccio alternativo per gestire la memoria occupata dagli elementi eliminati consiste nel marcarli anziché recuperarli immediatamente. Questo metodo posticipa l'operazione di recupero e viene eseguito periodicamente attraverso una procedura chiamata garbage collection. Durante la garbage collection, si esamina l'intera area di memoria allocata per l'archivio e si riuniscono i blocchi marcati come cancellati in una lista apposita. In pratica, anche in questo sistema si crea una "lista libera" a cui si accede ogni volta che è necessario inserire nuovi elementi.
#### Conclusioni 
Come si può intuire, l'organizzazione a lista, per certi tipi di applicazioni, non è sicuramente la più efficiente sotto l'aspetto della ricerca, e per questa ragione raramente viene utilizzata direttamente come struttura portante di archivi semplici.
Inoltre, val la pena sottolineare alcuni aspetti peculiari di questa struttura che ne condizionano
l’applicabilità:
- le operazioni di inserimento e cancellazione possono essere facilmente implementate e non richiedono la ristrutturazione dell'archivio già esistente
- l’aggiornamento, dipendendo dalla ricerca, risulta piuttosto oneroso in termini di tempo
- un archivio a lista risulta piuttosto fragile perché la struttura può essere interrotta dalla scomparsa di un puntatore dovuta a difetti hardware (imperfezione di una traccia) o software (errore di programmazione). E' necessario quindi garantire una maggior sicurezza costruendo liste bidirezionali o circolari che consentono di ricostruire la catena dei puntatori.

## Archivi ad accesso diretto
Le organizzazioni sequenziali e sequenziali con indice sono adeguate per la gestione di grandi quantità di dati, ma possono risultare inefficaci quando gli archivi sono dinamici e richiedono frequenti operazioni di inserimento, cancellazione e interrogazione. Poiché queste operazioni richiedono lo scorrimento dell'archivio, i tempi di accesso possono diventare eccessivamente lunghi, soprattutto se le richieste sono casuali e causano un deterioramento della struttura dell'archivio. Per affrontare questo problema in modo più efficiente, si utilizza un'organizzazione ad accesso diretto, in cui l'indirizzo di una registrazione viene ricavato direttamente dal valore della chiave associata ad essa. Questo metodo consente di accedere direttamente alle registrazioni senza dover scorrere l'intero archivio, migliorando notevolmente i tempi di accesso e riducendo i disagi causati dalla struttura degradante dell'archivio.
Esistono diverse forme di relazione tra il valore della chiave e l'indirizzo del record in un'organizzazione ad accesso diretto:
1. Tabella indice: una tabella memorizzata in memoria centrale che associa ogni chiave alla posizione del record nell'archivio. Questa soluzione presenta sfide legate alle dimensioni della tabella in memoria centrale ed è simile a un'organizzazione sequenziale con indice.
2. Corrispondenza biunivoca: ogni chiave è direttamente correlata a un indirizzo. Ad esempio, in un foglio di calendario, il giorno 12 corrisponde alla dodicesima riga del foglio stesso. Questo tipo di archivio è chiamato archivio autoindicizzato o autoindirizzato.
3. Funzione di trasformazione: la chiave viene convertita in un indirizzo all'interno dell'archivio utilizzando una funzione. In questo caso, l'archivio può essere considerato più propriamente casuale, poiché non esiste una relazione predefinita tra le posizioni dei record e l'ordine logico delle chiavi. La corrispondenza è garantita da un algoritmo di randomizzazione, noto come algoritmo di randomizzazione o indirizzamento hash.
#### Le funzioni di randomizzazione
Come abbiamo accennato, negli archivi casuali il problema fondamentale è quello di definire una funzione che associ ad ogni record logico l'indirizzo di un record fisico in cui memorizzarlo, per cui occorre realizzare, mediante un algoritmo, un'associazione chiave-indirizzo tale che ad ogni valore k della chiave faccia corrispondere un indirizzo I(k).
La situazione ideale si otterrebbe con una funzione che, ad ogni valore ipotetico della chiave, faccia corrispondere un indirizzo distinto, in modo che ogni elemento possa essere raggiunto con un unico accesso (trasformazione perfetta).![[diretto.png]]E' evidente che, poiché nella realtà il numero di chiavi reali è di gran lunga più basso di quello delle chiavi ipotetiche, una organizzazione di questo tipo porterebbe ad un inaccettabile spreco di memoria.
La scelta dell'algoritmo di calcolo risulta quindi cruciale e richiede un'attenta considerazione dei seguenti aspetti:
- l’algoritmo usato per la trasformazione deve sempre produrre lo stesso indirizzo a partire dalla medesima chiave
- se per la memorizzazione dell’archivio è stata riservata una certa area compresa tra un indirizzo iniziale ed un indirizzo finale, lo trasformazione di una qualsiasi chiave k deve produrre sempre un indirizzo che ricada in tale intervallo
- l'algoritmo dovrebbe essere il più semplice possibile, in modo da non appesantire le operazioni di conversione della chiave ed abbassare il tempo di accesso
- la trasformazione dovrebbe coprire l'intero intervallo degli indirizzi, poiché, se l’algoritmo non genera mai un indirizzo , lo spazio di memoria ad esso associato non verrà mai occupato
- occorrerebbe evitare che due o più chiavi vengano trasformate dall’algoritmo di randomizzazione nello stesso indirizzo (collisione). In questi casi, infatti, occorrerebbe mettere a punto procedure particolari per poter allocare le varie registrazioni (sinonimi) ad indirizzi distinti.
#### Conclusioni 
Indubbiamente il maggior vantaggio dell’organizzazione ad accesso diretto è dato dalla alta velocità media di ricerca, modifica, inserimento o cancellazione di una singola registrazione. Per questo motivo l’organizzazione casuale è spesso usata per mettere a punto sistemi di interrogazione che non hanno esigenze di elaborazione sequenziale e che sono relativamente statici.
Infatti, non è possibile effettuare una scansione sequenziale ordinata dell'archivio, poiché non vi è nessun legame tra l'ordine con cui si susseguono le chiavi e quello con cui si susseguono i record.

## Archivi Invertiti
#### Archivio parzialmente invertito
Per facilitare la ricerca attraverso una chiave secondaria è possibile estendere il concetto di indice ad un attributo diverso dalla chiave primaria. Un indice siffatto prevede che ad ogni valore dell’attributo venga associato I'insieme dei puntatori a tutti i record dell'archivio principale che possiedono la proprietà espressa da detto attributo.
È evidente che l’indice della chiave secondaria (dizionario) dovrà essere organizzato in modo da risultare ordinato rispetto alla chiave secondaria, così da facilitare le operazioni di ricerca.
![[inv.png]]
- Il termine invertito attribuito a tale organizzazione trova giustificazione nel fatto che, mentre negli archivi visti finora in base alla chiave primaria si ricerca una registrazione per ricavarne le informazioni relative agli altri attributi, in questo caso, dagli attributi si risale alla chiave primaria.
Anche se questa organizzazione prevede una procedura di ricerca più laboriosa (si deve scandire l'ulteriore indice primario), essa presenta indubbi vantaggi poiché non richiede di ristrutturare i dizionari a fronte di un riordinamento dei record nell'archivio principale.
#### Archivio totalmente invertito
Un'organizzazione estesa dell'archivio prevede la creazione di un indice secondario per tutti i campi del record. Nel caso di un archivio completamente invertito, è possibile mantenere solo una piccola parte delle informazioni nell'archivio principale, come la chiave primaria, e ricostruire l'intero record utilizzando gli indirizzi contenuti negli indici secondari. Se la chiave primaria è presente negli indici, l'archivio principale diventa inutile.
Nella ricerca di un archivio completamente invertito, si cerca il valore della chiave primaria nell'archivio principale per ottenere l'indirizzo corrispondente. Successivamente, si scansionano i dizionari degli indici secondari per trovare i record che contengono l'indirizzo precedentemente trovato.
Tuttavia, l'uso di un archivio completamente invertito può comportare l'omissione di analizzare alcuni attributi, rendendo l'informazione incompleta. Per evitare questo problema, è preferibile mantenere l'intero record nell'archivio principale, anche se ciò comporta un maggiore utilizzo di memoria.
L'organizzazione dell'archivio completamente invertito è efficiente poiché consente di accedere alle informazioni utilizzando diverse combinazioni di attributi. Tuttavia, richiede un notevole aumento dell'utilizzo di memoria a causa della necessità di creare numerosi indici secondari completi.
## Archivi ad albero
Il B-albero è spesso utilizzato per organizzare e mantenere gli indici di archivi di grandi dimensioni e, come gli alberi binari, offre delle ottime prestazioni sia per quanto riguarda la ricerca, sia per l’aggiornamento.
Inoltre, dato che in un B-albero è sempre possibile effettuare una visita che rispetti l’ordinamento della chiave, è anche possibile realizzare elaborazioni sequenziali dell'archivio principale senza per questo doverlo riorganizzare.
I nodi di un B-albero, detti pagine, sono composti da più record (voci) e la loro struttura può essere schematizzata nel modo seguente:
![[albero.png]]
#### Operazioni
**ricerca**
La procedura di ricerca (ricorsiva) può essere schematizzata come segue:
- se l’albero è vuoto, il record non esiste
- altrimenti, analizza le voci della pagina radice:
	- se la chiave è presente accede all’archivio
	- altrimenti applica la ricerca al sottoalbero ricavato dal confronto con la chiave
**Inserimento e cancellazione**
Sia l’aggiunta di un record di chiave k sia la sua cancellazione comportano la preventiva ricerca della chiave k tra quelle memorizzate; nel primo caso, l'operazione potrebbe causare l'aumento del numero di nodi (inserimento in una pagina satura e relativo sdoppiamento ) mentre nel secondo la loro diminuzione(concatenazione di due pagine).
Infatti, in questo caso i tempi medi di ricerca sono paragonabili a quelli delle organizzazioni casuali, con l'ulteriore vantaggio di poter predire anche il numero massimo di accessi necessari per poter raggiungere una registrazione.
## Limiti degli archivi
Gli archivi presentano alcuni limiti che possono influire sulla loro efficacia e prestazioni. Ecco alcuni dei principali limiti degli archivi:

1. Dimensione e occupazione di memoria: Gli archivi possono diventare ingenti in termini di dimensioni e occupazione di memoria, soprattutto quando contengono grandi quantità di dati. Questo può comportare problemi di gestione della memoria e richiedere risorse hardware significative.
2. Tempi di accesso: A seconda dell'organizzazione dell'archivio e del tipo di operazioni effettuate (inserimento, cancellazione, interrogazione), i tempi di accesso possono variare. Alcune strutture possono richiedere scorrimenti o operazioni complesse per accedere ai dati desiderati, rallentando l'efficienza delle operazioni.
3. Operazioni di modifica: Le operazioni di modifica degli archivi possono essere laboriose, soprattutto in strutture sequenziali o ordinate, dove è necessario spostare o riscrivere i dati esistenti per inserire o eliminare un elemento. Ciò può comportare una penalizzazione delle prestazioni e richiedere maggiori risorse computazionali.
4. Mantenimento dell'ordine e dell'integrità: Nel caso di archivi ordinati, è necessario garantire il mantenimento dell'ordine dei dati. Ciò può richiedere complesse operazioni di riallocazione o riorganizzazione dell'archivio in seguito a modifiche o inserimenti. Inoltre, è fondamentale preservare l'integrità dei dati, evitando duplicati o errori di memorizzazione.