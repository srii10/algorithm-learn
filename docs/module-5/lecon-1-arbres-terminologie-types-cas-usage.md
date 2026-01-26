##### Leçon 25 sur 42

# Arbres : Terminologie, Types et Cas d'Usage

**Module 5** : Arbres et Parcours de Graphes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre la structure **hiérarchique** des arbres
- Maîtriser la **terminologie** des arbres (nœud, racine, feuille, profondeur, hauteur)
- Distinguer les différents **types d'arbres** (binaire, complet, parfait)
- Identifier les **cas d'usage** des arbres dans des applications réelles
- Reconnaître quand utiliser un **arbre** plutôt qu'une autre structure de données
- Représenter visuellement des **structures arborescentes**

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Module 4 complété** : Maîtriser la récursion (les arbres sont naturellement récursifs)
- **Listes chaînées** : Comprendre les nœuds et les références
- **Complexité algorithmique** : Connaître la notation Big O
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Au-delà des Structures Linéaires

Jusqu'à présent, vous avez travaillé avec des structures de données **linéaires** : tableaux, listes chaînées, piles et files. Ces structures organisent les données en **séquence**, où chaque élément a au plus un prédécesseur et un successeur.

Les **arbres** sont différents : ce sont des structures de données **non linéaires** qui organisent les données de manière **hiérarchique**. Imaginez :

- Un **arbre généalogique** : ancêtres et descendants
- Un **système de fichiers** : dossiers et sous-dossiers
- Un **organigramme** : direction et employés
- Une **page web (DOM)** : éléments HTML imbriqués

Ces exemples ont tous une caractéristique commune : une structure **parent-enfant** où chaque élément peut avoir plusieurs "enfants" mais un seul "parent".

> **Point Clé**
>
> Les arbres sont des structures **naturellement récursives** : chaque nœud d'un arbre peut être considéré comme la racine de son propre sous-arbre. Cette propriété explique pourquoi la récursion (Module 4) est si importante pour manipuler les arbres.

---

## 📦 Terminologie des Arbres

Pour parler des arbres, il faut maîtriser un vocabulaire spécifique. Voici les termes essentiels.

---

### Nœud (Node)

Un **nœud** est l'unité fondamentale d'un arbre. Il contient :

- Une **donnée** (valeur)
- Des **références** vers d'autres nœuds (ses enfants)

```javascript
// Représentation simple d'un nœud d'arbre
const noeud = {
  valeur: "Documents",
  enfants: [
    /* références vers d'autres nœuds */
  ],
};
```

---

### Racine (Root)

La **racine** est le nœud situé au **sommet** de l'arbre. C'est le seul nœud qui n'a **pas de parent**.

```
        [Racine]     ← Nœud sans parent
        /      \
     [A]        [B]
     /  \         \
   [C]  [D]       [E]
```

**Exemple :** Dans un système de fichiers, le répertoire racine `/` (Linux) ou `C:\` (Windows) est la racine de l'arbre.

---

### Parent

Un **parent** est un nœud qui a un ou plusieurs **enfants** connectés directement en dessous.

```
        [Parent]
        /      \
  [Enfant1] [Enfant2]
```

**Exemple :** Dans `C:\Utilisateurs\Chermann\Documents`, le dossier `Chermann` est le parent de `Documents`.

---

### Enfant (Child)

Un **enfant** est un nœud directement connecté à un nœud parent, situé un niveau en dessous.

**Propriété :** Un nœud peut avoir **plusieurs enfants**, mais un seul **parent**.

---

### Frère/Sœur (Sibling)

Des **frères/sœurs** sont des nœuds qui partagent le **même parent**. Ils sont au même niveau dans l'arbre.

```
        [Parent]
       /    |    \
    [A]    [B]    [C]   ← A, B et C sont frères/sœurs
```

**Exemple :** Si le dossier `Utilisateurs` contient `Chermann`, `Ingrid` et `Prudence`, ces trois dossiers sont frères/sœurs.

---

### Feuille (Leaf)

Une **feuille** est un nœud qui n'a **aucun enfant**. C'est l'extrémité d'une branche.

```
        [Racine]
        /      \
     [A]        [B]
     /  \
   [C]  [D]     ← C, D et B sont des feuilles
