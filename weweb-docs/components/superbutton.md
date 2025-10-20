# 🔘 Composant Bouton avec Loader — WeWeb

**Auteur :** Florian Harmel  
**Version :** 1.0
**Date :** Octobre 2025  

---

## 🎯 Objectif

Bouton amélioré avec **loader intégré** et **validation de formulaire**.  
Ce composant est conçu pour remplacer un bouton standard WeWeb, tout en gérant :  
- un indicateur visuel de chargement,  
- et la **validation + soumission automatique** d’un formulaire parent.

---

## 🧩 Fonctionnalités principales

- Texte personnalisable (`title`)  
- Couleur de fond (`background`)  
- État désactivé (`disabled`)  
- Loader intégré, contrôlé via workflow  
- Workflow de **validation de formulaire HTML** (prise en charge des champs `required`)

---

## ⚙️ Paramètres

| Paramètre | Type | Description |
|------------|------|-------------|
| **title** | string | Libellé affiché sur le bouton. |
| **background** | color | Couleur du bouton (ex. _Bleu ORA_). |
| **disabled** | boolean | Active ou désactive le bouton. |

---

## 🌀 Gestion du Loader

Le composant expose une **action personnalisée** `setLoader(enabled: boolean)`  
permettant d’activer ou de désactiver l’animation de chargement.

### Exemple

```js
Bouton.setLoader(true)
// appel API ou traitement
Bouton.setLoader(false)
```

💡 **Astuce :** le loader désactive automatiquement le clic pendant son affichage.

---

## ✅ Workflow « Valider formulaire »

Ce workflow est conçu pour **valider et soumettre le formulaire parent**,  
tout en respectant les contraintes natives des champs (`required`, `pattern`, `type`, etc.).

### Étapes de configuration (dans WeWeb)
1. Ouvre l’onglet **Workflows** du bouton.  
2. Crée un **workflow “On click”**.  
3. Ajoute une **action Custom JavaScript**.  
4. Nom : `Validate Form`.  
5. Colle le code suivant :

```js
const form = document.querySelector("form"); // ou un ID spécifique : document.querySelector("#monFormulaire")
if (form && form.reportValidity()) {
  form.requestSubmit();
}
```

---

### 🧠 Explication du code

| Ligne | Rôle |
|-------|------|
| `document.querySelector("form")` | Sélectionne le formulaire parent (ou un formulaire spécifique via ID). |
| `form.reportValidity()` | Vérifie si tous les champs requis sont valides. Affiche les messages d’erreur natifs du navigateur si besoin. |
| `form.requestSubmit()` | Déclenche l’événement `submit` du formulaire uniquement **si la validation est réussie**. |

⚠️ Si un champ `required` ou invalide est détecté,  
le navigateur **empêche la soumission** et **met en évidence le champ concerné**.

---

## 💡 Bonnes pratiques

- Toujours cibler un **ID précis** de formulaire (`#myForm`) si plusieurs sont présents.  
- Utiliser `reportValidity()` pour bénéficier des validations HTML natives sans dépendances externes.  
- Combiner `setLoader(true)` avant l’envoi, et `setLoader(false)` après la réponse.  
- Utiliser `disabled` pour bloquer des actions tant que le formulaire n’est pas complet.

---

## 🔗 Références

- **WeWeb** : compatible avec les workflows standards et personnalisés  
- **Xano / API** : intégration possible pendant le `submit` du formulaire  
- **Actions supportées** : `click`, `setLoader`, `validateForm`

---

## ✅ Résumé

| Élément | Description |
|----------|--------------|
| **Nom du composant** | Bouton avec Loader |
| **Type** | Bouton interactif + validation |
| **Actions personnalisées** | `setLoader(enabled: boolean)` |
| **Workflow inclus** | `Validate Form` (JS) |
| **Comportement clé** | Vérifie les champs `required` avant `submit` |
| **Utilisation typique** | Bouton de validation ou d’envoi de formulaire |

---
