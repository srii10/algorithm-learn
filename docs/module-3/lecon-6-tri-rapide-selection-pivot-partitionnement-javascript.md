##### Leçon 18 sur 42

# Tri Rapide (Quick Sort) : Sélection du Pivot et Partitionnement en JavaScript

**Module 3** : Techniques de Tri Essentielles

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **rôle crucial du pivot** dans le tri rapide et son impact sur les performances
- Connaître les différentes **stratégies de sélection du pivot** et leurs avantages/inconvénients
- **Implémenter** le schéma de partitionnement de Lomuto en JavaScript
- **Tracer** manuellement l'exécution du partitionnement étape par étape
- Identifier les **scénarios de pire cas** et comprendre comment les éviter
- Préparer les bases pour l'implémentation complète du tri rapide

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 17 complétée** : Comprendre le paradigme "Diviser pour Régner"
- **Module 1** : Maîtriser la notation Big O et comprendre O(n²) vs O(n log n)
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Un Autre Champion du Divide and Conquer

Si le tri fusion divise toujours le tableau exactement au milieu, le **tri rapide** (Quick Sort) adopte une approche plus astucieuse : il choisit un élément appelé **pivot** et réorganise le tableau de sorte que tous les éléments plus petits soient à gauche du pivot et tous les plus grands à droite.

Le tri rapide est l'un des algorithmes de tri les plus utilisés en pratique :

- **Performances moyennes excellentes** : O(n log n) en moyenne
- **Tri en place** : contrairement au tri fusion, il ne nécessite pas O(n) d'espace supplémentaire
- **Cache-efficient** : accès mémoire séquentiels, favorable pour les processeurs modernes
- **Largement utilisé** : implémentation par défaut dans de nombreux langages (C stdlib `qsort`)

Cependant, le tri rapide a un talon d'Achille : **le choix du pivot**. Un mauvais choix peut dégrader les performances de O(n log n) à O(n²) !

> **Point Clé**
>
> Le tri rapide est comme une balance : le pivot est le point d'équilibre. Si le pivot est bien choisi (proche de la médiane), les deux côtés sont équilibrés et l'algorithme est efficace. Si le pivot est mal choisi (le plus petit ou le plus grand élément), la balance penche d'un côté et les performances se dégradent.

---

## 📦 Le Concept du Pivot

Le **pivot** est l'élément central du tri rapide. C'est l'élément autour duquel le tableau est partitionné.

---

### Rôle du Pivot

Après le partitionnement :

```
┌───────────────────────────────────────────────────┐
│  Éléments < pivot  │  PIVOT  │  Éléments > pivot  │
└───────────────────────────────────────────────────┘
                          ↑
              Position finale définitive
```

**Le pivot est à sa position finale triée** après le partitionnement. Il ne bougera plus jamais !

---

### Impact du Choix du Pivot

Le choix du pivot détermine l'équilibre des partitions :

| Qualité du Pivot         | Résultat                           | Complexité |
| ------------------------ | ---------------------------------- | ---------- |
| **Idéal** (médiane)      | Partitions égales (n/2, n/2)       | O(n log n) |
| **Bon**                  | Partitions raisonnables            | O(n log n) |
| **Mauvais** (min ou max) | Partitions déséquilibrées (0, n-1) | O(n²)      |

**Exemple de partitions déséquilibrées :**

```
Tableau trié : [1, 2, 3, 4, 5]
Pivot = dernier élément = 5

Partition : [1, 2, 3, 4] | 5 | []
            ↑ n-1 éléments     ↑ 0 élément

→ On doit faire n passes au lieu de log(n)
→ Complexité dégradée en O(n²)
```

---

## 🎯 Stratégies de Sélection du Pivot

Il existe plusieurs stratégies pour choisir le pivot. Chacune a ses avantages et inconvénients.

---

### 1. Premier Élément comme Pivot

```javascript
const pivot = tableau[debut];
```

| Aspect           | Évaluation                              |
| ---------------- | --------------------------------------- |
| **Avantage**     | Implémentation très simple              |
| **Inconvénient** | Pire cas sur tableaux triés ou inversés |

**Exemple problématique :**

```javascript
const tableauTrie = [10, 20, 30, 40, 50];
// Pivot = 10 (le plus petit !)
// Partition : [] | 10 | [20, 30, 40, 50]
// → Partition de taille 0 et n-1 → O(n²)
```

---

### 2. Dernier Élément comme Pivot

```javascript
const pivot = tableau[fin];
```

| Aspect           | Évaluation                                    |
| ---------------- | --------------------------------------------- |
| **Avantage**     | Implémentation simple, utilisé dans Lomuto    |
| **Inconvénient** | Même problème avec tableaux triés ou inversés |

**Exemple problématique :**

```javascript
const tableauTrie = [10, 20, 30, 40, 50];
// Pivot = 50 (le plus grand !)
// Partition : [10, 20, 30, 40] | 50 | []
// → Partition de taille n-1 et 0 → O(n²)
```

---

### 3. Médiane de Trois (Median-of-Three)

On choisit trois éléments (premier, milieu, dernier) et on prend leur **médiane**.

