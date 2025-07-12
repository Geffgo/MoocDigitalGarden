---
{"dg-publish":true,"permalink":"/10010-modeles-osi-et-tcp-ip/"}
---

# Fiche Réseau : Modèles OSI et TCP/IP
# Fiches Liées
- [[Accueil\|Accueil]]
---
## COMPARAISON DES MODÈLES

|Couche OSI|Nom OSI|Couche TCP/IP|Nom TCP/IP|Fonction principale|
|---|---|---|---|---|
|7|Application|4|Application|Interface utilisateur|
|6|Présentation|4|Application|Formatage des données|
|5|Session|4|Application|Gestion des sessions|
|4|Transport|3|Transport|Fiabilité bout en bout|
|3|Réseau|2|Internet|Routage des paquets|
|2|Liaison|1|Accès réseau|Contrôle d'accès au support|
|1|Physique|1|Accès réseau|Transmission des bits|

---

## MODÈLE OSI (7 COUCHES)

### Couche 7 - APPLICATION

**Rôle :** Interface entre les applications et le réseau

**Protocoles principaux :**

- **HTTP/HTTPS** : Navigation web (ports 80/443)
- **FTP** : Transfert de fichiers (ports 20/21)
- **SMTP** : Envoi d'emails (port 25)
- **POP3/IMAP** : Réception d'emails (ports 110/143)
- **DNS** : Résolution de noms (port 53)
- **DHCP** : Attribution d'adresses IP (ports 67/68)

---

### Couche 6 - PRÉSENTATION

**Rôle :** Formatage, chiffrement, compression des données

**Fonctions :**

- **Chiffrement/Déchiffrement** : SSL/TLS
- **Compression** : Réduction de la taille des données
- **Conversion** : ASCII ↔ EBCDIC, Little/Big Endian
- **Formatage** : JPEG, GIF, MPEG

---

### Couche 5 - SESSION

**Rôle :** Établissement, gestion et terminaison des sessions

**Fonctions :**

- **Établissement** : Authentification, autorisation
- **Gestion** : Synchronisation, points de reprise
- **Terminaison** : Fermeture propre des connexions

**Protocoles :**

- **NetBIOS** : Noms de machines Windows
- **SQL** : Sessions de base de données

---

### Couche 4 - TRANSPORT

**Rôle :** Fiabilité de bout en bout, contrôle de flux

**Protocoles principaux :**

**TCP (Transmission Control Protocol) :**

- **Fiable** : Garantit la livraison des données
- **Orienté connexion** : Handshake 3-way
- **Contrôle de flux** : Évite la saturation du récepteur
- **Détection d'erreurs** : Retransmission automatique
- **Numérotation** : Séquences et accusés de réception

**UDP (User Datagram Protocol) :**

- **Non fiable** : Pas de garantie de livraison
- **Sans connexion** : Pas d'établissement de session
- **Rapide** : Moins d'overhead
- **Utilisé pour** : Streaming, DNS, DHCP

---

### Couche 3 - RÉSEAU

**Rôle :** Routage des paquets entre réseaux différents

**Protocole principal : IP (Internet Protocol)**

**IPv4 :**

- **Format** : 32 bits (4 octets)
- **Exemple** : 192.168.1.1
- **Classes** : A, B, C (obsolète, remplacé par CIDR)
- **Adresses privées** : 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16

**IPv6 :**

- **Format** : 128 bits (16 octets)
- **Exemple** : 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- **Avantages** : Plus d'adresses, sécurité intégrée

**Autres protocoles :**

- **ICMP** : Messages d'erreur et diagnostic (ping)
- **ARP** : Résolution IP → MAC

---

### Couche 2 - LIAISON

**Rôle :** Contrôle d'accès au support physique

**Fonctions :**

- **Adressage physique** : Adresses MAC (48 bits)
- **Contrôle d'erreurs** : Détection et correction
- **Contrôle de flux** : Éviter la saturation
- **Accès au support** : CSMA/CD (Ethernet)

**Sous-couches :**

- **LLC** (Logical Link Control) : Interface avec couche réseau
- **MAC** (Media Access Control) : Contrôle d'accès au support

**Équipements :**

- **Switch** : Commutation au niveau 2
- **Bridge** : Interconnexion de segments
- **Point d'accès WiFi** : Accès sans fil

---

### Couche 1 - PHYSIQUE

**Rôle :** Transmission des bits sur le support physique

**Caractéristiques :**

- **Signaux** : Électriques, optiques, radio
- **Supports** : Câbles, fibres, ondes
- **Topologies** : Bus, étoile, anneau, maillée
- **Débit** : Vitesse de transmission

**Exemples de supports :**

- **Câble cuivre** : Ethernet (RJ45)
- **Fibre optique** : Longue distance, haut débit
- **WiFi** : Sans fil (2.4 GHz, 5 GHz)
- **Bluetooth** : Courte portée

---
## POINTS CLÉS À RETENIR

### Différences OSI vs TCP/IP :

- **OSI** : 7 couches
- **TCP/IP** : 4 couches

### Avantages de la modélisation en couches :

- **Modularité** : Chaque couche a un rôle précis
- **Interopérabilité** : Standards communs
- **Évolutivité** : Modification d'une couche sans impact sur les autres
- **Troubleshooting** : Diagnostic par couche

