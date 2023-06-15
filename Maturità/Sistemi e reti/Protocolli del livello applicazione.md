---
Data: 15th June 2023
Descrizione: DHCP, DNS, http(s) con gestione delle sessioni tramite cookie
---
# Livello applicazione (L7)
### Breve introduzione
Il livello delle applicazioni (7 pila ISO/0SI) si occupa di **implementare tutti quei protocolli utilizzati dalle applicazioni di rete**.
Un’applicazione di rete è un insieme di due o più programmi in esecuzione
contemporaneamente su due o più host: **ciascun processo** è **identificato** in maniera univoca **dalla coppia dell’indirizzo IP dell’host e dal numero di porta logica**.

L'architettura delle applicazioni di rete può essere principalmente di 2 tipi:
* **Client-Server** &rarr; i server sono host passivi che dispongono delle risorse, i client sono invece dispositivi attivi che fanno richiesta delle risorse ai server
* **peer-to-peer** &rarr; architettura decentralizzata in cui tutti gli host si comportano sia da client che da server facendo richieste agli altri peer e fornendo le risorse

# DHCP
### Protocollo DHCP
E' un protocollo **Client/Server** trasportato da **UDP** su reti LAN, PPP o WAN. Viene utilizzato per **assegnare indirizzi ip** e altre impostazioni agli host di una rete TCP/IP, evitando di doverli configurare manualmente. In una LAN i **pacchetti DHCP** sono sempre **inviati in broadcast**, la parte **client invia richieste** sulla porta **UDP 67** e **attende risposte** sulla porta **UDP 68**. Il DHCP previene lo spreco di indirizzi ip, distribuendo ip solo a stazioni connesse ad un ISP. 
Gli ip ottenuti dal client in questo modo si dicono dinamici. 
DHCP su LAN opera a livello di dominio di broadcast, un **client DHCP agisce durante la fase di bootstrap**, un server DHCP deve essere presente all'interno del dominio di broadcast per poter rispondere alla richiesta. Se così non fosse, deve essere presente una stazione su cui opera la parte **DCHP relay** che trasmette la richiesta su un altro dominio di broadcast. 
Oltre all'ip vengono settati:
- **subnet mask**
- **gateaway di default**
- **indirizzi server DNS**

La distribuzione deve essere definita su un ambito, ovvero un gruppo definito di ip.
- per **host generico**, **ip** dinamico **valido** per un determinato tempo chiamato **lease**
- per **host** che necessitano di **ip permanenti**, il server **riconosce il** suo indirizzo **MAC**, e fornisce l'ip predeterminato (**reservation**);

Si utilizza un pacchetto nel quale i campi identificano un **4 way handshake** simmetrico detto **DORA**
- **DCHP discover** &rarr; Client cerca Server e chiede configurazione
- **DCHP offer** &rarr; Server offre configurazione, indicando il suo ip
- **DCHP request** &rarr; Client accetta configurazione
- **DCHP ack** &rarr; Server conferma dati e chiude la sessione

I parametri settati sono:
- **Ip Address**
- **Subnet mask**
- **Default Gateaway** &rarr; ip del router di default per il client routing
- **Dns** &rarr; ip di uno o due host che ospitano un server dns
### Sicurezza DHCP
Siccome DHCP è studiato per reti trust, non prevede autenticazione. 
Questo potrebbe far verificare due problematiche:
- **DHCP Address Starvation** &rarr; un programma può fare più richieste DHCP impersonando MAC diversi, causando l'esaurimento del pool di indirizzi
- **DHCP Rogue Server** &rarr; un programma potrebbe sostituirsi ai server DHCP presenti nella rete fisica e di conseguenza fornire configurazioni false

# DNS
### Breve introduzione
Il DNS indica un **sistema complessivo per ottenere l'indirizzo ip di un nodo della rete dal suo nome simbolico o host name** (risoluzione DNS) **o viceversa**(risoluzione inversa).
Con lo stesso acronimo si indica il protocollo che regola il funzionamento delle macchine server che hanno accesso al server con le associazioni nomi/indirizzi. Il protocollo DNS è un **protocollo Client/Server** trasportato da **UDP** sulla **porta 53**.
La **parte client** del protocollo DNS è **sempre attiva su ogni host** ed è **chiamata resolver**, **quella server** sono **macchine che hanno accesso ad un database locale** dei nomi (server dns) ed è **chiamata name server**.
### Protocollo DNS
Il protocollo si suddivide in due passi:
- la **richiesta** del **resolver** (client DNS)
- la **risposta** del **name server** (server DNS)

