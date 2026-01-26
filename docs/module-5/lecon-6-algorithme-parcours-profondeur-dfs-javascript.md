##### Leçon 30 sur 42

# Algorithme de Parcours en Profondeur (DFS) en JavaScript

**Module 5** : Arbres et Parcours de Graphes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **principe du DFS** (exploration en profondeur)
- Différencier les parcours **pré-ordre, in-ordre et post-ordre** pour les arbres
- Implémenter le DFS de manière **récursive** et **itérative**
- Utiliser une **pile (stack)** pour le DFS itératif
- **Détecter les cycles** dans un graphe avec le DFS
- Comparer **DFS vs BFS** et choisir le bon algorithme

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 29 complétée** : Parcours en largeur (BFS)
- **Module 4** : Récursion et pile d'appels
- **Module 2** : Piles (Stacks) et principe LIFO
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Explorer en Profondeur

Dans la leçon précédente, nous avons vu le **BFS** qui explore "niveau par niveau". Le **DFS (Depth-First Search)** adopte une stratégie opposée : il explore **aussi loin que possible** le long de chaque branche avant de revenir en arrière.

Imaginez que vous explorez un labyrinthe :

- **BFS** : Vous explorez toutes les intersections à 1 pas, puis à 2 pas, etc.
- **DFS** : Vous choisissez un chemin et le suivez jusqu'au bout (ou jusqu'à un cul-de-sac), puis vous revenez en arrière pour essayer un autre chemin.

> **Point Clé**
>
> Le DFS utilise une **pile** (explicite ou implicite via la récursion) au lieu d'une file. Cela lui permet de "mémoriser" le chemin parcouru et de revenir en arrière (backtracking) quand nécessaire.

---

## 📦 Principe du DFS : La Pile (Stack)

Le DFS utilise une **pile** pour gérer l'ordre de visite des sommets.

---

### Rappel : Structure LIFO

Une **pile** suit le principe **LIFO** (Last In, First Out) :

- Le dernier élément ajouté est le premier retiré
- Comme une pile d'assiettes !

```
Pile :  [A] [B] [C] [D]
                     ↑
                  Sommet
                  (dernier ajouté,
                   premier retiré)

Opérations :
- push(E) → [A] [B] [C] [D] [E]  (ajouter au sommet)
- pop()   → [A] [B] [C] [D]     (retirer du sommet, retourne E)
```

---

### Algorithme DFS Pas à Pas

```
1. INITIALISATION :
   - Créer une pile vide (ou utiliser la récursion)
   - Créer un ensemble "visités" vide
   - Ajouter le sommet de départ à la pile
   - Marquer le sommet de départ comme visité

2. EXPLORATION (tant que la pile n'est pas vide) :
   a. Retirer l'élément du sommet de la pile (pop)
   b. Traiter ce sommet
   c. Pour chaque voisin non visité :
      - Le marquer comme visité
      - L'ajouter à la pile (push)

3. TERMINAISON :
   - La pile est vide = tous les sommets accessibles ont été visités
```

---

### Visualisation : DFS vs BFS

```
Graphe :
        [A]
       /   \
     [B]   [C]
     / \     \
   [D] [E]   [F]

BFS depuis A (file - FIFO) :      DFS depuis A (pile - LIFO) :
Ordre : A → B → C → D → E → F     Ordre : A → C → F → B → E → D
(niveau par niveau)               (en profondeur d'abord)

BFS :                             DFS :
    [A]          Niveau 0             [A]
   /   \                             /   \
  [B]  [C]       Niveau 1           [C]  [B]
  / \    \                           \    / \
[D] [E]  [F]     Niveau 2           [F] [E] [D]

Exploration horizontale           Exploration verticale
```

---

## 🌳 Parcours DFS sur les Arbres Binaires

Pour les arbres binaires, le DFS a trois variantes selon **quand** on traite le nœud courant.

---

### Les Trois Types de Parcours

```
Arbre exemple :
        [A]
       /   \
     [B]   [C]
     / \
   [D] [E]
```

| Parcours       | Ordre des actions      | Résultat      |
| -------------- | ---------------------- | ------------- |
| **Pré-ordre**  | Nœud → Gauche → Droite | A, B, D, E, C |
| **In-ordre**   | Gauche → Nœud → Droite | D, B, E, A, C |
| **Post-ordre** | Gauche → Droite → Nœud | D, E, B, C, A |

---

### Implémentation des Trois Parcours

