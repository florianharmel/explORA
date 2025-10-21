[↩️ Retour à la technique](../technique.md) · [↩️ README](../README.md)

# Composant — Catalog

## But
Afficher un **catalogue** filtré par **retailer** / **marque**, permettre la **sélection** de produits et d’options, et contribuer au **chiffrage**.

## Entrées (props / data)
- `retailerId` (obligatoire), `brandIds[]`
- `visibility` (droits calculés côté Xano)
- `pricingContext` (options/logistique par défaut)

## Comportement
1. Charge la **liste** de produits : `GET /catalogs?retailer=...&brands=...`
2. Pour chaque ligne, applique les **règles d’options** et affiche le **prix** courant.
3. Émet des **événements** : `onSelect(product, options)`, `onQuoteRequested(lignes)`.

## Intégrations
- **Xano** (catalogs, pricing, permissions)
- **Brandfolder** (visuels)
