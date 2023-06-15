#### Cloud Computing
Con **cloud computing** si intende un modello di gestione della rete tale per cui gli **utenti di una rete privata delegano a terzi la gestione di uno o più servizi** della propria rete interna. La delega viene decisa per sollevare gli amministratori dalla gestione in prima persona dei servizi, gestione interna che viene ritenuta o troppo costosa o troppo tecnicamente impegnativa o non all’altezza del servizio richiesto. Modi di gestione che hanno anticipato il cloud computing sono anche **l’hosting e l’housing** offerto dagli ISP o da altri operatori. 

###### Housing VS Hosting: 
La **differenza principale** tra i due servizi è che con l’**housing** il cliente **acquista un server fisico** e lo fa ospitare nella sala server del provider, mentre con l’**hosting** il cliente **affitta una parte di un server** che è di proprietà del provider.

Inoltre, con l’housing il cliente ha completa libertà per quanto riguarda la gestione e la suddivisione delle risorse hardware e software, mentre con l’hosting la libertà di gestione del servizio è limitata dal fatto che il cliente affitta solo una parte del server.

###### Roi: 
In generale il **cloud computing investe soprattutto le aziende che operano in rete**. L’infrastruttura IT interna si ritrova a dover rispondere velocemente alle richieste e l’amministrazione della rete è impegnata continuamente alla configurazione e alla gestione di nuovi servizi. Questo sforzo spesso non è compensato dal **ROI(Return On Investment): i costi di gestione dell’infrastruttura interna della rete superano i benefici ricavati da essi**. Questi costi di gestione riguardano le voci di: 
- investimento iniziale (ovvero l’acquisto dell’hardware quali server, apparati e cablaggi); 
- mantenimento (la gestione nel tempo della manutenzione efficiente del servizio); 
- risorse umane (la forza lavoro degli amministratori di sistema); 
- licensing (i costi delle licenze dei prodotti software); 
- consumi energetici(per mantenere accesi i server e gli apparati interni); 
- formazione (per mantenere tecnicamente aggiornata la forza lavoro interna).

Per organizzare un sistema cloud normalmente sono previsti tre soggetti: 
- il **cliente** (end user): l’utente o l’azienda che richiede il servizio e sottoscrive un contratto per esso; 
- l’**amministratore** (cloud user): un utente tecnico che sceglie e configura i servizi offerti dal fornitore. Mette in contatto il cliente finale con il fornitore di cui conosce l’infrastruttura e ne cura i rapporti tecnici. Questa figura di intermediazione è presente soprattutto quando il servizio è richiesto da un’azienda; 
- il **fornitore** (cloud provider): l’azienda che possiede le piattaforme hardware e software (datacenter) con cui il servizio viene erogato: connettività, macchine, archiviazione, applicazioni, ecc., e che si fa pagare in base all’uso (pay-per-use).

###### Servizi cloud: 
- Il modello più semplice è definito **SaaS (Software as a Service)**. In questo caso il cliente **utilizza il software messo a disposizione del fornitore** per ottenere servizi quali file sharing, archiviazione, gestione posta elettronica, messaggistica, applicativi d’ufficio, ecc. Es: Google Docs
- A un livello superiore si pone il **PaaS (Platform as a Service)**. In questo caso il cliente **usa ambienti di sviluppo messi a disposizione del fornitore** e, tramite SDK specializzati, può scrivere applicazioni personalizzate che verranno poi messe a disposizione come servizi cloud. Es: Google App Engine
- Infine il servizio più promettente viene denominato **IaaS (Infrastructure as a Service)**. In questo caso il cliente **affitta spazio di calcolo** presso il fornitore in termini di quantità di CPU, **spazio disco e connettività** in base alle esigenze dei servizi che intende sviluppare. Es: Amazon EC2

