

#### **VM Windows Server** :

##### Page web pfsense: **Services → DHCP Server**
![[Pasted image 20260801152618.png]]
=>  Plage IP configurée du serveur DHCP : 192.168.1.100 → 200
##### Vérification de l’adresse actuelle : 
```
ipconfig
```
![[Pasted image 20260801134108.png|427]]
=> la VM windows server a une IP actuelle valide (192.168.1.100).

##### Renouvellement DHCP (Windows) :
```
ipconfig /renew
```
![[Pasted image 20260801134134.png]]
=> La commande pour redemander une IP s’exécute sans erreur. L’adresse reste 192.168.1.100. car le bail DHCP ne doit pas être expiré.

##### Vérification du bail DHCP et ses paramètres :
```
ipconfig /all
```
![[Pasted image 20260801134318.png]]
=> DHCP actif, IP serveur DHCP pfsense : 192.168.1.1, adresse IPV4 préférée : 192.168.1.100, bail obtenu le 1/08/2026 et expirant le 01/08/2026.

##### Test du serveur DHCP

Ping de la passerelle (pour valider la connectivité après attribution IP) :

```
ping 192.168.1.1
```
![[Pasted image 20260801143258.png]]
=> passerelle répond correctement.


#### **VM Ubuntu Desktop :

```
ip a
```
![[Pasted image 20260801175709.png]]
=>La machine Ubuntu Desktop a une adresse IPv4 active valide 192.168.1.101. et une passerelle active (192.168.1.1) via le serveur DHCP de pfSense