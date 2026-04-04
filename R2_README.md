# ÉPS Manager — README

Application web HTML/CSS/JS **standalone** (aucune dépendance serveur) destinée aux enseignants d'EPS pour gérer des équipes, suivre les scores et analyser le temps de jeu des élèves. L'interface suit la charte graphique **UNSS** (bleu `#003087`, orange `#f47920`).

---

## Fonctionnalités

### 👥 Gestion des élèves
- Ajouter, modifier ou supprimer des élèves (prénom, nom, sexe, niveau 1–5)
- Définir des **affinités positives** (élèves à regrouper) et des **incompatibilités** (élèves à séparer)
- Filtrer par nom, sexe ou niveau
- Importer / exporter les données en JSON

### 🏀 Composition des équipes
- Génération automatique selon 4 modes :
  - Homogène démixé / Hétérogène démixé
  - Homogène mixte / Hétérogène mixte
- Choix du nombre d'équipes (2 à 6) et du format de jeu (3c3, 4c4, 5c5)
- Respect des contraintes d'affinités et d'incompatibilités
- **Drag & drop** pour déplacer manuellement un élève d'une équipe à une autre
- Affichage du niveau moyen par équipe avec barre de progression

### ⏱ Suivi du match
- Tableau de score en temps réel avec boutons `+1`, `+2`, `+3`, `−1`
- Chronomètre par période (durée et nombre de périodes configurables)
- Calcul et affichage du **+/−** (plus/minus) de chaque joueur
- Suivi du **temps de jeu** individuel (terrain / banc)
- Boutons Entrer / Sortir pour gérer les rotations
- **Règles de seuil** : déclenchement automatique d'alertes visuelles selon l'écart au score (ex. : écart ≥ 4 pts → règle handicap)
- Onglet **Stats** : classement des joueurs par +/−

### 💾 Persistance des données
- Sauvegarde automatique dans le `localStorage` du navigateur
- Export JSON (`eps_manager_sauvegarde.json`)
- Import JSON pour restaurer une session
- Données démo intégrées (20 élèves fictifs + règles exemples)

---

## Installation

Aucune installation requise. Il s'agit d'un fichier HTML **autonome** :

```bash
# Ouvrir directement dans le navigateur
open eps_manager_unss.html
```

Compatible avec tous les navigateurs modernes (Chrome, Firefox, Safari, Edge).

---

## Structure du fichier

```
eps_manager_unss.html
│
├── <style>          # CSS complet (variables, composants, responsive)
│   ├── Variables UNSS (--accent: #f47920, --accent2: #003087 …)
│   ├── Nav, Hero, Cards, Buttons, Inputs
│   ├── Équipes (config + résultat + drag & drop)
│   ├── Match (score, timer, joueurs, règles, stats)
│   └── Modal, Toast, Responsive
│
├── <body>           # HTML structuré en pages SPA
│   ├── <nav>        # Barre de navigation sticky
│   ├── #page-home   # Accueil avec raccourcis et démo
│   ├── #page-eleves # Grille des élèves + filtres
│   ├── #page-equipes# Config + résultat des équipes
│   ├── #page-match  # Tableau de bord du match
│   ├── .modal-overlay (×2) # Modals élève et config match
│   └── #toast       # Notification flottante
│
└── <script>         # Logique JavaScript (~700 lignes)
    ├── state {}     # État global centralisé
    ├── Navigation   # showPage()
    ├── Storage      # localStorage + import/export JSON
    ├── Élèves       # CRUD + filtres + rendu
    ├── Équipes      # Génération + affinités + drag & drop
    └── Match        # Score + timer + PM + règles + stats
```

---

## Charte graphique UNSS

| Rôle | Variable CSS | Valeur |
|---|---|---|
| Fond général | `--bg` | `#f0f4f8` |
| Nav / En-têtes | `--bg2` | `#003087` |
| Fond secondaire | `--bg3` | `#e8eef5` |
| Cartes | `--card` | `#ffffff` |
| Accent principal | `--accent` | `#f47920` |
| Accent secondaire | `--accent2` | `#003087` |
| Succès | `--green` | `#2ecc71` |
| Erreur | `--red` | `#e74c3c` |

Police : **Barlow Condensed** (titres) + **Barlow** (corps) — Google Fonts.

---

## Utilisation rapide

1. Ouvrir `eps_manager_unss.html` dans le navigateur
2. Aller dans **Élèves** → ajouter les élèves de la classe (ou charger la démo)
3. Aller dans **Équipes** → configurer et générer les équipes
4. Aller dans **Match** → configurer le match (équipes, durée, périodes)
5. Lancer le chronomètre, saisir les scores, gérer les rotations en direct
6. Consulter les **Stats** en fin de match
7. **Exporter** les données JSON pour les réutiliser lors de la prochaine séance

---

## Limites connues

- Les données sont stockées dans le navigateur (`localStorage`) : elles sont perdues si le cache est vidé ou si l'on change de navigateur/appareil. Utiliser l'export JSON pour la persistance long terme.
- Pas de mode multijoueur réseau : l'application est mono-poste.
- Le drag & drop des joueurs entre équipes n'est pas disponible sur mobile (touch events non implémentés).

---

## Licence

Usage interne EPS / UNSS. Application non distribuée commercialement.