```javascript
function medianeDeTrois(tableau, debut, fin) {
  const milieu = Math.floor((debut + fin) / 2);

  const a = tableau[debut];
  const b = tableau[milieu];
  const c = tableau[fin];

  // Trouver la médiane
  if ((a <= b && b <= c) || (c <= b && b <= a)) return milieu;
  if ((b <= a && a <= c) || (c <= a && a <= b)) return debut;
  return fin;
}
```

| Aspect           | Évaluation                                 |
| ---------------- | ------------------------------------------ |
| **Avantage**     | Réduit drastiquement le risque de pire cas |
| **Inconvénient** | Légèrement plus de calculs                 |

**Exemple :**

```javascript
const tableau = [50, 20, 70, 10, 60, 30, 80];
//               ↑           ↑            ↑
//            premier     milieu       dernier
//              50          10           80

// Valeurs : 50, 10, 80
// Médiane de {50, 10, 80} = 50
// → Pivot = 50 (bien meilleur que 10 ou 80 !)
```

---

### 4. Élément Aléatoire comme Pivot

```javascript
function pivotAleatoire(debut, fin) {
  return Math.floor(Math.random() * (fin - debut + 1)) + debut;
}
```

| Aspect           | Évaluation                       |
| ---------------- | -------------------------------- |
| **Avantage**     | Pire cas extrêmement improbable  |
| **Inconvénient** | Génération de nombres aléatoires |

**Pourquoi c'est efficace :**

- La probabilité de toujours choisir le pire pivot est astronomiquement faible
- En moyenne, le pivot sera "raisonnable"
- Utilisé en pratique pour garantir O(n log n) en moyenne

---

### Comparaison des Stratégies

| Stratégie    | Implémentation | Pire Cas       | Recommandation |
| ------------ | -------------- | -------------- | -------------- |
| Premier      | Très simple    | Tableaux triés | À éviter       |
| Dernier      | Très simple    | Tableaux triés | Pédagogique    |
| Médiane de 3 | Moyenne        | Très rare      | Production     |
| Aléatoire    | Moyenne        | Improbable     | Production     |

> **Point Clé**
>
> En production, préférez la **médiane de trois** ou le **pivot aléatoire**. Pour l'apprentissage, le **dernier élément** (schéma de Lomuto) est plus simple à comprendre et à tracer.

---

## 📝 Micro-Exercice #1 : Choisir le Meilleur Pivot

**Objectif :** Comprendre l'impact du choix du pivot.

**Instructions :** Pour chaque tableau, déterminez quel serait le meilleur et le pire choix de pivot parmi {premier, dernier, médiane de trois}.

1. `[1, 2, 3, 4, 5]` (trié)
2. `[5, 4, 3, 2, 1]` (inversé)
3. `[3, 7, 1, 9, 5]` (aléatoire)

<details>
<summary>💡 Voir la solution</summary>

**1. Tableau trié `[1, 2, 3, 4, 5]` :**

- Premier (1) : Pire cas - le plus petit élément
- Dernier (5) : Pire cas - le plus grand élément
- Médiane de trois {1, 3, 5} → 3 : **Meilleur** - partitions équilibrées

**2. Tableau inversé `[5, 4, 3, 2, 1]` :**

- Premier (5) : Pire cas - le plus grand élément
- Dernier (1) : Pire cas - le plus petit élément
- Médiane de trois {5, 3, 1} → 3 : **Meilleur** - partitions équilibrées

**3. Tableau aléatoire `[3, 7, 1, 9, 5]` :**

- Premier (3) : Moyen - partition [1] | 3 | [7, 9, 5]
- Dernier (5) : Bon - partition [3, 1] | 5 | [7, 9]
- Médiane de trois {3, 1, 5} → 3 : Moyen - partition [1] | 3 | [7, 9, 5]

**Conclusion :** La médiane de trois est toujours un choix sûr, surtout pour les tableaux triés ou inversés où les autres stratégies échouent.

</details>

---

## 🔄 Le Partitionnement : Schéma de Lomuto

Le **partitionnement** est l'opération centrale du tri rapide. Le schéma de Lomuto est l'un des plus simples à comprendre.

---

### Principe du Schéma de Lomuto

1. **Choisir le pivot** : Le dernier élément du sous-tableau
2. **Maintenir une frontière** : Index `i` sépare les éléments ≤ pivot des éléments > pivot
3. **Parcourir le tableau** : Pour chaque élément, si ≤ pivot, l'échanger avec la frontière
4. **Placer le pivot** : Échanger le pivot avec l'élément juste après la frontière

```
Avant partitionnement :
[  éléments non triés  | pivot ]

Après partitionnement :
[ ≤ pivot | PIVOT | > pivot ]
```

---

### Visualisation du Processus

Prenons le tableau `[10, 80, 30, 90, 40, 50, 70]` avec pivot = 70 (dernier élément).

```
État initial : [10, 80, 30, 90, 40, 50, 70]
                                        ↑
                                      pivot

Frontière i = -1 (avant le début)

Parcours avec j :
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ 10  │ 80  │ 30  │ 90  │ 40  │ 50  │ 70  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘
   ↑
   j=0

10 ≤ 70 ? OUI → i++, échanger arr[i] avec arr[j]
         i devient 0, échanger arr[0] avec arr[0] (pas de changement)
```

