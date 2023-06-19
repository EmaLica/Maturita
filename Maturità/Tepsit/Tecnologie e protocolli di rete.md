---
Data: 17th June 2023
Descrizione: modello ISO-OSI e lo stack TCP/IP
---
# Modello ISO-OSI
### Breve introduzione
Il modello **ISO-OSI** (International Organization for Standardization - Open Systems Interconnection) è un **modello concettuale utilizzato per descrivere il funzionamento delle reti di computer**. È stato sviluppato negli anni '70 dall'ISO per facilitare l'interoperabilità delle reti provenienti da diversi fornitori e standard.

Il modello ISO-OSI è **composto da sette strati**, **ognuno** dei quali **svolge funzioni specifiche nella comunicazione** tra dispositivi di rete. Questi strati sono progettati in modo che ciascuno fornisca servizi al livello superiore e utilizzi i servizi del livello inferiore per garantire una comunicazione affidabile e standardizzata.
![[tcpip.png]]

### Gli strati
1. **Strato fisico L1** : È il livello più basso del modello e si occupa della **trasmissione effettiva dei bit attraverso un canale di comunicazione fisico**, come cavi, fibre ottiche o onde radio. Definisce le specifiche elettriche, meccaniche e procedurali per il collegamento fisico dei dispositivi di rete.
2. **Strato di collegamento dati L2**: Questo strato si occupa della **trasmissione affidabile dei dati tra nodi adiacenti all'interno di una rete**. Fornisce la **correzione degli errori**, il **controllo di flusso** e il **controllo di accesso al mezzo di trasmissione**. I dati sono divisi in frame e vengono gestiti gli errori di trasmissione.
3. **Strato di rete L3**: Il compito principale di questo strato è **instradare i pacchetti di dati tra diverse reti**. Determina il percorso ottimale per la consegna dei pacchetti attraverso l'uso di algoritmi di routing, garantendo che i dati raggiungano la loro destinazione finale.
4. **Strato di trasporto L4**: Fornisce un servizio di **trasporto affidabile** per i dati, suddividendo i dati in segmenti e garantendo la **consegna ordinata e senza errori**. Si occupa anche del controllo di flusso e del controllo degli errori tra l'host mittente e l'host destinatario.
5. **Strato di sessione L5**: Gestisce le **sessioni di comunicazione tra i processi delle applicazioni** in esecuzione su dispositivi di rete separati. Fornisce i meccanismi per stabilire, gestire e terminare le connessioni tra i dispositivi.
6. **Strato di presentazione L6**: Si occupa della **rappresentazione dei dati in un formato comprensibile** per le applicazioni. Comprende funzioni di traduzione, crittografia, compressione e conversione dei dati in modo che i dispositivi di rete possano comunicare tra loro utilizzando formati compatibili.
7. **Strato di applicazione L7**: È il livello più alto del modello ISO-OSI e rappresenta **l'interfaccia tra il software dell'applicazione e il modello di comunicazione sottostante**. Include protocolli e servizi per le applicazioni di rete, come la posta elettronica, il trasferimento di file, la navigazione web, ecc.

Il modello ISO-OSI offre una struttura chiara per comprendere e descrivere il funzionamento delle reti, consentendo la standardizzazione e l'interoperabilità dei sistemi di comunicazione. Tuttavia, è importante notare che molti protocolli e tecnologie di rete attuali, come il protocollo TCP/IP, si basano su un modello di riferimento più semplice.

# Stack TCP/IP
### Breve introduzione
Lo stack **TCP/IP** (Transmission Control Protocol/Internet Protocol) **è un insieme di protocolli di comunicazione che costituiscono la base dell'interconnessione delle reti** nel contesto di Internet. È stato sviluppato negli anni '70 e '80 e ha avuto un ruolo fondamentale nello sviluppo e nella diffusione di Internet come lo conosciamo oggi.
![[tcpip.png]]

### I Componenti
Il TCP/IP è un modello di comunicazione a quattro strati, che include i seguenti componenti:

1. **Strato di collegamento**: Questo strato corrisponde in parte al **secondo strato** del modello **ISO-OSI**. Si occupa dell'accesso alla rete fisica e della trasmissione dei dati in forma di frame attraverso il collegamento di rete. Include protocolli come Ethernet, Wi-Fi e PPP (Point-to-Point Protocol).
2. **Strato di rete** (Internet): Questo strato corrisponde in parte al **terzo strato** del modello **ISO-OSI**. Il protocollo principale in questo strato è l'Internet Protocol (IP), che gestisce l'instradamento dei pacchetti attraverso diverse reti per raggiungere la destinazione desiderata. Altri protocolli importanti in questo strato includono ICMP (Internet Control Message Protocol), che fornisce informazioni di controllo e di errore, e ARP (Address Resolution Protocol), che consente di mappare indirizzi IP a indirizzi MAC.
3. **Strato di trasporto**: Questo strato corrisponde al **quarto strato** del modello **ISO-OSI**. I protocolli chiave in questo strato sono il Transmission Control Protocol (TCP) e il User Datagram Protocol (UDP). Il TCP offre un servizio di trasporto affidabile e orientato alla connessione, garantendo che i dati vengano consegnati in modo corretto e ordinato. L'UDP, invece, offre un servizio di trasporto non affidabile e senza connessione, adatto per applicazioni che richiedono una comunicazione veloce e a bassa latenza.
4. **Strato di applicazione**: Questo strato corrisponde a parte del **quinto, sesto e settimo** strato del modello **ISO-OSI**. Include una vasta gamma di protocolli che consentono alle applicazioni di comunicare tra loro. Alcuni esempi di protocolli di livello applicativo sono HTTP (Hypertext Transfer Protocol) per la navigazione web, SMTP (Simple Mail Transfer Protocol) per l'invio di email, FTP (File Transfer Protocol) per il trasferimento di file e DNS (Domain Name System) per la risoluzione dei nomi di dominio.

Il TCP/IP è stato ampiamente adottato ed è diventato lo standard de facto per la comunicazione di rete, in particolare per Internet. La sua flessibilità, scalabilità e capacità di adattarsi a diversi tipi di reti e applicazioni hanno contribuito al successo e alla crescita di Internet come infrastruttura globale di comunicazione.

