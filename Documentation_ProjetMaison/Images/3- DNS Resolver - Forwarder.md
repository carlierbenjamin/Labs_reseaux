
#### **VM Windows Server** :

Page web pfsense: **Services → DNS Resolver**
![[Pasted image 20260801152934.png]]
=> pfSense configuré pour répondre aux requêtes DNS

##### Test de résolution DNS : 
```
nslookup google.com
```
![[Pasted image 20260801142729.png]]
=> Serveur DNS actif :  pfSense.home.arpa, addresse IP du serveur DNS :  192.168.1.1. 
"Réponse ne faisant pas autorité" car pfSense **n’héberge pas** la zone 'google.com'. pfSense interroge les DNS publics configurés. 
pfSense résout **correctement les enregistrements AAAA** (adresses IPv6)

##### Test DNS + connectivité :
```
ping google.com
```
![[Pasted image 20260801144837.png]]
=> ping internet fonctionne


#### **VM Ubuntu Desktop** :

##### teste du DNS :
```
dig google.com
```
![[Pasted image 20260801180002.png]]
=> requête transite du LAN vers pfSense, puis vers Internet via VirtualBox NAT. 
Le serveur DNS local (127.0.0.53) relaie la requête vers pfSense, ce qui confirme le bon fonctionnement du routage et du NAT.
-status: NOERROR : Le DNS fonctionne et la requête a été résolue
-ANSWER: 6 : on obtient 6 adresses IPv4 de Google
-SERVER: 127.0.0.53#53 : Ubuntu interroge son DNS loca
##### Test de résolution DNS :
```
nslookup google.com
```
![[Pasted image 20260801180140.png]]=> **Serveur DNS actif :** 127.0.0.53 (résolveur local _systemd‑resolved_), 
Ubuntu interroge son résolveur local **127.0.0.53**, qui relaie ensuite la requête vers le serveur DNS fourni par DHCP, c’est‑à‑dire **pfSense (192.168.1.1)**.
"Non-authoritative answer" =  pfSense n’héberge pas la zone “google.com”. Il interroge les serveurs DNS publics configurés.
##### Test DNS + connectivité :
```
ping google.com
```
![[Pasted image 20260801181109.png]]
![[Pasted image 20260801181141.png]]
=> ping internet fonctionne