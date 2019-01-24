# Lab 1 POC 3 : configuration du parefeu ASA

Reprendre la configuration [présentée ici](http://blog.isitix.com//main/2018/07/25/configuration-base-asa-5505.html) en l'adaptant à l'environnement et à packet tracer

## Configuration des adresses LAN

### Sous-réseaux

|Domaine | Réseau | 1ère IP | Dernière IP | Broadcast | Mask |
|--------|--------|---------|-------------|-----------|------|
|Admin |192.168.0.0 | .1 | .30 | .31 | /27 255.255.255.224 |
|Serveurs | 192.168.0.54 | .65 | .94 | .95 | /27 255.255.255.224 |
|PCs | 192.168.0.128 | .129 | .190 | .191 | /26 255.255.255.192 |

### Plan d'adressage

|Station / Interface|Adresse|
|-------|-------|
|Réseau / Masque|192.168.0.0/24|
|ASA / Mgt|192.168.0.2|
|Switch 1 / Mgt|192.168.0.3|
| Plage DHCP | .129  -> .190|
| Serveur | 192.168.0.66|
|ASA / gw | 192.168.0.254|
|ASA / internet|190.250.122.45 255.255.255.248|
|Default route opérateur|190.250.122.46|
|NTP server |192.168.0.67|
|DNS server |192.168.0.67|

### Configuration des VLANs et des ports

[Configuration de l'ASA V0](configasaV0.txt)

### Configuration route par défaut et NAT

pb sur le NAT...

### Réalisation d'une maquette NAT

Suivre le tutoriel suivant <https://courses.cs.ut.ee/MTAT.08.004/2015_spring/uploads/Main/34_1.pdf>
Explication concernant le NAT [ici](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/13772-12.html#topic2)
## Prochaines étapes :

[Lab 1 POC 4](lab1poc4.md) : configuration d'un réseau de management

