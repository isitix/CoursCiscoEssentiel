# Configuration d'un réseau de management

## Dans un environnement vide

- Mettre en place un 2960
- Attribuer une adresse au switch sur son interface VLAN1 (192.168.0.1)
- Connecter un serveur DHCP et une station au switch
- S'assurer que la station a bien une adresse
- S'assurer que l'on peut se connecter au switch en telnet / SSH
- Déplacer tous les ports sauf le 24 vers le VLAN 10
- Vérifier que le réseau fonctionne toujours (dhcp et station)
- Mettre une station avec une IP fixe sur le port 24
- Vérifier que la station a bien accès au switch
- Déplacer le réseau se trouvant sur le VLAN 10 du 192.168.0.0/24 vers le 192.168.44.0/44
- Vérifier que tout fonctionne correctement

## Dans l'architecture WAN POC

- Attribuer une adresse IP au switch sur le VLAN1
- Attribuer ouvrir un port VLAN 1 sur le switch (par exemple le dernier de la plage)
- Connecter un PC sur ce port
- Attribuer une adresse IP au routeur sur le VLAN 1
- Vérifier que le PC VLAN 1 ping les deux adresses IP VLAN 1
- Les autres machines ont-elles accès au VLAN 1?
- Bloquer l'accès VLAN 1 sur le routeur en ajoutant une route statique vers une interface null
- Activer le SSH sur le switch et le routeur sur leur adresse de management
- Vérifier que vous pouvez accéder aux deux équipements en SSH
