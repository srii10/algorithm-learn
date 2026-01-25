##### Leçon 22 sur 42

# Implémentation de Fonctions Récursives de Base en JavaScript

**Module 4** : Algorithmes de Recherche et Introduction à la Récursion

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Structurer correctement une fonction récursive avec **cas de base** et **appel récursif**
- Implémenter la fonction **factorielle** de manière récursive
- Implémenter la **suite de Fibonacci** et comprendre ses limites
- Appliquer la récursion à des **opérations sur tableaux** (somme, produit)
- Tracer l'**exécution complète** d'appels récursifs imbriqués
- Identifier les **problèmes de performance** de la récursion naïve

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 21 complétée** : Comprendre les concepts de cas de base et d'appel récursif
- **Module 1 complété** : Maîtriser les fonctions JavaScript et leur fonctionnement
- **Concepts mathématiques** : Factorielle et suite de Fibonacci (rappels inclus)
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : De la Théorie à la Pratique

Dans la leçon précédente, vous avez découvert les fondements de la récursion : le **cas de base** qui arrête la récursion et l'**appel récursif** qui réduit le problème. Maintenant, il est temps de mettre ces concepts en pratique !

Dans cette leçon, nous allons implémenter ensemble plusieurs fonctions récursives classiques :

- **La factorielle** : Le classique absolu pour apprendre la récursion
- **La suite de Fibonacci** : Un exemple de récursion multiple (deux appels)
- **Les opérations sur tableaux** : Somme et produit récursifs

Ces exemples vous permettront de maîtriser les patterns récursifs fondamentaux que vous retrouverez dans des algorithmes plus complexes comme le tri fusion ou le parcours d'arbres.

> **Point Clé**
>
> Chaque fonction récursive suit le même schéma mental : "Qu'est-ce que je peux résoudre directement ?" (cas de base) et "Comment puis-je réduire ce problème ?" (appel récursif). Une fois ce schéma maîtrisé, vous pourrez l'appliquer à n'importe quel problème récursif.

---

## 📦 Structure d'une Fonction Récursive

Avant de plonger dans les exemples, rappelons la structure fondamentale de toute fonction récursive.

---

### Les Deux Composantes Essentielles

```javascript
function fonctionRecursive(parametre) {
  // 1. CAS DE BASE - La condition d'arrêt
  if (conditionSimple) {
    return resultatDirect; // Pas d'appel récursif
  }

  // 2. APPEL RÉCURSIF - Réduction du problème
  // Effectuer un travail + appeler avec un paramètre réduit
  return travailActuel + fonctionRecursive(parametreReduit);
}
```

**Les règles d'or :**

- Le **cas de base** doit être vérifié EN PREMIER
- L'**appel récursif** doit TOUJOURS réduire le problème
- Chaque appel doit se **rapprocher** du cas de base
- Sans cas de base ou avec un mauvais cas de base = **stack overflow**

---

## 💻 Exemple 1 : La Fonction Factorielle

La **factorielle** d'un entier n (notée n!) est le produit de tous les entiers de 1 à n.

```
5! = 5 × 4 × 3 × 2 × 1 = 120
4! = 4 × 3 × 2 × 1 = 24
3! = 3 × 2 × 1 = 6
2! = 2 × 1 = 2
1! = 1
0! = 1 (par définition mathématique)
```

---

### Analyse du Problème

| Composante             | Définition                       |
| ---------------------- | -------------------------------- |
| **Cas de base**        | n === 0 ou n === 1 → retourner 1 |
| **Relation récursive** | n! = n × (n-1)!                  |
| **Réduction**          | Chaque appel utilise n-1         |

---

### Implémentation

```javascript
/**
 * Calcule la factorielle d'un nombre n de manière récursive.
 * @param {number} n - Un entier non négatif.
 * @returns {number} - La factorielle de n (n!).
 * @throws {Error} - Si n est négatif.
 */
function factorielle(n) {
  // Validation de l'entrée
  if (n < 0) {
    throw new Error(
      "La factorielle n'est pas définie pour les nombres négatifs.",
    );
  }

  // Cas de base : 0! = 1 et 1! = 1
  // C'est la condition qui arrête la récursion
  if (n === 0 || n === 1) {
    return 1;
  }

  // Appel récursif : n! = n × (n-1)!
  // On réduit le problème en appelant avec n-1
  return n * factorielle(n - 1);
}

// Tests
console.log("Factorielle de 5 :", factorielle(5)); // 120
console.log("Factorielle de 4 :", factorielle(4)); // 24
console.log("Factorielle de 1 :", factorielle(1)); // 1
console.log("Factorielle de 0 :", factorielle(0)); // 1
```

