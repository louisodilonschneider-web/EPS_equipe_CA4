# UNSS – Gestionnaire de Tournois 🏸

Application web autonome destinée aux enseignants d'EPS dans le cadre des compétitions **UNSS** (Union Nationale du Sport Scolaire). Elle permet de gérer l'intégralité d'un tournoi : inscription des participants, génération des poules, gestion des tableaux à élimination, rencontres académiques, situation « Partenaire en Or » et export PDF.

---

## Sommaire

- [Prérequis](#prérequis)
- [Installation et lancement](#installation-et-lancement)
- [Vue d'ensemble](#vue-densemble)
- [Modules](#modules)
  - [1. Compétitions](#1-compétitions)
  - [2. Participants](#2-participants)
  - [3. Poules](#3-poules)
  - [4. Tableau](#4-tableau)
  - [5. Rencontres Académiques](#5-rencontres-académiques)
  - [6. Partenaire en Or](#6-partenaire-en-or)
  - [7. Classement](#7-classement)
- [Export PDF](#export-pdf)
- [Persistance des données](#persistance-des-données)
- [Technologies utilisées](#technologies-utilisées)
- [Limitations connues](#limitations-connues)
- [Pistes d'évolution](#pistes-dévolution)

---

## Prérequis

- Un navigateur web moderne (Chrome, Firefox, Edge, Safari)
- Une connexion internet pour le chargement des polices (Google Fonts) et de la librairie PDF (jsPDF via CDN)
- Aucune installation de serveur, base de données ou logiciel tiers

---

## Installation et lancement

1. Télécharger le fichier `unss_tournoi.html`
2. L'ouvrir dans un navigateur web

C'est tout. L'application fonctionne entièrement côté client, sans serveur ni backend.

---

## Vue d'ensemble

L'interface reprend les couleurs officielles UNSS :

- **Bleu principal** `#1a3fa8`
- **Orange accent** `#f47c20`

La navigation se fait via la barre en haut de page. Chaque onglet correspond à un module indépendant. Les données sont sauvegardées automatiquement dans le `localStorage` du navigateur à chaque modification.

---

## Modules

### 1. Compétitions

Point d'entrée de l'application. Chaque compétition est un contexte isolé avec ses propres participants, poules et tableaux.

**Paramètres configurables :**

| Champ | Description |
|---|---|
| Nom | Intitulé de la compétition |
| Sport / Discipline | Libellé libre (ex. Badminton, Tennis de table…) |
| Date | Date de l'événement |
| Type de victoire | Par **points** (ex. 21 pts) ou par **sets** |
| Valeur de victoire | Nombre de points ou de sets requis |
| Format | **Individuel** ou **Par équipes** |
| Lieu | Gymnase ou salle |

Plusieurs compétitions peuvent coexister. La compétition active est signalée par un bandeau orange. Elle peut être supprimée à tout moment.

---

### 2. Participants

Gestion de la liste des joueurs inscrits à la compétition active.

**Données par participant :**
- Prénom, Nom
- Établissement scolaire
- Équipe (affiché uniquement en format équipe)
- Niveau de jeu (1 à 5) — utilisé pour les répartitions hétérogènes

**Modes de saisie :**
- Formulaire individuel
- **Import rapide** : coller une liste de joueurs en texte brut, un par ligne, au format `Prénom Nom Établissement Niveau`

---

### 3. Poules

Génération et gestion des phases de poules.

**Trois modes de répartition :**

| Mode | Comportement |
|---|---|
| Manuelle | Les élèves sont répartis dans l'ordre de la liste |
| Hétérogène | Algorithme en serpentin par niveau — les meilleurs joueurs sont distribués équitablement entre les poules |
| Aléatoire | Tirage au sort |

**Taille des poules :** 3 ou 4 joueurs maximum, configurable.

**Saisie des scores :** chaque match de poule dispose de deux champs de score. Le résultat est validé automatiquement dès qu'un joueur atteint le score de victoire défini.

**Classement de poule :** calculé en temps réel avec victoires (3 pts), défaites (0 pt) et différentiel de points comme critère secondaire.

**Depuis les poules :** un bouton permet de basculer directement vers le module Tableau en important le classement des poules comme seeds.

---

### 4. Tableau

Tableau à élimination directe avec gestion automatique de la structure selon le nombre de participants.

**Sources d'alimentation :**
- Depuis les poules (classement)
- Placement manuel (ordre de la liste)
- Aléatoire
- Par niveau

**Gestion des byes :** si le nombre de participants ne correspond pas à une puissance de 2, les joueurs en trop peu de byes sont automatiquement positionnés pour sauter le premier tour. Le tableau s'adapte que l'on ait 5, 13, 24 ou 36 joueurs.

**Tableau consolante (optionnel) :** les joueurs éliminés au premier tour sont réorientés dans un tableau parallèle. Cela permet de produire un **classement complet** (1er, 2e, 3e, 4e…) sans qu'aucun joueur reste sans rencontre.

**Propagation automatique :** les gagnants avancent automatiquement dans l'arbre dès la saisie du score, sans action supplémentaire.

---

### 5. Rencontres Académiques

Module dédié aux phases académiques réunissant plusieurs départements.

**Structure :**
- 3 départements, jusqu'à 6 joueurs chacun (paramétrable)
- Poules hétérogènes de 3 à 4 joueurs
- L'algorithme s'assure de **ne pas regrouper deux joueurs du même département** dans la même poule, tout en équilibrant les niveaux

**Paramètre :** le score de victoire (points ou sets) est saisi séparément pour ce module.

**Sortie :** les résultats des poules académiques alimentent un tableau à qualification directe, avec consolante pour un classement complet.

---

### 6. Partenaire en Or

Situation pédagogique coopérative propre au badminton UNSS.

**Principe :**
- Deux joueurs doivent réaliser un nombre d'échanges défini à l'avance
- **Succès** (objectif atteint) → 10 points chacun
- **Échec** → 1 point chacun
- Chaque paire ne peut jouer qu'**une seule fois** ensemble
- La situation prend fin quand un joueur a affronté tous ses camarades, ou quand le temps imparti est écoulé

**Fonctionnalités :**

| Élément | Description |
|---|---|
| Nombre d'échanges | Objectif configurable avant le départ |
| Durée | Chronomètre dégressif (en minutes) ; 0 = pas de limite |
| Matrice des paires | Tableau croisant tous les joueurs, indiquant en vert les paires ayant joué, avec le résultat |
| Alerte automatique | Un message s'affiche quand un joueur a complété toutes ses paires |
| Saisie des résultats | Menu déroulant joueur 1 / joueur 2 / résultat |
| Scores en direct | Classement mis à jour en temps réel |

---

### 7. Classement

Synthèse globale des résultats de la compétition active.

**Classement individuel :** agrège les points de victoire issus de toutes les phases de poules. Trié par points, puis par nombre de victoires.

**Classement par équipe :** somme des points individuels regroupés par équipe (disponible en format équipe uniquement).

Les trois premiers sont mis en valeur visuellement (🥇🥈🥉).

---

## Export PDF

Un bouton **📄 Export PDF** est disponible en haut à droite à tout moment. Il génère un fichier PDF nommé `UNSS_[NomCompétition]_[Date].pdf` contenant :

- En-tête aux couleurs UNSS avec nom de la compétition et date
- Tableau du classement individuel complet
- Résultats détaillés de chaque poule
- Numérotation des pages
- Mise en page optimisée impression A4

---

## Persistance des données

Les données sont sauvegardées automatiquement dans le `localStorage` du navigateur à chaque action (ajout de joueur, saisie de score, génération de poule…). Elles persistent entre les sessions sur le même navigateur et le même appareil.

> **Attention :** vider le cache ou les données du navigateur effacera toutes les compétitions enregistrées. Pour archiver, utiliser l'export PDF avant toute opération de nettoyage du navigateur.

---

## Technologies utilisées

| Technologie | Usage |
|---|---|
| HTML5 / CSS3 / JavaScript (vanilla) | Structure, style, logique applicative |
| [Google Fonts – Barlow](https://fonts.google.com/specimen/Barlow) | Typographie (Barlow + Barlow Condensed) |
| [jsPDF 2.5.1](https://github.com/parallax/jsPDF) | Génération des exports PDF côté client |
| localStorage | Persistance des données sans serveur |

Aucune dépendance npm, aucun framework JS. Le fichier est entièrement autonome.

---

## Limitations connues

- Les données sont liées au navigateur : elles ne se synchronisent pas entre appareils
- L'export PDF ne reproduit pas le style graphique complet (limites de jsPDF)
- L'application nécessite une connexion internet au premier chargement (CDN Google Fonts et jsPDF)
- Le module Académique ne génère pas encore automatiquement le tableau final depuis les poules académiques (saisie manuelle des scores)

---

## Pistes d'évolution

- Export Excel / CSV des listes de joueurs et résultats
- Mode hors-ligne complet via Service Worker
- Synchronisation cloud (Firebase, Supabase…)
- Support multi-sport avec règles adaptées (tennis de table, volleyball…)
- Impression de feuilles de match au format A5
- QR Code de saisie pour les élèves arbitres
- Mode responsive optimisé tablette pour utilisation en gymnase

---

> Développé pour les enseignants d'EPS dans le cadre du dispositif **UNSS 2024–2028**.
