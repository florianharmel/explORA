# 🧮 Composant Admin Grid

## 🎯 Présentation
Tableau de données administratives avec tri, filtres et actions.

## ⚙️ Propriétés
| Nom | Type | Description | Exemple |
|------|------|-------------|----------|
| items | Array | Données à afficher | `[ { name:'Projet 1' } ]` |
| columns | Array | Colonnes du tableau | `[ 'Nom', 'Statut' ]` |

## 🔁 Événements
| Nom | Payload | Description |
|------|----------|-------------|
| grid:select | `{ item }` | Élément sélectionné |
| grid:action | `{ item, action }` | Action sur élément |

📄 Version : 1.0.0
✍️ Auteur : Florian Harmel