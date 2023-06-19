---
Data: 17th June 2023
Descrizione: Classificazione, benefici legati alla distribuzione, svantaggi legati  alla distribuzione 
---
# I Sistemi distribuiti
### Breve introduzione
I sistemi distribuiti sono un tipo di **sistema informatico composto da componenti o nodi interconnessi che collaborano tra loro** per eseguire un'attività comune. Questi sistemi sono **progettati per sfruttare le risorse e le capacità di più macchine**, migliorando la **scalabilità**, la **disponibilità**, la **ridondanza** e la **tolleranza ai guasti**. Possono essere classificati in base alla loro architettura, al modello di comunicazione e alla modalità di coordinamento tra i nodi.

### Classificazione
Esistono diverse classificazioni dei sistemi distribuiti, ma una delle più comuni si basa sull'architettura:

1. Sistemi distribuiti **omogenei** (**cluster computing**): **Tutti i nodi** del sistema hanno lo **stesso sistema operativo** e le **stesse caratteristiche hardware**. Questa omogeneità **semplifica la gestione** del sistema, ma limita la flessibilità.
2. Sistemi distribuiti **eterogenei** (**grid computing**): I nodi possono avere **diversi sistemi operativi, hardware o software**. Questa eterogeneità consente di sfruttare al meglio le risorse disponibili, ma richiede una maggiore **complessità di gestione**.

### Benefici legati alla distribuzione
1. **Scalabilità**: La distribuzione dei sistemi consente di **aumentare le risorse**disponibili **aggiungendo** nuovi **nodi** al sistema. Questo permette di gestire carichi di lavoro crescenti senza dover sostituire completamente l'infrastruttura esistente.
2. **Disponibilità**: La distribuzione dei sistemi permette di **aumentare la disponibilità del servizio**. Se un nodo fallisce, altri nodi possono continuare a fornire il servizio, garantendo una maggiore resilienza.
3. **Prestazioni migliorate**: **Suddividere** un'applicazione tra più nodi può **migliorare le prestazioni complessive del sistema**. I carichi di lavoro possono essere distribuiti in modo più uniforme tra i nodi, riducendo la congestione e migliorando la velocità di risposta complessiva.
4. **Ridondanza**: La distribuzione dei sistemi consente di creare **copie dei dati** o delle risorse in più nodi. Questa ridondanza permette di **recuperare i dati in caso di guasti** o malfunzionamenti, garantendo la persistenza delle informazioni.

### Svantaggi legati alla distribuzione
1. **Complessità di sviluppo**: La progettazione e l'implementazione di sistemi distribuiti possono essere **più complesse rispetto ai sistemi centralizzati**. È necessario gestire la comunicazione, la **sincronizzazione e la coerenza dei dati tra i nodi**, che richiedono un'adeguata progettazione e un'attenta gestione delle risorse.
2. **Costi aggiuntivi**: L'introduzione di nodi aggiuntivi e delle relative infrastrutture può comportare **costi aggiuntivi** in termini di **hardware, software e manutenzione**. Inoltre, la complessità del sistema richiede personale specializzato per la sua gestione e manutenzione.
3. **Problemi di sicurezza**: La distribuzione dei sistemi può introdurre **nuovi punti di vulnerabilità** che devono essere affrontati per garantire la sicurezza dei dati e delle risorse. È necessario **implementare** adeguati meccanismi di **autenticazione, crittografia e controllo degli accessi** per proteggere il sistema dai potenziali attacchi.
4. **Latenza e overhead di comunicazione**: La comunicazione tra i nodi distribuiti introduce un certo **livello di latenza e overhead**. Le prestazioni del sistema possono essere influenzate dalla **velocità** e dalla qualità della rete **di comunicazione tra i nodi**.