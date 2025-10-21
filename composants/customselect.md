[↩️ Retour à la technique](../technique.md) · [↩️ README](../README.md)

# Composant — CustomSelect

## But
Sélecteur **avancé** (recherche, lazy-load, multi-sélection) respectant les **droits** et la **visibilité**.

## Entrées
- `resource` (ex. `brands`, `retailers`), `searchable` (bool), `multiple` (bool)
- `filters` (limitation par droits), `pageSize`

## Comportement
- Requête **lazy** `GET /{resource}?q=...&page=...`
- Gère les **chips** de sélection multi, clavier/ARIA, et placeholder contextualisé.
