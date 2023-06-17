---
Data: 17th June 2023
Descrizione: Funzioni di HASH, Cifratura a chiave simmetrica e asimmetrica, Autenticazione
---
# Funzioni di HASH
Le **funzioni di hash** sono **algoritmi crittografici** che prendono in **input un dato arbitrario** e **producono una stringa di output di dimensioni fisse**, chiamata hash. L'hash è un valore univoco che rappresenta il dato originale.  L'operazione di hashing è **unidirezionale**, il che significa che è **facile  e veloce calcolare l'hash di un dato**, ma computazionalmente **difficile o impossibile ottenere l'input originale** dall'hash. Questo rende le funzioni di hash utili per scopi come la verifica dell'**integrità dei dati**, l'**archiviazione delle password** (utilizzando una tecnica chiamata "hashing delle password") e l'**identificazione univoca dei dati**.

### Tipi di HASH
- **MD5**: Produce un hash di **128 bit** ed è utilizzato per scopi non critici come la verifica dell'integrità dei file, ma è considerato debole dal punto di vista della sicurezza.
- **SHA-1**: Produce un hash di **160 bit** ed è stato ampiamente utilizzato in passato, ma è considerato obsoleto a causa delle vulnerabilità agli attacchi di collisione.
- **SHA-256**: Fa parte della famiglia delle funzioni di hash SHA-2 e produce un hash di **256 bit**. È ampiamente utilizzato per scopi di sicurezza ed è considerato sicuro per molte applicazioni.
- **SHA-3**: È una famiglia di algoritmi di hash recentemente introdotta come alternativa a SHA-2, offrendo maggiore sicurezza e resistenza agli attacchi crittografici.
- **HMAC**: Non è un algoritmo di hash autonomo, ma un costrutto crittografico che combina una funzione di hash con una chiave segreta per generare un codice di autenticazione dei messaggi. Viene utilizzato per garantire l'integrità e l'autenticità dei dati.

Tuttavia, MD5 e SHA-1 sono considerati deboli dal punto di vista della sicurezza e non dovrebbero essere utilizzati per scopi critici. È consigliabile utilizzare algoritmi di hash più sicuri come SHA-256 o SHA-3 per garantire la protezione adeguata dei dati.

# Crittografia
I **principi fondamentali per garantire la sicurezza** della comunicazione o di una rete sono: 
- **riservatezza**: i messaggi devono poter essere compresi soltanto dal mittente e dal destinatario.
- **autenticazione**: si deve stabilire in modo certo l'identità del mittente e del destinatario, impedendo a terzi di replicare la loro identità
- **integrità del messaggio**: il contenuto non deve subire alterazioni (volontarie o non) durante la comunicazione
- **disponibilità del servizio**: il servizio deve essere sempre accessibile quando richiesto
- **controllo dell'accesso**: il servizio deve essere disponibile soltanto per gli utenti che sono autorizzati ad utilizzarlo

Molti di questi principi **si realizzano attraverso l'uso della crittografia**. 
La situazione esempio per spiegare i principi di funzionamento della crittografia prevede Alice (il mittente) che deve inviare un messaggio riservato a Bob (il destinatario), senza che Tom (l'intruso) possa leggerlo.
Nella realtà, Alice e Bob possono essere un browser e un server web, dei server DNS, o altri host di vario genere. Tom invece può spiare le conversazioni, sovraccaricare il sistema mandando messaggi non desiderati (attacchi DDoS) o fingere di essere qualcun altro

### Principi base 
La crittografia si basa, come afferma il **principio di Kerckhoffs**, sulla **segretezza della chiave**: 
- **non importa che l'algoritmo sia segreto, ma solo che lo sia la chiave**. 

La sicurezza di una comunicazione dipende anche e soprattutto dal numero di chiavi possibili: più alto è questo numero, minore è la possibilità che la comunicazione sia soggetta ad un attacco brute-force

### Tipologie di crittografia
Esistono **due principali tipologie di crittografia**: la crittografia **simmetrica** (o crittografia a chiave simmetrica) e la crittografia **asimmetrica** (o crittografia a chiave pubblica). Qualsiasi tecnica di cifratura prevede inoltre l'uso di un cifrario (l'algoritmo) e di una o più chiavi (a seconda del tipo di crittografia che viene applicata).  

