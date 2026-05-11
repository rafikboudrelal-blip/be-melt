# Note de cadrage — BE MELT

**Boussole Emploi Lys-Tourcoing transfrontalière**

---

| **Champ** | **Valeur** |
|---|---|
| Structure | MELT — Mission Emploi Lys-Tourcoing |
| Document | Note de cadrage V1 — BE MELT |
| Version | V1 — socle de présentation direction |
| Date | Mai 2026 |
| Statut | Document de travail — projet en cours de prototypage |
| Articulation | Projet sœur d'ARIA (Note-cadre V2.1) — outil complémentaire de visualisation territoriale |

---

## 1. Pourquoi BE MELT

Les jeunes accompagnés par la MELT cherchent un emploi sur un territoire fragmenté : 12 communes MELT, 95 communes MEL, et un bassin transfrontalier belge largement sous-exploité par les conseillers et publics français. Aujourd'hui, accéder à une vue territoriale unifiée des offres demande de naviguer entre francetravail.fr, leforem.be, vdab.be, actiris.brussels — sans compter les jobboards privés. Aucun outil ne propose une lecture intégrée du marché de l'emploi à l'échelle pertinente pour MELT.

BE MELT comble ce vide. C'est une Progressive Web App (PWA) installable sur mobile et desktop, qui agrège en temps réel les offres d'emploi des données publiques officielles France Travail et Le Forem, restituées en trois niveaux territoriaux emboîtés. L'outil intègre nativement les contraintes réelles du public ML : mobilité, permis, transports en commun, distance domicile-emploi.

## 2. Positionnement vis-à-vis d'ARIA

BE MELT et ARIA forment un écosystème cohérent et complémentaire, sans recouvrement fonctionnel.

| **ARIA** | **BE MELT** |
|---|---|
| Couche de connaissance organisationnelle interne MELT | Couche de visualisation territoriale de données publiques externes |
| Ressources, partenaires, référents, dispositifs MELT | Offres d'emploi, événements, agences France Travail |
| Public : professionnels MELT | Public : jeunes accompagnés, professionnels MELT, grand public |
| Donnée structurée en interne | Donnée publique agrégée (France Travail, Le Forem) |
| Outil d'aide à l'entretien et à la décision métier | Outil d'aide à la recherche d'emploi et au pilotage territorial |

**Articulation opérationnelle** : depuis ARIA, dans la Boussole solutions, un lien sortant unique pointe vers BE MELT pour la consultation des offres territoriales. BE MELT n'a pas de lien vers ARIA (BE MELT est destiné aussi au grand public).

## 3. Trois niveaux territoriaux

BE MELT structure la consultation des offres autour de trois cercles géographiques alignés sur des cadres institutionnels existants.

### Niveau 1 — Territoire MELT (12 communes)

Bondues, Bousbecque, Comines, Deûlémont, Halluin, Linselles, Mouvaux, Neuville-en-Ferrain, Roncq, Tourcoing, Warneton, Wervicq-Sud.

### Niveau 2 — Métropole Européenne de Lille (95 communes)

Périmètre administratif de l'EPCI Métropole Européenne de Lille, financeur métropolitain.

### Niveau 3 — Eurométropole Lille-Kortrijk-Tournai

Périmètre du GECT créé en 2008, qui constitue le cadre officiel de la coopération transfrontalière pour la MEL. Couvre :
- En France : MEL (95 communes)
- En Belgique francophone : arrondissement de Mouscron (IEG), arrondissements de Tournai et Ath (IDETA), communes de Lessines, Silly, Enghien
- En Belgique néerlandophone : arrondissement de Kortrijk (LEIEDAL), arrondissements d'Ieper, Roeselare et Tielt (WVI)

Soit environ 157 communes pour 2,1 millions d'habitants — la plus importante métropole transfrontalière d'Europe.

**Note stratégique** : l'alignement BE MELT sur le périmètre Eurométropole permet à MELT de matérialiser concrètement la dimension transfrontalière que sa propre communication institutionnelle revendique, et de parler le langage de son financeur MEL en matière de compétence métropolitaine.

## 4. Sources de données

BE MELT consomme exclusivement des données publiques officielles, sous licences ouvertes.

| Source | Périmètre | Format | Licence |
|---|---|---|---|
| API France Travail Offres d'emploi v2 | France | REST/JSON, OAuth2 | Licence dédiée France Travail (gratuite) |
| API France Travail Référentiel agences | France | REST/JSON, OAuth2 | Licence dédiée France Travail (gratuite) |
| API France Travail Événements | France | REST/JSON, OAuth2 | Licence dédiée France Travail (gratuite) |
| Le Forem Open Data | Wallonie + offres VDAB traduites + Actiris | API ODSO | Licence Ouverte ODbL |
| GTFS Ilévia (MEL) | Transports MEL | GTFS standard | Licence Ouverte v2 MEL |

Aucune donnée à caractère personnel n'est traitée. Aucun compte utilisateur n'est requis. Les préférences de l'utilisateur (commune de résidence, mode de transport) sont stockées localement dans le navigateur via LocalStorage, sans transmission serveur. Conformité RGPD assurée par minimisation.

## 5. Fonctionnalités V1

### Consultation des offres

- Vue chronologique des offres actives par niveau territorial sélectionné
- Détail offre : titre, employeur, lieu, contrat, salaire si renseigné, lien direct vers la source officielle pour candidater

