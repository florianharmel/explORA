[↩️ Retour au README](README.md)

# Technique — Architecture, données & composants

## Sommaire
- [1. Stack & principes](#1-stack--principes)
- [2. Architecture logique](#2-architecture-logique)
- [3. Données & API Xano](#3-données--api-xano)
- [4. Intégrations](#4-intégrations)
- [5. Authentification & sécurité](#5-authentification--sécurité)
- [6. Composants WeWeb](#6-composants-weweb)
- [7. Bonnes pratiques & maintenance](#7-bonnes-pratiques--maintenance)

---

## 1. Stack & principes
- **WeWeb** : pages, collections, workflows, **composants custom**. Tous les appels sont faits vers **Xano**.
- **Xano** : API REST, **auth JWT**, modèle de données (projets, catalogues, produits, prix, droits).
- **Airtable** : suivi des **statuts**.
- **Brandfolder** : **DAM**.
- **SendGrid** : notifications email.
- **Sage** : export/synchro **comptable**.

## 2. Architecture logique
```
[Client Web (WeWeb)] --REST--> [Xano (API + Data + Rules)] --(integrations)--> Brandfolder / SendGrid / Sage
                                               |
                                               +--> Airtable (sync statuts/ops)
```
- **WeWeb** : UI, validation de base, orchestration simple via **workflows**.
- **Xano** : logique métier (prix, droits, filtrage), **source de vérité** des données.

## 3. Données & API Xano
**Objets** (exemples) :
- **users** (rôles, permissions, marque/retailer scope)
- **projects** (client, retailer, période, lignes)
- **catalogs / products / prices** (par retailer, options, paliers)
- **campaigns** (fenêtres temporelles, marque, éligibilité)

**Endpoints** (exemples génériques) :
- `POST /auth/login` → JWT
- `GET /catalogs?retailer=...&brand=...`
- `POST /projects` · `POST /projects/{id}/duplicate`
- `POST /pricing/quote` (produits + options + quantités → prix)
- `GET /permissions/me` (visibilité marques/retailers/catalogues)

> Les schémas exacts sont documentés dans Xano (Swagger).

## 4. Intégrations
- **Brandfolder** : récupération d’assets par SKU/brand.
- **SendGrid** : e-mails transactionnels (confirmation, recap PDF).
- **Sage** : mapping articles/clients/TVA, export validé par compta (Stéphane Bayez).
- **PDF** : génération récapitulatif commande.

## 5. Authentification & sécurité
- **JWT** côté Xano, token stocké côté WeWeb de manière sécurisée.
- Contrôles de **visibilité** (marques/retailers) renvoyés par l’API et respectés côté UI.
- Journalisation des actions critiques (création/duplication/validation).

## 6. Composants WeWeb
- **Catalog** : filtrage par retailer/marque, affichage produits, options, calculs liés. → [Voir la fiche](composants/catalog.md)
- **Admin Grid** : CRUD complet sur tables Xano (référentiels). → [Voir la fiche](composants/admin-grid.md)
- **Gantt** : visualisation des projets & jalons. → [Voir la fiche](composants/gantt.md)
- **SuperButton** : bouton enrichi (états, loaders, droits). → [Voir la fiche](composants/superbutton.md)
- **CustomSelect** : select avancé (recherche, lazy load, droits). → [Voir la fiche](composants/customselect.md)

## 7. Bonnes pratiques & maintenance
- **Séparer** les responsabilités : UI (WeWeb) / métier (Xano).
- **Documenter** les endpoints et payloads.
- **Versionner** la config WeWeb (noms de collections, workflows).
- **Tests par scénario** (Trade, Optique, Travel).
