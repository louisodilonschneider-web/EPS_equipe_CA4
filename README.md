# Organisation CA4 — Collège Louis Pasteur, Villemomble

Application web pour organiser un affrontement en un contre un — **poules**, **ligues** et
**défis** — suivre les compétences de chaque élève au fil du cycle, différencier les situations
d'apprentissage et évaluer. Elle est livrée réglée sur le **badminton**, et sait aussi faire du
tennis de table, de l'escrime, ou revenir au fonctionnement d'un sport collectif.

Elle fonctionne **hors ligne**, **sans compte**, et **sans envoyer aucune donnée sur Internet**
tant que la synchronisation n'est pas activée. Tout tient dans un dossier de fichiers statiques.

Une classe traverse **jusqu'à dix APSA dans l'année**, et chacune est un cycle autonome : son
activité, ses critères, ses relevés… et **ses propres indices**. Être à l'aise en badminton ne dit
rien de ce qu'on vaut en handball : l'application ne mélange jamais les deux.

> **C'est le second site**, jumeau de l'application d'ultimate : même moteur d'indices, mêmes
> situations à paliers, même banque, même mode kiosque. Ce qui change tient en trois choses : les
> **APSA**, qui découpent l'année en cycles cloisonnés ; l'onglet **Rencontres**, qui organise les
> duels ; et les **familles d'activité**, qui décident de ce qui s'affiche. Les deux applications
> ont chacune leur stockage, leur cache et leur espace de synchronisation : **elles ne se marchent
> jamais dessus**, même déposées sur le même compte GitHub.

---

## 1. Mise en route

### Option A — GitHub Pages (recommandée)

1. Crée un dépôt sur GitHub (par exemple `organisation-ca4`) et dépose-y le contenu de ce dossier.
2. Dans le dépôt : **Settings → Pages → Source : Deploy from a branch → `main` / `/ (root)`**.
3. Au bout d'une minute, l'application est à l'adresse `https://<ton-compte>.github.io/organisation-ca4/`.
4. Sur ta tablette, ouvre cette adresse puis « Ajouter à l'écran d'accueil ». Elle s'installe
   comme une application et fonctionne ensuite **sans réseau**, ce qui est indispensable en gymnase.

### Option B — le fichier unique, sans rien installer

`organisation-ca4-autonome.html` est l'application **entière dans un seul fichier**
(HTML, CSS et JavaScript réunis, aucune dépendance). Double-clique dessus : elle s'ouvre
dans le navigateur et fonctionne immédiatement.

C'est la version à utiliser si tu veux essayer tout de suite, l'envoyer à un collègue,
ou la copier sur une clé USB. Tu peux aussi la déposer telle quelle sur GitHub Pages :
renomme-la `index.html` et c'est en ligne.

Seules différences avec la version en dossier : pas d'installation en application
sur l'écran d'accueil, et pas de cache hors ligne automatique (ces deux fonctions
exigent une adresse `http(s)` et le fichier `sw.js`).

> Les deux versions ne partagent pas leurs données : chaque adresse a son propre stockage.
> Choisis-en une pour ton cycle, et utilise l'export JSON pour passer de l'une à l'autre.

### Option C — serveur local, pour développer

```bash
python3 -m http.server 8000
# puis http://localhost:8000
```

### Combien de place l'application prend-elle ?

Le navigateur accorde environ **5 Mo par adresse**. Le texte n'y fait rien : classes, leçons, scores et
notes d'un cycle entier pèsent quelques dizaines de kilo-octets. Ce sont les **images** — schémas de
situations, illustrations des messages de palier — qui remplissent l'espace : une photo compressée
tourne autour de 50 à 90 Ko, et une situation à trois paliers peut en porter dix.

Quand la limite est atteinte, le navigateur refuse d'écrire et l'application prévient :
*« Stockage plein : rien n'est enregistré depuis maintenant »*. Tant que ce message est là, ce que tu
saisis sera perdu au rechargement — c'est le seul cas où l'application peut te faire perdre du travail.

**Réglages → Stockage** montre une jauge, le poids des images et celui du texte, et propose
**« Alléger les images »** : toutes les images enregistrées sont recompressées en 720 px, ce qui
divise leur poids par deux ou trois sans les rendre illisibles sur tablette. C'est le geste qui
débloque un stockage saturé — l'écriture qui suit est plus petite que ce qui était déjà en place,
elle passe donc même quand tout est plein. Si cela ne suffit pas : exporte une sauvegarde, puis
supprime les leçons des cycles terminés (leurs scores restent dans le fichier exporté).

Les nouvelles images sont enregistrées en 800 px, ce qui suffit largement pour un schéma de terrain.

### Mettre à jour l'application sans perdre ses données

Remplacer les fichiers sur GitHub (ou le fichier autonome sur la clé) **ne touche jamais aux données** :
classes, leçons, situations et notes vivent dans le stockage local du navigateur, pas dans les fichiers
du site. Dépose la nouvelle version, recharge la page, tout est là.

Deux points de vigilance, et un seul geste de prudence :

- **L'adresse doit rester la même.** Le stockage est attaché à l'adresse du site : `toncompte.github.io`
  et le fichier ouvert depuis le disque sont deux espaces séparés. Renommer le dépôt change l'adresse,
  donc l'espace de données.
- **Le cache hors ligne peut retarder l'affichage d'une nouveauté.** L'application se met en cache pour
  fonctionner sans réseau ; elle interroge d'abord le réseau (avec un délai de 2,5 s) et ne se rabat sur
  le cache qu'au-delà. Une nouvelle version déposée est donc visible dès le rechargement suivant. Si
  l'ancienne persiste, un rechargement forcé (Ctrl/Cmd + Maj + R) suffit ; sur tablette, ferme et
  rouvre l'application.
- **Exporte une sauvegarde avant une grosse mise à jour** (Réglages → Exporter). Le fichier JSON se
  réimporte en un clic, et te met à l'abri d'une fausse manœuvre — y compris d'un « effacer les données
  du site » déclenché par erreur.

### Ne jamais désinstaller l'application pour la « rafraîchir »

Sur tablette, l'icône ajoutée à l'écran d'accueil n'est pas un raccourci : c'est une application
installée, **avec son propre stockage**. La supprimer efface ce stockage — classes, leçons et notes
partent avec elle, et la réinstaller rend une application vide. C'est la seule manœuvre capable de
tout perdre d'un coup.

Quand une nouveauté ne s'affiche pas, c'est le cache hors ligne qui sert l'ancienne version. Le
bouton **Réglages → Mettre à jour l'application → « Recharger la dernière version »** vide ce cache
et redémarre l'application sur la version la plus récente, **sans toucher aux données**. C'est le
geste à faire, à la place de la désinstallation.

Trois filets de sécurité, dans l'ordre :

1. **L'export JSON** (Réglages → Exporter). C'est la seule copie qui survit à une réinstallation ou
   à un « effacer les données du site ». L'application affiche un rappel sur la liste des leçons dès
   que la dernière copie date de plus de deux semaines — range le fichier dans ton cloud habituel ou
   envoie-le-toi par mail.
2. **La synchronisation** (voir plus bas) : une copie complète part sur le serveur à chaque
   enregistrement. Sur un appareil réinstallé, il suffit de se reconnecter : l'application constate
   qu'elle est vide alors que le serveur garde une sauvegarde, et propose de la récupérer.
   **Un appareil vide n'écrase jamais la sauvegarde du serveur** — l'envoi est suspendu et la
   récupération proposée à la place.
3. **Un autre appareil.** Les données ne sont pas partagées entre l'ordinateur et la tablette :
   si l'un des deux a encore les données, exporte-les là-bas et importe-les ici.

Si tout cela manque au moment où l'accident arrive, il reste la restauration d'une sauvegarde
complète de la tablette (iCloud, Google), antérieure à la suppression — et rien d'autre.

> **Important :** les données sont stockées **par navigateur et par adresse**.
> La version ouverte depuis GitHub Pages et celle ouverte depuis le fichier local
> ne partagent rien. Choisis une adresse et gardes-y tes données, ou fais circuler
> la sauvegarde JSON (Réglages → Exporter / Importer).

---

## 2. Importer une classe

**Classes → Importer un CSV.**

**L'export d'appel du collège est reconnu tel quel** :

```csv
Élèves;encouragement/valorisation;Né(e) le;Sexe
MARTIN Léa;;12/03/2012;Féminin
BERNARD Lucas;à encourager;05/07/2011;Masculin
DE LA TOUR Jean-Luc;;01/01/2012;Masculin
```

| Colonne | Contenu | Ce qu'en fait l'application |
|---|---|---|
| 1 | `Élèves` — NOM et Prénom | séparés automatiquement : les mots en majuscules forment le nom |
| 2 | `encouragement/valorisation` | ignorée |
| 3 | `Né(e) le` | ignorée |
| 4 | `Sexe` — Masculin ou Féminin | sert uniquement à la contrainte de mixité |

L'application détecte seule le séparateur et l'encodage (UTF-8 avec repli sur Windows-1252, le cas
des exports Excel français). Un écran de mappage s'affiche quand même, avec un aperçu en direct : tu
vérifies d'un coup d'œil et tu corriges si besoin.

**Le séparateur se change à la main** — point-virgule, virgule, tabulation, barre verticale : le
fichier est relu aussitôt et l'aperçu se recalcule. Utile quand la détection tombe à côté, par
exemple sur un export où des virgules traînent à l'intérieur des cellules.

**« Prénom Nom » marche aussi bien que « Nom Prénom ».** Un mot tout en majuscules est lu comme le
nom de famille, où qu'il se trouve : `MARTIN Léa` et `Léa MARTIN` se lisent l'un comme l'autre, et
`Jean-Luc DE LA TOUR` garde sa particule. Un menu **« Dans quel ordre »** tranche les cas où la
casse ne dit rien (`Dupont Marie`) — il est pré-réglé d'après l'en-tête (`Prénom Nom`) et d'après ce
que contiennent les premières lignes, et tu peux le forcer.

Cas gérés :

- noms composés et particules (`DE LA TOUR Jean-Luc`), apostrophes (`N'GUYEN Maï`) ;
- colonnes `Nom` et `Prénom` séparées, si ton export a cette forme ;
- sexe sous n'importe quelle forme (`Masculin`/`Féminin`, `M`/`F`, `Garçon`/`Fille`, `1`/`2`) ;
- fichier **sans ligne d'en-tête** : la première colonne sert de nom et la colonne du sexe est
  devinée d'après son contenu ;
- absence de colonne sexe : le mode « équipes mixtes » est alors sans effet, et on peut
  renseigner le sexe élève par élève dans sa fiche.

---

## 2 bis. Les APSA : une année, plusieurs cycles

Une classe ne fait pas du badminton toute l'année. Elle fait du badminton, puis du handball, puis de
l'escrime — **jusqu'à dix activités**, et chacune est un cycle à part entière.

Le bandeau en haut des **Leçons**, des **Statistiques** et des **Réglages** montre les APSA de la
classe et laisse en choisir une. C'est là qu'on en crée une nouvelle (« + APSA »), qu'on la renomme,
qu'on change son activité support ou qu'on la supprime. Tout ce que tu fais ensuite — leçons,
rencontres, situations, évaluation — appartient au cycle ouvert.

**Chaque APSA apporte trois choses :**

| Ce qu'elle fournit | Exemple en badminton |
|---|---|
| les **critères évalués** | Frappes et technique · Déplacements · Tactique · Fair-play et arbitrage |
| les **relevés** | points gagnants, fautes directes, services ratés, et deux compteurs facultatifs |
| le **format d'une rencontre** | 11 points, 2 d'écart |

Dix préréglages sont livrés, répartis en deux familles :

- **duel** (raquettes, sports de combat) : **badminton**, **tennis de table**, **tennis**,
  **escrime**, **boxe française** — qui vaut aussi pour la lutte ou le judo ;
- **collectif** (avec un ballon ou un disque) : **ultimate**, **handball**, **basket-ball**,
  **volley-ball**, **rugby**.