```

**Exemple :** Dans un système de fichiers, les fichiers (pas les dossiers) sont généralement des feuilles.

---

### Nœud Interne (Internal Node)

Un **nœud interne** est un nœud qui a **au moins un enfant**. Ce n'est pas une feuille.

**Exemple :** Tous les dossiers qui contiennent des fichiers ou sous-dossiers sont des nœuds internes.

---

### Arête (Edge)

Une **arête** est le lien qui connecte deux nœuds (parent ↔ enfant).

```
    [A]
     │  ← Arête
    [B]
```

**Propriété :** Un arbre avec **n nœuds** a exactement **n-1 arêtes**.

---

### Chemin (Path)

Un **chemin** est une séquence de nœuds connectés par des arêtes.

**Exemple :** Le chemin de `C:\` à `rapport.pdf` :

```
C:\ → Utilisateurs → Chermann → Documents → rapport.pdf
```

Ce chemin a **4 arêtes** (longueur = 4).

---

### Profondeur d'un Nœud (Depth)

La **profondeur** d'un nœud est le nombre d'arêtes entre la **racine** et ce nœud.

```
        [A]        ← Profondeur 0
       /   \
     [B]   [C]     ← Profondeur 1
     /  \
   [D]  [E]        ← Profondeur 2
```

| Nœud       | Profondeur |
| ---------- | ---------- |
| A (racine) | 0          |
| B, C       | 1          |
| D, E       | 2          |

---

### Hauteur d'un Nœud (Height)

La **hauteur** d'un nœud est le nombre d'arêtes sur le **plus long chemin** de ce nœud jusqu'à une feuille.

```
        [A]        ← Hauteur 2
       /   \
     [B]   [C]     ← Hauteur B=1, Hauteur C=0
     /  \
   [D]  [E]        ← Hauteur 0 (feuilles)
```

| Nœud       | Hauteur      |
| ---------- | ------------ |
| D, E, C    | 0 (feuilles) |
| B          | 1            |
| A (racine) | 2            |

---

### Hauteur de l'Arbre

La **hauteur de l'arbre** est la hauteur de sa racine, c'est-à-dire la **profondeur maximale** de l'arbre.

---

### Sous-Arbre (Subtree)

Un **sous-arbre** est formé par un nœud et tous ses descendants.

```
        [A]
       /   \
     [B]   [C]
     /  \
   [D]  [E]

Le sous-arbre de B :
     [B]
     /  \
   [D]  [E]
```

> **Propriété Récursive**
>
> Chaque nœud d'un arbre est la racine de son propre sous-arbre. C'est pourquoi les algorithmes sur les arbres sont souvent récursifs !

---

### Degré d'un Nœud

Le **degré** d'un nœud est le nombre de ses **enfants directs**.

**Exemple :**

- Un nœud avec 3 enfants a un degré de 3
- Une feuille a un degré de 0

---

## 📝 Micro-Exercice #1 : Identifier la Terminologie

**Objectif :** Vérifier votre compréhension de la terminologie des arbres.

**Instructions :** Considérez cette structure de répertoires :

```
/
├── home
│   ├── chermann
│   │   ├── documents
│   │   │   └── rapport.pdf
│   │   └── photos
│   │       ├── vacances.jpg
│   │       └── profil.png
│   └── ingrid
│       └── notes.txt
└── var
    └── log
        └── systeme.log
```

Répondez aux questions suivantes :

1. Quelle est la racine ?
2. Listez les enfants du nœud `/home`
3. Qui est le parent de `rapport.pdf` ?
4. Listez les frères/sœurs de `chermann`
5. Listez toutes les feuilles
6. Quelle est la profondeur de `vacances.jpg` ?
7. Quelle est la hauteur du nœud `chermann` ?
8. Quelle est la hauteur de l'arbre ?

<details>
<summary>💡 Voir la solution</summary>

1. **Racine** : `/`
2. **Enfants de `/home`** : `chermann`, `ingrid`
3. **Parent de `rapport.pdf`** : `documents`
4. **Frères/sœurs de `chermann`** : `ingrid`
5. **Feuilles** : `rapport.pdf`, `vacances.jpg`, `profil.png`, `notes.txt`, `systeme.log`
6. **Profondeur de `vacances.jpg`** : 4 (/ → home → chermann → photos → vacances.jpg)
7. **Hauteur de `chermann`** : 2 (chemin le plus long : chermann → photos → vacances.jpg)
8. **Hauteur de l'arbre** : 4 (profondeur maximale des feuilles)

</details>

---

## 🌳 Types d'Arbres

Tous les arbres partagent une structure hiérarchique, mais il existe plusieurs types spécialisés avec des propriétés particulières.

---

### Arbre Général (General Tree)

Un **arbre général** est la forme la plus libre : chaque nœud peut avoir **n'importe quel nombre d'enfants**.

```
          [A]
        / | | \
      [B][C][D][E]
      /      / \
    [F]    [G] [H]
