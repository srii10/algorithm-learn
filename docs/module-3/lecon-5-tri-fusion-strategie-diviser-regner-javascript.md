##### Leçon 17 sur 42

# Tri Fusion (Merge Sort) : Stratégie Diviser pour Régner en JavaScript

**Module 3** : Techniques de Tri Essentielles

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le paradigme **"Diviser pour Régner"** (Divide and Conquer) et son application au tri
- **Visualiser** le fonctionnement récursif du tri fusion avec les étapes de division et fusion
- **Implémenter** le tri fusion en JavaScript avec les fonctions `mergeSort` et `merge`
- **Analyser** la complexité temporelle O(n log n) et spatiale O(n) de l'algorithme
- **Comparer** le tri fusion avec les algorithmes élémentaires et comprendre ses avantages
- Identifier les **cas d'utilisation** où le tri fusion excelle

---

### ⏱️ Durée estimée : 3h - 3h30

---

## 📚 Prérequis

- **Module 1 complété** : Maîtriser la notation Big O et comprendre O(n log n)
- **Leçons 14-16 complétées** : Connaître les trois algorithmes de tri élémentaires
- **Récursivité** : Comprendre le concept de fonctions qui s'appellent elles-mêmes
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Diviser pour Mieux Régner

Imaginez que vous devez trier une bibliothèque de 1000 livres. Plutôt que d'essayer de tout organiser d'un coup (ce qui serait écrasant), une approche plus intelligente serait de :

1. **Diviser** la bibliothèque en deux sections de 500 livres
2. **Répéter** cette division jusqu'à avoir des piles d'un seul livre (déjà triées !)
3. **Fusionner** les piles en les combinant dans l'ordre

C'est exactement le principe du **tri fusion** (Merge Sort), un algorithme qui incarne parfaitement le paradigme **"Diviser pour Régner"** (Divide and Conquer). Ce paradigme est l'une des techniques les plus puissantes en algorithmique.

Le tri fusion représente un **saut qualitatif** par rapport aux algorithmes élémentaires :

- Complexité **garantie O(n log n)** dans tous les cas (meilleur, moyen, pire)
- Algorithme **stable** : préserve l'ordre des éléments égaux
- **Prévisible** : pas de cas dégénéré comme le Quick Sort
- Idéal pour les **grandes quantités de données**
- Utilisé comme base dans de nombreux algorithmes hybrides (Timsort)

> **Point Clé**
>
> Le tri fusion est le premier algorithme de notre cours avec une complexité **meilleure que O(n²)**. Là où le tri par insertion peut nécessiter 1 million de comparaisons pour 1000 éléments, le tri fusion n'en nécessite que ~10 000 (environ 1000 × log₂(1000) ≈ 1000 × 10).

---

## 📦 Le Paradigme "Diviser pour Régner"

Le paradigme "Diviser pour Régner" est une stratégie fondamentale de résolution de problèmes en informatique. Il se décompose en trois étapes :

---

### Les Trois Étapes

