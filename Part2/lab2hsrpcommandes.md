# Commandes de configuration du lab HSRP dans packet tracer

## Configuration du switch de distribution D1

```ios
en
conf t
hostname D1

interface vlan 1
    ip address 192.168.1.11 255.255.255.0
    no shutdown
    exit

vlan 10
    name workstation
    exit

vlan 20
    name server
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
spanning-tree mode rapid
exit
copy run start
```

## Configuration du switch de distribution D2

```ios
en
conf t
hostname D2

interface vlan 1
    ip address 192.168.1.12 255.255.255.0
    no shutdown
    exit

vlan 10
    name workstation
    exit

vlan 20
    name server
    exit

interface range Fa 0/1-24
    switchport mode access
    switchport access vlan 20
    spanning-tree portfast
    no shutdown
    exit

interface range Giga 0/1-2
    switchport mode trunk
    no shutdown
    exit
spanning-tree mode rapid
exit
copy run start
```

## Configuration de base

### Switch Core C1

```ios
en
conf t
hostname C1

interface vlan 1
    ip address 192.168.1.1 255.255.255.0
    no shutdown
    exit

vlan 10
    name workstation
    exit

vlan 20
    name server
    exit

interface range Giga 1/0/1-3
    switchport trunk encapsulation dot1q 
    switchport mode trunk
    no shutdown
    exit

interface range Giga 1/0/4-24
    switchport trunk encapsulation dot1q 
    switchport mode trunk
    shutdown
    exit

interface range Giga 0/1/1-4
    switchport trunk encapsulation dot1q 
    switchport mode trunk
    shutdown
    exit

spanning-tree mode rapid
exit
copy run start
```

### Switch Core C2

```ios
en
conf t
hostname C2

interface vlan 1
    ip address 192.168.1.2 255.255.255.0
    no shutdown
    exit

vlan 10
    name workstation
    exit

vlan 20
    name server
    exit

interface range Giga 1/0/1-3
    switchport trunk encapsulation dot1q 
    switchport mode trunk
    no shutdown
    exit

interface range Giga 1/0/4-24
    switchport trunk encapsulation dot1q 
    switchport mode trunk
    shutdown
    exit

interface range Giga 1/1/1-4
    switchport trunk encapsulation dot1q
    switchport mode trunk
    shutdown
    exit

spanning-tree mode rapid
exit
copy run start
```

## Configuration SVI

### C1

```ios
interface vlan 10
    ip address 192.168.10.251 255.255.255.0
    no shut
    exit

interface vlan 20
    ip address 192.168.20.251 255.255.255.0
    no shut
    exit
```

### C2

```ios
interface vlan 10
    ip address 192.168.10.252 255.255.255.0
    no shut
    exit

interface vlan 20
    ip address 192.168.20.252 255.255.255.0
    no shut
    exit
```

## Activation du routage sur C1 et 2

A faire sur C1 et C2

```ios
ip routing
```

## Root spanning tree C1

```ios
spanning-tree vlan 10 priority 4096
spanning-tree vlan 20 priority 4096
```

## Root 2 sur C2

```ios
spanning-tree vlan 10 priority 8192
spanning-tree vlan 20 priority 8192
```

## HSRP sur Vlan 10 et 20

### C1

```ios
interface vlan 10
    standby ip 192.168.10.254
    standby track Giga 1/0/3
    standby priority 100
    exit
interface vlan 20
    standby ip 192.168.20.254
    standby track Giga 1/0/3
    standby priority 100
    exit
```

### C2

```ios
interface vlan 10
    standby ip 192.168.10.254
    standby track Giga 1/0/3
    standby priority 90
    exit
interface vlan 20
    standby ip 192.168.20.254
    standby track Giga 1/0/3
    standby priority 90
    exit
```