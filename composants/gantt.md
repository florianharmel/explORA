# 📊 Composant GANTT — Vue projets (WeWeb)

**Auteur :** Florian Harmel  
**Version :** 1.0  
**Date :** Octobre 2025  

---

## 🎯 Objectif

Le composant **GANTT** permet de visualiser les projets sur une **échelle de temps**.  
Chaque projet est représenté par une **barre colorée** correspondant à sa période de réalisation (début / fin).  
L’objectif est d’offrir une **vue synthétique et interactive** des projets sur plusieurs mois, directement dans WeWeb.

---

## 🏗️ Architecture

Le composant s’appuie sur une structure simple :

1. **L’échelle de temps (timeline)**  
   - Affiche les mois de manière horizontale sur une période définie.  
   - La durée visible est contrôlée via le paramètre `Number of Months`.

2. **Les barres de projets**  
   - Chaque projet est affiché sous forme de barre horizontale positionnée selon sa date de début et de fin.  
   - La couleur de la barre dépend du niveau de criticité du projet.  
   - Un clic sur la barre permet de **rediriger vers la fiche du projet**.

3. **La pagination**  
   - Si la période contient plus de projets que la zone d’affichage ne peut en contenir,  
     le composant affiche un système de pagination (page 1, 2, …).

---

## ⚙️ Paramètres configurables

| Paramètre | Type | Description |
|------------|------|-------------|
| **Number of Months** | number | Définit le nombre de mois visibles sur la timeline (ex : `6`). |
| **Animations** | JavaScript / JSON | Liste des projets à afficher (voir structure ci-dessous). |

---

## 🧾 Format attendu pour le paramètre `Animations`

Ce paramètre attend une **liste d’objets JSON** représentant les projets.  
Chaque objet décrit les métadonnées nécessaires à l’affichage du GANTT.

### Exemple

```js
[
  {
    Name: "Juliette Has A Gun / Nocibé : Summer Pack - S30",
    id: "recw8rI4xjF6vTGrn",
    criticity: "VERT",
    "Start Date": "2025-07-21T00:00:00.000Z",
    "End Date": "2025-08-05T00:00:00.000Z",
    Statut: "En attente de prise en charge Elba"
  },
  {
    Name: "Juliette Has A Gun / Nocibé : Gentlewoman Sparkle - S31",
    id: "recpUxa6HkF5DwqJ6",
    criticity: "VERT",
    "Start Date": "2025-07-25T00:00:00.000Z",
    "End Date": "2025-08-10T00:00:00.000Z",
    Statut: "En attente de brief"
  },
  {
    Name: "Juliette Has A Gun / Sephora : Sephora Elba - S39",
    id: "recfKz61pM7DQyR2k",
    criticity: "ROUGE",
    "Start Date": "2025-09-23T00:00:00.000Z",
    "End Date": "2025-10-10T00:00:00.000Z",
    Statut: "En cours de production"
  }
]
```

---

## 🎨 Couleurs et criticité

Le champ **`criticity`** détermine la **couleur de la barre du projet**.

| Criticity | Couleur associée | Signification |
|------------|------------------|----------------|
| `VERT` | 🟩 Vert | Projet sans alerte, dans les temps. |
| `ORANGE` | 🟧 Orange | Attention : suivi requis. |
| `ROUGE` | 🟥 Rouge | Projet critique / en retard. |
| `BLEU` | 🟦 Bleu | Projet terminé ou stable. |

Les couleurs peuvent être ajustées dans le code du composant selon la charte graphique.

---

## 🖱️ Interaction — Clic sur une barre

Chaque barre est **cliquable**.  
L’action par défaut est une **redirection vers la fiche du projet**.

- **Événement émis :** `onProjectClick`
- **Valeur passée :** l’objet du projet concerné (même structure que `Animations`)

### Exemple d’intégration (workflow WeWeb)

Lors du clic sur une barre :
```json
{
  "id": "recw8rI4xjF6vTGrn",
  "Name": "Juliette Has A Gun / Nocibé : Summer Pack - S30",
  "criticity": "VERT",
  "Start Date": "2025-07-21T00:00:00.000Z",
  "End Date": "2025-08-05T00:00:00.000Z"
}
```

➡️ **Action à brancher :**
- Redirection vers `/projets/{{id}}`
- Ou déclenchement d’un workflow personnalisé (ex : affichage d’un détail latéral).

---

## 📆 Pagination

Lorsque plusieurs pages sont nécessaires (ex : plus de projets que la hauteur visible),
un système de **pagination numérique** est affiché (1, 2, 3…).

- La pagination ne modifie pas l’échelle de temps, mais **alterne les lignes affichées**.
- Chaque page conserve les proportions temporelles.

---

## 📦 Données en entrée typiques

Les projets proviennent généralement :
- d’un **appel Xano** (collection WeWeb),
- ou d’une **source statique formatée** pour le champ `Animations`.

### Exemple d’intégration WeWeb :
```js
{{ collections["Projets_En_Cours"].data }}
```

---

## 🔧 Options de personnalisation

| Élément | Description |
|----------|--------------|
| **Nombre de mois visibles** | Ajuste la largeur totale du GANTT. |
| **Échelle temporelle** | Adaptée automatiquement selon la période des projets. |
| **Couleur des barres** | Définie via la clé `criticity`. |
| **Hauteur de ligne** | Automatique selon le nombre de projets visibles. |
| **Animation d’apparition** | Optionnelle (fade / slide sur chargement). |

---

## 📸 Exemples visuels

Les captures suivantes montrent :
1. Une vue complète du GANTT sur 6 mois.  
2. La distinction des projets selon leur criticité.  
3. Le positionnement temporel précis des barres.  
4. La pagination inférieure pour naviguer entre les ensembles de projets.

*(Voir les images associées dans la documentation du projet.)*

---

## 🔗 Références

- **WeWeb** : composant personnalisé intégré à la logique du projet.  
- **Xano** : source des données (API REST).  
- **Structure JSON** : compatible avec les workflows dynamiques.

---

## ✅ Bonnes pratiques

- Vérifier la cohérence des dates (`Start Date` < `End Date`).  
- Uniformiser les formats de date (ISO 8601 recommandé).  
- Définir clairement la criticité (`VERT`, `ORANGE`, `ROUGE`, `BLEU`).  
- Utiliser la pagination pour les longues listes (>10 projets).  
- Brancher l’action de clic sur un workflow de navigation vers le détail du projet.

---