```javascript
/**
 * Structure d'un nœud d'arbre binaire.
 */
class NoeudArbre {
  constructor(valeur) {
    this.valeur = valeur;
    this.gauche = null;
    this.droite = null;
  }
}

/**
 * Parcours PRÉ-ORDRE : Nœud → Gauche → Droite
 * Utile pour : copier un arbre, sérialiser
 */
function parcoursPreOrdre(noeud, resultat = []) {
  if (noeud === null) return resultat;

  resultat.push(noeud.valeur); // 1. Traiter le nœud
  parcoursPreOrdre(noeud.gauche, resultat); // 2. Gauche
  parcoursPreOrdre(noeud.droite, resultat); // 3. Droite

  return resultat;
}

/**
 * Parcours IN-ORDRE : Gauche → Nœud → Droite
 * Utile pour : BST (donne les valeurs triées)
 */
function parcoursInOrdre(noeud, resultat = []) {
  if (noeud === null) return resultat;

  parcoursInOrdre(noeud.gauche, resultat); // 1. Gauche
  resultat.push(noeud.valeur); // 2. Traiter le nœud
  parcoursInOrdre(noeud.droite, resultat); // 3. Droite

  return resultat;
}

/**
 * Parcours POST-ORDRE : Gauche → Droite → Nœud
 * Utile pour : supprimer un arbre, calculer la taille
 */
function parcoursPostOrdre(noeud, resultat = []) {
  if (noeud === null) return resultat;

  parcoursPostOrdre(noeud.gauche, resultat); // 1. Gauche
  parcoursPostOrdre(noeud.droite, resultat); // 2. Droite
  resultat.push(noeud.valeur); // 3. Traiter le nœud

  return resultat;
}

// Construire l'arbre exemple
//        [10]
//       /    \
//     [5]    [15]
//     / \      \
//   [3] [7]   [20]

const racine = new NoeudArbre(10);
racine.gauche = new NoeudArbre(5);
racine.droite = new NoeudArbre(15);
racine.gauche.gauche = new NoeudArbre(3);
racine.gauche.droite = new NoeudArbre(7);
racine.droite.droite = new NoeudArbre(20);

console.log("Pré-ordre :", parcoursPreOrdre(racine));
// [10, 5, 3, 7, 15, 20]

console.log("In-ordre :", parcoursInOrdre(racine));
// [3, 5, 7, 10, 15, 20] → valeurs triées ! (c'est un BST)

console.log("Post-ordre :", parcoursPostOrdre(racine));
// [3, 7, 5, 20, 15, 10]
```

---

### Cas d'Usage de Chaque Parcours

| Parcours       | Cas d'usage                                |
| -------------- | ------------------------------------------ |
| **Pré-ordre**  | Copier un arbre, sérialiser pour stockage  |
| **In-ordre**   | Obtenir les valeurs triées d'un BST        |
| **Post-ordre** | Supprimer un arbre (enfants avant parents) |

---

## 📝 Micro-Exercice #1 : Identifier le Type de Parcours

**Objectif :** Reconnaître les différents parcours.

**Instructions :** Pour cet arbre, quel parcours donne le résultat `[F, D, E, B, G, C, A]` ?

```
        [A]
       /   \
     [B]   [C]
     / \     \
   [D] [E]   [G]
   /
 [F]
```

<details>
<summary>💡 Voir la solution</summary>

```
C'est le parcours POST-ORDRE (Gauche → Droite → Nœud)

Vérification :
1. Aller à gauche de A → B
2. Aller à gauche de B → D
3. Aller à gauche de D → F
4. F n'a pas d'enfants → Traiter F ✓
5. Retour à D, pas de droite → Traiter D ✓
6. Retour à B, aller à droite → E
7. E n'a pas d'enfants → Traiter E ✓
8. Retour à B → Traiter B ✓
9. Retour à A, aller à droite → C
10. C, aller à droite → G
11. G n'a pas d'enfants → Traiter G ✓
12. Retour à C → Traiter C ✓
13. Retour à A → Traiter A ✓

Résultat : F, D, E, B, G, C, A ✓
```

</details>

---

## 💻 DFS pour les Graphes : Implémentation Récursive

Pour les graphes, on utilise un ensemble `visites` pour éviter les boucles infinies.

---

### Représentation du Graphe

```javascript
// Graphe exemple (non orienté)
//     [A]---[B]
//     | \  / |
//     |  \/  |
//     |  /\  |
//     | /  \ |
//     [C]---[D]

const graphe = {
  A: ["B", "C", "D"],
  B: ["A", "D"],
  C: ["A", "D"],
  D: ["A", "B", "C"],
};
```

---

### DFS Récursif

```javascript
/**
 * Parcours en profondeur récursif sur un graphe.
 * @param {Object} graphe - Le graphe en liste d'adjacence.
 * @param {string} depart - Le sommet de départ.
 * @returns {string[]} - L'ordre de visite des sommets.
 */
function dfsRecursif(graphe, depart) {
  const visites = new Set();
  const resultat = [];

  /**
   * Fonction récursive d'exploration.
   */
  function explorer(sommet) {
    // Cas de base : sommet invalide ou déjà visité
    if (!sommet || visites.has(sommet)) {
      return;
    }

    // Marquer comme visité et traiter
    visites.add(sommet);
    resultat.push(sommet);

    // Explorer récursivement tous les voisins non visités
    const voisins = graphe[sommet] || [];
    for (const voisin of voisins) {
      explorer(voisin);
    }
  }

  // Lancer l'exploration
  explorer(depart);
  return resultat;
}

// Test
const grapheTest = {
  A: ["B", "C", "D"],
  B: ["A", "D"],
  C: ["A", "D"],
  D: ["A", "B", "C"],
};

console.log("DFS récursif depuis A :", dfsRecursif(grapheTest, "A"));
// Possible : ['A', 'B', 'D', 'C'] (dépend de l'ordre des voisins)
```

---

### Trace d'Exécution