```

**Exemples d'utilisation :**

- Systèmes de fichiers
- Organigrammes d'entreprise
- Structures de menus

---

### Arbre Binaire (Binary Tree)

Un **arbre binaire** est un arbre où chaque nœud a **au maximum 2 enfants**, appelés **enfant gauche** et **enfant droit**.

```
        [A]
       /   \
     [B]   [C]
     /  \     \
   [D]  [E]   [F]
```

**Caractéristiques :**

- Maximum **2 enfants** par nœud
- Les enfants sont **ordonnés** (gauche, droite)
- Très utilisé en informatique

**Représentation en JavaScript :**

```javascript
class NoeudBinaire {
  constructor(valeur) {
    this.valeur = valeur;
    this.gauche = null; // Enfant gauche
    this.droite = null; // Enfant droit
  }
}

// Exemple : créer un arbre binaire simple
const racine = new NoeudBinaire("A");
racine.gauche = new NoeudBinaire("B");
racine.droite = new NoeudBinaire("C");
racine.gauche.gauche = new NoeudBinaire("D");
racine.gauche.droite = new NoeudBinaire("E");
```

---

### Arbre Binaire de Recherche (BST)

Un **Arbre Binaire de Recherche** (Binary Search Tree) est un arbre binaire avec une propriété supplémentaire :

- Tous les nœuds du **sous-arbre gauche** ont des valeurs **inférieures** à la racine
- Tous les nœuds du **sous-arbre droit** ont des valeurs **supérieures** à la racine

```
          [50]
         /    \
      [30]    [70]
      /  \    /  \
   [20] [40][60] [80]
```

**Vérification :** Pour le nœud 50 :

- Sous-arbre gauche : 30, 20, 40 → tous < 50
- Sous-arbre droit : 70, 60, 80 → tous > 50

> **Important**
>
> Les BST seront étudiés en détail dans la **Leçon 26**. Ils permettent des opérations de recherche, insertion et suppression en **O(log n)** dans le meilleur cas.

---

### Arbre Binaire Plein (Full Binary Tree)

Un **arbre binaire plein** est un arbre où chaque nœud a **soit 0, soit 2 enfants**. Aucun nœud n'a exactement 1 enfant.

```
        [A]        Arbre binaire plein
       /   \
     [B]   [C]
     /  \
   [D]  [E]

        [A]        PAS plein (C a 1 enfant)
       /   \
     [B]   [C]
     /  \     \
   [D]  [E]   [F]
```

---

### Arbre Binaire Complet (Complete Binary Tree)

Un **arbre binaire complet** est un arbre où :

- Tous les niveaux sont **complètement remplis**, sauf éventuellement le dernier
- Le dernier niveau est rempli **de gauche à droite**

```
        [A]        Complet
       /   \
     [B]   [C]
     /  \   /
   [D]  [E][F]

        [A]        PAS complet (E absent, F présent)
       /   \
     [B]   [C]
     /        \
   [D]        [F]
```

**Usage :** Les **tas (heaps)** utilisent cette structure pour une implémentation efficace en tableau.

---

### Arbre Binaire Parfait (Perfect Binary Tree)

Un **arbre binaire parfait** est un arbre où :

- C'est un arbre binaire **plein**
- Toutes les **feuilles sont au même niveau**

```
        [A]       Parfait (hauteur 2)
       /   \
     [B]   [C]
     /  \  /  \
   [D][E][F][G]