```
┌─────────────────────────────────────────────────────────┐
│                    DIVISER POUR RÉGNER                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1. DIVISER                                             │
│     Décomposer le problème en sous-problèmes            │
│     plus petits du même type                            │
│                                                         │
│  2. RÉGNER (Conquérir)                                  │
│     Résoudre les sous-problèmes récursivement           │
│     Cas de base : si assez petit, résoudre directement  │
│                                                         │
│  3. COMBINER                                            │
│     Fusionner les solutions des sous-problèmes          │
│     pour former la solution du problème original        │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

### Application au Tri

Pour le tri fusion, ces trois étapes se traduisent par :

| Étape        | Action                            | Exemple avec [5, 2, 4, 1] |
| ------------ | --------------------------------- | ------------------------- |
| **Diviser**  | Couper le tableau en deux moitiés | [5, 2] et [4, 1]          |
| **Régner**   | Trier récursivement chaque moitié | [2, 5] et [1, 4]          |
| **Combiner** | Fusionner les moitiés triées      | [1, 2, 4, 5]              |

---

### Analogie : Trier un Jeu de Cartes

Imaginez un jeu de 52 cartes mélangé :

```
1. DIVISER
   ┌──────────────────────────────┐
   │     52 cartes mélangées      │
   └──────────────────────────────┘
                   ↓
    ┌────────────┐  ┌────────────┐
    │ 26 cartes  │  │ 26 cartes  │
    └────────────┘  └────────────┘
           ↓               ↓
     ┌────┐ ┌────┐   ┌────┐ ┌────┐
     │ 13 │ │ 13 │   │ 13 │ │ 13 │
     └────┘ └────┘   └────┘ └────┘
        ↓      ↓        ↓      ↓
  ... (continuer jusqu'à 1 carte chacune) ...

2. RÉGNER
   Une seule carte = déjà triée ! (cas de base)

3. COMBINER
   Fusionner les cartes triées deux par deux,
   puis quatre par quatre, etc.
```

---

## 🔍 Fonctionnement Détaillé du Tri Fusion

Le tri fusion utilise deux fonctions complémentaires :

1. **`mergeSort`** : Divise récursivement le tableau
2. **`merge`** : Fusionne deux tableaux triés en un seul

---

### La Fonction `mergeSort` (Diviser et Régner)

```javascript
function mergeSort(tableau) {
  // CAS DE BASE : Un tableau de 0 ou 1 élément est déjà trié
  if (tableau.length <= 1) {
    return tableau;
  }

  // DIVISER : Trouver le milieu et séparer en deux moitiés
  const milieu = Math.floor(tableau.length / 2);
  const moitieGauche = tableau.slice(0, milieu);
  const moitieDroite = tableau.slice(milieu);

  // RÉGNER : Trier récursivement chaque moitié
  const gaucheTriee = mergeSort(moitieGauche);
  const droiteTriee = mergeSort(moitieDroite);

  // COMBINER : Fusionner les deux moitiés triées
  return merge(gaucheTriee, droiteTriee);
}
```

---

### La Fonction `merge` (Combiner)

La fonction `merge` est le cœur du tri fusion. Elle prend deux tableaux **déjà triés** et les combine en un seul tableau trié.

```javascript
function merge(gauche, droite) {
  const resultat = [];
  let i = 0; // Pointeur pour le tableau gauche
  let j = 0; // Pointeur pour le tableau droite

  // Comparer et fusionner tant que les deux tableaux ont des éléments
  while (i < gauche.length && j < droite.length) {
    if (gauche[i] <= droite[j]) {
      resultat.push(gauche[i]);
      i++;
    } else {
      resultat.push(droite[j]);
      j++;
    }
  }

  // Ajouter les éléments restants (un seul des deux aura des restes)
  while (i < gauche.length) {
    resultat.push(gauche[i]);
    i++;
  }
  while (j < droite.length) {
    resultat.push(droite[j]);
    j++;
  }

  return resultat;
}
```

---

### Visualisation Complète

Traçons l'exécution de `mergeSort([5, 2, 8, 1])` :

```
                 mergeSort([5, 2, 8, 1])
                            │
              ┌─────────────┴─────────────┐
              │                           │
      mergeSort([5, 2])           mergeSort([8, 1])
              │                           │
        ┌─────┴─────┐               ┌─────┴─────┐
        │           │               │           │
  mergeSort([5]) mergeSort([2]) mergeSort([8]) mergeSort([1])
        │           │               │           │
       [5]         [2]             [8]         [1]
        │           │               │           │
        └─────┬─────┘               └─────┬─────┘
              │                           │
     merge([5], [2])            merge([8], [1])
              │                           │
           [2, 5]                      [1, 8]
              │                           │
              └─────────────┬─────────────┘
                            │
                  merge([2, 5], [1, 8])
                            │
                      [1, 2, 5, 8]
```

---

### Détail de la Fusion `merge([2, 5], [1, 8])`

| Étape | gauche[i] | droite[j] | Comparaison   | Action         | resultat     |
| ----- | --------- | --------- | ------------- | -------------- | ------------ |
| 1     | 2         | 1         | 2 > 1         | Ajouter 1, j++ | [1]          |
| 2     | 2         | 8         | 2 < 8         | Ajouter 2, i++ | [1, 2]       |
| 3     | 5         | 8         | 5 < 8         | Ajouter 5, i++ | [1, 2, 5]    |
| 4     | -         | 8         | gauche épuisé | Ajouter reste  | [1, 2, 5, 8] |

**Résultat final : `[1, 2, 5, 8]`**

---

## 📝 Micro-Exercice #1 : Tracer la Fonction merge

**Objectif :** Comprendre le mécanisme de fusion.

**Instructions :** Tracez manuellement l'exécution de `merge([1, 5, 10], [2, 7, 8])`. Notez les valeurs de `i`, `j` et `resultat` à chaque étape.

```javascript
// gauche = [1, 5, 10]
// droite = [2, 7, 8]
```

<details>
<summary>💡 Voir la solution</summary>

| Étape | i   | j   | gauche[i] | droite[j] | Comparaison   | Action         | resultat            |
| ----- | --- | --- | --------- | --------- | ------------- | -------------- | ------------------- |
| Init  | 0   | 0   | 1         | 2         | -             | -              | []                  |
| 1     | 0   | 0   | 1         | 2         | 1 < 2         | Ajouter 1, i++ | [1]                 |
| 2     | 1   | 0   | 5         | 2         | 5 > 2         | Ajouter 2, j++ | [1, 2]              |
| 3     | 1   | 1   | 5         | 7         | 5 < 7         | Ajouter 5, i++ | [1, 2, 5]           |
| 4     | 2   | 1   | 10        | 7         | 10 > 7        | Ajouter 7, j++ | [1, 2, 5, 7]        |
| 5     | 2   | 2   | 10        | 8         | 10 > 8        | Ajouter 8, j++ | [1, 2, 5, 7, 8]     |
| 6     | 2   | 3   | 10        | -         | droite épuisé | Ajouter reste  | [1, 2, 5, 7, 8, 10] |

**Résultat : `[1, 2, 5, 7, 8, 10]`**

**Explication :**

- La fonction compare les éléments aux positions `i` et `j`
- L'élément le plus petit est ajouté au résultat
- Le pointeur correspondant avance
- Une fois un tableau épuisé, le reste de l'autre est ajouté directement

</details>

---

## 💻 Implémentation Complète en JavaScript

Voici l'implémentation complète et commentée du tri fusion.

---

### Version Standard

```javascript
/**
 * Fusionne deux tableaux triés en un seul tableau trié
 * @param {number[]} gauche - Premier tableau trié
 * @param {number[]} droite - Deuxième tableau trié
 * @returns {number[]} - Nouveau tableau contenant tous les éléments, triés
 */
function merge(gauche, droite) {
  const resultat = [];
  let i = 0;
  let j = 0;

  // Comparer et fusionner
  while (i < gauche.length && j < droite.length) {
    if (gauche[i] <= droite[j]) {
      resultat.push(gauche[i]);
      i++;
    } else {
      resultat.push(droite[j]);
      j++;
    }
  }

  // Ajouter les éléments restants
  while (i < gauche.length) {
    resultat.push(gauche[i]);
    i++;
  }
  while (j < droite.length) {
    resultat.push(droite[j]);
    j++;
  }

  return resultat;
}

/**
 * Tri fusion - Implémentation récursive
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Nouveau tableau trié
 */
function triFusion(tableau) {
  // Cas de base : tableau de 0 ou 1 élément
  if (tableau.length <= 1) {
    return tableau;
  }

  // Diviser
  const milieu = Math.floor(tableau.length / 2);
  const moitieGauche = tableau.slice(0, milieu);
  const moitieDroite = tableau.slice(milieu);

  // Régner et Combiner
  const gaucheTriee = triFusion(moitieGauche);
  const droiteTriee = triFusion(moitieDroite);

  return merge(gaucheTriee, droiteTriee);
}

// Tests
const tableau1 = [10, 24, 76, 73, 72, 1, 9];
console.log("Original:", tableau1);
console.log("Trié:", triFusion(tableau1));
// Trié: [1, 9, 10, 24, 72, 73, 76]

const tableau2 = [5, 2, 8, 1, 9, 4, 6, 3, 7, 0];
console.log("Original:", tableau2);
console.log("Trié:", triFusion(tableau2));
// Trié: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

### Version avec Visualisation

```javascript
/**
 * Tri fusion avec affichage des étapes
 * @param {number[]} tableau - Le tableau à trier
 * @param {number} profondeur - Niveau de récursion (pour l'indentation)
 * @returns {number[]} - Tableau trié
 */
function triFusionVisuel(tableau, profondeur = 0) {
  const indent = "  ".repeat(profondeur);

  console.log(`${indent}triFusion([${tableau.join(", ")}])`);

  // Cas de base
  if (tableau.length <= 1) {
    console.log(`${indent}  → Cas de base, retourne [${tableau.join(", ")}]`);
    return tableau;
  }

  // Diviser
  const milieu = Math.floor(tableau.length / 2);
  const moitieGauche = tableau.slice(0, milieu);
  const moitieDroite = tableau.slice(milieu);

  console.log(`${indent}  Diviser: [${moitieGauche}] | [${moitieDroite}]`);

  // Régner
  const gaucheTriee = triFusionVisuel(moitieGauche, profondeur + 1);
  const droiteTriee = triFusionVisuel(moitieDroite, profondeur + 1);

  // Combiner
  const resultat = merge(gaucheTriee, droiteTriee);
  console.log(
    `${indent}  Fusionner [${gaucheTriee}] + [${droiteTriee}] = [${resultat}]`,
  );

  return resultat;
}

// Test
console.log("=== Exécution du Tri Fusion ===\n");
const resultat = triFusionVisuel([5, 2, 8, 1]);
console.log("\nRésultat final:", resultat);
```

**Sortie :**

```
=== Exécution du Tri Fusion ===

triFusion([5, 2, 8, 1])
  Diviser: [5,2] | [8,1]
  triFusion([5, 2])
    Diviser: [5] | [2]
    triFusion([5])
      → Cas de base, retourne [5]
    triFusion([2])
      → Cas de base, retourne [2]
    Fusionner [5] + [2] = [2,5]
  triFusion([8, 1])
    Diviser: [8] | [1]
    triFusion([8])
      → Cas de base, retourne [8]
    triFusion([1])
      → Cas de base, retourne [1]
    Fusionner [8] + [1] = [1,8]
  Fusionner [2,5] + [1,8] = [1,2,5,8]

Résultat final: [1, 2, 5, 8]
```

---

## 📝 Micro-Exercice #2 : Tracer l'Exécution Complète

**Objectif :** Comprendre la récursivité du tri fusion.

**Instructions :** Tracez l'exécution de `triFusion([7, 3, 9, 1, 5])`. Dessinez l'arbre des appels récursifs et notez les résultats de chaque fusion.

<details>
<summary>💡 Voir la solution</summary>

```
                        triFusion([7, 3, 9, 1, 5])
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
           triFusion([7, 3])               triFusion([9, 1, 5])
                    │                               │
              ┌─────┴─────┐                   ┌─────┴─────┐
              │           │                   │           │
        triFusion([7]) triFusion([3])   triFusion([9]) triFusion([1, 5])
              │           │                   │           │
            [7]         [3]                 [9]     ┌─────┴─────┐
              │           │                   │     │           │
              └─────┬─────┘                   │  triFusion([1]) triFusion([5])
                    │                         │     │           │
              merge([7],[3])                  │   [1]         [5]
                    │                         │     │           │
                 [3, 7]                       │     └─────┬─────┘
                    │                         │           │
                    │                         │     merge([1],[5])
                    │                         │           │
                    │                         │        [1, 5]
                    │                         │           │
                    │                         └─────┬─────┘
                    │                               │
                    │                       merge([9],[1,5])
                    │                               │
                    │                          [1, 5, 9]
                    │                               │
                    └───────────────┬───────────────┘
                                    │
                          merge([3,7],[1,5,9])
                                    │
                              [1, 3, 5, 7, 9]
```

**Ordre des fusions :**

1. `merge([7], [3])` → `[3, 7]`
2. `merge([1], [5])` → `[1, 5]`
3. `merge([9], [1, 5])` → `[1, 5, 9]`
4. `merge([3, 7], [1, 5, 9])` → `[1, 3, 5, 7, 9]`

**Résultat final : `[1, 3, 5, 7, 9]`**

</details>

---

## 📊 Analyse de Complexité

Le tri fusion a une complexité remarquablement stable et prévisible.

---

### Complexité Temporelle

| Cas              | Complexité | Description |
| ---------------- | ---------- | ----------- |
| **Meilleur cas** | O(n log n) | Toujours    |
| **Cas moyen**    | O(n log n) | Toujours    |
| **Pire cas**     | O(n log n) | Toujours    |

**Pourquoi O(n log n) ?**

```
Niveau de récursion    Nombre de tableaux    Travail par niveau
──────────────────────────────────────────────────────────────
        0                    1                    n (fusion)
        1                    2                    n (fusions)
        2                    4                    n (fusions)
        3                    8                    n (fusions)
       ...                  ...                  ...
      log₂(n)                n                    n (fusions)

Total = O(n) × O(log n) = O(n log n)
```

- **log n niveaux** : À chaque niveau, on divise par 2, donc log₂(n) niveaux
- **n opérations par niveau** : Chaque niveau fusionne tous les éléments une fois

---

### Comparaison avec les Algorithmes Élémentaires

| Taille (n) | O(n²) opérations | O(n log n) opérations | Gain   |
| ---------- | ---------------- | --------------------- | ------ |
| 100        | 10 000           | ~664                  | 15×    |
| 1 000      | 1 000 000        | ~9 966                | 100×   |
| 10 000     | 100 000 000      | ~132 877              | 753×   |
| 100 000    | 10 000 000 000   | ~1 660 964            | 6 020× |

> **Point Clé**
>
> Pour 100 000 éléments, le tri par insertion nécessiterait environ **10 milliards** de comparaisons dans le pire cas, tandis que le tri fusion n'en nécessite que ~1.6 million. C'est la différence entre quelques secondes et plusieurs heures !

---

### Complexité Spatiale

| Aspect            | Complexité |
| ----------------- | ---------- |
| Espace auxiliaire | O(n)       |

**Attention :** Le tri fusion n'est **pas en place**. Il nécessite de la mémoire supplémentaire proportionnelle à la taille du tableau pour stocker les sous-tableaux lors des fusions.

---

### Stabilité

Le tri fusion est **stable** : deux éléments égaux conservent leur ordre relatif original.

```javascript
// La condition gauche[i] <= droite[j] (avec <=) garantit la stabilité
// L'élément de gauche est choisi en cas d'égalité,
// préservant l'ordre original
```

---

## 📝 Micro-Exercice #3 : Implémenter le Tri Descendant

**Objectif :** Adapter l'algorithme pour trier en ordre décroissant.

**Instructions :** Modifiez les fonctions `merge` et `triFusion` pour trier du plus grand au plus petit.

```javascript
function mergeDescendant(gauche, droite) {
  // Votre implémentation ici
}

function triFusionDescendant(tableau) {
  // Votre implémentation ici
}

// Test
console.log(triFusionDescendant([5, 2, 8, 1, 9]));
// [9, 8, 5, 2, 1]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Fusionne deux tableaux triés en ordre décroissant
 * @param {number[]} gauche - Premier tableau trié (décroissant)
 * @param {number[]} droite - Deuxième tableau trié (décroissant)
 * @returns {number[]} - Tableau fusionné en ordre décroissant
 */
function mergeDescendant(gauche, droite) {
  const resultat = [];
  let i = 0;
  let j = 0;

  // Inverser la comparaison : prendre le PLUS GRAND
  while (i < gauche.length && j < droite.length) {
    if (gauche[i] >= droite[j]) {
      resultat.push(gauche[i]);
      i++;
    } else {
      resultat.push(droite[j]);
      j++;
    }
  }

  while (i < gauche.length) {
    resultat.push(gauche[i]);
    i++;
  }
  while (j < droite.length) {
    resultat.push(droite[j]);
    j++;
  }

  return resultat;
}

/**
 * Tri fusion descendant
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Tableau trié en ordre décroissant
 */
function triFusionDescendant(tableau) {
  if (tableau.length <= 1) {
    return tableau;
  }

  const milieu = Math.floor(tableau.length / 2);
  const moitieGauche = tableau.slice(0, milieu);
  const moitieDroite = tableau.slice(milieu);

  const gaucheTriee = triFusionDescendant(moitieGauche);
  const droiteTriee = triFusionDescendant(moitieDroite);

  return mergeDescendant(gaucheTriee, droiteTriee);
}

// Tests
console.log(triFusionDescendant([5, 2, 8, 1, 9]));
// [9, 8, 5, 2, 1]

console.log(triFusionDescendant([10, 24, 76, 73]));
// [76, 73, 24, 10]
```

**Explication :**

La seule modification est dans la fonction `merge` :

- **Ascendant** : `gauche[i] <= droite[j]` → prendre le plus petit
- **Descendant** : `gauche[i] >= droite[j]` → prendre le plus grand

</details>

---

## 🔄 Comparaison avec les Autres Algorithmes

| Critère          | Tri Insertion | Tri Sélection      | Tri Fusion          |
| ---------------- | ------------- | ------------------ | ------------------- |
| **Meilleur cas** | O(n)          | O(n²)              | O(n log n)          |
| **Cas moyen**    | O(n²)         | O(n²)              | O(n log n)          |
| **Pire cas**     | O(n²)         | O(n²)              | O(n log n)          |
| **Espace**       | O(1)          | O(1)               | O(n)                |
| **Stabilité**    | Stable        | Instable           | Stable              |
| **En place**     | Oui           | Oui                | Non                 |
| **Prévisible**   | Variable      | Constant mais lent | Toujours O(n log n) |

**Quand utiliser le tri fusion ?**

- Grandes quantités de données
- Besoin de performances garanties
- Stabilité requise
- Mémoire disponible
- Éviter si la mémoire est très limitée
- Éviter pour les petits tableaux (overhead de récursion)

---

## 💻 Application Pratique : Tri de Données Complexes

Le tri fusion excelle pour trier des données complexes de manière stable.

---

### Exemple 1 : Tri de Transactions par Date

```javascript
/**
 * Fusionne deux tableaux d'objets triés par une propriété
 * @param {Array} gauche - Premier tableau trié
 * @param {Array} droite - Deuxième tableau trié
 * @param {Function} comparateur - Fonction de comparaison
 * @returns {Array} - Tableau fusionné et trié
 */
function mergeObjets(gauche, droite, comparateur) {
  const resultat = [];
  let i = 0;
  let j = 0;

  while (i < gauche.length && j < droite.length) {
    if (comparateur(gauche[i], droite[j]) <= 0) {
      resultat.push(gauche[i]);
      i++;
    } else {
      resultat.push(droite[j]);
      j++;
    }
  }

  return resultat.concat(gauche.slice(i)).concat(droite.slice(j));
}

/**
 * Tri fusion générique pour objets
 * @param {Array} tableau - Le tableau d'objets à trier
 * @param {Function} comparateur - Fonction (a, b) => number
 * @returns {Array} - Tableau trié
 */
function triFusionObjets(tableau, comparateur) {
  if (tableau.length <= 1) {
    return tableau;
  }

  const milieu = Math.floor(tableau.length / 2);
  const gaucheTriee = triFusionObjets(tableau.slice(0, milieu), comparateur);
  const droiteTriee = triFusionObjets(tableau.slice(milieu), comparateur);

  return mergeObjets(gaucheTriee, droiteTriee, comparateur);
}

// Données de test
const transactions = [
  { id: 1, date: new Date("2024-01-15"), montant: 150 },
  { id: 2, date: new Date("2024-01-10"), montant: 200 },
  { id: 3, date: new Date("2024-01-12"), montant: 75 },
  { id: 4, date: new Date("2024-01-10"), montant: 300 },
  { id: 5, date: new Date("2024-01-15"), montant: 50 },
];

// Tri par date (chronologique)
const parDate = triFusionObjets(transactions, (a, b) => a.date - b.date);

console.log("Transactions par date:");
parDate.forEach((t) => {
  console.log(
    `  ${t.date.toISOString().split("T")[0]} - ${t.montant}€ (id:${t.id})`,
  );
});
// 2024-01-10 - 200€ (id:2)
// 2024-01-10 - 300€ (id:4)  ← Même date, ordre préservé (stable !)
// 2024-01-12 - 75€ (id:3)
// 2024-01-15 - 150€ (id:1)
// 2024-01-15 - 50€ (id:5)   ← Même date, ordre préservé (stable !)
```

---

### Exemple 2 : Tri Multi-Critères

Grâce à sa stabilité, le tri fusion permet de trier par plusieurs critères en effectuant des tris successifs :

```javascript
const employes = [
  { nom: "Chermann", dept: "Engineering", salaire: 75000 },
  { nom: "Prudence", dept: "RH", salaire: 65000 },
  { nom: "Germain", dept: "Engineering", salaire: 80000 },
  { nom: "Ingrid", dept: "RH", salaire: 65000 },
  { nom: "Sing", dept: "Engineering", salaire: 75000 },
];

// Tri par salaire (décroissant)
let trieSalaire = triFusionObjets(employes, (a, b) => b.salaire - a.salaire);

// Puis par département (stable : préserve l'ordre des salaires)
let trieFinal = triFusionObjets(trieSalaire, (a, b) =>
  a.dept.localeCompare(b.dept),
);

console.log("\nEmployés par département puis salaire:");
trieFinal.forEach((e) => {
  console.log(`  ${e.dept} - ${e.nom}: ${e.salaire}€`);
});
// Engineering - Germain: 80000€
// Engineering - Chermann: 75000€
// Engineering - Sing: 75000€
// RH - Prudence: 65000€
// RH - Ingrid: 65000€
```

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension du tri fusion, implémentez les problèmes suivants.

---

### Exercice 1 : Cas Limites

**Objectif :** Vérifier la robustesse de l'implémentation.

**Instructions :** Testez et expliquez le comportement de `triFusion` pour les cas suivants :

```javascript
console.log(triFusion([])); // ?
console.log(triFusion([5])); // ?
console.log(triFusion([5, 5, 5])); // ?
console.log(triFusion([1, 2, 3, 4])); // Déjà trié
console.log(triFusion([4, 3, 2, 1])); // Ordre inverse
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
// Tableau vide
console.log(triFusion([]));
// [] - Le cas de base retourne immédiatement le tableau vide

// Tableau d'un élément
console.log(triFusion([5]));
// [5] - Un seul élément est déjà trié (cas de base)

// Éléments identiques
console.log(triFusion([5, 5, 5]));
// [5, 5, 5] - Fonctionne normalement, les comparaisons <=
// gèrent les égalités correctement

// Déjà trié
console.log(triFusion([1, 2, 3, 4]));
// [1, 2, 3, 4] - Même complexité O(n log n), mais les
// comparaisons sont optimales (chaque élément va directement à sa place)

// Ordre inverse
console.log(triFusion([4, 3, 2, 1]));
// [1, 2, 3, 4] - Même complexité O(n log n), pas de cas dégénéré
```

**Explication :**

Le tri fusion traite tous ces cas avec la même complexité O(n log n). C'est sa force : pas de cas dégénéré comme le Quick Sort avec un tableau déjà trié.

</details>

---

### Exercice 2 : Compter les Opérations

**Objectif :** Analyser empiriquement la complexité.

**Instructions :** Modifiez les fonctions pour compter le nombre de comparaisons et de copies (écritures dans le tableau résultat).

```javascript
function triFusionAvecStats(tableau) {
  // Votre implémentation ici
  // Retourner { resultat, comparaisons, copies }
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri fusion avec comptage des opérations
 */
function triFusionAvecStats(tableau) {
  let comparaisons = 0;
  let copies = 0;

  function merge(gauche, droite) {
    const resultat = [];
    let i = 0;
    let j = 0;

    while (i < gauche.length && j < droite.length) {
      comparaisons++;
      if (gauche[i] <= droite[j]) {
        resultat.push(gauche[i]);
        copies++;
        i++;
      } else {
        resultat.push(droite[j]);
        copies++;
        j++;
      }
    }

    while (i < gauche.length) {
      resultat.push(gauche[i]);
      copies++;
      i++;
    }
    while (j < droite.length) {
      resultat.push(droite[j]);
      copies++;
      j++;
    }

    return resultat;
  }

  function mergeSort(arr) {
    if (arr.length <= 1) {
      return arr;
    }

    const milieu = Math.floor(arr.length / 2);
    const gaucheTriee = mergeSort(arr.slice(0, milieu));
    const droiteTriee = mergeSort(arr.slice(milieu));

    return merge(gaucheTriee, droiteTriee);
  }

  const resultat = mergeSort(tableau);

  return {
    resultat,
    comparaisons,
    copies,
  };
}

// Tests
console.log("n=4:", triFusionAvecStats([5, 2, 8, 1]));
// { resultat: [1, 2, 5, 8], comparaisons: 4, copies: 8 }

console.log("n=8:", triFusionAvecStats([5, 2, 8, 1, 9, 4, 6, 3]));
// { resultat: [...], comparaisons: ~12, copies: 24 }

console.log(
  "n=16:",
  triFusionAvecStats([...Array(16).keys()].sort(() => Math.random() - 0.5)),
);
// comparaisons: ~32-48, copies: 64
```

**Observation :** Le nombre de copies est toujours n × log₂(n) car chaque élément est copié une fois par niveau de récursion.

</details>

---

### Exercice 3 : Fusion de K Tableaux Triés

**Objectif :** Étendre le concept de fusion.

**Instructions :** Implémentez une fonction qui fusionne K tableaux déjà triés en un seul tableau trié.

```javascript
function fusionnerK(tableaux) {
  // Votre implémentation ici
}

// Test
const tableaux = [
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9],
];
console.log(fusionnerK(tableaux));
// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Fusionne deux tableaux triés
 */
function merge(gauche, droite) {
  const resultat = [];
  let i = 0;
  let j = 0;

  while (i < gauche.length && j < droite.length) {
    if (gauche[i] <= droite[j]) {
      resultat.push(gauche[i]);
      i++;
    } else {
      resultat.push(droite[j]);
      j++;
    }
  }

  return resultat.concat(gauche.slice(i)).concat(droite.slice(j));
}

/**
 * Fusionne K tableaux triés en utilisant Divide and Conquer
 * @param {Array[]} tableaux - Liste de tableaux triés
 * @returns {Array} - Tableau fusionné et trié
 */
function fusionnerK(tableaux) {
  // Cas de base
  if (tableaux.length === 0) return [];
  if (tableaux.length === 1) return tableaux[0];

  // Diviser : séparer en deux moitiés
  const milieu = Math.floor(tableaux.length / 2);
  const moitieGauche = tableaux.slice(0, milieu);
  const moitieDroite = tableaux.slice(milieu);

  // Régner : fusionner récursivement chaque moitié
  const gaucheTriee = fusionnerK(moitieGauche);
  const droiteTriee = fusionnerK(moitieDroite);

  // Combiner : fusionner les deux résultats
  return merge(gaucheTriee, droiteTriee);
}

// Tests
const tableaux = [
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9],
];
console.log(fusionnerK(tableaux));
// [1, 2, 3, 4, 5, 6, 7, 8, 9]

const plusDeTableaux = [
  [1, 10, 20],
  [2, 11, 21],
  [3, 12, 22],
  [4, 13, 23],
];
console.log(fusionnerK(plusDeTableaux));
// [1, 2, 3, 4, 10, 11, 12, 13, 20, 21, 22, 23]
```

**Explication :**

Cette solution utilise le même paradigme Divide and Conquer :

- Diviser la liste de tableaux en deux
- Fusionner récursivement chaque moitié
- Combiner les résultats avec `merge`

Complexité : O(N log K) où N est le nombre total d'éléments et K le nombre de tableaux.

</details>

---

### Exercice 4 : Tri Fusion In-Place (Bonus)

**Objectif :** Comprendre le compromis espace/temps.

**Instructions :** Recherchez et expliquez pourquoi le tri fusion standard n'est pas "en place" et quelles modifications seraient nécessaires pour le rendre en place. (Pas besoin d'implémenter)