```
dfsRecursif(graphe, 'A') avec graphe['A'] = ['B', 'C', 'D']

Appel : explorer('A')
  → visites = {A}, resultat = ['A']
  → voisins de A : ['B', 'C', 'D']

  Appel : explorer('B')
    → visites = {A, B}, resultat = ['A', 'B']
    → voisins de B : ['A', 'D']

    Appel : explorer('A') → déjà visité, RETOUR

    Appel : explorer('D')
      → visites = {A, B, D}, resultat = ['A', 'B', 'D']
      → voisins de D : ['A', 'B', 'C']

      Appel : explorer('A') → déjà visité, RETOUR
      Appel : explorer('B') → déjà visité, RETOUR

      Appel : explorer('C')
        → visites = {A, B, D, C}, resultat = ['A', 'B', 'D', 'C']
        → voisins de C : ['A', 'D']

        Appel : explorer('A') → déjà visité, RETOUR
        Appel : explorer('D') → déjà visité, RETOUR

      FIN explorer('C')
    FIN explorer('D')
  FIN explorer('B')

  Appel : explorer('C') → déjà visité, RETOUR
  Appel : explorer('D') → déjà visité, RETOUR
FIN explorer('A')

Résultat final : ['A', 'B', 'D', 'C']
```

---

## 📝 Micro-Exercice #2 : Tracer un DFS Récursif

**Objectif :** Comprendre l'ordre de visite du DFS.

**Instructions :** Tracez le DFS récursif depuis 'X' :

```javascript
const graphe = {
  X: ["Y", "Z"],
  Y: ["X", "W"],
  Z: ["X"],
  W: ["Y", "V"],
  V: ["W"],
};
```

<details>
<summary>💡 Voir la solution</summary>

```
explorer('X')
  → visites = {X}, resultat = ['X']

  explorer('Y')
    → visites = {X, Y}, resultat = ['X', 'Y']

    explorer('X') → déjà visité

    explorer('W')
      → visites = {X, Y, W}, resultat = ['X', 'Y', 'W']

      explorer('Y') → déjà visité

      explorer('V')
        → visites = {X, Y, W, V}, resultat = ['X', 'Y', 'W', 'V']

        explorer('W') → déjà visité

      FIN explorer('V')
    FIN explorer('W')
  FIN explorer('Y')

  explorer('Z')
    → visites = {X, Y, W, V, Z}, resultat = ['X', 'Y', 'W', 'V', 'Z']

    explorer('X') → déjà visité
  FIN explorer('Z')
FIN explorer('X')

Résultat : ['X', 'Y', 'W', 'V', 'Z']
```

</details>

---

## 💻 DFS pour les Graphes : Implémentation Itérative

L'implémentation itérative utilise une **pile explicite** au lieu de la récursion.

---

### DFS Itératif avec Pile

```javascript
/**
 * Parcours en profondeur itératif sur un graphe.
 * @param {Object} graphe - Le graphe en liste d'adjacence.
 * @param {string} depart - Le sommet de départ.
 * @returns {string[]} - L'ordre de visite des sommets.
 */
function dfsIteratif(graphe, depart) {
  // Vérifier que le sommet existe
  if (!graphe[depart]) {
    return [];
  }

  const pile = [depart]; // Pile initialisée avec le départ
  const visites = new Set();
  const resultat = [];

  visites.add(depart); // Marquer le départ comme visité

  while (pile.length > 0) {
    // Retirer le sommet du haut de la pile (LIFO)
    const sommetActuel = pile.pop();
    resultat.push(sommetActuel);

    // Ajouter les voisins non visités à la pile
    // Note : On itère en sens inverse pour garder un ordre similaire au récursif
    const voisins = graphe[sommetActuel] || [];

    for (let i = voisins.length - 1; i >= 0; i--) {
      const voisin = voisins[i];
      if (!visites.has(voisin)) {
        visites.add(voisin);
        pile.push(voisin);
      }
    }
  }

  return resultat;
}

// Test
const grapheTest = {
  A: ["B", "C", "D"],
  B: ["A", "D"],
  C: ["A", "D"],
  D: ["A", "B", "C"],
};

console.log("DFS itératif depuis A :", dfsIteratif(grapheTest, "A"));
// ['A', 'B', 'D', 'C'] (avec itération inverse)
```

---

### Comparaison Récursif vs Itératif

| Aspect          | Récursif                  | Itératif                    |
| --------------- | ------------------------- | --------------------------- |
| **Code**        | Plus simple, plus lisible | Plus verbeux                |
| **Pile**        | Implicite (call stack)    | Explicite (tableau)         |
| **Limite**      | Risque de stack overflow  | Pas de limite de profondeur |
| **Contrôle**    | Moins de contrôle         | Plus de contrôle            |
| **Performance** | Légèrement plus lent      | Légèrement plus rapide      |

> **Attention**
>
> En JavaScript, la **pile d'appels** a une limite (environ 10 000-20 000 appels selon le moteur). Pour de très grands graphes, préférez la version **itérative**.

---

### Version Alternative : Sans Inverser l'Ordre

```javascript
/**
 * DFS itératif sans inversion (ordre légèrement différent).
 */
function dfsIteratifSimple(graphe, depart) {
  if (!graphe[depart]) return [];

  const pile = [depart];
  const visites = new Set();
  const resultat = [];

  while (pile.length > 0) {
    const sommet = pile.pop();

    // Vérifier si déjà visité (car on marque au pop, pas au push)
    if (visites.has(sommet)) continue;

    visites.add(sommet);
    resultat.push(sommet);

    // Ajouter les voisins (pas besoin de vérifier visites ici)
    for (const voisin of graphe[sommet] || []) {
      if (!visites.has(voisin)) {
        pile.push(voisin);
      }
    }
  }

  return resultat;
}
```

