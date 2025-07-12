---
{"dg-publish":true,"permalink":"/untitled/"}
---

# Guide d'installation SSL 
# Fiches Liées
- [[Accueil\|Accueil]]
- [[10020 HTTP et HTTPS\|10020 HTTP et HTTPS]]
---
## 1. Prérequis

### Informations nécessaires

- Nom de domaine valide
- Accès administrateur au serveur
- Serveur web configuré (Apache, Nginx, IIS, etc.)
- Ports 80 et 443 ouverts

### Outils requis

- Terminal/ligne de commande
- Éditeur de texte
- Accès FTP/SFTP ou SSH

## 2. Types de certificats SSL

### Certificats gratuits

- **Let's Encrypt** : Gratuit, automatisé, valide 90 jours
- **Cloudflare SSL** : Gratuit avec compte Cloudflare

### Certificats payants

- **DV (Domain Validated)** : Validation basique du domaine
- **OV (Organization Validated)** : Validation de l'organisation
- **EV (Extended Validation)** : Validation étendue (barre verte)

## 3. Installation avec Let's Encrypt

### Installation sur Ubuntu/Debian

```bash
# Installation de Certbot
sudo apt update
sudo apt install certbot python3-certbot-apache

# Génération du certificat (Apache)
sudo certbot --apache -d example.com -d www.example.com

# Génération du certificat (Nginx)
sudo apt install python3-certbot-nginx
sudo certbot --nginx -d example.com -d www.example.com
```
### Renouvellement automatique

```bash
# Test du renouvellement
sudo certbot renew --dry-run

# Cron job pour renouvellement automatique
echo "0 12 * * * /usr/bin/certbot renew --quiet" | sudo crontab -
```

## 4. Installation manuelle d'un certificat SSL

### Génération d'une clé privée

```bash
# Génération de la clé privée (2048 bits)
openssl genrsa -out private.key 2048

# Génération de la clé privée (4096 bits - plus sécurisé)
openssl genrsa -out private.key 4096
```

### Création d'une CSR (Certificate Signing Request)

```bash
openssl req -new -key private.key -out certificate.csr
```

### Informations à fournir pour la CSR

- **Country Name (C)** : Code pays (FR)
- **State (ST)** : Région/État
- **City (L)** : Ville
- **Organization (O)** : Nom de l'organisation
- **Organizational Unit (OU)** : Département
- **Common Name (CN)** : Nom de domaine principal
- **Email Address** : Adresse e-mail

## 5. Configuration Nginx

### Fichier de configuration SSL

```nginx
server {
    listen 443 ssl http2;
    server_name example.com www.example.com;
    root /var/www/html;
    
    # Certificats SSL
    ssl_certificate /path/to/certificate.crt;
    ssl_certificate_key /path/to/private.key;
    
    # Sécurité SSL moderne
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256;
    ssl_prefer_server_ciphers off;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    
    # HSTS (optionnel)
    add_header Strict-Transport-Security "max-age=63072000" always;
    
    location / {
        try_files $uri $uri/ =404;
    }
}

# Redirection HTTP vers HTTPS
server {
    listen 80;
    server_name example.com www.example.com;
    return 301 https://$server_name$request_uri;
}
```

### Test et rechargement Nginx

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 6. Vérification de l'installation

### Tests en ligne de commande

```bash
# Test de connectivité SSL
openssl s_client -connect example.com:443

# Vérification du certificat
openssl x509 -in certificate.crt -text -noout

# Test avec curl
curl -I https://example.com
```

### Outils de test en ligne

- **SSL Labs** : https://www.ssllabs.com/ssltest/
- **SSL Checker** : https://www.sslchecker.com/sslchecker
- **DigiCert SSL Installation Checker**

