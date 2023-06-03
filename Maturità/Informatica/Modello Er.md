---
title: Modello ER
author: Ema
---
### Progettazione di un db:
1. Analisi dei requisiti – scopo: individuare e studiare le funzionalità che il sistema dovrà fornire. Raccolta e studio delle funzionalità che il sistema dovrà avere. Comporta l’interazione con gli utenti del sistema e si conclude in una descrizione informale dei requisiti che il sistema dovrà avere
3. Progettazione – scopo: (a) strutturare e organizzare i dati (b) caratteristiche dei programmi applicativi. Ha lo scopo di rappresentare la realtà di interesse in termini di una descrizione precisa e completa ma indipendente dai criteri di rappresentazione usati dal sistema informatico scelto per gestire la base di dati (rappresentazione astratta)
4. Realizzazione (implementazione): costruzione del sistema
5. Collaudo: verifica del corretto funzionamento del sistema

![[Cattura.png]]
### Entita e relazioni
Entità: sono classi di oggetti, che hanno tutti le stesse proprietà ed esistono in modo autonomo; ogni entità è un insieme di oggetti (detti anche istanze o occorrenze)

Associazioni: sono legami logici fra due o più entità. Anche una associazione è un insieme, è l’insieme delle correlazioni fra i singoli elementi delle entità coinvolte
![[Cattura 1.png]]
![[Cattura 2.png]]
### Cardinalità delle relazioni
Per ogni entità che partecipa a una relazione è possibile indicare il num. min e max di legami che le sue istanze possono avere con istanze delle altre entità partecipanti alla medesima relazione
![[Cattura 3.png]]
Esempi:
0:1
0:N
1:1
1:N
### Associazioni a molte entità
Le associazioni possono collegare più di due entità, peresempio il concetto di pubblicazione, intesa come libro scritto da un certo scrittore per una certa casa editrice, potrebbe essere rappresentato come:
![[Cattura 4.png]]
### Identificatori
ogni entità è un insieme di oggetti aventi le stesse proprietà, è però necessario poter identificare in modo univoco ciascuna istanza di un’entità (anziché parlare di “persone” talvolta occorre parlare dello specifico “sig. Rossi”)
A. Identificatore interno: sottoinsieme di attributi che costituiscono una chiave per l’entità
B. Identificatore esterno: quando non è sufficiente utilizzare un sottoinsieme di attributi ma l’entità partecipa a una relazione con cardinalità (1,1), i suoi elementi possono essere identificati tramite tale relazione
![[Cattura 5.png]]
### Generalizzazioni
![[Cattura 6.png]]
### Relazioni ricorsive 
![[Cattura 7.png]]![[Cattura 8.png]]
### Vincoli di integrità
• Il modello E-R include una serie di costrutti che permettono di definire dei vincoli di integrità sui costrutti già visti
• Queste in altre parole sono delle proprietà che occorrenze di entità e relazioni devono soddisfare per essere considerate valide
	• Cardinalità delle relazioni
	• Cardinalità degli attributi
	• Identificatori delle entità
	• Generalizzazioni

### Cardinalità delle relazioni
1. 0 e 1 per la cardinalità minima:
	• 0 ="è opzionale"
	• 1 ="è obbligatoria“

2. 1 e N per la cardinalità massima:
	• N = “non pone alcun limite”

### Gerarchie 
• Gli attributi (proprietà) del Padre sono ereditati dai Figli
• Non vanno quindi replicati nello schema, sarebbe un errore! NOTA: Non è vero il viceversa!
![[Cattura 9.png]]
### Collassi![[WhatsApp Image 2022-12-11 at 17.34.39.jpeg]]