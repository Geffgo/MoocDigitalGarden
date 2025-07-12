---
{"dg-publish":true,"permalink":"/10020-http-et-https/"}
---

# Fiche Réseau : HTTP et HTTPS
# Fiches Liées
- [[Accueil\|Accueil]]
- [[10021 Guide d'installation HTTPS SSL\|10021 Guide d'installation HTTPS SSL]]
---
## INTRODUCTION

### HTTP (HyperText Transfer Protocol)

**Définition :** Protocole de communication pour le transfert de documents web

**Caractéristiques principales :**

- **Couche application** (couche 7 OSI)
- **Port par défaut** : 80
- **Protocole texte** : Lisible par l'homme
- **Sans état** : Chaque requête est indépendante
- **Client-Serveur** : Architecture requête/réponse

### HTTPS (HTTP Secure)

**Définition :** Version sécurisée de HTTP utilisant SSL/TLS

**Caractéristiques principales :**

- **Port par défaut** : 443
- **Chiffrement** : Communication cryptée
- **Authentification** : Vérification de l'identité du serveur
- **Intégrité** : Protection contre la modification des données

---

## COMPARAISON HTTP vs HTTPS

|Aspect|HTTP|HTTPS|
|---|---|---|
|**Sécurité**|Aucune|Chiffrement SSL/TLS|
|**Port**|80|443|
|**Vitesse**|Plus rapide|Légèrement plus lent|
|**Certificats**|Non requis|Certificat SSL obligatoire|
|**URL**|http://example.com|https://example.com|
|**Confidentialité**|Données visibles|Données chiffrées|
|**SEO**|Pénalisé|Favorisé par Google|

---

## FONCTIONNEMENT HTTP

### Architecture Client-Serveur

```
Client (Navigateur)  →  Requête HTTP  →  Serveur Web
                    ←  Réponse HTTP  ←
```

### Cycle de vie d'une requête :

1. **Résolution DNS** : www.example.com → 192.168.1.100
2. **Connexion TCP** : Établissement sur port 80
3. **Envoi requête** : GET /index.html HTTP/1.1
4. **Traitement serveur** : Recherche de la ressource
5. **Envoi réponse** : 200 OK + contenu HTML
6. **Fermeture connexion** : Fin de la communication

---

## STRUCTURE DES MESSAGES HTTP

### Requête HTTP

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
Accept-Language: fr-FR,fr;q=0.9,en;q=0.8
Connection: keep-alive
```

### Réponse HTTP

```
HTTP/1.1 200 OK
Date: Mon, 12 Jul 2025 10:30:00 GMT
Server: Apache/2.4.41
Content-Type: text/html; charset=UTF-8
Content-Length: 1234
Connection: close

<!DOCTYPE html>
<html>
<head><title>Page d'accueil</title></head>
<body>Contenu de la page</body>
</html>
```

---

## MÉTHODES HTTP

### Méthodes principales :

#### GET

- **Usage** : Récupérer une ressource
- **Idempotent** : Oui (peut être répété)
- **Cache** : Oui
- **Exemple** : `GET /users/123`

#### POST

- **Usage** : Créer une nouvelle ressource
- **Idempotent** : Non
- **Cache** : Non
- **Exemple** : `POST /users` (création utilisateur)

#### PUT

- **Usage** : Créer ou remplacer une ressource
- **Idempotent** : Oui
- **Cache** : Non
- **Exemple** : `PUT /users/123` (mise à jour complète)

#### DELETE

- **Usage** : Supprimer une ressource
- **Idempotent** : Oui
- **Cache** : Non
- **Exemple** : `DELETE /users/123`

#### PATCH

- **Usage** : Modification partielle
- **Idempotent** : Non
- **Cache** : Non
- **Exemple** : `PATCH /users/123` (mise à jour partielle)

#### HEAD

- **Usage** : Récupérer les en-têtes uniquement
- **Idempotent** : Oui
- **Cache** : Oui
- **Exemple** : `HEAD /users/123` (vérifier existence)

#### OPTIONS

- **Usage** : Découvrir les méthodes supportées
- **Idempotent** : Oui
- **Cache** : Oui
- **Exemple** : `OPTIONS /users`
