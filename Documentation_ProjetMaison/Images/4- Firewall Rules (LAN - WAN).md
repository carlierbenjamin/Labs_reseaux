

Screenshots :
- **Configuration du pare-feu et règle LAN** 
![[Pasted image 20260801154031.png]]
=> le pare-feu est configuré pour autoriser le LAN vers ANY (n'importe où)
-Anti‑Lockout Rule : pfSense autorise **toujours** l’accès à son interface Web (80/443) et SSH (22) depuis le LAN.
-Default allow LAN to any rule (IPv4/IPv6) : Autoriser le trafic IPv4/6 du LAN vers n’importe où (internet, autre LAN...)

- **Configuration du pare-feu et règle WAN** 
![[Pasted image 20260801154424.png]]
=> le pare-feu est configuré pour bloquer le WAN vers LAN
-Block private networks (RFC 1918 networks): Blocage de toutes les adresses privées qui tenteraient d’entrer par le WAN
-Block bogon networks (Reserved Not assigned by IANA): Blocage des réseaux **bogons** (plages non attribuées par l’IANA, plages réservées, plages non encore routées)

#### **VM Wan :
a faire pour le test :
soit : 
- une VM **WAN** (192.168.122.x),
- une VM sur le réseau NAT VirtualBox (10.0.2.x)
##### Test de blocage WAN → LAN 

```
ping 192.168.1.1
```
=> ping doit échouer car blocage machines hors LAN



#### **VM Windows Server** :
##### Test LAN → Internet :
```
ping 8.8.8.8
```
![[Pasted image 20260801151927.png]]
=>ping fonctionne: LAN peut **sortir vers Internet**, NAT fonctionne, et pfSense route correctement.
##### Traceroute pour vérifier le passage vers internet :
```
tracert 8.8.8.8
```
![[Pasted image 20260729214214.png]]
Le traceroute vers **8.8.8.8** démontre que :
- la VM Windows atteint pfSense via **LAN (192.168.1.1)** (*réseau VirtualBox = 192.168.x.x*) : saut 1
- pfSense route correctement vers **WAN (192.168.122.1)** : saut 2
- le NAT VirtualBox fonctionne (**10.0.2.2**) : saut 3
- le trafic sort du réseau virtuel et transite vers le réseau physique (192.168.2.1) : saut 4
- le FAI/fournisseur accès internet (Bell Canada) relaie le trafic vers Google (*142.x.x.x = **adresse publique***) : saut 5 
- transit bell vers google : saut 5 à 10
- google.bx1-montrealgz.net.bell.ca = routeur Google **hébergé dans l’infrastructure Bell** = saut 10
- la destination finale **dns.google (8.8.8.8)** est atteinte  : saut 13
=>  la chaîne réseau est fonctionnelle et conforme au Plan IP.**


#### **VM Ubuntu Desktop :

##### Traceroute vers Internet : 
```
traceroute 8.8.8.8
```
![[Pasted image 20260801175103.png]]
=> Le traceroute vers **8.8.8.8** démontre que :
- la VM Ubuntu Desktop atteint pfSense via **LAN (192.168.1.1)** (*réseau VirtualBox = 192.168.x.x*) : saut 1
- pfSense route correctement vers **WAN (192.168.122.1)** : saut 2
- le routeur interne NAT VirtualBox fonctionne (**10.0.2.2**) : saut 3
- le trafic sort du réseau virtuel et transite vers le réseau internet (* signifie que le routeur suivant ne répond pas aux requêtes ICMP = normal pour beaucoup de routeurs Internet avec traceroute apparemment) : saut 4
=>  la chaîne réseau est fonctionnelle et conforme au Plan IP.**