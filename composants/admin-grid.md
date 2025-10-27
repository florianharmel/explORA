# 🧩 Composant DataGrid d’administration — WeWeb + Xano

**Auteur :** Florian Harmel  
**Version :** 1.2  
**Date :** Octobre 2025  

---

## 🎯 Objectif

Fournir un **composant générique d’administration** permettant d’afficher, filtrer, trier et gérer les données issues d’une **table Xano**, directement depuis **WeWeb**.

Le composant repose sur le **Data Grid natif de WeWeb** (basé sur AG Grid) et ajoute des fonctionnalités CRUD (Create / Read / Update / Delete), de **détail**, et d’**import/export CSV**.

---

## 🏗️ Architecture

Le composant est structuré autour de deux parties :

1. **La grille principale (`admin_grid`)**
   - Affiche les données (listes, colonnes dynamiques).
   - Gère les boutons d’action (`Détails`, `Suppression`, etc.).
   - Contient les réglages de tri, filtre, import/export et template JSON.

2. **La popup de détail / édition**
   - Générée dynamiquement à partir des paramètres JSON.
   - Sert à :
     - la **consultation** d’un enregistrement,
     - la **modification**,
     - ou l’**ajout** d’un nouvel élément.

---

## ⚙️ Configuration principale (dans WeWeb)

| Propriété | Description |
|------------|-------------|
| **Data** | Collection principale affichée dans la grille. |
| **Template** | Code JSON décrivant les colonnes, champs et comportements. |
| **Sort / Filter** | Activation des options de tri et de filtrage. Ces éléments sont bindés au modèle et donc permettent de contrôler les filtres et tris depuis d'autres composants WeWeb |
| **Import / Export** | Configuration de l’import/export CSV. |
| **Display Documentation** | Active ou non la zone de documentation du composant. |
| **ViewOnly** | Active le mode lecture seule (aucun ajout/modification). |
| **FullSizeScreen** | Étend la grille à la largeur de la page. |
| **editOnly** | Active uniquement la modification (sans ajout). |
| **addOnly** | Active uniquement l'ajout (sans modification). |

---

## 📑 Structure JSON de configuration

Chaque configuration de grille est définie sous forme d’un tableau d’objets décrivant les colonnes et champs du formulaire.

### Exemple minimal

```js
return [
  {
    field: "name",
    headerName: "Nom",
    cellDataType: "text",
    inForm: true,
    required: true,
    editable: true,
    filter: true,
    sort: true,
    width: "300px"
  },
  {
    headerName: "Détails",
    cellDataType: "action",
    actionName: "details",
    actionLabel: "Détails",
    pinned: "right",
    width: "100px"
  }
];
```

---

## 🧱 Champs disponibles

### 🏷️ Champs standards