---

## 📝 Micro-Exercice #3 : DFS Itératif

**Objectif :** Tracer l'exécution du DFS itératif.

**Instructions :** Tracez l'état de la pile à chaque étape pour ce graphe :

```javascript
const graphe = {
  1: ["2", "3"],
  2: ["4"],
  3: ["5"],
  4: [],
  5: [],
};
```

<details>
<summary>💡 Voir la solution</summary>

```
Départ : '1'

Étape 0 : Pile = ['1'], Visités = {'1'}, Résultat = []
          → Pop '1', ajouter '3' puis '2' (ordre inverse)

Étape 1 : Pile = ['3', '2'], Visités = {'1', '2', '3'}, Résultat = ['1']
          → Pop '2', ajouter '4'

Étape 2 : Pile = ['3', '4'], Visités = {'1', '2', '3', '4'}, Résultat = ['1', '2']
          → Pop '4', pas de voisins

Étape 3 : Pile = ['3'], Visités = {'1', '2', '3', '4'}, Résultat = ['1', '2', '4']
          → Pop '3', ajouter '5'

Étape 4 : Pile = ['5'], Visités = {'1', '2', '3', '4', '5'}, Résultat = ['1', '2', '4', '3']
          → Pop '5', pas de voisins

Étape 5 : Pile = [], TERMINÉ
          Résultat final : ['1', '2', '4', '3', '5']
```

</details>

---

## 🔄 Application : Détection de Cycles avec DFS

Le DFS est particulièrement efficace pour détecter les **cycles** dans un graphe.

---

### Principe de la Détection

Pour un graphe **non orienté** :

- Un cycle existe si on rencontre un sommet déjà visité qui n'est pas le parent direct.

Pour un graphe **orienté** :

- Un cycle existe si on rencontre un sommet qui est déjà dans le "chemin actuel" (pile de récursion).

---

### Détection de Cycle dans un Graphe Non Orienté

```javascript
/**
 * Détecte si un graphe non orienté contient un cycle.
 * @param {Object} graphe - Le graphe en liste d'adjacence.
 * @returns {boolean} - True si un cycle existe.
 */
function detecterCycleNonOriente(graphe) {
  const visites = new Set();

  /**
   * Explore récursivement en mémorisant le parent.
   */
  function dfs(sommet, parent) {
    visites.add(sommet);

    for (const voisin of graphe[sommet] || []) {
      if (!visites.has(voisin)) {
        // Explorer le voisin non visité
        if (dfs(voisin, sommet)) {
          return true; // Cycle trouvé plus profond
        }
      } else if (voisin !== parent) {
        // Voisin déjà visité et ce n'est pas le parent → CYCLE !
        return true;
      }
    }

    return false;
  }

  // Lancer DFS depuis chaque composante
  for (const sommet of Object.keys(graphe)) {
    if (!visites.has(sommet)) {
      if (dfs(sommet, null)) {
        return true;
      }
    }
  }

  return false;
}

// Tests
const grapheAvecCycle = {
  A: ["B", "C"],
  B: ["A", "C"], // B-C crée un cycle A-B-C-A
  C: ["A", "B"],
};

const grapheSansCycle = {
  A: ["B", "C"],
  B: ["A"],
  C: ["A"],
};

console.log(
  "Graphe triangle a un cycle ?",
  detecterCycleNonOriente(grapheAvecCycle),
);
// true

console.log(
  "Graphe étoile a un cycle ?",
  detecterCycleNonOriente(grapheSansCycle),
);
// false
```

---

### Détection de Cycle dans un Graphe Orienté

```javascript
/**
 * Détecte si un graphe orienté contient un cycle.
 * Utilise trois états : non visité, en cours, terminé.
 */
function detecterCycleOriente(graphe) {
  const BLANC = 0; // Non visité
  const GRIS = 1; // En cours de visite (dans la pile de récursion)
  const NOIR = 2; // Visité et terminé

  const couleurs = new Map();

  // Initialiser tous les sommets à BLANC
  for (const sommet of Object.keys(graphe)) {
    couleurs.set(sommet, BLANC);
  }

  function dfs(sommet) {
    couleurs.set(sommet, GRIS); // Marquer en cours

    for (const voisin of graphe[sommet] || []) {
      if (couleurs.get(voisin) === GRIS) {
        // Voisin GRIS = dans le chemin actuel → CYCLE !
        return true;
      }
      if (couleurs.get(voisin) === BLANC) {
        if (dfs(voisin)) {
          return true;
        }
      }
    }

    couleurs.set(sommet, NOIR); // Marquer terminé
    return false;
  }

  // Lancer DFS depuis chaque sommet non visité
  for (const sommet of Object.keys(graphe)) {
    if (couleurs.get(sommet) === BLANC) {
      if (dfs(sommet)) {
        return true;
      }
    }
  }

  return false;
}

// Tests
const grapheOrienteAvecCycle = {
  A: ["B"],
  B: ["C"],
  C: ["A"], // C → A crée un cycle
};

const grapheOrienteSansCycle = {
  A: ["B", "C"],
  B: ["D"],
  C: ["D"],
  D: [],
};

console.log(
  "Graphe orienté avec cycle ?",
  detecterCycleOriente(grapheOrienteAvecCycle),
);
// true

console.log(
  "Graphe orienté sans cycle ?",
  detecterCycleOriente(grapheOrienteSansCycle),
);
// false (DAG - Directed Acyclic Graph)
```

