[↩️ Retour à la technique](../technique.md) · [↩️ README](../README.md)

# Composant — SuperButton

## But
Bouton **amélioré** gérant les **états** (loading, disabled), les **droits** et les **confirmations**.

## Entrées
- `label`, `icon`, `variant`
- `action` (workflow / appel Xano)
- `requiresPermission` (string)
- `confirmMessage` (optionnel)

## Comportement
- Vérifie les **droits** avant exécution.
- Affiche un **loader** pendant l’action.
- Émet `onSuccess(payload)` / `onError(err)`.
