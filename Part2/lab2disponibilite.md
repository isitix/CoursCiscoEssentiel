# Lab2 : redondance 1+1 d'un équipement

## Objectifs

- HSRP

## Secours et haute disponiblité

### Solutions étudiées

Plusieurs solutions sont disponibles pour assurer le secours du réseau :

- Agrégation de liens et partage de charge (LACP)
- Spanning tree
- Routage dynamique
- Stacks
- Redondance des équipements 1+1 (HSRP)

Ces solutions ont chacun des applications différentes. Elles ne répondent, individuellement, qu'à une partie du besoin. C'est l'association de ces différentes technoligies au sein d'une architecture cohérente qui permet de construire un réseau réellement robuste.

### Enjeux de la redondance

Les principaux enjeux d'un dispositif de redondance et de haute disponibilité sont :

- La *détection de la panne*, c'est-à-dire, quel critère conduit à décider qu'il y a une panne et à basculer vers les secours. Le sujet est difficile parce que certaines pannes sont très transientes, d'autres ne sont pas franches et une situation plus ou moins dégradée peut perdurer. 
- Le *niveau de redondance* : il s'agit d'un compromis entre le coût et la capacité à définir un mode dégragé utile.
- Le *mécanisme de basculement* : le basculement nécessite un délai plus ou moins long en fonction du temps de détection, des durées intrinsèques du réseau (timeout de connexion par exemple) et du temps de convergence du nouveau réseau. Le basculement peut conduire à une nouvelle topologie du réseau très différente du réseau initial avec des impacts importants en terme de flux, qui peuvent conduire à de nouvelles pannes si certains équipeements sont sursollicités.
- Le *mode de basculement* : il peut s'agir d'un mode secours, avec potentiellement des pertes de paquets ou des pertes de session ou d'un mode transparent, sans perte pour l'utilisateur.
- Le *mécanisme de retour au mode nominal* : dans certains cas, il peut être préférable de considérer que le mode secours est le nouveau mode nominal. Le retour au nominal peut être nécessaire si le secours est dégradé, ou au contraire être un facteur d'instabilité.

## HSRP

HSRP est une solution très répandue pour assurer le secours matériel des routeurs en 1+1. Des technologies voisines sont VRRP et GLBP.

- [Description générale](https://en.wikipedia.org/wiki/Hot_Standby_Router_Protocol)  de HSRP
- [Guide de configuration](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/software/release/12-2_55_se/configuration/guide/3750xscg/swhsrp.html) fourni par Cisco
- [Explications](https://www.cisco.com/c/en/us/support/docs/ip/hot-standby-router-protocol-hsrp/13780-6.html) concernant les paramètres preempt et track

## Lab

- Réaliser le [lab packet tracer](lab2hsrp.pkt)