---

## 📊 Comparaison : DFS vs BFS

Quand utiliser DFS ? Quand utiliser BFS ?

---

### Tableau Comparatif

| Critère                  | DFS                  | BFS                      |
| ------------------------ | -------------------- | ------------------------ |
| **Structure**            | Pile (LIFO)          | File (FIFO)              |
| **Exploration**          | En profondeur        | En largeur               |
| **Complexité temps**     | O(V + E)             | O(V + E)                 |
| **Complexité espace**    | O(V) pire cas        | O(V) pire cas            |
| **Chemin le plus court** | Non garanti          | Garanti (non pondéré)    |
| **Utilisation mémoire**  | Généralement moins   | Plus pour graphes larges |
| **Implémentation**       | Récursif ou itératif | Itératif (file)          |

---

### Quand Choisir DFS ?

**Utiliser DFS pour :**

- Détecter des **cycles**
- Explorer des **labyrinthes** (backtracking)
- Résoudre des **puzzles** (Sudoku, N-Queens)
- **Topological sort** (tri topologique)
- Vérifier la **connectivité**
- Trouver des **composantes fortement connexes**

---

### Quand Choisir BFS ?

**Utiliser BFS pour :**

- Trouver le **chemin le plus court** (non pondéré)
- Calculer les **distances** depuis une source
- Explorer **niveau par niveau**
- **Web crawling** avec limite de profondeur
- Réseaux sociaux (degrés de séparation)

---

### Visualisation Comparative

```
Graphe :
      [1]
     / | \
   [2][3][4]
   /     / \
 [5]   [6] [7]

BFS depuis 1 :              DFS depuis 1 :
Niveau 0: 1                 1 → 2 → 5 (fond)
Niveau 1: 2, 3, 4           retour → 3
Niveau 2: 5, 6, 7           retour → 4 → 6 (fond)
                            retour → 7 (fond)
Ordre: 1,2,3,4,5,6,7        Ordre: 1,2,5,3,4,6,7
(horizontal)                (vertical d'abord)
```

---

## 📊 Analyse de Complexité du DFS

| Opération             | Complexité | Explication                             |
| --------------------- | ---------- | --------------------------------------- |
| **Temps**             | O(V + E)   | Chaque sommet et arête visités une fois |
| **Espace (récursif)** | O(V)       | Profondeur max de la pile d'appels      |
| **Espace (itératif)** | O(V)       | Taille max de la pile explicite         |

---

## 💼 Application : Étude de Cas - Vérification de Connectivité

Utilisons le DFS pour vérifier si deux personnes sont connectées dans un réseau social.

---

### Scénario

Germain développe une fonctionnalité "Êtes-vous connectés ?" pour son réseau social. Deux personnes sont connectées s'il existe un chemin d'amitiés entre elles.

---

### Implémentation

```javascript
/**
 * Gestionnaire de réseau social avec vérification de connectivité.
 */
class ReseauSocialDFS {
  constructor() {
    this.connexions = {};
  }

  /**
   * Ajoute une amitié bidirectionnelle.
   */
  ajouterAmitie(personne1, personne2) {
    if (!this.connexions[personne1]) this.connexions[personne1] = [];
    if (!this.connexions[personne2]) this.connexions[personne2] = [];

    this.connexions[personne1].push(personne2);
    this.connexions[personne2].push(personne1);
  }

  /**
   * Vérifie si deux personnes sont connectées (DFS).
   */
  sontConnectes(personne1, personne2) {
    if (personne1 === personne2) return true;
    if (!this.connexions[personne1] || !this.connexions[personne2]) {
      return false;
    }

    const visites = new Set();

    function dfs(actuel, cible, graphe) {
      if (actuel === cible) return true;

      visites.add(actuel);

      for (const ami of graphe[actuel] || []) {
        if (!visites.has(ami)) {
          if (dfs(ami, cible, graphe)) {
            return true;
          }
        }
      }

      return false;
    }

    return dfs(personne1, personne2, this.connexions);
  }

  /**
   * Trouve le chemin entre deux personnes (DFS avec backtracking).
   */
  trouverChemin(personne1, personne2) {
    if (personne1 === personne2) return [personne1];
    if (!this.connexions[personne1] || !this.connexions[personne2]) {
      return null;
    }

    const visites = new Set();

    function dfs(actuel, cible, graphe, chemin) {
      visites.add(actuel);
      chemin.push(actuel);

      if (actuel === cible) {
        return [...chemin]; // Copie du chemin trouvé
      }

      for (const ami of graphe[actuel] || []) {
        if (!visites.has(ami)) {
          const resultat = dfs(ami, cible, graphe, chemin);
          if (resultat) return resultat;
        }
      }

      chemin.pop(); // Backtracking
      return null;
    }

    return dfs(personne1, personne2, this.connexions, []);
  }

  /**
   * Trouve toutes les composantes connexes du réseau.
   */
  trouverComposantes() {
    const visites = new Set();
    const composantes = [];

    const dfs = (sommet, composante) => {
      visites.add(sommet);
      composante.push(sommet);

      for (const voisin of this.connexions[sommet] || []) {
        if (!visites.has(voisin)) {
          dfs(voisin, composante);
        }
      }
    };

    for (const personne of Object.keys(this.connexions)) {
      if (!visites.has(personne)) {
        const composante = [];
        dfs(personne, composante);
        composantes.push(composante);
      }
    }

    return composantes;
  }

  /**
   * Affiche le réseau.
   */
  afficher() {
    console.log("=== Réseau Social ===");
    for (const [personne, amis] of Object.entries(this.connexions)) {
      console.log(`${personne}: [${amis.join(", ")}]`);
    }
  }
}

// Utilisation
const reseau = new ReseauSocialDFS();

// Groupe 1 : Équipe de développement
reseau.ajouterAmitie("Chermann", "Ingrid");
reseau.ajouterAmitie("Ingrid", "Prudence");
reseau.ajouterAmitie("Prudence", "Germain");

// Groupe 2 : Équipe marketing (déconnecté du groupe 1)
reseau.ajouterAmitie("Sarr", "Sing");
reseau.ajouterAmitie("Sing", "Destinée");

// Groupe 3 : Personne isolée
reseau.ajouterAmitie("Marc-Élie", "Marc-Élie"); // Pour créer le nœud

reseau.afficher();

console.log("\n=== Tests de Connectivité ===");
console.log(
  "Chermann ↔ Germain ?",
  reseau.sontConnectes("Chermann", "Germain"),
); // true
console.log("Chermann ↔ Sarr ?", reseau.sontConnectes("Chermann", "Sarr")); // false
console.log("Sarr ↔ Destinée ?", reseau.sontConnectes("Sarr", "Destinée")); // true

console.log("\n=== Chemins ===");
console.log(
  "Chemin Chermann → Germain :",
  reseau.trouverChemin("Chermann", "Germain"),
);
// ["Chermann", "Ingrid", "Prudence", "Germain"]

console.log("\n=== Composantes Connexes ===");
console.log(reseau.trouverComposantes());
// [["Chermann", "Ingrid", "Prudence", "Germain"], ["Sarr", "Sing", "Destinée"], ["Marc-Élie"]]
```

