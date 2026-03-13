# Projets au Centre Socioculturel Yannick Noah (CSYN)

[![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Base44](https://img.shields.io/badge/Base44-IA-blueviolet.svg)](https://base44.com)
[![Google Workspace](https://img.shields.io/badge/Google%20Workspace-4285F4.svg?style=for-the-badge&logo=google-workspace&logoColor=white)](https://workspace.google.com/)

# C'est quoi le CSYN ?
Dans une optique de développement social local, le CSYN a pour finalité de répondre aux besoins exprimés par les habitants d’Asnières-sur-Seine (92) à travers des projets innovants et pertinents.

# 1. Projet Migration Cloud (Direction)

[📄 Rapport de Modernisation](docs/Rapport-Projet-Migration-Cloud.md)

# 1.1. Problèmes

- Incohérence de la base de données (sources multiples).
- Gestion locale sans management des accès.

[🔄 Migration]()

# 1.2. Solutions apportées

+ Consolidation et agrégation de toutes les ressources dans une base de données via Google Workspace.
+ Mise en place d’une gestion des droits d’accès pour la direction.

**Impact :** Centralisation sécurisée des données, accès contrôlé et réduction des erreurs liées aux multiples fichiers.

[📊 Base de données](images/migration-dashboard.png)

# 2. Projet App Web (Accueil)

# 2.1. Problèmes

- Demandes urgentes de statistiques par differents parties prennantes.
- Équipe débordée par les tâches quotidiennes et les questionnaires.

# 2.2. Solutions apportées

+ Développement d'une app web full-stack avec Base44 + React: dashboard interactif pour suivi quotidien, déploiement instantané, backend serverless inclus, authentification native, zero-config.
+ Base de données auto-gérée: entité `StatistiquesQuotidiennes` avec 13 champs (date, métriques, notes), CRUD via `@base44/sdk`.
+ Visualisations avancées: graphiques Recharts (barres mensuelles, lignes annuelles), filtres mois/année, historique récent.
+ 3 versions itératives: V1 (MVP), V2 (stats + graphiques), V3 (layout responsive, premiers retours).
+ Interface direction: sidebar navigation, design moderne (shadcn/ui, Tailwind, Framer Motion), déploiement instantané Base44.
+ Comptoirs incrémentables temps réel

**Impact :** 
- **Gain de temps** : production rapports quotidiens réduite (automatisation saisie + visualisations).
- **Adoption 100% direction** : accès 24/7 aux KPIs critiques, fin des emails urgents.
- **Fiabilité données** : centralisation unique vs sources multiples, audit trail complet.
- **Scalabilité** : supporte utilisateurs simultanés, évolution facile (nouveaux RDV, métriques).

## Technologies & Outils
| **Stack Technique** | **Détails** |
|---------------------|-------------|
| **Frontend** | React 18, TypeScript, TailwindCSS, shadcn/ui |
| **État & Requêtes** | React Query (Tanstack), Framer Motion (animations) |
| **Visualisations** | Recharts (barres/lignes), date-fns (français) |
| **Base44** | `@base44/sdk`, entité `StatistiquesQuotidiennes` (13 champs) |
| **UI/UX** | Lucide React icons, Layout responsive (mobile-first) |
| **Gestion Données** | CRUD auto (create/update), filtres temps réel (mois/année) |

## Contact
LinkedIn : [Francesca Oliveira](https://www.linkedin.com/in/oliveirafrancesca/)

Email : fran.odc@pm.me

*Dernière mise à jour : Mars 2026*
