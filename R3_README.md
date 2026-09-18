# 🏀 ÉPS Manager — Gestion d'équipes sportives

Application web **tout-en-un** destinée aux professeurs d'ÉPS (Éducation Physique et Sportive) pour gérer leurs classes, composer des équipes équilibrées et arbitrer des matchs en temps réel — le tout dans un **fichier HTML unique**, sans installation, sans serveur.

---

## ✨ Nouveautés v4

- **Authentification** : création de compte (email ou Google), profil enseignant persistant
- **Gestion multi-classes** : plusieurs classes par compte, partage avec collègues
- **Historique des leçons** : suivi de toutes les séances et groupements réalisés
- **Niveaux dynamiques** : le niveau de chaque élève évolue automatiquement selon ses statistiques
- **5 modes de scoring** : Classique, Bonifier, Contrat, Bingo, Évolutive
- **Statistiques individuelles complètes** : +/−, minutes jouées, % tir, victoires...
- **Gestion des rotations** avec feuille de route automatique
- **Design responsive** : téléphone, tablette et ordinateur

---

## 📋 Fonctionnalités détaillées

### 🔐 Identification
- Création de compte avec adresse email et mot de passe
- Connexion via Google (OAuth simulé — intégrable en production)
- Données sauvegardées séparément par compte dans le navigateur
- Session persistante entre les visites

### 🏫 Gestion des classes
- Créer, modifier et supprimer des classes (nom, sport, année scolaire)
- **Partager une classe** avec des collègues via leurs adresses email
- Vue synthétique : nombre d'élèves, leçons, partage actif
- Sélecteur de classe rapide dans la barre latérale

### 👥 Gestion des élèves
- Ajouter, modifier et supprimer des élèves : prénom, nom, genre (M / F / Autre), niveau
- **Import CSV / PDF** : colonne Prénom, Nom, Genre (M/F/A), Niveau
- Affinités et incompatibilités pour guider la composition des équipes
- Affichage de la progression du niveau (historique complet)
- Barre de niveau visuelle et statistiques récapitulatives par élève

### 📋 Leçons & groupements

#### Composition des équipes
- Définir le nombre d'équipes (2 à 6), le format (3×3, 4×4, 5×5), le type et le sport
- **Types de groupement** : Homogène démixé, Hétérogène démixé, Homogène mixte, Hétérogène mixte
- **Gestion de la présence** : Présent / Absent / Blessé (le blessé intègre un groupe sans jouer)
- **Copier la configuration** d'une leçon précédente
- **Remélanger** les équipes en respectant les critères définis
- **Drag-and-drop** pour déplacer manuellement les élèves entre équipes
- Suppression d'une leçon possible

### ⏱ Match en direct

#### Modes de scoring
| Mode | Description |
|------|-------------|
| 🏀 **Classique** | 1, 2 ou 3 points par panier |
| ⭐ **Bonifier** | Tirs valant 1, 10 ou 100 pts (critères configurables) |
| 📝 **Contrat** | Condition spéciale rapportant +10 pts (optionnel : mort subite) |
| 🎯 **Bingo** | 3 contrats à réaliser — l'équipe en réalisant le plus gagne |
| ⚡ **Évolutive** | Règles déclenchées selon l'écart de score (cumulables) |

#### Tableau de score
- Score en temps réel avec boutons de panier adaptés au mode
- **Tir tenté** et **Perte de balle** par équipe
- Chronomètre avec démarrage, pause et navigation entre les périodes
- Bouton **Fin du match** → retour à la sélection du prochain match

#### Onglet Joueurs & +/−
- Statut terrain / banc de chaque joueur
- Temps de jeu individuel à la seconde
- Indicateur **+/−** en temps réel

#### Onglet Stats live
- Score, % de tir, pertes de balle, temps écoulé par équipe
- Actualisé à chaque action

#### Onglet Graphique
- Courbe d'évolution des scores des deux équipes au fil du match

#### Classement de la leçon
- Tableau récapitulatif des équipes en cours de match

### 🔄 Gestion des rotations

#### Configuration des espaces
- Nombre de terrains disponibles (1 à 6)
- Durée de rotation paramétrable
- Espaces : Terrain(s), Arbitrage, Apprentissage (activables / désactivables)
- **Drag-and-drop** des équipes entre les espaces

#### Rotations automatiques
- **Roulement** : toutes les équipes avancent d'un espace
- **Inversion** : les équipes s'inversent dans chaque espace

#### Feuille de route
- Tableau horodaté de toutes les rotations planifiées
- **Sur-brillance** de la ligne active en corrélation avec le match en cours
- Suppression de la dernière rotation possible

### 📊 Statistiques individuelles
- Matchs gagnés (total, toutes leçons)
- +/− cumulé sur l'ensemble des matchs
- Minutes jouées totales
- % de tirs réussis sur tentés (calculé lors des présences terrain)
- **Niveau dynamique** : ajusté automatiquement selon le différentiel +/− à chaque fin de match
- Classement général des élèves de la classe active

---

## 💾 Persistance des données

- Les données sont stockées dans le **localStorage** du navigateur, séparément par compte
- **Export JSON** : sauvegarde complète téléchargeable
- **Import JSON** : rechargement d'une sauvegarde
- **Import CSV** : ajout rapide d'élèves depuis un tableur
- Bouton **Démo** : charge une classe fictive de 20 élèves avec 2 leçons préconfigurées

---

## 🚀 Installation & utilisation

Aucune installation requise.

1. Télécharger le fichier `Manager_V4_index.html`
2. L'ouvrir dans un navigateur moderne (Chrome, Firefox, Edge, Safari)
3. Créer un compte ou se connecter
4. Créer une classe → ajouter les élèves → générer les équipes

> **Note** : une connexion internet est uniquement nécessaire pour charger les polices Google Fonts au premier lancement. L'application fonctionne ensuite hors-ligne.

---

## 📱 Compatibilité

| Support | Statut |
|---------|--------|
| 📱 Téléphone (320px+) | ✅ Optimisé |
| 📊 Tablette | ✅ Optimisé |
| 💻 Ordinateur | ✅ Optimisé |
| Chrome / Firefox / Safari / Edge | ✅ Compatible |

---

## 🛠 Stack technique

| Élément | Détail |
|---------|--------|
| Langage | HTML5 / CSS3 / JavaScript vanilla |
| Polices | Outfit & Space Grotesk (Google Fonts) |
| Stockage | `localStorage` (navigateur, par compte) |
| Dépendances | Aucune — fichier unique auto-suffisant |

---

## 📋 Workflow typique

```
1. Créer un compte → sélectionner ou créer une classe
2. Ajouter les élèves (manuellement ou via CSV)
3. Créer une leçon → gérer la présence → générer les équipes
4. Ajuster les équipes manuellement (drag-and-drop)
5. Configurer un match (mode de scoring + équipes)
6. Démarrer le chronomètre → saisir les scores en temps réel
7. Gérer les rotations via l'onglet Gestion → renseigner la feuille de route
8. Consulter les statistiques en fin de séquence
9. Exporter les données pour archiver
```

---

## 📄 Licence

Projet à usage pédagogique — libre d'utilisation et de modification.