#### Iso 27001
Il problema della sicurezza in un **sistema informatico** (SI) abbraccia numerosi ambiti che è abbastanza complicato descrivere in maniera completa. In generale la sicurezza nei sistemi informatici riguarda tutte quelle attività che vengono messe in campo per evitare che le informazioni contenute nel sistema informatico possano essere compromesse, disperse o trafugate. Il SI stesso deve preservare le informazioni da eventi che possono intaccarle, **eventi di tipo accidentale** (come per esempio guasti alle apparecchiature del SI) **o eventi di tipo volontario** (come attività di manomissione delle informazioni di un SI). Il **problema della sicurezza dei SI è estremamente sentito dagli addetti dell’IT (Information Technology)**, inoltre **ogni paese** possiede un **quadro normativo che impone alle organizzazioni pubbliche (PA, Pubblica Amministrazione)** e private a una serie di obblighi di legge. A partire dalla fine degli anni ’80 l’ISO ha emanato una serie di documenti tecnici che descrive in maniera internazionalmente condivisa  i criteri essenziali per la sicurezza di un sistema informatico. In effetti la **norma** è stata **concepita a fini certificativi**. La normativa, nel suo complesso, **descrive come realizzare il cosiddetto Sistema di Gestione per la Sicurezza delle Informazioni** (**SGSI**) senza specificare il «come», ma descrivendo quali processi aziendali devono essere realizzati per adeguarsi agli standard di sicurezza. **Essa parte dal cosiddetto risk management**(gestione del rischio), ovvero quel processo mediante il quale **prima si misura** o si stima **il rischio** (assessment), **e** solo **successivamente si sviluppano delle strategie per governarlo** (governance). Quindi **suggerisce un modello attivo** per implementare le strategie per la sicurezza **denominato PDCA** (Plan Do Check Act, o ciclo di Deming).

###### Sistema di Gestione per la Sicurezza delle Informazioni
La norma ISO 27001 offre un’efficace definizione di sicurezza per un SI, ovvero una serie di attributi che la contraddistinguono: 
- **riservatezza** (confidentiality): esprime la garanzia che l’informazione del SI sia disponibile solo a coloro (utenti o processi) che hanno l’autorizzazione a usarla; 
- **integrità** (integrity): esprime la garanzia che l’informazione del SI sia esattamente quella generata dal sistema e non altro; 
- **disponibilità** (availability): esprime la garanzia che l’informazione del SI sia sempre reperibile, sia rispetto alle esigenze del sistema, sia rispetto alle esigenze delle leggi. 

Questi attributi che definiscono la sicurezza di un SI sono a volte ricordati con l’acronimo **RID**.

Il modello suggerito dalla norma per realizzare il SGSI è denominato **Plan Do Check Act** (PDCA) e consiste in una serie ciclica di attività volte al miglioramento continuo del sistema di sicurezza:
- **Plan**: pianificare la politica del SGSI, stabilire obiettivi e indicare la valutazione dei rischi. 
- **Do**: realizzare la politica del SGSI, implementare i controlli, i processi e attuare le contromisure decise durante la valutazione del rischio. 
- **Check**: controllare e valutare l’efficacia delle contromisure realizzate e raccogliere i dati di controllo. 
- **Act**: intraprendere le azioni correttive e preventive, basate sui risultati delle fasi di controllo (audit) o definire nuovi requisiti per il ciclo successivo.

Alcuni esempi di documenti:
NIST 800-300, AS/NZS 4360, CRAMM EBIOS, IT-Grundschutz, RiskWatch, MIGRA

###### Terminologia
- **asset** (bene) Una qualsiasi cosa di valore per l’organizzazione.
- **policy** (politica) L’insieme dei criteri e delle direttive espresse formalmente da un’organizzazione.
- **threat** (minaccia)
- **accountability** (tracciabilità) La proprietà che assicura che le azioni di un ente possono essere ricondotte solo a quell’ente.
- **non-repudiation** (non ripudio o innegabilità) La capacità di provare che un’azione o un evento ha avuto luogo.

##### Il Quadro normativo in Italia
Si può provare a **classificare l’insieme delle normative** (leggi, decreti legislativi, decreti legge, decreti del presidente della repubblica, sentenze e quant’altro) **in** alcune grandi aree corrispondenti a: 
- **disciplina sulle frodi e i crimini informatici**;
- **tutela della riservatezza**; 
- **disciplina della sicurezza per la Pubblica Amministrazione**;
- **tutela del diritto d’autore(NB)**.
Per un elenco tendenzialmente omogeneo delle normative più importanti per area, consultare l’Appendice. Antologia normativa sulla sicurezza informatica in Italia.

###### Frode e crimini informatici
Il Codice di Procedura Penale italiano prevede alcuni articoli che trattano di reati connessi a pratiche illegali di tipo informatico. 
- **è previsto il reato di Frode Informatica**
- **è previsto il reato di Accesso abusivo a un sistema informatico**
- **è previsto il reato di Detenzione e diffusione abusiva di codici di accesso a sistemi informatici**

