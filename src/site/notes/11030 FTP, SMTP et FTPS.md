---
{"dg-publish":true,"permalink":"/11030-ftp-smtp-et-ftps/"}
---

# Fiche Réseau : FTP, FTPS et SFTP
# Fiches Liées
- [[Accueil\|Accueil]]
- 
---
## Vue d'ensemble

### FTP (File Transfer Protocol)

**Définition** : Protocole de transfert de fichiers standardisé, non sécurisé, datant de 1971.

### FTPS (FTP over SSL/TLS)

**Définition** : Extension sécurisée de FTP utilisant SSL/TLS pour le chiffrement.

### SFTP (SSH File Transfer Protocol)

**Définition** : Protocole de transfert de fichiers sécurisé fonctionnant sur SSH.

## Comparaison technique

|Caractéristique|FTP|FTPS|SFTP|
|---|---|---|---|
|**Port par défaut**|21 (cmd) + 20 (data)|21 (explicite) / 990 (implicite)|22|
|**Protocole de base**|TCP|TCP + SSL/TLS|SSH|
|**Chiffrement**|Aucun|SSL/TLS|SSH|
|**Authentification**|Mot de passe en clair|Certificats SSL + mot de passe|Clés SSH + mot de passe|
|**Nombre de connexions**|2 (contrôle + données)|2 (contrôle + données)|1 (multiplexée)|
|**Pare-feux**|Complexe|Complexe|Simple|

## Sécurité

### FTP

- **Niveau de sécurité** : Aucun
- **Problèmes** :
    - Mots de passe transmis en clair
    - Données non chiffrées
    - Vulnérable aux écoutes réseau
    - Attaques man-in-the-middle faciles

### FTPS

- **Niveau de sécurité** : Élevé
- **Avantages** :
    - Chiffrement SSL/TLS des données et commandes
    - Authentification par certificats
    - Intégrité des données garantie
- **Modes** :
    - **Explicite** : commence en FTP puis passe en SSL
    - **Implicite** : SSL dès la connexion

### SFTP

- **Niveau de sécurité** : Très élevé
- **Avantages** :
    - Chiffrement SSH complet
    - Authentification par clés publiques/privées
    - Tunnel sécurisé unique
    - Résistant aux attaques

## Fonctionnement

### FTP

1. Connexion de contrôle (port 21)
2. Authentification en clair
3. Ouverture canal de données (port 20)
4. Transfert non chiffré

### FTPS

1. Connexion FTP standard
2. Négociation SSL/TLS
3. Authentification sécurisée
4. Transfert chiffré sur canaux séparés

### SFTP

1. Connexion SSH unique (port 22)
2. Authentification SSH
3. Tunnel multiplexé pour commandes et données
4. Transfert intégralement chiffré

## Clients et outils

### Multi-protocoles

- **FileZilla** : FTP, FTPS, SFTP
- **WinSCP** : FTPS, SFTP
- **Cyberduck** : FTP, FTPS, SFTP

### Spécialisés

- **PuTTY/PSCP** : SFTP uniquement
- **OpenSSH** : SFTP natif
- **curl** : Support des trois protocoles