---

### Traçage Complet de factorielle(5)

```
factorielle(5)
│ n = 5, n > 1, donc return 5 * factorielle(4)
│
├── factorielle(4)
│   │ n = 4, n > 1, donc return 4 * factorielle(3)
│   │
│   ├── factorielle(3)
│   │   │ n = 3, n > 1, donc return 3 * factorielle(2)
│   │   │
│   │   ├── factorielle(2)
│   │   │   │ n = 2, n > 1, donc return 2 * factorielle(1)
│   │   │   │
│   │   │   ├── factorielle(1)
│   │   │   │   │ n = 1, CAS DE BASE → return 1
│   │   │   │
│   │   │   └── return 2 * 1 = 2
│   │   │
│   │   └── return 3 * 2 = 6
│   │
│   └── return 4 * 6 = 24
│
└── return 5 * 24 = 120

Résultat final : 120
```

---

## 📝 Micro-Exercice #1 : Tracer la Factorielle

**Objectif :** Vérifier votre compréhension du déroulement récursif.

**Instructions :** Tracez manuellement l'exécution de `factorielle(4)`. Listez chaque appel et son résultat.

<details>
<summary>💡 Voir la solution</summary>

```
Appels (descente) :
1. factorielle(4) → 4 * factorielle(3)
2. factorielle(3) → 3 * factorielle(2)
3. factorielle(2) → 2 * factorielle(1)
4. factorielle(1) → CAS DE BASE → 1

Retours (remontée) :
4. factorielle(1) = 1
3. factorielle(2) = 2 * 1 = 2
2. factorielle(3) = 3 * 2 = 6
1. factorielle(4) = 4 * 6 = 24

Résultat : 24
```

**Explication :** L'exécution "descend" jusqu'au cas de base (n=1), puis "remonte" en calculant les résultats à chaque niveau.

</details>

---

## 💻 Exemple 2 : La Suite de Fibonacci

La **suite de Fibonacci** est une séquence où chaque nombre est la somme des deux précédents :

```
Position : 0, 1, 2, 3, 4, 5,  6,  7,  8,  9, 10, ...
Valeur   : 0, 1, 1, 2, 3, 5,  8, 13, 21, 34, 55, ...
```

Par exemple : `fibonacci(6) = 8` car c'est le 7ème terme (index 6).

---

### Analyse du Problème

| Composante             | Définition                               |
| ---------------------- | ---------------------------------------- |
| **Cas de base 1**      | n === 0 → retourner 0                    |
| **Cas de base 2**      | n === 1 → retourner 1                    |
| **Relation récursive** | fib(n) = fib(n-1) + fib(n-2)             |
| **Particularité**      | **Deux appels récursifs** par invocation |

---

### Implémentation

```javascript
/**
 * Calcule le n-ième terme de la suite de Fibonacci (index 0).
 * @param {number} n - L'index du terme (0, 1, 2, ...).
 * @returns {number} - Le n-ième nombre de Fibonacci.
 */
function fibonacci(n) {
  // Validation de l'entrée
  if (n < 0) {
    throw new Error(
      "La suite de Fibonacci n'est pas définie pour les indices négatifs.",
    );
  }

  // Cas de base 1 : Le premier terme (index 0) est 0
  if (n === 0) {
    return 0;
  }

  // Cas de base 2 : Le deuxième terme (index 1) est 1
  if (n === 1) {
    return 1;
  }

  // Appel récursif : fib(n) = fib(n-1) + fib(n-2)
  // ATTENTION : Deux appels récursifs !
  return fibonacci(n - 1) + fibonacci(n - 2);
}

// Tests
console.log("Fibonacci(0) :", fibonacci(0)); // 0
console.log("Fibonacci(1) :", fibonacci(1)); // 1
console.log("Fibonacci(2) :", fibonacci(2)); // 1
console.log("Fibonacci(6) :", fibonacci(6)); // 8
console.log("Fibonacci(10) :", fibonacci(10)); // 55
```

---

### Traçage de fibonacci(4)