**Più in particolare** la legislazione che tratta dei crimini informatici si riferisce soprattutto a una legge, la **Legge 547 del 1993**.
- **Furto di identità semplice**: attuata tramite cosiddette tecniche di pishing.
- **Violazione del profilo**: in questi casi i profili di piattaforme Internet per il commercio elettronico.
- **Accessi abusivi**: tecniche per accedere a sistemi informatici senza disporre di autenticazione. (trojan, backdoor, keylogger).
- **Impedimento o interruzione illecita di servizi informatici**. (DoS, spam, hijacker, worm, botnet).
- **Danneggiamento di sistemi informatici**. (irus, malware, spyware, rootkit che consentono il funzionamento di spyware e backdoor).

###### Riservatezza
Le reti di calcolatori, soprattutto se connesse all’infrastruttura pubblica, diventano anche sistemi di comunicazione di massa: esse veicolano dati di ogni natura e quindi anche dati che non dovrebbero essere resi pubblici.
**ogni cittadino ha diritto alla riservatezza delle informazioni che lo riguardano in prima persona e nell’ambito della sua vita privata (privacy).**
- Art. 1. Diritto alla protezione dei dati personali «1. Chiunque ha diritto alla protezione dei dati personali che lo riguardano.»
DPS:
Il **Codice n.196/2003** indica **precise attività che il titolare deve attuare per garantire il diritto alla privacy**. Tra queste la più importante è sicuramente la **stesura di un documento tecnico denominato DPS** (Documento Programmatico sulla Sicurezza) contenuto nel Disciplinare tecnico in materia di misure minime di sicurezza. Il DPS è un vero e proprio **documento di prescrizioni tecniche** che deve essere redatto e aggiornato entro il 31 marzo di ogni anno da ogni organizzazione che tratta dati personali, almeno fino a quando due successive normative hanno svincolato dall’obbligo quasi tutti gli operatori, limitandone la tenuta solo a quelle organizzazioni che trattano dati sensibili con «indicazione di diagnosi»..

###### La Pubblica Amministrazione
Un’importante applicazione di questioni legate alla sicurezza informatica riguarda le attività digitali della **Pubblica Amministrazione (PA)**, attività note anche con l’anglicismo **e-government**(electronic government o amministrazione digitale).
In proposito la **legislazione italiana si basa** sulle leggi 241/90, 150/2000 e il Decreto legislativo 82/2005, modificato dal Decreto legislativo 159/2006 e meglio conosciuto come **Codice dell’Amministrazione Digitale (CAD)**.
I principali elementi di cui si occupa il CAD e dei quali disciplina l’uso sono:
- **valore giuridico dei documenti informatici**.
- **valore giuridico delle comunicazioni elettroniche**.
- **garanzia dell’accesso ai documenti e alla trasparenza degli atti amministrativi**.
- **dematerializzazione progressiva dei documenti amministrativi**.
Per rispondere a queste problematiche il CAD introduce il **RID**: riservatezza, integrità, disponibilità.
Tra le innovazioni introdotte dal CAD per la Pubblica Amministrazione vanno citate:
- **la carta di identità elettronica (CIE)**;
- **la posta elettronica certificata con valore legale (PEC)**; 
- **il sistema pubblico di connettività (SPC)**; 
- **la firma elettronica**.

###### La Firma Elettronica

Firma elettronica semplice:
- io devo dimostrarne l'autenticità
- insieme di dati in forma elettronica
- metodo di identificazione informatica
- 0% valore legale

Firma elettronica avanzata:
- io devo dimostrarne l'autenticità
- 50% valore legale

Firma elettronica qualificata: 
- particolare tipo di firma ea
- un terzo deve dimostrarne la non autenticità
- 100% valore legale
- si basa su un certificato qualificato
- si effettua da un dispositivo sicuro per la creazione della firma

Firma digitale: 
- particolare tipo di firma eq
- un terzo deve dimostrarne la non autenticità
- 100% valore legale
- formata da una coppia di chiavi simmetrica

1. Con la firma digitale si ottiene **l'autenticazione** di un utente
2. Con il **MAC** (Message Authentication Code) si ottiene **l'integrità e la non ripudiabilità**