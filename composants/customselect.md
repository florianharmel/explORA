
# 🔽 Composant — SelectCustom (WeWeb)

**Auteur :** Florian Harmel  
**Version :** 1.0  
**Date :** Octobre 2025  

---

## 🎯 Objectif
Sélecteur personnalisable avec recherche intégré, trois rendus visuels et la capacité d’exposer **l’objet complet sélectionné** (pas seulement un id). Idéal pour les listes de marques, magasins, espaces, etc.

---

## 🧩 Variantes disponibles
- **SelectCustom** : dropdown classique (ouvre vers le bas).  
- **SelectCustomTop** : dropdown **ouvre vers le haut** (utile en bas d’écran).  
- **SelectCustomVisual** : option **avec visuel** (vignette image + label).

> Les trois partagent les mêmes props et le même modèle de données.

---

## ⚙️ Propriétés (paneau Specific)

| Propriété | Type | Description |
|---|---|---|
| **options** | `Array<Object>` | Source de données du sélecteur. Peut être une collection, un tableau statique, ou une formule. |
| **default** | `string \| number \| null` | Valeur initiale (id/clé d’une option). |
| **placeholder** | `string` | Texte affiché quand aucune valeur n’est choisie. |
| **dropdownMaxHeight** (`dropdown…`) | `number(px)` | Hauteur max. du menu (scroll interne au‑delà). |
| **icon** | `string` | Nom de l’icône Material Symbols affichée dans le champ. |
| **label** | `string` | Nom de la **propriété de l’option** utilisée comme libellé (ex. `brand_name`). |
| **Map keys** | `bool` | Si activé, mappe les noms attendus (`id`, `label`, `image`, etc.). Sinon, utilisez des formules pour lire d’autres champs. |

---

## 🗂️ Schéma attendu des `options`

Le composant **n’impose pas** un schéma unique, mais pour bénéficier de toutes les features il est recommandé de fournir au minimum :

```js
[
  {
    id: "rec123",            // identifiant technique
    label: "RAY-BAN",        // libellé pour l’affichage
    // Champs additionnels libres :
    brand_name: "RAY-BAN",
    visual_url: "https://.../image.jpg",
    description: "…",
    // … n’importe quel autre attribut métier
  },
  // ...
]
```

- La propriété **`label`** affichée peut être remplacée via la prop **`label`** (ex. `brand_name`).  
- **SelectCustomVisual** utilise `visual_url` (ou le champ que vous mappez) pour afficher l’image.

---

## 🔎 Recherche
Un **champ de recherche** est disponible en tête du menu pour filtrer les options (client‑side).

---

## 🧠 Valeurs exposées par le composant

| Binding | Type | Description |
|---|---|---|
| **value** | `string \| number \| null` | Identifiant de l’option sélectionnée (par défaut `option.id`). |
| **label** | `string` | Libellé de l’option sélectionnée (`option[labelField]`). |
| **selected_object** | `Object` | **Objet complet** correspondant à l’option choisie. Exposé tel quel au formulaire / workflows. |

> Exemple (capture “espace — selected_object”) :  
> `{ id, name, label, visual_url, description, ... }`

---

## 🛠️ Exemple — alimenter `options` depuis une collection

Supposons une collection `brands` dont chaque entrée possède `airtable_id`, `brand_name`, `logo_url`.

**Formule (JS) dans `options` :**
```js
collections["brands"]?.data?.map(b => ({
  id: b.airtable_id,              // value renvoyée par le select
  label: b.brand_name,            // libellé affiché
  brand_name: b.brand_name,       // conservé pour selected_object
  visual_url: b.logo_url,         // utilisé par SelectCustomVisual
  raw: b                          // on peut garder l’objet brut si besoin
})) ?? []
```

**Prop `label`** (paneau Specific) : `brand_name`  
> Le champ affiché dans la liste et le champ “value label” peut être redéfini sans modifier l’objet.

---

## 🖼️ Variante avec visuel (SelectCustomVisual)

Pour afficher une **vignette image** dans la liste **et** dans le champ sélectionné :
- Fournir une clé `visual_url` (ou votre nom personnalisé) sur chaque option.  
- Dans le composant, l’image sera rendue à gauche du label.

Astuce : pensez à **optimiser** vos vignettes (webp, tailles raisonnables) pour garder le menu fluide.

---

## ⬆️ Variante top (SelectCustomTop)

- Identique à **SelectCustom**, mais le menu s’ouvre **vers le haut** pour éviter le overflow lorsqu’on est proche du bas de la page.  
- Aucune config supplémentaire, c’est un **rendu différent**.

---

## 🔗 Intégration dans un formulaire

- Liez **`value`** au champ attendu par votre backend (ex. `brand_id`).  
- Liez **`selected_object`** à un champ objet si vous souhaitez **pré-remplir** d’autres entrées du formulaire (ex. `espace.image = selected_object.visual_url`).

**Exemple de mapping rapide :**
```js
variables.set("selected_brand", component.value);
variables.set("selected_brand_obj", component.selected_object);
```

---

## ⚙️ Workflows & événements

- **On change (recommandé)** : déclencher un workflow pour mettre à jour des filtres, requêtes, ou un autre composant (ex. filtrer une liste de produits par marque).  
- Vous pouvez également **réinitialiser** le composant en assignant `null` à `default` via une variable bindée.

---

## ✅ Bonnes pratiques

- Utiliser des **ids stables** pour `option.id`.  
- Fournir des **objets d’option riches** pour tirer parti de `selected_object`.  
- Définir `dropdownMaxHeight` pour éviter les menus trop longs.  
- Avec **SelectCustomVisual**, hébergez vos images sur un CDN et compressez‑les.  
- Internationalisation : mappez `label` vers le champ localisé (`name_fr`, `name_en`, …).

---

## 🧪 Exemple minimal (statique)

```js
[
  { id: "rb", label: "RAY-BAN" },
  { id: "ok", label: "OAKLEY" },
  { id: "ds", label: "DIESEL" }
]
```

---

## 🔍 Débogage rapide

- Vérifiez dans l’inspecteur WeWeb les bindings **`value`** et surtout **`selected_object`** : vous devez voir **tout l’objet** choisi.  
- Si rien n’apparaît, inspectez la formule `options` (chemin `collections["..."].data`).  
- Si le label n’est pas celui attendu, vérifiez la prop **`label`** du composant.

---