Le **rugby** est réglé pour le jeu à toucher ou à effectif réduit, tel qu'il se pratique au collège :
critères *Passe et réception · Avancer et soutenir · Défense · Fair-play et arbitrage* ; relevés
*passes réussies*, *ballons perdus (en-avant, passe au sol)*, *ballons récupérés et touchers
réussis*, *essais* — plus deux compteurs à activer au besoin, *franchissements* et *soutiens au
porteur*, pour une leçon centrée sur l'avancée ou sur le jeu à plusieurs.

Ce sont des points de départ : critères, relevés et format se renomment et se repondèrent dans les
réglages, **sans toucher aux autres cycles de la classe**. Un cycle de tennis de table part du
badminton et change trois mots.

Le format sert de repère à la saisie (« rencontre en 11 points ») sans jamais bloquer un score que
tu corriges à la main — un set interrompu par la sonnerie se note tel qu'il s'est arrêté.

### Un indice par APSA

C'est le point le plus important, et le plus facile à manquer : **l'indice d'un élève est calculé à
l'intérieur d'une APSA**, sur les seules leçons de ce cycle et avec ses seuls critères. La fiche
élève ouvre d'ailleurs sur un tableau « Indice par APSA » : un élève peut être à 6,2 en badminton et
à 4,7 en handball, et c'est exactement ce qu'on veut lire. Mélanger les deux produirait un chiffre
qui ne veut rien dire — ni pour composer des groupes, ni pour évaluer.

Conséquence pratique : les poules, les ligues et les équipes se composent à partir de l'indice du
cycle en cours. En début de cycle, tout le monde part de 5 et les groupes sont donc quasi aléatoires
— c'est normal, et c'est honnête : l'application ne fait pas semblant de savoir.

### Duel ou collectif : ce qui change à l'écran

La famille de l'activité décide des onglets de la leçon :

| Famille | Onglets | Le mot employé |
|---|---|---|
| **duel** | Présences · Échauffement · Situations · **Rencontres** | une **rencontre** |
| **collectif** | Présences · **Équipes** · Échauffement · Situations · **Matchs** | un **match** |

L'affrontement arrive en fin de ligne dans les deux familles : c'est l'ordre du cours — on met en
train, on travaille, puis on se rencontre.

En badminton, ni équipes ni tournoi : on ne voit que ce qui sert. En handball, pas d'échelle de
défis : les affrontements sont des matchs entre équipes. Rien n'est perdu — changer de cycle suffit
à retrouver l'autre organisation.

Dernière différence, invisible mais importante : en duel, **le résultat pèse plus lourd** dans
l'indice global que dans un sport collectif (40 % au lieu de 10 %). C'est logique — en badminton,
gagner ne dépend de personne d'autre que soi, alors qu'en handball le score dit d'abord quelque
chose de l'équipe. Le réglage reste modifiable dans « D'où vient l'indice de chaque élève ».

---

## 3. Le parcours de l'application

Le menu suit l'ordre dans lequel on travaille vraiment :

```
1. Classes  →  APSA du cycle  →  2. Leçons  →  Présences  →  ┌ Équipes      (collectif)
                                                  │           ├ Échauffement
                                                  │           ├ Situations
                                                  │           └ Rencontres  (duel)
                                                  │              ou Matchs  (collectif)
                                                  └─ Évaluation

puis, hors séance :   Contraintes  ·  Statistiques  ·  Réglages  ·  Situations (banque)
```

On choisit la classe, on ouvre la leçon, on fait l'appel — et l'appel fait, les entrées de la
séance s'ouvrent : organiser les rencontres, composer des équipes, lancer l'échauffement, lancer
une situation, saisir les matchs.

**Dans un cycle de duel, tout part de l'onglet Rencontres** : c'est là que vivent les poules, les
ligues et les défis. Dans un cycle collectif, ce sont les onglets Équipes et Matchs qui s'affichent
à la place. L'échauffement, les situations, la banque, le kiosque et l'évaluation sont communs aux
deux familles.

**Contraintes** (élèves à séparer ou à garder ensemble), **Statistiques** (niveau des élèves,
évaluation, qualité des données) et **Réglages** vivent en dehors de la séance : on y passe
une fois de temps en temps, pas chaque semaine.

**Situations** est la banque : une bibliothèque de situations toutes prêtes, indépendante des
classes et des leçons (voir plus bas).

La liste des leçons est **entièrement cliquable** : une ligne suffit pour rouvrir une leçon
passée ou une leçon préparée à l'avance. Cliquer sur « 2. Leçons » dans le menu ramène
toujours à cette liste.

### Présences

Tout le monde est **présent par défaut**. On touche simplement le nom de l'élève pour le
faire changer d'état :

| Clic | État | Fond |
|---|---|---|
| — | présent | vert |
| 1 | absent | rouge |
| 2 | blessé / dispensé | orange |
| 3 | retour à présent | vert |

Un élève marqué blessé reçoit un menu « rôle » (arbitre, observateur, secrétaire, coach)
sur une deuxième ligne, pour que la ligne du nom reste entièrement cliquable. C'est le moyen
le plus simple de collecter des statistiques de match : les dispensés tiennent la tablette
pendant que les autres jouent.

**Et comme il ne joue pas, aucun score ne le concerne : son indice resterait figé toute la séance.**
Le bouton **« Apprécier son rôle »**, sous le menu de rôle, ouvre une appréciation directe sur les
quatre critères — à reprendre / rien / à valoriser. Un arbitre juste, un observateur rigoureux, un
coach qui fait progresser son équipe font du travail d'EPS : cela compte, au titre de l'observation
enseignante (dont tu règles le poids dans Réglages → Pondération des sources). Une appréciation
laissée vide ne compte pas, et se retire d'un clic.

**L'équipe des Dispensés.** Dans l'onglet Équipes, les élèves blessés ou dispensés forment une équipe
à part, en jaune, à côté des autres — avec leur rôle et leur bouton « Apprécier » à portée de main.
Elle n'existe que pour toi : elle n'est dans aucun appariement, donc ni le tournoi, ni les
confrontations d'échauffement, ni les relevés ne peuvent l'atteindre. **Un élève déclaré blessé après
la composition des équipes en sort automatiquement** : il garde sa place pour son retour, mais ne
reçoit plus les relevés collectifs, ni le fair-play de match, ni rien de ce qui se joue sans lui.
Son indice n'évolue alors que par l'appréciation de son rôle. Dès qu'il repasse « présent »,
il retrouve son équipe et tout redevient normal.

Le bouton « Reprendre la leçon précédente » évite de tout ressaisir chaque semaine.

### Rencontres : poules, ligues et défis

Le cœur du site. Trois façons d'organiser un affrontement en un contre un, choisies d'un bouton en
haut de l'onglet. Le **nombre de terrains** (les courts disponibles) se règle juste à côté : c'est
lui qui décide du nombre de rencontres simultanées, donc du découpage en tours.

**Changer de mode n'efface rien.** Chaque mode garde sa mise en place dans son tiroir : on peut
aller voir les défis au milieu d'un tour de poules, revenir, et retrouver ses groupes, ses
rencontres et ses scores exactement où on les avait laissés. Un badge sur le bouton rappelle ce que
les autres modes ont en réserve (« Défis · 12 renc. »). Une fausse manœuvre en pleine leçon ne coûte
plus qu'un clic pour revenir.

#### Poules

