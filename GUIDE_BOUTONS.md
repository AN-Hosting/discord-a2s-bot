# 🎮 Guide des Boutons de Contrôle - Bot Discord A2S

## 🚀 Boutons Disponibles

### ▶️ Bouton START
**Fonction** : Démarre le bot et commence la surveillance des serveurs

**Quand l'utiliser** :
- Au premier lancement du bot
- Après avoir arrêté le bot avec STOP
- Quand vous voulez reprendre la surveillance

**Ce qui se passe** :
- Le bot se connecte à Discord
- Il commence à surveiller tous les serveurs configurés
- Les canaux Discord se mettent à jour automatiquement

---

### ⏹️ Bouton STOP
**Fonction** : Arrête le bot et la surveillance

**Quand l'utiliser** :
- Pour arrêter temporairement la surveillance
- Avant de modifier la configuration
- Pour économiser les ressources

**Ce qui se passe** :
- Le bot se déconnecte de Discord
- La surveillance s'arrête
- Les canaux ne se mettent plus à jour

---

### 🔄 Bouton REDÉMARRER
**Fonction** : Redémarre le bot avec la nouvelle configuration

**Quand l'utiliser** :
- Après avoir modifié le fichier `config.yaml`
- Quand le bot ne répond plus
- Pour appliquer de nouveaux paramètres

**Ce qui se passe** :
- Le bot s'arrête complètement
- Il relit le fichier de configuration
- Il redémarre avec les nouveaux paramètres

---

## 📋 Ordre d'Utilisation Recommandé

### 1. Configuration Initiale
1. Modifiez le fichier `config.yaml`
2. Cliquez sur **START** pour démarrer

### 2. Modification de Configuration
1. Cliquez sur **STOP** pour arrêter
2. Modifiez le fichier `config.yaml`
3. Cliquez sur **REDÉMARRER** pour appliquer les changements

### 3. Utilisation Quotidienne
- **START** : Pour démarrer la surveillance
- **STOP** : Pour arrêter temporairement
- **REDÉMARRER** : Pour appliquer des modifications

---

## ⚠️ Points Importants

### Avant de Cliquer START
- ✅ Vérifiez que le fichier `config.yaml` est correctement configuré
- ✅ Vérifiez que votre token Discord est valide
- ✅ Vérifiez que vos serveurs sont accessibles

### Avant de Cliquer REDÉMARRER
- ✅ Sauvegardez vos modifications dans `config.yaml`
- ✅ Vérifiez la syntaxe YAML (pas d'erreurs d'indentation)
- ✅ Assurez-vous que tous les IDs Discord sont corrects

### En Cas de Problème
1. Cliquez sur **STOP**
2. Vérifiez les logs pour identifier l'erreur
3. Corrigez la configuration
4. Cliquez sur **REDÉMARRER**

---

## 🔍 Vérification du Fonctionnement

### Après avoir cliqué START
- ✅ Le bot apparaît en ligne sur Discord
- ✅ Les canaux se mettent à jour avec les informations des serveurs
- ✅ Les logs montrent des messages de connexion réussie

### Si ça ne fonctionne pas
- ❌ Vérifiez les logs pour les erreurs
- ❌ Vérifiez que le token Discord est correct
- ❌ Vérifiez que les IDs des canaux sont bons
- ❌ Vérifiez que vos serveurs sont accessibles

---

## 📞 Support

Si les boutons ne fonctionnent pas :
1. Vérifiez que l'application est bien lancée
2. Vérifiez les logs pour les erreurs
3. Contactez le support technique

---

*Guide rapide pour l'utilisation des boutons de contrôle du Bot Discord A2S* 