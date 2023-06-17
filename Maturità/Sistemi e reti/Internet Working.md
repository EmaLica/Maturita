---
Data: 16th June 2023
Descrizione: Nat, port forwarding, Firewall, Lan/Trust e DMZ,Tunneling,SSH, Desktop Remoto, VPN, cloud computing
---
# NAT
Il **Network Address Translation** (NAT) è un **processo** che consente di **mascherare** un **host privato sulla rete pubblica**. Il funzionamento di NAT avviene in due fasi:

1. Quando arriva una **richiesta**, NAT **cambia l'indirizzo IP** dell'host privato con il proprio indirizzo IP pubblico.
2. Quando arriva una **risposta** dalla rete, NAT **sostituisce l'indirizzo** del mittente nei pacchetti ricevuti con l'indirizzo IP dell'host privato.

Internet Connection Sharing (ICS) è una versione primitiva del NAT.

**Port Address Translation** (PAT) è una **variante di NAT** che **mappa le richieste sulle porte effimere**, consentendo di distinguere i client nel caso in cui più di uno effettui contemporaneamente una richiesta alla stessa porta dello stesso server.

La **Destination NAT** (DNAT) si verifica **quando un host privato fornisce un servizio alla rete pubblica**, ad esempio un server web. Il router mappa le connessioni provenienti dall'esterno e indirizzate al suo indirizzo IP pubblico verso l'indirizzo IP privato della macchina che fornisce il servizio.
### Sicurezza NAT
La sicurezza di NAT presenta alcune problematiche da considerare:

1. **Carico elevato sui router**: NAT richiede ai router di mantenere tabelle di correlazione contenenti molti indirizzi host, il che può generare un carico significativo sulle risorse dei router.
2. **Ricalcolo del checksum IP**: ogni volta che il router cambia l'indirizzo IP di destinazione di un messaggio, è necessario ricalcolare il checksum IP.
3. **Problemi con alcuni protocolli**: alcuni protocolli possono negoziare gli indirizzi IP, il che può causare problemi quando si utilizza NAT.
4. **Single point of failure**: un server NAT costituisce un punto di vulnerabilità singolo, poiché un malfunzionamento del server può causare un'interruzione del sistema.

Nonostante queste problematiche, NAT offre una certa sicurezza poiché l'indirizzo IP della macchina privata non viene mai esposto direttamente nella rete pubblica.

# Port Forwarding
Il port forwarding è un'operazione utilizzata nelle reti informatiche per consentire il **trasferimento dei dati da un computer a un altro attraverso una porta** di comunicazione specifica. Questa tecnica permette a un utente esterno di raggiungere un host con un indirizzo IP privato all'interno di una rete locale (LAN) utilizzando una porta dell'indirizzo IP pubblico. Per poter eseguire il port forwarding, **è necessario** disporre di **un router in grado di effettuare** una traduzione automatica degli indirizzi di rete, nota come **NAT** (Network Address Translation).

# Firewall
Il **firewall** è un **processo che controlla**, a vari livelli, **il contenuto dei pacchetti in entrata e in uscita** su una rete al fine di garantirne la sicurezza. Le prestazioni di un firewall vengono misurate in PPS (pacchetti al secondo).

### Tipi di Firewall
1. **Personal Firewall**: è un software **installato su un singolo host** che controlla il traffico di rete in entrata e in uscita da quel dispositivo.
2. **Firewall perimetrale**: è **installato su un router** che si trova **all'interfaccia tra la rete interna** (affidabile) **e la rete esterna** (insicura o pubblica). Opera su due interfacce, una rivolta alla rete di fiducia (privata) e l'altra verso la rete insicura (pubblica).
3. **Firewall hardware**: è **un'apparecchiatura hardware dedicata** che funge da firewall e dispone di almeno due interfacce di rete, una per la rete di fiducia e l'altra per la rete pubblica. Un firewall hardware può anche svolgere il ruolo di router per connettere le due reti.

