# Ports physiques

Savoir forcer les paramètres physiques des ports permet de régler certains dysfonctionnements :

- Débit, perte de paquets, latence du fait d'un défaut sur un câble ou d'une autonégociation incorrecte
- Connexion câble croisée / câble droit sur des équipements anciens

La sécurité des ports peut également être renforcée en imposant des règles :

- Limiter le nombre d'adresses MAC
- Fermer les ports non utilisés
- Mettre en place un contrôle de storm
- Verrouiller un port sur un équipement 

## Lab

### Paramètres physiques

- Mettre deux 2960 sur le lab, 2960-1 et 2960-2
- Connecter deux PC sur le 2960-1
- Connecter un serveur DHCP sur le 2960-2
- Etat des deux ports (vitesse, duplex) ?
- Forcer les ports à 10. Que se passe-t-il ?
- Connecter les deux 2960 par un de leur port Giga
- Vitesse, état des ports ?
- Forcer le port de l'un d'eux à 100 et l'autre à 1000, que se passe-t-il ?
- Revenir en arrière
- Connecter le port Giga de l'un sur un port 100 de l'autre. Que se passe-il ?

### Sécurité

- Ajouter une règle de sécurité type au plus 2 adresses MAC ou shutdown sur les ports du 2960-1
- Connecter un troisième 2960-3 à un des ports access
- Connecter un, puis deux, puis trois PC sur le 2960-3, que se passe-il ?
- Mettre les ports de PC1 et 2 en mode sticky
- Echanger les deux PCs, que se passe-t-il ?
- Comment rétablir le trafic sur ces deux PCs en les maintenant sur le même port
- Lire le blog suivant <https://www.netcraftsmen.com/understanding-cisco-traffic-storm-control/>
- Ajouter du storm control sur les ports

## Méthode standard Cisco de troubleshooting des ports

<https://www.cisco.com/c/en/us/support/docs/switches/catalyst-6500-series-switches/12027-53.html>