###### Crittografia simmetrica (AES)
Nel caso della **crittografia simmetrica**, il **mittente e destinatario condividono una stessa chiave**: essa viene utilizzata sia per **codificare il messaggio** che per **decodificarlo**: la **velocità** di codifica e decodifica è **maggiore rispetto alla crittografia asimmetrica**, ma occorre stabilire un modo per scambiarsi in modo riservato la chiave (vedi algoritmo Diffie-Hellman). Il principale svantaggio risiede nel numero di chiavi che devono essere generate per garantire la riservatezza della comunicazione tra ciascuna coppia di host in un gruppo di n host: il numero totale di chiavi "simmetriche" è pari a n(n-1)/2.  

Nel processo di cifratura simmetrica, il **mittente** utilizza la **chiave segreta per crittografare** i dati, trasformandoli in una forma illeggibile chiamata testo cifrato. Il **destinatario** può poi utilizzare la **stessa chiave segreta per decrittografare** il testo cifrato e ripristinarlo allo stato originale.

###### Crittografia asimmetrica (RSA)
La **crittografia asimmetrica** prevede invece che **ciascun host** abbia una **coppia di chiavi**, una **pubblica** ed una **privata**: non è necessario avere un canale per lo scambio sicuro delle chiavi, in quanto la chiave pubblica è nota a tutti e quella privata solo al possessore della chiave stessa. Lo svantaggio risiede invece nella lentezza delle operazioni di cifratura e decodifica.

Nel processo di cifratura asimmetrica, il **mittente** utilizza la **chiave pubblica del destinatario per crittografare** i dati. Il **destinatario** può quindi utilizzare la **sua chiave privata** corrispondente **per decrittografare** i dati e ripristinarli al loro stato originale.

### Autenticazione con crittografia
L'autenticazione con crittografia è un processo per verificare l'identità di una parte utilizzando tecniche di crittografia. Si utilizzano chiavi crittografiche e algoritmi per confermare l'identità del mittente o del destinatario di un messaggio. 
Ci sono diverse modalità di autenticazione crittografica: 
- **l'utilizzo di firme digitali **
- **certificati digitali**
- **scambio di chiavi segrete**

La firma digitale associa un messaggio a un mittente utilizzando la crittografia asimmetrica. I certificati digitali contengono informazioni identificative e chiavi pubbliche di entità, e possono essere verificati tramite firme digitali. Lo scambio di chiavi segrete coinvolge la condivisione di una chiave segreta per crittografare e decrittografare i dati. Questi metodi di autenticazione crittografica forniscono sicurezza e garantiscono che solo le parti legittime possano accedere ai dati crittografati.

###### Con Alice e Bob
- Bob genera una coppia di chiavi crittografiche: chiave pubblica e chiave privata.
- Alice richiede la chiave pubblica di Bob da una fonte affidabile.
- Alice crittografa il messaggio utilizzando la chiave pubblica di Bob per garantire la riservatezza.
- Alice firma digitalmente il messaggio crittografato utilizzando la sua chiave privata.
- Alice invia il messaggio crittografato e la firma digitale a Bob.
- Bob riceve il messaggio crittografato e la firma digitale di Alice.
- Bob utilizza la chiave pubblica di Alice per verificare la firma digitale.
- Se la firma digitale è valida, Bob conferma l'autenticità del messaggio inviato da Alice.
- Bob utilizza la sua chiave privata per decrittografare il messaggio ricevuto.
- Bob può leggere il messaggio originale in modo sicuro e autenticato.

In sintesi, Alice utilizza la chiave pubblica di Bob per crittografare il messaggio e firma digitalmente il messaggio crittografato con la sua chiave privata. Bob verifica la firma digitale utilizzando la chiave pubblica di Alice e decrittografa il messaggio utilizzando la sua chiave privata. Questo processo garantisce la riservatezza, l'autenticità e l'integrità della comunicazione tra Bob e Alice.