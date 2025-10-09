# 🗓️ Composant Gantt

## 🎯 Présentation
Diagramme de Gantt pour visualiser et modifier les tâches d’un projet.

## ⚙️ Propriétés
| Nom | Type | Description | Exemple |
|------|------|-------------|----------|
| tasks | Array | Liste des tâches | `[ { id:1, name:'Phase 1' } ]` |
| editable | Boolean | Permet l’édition | `true` |

## 🔁 Événements
| Nom | Payload | Description |
|------|----------|-------------|
| gantt:updated | `{ tasks }` | Lorsqu’une tâche est modifiée |
| gantt:select | `{ id }` | Lorsqu’une tâche est sélectionnée |

📄 Version : 1.0.0
✍️ Auteur : Florian Harmel