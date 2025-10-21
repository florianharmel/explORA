[↩️ Retour au README](README.md)

# Fonctionnel — Logique métier & parcours

## Sommaire
- [1. Types d’utilisateurs](#1-types-dutilisateurs)
- [2. Parcours — Trade](#2-parcours--trade)
- [3. Parcours — Optique](#3-parcours--optique)
- [4. Parcours — Travel Retail](#4-parcours--travel-retail)
- [5. Droits & visibilité](#5-droits--visibilité)
- [6. Règles de pricing](#6-règles-de-pricing)
- [7. Scénarios d’usage](#7-scénarios-dusage)

---

## 1. Types d’utilisateurs
- **Preneurs de commande** : clients finaux (ex. L’Oréal) ou **commerciaux terrain** (Optique).  
- **Administrateurs clients** : configurent **visibilité** des marques/campagnes (ex. Luxottica).  
- **Administrateurs internes (Elba)** : référentiels, catalogues, **campagnes**, prix.

## 2. Parcours — Trade
Entrées possibles :
1. **Nouveau projet** : formulaire (nom, temporalité, **retailer**). Le retailer détermine les **catalogues** disponibles. Choix des **produits**, **options**, **mode de livraison** → **prix** recalculé.
2. **Duplication** : reprise des champs structurants (retailer, produits, options, quantités…) avec possibilité de **renommer** et d’ajuster. Raccourci de productivité.

**Catalogue & matrice de prix** : par **produit** et par **retailer**. Un client (ex. L’Oréal) voit uniquement son réseau autorisé (Galeries Lafayette, Sephora, etc.) avec ses tarifs spécifiques.

## 3. Parcours — Optique
- **Précommandes** : mise en avant par période/marque selon le **plan marketing** (piloté par les admins côté client, ex. Luxottica).
- **Commandes classiques** : segmentation par **genre** (femmes/hommes/mixtes) et **type** (optique/solaire).  
- **Association magasin ↔ preneur** (ISS) : page d’admin dédiée pour lier magasins et commerciaux terrain.

## 4. Parcours — Travel Retail
- Logique proche du Trade, avec contraintes **logistiques** (aéroports/gares) et fenêtres de **déploiement** dédiées.
- Accès par **marques**/zones autorisées uniquement.

## 5. Droits & visibilité
- La **visibilité** des **marques**, **retailers** et **catalogues** dépend du **profil** (client/entité) et des **campagnes** actives.
- Les **administrateurs clients** définissent ce qui est **commandable** selon **période**/**magasin**/**marque**.
- Les **admins Elba** peuvent forcer des **règles globales** et maintenir les **référentiels**.

## 6. Règles de pricing
- Prix **par produit** et **par retailer**, modulés par **options** et **logistique**.
- Possibilité de paliers (quantités), remises contractuelles par **client**.
- Le **prix final** est calculé côté **Xano** (source de vérité), affiché côté WeWeb.

## 7. Scénarios d’usage
- **S1 – Création Trade** : un chef de marque L’Oréal crée un projet Sephora, filtre le catalogue, configure les options, reçoit le chiffrage, génère un récap PDF, envoie pour validation, et suit l’exécution.
- **S2 – Duplication** : duplication d’un projet Galeries Lafayette existant pour une nouvelle période, ajustement des quantités, relance du flux.
- **S3 – Optique terrain** : un commercial associe son ISS au magasin Atol, commande les visuels solaires du mois, avec branding localisé.