<details>
<summary>💡 Voir la solution</summary>

**Pourquoi le tri fusion n'est pas en place :**

Le tri fusion crée de nouveaux tableaux à chaque étape :

1. `slice()` crée des copies des moitiés
2. `merge()` crée un nouveau tableau `resultat`
3. Chaque niveau de récursion alloue de la mémoire

**Pour le rendre en place, il faudrait :**

1. **Travailler sur des indices** au lieu de créer des sous-tableaux

   ```javascript
   function mergeSortInPlace(arr, debut, fin) {
     // Trier arr[debut...fin] sans créer de copie
   }
   ```

2. **Fusion en place** : C'est la partie difficile !
   - Rotation de blocs
   - Fusion par blocs (Block Merge Sort)
   - Complexité supplémentaire

3. **Compromis** :
   - Tri fusion en place existe mais est plus complexe
   - La constante cache de O(n log n) augmente
   - Généralement, on préfère accepter O(n) d'espace pour la simplicité

**Alternative pratique :** Utiliser un seul tableau auxiliaire de taille n réutilisé à chaque niveau, au lieu de créer de nouveaux tableaux à chaque appel.

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelles sont les trois étapes du paradigme "Diviser pour Régner" ?**

- [ ] A. Créer, Modifier, Supprimer
- [ ] B. Diviser, Régner (Conquérir), Combiner
- [ ] C. Initialiser, Itérer, Terminer
- [ ] D. Comparer, Échanger, Répéter

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Les trois étapes sont :

