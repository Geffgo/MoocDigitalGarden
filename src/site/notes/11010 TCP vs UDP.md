---
{"dg-publish":true,"permalink":"/11010-tcp-vs-udp/"}
---

# Fiche Réseau : TCP vs UDP
# Fiches Liées
- [[Accueil\|Accueil]]
---
## INTRODUCTION

**TCP** et **UDP** sont les deux protocoles de transport principaux de la suite TCP/IP. Ils opèrent à la **couche 4 (Transport)** du modèle OSI et assurent la communication entre applications sur différents hôtes.

### Position dans le modèle TCP/IP

```
Application  ←→  HTTP, FTP, SMTP, DNS
Transport    ←→  TCP, UDP
Internet     ←→  IP
Accès réseau ←→  Ethernet, WiFi
```

---

## COMPARAISON GÉNÉRALE

|Aspect|TCP|UDP|
|---|---|---|
|**Nom complet**|Transmission Control Protocol|User Datagram Protocol|
|**Fiabilité**|Fiable|Non fiable|
|**Connexion**|Orienté connexion|Sans connexion|
|**Vitesse**|Plus lent|Plus rapide|
|**Taille en-tête**|20-60 octets|8 octets|
|**Contrôle de flux**|Oui|Non|
|**Détection d'erreurs**|Oui + correction|Oui (basique)|
|**Ordre des données**|Garanti|Non garanti|
|**Utilisation**|Applications critiques|Applications temps réel|

---

## TCP (Transmission Control Protocol)

### Caractéristiques principales

#### Fiabilité

- **Acquittement** : Chaque segment reçu est confirmé
- **Retransmission** : Renvoi automatique des segments perdus
- **Numérotation** : Séquences pour ordonner les données
- **Contrôle d'intégrité** : Somme de contrôle (checksum)

#### Orienté connexion

- **Établissement** : Handshake à 3 voies
- **Maintien** : Gestion de l'état de la connexion
- **Fermeture** : Terminaison propre

#### Contrôle de flux

- **Fenêtre glissante** : Évite la saturation du récepteur
- **Adaptation dynamique** : Ajustement selon les conditions
- **Gestion de congestion** : Prévention des embouteillages

### Structure de l'en-tête TCP

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Port source          |       Port destination       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Numéro de séquence                    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Numéro d'acquittement                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  HL   |Rés|   Drapeaux    |            Fenêtre            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Somme de contrôle   |        Pointeur urgent       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options (0-40 octets)                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

#### Champs importants :

- **Ports** : Identification des applications (16 bits chacun)
- **Numéro de séquence** : Position des données (32 bits)
- **Numéro d'acquittement** : Prochaine séquence attendue (32 bits)
- **Drapeaux** : Contrôle de connexion (9 bits)
- **Fenêtre** : Taille du buffer de réception (16 bits)
- **Somme de contrôle** : Vérification d'intégrité (16 bits)

### Drapeaux TCP

|Drapeau|Nom|Fonction|
|---|---|---|
|**URG**|Urgent|Données urgentes|
|**ACK**|Acknowledgment|Acquittement valide|
|**PSH**|Push|Transmission immédiate|
|**RST**|Reset|Réinitialisation de connexion|
|**SYN**|Synchronize|Établissement de connexion|
|**FIN**|Finish|Terminaison de connexion|

---

## UDP (User Datagram Protocol)

### Caractéristiques principales

#### Simplicité

- **Sans connexion** : Pas d'établissement de session
- **Pas d'état** : Aucune information de connexion
- **Minimal** : En-tête de seulement 8 octets
- **Rapide** : Transmission immédiate

#### Non fiable

- **Pas d'acquittement** : Aucune confirmation de réception
- **Pas de retransmission** : Données perdues = perdues
- **Pas d'ordre** : Les datagrammes peuvent arriver dans le désordre
- **Best effort** : Livraison au mieux

### Structure de l'en-tête UDP

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Port source          |       Port destination       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|            Longueur           |       Somme de contrôle      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             Données                           |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

#### Champs :

- **Port source** : Port de l'expéditeur (16 bits)
- **Port destination** : Port du destinataire (16 bits)
- **Longueur** : Taille totale du datagramme (16 bits)
- **Somme de contrôle** : Vérification d'intégrité (16 bits)

### Fonctionnement UDP

```
Application A                   Application B
     |                               |
     |-- Datagramme 1 -------------->|
     |-- Datagramme 2 -------------->|
     |-- Datagramme 3 -------------->|
     |                               |
   (Aucun acquittement requis)
```

---

## PORTS ET SERVICES

### Ports TCP courants

|Port|Service|Description|
|---|---|---|
|**20**|FTP-Data|Transfert de données FTP|
|**21**|FTP-Control|Contrôle FTP|
|**22**|SSH|Connexion sécurisée|
|**23**|Telnet|Connexion distante|
|**25**|SMTP|Envoi d'emails|
|**53**|DNS|Résolution de noms (aussi UDP)|
|**80**|HTTP|Navigation web|
|**110**|POP3|Réception d'emails|
|**143**|IMAP|Gestion d'emails|
|**443**|HTTPS|Navigation web sécurisée|
|**993**|IMAPS|IMAP sécurisé|
|**995**|POP3S|POP3 sécurisé|

### Ports UDP courants

|Port|Service|Description|
|---|---|---|
|**53**|DNS|Résolution de noms|
|**67**|DHCP Server|Attribution d'IP|
|**68**|DHCP Client|Réception d'IP|
|**69**|TFTP|Transfert de fichiers simple|
|**123**|NTP|Synchronisation d'heure|
|**161**|SNMP|Gestion de réseau|
|**162**|SNMP Trap|Alertes SNMP|
|**500**|IKE|Échange de clés IPSec|
|**514**|Syslog|Journalisation|
|**1701**|L2TP|Tunneling VPN|
