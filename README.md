# CoursCiscoEssentiel
Un cours Cisco pour débutant librement inspiré du livre ["Cisco in a month of lunches" paru aux éditions Manning](https://www.manning.com/books/learn-cisco-network-administration-in-a-month-of-lunches) et donné à l'IMIE de Nantes en 2019, sous forme de deux sessions de quatre jours.

## Syllabus
Le syllabus a été défini par l'équipe pédagogique de [l'IMIE de Nantes](https://numerique.imie.fr/).

### Objectifs du module
Le module a pour objectif de couvrir de manière générale quatre compétences des réseaux d'entreprise :
1. Conception des réseaux
2. Configuration des équipements (maquette et implémentation réelle)
3. Supervision, support, et contrats de service
4. Sécurité et disponibilité

### Sujets abordés
Les sujets qui pourront être abordés lors du cours sont les suivants: 
- Gestion des équipements
    + Utilisateurs et droits
    + Authentification simple, par clé, kerberos
    + Sauvegarde, restauration
    + Accès port console, SSH
    + Sauvegarde, restauration de la configuration
    + Mise à jour
    + SNMP
- Commutation
    + Configuration physique des ports
    + Sécurité des ports
    + Services locaux (ARP, NTP, DHCP, DNS)
    + VTP (Vlan Trunk Protocol)
    + DTP (Dynamic Trunking Protocol)
    + STP (Spanning Tree Protocol)
    + Etherchannel
- Routage
    + Static
    + Policy based routing (PBR)
    + OSPF
    + RIP
    + EIGRP
    + BGP
    + Sécurité du routage
- Gestion des flux
    + ACL
    + NAT
    + Prise en charge IPV6
- VPN
    + IPSEC site à site
    + IPSEC client
    + GRE
    + DMVPN
- Disponibilité
    + HSRP
    + VRPP
- Outils de diagnostic
    + Port mirroring
    + Netflow
    + Syslog

### Environnement de travail
Le cours se déroule principalement sous forme de labs, avec quelques éléments théoriques donnés au fil de l'eau et des quizz pour tester ses connaissances.
Les environnements suivants sont utilisés en fonction des besoins :
- Cisco packet tracer
- Matériels Cisco (commutateurs et routeurs)
- GSN3
- Cisco dcloud

### Savoir-faire acquis
- Définir les besoins, identifier les contraintes d'un projet réseau
- Concevoir un réseau
- Rédiger des spécifications, fournir les informations nécessaires pour établir un devis
- Maquetter la solution envisagée, valider les choix
- Déployer la version de production
- Recetter le réseau dans ses différentes dimensions, performance, robustesse, sécurité
- Exploiter, monitorer un réseau existant
- Auditer, diagnostiquer, tuner un réseau existant

## Déroulement du cours
- [Lab 1 : gestion des équipements](lab1.md)