1. **Diviser** : Décomposer le problème en sous-problèmes
2. **Régner** : Résoudre les sous-problèmes récursivement
3. **Combiner** : Fusionner les solutions

</details>

---

### Question 2

**Quelle est la complexité temporelle du tri fusion dans le pire cas ?**

- [ ] A. O(n)
- [ ] B. O(n²)
- [ ] C. O(n log n)
- [ ] D. O(log n)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le tri fusion a une complexité de O(n log n) dans **tous** les cas (meilleur, moyen, pire). C'est l'une de ses forces : performances prévisibles et garanties.

</details>

---

### Question 3

**Quelle est la complexité spatiale du tri fusion standard ?**

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le tri fusion nécessite O(n) d'espace supplémentaire pour stocker les sous-tableaux temporaires lors des fusions. Il n'est pas "en place".

</details>

---

### Question 4

**Le tri fusion est-il un algorithme stable ?**

- [ ] A. Non, il peut modifier l'ordre des éléments égaux
- [ ] B. Oui, grâce à la condition `<=` dans la fusion qui favorise le tableau gauche
- [ ] C. Ça dépend de l'implémentation
- [ ] D. La stabilité n'est pas applicable au tri fusion

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri fusion est stable. Lors de la fusion, quand deux éléments sont égaux (`gauche[i] <= droite[j]`), l'élément du tableau gauche est choisi, préservant l'ordre relatif original.

