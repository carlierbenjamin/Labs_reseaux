Projet daté de **juillet 2026**.

À la fin de cette première année en Techniques de l’informatique, j’ai eu l’occasion de découvrir les bases du réseau et de la configuration de postes. 
Souhaitant aller plus loin et mieux comprendre la structure d’un réseau réel, j’ai pris l’initiative de concevoir ce projet de virtualisation afin de reproduire une architecture proche de celle que l’on retrouve en entreprise.

L’objectif de ce laboratoire est de **concevoir et déployer une architecture réseau virtuelle fonctionnelle** en utilisant pfSense, GNS3, VirtualBox et plusieurs machines virtuelles. Au fil du projet, j’ai non seulement appliqué des notions vues en cours, mais j’ai aussi développé ma **curiosité**, ma **persévérance** et ma capacité à comprendre un réseau dans sa globalité.

Ce travail m’a amené à :
- **Configurer un pare‑feu pfSense** avec des interfaces WAN et LAN fonctionnelles.
- **Mettre en place un réseau interne (LAN)** incluant DHCP, DNS et routage.
- **Intégrer un réseau externe simulé (WAN)** via VirtualBox NAT.
- **Assurer la communication entre les machines virtuelles** (Windows, Ubuntu).
- **Appliquer des règles de sécurité** (firewall, NAT, isolation WAN/LAN).
- **Tester et valider la connectivité** interne et externe (ping, traceroute, résolution DNS).
- **Documenter l’ensemble de l’architecture** et des configurations réalisées.

Ce projet a été conçu pour **évoluer facilement**, en même temps que les compétences que je développerai au cours de mon DEC :

### **Partie 1 — Réseau simple fonctionnel**
-réalisée-
Construction d’un réseau composé de machines périphériques (virtuelles), partiellement administré et sécurisé via un pare‑feu, un DNS et un DHCP.

### **Partie 2 — Ajout d’un réseau supplémentaire via routeur Cisco**
-A réaliser plus tard-
Extension du laboratoire avec un réseau additionnel derrière un routeur Cisco, permettant d’expérimenter : VLAN, routage inter‑VLAN, OSPF/routage dynamique, ACL/Filtrage.

### **Partie 3 — Extension avec Windows Server**
-A réaliser plus tard-
Évolution vers une architecture réseau plus complète en ajoutant un Windows Server pouvant devenir un **contrôleur de domaine (Active Directory)** et autres services  : DNS interne, DHCP plus avancé, FTP/partage de fichiers, gestion centralisée des utilisateurs, authentification sécurisée.

## **Limites matérielles**

Mon principal facteur limitant est **le manque de RAM sur ma machine hôte** (16 Go), ce qui restreint fortement la réalisation complète du projet, notamment de la partie 3, particulièrement l’exécution simultanée de plusieurs machines lourdes (Windows Server, routeur Cisco, clients supplémentaires).
Note : possibilité d'utiliser Docker pour remplacer quelques machines virtuelles lourdes.
- Partie 1 : pfSense + 1 Windows + Docker ?
- Partie 2 : pfSense + Cisco + Docker ?
- Partie 3 : Windows Server + 1 Windows + Docker ? (isolé du reste du projet?)


## **Conclusion**

Ce laboratoire est conçu pour évoluer d’un réseau simple vers une **véritable infrastructure d’entreprise**, permettant de simuler un environnement réaliste et d’expérimenter des fonctionnalités utilisées dans les réseaux professionnels. Ce projet constitue une base solide pour poursuivre mon apprentissage du réseautage, de la virtualisation et de l’administration système.