---

### Visualisation du Réseau

```
Groupe 1 (Dev) :          Groupe 2 (Marketing) :    Groupe 3 :
[Chermann]                [Sarr]                    [Marc-Élie]
    |                        |                      (isolé)
 [Ingrid]                 [Sing]
    |                        |
[Prudence]               [Destinée]
    |
 [Germain]

3 composantes connexes distinctes
```

---

## 💪 Exercices Pratiques

Consolidez vos connaissances avec ces exercices progressifs.

---

### Exercice 1 : Parcours d'Arbre BST

**Objectif :** Implémenter les trois parcours sur un BST.

**Instructions :** Construisez le BST suivant et affichez les trois parcours :

```
       [8]
      /   \
    [4]   [12]
    / \    / \
  [2] [6] [10][14]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class NoeudBST {
  constructor(valeur) {
    this.valeur = valeur;
    this.gauche = null;
    this.droite = null;
  }
}

// Construction du BST
const racine = new NoeudBST(8);
racine.gauche = new NoeudBST(4);
racine.droite = new NoeudBST(12);
racine.gauche.gauche = new NoeudBST(2);
racine.gauche.droite = new NoeudBST(6);
racine.droite.gauche = new NoeudBST(10);
racine.droite.droite = new NoeudBST(14);

function preOrdre(noeud, res = []) {
  if (!noeud) return res;
  res.push(noeud.valeur);
  preOrdre(noeud.gauche, res);
  preOrdre(noeud.droite, res);
  return res;
}

function inOrdre(noeud, res = []) {
  if (!noeud) return res;
  inOrdre(noeud.gauche, res);
  res.push(noeud.valeur);
  inOrdre(noeud.droite, res);
  return res;
}

function postOrdre(noeud, res = []) {
  if (!noeud) return res;
  postOrdre(noeud.gauche, res);
  postOrdre(noeud.droite, res);
  res.push(noeud.valeur);
  return res;
}

console.log("Pré-ordre :", preOrdre(racine));
// [8, 4, 2, 6, 12, 10, 14]

console.log("In-ordre :", inOrdre(racine));
// [2, 4, 6, 8, 10, 12, 14] ← Valeurs triées !

console.log("Post-ordre :", postOrdre(racine));
// [2, 6, 4, 10, 14, 12, 8]
```

</details>

---

### Exercice 2 : Vérifier la Connectivité

**Objectif :** Utiliser le DFS pour vérifier si un graphe est connexe.

**Instructions :** Créez une fonction `estConnexe(graphe)` qui retourne `true` si tous les sommets sont atteignables depuis n'importe quel autre.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function estConnexe(graphe) {
  const sommets = Object.keys(graphe);
  if (sommets.length === 0) return true;

  // DFS depuis le premier sommet
  const visites = new Set();

  function dfs(sommet) {
    visites.add(sommet);
    for (const voisin of graphe[sommet] || []) {
      if (!visites.has(voisin)) {
        dfs(voisin);
      }
    }
  }

  dfs(sommets[0]);

  // Connexe si tous les sommets ont été visités
  return visites.size === sommets.length;
}

// Tests
const grapheConnexe = {
  A: ["B", "C"],
  B: ["A", "C"],
  C: ["A", "B"],
};

const grapheNonConnexe = {
  A: ["B"],
  B: ["A"],
  X: ["Y"],
  Y: ["X"],
};

