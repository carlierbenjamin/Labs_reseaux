=> pfSense joue le rôle de NAT

#### **VM Windows Server** :

Page web pfsense: **Firewall → NAT**
![[Pasted image 20260801155533.png]]
=>  pfSense génère **automatiquement** les règles NAT nécessaires pour :
- transformer les IP LAN (192.168.1.x) en IP WAN (192.168.122.175)
- pour sortir vers Internet


##### Test NAT :
```
ping 8.8.8.8
```
![[Pasted image 20260801160245.png]]
=> ping fonctionne, internet atteint. LAN **ne peut pas** atteindre Internet sans NAT, car 192.168.1.x est une adresse privée (non routable sur internet), donc NAT OK.


#### **VM Ubuntu Desktop** :

##### Vérification de l’IP publique simulée :
```
curl ifconfig.me
```
![[Pasted image 20260801181314.png|427]]
=> 70.29.253.137 recu = adresse publique fournie par le FAI réel. Cela ce qui confirme que la machine Ubuntu sort correctement sur Internet. Le trafic transite par pfSense (LAN → WAN), puis par le NAT de VirtualBox avant d’atteindre le service externe. Ce test valide le fonctionnement du routage et du NAT dans l’architecture réseau.


##### Test NAT :
```
ping 8.8.8.8
```
![[Pasted image 20260801181917.png]]
=> ping fonctionne, internet atteint. LAN **ne peut pas** atteindre Internet sans NAT, car 192.168.1.x est une adresse privée (non routable sur internet), donc NAT OK.
