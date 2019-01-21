# POC1 : lan basic

## Objectif

Tester un lan basic avec les machines prévus dans le plan initial dur réseau

## Réalisation

BOM

### Initialisation de l'environnement packet tracer

- Installer et démarrer packet tracer
- Prendre un switch 2960
- Prendre 3 PC, un serveur
- Connecter le serveur sur le port 0/1, les PCs sur les ports 2, 3 et 4
- Définir le plan d'adressage IP
  - Adresse IP d'administration du switch (et sous-réseau)
  - Plage DHCP (sous-réseau)
  - Adresse IP du serveur (sous-réseau)

### Première connexion au switch

- Se connecter au switch
- Renommer le switch en imie-sw1
- Activer le chiffrement des mots de passe
- Définir le mot de passe enable à imie123
- Modifier le message du jour(motd) "hello imie-sw1"

### Sauvegarde / restauration de configuration

- Enregister la configuration actuelle en configuration de démarrage
- Modifier un paramètres (banner motd par exemple) sans sauvegarder
- Recharger la configuration => perte de la modification ?
- Visualiser la configuration en cours et la configuration sauvegardée

### Analyse de l'état du switch

- Afficher les informations concernant le matériel (version firmware)
- Afficher la liste des ports et leur état
- Afficher la liste des VLANs
- Afficher les principaux compteurs
- Configurer l'heure du switch

### Paramétrage IP et DHCP

- Définir l'adresse IP d'administration du switch
- Définir l'adresse IP du serveur
- Activer et configurer DHCP sur la plage prédéfinie
- Activer le client DHCP sur les trois PCs
- Verrouiller le PC2 sur une adresse IP spécifique via DHCP
- Vérifier que les trois PC ont bien une adresse
  - Directement sur les PCs
  - En visualisant les données DHCP du switch
- Envoyer un ping du PC1 vers le PC2 et du PC3 vers le PC1
- Visualiser la table ARP du switch
- Revenir en arrière sur le paramétrage de l'adresse du PC2

## Technologies abordées dans ce premier lab

- Câblage réseau
- Ethernet
- ARP
- ICMP
- DHCP
- IP / Adressage IP

Pour plus de détails, voir le document ["bagage technique minimum"](bagagetechniquelab1poc1.md).

## Fin du POC1, prochaines étapes :

[Quizz du POC](https://goo.gl/forms/w5P1q7Pyi7i2lEax2)
[Accès au POC2](lab1poc2.md)