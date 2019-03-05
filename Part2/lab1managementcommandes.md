# Commandes du lab 1

## Configuration du switch L3 A1

```ios
en
conf t
host A1
interface range Giga 0/1-2
    switchport trunk encapsulation dot1q
    switchport mode trunk
    exit

vtp mode server
vtp domain imie
vtp password imie

vlan 100
    name PC
    exit
vlan 101
    name server
    exit

interface vlan 100
    ip address 192.168.100.254 255.255.255.0
    no shutdown
    exit

interface vlan 101
    ip address 192.168.101.254 255.255.255. 0
    no shutdown
    exit

interface vlan 1
    ip addres 192.168.1.1 255.255.255.0
    no shutdown
    exit

spanning-tree mode rapid-pvst

interface range Fast 0/1-24
    switchport mode access
    switchport access vlan 101
    spanning-tree portfast
    no shutdown
    exit
exit
copy run start
```