```

**Propriété mathématique :** Un arbre parfait de hauteur h a **2^(h+1) - 1** nœuds.

| Hauteur | Nœuds |
| ------- | ----- |
| 0       | 1     |
| 1       | 3     |
| 2       | 7     |
| 3       | 15    |
| 4       | 31    |

---

### Tableau Récapitulatif des Types

| Type        | Propriété                    | Exemple d'usage       |
| ----------- | ---------------------------- | --------------------- |
| **Général** | N enfants par nœud           | Systèmes de fichiers  |
| **Binaire** | Max 2 enfants                | Arbres d'expression   |
| **BST**     | Gauche < Racine < Droite     | Recherche efficace    |
| **Plein**   | 0 ou 2 enfants               | Compression (Huffman) |
| **Complet** | Rempli gauche→droite         | Tas (Heap)            |
| **Parfait** | Plein + feuilles même niveau | Cas théorique idéal   |

---

## 📝 Micro-Exercice #2 : Classifier les Types d'Arbres

**Objectif :** Identifier le type d'arbre selon sa structure.

**Instructions :** Pour chaque description, identifiez le type d'arbre le plus précis.

1. Un arbre où chaque nœud a 0 ou 2 enfants, et toutes les feuilles sont au même niveau
2. Un arbre où le nœud racine a 3 enfants, un enfant a 1 enfant, un autre en a 2
3. Un arbre où chaque nœud a au maximum 2 enfants
4. Un arbre où tous les niveaux sont complets sauf le dernier, rempli de gauche à droite
5. Un arbre où chaque nœud a 0 ou 2 enfants (pas nécessairement au même niveau)

<details>
<summary>💡 Voir la solution</summary>

1. **Arbre binaire parfait** (plein + feuilles au même niveau)
2. **Arbre général** (plus de 2 enfants à la racine)
3. **Arbre binaire** (définition de base)
4. **Arbre binaire complet**
5. **Arbre binaire plein**

</details>

---

## 💼 Cas d'Usage des Arbres

Les arbres sont omniprésents en informatique. Voici leurs applications les plus courantes.

---

### 1. Systèmes de Fichiers

L'exemple le plus intuitif d'arbre est le **système de fichiers** de votre ordinateur.

```
C:\
├── Utilisateurs
│   ├── Chermann
│   │   ├── Documents
│   │   │   ├── Projets
│   │   │   │   ├── AlgoLearn
│   │   │   │   └── Portfolio
│   │   │   └── Factures
│   │   └── Photos
│   └── Ingrid
└── Programme Files
    └── VSCode
```

**Avantages de la structure arborescente :**

- **Organisation logique** : hiérarchie intuitive
- **Navigation facile** : chemin clair vers chaque fichier
- **Gestion des permissions** : héritées des dossiers parents

---

### 2. Document Object Model (DOM)

Les pages web sont représentées comme des arbres dans le navigateur.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Ma Page</title>
  </head>
  <body>
    <div>
      <h1>Bienvenue</h1>
      <p>Un paragraphe</p>
    </div>
  </body>
</html>
```

**Représentation en arbre :**

```
      [html]
      /    \
  [head]  [body]
    |        |
 [title]   [div]
    |      /    \
 "Ma Page" [h1]  [p]
            |      |
       "Bienvenue" "Un paragraphe"
```

**JavaScript peut manipuler cet arbre :**

```javascript
// Accéder à des nœuds
const h1 = document.querySelector("h1"); // Trouve le nœud h1
const parent = h1.parentElement; // div
const enfants = parent.children; // h1 et p
```

---

### 3. Indexation de Bases de Données

Les bases de données utilisent des arbres (B-trees, B+ trees) pour indexer les données et accélérer les recherches.

**Sans index (recherche linéaire) :** O(n) - parcourir toute la table
**Avec index (arbre B+) :** O(log n) - navigation rapide

```
Recherche de client_id = 5432 dans 1 000 000 enregistrements :

Sans index : jusqu'à 1 000 000 comparaisons
Avec index : ~20 comparaisons (log₂(1 000 000) ≈ 20)
```

---

### 4. Arbres d'Expression (Compilateurs)

Les compilateurs convertissent les expressions mathématiques en arbres pour les évaluer.

**Expression :** `(3 + 5) * 2`

```
        [*]
       /   \
     [+]    [2]
     / \
   [3] [5]
```

**Évaluation récursive :**

1. Évaluer sous-arbre gauche : 3 + 5 = 8
2. Évaluer sous-arbre droit : 2
3. Appliquer l'opérateur : 8 \* 2 = 16

---

### 5. Arbres de Décision (Machine Learning)

En intelligence artificielle, les arbres de décision prennent des décisions basées sur des conditions.

```
        [Température > 30°C ?]
              /         \
           Oui          Non
            |             |
    [Humidité > 70% ?]  "Pas besoin de clim"
         /       \
       Oui       Non
        |          |
  "Clim forte"  "Clim légère"
```

---

### 6. Structures de Données Avancées

Plusieurs structures de données importantes sont basées sur les arbres :

| Structure      | Description                | Complexité Recherche |
| -------------- | -------------------------- | -------------------- |
| **BST**        | Arbre binaire de recherche | O(log n) moyen       |
| **AVL**        | BST auto-équilibré         | O(log n) garanti     |
| **Tas (Heap)** | Arbre binaire complet      | O(1) pour min/max    |
| **Trie**       | Arbre de préfixes          | O(m) où m = longueur |

