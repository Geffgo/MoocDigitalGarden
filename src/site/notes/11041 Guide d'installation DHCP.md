---
{"dg-publish":true,"permalink":"/11041-guide-d-installation-dhcp/"}
---

# Guide d'installation Serveur DHCP
# Fiches Liées
- [[Accueil\|Accueil]]
- [[11040 DHCP\|11040 DHCP]]
---
## 1. Prérequis et Planification

### Prérequis Système

- **RAM minimum** : 1 GB (2 GB recommandé)
- **Espace disque** : 20 GB minimum
- **Réseau** : Interface réseau configurée avec IP statique
- **Système** : Ubuntu 20.04+ / CentOS 8+ / Windows Server 2016+

### Planification Réseau

```
Exemple de configuration :
- Réseau : 192.168.1.0/24
- Serveur DHCP : 192.168.1.10
- Passerelle : 192.168.1.1
- DNS : 8.8.8.8, 8.8.4.4
- Pool DHCP : 192.168.1.100-200
```

## 2. Installation sur Ubuntu/Debian

### Installation du Package

```bash
# Mise à jour du système
sudo apt update
sudo apt upgrade -y

# Installation du serveur DHCP
sudo apt install isc-dhcp-server -y
```

### Configuration de l'Interface

```bash
# Éditer le fichier de configuration des interfaces
sudo nano /etc/default/isc-dhcp-server

# Spécifier l'interface réseau
INTERFACESv4="eth0"
INTERFACESv6=""
```

### Configuration Principale

```bash
# Éditer le fichier de configuration principal
sudo nano /etc/dhcp/dhcpd.conf

# Contenu du fichier :
# Configuration globale
default-lease-time 86400;
max-lease-time 172800;
authoritative;

# Configuration DNS
option domain-name "example.local";
option domain-name-servers 8.8.8.8, 8.8.4.4;

# Déclaration du sous-réseau
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;
    option routers 192.168.1.1;
    option subnet-mask 255.255.255.0;
    option broadcast-address 192.168.1.255;
    option domain-name-servers 8.8.8.8, 8.8.4.4;
    option ntp-servers 192.168.1.1;
}

# Réservation d'adresse
host serveur-web {
    hardware ethernet 00:11:22:33:44:55;
    fixed-address 192.168.1.50;
}
```

### Démarrage et Activation

```bash
# Démarrer le service
sudo systemctl start isc-dhcp-server

# Activer au démarrage
sudo systemctl enable isc-dhcp-server

# Vérifier le statut
sudo systemctl status isc-dhcp-server
```