---

### Implémentation JavaScript

```javascript
/**
 * Échange deux éléments dans un tableau
 * @param {number[]} tableau - Le tableau
 * @param {number} i - Index du premier élément
 * @param {number} j - Index du deuxième élément
 */
function echanger(tableau, i, j) {
  const temp = tableau[i];
  tableau[i] = tableau[j];
  tableau[j] = temp;
}

/**
 * Partitionne un sous-tableau autour d'un pivot (schéma de Lomuto)
 * Le dernier élément est choisi comme pivot
 *
 * @param {number[]} tableau - Le tableau à partitionner
 * @param {number} debut - Index de début du sous-tableau
 * @param {number} fin - Index de fin du sous-tableau
 * @returns {number} - L'index du pivot après partitionnement
 */
function partitionLomuto(tableau, debut, fin) {
  // Sélectionner le dernier élément comme pivot
  const pivot = tableau[fin];

  // i sera l'index du dernier élément trouvé ≤ pivot
  let i = debut - 1;

  // Parcourir le sous-tableau de debut à fin-1
  for (let j = debut; j < fin; j++) {
    // Si l'élément courant est ≤ pivot
    if (tableau[j] <= pivot) {
      // Avancer la frontière
      i++;
      // Échanger l'élément avec la frontière
      echanger(tableau, i, j);
    }
  }

  // Placer le pivot à sa position finale (juste après la frontière)
  echanger(tableau, i + 1, fin);

  // Retourner l'index du pivot
  return i + 1;
}
```

---

### Trace Complète : `partitionLomuto([10, 80, 30, 90, 40, 50, 70], 0, 6)`

| Étape | j   | tableau[j] | ≤ pivot (70) ? | Action         | i   | État du tableau                  |
| ----- | --- | ---------- | -------------- | -------------- | --- | -------------------------------- |
| Init  | -   | -          | -              | -              | -1  | [10, 80, 30, 90, 40, 50, 70]     |
| 1     | 0   | 10         | Oui            | i++, swap(0,0) | 0   | [10, 80, 30, 90, 40, 50, 70]     |
| 2     | 1   | 80         | Non            | -              | 0   | [10, 80, 30, 90, 40, 50, 70]     |
| 3     | 2   | 30         | Oui            | i++, swap(1,2) | 1   | [10, 30, 80, 90, 40, 50, 70]     |
| 4     | 3   | 90         | Non            | -              | 1   | [10, 30, 80, 90, 40, 50, 70]     |
| 5     | 4   | 40         | Oui            | i++, swap(2,4) | 2   | [10, 30, 40, 90, 80, 50, 70]     |
| 6     | 5   | 50         | Oui            | i++, swap(3,5) | 3   | [10, 30, 40, 50, 80, 90, 70]     |
| Fin   | -   | -          | -              | swap(4,6)      | -   | [10, 30, 40, 50, **70**, 90, 80] |

**Résultat :**

```
[10, 30, 40, 50, 70, 90, 80]
 └─────────────┘  ↑  └─────┘
    ≤ pivot    pivot  > pivot

Index du pivot retourné : 4
```

---

## 📝 Micro-Exercice #2 : Tracer le Partitionnement

**Objectif :** Maîtriser le schéma de Lomuto.

**Instructions :** Tracez l'exécution de `partitionLomuto([7, 2, 1, 6, 8, 5, 3, 4], 0, 7)`.

- Pivot = 4 (dernier élément)
- Montrez l'état du tableau après chaque itération

<details>
<summary>💡 Voir la solution</summary>

**Tableau initial :** `[7, 2, 1, 6, 8, 5, 3, 4]`
**Pivot = 4**

| Étape | j   | tableau[j] | ≤ 4 ? | Action         | i   | État du tableau              |
| ----- | --- | ---------- | ----- | -------------- | --- | ---------------------------- |
| Init  | -   | -          | -     | -              | -1  | [7, 2, 1, 6, 8, 5, 3, 4]     |
| 1     | 0   | 7          | Non   | -              | -1  | [7, 2, 1, 6, 8, 5, 3, 4]     |
| 2     | 1   | 2          | Oui   | i++, swap(0,1) | 0   | [2, 7, 1, 6, 8, 5, 3, 4]     |
| 3     | 2   | 1          | Oui   | i++, swap(1,2) | 1   | [2, 1, 7, 6, 8, 5, 3, 4]     |
| 4     | 3   | 6          | Non   | -              | 1   | [2, 1, 7, 6, 8, 5, 3, 4]     |
| 5     | 4   | 8          | Non   | -              | 1   | [2, 1, 7, 6, 8, 5, 3, 4]     |
| 6     | 5   | 5          | Non   | -              | 1   | [2, 1, 7, 6, 8, 5, 3, 4]     |
| 7     | 6   | 3          | Oui   | i++, swap(2,6) | 2   | [2, 1, 3, 6, 8, 5, 7, 4]     |
| Fin   | -   | -          | -     | swap(3,7)      | -   | [2, 1, 3, **4**, 8, 5, 7, 6] |

**Résultat final :** `[2, 1, 3, 4, 8, 5, 7, 6]`

```
[2, 1, 3] | 4 | [8, 5, 7, 6]
  ≤ 4     pivot    > 4
```