Il **resolver invia** una **richiesta** di risoluzione con un pacchetto **dns standard query** sulla porta **udp 53**, con ip remoto settato con quello del server dns, la porta locale sarà designata casualmente. 
Il **name server risponde** con un pacchetto **dns standard response**.
Il name server consulta un db locale con le corrispondenze nome/ip, se la **ricerca** da **esito negativo il ns diventa resolver e inoltra** la richiesta. 
Per risolvere un host name pubblico, ci si basa su un db distribuito e sulla gerarchia dei nomi di dominio, che si leggono in `little endian`. Quando un nome di dominio indica un nodo preciso dell'albero, si dice **FQDN** (Fully Qualified Domain Name)
- **Ricorsivo** &rarr; server dns diventa client
- **Iterativo** &rarr; server dns risponde con l'ip di un server dns che potrebbe conoscere la risposta

Quando un name server trova nel suo db una corrispondenza viene detto autoritativo.

# HTTP
### Protocollo HTTP
Il protocollo HTTP assieme al linguaggio HTML costituisce l'ossatura del World Wide Web. E' un protocollo **Client/Server** trasportato da **TCP** sulla **porta 80**. 
Il **Server rimane in ascolto** sulla porta 80 su cui attende connessioni TCP.
Il **Client** effettua **richieste sotto forma di testo** e il Server fornisce le relative risposte sottoforma di file.
- applicazioni client http &rarr; **web browser**
- applicazioni server http &rarr; **web server**

Le **richieste del client** vengono **effettuate tramite** un indirizzamento delle risorse denominato **URL** (Uniform Resource Locator), sulla rete TCP/IP e il modo in cui raggiungerla. In un URL deve essere sempre presente un indirizzo IP, magari sottoforma di dominio da risolvere con DNS. La **parte iniziale obbligatoria dell'URL** (**protocollo**) è detta schema e indica il nome del protocollo utilizzato. Le **connessioni** vengono **immediatamente chiuse** subito **dopo** che la **risposta** è stata fornita dal **server**, implica che **HTTP è un protocollo stateless**. 
### Richiesta HTTP
-  riga iniziale: | metodo | URI | versione HTTP |
- headers: nomeHeader: valore

Esempi di header:
- **Accept** &rarr; tipo di formato desiderato della risposta
- **Content Type** &rarr; in che formato sto inviando al server (Json, XML…)
### Risposta HTTP
-  riga iniziale: | versione HTTP | stato | 
- headers: nomeHeader: valore
### Metodi principali
- **GET**: Richiede una rappresentazione di una risorsa specificata dall'URL.
- **POST**: Invia dati al server per essere elaborati, spesso utilizzato per inviare dati attraverso moduli HTML o creare nuove risorse.
- **PUT**: Sostituisce completamente una risorsa esistente con una nuova rappresentazione o crea una nuova risorsa.
- **DELETE**: Rimuove una risorsa specificata dall'URL.
- **PATCH**: Applica modifiche parziali a una risorsa, aggiornando solo una parte dei dati senza inviare l'intera rappresentazione.
- **HEAD**: Richiede solo l'intestazione di risposta, senza il corpo della risposta, utile per ottenere informazioni sull'intestazione senza scaricare il contenuto completo.
- **OPTIONS**: Ottiene le opzioni di comunicazione supportate per una risorsa, spesso utilizzato per verificare le funzionalità e le opzioni del server.
### Stati di risposta principali
- **200 OK**:: Richiesta elaborata correttamente, risposta contenente le informazioni richieste.
- **201 Created**: Richiesta elaborata con successo, nuova risorsa creata come risultato.
- **204 No Content**: Richiesta elaborata correttamente, ma senza contenuto da visualizzare.
- **400 Bad Request**: Errore nella richiesta a causa di sintassi errata o parametri mancanti.
- **401 Unauthorized**: Richiesta richiede autenticazione per accedere alla risorsa.
- **403 Forbidden**: Richiesta compresa, ma il client non ha i permessi necessari per accedere alla risorsa.
- **404 Not Found**: Risorsa richiesta non trovata sul server.
- **500 Internal Server Error**: Errore interno del server durante l'elaborazione della richiesta.
-**503 Service Unavailable**: Server temporaneamente incapace di gestire la richiesta.
### Sessioni
Quando si utilizza HTTPS (HTTP sicuro) per comunicazioni sicure tra client e server, **la gestione delle sessioni può essere implementata utilizzando i cookie o i token di sessione**.

1. Gestione delle sessioni con i cookie:
    - Il **server genera** un **cookie** univoco per ogni sessione utente.
    - Il **cookie** viene **inviato al client** come parte della risposta HTTP.
    - Il **client memorizza** il **cookie** e lo invia al server come parte delle richieste successive.
    - Il **server verifica il cookie** ricevuto per identificare la sessione utente corrente.
2. Gestione delle sessioni con i token di sessione:
    - Quando **l'utente si autentica**, il **server genera un token di sessione univoco**.
    - Il **token di sessione** viene **inviato al client** come parte della risposta HTTP.
    - Il **client memorizza il token** di sessione (ad esempio, nel local storage o nei cookie).
    - Il **client invia il token di sessione** al server come parte delle richieste successive.
    - Il **server verifica il token di sessione** ricevuto per identificare la sessione utente corrente.