</details>

---

### Question 5

**Quel est le cas de base de la récursion dans le tri fusion ?**

- [ ] A. Le tableau a 0 élément
- [ ] B. Le tableau a 0 ou 1 élément
- [ ] C. Le tableau a 2 éléments
- [ ] D. Le tableau est déjà trié

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le cas de base est quand le tableau a 0 ou 1 élément (`arr.length <= 1`). Un tableau vide ou à un seul élément est déjà trié par définition.

</details>

---

### Question 6

**Combien de niveaux de récursion le tri fusion a-t-il pour un tableau de n éléments ?**

- [ ] A. n
- [ ] B. n/2
- [ ] C. log₂(n)
- [ ] D. n × log(n)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Il y a log₂(n) niveaux de récursion car le tableau est divisé en deux à chaque niveau. Par exemple, pour n=8 : 8→4→2→1, soit 3 niveaux (log₂(8) = 3).

</details>

---

### Question 7

**Quand le tri fusion est-il préférable au tri par insertion ?**

- [ ] A. Pour les très petits tableaux (< 10 éléments)
- [ ] B. Pour les tableaux presque triés
- [ ] C. Pour les grands tableaux où la performance est critique
- [ ] D. Quand la mémoire est très limitée

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le tri fusion excelle pour les grands tableaux grâce à sa complexité O(n log n) garantie. Pour les petits tableaux ou les données presque triées, le tri par insertion peut être plus rapide (moins d'overhead). Quand la mémoire est limitée, le tri fusion n'est pas idéal car il nécessite O(n) d'espace.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Paradigme Diviser pour Régner

Le tri fusion illustre parfaitement le paradigme "Divide and Conquer" : diviser le problème en sous-problèmes, les résoudre récursivement, puis combiner les solutions.

### 2. Deux Fonctions Complémentaires

- **`mergeSort`** : Divise récursivement le tableau jusqu'aux cas de base
- **`merge`** : Fusionne deux tableaux triés en un seul

### 3. Complexité Temporelle Garantie

O(n log n) dans **tous** les cas, sans exception. Pas de cas dégénéré comme le Quick Sort.

### 4. Coût en Mémoire

Le tri fusion nécessite O(n) d'espace supplémentaire. Il n'est pas en place, contrairement aux algorithmes élémentaires.

### 5. Stabilité

Le tri fusion est stable : il préserve l'ordre relatif des éléments égaux, ce qui est crucial pour les tris multi-critères.

### 6. Efficacité sur Grandes Données

Pour n=100 000 éléments : ~1.6 million d'opérations (O(n log n)) vs ~10 milliards (O(n²)) pour les algorithmes élémentaires.

### 7. Cas d'Utilisation

Idéal pour les grandes quantités de données, le tri de fichiers externes, et quand des performances prévisibles sont requises.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maîtrisé le tri fusion, votre premier algorithme de tri avec une complexité sous-quadratique !

### Ce que vous avez appris aujourd'hui

- Le paradigme "Diviser pour Régner" et son application au tri
- Le fonctionnement récursif du tri fusion avec ses deux fonctions clés
- L'implémentation complète en JavaScript
- L'analyse de complexité O(n log n) et le compromis espace/temps
- Les avantages de stabilité et de prévisibilité

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter le tri fusion pour différents types de données
- Comprendre et appliquer le paradigme Divide and Conquer
- Choisir entre tri fusion et algorithmes élémentaires selon le contexte

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Le tri fusion est un algorithme fondamental utilisé dans de nombreux contextes réels : tri de fichiers, bases de données, et comme composant de Timsort (l'algorithme de tri par défaut de Python et Java). Comprendre son fonctionnement vous prépare à aborder d'autres algorithmes Divide and Conquer.

---

## ➡️ Prochaine Étape : Leçon 18

### Ce qui vous attend

La prochaine leçon, **« Tri Rapide (Quick Sort) : Sélection du Pivot et Partitionnement »**, vous présentera un autre algorithme "Diviser pour Régner" extrêmement populaire.

**Vous découvrirez :**

- Le concept du **pivot** et son rôle crucial dans le tri rapide
- Les différentes **stratégies de sélection du pivot** (premier, dernier, médiane de trois, aléatoire)
- Le **schéma de partitionnement de Lomuto** et son implémentation
- Pourquoi le choix du pivot impacte les performances (O(n log n) vs O(n²))

### Préparez-vous !

Le tri rapide (Quick Sort) est l'un des algorithmes de tri les plus utilisés en pratique. Contrairement au tri fusion qui divise toujours au milieu, le tri rapide divise intelligemment autour d'un pivot. Comprendre la sélection du pivot et le partitionnement est essentiel avant d'implémenter l'algorithme complet !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Merge Sort](https://visualgo.net/en/sorting) - Visualisation interactive
- [GeeksforGeeks - Merge Sort](https://www.geeksforgeeks.org/merge-sort/) - Tutoriel détaillé
- [Sorting Algorithms Visualized](https://www.toptal.com/developers/sorting-algorithms/merge-sort) - Comparaison visuelle

### Outils de pratique

- **[JS Bin](https://jsbin.com/)** : Testez vos implémentations en ligne
- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez la récursion pas à pas

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour bien comprendre la récursion du tri fusion, dessinez l'arbre des appels pour un petit tableau (4-8 éléments). Suivez chaque division et fusion. C'est en visualisant le processus que le concept devient vraiment clair !

---

**Prêt pour la Leçon 18 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir le tri rapide et le partitionnement !

---

<div align="center">

**Leçon 17 sur 42 - Module 3 : Techniques de Tri Essentielles**

[⬅️ Leçon 16 : Tri par Insertion : Concept et Implémentation JavaScript Pratique](./lecon-4-tri-insertion-concept-implementation-javascript-pratique.md) | [Retour au sommaire](./README.md) | [Leçon 18 : Tri Rapide : Sélection du Pivot et Partitionnement en JavaScript ➡️](./lecon-6-tri-rapide-selection-pivot-partitionnement-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
