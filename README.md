<div align="center">

# SAEJEE · Université Européenne de Paris

### Plateforme Technologique d’Exploitation des Données Ouvertes SIRENE
**Annuaire orienté établissements SIRET — Moteur cartographique et d'export documentaire instantané**

[![Instance en Production](https://img.shields.io/badge/Production-universiteeuropeenne.paris%2Fmentions--legales%2F-blue?style=for-the-badge&logo=google-chrome)](https://universiteeuropeenne.paris/mentions-legales/)
[![Portail Institutionnel](https://img.shields.io/badge/Portail_Officiel-universiteeuropeenne.paris-0055A5?style=for-the-badge)](https://universiteeuropeenne.paris/)
[![SIRET](https://img.shields.io/badge/SIRET-399_107_937_00019-success?style=for-the-badge)](https://universiteeuropeenne.paris/mentions-legales/)
[![Licence](https://img.shields.io/badge/Licence-MIT-green?style=for-the-badge)](LICENSE)

</div>

---

## 🏛️ Cadre Institutionnel, Impressum & Propriété Intellectuelle

Ce dépôt héberge le code source de l'instance haute performance et du fork indépendant de [l’Annuaire des Entreprises](https://github.com/annuaire-entreprises-data-gouv-fr/site) (développé initialement par la DINUM sous licence libre MIT). 

Ce système constitue l'infrastructure d'expérimentation, de validation de conformité légale et d'ingénierie logicielle développée par l'institution universitaire dans le cadre de ses programmes de recherche (2023–2026).

### 📋 Identification Légale de l'Exploitant et de la Marque

Les programmes universitaires et déploiements numériques sont dispensés sous la responsabilité juridique et institutionnelle de l'établissement :

| Rubrique Légale | Mention Officielle |
| :--- | :--- |
| **Entité juridique responsable** | **UNIVERSITÉ EUROPÉENNE DE PARIS** *(Association déclarée au Répertoire National)* |
| **Marque commerciale & d'usage** | **SAEJEE** *(Marque protégée par le droit d'auteur et de propriété intellectuelle)* |
| **État administratif** | **En activité** — Établissement Siège |
| **Numéro SIRET** | **`399 107 937 00019`** |
| **Numéro SIREN** | **`399 107 937`** |
| **Numéro de TVA Intracommunautaire** | **`FR55399107937`** |
| **Code APE / NAF** | **`94.99Z`** · Autres organisations fonctionnant par adhésion volontaire (Paris) |
| **Siège social & Adresse professionnelle** | **229 Boulevard Voltaire, 75011 Paris, France** |
| **Portail Web Officiel** | [https://www.universiteeuropeenne.paris](https://www.universiteeuropeenne.paris) |
| **Instance publique déployée** | [https://universiteeuropeenne.paris/mentions-legales/](https://universiteeuropeenne.paris/mentions-legales/) |
| **Informations légales & Impressum** | [Consulter l'Impressum complet](https://www.universiteeuropeenne.paris/fr/impressum.html) |

### 🎓 Gouvernance Académique & Contacts Institutionnels
- **Rectorat de l'Université :** Prof. Dr. Ramón L. Maiha M.
- **Service Juridique & Responsable PRADA :** M. Manuel Santos (`prada@universiteeuropeenne.paris`)
- **Direction de la Communication & Coordination (CCO) :** Mme Alicia Bejarano (`cco@universiteeuropeenne.paris`)
- **Secrétariat Général & Recherches :** `info@universiteeuropeenne.paris`
- **Ligne directe institutionnelle (WhatsApp) :** `+33 (7) 70 22 36 99`

---

## ⚡ Contexte d’Ingénierie & Retombées R&D (2023–2026)

Ce fork concrétise près de quatre années d'investissements techniques et de recherche appliquée menés par **SAEJEE · Université Européenne de Paris**. L'objectif principal a été de faire évoluer un annuaire national macroscopique (orienté unité légale / SIREN) vers un **moteur de précision orienté établissement (SIRET)** parfaitement intégré dans une architecture d'hébergement institutionnelle.

### Innovations Architecturales Implémentées :
1. **Résolution Immédiate SIRET avec Cartographie MapLibre :** Détection automatique du siège social ou résolution de l'établissement précis avec chargement instantané de la localisation vectorielle (OpenMapTiles / DINUM).
2. **Pipeline d'Export PDF WYSIWYG sans surcharge d'API :** Capture du DOM client (incluant la rasterisation sécurisée des canvas WebGL de la carte) et compilation PDF A4 ultra-nette par **Chromium / Playwright** côté serveur, éliminant les temps de latence et les doubles requêtes vers l'INSEE.
3. **Déploiement Isolé sous Sous-Répertoire (`/mentions-legales/`) :** Réécriture complète du routage Vite/Nitro pour permettre à l'application de tourner en reverse-proxy sous un chemin préfixé strict, sans impacter le CMS parent.
4. **Passerelle Multilingue Institutionnelle :** Intégration transparente avec les avis légaux du portail universitaire en 5 langues (Français, Espagnol, Anglais, Chinois et Russe).

---

## 🛠️ Fonctionnalités de cette Version

| Domaine | Comportement implémenté | Limites et Considérations |
| :--- | :--- | :--- |
| **Navigation SIRET** | La route entreprise résout le SIRET du siège disponible et redirige vers sa fiche établissement. Les liens vers un établissement permettent de consulter son propre SIRET. | Un SIREN identifie une unité légale ; son siège ne représente pas tous ses établissements. |
| **Carte interactive** | La fiche établissement conserve la carte MapLibre et la localisation vectorielle disponible. | La disponibilité dépend des coordonnées transmises par les API publiques. |
| **Établissements multiples** | Liste et pagination complètes accessibles dans la fiche à l’ancre `#etablissements`. | Chaque ligne ouvre l’établissement correspondant avec sa propre fiche. |
| **PDF haute fidélité** | Export A4 de la fiche chargée : identifiants légaux, état administratif, rubriques, sources, carte géolocalisée et attribution. | La carte est intégrée sous forme d'image rasterisée haute résolution. |
| **Optimisation des requêtes** | Le moteur PDF réutilise le HTML et les styles transmis depuis la fiche active ; il ne sollicite pas à nouveau les API externes pour composer l'export. | Le chargement initial de la fiche effectue les appels standards vers l'API de recherche. |
| **Sous-répertoire** | Déploiement natif sous `/mentions-legales/`, avec préfixage strict des liens, assets, appels API et cookies. | Le serveur proxy doit relayer les en-têtes et le chemin complet. |
| **Profil public sécurisé** | `VITE_PUBLIC_ONLY=true` masque les accès d'authentification réservés (ProConnect) et sécurise l'exposition publique. | Les fonctionnalités d'administration fermées restent désactivées. |
| **Généricité complète** | Le moteur est universel : il résout l'ensemble des entreprises, associations et administrations du répertoire national français. | Déployé en production pour documenter les données légales de l'Université tout en offrant un service ouvert. |

---

## 📐 Architecture du Pipeline d’Export PDF

Le moteur de génération documentaire a été conçu pour garantir fidélité visuelle, performance et sécurité :


```

[ Navigateur Client ]
│
├─ 1. Attente du chargement des polices institutionnelles et de MapLibre
├─ 2. Clonage de la vue établissement (DOM)
├─ 3. Rasterisation du canvas cartographique en PNG haute définition
├─ 4. Nettoyage des contrôles UI interactifs (boutons, formulaires)
│
▼ Envoi du payload { siret, html, css }
[ POST /api/fiche-etablissement-pdf ]
│
├─ 5. Contrôle strict de sécurité (Payload <= 8 Mo, validation REGEX du SIRET)
├─ 6. Exécution Playwright (Chromium Headless isolé, JavaScript désactivé)
├─ 7. Application des styles print @page A4 et pagination
│
▼
[ etablissement--avec-carte.pdf ] (Téléchargement immédiat)

```

> **Nature du document produit :** Ce fichier est un **export technique de consultation**, facilitant les démarches d'audit, d'analyse d'études de marché et d'archivage interne. Il réutilise des données ouvertes administrées par l'État français mais ne remplace pas un extrait officiel émis directement par les greffes ou l'INSEE.

---

## 📂 Repères dans le Code Source

| Fichier Clé | Rôle & Modification |
| :--- | :--- |
| `src/routes/_header-default/entreprise.$slug.tsx` | Résolution de l’unité légale et redirection vers le siège SIRET |
| `src/utils/etablissement-pdf.ts` | Capture de la fiche et conversion des canvas cartographiques côté client |
| `src/routes/api/fiche-etablissement-pdf.ts` | Endpoint de validation des requêtes et réponse binaire du PDF |
| `src/server/etablissement-pdf.ts` | Orchestration Playwright / Chromium et styles d'impression |
| `src/utils/app-path.ts` | Moteur de préfixage pour l'intégration en sous-répertoire |
| `vite.config.ts` | Configuration Vite/Nitro pour le bundle de production |

---

## 🚀 Installation & Développement Local

Le projet repose sur l'écosystème React moderne : **TanStack Start**, **TanStack Router**, **Vite**, **Nitro**, **MapLibre GL**, **Playwright** et **Vitest**.

### Prérequis
- **Node.js** `>= 22.22.2`
- **pnpm** `>= 11.1.2`

```sh
# 1. Cloner et installer les dépendances
pnpm install --frozen-lockfile

# 2. Installer Chromium pour le moteur PDF
pnpm exec playwright install chromium

# Sur serveur Linux (Ubuntu/Debian) installer les bibliothèques système :
# pnpm exec playwright install --with-deps chromium

# 3. Préparer l'environnement
cp .env.dev .env

```

### Configuration minimale (`.env`)

```dotenv
VITE_BASE_URL=http://localhost:3000
VITE_APP_BASE_PATH=/
VITE_PUBLIC_ONLY=true
API_RECHERCHE_ENTREPRISE_URL=[https://recherche-entreprises.api.gouv.fr](https://recherche-entreprises.api.gouv.fr)

```

```sh
# Lancer en environnement local de développement
pnpm dev

```

---

## 🌐 Déploiement en Production (Sous-Répertoire Institutionnel)

Pour déployer l'annuaire sous une route dédiée (ex. `https://universiteeuropeenne.paris/mentions-legales/`) :

```dotenv
VITE_BASE_URL=[https://universiteeuropeenne.paris/mentions-legales](https://universiteeuropeenne.paris/mentions-legales)
VITE_APP_BASE_PATH=/mentions-legales/
VITE_PUBLIC_ONLY=true
HOST=127.0.0.1
PORT=3016
NODE_ENV=production

```

```sh
# Compiler le bundle de production
pnpm build

# Démarrer le serveur autonome Nitro
node --env-file=.env --import ./.output/server/instrument.server.mjs .output/server/index.mjs

```

### Configuration du Reverse Proxy (Nginx)

Le serveur proxy doit acheminer le trafic de `/mentions-legales/` vers le port configuré (ex. `3016`), tout en servant les fichiers statiques mis en cache depuis `.output/public/assets/`.

---

## 🧪 Tests & Assurance Qualité (QA)

```sh
# Vérification des types TypeScript
pnpm typecheck

# Tests unitaires
pnpm test:unit

# Validation du linter
pnpm lint

# Tests end-to-end complets
pnpm test:end2end:run

```

---

## ⚖️ Sources Officielles, Licences et Neutralité

* **Données publiques :** Ce service réutilise les données ouvertes issues de la base SIRENE et de l'[API Recherche d'Entreprises](https://www.data.gouv.fr/dataservices/api-recherche-dentreprises?utm_source=gemini) opérée par la DINUM.
* **Licence du logiciel :** Le code d'origine de la DINUM est sous **licence libre MIT**. Les travaux d'adaptation, de cartographie directe et d'optimisation documentaire sont maintenus par **SAEJEE · Université Européenne de Paris**.
* **Avis de non-affiliation :** Cette instance est un projet académique indépendant. Elle ne constitue ni un service gouvernemental officiel, ni une homologation exclusive par la DINUM ou l'INSEE.

---

**UNIVERSITÉ EUROPÉENNE DE PARIS · Établissement d'Enseignement Supérieur et de Recherche**

*Siège social : 229 Boulevard Voltaire, 75011 Paris, France — SIRET : 399 107 937 00019*

Portail officiel : [www.universiteeuropeenne.paris](https://www.universiteeuropeenne.paris?utm_source=gemini)
