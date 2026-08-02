Screenshots :
- Windows : `ipconfig`
- Ubuntu : `ip a`
- Passerelle et DNS visibles

**Objectif :** prouver que les VMs reçoivent les bonnes IP du DHCP.

### #### **VM Windows Server** :
##### Vérification de configuration de la VM Windows server

```
ipconfig
ping 192.168.1.1
```
![[Pasted image 20260801142510.png]]
=> la VM windows server a une IPv4 actuelle valide (192.168.1.100). et une passerelle active (192.168.1.1).

![[Pasted image 20260801162232.png]]
=> ping passerelle de pfsense fonctionne (192.168.1.1)

##### Vérification de connectivité entre la VM Windows server et VM Ubuntu Desktop

```
ping 192.168.1.101
```

![[Pasted image 20260802095036.png]]
=> machine Ubuntu Desktop possède une IP 192.168.1.101. Le ping fonctionne. 
La machine Ubuntu Desktop répond correctement aux requêtes ICMP. Cela confirme que :
- les deux machines sont bien situées dans le même réseau LAN (192.168.1.0/24)
- le switch virtuel GNS3 est fonctionnel
- le DHCP pfSense a attribué les adresses correctement
- aucune règle firewall ne bloque le trafic ICMP
- la connectivité interne du LAN entre les deux hôtes est opérationnelle

#### **VM Linux Desktop :

##### Vérification de configuration de la VM Ubuntu Desktop

```
ip a
```
![[Pasted image 20260801171736.png]]
=>La machine Ubuntu Desktop a une adresse IPv4 active valide 192.168.1.101. et une passerelle active (192.168.1.1) 

```
ping 192.168.1.1
```
![[Pasted image 20260801171946.png]]
=> ping passerelle de pfSense fonctionne
```
dig google.com
```
![[Pasted image 20260801172201.png]]
=> requête transite du LAN vers pfSense, puis vers Internet via VirtualBox NAT. 
Le serveur DNS local (127.0.0.53) relaie la requête vers pfSense, ce qui confirme le bon fonctionnement du routage et du NAT.
-status: NOERROR : Le DNS fonctionne et la requête a été résolue
-ANSWER: 6 : on obtient 6 adresses IPv4 de Google
-SERVER: 127.0.0.53#53 : Ubuntu interroge son DNS local


##### Vérification de connectivité entre la VM Ubuntu Desktop et VM Windows server

```
ping 192.168.1.100
```
![[Pasted image 20260802095650.png]]
=> machine Windows Server possède une IP 192.168.1.100. Le ping fonctionne. 
La machine Windows Server répond correctement aux requêtes ICMP. Cela confirme que :
- les deux machines sont bien situées dans le même réseau LAN (192.168.1.0/24)
- le switch virtuel GNS3 est fonctionnel
- le DHCP pfSense a attribué les adresses correctement
- aucune règle firewall ne bloque le trafic ICMP
- la connectivité interne du LAN entre les deux hôtes est opérationnelle
