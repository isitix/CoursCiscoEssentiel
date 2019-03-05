# Routage

## Rappel des notions

### Autonomous System (AS)

Les routeurs sont regroupés par domaine (ou autonomous system). Un système autonome est un ensemble de routeurs qui partagent les informations entre eux, souvent parce qu'ils sont administrés par la même entité.

### Intérieur / extérieur

Un protocole intérieur est un protocole qui permet de router jusqu'à la station de terminaison du trafic. Un protocole extérieur est un protocole qui permet de router le trafic entre des zones de routage. C'est une notion voisine de celle de desserte locale = intérieur / transit = extérieur.

- Protocoles intérieurs : RIP, EIGRP, OSPF
- Protocole extérieur : BGP

### Distance vector / link state

Deux manières de calculer les routes sont possibles, distance vector ou link state.

Un protocole de type link state entretient une base complète des liens source / destination et a donc une représentation interne de la topologie du réseau. Il calcule ensuite le meilleur chemin en fonction de la topologie du réseau qu'il connaît.

Un protocole de type distance vector est un protocole ou chaque routeur connaît le ou les next hop en fonction de la destination, c'est-à-dire le routeur suivant. Le meilleur routeur suivant est calculé de manière distribué par l'ensemble des routeurs, par inondation.

Le mode de fonctionnement de ces deux types de protocole est très différent :

- pour le link state, seule l'information concernant les voisins est transmise entre les routeurs; le calcul de la route est collectif, la convergence est distribuée mais peut être lente
- pour le distance vector, les routeurs échangent des informations de mise à jour de leur base de liens; le volume d'information échangé et stocké est plus important. Chaque routeur calcule lui-même sa route, ce qui représente également une charge CPU importante. 

Dans les protocoles intérieurs, seul OSPF est de type distance vector. Les autres sont de type link state (eigrp, rip).

### CIDR et route summarization

Les protocoles récents supporter le CIDR (Classless Interdomain Routing) qui permet de router sur un réseau avec des masques variables (/x).

Attention, les protocoles plus anciens (RIPV1 et IGRP notamment) ne supportent pas CIDR.

Pour accélérer le routage et réduire la taille des tables, les routeurs regroupent les routes sur des préfixes identiques (par exemple 192.168.1.0/24 et 192.168.2.0/24 vont être regroupés dans 192.168.0.0/16). Pour que cette "summarization" soit possible et se passe bien, il est nécessaire que le réseau soit organisé pour le permettre en assurant que les sous-réseaux voisins soient sur des préfixes communs pour pouvoir les regrouper.

### Configuration du routage

La configuration du routage intérieur consiste dans un premier temps à :

- Identifier et marquer la liste des routeurs appartenant au domaine intérieur
- S'assurer du transfert de l'information entre ces routeurs
- S'assurer que l'information ne sort pas de ces routeurs
- Gérer les interfaces avec les autres systèmes autonomes (route statique, autre protocole...)
- Fixer le poids des liens pour avoir une bonne répartition des flux
- Tuner, vérifier les problèmes de route summarization
- Gérer les problèmes de disponibilité, perte de liens

## Lab EIGRP

Réaliser le lab accessible gratuitement sur le site de David Bombal :

Les énoncés :

- [Partie 1](https://davidbombal.com/cisco-ccna-packet-tracer-ultimate-labs-eigrp-troubleshooting-lab-1-can-complete-lab/)
- [Partie 2](https://davidbombal.com/cisco-ccna-packet-tracer-ultimate-labs-eigrp-troubleshooting-lab-2-can-complete-lab/)
- [Partie 3](https://davidbombal.com/cisco-ccna-packet-tracer-ultimate-labs-eigrp-troubleshooting-lab-3-can-complete-lab/)
- [Partie 4](https://davidbombal.com/cisco-ccna-packet-tracer-ultimate-labs-eigrp-troubleshooting-lab-4-can-complete-lab/)
- [Partie 5](https://davidbombal.com/cisco-ccna-packet-tracer-ultimate-labs-eigrp-troubleshooting-lab-5-can-complete-lab/)