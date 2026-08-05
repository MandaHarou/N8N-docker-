<<<<<<< HEAD
# 🤖 n8n — Déploiement Docker Sécurisé

> Instance **n8n** auto-hébergée via Docker, exposée publiquement avec **ngrok**, sécurisée par authentification et chiffrement.

---

## 📋 Table des matières

- [Prérequis](#prérequis)
- [Installation rapide](#installation-rapide)
- [Configuration](#configuration)
- [Démarrage](#démarrage)
- [Accès à l'interface](#accès-à-linterface)
- [Commandes utiles](#commandes-utiles)
- [Sécurité](#sécurité)
- [Structure du projet](#structure-du-projet)

---

## Prérequis

Avant de commencer, assurez-vous d'avoir installé :

- [Docker](https://docs.docker.com/get-docker/) ≥ 24
- [Docker Compose](https://docs.docker.com/compose/install/) ≥ 2
- Un tunnel [ngrok](https://ngrok.com/) actif (ou un autre reverse-proxy)

---

## Installation rapide

```bash
# 1. Cloner le dépôt
git clone https://github.com/votre-utilisateur/n8n-docker.git
cd n8n-docker

# 2. Copier le fichier de configuration
cp .env.example .env

# 3. Remplir les variables sensibles
nano .env

# 4. Lancer le conteneur
docker compose up -d
```

---

## Configuration

Toutes les variables sensibles sont gérées dans le fichier **`.env`** (jamais commité).

Copiez `.env.example` vers `.env` et renseignez chaque valeur :

```bash
cp .env.example .env
```

### Variables disponibles

| Variable | Description | Exemple |
|---|---|---|
| `N8N_BASIC_AUTH_ACTIVE` | Active l'authentification HTTP | `true` |
| `N8N_BASIC_AUTH_USER` | Nom d'utilisateur de connexion | `admin` |
| `N8N_BASIC_AUTH_PASSWORD` | Mot de passe de connexion | `MonMotDePasse!` |
| `N8N_ENCRYPTION_KEY` | Clé de chiffrement des credentials n8n | `<hex 64 chars>` |
| `N8N_HOST` | Domaine public exposé | `xyz.ngrok-free.dev` |
| `N8N_PORT` | Port interne de n8n | `5678` |
| `N8N_PROTOCOL` | Protocole utilisé | `https` |
| `WEBHOOK_URL` | URL de base pour les webhooks | `https://xyz.ngrok-free.dev/` |
| `N8N_CORS_ALLOW_ORIGIN` | Origine autorisée par CORS | `https://xyz.ngrok-free.dev` |
| `N8N_CORS_ALLOW_METHODS` | Méthodes HTTP autorisées | `GET,POST,OPTIONS` |
| `N8N_CORS_ALLOW_HEADERS` | Headers HTTP autorisés | `Content-Type,Authorization` |

### Générer une clé de chiffrement sécurisée

```bash
openssl rand -hex 32
```

---

## Démarrage

```bash
# Démarrer en arrière-plan
docker compose up -d

# Vérifier que le conteneur est bien actif
docker compose ps

# Voir les logs en temps réel
docker compose logs -f n8n
```

---

## Accès à l'interface

Une fois démarré, n8n est accessible via votre tunnel ngrok :

```
https://<N8N_HOST>
```

Connectez-vous avec les identifiants définis dans `.env` :
- **Utilisateur** : valeur de `N8N_BASIC_AUTH_USER`
- **Mot de passe** : valeur de `N8N_BASIC_AUTH_PASSWORD`

> 💡 En local, n8n est également accessible sur `http://localhost:5678`

---

## Commandes utiles

```bash
# Arrêter le conteneur
docker compose down

# Redémarrer après modification du .env
docker compose down && docker compose up -d

# Mettre à jour l'image n8n vers la dernière version
docker compose pull && docker compose up -d

# Accéder au shell du conteneur
docker exec -it n8n sh

# Sauvegarder les données n8n
tar -czf n8n_backup_$(date +%Y%m%d).tar.gz ~/.n8n
```

---

## Sécurité

Ce projet applique les bonnes pratiques suivantes :

- 🔐 **Authentification HTTP Basic** activée sur toutes les routes
- 🔑 **Clé de chiffrement** pour les credentials stockés dans n8n
- 🌐 **CORS restreint** à l'origine ngrok uniquement
- 📁 **Variables sensibles** isolées dans `.env` (jamais commité)
- 🚫 **`.gitignore`** protégeant `.env`, les données locales et les logs

> ⚠️ **Important** : Si votre dépôt est public ou partagé, changez immédiatement votre `N8N_BASIC_AUTH_PASSWORD` et `N8N_ENCRYPTION_KEY` si ceux-ci ont déjà été exposés dans un commit précédent.

---

## Structure du projet

```
n8n-docker/
├── docker-compose.yml   # Définition du service n8n
├── .env                 # 🔒 Variables sensibles (NON commité)
├── .env.example         # Template de configuration (commité)
├── .gitignore           # Fichiers exclus du dépôt Git
├── n8n.json             # Export de workflow n8n (exemple)
└── README.md            # Ce fichier
```

---

## Licence

Projet personnel — libre d'utilisation et d'adaptation.
=======
## N8N ON DOCKER
>>>>>>> f0c2847229bda37fd36674c0c97d280d7be0326e
