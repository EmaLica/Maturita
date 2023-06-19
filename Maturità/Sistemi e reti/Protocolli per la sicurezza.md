---
Data: 17th June 2023
Descrizione: HTTPS, Certificati e firma digitale
---
# HTTPS
### Breve introduzione
**HTTPS** (Hypertext Transfer Protocol Secure) **è un protocollo di comunicazione sicuro** utilizzato per la trasmissione sicura di dati su Internet. **È una versione sicura del protocollo HTTP**, utilizzato per il trasferimento di informazioni tra un client (come un browser web) e un server.

**HTTPS utilizza il protocollo SSL/TLS** (Secure Sockets Layer/Transport Layer Security) **per crittografare i dati trasmessi tra il client e il server**. Questo fornisce diversi livelli di sicurezza e **garantisce la confidenzialità, l'integrità e l'autenticità dei dati** durante la comunicazione.

### Come funziona
Ecco come funziona il processo di comunicazione tramite HTTPS:

1. **Handshake SSL/TLS**: Il client richiede una connessione sicura inviando un messaggio al server. Il server risponde con il suo certificato digitale, che contiene la sua chiave pubblica.
2. **Verifica del certificato**: Il client verifica la validità del certificato del server utilizzando una catena di certificati fidati (root certificate authorities) presenti nel suo sistema. In questo modo, il client può verificare che il server sia autentico e attendibile.
3. **Scambio di chiavi**: Il client genera una chiave di sessione casuale e la crittografa utilizzando la chiave pubblica del server. Solo il server, con la sua chiave privata corrispondente, può decifrare la chiave di sessione.
4. **Crittografia simmetrica**: Una volta stabilita la connessione sicura, client e server utilizzano la chiave di sessione per crittografare e decrittografare i dati scambiati durante la comunicazione. Questa crittografia simmetrica garantisce la riservatezza dei dati.
5. **Integrità dei dati**: Durante la trasmissione, viene utilizzata una funzione di hash crittografica per creare un valore di hash dei dati. Questo valore di hash viene inviato insieme ai dati crittografati. Il destinatario può verificare l'integrità dei dati calcolando nuovamente il valore di hash e confrontandolo con quello ricevuto.

### Cosa garantisce
1. **Crittografia dei dati**: Tutti i dati trasmessi tra il client e il server sono crittografati, impedendo a terzi non autorizzati di leggere o modificare i dati sensibili.
2. **Autenticazione del server**: Il certificato del server garantisce l'autenticità dell'identità del server, impedendo gli attacchi di phishing o l'intercettazione dei dati da parte di server non autorizzati.
3. **Integrità dei dati**: L'utilizzo di funzioni di hash garantisce che i dati trasmessi non siano stati alterati durante la comunicazione.
4. **Ricerca e indicizzazione dei motori di ricerca**: I siti web con connessione HTTPS sono favoriti dai motori di ricerca, fornendo una migliore visibilità e indicizzazione.

In sintesi, HTTPS è essenziale per garantire la sicurezza delle comunicazioni su Internet, proteggendo i dati sensibili e garantendo l'autenticità e l'integrità dei dati durante la trasmissione.

# Certificati
I certificati sono **emessi da entità di certificazione (CA)**, che sono organizzazioni fidate responsabili di verificare l'identità del richiedente del certificato e di firmare digitalmente il certificato per garantirne l'autenticità. I certificati **sono utilizzati per garantire la sicurezza delle comunicazioni online e stabilire la fiducia tra le parti**.

Un certificato digitale contiene diverse informazioni:
1. **Identità del titolare del certificato**: Il certificato identifica l'entità a cui è stato rilasciato, che può essere un individuo, un'azienda o un sito web. L'identità può includere il nome, l'indirizzo e altre informazioni rilevanti.
2. **Chiave pubblica**: Il certificato contiene una chiave pubblica associata all'entità identificata. La chiave pubblica viene utilizzata per crittografare i dati o verificare la firma digitale generata con la chiave privata corrispondente.
3. **Firma digitale**: Il certificato è firmato digitalmente dalla CA per garantirne l'autenticità. La firma digitale è generata utilizzando la chiave privata della CA e può essere verificata utilizzando la chiave pubblica della CA, che è già presente nel software o nel sistema del destinatario.
4. **Validità**: Il certificato include una data di inizio e di scadenza, specificando il periodo in cui il certificato è considerato valido. Dopo la scadenza, il certificato deve essere rinnovato per continuare a essere valido.

I certificati digitali sono ampiamente utilizzati per garantire la sicurezza delle comunicazioni su Internet. Ad esempio, **nei siti web con protocollo HTTPS**, il certificato **viene utilizzato per stabilire una connessione sicura tra il browser del visitatore e il server del sito**, garantendo che le informazioni scambiate siano crittografate e che il sito sia autenticato.

# Firma digitale
### La Firma Elettronica

**Firma elettronica semplice** (FES):
- io devo dimostrarne l'autenticità
- insieme di dati in forma elettronica
- metodo di identificazione informatica
- 0% valore legale

**Firma elettronica avanzata** (FEA):
- io devo dimostrarne l'autenticità
- 50% valore legale

**Firma elettronica qualificata** (FEQ): 
- particolare tipo di firma ea
- un terzo deve dimostrarne la non autenticità
- 100% valore legale
- si basa su un certificato qualificato
- si effettua da un dispositivo sicuro per la creazione della firma

**Firma digitale**: 
- particolare tipo di firma eq
- un terzo deve dimostrarne la non autenticità
- 100% valore legale
- formata da una coppia di chiavi simmetrica

1. Con la firma digitale si ottiene **l'autenticazione** di un utente
2. Con il **MAC** (Message Authentication Code) si ottiene **l'integrità e la non ripudiabilità**

### Da cosa è composta
- **Dati del messaggio**: Contenuto o versione crittograficamente sicura del messaggio incluso nella firma digitale.
- **Hash crittografico**: Valore univoco calcolato utilizzando una funzione di hash crittografica come SHA-256 per garantire l'integrità del messaggio.
- **Chiave privata del firmatario**: Segreto conosciuto solo dal firmatario, utilizzato per applicare una funzione crittografica alla combinazione dei dati del messaggio e dell'hash.
- **Firma digitale**: Risultato dell'applicazione della chiave privata ai dati del messaggio e all'hash, rappresentando la prova che il messaggio è stato firmato dal firmatario e che i dati non sono stati alterati. Serve per verificare l'autenticità del messaggio e l'integrità dei dati.