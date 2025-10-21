# Explora — Documentation du projet
Version 1.0 – Octobre 2025

> **Explora** est la colonne vertébrale digitale qui relie les métiers du groupe **Ora** (Elba, Piranèse, Mask, Coraux) et leurs clients du **luxe** (L’Oréal, Luxottica, Shiseido, etc.). Pensé avec pragmatisme et exigence, Explora vise à **fluidifier la prise de commande**, **rendre visibles les campagnes et catalogues**, et **accélérer l’exécution** tout en garantissant la traçabilité de bout en bout.

---

## Table des matières
- [1. Avant-propos](#1-avant-propos)
- [2. Vision et objectifs](#2-vision-et-objectifs)
- [3. Portée et publics](#3-portée-et-publics)
- [4. Architecture d’ensemble (aperçu)](#4-architecture-densemble-aperçu)
- [5. Comment naviguer dans cette documentation](#5-comment-naviguer-dans-cette-documentation)
- [6. Philosophie de conception](#6-philosophie-de-conception)
- [7. Crédits et pilotage](#7-crédits-et-pilotage)

---

## 1. Avant-propos

Le groupe Ora intervient sur des projets **PLV** (Publicité sur le Lieu de Vente) exigeants pour des **marques de luxe**. Les équipes travaillent historiquement avec une forte **culture métier** et une organisation **horizontale**. Cette richesse devait trouver son miroir côté digital : **un espace partagé**, simple d’usage, qui aligne **clients, production et installation**.

Explora naît de ce besoin de **réunir** sans brusquer, d’**outiller** sans complexifier. C’est un **portail client** et un **poste de pilotage interne** : un même socle pour **prendre commande**, **gérer des catalogues**, **orchestrer des campagnes** et **suivre l’avancement**.

## 2. Vision et objectifs

- **Fluidité** : un seul point d’entrée pour créer/dupliquer des projets, choisir un **retailer**, filtrer un **catalogue**, configurer **produits/options/livraison** et obtenir un **prix** fiable.
- **Visibilité** : des **catalogues personnalisés par client/retailer/marque**, des **campagnes** pilotées par période, une **matrice tarifaire** claire.
- **Confiance** : des droits finement gérés (clients, commerciaux terrain, admins), une **authentification Xano** et une traçabilité **Airtable** des statuts de commande.
- **Ouverture** : composants **WeWeb** sur-mesure, **intégrations** (Brandfolder, SendGrid, Sage), et évolutivité par **API**.

## 3. Portée et publics

Explora s’adresse à :
- **Preneurs de commande** (clients finaux, commerciaux terrain Optique).
- **Administrateurs clients** (ex. Luxottica) : pilotent la visibilité des marques, précommandes et campagnes.
- **Administrateurs internes** (Elba) : création/mise à jour de catalogues, paramétrage de **campagnes**, gestion des prix et référentiels.

Les **interfaces** et **droits** s’adaptent au profil (ex. un client L’Oréal ne voit que ses **marques/retailers** autorisés).

## 4. Architecture d’ensemble (aperçu)

- **WeWeb** : front-end, logique d’UI, composants personnalisés, collections et workflows reliés à **Xano**.
- **Xano** : back-end/API, auth **JWT**, données (projets, catalogues, produits, prix, droits), middleware des intégrations.
- **Airtable** : suivi des **statuts** post-commande et coordination opérationnelle.
- **Brandfolder** : **DAM** des assets (images/visuels PLV).
- **SendGrid** : emails transactionnels.
- **Sage** : intégration **comptable** (pilotée avec la comptabilité Elba).

> Détails complets : voir [technique.md](technique.md).

## 5. Comment naviguer dans cette documentation

- **Fonctionnel** : logique métier, parcours, permissions → [fonctionnel.md](fonctionnel.md)  
- **Organisation** : rôles, entités Ora, partenaires, workflows → [organisation.md](organisation.md)  
- **Technique** : architecture, API, intégrations, composants → [technique.md](technique.md)  
- **Composants WeWeb** :
  - [Catalog](composants/catalog.md) · [Admin Grid](composants/admin-grid.md) · [Gantt](composants/gantt.md) · [SuperButton](composants/superbutton.md) · [CustomSelect](composants/customselect.md)

## 6. Philosophie de conception

- **Clarté d’abord** : des interfaces **contextuelles** par rôle, des champs **pertinents** uniquement, des états **explicites**.
- **Évolutif par design** : composants **modulaires**, endpoints **documentés**, séparation **métier/présentation**.
- **Données fiables** : un **modèle de données** unifié et des **règles de validation** cohérentes.
- **Temps réel raisonnable** : rafraîchissements ciblés (WeWeb/Xano) plutôt que surcharges.

## 7. Crédits et pilotage

- **Sponsor** : François Fillat (Piranèse)  
- **Chef de projet** : Axelle Andrieu (Piranèse)  
- **Exécution & Data** : Benoît Renou (Xano, modèle de données)  
- **Suivi & Coordination** : Marine Cantet (Airtable / suivi projet)  
- **Direction générale** : Thibaut de Malézieux  
- **Comptabilité / Sage** : Stéphane Baillez  
- **Contacts clés** : Aurore Cnudde (Trade), Lydia Almela (L’Oréal), Amélie Vargoz & Cristina Ruivo (Luxottica), Virginie du Boucher (Coraux), Valérie Thébeau (Mask)

---

**Documentation préparée par Florian Harmel.**
