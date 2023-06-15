---
Data: 14th June 2023
Descrizione: L4, udp e tcp
---
# Livello di trasporto (L4)
### Breve introduzione
**Il compito** del livello 4 di trasporto è quello di **consegnare ordinatamente e correttamente i pacchetti ai livelli superiori** operanti sugli end system. E' definito **end-to-end** e i pacchetti vengono chiamati segmenti. Deve essere in grado di frammentare i segmenti per rispettare l'mtu del livello di rete, e di conseguenza ricompattare i segmenti in arrivo.
Il L4 non **ha come mittente o destinatario** un host, ma **un processo in esecuzione su un host**.
- Multiplazione: identificazione dei flussi di un mittente
- Demultiplazione: al processo ricevente sul destinatario arrivano flussi corretti

Quando il L3 è disconnesso, il L4 deve garantire tutti i servizi orientati alla connessione. 
Il L4 deve affrontare i problemi di:
**1.** gestione del flusso
**2.** dell'errore
**3.** della congestione.
###### Funzioni L4:
- **indirizzamento e multiplazione**: distinzione dei flussi da inviare, e in ricezione riconoscere i flussi in entrata per consegnarli alla giusta applicazione
- **instaurare connessioni (se L3 non connesso)**: quindi ordinare sequenze e recuperare errori
- **controllare il flusso**: evitando le congestioni e sincronizzando host lenti con host veloci.

**Entità di trasporto** &rarr; insieme di librerie fornite dal sistema operativo che implementano il L4.
### Connessioni
Il L4, dovendo spesso instaurare connessioni e quindi **creare un canale affidabile su cui comunicare**, nel momento in cui la connessione sta per verificarsi, deve essere **gestita come una sezione critica**, affidabile poiché mittente e destinatario non operano sempre sulla stessa rete. Una connessione è stabilita quando si è concluso un three way handshake.

# Protocollo UDP
L'User Datagram Protocol è un protocollo utilizzato nella rete TCP/IP di tipo **non connesso**. 
UDP gestisce: 
- indirizzamento
- multiplazione 
- controllo dell'errore
Dato che non è connesso, l'**affidabilità non è garantita**. Il pacchetto UDP viene chiamato **`datagramma`**. E' un protocollo **peer to peer**, ovvero che **entrambi i lati** hanno le **medesime capacità**, e consente una comunicazione full-duplex.
Lo schema di indirizzamento UDP si basa sul concetto di porta (identificativo numerico di 16 bit massimo 2 alla sedicesima).
###### Porte:
- 0 &rarr; 1023 **&rarr;** well known ports (processi che usano protocolli)
- 1024 &rarr; 49151 **&rarr;** registered ports (date da Iana su richiesta di aziende)
- 49152 &rarr; 65535 **&rarr;** dynamic ports (utilizzabili localmente)
### Pacchetto UDP
- **source port** &rarr; numero di porta sulla quale si vuole ricevere i pacchetti
- **destination port** &rarr;  numero di porta verso la quale si spediscono i pacchetti
- **lenght** &rarr; lunghezza totale del datagramma
- **checksum** &rarr; complemento a 2 della somma dei complementi a 2 di tutti i gruppi da 16 bit
### Comunicazione UDP
Quando un host vuole comunicare con un altro host deve conoscerne l'ip, quindi specificare il numero di porta di destinazione e il numero di porta sulla quale vuole ricevere. 
Ogni Host deve impostare un 3-pla se vuole usare UDP:
```java
<IP DestinationAddress, UDP SourcePort, UDP DestinationPort>
```
Se si utilizza una struttura dati detta socket si può omettere la porta sorgete utilizzando la coppia di valori chiamata **endpoint**.
**Ai due host** che si scambiano datagrammi in modo full duplex **non** viene **garantito che i pacchetti inviati vengano consegnati**. **Se** viene **utilizzato su LAN grazie al L2 Data Link il problema non si presenta**, ma su WLAN necessita dell'aiuto di un protocollo di livello superiore con il compito di controllare la comunicazione. 
E' client/server solo a livello applicativo e viene anche definito protocollo **fire and forget**.

# Protocollo TCP
Il Transmission Control Protocol è il protocollo di trasporto fondamentale della rete TCP/IP di tipo **connesso**, e viene **considerato affidabile**.
Realizza tutte le funzioni tipiche di un protocollo di trasporto:
- indirizzamento
- multiplazione
- controllo dell'errore
- controllo del flusso
- controllo delle congestioni

