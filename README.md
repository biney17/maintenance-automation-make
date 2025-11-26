# 🏭 Maintenance Automation - Python + GPT

[![Platform: Make.com](https://img.shields.io/badge/Platform-Make.com-9B59B6)](https://make.com)
[![Language: Python](https://img.shields.io/badge/Language-Python-3776AB?logo=python)](https://www.python.org/)
[![API: OpenAI](https://img.shields.io/badge/API-OpenAI-412991?logo=openai)](https://openai.com)
[![Database: Airtable](https://img.shields.io/badge/Database-Airtable-18ACEA?logo=airtable)](https://airtable.com)

Système **automatisé et intelligent** de maintenance industrielle qui détecte les anomalies machines en temps réel et génère des rapports professionnels avec l'IA.

---

## 📋 Table des matières

- [🎯 Vue d'ensemble](#-vue-densemble)
- [✨ Fonctionnalités](#-fonctionnalités)
- [🚀 Démarrage rapide](#-démarrage-rapide)
- [📊 Architecture](#-architecture)
- [📚 Guide d'utilisation](#-guide-dutilisation)
- [💰 Coûts](#-coûts)
- [🔧 Configuration avancée](#-configuration-avancée)
- [🐛 Dépannage](#-dépannage)
- [📞 Support](#-support)

---

## 🎯 Vue d'ensemble

Ce projet automatise complètement le processus de **surveillance et maintenance** des machines industrielles:

1. **📥 Collecte** des données de capteurs (température, pression, vibration)
2. **🔍 Analyse** automatique pour détecter les anomalies
3. **📝 Génération** de rapports professionnels avec GPT
4. **💾 Sauvegarde** des données et rapports dans Airtable
5. **⏰ Exécution** automatique sans surveillance humaine

**Résultat:** Maintenance prédictive et réactive en temps réel! 🚀

---

## ✨ Fonctionnalités

### 🔴 Détection d'anomalies intelligente
- ✅ Analyse **3 paramètres critiques** en temps réel
- ✅ Seuils **configurables** pour chaque machine
- ✅ **Alertes immédiates** en cas d'anomalie
- ✅ Historique complet des détections

### 🤖 Génération de rapports avec IA
- ✅ Rapports **professionnels** générés automatiquement
- ✅ Format **structuré** prêt pour email/PDF
- ✅ **Recommandations techniques** personnalisées
- ✅ Analyse contextuelle intelligente

### 📊 Intégration complète Airtable
- ✅ Synchronisation **bidirectionnelle** des données
- ✅ **Historique complet** des maintenances
- ✅ Base de données **centralisée**
- ✅ Visualisation facile dans Airtable

### ⚙️ Automatisation sans surveillance
- ✅ Exécution **programmée** (configurable)
- ✅ **Pas d'intervention** manuelle requise
- ✅ **Notifications** automatiques
- ✅ Logging complet des exécutions

### 🧩 Facilement extensible
- ✅ Ajouter de **nouvelles machines** facilement
- ✅ Modifier les **seuils d'alerte** en 1 clic
- ✅ Intégrer d'**autres services** (Slack, Email, Webhook)
- ✅ Adapter le prompt GPT à tes besoins

---

## 🚀 Démarrage rapide

### Prérequis

Assure-toi d'avoir:

- ✅ Un compte [Make.com](https://make.com) (gratuit)
- ✅ Une base [Airtable](https://airtable.com) (gratuit)
- ✅ Un compte [OpenAI](https://platform.openai.com) avec crédits ($5 gratuit)
- ✅ [Git](https://git-scm.com/) installé (optionnel)

### Installation en 5 minutes

#### 1️⃣ Cloner le projet

```bash
git clone https://github.com/biney17/maintenance-automation-make.git
cd maintenance-automation-make
```

#### 2️⃣ Configurer Airtable

Crée une nouvelle base avec **2 tables:**

**📥 Table 1: "Imported table" (Source de données)**

Crée ces colonnes:

| Colonne | Type | Description |
|---------|------|-------------|
| machine_id | Text | ID unique de la machine |
| date | Date | Date de la mesure |
| temperature | Number | Température en °C |
| pressure | Number | Pression en bar |
| vibration | Number | Vibration en m/s² |
| status | Text | État (OK, WARNING, CRITICAL, etc.) |
| created_at | Created time | Timestamp automatique |

**📤 Table 2: "Reports" (Rapports générés)**

Crée ces colonnes:

| Colonne | Type | Description |
|---------|------|-------------|
| machine_id | Text | ID de la machine |
| date | Date | Date du rapport |
| temperature | Number | Température mesurée |
| pressure | Number | Pression mesurée |
| vibration | Number | Vibration mesurée |
| status | Text | État de la machine |
| report | Long text | Rapport complet généré par GPT |
| created_at | Created time | Date de création |

#### 3️⃣ Importer le scénario Make

Le fichier `scenario.json` est juste une sauvegarde pour pouvoir le partager ou le restaurer.

#### 4️⃣ Configurer les connexions

**🔗 Airtable:**
- Base ID: Récupère depuis ton URL Airtable
- Table source: `Imported table`
- Table destination: `Reports`

**🔑 OpenAI:**
- API Key: [Récupère ici](https://platform.openai.com/api-keys)
- Modèle: `gpt-3.5-turbo`

#### 5️⃣ Tester le système

1. **Ajoute un enregistrement** dans Airtable (Imported table):
   ```
   machine_id: TEST_MACHINE
   date: 25/11/2024
   temperature: 75
   pressure: 2.5
   vibration: 3.2
   status: OK
   ```

2. **Clique "Run once"** dans Make

3. **Vérifie** que le rapport apparaît dans la table "Reports" ✅

✅ **C'est fait! Le système fonctionne!** 🎉

---

## 📊 Architecture

### Flux de traitement

```
┌─────────────────────┐
│   Airtable          │
│  "Imported table"   │  ← Ajoute des données ici
│   (Source)          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────────┐
│  Make Module 2          │
│  Airtable Watch Records │  → Détecte nouveaux records
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  Make Module 3          │
│  Python Code            │  → Analyse anomalies
│  Détection seuils       │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  Make Module 4          │
│  OpenAI GPT-3.5-turbo   │  → Génère rapport
│  Génération rapport     │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  Make Module 5          │
│  Airtable Create Record │  → Sauvegarde résultat
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────┐
│   Airtable          │
│   "Reports"         │  ← Récupère les rapports ici
│   (Destination)     │
└─────────────────────┘
```

### Seuils d'anomalies (par défaut)

| Paramètre | Minimum | Maximum | Unité | Action |
|-----------|---------|---------|-------|--------|
| Temperature | 20 | 80 | °C | 🔴 ANOMALY si dépassé |
| Pressure | 1.0 | 3.0 | bar | 🔴 ANOMALY si dépassé |
| Vibration | 0 | 5.0 | m/s² | 🔴 ANOMALY si dépassé |

---

## 📚 Guide d'utilisation

### Ajouter des données machines

**Étape 1: Va dans Airtable**
- Ouvre ta base
- Clique sur la table **"Imported table"**

**Étape 2: Ajoute un nouvel enregistrement**
- Clique le bouton **"+ Créer"**
- Remplis les colonnes:
  - machine_id: `TRUCK_A5`
  - date: `25/11/2024`
  - temperature: `72` (°C)
  - pressure: `2.1` (bar)
  - vibration: `2.5` (m/s²)
  - status: `OK`

**Étape 3: Sauvegarde**
- Clique **"Save"** ou appuie sur **Entrée**

### Voir les rapports générés

**Étape 1: Va dans Airtable**
- Ouvre ta base
- Clique sur la table **"Reports"**

**Étape 2: Consulte les rapports**
- Chaque ligne = 1 rapport généré
- Clique sur la colonne **"report"** pour voir le contenu complet

**Exemple de rapport généré:**
```
RAPPORT DE MAINTENANCE

Machine: TRUCK_A5
Date: 25/11/2024
Temperature: 72C
Pression: 2.1 bar
Vibration: 2.5 m/s2
Status: OK

ANALYSE
Anomalie: NON
Tous les parametres sont nominaux.
La machine fonctionne normalement.

RECOMMANDATIONS
- Continuer la surveillance standard
- Prochain controle: routine
- Maintenir la frequence actuelle
```

### Fréquence d'exécution

**Par défaut:** Toutes les 15 minutes

**Pour modifier dans Make:**
1. En bas du scénario, trouve **"Every 15 minutes"**
2. Clique pour changer:
   - "Every 5 minutes" (vérifications plus fréquentes)
   - "Every hour" (moins de coûts API)
   - "Every 30 minutes" (équilibre)

---

## 💰 Coûts

### Estimation mensuelle

| Service | Gratuit? | Prix | Usage estimé |
|---------|----------|------|--------------|
| **Airtable** | ✅ Oui (50 records) | $0 | Inclus |
| **Make.com** | ✅ Partiellement (1,000 ops) | $9-15 | ~50 ops/mois |
| **OpenAI API** | ✅ Oui ($5 trial) | ~$0.0005/1K tokens | ~$0.50-1 |
| **Total** | - | **$10-16/mois** | Production |

### Optimiser les coûts

1. **Diminue la fréquence** → Exécute toutes les heures au lieu de 15 min
2. **Limite les machines** → Commence avec quelques machines de test
3. **Réduis le prompt** → Moins de tokens = moins de coûts OpenAI

---

## 🔧 Configuration avancée

### Modifier les seuils d'anomalies

**Dans Make, Module 3 (Python), trouve:**

```python
temp_min, temp_max = 20, 80
pressure_min, pressure_max = 1.0, 3.0
vibration_min, vibration_max = 0, 5.0
```

**Exemple - Pour une machine très chaude:**
```python
temp_min, temp_max = 50, 120  # 50-120°C au lieu de 20-80°C
```

---

## 🐛 Dépannage

### ❌ "No space left on device"

**Cause:** Dépendances Python trop lourdes

**Solution:** J'ai déjà utilisé la détection par seuils simple (pas de scikit-learn)

### ❌ "Invalid API key"

**Cause:** Clé OpenAI invalide ou expirée

**Solution:**
1. Va sur https://platform.openai.com/api-keys
2. Génère une **nouvelle clé**
3. Mets à jour dans Make

### ❌ "Base not found"

**Cause:** ID Airtable incorrect

**Solution:**
1. Va dans Airtable
2. Copie l'ID de la base depuis l'URL
3. Mets à jour dans Make

### ❌ Aucun record créé dans "Reports"

**Cause:** Module 5 ne sauvegarde pas

**Solution:**
1. Clique "Run once"
2. Vérifie le mapping du Module 5
3. Assure-toi que le champ "report" contient `{{4.result}}`

### ❌ Rapport vide dans Airtable

**Cause:** GPT ne génère rien

**Solution:**
1. Vérifie que le Module 4 retourne du contenu
2. Vérifie le mapping dans Module 5
3. Utilise `{{4.result}}` au lieu de `{{4.choices[0].message.content}}`

### ❌ Le scénario ne se déclenche pas

**Cause:** Pas de nouveaux records dans "Imported table"

**Solution:**
1. Ajoute manuellement un enregistrement
2. Attends 30 secondes
3. Ou clique "Run once" pour forcer

---

## 📞 Support

### 📚 Documentation officielle

- [Make.com Help Center](https://www.make.com/en/help)
- [Airtable API Documentation](https://airtable.com/api)
- [OpenAI API Documentation](https://platform.openai.com/docs)
- [Python Documentation](https://docs.python.org/)

### 🐛 Signaler un bug

Ouvre une issue: [GitHub Issues](https://github.com/biney17/maintenance-automation-make/issues)

### 💬 Questions?

Crée une discussion: [GitHub Discussions](https://github.com/biney17/maintenance-automation-make/discussions)

---

## 📁 Structure du projet

```
maintenance-automation-make/
├── README.md                 # Documentation (ce fichier)
├── scenario.json             # Configuration Make (créée manuellement)
└── .gitignore               # Fichiers à ignorer
```

---

## 🎓 Concepts clés

### Détection d'anomalies simple

Le système compare les valeurs mesurées aux **seuils normaux**:

```python
IF temperature > 80°C THEN ANOMALY
IF pressure < 1.0 bar THEN ANOMALY
IF vibration > 5.0 m/s² THEN ANOMALY
```

### Génération de rapports IA

GPT prend les données analysées et génère un rapport **professionnel et contextuel** en langage naturel.

### Automatisation sans code

Tout fonctionne via **Make.com** - pas besoin de coder!

---

## 📈 Améliorations futures

- [ ] Dashboard de visualisation temps réel
- [ ] Prédictions IA avec historique
- [ ] Intégration Slack native
- [ ] Export PDF automatique
- [ ] Alertes SMS
- [ ] API REST personnalisée
- [ ] Machine Learning pour seuils adaptatifs

---

## 📄 Licence

Tous droits réservés. Ce projet est personnel et propriétaire.

Créé par **biney17** - 2025

---

## 🙏 Crédits

Créé par **biney17** - 2025

Utilise:
- [Make.com](https://make.com) - Plateforme d'automatisation
- [Airtable](https://airtable.com) - Base de données
- [OpenAI](https://openai.com) - Intelligence artificielle

---

## 📊 Statistiques du projet

- **Status:** ✅ Production Ready
- **Version:** 10.0
- **Dernière mise à jour:** 25/11/2025
- **Licence:** Propriétaire
- **Langage principal:** Python + Make Workflow

---

## 🚀 Prochaines étapes

1. **Clone le projet** et configure Airtable
2. **Importe le scénario** dans Make
3. **Ajoute tes données** dans Airtable
4. **Active l'automatisation** (Every 15 minutes)
5. **Consulte les rapports** automatiquement générés

**C'est prêt!** Profite de la maintenance automatisée! 🎉

---

**Questions?** Ouvre une issue sur GitHub! 💬
