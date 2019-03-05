# Les ACL

## Présentation

Les ACL, access control list, sont un outil pour *sélectionner* du trafic réseau en fonction de *critères* et lui appliquer des *actions*.

Il existe deux types d'ACL, les ACLs standard et les ACLs étendues. Elles fonctionnent de la même manière avec des différences :

1. les ACL standard ne filtrent que sur la source; les ACLs étendues source et destination
2. Historiquement, les ACL standard sont identifiées par un numéro inférieur à 100. Dans les dernières versions d'IOS, l'usage d'un numéro ou d'un nom est possible.
3. Les ACL standard filtrent uniquement sur l'adresse ou le bloc d'adresse IP source

Les ACLs étendues comportent 5 niveaux :

- Bloc : deux blocs, un bloc source (IP, protocole, port) et un bloc destination (IP, protocole, port) qui définissent le trafic sur lequel s'applique l'ACL
- Règles : chaque règle est constitué des deux blocs source et destination et d'une ou plusieurs actions (permit / deny / log)
- Groupe de règles : toutes les règles ayant un même identifiant constituent un groupe de règles. Elles sont analysées dans l'ordre par l'équipement pour sélectionner le trafic. Le premier match arrête l'analyse. Le groupe se termine par une règle implicite qui bloque le trafic qui ne matche aucun règle
- Point d'application : le groupe s'applique à une interface avec un sens. Le sens peut être in ou out. Le sens est vu du point de vue de l'équipement, in étant un trafic qui rentre dans l'équipement, out qui sort, par l'interface considérée. Il peut aussi s'appliquer à l'accès à une ressource ou au passage par un processus de traitement. Ressource : terminal, accès admin interface web... Processus de traitement : inspection de trafic, nat, vpn...

*ATTENTION* : le wild card mask (qui permet de définir le sous-réseau auquel s'applique l'ACL) est inversé par rapport au netmask dans IOS. Sur les ASA, il est par contre comme le net mask.

*ATTENTION* Sur les équipements de routage (IOS), les access list sont dans un seul sens à moins d'employer les mécanismes de etablished, qui permet d'autoriser le out des des connexions établies en in ou réciproquement, ou de reflexive, qui met à jour automatiquement la liste en out pour les connexions en in ou réciproquement. Sur les parefeux ASA, le filtrage est stateful, et le flux entrant correspondant au flux sortant est automatiquement autorisé.
Exemple : autoriser ssh et http vers depuis n'importe quelle IP vers le 192.168.1.23

```ios
access-list 120 permit tcp any host 192.168.1.23 eq ssh
access-list 120 permit tcp any host 192.168.1.23 eq http
```

ou plus compact

```ios
access-list 120 permit tcp any host 192.168.1.23 eq ssh http
```

Exemple : bloquer l'accès au serveur 192.168.10.18 depuis le sous-réseau 192.168.1.0/24

```ios
access-list 130 deny ip 192.168.1.0 0.0.0.255 host 102.168.10.18
```

Les règles s'appliquent dans l'ordre jusqu'au premier match. Une modification dans un groupe de règles est souvent complexe à mener. Il vaut parfois mieux effacer le groupe et le réécrire.

Le choix entre filtrage par liste blanche (implicit deny) ou liste noire (implicit permit) dépend des applications. Le choix entre in et out dépend également du besoin. Deux règles générales s'opposent : appliquer au plus près de la source du trafic à bloquer ou appliquer en out pour des questions de performance du routage et de volume à filtrer

## Lab

- Réaliser le lab packet tracer [suivant](lab3acl.pkt)