La suite de Fibonacci génère un **arbre d'appels** car chaque appel en génère deux :

```
fibonacci(4)
├── fibonacci(3)
│   ├── fibonacci(2)
│   │   ├── fibonacci(1) → 1 (base)
│   │   └── fibonacci(0) → 0 (base)
│   │   └── return 1 + 0 = 1
│   └── fibonacci(1) → 1 (base)
│   └── return 1 + 1 = 2
└── fibonacci(2)
    ├── fibonacci(1) → 1 (base)
    └── fibonacci(0) → 0 (base)
    └── return 1 + 0 = 1
└── return 2 + 1 = 3

Résultat : 3
```

---

### Problème de Performance

Remarquez-vous quelque chose ? **fibonacci(2) est calculé deux fois !**

Pour `fibonacci(6)`, l'arbre d'appels devient énorme avec de nombreux calculs redondants :

| n   | Nombre d'appels |
| --- | --------------- |
| 5   | 15              |
| 10  | 177             |
| 20  | 21 891          |
| 30  | 2 692 537       |
| 40  | 331 160 281     |

> **Attention**
>
> Cette implémentation récursive naïve a une complexité **O(2^n)** qui est extrêmement inefficace ! Pour les grandes valeurs de n, utilisez la programmation dynamique (mémoïsation) que nous verrons dans un module ultérieur.

---

## 📝 Micro-Exercice #2 : Compter les Appels

**Objectif :** Comprendre l'explosion du nombre d'appels dans Fibonacci récursif.

**Instructions :** Combien de fois `fibonacci(1)` est-il appelé lors de l'exécution de `fibonacci(5)` ?

<details>
<summary>💡 Voir la solution</summary>

**Arbre d'appels de fibonacci(5) :**

```
fibonacci(5)
├── fibonacci(4)
│   ├── fibonacci(3)
│   │   ├── fibonacci(2)
│   │   │   ├── fibonacci(1) ← appel #1
│   │   │   └── fibonacci(0)
│   │   └── fibonacci(1) ← appel #2
│   └── fibonacci(2)
│       ├── fibonacci(1) ← appel #3
│       └── fibonacci(0)
└── fibonacci(3)
    ├── fibonacci(2)
    │   ├── fibonacci(1) ← appel #4
    │   └── fibonacci(0)
    └── fibonacci(1) ← appel #5
```

**Réponse : 5 fois !**

C'est cette redondance qui rend l'algorithme inefficace. Avec la mémoïsation, chaque valeur ne serait calculée qu'une seule fois.

</details>

---

## 💻 Exemple 3 : Somme des Éléments d'un Tableau

Calculons la somme de tous les éléments d'un tableau de manière récursive.

---

### Analyse du Problème

| Composante             | Définition                                     |
| ---------------------- | ---------------------------------------------- |
| **Cas de base**        | Tableau vide → retourner 0                     |
| **Relation récursive** | somme([a, b, c, ...]) = a + somme([b, c, ...]) |
| **Réduction**          | À chaque appel, le tableau perd un élément     |

---

### Implémentation

```javascript
/**
 * Calcule la somme des éléments d'un tableau de manière récursive.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - La somme de tous les éléments.
 */
function sommeTableau(tableau) {
  // Cas de base : tableau vide → somme = 0
  if (tableau.length === 0) {
    return 0;
  }

  // Appel récursif :
  // Premier élément + somme du reste
  // slice(1) crée un nouveau tableau sans le premier élément
  return tableau[0] + sommeTableau(tableau.slice(1));
}

// Tests avec des exemples français
const notesChermann = [15, 18, 12, 16, 14]; // Notes de Chermann
console.log("Somme des notes de Chermann :", sommeTableau(notesChermann)); // 75

const prixCourses = [25, 30, 15, 8]; // Prix en euros
console.log("Total des courses :", sommeTableau(prixCourses)); // 78

console.log("Tableau vide :", sommeTableau([])); // 0
console.log("Un seul élément :", sommeTableau([42])); // 42
```

---

### Traçage de sommeTableau([5, 3, 8, 2])