Un **firewall perimetrale può essere anche un'applicazione di livello 7**, noto come application layer firewall, che opera su un server. Questo tipo di firewall analizza i pacchetti a livello di applicazione per controllare l'uso corretto dei protocolli applicativi e ispezionarne il contenuto.

### Livelli di controllo
I livelli di controllo del firewall includono:

1. **Packet Filter**: fornisce un **controllo di base del traffico a livello di indirizzamento IP** e verifica dei flag SYN di TCP per rilevare tentativi di connessione.
2. **Stateful Inspection**: valuta la qualità delle connessioni TCP attraverso un **controllo dettagliato degli header dei pacchetti TCP fino al livello 4** (trasporto). Questa funzionalità consente di intercettare il traffico TCP che potrebbe costituire un tentativo di intrusione.
3. **Deep Inspection**: analizza il **traffico dei pacchetti fino al livello 7**(applicazione), ispezionando il corretto utilizzo dei protocolli applicativi e il contenuto dei pacchetti. Questo tipo di firewall **può intercettare firme di virus o applicazioni** di intrusione comuni e può bloccare il traffico verso determinati siti o in base a parole chiave. Tuttavia, richiede una capacità prestazionale significativa.

### Sicurezza Firewall
**La sicurezza** del firewall **dipende dall'host su cui viene eseguito** il processo del firewall, noto come **bastion host**. Queste **macchine** devono essere **potenti**, affidabili e sicure, e devono essere ottimizzate per ridurre al minimo le possibilità di problemi.

**Uno degli attacchi principali** ai firewall è **l'IP spoofing**, che consiste nell'accedere ai servizi di una rete **simulando un indirizzo IP diverso falsificato**. Uno degli **obiettivi comuni** degli attacchi informatici è il **Denial of Service (DoS)**, che **mira a sovraccaricare un servizio** sottoponendolo a uno stress eccessivo o sfruttando vulnerabilità. 

# Reti LAN Trust/Dmz
Nelle configurazioni di rete dual home, viene creata una subnet di collegamento che comporta la presenza di **due sottoreti**: una **sicura chiamata TRUST**, che contiene gli **host privati e il traffico in uscita**, e **un'altra sottorete chiamata DMZ** (DeMilitarized Zone), che **contiene le macchine che devono esporre servizi pubblici** e **quindi** gestisce il **traffico in entrata**. 
Questo tipo di **schema** di rete trust/dmz è **noto come SCREENED SUBNET**.

Tutto il **traffico in ingresso** è **confinato all'interno della DMZ** dopo essere passato attraverso il firewall perimetrale e non tocca la rete TRUST. **L'unico traffico consentito tra la DMZ e la TRUST riguarda i servizi interni**, come ad esempio le mail.

Nelle configurazioni TRUST/DMZ, è necessario **specificare** all'interno del router **gli indirizzi IP pubblici** che devono essere **utilizzati per i servizi implementati nella DMZ**.

# Tunneling
Il tunneling **consiste nell'incapsulare completamente un protocollo all'interno di un altro che lo trasporta alla destinazione**, permettendo al protocollo incapsulato di **attraversare parti di rete che** normalmente **non potrebbe attraversare**.

Un **esempio** di tunneling è il **protocollo PPPoE**, in cui il **protocollo PPP è incapsulato in Ethernet**.

Il protocollo incapsulato e quello incapsulante sono totalmente indipendenti.

# SSH
**SSH** (Secure Shell) è un **protocollo di rete per l'accesso remoto sicuro a computer remoti**. Funziona **creando una connessione crittografata tra due dispositivi** consentendo agli utenti di eseguire comandi e trasferire dati in modo sicuro. SSH è utilizzato per il controllo e l'amministrazione sicura di server e dispositivi di rete. Offre la possibilità di **eseguire comandi remoti tramite una sessione di terminale sicura** e consente il **trasferimento sicuro di file tramite il programma "scp" (Secure Copy)**. In sintesi, SSH permette l'accesso remoto sicuro e la gestione di computer e server.

