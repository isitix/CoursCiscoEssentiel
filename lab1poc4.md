# Configuration d'un réseau de management

## Dans l'architecture WAN

- Attribuer une adresse IP au switch sur le VLAN1
- Attribuer ouvrir un port VLAN 1 sur le switch (par exemple le dernier de la plage)
- Connecter un PC sur ce port
- Attribuer une adresse IP au routeur sur le VLAN 1
- Vérifier que le PC VLAN 1 ping les deux adresses IP VLAN 1
- Les autres machines ont-elles accès au VLAN 1?
- Bloquer l'accès VLAN 1 sur le routeur en ajoutant une route statique vers une interface null
- Activer le SSH sur le switch et le routeur sur leur adresse de management
- Vérifier que vous pouvez accéder aux deux équipements en SSH