---

## 💼 Application : Étude de Cas - Gestion de Tâches par Catégories

Reprenons notre gestionnaire de tâches et imaginons une organisation **hiérarchique** des tâches.

---

### Scénario

Germain veut organiser ses tâches en catégories et sous-catégories :

```
Tâches de Germain
├── Travail
│   ├── Projet Alpha
│   │   ├── Conception
│   │   │   └── [Tâche: Créer les maquettes]
│   │   ├── Développement
│   │   │   ├── [Tâche: Implémenter le frontend]
│   │   │   └── [Tâche: Développer l'API]
│   │   └── Tests
│   │       └── [Tâche: Écrire les tests unitaires]
│   └── Projet Beta
│       └── [Tâche: Réunion de lancement]
├── Personnel
│   ├── Santé
│   │   └── [Tâche: Rendez-vous médecin]
│   └── Finances
│       ├── [Tâche: Payer les factures]
│       └── [Tâche: Vérifier le budget]
└── Loisirs
    └── [Tâche: Finir le livre]
```

---

### Implémentation en JavaScript

```javascript
// Représentation d'un nœud de catégorie
class NoeudCategorie {
  constructor(nom, estTache = false) {
    this.nom = nom;
    this.estTache = estTache;
    this.enfants = [];
    this.parent = null;
  }

  // Ajouter un enfant (sous-catégorie ou tâche)
  ajouterEnfant(enfant) {
    enfant.parent = this;
    this.enfants.push(enfant);
    return enfant;
  }

  // Obtenir le chemin complet jusqu'à la racine
  obtenirChemin() {
    const chemin = [];
    let noeud = this;
    while (noeud) {
      chemin.unshift(noeud.nom);
      noeud = noeud.parent;
    }
    return chemin.join(" > ");
  }

  // Compter toutes les tâches dans ce sous-arbre
  compterTaches() {
    if (this.estTache) {
      return 1;
    }
    let total = 0;
    for (const enfant of this.enfants) {
      total += enfant.compterTaches();
    }
    return total;
  }

  // Lister toutes les tâches dans ce sous-arbre
  listerTaches() {
    const taches = [];
    if (this.estTache) {
      taches.push(this.obtenirChemin());
    }
    for (const enfant of this.enfants) {
      taches.push(...enfant.listerTaches());
    }
    return taches;
  }
}

// Créer l'arbre de catégories de Germain
const racine = new NoeudCategorie("Tâches de Germain");

const travail = racine.ajouterEnfant(new NoeudCategorie("Travail"));
const projetAlpha = travail.ajouterEnfant(new NoeudCategorie("Projet Alpha"));
const conception = projetAlpha.ajouterEnfant(new NoeudCategorie("Conception"));
conception.ajouterEnfant(new NoeudCategorie("Créer les maquettes", true));

const dev = projetAlpha.ajouterEnfant(new NoeudCategorie("Développement"));
dev.ajouterEnfant(new NoeudCategorie("Implémenter le frontend", true));
dev.ajouterEnfant(new NoeudCategorie("Développer l'API", true));

const tests = projetAlpha.ajouterEnfant(new NoeudCategorie("Tests"));
tests.ajouterEnfant(new NoeudCategorie("Écrire les tests unitaires", true));

const projetBeta = travail.ajouterEnfant(new NoeudCategorie("Projet Beta"));
projetBeta.ajouterEnfant(new NoeudCategorie("Réunion de lancement", true));

const personnel = racine.ajouterEnfant(new NoeudCategorie("Personnel"));
const sante = personnel.ajouterEnfant(new NoeudCategorie("Santé"));
sante.ajouterEnfant(new NoeudCategorie("Rendez-vous médecin", true));

// Tests
console.log("Total de tâches :", racine.compterTaches()); // 7
console.log("Tâches dans Travail :", travail.compterTaches()); // 5
console.log("Tâches dans Projet Alpha :", projetAlpha.compterTaches()); // 4

console.log("\nToutes les tâches :");
racine.listerTaches().forEach((t) => console.log("  - " + t));
```

---

### Avantages de l'Approche Arborescente

| Avantage                 | Description                                                           |
| ------------------------ | --------------------------------------------------------------------- |
| **Organisation logique** | Hiérarchie naturelle par catégories                                   |
| **Filtrage facile**      | Sélectionner une catégorie inclut automatiquement ses sous-catégories |
| **Permissions**          | Appliquer des règles à une catégorie cascade aux sous-catégories      |
| **Scalabilité**          | Profondeur illimitée sans modification du code                        |

