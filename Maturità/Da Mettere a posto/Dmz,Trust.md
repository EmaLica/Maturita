### Argomenti

##### Zone LAN/DMZ e Trust - NAT - Port forwarding - NAT e Port forwarding con Cisco Packet Tracer - Firewall con relative tabelle ACL - Proxy - Tunneling - Accesso da remoto - Housing e Hosting.
---

Zone Trust E Dmz (Lan)
 Nella tipologia dual home, la subnet di link fa si che ci siano due sottoreti, una sicura e definita TRUST contenente gli host privati e il traffico outgoing, un'altra invece insicura definita DMZ (DeMilitarized Zone) contenente le macchine che devono esporre i servizi pubblici e quindi il traffico ingoing. Questo schema di rete trust/dmz è detto SCREENED SUBNET
 Tutto il traffico incoming è confinato all'interno della DMZ dopo aver superato il firewall perimetrale, e non tocca quindi la rete TRUST, l'unico traffico permesso tra DMZ e TRUST riguarda servizi interni come ad esempio le mail
 Nelle configurazioni TRUST/DMZ è necessario specificare nel router gli indirizzi IP pubblici che devono essere utilizzati, come quelli dei servizi realizzati dalla DMZ

RETE MICROSOFT:
Essa consiste in una rete con due DMZ, DMZ out per il traffico pericoloso e DMZ in per il traffico considerato generalmente sicuro
Il traffico incoming rimane confinato nella DMZ out
Il traffico interno invece per raggiungere internet passa prima dal firewall della DMZ in, poi dal gateway/proxy della rete e infine dal firewall della DMZ ou
una TRUST è 

ROUTER:
Per permettere la connessione tra reti differenti si usa il router (connette anche una rete privata a una pubblica), esso potrebbe anche essere un pc

A causa del numero di host, macchine di reti private non possono avere assegnato un indirizzo pubblico, bisogna permettere però l'accesso alla rete pubblica -> NAT

Altro problema sta nella sicurezza, la rete pubblica è pericolosa, per proteggere la propria rete privata si usa il -> FIREWALL

Per controllare e gestire il traffico dalla rete privata verso l'esterno si usa il -> PROXY

NAT (Network Address Translation):

Esso è un processo che impersona l'host privato sulla rete pubblica, funziona con 2 passaggi:
	- Ricevuta la richiesta, cambia l'ip dell'host con il proprio (pubblico) 
	- Ricevuta la risposta dalla rete, sostituisce nei pacchetti ricevuti l'indirizzo del destinatario dal proprio a quello dell'host
	
ICS -> E' una versione primitiva del NAT

PAT (Port Address Translation):
NAT che mappa le richieste sulle porte effimere, per poter distinguere i client in caso più di uno effettui contemporaneamente una richiesta alla stessa porta dello stesso server

DESTINATION NAT:
Quando avviene l'inverso, ovvero un host privato fornisce un servizio alla rete pubblica (server web), il router mappap le connessioni provenienti dall esterno e dirette al suo indirizzo pubblico verso l'indirizzo privato della macchina che effettua il servizio

SICUREZZA NAT:
Il NAT causa 2 problemi principali:
	 - alto carico sui router che sono obbligati a mantenere tabelle di correlazione (contententi gli host) molto grandi
	 - per ogni messaggio a cui il router cambia l'ip di destinazione esso deve ricalcolare il checksum IP
	 - alcuni protocolli negoziano gli indirizzi IP
	 - Il server NAT costituisce un single point of failure, in quanto il suo malfunzionamento causa un down del sistema
	 
Il NAT offre una certa sicurezza in quanto l'indirizzo della macchina privata non verrà mai esposto nella rete pubblica 

FIREWALL: 
Anche il firewall è un processo
Esso è un processo in grado di controllare, a vari livelli, il contenuto dei pacchetti in entrata e uscita su una rete al fine di controllarne la sicurezza
Le prestazioni di un firewall si misurano in PPS (Pacchetti per secondo)

Essi possono essere 
	- Personal firewall: Programmi su un singolo host 
	- Firewall perimetrale: Installato su un router che si affaccia alla rete pubblica
	-> in questo caso il firewall opera su 2 interfacce, una sulla rete trust (privata) e una sulla rete insicura (pubblica)
	- Firewall hardware: il firewall è costituito da un apparato hardware con almeno due interfacce, una sulla trust e una sulla pubblica, il firewall hardware può fungere anche da router per mettere in contatto le due reti
	
Un firewall perimetrale può essere anche un applicazione di livello 7, (application layer firewall) che opera su un server

LIVELLI DI CONTROLLO DEL FIREWALL:
FirewallPacket Filter: funzionalità minima che controlla il traffico a livello di indirizzamento IP e ispezione del flag SYN di TCP per intercettare  tentativi  di  connessione.
Livello  indispensabile  per  bloccare  opermettere il traffico tra subnet e/o reti IP pubbliche;

FirewallStateful  Inspection: in  grado  di  valutare  la  qualità  delle  connessioni TCP tramite il controllo approfondito dell’header dei pacchetti TCP, ovvero analisi fino a livello 4 di Trasporto. Questa funzionalità consente di intercettare traffico TCP che apparentemente appartiene a una connessione ma in realtà costituisce un tentativo di intrusione;

FirewallDeep Inspection: in grado di analizzare il traffico dei pacchetti fino a livello 7 Applicazione, analizzando il corretto uso dei protocolli applicativi e ispezionandone anche il contenuto. In base a un glossario su database, questo tipo di processo riesce a intercettare le firme dei virus o degli applicativi d’intrusione più diffusi. Inoltre è in grado di bloccare il traffico per determinati siti o in base a un elenco di parole chiave.
Queste funzionalità richiedono una cospicua capacità prestazionale