Come protocollo connesso, **implica la struttura di Client-Server**.
Client &rarr; richiedente;
Server &rarr; fornitore (HTTP);
Si basa sul concetto di porta analogamente ad UDP.
###### Porte:
- 0 &rarr; 1023 **&rarr;** well known ports (processi che usano protocolli)
- 1024 &rarr; 49151 **&rarr;** registered ports (date da Iana su richiesta di aziende)
- 49152 &rarr; 65535 **&rarr;** dynamic ports (utilizzabili localmente)
### Pacchetto TCP
- **source port** &rarr; numero di porta sulla quale si vuole ricevere i pacchetti
- **destination port** &rarr;  numero di porta verso la quale si spediscono i pacchetti
- **sequence number** &rarr; numero di sequenza del primo byte contenuto nel pacchetto; Quando il flag `syn` vale 1 indica l'isn (initial sequence number)
- **acknowledgement number** &rarr;  se il flag `ack` vale 1, il campo indica il numero di sequenza del prossimo byte da ricevere
- **header lenght** &rarr; il numero di parole a 32 bit dell'intestazione TCP
- **flags** &darr; 
	- `ack` &rarr; a 1 quando contiene un ack valido
	- `syn` a 1 quando l'host mittente vuole avviare una connessione (se accetta si risponde con i flag `syn` e `ack` a 1, poi si fa il sync sul numero di sequenza)
	- `fin` &rarr; a 1 quando l'host mittende vuole chiudere la connessione (se accetta si risponde con i flag `fin` e `ack` settati a 1)
- **checksum** &rarr; complemento a 2 della somma dei complementi a 2 di tutti i gruppi da 16 bit
### Connessione TCP
**Instaurata dalle entità di trasporto** dei s.o. **su ordine dei processi**, ottenuta con lo scambio di segmenti TCP di servizio in modo da **completare un three way handshake**. Il Client chiede una connessione, e il server fornisce questa connessione. **Negoziano** la **porta effimera** (porta che sceglie il client sulla quale sceglie di ricevere risposta dal server), i numeri di sequenza iniziali (**isn**), la massima lunghezza del segmento (**mss**) e la **dimensione delle finestre**. 
Siccome offre il servizio di **multiplazione**, è frequente che più processi client di host differenti (o stesso host) vogliano comunicare verso lo stesso processo server. Il TCP deve garantire che i vari flussi in arrivo sulla stessa porta del server siano distinguibili e separati anche se l'IP del mittente è lo stesso.
1. Due processi stesso host, TCP impone a ogni processo di scegliere una porta effimera locale sempre diversa per ogni connessione
2. Due processi diverso client, oltre alla porta si associa l'indirizzo IP
**Flusso TCP**:
```java
<IP SourceAdd, IP DestinationAdd, TCP SourcePort, TCP DestinationPort>
```
Questa 4-pla è detta TCB.
#### I passaggi della connessione
1. Client invia un segmento TCP (**in broadcast**):
	- Source Port
	- Destination Port
	- Flag `syn = 1` e `isn = x`
2. Server risponde:
	- Source Port
	- Destination Port
	- Flag `syn = 1` e `isn = y
	- Flag `ack = 1` conferma segmento e richiesto del prossimo (x + 1)
	- Mss
3. Il Client chiude il three way handshake
	- Source Port e Destination Port **stabilite**
	- numero sequenza successivo (x + 1)
	-  Flag `ack = 1`  numerato (y + 1)
Quando Client e Server fanno coincidere: 
```js
TCP SourcePort(Server) a TCP DestinationPort(Client)
TCP DestinationPort(Server) a TCP SourcePort(Client)
```
Allora la connessione è stata instaurata.
### Disconnessione TCP
La disconnessione viene avviata da un capo e confermata dall'altro, affinché termini deve essere completata su entrambi i lati. (Uno tra Client e Server decide di terminare)
**Scenario in cui il Server non ha nient'altro da comunicare al Client**
1. Server vuole smettere, invia un segmento TCP:
	- Flag `fin = 1` e numero di sequenza attuale.
	- Se `ack = 1` anche lui è settato
2. Client risponde:
	- Flag `ack = 1`
3. Client di nuovo:
	- Flag `fin = 1` e numero di sequenza attuale
	- Se `ack = 1` anche lui è settato
4. Server invia un TCP finale con:
	- Flag `ack = 1`
**Connessione terminata**
```js
NOTA: I segmenti `1 - 2 - 3` non aumentano il numero di sequenza iniziale
```