```
sommeTableau([5, 3, 8, 2])
│ tableau = [5, 3, 8, 2], length > 0
│ return 5 + sommeTableau([3, 8, 2])
│
├── sommeTableau([3, 8, 2])
│   │ tableau = [3, 8, 2], length > 0
│   │ return 3 + sommeTableau([8, 2])
│   │
│   ├── sommeTableau([8, 2])
│   │   │ tableau = [8, 2], length > 0
│   │   │ return 8 + sommeTableau([2])
│   │   │
│   │   ├── sommeTableau([2])
│   │   │   │ tableau = [2], length > 0
│   │   │   │ return 2 + sommeTableau([])
│   │   │   │
│   │   │   ├── sommeTableau([])
│   │   │   │   │ CAS DE BASE → return 0
│   │   │   │
│   │   │   └── return 2 + 0 = 2
│   │   │
│   │   └── return 8 + 2 = 10
│   │
│   └── return 3 + 10 = 13
│
└── return 5 + 13 = 18

Résultat : 18
```

---

## 📝 Micro-Exercice #3 : Produit Récursif

**Objectif :** Appliquer le même pattern pour calculer un produit.

**Instructions :** Implémentez `produitTableau(tableau)` qui calcule le produit de tous les éléments.

```javascript
// Exemples attendus :
produitTableau([1, 2, 3, 4]); // 24
produitTableau([5, 2, 10]); // 100
produitTableau([]); // 1 (produit vide = 1)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Calcule le produit des éléments d'un tableau de manière récursive.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - Le produit de tous les éléments.
 */
function produitTableau(tableau) {
  // Cas de base : tableau vide → produit = 1
  // (Le produit vide est 1, tout comme la somme vide est 0)
  if (tableau.length === 0) {
    return 1;
  }

  // Appel récursif : premier élément × produit du reste
  return tableau[0] * produitTableau(tableau.slice(1));
}

// Tests
console.log("Produit de [1, 2, 3, 4] :", produitTableau([1, 2, 3, 4])); // 24
console.log("Produit de [5, 2, 10] :", produitTableau([5, 2, 10])); // 100
console.log("Produit de [] :", produitTableau([])); // 1
console.log("Produit de [7] :", produitTableau([7])); // 7
```

**Explication :**

Le pattern est identique à la somme, mais avec :

- Cas de base : 1 au lieu de 0
- Opération : multiplication au lieu d'addition

</details>

---

## 💻 Application Pratique : Étude de Cas

Appliquons nos connaissances récursives à des problèmes plus concrets.

---

### Exemple 1 : Fonction Puissance

Calculons x^n de manière récursive :

```javascript
/**
 * Calcule base élevé à la puissance exposant de manière récursive.
 * @param {number} base - La base (x).
 * @param {number} exposant - L'exposant (n), doit être >= 0.
 * @returns {number} - Le résultat de x^n.
 */
function puissance(base, exposant) {
  // Validation
  if (exposant < 0) {
    throw new Error("L'exposant doit être un entier non négatif.");
  }

  // Cas de base : x^0 = 1 pour tout x
  if (exposant === 0) {
    return 1;
  }

  // Appel récursif : x^n = x × x^(n-1)
  return base * puissance(base, exposant - 1);
}

// Tests
console.log("2^3 =", puissance(2, 3)); // 8
console.log("5^0 =", puissance(5, 0)); // 1
console.log("3^4 =", puissance(3, 4)); // 81
console.log("10^2 =", puissance(10, 2)); // 100
```

---

### Exemple 2 : Calculer la Moyenne Récursivement

Calculons la moyenne des notes d'Ingrid et ses amis :

```javascript
/**
 * Calcule la moyenne des éléments d'un tableau.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - La moyenne des éléments.
 */
function moyenne(tableau) {
  if (tableau.length === 0) {
    return 0; // Ou throw une erreur selon le contexte
  }

  // Utiliser notre fonction somme récursive
  const total = sommeTableau(tableau);
  return total / tableau.length;
}

// Notes des élèves
const notesIngrid = [16, 18, 14, 17, 15];
const notesPrudence = [12, 14, 13, 15, 16];
const notesGermain = [18, 19, 17, 20, 18];

console.log("Moyenne d'Ingrid :", moyenne(notesIngrid)); // 16
console.log("Moyenne de Prudence :", moyenne(notesPrudence)); // 14
console.log("Moyenne de Germain :", moyenne(notesGermain)); // 18.4
```

---

### Exemple 3 : Trouver le Maximum Récursivement

Trouvons le maximum d'un tableau sans utiliser `Math.max` :

