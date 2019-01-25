# Agrégation de liens

## Usage

Augmenter le débit et améliorer la robustesse de la liaison entre deux équipements en rassemblant des ports physiques pour former une seule liaison agrégeant les débits des ports assemblés

Pour plus de détails, [voir ici](https://en.wikipedia.org/wiki/Link_aggregation)

## Composants

[Documentation de référence](https://www.cisco.com/c/en/us/td/docs/optical/cpt/r9_3/command/reference/cpt93_cr/cpt93_cr_chapter_01000.html)

### Groupe de ports

On définit le groupe de ports *channel-group* à agréger sur chaque équipement 

### Interface virtuelle

On crée une interface virtuelle *port-channel* à laquelle on rattache le groupe de port.

### LACP

Link Aggregation Control Protocol : c'est le protocole de négociation de l'agrégation entre les ports des deux équipements reliés par l'agrégation

### Options

Différentes options d'agrégration sont disponibles :

- Répartition de charge (load-balance)
- Mode en cas de panne (switchover, bundle)

## LAB

- Prendre deux switch 2960
- Les connecter par leurs deux ports Giga
- Créer une aggrégation avec les deux ports Giga
- Vérifier l'état de l'aggrégation
- Ajouter une station sur chaque switch
- L'aggrégration est-elle en mode trunk ou access ?
- Ajouter deux VLANs sur chaque switch 44 et 45
- Mettre les ports 1 à 12 dans 44 et 13 à 18 dans 45
- Passer l'agrégation en mode trunk
- Ajouter les ports FA 23 et 24 dans l'agrégation sur le SW1
- Que se passe-t-il ?
- Faire de même sur le SW2
- Faire un ping entre les stations sur les deux SW
- Débrancher les deux ports Giga
- Que se passe-t-il ?





