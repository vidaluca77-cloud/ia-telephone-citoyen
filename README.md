# IA Téléphone Citoyen

Système d'IA téléphonique pour améliorer l'engagement citoyen et faciliter l'accès aux services publics.

## 📋 Description

Ce projet utilise n8n pour créer un système d'IA téléphonique intelligent qui permet aux citoyens d'accéder facilement aux informations et services publics via un système de réponse vocale automatisé alimenté par l'intelligence artificielle.

## 🚀 Fonctionnalités

- **Réponse vocale intelligente** : Utilisation d'OpenAI pour comprendre et répondre aux questions des citoyens
- **Intégration téléphonique** : Compatible avec Twilio pour les appels entrants
- **Base de connaissances** : Accès aux informations sur les services publics français
- **Workflows automatisés** : Gestion des demandes et routage intelligent avec n8n
- **Multilingue** : Support du français avec possibilité d'extension

## 🛠️ Technologies utilisées

- **n8n** : Plateforme d'automatisation de workflows
- **Docker** : Conteneurisation de l'application
- **OpenAI** : IA pour la compréhension et génération de texte/voix
- **Twilio** : Services de téléphonie cloud
- **PostgreSQL** : Base de données (optionnelle)
- **Redis** : Cache et sessions (optionnel)

## 📦 Installation

### Prérequis

- Docker et Docker Compose installés
- Compte OpenAI avec clé API
- Compte Twilio pour les services téléphoniques
- Git pour cloner le repository

### Étapes d'installation

1. **Cloner le repository**
   ```bash
   git clone https://github.com/vidaluca77-cloud/ia-telephone-citoyen.git
   cd ia-telephone-citoyen
   ```

2. **Configurer les variables d'environnement**
   ```bash
   cp .env.example .env
   ```
   
   Éditez le fichier `.env` et remplissez les valeurs nécessaires :
   - `OPENAI_API_KEY` : Votre clé API OpenAI
   - `TWILIO_ACCOUNT_SID` : Votre SID de compte Twilio
   - `TWILIO_AUTH_TOKEN` : Votre token d'authentification Twilio
   - `TWILIO_PHONE_NUMBER` : Votre numéro de téléphone Twilio
   - Autres configurations selon vos besoins

3. **Lancer avec Docker Compose**
   ```bash
   # Démarrage simple avec SQLite
   docker-compose up -d
   
   # Ou avec PostgreSQL
   docker-compose --profile postgres up -d
   
   # Ou avec Redis en plus
   docker-compose --profile postgres --profile redis up -d
   ```

4. **Accéder à n8n**
   - Ouvrez votre navigateur et allez sur `http://localhost:5678`
   - Connectez-vous avec les identifiants définis dans votre fichier `.env`
   - Par défaut : `admin` / `changeme`

5. **Importer les workflows**
   - Les workflows seront disponibles dans le dossier `./workflows`
   - Importez-les dans n8n via l'interface web

## 🔧 Configuration

### Variables d'environnement importantes

| Variable | Description | Valeur par défaut |
|----------|-------------|-----------------|
| `N8N_BASIC_AUTH_USER` | Nom d'utilisateur n8n | `admin` |
| `N8N_BASIC_AUTH_PASSWORD` | Mot de passe n8n | `changeme` |
| `OPENAI_API_KEY` | Clé API OpenAI | - |
| `TWILIO_ACCOUNT_SID` | SID du compte Twilio | - |
| `TWILIO_AUTH_TOKEN` | Token d'auth Twilio | - |
| `TWILIO_PHONE_NUMBER` | Numéro Twilio | - |

### Configuration de Twilio

1. Créez un compte sur [Twilio](https://www.twilio.com)
2. Obtenez un numéro de téléphone
3. Configurez les webhooks pour pointer vers votre instance n8n
4. URL webhook : `http://votre-domaine:5678/webhook/twilio`

## 📚 Utilisation

### Démarrage rapide

1. Assurez-vous que tous les services sont démarrés :
   ```bash
   docker-compose ps
   ```

2. Vérifiez les logs en cas de problème :
   ```bash
   docker-compose logs n8n
   ```

3. Testez votre configuration en appelant le numéro Twilio configuré

### Workflows disponibles

- **Réception d'appels** : Workflow principal pour traiter les appels entrants
- **Traitement IA** : Analyse des demandes et génération de réponses
- **Routage intelligent** : Redirection vers les services appropriés
- **Logging** : Enregistrement des interactions pour amélioration

## 🔒 Sécurité

- Changez les mots de passe par défaut
- Utilisez HTTPS en production
- Configurez un firewall approprié
- Limitez l'accès aux ports Docker
- Sauvegarder régulièrement la base de données

## 🚀 Déploiement en production

### Avec reverse proxy (Nginx)

```nginx
server {
    listen 80;
    server_name votre-domaine.com;
    
    location / {
        proxy_pass http://localhost:5678;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Variables d'environnement pour la production

```bash
N8N_PROTOCOL=https
N8N_HOST=votre-domaine.com
WEBHOOK_URL=https://votre-domaine.com/
APP_ENV=production
```

## 🤝 Contribution

1. Forkez le projet
2. Créez une branche pour votre fonctionnalité
3. Committez vos changements
4. Pushez vers la branche
5. Ouvrez une Pull Request

## 📝 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 📞 Support

Pour toute question ou problème :
- Ouvrez une issue sur GitHub
- Consultez la documentation de [n8n](https://docs.n8n.io/)
- Vérifiez la documentation [Twilio](https://www.twilio.com/docs)

## 🔄 Mise à jour

```bash
# Arrêter les services
docker-compose down

# Mettre à jour le code
git pull origin main

# Reconstruire et redémarrer
docker-compose up -d --build
```

---

**Note** : Ce projet est conçu pour améliorer l'accessibilité aux services publics français. Assurez-vous de respecter la réglementation RGPD lors de la collecte et du traitement des données personnelles.
