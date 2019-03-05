# Correction du lab SNMP

Commandes à passer sur le switch

```ios
en
conf t
host D1
interface vlan 1
    ip address 192.168.1.1 255.255.255.0
    no shut
    exit
interface vlan 100
    description PC
    no shut
interface range FA 0/2-24
    switchport mode access
    switchport access vlan 100
    no shut
    exit
interface FA 0/1
    switchport mode access
    switchport access vlan 1
    no shut
    exit
snmp-server community imie ro
exit
copy run start
```