ACL (Access Control List):
Essa è una lista contenente delle regole (permessi d'uso relativi ad un particolare oggetto) 
Ogni singolo criterio di una ACL è detto ACE (Access Control Entry) oppure regola

Una ACE è comunemente composta da:
	- obiettivo: cosa fare del pacchetto, scartarlo (deny, drop, discard) o inoltrarlo (permit, accept, allow)
	- interfaccia e verso: su quale interfaccia applicare la regola e in quale verso (input o output)
	- specifiche: caratteristiche del pacchetto (IP, netmask, n. di porta, protocollo ecc.)
	
Le regole hanno un ordine, le prime sono più severe e ristrette
In caso nessuna regola sia applicabile al pacchetto, si applica quella predefinita (allow all o deny all)

SICUREZZA FIREWALL:
L'apparato su cui gira il processo del firewall è detto BASTION HOST, queste macchine devono essere particolarmente potenti, affidabili e sicure, oltre che ottimizzate in modo da ridurre al minimo le possibilità di problemi.

Uno degli attacchi principali verso i firewall è l'IP SPOOFING, che consiste nell'accedere ai servizi di una rete simulando un'identità diversa, falsificando l'indirizzo IP
L'obiettivo principale di molti attacchi informatici è il DoS (Denial of Service) ovvero l'annientamento del servizio sottoponendolo a uno stress eccessivo (oppure  sfruttandone dei problemi)
Un metodo comune è l'IP Smurfing, che consiste nell'invio di pacchetti echo request in broadcast, se il router non li riconosce, essi cominceranno a rimbalzare a cascata all'interno della rete finendo per generare un traffico troppo pesante

PROXY:
Quando un attività di routing viene effettuata a livello 7, il sistema viene definito GATEWAY
Anche il proxy è un processo 

Per poter usare il proxy l host deve poter raggiungere la macchina che funge da server proxy attraverso un protocollo di livello 7, in seguito il proxy comunicherà con la rete pubblica al posto del client, reindirizzando a lui le risposte. Un client quindi (un browser) dovrà effettuare le richieste al proxy e non alla destinazione finale

REVERSE PROXY:
Permette ad host pubblici di utilizzare servizi implementati su host di una rete privata (es. server web) tramite un proxy

SICUREZZA PROXY:
Il proxy fornisce di base un livello importante di sicurezza, ad esempio quando il server proxy riceve una richiesta può effettuare un autenticazione nei confronti dell host che l ha effettuata ( non eseguibile con il nat, in quanto trasparente)
Questa autenticazione può essere anche collegata ad un database
Un proxy garantisce anche un completo logging degli accessi 
Per Windows il proxy più usato è Microsoft Forefront Threat mangement Gateway
Per Linux invece è Squid

TIPI DI RETE:
Residenziale ->modem ADSL, host gateway, switch, clients
PPPoE -> PPP over Ethernet
Residenziale (altro tipo) -> apparato integrato (fa da switch, router, firewall, modem, AP) e clients

Single-Homed -> Router (packet filter) collegato allo switch, un host che funge da proxy/firewall collegato allo switch, cllients, il proxy offre agli host interni i servizi esterni (out-going)
Dual-Homed -> Router (packet filter) collegato all'host gateway ecc, host che fa da gateway/firewall/proxy collegato allo switch, clients, QUESTA TIPOLOGIA PREVEDE L'USO DI UNA SUBNET DI LINK
Single-home consente ai pacchetti pubblici di circolare nella rete privata, dual-home invece non lo permette

ACCESSO REMOTO:
Esso è necessario per gli amministratori di rete in quanto permette loro di operare, gestire e monitorare la rete anche senza essere in presenza tramite l'uso di una macchina locale
Quasi sempre per effettuare un accesso remoto si usa il tunneling

PORT FORWARDING:
Nelle reti informatiche il port forwarding è l'operazione che permette il trasferimento dei dati (forwarding) da un computer ad un altro tramite una specifica porta di comunicazione. Questa tecnica può essere usata per permettere ad un utente esterno di raggiungere un host con indirizzo IP privato (all'interno di una LAN) mediante una porta dell'IP pubblico dello stesso. Per eseguire questa operazione si ha bisogno di un router in grado di eseguire una traduzione automatica degli indirizzi di rete, detta NAT.

TUNNELING:
Esso consiste nell'incapsulare completamente un protocollo all'interno di un'altro che  lo trasporta alla destinazione, questo per permettere al protocollo incapsulato di attraversare parti di rete che normalmente non potrebbe attraversare.
PPPoE -> protocollo PPP incapsulato in Ethernet
Il protocollo incapsulato e quello incapsulante sono totalmente indipendenti
Fondamentali per l'accesso remoto sono authentication, confidentiality e integrity

VPN 
Simula una rete privata, di fatto permettendo ad un utente della rete pubblica di usare i servizi della rete privata come se ne facesse parte

COMANDI PACKET TRACER:
# Entrata e uscita NAT:
(config-if)# int f0/0
(config-if)# ip nat inside

(config-if)# int f0/1
(config-if)# ip nat outside

# Access List:
Router(config)# acc <id_numero> permit <permesso>
ip nat inside source list <id_numero> interface<interfaccia_esterna (f0/1) > overload 

# Port forwarding:
(config)#ip nat inside source static tcp <inside-address port>  <outside-address port> 

Router enable
Router# configure terminal



Spunta Router Port on
