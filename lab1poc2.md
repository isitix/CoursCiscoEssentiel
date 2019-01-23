# Router on a stick

Nous allons à présent paramétrer la partie "WAN" et mettre en place une configuration du type "router on a stick".

## Contenu du POC

- Prendre la partie WAN du schéma intial
- Ajouter les équipements correspondants dans packet tracer
  - Cisco 2960
  - Routeur ISR 4321
  - 2 serveurs
  - 1 poste de travail
  - 1 ASA 5505
- Réaliser la configuration de base du routeur et du switch
- Connecter
  - serveur 1 : port 1
  - serveur 2 : port 7
  - PC : port 13
  - ASA : port 19 switch sur port 0 ASA
  - Routeur : port giga 0 du switch sur port giga 0 du routeur
- Attribuer les VLANs
  - Ports 1 à 6 : vlan 10
  - Ports 7 à 12 : vlan 70
  - Ports 13 à 18 : vlan 130
  - Ports 19 à 24 : vlan 190
- Attribuer les sous-réseaux suivants : 
  - vlan 10 : 12.10.0.0 / 16
  - vlan 70 : 12.70.0.0 / 16
  - vlan 130 : 12.130.0.0 / 24
  - vlan 190 : 12.190.0.0 / 16
- Activer DHCP sur le VLAN du Poste de travail
- Attribuer des adresses IP fixes aux autres équipements :
  - .129 pour les serveurs
  - .1 pour le routeur
  - .254 pour l'ASA
  - .2 pour le switch
- Configurer un trunk entre le switch et le routeur
- Activer le routage entre les réseaux
- Vérifier que vous parvenez à pinger l'ensemble des interfaces

### Configuration des ports d'accès

``` 
enable
conf t
interface range FastEthernet 0/1-6
switchport mode access
switchport access vlan 10
exit
interface range FastEthernet 0/7-12
switchport mode access
switchport access vlan 70
exit
interface vlan 10
no shutdown
exit
interface vlan 70
no shutdown
exit
exit
copy running-config startup-config
```

### Configuration des serveurs

|Serveur | VLAN | Port | IP | Mask | Gateway |
|--------|------|------|----|------|---------|
|Serveur1|10|Fa0/1|12.10.1.1|255.255.0.0|12.10.0.1|
|Serveur2|10|Fa0/2|12.10.1.2|255.255.0.0|12.10.0.1|
|Serveur3|70|Fa0/6|12.70.1.1|255.255.0.0|12.70.0.1|
|Serveur4|70|Fa0/6|12.70.1.2|255.255.0.0|12.70.0.1|

Test de ping S1 => S2, etc...

### Configuration du trunk sur le switch


### Configuration du trunk sur le routeur


## Prochaines étapes

[Lab1Poc3](lab1poc3.md) : configuration de l'ASA