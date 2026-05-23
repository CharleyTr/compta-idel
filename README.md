# 💼 Comptabilité IDEL Cloud

Application de comptabilité pour infirmière libérale avec synchronisation cloud Supabase.

## 🚀 Déploiement sur GitHub Pages (5 minutes)

### Étape 1 : Créer un dépôt GitHub

1. Allez sur https://github.com
2. Cliquez sur **"New repository"** (bouton vert)
3. **Nom du dépôt** : `compta-idel` (ou autre nom)
4. **Public** ou **Private** (au choix)
5. ✅ Cochez **"Add a README file"**
6. Cliquez **"Create repository"**

### Étape 2 : Uploader les fichiers

1. Dans votre dépôt, cliquez sur **"Add file"** → **"Upload files"**
2. **Glissez-déposez** le fichier `index.html` (et tous les autres fichiers de ce dossier)
3. **Commit message** : "Initial commit"
4. Cliquez **"Commit changes"**

### Étape 3 : Activer GitHub Pages

1. Dans votre dépôt, allez dans **"Settings"** (en haut)
2. Dans le menu de gauche, cliquez sur **"Pages"**
3. **Source** : Sélectionnez `main` (ou `master`)
4. **Folder** : `/ (root)`
5. Cliquez **"Save"**
6. ✅ Attendez 1-2 minutes

### Étape 4 : Accéder à votre application

Votre app sera disponible à :
```
https://VOTRE-USERNAME.github.io/compta-idel/
```

**Exemple** : Si votre username est `marie-dupont` et le dépôt `compta-idel` :
```
https://marie-dupont.github.io/compta-idel/
```

---

## 📱 Installation sur mobile (PWA)

Une fois déployée, vous pouvez **installer l'application** sur votre téléphone :

### iPhone / iPad :
1. Ouvrez l'URL dans Safari
2. Cliquez sur le bouton **Partager** (□↑)
3. Descendez et cliquez **"Sur l'écran d'accueil"**
4. Cliquez **"Ajouter"**
5. ✅ L'icône apparaît sur votre écran d'accueil !

### Android :
1. Ouvrez l'URL dans Chrome
2. Menu (⋮) → **"Installer l'application"**
3. Cliquez **"Installer"**
4. ✅ L'app apparaît dans vos applications !

---

## ⚙️ Configuration Supabase

Vos identifiants Supabase sont **déjà configurés** dans l'application :

- **Project ID** : `hzwypmkhedplzrlsksqd`
- **URL** : `https://hzwypmkhedplzrlsksqd.supabase.co`
- **Anon Key** : Configurée ✅

### Tables créées :
- ✅ `profile` - Profil professionnel
- ✅ `transactions` - Opérations comptables
- ✅ `attachments` - Justificatifs

### Bucket créé :
- ✅ `justificatifs` - Stockage des documents scannés

---

## 🎯 Fonctionnalités

✅ **Profil professionnel** - SIRET, RPPS, ADELI, etc.  
✅ **Opérations** - Recettes et dépenses  
✅ **Justificatifs** - Scan de documents (photos/PDF)  
✅ **Cloud sync** - Données sauvegardées automatiquement  
✅ **Export Excel** - Pour votre comptable  
✅ **Multi-device** - Accédez depuis n'importe où  
✅ **PWA** - Installable comme une app native  

---

## 🔒 Sécurité

### Données privées
- Vos données sont **privées** dans Supabase
- Seul vous y avez accès via votre compte
- GitHub Pages sert juste le code HTML (pas de données)

### HTTPS
- GitHub Pages utilise **HTTPS automatiquement**
- Toutes les communications sont chiffrées

---

## 🛠️ Mise à jour de l'application

Pour mettre à jour l'application :

1. Dans GitHub, allez dans votre dépôt
2. Cliquez sur le fichier `index.html`
3. Cliquez sur l'icône **"Éditer"** (✏️)
4. Faites vos modifications
5. **Commit changes**
6. ✅ Le site se met à jour automatiquement en ~1 minute

---

## 📊 Utilisation

1. **Première utilisation** :
   - Remplissez votre profil professionnel
   - Vos infos sont sauvegardées dans Supabase

2. **Ajouter des opérations** :
   - Cliquez "Nouvelle opération"
   - Remplissez le formulaire
   - Attachez des justificatifs (photos de factures)
   - Sauvegardé automatiquement ☁️

3. **Export pour comptable** :
   - Cliquez "Télécharger Excel"
   - Fichier prêt avec toutes les infos !

---

## 🆘 Problèmes courants

### "Impossible de se connecter à Supabase"
- Vérifiez que les tables SQL sont bien créées
- Vérifiez que le bucket `justificatifs` existe

### "L'application ne se charge pas"
- Attendez 2-3 minutes après l'activation de GitHub Pages
- Videz le cache du navigateur (Ctrl+F5)
- Vérifiez l'URL (doit finir par `.github.io/...`)

### "Je ne vois pas mes données"
- Les données sont dans Supabase, pas dans GitHub
- Ouvrez la console (F12) pour voir les erreurs

---

## 💡 Conseils

✅ **Ajoutez l'app à votre écran d'accueil** pour un accès rapide  
✅ **Utilisez depuis n'importe quel appareil** avec la même URL  
✅ **Faites des exports Excel réguliers** pour backups  
✅ **Vérifiez Supabase** de temps en temps pour voir vos données  

---

## 📞 Support

Si vous avez des questions :
- Ouvrez la console du navigateur (F12) pour voir les erreurs
- Vérifiez que Supabase est bien configuré
- Testez l'URL sur plusieurs navigateurs

---

## 🎉 Prêt !

Votre application comptable cloud est maintenant déployée et accessible partout ! 🚀

**URL de votre app** : `https://VOTRE-USERNAME.github.io/VOTRE-REPO/`
