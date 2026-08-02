README — Lab réseau GNS3 / pfSense / VirtualBox / KVM

-> Présentation
Ce dépôt contient mon laboratoire réseau réalisé avec GNS3, pfSense, VirtualBox et QEMU/KVM.
Le but du projet est de construire un environnement fonctionnel pour tester :
-Routage LAN ↔ WAN
-Double NAT (libvirt/KVM GNS3 → VirtualBox → Internet)
-Firewall pfSense
-DHCP / DNS
-Tests de connectivité (ping, traceroute)

-> Documentation technique
Ce lab me sert pour pratiquer la virtualisation et la configuration réseau dans un environnement hybride/virtuel.

-> Architecture réseau
+ Hyperviseurs :
-GNS3 VM : backend QEMU/KVM
-VirtualBox : hôte Windows + VMs LAN

+ pfSense
-WAN (em0) : 192.168.122.175
-Réseau : 192.168.122.0/24 (libvirt/KVM-> GNS3)
-Passerelle : 192.168.122.1
-LAN (em1) : 192.168.1.1/24
-DHCP : 192.168.1.100–200
-DNS : 192.168.1.1

+VirtualBox NAT
-IP VM : 10.0.2.15
-Passerelle : 10.0.2.2
-Rôle : sortie Internet

+Machines LAN
-Windows Server - Windows 11
-IP : 192.168.1.100
-Passerelle/Gatteway : 192.168.1.1

+Ubuntu Desktop
-IP : 192.168.1.101
-Passerelle/Gatteway : 192.168.1.1

-> Chemin réseau (double NAT)
Le trafic passe par :
LAN → pfSense LAN → pfSense WAN (KVM) → VirtualBox NAT → Internet
GNS3 gère automatiquement le lien entre le réseau KVM/Gns3 (192.168.122.x) et VirtualBox NAT (10.0.2.x).

-> Tests
+ Ping LAN → pfSense
ping 192.168.1.1
Résultat : OK

+ Traceroute Windows → Internet
tracert 8.8.8.8
Chemin observé :
-pfSense LAN
-pfSense WAN passerelle
-VirtualBox NAT
-Routeur Bell
-réseau Principal FAI/Backbone Bell
-Destination atteinte

+ Traceroute Ubuntu → Internet
traceroute 8.8.8.8
Résultat similaire → Internet OK

-> Contenu du dépôt
documentation
00 – Vue Générale et architecture…
01 – Virtualisation VirtualBox
02 – Configuration GNS3 Desktop
03 – Configuration réseau et interfaces…
Images
README.md

-> Objectifs
Comprendre un environnement multi‑hyperviseur
Configurer pfSense dans GNS3
Tester un double NAT réel
Documenter un lab réseau complet

-> Auteur
Benjamin Carlier   
Québec, Canada
DEC Techniques de l’informatique – 1ère année
Réseau & Virtualisation
