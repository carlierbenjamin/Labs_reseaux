=>  VirtualBox joue le rôle de NAT (par défaut) 
attention: sans pfsense: plus de firewall!

Screenshots :
- Paramètres du NAT VirtualBox
![[Pasted image 20260801163000.png]]
=> La GNS3 VM est configurée avec l’adaptateur 1 en mode NAT ce qui permet à pfSense de recevoir une adresse WAN (192.168.122.175) via VirtualBox, qui joue le rôle de routeur NAT simulant un fournisseur d’accès Internet. 
Cette configuration est essentielle pour permettre au LAN de sortir vers Internet via pfSense.

- Paramètres de l’adaptateur Host-only (192.168.56.1)
![[Pasted image 20260801163120.png]]
=> L’adaptateur 2 de la GNS3 VM est configuré en mode Host‑Only (réseau 192.168.56.0/24). Ce réseau isolé permet la communication interne entre VirtualBox et GNS3, sans accès Internet. Il ne transporte ni le LAN ni le WAN de pfSense, garantissant que tout le trafic LAN passe exclusivement par pfSense.

**Objectif :** prouver que ton WAN pfSense est bien connecté à VirtualBox NAT.

#### **VM Windows Host** :
##### Vérification de la présence de carte VirtualBox (Windows Host)
```
ipconfig
```
![[Pasted image 20260801164213.png]]
=> PC hôte possède une interface **Host‑Only VirtualBox**, IPv4 192.168.56.1

#### **VM Windows Server :

##### Vérification de connectivité vers carte VirtualBox (Windows Host)
```
ping 192.168.56.1
```
![[Pasted image 20260801164623.png]]
=> ping échoue parce que le LAN pfSense (192.168.1.0/24) est totalement isolé du réseau Host‑Only VirtualBox (192.168.56.0/24). Le test est correct.

##### Test de sortie Internet via NAT :
```
ping 8.8.8.8
```
![[Pasted image 20260801165100.png]]
=> Le ping vers 8.8.8.8 fonctionne, car le LAN (192.168.1.0) sort via pfSense, pfSense effectue le NAT LAN vers WAN (192.168.122.175), VirtualBox NAT fournit ensuite l’accès Internet.
Le routage LAN → pfSense → WAN → Internet est opérationnel.

