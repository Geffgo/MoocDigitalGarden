---
{"dg-publish":true,"permalink":"/10022-guide-d-installation-https-tls/"}
---

# Guide d'installation TLS 
# Fiches Liées
- [[Accueil\|Accueil]]
- [[10020 HTTP et HTTPS\|10020 HTTP et HTTPS]]
- [[10021 Guide d'installation HTTPS SSL\|10021 Guide d'installation HTTPS SSL]]
---
## 1. Prérequis

### Informations Nécessaires

- **Nom de domaine** : example.com
- **Serveur web** : Apache ou Nginx
- **Accès root** : sudo ou administrateur
- **Ports ouverts** : 80 (HTTP) et 443 (HTTPS)

### Vérifications Préalables

```bash
# Vérifier le domaine
ping example.com

# Vérifier les ports
sudo netstat -tlnp | grep :80
sudo netstat -tlnp | grep :443
```

## 2. Installation Automatique avec Let's Encrypt

### Ubuntu/Debian + Apache

```bash
# Installation
sudo apt update
sudo apt install certbot python3-certbot-apache

# Génération du certificat
sudo certbot --apache -d example.com -d www.example.com

# Renouvellement automatique
sudo crontab -e
# Ajouter : 0 12 * * * /usr/bin/certbot renew --quiet
```

### Ubuntu/Debian + Nginx

```bash
# Installation
sudo apt update
sudo apt install certbot python3-certbot-nginx

# Génération du certificat
sudo certbot --nginx -d example.com -d www.example.com

# Renouvellement automatique
sudo systemctl enable certbot.timer
```

## 3. Configuration Apache

### Fichier de Configuration SSL

```apache
# /etc/apache2/sites-available/example.com-ssl.conf

<VirtualHost *:443>
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/html
    
    # Certificats SSL
    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
    
    # Sécurité SSL
    SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
    SSLCipherSuite ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256
    
    # Redirection HTTPS
    Header always set Strict-Transport-Security "max-age=31536000"
</VirtualHost>

# Redirection HTTP vers HTTPS
<VirtualHost *:80>
    ServerName example.com
    ServerAlias www.example.com
    Redirect permanent / https://example.com/
</VirtualHost>
```

### Activation des Modules

```bash
# Activer SSL
sudo a2enmod ssl
sudo a2enmod headers
sudo a2enmod rewrite

# Activer le site
sudo a2ensite example.com-ssl.conf
sudo systemctl reload apache2
```

### Activation de la Configuration

```bash
# Tester la configuration
sudo nginx -t

# Activer le site
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
sudo systemctl reload nginx
```

## 4. Installation Manuelle (Certificat Payant)

### Génération de la Clé Privée

```bash
# Créer le répertoire
sudo mkdir -p /etc/ssl/private
sudo mkdir -p /etc/ssl/certs

# Générer la clé privée
sudo openssl genrsa -out /etc/ssl/private/example.com.key 2048
sudo chmod 600 /etc/ssl/private/example.com.key
```

### Création de la CSR

```bash
# Générer la CSR
sudo openssl req -new -key /etc/ssl/private/example.com.key -out /tmp/example.com.csr

# Informations à saisir :
# Country Name: FR
# State: Votre région
# City: Votre ville
# Organization: Votre entreprise
# Organizational Unit: IT Department
# Common Name: example.com
# Email: admin@example.com
```

### Installation du Certificat

```bash
# Copier le certificat reçu
sudo cp certificate.crt /etc/ssl/certs/example.com.crt
sudo cp intermediate.crt /etc/ssl/certs/intermediate.crt

# Créer la chaîne complète
sudo cat /etc/ssl/certs/example.com.crt /etc/ssl/certs/intermediate.crt > /etc/ssl/certs/example.com-fullchain.crt
```

## 5. Tests et Vérification

### Tests de Base

```bash
# Test de connectivité
curl -I https://example.com

# Vérifier le certificat
openssl s_client -connect example.com:443 -servername example.com

# Test de redirection
curl -I http://example.com
```

### Outils de Test en Ligne

- **SSL Labs** : https://www.ssllabs.com/ssltest/
- **SSL Checker** : https://www.sslchecker.com/sslchecker

### Validation du Certificat

```bash
# Vérifier l'expiration
echo | openssl s_client -connect example.com:443 2>/dev/null | openssl x509 -noout -dates

# Vérifier la chaîne de certificats
echo | openssl s_client -connect example.com:443 -showcerts 2>/dev/null
```

