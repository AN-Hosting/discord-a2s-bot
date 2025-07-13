# 📋 Guide de Configuration du Bot Discord A2S

## 🎯 Vue d'ensemble

Ce bot Discord surveille vos serveurs de jeux et met à jour automatiquement les canaux Discord avec les informations en temps réel (nombre de joueurs, statut, etc.).

## 📋 Prérequis

- Un compte Discord
- Un serveur Discord où vous avez les permissions d'administrateur
- Les informations de vos serveurs de jeux (adresse IP, port query)

---

## 🚀 Étape 1 : Créer l'Application Discord

### 1.1 Accéder au Portail Développeur Discord

1. Allez sur [Discord Developer Portal](https://discord.com/developers/applications)
2. Connectez-vous avec votre compte Discord
3. Cliquez sur **"New Application"** (Nouvelle Application)

### 1.2 Configurer l'Application

1. **Nom de l'application** : Donnez un nom à votre bot (ex: "Mon Bot Serveur")
2. Cliquez sur **"Create"** (Créer)

### 1.3 Créer le Bot

1. Dans le menu de gauche, cliquez sur **"Bot"**
2. Cliquez sur **"Add Bot"** (Ajouter Bot)
3. Cliquez sur **"Yes, do it!"** pour confirmer

### 1.4 Récupérer le Token

1. Dans la section **"Token"**, cliquez sur **"Copy"** pour copier le token
2. **⚠️ IMPORTANT** : Gardez ce token secret ! Ne le partagez jamais
3. Ce token sera utilisé dans le fichier `config.yaml`

### 1.5 Configurer les Permissions

1. Dans la section **"Privileged Gateway Intents"**, activez :
   - ✅ **Presence Intent**
   - ✅ **Server Members Intent**
   - ✅ **Message Content Intent**

2. Cliquez sur **"Save Changes"** (Sauvegarder)

### 1.6 Inviter le Bot sur votre Serveur

1. Dans le menu de gauche, cliquez sur **"OAuth2"** puis **"URL Generator"**
2. Dans **"Scopes"**, cochez **"bot"**
3. Dans **"Bot Permissions"**, cochez :
   - ✅ **Manage Channels** (Gérer les canaux)
   - ✅ **Send Messages** (Envoyer des messages)
   - ✅ **Embed Links** (Intégrer des liens)
   - ✅ **Read Message History** (Lire l'historique des messages)
   - ✅ **Use External Emojis** (Utiliser des emojis externes)
   - ✅ **Add Reactions** (Ajouter des réactions)

4. Copiez l'URL générée et ouvrez-la dans votre navigateur
5. Sélectionnez votre serveur et cliquez sur **"Authorize"** (Autoriser)

---

## ⚙️ Étape 2 : Configurer le Fichier config.yaml

### 2.1 Configuration de Base

Ouvrez le fichier `config.yaml` et modifiez la section `bot` :

```yaml
bot:
  token: VOTRE_TOKEN_DISCORD_ICI  # Remplacez par votre token
  update_interval: 30s  # Intervalle de mise à jour (30 secondes)
  concurrency: 10  # Nombre de serveurs surveillés simultanément
```

### 2.2 Ajouter vos Serveurs

Dans la section `servers`, ajoutez vos serveurs :

```yaml
servers:
  - id: "Nom de votre serveur"  # Identifiant unique
    host: "IP_DE_VOTRE_SERVEUR"  # Adresse IP du serveur
    port: 27015  # Port query du serveur (27015 pour Steam par défaut)
    channel_id: 1234567890123456789  # ID du canal Discord
    category_id: 1234567890123456789  # ID de la catégorie Discord (optionnel)
    <<: *tpl  # Utilise le template de base
```

### 2.3 Récupérer les IDs Discord

#### Pour obtenir l'ID d'un canal :
1. Activez le mode développeur dans Discord : **Paramètres** → **Avancés** → **Mode développeur**
2. Clic droit sur le canal → **Copier l'identifiant**

#### Pour obtenir l'ID d'une catégorie :
1. Clic droit sur la catégorie → **Copier l'identifiant**

---

## 🎮 Étape 3 : Configuration des Serveurs de Jeux

### 3.1 Informations Requises

Pour chaque serveur, vous aurez besoin de :
- **Adresse IP** : L'adresse de votre serveur
- **Port** : Le port query de votre serveur (ex: 27015 pour Steam)
- **Nom unique** : Un identifiant pour le serveur

### 3.2 Exemple de Configuration

```yaml
servers:
  - id: "Mon Serveur DayZ"
    host: "192.168.1.100"
    port: 2302
    channel_id: 1234567890123456789
    category_id: 1234567890123456789
    <<: *tpl

  - id: "Mon Serveur Rust"
    host: "192.168.1.101"
    port: 28015
    channel_id: 9876543210987654321
    category_id: 9876543210987654321
    <<: *tpl
```

---

## 🎯 Étape 4 : Personnalisation des Templates

### 4.1 Nom du Canal

Le template `channel_name` définit le nom du canal Discord :

```yaml
channel_name: |
  {{ if .Info -}}
  {{ if eq .Info.ID 221100 }}{{ if .Extra.Time }}{{ DurationEmoji .Extra.Time }}{{ end }}{{ else }}🟢{{ end -}}
  -{{ .Info.Players }}∶{{ .Info.MaxPlayers }}-{{- .ID -}}
  {{ else -}}
  🔴-{{- .ID -}}
  {{ end -}}
```

**Variables disponibles :**
- `{{ .Info.Players }}` : Nombre de joueurs connectés
- `{{ .Info.MaxPlayers }}` : Nombre maximum de joueurs
- `{{ .ID }}` : Nom du serveur
- `🟢` : Serveur en ligne
- `🔴` : Serveur hors ligne

### 4.2 Description du Canal

Le template `channel_description` définit la description du canal :

```yaml
channel_description: |
  {{ if .Info -}}
  🟢 {{ .Info.Name }}
  📜 {{ .Info.Game }}
  👥 {{ .Info.Players }}/{{ .Info.MaxPlayers }}
  🌍 {{ .Info.Map }}
  📡 {{ .Host }}:{{ .Info.Port }}
  {{ else -}}
  🔴 Server {{ .ID }} offline
  📡 {{ .Host }}:{{ .Port }}
  {{ end -}}
```

---

## 🚀 Étape 5 : Utilisation des Boutons de Contrôle

### 5.1 Bouton Start
- **Fonction** : Démarre le bot et commence la surveillance
- **Utilisation** : Cliquez quand vous voulez activer la surveillance

### 5.2 Bouton Stop
- **Fonction** : Arrête le bot et la surveillance
- **Utilisation** : Cliquez pour arrêter temporairement

### 5.3 Bouton Redémarrer
- **Fonction** : Redémarre le bot avec la nouvelle configuration
- **Utilisation** : Cliquez après avoir modifié le fichier `config.yaml`

---

## 🔧 Configuration Avancée

### 6.1 Paramètres de Logging

```yaml
logging:
  level: info  # Niveau de log (debug, info, warn, error)
  format: text  # Format des logs (text ou json)
  output: stdout  # Sortie des logs (stdout, stderr, ou fichier)
```

### 6.2 Paramètres de Performance

```yaml
bot:
  update_interval: 30s  # Intervalle de mise à jour
  concurrency: 10  # Nombre de serveurs surveillés simultanément
```

### 6.3 Paramètres de Connexion

```yaml
base-template: &tpl
  timeout: 3  # Timeout en secondes
  buffer_size: 1024  # Taille du buffer
```

---

## ❗ Dépannage

### Problèmes Courants

#### 1. Bot ne répond pas
- ✅ Vérifiez que le token est correct
- ✅ Vérifiez que le bot a les bonnes permissions
- ✅ Vérifiez que le bot est bien invité sur le serveur

#### 2. Canaux ne se mettent pas à jour
- ✅ Vérifiez les IDs des canaux
- ✅ Vérifiez que le bot peut gérer les canaux
- ✅ Vérifiez la connectivité réseau vers vos serveurs

#### 3. Erreurs de connexion aux serveurs
- ✅ Vérifiez l'adresse IP et le port
- ✅ Vérifiez que le serveur est accessible
- ✅ Vérifiez le firewall

### Logs et Debug

Pour activer les logs détaillés, modifiez :

```yaml
logging:
  level: debug  # Changez info en debug
```

---

## 📞 Support

Si vous rencontrez des problèmes :
1. Vérifiez les logs du bot
2. Vérifiez la configuration
3. Contactez le support technique

---

## 🔒 Sécurité

- **Ne partagez jamais votre token Discord**
- **Gardez le fichier config.yaml sécurisé**
- **Utilisez des permissions minimales pour le bot**

---

*Documentation créée pour la configuration du Bot Discord A2S* 