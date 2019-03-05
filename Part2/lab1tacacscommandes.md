# Commandes de configuration tacacs

```ios
en
conf t
host A1
interface vlan 1
    ip address 192.168.1.1 255.255.255.0
    no shut
    exit
ip domain-name imie
service password
username backup privilege 15 password imie
enable password imie

ip domain-name imie
crypto key gener rsa gen mod 4096

aaa new-model
aaa authentication login default group tacacs+ local
aaa authentication enable default group tacacs+ local

line vty 0 15
    login authentication default
    exit

tacacs-server host 192.168.1.2 key tacacs
exit
```