---

## 📝 Micro-Exercice #3 : Compléter l'Arbre

**Objectif :** Ajouter des catégories à l'arbre de Germain.

**Instructions :** Complétez le code pour ajouter :

- Une sous-catégorie "Finances" sous "Personnel" avec la tâche "Vérifier le budget"
- Une catégorie "Loisirs" à la racine avec la tâche "Finir le livre"

<details>
<summary>💡 Voir la solution</summary>

```javascript
// Ajouter Finances sous Personnel
const finances = personnel.ajouterEnfant(new NoeudCategorie("Finances"));
finances.ajouterEnfant(new NoeudCategorie("Vérifier le budget", true));

// Ajouter Loisirs à la racine
const loisirs = racine.ajouterEnfant(new NoeudCategorie("Loisirs"));
loisirs.ajouterEnfant(new NoeudCategorie("Finir le livre", true));

// Vérification
console.log("Nouveau total :", racine.compterTaches()); // 9
```

</details>

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension des arbres, complétez les exercices suivants.

---

### Exercice 1 : Identifier la Terminologie

**Objectif :** Analyser une structure arborescente.

**Instructions :** Considérez cette structure de fichiers :

```
/
├── home
│   ├── sarr
│   │   ├── docs
│   │   │   └── rapport.pdf
│   │   └── photos
│   │       ├── vacances.jpg
│   │       └── profil.png
│   └── sing
│       └── notes.txt
└── var
    └── log
        └── systeme.log
```

Répondez aux questions :
a. Quelle est la racine ?
b. Listez les enfants de `/home`
c. Qui est le parent de `rapport.pdf` ?
d. Listez les frères/sœurs de `sarr`
e. Listez toutes les feuilles
f. Quelle est la profondeur de `vacances.jpg` ?
g. Quelle est la hauteur du nœud `sarr` ?
h. Quelle est la hauteur de l'arbre ?
i. Quel est le degré du nœud `photos` ?

<details>
<summary>💡 Voir la solution</summary>

a. **Racine** : `/`
b. **Enfants de `/home`** : `sarr`, `sing`
c. **Parent de `rapport.pdf`** : `docs`
d. **Frères/sœurs de `sarr`** : `sing`
e. **Feuilles** : `rapport.pdf`, `vacances.jpg`, `profil.png`, `notes.txt`, `systeme.log`
f. **Profondeur de `vacances.jpg`** : 4 (/ → home → sarr → photos → vacances.jpg)
g. **Hauteur de `sarr`** : 2 (chemin le plus long : sarr → photos → vacances.jpg)
h. **Hauteur de l'arbre** : 4
i. **Degré de `photos`** : 2 (vacances.jpg et profil.png)

</details>

---

### Exercice 2 : Classifier les Types d'Arbres

**Objectif :** Identifier le type d'arbre le plus précis.

**Instructions :** Pour chaque description, choisissez parmi : Arbre Général, Arbre Binaire, Arbre Binaire Plein, Arbre Binaire Complet, Arbre Binaire Parfait.

a. Un arbre où chaque nœud a 0 ou 2 enfants, et toutes les feuilles sont au niveau 3
b. Un arbre où la racine a 5 enfants, chacun ayant un nombre variable d'enfants
c. Un arbre où chaque nœud a au maximum 2 enfants
d. Un arbre où tous les niveaux sont remplis sauf le dernier (rempli de gauche à droite)
e. Un arbre où chaque nœud a exactement 0 ou 2 enfants

<details>
<summary>💡 Voir la solution</summary>

a. **Arbre Binaire Parfait** (plein + feuilles au même niveau)
b. **Arbre Général** (plus de 2 enfants)
c. **Arbre Binaire** (définition de base)
d. **Arbre Binaire Complet**
e. **Arbre Binaire Plein**

</details>

---

### Exercice 3 : Associer les Cas d'Usage

**Objectif :** Choisir le bon type d'arbre pour chaque scénario.

**Instructions :** Associez chaque scénario au type d'arbre le plus approprié.

**Scénarios :**
a. Organisation hiérarchique d'une entreprise avec plusieurs niveaux de management
b. Stockage de nombres permettant une recherche très rapide (gauche < racine < droite)
c. Représentation d'une famille où chaque personne peut avoir un nombre quelconque d'enfants
d. Implémentation d'une file de priorité efficace

