# VPN

## Introduction

Cinq technologies VPN

1. IPSEC site à site
2. IPSEC remote
3. Liaison point à point GRE (+ IPSEC)
4. SSL (anyconnect) remote
5. L2TP (Microsoft)

La configuration VPN est un sujet complexe :

- Difficulté intrinsèque de debuggage : le trafic est chiffré
- Complexité, coût, opacité des technologies de chiffrement
- Problématique résultant de la sécurité de ces dispositifs (NAT traversal, ...)

Par rapport à Cisco :

- la manière de configurer le VPN est différente sur ASA et sur routeur
- l'évolution des technologies de chiffrement a rendu obsolètes certains équipements anciens, du moins pour faire du VPN. Cisco ne propose malheureusement pas d'évolution de ces équipements (SHA1, ...)
- les solutions les plus simples sont payantes (anyconnect)
- Microsoft reste très présent, côté client, dans l'accès remote, avec une technologie dépassée (L2TP) et difficile à faire fonctionner

## IPSec site

Points importants à retenir :

- le système ne fonctionne que si les deux routeurs ou parefeu (point de terminaison) sont configurés avec les mêmes paramètres
- la négociation des clés a lieu en deux phases :
  - Phase 1 : négociation des clés d'échange de clés
  - Phase 2 : négociation des clés de chiffrement
- Les clés de chiffrement ne sont pas connues a priori mais négociées entre les deux points de terminaison
- L'authentification des points de terminaison fait l'objet d'un échange spécifique, soit par clé partagée soit par certificat
- l'établissement du trafic une fois le tunnel monté peut être complexe du fait de l'effet tunnel
  - NAT
  - Routage
  - ACL
- Sur les ASA notamment, le chiffrement et la montée du tunnel sont induits par le trafic et pas l'inverse. C'est la transformation du trafic qui fait monter le tunnel et le tunnel n'existe que par le trafic qu'il transporte. Le tunnel n'est donc pas un lien réseau à proprement mais une transformation appliquée à des paquets en fonction d'une security map.