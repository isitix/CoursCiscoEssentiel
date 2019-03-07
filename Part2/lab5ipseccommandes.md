# VPN site à site entre deux ASA

Le fichier packet tracer de départ est accessible ici

## Configuration des switches WS et ES

### WS

```ios
en
conf t
hostname WS
vlan 10
    name data
    exit

interface vlan 1
    ip address 192.168.1.1 255.255.255.0
    no shutdown

interface range Fa 0/1-23
    switchport mode access
    switchport access vlan 10
    spanning-tree portfast
    no shutdown
    exit
interface Fa 0/24
    switchport mode access
    switchport access vlan 1
    no shutdown
interface range Giga 0/1-2
    switchport mode access
    switchport access vlan 10
    no shutdown
    exit
exit
copy run start
```

### ES

Identique à WS sauf le nom.

## Configuration générale de l'ASA

### WASA

```ios
hostname WASA
domain-name west

interface management 1/1
    ip address 192.168.1.2 255.255.255.0
    no shutdown
    exit

interface Giga 1/1
    ip address 192.168.10.254 255.255.255.0
    nameif inside
    no shutdown
    exit

interface Giga 1/2
    no nameif outside
    shutdown
    exit
interface Giga 1/3
    shutdown
    exit
interface Giga 1/4
    shutdown
    exit
interface Giga 1/5
    shutdown
    exit
interface Giga 1/6
    shutdown
    exit
interface Giga 1/7
    shutdown
    exit

interface Giga 1/8
    ip address 172.0.0.1 255.255.255.0
    nameif outside
    no shutdown
    exit
```

### EASA

Idem WASA sauf IP et nom

```ios
hostname EASA
domain-name east

interface management 1/1
    ip address 192.168.1.2 255.255.255.0
    no shutdown
    exit

interface Giga 1/1
    ip address 192.168.110.254 255.255.255.0
    nameif inside
    no shutdown
    exit

interface Giga 1/2
    no nameif outside
    shutdown
    exit
interface Giga 1/3
    shutdown
    exit
interface Giga 1/4
    shutdown
    exit
interface Giga 1/5
    shutdown
    exit
interface Giga 1/6
    shutdown
    exit
interface Giga 1/7
    shutdown
    exit

interface Giga 1/8
    ip address 172.0.0.2 255.255.255.0
    nameif outside
    no shutdown
    exit
```

## NAT

### WASA

```ios
object network LAN_DATA
    subnet 192.168.10.0 255.255.255.0
    nat (inside,outside) dynamic interface
```

### EASA

```ios
object network LAN_DATA
    subnet 192.168.110.0 255.255.255.0
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

## Traffic inspection

```ios
class-map insideout
    match any
    exit
policy-map global_policy
    class insideout
        inspect icmp
        exit
    exit
service-policy global_policy global
```