**Types disponibles :** Arbre Général, Arbre Binaire de Recherche (BST), Tas (Heap)

<details>
<summary>💡 Voir la solution</summary>

a. **Arbre Général** - nombre variable de subordonnés par manager
b. **Arbre Binaire de Recherche (BST)** - propriété gauche < racine < droite
c. **Arbre Général** - nombre variable d'enfants
d. **Tas (Heap)** - accès O(1) au min/max, structure de arbre binaire complet

</details>

---

### Exercice 4 : Implémenter un Nœud d'Arbre Binaire

**Objectif :** Créer une classe représentant un nœud d'arbre binaire.

**Instructions :** Implémentez une classe `NoeudBinaire` avec :

- Un constructeur prenant une valeur
- Des propriétés `gauche` et `droite` (initialement null)
- Une méthode `estFeuille()` retournant `true` si le nœud n'a pas d'enfants

<details>
<summary>💡 Voir la solution</summary>

```javascript
class NoeudBinaire {
  constructor(valeur) {
    this.valeur = valeur;
    this.gauche = null;
    this.droite = null;
  }

  estFeuille() {
    return this.gauche === null && this.droite === null;
  }
}

// Test
const racine = new NoeudBinaire(10);
console.log(racine.estFeuille()); // true

racine.gauche = new NoeudBinaire(5);
console.log(racine.estFeuille()); // false
console.log(racine.gauche.estFeuille()); // true
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Qu'est-ce qui distingue un arbre d'une liste chaînée ?**

- [ ] A. Un arbre a plus de nœuds
- [ ] B. Un arbre est une structure linéaire
- [ ] C. Un arbre permet à chaque nœud d'avoir plusieurs enfants
- [ ] D. Un arbre n'utilise pas de références

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un arbre est une structure **non linéaire** où chaque nœud peut avoir **plusieurs enfants**, contrairement à une liste chaînée où chaque nœud n'a qu'un seul successeur.

</details>

---

### Question 2

**Dans un arbre, qu'est-ce qu'une feuille ?**

- [ ] A. Un nœud qui a exactement deux enfants
- [ ] B. Un nœud qui n'a aucun enfant
- [ ] C. Le nœud situé au sommet de l'arbre
- [ ] D. Un nœud qui n'a pas de parent

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Une **feuille** est un nœud qui n'a **aucun enfant**. Ce sont les nœuds aux extrémités des branches de l'arbre.

</details>

---

### Question 3

**Si un arbre a 10 nœuds, combien d'arêtes a-t-il ?**

- [ ] A. 10
- [ ] B. 11
- [ ] C. 9
- [ ] D. 20

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un arbre avec **n nœuds** a exactement **n-1 arêtes**. Donc 10 nœuds = **9 arêtes**.

</details>

---

### Question 4

**Quelle est la différence entre la profondeur et la hauteur d'un nœud ?**

- [ ] A. Ce sont des synonymes
- [ ] B. Profondeur = distance à la racine, Hauteur = distance à la feuille la plus loin
- [ ] C. Hauteur = distance à la racine, Profondeur = distance à la feuille la plus loin
- [ ] D. Il n'y a pas de différence significative

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

- **Profondeur** = nombre d'arêtes de la **racine** au nœud (compté vers le bas)
- **Hauteur** = nombre d'arêtes du nœud à la **feuille la plus éloignée** (compté vers le bas)

</details>

---

### Question 5

**Quelle est la caractéristique principale d'un arbre binaire de recherche (BST) ?**

- [ ] A. Chaque nœud a exactement 2 enfants
- [ ] B. Gauche < Racine < Droite pour chaque nœud
- [ ] C. Toutes les feuilles sont au même niveau
- [ ] D. C'est un arbre équilibré

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Dans un BST, pour chaque nœud : tous les nœuds du **sous-arbre gauche** sont **inférieurs**, et tous les nœuds du **sous-arbre droit** sont **supérieurs**.

</details>

---

### Question 6

**Quel type d'arbre est utilisé pour implémenter efficacement une file de priorité ?**

- [ ] A. Arbre binaire de recherche
- [ ] B. Arbre général
- [ ] C. Tas (Heap) - Arbre binaire complet
- [ ] D. Arbre binaire parfait

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un **tas (heap)** est un arbre binaire **complet** qui permet d'accéder au minimum ou maximum en **O(1)** et d'insérer/supprimer en **O(log n)**.

</details>

---

### Question 7

**Combien de nœuds possède un arbre binaire parfait de hauteur 3 ?**

- [ ] A. 7
- [ ] B. 8
- [ ] C. 15
- [ ] D. 16

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un arbre binaire parfait de hauteur h a **2^(h+1) - 1** nœuds.
Pour h = 3 : 2^4 - 1 = 16 - 1 = **15 nœuds**.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Structure Hiérarchique

Les arbres organisent les données en relations parent-enfant, contrairement aux structures linéaires (tableaux, listes).

### 2. Terminologie Essentielle

Racine (sommet), feuilles (extrémités), nœuds internes (avec enfants), arêtes (liens), profondeur (distance à la racine), hauteur (distance à la feuille la plus loin).

### 3. Propriété des Arêtes

Un arbre avec n nœuds a exactement n-1 arêtes.

### 4. Types d'Arbres Binaires

Binaire (max 2 enfants), plein (0 ou 2 enfants), complet (rempli gauche→droite), parfait (plein + feuilles au même niveau).

### 5. BST (Binary Search Tree)

Propriété d'ordre : gauche < racine < droite. Permet recherche/insertion/suppression en O(log n) moyen.

### 6. Nature Récursive

Chaque nœud est la racine de son propre sous-arbre, ce qui rend les arbres idéaux pour les algorithmes récursifs.

### 7. Applications Clés

Systèmes de fichiers, DOM HTML, indexation de bases de données, arbres d'expression, arbres de décision.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez découvert les arbres, une des structures de données les plus importantes en informatique !

### Ce que vous avez appris aujourd'hui

- La structure hiérarchique des arbres et leur différence avec les structures linéaires
- La terminologie complète : nœud, racine, feuille, profondeur, hauteur, sous-arbre
- Les différents types d'arbres binaires et leurs propriétés
- Les cas d'usage réels : systèmes de fichiers, DOM, bases de données
- L'implémentation basique d'un nœud d'arbre en JavaScript

### Compétences acquises

Vous êtes maintenant capable de :

- Identifier et décrire les composants d'un arbre
- Choisir le bon type d'arbre pour un problème donné
- Comprendre pourquoi la récursion est naturelle pour les arbres

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Les arbres sont **omniprésents** en informatique. Chaque fois que vous naviguez dans des fichiers, visitez une page web, ou effectuez une recherche dans une base de données, vous interagissez avec des structures arborescentes. Comprendre les arbres est **fondamental** pour devenir un développeur compétent.

---

## ➡️ Prochaine Étape : Leçon 26

### Ce qui vous attend

La prochaine leçon, **« Arbres de Recherche Binaires (BST) : Insertion et Recherche en JavaScript »**, vous apprendra à implémenter et utiliser cette structure de données puissante.

**Vous découvrirez :**

- L'**implémentation complète** d'un BST en JavaScript
- Comment **insérer** des éléments en respectant la propriété d'ordre
- Comment **rechercher** efficacement une valeur
- L'analyse de **complexité** des opérations

### Préparez-vous !

Les BST combinent la structure des arbres avec la propriété d'ordre pour permettre des recherches ultra-rapides. C'est une structure que vous utiliserez très souvent !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Binary Tree](https://visualgo.net/en/bst) - Visualisation interactive
- [MDN - Document Object Model](https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model) - Le DOM comme arbre
- [CS50 - Trees](https://cs50.harvard.edu/x/2024/shorts/trees/) - Cours Harvard

### Outils de pratique

- **[Binary Tree Visualizer](https://www.cs.usfca.edu/~galles/visualization/BST.html)** : Créez et manipulez des arbres
- 🔧 **DevTools DOM** : Inspectez l'arbre DOM de n'importe quelle page web

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Dessiner des arbres sur papier pour mieux visualiser
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour bien comprendre les arbres, **dessinez-les** ! Prenez un papier et tracez la structure des exemples de cette leçon. Identifiez visuellement les racines, feuilles, profondeurs et hauteurs. Cette pratique visuelle rendra les concepts beaucoup plus concrets.

---

**Prêt pour la Leçon 26 ?** 🚀

Rendez-vous dans la prochaine leçon pour maîtriser les Arbres de Recherche Binaires !

---

<div align="center">

**Leçon 25 sur 42 - Module 5 : Arbres et Parcours de Graphes**

[⬅️ Module 4 : Recherche et Récursion](../module-4/README.md) | [Retour au sommaire](./README.md) | [Leçon 26 : Arbres de Recherche Binaires ➡️](./lecon-2-arbres-recherche-binaires-insertion-recherche-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
