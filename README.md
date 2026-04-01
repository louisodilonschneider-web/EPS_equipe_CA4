# 🏀 ÉPS Manager — Gestion d'équipes sportives

Application web **tout-en-un** destinée aux professeurs d'ÉPS (Éducation Physique et Sportive) pour gérer une classe, composer des équipes équilibrées et arbitrer un match en temps réel — le tout dans un **fichier HTML unique**, sans installation, sans serveur.

---

## ✨ Fonctionnalités

### 👥 Gestion des élèves
- Ajouter, modifier et supprimer des élèves avec : prénom, nom, sexe (M / F / Autre) et niveau (1 à 5 étoiles)
- Définir des **affinités** (élèves à regrouper) et des **incompatibilités** (élèves à séparer)
- Filtrer la liste par sexe, niveau ou recherche textuelle
- Avatars colorés générés automatiquement selon le sexe

### 🏀 Composition des équipes
- Génération automatique d'équipes selon plusieurs paramètres :
  - **Nombre d'équipes** : de 2 à 6
  - **Format de jeu** : 3×3, 4×4 ou 5×5
  - **Type de groupement** :
    - Homogène démixé
    - Hétérogène démixé
    - Homogène mixte
    - Hétérogène mixte *(par défaut)*
  - **Sport** : champ libre (ex. Basketball, Handball…)
- Bouton **Remélanger** pour redistribuer les joueurs aléatoirement
- Drag-and-drop des joueurs entre équipes pour ajustement manuel
- Chaque équipe affiche son niveau moyen et sa composition

### ⏱ Suivi du match en temps réel
- Sélection de deux équipes parmi celles créées
- **Tableau de score** avec boutons +1 / +2 / +3 / −1 pour chaque équipe
- **Chronomètre** avec démarrage, pause et remise à zéro
- Gestion des **périodes** de jeu
- Affichage de l'**écart de score** en temps réel

#### 👥 Onglet Joueurs & +/−
- Vue côte à côte des deux équipes
- Statut terrain / banc pour chaque joueur
- **Temps de jeu individuel** suivi à la seconde
- Indicateur **+/−** (différentiel de score pendant le temps de présence du joueur)
- Bouton Entrer / Sortir pour gérer les rotations

#### ⚡ Onglet Règles
- Ajout de **règles de seuil** déclenchées automatiquement selon l'écart au score  
  *(ex. : « Si écart ≥ 4 pts, l'équipe en retard joue avec un défenseur supplémentaire »)*
- Alertes visuelles animées lorsqu'une règle est activée

#### 📊 Onglet Stats
- Classement de tous les joueurs par différentiel +/−
- Affichage du temps de jeu total par joueur

---

## 💾 Persistance des données

- Les données sont sauvegardées automatiquement dans le **localStorage** du navigateur
- **Export** : téléchargement d'un fichier `eps_manager_sauvegarde.json`
- **Import** : rechargement d'une sauvegarde JSON existante
- Un bouton **Démo** charge une classe fictive de 20 élèves avec des règles préconfigurées pour tester l'application immédiatement

---

## 🚀 Installation & utilisation

Aucune installation requise. L'application fonctionne entièrement dans le navigateur.

1. Télécharger le fichier `eps_manager.html`
2. L'ouvrir dans un navigateur moderne (Chrome, Firefox, Edge, Safari)
3. C'est tout — aucune connexion internet nécessaire après chargement (sauf pour les polices Google Fonts)

---

## 🛠 Stack technique

| Élément | Détail |
|---|---|
| Langage | HTML5 / CSS3 / JavaScript vanilla |
| Polices | Barlow & Barlow Condensed (Google Fonts) |
| Stockage | `localStorage` (navigateur) |
| Dépendances | Aucune — fichier unique auto-suffisant |

---

## 📋 Workflow typique

```
1. Charger la démo ou saisir sa classe (onglet Élèves)
2. Configurer le format de jeu et générer les équipes (onglet Équipes)
3. Ajuster manuellement les équipes si besoin (drag-and-drop)
4. Configurer un match : choisir les deux équipes qui s'affrontent
5. Démarrer le chronomètre et gérer le score en temps réel
6. Faire tourner les joueurs via l'onglet Joueurs & +/−
7. Consulter les stats en fin de match
8. Exporter les données pour les archiver
```

---

## 📄 Licence

Projet à usage pédagogique — libre d'utilisation et de modification.
