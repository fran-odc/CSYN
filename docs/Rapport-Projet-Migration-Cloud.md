## Rapport de Modernisation : Centralisation et Sécurisation de la Gestion des Bénévoles

# 1. Contexte et Objectifs de la Modernisation

En tant que responsable en Transformation Digitale, j'ai procédé à l'audit du système de gestion des bénévoles actuel au CSYN.
Le constat est celui d'un centre reposant sur un héritage de gestion fragmentée et locale, où l'information est silotée dans des fichiers disparates.
Cette architecture "artisanale" freine l'agilité opérationnelle et présente des vecteurs de vulnérabilité critiques pour la donnée.

Le présent schéma directeur vise à opérer une transition vers un Référentiel de Données Unique (Single Source of Truth).

La **stratégie** repose sur:
- la centralisation des flux au sein de l'écosystème Google Workspace pour la production,
- doublée d'une couche de gouvernance et
- de documentation technique hébergée sur GitHub.

L'**objectif** est de passer d'un stockage passif à un actif informationnel sécurisé, versionné et pilotable.

# 2. Audit du Système Existant : Fragmentation et Inconsistance

# 2.1. Inventaire des supports de données (Silos informationnels)

L'audit a identifié une dispersion des données sur des supports non synchronisés, mêlant formats structurés (Excel) et semi-structurés (Word) :

- **Actifs Tableurs** : Missions bénévoles.xls, liste benevole adresse semi complete.xlsx, tabl benevole.xlsx.
- **Actifs Textuels** : Bénévolat oui mais pourquoi.docx, Fiche bénévoles (fichier sans extension), Lieux ressources conseils contacts.docx, tableau propositions.docx.

# 2.2. Analyse de l'inconsistance et des écarts de structure

La comparaison des schémas de données entre les différents fichiers révèle des gaps structurels majeurs qui empêchent toute vision consolidée.

| **Champ de donnée** | **Fichier de base** | **Tableau de bord consolidé** | **Fiche d'entretien** |
|---------------------|---------------------|-------------------------------|-----------------------|
| **Identité (Données génériques)** | Présent | Présent | Présent |
| **Contact (Mail/Tel)** | Présent | Présent | Présent |
| **RENCONTRE (Date/Statut)** | Absent | Présent | Absent |
| **Statut (Retraité/Sénior Actif)** | Absent | Présent | Absent |
| **Genre (M/F)** | Absent | Présent | Présent |
| **Activités au CSYN / Missions** | Absent | Présent | Absent |
| **Autres activités au CSYN** | Absent | Présent | Absent |
| **Disponibilités (Matin/AM/Soir)** | Absent | Présent | Présent |


# 2.3. Identification des risques et vecteurs de vulnérabilité

- **Qualité de donnée dégradée** :
  + L'analyse des sources (ex: 11.58.37) montre une absence de normalisation.
  + Les numéros de téléphone utilisent des délimiteurs incohérents (07.55... vs 01 47 ... vs 06;22;...).
  + La toponymie est instable (Asnières sur seine vs Asnieres sur Seine vs Asnieres-sur-seine).
- **Effet "Silo Informationnel"** :
  + Des données critiques comme la profession ou les motivations (issues de Bénévolat oui mais pourquoi.docx) sont piégées dans des fichiers textuels, rendant tout filtrage ou reporting impossible.
- **Risque d'intégrité** :
  + Le stockage local ne permet aucun versionnage, exposant le système à des écrasements accidentels ou à des pertes sèches en cas de défaillance matérielle.

# 3. La Solution Proposée : Centralisation et Agrégation

# 3.1. Stratégie d'agrégation et transformation

Le projet prévoit une phase de transformation (ETL) visant à convertir les données non structurées des fiches Word 2019/2020 en métadonnées exploitables. Par exemple, les textes libres sur la motivation seront traduits en "Tags de motivation" dans la base de données centrale.

# 3.2. Architecture Technique

La solution repose sur une synergie entre deux plateformes leaders :

- **Google Workspace (Environnement de Production)** : Centralisation de la base de données unique pour une collaboration multi-utilisateurs en temps réel.
- **GitHub (Dépôt fran-odc/CSYN)** : Espace d'archivage et de documentation du projet. Le dépôt **ne contient pas** les données nominatives elles-mêmes, mais agit comme une couche de transparence. L'image migration-dashboard.png (référence commit d172c1e) sert de preuve visuelle de la migration effectuée, garantissant que le processus de centralisation est documenté, versionné et vérifiable par le CSYN.

# 3.3. Standardisation du Référentiel (SSOT)

La structure cible harmonise les besoins administratifs et opérationnels identifiés dans les sources :

1. Bloc Administratif : Identité, Genre, Contact (format normalisé), Adresse (référentiel unique).
2. Bloc Profil : Profession, Expériences, Statut (Actif/Retraité).
3. Bloc Opérationnel :
  * Matrice des disponibilités (Lundi au Samedi / Matin, Après-midi, Soirée).
  * Contraintes d'exclusion : Champ "Jamais disponible" pour optimiser le recrutement.
  * Suivi : Date de rencontre, missions souhaitées et activités actuelles au CSYN.

# 4. Sécurité, Contrôle des Accès et Gouvernance

# 4.1. Matrice comparative de sécurité

Le passage d'une gestion locale à une architecture Cloud renforce drastiquement la posture de sécurité :

| **Aspect** | **Système Existant (Fichiers Locaux)** | **Nouveau Système (Cloud & Doc GitHub)** | 
|------------|----------------------------------------|------------------------------------------|
| **Gouvernance** | Nulle : Multiples copies de fichiers Excel (Missions, liste benevole) et Word stockées localement | Centralisée : Une source de vérité unique ("Single Source of Truth") via une base de données no-code agrégée |
| **Contrôle d'accès** | Faible : Risque de perte ou de fuite via des copies sur clés USB ou envois par mail sans traçabilité | Sécurisé : Authentification forte (IAM) et accès granulaires gérés via Google Workspace & GitHub |
| **Traçabilité** | Impossible : Aucune visibilité sur qui a modifié quoi dans les fichiers tabl benevole.xlsx | Auditable : Logs d'activité et audit trail complet; historique immuable des étapes de migration documenté |
| **Cohérence** | Inconsistante : Données fragmentées entre les fiches d'inscription papier et divers fichiers numériques | Unifiée : Consolidation et nettoyage des données dans un tableau de bord de suivi structuré |

# 4.2. Traçabilité et Conformité

L'utilisation de GitHub permet une "Infrastructure as Code" pour la documentation : chaque modification de la structure de données est tracée par un commit (ex: mise à jour du dashboard de migration effectuée il y a "X" minutes selon les logs du dépôt). Cette rigueur garantit l'élimination des doublons et la confidentialité des informations sensibles des bénévoles.

# 5. Impacts Attendus et Conclusion

La mise en œuvre de cette modernisation garantit :

- **Intégrité Totale** : Suppression des erreurs de saisie grâce à la standardisation des masques de saisie (Google Forms/Sheets).
- **Efficacité Opérationnelle** : Réduction du temps de recherche de profils (ex: filtrage instantané sur le champ "Matin" et la compétence "Soutien Scolaire").
- **Pérennité de la Mémoire Organisationnelle** : Les données d'entretiens ne sont plus des documents isolés mais une base vivante et interrogeable.

En conclusion, en adoptant Google Workspace et GitHub, le CSYN ne se contente pas de "ranger des fichiers" ; il se dote d'un véritable système d'information capable de soutenir sa croissance et de sécuriser son capital humain.
