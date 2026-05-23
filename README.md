# 💼 Comptabilité IDEL Pro V7

Application web de comptabilité professionnelle pour infirmiers libéraux (IDEL), avec synchronisation cloud via Supabase.

## ✨ Fonctionnalités

### 📋 6 Modules Complets

#### 👤 Profil
- Informations professionnelles (SIRET, RPPS, ADELI, URSSAF)
- Coordonnées complètes (adresse, téléphone, email)
- **Nouveau** : Informations de l'expert-comptable
  - Nom du cabinet
  - Adresse et téléphone
  - Email (pré-rempli automatiquement dans les envois)
- Configuration de l'exercice comptable

#### 💰 Opérations
- Ajout/modification/suppression d'opérations
- Classification par type (recette/dépense)
- Catégories du plan comptable IDEL
- Pièces justificatives (multi-fichiers)
- 🤖 **Scan IA** : Analyse automatique des factures (Claude API)
- Filtre par exercice comptable

#### 🏦 Banque
- Journal de trésorerie
- Suivi des encaissements réels
- Rapprochement bancaire
- Distinction opérations comptables vs flux bancaires

#### 🔄 Récurrentes
- Automatisation des dépenses fixes
- Périodicité configurable (mensuel, trimestriel, annuel)
- Création automatique des opérations

#### 📑 Documents
- Stockage de documents administratifs
- Organisation par catégories
- Upload et téléchargement sécurisés

#### 📊 Statistiques
- Graphiques de répartition
- Évolution des recettes/dépenses
- **Exports professionnels**
- **Email automatisé pour l'expert-comptable**

### 📧 Export Comptable Automatisé (Nouveauté V7)

#### Un seul bouton : "📧 Préparer l'envoi au comptable"

**Génère automatiquement** :
1. **Un fichier Excel complet** avec tous les onglets :
   - 📋 **Résumé** : Synthèse de la période, totaux, contenu
   - ⚖️ **Balance** : Balance des comptes avec totaux
   - 📚 **Grand Livre** : Un onglet par compte avec soldes cumulés
   - 📑 **FEC** : Format fiscal conforme (Fichier des Écritures Comptables)

2. **ZIP des justificatifs** : Toutes les pièces de la période

3. **Email pré-rempli** :
   - Destinataire : Email du comptable (depuis le profil)
   - Sujet automatique
   - Message professionnel avec liste des fichiers
   - Bouton pour ouvrir le client email

**Avantages** :
- ✅ Un seul fichier Excel au lieu de 3 fichiers séparés
- ✅ Email pré-rédigé et personnalisé
- ✅ Plus besoin de se rappeler quoi envoyer
- ✅ Gain de temps considérable

### 📊 Formats d'Export

#### Excel - Dossier Comptable Complet
- **Formatage professionnel** : En-têtes colorés, bordures, euros (1 234,56 €)
- **Balance des comptes** : Débit, crédit, solde
- **Grand Livre détaillé** : Un onglet par compte avec solde cumulé
- **FEC réglementaire** : 18 colonnes conformes à la norme fiscale
- **Résumé exécutif** : Vue d'ensemble de la période

#### ZIP - Justificatifs
- Organisation par opération (dossiers UUID)
- Noms de fichiers explicites avec timestamps
- Téléchargement direct depuis Supabase Storage

### 🤖 Intelligence Artificielle

**Scan de factures** (via Claude API Anthropic) :
- Upload d'une image de facture
- Extraction automatique :
  - Date
  - Montant
  - Description
  - Catégorie suggérée
- Pré-remplissage du formulaire

### 🎨 Caractéristiques Techniques

- **100% Web** : Aucune installation nécessaire
- **Cloud Supabase** : Synchronisation automatique
- **Responsive** : Mobile et desktop
- **Sécurisé** : Authentification et RLS (Row Level Security)
- **Temps réel** : Mises à jour instantanées
- **Formatage euros** : Respect des conventions françaises (espace comme séparateur de milliers)
- **Plan comptable IDEL** : Comptes 706xxx-708xxx (recettes) et 606xxx-628xxx (dépenses)

## 🚀 Installation