# Desktop remoto
L'accesso remoto è necessario per gli amministratori di rete, poiché consente loro di operare, **gestire e monitorare la rete** anche senza essere fisicamente presenti, **utilizzando una macchina locale**.
Quasi sempre, per effettuare un accesso remoto, si utilizza il tunneling.

# VPN
**Una VPN** (Virtual Private Network) è una tecnologia che **crea una connessione sicura e crittografata tra un dispositivo** (come un computer o uno smartphone) **e una rete privata su Internet**. Essenzialmente, una VPN estende una rete privata su una rete pubblica, come Internet, consentendo agli utenti di inviare e ricevere dati in modo sicuro e anonimo.

Quando ci si connette a una VPN, il dispositivo crea un **tunnel crittografato** tra il dispositivo stesso e il server VPN. Tutti i **dati** che vengono trasmessi attraverso questo tunnel **sono criptati**, rendendoli **inaccessibili a terze parti** non autorizzate. Questo offre protezione e sicurezza, specialmente quando si accede a reti pubbliche non sicure, come hotspot Wi-Fi in luoghi pubblici.

Una **VPN** offre anche l'opportunità di **nascondere l'indirizzo IP** del dispositivo, sostituendolo con l'indirizzo IP del server VPN. Questo crea un'anonimato aggiuntivo, impedendo a siti web, servizi online o altri utenti di monitorare o tracciare l'attività online dell'utente.

Le VPN sono utilizzate per vari scopi, tra cui la 
- **sicurezza delle comunicazioni aziendali**
- **l'accesso remoto a risorse aziendali**
- **la protezione della privacy online** 
- **il superamento delle restrizioni geografiche** per accedere a contenuti o servizi disponibili solo in determinate regioni.

# Cloud Computing
### Breve introduzione
Con **cloud computing** si intende un modello di gestione della rete tale per cui gli **utenti di una rete privata delegano a terzi la gestione di uno o più servizi** della propria rete interna. La delega viene decisa per sollevare gli amministratori dalla gestione in prima persona dei servizi, gestione interna che viene ritenuta o troppo costosa o troppo tecnicamente impegnativa o non all’altezza del servizio richiesto. Modi di gestione che hanno anticipato il cloud computing sono anche **l’hosting e l’housing** offerto dagli ISP o da altri operatori. 

#### Housing VS Hosting: 
La **differenza principale** tra i due servizi è che con l’**housing** il cliente **acquista un server fisico** e lo fa ospitare nella sala server del provider, mentre con l’**hosting** il cliente **affitta una parte di un server** che è di proprietà del provider.

Inoltre, con l’housing il cliente ha completa libertà per quanto riguarda la gestione e la suddivisione delle risorse hardware e software, mentre con l’hosting la libertà di gestione del servizio è limitata dal fatto che il cliente affitta solo una parte del server.

### Roi: 
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

### Servizi cloud: 
- Il modello più semplice è definito **SaaS (Software as a Service)**. In questo caso il cliente **utilizza il software messo a disposizione del fornitore** per ottenere servizi quali file sharing, archiviazione, gestione posta elettronica, messaggistica, applicativi d’ufficio, ecc. Es: Google Docs
- A un livello superiore si pone il **PaaS (Platform as a Service)**. In questo caso il cliente **usa ambienti di sviluppo messi a disposizione del fornitore** e, tramite SDK specializzati, può scrivere applicazioni personalizzate che verranno poi messe a disposizione come servizi cloud. Es: Google App Engine
- Infine il servizio più promettente viene denominato **IaaS (Infrastructure as a Service)**. In questo caso il cliente **affitta spazio di calcolo** presso il fornitore in termini di quantità di CPU, **spazio disco e connettività** in base alle esigenze dei servizi che intende sviluppare. Es: Amazon EC2