```javascript
/**
 * Trouve le maximum d'un tableau de manière récursive.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - Le maximum du tableau.
 */
function maximum(tableau) {
  // Cas de base : un seul élément = c'est le max
  if (tableau.length === 1) {
    return tableau[0];
  }

  // Cas erreur : tableau vide
  if (tableau.length === 0) {
    throw new Error("Impossible de trouver le maximum d'un tableau vide.");
  }

  // Appel récursif : comparer le premier avec le max du reste
  const maxDuReste = maximum(tableau.slice(1));

  // Retourner le plus grand entre le premier et le max du reste
  if (tableau[0] > maxDuReste) {
    return tableau[0];
  } else {
    return maxDuReste;
  }
}

// Tests avec les scores de Sarr au jeu vidéo
const scoresSarr = [1250, 980, 1420, 1150, 1380];
console.log("Meilleur score de Sarr :", maximum(scoresSarr)); // 1420

const temperatures = [22, 28, 25, 31, 27, 29];
console.log("Température maximale :", maximum(temperatures)); // 31
```

**Analyse de l'exemple :**

- **Cas de base** : Un tableau d'un seul élément - c'est forcément le maximum
- **Appel récursif** : Trouver le maximum du reste, puis comparer avec le premier élément
- **Pattern** : "Diviser pour régner" - traiter un élément, puis déléguer le reste

---

## 💪 Exercices Pratiques

Pour solidifier votre maîtrise des fonctions récursives, implémentez les problèmes suivants.

---

### Exercice 1 : Fonction Puissance

**Objectif :** Implémenter le calcul de puissance récursivement.

**Instructions :** Écrivez `puissance(base, exposant)` qui calcule base^exposant.

```javascript
// Exemples attendus :
puissance(2, 3); // 8
puissance(5, 0); // 1
puissance(3, 4); // 81
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function puissance(base, exposant) {
  // Validation
  if (exposant < 0) {
    throw new Error("L'exposant doit être non négatif.");
  }

  // Cas de base : x^0 = 1
  if (exposant === 0) {
    return 1;
  }

  // Appel récursif : x^n = x × x^(n-1)
  return base * puissance(base, exposant - 1);
}

// Tests
console.log(puissance(2, 3)); // 8
console.log(puissance(5, 0)); // 1
console.log(puissance(3, 4)); // 81
```

</details>

---

### Exercice 2 : Produit de Tableau

**Objectif :** Calculer le produit de tous les éléments d'un tableau.

**Instructions :** Implémentez `produitTableau(tableau)`.

```javascript
// Exemples attendus :
produitTableau([1, 2, 3]); // 6
produitTableau([5, 2, 10]); // 100
produitTableau([]); // 1
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function produitTableau(tableau) {
  // Cas de base : tableau vide → produit = 1
  if (tableau.length === 0) {
    return 1;
  }

  // Appel récursif
  return tableau[0] * produitTableau(tableau.slice(1));
}

// Tests
console.log(produitTableau([1, 2, 3])); // 6
console.log(produitTableau([5, 2, 10])); // 100
console.log(produitTableau([])); // 1
console.log(produitTableau([7])); // 7
```

</details>

---

### Exercice 3 : Compter les Occurrences

**Objectif :** Compter combien de fois une valeur apparaît dans un tableau.

**Instructions :** Implémentez `compterOccurrences(tableau, valeur)`.

```javascript
// Exemples attendus :
compterOccurrences([1, 2, 3, 2, 4, 2], 2); // 3
compterOccurrences(["pomme", "banane", "pomme"], "pomme"); // 2
compterOccurrences([1, 2, 3], 5); // 0
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Compte le nombre d'occurrences d'une valeur dans un tableau.
 * @param {Array<any>} tableau - Le tableau à parcourir.
 * @param {any} valeur - La valeur à compter.
 * @returns {number} - Le nombre d'occurrences.
 */
function compterOccurrences(tableau, valeur) {
  // Cas de base : tableau vide → 0 occurrences
  if (tableau.length === 0) {
    return 0;
  }

  // Vérifier si le premier élément correspond
  const correspondance = tableau[0] === valeur ? 1 : 0;

  // Appel récursif : ajouter les occurrences dans le reste
  return correspondance + compterOccurrences(tableau.slice(1), valeur);
}

// Tests
console.log(compterOccurrences([1, 2, 3, 2, 4, 2], 2)); // 3
console.log(compterOccurrences(["pomme", "banane", "pomme"], "pomme")); // 2
console.log(compterOccurrences([1, 2, 3], 5)); // 0
```

