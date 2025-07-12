---
{"dg-publish":true,"permalink":"/11021-guide-d-installation-dns-bind-9/"}
---

# Guide d'installation BIND9
# Fiches Liées
- [[Accueil\|Accueil]]
- [[11020 DNS\|11020 DNS]]
---
## Prérequis système

- **OS** : Ubuntu/Debian (22.04 LTS recommandé)
- **RAM** : 2 GB minimum, 4 GB recommandé
- **Espace disque** : 10 GB minimum
- **Privilèges** : accès root/sudo
- **Réseau** : IP statique configurée

## Installation

### 1. Mise à jour du système

```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Installation des packages

```bash
# Installation de BIND9 et utilitaires
sudo apt install bind9 bind9utils bind9-doc -y

# Installation d'outils de diagnostic
sudo apt install dnsutils -y
```

### 3. Vérification de l'installation

```bash
# Vérifier le statut du service
sudo systemctl status bind9

# Vérifier la version
named -v
```

## Configuration de base

### 1. Structure des fichiers

```
/etc/bind/
├── named.conf           # Configuration principale
├── named.conf.options   # Options globales
├── named.conf.local     # Zones locales
├── named.conf.default-zones  # Zones par défaut
└── zones/               # Répertoire des fichiers de zones
```

### 2. Configuration des options globales

**Fichier : `/etc/bind/named.conf.options`**

```bash
options {
    directory "/var/cache/bind";
    
    # Serveurs DNS de forwarding
    forwarders {
        8.8.8.8;
        8.8.4.4;
        1.1.1.1;
    };
    
    # Sécurité
    allow-recursion { localhost; 192.168.1.0/24; };
    allow-query { localhost; 192.168.1.0/24; };
    
    # Désactiver les transferts de zones
    allow-transfer { none; };
    
    # Écouter sur toutes les interfaces
    listen-on { any; };
    listen-on-v6 { any; };
    
    # Logs
    query-source address * port 53;
    
    # DNSSEC
    dnssec-validation auto;
};
```

### 3. Configuration des zones locales

**Fichier : `/etc/bind/named.conf.local`**

```bash
# Zone directe
zone "mondomaine.local" {
    type master;
    file "/etc/bind/zones/db.mondomaine.local";
};

# Zone inverse
zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.192.168.1";
};
```

## Création des fichiers de zones

### 1. Créer le répertoire des zones

```bash
sudo mkdir -p /etc/bind/zones
```

### 2. Zone directe

**Fichier : `/etc/bind/zones/db.mondomaine.local`**

```bash
$TTL    86400
@       IN      SOA     ns1.mondomaine.local. admin.mondomaine.local. (
                        2024071201  ; Serial
                        3600        ; Refresh
                        1800        ; Retry
                        604800      ; Expire
                        86400       ; Minimum TTL
)

; Serveurs de noms
@       IN      NS      ns1.mondomaine.local.
@       IN      NS      ns2.mondomaine.local.

; Enregistrements A
ns1     IN      A       192.168.1.10
ns2     IN      A       192.168.1.11
www     IN      A       192.168.1.20
mail    IN      A       192.168.1.30
ftp     IN      A       192.168.1.40

; Enregistrements MX
@       IN      MX      10 mail.mondomaine.local.

; Enregistrements CNAME
webmail IN      CNAME   mail.mondomaine.local.
```

### 3. Zone inverse

**Fichier : `/etc/bind/zones/db.192.168.1`**

```bash
$TTL    86400
@       IN      SOA     ns1.mondomaine.local. admin.mondomaine.local. (
                        2024071201  ; Serial
                        3600        ; Refresh
                        1800        ; Retry
                        604800      ; Expire
                        86400       ; Minimum TTL
)

; Serveurs de noms
@       IN      NS      ns1.mondomaine.local.
@       IN      NS      ns2.mondomaine.local.

; Enregistrements PTR
10      IN      PTR     ns1.mondomaine.local.
11      IN      PTR     ns2.mondomaine.local.
20      IN      PTR     www.mondomaine.local.
30      IN      PTR     mail.mondomaine.local.
40      IN      PTR     ftp.mondomaine.local.
```

## Permissions et propriétés

### 1. Définir les permissions

```bash
# Propriétaire des fichiers
sudo chown -R bind:bind /etc/bind/zones/

# Permissions des fichiers
sudo chmod 644 /etc/bind/zones/*
```

### 2. Vérifier la configuration

```bash
# Vérifier la syntaxe de la configuration principale
sudo named-checkconf

# Vérifier les fichiers de zones
sudo named-checkzone mondomaine.local /etc/bind/zones/db.mondomaine.local
sudo named-checkzone 1.168.192.in-addr.arpa /etc/bind/zones/db.192.168.1
```

## Démarrage et gestion du service

### 1. Gestion du service

```bash
# Démarrer le service
sudo systemctl start bind9

# Activer au démarrage
sudo systemctl enable bind9

# Redémarrer le service
sudo systemctl restart bind9

# Recharger la configuration
sudo systemctl reload bind9
```

### 2. Vérifier les logs

```bash
# Logs système
sudo journalctl -u bind9 -f

# Logs BIND spécifiques
sudo tail -f /var/log/syslog | grep named
```

## Tests et validation

### 1. Tests de base

```bash
# Test de résolution directe
nslookup www.mondomaine.local localhost

# Test de résolution inverse
nslookup 192.168.1.20 localhost

# Test avec dig
dig @localhost www.mondomaine.local
```

### 2. Tests avancés

```bash
# Test de résolution récursive
dig @localhost google.com

# Test des enregistrements MX
dig @localhost MX mondomaine.local

# Test de transfert de zone
dig @localhost AXFR mondomaine.local
```

## Sécurisation

### 1. Firewall

```bash
# UFW
sudo ufw allow 53/tcp
sudo ufw allow 53/udp

# iptables
sudo iptables -A INPUT -p tcp --dport 53 -j ACCEPT
sudo iptables -A INPUT -p udp --dport 53 -j ACCEPT
```

### 2. Configuration sécurisée

```bash
# Dans /etc/bind/named.conf.options
options {
    # Limiter les requêtes récursives
    allow-recursion { localhost; 192.168.1.0/24; };
    
    # Désactiver les notifications
    notify no;
    
    # Cache empoisoning protection
    max-cache-ttl 86400;
    max-ncache-ttl 10800;
    
    # Rate limiting
    rate-limit {
        responses-per-second 5;
        window 5;
    };
};
```

## Dépannage

### 1. Problèmes courants

```bash
# Vérifier si le port 53 est utilisé
sudo netstat -tlnp | grep :53

# Vérifier les processus BIND
ps aux | grep named

# Tester la connectivité
telnet localhost 53
```

### 2. Commandes utiles

```bash
# Vider le cache DNS
sudo rndc flush

# Recharger une zone spécifique
sudo rndc reload mondomaine.local

# Statistiques BIND
sudo rndc stats
```

## Configuration client

### 1. Configurer les clients

```bash
# /etc/resolv.conf
nameserver 192.168.1.10
nameserver 192.168.1.11
search mondomaine.local
```

### 2. Test depuis un client

```bash
# Test de résolution
nslookup www.mondomaine.local
ping www.mondomaine.local
```