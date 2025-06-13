Projet SAE 21 – Conception et Sécurisation d’un Réseau d’Entreprise

1. Contexte et objectifs
Ce projet, réalisé dans le cadre de la SAE 21, a pour but de mettre en pratique la conception, la configuration et la sécurisation d’un réseau local d’entreprise. L’architecture repose sur des équipements de niveau 2 (commutateurs) et de niveau 3 (routeurs), avec la mise en place de services essentiels et de règles de sécurité. L’ensemble du projet a été modélisé et testé sous GNS3.

2. Topologie du réseau
La topologie du réseau s’articule autour de :
    
    Trois routeurs (R1, R2, R3) assurant l’interconnexion interne et l’accès au réseau extérieur (Cloud).
    Deux commutateurs principaux (commutateur-fed et commutateur-1) pour la gestion centralisée des VLAN et la distribution des connexions.
    Plusieurs serveurs dédiés : serveur DHCP, serveur de sauvegarde (FTP), serveur de développement (web), serveur de production (web).
    Des postes utilisateurs répartis par service : administration, développement, administration système.

Le schéma ci-joint illustre la structure du réseau, la segmentation des VLAN et la répartition des équipements.

3. Segmentation du réseau et gestion des VLAN
Le réseau de base attribué est 192.168.128.0/20. Il a été segmenté en sous-réseaux pour isoler les différents services et utilisateurs, avec l’utilisation de masques variables :
    
    VLAN 100 : Administration – 192.168.139.129/29
    VLAN 200 : Développeur – 192.168.139.137/29
    VLAN 300 : Administrateur – 192.168.139.145/29

La gestion des VLANs est centralisée sur le commutateur-fed. Le VLAN natif a été déplacé sur le VLAN 999 et tagué pour renforcer la sécurité. Le routage inter-VLAN est assuré sur le commutateur-fed.
Un équilibrage de charge est mis en place entre les deux commutateurs via le protocole Spanning-Tree, chaque lien dédié à un VLAN, avec bascule automatique en cas de panne d’un lien.

4. Adressage IP
    Les sous-réseaux sont alloués pour chaque VLAN, pour les serveurs et pour les liaisons inter-routeurs (en /30).
    Les serveurs disposent d’adresses fixes, tandis que les postes utilisateurs reçoivent leurs adresses via le serveur DHCP.

5. Déploiement des services réseau
Serveur DHCP
    Attribue dynamiquement les adresses IP aux postes clients.

Serveur FTP (sauvegarde)
    Service FTP avec accès anonyme autorisé.
    Comptes utilisateurs spécifiques (Antoine, Elise) avec droits en lecture/écriture.

Serveurs Web (dev et production)
    Apache installé sur les deux serveurs.
    La page web du serveur dev est modifiée puis synchronisée vers le serveur de production via rsync.

6. Sécurisation du réseau
Port-security
    Sur chaque port des commutateurs, seule la première adresse MAC connectée est autorisée.

ACL sur R2
    Seuls les flux HTTP, SSH (port 22) et rsync (port 873) sont autorisés.

ACL sur R3 (routeur de bordure)
    Seuls les flux ICMP et HTTP sont autorisés depuis l’extérieur.

Routage dynamique
    RIP v2 assure la mise à jour automatique des routes entre les routeurs.

7. Accès au réseau extérieur
    Le routeur R3 est configuré pour permettre à toutes les machines internes d’accéder au réseau extérieur (Cloud).

8. Compétences mobilisées
Ce projet m’a permis de :

    Concevoir une architecture réseau complète et sécurisée.
    Configurer des équipements réseau avancés (VLAN, routage, port-security, ACL).
    Déployer et synchroniser des services applicatifs sur des serveurs Linux.
    Appliquer des politiques de sécurité réseau adaptées à un contexte professionnel.
    Utiliser GNS3 pour la simulation et la validation de l’infrastructure.

9. Conclusion
Ce projet illustre l’ensemble des étapes nécessaires à la mise en place d’un réseau d’entreprise moderne, de la conception à la sécurisation, en passant par le déploiement des services essentiels. Il constitue une expérience concrète et professionnalisante, valorisable dans tout portfolio technique.
