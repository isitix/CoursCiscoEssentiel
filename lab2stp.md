# Spanning tree protocol (STP)

## Usage

Deux usages principaux :

- Prévenir les boucles dans le réseau et les tempêtes de broadcast qu'elles déclenchent
- Redonder les équipements (en créant des boucles avec des liens désactivés)

## Difficultés

Principales difficultés de paramétrage

- Convergence lente en version standard
- Instabilité dans certaines architectures (lien actif puis inactif puis actif...)
- Paramétrage pour le choix de la topologie cible en mode de fonctionnement normal en fonction des priorités des stations

## Principe de fonctionnement

Pour plus de détails, voir [Wikipedia](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol)

A partir d'un réseau maillé ou partiellement maillé, le spanning tree est un algorithme distribué qui permet de constituer un arbre en coupant (désactivant) certains liens. Les étapes de fonctionnement sont les suivantes :

- L'id d'un équipement est une priorité stp (un paramètre que l'on définit) concaténée avec son adresse MAC
- Choix d'un *root node* pour l'ensemble du réseau 
  - C'est le noeud racine de l'arbre vers qui tout le trafic converge
  - Un protocole d'élection est défini, avec des priorités en fonction de la priorité de l'équipement; les équipements dont l'id est le plus bas ont la priorité la plus forte
- Choix d'un root port par équipement. Le port root est le port le moins coûteux pour atteindre le root bridge. Le coût d'un port est inversement proportionnel à la bande passante sur le lien vers le root bridge par ce port; plus la bande passante est élevée, plus le coût est faible
- Des règles de suppression des liens redondants sont définies en fonction des règles de priorité entre les équipements et les ports

## Couche réseau

STP agit au niveau d'ethernet.

Les paquets échangés sont des BPDU, Bridge Protocol Data Unit.

## Etat des ports

Quatre états sont possibles pour les ports réseau :

- Blocking : port fermé parce qu'il créerait une boucle s'il était ouvert
- Listening : collecte d'information via les BPDU, clacul de la position du switch et de ses ports
- Learning : en cours d'activation, alimentation de la table des adresses MAC
- Forwarding : actif, émet et reçoit des paquets sur le réseau
- Disabled : port désactivé par l'administrateur

## Trois configurations du protocole

### Spanning tree

Version standard normalisé

Avantages : possibilité d'utiliser spanning tree en environnement multi-propriétaire

Inconvénients : convergence très lente

### Rapid spanning tree

Version propriétaire Cisco

Avantages : convergence rapide
Inconvénients : réservé à des switchs Cisco

### PortFast

Procédure spécidique Cisco d'activation rapide des ports Access
Voir [ici pour plus de détails](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst4000/8-2glx/configuration/guide/stp_enha.html)

## Cas d'usage
Il faut impérativement protéger le réseau contre les boucles.

En environnement de bureaux, elles sont peu probables, s'il n'y a pas de hubs. On peut envisager d'activer PortFast sur l'ensemble des ports d'accès, tout en maintenant un mécanisme pour protéger le réseau si une boucle est créée sur un switch

En environnement local technique et salle serveur, les boucles sont plus probables (erreur de manipulation des administrateurs). La problématique de convergence des ports est également moins importante, les ports passant moins souvent par l'état down. STP a alors deux rôles :

- Bloquer les boucles
- Permettre la redondance des liens

## LAB

- Monter 3 switches 2960 en triangle sur leurs ports giga, Access0, Access1, Distribution0
- Déployer 3 PCs et un serveur DHCP sur Distribution1
- Mettre en place le spanning tree standard
- Visualiser l'état des noeuds et des ports
- Quelle est la topologie de convergence ?
- Déconnecter un lien
- Temps de convergence ?
- Reconnecter le lien
- Passer en mode rapid
- Déconnecter un lien
- Temps de convergence ?
- Modifier les priorités pour que Access0 soit le root node
- Quelle est la topologie de convergence ?
- Déconnecter puis reconnecter un PC
- Combien de temps faut-il pour que le port soit à nouveau forwarding ?
- Passer les ports d'accès en mode PortFast
- Déconnecter et reconnecter un PC
- Combien de temps faut-il pour que le port soit à nouveau forwarding ?
- Connecter deux ports accès de Distribution0 entre eux 
- Que passe-t-il ?
- Ajouter un deuxième switch de distribution Distribution1 en double attachement sur les Access
- Ajouter deux PCs sur Distribution1
- Pinger un PC de D0 depuis D1. Par quel A le trafic passe-t-il ?
- Ajouter un lien entre les ports 24 de D0 et D1. 
Que se passe-t-il ?
- Passer les ports 24 de D0 et D1 en rapid STP. 
- Quelle est la topologie de convergence ?
- Retirer ce lien
- Migrer les ports 1 à 12 de D0 et D1 vers le VLAN 44.
- Quel est l'impact sur la configuratoin STP
