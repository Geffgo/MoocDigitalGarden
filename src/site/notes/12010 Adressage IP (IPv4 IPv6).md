---
{"dg-publish":true,"permalink":"/12010-adressage-ip-i-pv4-i-pv6/"}
---

# Fiche Réseau : Adressage IP : IPv4 et IPv6
# Fiches Liées
- [[Accueil\|Accueil]]
---
## Introduction

L'adressage IP est un système d'identification unique des équipements sur un réseau. Il existe actuellement deux versions principales : IPv4 et IPv6.

## IPv4 (Internet Protocol version 4)

### Caractéristiques générales

- **Format** : 32 bits (4 octets)
- **Notation** : Décimale pointée (ex: 192.168.1.1)
- **Espace d'adressage** : 2³² = 4 294 967 296 adresses
- **Année d'introduction** : 1981 (RFC 791)

### Structure d'une adresse IPv4

```
192.168.1.1
└─┬─┘└─┬─┘└┬┘└┬┘
  │   │  │ │
  │   │  │ └─ Hôte (0-255)
  │   │  └─── Réseau
  │   └────── Réseau  
  └────────── Réseau
```

### Classes d'adresses IPv4

|Classe|Plage|Masque par défaut|Usage|
|---|---|---|---|
|**A**|1.0.0.0 - 126.255.255.255|/8 (255.0.0.0)|Très grands réseaux|
|**B**|128.0.0.0 - 191.255.255.255|/16 (255.255.0.0)|Réseaux moyens|
|**C**|192.0.0.0 - 223.255.255.255|/24 (255.255.255.0)|Petits réseaux|
|**D**|224.0.0.0 - 239.255.255.255|-|Multicast|
|**E**|240.0.0.0 - 255.255.255.255|-|Expérimental|

### Adresses IPv4 spéciales

#### Adresses privées (RFC 1918)

- **Classe A** : 10.0.0.0/8 (10.0.0.0 - 10.255.255.255)
- **Classe B** : 172.16.0.0/12 (172.16.0.0 - 172.31.255.255)
- **Classe C** : 192.168.0.0/16 (192.168.0.0 - 192.168.255.255)

#### Autres adresses spéciales

- **Loopback** : 127.0.0.0/8 (127.0.0.1 = localhost)
- **APIPA** : 169.254.0.0/16 (autoconfiguration)
- **Broadcast** : 255.255.255.255
- **Réseau par défaut** : 0.0.0.0/0

### Masques de sous-réseau (CIDR)

|CIDR|Masque|Hôtes disponibles|
|---|---|---|
|/8|255.0.0.0|16 777 214|
|/16|255.255.0.0|65 534|
|/24|255.255.255.0|254|
|/25|255.255.255.128|126|
|/26|255.255.255.192|62|
|/27|255.255.255.224|30|
|/28|255.255.255.240|14|
|/30|255.255.255.252|2|

## IPv6 (Internet Protocol version 6)

### Caractéristiques générales

- **Format** : 128 bits (16 octets)
- **Notation** : Hexadécimale avec séparateurs ":"
- **Espace d'adressage** : 2¹²⁸ = 340 undécillions d'adresses
- **Année d'introduction** : 1998 (RFC 2460)

### Structure d'une adresse IPv6

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
└─────────────┬─────────────┘└─────────────┬─────────────┘
          Préfixe réseau              Identifiant interface
           (64 bits)                      (64 bits)
```

### Format et notation IPv6

#### Format complet

`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

#### Règles de compression

- **Suppression des zéros** : `2001:db8:85a3:0:0:8a2e:370:7334`
- **Double deux-points** : `2001:db8:85a3::8a2e:370:7334`
- **Une seule compression** par adresse

### Types d'adresses IPv6

#### Unicast

- **Global Unicast** : 2000::/3 (Internet public)
- **Link-Local** : fe80::/10 (lien local)
- **Unique Local** : fc00::/7 (privé)
- **Loopback** : ::1

#### Multicast

- **Préfixe** : ff00::/8
- **Exemples** :
    - ff02::1 (tous les nœuds)
    - ff02::2 (tous les routeurs)

#### Anycast

- Même format qu'unicast
- Plusieurs interfaces partagent la même adresse

### Comparaison IPv4 vs IPv6

|Aspect|IPv4|IPv6|
|---|---|---|
|**Taille d'adresse**|32 bits|128 bits|
|**Notation**|Décimale pointée|Hexadécimale|
|**Espace d'adressage**|4,3 milliards|340 undécillions|
|**Configuration**|Manuelle/DHCP|Auto/DHCPv6/SLAAC|
|**Sécurité**|Optionnelle (IPSec)|Intégrée (IPSec)|
|**Fragmentation**|Routeurs et hôtes|Hôtes uniquement|
|**Broadcast**|Oui|Non (multicast)|
|**NAT**|Courant|Inutile|

## Sous-réseaux et calculs

### Calcul IPv4 (exemple /26)

```
Réseau : 192.168.1.0/26
Masque : 255.255.255.192
Hôtes : 2^(32-26) - 2 = 62 hôtes
Plage : 192.168.1.1 - 192.168.1.62
Broadcast : 192.168.1.63
```

### Calcul IPv6 (exemple /64)

```
Réseau : 2001:db8:1234:5678::/64
Préfixe : 2001:db8:1234:5678
Hôtes : 2^64 interfaces possibles
```

