# Simulation de la configuration matérielle du lab sous packet tracer

## Ressources

[Accès au fichier packet tracer](labfinalmateriel.pkt)

## Configuration du switch 2950 WS1

```ios
en
conf t
hostname WS1
interface vlan 1
    ip address 192.168.0.1 255.255.255.0
    no shutdown
    exit

interface FastEthernet 0/1
    switchport mode access
    switchport access vlan 1
    no shutdwon
    exit

vlan 10
    exit
vlan 20
    exit

interface vlan 10
    description PC
    no shutdown
    exit

interface vlan 20
    description server
    no shutdown
    exit

interface range Fa 0/2-12
    switchport mode access
    switchport access vlan 10
    spanning-tree portfast
    no shutdown
    exit

interface range Fa 0/13-23
    switchport mode access
    switchport access vlan 20
    spanning-tree portfast
    no shutdown
    exit

interface Fa 0/24
    switchport mode trunk
    no shutdown
    exit

service password-encryption
username administrateur privilege 15 password imie
line console 0
    login local
    exit

line vty 0 15
    login local
    transport input ssh
    transport output ssh
    exit

enable password imie

ip domain-name imie
crypto key generate rsa general-keys modulus 4096
ip scp server enable
exit
copy run start
ssh -l administrateur 192.168.0.1
```

## Configuration du switch 2950 ES2

Configuration voisine de WS1

```ios
en
conf t
hostname ES2
interface vlan 1
    ip address 192.168.1.3 255.255.255.0
    no shutdown
    exit

vlan 10
    exit
vlan 20
    exit

interface FastEthernet 0/1
    switchport mode access
    switchport access vlan 1
    no shutdwon
    exit

interface vlan 10
    description PC
    no shutdown
    exit

interface vlan 20
    description server
    no shutdown
    exit

interface range Fa 0/2-23
    switchport mode access
    switchport access vlan 10
    spanning-tree portfast
    no shutdown
    exit

interface Fa 0/24
    switchport mode trunk
    no shutdown
    exit

service password-encryption
username administrateur privilege 15 password imie
line console 0
    login local
    exit

line vty 0 15
    login local
    transport input ssh
    transport output ssh
    exit

enable password imie

ip domain-name imie
crypto key generate rsa general-keys modulus 4096
ip scp server enable
exit
copy run start
ssh -l administrateur 192.168.0.1
```

## Configuration du switch 2060 ES1

Configuration voisine de ES2

```ios
en
conf t
hostname ES1
interface vlan 1
    ip address 192.168.1.1 255.255.255.0
    no shutdown
    exit

vlan 10
    exit
vlan 20
    exit

interface vlan 10
    description PC
    no shutdown
    exit

interface vlan 20
    description server
    no shutdown
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

service password-encryption
username administrateur privilege 15 password imie
line console 0
    login local
    exit

line vty 0 15
    login local
    transport input ssh
    transport output ssh
    exit

enable password imie

ip domain-name imie
crypto key generate rsa general-keys modulus 4096
ip scp server enable
exit
copy run start
ssh -l administrateur 192.168.0.1
```

## Configuration du routeur ER1

```ios
en
conf t
hostname er1

interface Fa 0/0.1
    encapsulation dot1Q 1
    ip address 192.168.1.254 255.255.255.0
    no shutdown
interface Fa 0/0.10
    encapsulation dot1Q 10
    ip address 10.1.10.254 255.255.255.0
    no shutdown
    exit
interface Fa 0/0.20
    encapsulation dot1Q 20
    ip address 10.1.20.254 255.255.255.0
    no shutdown
    exit
interface Fa 0/0
    no shutdown
    exit

interface Fa 0/1
    ip address 172.0.0.2 255.255.255.252
    no shutdown
    exit

service password-encryption
username administrateur privilege 15 password imie
line console 0
    login local
    exit
line vty 0 15
    login local
    transport input ssh
    transport output ssh
    exit

enable password imie

ip domain-name imie
crypto key generate rsa general-keys modulus 4096
ip scp server enable
ip routing

router rip
    version 2
    no auto-summary
    network 172.0.0.0
    network 10.0.10.0
    network 10.0.20.0
    passive-interface FastEthernet 0/0
    exit
```

## Configuration du routeur WR1
Voisine de ER1

```ios
en
conf t
hostname wr1

interface Fa 0/0.1
    encapsulation dot1Q 1
    ip address 192.168.0.254 255.255.255.0
    no shutdown
interface Fa 0/0.10
    encapsulation dot1Q 10
    ip address 10.0.10.254 255.255.255.0
    no shutdown
    exit
interface Fa 0/0.20
    encapsulation dot1Q 20
    ip address 10.0.20.254 255.255.255.0
    no shutdown
    exit
interface Fa 0/0
    no shutdown
    exit

interface Ethernet 1/0
    ip address 172.0.0.1 255.255.255.252
    no shutdown
    exit

service password-encryption
username administrateur privilege 15 password imie
line console 0
    login local
    exit
line vty 0 15
    login local
    transport input ssh
    transport output ssh
    exit

enable password imie

ip domain-name imie
crypto key generate rsa general-keys modulus 4096
ip scp server enable
ip routing

router rip
    version 2
    no auto-summary
    network 172.0.0.0
    network 10.1.10.0
    network 10.1.20.0
    exit