**Explication :**

- On vérifie si le premier élément correspond à la valeur (0 ou 1)
- On ajoute ce résultat aux occurrences dans le reste du tableau
- Le cas de base est un tableau vide (0 occurrences)

</details>

---

### Exercice 4 : Trouver le Minimum

**Objectif :** Trouver le minimum d'un tableau récursivement.

**Instructions :** Implémentez `minimum(tableau)`.

```javascript
// Exemples attendus :
minimum([5, 2, 8, 1, 9]); // 1
minimum([10]); // 10
minimum([3, 3, 3]); // 3
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trouve le minimum d'un tableau de manière récursive.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - Le minimum du tableau.
 */
function minimum(tableau) {
  // Cas erreur : tableau vide
  if (tableau.length === 0) {
    throw new Error("Impossible de trouver le minimum d'un tableau vide.");
  }

  // Cas de base : un seul élément
  if (tableau.length === 1) {
    return tableau[0];
  }

  // Appel récursif : trouver le min du reste
  const minDuReste = minimum(tableau.slice(1));

  // Retourner le plus petit
  return tableau[0] < minDuReste ? tableau[0] : minDuReste;
}

// Tests
console.log(minimum([5, 2, 8, 1, 9])); // 1
console.log(minimum([10])); // 10
console.log(minimum([3, 3, 3])); // 3
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quel est le résultat de `factorielle(4)` ?**

- [ ] A. 4
- [ ] B. 16
- [ ] C. 24
- [ ] D. 120

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

4! = 4 × 3 × 2 × 1 = **24**

</details>

---

### Question 2

**Quel est le cas de base approprié pour la suite de Fibonacci ?**

- [ ] A. n === 0 seulement
- [ ] B. n === 1 seulement
- [ ] C. n === 0 ou n === 1
- [ ] D. n < 5

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La suite de Fibonacci a **deux cas de base** : fibonacci(0) = 0 et fibonacci(1) = 1. Ces deux valeurs sont connues directement et permettent de calculer tous les autres termes.

</details>

---

### Question 3

**Pourquoi l'implémentation récursive naïve de Fibonacci est-elle inefficace ?**

- [ ] A. Elle utilise trop de mémoire
- [ ] B. Elle effectue des calculs redondants
- [ ] C. Elle ne fonctionne pas pour n > 10
- [ ] D. Elle ne retourne pas le bon résultat

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

L'implémentation naïve **recalcule les mêmes valeurs** plusieurs fois. Par exemple, pour fibonacci(5), fibonacci(2) est calculé 3 fois. Cela donne une complexité O(2^n) au lieu de O(n).

</details>

---

### Question 4

**Dans `sommeTableau([5, 3, 8])`, combien d'appels récursifs sont effectués au total ?**

- [ ] A. 2
- [ ] B. 3
- [ ] C. 4
- [ ] D. 5

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

1. sommeTableau([5, 3, 8]) → appelle sommeTableau([3, 8])
2. sommeTableau([3, 8]) → appelle sommeTableau([8])
3. sommeTableau([8]) → appelle sommeTableau([])
4. sommeTableau([]) → cas de base, retourne 0

**4 appels au total** (incluant le premier).

</details>

---

### Question 5

**Quel est le résultat de `fibonacci(6)` ?**

- [ ] A. 5
- [ ] B. 8
- [ ] C. 13
- [ ] D. 21

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La suite : 0, 1, 1, 2, 3, 5, 8, ...

- fibonacci(0) = 0
- fibonacci(1) = 1
- fibonacci(2) = 1
- fibonacci(3) = 2
- fibonacci(4) = 3
- fibonacci(5) = 5
- fibonacci(6) = **8**

</details>

---

### Question 6

**Quel devrait être le cas de base pour `produitTableau([])` ?**

- [ ] A. 0
- [ ] B. 1
- [ ] C. null
- [ ] D. undefined

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le produit d'un ensemble vide est **1** (élément neutre de la multiplication), tout comme la somme d'un ensemble vide est 0 (élément neutre de l'addition).

</details>

---

### Question 7

**Dans l'expression `return n * factorielle(n - 1)`, quelle partie réduit le problème vers le cas de base ?**

- [ ] A. return
- [ ] B. n \*
- [ ] C. factorielle
- [ ] D. n - 1

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

**n - 1** est la réduction qui rapproche chaque appel du cas de base (n === 0 ou n === 1). Sans cette réduction, la fonction s'appellerait indéfiniment avec la même valeur.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Structure Universelle

Toute fonction récursive suit le schéma : cas de base (condition d'arrêt) + appel récursif (réduction du problème).

### 2. Factorielle

n! = n × (n-1)! avec cas de base 0! = 1! = 1. Un seul appel récursif par invocation.

### 3. Fibonacci

fib(n) = fib(n-1) + fib(n-2) avec cas de base fib(0) = 0, fib(1) = 1. Deux appels récursifs créent un arbre d'exécution.

### 4. Opérations sur Tableaux

somme([a, b, c]) = a + somme([b, c]). Le tableau se réduit avec `slice(1)` jusqu'au tableau vide.

### 5. Problème de Performance

La récursion naïve peut avoir une complexité exponentielle (Fibonacci O(2^n)). La mémoïsation résout ce problème.

### 6. Traçage des Appels

Pour comprendre une fonction récursive, tracez la descente vers le cas de base puis la remontée avec les calculs.

### 7. Patterns Réutilisables

Les patterns (somme, produit, max, min) suivent tous la même structure : traiter un élément + récursion sur le reste.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez implémenté vos premières fonctions récursives en JavaScript !

### Ce que vous avez appris aujourd'hui

- La structure universelle des fonctions récursives
- L'implémentation de la factorielle avec un appel récursif
- L'implémentation de Fibonacci avec deux appels récursifs
- Les opérations récursives sur tableaux (somme, produit, max)
- Le traçage complet des appels récursifs
- Les problèmes de performance de la récursion naïve

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter des fonctions récursives classiques en JavaScript
- Tracer l'exécution et comprendre le flux des appels
- Identifier les limites de performance de la récursion naïve

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Les fonctions récursives que vous avez implémentées sont les **briques de base** d'algorithmes plus complexes. La factorielle vous prépare aux permutations, Fibonacci à la programmation dynamique, et les opérations sur tableaux aux tris récursifs (fusion, rapide). Maîtriser ces patterns vous permettra d'aborder n'importe quel algorithme récursif avec confiance.

---

## ➡️ Prochaine Étape : Leçon 23

### Ce qui vous attend

La prochaine leçon, **« Comprendre la Pile d'Appels (Call Stack) en Récursion »**, vous révélera les mécanismes internes de JavaScript lors de l'exécution récursive.

**Vous découvrirez :**

- Comment JavaScript gère la **pile d'appels** (call stack)
- Pourquoi et quand survient l'erreur **stack overflow**
- Comment **visualiser** la pile d'appels avec les outils de débogage
- Les stratégies pour éviter les débordements de pile

### Préparez-vous !

Comprendre la pile d'appels est essentiel pour écrire des fonctions récursives robustes et éviter les erreurs silencieuses qui peuvent faire planter vos programmes.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Recursion](https://visualgo.net/en/recursion) - Visualisation interactive
- [MDN - Fonctions JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Functions) - Documentation officielle
- [FreeCodeCamp - Recursion Course](https://www.freecodecamp.org/news/recursion-in-javascript/) - Tutoriel complet

### Outils de pratique

- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez la pile d'appels
- **[Chrome DevTools](https://developer.chrome.com/docs/devtools/)** : Débogage pas à pas

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour chaque fonction récursive que vous implémentez, **tracez manuellement** l'exécution avec de petites valeurs. Par exemple, tracez factorielle(3) ou fibonacci(4) sur papier. Cette habitude vous aidera à détecter les erreurs dans vos propres implémentations et à vraiment comprendre le flux récursif.

---

**Prêt pour la Leçon 23 ?** 🚀

Rendez-vous dans la prochaine leçon pour explorer les mystères de la pile d'appels !

---

<div align="center">

**Leçon 22 sur 42 - Module 4 : Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Leçon 21 : Introduction à la Récursion : Cas de Base et Appels Récursifs](./lecon-3-introduction-recursion-cas-base-appels-recursifs.md) | [Retour au sommaire](./README.md) | [Leçon 23 : Comprendre la Pile d'Appels (Call Stack) en Récursion ➡️](./lecon-5-comprendre-pile-appels-recursion.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
