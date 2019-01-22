# Fondamentaux techniques du LAB 1 / POC1

## Couches OSI

Nombreuses ressources en ligne, par exemple <https://fr.wikipedia.org/wiki/Mod%C3%A8le_OSI>

## Les normes de câblage

Le câblage le plus fréquemment rencontré est un câblage cuivre, ethernet, avec des prises RJ45 et du câblage catégorie 5, 6 ou 7, blindée (Shielded TP) ou pas (Unshielded TP).

Nombreuses ressources en ligne, par exemple : 

- <https://reseau-vdi.fr/cablage-rj45/> pour la pause des câbles
- <https://reseau-vdi.fr/cable-ethernet-grade-3-ou-categorie-6/> pour le choix de la catégorie

Points à retenir :

- Vérifier la qualité du câble employé,
- Vérifier que le câblage est bien structuré,
- Demander les rapports de vérification de l'installateur
- Calculer la longueur des cordons entre le panneau de brassage et l'équipement
- Choisir des codes couleurs qui facilitent le repérage
- Soigner le choix des câbles pour les liens d'aggrégation qui nécessitent des débits plus élevés
  - Rocade en fibre sur la hauteur d'un immeuble
  - Câblage 1Gbps ou 10Gbps
- Pour la fibre
  - Monomode / multimode
  - Module GBic

Pour info, les GBIC sont adaptés à la fibre monomode et nécessitent des équipements d'adaptation pour connecter une fibre multimode mais les règles dépendent aussi de la longueur du câble ... <https://www.cisco.com/c/en/us/td/docs/routers/7200/install_and_upgrade/gbic_sfp_modules_install/5067g.html#wp29618>

Pensez à vérifier les indicateurs permettant de déceler un problème sur un câble ou un fourreau de câble :

- Pertes de paquets
- Temps de transit
- etc...

Les problèmes peuvent provenir du câble ou des prises.

Sur une nouvelle installation ou dans un existant, faites le point avec le responsable du câblage ou faites qualifier le câblage et pensez également à vérifier la compatibilité des équipements avec le câblage envisagé.

## Ethernet

Trois ressources possibles :

- <https://en.wikipedia.org/wiki/Ethernet> pour une définition générale
- <https://en.wikipedia.org/wiki/Ethernet_frame> pour la structure de la trame
- <https://en.wikipedia.org/wiki/MAC_address> pour la structure des adresses MAC
- <https://en.wikipedia.org/wiki/Jumbo_frame> pour des détails concernant les jumbo frames

*Quelques points à retenir :*

- la trame comporte l'adresse MAC destination et l'adresse MAC source, chacune sur 6 octets soit 12 hexa (12:34:56:78:9A:BC) 
- le payload (= le paquet IP inclus) fait 1500 octets sauf usage des jumbo frames
- le champ 802.1Q de 4 octets est utilisé pour tagger le VLAN qui est mécanisme niveau 2
- les adresses MAC sont hiérarchisées et les 24 premiers  bits soit les 6 premiers hexa correspondent, pour des adresses universelles au fournisseur de la carte qui porte l'adresse
- le format 48 bits historique dit EUI-48 utilisé par ethernet est étendu par un format à 68 bits dit EUI-64 utilisé ailleurs <https://networkengineering.stackexchange.com/questions/23566/what-are-eui-48-and-eui-64>
- Une carte réseau ne décode que les trames avec une adresse MAC destination qu'elle gère, sauf si elle est en promiscuous mode
- Une trame avec destination FF:FF:FF:FF:FF:FF est une trame broadcast
- une trame avec le bit de poids faible à 1 est une trame multicast décodée par les stations ayant enregistré l'adresse multicast correspondante (abonnées)

## IP V4

Nombreuses ressources en ligne : 

- Présentation générale du protocole <https://en.wikipedia.org/wiki/Internet_Protocol>
- Détail de la V4 et de la structure du paquet V4 <https://en.wikipedia.org/wiki/IPv4>
- Liste complète des protocoles transportés dans IP <https://en.wikipedia.org/wiki/List_of_IP_protocol_numbers>

Que retenir ?

- Adresse source et destination font 32 bits
- le header fait 256 bits

Un paquet IP est un objet relativement simple, contenant un header comportant :

- une adresse source,
- une adresse destination,
- quelques octets d'option

suivi un payload

Parmi les options du header, trois sont importantes :

- Le flag fragment qui découpe les gros paquets pour les loger dans des trames plus petites
- Le champ DSCP qui peut être utilisé pour gérer la qualité de service
- Le flag TTL qui est un compteur de la durée de vie restant du paquet
- Le checksum qui vérifie l'intégrité du header (mais pas du payload)

Toutes les autres informations que l'on traite habituellement lorsque l'on analyse du trafic dit IP, numéros de port, etc..., sont en fait contenus dans la partie payload d'IP et appartiennent aux protocoles au dessus.

Les principaux protocoles au-dessus (que l'on rencontre dans le payload) sont :

- TCP
- UDP
- ICMP
- OSPF

## ARP

Ressource possible : <https://en.wikipedia.org/wiki/Address_Resolution_Protocol>

Points importants :

- Permet de trouver l'adresse MAC d'une machine correspondant à une adresse IP
- A l'interface entre la couche liaison et la couche IP
- Standard Internet
- Broadcast sur un segment de LAN (broadcast MAC, adresse MAC de destination = FF:FF:FF:FF:FF:FF)
- Plusieurs types de message
  - Request
  - Reply
  - Probe
  - Announcement

## DHCP

Ressource possible : <https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol>

Points importants :

- Permet l'attribution d'une IP à une station
- Client-serveur : le client envoie une demande d'IP au serveur qui lui attribue une adresse
- Broadcast ethernet
- Discover - Offer - Request - Acknowledge
- Le serveur peut envoyer des paramètres supplémentaires au client
- Si plusieurs serveurs sont présents sur le réseau, le client indique dans le message REQUEST quelle offre il prend

## ICMP

Ressource possible : <https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol>

C'est un protocole d'échange de messages de contrôle du réseau au niveau IP.

Le format est défini dans un RFC (et sur la page Wikipedia). Il comprend notamment :

- le type de message
- le code du message
- un checksum
- le header et les 8 premiers octets du paquet auquel il répond si pertinent

En pratique, il nous intéresse parce qu'il intervient pour :

- le ping (type 8 code 0 echo request; type 0 code 0 echo response)
- traceroute (TTL)
- destination unreachable
- messages de routage

## Quizz
[Quizz concernant les fondamentaux LAN](https://goo.gl/forms/pEL958xrJduLg6uo2)