Un groupe où **tout le monde rencontre tout le monde**. « Composer les groupes » demande le nombre
de poules (ou le nombre d'élèves par poule), puis **deux réglages indépendants** — voir
« Niveau et sexe » ci-dessous.

**Trois élèves par groupe au minimum.** Si le découpage demandé donnait des duos — 12 poules pour
25 élèves —, l'application réduit le nombre de groupes et te le dit : une poule de deux, c'est une
seule rencontre et beaucoup d'attente.

**« Remodeler à la main »** ouvre la composition, avec **deux gestes au choix** :

- **toucher l'élève, puis le groupe** où l'envoyer — le geste qui marche partout, y compris à la
  souris ;
- **rester appuyé sur l'élève et le faire glisser** jusqu'au groupe. Une pastille suit le doigt, le
  groupe survolé s'allume, on lâche. L'appui s'arme en deux dixièmes de seconde : sans ce délai, le
  moindre effleurement en faisant défiler la liste emporterait un élève ailleurs. À la souris, un
  déplacement franc suffit et le délai ne se sent pas. Lâché dans le vide, l'élève reste simplement
  sélectionné — rien n'est perdu.

Les noms se modifient sur place, on ajoute ou retire un groupe, « Répartir ceux qui restent » place
les non-affectés dans les groupes les plus creux. Tu connais des choses que les indices ignorent —
une inimitié, un retour de blessure, deux élèves qui progressent mieux ensemble. Les rencontres
devenues impossibles (deux élèves désormais séparés) disparaissent toutes seules.

« Générer les rencontres » construit le calendrier par la méthode du carrousel : dans une poule de
`n`, il faut `n−1` tours, personne ne joue deux fois dans le même tour, et les poules tournent en
parallèle. S'il y a plus de rencontres simultanées que de courts, le tour se découpe et chaque
rencontre reçoit son numéro de terrain.

**« Nouvelles rencontres »** sert quand les élèves ont fini avant la fin de l'heure. Le même geste
que « Nouvelle situation » ou « Nouvel échauffement » : une fenêtre demande **avec qui**, **combien
de rencontres par élève**, et si l'on veut **uniquement des adversaires jamais rencontrés**.

Trois façons d'apparier :

- **une revanche dans sa poule** — on rejoue dans le même groupe, en priorité contre ceux qu'on a
  le moins vus ;
- **croiser les poules, à place comparable** — le 2ᵉ d'une poule contre le 2ᵉ d'une autre : même
  statut, même enjeu, et la rencontre a du sens pour les deux ;
- **croiser les poules, à indice proche** — des rencontres serrées, quelles que soient les places.

**Croiser ne prend que les élèves qui ont fini leurs rencontres** — ceux qui tournent en rond
pendant que les autres jouent encore. La fenêtre indique combien ils sont. Ces rencontres
n'appartiennent à aucune poule : elles s'affichent dans une carte **« Rencontres supplémentaires »**
et **ne comptent dans aucun classement de poule**, pour ne pas fausser une montée. Elles
nourrissent bien sûr les indices, comme toute rencontre jouée, et l'arbitre peut y venir de
n'importe quelle poule.

#### Les élèves qui ont fini enchaînent sans t'attendre

Une poule de quatre finit en trois tours ; une poule de sept, non. Les premiers libérés n'ont alors
rien à faire, et c'est précisément le moment où une leçon se délite. Tu n'as pas à traverser le
gymnase pour relancer : **la tablette le fait**.

Dès qu'un élève n'a plus de rencontre en attente, son écran affiche « Tu as fini tes rencontres » et
lui propose les camarades **qui ont fini aussi** — donc au même stade que lui. Il touche un prénom,
ils jouent, ils reviennent saisir le score. Sur l'écran d'accueil du kiosque, chaque prénom porte
d'ailleurs sa mention : « 2 à jouer » ou « a fini », ce qui suffit à se trouver.

Le cadre reste le tien, dans la même fenêtre « Nouvelles rencontres », section **« Quand un élève a
fini, sans t'attendre »** :

| Réglage | Ce qu'il change |
|---|---|
| **Les élèves peuvent enchaîner eux-mêmes** | actif par défaut. Décoché, la tablette dit seulement « bravo, va arbitrer ou passe la tablette » |
| **Contre qui, en priorité** | une **place comparable** dans sa poule (le 2ᵉ avec le 2ᵉ) ou un **indice proche** |
| **Rencontres supplémentaires par élève** | 0 pour ne pas limiter. Deux ou trois suffisent souvent à finir l'heure |
| **Accepter un adversaire de sa propre poule** | si personne d'autre n'a fini. Une autre poule est toujours proposée en premier |

Un élève déjà reparti jouer n'est jamais proposé, et la règle est revérifiée au moment du clic : si
le camarade vient d'être pris, la tablette le dit et en propose un autre. « **Personne d'autre n'a
encore fini** » est aussi une réponse claire — passe la tablette, reviens dans deux minutes.

De ton côté, un bandeau vert liste les prénoms de **ceux qui ont fini** : c'est l'information qu'on
cherche des yeux au milieu du gymnase. Le bouton « Nouvelles rencontres » est juste à côté, si tu
préfères apparier toi-même.

L'application apparie d'abord ceux qui ont le moins joué. Rien n'est effacé : les rencontres prévues
ou déjà jouées restent, les nouvelles s'ajoutent à la suite. Avec la case « jamais rencontrés », un
élève qui a déjà vu tous ses adversaires possibles passe son tour plutôt que de rejouer le même
match.

Le classement se calcule tout seul : **victoire 3 points, défaite jouée 1 point** — se déplacer et
jouer rapporte déjà quelque chose — puis la différence de points départage. « Ajouter une
rencontre » permet de rattraper un cas particulier sans refaire le calendrier.

#### Niveau et sexe : deux réglages indépendants

La même fenêtre compose les poules **et** les ligues, avec deux listes qui ne se commandent pas
l'une l'autre. Ton choix est mémorisé et repropose à la composition suivante.

**Niveau**

- **Par niveau** — les élèves proches se retrouvent ensemble, les rencontres sont serrées. En
  ligues, c'est l'ordre du classement : Ligue 1 pour les plus à l'aise, puis Ligue 2, Ligue 3.
- **Peu importe** — répartition en serpentin : chaque groupe ressemble à la classe, un fort, un
  faible, et ainsi de suite. Y compris en ligues : rien n'oblige à partir du niveau, et une ligue
  mélangée où la montée-descente se gagne au mérite est un format qui se défend.

**Sexe**

- **Peu importe** — aucune contrainte, c'est le niveau (ou le hasard du serpentin) qui décide.
- **Groupes non mixtes** — filles entre elles, garçons entre eux. Le nombre de groupes se partage
  au prorata de l'effectif, chaque côté gardant ses trois élèves minimum. Les groupes s'appellent
  alors « Ligue filles 1 », « Ligue garçons 1 », « Poule filles A »…
- **Mixité équilibrée** — chaque groupe reçoit sa part de filles et sa part de garçons, la consigne
  de niveau s'appliquant à l'intérieur de chaque genre.

Quand un seul genre est présent, la consigne de mixité est sans objet : l'application compose
normalement et te le dit dans le message de confirmation.

En ligues non mixtes, **les deux échelles sont cloisonnées** : une fille ne monte pas dans une ligue
de garçons. Les flèches ↑ ↓ et les mouvements proposés restent à l'intérieur de leur échelle, et la
flèche est grisée en haut et en bas de chacune.

Dans tous les cas, « Remodeler à la main » reste le dernier mot : la composition automatique est une
proposition, pas une décision.

#### Ligues

Les mêmes poules, mais **ordonnées et cloisonnées** : **on ne rencontre que les élèves de sa
ligue.** C'est le format qui fait progresser un cycle entier : chacun joue contre des adversaires à
sa mesure, et la ligue devient un objectif.

Les montées et les descentes sont **à ta main**. L'application classe, puis propose — « ↑ Léa →
Ligue 1 », « ↓ Tom → Ligue 3 » — en prenant le premier et le dernier de chaque ligue. Rien ne bouge
tant que tu n'as pas cliqué : une montée se décide aussi sur ce que tu as vu du match, pas seulement
sur le tableau. Les flèches ↑ ↓ de chaque ligne du classement font le même travail, élève par élève,
et « Tout appliquer » prend la proposition en bloc quand elle te convient.

#### Défis

Une **échelle**, comme un classement de tournoi. Chacun choisit son adversaire — dans les limites
que tu as posées. « Règles des défis » ouvre tous les leviers, et ce sont eux qui font la différence
entre une cohue et une situation d'apprentissage :

| Réglage | Ce qu'il change |
|---|---|
| **Un élève peut défier…** | un élève **mieux classé** que lui (l'échelle classique : on monte en battant plus fort) · un élève **de niveau proche**, au-dessus ou en dessous (des matchs serrés dans les deux sens) · **n'importe qui** (confrontation libre) |
| **Écart maximum** | en nombre de rangs. 3 signifie « les trois places au-dessus » : on ne défie pas le premier quand on est dixième |
| **Défis par élève et par séance** | 0 pour ne pas limiter. Trois défis, c'est une séance bien remplie |
| **Jamais deux fois le même adversaire** | force le brassage, et rend les indices plus justes puisque chacun est mesuré face à des joueurs différents |

**Et surtout, la conséquence d'une victoire** — c'est elle qui donne son caractère à la situation :

| Conséquence | Ce que ça produit dans la classe |
|---|---|
| **Le vainqueur prend la place du perdant** | l'échelle classique. Chaque défi peut renverser l'ordre : c'est vif, lisible, et un peu brutal pour celui qui redescend |
| **Le vainqueur monte de N rangs** | la progression est plus douce : battre le troisième quand on est dixième ne fait pas de vous le troisième. Le perdant recule d'autant |
| **Classement aux points** | victoire, défaite jouée, et **bonus par rang d'écart** : battre un élève trois places au-dessus rapporte trois fois le bonus. Un plafond est réglable. On récompense la prise de risque sans renverser l'ordre à la première victoire — et jouer sans gagner rapporte quand même |
| **Rien ne change au classement** | les défis restent des matchs libres. Utile quand tu veux du volume de jeu sans enjeu de classement |

En mode « aux points », un tableau **Classement aux points** s'ajoute sous l'échelle, et la tablette
annonce à l'élève son total avec la même logique : « battre plus fort que toi en rapporte davantage ».

L'échelle de départ suit l'ordre des indices — c'est ce qui donne les premiers défis les plus
équilibrés — et les flèches ↑ ↓ permettent de la rebattre à la main. « Refaire l'échelle » la
reconstruit à partir des indices du moment, sans effacer les défis déjà joués.

**Pour lancer la situation, un seul bouton : « ▣ Lancer les défis ».** Il ouvre le kiosque des
élèves dès que deux élèves sont présents — tu n'as rien à créer d'abord. Tu passes la tablette,
chaque élève se désigne, choisit un adversaire parmi ceux que les règles autorisent, joue, et saisit
son score. Le bouton « Lancer un défi à la main » reste là pour rattraper un cas particulier depuis
ton écran, mais ce n'est pas le chemin normal.

Un tableau montre, pour chaque élève, son rang, ses défis joués, ses victoires, et **qui il peut
défier** — pratique pour repérer d'un coup d'œil celui qui n'a plus personne à affronter.

#### Les élèves saisissent eux-mêmes

Le bouton violet ouvre le **mode kiosque** de l'onglet. L'élève touche son prénom, et ne voit que
ce qui le concerne : sa poule ou sa ligue, ses rencontres à jouer avec leur tour et leur terrain,
son classement — ou, en mode défi, son rang et **la liste des adversaires que les règles
autorisent**. Impossible de se tromper : ce qui est interdit n'est pas proposé.

La saisie du score se fait à deux gros boutons `+ 1` et `−`, un par joueur, puis « Valider ». Quand
un défi renverse l'échelle, la tablette le dit : « tu prends la place de ton adversaire ».

**Les deux fiches sont jumelles** : même largeur, mêmes gabarits de boutons, et les compteurs
observés (fautes directes, services ratés, ce que tu as choisi de relever) s'affichent en vignettes
alignées, libellé au-dessus. C'est vrai sur l'écran de l'ordinateur comme sur la tablette — sur un
téléphone, les deux fiches passent l'une sous l'autre. Deux élèves qui saisissent côte à côte
doivent voir exactement la même chose, sinon on doute de ce qu'on lit.

#### Ce qu'on observe pendant une rencontre

Le bouton **« Relevés et bonus »** ouvre ce qui se compte, et c'est propre à la leçon : une séance
centrée sur le jeu au filet ne relève pas la même chose qu'une séance sur le service.

- **Les critères observés** sont des compteurs — points gagnants, fautes directes, montées au filet,
  ce que tu veux ajouter. Chacun peut être **relié à un critère d'évaluation** : le relevé nourrit
  alors l'indice de l'élève, exactement comme les relevés de match d'un sport collectif. Sans
  critère relié, il reste un comptage — ce qui est déjà utile pour en parler avec l'élève.
- **Les actions bonus** ajoutent des points au score : « smash gagnant après déplacement = 2 points »
  valorise une intention de jeu sans changer les règles du badminton. Sur la tablette, le bouton
  ambré ajoute directement ses points ; dans ta saisie, le score reste celui que tu tapes et les
  bonus ne sont que comptés.

En kiosque, l'élève retrouve sous son score les boutons bonus et les compteurs à incrémenter : tout
se saisit au doigt, sans clavier.

#### Qui a arbitré ?

Sous le score, la tablette demande **qui a arbitré la rencontre** : « Pas d'arbitre », ou un ou
plusieurs camarades du groupe. Ce sont ceux qui étaient là qui le déclarent, et l'information
remonte sur ta carte (colonne « Arbitre ») comme dans le dossier de séquence.

En CA4, tenir le rôle d'arbitre fait partie de ce qu'on évalue : ces arbitrages **comptent dans le
critère de fair-play**, modérément et plafonnés — déclarer trois arbitrages ne fait pas un dixième
de moyenne, mais l'élève qui s'en charge sans qu'on le lui demande n'est plus invisible.

#### Le fair-play, aussi dans les rencontres

Le bandeau de fair-play, déjà présent sur les échauffements et les situations qui visent ce critère,
existe maintenant **sur les rencontres** : « Rien à signaler » par groupe ou pour tout le monde, et
« Ajuster individuellement » pour distinguer ceux qui ont tenu un rôle exemplaire — arbitrage
compris — et reprendre ceux qu'il a fallu reprendre. Même barème que partout ailleurs.

#### Ce que les rencontres alimentent

- **Le score** nourrit l'indice global, par la « surprise » : battre un élève mieux classé que soi
  rapporte davantage que battre un élève moins bien classé, et perdre contre plus fort coûte peu.
  C'est ce qui empêche le classement de récompenser le simple fait de choisir des adversaires
  faibles.
- **Les relevés** — points gagnants, fautes directes, services ratés — sont facultatifs et se
  saisissent dans la fenêtre du score, joueur par joueur, quand une rencontre a été observée. Eux
  alimentent les critères : efficacité, volume de points gagnants, fiabilité au service.

### Équipes

- **Reprendre les équipes de la leçon précédente** en un bouton : les **absents et les blessés
  du jour** sont retirés, les élèves de retour retrouvent leur équipe, les nouveaux venus sont
  placés dans la moins fournie. Un message récapitule ce qui a changé (« 5 absents retirés ·
  7 blessés retirés · 1 élève replacé »). C'est le moyen le plus rapide d'avoir des équipes
  stables d'une semaine à l'autre.
- **Toute équipe tombée sous 4 joueurs est signalée par un fond bleu clair**, avec l'étiquette
  « effectif à compléter » et un rappel sous les équipes. C'est le cas typique après le retrait
  des absents : on voit immédiatement où déplacer quelqu'un.
- **3 à 9 équipes**, **2 à 7 élèves** par équipe. Tu fixes soit le nombre d'équipes,
  soit la taille : l'autre valeur se déduit des présents, avec alerte si la combinaison
  est impossible.
- **Deux modes de composition**, à croiser librement avec la mixité :

| Mode | Ce que ça donne | Quand s'en servir |
|---|---|---|
| **Équilibré** | équipes de force égale entre elles, mélangeant les niveaux en leur sein | matchs équilibrés, entraide entre élèves |
| **Niveau** | équipes homogènes en leur sein, **appariées deux à deux** de force équivalente | travail différencié ; conseillé avec un **nombre pair** d'équipes, pour que chacune ait un adversaire à sa mesure |

  En mode Niveau, les équipes 1 et 2 sont les plus fortes et se valent, les 3 et 4 viennent
  ensuite, et ainsi de suite. Avec un nombre impair, la dernière équipe n'a pas de jumelle :
  l'application le signale.
- **Mixité** : équipes mixtes équilibrées, équipes non mixtes, ou sans contrainte —
  choix libre à chaque leçon, et combinable avec les deux modes ci-dessus.
- **Stabilité** (curseur 0 → 100) : à 100, on ne touche qu'au strict nécessaire par rapport
  à la leçon précédente (les absents sortent, les revenants réintègrent leur équipe) ;
  à 0, rebrassage complet.
- **Contraintes** de la classe (élèves à séparer, élèves à garder ensemble) toujours prioritaires.
- Déplacement manuel : glisser-déposer à la souris, ou **touche un élève puis touche
  l'équipe d'arrivée** sur tablette. Les indicateurs se recalculent en direct.
- **Couleur de chasuble** : la pastille ronde à droite du nom d'équipe ouvre une palette de
  douze couleurs. On choisit celle du jeu de chasubles réellement distribué ; le nom de
  l'équipe suit la couleur (« Bleue », « Rouge »…), et un point signale les couleurs déjà
  portées par une autre équipe. Le champ « nom affiché » reste là si tu préfères un autre
  intitulé. La couleur se retrouve partout : cartes d'équipe, tableau des matchs, classement,
  écran kiosque, feuille imprimable.
- « Affichage à projeter » ouvre une vue plein écran imprimable.

### La banque de situations (onglet « Situations »)

Préparer une situation avec ses paliers, ses seuils, ses messages et ses images prend du temps.
La banque évite de recommencer : une fiche s'y range une fois, et se réutilise autant de fois
qu'on veut.

- **« Copier dans la banque »** sur n'importe quelle fiche de leçon — échauffement comme situation,
  paliers comme confrontation — l'y enregistre sans ses scores. La fiche de la leçon continue sa vie
  de son côté. Si elle venait déjà de la banque, on choisit entre mettre la fiche d'origine à jour
  ou en créer une variante à côté.
- **Des dossiers** regroupent les variantes d'un même exercice : « Passe à 10 » à 5 m, à 8 m, en
  mouvement. Le bouton « Nouveau dossier » en crée un ; le menu **Dossier** de chaque ligne y range
  une fiche (avec l'entrée « ＋ Nouveau dossier… » pour en créer un sans quitter la page) ; et la
  fenêtre « Copier dans la banque » permet de choisir le dossier, ou d'en créer un au passage.
  **Dupliquer** crée une variante dans le même dossier, prête à être ajustée.
- **Une fiche peut vivre dans plusieurs dossiers à la fois.** Un passe à 10 est un échauffement *et*
  un travail de progression du disque : plutôt que d'en faire deux copies qui divergeront, la même
  fiche est rangée dans les deux. La colonne **Dossier** montre ses rangements sous forme
  d'étiquettes — la croix en retire un — et le menu « ＋ aussi dans… » l'ajoute ailleurs, sans jamais
  proposer un dossier qu'elle occupe déjà. C'est toujours **la même fiche** : la modifier depuis l'un
  des dossiers la met à jour dans tous. Pour obtenir une vraie variante à ajuster séparément, c'est
  **Dupliquer** qu'il faut.
- **Les dossiers se rangent les uns dans les autres**, jusqu'à quatre niveaux : « Ultimate » peut
  contenir « Passe à 10 », qui contient « à 5 m » et « en mouvement ». Le bouton **« + sous-dossier »**
  du bandeau crée un dossier à l'intérieur, et le menu de rangement d'une fiche affiche l'arbre
  complet (`Passe à 10 › à 5 m`). Chaque bandeau annonce ce qu'il contient, sous-dossiers compris.
- **Un clic sur le bandeau ouvre ou referme le dossier** — avec ses sous-dossiers. L'état est
  mémorisé : il survit aux allers-retours entre les pages et au rechargement. Les boutons
  « Tout replier » / « Tout déplier » traitent la banque entière d'un coup.
- Supprimer un dossier ne supprime jamais son contenu : ses fiches et ses sous-dossiers **remontent
  d'un cran**, dans le dossier parent — ou dans « Sans dossier » s'il était à la racine. Une fiche
  rangée ailleurs par ailleurs garde simplement ses autres dossiers.
- **« Ajouter à la leçon »** insère une copie dans la leçon ouverte, et propose au passage
  **d'ajuster les critères alimentés** : la même situation peut servir la Technique cette semaine
  et la Défense la suivante, sans toucher à la fiche d'origine.
- La copie repart avec des paliers neufs : les messages reçus lors d'une leçon précédente ne se
  mélangent pas avec ceux du jour. Les oppositions et les équipes d'une confrontation ne sont jamais
  mises en banque : elles dépendent des présents du jour.
- La banque s'**exporte et s'importe** en un fichier JSON, dossiers compris, pour l'échanger avec un
  collègue. À l'import, un dossier du même nom est réutilisé plutôt que dupliqué.

### Échauffement et situations : deux onglets, deux formats

La leçon sépare **Échauffement** et **Situations**. Le fonctionnement est exactement le même — les
deux familles vivent simplement dans deux onglets différents, et la banque les range séparément
(filtre « Échauffements » / « Situations d'apprentissage »).

**Dans les deux cas, la fiche se mène de trois façons, au choix.** Le menu « Comment se mène cette
situation ? » est la première question posée à la création.

| Format | Ce que font les élèves | Exemples |
|---|---|---|
| **Par paliers** | groupes de travail, paliers, seuils, score saisi, retour automatique différencié | maximum de passes en 1 minute, montée de disque chronométrée, 3 contre 2 défensif |
| **En confrontation** | deux équipes s'opposent, chacune note son score, le vainqueur s'affiche tout seul | passe à 10, déménageur, gagne-terrain, épervier |
| **En co-frontation** | deux élèves coopèrent pour atteindre un objectif, marquent des points ensemble, puis changent de partenaire | partenaire en or, 15 passes en 3 essais |

Un échauffement peut donc être une simple opposition, et une situation d'apprentissage peut l'être
aussi : un gagne-terrain est un vrai contenu d'apprentissage, pas une mise en route.

**Un exercice n'est pas enfermé dans sa famille.** Le menu « ⋯ » de chaque carte propose « Déplacer
vers Situations » (ou vers Échauffement) : la fiche change d'onglet avec ses paliers, ses scores et
ses groupes. Et depuis la banque, la fenêtre « Ajouter à la leçon » demande dans quel onglet insérer
la copie. Le même passe à 10 met en train le lundi et devient un contenu d'apprentissage le jeudi.

**Les fiches se réordonnent** dans la leçon : les flèches ↑ ↓ de chaque carte la déplacent dans sa
liste, sans toucher à l'autre onglet. L'ordre affiché est celui du déroulement prévu — pratique quand
on prépare la séance la veille et qu'on intercale une situation le matin même.

En format **confrontation**, le bouton « Opposer les équipes » ouvre une fenêtre en deux temps.

**1. Quelles équipes s'affrontent ?** Soit les équipes de la leçon, soit **des équipes composées pour
ce seul échauffement**. Un échauffement n'a pas les mêmes contraintes qu'un match d'ultimate : rien
n'oblige à jouer un déménageur à quatre équipes de sept parce que le tournoi se joue comme ça. Tu
retrouves donc ici les mêmes réglages que dans l'onglet Équipes — nombre d'équipes ou taille des
équipes, composition équilibrée ou par niveau, mixité — et le bouton « Composer les équipes » les
tire à partir des élèves **présents du jour**, avec les contraintes de la classe. La composition
s'affiche aussitôt, nom par nom ; un second clic rebrasse. **Les équipes de la leçon ne sont jamais
modifiées** : les matchs d'ultimate gardent les leurs. Les équipes propres à l'échauffement restent
attachées à la fiche, sont rappelées sur la carte et servent aussi bien à ta saisie qu'à celle des
élèves sur tablette.

**2. Qui affronte qui ?** *Un tour simple* (chaque équipe joue une fois), *toutes contre toutes*, ou
*je choisis les affiches équipe par équipe* — on part du tournoi complet et on décoche ce qu'on ne
veut pas. Un aperçu montre, avant de valider, le détail **tour par tour** des oppositions.

**Les confrontations acceptent des bonus**, comme les matchs d'ultimate : « marquer après trois
passes sans perte = 3 points ». Ils se définissent dans la fiche, s'affichent en ambré avec une
étoile à côté du bouton `+ 1` sur la tablette, et rapportent leurs points au score de l'équipe.

Le champ **Terrains disponibles** décide du nombre d'oppositions simultanées : deux par défaut, mais
un déménageur peut tourner sur quatre petites aires pendant qu'un passe à 10 n'en occupe qu'une.
L'application ne promet jamais plus de terrains que le nombre d'équipes ne permet d'en remplir, et
le dit (« 5 équipes ne remplissent que 2 terrains »). **Les équipes en trop attendent leur tour —
jamais les mêmes** : le planificateur fait passer en premier celles qui ont le moins joué.

Il essaie plusieurs ordres de passage et garde le meilleur : de trois à neuf équipes, en « toutes
contre toutes », il atteint le nombre de tours minimal et répartit l'attente à une fois près. Cinq
équipes sur deux terrains donnent dix oppositions en cinq tours ; six équipes sur trois terrains,
quinze oppositions en cinq tours de trois. Les équipes au repos sont nommées sur ta fiche comme sur
la tablette des élèves.

C'est le même planificateur qui organise le tournoi d'ultimate — avec le nombre de terrains de la
leçon.

Chaque opposition reçoit deux scores, saisis par toi dans le tableau ou par les élèves en mode
kiosque (deux gros boutons `+1` par équipe). Ni palier, ni unité, ni groupe de travail :
l'éditeur masque tout ce qui ne sert pas.

**Ce que le résultat alimente** : l'écart relatif entre les deux scores — `(nous − eux) / total`,
donc indépendant du barème du jeu — nourrit les critères que tu as cochés, à l'échelle de l'équipe,
avec la même dilution que les relevés collectifs de match (il ne distingue pas les joueurs entre eux).
**Ce résultat n'entre pas dans le classement de la leçon** : un échauffement n'est pas une rencontre
officielle. Si tu préfères un échauffement purement qualitatif, ne coche aucun critère : la fiche
sert alors de simple rappel de consigne à projeter.

Créer une fiche dans l'onglet Échauffement la marque comme échauffement ; une fiche prise
dans la banque revient dans l'onglet dont elle vient, avec son format. Les oppositions, elles,
ne sont jamais mises en banque : elles dépendent des équipes du jour.

#### La co-frontation : coopérer *et* se classer

Troisième format, pour les situations comme pour les échauffements. **Deux élèves coopèrent pour
atteindre un objectif en un nombre d'essais limité. Réussi ou raté, le duo marque des points — c'est
ce qui permet de se classer — puis chacun repart chercher un autre partenaire.** L'exemple type,
« partenaire en or » : **15 passes en 3 essais**, *10 points* si c'est réussi, *1 point* sinon.

Le mot dit l'intention : on est en coopération sur le terrain et en confrontation au tableau. Aucun
élève ne peut gagner seul, personne n'a intérêt à éviter les plus fragiles — et pourtant tout le
monde a une raison de s'appliquer. C'est aussi la raison pour laquelle **l'échec rapporte rarement
zéro** : essayer avec un partenaire difficile doit rapporter quelque chose, sans quoi le classement
punit exactement ce qu'on cherche à encourager.

Quatre réglages, dans la fiche :

- **l'objectif** (15) et **l'unité**, celle de la fiche — passes, réceptions, aller-retours ;
- **les essais autorisés** (3) : un duo a droit à l'erreur avant d'annoncer son résultat ;
- **le barème** : points si l'objectif est atteint, points s'il ne l'est pas ;
- **la taille du groupe** : binôme, trinôme, quatuor… jusqu'à six. Un objectif à trois ne se règle
  pas comme à deux : pense à relever l'objectif en même temps ;
- **« Interdire de refaire un groupe déjà formé »** : coché, deux élèves qui ont déjà coopéré ne
  peuvent plus se retrouver ensemble. Ni ta saisie ni la tablette ne l'acceptent — les camarades
  déjà rencontrés s'éteignent à l'écran. Dans un trinôme, c'est **chaque paire** du groupe qui
  compte : deux élèves qui ont déjà travaillé ensemble ne peuvent pas se retrouver dans le même
  trio. C'est ce qui force le brassage, et c'est aussi ce qui rend les indices plus justes,
  puisque chacun est alors mesuré avec des partenaires différents ;
- **la condition de fin** : *après un nombre de coopérations* par élève (4, 6…), *dès qu'un élève a
  coopéré avec toute la classe* — c'est une **course au tour complet**, le premier à avoir fait le
  tour arrête la situation, et l'objectif se calcule sur les présents du jour — ou *au bout d'un
  temps donné*, auquel cas rien ne s'arrête tout seul : c'est ton chrono qui décide.

En course au tour complet, ce sont les **camarades différents** qui comptent : refaire deux fois le
même duo rapporte des points, mais ne fait pas avancer d'une case. La carte affiche « Camarades vus »
et dit qui mène la course.

**Et dans tous les cas, tu arrêtes la situation quand tu veux**, d'un bouton sur sa carte. Le
classement se fige, la tablette affiche le classement final et n'accepte plus de manche, « Relancer »
rouvre tout sans rien effacer. Quand c'est la règle qui a arrêté la situation — un élève a fait le
tour, ou chacun a mené ses coopérations — le bouton devient « **Poursuivre quand même** » : le
vainqueur est annoncé, sur ta carte comme sur la tablette, et les autres finissent leur tour.

La carte affiche les règles en clair, le **classement** (points, coopérations réalisées sur celles
demandées, réussites, jauge d'avancement) et, en dessous, **qui n'est pas encore entré en jeu** —
c'est le seul tableau de bord utile en cours de séance. Le bouton « Saisir une manche » permet la
saisie enseignant : deux élèves, réussi ou raté, et au besoin le meilleur essai. Si les deux élèves
choisis ont déjà coopéré ensemble, l'application le signale sans l'interdire.

**En mode kiosque, les élèves se débrouillent seuls** : ils se désignent dans la liste (leurs points
et leurs coopérations sont affichés à côté de chaque nom, ce qui suffit à trouver quelqu'un qu'on n'a
pas encore rencontré), valident, annoncent « Objectif atteint » ou « Pas cette fois », lisent le
retour en vert ou en orange, et repartent. Un bouton « Voir le classement » ouvre le tableau complet.

**Ce que le résultat alimente** : chaque manche est une tentative ordinaire, à autant de membres que
le groupe en compte et à valeur égale aux points marqués. À une différence près, et elle est
importante : les points d'une co-frontation ne sont **pas** normalisés par rapport à la classe comme
le serait un nombre de passes. Objectif atteint vaut `+1`, manqué vaut `−1`, quel que soit le barème
choisi (10/1 ou 3/0, même effet). Sans cela, une séance où tout le monde réussit n'aurait aucun écart
à mesurer — donc aucun effet sur les indices, ce qui serait absurde pour une séance entière de
travail réussi. Elle passe donc par le même moteur que les
situations à paliers — la régression départage les élèves qui réussissent souvent de ceux qui
réussissent peu, en tenant compte des partenaires rencontrés — et nourrit les critères cochés sur la
fiche. D'où l'importance du brassage : plus les groupes changent, plus la part de chacun est
mesurable.

**Une co-frontation fait donc bouger les indices**, au même titre qu'une situation à paliers. La
seule condition est qu'au moins un critère soit coché dans « Critères alimentés par cette
situation » : le format en propose un par défaut (Technique), à déplacer vers Défense ou Jeu en
progression selon ce que la tâche mobilise vraiment. Tant qu'aucun critère n'est coché, la carte
l'annonce en rouge — la fiche ne sert alors qu'à afficher la consigne et à classer. Et la **fiche
élève** garde la trace de tout : un tableau « Parcours en co-frontation » liste chaque manche, avec
qui, réussie ou non, et les points marqués.

#### Rattraper une co-frontation déjà menée

Sur la carte d'une co-frontation, entre « Arrêter » et les flèches, le bouton **« Saisie
rétro-active »** ouvre la liste des élèves présents : **un total de points par élève**, et c'est
tout. L'application reconstitue les manches à partir du barème de la fiche — 31 points avec un
barème 10/1, c'est trois réussites et un échec — puis les enregistre une par une, parce que c'est ce
que le classement, la fiche élève et le moteur d'indices savent lire.

Une seconde colonne, facultative, dit **sur combien de coopérations** ces points ont été marqués
(le réglage de la fiche s'applique par défaut). **Les partenaires ne sont jamais demandés** : on ne
les invente pas. Ces manches sont donc individuelles, les points reviennent à leur auteur seul, et
le classement marque ces élèves d'un discret « rétro » — utile pour se rappeler, trois semaines
plus tard, ce qui a été relevé en direct et ce qui a été rattrapé.

#### Rattraper une séance à paliers (et les groupes qu'on ne se rappelle plus)

Rien n'oblige à saisir pendant le cours. Crée la leçon **à sa vraie date** (« Nouvelle leçon » puis
le champ Date, ou « Modifier l'en-tête » ensuite), fais l'appel tel qu'il était, ajoute la situation,
puis utilise **« Saisie en série »** sur sa carte : une ligne par élève présent, son palier, son
score, et tout part d'un coup. Les lignes laissées vides ne sont pas enregistrées — pratique quand
seuls quelques élèves ont été relevés.

**Ne plus savoir qui était passé avec qui n'est pas un problème** : la saisie en série enregistre
chaque score comme une tentative **individuelle**. C'est même la situation la plus favorable pour le
calcul des indices — quand un score est partagé par un groupe, le moteur doit démêler la part de
chacun par régression ; un score individuel est attribué sans ambiguïté. Les groupes ne servent qu'à
deux choses : partager une mesure commune, et afficher les paliers à projeter. Ni l'un ni l'autre
n'a de sens après coup.

Deux détails qui comptent pour un rattrapage :

- les tentatives sont **horodatées à la date de la leçon**, pas au jour de la saisie, pour que la
  progression et l'historique restent justes (l'indice pondère les séances récentes) ;
- une case propose de **ne pas afficher les retours aux élèves**, cochée d'office quand la leçon est
  passée : les messages de palier sont calculés et enregistrés, mais marqués comme déjà lus — on
  n'affiche pas à un élève le retour d'une séance vieille de trois semaines.

Si tu te souviens des groupes et que la mesure était bien commune (un score pour deux), garde
« Saisir un score » et coche les élèves concernés : c'est là que le partage a un sens.

### Situations — critères travaillés et paliers

Une situation, c'est une tâche mesurable, rattachée à une leçon, qui alimente
**les critères que tu choisis** avec leur pondération. Exemple :

| Situation | Critères alimentés |
|---|---|
| Passe et va, 10 tentatives | Technique 100 % |
| Montée de disque sur 3 zones, chrono | Jeu en progression 80 % · Technique 20 % |
| 3 contre 2 défensif | Défense 100 % |

Technique et Jeu en progression se travaillent isolément ou ensemble : il suffit de monter
les deux curseurs. Un curseur à 0 veut dire que la situation ne dit rien sur ce critère.

Chaque situation se découpe en **paliers** ordonnés (par exemple 5 m, 8 m, 11 m).
Chaque palier définit deux seuils qui découpent le score en trois bandes :

| Score | Bande | Ce qui s'affiche à l'élève |
|---|---|---|
| < seuil bas | ◆ Critères de réalisation | ton message d'aide technique |
| entre les deux | ▶ Recommandation | placement, intention, consigne de jeu |
| ≥ seuil haut | ▲ Complexification | « recule de 3 mètres », etc. |

Pour **chacune des trois bandes** tu choisis librement ce qui arrive ensuite :
redescendre de deux paliers, redescendre d'un palier, rester, monter d'un palier,
ou **sauter deux paliers** d'un coup. Un élève qui explose l'objectif peut donc gagner
deux crans en une tentative, et un élève en difficulté redescendre là où il réussit.
L'application ne sort jamais des paliers existants.

**Les paliers sont colorés du orange au vert foncé** : le palier 1 tire vers l'orange, et plus on
monte, plus la couleur vire au vert profond. Le dégradé s'étale toujours sur le nombre de paliers
réellement définis — avec trois paliers comme avec sept, le premier est orange et le dernier vert
foncé. On retrouve cette couleur partout où un palier est nommé : la répartition de la classe, le
tableau des tentatives, les cartes de groupe, l'écran de choix du kiosque, le bandeau « nouveau
palier » après un score, et la feuille imprimable. De loin, dans un gymnase, la couleur suffit à
savoir où en est un groupe sans rien lire.

Chaque message accepte les **retours à la ligne** (pour lister des critères de réalisation)
et peut porter une **image** : schéma de placement, photo d'un geste, croquis de terrain.
L'image est réduite automatiquement avant d'être enregistrée.

La situation elle-même peut porter un **schéma du dispositif** — plots, zones, sens de
déplacement. Il apparaît sur sa fiche, sur la tablette au moment où le groupe se présente,
et sur la feuille imprimable des groupes.

**L'écran de rappel des messages est rangé par palier.** Quand un groupe se présente, la tablette
n'aligne plus les élèves les uns après les autres : elle forme un bloc par palier — orange pour le
premier, vert de plus en plus foncé à mesure qu'on monte, exactement les couleurs de l'écran de choix
du palier. Chaque bloc annonce en gros le palier et sa consigne, affiche les **prénoms en grosses
pastilles** (celles des messages non encore lus sont pleines), puis le message. Un message identique
pour tout le bloc n'est écrit qu'une fois ; s'ils diffèrent, chaque message porte le prénom des
élèves concernés. Les élèves qui vont travailler au même endroit lisent au même endroit.

**Le fair-play se relève aussi dans une situation.** Dès que la fiche vise le critère Fair-play
(curseur au-dessus de 0), un bandeau apparaît sous la carte : un bouton « Rien à signaler » par groupe
de travail — par équipe si la fiche est une confrontation —, un bouton « tout le monde » quand les
groupes sont nombreux, et « Ajuster individuellement » pour les exceptions, dans un sens comme dans
l'autre. C'est le même mécanisme que sur les matchs, avec le même poids. Un auto-arbitrage en 3 contre
3, le respect de la règle dans un déménageur, l'aide au partenaire en difficulté : cela s'observe en
situation autant qu'en match. Sans critère visé, rien ne s'affiche et rien n'est compté.

**Effacer une tentative efface tout ce qu'elle avait produit.** C'est le cas typique de la situation
qu'on essaie soi-même avant le cours, avec un score inventé : la croix rouge en bout de ligne, dans
« Dernières tentatives », retire la tentative **et** le palier atteint, la recommandation et le
message qui en découlaient. L'application rejoue les tentatives restantes dans l'ordre et reconstruit
l'état exact d'avant l'essai — les élèves retrouvent la recommandation qu'ils auraient eue. Un message
déjà lu par un élève reste marqué comme lu, et rien ne se rouvre sans raison.

Le bouton **« Effacer les résultats »**, en tête de fiche, fait le ménage d'un coup : toutes les
tentatives, tous les paliers atteints, toutes les recommandations. Il n'apparaît que s'il y a
quelque chose à effacer. Sur une fiche de confrontation, il efface les scores des oppositions en
gardant les appariements.

Le message s'affiche dès la saisie du score. **S'il est fermé par mégarde, il n'est pas perdu** :
il est mémorisé par élève, réaffiché au passage suivant en mode kiosque, et consultable
depuis la fiche de la situation. Au passage suivant, l'élève **choisit** son palier
(le palier conseillé est mis en avant) — l'application note s'il a suivi la recommandation,
ce qui donne un indicateur d'autonomie de la classe.

Les **groupes de travail** (2 à 8 élèves) se composent à la main, se reprennent des équipes,
ou se génèrent automatiquement en **maximisant le brassage** : le générateur évite de reformer
les paires déjà vues. C'est ce brassage qui rend possible l'estimation individuelle (voir §4).

On déplace un élève d'un groupe à l'autre en le touchant puis en touchant le groupe
d'arrivée, **sans limite de taille** : rien n'empêche de faire un groupe de 2 et un de 8.
Le bouton **« Afficher / imprimer »** produit une feuille propre, lisible de loin, avec pour
chaque groupe sa composition, son palier, sa consigne et des cases vierges pour noter
les scores à la main.

### Matchs

- **Les rencontres sont organisées en tours, à raison d'un match par terrain disponible.** Deux
  terrains par défaut, donc deux matchs simultanés ; le champ **Terrains** de la barre d'outils
  change cela en un geste, et le découpage en tours se refait aussitôt. Les équipes qui ne jouent
  pas pendant un tour sont affichées comme **observatrices** — ce sont elles qui tiennent les
  feuilles de relevés et arbitrent. Le tour de chaque match reste modifiable à la main ; si tu
  places dans un tour plus de matchs qu'il n'y a de terrains, le surnuméraire bascule au suivant.

  Le nombre de terrains se règle à trois endroits, du plus général au plus précis : **Réglages → Le
  gymnase** donne la valeur par défaut de toute l'application ; le champ **Terrains** de l'onglet
  Matchs (ou de « Modifier les relevés ») la redéfinit pour **cette leçon** ; la fenêtre d'une
  confrontation d'échauffement la redéfinit pour **cette fiche**. Le jour où le gymnase est coupé en
  deux, une seule case à changer.
- **Bouton « Modifier les relevés »** : tu choisis ce que les observateurs comptent, tu renommes
  les compteurs, tu les **ranges dans l'ordre** où tu veux les voir sur la tablette (flèches ↑ ↓),
  et tu décides lesquels **rapportent des points au score**. Si tu actives « Buts »
  avec 1 point, chaque but relevé met le résultat de la rencontre à jour immédiatement. La passe
  décisive, elle, est décochée par défaut : tu ne la relèves que si tu en as vraiment besoin.
- **Bonus par combinaison d'actions** : « trois passes puis but sans perte de disque = 5 points ».
  Ces boutons apparaissent sur **fond ambré, avec une étoile**, pour qu'on ne les confonde jamais
  avec un but ordinaire — ce sont eux qui rapportent gros.
- **Qui a arbitré, qui a observé.** Sous le fair-play de chaque match, le bouton **« Désigner »**
  ouvre trois listes : **arbitre central** (un seul), **arbitres de touche** et **observateurs**
  (autant que nécessaire). Chaque liste propose d'abord les élèves **au repos** — ceux qui ne jouent
  pas ce match, **blessés compris**, marqués d'un point : tenir un rôle reste une façon de
  participer. Sous un second intertitre viennent les élèves **des deux équipes** : une équipe plus
  nombreuse que le terrain a des remplaçants, et rien n'interdit à un remplaçant d'observer. Un
  élève ne tient qu'un rôle à la fois — le désigner ailleurs le retire du précédent.

  **Et le rôle s'apprécie, exactement comme le fair-play juste au-dessus.** À droite de
  « Modifier », un bouton **« Ajuster individuellement »** ouvre la liste des élèves désignés avec
  le même réglage à trois états : **−** (rôle bâclé, à reprendre), **r.à.s.** (rien à signaler,
  l'état par défaut), **+** (rôle remarquablement tenu). Tu ne renseignes que les exceptions :
  tenir le rôle compte déjà par lui-même. Si tu retires un élève d'un rôle, son appréciation
  disparaît avec — elle n'aurait plus d'objet.

  Les noms désignés s'affichent **juste en dessous de ces deux boutons**, groupés par rôle et
  portant leur mention (« central : Léa M. + · obs. : Tom B. ») — et se retrouvent
  dans le dossier de séquence imprimé, ligne « Arbitrage et observation ». **Le rôle tenu crédite le
  critère de fair-play et d'arbitrage**, modérément : c'est un engagement réel, pas une performance
  de jeu, et l'arbitre central pèse un peu plus que l'observateur. **Un rôle apprécié pèse deux fois
  plus** — dans un sens comme dans l'autre : à ce moment-là, tu as regardé et tranché, ce n'est plus
  la simple présence au sifflet. Un élève blessé qui arbitre bien toute l'heure n'a donc plus une
  leçon vide, et celui qui siffle en regardant ailleurs ne s'en tire pas mieux que les autres.
- **Réinitialiser une rencontre** efface son score, ses relevés, son fair-play et les rôles — cette
  action détruit du travail saisi par les élèves, elle demande donc **le code enseignant**, le même
  que pour sortir du kiosque.
- **Relevés de tous les matchs d'un tour en une seule fenêtre** : le bouton « Relevés des N matchs »,
  dans l'en-tête du tour, ouvre les rencontres du tour l'une sous l'autre — scores et compteurs. Les
  équipes observatrices rendent leur feuille en même temps, tu saisis tout d'un bloc et tu valides
  une fois. Un récapitulatif en bas montre en direct ce qui sera calculé (passes réussies, total
  des passes ratées interceptions comprises, pourcentage de réussite), pour repérer une erreur de
  relevé avant d'enregistrer.
- **Génération du tournoi, avec des choix** : le bouton « Générer le tournoi » ouvre une fenêtre
  d'options plutôt que de tout décider à ta place. Trois questions indépendantes.

  **Qui rencontre qui ?**

  | Formule | Effet |
  |---|---|
  | **Toutes contre toutes** | chaque équipe rencontre toutes les autres — le tournoi complet |
  | **Un tour simple** | chaque équipe joue une fois au plus : de quoi occuper une fin de séance |
  | **Je choisis les affiches équipe par équipe** | tu désignes toi-même les rencontres |

  Dans le troisième cas, tu sélectionnes une équipe et coches celles qu'elle doit rencontrer —
  avec « tout cocher » / « tout décocher » pour aller vite. Une affiche cochée d'un côté l'est
  forcément de l'autre : la Bleue contre la Verte, c'est la même rencontre que la Verte contre la
  Bleue. La liste des affiches retenues s'affiche en dessous, aux couleurs des équipes. On part du
  tournoi complet : on retire ce qu'on ne veut pas plutôt que de tout construire depuis une page
  blanche.

  **Combien de fois chaque affiche se joue-t-elle ?** — une fois (match aller seulement), deux fois
  (aller et retour), trois ou quatre. Au match retour, les deux équipes changent de côté sur la
  feuille, et tous les matchs aller se jouent avant d'entamer les retours.

  **Et deux cases à cocher** : *n'apparier que des équipes de même composition* — deux équipes non
  mixtes de sexe opposé ne se rencontrent pas, une équipe mixte rencontre tout le monde ; et
  *remplacer les matchs déjà créés*, à décocher pour ajouter des rencontres aux précédentes.

  L'option de composition n'apparaît que si la classe compte effectivement des équipes non mixtes
  des deux sexes — sinon elle n'aurait aucun effet, et l'application le dit ; elle disparaît aussi
  quand tu désignes les affiches toi-même, puisqu'elle agirait alors dans ton dos. Un **aperçu
  vivant** annonce, avant de valider, combien de matchs et combien de tours seront créés ; si les
  options choisies ne laissent aucune rencontre possible, il le signale au lieu de générer un
  tournoi vide.
- Ou match par match, à la main, en choisissant les deux équipes et le tour.
- **Barème propre à chaque match** : valeur du but ordinaire, plus autant d'actions bonus
  que tu veux (« but après passe dans le dernier tiers = 10 points »). Boutons de saisie rapide.
- **Classement automatique** de la leçon : **victoire 3 points, match nul 2, défaite 1**.
  Le point de participation récompense l'équipe qui joue même battue, ce qui évite de
  décrocher après deux défaites.
- **Trois comptages seulement**, par équipe (un observateur suffit) ou par joueur
  (plus précis) : **passes réussies**, **passes perdues**, **interceptions**. Rien de plus,
  pour que ce soit tenable par un élève pendant un match.
- **Une interception est automatiquement comptée comme une passe ratée pour l'adversaire.**
  L'observateur n'appuie donc que sur « interception » : l'application ajoute la passe ratée
  en face toute seule, sans double comptage. Le compteur « passes perdues » ne sert qu'aux
  pertes non interceptées — disque lâché, sorti du terrain, passe au sol. Un récapitulatif
  affiche en direct le total réel et le pourcentage de réussite de chaque équipe.
  (En relevé joueur par joueur, ce report automatique est désactivé : on ne peut pas savoir
  à quel adversaire précis attribuer la passe manquée.)
- **Fair-play** : un bouton « Rien à signaler » par équipe crédite tout le monde d'un coup ;
  ensuite, « Ajuster individuellement » permet de désigner les exceptions, dans un sens
  (à valoriser) comme dans l'autre (à reprendre). Les élèves non désignés gardent la note
  collective de leur équipe.

### La fiche d'un élève

Un clic sur une ligne de la liste des élèves ouvre sa fiche. En tête, dès qu'une classe compte
plusieurs cycles, un tableau **« Indice par APSA »** : une ligne par activité, avec le nombre de
leçons, l'indice, les observations et la fiabilité. C'est la vue d'ensemble de l'année — 6,2 en
badminton, 4,7 en handball — et le cycle ouvert y est surligné.

Le reste de la fiche porte sur ce cycle ouvert : radar des quatre critères, indice global, nombre
d'observations, courbe de progression — puis les tableaux de parcours.

- **Parcours en match** : bilan victoires / nuls / défaites, différence de points, et pour chaque leçon
  l'équipe portée et les coéquipiers côtoyés, avec le total de coéquipiers différents sur le cycle.
- **Parcours en confrontation** : toutes les oppositions d'échauffement et de situation — passe à 10,
  déménageur, gagne-terrain — avec la leçon, la fiche (l'échauffement est signalé), son équipe,
  l'adversaire, le score et le résultat. Ces oppositions n'entrent pas dans le classement de la leçon :
  sans ce tableau, elles n'apparaissaient nulle part. Les oppositions programmées mais pas encore
  jouées sont listées en « à jouer », et celles qui se sont déroulées pendant qu'il était blessé ou
  absent ne sont pas comptées — il ne les a pas jouées.

### Évaluation

**On y accède depuis la liste des leçons**, à côté de « Nouvelle leçon » — c'est là qu'on y pense,
au moment de préparer la séance — et toujours depuis Statistiques → Évaluation.

D'une classe à l'autre, la grille part des mêmes bases mais n'est pas forcément la même. Le bouton
**« Dupliquer pour cette classe »** copie la grille choisie : les items, les coefficients et les
niveaux sont repris, et la copie peut ensuite diverger sans toucher à l'originale. Les grilles
restent une bibliothèque commune, partagée par toutes les classes.

- Constructeur de grille : items librement nommés, chacun rattaché à un critère
  (ou à l'indice global, ou au résultat des affrontements), avec coefficient ; niveaux de maîtrise
  et barème paramétrables ; note sur 20 par défaut.
- Le menu **« Rattaché à »** permet aussi de **créer un critère sans quitter la grille** — c'est
  souvent là qu'on s'aperçoit qu'il en manque un — et de choisir **« Rien : je note cet item à la
  main »**, auquel cas l'application ne propose aucun niveau et te laisse décider.
- **Les niveaux de maîtrise se rédigent item par item.** Voir plus bas.
- **« Proposer les niveaux depuis les indices »** remplit les cases vides à partir des données
  récoltées. Les cases déjà saisies à la main ne sont jamais écrasées. C'est un point de départ,
  pas un verdict.
- **Auto-évaluation** en mode kiosque : l'élève se situe sur chaque critère, voit sa note estimée
  et sa courbe de progression depuis le début du cycle.
- Le tableau affiche l'**écart auto-évaluation / évaluation**. Ce n'est pas une erreur de l'élève :
  c'est un indicateur de lucidité et un excellent support d'entretien.
- Export CSV des notes (séparateur `;`, décimales à la française, compatible Excel/Pronote).

### Les niveaux de maîtrise, item par item

« Maîtrise satisfaisante » ne veut pas dire la même chose pour la tactique et pour le fair-play. En
badminton, un niveau de tactique se dit souvent par un chiffre observable dans une situation
d'évaluation — « déplace son adversaire et marque 3 points directs sur 10 échanges » ; un niveau de
fair-play se dit par une description. La grille garde donc ses quatre niveaux et leurs points, mais
**chaque item peut les réécrire dans ses propres termes**.

Dans l'éditeur de grille, la colonne **Niveaux** ouvre les quatre zones de rédaction de l'item. Le
bouton passe à « Rédigés » quand quelque chose y est écrit. **Ce qu'on laisse vide retombe sur le
libellé général de la grille** : on précise ce qui en vaut la peine, et rien de plus.

Ces descriptions se retrouvent là où l'on en a besoin :

- dans le **tableau d'évaluation**, le menu de chaque case propose les mots de l'item plutôt que
  « maîtrise fragile » ; un ⓘ à côté du titre de la colonne ouvre les quatre niveaux en entier ;
- dans l'**auto-évaluation en kiosque**, l'élève lit la description sous le libellé — c'est là que
  l'exercice devient sérieux : il se situe sur un comportement observable, pas sur un mot abstrait.
  Dès qu'un critère a ses niveaux rédigés, les quatre choix passent **l'un sous l'autre, sur toute
  la largeur** : le niveau en tête, sa précision dessous, avec la place de la lire. Un texte de deux
  lignes dans une colonne de 150 px ne se lit pas, et un élève qui ne lit pas coche au hasard. Les
  critères sans précision gardent leurs quatre libellés côte à côte ;
- dans le **dossier de séquence imprimé**, un tableau récapitule les niveaux rédigés, à relire au
  moment d'écrire les appréciations.

Le barème ne change pas : les points restent ceux des niveaux de la grille, et la note se calcule
comme avant. Ce qui change, c'est ce que le niveau veut dire — et donc ce qu'on peut en discuter
avec l'élève.

### Les attendus de fin de cycle

Une note dit un chiffre ; un attendu dit ce que ce chiffre atteste. Sous la grille, la section
**Attendus de fin de cycle** est ta bibliothèque.

**Les attendus du champ d'apprentissage 4 sont livrés avec l'application**, marqués d'un repère
`CA4`. Ils valent **pour toutes les activités** — c'est le rapport de force qui les porte, pas le
volant ni le ballon — et sont rangés dans leur cycle :

| Cycle 3 (6ᵉ) | |
|---|---|
| **AFC3 n°1** | S'organiser tactiquement pour gagner le duel ou le match en identifiant les situations favorables de marque. |
| **AFC3 n°2** | Maintenir un engagement moteur efficace sur tout le temps de jeu prévu. |
| **AFC3 n°3** | Respecter les partenaires, les adversaires et l'arbitre. |
| **AFC3 n°4** | Assurer différents rôles sociaux (joueur, arbitre, observateur) inhérents à l'activité et à l'organisation de la classe. |
| **AFC3 n°5** | Accepter le résultat de la rencontre et être capable de le commenter. |

| Cycle 4 (5ᵉ, 4ᵉ, 3ᵉ) | |
|---|---|
| **AFC4 n°1** | Réaliser des actions décisives en situation favorable afin de faire basculer le rapport de force en sa faveur ou en faveur de son équipe. |
| **AFC4 n°2** | Adapter son engagement moteur en fonction de son état physique et du rapport de force. |
| **AFC4 n°3** | Être solidaire de ses partenaires et respectueux de son (ses) adversaire(s) et de l'arbitre. |
| **AFC4 n°4** | Observer et co-arbitrer. |
| **AFC4 n°5** | Accepter le résultat de la rencontre et savoir l'analyser avec objectivité. |

Ce sont des fiches comme les autres : **reformulables, supprimables**, et tu ajoutes les tiennes à
côté avec « Écrire un attendu ». Un attendu que tu as réécrit n'est jamais réécrasé par une mise à
jour, et un attendu supprimé ne revient pas tout seul — le bouton **« Rétablir les attendus du
CA4 »** apparaît alors si tu changes d'avis. Rien n'est livré pour le lycée : ce niveau reste à ta
plume.

Chaque attendu porte trois choses : le **cycle** auquel il appartient — **cycle 3** (les sixièmes),
**cycle 4** (cinquième, quatrième, troisième), **lycée** —, l'**activité** concernée (ou « toutes »),
et un **code court** facultatif (« AFC 1 », « CA4-2 ») qui sert d'étiquette sur les boutons.

La classe, elle, porte son cycle : il est deviné à partir de son nom — « 6e B » relève du cycle 3,
« 2nde 4 » du lycée — et se corrige d'un menu à côté des attendus. Dans l'éditeur de grille, chaque
item affiche alors les attendus **de ce cycle et de cette activité** : un clic relie, un autre
délie. Les boutons ne portent que le **code**, faute de place — le **texte entier des attendus
proposés est rappelé tout en bas de la fenêtre**, pendant que tu construis ta grille, pour choisir
sans avoir à les retenir. Les mêmes attendus ne sont donc pas proposés à une classe de sixième et à une classe de
troisième, ce qui est bien le but.

Sous le tableau des notes, un récapitulatif **« Ce que cette grille atteste »** liste les attendus
reliés et les items qui les servent. C'est ce qu'on colle dans un bulletin, ou ce qu'on montre en
conseil de classe.

### Le dossier de séquence (à imprimer ou enregistrer en PDF)

Bouton **« Dossier de séquence »**, à côté de « Nouvelle leçon ». Il rassemble, pour la classe et le
cycle ouverts, tout ce qu'il faut avoir sous les yeux pour rédiger ses appréciations :

1. **Vue d'ensemble** : une ligne par élève — présences, indice par critère, indice global, nombre
   d'observations, fiabilité, et la note de la grille si elle est saisie.
2. **Déroulement de la séquence** : leçon par leçon, l'objectif, les présents, les échauffements et
   situations menés avec leur format et leur nombre de relevés, les rencontres avec les classements
   de chaque poule ou l'échelle finale des défis, et les arbitrages déclarés.
3. **Évaluation** : la grille, ce que chaque item atteste (attendus de fin de cycle reliés), puis
   les niveaux et notes de chaque élève.
4. **Appréciations** : une ligne par élève avec ses chiffres clés et **un cadre vide**.
   L'application n'écrit pas les appréciations — ce n'est pas son travail.

Le bouton « Imprimer / Enregistrer en PDF » ouvre la fenêtre d'impression du navigateur : choisis
« Enregistrer au format PDF ». Il n'y a pas de bibliothèque PDF embarquée, donc cela marche hors
ligne, sur ordinateur comme sur tablette. La barre d'outils ne s'imprime pas, les sections partent
sur de nouvelles pages, et les tableaux ne se coupent pas au milieu d'une ligne.

---

## 4. Comment les indices sont calculés

C'est le cœur de l'application. Elle ne cache rien : la page **Fiabilité** vérifie
le modèle sur tes propres données.

### Les critères

Chaque APSA a les siens, fournis par l'activité choisie et **entièrement renommables, ajoutables et
repondérables**. En badminton, le préréglage livré est **Frappes et technique · Déplacements ·
Tactique · Fair-play et arbitrage**. Un **indice global** sur 10 en est la moyenne pondérée, avec
**5 = moyenne de la classe**.

La **fiche d'un élève** (Statistiques → Élèves, puis clic sur son nom) affiche, en plus de son
radar et de sa progression, son parcours en rencontre et en match : victoires, défaites,
différence de points, et les adversaires ou coéquipiers par lesquels il est passé.

#### Où voir ce qui alimente quoi

**Statistiques → « Ce qui alimente l'indice »**, et un raccourci du même nom dans la barre d'outils
des Rencontres et des Matchs — c'est là que la question se pose, au moment où l'on règle les
relevés. La page répond pour l'APSA ouverte :

- le **poids des quatre sources** (situations, relevés, observation, résultat) ;
- les **indicateurs calculés** à partir des relevés, avec leur formule et les critères qu'ils
  visent, en pourcentage : en badminton, « rapport points gagnants / fautes » nourrit *Frappes et
  technique* à 60 % et *Tactique* à 40 % ;
- les **compteurs relevés pendant la rencontre**, ce qu'ils valent au score, et lesquels sont
  activés par défaut ;
- les **compteurs que tu as reliés toi-même** à un critère, leçon par leçon, dans « Relevés et
  bonus » ;
- les **situations** de la séquence et les critères que chacune cible ;
- le reste : « rien à signaler », ajustements individuels, **arbitrages déclarés en kiosque**, un ＋
  ou un − posé en observation, et le **score** — qui ne nourrit aucun critère en particulier mais
  pèse à part sur l'indice global ;
- enfin, un avertissement quand **un critère n'est alimenté par rien** : il reste alors à 5 pour
  tout le monde, et la page dit par où le nourrir.

| Critère (badminton) | D'où viennent les données |
|---|---|
| Frappes et technique | situations qui le ciblent · rapport points gagnants / fautes · volume de points gagnants · fiabilité au service |
| Déplacements | situations qui le ciblent · volume de points gagnants |
| Tactique | situations qui le ciblent · rapport points gagnants / fautes |
| Fair-play et arbitrage | « rien à signaler » sur un groupe, un match ou une rencontre · ajustements individuels · arbitrages déclarés par les élèves |

### Quatre sources, dans cet ordre

**1. Situations d'entraînement** (45 % par défaut)

Les scores bruts sont normalisés en z-score : « 14 passes » ne veut rien dire seul,
« 14 passes, soit au-dessus de la moyenne de la classe sur cette situation » veut dire quelque chose.

Quand une tentative est réalisée **en groupe**, on ne peut pas attribuer le score à un seul élève.
L'application résout un système de **moindres carrés régularisés (ridge)** où chaque élève a une
contribution individuelle inconnue, et où chaque tentative affirme « la moyenne des contributions
de ce groupe vaut *z* ». Si les partenaires tournent entre les tentatives, le système devient
identifiable et **sépare l'élève de ses partenaires** — c'est le principe du *plus-minus ajusté*
utilisé dans les sports collectifs professionnels.

Vérification faite sur données simulées (`test/check.js`) :

| Protocole | Corrélation entre niveau réel et niveau estimé |
|---|---|
| Mesure individuelle | r = 1,00 |
| 6 tours, groupes de 3, partenaires brassés | r = 0,91 |
| 6 tours, groupes de 3, partenaires figés | r = 0,70 |

D'où l'indicateur « brassage suffisant / insuffisant » affiché sur chaque situation.
L'objectif est **au moins 3 partenaires distincts** par élève et par situation.

**Paliers** : 15 passes à 5 m et 15 passes à 8 m ne valent pas la même chose. La normalisation
se fait **à l'intérieur de chaque palier** (dès qu'il compte au moins 3 tentatives), puis une
**prime de palier** est ajoutée proportionnellement à l'écart au palier moyen de la classe.
Sans elle, un élève serait pénalisé d'avoir accepté de complexifier sa tâche — exactement
le contraire de ce qu'on veut encourager.

**2. Statistiques de match** (30 %)

Les trois comptages sont convertis en indicateurs comparables, puis normalisés au niveau
de la classe :

| Indicateur | Critère alimenté |
|---|---|
| Pourcentage de passes réussies | Technique |
| Volume de passes réussies | Jeu en progression |
| Interceptions | Défense |

Le total des passes ratées d'une équipe vaut **ce que l'observateur a saisi plus les
interceptions relevées en face**. Une interception n'est donc comptée qu'une seule fois,
mais elle pèse des deux côtés : en défense pour celui qui intercepte, en technique pour
celui qui a perdu le disque.

Une statistique relevée **par équipe** est diluée à 60 % avant d'être attribuée aux joueurs :
elle ne les distingue pas entre eux. Une statistique **par joueur** compte pleinement.

**3. Ce que tu observes** (15 %) — le fair-play relevé sur chaque match, et tes `+` / `−`
sur un critère pendant la leçon.

**4. Résultat des matchs** (10 %) — calculé **en dernier**, volontairement.

L'écart de points est d'abord rendu indépendant du barème : on utilise la marge relative
`(A − B) / (A + B)`, si bien que 30–10 avec des buts à 1 point et 300–100 avec des buts à
10 points donnent exactement la même valeur. Cette marge est ensuite comparée à la
**marge attendue** compte tenu des indices des deux équipes : battre l'équipe la plus forte
de 2 points vaut plus que battre la plus faible de 15. Seule cette « surprise » alimente
l'indice **global** — jamais les critères techniques.

> **Pourquoi en dernier ?** Si l'écart de points alimentait le critère technique, et que le
> critère technique servait à prédire l'écart de points, le modèle se mordrait la queue et
> amplifierait ses propres erreurs. En calculant le résultat après coup, on garde une mesure
> indépendante — et la page Fiabilité peut alors vérifier honnêtement si les deux concordent.

### Agrégation dans le temps

- **Moyenne glissante pondérée (EWMA)** sur les leçons : les séances récentes comptent plus
  (35 % par défaut), sans effacer l'historique. C'est ce qui fait évoluer l'indice au fil du cycle.
- **Régression vers la moyenne** proportionnelle au nombre d'observations : un élève vu deux fois
  reste proche de 5. Le niveau de fiabilité (faible / moyenne / bonne) est affiché partout.
  Un élève peu observé est réparti comme un élève moyen — c'est volontaire, c'est plus juste
  que de lui inventer un niveau.
- **Une observation, c'est un relevé, pas une séance** : un élève qui mène quatre manches dans une
  situation compte pour plusieurs observations (jusqu'à trois par situation et par leçon), pas pour
  une seule. Sans cela, une séance entière de travail mesuré pesait autant qu'un passage unique et
  l'indice ne bougeait presque pas.
- **L'indice global est la moyenne des critères RENSEIGNÉS.** Un critère sur lequel l'élève n'a
  jamais été observé ne dit rien : le compter comme « exactement dans la moyenne » diviserait par
  quatre l'effet de la seule situation menée. En début de cycle, l'indice global suit donc ce qui a
  réellement été mesuré, et s'élargit à mesure que les autres critères se remplissent.

### L'onglet Qualité des données

- **Corrélation** entre l'écart d'indice des deux équipes et la marge réelle des matchs,
  avec nuage de points et droite d'ajustement. C'est la vérification de ton hypothèse
  « plus la technique est maîtrisée, plus l'écart est important », sur *ta* classe.
- **Brassage des partenaires** situation par situation.
- **Couverture des données** critère par critère, et liste des élèves à moins de 4 observations.

---

## 5. Mode kiosque (la tablette qui circule)

Plein écran, gros boutons, aucun accès aux réglages ni aux notes des autres. Le bouton qui
l'ouvre est violet, pour ne pas le confondre avec les commandes de l'enseignant.

**La sortie est protégée par un code** (**2706** par défaut, modifiable dans Réglages → Mode kiosque).
Un espace créé avant ce changement et resté sur l'ancien code bascule automatiquement sur 2706 ;
un code que tu aurais personnalisé toi-même n'est jamais touché.
Un pavé numérique s'affiche : sans le code, la tablette reste en mode élève et personne ne va se
promener dans les notes de la classe. Le même code protège la réinitialisation d'une rencontre.

Trois modes :

- **Situations ou échauffement** : le bouton kiosque de chaque onglet n'ouvre que les fiches de
  cet onglet — pas question qu'un élève tombe sur la situation d'apprentissage alors qu'il en est
  encore à l'échauffement. L'élève touche son groupe → relit le message du passage précédent →
  choisit son palier (les boutons sont teintés de l'orange au vert foncé) → saisit son score →
  reçoit son retour automatique (texte et image) → passe la tablette.
  Un échauffement **en confrontation** saute tout cela : l'écran affiche directement les oppositions
  tour par tour, deux gros boutons `+1` par équipe, le vainqueur annoncé en tête de bloc et l'équipe
  au repos rappelée dans le titre du tour.
  Une fiche **en co-frontation** affiche la liste de la classe : les élèves se désignent (chaque nom
  porte ses points et ses coopérations, de quoi repérer qui reste à rencontrer), valident, annoncent
  « Objectif atteint » ou « Pas cette fois », lisent leur retour et repassent la tablette. Un bouton
  ouvre le classement complet. Le nombre de prénoms à toucher suit la taille du groupe réglée dans la
  fiche, et si elle interdit de refaire un groupe déjà formé, les camarades déjà rencontrés sont
  éteints — impossible de se tromper. Quand la situation est terminée — par la règle ou parce que tu
  l'as arrêtée — la tablette n'affiche plus que le **classement final** et invite à la rapporter.
- **Statistiques de match** : les deux équipes **côte à côte sur un seul écran**, sans aucun
  défilement. Score en gros en haut de chaque colonne, gros bouton **« + But »** qui met
  le résultat à jour immédiatement, et trois compteurs `+` / `−` en dessous. Une légende
  rappelle qu'on ne compte pas une passe ratée en plus d'une interception.
  Depuis l'écran de choix, le bouton violet **« Relever les N matchs ensemble »** ouvre les
  rencontres du tour l'une sous l'autre, repérées « Terrain 1 », « Terrain 2 »… : les équipes
  observatrices se partagent une seule tablette et ne reviennent jamais en arrière. Chaque bouton
  agit sur son propre match — rien ne se mélange entre les terrains.
- **Auto-évaluation** : l'élève se situe sur chaque critère, voit sa note estimée et sa progression.

Les **bonus par combinaison d'actions** définis dans « Modifier les relevés » apparaissent bien
dans le kiosque, sur la ligne des boutons de score de chaque équipe, en **ambré avec une étoile**
à côté du bouton « + But ».

Depuis l'écran des matchs, un bouton **Statistiques** ouvre une page faite pour les élèves :
ils choisissent leur équipe, voient ses totaux (points au classement, bilan, différence, pourcentage
de passes réussies, chaque compteur relevé), **comparent les équipes entre elles** dans un tableau
où la leur est surlignée, et parcourent le **détail de chaque match** tour par tour.

---

## 6. Données, sauvegarde et RGPD

- Tout est enregistré dans le **stockage local du navigateur** de l'appareil.
- **Exporte régulièrement** ta sauvegarde JSON (Réglages). Vider le cache du navigateur
  efface les données ; il n'y a pas de récupération possible.
- L'import propose de **fusionner** ou de **remplacer**.
- Option **anonymisation** : les élèves s'affichent en « Prénom N. » partout, y compris
  en vidéoprojection.

### Synchronisation ordinateur ↔ tablette (Realtime Database)

La configuration du projet Firebase **`eps-pasteur`** est intégrée à l'application : il n'y a
aucun code à coller. La base est une **Realtime Database hébergée en Europe** (`europe-west1`),
ce qui est le bon choix pour des données scolaires.

**Réglages → Synchronisation ordinateur ↔ tablette.** Sur chaque appareil, tu te connectes avec
**le même compte e-mail + mot de passe**. La première fois, « Créer le compte » ; ensuite,
« Se connecter ». Le mot de passe n'est jamais stocké par l'application — c'est Firebase qui
garde la session ouverte.

> **Pourquoi un compte et pas une connexion anonyme ?** La connexion anonyme attribue un
> identifiant différent à chaque appareil : ton ordinateur et ta tablette se retrouveraient dans
> deux espaces séparés, sans rien partager. Un compte, c'est un identifiant unique — donc un seul
> espace — et c'est aussi ce qui permet d'écrire des règles de sécurité qui tiennent.

#### À faire une seule fois dans la console Firebase

Sans ces deux réglages, la synchronisation ne fonctionnera pas — et surtout, **la base créée en
« mode test » est ouverte à tout le monde pendant 30 jours**.

1. **Authentication → Sign-in method** : activer **E-mail/Mot de passe**.
2. **Realtime Database → Règles** : remplacer tout par ceci, puis **Publier**.

```json
{
  "rules": {
    "ca4": {
      "$uid": {
        ".read": "auth != null && auth.uid === $uid",
        ".write": "auth != null && auth.uid === $uid"
      }
    }
  }
}
```

Ce que ces règles disent : chaque compte ne peut lire et écrire que son propre espace CA4 (l'application d'ultimate, elle, écrit sous `espaces/` : les deux cohabitent dans le même projet Firebase), et un
visiteur non connecté n'a accès à rien. Le bouton « Voir les règles à coller » dans les réglages
te les affiche avec un bouton de copie, pour ne pas avoir à revenir ici.

> Une clé d'API web Firebase n'est pas un mot de passe : elle identifie le projet et se retrouve
> forcément dans le code de n'importe quelle page web. **Ce sont les règles ci-dessus, et elles
> seules, qui protègent les données.** Publie-les avant de saisir la moindre donnée réelle.

#### Comment ça se comporte au quotidien

- **Le local reste la référence.** Tout est d'abord enregistré dans le navigateur ; la
  synchronisation vient par-dessus. Sans réseau — un gymnase, typiquement — l'application
  fonctionne normalement et rattrape son retard dès que la connexion revient.
- Un **voyant** dans la barre du haut indique l'état : synchronisé, envoi en cours, hors ligne,
  non connecté, erreur. Un clic dessus ouvre les réglages.
- L'envoi est **différé de deux secondes** après la dernière modification, pour ne pas
  bombarder le serveur pendant une saisie.
- **En cas de modification des deux côtés**, l'application ne tranche jamais toute seule : si des
  changements locaux existent, elle signale qu'un autre appareil a envoyé quelque chose et te
  laisse choisir entre « Envoyer mes données » et « Récupérer celles du serveur ». Si rien n'a
  bougé localement, la mise à jour distante s'applique d'elle-même avec un message discret.
- Les **images** des situations voyagent avec les données. Au-delà de 6 Mo de sauvegarde,
  l'envoi est refusé avec un message : allège les schémas.
- « Désactiver sur cet appareil » arrête la synchronisation sans rien effacer, ni en local ni
  sur le serveur.

Le projet peut être remplacé par un autre (section « Utiliser un autre projet Firebase ») si tu
changes d'établissement ou si tu veux un projet par classe.

---

## 7. Structure du code

```
index.html               page unique, aucune dépendance externe
css/app.css              feuille de style (clair par défaut, mode sombre disponible)
js/core.js               stockage local, activités CA4, utilitaires, algèbre linéaire, import CSV
js/progress.js           paliers, seuils, messages conditionnels
js/ratings.js            moteur d'indices (ridge, EWMA, régression vers la moyenne)
js/teams.js              composition des équipes (coût + recherche locale avec recuit)
js/ui.js                 briques d'interface (radar, courbes, nuage de points, modales)
js/cloud.js              synchronisation Realtime Database (compte enseignant)
js/views.js              classes, élèves, contraintes, fiabilité, réglages
js/bank.js               banque de situations, dossiers de variantes
js/training.js           échauffements, situations et paliers
js/eval.js               grilles, notes, auto-évaluation
js/arena.js              rencontres individuelles : poules, ligues, défis
js/dossier.js            dossier de séquence imprimable (PDF par le navigateur)
js/lesson.js             présences, équipes, matchs
js/kiosk.js              mode tablette
js/main.js               routeur, actions, jeu de démonstration
build.js                 fabrique le fichier autonome (node build.js)
sw.js                    cache hors ligne
test/check.js            vérification des calculs (Node, sans navigateur)
test/csv.js              vérification de l'import CSV sur l'export du collège
test/browser.js          test de bout en bout (Playwright)
PROMPT-reconstruction.md prompt complet pour repartir du projet dans une nouvelle discussion
```

Aucune bibliothèque tierce, aucun outil de compilation : les fichiers déposés sont les
fichiers exécutés. Les scripts sont des scripts classiques (pas des modules ES), ce qui
permet d'ouvrir `index.html` directement depuis le disque.

### Tests

```bash
node test/check.js      # ridge, paliers, équipes, barème, co-frontation, mode Niveau, effacement
node test/csv.js        # import de l'export d'appel du collège
npm i playwright && node test/browser.js   # parcours complet dans Chromium (102 vérifications)
node build.js           # régénère ultimate-eps-autonome.html après une modification
```

---

## 8. Conseils d'usage

**Les trois premières leçons servent à alimenter le modèle.** Avant cela, les indices valent
tous à peu près 5 et les équipes sont composées presque au hasard — ce qui reste préférable
à un choix par affinités. Commence par des situations mesurables à partir de la leçon 1.

**Brasse les partenaires.** C'est la condition qui fait la différence entre « je sais que ce
groupe réussit » et « je sais qui, dans ce groupe, fait la différence ». Le bouton
« Générer automatiquement » est fait pour ça.

**Garde le résultat des matchs à faible poids.** Un élève peut très bien jouer dans une équipe
qui perd. Le réglage par défaut (10 %) est déjà un maximum raisonnable. Si tu veux valoriser
l'investissement en match, la **progression individuelle** entre la première et la dernière
leçon est un indicateur plus juste que le résultat brut.

**Regarde la qualité des données avant de noter.** Si la corrélation affichée est faible,
c'est que le modèle n'explique pas grand-chose de ta classe : sers-t'en pour composer les
équipes, mais pas pour justifier une note.

---

Développé pour un cycle d'ultimate en collège. Réutilisable pour toute APSA en renommant
les cinq critères dans les Réglages.
