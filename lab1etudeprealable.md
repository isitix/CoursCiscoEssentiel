# Etude préalable
## Questions préliminaires
- A quel endroit les équipements vont-ils être installés ?
    * Energie, onduleur
    * Climatisation
    * Protection physique, clé ou code d'accès
    * Baie d'installation
- Comment le câblage est-il organisé ?
    * Catégorie
    * Panneaux de brassage
    * Etiquetage
- Configuration IP
    * Le plan d'adressage est-il défini ?
    * Faut-il anticiper des évolutions du besoin ?
- Y-a-t-il des besoins auxiliaires non spécifiés ?
    * Accès à distance pour certains collaborateurs
    * Borne Wifi
    * Imprimante partagée
    * Vidéosurveillance accessible de l'extérieur
    * Accès VPN pour des techniciens de maintenance
    * Téléphonie IP
    * VPN vers du cloud (sauvegarde, etc...)
    * Ports Giga pour des serveurs, problème de débit
    * DHCP existant sur contrôleur de domaine Windows
- Des applications qui pourraient poser des problèmes au niveau du filtrage firewall sont-elles utilisées ?
    * Téléphonie ou multimedia
    * Accès à des serveurs sur des ports non standards
- Quelles sont les possibilités d'avoir des moyens supplémentaires ?
    * Pour installer un serveur syslog
    * Pour tester, vérifier la solution à distance ou sur site (accès à un poste de travail, accès teamviewer...)
- Comment la solution sera-t-elle maintenue et administrée ?
    * Déplacement sur site
    * Intervention à distance (VPN ou équivalent)
- Quels sont les besoins en sécurité et en disponibilité ?
    * Est-ce qu'il y a un contrat de service / support qui permet la mise à jour des équipements ?
    * Quel est le niveau de sécurité attendu ?
    * Quel est le niveau de risque acceptable ?
        + Confidentialité des données (piratage externe ou interne)
        + Intégrité (cryptolocker ...)
        + Disponiblité : combien de temps sans accès Internet ?
        + Traçabilité : besoin de savoir qui fait quoi ?
        + Données privées, données clients ?
- Qui est le référent du projet ?
- Quel est l'origine du projet ?

## Liste des matériels
BOM (Bill of materials)
Il s'agit d'établir la liste des matériels nécessaires à la réalisation du projet et de vérifier que ces matériels seront bien présents au démarrage du projet :
- Equipements
- Licences logicielles
- Accès à des matériels ou des logiciels extérieurs au projet
- Accès physique au site, aux armoires techniques...
- Câbles réseau
- Outils (pour racker les équipements, etc...)

## Prototypage
Pour des premiers projets ou des projets complexes, la réalisation d'un prototype (POC) peut être utile :
- sous packet tracer
- sous GNS3
- avec des équipements prếtés par le client ou le constructeur