| Champ | Type | Description |
|-------|------|-------------|
| `field` | string | Nom du champ Xano (chemin imbriqué possible, ex. `"brand.name"`). |
| `headerName` | string | Nom affiché dans l’en-tête. |
| `cellDataType` | string | `"text"`, `"number"`, `"boolean"`, `"date"`, `"image"`, `"action"`. |
| `width` | string | Largeur (ex. `"200px"`). |
| `widthAlgo` | string | Si flex, un paramètre flex est attendu (`"fixed"`, `"flex"`) |
| `flex` | number | Nombre permettant de déterminer une largeur de colonne en proportionnel |
| `editable` | bool | Permet l’édition inline. |
| `filter` | bool | Active le filtre. |
| `sort` | bool | Active le tri. |
| `pinned` | string | Fige la colonne (`"left"` / `"right"`). |
| `hide` | bool | Masque la colonne dans la grille. (Pas dans le formulaire d'édition / ajout) |

---

### 🧩 Champs spécifiques au formulaire

| Champ | Type | Description |
|-------|------|-------------|
| `inForm` | string | Définit la visibilité du champ dans les formulaires. <br>Valeurs possibles : `"view"`, `"edit"`, `"add"`, `"none"`. |
| `required` | bool | Rend le champ obligatoire. |
| `editType` | string | Type d’éditeur : `"text"`, `"select"`, `"select_dynamic"`, `"select_conditional"`, `"image"`. |
| `options` | array / ref | Liste d’options statiques ou collection Xano. |
| `fieldObject` | string | Objet parent pour la sérialisation (ex. `"brand"`). |
| `initLinkedObjectValue` | string | (select_conditional) référence à la colonne servant de paramètre conditionnel (ex. `"target_id"`). |
| `dynamicParameter` | string | (select_dynamic) paramètre transmis à l’endpoint. |
| `endPoint_path` | string | (select_dynamic) chemin de l’endpoint Xano. |
| `endPoint_groupApi` | string | (select_dynamic) ID du groupe d’API Xano. |
| `imageWidth` | string | Largeur d’affichage pour les champs `"image"`. |
| `imageHeight` | string | Hauteur d’affichage pour les champs `"image"`. |

> **Remarque :** la valeur `"none"` pour `inForm` indique que le champ est présent dans la grille mais n’apparaît ni en vue détail, ni dans les formulaires d’ajout ou d’édition.

---

## 🧠 Types de champs dynamiques

### 🪄 Select simple

```js
editType: "select",
options: [
  { id: "FR", name: "France" },
  { id: "CH", name: "Suisse" },
  { id: "LU", name: "Luxembourg" }
]
```

### 🔁 Select dynamique

Les options sont chargées depuis un **endpoint Xano**, en fonction d’un paramètre.

```js
editType: "select_dynamic",
dynamicParameter: "group_id",
endPoint_path: "group_entities",
endPoint_groupApi: "coqyvShK"
```

🧩 Fonctionnement :  
- Ouvre un **mini DataGrid** affichant les options reçues de l’API.  
- Permet la **sélection multiple** si configurée.  
- Inclut une **pagination automatique** (ex. “1 à 10 sur 245 éléments”).  
- Retourne un ou plusieurs objets selon la configuration du champ.  

---

### 🔗 Select conditionnel

Une liste dépend d’une autre :

```js
editType: "select_conditional",
options: collections['1234abcd']?.['data']?.['targets']
```

Structure de données attendue :

```js
[{
   code: "code",
   label: "Libellé du code",
   options : [{}, ...]
}]
```

💡 Utilisé pour des cas de sélection hiérarchique (ex. type → sous-type).

---

### 🖼️ Image

Affichage et upload d’image :

```js
editType: "image",
field: "medias_dam.url",
fieldObject: "medias_dam",
cellDataType: "image",
imageHeight: "100%"
```

---

## 🧭 Modes d’affichage

| Mode | Description |
|------|--------------|
| **Affichage simple** | Lecture seule (aucun ajout ni édition). |
| **Ajout + Modification** | CRUD complet. |
| **Modification seule** | Pas d’ajout, uniquement édition/suppression. |
| **Ajout seul** | Pas de modification, uniquement ajout. |
| **ViewOnly** | Lecture seule sur tous les champs. |
| **EditOnly** | Permet uniquement l’édition d’enregistrements existants. |
| **AddOnly** | Permet uniquement l’ajout de nouveaux éléments. |

Les modes se contrôlent via les propriétés `ViewOnly`, `editOnly`, `addOnly`, ou les boutons de la barre supérieure.

---

## ⚙️ Gestion des workflows (Add / Edit / Delete)

Les actions principales (`add`, `edit`, `delete`) ne déclenchent **aucune requête par défaut**.  
Elles **émettent un événement** que l’on peut intercepter via un **workflow WeWeb** branché sur le composant.

### ➕ Workflow : `add`

- **Entrée du workflow :** un objet contenant les valeurs du formulaire.  
- **Utilisation :** libre à l’utilisateur d’appeler l’API Xano correspondante ou de modifier le comportement (par ex. ajouter à une collection locale).

Exemple :
```json
{
  "name": "Nouveau client",
  "country_code": "FR",
  "postal_code": "75001"
}
```

---

### ✏️ Workflow : `edit`

- **Entrée du workflow :** un tableau comportant deux éléments :
  1. La **ligne initiale** (objet d’origine).
  2. Les **valeurs modifiées** issues du formulaire.  

Le composant effectue un **merge des deux** avant de le transmettre.

Exemple :
```json
[
  {
    "id": 14,
    "name": "Client ORA",
    "postal_code": "75001"
  },
  {
    "postal_code": "75002"
  }
]
```

---

### 🗑️ Workflow : `delete`

- **Entrée du workflow :** un objet représentant la ligne à supprimer.  
- **Utilisation :** à connecter à l’API Xano de suppression, ou à tout autre traitement personnalisé.

Exemple :
```json
{
  "id": 14,
  "name": "Client ORA",
  "country_code": "FR"
}
```

---

## 📦 Import / Export CSV

Accessible via le panneau latéral :

- **Import** : charge un fichier `.csv` respectant la structure du template.  
- **Export** : permet d’exporter toutes les lignes ou uniquement la vue filtrée.

### Paramètres :

| Champ | Description |
|--------|-------------|
| `type_import` | Identifiant technique (ex. `display_spot`). |
| `label` | Nom affiché dans le sélecteur (ex. `Espaces d’affichage`). |

---

## 📜 Événements émis

| Événement | Déclencheur | Description |
|------------|-------------|--------------|
| `add` | Validation du formulaire d’ajout | Création d’un nouvel élément. |
| `edit` | Validation du formulaire d’édition | Mise à jour d’un élément existant. |
| `delete` | Clic sur le bouton “Suppression” | Suppression d’un élément. |
| `details` | Clic sur le bouton “Détails” | Ouvre la popup de détail. |

---

## 🔗 Références

- **Documentation officielle WeWeb DataGrid**  
  👉 [https://docs.weweb.io/elements/data-grid.html](https://docs.weweb.io/elements/data-grid.html)
- **Backend :** Xano (API REST configurée via `endPoint_path` et `groupApi`)
- **Exemples JSON complets :** `display_spot`, `catalog_scope`, `client_group`, etc.

---

## ✅ Bonnes pratiques

- Utiliser `inForm: "view"`, `"edit"`, `"add"` pour ajuster la visibilité et l’éditabilité des champs selon le contexte.  
- Centraliser les `options` dynamiques dans des **collections WeWeb**.  
- Définir un `actionName` explicite pour chaque action.  
- Tester les imports CSV avec le **template exporté**.  
- Utiliser `fieldObject` pour les structures imbriquées (`object.property`).  
- Connecter systématiquement les workflows `add`, `edit` et `delete` à vos APIs Xano.  
- Préférer `select_dynamic` pour des données volumineuses et `select_conditional` pour des relations parent/enfant.  

---
