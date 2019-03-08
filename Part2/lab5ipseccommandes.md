# Labs ASA

## Lab asa_service_policy (exemples fournis avec packet tracer)

### Nom du parefeu

```ios
hostname ciscoasa
```

### Activation de la conversion IP<->Nom

```ios
names
```

Voir [ici](https://community.cisco.com/t5/firewalls/what-happens-if-i-issue-the-quot-no-names-quot-command-on-a/td-p/1364904
)

### Configuration des interfaces

```ios
interface Ethernet0/0
 switchport access vlan 2
interface Ethernet0/2
 switchport access vlan 3
```

### Configuration des VLANs

```ios
interface Vlan1
 nameif inside
 security-level 100
 ip address 192.168.1.1 255.255.255.0
 ipv6 address 1920:1::1/80

interface Vlan2
 nameif outside
 security-level 0
 ip address 209.165.200.226 255.255.255.248
 ipv6 address 2090::226/64

interface Vlan3
 no forward interface Vlan1
 nameif dmz
 security-level 70
 ip address 192.168.2.1 255.255.255.0
 ipv6 address 1920:2::1/80
```

security-level : le trafic passe des security-level les plus hauts vers les plus bas, par défaut, mais pas dans l'autre sens.
no-forward : bloque le trafic sortant du VLAN (pour respecter les règles de licence). Voir [ici](http://www.gomjabbar.com/2011/09/11/no-forward-interface-command-on-the-cisco-asa-5505-with-a-base-license/#sthash.Ryd8yyzg.dpbs) pour plus de détails.

### Configuration d'une security-policy pour laisser passer le ping

Définir le trafic auquel la security policy va s'appliquer

```ios
class-map testMap
    match any
    exit
```

Définir la politique de sécurit

```ios
policy-map testPolicy
    class testMap
    inspect icmp
    exit
```

Appliquer la politique de sécurité à l'interface

```ios
service-policy testPolicy interface inside
```

## Lab asa_acl_nat

La configuration de base est identique à celle de l'exemple précédent.

Y a été ajouté une route par défaut en IPV4 et IPV6:

```ios
ipv6 route outside ::/0 2090::225
route outside 0.0.0.0 0.0.0.0 209.165.200.225 1
```

la récupération automatique de paramètres réseau par dhcp si l'IP outside est en dhcp. [Voir ici](https://community.cisco.com/t5/vpn-and-anyconnect/dhcpd-auto-config-outside/td-p/1656016) pour plus de détails.

```ios
dhcpd auto_config outside
```

Un serveur dhcpd interne :

```ios
dhcpd address 192.168.1.5-192.168.1.34 inside
dhcpd enable inside
```

## Lab VPN
VPN site à site entre deux ASA

Le fichier packet tracer de départ est accessible ici

## Configuration des switches WS et ES

### WS

```ios
en
conf t
hostname WS

interface vlan 1
    ip address 192.168.1.1 255.255.255.0
    no shutdown
    exit
vlan 10
    exit
interface range Fa 0/1-24
    switchport mode access
    switchport access vlan 10
    spanning-tree portfast
    no shutdown
    exit
interface range Giga 0/1-2
    switchport mode trunk
    no shutdown
    exit
exit
copy run start
```

### ES

Identique à WS sauf le nom.

## Configuration générale de l'ASA

### WASA

#### host et domain

```ios
hostname WASA
domain-name west
```

#### VLAN

Remarque : on supprime la configuration par défaut, d'où les commandes en no

```ios
interface vlan 2
    no nameif outside
    no security-level 0
    no ip address dhcp
    exit

interface vlan 1
    no nameif inside
    no security-level 100
    exit

interface vlan 10
    nameif inside
    ip address 192.168.10.254 255.255.255.0
    no shut
    exit

interface vlan 20
    ip address 172.0.0.1 255.255.255.0
    nameif outside
    no shutdown
    exit

interface vlan 1
    ip address 192.168.1.2 255.255.255.0
    no forward interface vlan 10
    no shutdown
    exit
```

#### Interfaces physiques

Remarque :

- on ne peut pas faire de trunk, ce qui pose des problèmes pour le VLAN de management (ou il faut lui attribuer un port physique ou le mettre en accès VPN)
- on désactive les ports physiques non utilisés (optionnel) 

```ios
interface ethernet 0/0
    switchport access vlan 10
    no shutdown
    exit

interface ethernet 0/7
    switchport access vlan 20
    exit

interface ethernet 0/1
    shutdown
    exit

interface ethernet 0/2
    shutdown
    exit

interface ethernet 0/3
    shutdown
    exit

interface ethernet 0/4
    shutdown
    exit

interface ethernet 0/5
    shutdown
    exit

interface ethernet 0/6
    shutdown
    exit
```

#### DHCPD

Option 3 : default gateway

```ios
no dhcpd auto_config outside

dhcpd address 192.168.10.17-192.168.10.31 inside 
dhcpd enable inside
dhcpd option 3 ip 192.168.10.254 interface inside
```

#### Trafic inspection

```ios
class-map ping-cm
    match any
    exit

policy-map ping-pm
    class ping-cm



## NAT

### WASA

```ios
object network LAN_DATA
    subnet 192.168.10.0 255.255.255.0
    nat (inside,outside) dynamic interface
```

## Threat detection

(ne fonctionne pas sous packet tracer)

```ios
threat-detection basic-threat
threat-detection statistics host
threat-detection statistics port
threat-detection statistics protocol
threat-detection statistics access-list
threat-detection statistics tcp-intercept
```