**Index du pivot retourné : 3**

</details>

---

## 💻 Implémentation Complète avec Visualisation

```javascript
/**
 * Échange deux éléments dans un tableau
 */
function echanger(tableau, i, j) {
  [tableau[i], tableau[j]] = [tableau[j], tableau[i]];
}

/**
 * Partitionnement de Lomuto avec visualisation
 */
function partitionLomutoVisuel(tableau, debut, fin) {
  const pivot = tableau[fin];
  console.log(`\nPartitionnement de [${tableau.slice(debut, fin + 1)}]`);
  console.log(`   Pivot = ${pivot} (index ${fin})`);
  console.log("─".repeat(50));

  let i = debut - 1;

  for (let j = debut; j < fin; j++) {
    const comparaison = tableau[j] <= pivot ? "✅" : "❌";
    console.log(`   j=${j}: ${tableau[j]} <= ${pivot} ? ${comparaison}`);

    if (tableau[j] <= pivot) {
      i++;
      if (i !== j) {
        console.log(
          `         → i=${i}, échanger ${tableau[i]} ↔ ${tableau[j]}`,
        );
        echanger(tableau, i, j);
        console.log(`         → [${tableau.join(", ")}]`);
      } else {
        console.log(`         → i=${i} (pas d'échange nécessaire)`);
      }
    }
  }

  // Placer le pivot
  echanger(tableau, i + 1, fin);
  console.log(`\n   Placement du pivot: échanger position ${i + 1} ↔ ${fin}`);
  console.log(`   Résultat: [${tableau.join(", ")}]`);
  console.log(`   Pivot ${pivot} maintenant à l'index ${i + 1}`);

  return i + 1;
}

// Test
const tableau = [10, 80, 30, 90, 40, 50, 70];
console.log("Tableau original:", tableau);
const indexPivot = partitionLomutoVisuel(tableau, 0, tableau.length - 1);
console.log(`\nIndex du pivot retourné: ${indexPivot}`);
```

**Sortie :**

```
Tableau original: [10, 80, 30, 90, 40, 50, 70]

📊 Partitionnement de [10, 80, 30, 90, 40, 50, 70]
   Pivot = 70 (index 6)
