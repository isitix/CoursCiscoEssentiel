# Lab 1 : gestion des équipements

## Objectifs

- Utilisateurs et droits
- Authentification simple
- Authentification Radius, Tacacs
- Accès port console, SSH
- Mise à jour
- SNMP

## Utilisateurs et droits

### Privilèges

Les privilèges vont de 0 à 15
15 = administrateur

### Accès au système

Deux modes :

- Console (câble local) : 1 port (port 0)
- VTY (telnet ou SSH) : 16 ports de 0 à 15

Pour utiliser SSH, ne pas oublier de générer ou uploader une clé locale avant d'activer le service.

### Moyens d'authentification

Il y a quatre moyens d'authentification : 

1. NONE = on désactive l'authentification
2. default password
3. local database
4. AAA service (serveurs externes)

## SNMP

### Présentation

SNMP = Simple Network Management Protocol

SNMP est un protocole en mode push et pull :

- en mode push, l'équipement envoie des messages (SNMP trap) à un outil de supervision,
- en mode pull, le serveur de commande émet des requêtes vers l'équipement, soit en consultation (Read only) soit en modification (Read/write)

### Versions

Il y a trois versions de SNMP, V1, V2, et V3. Les trois versions fonctionnent en UDP ou TCP. UDP est avantageux pour la remontée d'information (push), TCP est a priori plus intéressant en mode pull.

V1 a la réputation d'être peu sécurisée, ce qui a conduit à l'écarter. L'authentification s'effectue en claire, par un "secret" partagé qui est le nom de la communauté. 

Il est possible de l'utiliser sur un VLAN d'administration fermé mais il est dangereux de l'utiliser sur un réseau ouvert.

V3 est la version courante. Elle est correctement sécurisée. Les variables de compteurs sont de plus étendues à 64 bits au contre 32 dans la V1.

### MIB

SNMP s'appuie sur un modèle arborescent et normalisé de représensation de l'information de l'équipement, la MIB (Management Information Base).

### Informations complémentaires

- Différences entre [les trois versions](https://www.logicmonitor.com/blog/whats-with-the-different-snmp-versions-s1-v2c-v3/) de SNMP
- [Article Wikipedia](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol)
- Des [recommandations de Cisco](https://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/20370-snmpsecurity-20370.html) pour sécuriser SNMP

## Lab 1.1 : révision de la partie 1 du cours, connexion SSH

- Télécharger [le fichier du lab ici](lab1management.pkt)
- Réaliser le lab en suivant les instructions
- Vérifier la configuration spanning tree en vous inspirant de [la vidéo suivante](https://youtu.be/_ZCFJtE_FXM)

## Lab 1.2 : authentification Tacacs

- Lire [l'article](https://www.networkworld.com/article/2838882/radius-versus-tacacs.html) comparant Radius et TACACS
- Regarder la vidéo d'une [version complète](https://youtu.be/WaS9BRNb4Yw) du lab en vidéo
- Réaliser la [version simplifiée](lab1tacacs.pkt) du lab

## Lab 1.3 : SNMP

- Regarder [la vidéo du lab complet](https://youtu.be/5h0fN0j2XS8) de David Bombal
- Réaliser [la version simplifiée](lab1snmp.pkt) suivante

## Mises à jour

Le firmware est un fichier stocké sur la mémoire flash de l'équipement. Pour mettre à jour, les opérations suivantes sont nécessaires :

- Télécharger le nouveau firmware
- Vérifier son empreinte MD5
- L'uploader sur l'équipement en SCP (plus simple et plus sûr) ou TFTP si l'équipement ne support pas SCP ou s'il n'est pas possible d'accéder en SCP
- Modifier la configuration de l'équipement pour faire pointer vers le nouveau firmware
- Faire un reload pour charger le nouveau firmware

L'opération peut très facilement être annulée en pointant vers l'ancien firmware, si ce dernier n'a pas été supprimé de la mémoire flash de l'équipement.

Nous testerons cette procédure sur le matériel de l'IMIE.