console.log("Graphe connexe ?", estConnexe(grapheConnexe)); // true
console.log("Graphe non connexe ?", estConnexe(grapheNonConnexe)); // false
```

</details>

---

### Exercice 3 : Trouver Tous les Chemins

**Objectif :** Trouver TOUS les chemins entre deux sommets.

**Instructions :** Créez `trouverTousLesChemins(graphe, depart, arrivee)`.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function trouverTousLesChemins(graphe, depart, arrivee) {
  const chemins = [];
  const cheminActuel = [];

  function dfs(sommet, visites) {
    visites.add(sommet);
    cheminActuel.push(sommet);

    if (sommet === arrivee) {
      chemins.push([...cheminActuel]); // Sauvegarder le chemin trouvé
    } else {
      for (const voisin of graphe[sommet] || []) {
        if (!visites.has(voisin)) {
          dfs(voisin, visites);
        }
      }
    }

    // Backtracking
    cheminActuel.pop();
    visites.delete(sommet);
  }

  dfs(depart, new Set());
  return chemins;
}

// Test
const graphe = {
  A: ["B", "C"],
  B: ["A", "C", "D"],
  C: ["A", "B", "D"],
  D: ["B", "C"],
};

console.log("Tous les chemins A → D :");
console.log(trouverTousLesChemins(graphe, "A", "D"));
// [['A', 'B', 'C', 'D'], ['A', 'B', 'D'], ['A', 'C', 'B', 'D'], ['A', 'C', 'D']]
```

</details>

---

### Exercice 4 : Résoudre un Labyrinthe

**Objectif :** Utiliser le DFS pour trouver la sortie d'un labyrinthe.

**Instructions :** Trouvez un chemin de 'S' (start) à 'E' (end) dans une grille.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function resoudreLabyrinthe(grille) {
  const lignes = grille.length;
  const colonnes = grille[0].length;

  // Trouver le départ 'S'
  let depart;
  for (let i = 0; i < lignes; i++) {
    for (let j = 0; j < colonnes; j++) {
      if (grille[i][j] === "S") {
        depart = [i, j];
        break;
      }
    }
  }

  const directions = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];
  const visites = new Set();

  function dfs(x, y, chemin) {
    // Hors limites ou obstacle
    if (x < 0 || x >= lignes || y < 0 || y >= colonnes) return null;
    if (grille[x][y] === "#") return null;

    const cle = `${x},${y}`;
    if (visites.has(cle)) return null;

    visites.add(cle);
    chemin.push([x, y]);

    // Arrivée trouvée !
    if (grille[x][y] === "E") {
      return [...chemin];
    }

    // Explorer les 4 directions
    for (const [dx, dy] of directions) {
      const resultat = dfs(x + dx, y + dy, chemin);
      if (resultat) return resultat;
    }

    // Backtracking
    chemin.pop();
    return null;
  }

  return dfs(depart[0], depart[1], []);
}

// Test
const labyrinthe = [
  ["S", ".", "#", ".", "."],
  ["#", ".", "#", ".", "#"],
  [".", ".", ".", ".", "."],
  [".", "#", "#", "#", "."],
  [".", ".", ".", ".", "E"],
];

console.log("Chemin trouvé :", resoudreLabyrinthe(labyrinthe));
// Exemple : [[0,0], [0,1], [1,1], [2,1], [2,2], [2,3], [2,4], [3,4], [4,4]]
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle structure de données est utilisée par le DFS ?**

