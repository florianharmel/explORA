[↩️ Retour à la technique](../technique.md) · [↩️ README](../README.md)

# Composant — Admin Grid

## But
Permettre un **CRUD complet** (Create/Read/Update/Delete) sur des **référentiels Xano** directement depuis WeWeb.

## Entrées
- `resource` (ex. `products`, `retailers`, `prices`)
- `columns[]` (mapping champs/affichage/format)
- `permissions` (création/édition/suppression)

## Comportement
- Liste paginée (tri/filtre), **édition inline**, création/suppression sécurisées (confirmation).
- **Validation** des champs avant envoi.
- Journalisation des **modifications** critiques.

## Intégrations
- **Xano** endpoints REST (standardisés par ressource).
