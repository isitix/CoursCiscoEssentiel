# Configuration et gestion des VLANs

## Types de port

*Port access* : pour les stations (distribution)
*Port trunk* : pour le trafic entre les équipements (concentration)

Une configuration spécifique est mise en place pour la ToIP, soit un trunk intégrant le PC et le téléphone soit une solution (semi-propriétaire) intégrant le VLAN voix. En règle général, la configuration est définie avec l'équipe qui déploie la ToIP, intégrateur ToIP ou fournisseur de solution cloud. Trois besoins doivent être adressés :

- Sécurité de la ToIP
- Espace d'adressage et environnement LAN dédié
  - Options DHCP
  - Bootp, tftp, provisioning des postes
- Mise en oeuvre de la qualité de service

## Tagging

- sur les ports access : Non
- sur les ports trunk : Oui, deux technologies possibles, propriétaire Cisco ou 802.1Q (standard). En général, on privilégie 802.1Q
- pour la ToIP : configuration spécifique, voir ci-dessus

## DTP

DTP = Dynamic Trunking Protocol
C'est un protocole de négociation dynamique du mode du port, entre Access et Trunk, au niveau du port. Si le port est en mode dynamique, le switch détermine automatiquement s'il doit être en mode access ou en mode trunk en fonction de la nature du device connecté au port.

### Intérêt de DTP

limité dans un réseau organisé, peut-être des applications en datacenter avec des switchs virtuels ?

## VTP

VTP = VLAN Trunking Protocol
C'est un protocole inter-switch véhiculant l'information concernant les VLANs et permettant de gérer les VLANs (ajout, suppression).

Les composants :

- Server : un des switches se déclare comme serveur
- Client : switch s'alimentant en information auprès du serveur
- Transparent : switch qui ne prend pas l'information du serveur mais la transmet
- Domaine : est constitué d'un serveur et de ses clients
- Password : c'est ce qui permet de rattacher des switches à un domaine

Pour les membres du domaine non transparents, la gestion des VLANs est réalisé en centrale sur le serveur.

### Intérêt de VTP

Avantage : configuration automatique
Inconvénient : la suppression d'un VLAN sur le serveur entraîne sa suppression en cascade sur tous les équipements connectés

- sur un petit réseau : non
- sur un gros réseau avec beaucoup de VLAN : solutions alternatives
- sur un réseau avec peu de VLANs et beaucoup de switchs : possible

## CDP
Cisco Discovery Protocol : protocole d'information entre les équipements propriétaire Cisco
Il peut être activer au niveau global de l'équipement et au niveau des ports

## Lab

- Ouvrir un nouveau lab
- Ajouter 2 2960 et un 3560
- Connecter les trois switchs comme suit 2960-1 -> 2960-2 -> 3560
- Activer VTP
  - Domaine : imie
  - Password : imie123
  - 3560 en server
  - 2960-1 en client
  - 2960-2 en transparent
- Vérifier que VTP est ok
- Ajouter les VLANs 20, 30 et 40 dans le domaine
- Visibilité des VLANs sur 2960-1 et 2960-2 ?
- Ajouter un VLAN50 sur 2960-2. Que se passe-t-il ?
- Mettre les 12 premiers ports de 2960-2 sur VLAN50 et les 12 derniers en access sur VLAN 50
- Que se passe-t-il si l'on déplace les connexions du 2960-1 et du 3560-1 sur l'un des 12 premiers ports ? sur l'un des douze derniers ports ?
- Revenir à la configuration de départ
- Vérifier que CDP est activé sur les trois équipements
- Visualiser les informations disponibles
- Désactiver CDP sur le 2960-2, que se passe-t-il ?
- Réactiver
- Désactiver CDP sur le port trunk du 2960-2 vers 2960-1, que se passe-t-il ?

## Autre LAB

Exemple standard sur packet tracer <https://www.packettracernetwork.com/labs/lab3-vlanvtpconfig.html>