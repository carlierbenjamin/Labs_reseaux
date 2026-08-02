#### **VM pfSense :

 ##### **Vérification de Interface WAN - em 0 :** 
```
ifconfig em0
```
![[Pasted image 20260729213143.png]]
=> 	- **IPv4 (inet): 192.168.122.175**
	- **Masque : 0xffffff00 (hexadécimal)  →  255.255.255.0 (décimal)
	- **Broadcast : 192.168.122.255**
	- **MAC (ether): 0c:e3:98:8b:00:00**

##### Vérification de Interface **LAN** - em 1 : 
```
ifconfig em1
```
![[Pasted image 20260729213223.png]]
=> 	-  **IPv4 (inet) : 192.168.1.1**
	- **Masque : 0xffffff00 (hexadécimal)  →  255.255.255.0 (décimal)
	- **Broadcast : 192.168.1.255**
	- **MAC : 0c:e3:98:8b:00:01**


#### **VM Windows Server** :

##### Ping de la passerelle LAN :
```
ping 192.168.1.1
```
![[Pasted image 20260729214019.png]]
=> passerelle répond

##### Traceroute vers Internet : 
```
tracert 8.8.8.8
```
![[Pasted image 20260729214214.png]]
=> Le traceroute vers **8.8.8.8** démontre que :
- la VM Windows Server atteint pfSense via **LAN (192.168.1.1)** (*réseau VirtualBox = 192.168.x.x*) : saut 1
- pfSense route correctement vers **WAN (192.168.122.1)** : saut 2
- le le routeur interne NAT VirtualBox fonctionne (**10.0.2.2**) : saut 3
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
