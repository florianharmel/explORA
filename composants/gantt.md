[↩️ Retour à la technique](../technique.md) · [↩️ README](../README.md)

# Composant — Gantt

## But
Visualiser l’**avancement** des projets, jalons et dépendances.

## Entrées
- `projects[]` (id, nom, période)
- `milestones[]` (dates, états)
- `filters` (client, retailer, période)

## Comportement
- Affichage **timeline**, zoom par période, **sur-couche** d’états (à valider/en cours/terminé).
- Clic sur une barre → ouvre le **détail** projet.

## Intégrations
- **Xano** (`GET /projects?filters=...`)
- (Optionnel) export **PNG/PDF** du diagramme.