──────────────────────────────────────────────────
   j=0: 10 <= 70 ? ✅
         → i=0 (pas d'échange nécessaire)
   j=1: 80 <= 70 ? ❌
   j=2: 30 <= 70 ? ✅
         → i=1, échanger 80 ↔ 30
         → [10, 30, 80, 90, 40, 50, 70]
   j=3: 90 <= 70 ? ❌
   j=4: 40 <= 70 ? ✅
         → i=2, échanger 80 ↔ 40
         → [10, 30, 40, 90, 80, 50, 70]
   j=5: 50 <= 70 ? ✅
         → i=3, échanger 90 ↔ 50
         → [10, 30, 40, 50, 80, 90, 70]

   Placement du pivot: échanger position 4 ↔ 6
   Résultat: [10, 30, 40, 50, 70, 90, 80]
   Pivot 70 maintenant à l'index 4

Index du pivot retourné: 4
```

---

## 📝 Micro-Exercice #3 : Modifier la Sélection du Pivot

**Objectif :** Adapter le partitionnement pour utiliser le premier élément comme pivot.

**Instructions :** Modifiez la fonction `partitionLomuto` pour utiliser le **premier élément** comme pivot au lieu du dernier.

**Indice :** Une approche simple est d'échanger le premier et le dernier élément au début, puis d'utiliser le schéma Lomuto standard.

```javascript
function partitionLomutoPremierPivot(tableau, debut, fin) {
  // Votre implémentation ici
}

// Test
const tab = [7, 2, 1, 6, 8, 5, 3, 4];
console.log(partitionLomutoPremierPivot(tab, 0, 7));
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Partitionnement de Lomuto avec le premier élément comme pivot
 */
function partitionLomutoPremierPivot(tableau, debut, fin) {
  // Échanger le premier et le dernier élément
  // pour que le pivot soit à la fin (comme Lomuto standard)
  echanger(tableau, debut, fin);

  // Maintenant on peut utiliser le schéma Lomuto standard
  const pivot = tableau[fin];
  let i = debut - 1;

  for (let j = debut; j < fin; j++) {
    if (tableau[j] <= pivot) {
      i++;
      echanger(tableau, i, j);
    }
  }

  echanger(tableau, i + 1, fin);
  return i + 1;
}

// Alternative : adapter directement la logique
function partitionPremierPivotDirect(tableau, debut, fin) {
  const pivot = tableau[debut]; // Premier élément comme pivot
  let i = fin + 1;

  for (let j = fin; j > debut; j--) {
    if (tableau[j] >= pivot) {
      i--;
      echanger(tableau, i, j);
    }
  }

  echanger(tableau, i - 1, debut);
  return i - 1;
}

// Test
const tab = [7, 2, 1, 6, 8, 5, 3, 4];
console.log("Original:", [...tab]);
const pivotIndex = partitionLomutoPremierPivot([...tab], 0, 7);
console.log("Après partition:", tab);
console.log("Index pivot:", pivotIndex);
```

**Explication :**

La solution la plus simple est d'échanger le premier et le dernier élément, puis d'appliquer le schéma Lomuto standard. Ainsi, le pivot (initialement au début) se retrouve à la fin et la logique reste identique.

</details>

---

## ⚠️ Analyse du Pire Cas

Comprendre le pire cas est essentiel pour éviter les mauvaises surprises en production.

---

### Conditions du Pire Cas

Le pire cas survient quand le pivot est toujours le plus petit ou le plus grand élément :

```
Tableau trié : [1, 2, 3, 4, 5]
Pivot (dernier) = 5

Niveau 1 : [1, 2, 3, 4] | 5 | []      → partition de n-1 et 0
Niveau 2 : [1, 2, 3] | 4 | []         → partition de n-2 et 0
Niveau 3 : [1, 2] | 3 | []            → partition de n-3 et 0
Niveau 4 : [1] | 2 | []               → partition de n-4 et 0

Total : n niveaux de récursion au lieu de log(n)
        n comparaisons par niveau
        → O(n²) au lieu de O(n log n)
```

---

### Comment Éviter le Pire Cas

| Stratégie                 | Efficacité    | Implémentation                          |
| ------------------------- | ------------- | --------------------------------------- |
| Mélanger le tableau avant | Efficace      | `shuffle()` au début                    |
| Pivot aléatoire           | Très efficace | `Math.random()`                         |
| Médiane de trois          | Très efficace | Comparer 3 éléments                     |
| Intro Sort                | Garanti       | Basculer vers Heap Sort si trop profond |

---

### Démonstration du Pire Cas

```javascript
/**
 * Compte les comparaisons lors du partitionnement complet
 */
function compterOperationsPartition(tableau) {
  let comparaisons = 0;

  function partition(arr, debut, fin) {
    if (debut >= fin) return;

    const pivot = arr[fin];
    let i = debut - 1;

    for (let j = debut; j < fin; j++) {
      comparaisons++;
      if (arr[j] <= pivot) {
        i++;
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
    }

    [arr[i + 1], arr[fin]] = [arr[fin], arr[i + 1]];
    const pivotIndex = i + 1;

    partition(arr, debut, pivotIndex - 1);
    partition(arr, pivotIndex + 1, fin);
  }

  partition([...tableau], 0, tableau.length - 1);
  return comparaisons;
}

// Tests
console.log("Tableau aléatoire [3, 1, 4, 1, 5, 9, 2, 6]:");
console.log(
  "Comparaisons:",
  compterOperationsPartition([3, 1, 4, 1, 5, 9, 2, 6]),
);

console.log("\nTableau trié [1, 2, 3, 4, 5, 6, 7, 8]:");
console.log(
  "Comparaisons:",
  compterOperationsPartition([1, 2, 3, 4, 5, 6, 7, 8]),
);

console.log("\nTableau inversé [8, 7, 6, 5, 4, 3, 2, 1]:");
console.log(
  "Comparaisons:",
  compterOperationsPartition([8, 7, 6, 5, 4, 3, 2, 1]),
);
```

**Résultat typique :**

```
Tableau aléatoire [3, 1, 4, 1, 5, 9, 2, 6]:
Comparaisons: ~16-20

Tableau trié [1, 2, 3, 4, 5, 6, 7, 8]:
Comparaisons: 28 (pire cas !)

Tableau inversé [8, 7, 6, 5, 4, 3, 2, 1]:
Comparaisons: 28 (pire cas !)
```

---

## 💻 Application Pratique : Partitionnement d'Objets

Le partitionnement peut être adapté pour trier des objets selon un critère.

---

### Exemple : Partitionner des Produits par Prix

```javascript
/**
 * Partitionne un tableau d'objets selon une propriété
 */
function partitionObjets(tableau, debut, fin, propriete) {
  const pivot = tableau[fin][propriete];
  let i = debut - 1;

  for (let j = debut; j < fin; j++) {
    if (tableau[j][propriete] <= pivot) {
      i++;
      [tableau[i], tableau[j]] = [tableau[j], tableau[i]];
    }
  }

  [tableau[i + 1], tableau[fin]] = [tableau[fin], tableau[i + 1]];
  return i + 1;
}

// Test
const produits = [
  { nom: "Laptop", prix: 999 },
  { nom: "Souris", prix: 29 },
  { nom: "Clavier", prix: 79 },
  { nom: "Écran", prix: 299 },
  { nom: "Webcam", prix: 89 },
];

console.log("Avant partition:");
produits.forEach((p) => console.log(`  ${p.nom}: ${p.prix}€`));

const pivotIndex = partitionObjets(produits, 0, 4, "prix");

console.log(`\nAprès partition (pivot index: ${pivotIndex}):`);
produits.forEach((p, i) => {
  const marker = i === pivotIndex ? " ← PIVOT" : "";
  console.log(`  ${p.nom}: ${p.prix}€${marker}`);
});
```

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension du partitionnement, implémentez les problèmes suivants.

---

### Exercice 1 : Tracer un Partitionnement Complet

**Objectif :** Maîtriser la trace manuelle.

**Instructions :** Appliquez `partitionLomuto` sur `[5, 2, 8, 1, 9]` avec le dernier élément (9) comme pivot. Montrez chaque étape.

<details>
<summary>💡 Voir la solution</summary>

**Tableau :** `[5, 2, 8, 1, 9]`
**Pivot = 9**

| Étape | j   | tableau[j] | ≤ 9 ? | Action         | i   | État                |
| ----- | --- | ---------- | ----- | -------------- | --- | ------------------- |
| Init  | -   | -          | -     | -              | -1  | [5, 2, 8, 1, 9]     |
| 1     | 0   | 5          | ✅    | i++, swap(0,0) | 0   | [5, 2, 8, 1, 9]     |
| 2     | 1   | 2          | ✅    | i++, swap(1,1) | 1   | [5, 2, 8, 1, 9]     |
| 3     | 2   | 8          | ✅    | i++, swap(2,2) | 2   | [5, 2, 8, 1, 9]     |
| 4     | 3   | 1          | ✅    | i++, swap(3,3) | 3   | [5, 2, 8, 1, 9]     |
| Fin   | -   | -          | -     | swap(4,4)      | -   | [5, 2, 8, 1, **9**] |

**Résultat :** `[5, 2, 8, 1, 9]` - Le pivot 9 est déjà à sa place (index 4) car tous les éléments sont ≤ 9.

**Note :** C'est un cas où le pivot est le maximum, illustrant pourquoi c'est un mauvais choix.

</details>

---

### Exercice 2 : Implémenter la Médiane de Trois

**Objectif :** Améliorer la sélection du pivot.

**Instructions :** Implémentez une fonction qui retourne l'index de la médiane de trois éléments (premier, milieu, dernier).

```javascript
function medianeDeTrois(tableau, debut, fin) {
  // Votre implémentation ici
}

// Tests
console.log(medianeDeTrois([50, 20, 70, 10, 60, 30, 80], 0, 6)); // Doit retourner l'index de 50
console.log(medianeDeTrois([1, 2, 3, 4, 5], 0, 4)); // Doit retourner l'index de 3
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Retourne l'index de la médiane parmi premier, milieu et dernier élément
 * @param {number[]} tableau - Le tableau
 * @param {number} debut - Index de début
 * @param {number} fin - Index de fin
 * @returns {number} - Index de la médiane
 */
function medianeDeTrois(tableau, debut, fin) {
  const milieu = Math.floor((debut + fin) / 2);

  const a = tableau[debut];
  const b = tableau[milieu];
  const c = tableau[fin];

  // Trouver la médiane
  if ((a <= b && b <= c) || (c <= b && b <= a)) {
    return milieu; // b est la médiane
  }
  if ((b <= a && a <= c) || (c <= a && a <= b)) {
    return debut; // a est la médiane
  }
  return fin; // c est la médiane
}

// Tests
const tab1 = [50, 20, 70, 10, 60, 30, 80];
// Premier=50, Milieu=10, Dernier=80
// Médiane de {50, 10, 80} = 50
console.log("Test 1:", medianeDeTrois(tab1, 0, 6)); // 0 (index de 50)

const tab2 = [1, 2, 3, 4, 5];
// Premier=1, Milieu=3, Dernier=5
// Médiane de {1, 3, 5} = 3
console.log("Test 2:", medianeDeTrois(tab2, 0, 4)); // 2 (index de 3)

const tab3 = [5, 4, 3, 2, 1];
// Premier=5, Milieu=3, Dernier=1
// Médiane de {5, 3, 1} = 3
console.log("Test 3:", medianeDeTrois(tab3, 0, 4)); // 2 (index de 3)
```

</details>

---

### Exercice 3 : Partitionnement avec Médiane de Trois

**Objectif :** Combiner sélection du pivot et partitionnement.

**Instructions :** Créez une fonction qui utilise la médiane de trois comme pivot, puis partitionne le tableau.

```javascript
function partitionMedianeTrois(tableau, debut, fin) {
  // Votre implémentation ici
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Partitionnement avec médiane de trois comme pivot
 */
function partitionMedianeTrois(tableau, debut, fin) {
  // Trouver l'index de la médiane
  const medianeIndex = medianeDeTrois(tableau, debut, fin);

  // Échanger la médiane avec le dernier élément
  // pour pouvoir utiliser le schéma Lomuto standard
  [tableau[medianeIndex], tableau[fin]] = [tableau[fin], tableau[medianeIndex]];

  // Appliquer le partitionnement Lomuto standard
  const pivot = tableau[fin];
  let i = debut - 1;

  for (let j = debut; j < fin; j++) {
    if (tableau[j] <= pivot) {
      i++;
      [tableau[i], tableau[j]] = [tableau[j], tableau[i]];
    }
  }

  [tableau[i + 1], tableau[fin]] = [tableau[fin], tableau[i + 1]];
  return i + 1;
}

// Test avec un tableau trié (cas problématique pour pivot dernier)
const tableauTrie = [1, 2, 3, 4, 5];
console.log("Avant:", [...tableauTrie]);
const pivotIndex = partitionMedianeTrois(tableauTrie, 0, 4);
console.log("Après:", tableauTrie);
console.log("Index pivot:", pivotIndex);
// Avec médiane de trois, le pivot sera 3 (milieu)
// Résultat bien équilibré !
```

</details>

---

### Exercice 4 : Analyser la Complexité Empirique

**Objectif :** Observer la différence entre cas moyen et pire cas.

**Instructions :** Créez une fonction qui compte le nombre de comparaisons pour différentes configurations de tableaux.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Analyse empirique du nombre de comparaisons
 */
function analyserComparaisons(taille) {
  // Générer différents types de tableaux
  const aleatoire = Array.from({ length: taille }, () =>
    Math.floor(Math.random() * 1000),
  );
  const trie = Array.from({ length: taille }, (_, i) => i + 1);
  const inverse = Array.from({ length: taille }, (_, i) => taille - i);

  function compterComparaisons(tableau) {
    let comparaisons = 0;
    const copie = [...tableau];

    function partition(arr, debut, fin) {
      if (debut >= fin) return;

      const pivot = arr[fin];
      let i = debut - 1;

      for (let j = debut; j < fin; j++) {
        comparaisons++;
        if (arr[j] <= pivot) {
          i++;
          [arr[i], arr[j]] = [arr[j], arr[i]];
        }
      }

      [arr[i + 1], arr[fin]] = [arr[fin], arr[i + 1]];
      const pivotIndex = i + 1;

      partition(arr, debut, pivotIndex - 1);
      partition(arr, pivotIndex + 1, fin);
    }

    partition(copie, 0, copie.length - 1);
    return comparaisons;
  }

  const theoriqueMoyen = Math.round(taille * Math.log2(taille));
  const theoriquePire = (taille * (taille - 1)) / 2;

  console.log(`\nAnalyse pour n = ${taille}`);
  console.log("─".repeat(40));
  console.log(`Théorique O(n log n) : ~${theoriqueMoyen}`);
  console.log(`Théorique O(n²)      : ${theoriquePire}`);
  console.log("─".repeat(40));
  console.log(`Tableau aléatoire    : ${compterComparaisons(aleatoire)}`);
  console.log(`Tableau trié         : ${compterComparaisons(trie)}`);
  console.log(`Tableau inversé      : ${compterComparaisons(inverse)}`);
}

analyserComparaisons(10);
analyserComparaisons(20);
analyserComparaisons(50);
```

**Résultat typique :**

```
Analyse pour n = 10
────────────────────────────────────────
Théorique O(n log n) : ~33
Théorique O(n²)      : 45
────────────────────────────────────────
Tableau aléatoire    : 22
Tableau trié         : 45  ← Pire cas !
Tableau inversé      : 45  ← Pire cas !
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quel est le rôle du pivot dans le tri rapide ?**

- [ ] A. C'est l'élément le plus grand du tableau
- [ ] B. C'est l'élément autour duquel le tableau est partitionné
- [ ] C. C'est toujours l'élément du milieu
- [ ] D. C'est l'élément qui sera supprimé

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le pivot est l'élément autour duquel le tableau est réorganisé : tous les éléments plus petits sont placés à sa gauche, tous les plus grands à sa droite. Après le partitionnement, le pivot est à sa position finale définitive.

</details>

---

### Question 2

**Quelle stratégie de sélection du pivot est la plus risquée sur un tableau déjà trié ?**

- [ ] A. Médiane de trois
- [ ] B. Élément aléatoire
- [ ] C. Premier ou dernier élément
- [ ] D. Toutes sont équivalentes

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Sur un tableau déjà trié, choisir le premier ou le dernier élément donne toujours le minimum ou le maximum, créant des partitions complètement déséquilibrées (0 et n-1) et dégradant la complexité en O(n²).

</details>

---

### Question 3

**Dans le schéma de Lomuto, que représente l'index `i` ?**

- [ ] A. L'index du pivot
- [ ] B. La frontière entre les éléments ≤ pivot et les éléments > pivot
- [ ] C. L'élément minimum trouvé
- [ ] D. Le nombre de comparaisons effectuées

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Dans le schéma de Lomuto, `i` maintient la frontière : tous les éléments de l'index 0 à `i` sont ≤ pivot, et tous les éléments de `i+1` jusqu'à la position courante sont > pivot.

</details>

---

### Question 4

**Quelle est la complexité du partitionnement d'un tableau de n éléments ?**

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le partitionnement parcourt tous les éléments une seule fois (de `debut` à `fin-1`), effectuant une comparaison et potentiellement un échange par élément. C'est donc O(n).

</details>

---

### Question 5

**Pourquoi la médiane de trois est-elle préférée au premier/dernier élément ?**

- [ ] A. Elle est plus rapide à calculer
- [ ] B. Elle garantit des partitions parfaitement équilibrées
- [ ] C. Elle réduit significativement le risque de pire cas
- [ ] D. Elle utilise moins de mémoire

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La médiane de trois ne garantit pas des partitions parfaites, mais elle évite de toujours choisir le minimum ou le maximum, réduisant ainsi drastiquement le risque de tomber dans le pire cas O(n²).

</details>

---

### Question 6

**Après le partitionnement, le pivot est-il à sa position finale ?**

- [ ] A. Oui, toujours
- [ ] B. Non, jamais
- [ ] C. Seulement si le tableau était déjà trié
- [ ] D. Seulement si on utilise la médiane de trois

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

Après le partitionnement, le pivot est **toujours** à sa position finale triée. Tous les éléments à sa gauche sont ≤ et tous les éléments à sa droite sont >. Il ne bougera plus lors des appels récursifs suivants.

</details>

---

### Question 7

**Quelle est la différence principale entre le tri fusion et le tri rapide concernant la division ?**

- [ ] A. Le tri fusion divise au milieu, le tri rapide divise autour d'un pivot
- [ ] B. Le tri fusion est récursif, le tri rapide est itératif
- [ ] C. Le tri fusion est stable, le tri rapide ne l'est pas
- [ ] D. A et C sont correctes

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Les deux différences sont :

- Le tri fusion divise toujours exactement au milieu (position), tandis que le tri rapide divise autour d'un pivot (valeur)
- Le tri fusion est stable (préserve l'ordre des égaux), le tri rapide avec Lomuto ne l'est généralement pas

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Rôle du Pivot

Le pivot est l'élément central du tri rapide. Après partitionnement, il est à sa position finale définitive avec les éléments ≤ à gauche et > à droite.

### 2. Stratégies de Sélection

Quatre stratégies principales : premier élément, dernier élément, médiane de trois, et élément aléatoire. Les deux dernières sont recommandées en production.

### 3. Impact du Choix

Un bon pivot (proche de la médiane) donne des partitions équilibrées et O(n log n). Un mauvais pivot (min ou max) donne O(n²).

### 4. Schéma de Lomuto

L'algorithme maintient une frontière `i` et parcourt avec `j`. Les éléments ≤ pivot sont échangés vers la gauche de la frontière.

### 5. Complexité du Partitionnement

Le partitionnement est toujours O(n) car il parcourt chaque élément une seule fois.

### 6. Pire Cas

Le pire cas (O(n²)) survient sur les tableaux triés ou inversés avec pivot premier/dernier. Évitable avec médiane de trois ou pivot aléatoire.

### 7. Position Finale du Pivot

Après chaque partitionnement, le pivot est définitivement à sa place. Les appels récursifs n'affectent que les sous-tableaux à gauche et à droite.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant les concepts fondamentaux du tri rapide : la sélection du pivot et le partitionnement.

### Ce que vous avez appris aujourd'hui

- L'importance cruciale du choix du pivot pour les performances
- Les quatre stratégies de sélection du pivot et leurs compromis
- Le fonctionnement détaillé du schéma de partitionnement de Lomuto
- Comment tracer manuellement un partitionnement
- Les conditions qui mènent au pire cas et comment les éviter

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter le partitionnement de Lomuto
- Choisir une stratégie de pivot adaptée au contexte
- Tracer l'exécution du partitionnement étape par étape

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Le partitionnement est le cœur du tri rapide. Maintenant que vous le maîtrisez, vous êtes prêt à assembler toutes les pièces et implémenter l'algorithme complet de tri rapide. Vous comprendrez aussi mieux d'autres algorithmes qui utilisent le partitionnement, comme la sélection du k-ième élément (QuickSelect).

---

## ➡️ Prochaine Étape : Leçon 19

### Ce qui vous attend

Dans la prochaine leçon, **« Recherche Linéaire : Trouver un Élément Simplement en JavaScript »**, vous allez entamer un nouveau module passionnant sur les algorithmes de recherche et la récursion.

**Vous découvrirez :**

- La **recherche linéaire** : l'algorithme de recherche le plus simple et intuitif
- Quand utiliser la recherche linéaire vs des méthodes plus avancées
- ⏱L'analyse de la complexité O(n) et ses implications
- Les optimisations possibles et les variantes de l'algorithme

### Préparez-vous !

Avec votre maîtrise des algorithmes de tri, vous avez maintenant une base solide pour aborder les algorithmes de recherche. La recherche binaire (que vous verrez ensuite) nécessite des données triées - vous savez maintenant comment y arriver efficacement !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Quick Sort](https://visualgo.net/en/sorting) - Visualisation interactive du partitionnement
- [GeeksforGeeks - Quick Sort](https://www.geeksforgeeks.org/quick-sort/) - Tutoriel détaillé
- [Sorting Algorithms Visualized](https://www.toptal.com/developers/sorting-algorithms/quick-sort) - Comparaison visuelle

### Outils utiles

- **[JS Bin](https://jsbin.com/)** : Testez vos implémentations en ligne
- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez le partitionnement pas à pas

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour bien comprendre le partitionnement, prenez des cartes numérotées et simulez l'algorithme de Lomuto physiquement. Marquez le pivot, maintenez la frontière avec votre doigt, et déplacez les cartes. Cette manipulation concrète ancre les concepts bien mieux que la simple lecture du code !

---

**Prêt pour la Leçon 19 ?** 🚀

Rendez-vous dans la prochaine leçon pour explorer les algorithmes de recherche !

---

<div align="center">

**Leçon 18 sur 42 - Module 3 : Techniques de Tri Essentielles**

[⬅️ Leçon 17 : Tri par Fusion - Stratégie Diviser pour Régner en JavaScript](./lecon-5-tri-fusion-strategie-diviser-regner-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 19 : Recherche Linéaire - Trouver un Élément Simplement en JavaScript ➡️](../module-4/lecon-1-recherche-lineaire-trouver-element-simplement-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
