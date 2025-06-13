# Présentation et résumé du projet réseau SAE 21

## Contexte du projet

Ce projet a été réalisé dans le cadre de la SAE 21 et a pour objectif la conception, la configuration et la sécurisation d’un réseau local d’entreprise, en utilisant des équipements de niveau 2 (commutateurs) et de niveau 3 (routeurs)[1]. L’ensemble de l’architecture a été simulé sous GNS3.

## Topologie et organisation du réseau

La topologie du réseau est composée de :
- Trois routeurs (R1, R2, R3) interconnectés, assurant la communication interne et l’accès au réseau extérieur (Cloud).
- Deux commutateurs principaux (commutateur-fed et commutateur-1) pour la gestion centralisée des VLAN et la distribution des connexions.
- Plusieurs serveurs dédiés : un serveur DHCP, un serveur de sauvegarde (FTP), un serveur de développement (web), un serveur de production (web).
- Des postes utilisateurs répartis selon trois services : administration, développement, administration système.

## Segmentation et VLAN

Le réseau est segmenté en trois VLAN correspondant à chaque groupe d’utilisateurs :
- **VLAN 100** : Administration (192.168.139.129/29)
- **VLAN 200** : Développeurs (192.168.139.137/29)
- **VLAN 300** : Administrateurs (192.168.139.145/29)

La gestion des VLANs est centralisée sur le commutateur-fed. Le VLAN natif a été déplacé sur le VLAN 999 et tagué pour plus de sécurité. Le routage inter-VLAN est assuré par le commutateur-fed.

## Adressage IP et services réseau

- Le réseau de base (192.168.128.0/20) a été segmenté pour chaque service et pour les liaisons inter-routeurs (/30).
- Le serveur DHCP attribue dynamiquement les adresses IP aux postes clients.
- Les serveurs disposent d’adresses fixes pour garantir la stabilité des services.

## Déploiement des services

- **Serveur FTP (sauvegarde)** : Service FTP avec accès anonyme et comptes utilisateurs spécifiques (Antoine, Elise) avec droits en lecture/écriture.
- **Serveur Web** : Apache installé sur les serveurs de développement et de production. La page web modifiée sur le serveur dev est synchronisée sur le serveur de production via rsync.
- **DHCP** : Attribution automatique des adresses IP aux postes clients.

## Sécurisation du réseau

- **Sécurité des ports** : Sur chaque port des commutateurs, seule la première adresse MAC connectée est autorisée (port-security).
- **ACL sur R2** : Seuls les flux HTTP, SSH (port 22) et rsync (port 873) sont autorisés.
- **ACL sur R3 (routeur de bordure)** : Seuls les flux ICMP et HTTP sont autorisés depuis l’extérieur.
- **Routage dynamique** : RIP v2 assure la mise à jour automatique des routes entre les routeurs.

## Ouverture vers l’extérieur

Le routeur R3 est configuré pour permettre à toutes les machines internes d’accéder au réseau extérieur (Cloud), assurant ainsi la connectivité globale du système.
