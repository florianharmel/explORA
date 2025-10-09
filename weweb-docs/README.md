# 🧭 Documentation du projet WeWeb

## 📚 Table des matières
1. [Aperçu général](#1-aperçu-général)
2. [Structure globale du site](#2-structure-globale-du-site)
3. [Fonctionnalités principales](#3-fonctionnalités-principales)
4. [Composants personnalisés](#4-composants-personnalisés)
5. [Développement et conventions](#5-développement-et-conventions)
6. [Appendices](#6-appendices)

---

## 1. Aperçu général

### 🎯 Objectif
Ce document centralise toute la documentation relative au **frontend WeWeb** du projet.

### 🌐 Architecture globale
Bien que ce dépôt se concentre sur **WeWeb**, il s’inscrit dans un écosystème composé de :
- **WeWeb** → Interface utilisateur (frontend)
- **Xano** → Backend et logique métier (API REST)
- **Airtable** → Base de données secondaire (catalogues, médias, etc.)

### 🔄 Flux simplifié
Utilisateur → WeWeb → Xano API → Airtable (via Xano)

---

## 2. Structure globale du site

### 🧩 Navigation
- Menu principal (top bar)
- Liens contextuels / boutons d’action
- Gestion des états (utilisateur connecté, droits, rôles)

### 🧱 Layout général
- **Header** : logo, navigation, boutons de session
- **Body** : contenu dynamique (sections, blocs, formulaires, modales)
- **Footer** : mentions, liens légaux, infos contextuelles

### 🗺️ Zones de contenu
- Zones configurables par page
- Intégration de données dynamiques (via variables et collections WeWeb)
- Bonnes pratiques de mise en page responsive

---

## 3. Fonctionnalités principales

### 🔐 Authentification
- Gestion de session utilisateur via WeWeb + Xano
- Variables globales d’utilisateur
- Redirections conditionnelles (connexion, déconnexion, rôles)

### 🧾 Gestion des projets
- Création / duplication d’un projet
- Sauvegarde d’état sur Xano
- Liaison dynamique des projets à l’utilisateur connecté

### 🛒 Passage de commande
- Processus en plusieurs étapes (sélection, récapitulatif, validation)
- Vérifications côté WeWeb avant appel API
- Gestion des statuts / retours utilisateurs

### 📸 Gestion média
- Upload photo / vidéo / fichier
- Aperçu, suppression, réimport
- Synchronisation avec Xano / Airtable via collections

### 🔔 Notifications internes
- Toasts / alertes / modales d’état
- Variables globales pour feedback (succès / erreur / info)

---

## 4. Composants personnalisés

| Composant | Description | Lien |
|------------|--------------|------|
| **Gantt** | Gestion et visualisation des plannings. | [📄 Voir la doc](./components/gantt.md) |
| **Admin Grid** | Tableau d’administration. | [📄 Voir la doc](./components/admin-grid.md) |
| **Catalog** | Affichage de produits ou éléments. | [📄 Voir la doc](./components/catalog.md) |
| **SuperButton** | Bouton intelligent. | [📄 Voir la doc](./components/superbutton.md) |
| **CustomSelect** | Sélecteur personnalisé. | [📄 Voir la doc](./components/customselect.md) |

---

## 5. Développement et conventions

### 🧩 Standards des composants
- Convention de nommage : `CustomComponentName`
- Fichiers : `config.js`, `element.vue`, `README.md`

### ⚙️ Événements
- Communication via le **bus d’événements WeWeb**
- Nom : `component:event` (ex : `gantt:updated`)

### 📝 Documentation embarquée
- Chaque composant affiche sa doc via un bouton “📘 Documentation”.
- Le markdown est chargé depuis son `README.md`.

### 🧱 Versioning
- Versions manuelles (`vX.Y`)
- Historique global dans `CHANGELOG.md`

---

## 6. Appendices

### 📖 Glossaire
| Terme | Définition |
|-------|-------------|
| WW Variable | Variable globale dans WeWeb |
| Collection | Liste connectée à une source |
| Custom Component | Composant Vue intégré dans WeWeb |

### 🗓️ Roadmap
- [ ] Finaliser la doc des composants
- [ ] Ajouter les captures d’écran
- [ ] Créer un guide contributeur

---
📄 Auteur : Florian Harmel
🔗 Version : 1.0.0
