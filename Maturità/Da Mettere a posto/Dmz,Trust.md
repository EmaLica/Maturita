### Argomenti

##### Zone LAN/DMZ e Trust - NAT - Port forwarding - NAT e Port forwarding con Cisco Packet Tracer - Firewall con relative tabelle ACL - Proxy - Tunneling - Accesso da remoto - Housing e Hosting.
---


ROUTER:
Per permettere la connessione tra reti differenti si usa il router (connette anche una rete privata a una pubblica), esso potrebbe anche essere un pc

A causa del numero di host, macchine di reti private non possono avere assegnato un indirizzo pubblico, bisogna permettere però l'accesso alla rete pubblica -> NAT

Altro problema sta nella sicurezza, la rete pubblica è pericolosa, per proteggere la propria rete privata si usa il -> FIREWALL

Per controllare e gestire il traffico dalla rete privata verso l'esterno si usa il -> PROXY

ACL (Access Control List):
Essa è una lista contenente delle regole (permessi d'uso relativi ad un particolare oggetto) 
Ogni singolo criterio di una ACL è detto ACE (Access Control Entry) oppure regola

Una ACE è comunemente composta da:
	- obiettivo: cosa fare del pacchetto, scartarlo (deny, drop, discard) o inoltrarlo (permit, accept, allow)
	- interfaccia e verso: su quale interfaccia applicare la regola e in quale verso (input o output)
	- specifiche: caratteristiche del pacchetto (IP, netmask, n. di porta, protocollo ecc.)
	
Le regole hanno un ordine, le prime sono più severe e ristrette
In caso nessuna regola sia applicabile al pacchetto, si applica quella predefinita (allow all o deny all)

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