### Filtres

- Commune (mono ou multi-sélection)
- Type de contrat (CDI, CDD, intérim, alternance, stage)
- Niveau d'expérience requis
- Métier (par grande famille ROME, 14 domaines)
- Permis B requis (oui / non / indifférent)

### Mobilité — différenciateur clé

L'utilisateur peut déclarer une fois sa commune de résidence (stockage local, anonyme). BE MELT affiche alors pour chaque offre :

- Distance à vol d'oiseau
- Temps de trajet estimé par mode (marche, vélo, trottinette électrique, scooter, voiture, transport en commun)
- Badge mobilité visuel selon le mode le plus pertinent

Filtre dédié : durée de trajet maximale acceptée (slider 15 à 60 min).

Bouton "Itinéraire précis" sur chaque offre, qui ouvre Google Maps ou Citymapper avec les deux points préremplis pour un calcul d'itinéraire détaillé.

### Vue pilotage MELT (mode conseiller)

Onglet "Statistiques territoriales" accessible à tous, avec lecture analytique :

- Nombre d'offres actives par commune et par niveau
- Répartition par famille de métier
- Ratio d'offres accessibles sans permis (indicateur de mobilité)
- Évolution hebdomadaire et mensuelle
- Comparaison MELT / MEL / Eurométropole

Cette vue permet à MELT de disposer pour la première fois d'un tableau de bord territorial de l'accessibilité réelle de l'emploi pour ses publics.

### Cas particulier Roncq

Conformément à la position de MELT, Roncq est intégrée au périmètre Niveau 1 sans distinction visuelle.

## 6. Architecture technique

| Couche | Technologie | Coût |
|---|---|---|
| Collecte de données | Python 3.11 + OAuth2 + requests | 0 € |
| Stockage | SQLite versionné dans le repo | 0 € |
| Génération site | Astro + Tailwind CSS | 0 € |
| Interactivité | Alpine.js (filtres, slider, sélecteur de commune) | 0 € |
| PWA installable | Service Worker via @vite-pwa/astro | 0 € |
| Hébergement | GitHub Pages avec HTTPS automatique | 0 € |
| Automatisation | GitHub Actions, cron 4×/jour | 0 € |
| Domaine | nom-de-domaine.fr en option | ~10 €/an |

Coût d'exploitation V1 : **0 € à 10 € par an**.

## 7. Calendrier V1

| Phase | Contenu | Durée |
|---|---|---|
| Sprint 0 — Préparation | Demande licence FT, création repo, validation périmètres | 1 semaine |
| Sprint 1 — Tuyaux de données | Collecteurs France Travail + Le Forem fonctionnels, SQLite peuplée | 2 semaines |
| Sprint 2 — Site statique + 3 niveaux | Pages Astro, filtres essentiels, déploiement GitHub Pages | 1 semaine |
| Sprint 3 — Mobilité + PWA | Filtres mobilité, calcul distances, manifest PWA, installation mobile | 1 semaine |
| Sprint 4 — Pilotage + polish | Onglet statistiques, charte visuelle finale, tests utilisateurs | 1 semaine |

**Cible présentation direction : 5 à 6 semaines après le démarrage.**

## 8. Évolutions envisagées V2

- Isochrones précalculées avec OpenRouteService (filtre par durée max précise pour tous modes hors TC)
- Calcul d'itinéraire fin en transports en commun via OpenTripPlanner local (multimodal Ilévia + TEC + De Lijn + SNCB)
- Lien sortant depuis ARIA vers BE MELT pour usage en entretien
- Tableau de bord pilotage enrichi pour la direction MELT
- Notification de nouvelles offres correspondant aux critères sauvegardés
- Mode "candidatures spontanées" via l'API La Bonne Boîte de France Travail

## 9. Gouvernance

- **Porteur projet** : Rafik [nom], conseiller MELT
- **Statut V1** : projet d'initiative interne, à des fins de démonstration et d'évaluation
- **Hébergement code** : repo GitHub privé tant que la direction n'a pas validé une publication
- **Décision attendue de la direction** : intégration officielle dans l'offre MELT, association éventuelle à ARIA dans un programme transversal "outils numériques d'insertion"
- **Soutiens institutionnels possibles** à explorer en cas de validation : FAJeM, FSE+, Interreg France-Wallonie-Vlaanderen (pour la dimension transfrontalière), MEL (compétence métropolitaine emploi)

## 10. Points d'attention et risques

- **Dépendance API France Travail** : si l'accès est retiré, le projet perd sa source principale (mitigation : Le Forem reste accessible, fallback partiel possible)
- **Qualité des données belges** : Le Forem traduit en français uniquement une partie des offres VDAB ; certaines offres flamandes restent invisibles côté BE MELT (à signaler)
- **Maintenance dans la durée** : un script de collecte automatisé demande un suivi mensuel léger (mise à jour des dépendances, vérification des quotas)
- **Cas Roncq** : la position MELT est intégrer sans distinction, à confirmer si évolution du financement
- **Présentation grand public** : BE MELT n'a pas vocation à remplacer francetravail.fr, juste à offrir une lecture territorialisée

---

*Document produit par Rafik [nom] avec l'assistance de Claude (Anthropic) — Mai 2026.*
