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
ip routing
exit
copy run start
```

### Configuration du switch L2 D1

```ios
en
conf t
host D1

vtp mode client
vtp dom imie
vtp pass imie

span mode rapid

interface range Giga 0/1-2
    switch mode trunk
    exit
interface range Fa 0/2-24
    switch mode access
    switch access vlan 100
    no shut
    exit
interface Fa 0/1
    switch mode access
    switch access vlan 1
    no shut
    exit

interface vlan 1
    ip address 192.168.1.11 255.255.255.0
    no shut
    exit

service password
username administrateur privilege 15 password imie

ip domain-name imie
crypto key gener rsa gen mod 4096

line vty 0 15
    login local
    transport input ssh
    transport output ssh
    exit
exit
```