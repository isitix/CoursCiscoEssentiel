# Commandes de configuration du lab HSRP dans packet tracer

## Configuration du switch de distribution D1

```ios
en
conf t
hostname D1

interface vlan 1
    ip address 192.168.1.11
    no shutdown
    exit

vlan 10
    name workstation
    no shutdown

vlan 20
    name server
    no shutdown

interface range Fa 0/1-24
    switchport mode access
    switchport access vlan workstation
    spanning-tree portfast
    no shutdown
    exit

interface range Giga 0/1-2
    switchport mode trunk
    no shutdown
    exit
exit
spanning-tree mode rapid
copy run start
```

