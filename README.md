# BE MELT — Boussole Emploi Lys-Tourcoing

Outil de consultation territorialisée des offres d'emploi pour les publics et professionnels de la Mission Emploi Lys-Tourcoing (MELT), avec ouverture transfrontalière vers la Belgique via le périmètre de l'Eurométropole Lille-Kortrijk-Tournai.

> Projet à finalité d'insertion professionnelle, non commercial. Données publiques uniquement.

---

## Vue d'ensemble

BE MELT agrège en temps réel les offres d'emploi de France Travail (et partenaires) et du Forem (et partenaires VDAB/Actiris) sur **trois niveaux territoriaux emboîtés** :

1. **MELT** — 12 communes du territoire Lys-Tourcoing
2. **MEL** — 95 communes de la Métropole Européenne de Lille
3. **Eurométropole** — ~157 communes du GECT Lille-Kortrijk-Tournai (transfrontalier)

L'outil intègre nativement les contraintes de mobilité du public ML : filtre par permis B, par distance, par temps de trajet selon le mode de transport (marche, vélo, trottinette électrique, scooter, voiture, transport en commun).

## Stack technique

- **Backend** : Python 3.11 + requests + sqlite3
- **Frontend** : Astro + Tailwind CSS + Alpine.js
- **PWA** : @vite-pwa/astro
- **Hébergement** : GitHub Pages (privé en phase V1)
- **Automatisation** : GitHub Actions, cron 4×/jour

Coût total d'exploitation : 0 €.

## Structure du repo

```
be-melt/
├── collectors/                 # Scripts Python de collecte API
│   ├── france_travail.py       # API France Travail Offres d'emploi v2
│   ├── le_forem.py             # API Le Forem (Open Data Wallon)
│   └── normalize.py            # Normalisation vers schéma commun
├── data/
│   ├── be_melt.db              # SQLite (généré par les collecteurs)
│   ├── communes_melt.json      # Référentiel 12 communes MELT + codes INSEE
│   ├── communes_mel.json       # Référentiel 95 communes MEL + codes INSEE
│   ├── communes_eurometropole.json  # Référentiel ~157 communes Eurométropole
│   └── reseaux_transport.json  # Table commune → réseaux TC desservants
├── site/                       # Code Astro
│   ├── src/
│   ├── public/
│   └── astro.config.mjs
├── scripts/                    # Utilitaires (build, deploy, helpers)
├── docs/                       # Documentation projet
│   ├── 01_NOTE_CADRAGE_BE_MELT.md
│   ├── 02_API_FRANCE_TRAVAIL.md
│   └── 03_API_LE_FOREM.md
├── .github/workflows/
│   ├── collect.yml             # Cron 4×/jour collecte + commit
│   └── deploy.yml              # Build Astro + déploiement GitHub Pages
├── .env.example                # Modèle pour les credentials FT (non commité)
├── requirements.txt            # Dépendances Python
├── package.json                # Dépendances Astro
└── README.md
```

## Installation locale

### Prérequis

- Python 3.11+
- Node.js 20+
- Compte France Travail Développeurs avec credentials API Offres d'emploi v2

### Mise en place

```bash
# Clone
git clone git@github.com:USER/be-melt.git
cd be-melt

# Backend Python
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Credentials France Travail
cp .env.example .env
# Éditer .env et renseigner FT_CLIENT_ID et FT_CLIENT_SECRET

# Première collecte
python -m collectors.france_travail
python -m collectors.le_forem

# Frontend Astro
cd site
npm install
npm run dev
```

## Statut du projet

- [ ] Sprint 0 — Demande licence France Travail
- [ ] Sprint 0 — Référentiels communes (3 niveaux)
- [ ] Sprint 1 — Collecteur Le Forem
- [ ] Sprint 1 — Collecteur France Travail
- [ ] Sprint 1 — Normalisation et stockage SQLite
- [ ] Sprint 2 — Site Astro avec 3 vues territoriales
- [ ] Sprint 2 — Déploiement GitHub Pages
- [ ] Sprint 3 — Filtres mobilité (permis, distance, mode, temps)
- [ ] Sprint 3 — PWA installable
- [ ] Sprint 4 — Vue pilotage MELT
- [ ] Sprint 4 — Charte visuelle finale
- [ ] Sprint 4 — Démo direction

## Licence

À définir lors de la publication. Probablement EUPL ou MIT pour le code, données reprises sous leurs licences respectives (Licence Ouverte France Travail, ODbL Le Forem, Licence Ouverte v2 MEL).

## Contact

Rafik [nom] — MELT — Mission Emploi Lys-Tourcoing