- [ ] A. Une file (Queue)
- [ ] B. Une pile (Stack)
- [ ] C. Un tableau trié
- [ ] D. Une table de hachage

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le DFS utilise une **pile** (Stack) avec le principe LIFO, soit explicitement, soit implicitement via la récursion (pile d'appels).

</details>

---

### Question 2

**Quel parcours d'arbre binaire visite les nœuds d'un BST dans l'ordre croissant ?**

- [ ] A. Pré-ordre
- [ ] B. In-ordre
- [ ] C. Post-ordre
- [ ] D. BFS

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le parcours **in-ordre** (Gauche → Nœud → Droite) visite les nœuds d'un BST dans l'ordre croissant de leurs valeurs.

</details>

---

### Question 3

**Quelle est la complexité temporelle du DFS ?**

- [ ] A. O(V)
- [ ] B. O(E)
- [ ] C. O(V + E)
- [ ] D. O(V × E)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le DFS visite chaque sommet une fois O(V) et examine chaque arête une fois O(E), donc **O(V + E)**.

</details>

---

### Question 4

**Pourquoi le DFS récursif peut-il causer un "stack overflow" ?**

- [ ] A. Il utilise trop de mémoire pour les résultats
- [ ] B. La pile d'appels a une limite de profondeur
- [ ] C. Il ne marque pas les sommets visités
- [ ] D. Il explore les mêmes sommets plusieurs fois

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La **pile d'appels** de JavaScript a une limite (environ 10 000-20 000 appels). Pour de très grands graphes ou arbres profonds, cette limite peut être atteinte.

</details>

---

### Question 5

**Le DFS garantit-il le chemin le plus court ?**

- [ ] A. Oui, toujours
- [ ] B. Non, jamais
- [ ] C. Seulement dans les graphes non orientés
- [ ] D. Seulement dans les arbres

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le DFS **ne garantit pas** le chemin le plus court. Il trouve UN chemin, pas forcément le plus court. Utilisez BFS pour le chemin le plus court.

</details>

---

### Question 6

**Dans la détection de cycle d'un graphe orienté, quel état indique un cycle ?**

- [ ] A. Trouver un sommet BLANC (non visité)
- [ ] B. Trouver un sommet NOIR (terminé)
- [ ] C. Trouver un sommet GRIS (en cours)
- [ ] D. Ne jamais trouver le sommet cible

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un sommet **GRIS** (en cours de visite) signifie qu'il est encore dans la pile de récursion. Le retrouver indique qu'on est revenu à un ancêtre → CYCLE !

</details>

---

### Question 7

**Quel parcours est le plus adapté pour supprimer un arbre ?**

- [ ] A. Pré-ordre
- [ ] B. In-ordre
- [ ] C. Post-ordre
- [ ] D. BFS

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le parcours **post-ordre** supprime d'abord les enfants, puis le parent. C'est l'ordre correct pour éviter de perdre les références aux enfants.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe du DFS

Explorer **en profondeur** : suivre un chemin jusqu'au bout, puis revenir en arrière (backtracking).

### 2. Structure : Pile (Stack)

Utilise une pile LIFO. Récursion = pile d'appels implicite.

### 3. Trois Parcours d'Arbres

- **Pré-ordre** : Nœud → Gauche → Droite
- **In-ordre** : Gauche → Nœud → Droite (trié pour BST)
- **Post-ordre** : Gauche → Droite → Nœud

### 4. Récursif vs Itératif

Récursif = plus simple. Itératif = évite le stack overflow.

### 5. Détection de Cycles

DFS avec coloration (BLANC/GRIS/NOIR) pour graphes orientés.

### 6. DFS vs BFS

DFS = profondeur, cycles, backtracking. BFS = chemin le plus court.

### 7. Complexité

Temps : O(V + E). Espace : O(V).

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant le parcours en profondeur (DFS) et avez terminé le **Module 5** !

### Ce que vous avez appris aujourd'hui

- Le principe du DFS : exploration **en profondeur** avec backtracking
- Les trois parcours d'arbres : **pré-ordre, in-ordre, post-ordre**
- Les implémentations **récursive** et **itérative**
- La **détection de cycles** dans les graphes
- La comparaison **DFS vs BFS**
- Des applications pratiques : connectivité, labyrinthes, puzzles

### Compétences acquises dans le Module 5

Vous êtes maintenant capable de :

- Comprendre et utiliser les **arbres** (terminologie, types)
- Implémenter et utiliser les **arbres de recherche binaires (BST)**
- Représenter des **graphes** (matrice et liste d'adjacence)
- Parcourir les graphes avec **BFS** et **DFS**
- Choisir le bon algorithme selon le problème

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Le DFS est un algorithme **fondamental** utilisé partout : compilateurs (AST), résolution de puzzles (Sudoku), détection de cycles (dépendances), pathfinding dans les jeux vidéo, et bien plus. Combiné avec le BFS, vous avez maintenant deux outils puissants pour explorer et analyser toutes les structures de données connectées !

---

## ➡️ Prochaine Étape : Module 6

### Ce qui vous attend

Le prochain module, **« Paradigmes Avancés de Conception d'Algorithmes »**, vous introduira aux grandes stratégies de conception d'algorithmes.

**Vous découvrirez :**

- Les **Algorithmes Gloutons** (Greedy) : choix localement optimal
- Le paradigme **Diviser pour Régner** approfondi
- La **Programmation Dynamique** : optimisation par mémorisation
- Des problèmes classiques : sac à dos, plus courts chemins, etc.

### Préparez-vous !

Vous avez maintenant toutes les bases (structures de données, tri, recherche, récursion, arbres, graphes) pour aborder les paradigmes algorithmiques avancés. Le Module 6 vous apprendra à **penser** les algorithmes, pas seulement à les coder !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - DFS/BFS](https://visualgo.net/en/dfsbfs) - Visualisation interactive
- [Wikipedia - Depth-First Search](https://en.wikipedia.org/wiki/Depth-first_search) - Théorie approfondie
- [MIT OpenCourseWare - DFS](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/) - Cours MIT

### Outils de pratique

- **[LeetCode DFS Problems](https://leetcode.com/tag/depth-first-search/)** : Exercices pratiques
- **[HackerRank Graph Theory](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=graph-theory)** : Défis algorithmiques

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ou le Module 5 en général ?

N'hésitez pas à :

- Comparer DFS et BFS sur les mêmes graphes
- Implémenter les deux versions (récursive et itérative) pour chaque
- Résoudre des labyrinthes avec les deux algorithmes

> 💡 **Conseil**
>
> La meilleure façon de maîtriser DFS et BFS est de les utiliser **ensemble** sur les mêmes problèmes. Vous verrez vite leurs forces et faiblesses respectives. Implémentez-les de zéro plusieurs fois jusqu'à ce que ça devienne naturel !

---

**🎉 Félicitations pour avoir terminé le Module 5 !** 🎉

Vous maîtrisez maintenant les arbres et les parcours de graphes. Le Module 6 vous attend pour des paradigmes algorithmiques avancés !

---

<div align="center">

**Leçon 30 sur 42 - Module 5 : Arbres et Parcours de Graphes**

[⬅️ Leçon 29 : Parcours en Largeur (BFS)](./lecon-5-algorithme-parcours-largeur-bfs-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 31 : Algorithmes Gloutons : Stratégie et Résolution de Problèmes Simples ➡️](../module-6/lecon-1-algorithmes-gloutons-strategie-resolution-problemes-simples.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