### Prérequis
- Un compte Supabase (gratuit)
- Un compte GitHub (pour l'hébergement)

### Étape 1 : Configurer Supabase

1. **Créer un projet** sur [Supabase](https://supabase.com)

2. **Exécuter le script SQL** dans SQL Editor :

```sql
-- Tables principales
CREATE TABLE profile (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  nom TEXT,
  prenom TEXT,
  siret TEXT,
  rpps TEXT,
  adeli TEXT,
  num_urssaf TEXT,
  adresse TEXT,
  code_postal TEXT,
  ville TEXT,
  telephone TEXT,
  email TEXT,
  comptable_cabinet TEXT,
  comptable_adresse TEXT,
  comptable_tel TEXT,
  comptable_email TEXT,
  exercice_debut DATE,
  exercice_fin DATE
);

CREATE TABLE transactions (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  date DATE NOT NULL,
  type TEXT NOT NULL,
  category TEXT NOT NULL,
  description TEXT NOT NULL,
  amount NUMERIC NOT NULL,
  payment_method TEXT,
  has_attachments BOOLEAN DEFAULT FALSE,
  encaisse BOOLEAN DEFAULT FALSE
);

CREATE TABLE attachments (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  transaction_id UUID REFERENCES transactions(id) ON DELETE CASCADE,
  file_name TEXT NOT NULL,
  file_type TEXT NOT NULL,
  file_size INTEGER NOT NULL,
  storage_path TEXT NOT NULL,
  public_url TEXT
);

-- Bucket Storage pour les justificatifs
INSERT INTO storage.buckets (id, name, public) 
VALUES ('justificatifs', 'justificatifs', true)
ON CONFLICT (id) DO NOTHING;

-- Policy RLS pour accès public au bucket
CREATE POLICY "Accès public justificatifs" 
ON storage.objects 
FOR ALL 
USING (bucket_id = 'justificatifs');
```

3. **Configurer le bucket Storage** :
   - Storage → Bucket "justificatifs"
   - Edit → ✅ Cocher "Public bucket"
   - Save

4. **Récupérer vos clés** :
   - Project Settings → API
   - Copier `Project URL` et `anon/public key`

### Étape 2 : Configurer l'application

1. **Cloner ou télécharger** ce repository

2. **Modifier `index.html`** (lignes ~200-202) :

```javascript
const SUPABASE_URL='VOTRE_URL_ICI';
const SUPABASE_KEY='VOTRE_CLE_ICI';
```

3. **Déployer sur GitHub Pages** :
   - Créer un nouveau repository
   - Uploader `index.html`
   - Settings → Pages → Source: main branch
   - Votre app sera sur : `https://VotreUsername.github.io/votre-repo/`

### Étape 3 : Première utilisation

1. **Ouvrir l'application**
2. **Onglet Profil** : Remplir vos informations
3. **Expert-comptable** : Renseigner le cabinet (nom, email, etc.)
4. **Exercice comptable** : Définir les dates de début et fin
5. **Commencer à saisir** vos opérations !

## 📖 Guide d'utilisation

### Ajouter une opération

1. **Onglet Opérations**
2. **Remplir le formulaire** :
   - Date
   - Type (Recette/Dépense)
   - Catégorie
   - Description
   - Montant
3. **📎 Ajouter des justificatifs** (optionnel)
4. **💾 Ajouter**

### Utiliser le scan IA

1. **Onglet Opérations**
2. **🤖 Scan intelligent**
3. **📸 Choisir une image** de facture
4. **Attendre l'analyse** (~5 secondes)
5. **Vérifier et ajuster** les données extraites
6. **💾 Ajouter**

### Envoyer à l'expert-comptable

1. **Onglet Profil** → Renseigner l'email du comptable
2. **Onglet Statistiques** → **📧 Préparer l'envoi au comptable**
3. **Vérifier** l'email pré-rempli
4. **Télécharger** les 2 fichiers générés :
   - `Comptabilite_YYYY-MM-DD_YYYY-MM-DD.xlsx`
   - `Justificatifs_YYYY-MM-DD_YYYY-MM-DD.zip`
5. **📧 Ouvrir mon client email**
6. **Joindre** les 2 fichiers téléchargés
7. **Envoyer** !

### Gérer les dépenses récurrentes

1. **Onglet Récurrentes**
2. **➕ Nouvelle dépense récurrente**
3. **Remplir** : Description, montant, périodicité, prochaine échéance
4. **💾 Ajouter**
5. L'app **créera automatiquement** l'opération à chaque échéance

### Rapprochement bancaire

1. **Onglet Banque**
2. **Ajouter** les opérations bancaires réelles
3. **Cocher** ✅ dans l'onglet Opérations pour marquer comme encaissé
4. **Voir** la trésorerie réelle vs comptabilité

## 🎯 Plan Comptable IDEL

### Recettes (Classe 7)
- **706100** : Honoraires (AMO) - Actes conventionnés
- **706200** : Honoraires (AMC) - Complémentaires
- **706300** : Honoraires hors nomenclature
- **706800** : Autres prestations (forfaits, indemnités)
- **708000** : Produits exceptionnels

### Dépenses (Classe 6)
- **606100** : Fournitures médicales
- **613200** : Locations immobilières (cabinet)
- **615100** : Entretien et réparations
- **615500** : Assurances professionnelles
- **616000** : Primes d'assurance
- **618100** : Documentation
- **618600** : Cotisations professionnelles
- **622600** : Honoraires comptables
- **623100** : Annonces et insertions
- **623200** : Publicité
- **625100** : Frais de voyages et déplacements
- **625600** : Missions et réceptions
- **626100** : Frais postaux
- **626200** : Frais de télécommunications
- **627200** : Frais bancaires
- **628000** : Autres charges

## 🔒 Sécurité et Confidentialité

- **RLS Supabase** : Chaque utilisateur ne voit que ses données
- **Bucket public** : Uniquement pour les justificatifs (pas de données sensibles dans les noms)
- **HTTPS** : Communication chiffrée
- **Pas de mot de passe** stocké côté client
- **Claude API** : Les images de scan ne sont pas conservées

## 🆘 Support et Problèmes Fréquents

### Le ZIP des justificatifs est vide
**Solution** : Le bucket n'est pas public
1. Supabase → Storage → Bucket "justificatifs"
2. Edit → ✅ Cocher "Public bucket"
3. Save

### Les fichiers ne s'uploadent pas
**Solution** : Vérifier la policy RLS
1. Supabase → Storage → Policies
2. Vérifier que "Accès public justificatifs" existe
3. Command: ALL, Applied to: public

### L'email du comptable n'est pas pré-rempli
**Solution** : Renseigner le profil
1. Onglet Profil
2. Section "Expert-comptable"
3. Remplir l'email
4. 💾 Enregistrer

### Les graphiques ne s'affichent pas
**Solution** : Problème de cache
1. Ctrl+Shift+R (vider le cache)
2. Recharger la page

## 📝 Changelog

### V7 (Mai 2026)
- ✨ Export comptable automatisé (1 fichier Excel complet)
- ✨ Email pré-rempli pour l'expert-comptable
- ✨ Nouveaux champs profil (téléphone, email)
- ✨ Section expert-comptable dans le profil
- 🐛 Correction : ZIP justificatifs (bucket public)

### V6 (Mai 2026)
- ✨ Préparation automatique de l'envoi comptable
- ✨ Modal email avec fichiers générés
- 🐛 Correction : Exports individuels déplacés en accordéon

### V5 (Mai 2026)
- ✨ Exports professionnels (FEC, Grand Livre, Balance)
- ✨ ZIP des justificatifs
- ✨ Formatage euros français
- ✨ Onglet Banque avec encaissements
- ✨ Dépenses récurrentes
- 🎨 UI améliorée avec graphiques

### V4 et antérieures
- Scan IA de factures
- Plan comptable IDEL
- Multi-attachments
- Supabase Storage
- Synchronisation cloud

## 🤝 Contribution

Les contributions sont bienvenues ! N'hésitez pas à :
- Signaler des bugs
- Proposer des améliorations
- Partager vos suggestions

## 📜 Licence

MIT License - Libre d'utilisation et de modification

## 👨‍💻 Auteur

Développé avec ❤️ pour les infirmiers libéraux

---

**Version actuelle : V7 - Mai 2026**

Pour toute question : Ouvrir une issue sur GitHub
