# 📘 Leçon 5 : Analyse des Opérations JavaScript Simples avec Big O

**Module 1** : Fondements des algorithmes et révision de JavaScript

---

## 🎯 Objectifs d'Apprentissage

À la fin de cette leçon, vous serez capable de :

- Identifier la complexité temporelle des opérations JavaScript de base
- Reconnaître les opérations O(1), O(n), O(n²) et O(log n) dans du code réel
- Analyser les boucles simples et imbriquées
- Comprendre la différence de performance entre les méthodes de tableaux
- Évaluer rapidement la complexité d'un bloc de code JavaScript

---

### ⏱️ Durée Estimée : 2h30 - 3h

---

## 📚 Prérequis

Avant de commencer cette leçon, assurez-vous de maîtriser :

- Les concepts de la notation Big O (Leçon 4)
- La complexité temporelle et spatiale (Leçon 3)
- Les structures de contrôle JavaScript (Leçon 2)
- Les tableaux et objets JavaScript

---

## 🚀 Introduction

Dans la leçon précédente, vous avez découvert la **notation Big O** et comment elle permet de classifier les algorithmes selon leur comportement asymptotique. Maintenant, il est temps de mettre cette théorie en pratique !

### Pourquoi Cette Leçon est Cruciale

Savoir analyser les opérations individuelles est la **première étape** pour évaluer la complexité d'algorithmes plus complexes. C'est comme apprendre les notes de musique avant de jouer une symphonie.

**Dans cette leçon, vous allez apprendre à :**

1. Reconnaître instantanément la complexité des opérations de base
2. Identifier les patterns qui mènent à différentes complexités
3. Anticiper les problèmes de performance avant qu'ils ne surviennent
4. Choisir les bonnes structures de données et méthodes

### Analogie : Le Diagnostic Médical

Un médecin expérimenté peut rapidement identifier les symptômes d'une maladie. De la même façon, un développeur compétent peut **instantanément reconnaître** les patterns de complexité dans le code et prédire les problèmes de performance potentiels.

---

## 📦 1. Opérations en Temps Constant : O(1)

### 1.1 Définition

Les opérations en **temps constant**, notées **O(1)**, prennent toujours le même temps d'exécution, **peu importe la taille de l'entrée**.

> **Point Clé**
>
> O(1) ne signifie pas "instantané" ou "1 opération". Cela signifie que le temps d'exécution **ne dépend pas de n**.

### 1.2 Affectation de Variables

Assigner une valeur à une variable est une opération O(1).

```javascript
let x = 10; // O(1)
const name = "Chermann"; // O(1)
let isActive = true; // O(1)

// Même avec de très grandes valeurs
let bigNumber = 9007199254740991; // O(1)
let longString = "Une chaîne de texte très longue..."; // O(1)
```

**Pourquoi O(1) ?**

Le processeur exécute cette instruction en un nombre fixe de cycles, indépendamment de la valeur assignée.

---

### 1.3 Opérations Arithmétiques

Les opérations arithmétiques de base sont **O(1)**.

```javascript
let sum = 5 + 3; // O(1)
let product = 10 * 2; // O(1)
let difference = 20 - 7; // O(1)
let quotient = 100 / 4; // O(1)
let remainder = 17 % 5; // O(1)

// Expressions plus complexes, mais toujours O(1)
let result = (5 + 3) * 2 - 10 / 2; // O(1)
```

> **Important :**
>
> Les processeurs modernes exécutent ces opérations en temps constant, même avec de grands nombres (dans les limites de JavaScript).

---

### 1.4 Accès aux Éléments de Tableau/Objet

Accéder à un élément d'un tableau par son **index** ou à une propriété d'un objet par sa **clé** est **O(1)**.

```javascript
const arr = [1, 2, 3, 4, 5];
let firstElement = arr[0]; // O(1)
let thirdElement = arr[2]; // O(1)
let lastElement = arr[arr.length - 1]; // O(1)

const user = { name: "Chermann", age: 43, city: "Charleroi" };
let userName = user.name; // O(1)
let userAge = user["age"]; // O(1)
```

**Pourquoi O(1) ?**

- **Tableaux** : L'adresse mémoire de `arr[i]` est calculée directement : `adresse_base + (i × taille_élément)`
- **Objets** : Les moteurs JavaScript utilisent des hash tables pour un accès direct par clé

> **Observation**
>
> Accéder à `arr[0]` prend **exactement le même temps** qu'accéder à `arr[999]` dans un tableau de 1000 éléments.

---

### 1.5 Appels de Fonctions Simples

Appeler une fonction (sans compter la complexité de son contenu) est **O(1)**.

```javascript
function greet() {
  // L'appel lui-même est O(1)
  console.log("Bonjour !"); // O(1)
}

greet(); // O(1)

function add(a, b) {
  return a + b; // O(1)
}

let sum = add(5, 3); // O(1) pour l'appel + O(1) pour l'addition = O(1)
```

**Note importante :**

Si la fonction contient une boucle qui itère `n` fois, alors l'appel de cette fonction sera **O(n)**, pas O(1).

---

## 📝 Micro-Exercice #1 : Identifier les Opérations O(1)

Pour chacune des opérations suivantes, déterminez si elle est **O(1)** :

```javascript
// A
let result = Math.max(10, 20, 30);

// B
const colors = ["rouge", "vert", "bleu"];
let secondColor = colors[1];

// C
const person = { name: "Claire", age: 25 };
person.age = 26;

// D
let value = 2 ** 10; // 2 puissance 10
```

<details>
<summary>💡 Voir la solution</summary>

**A. Math.max(10, 20, 30)** : **O(1)**

- Avec un nombre fixe d'arguments (3), c'est une opération constante
- **Note** : Si le nombre d'arguments était variable (par exemple `Math.max(...tableau)`), ce serait O(n)

**B. colors[1]** : **O(1)**

- Accès direct par index

**C. person.age = 26** : **O(1)**

- Affectation de propriété par clé

**D. 2 \*\* 10** : **O(1)**

- Opération arithmétique constante
- **Note** : Pour des exposants très grands, cela pourrait devenir plus complexe, mais pour les nombres JavaScript standards, c'est O(1)

</details>

---

## 📦 2. Opérations en Temps Linéaire : O(n)

### 2.1 Définition

Les opérations en **temps linéaire**, notées **O(n)**, ont un temps d'exécution qui croît **proportionnellement** à la taille de l'entrée.

Si l'entrée double, le temps d'exécution double aussi.

---

### 2.2 Boucles Simples

Une boucle qui itère `n` fois, effectuant des opérations O(1) à chaque itération, résulte en **O(n)**.

```javascript
function printElements(arr) {
  // Soit n = arr.length

  for (let i = 0; i < arr.length; i++) {
    // Boucle : n itérations
    console.log(arr[i]); // O(1) à chaque itération
  }

  // Total : n × O(1) = O(n)
}

const numbers = [10, 20, 30, 40, 50];
printElements(numbers); // O(5) = O(n) où n = 5
```

**Analyse détaillée :**

| Opération             | Complexité | Exécutions |
| --------------------- | ---------- | ---------- |
| `i = 0`               | O(1)       | 1 fois     |
| `i < arr.length`      | O(1)       | n+1 fois   |
| `i++`                 | O(1)       | n fois     |
| `console.log(arr[i])` | O(1)       | n fois     |

**Total : n + n + (n+1) + 1 = 3n + 2 → simplifié en O(n)**

---

### 2.3 Recherche dans un Tableau Non Trié

Chercher un élément dans un tableau non trié nécessite de vérifier chaque élément un par un : **O(n)**.

```javascript
function findElement(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    // Itère jusqu'à n fois
    if (arr[i] === target) {
      // O(1) comparaison
      return true; // Trouvé !
    }
  }
  return false; // Non trouvé
}

const data = ["pomme", "banane", "cerise", "datte"];

findElement(data, "cerise"); // Meilleur cas : O(1) (trouvé immédiatement)
findElement(data, "datte"); // Pire cas : O(n) (à la fin)
findElement(data, "raisin"); // Pire cas : O(n) (pas dans le tableau)
```

> ⚠️ **Important**
>
> En analyse de complexité, on considère généralement le **pire cas**. Donc `findElement` est **O(n)**.

---

### 2.4 Méthodes de Tableaux Courantes

De nombreuses méthodes de tableaux intégrées JavaScript opèrent en **O(n)** :

```javascript
const fruits = ["pomme", "banane", "cerise", "datte"];

// Recherche : O(n)
fruits.indexOf("banane"); // O(n)
fruits.includes("raisin"); // O(n)
fruits.find((f) => f.startsWith("c")); // O(n)
fruits.findIndex((f) => f.length > 5); // O(n)

// Itération : O(n)
fruits.forEach((fruit) => console.log(fruit)); // O(n)
fruits.map((fruit) => fruit.toUpperCase()); // O(n)
fruits.filter((fruit) => fruit.length > 5); // O(n)

// Réduction : O(n)
const numbers = [1, 2, 3, 4, 5];
numbers.reduce((sum, num) => sum + num, 0); // O(n)
```

**Pourquoi O(n) ?**

Toutes ces méthodes doivent **parcourir le tableau** élément par élément, donc leur temps d'exécution est proportionnel à la taille du tableau.

---

### 2.5 Opérations sur les Chaînes

Beaucoup d'opérations sur les chaînes sont **O(n)**, où `n` est la longueur de la chaîne.

```javascript
const str = "bonjour monde";

// Longueur : O(1) dans les moteurs modernes
const len = str.length; // O(1)

// Concaténation : O(n + m)
const str1 = "bonjour"; // n = 7
const str2 = " monde"; // m = 6
const result = str1 + str2; // O(n + m) = O(13) → O(n)
// JavaScript doit créer une nouvelle chaîne et copier tous les caractères

// Recherche dans une chaîne : O(n)
str.indexOf("monde"); // O(n)
str.includes("jour"); // O(n)

// Conversion : O(n)
str.toUpperCase(); // O(n) - doit parcourir tous les caractères
str.split(" "); // O(n) - doit parcourir la chaîne
```

> 💡 **Note sur la Concaténation**
>
> Concaténer deux chaînes de longueurs `n` et `m` est **O(n + m)**, car JavaScript doit créer une nouvelle chaîne et copier tous les caractères des deux chaînes.

---

## 📝 Micro-Exercice #2 : Analyser des Boucles

Quelle est la complexité temporelle de cette fonction ?

```javascript
function sumArray(numbers) {
  let total = 0;
  for (let i = 0; i < numbers.length; i++) {
    total += numbers[i];
  }
  return total;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Complexité : O(n)** où n = `numbers.length`

**Analyse :**

- `total = 0` : O(1) - 1 fois
- Boucle `for` : n itérations
  - `total += numbers[i]` : O(1) - n fois
- `return total` : O(1) - 1 fois

**Total : O(1) + n × O(1) + O(1) = O(n)**

**Conclusion :** La boucle domine la complexité, donc la fonction est **O(n)**.

</details>

---

## 📦 3. Opérations en Temps Quadratique : O(n²)

### 3.1 Définition

Les opérations en **temps quadratique**, notées **O(n²)**, ont un temps d'exécution qui croît avec le **carré** de la taille de l'entrée.

Si l'entrée double, le temps d'exécution **quadruple**.

---

### 3.2 Boucles Imbriquées

Le pattern le plus courant pour O(n²) est les **boucles imbriquées** où la boucle interne itère `n` fois pour chaque itération de la boucle externe.

```javascript
function printPairs(arr) {
  // Soit n = arr.length

  for (let i = 0; i < arr.length; i++) {
    // Boucle externe : n fois
    for (let j = 0; j < arr.length; j++) {
      // Boucle interne : n fois pour chaque i
      console.log(arr[i], arr[j]); // O(1)
    }
  }

  // Total : n × n × O(1) = O(n²)
}

const elements = [1, 2, 3];
printPairs(elements);

/*
Sortie :
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3

Total : 3 × 3 = 9 opérations = n²
*/
```

**Analyse :**

| Taille n | Opérations (n²) |
| -------- | --------------- |
| 10       | 100             |
| 100      | 10 000          |
| 1 000    | 1 000 000       |
| 10 000   | 100 000 000     |

> ⚠️ **Avertissement**
>
> La croissance de O(n²) est **très rapide**. Évitez les boucles imbriquées sur de grandes données !

---

### 3.3 Exemple Pratique : Recherche de Doublons

Vérifions si un tableau contient des doublons avec des boucles imbriquées.

```javascript
function areThereDuplicates(arr) {
  // Soit n = arr.length

  for (let i = 0; i < arr.length; i++) {
    // Boucle externe : n fois
    for (let j = 0; j < arr.length; j++) {
      // Boucle interne : n fois
      if (i !== j && arr[i] === arr[j]) {
        // O(1)
        return true; // Doublons trouvés
      }
    }
  }

  return false; // Pas de doublons
}

console.log(areThereDuplicates([1, 2, 3, 4, 5])); // false
console.log(areThereDuplicates([1, 2, 3, 2, 5])); // true
```

**Complexité : O(n²)**

**Amélioration possible (aperçu) :**

Avec un objet JavaScript comme hash table, on peut réduire cela à **O(n)** :

```javascript
function areThereDuplicatesOptimized(arr) {
  const seen = {}; // Hash table

  for (let i = 0; i < arr.length; i++) {
    // O(n)
    if (seen[arr[i]]) {
      // O(1) lookup
      return true;
    }
    seen[arr[i]] = true; // O(1) assignment
  }

  return false;
}

// O(n) au lieu de O(n²) !
```

---

### 3.4 Opérations sur les Matrices

Les opérations sur des matrices carrées impliquent souvent des boucles imbriquées : **O(n²)**.

```javascript
function createZeroMatrix(size) {
  const matrix = [];

  for (let i = 0; i < size; i++) {
    // Boucle externe : size fois
    matrix[i] = [];
    for (let j = 0; j < size; j++) {
      // Boucle interne : size fois
      matrix[i][j] = 0; // O(1)
    }
  }

  return matrix;
}

const myMatrix = createZeroMatrix(5);
// Crée une matrice 5×5 = 25 opérations = O(5²) = O(n²)

console.log(myMatrix);
/*
[
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0]
]
*/
```

---

## 📝 Micro-Exercice #3 : Boucles Imbriquées

Quelle est la complexité de cette fonction ?

```javascript
function findPairSum(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === target) {
        return [arr[i], arr[j]];
      }
    }
  }
  return null;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Complexité : O(n²)**

**Analyse :**

- Boucle externe : n itérations
- Boucle interne : commence à `i+1`, donc fait (n-1) + (n-2) + ... + 1 itérations
- Total : (n-1) + (n-2) + ... + 1 = n(n-1)/2 ≈ n²/2

**Simplification Big O : n²/2 → O(n²)**

> 💡 **Observation**
>
> Même si la boucle interne ne parcourt qu'environ la moitié des éléments (grâce à `j = i + 1`), la complexité reste **O(n²)** car on ignore les constantes.

</details>

---

## 📦 4. Opérations en Temps Logarithmique : O(log n)

### 4.1 Définition

Les opérations en **temps logarithmique**, notées **O(log n)**, voient leur temps d'exécution augmenter **très lentement** par rapport à la taille de l'entrée.

À chaque étape, le problème est **divisé** (généralement par 2).

---

### 4.2 Recherche Binaire (Conceptuel)

La **recherche binaire** fonctionne sur des données **triées** en divisant répétitivement l'intervalle de recherche par deux.

**Analogie : Trouver une Page dans un Livre**

Imaginez que vous cherchez la page 73 dans un livre de 100 pages.

1. **Étape 1** : Ouvrez à la page 50
   - 73 > 50 → Cherchez dans les pages 51-100
2. **Étape 2** : Ouvrez à la page 75
   - 73 < 75 → Cherchez dans les pages 51-75
3. **Étape 3** : Ouvrez à la page 63
   - 73 > 63 → Cherchez dans les pages 64-75
4. **Étape 4** : Ouvrez à la page 69
   - 73 > 69 → Cherchez dans les pages 70-75
5. **Étape 5** : Ouvrez à la page 72
   - 73 > 72 → Cherchez dans les pages 73-75
6. **Étape 6** : Ouvrez à la page 73
   - **Trouvé !**

**Résultat :** En **6 étapes**, vous avez trouvé la page dans un livre de 100 pages.

**Calcul mathématique :** log₂(100) ≈ 6,64 → environ 7 comparaisons maximum

---

### 4.3 Exemple JavaScript : Recherche Binaire

```javascript
function binarySearch(sortedArr, target) {
  let left = 0;
  let right = sortedArr.length - 1;

  while (left <= right) {
    // Chaque itération réduit l'espace de recherche de moitié
    const mid = Math.floor((left + right) / 2);

    if (sortedArr[mid] === target) {
      return mid; // Trouvé !
    } else if (sortedArr[mid] < target) {
      left = mid + 1; // Chercher dans la moitié droite
    } else {
      right = mid - 1; // Chercher dans la moitié gauche
    }
  }

  return -1; // Non trouvé
}

const numbers = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]; // Tableau trié
console.log(binarySearch(numbers, 13)); // 6 (index de 13)
console.log(binarySearch(numbers, 8)); // -1 (non trouvé)
```

**Complexité : O(log n)**

**Comparaison avec la recherche linéaire :**

| Taille n | Linéaire O(n) | Binaire O(log n) |
| -------- | ------------- | ---------------- |
| 10       | 10            | 4                |
| 100      | 100           | 7                |
| 1 000    | 1 000         | 10               |
| 1 000000 | 1 000 000     | **20**           |

> 🚀 **Performance Impressionnante**
>
> Pour chercher dans **1 million d'éléments**, la recherche binaire ne nécessite que **20 comparaisons** au maximum !

---

### 4.4 Autres Exemples de O(log n)

**Arbres Binaires de Recherche Équilibrés** (Module 5)

- Recherche, insertion, suppression : O(log n)

**Algorithmes de Division** (Module 6)

- Merge Sort, Quick Sort (dans le meilleur cas)

---

## 💻 5. Exemples Pratiques et Démonstrations

### Exemple 1 : Calculer la Somme d'un Tableau

```javascript
function calculateSum(arr) {
  let total = 0; // O(1)

  for (let i = 0; i < arr.length; i++) {
    // O(n)
    total += arr[i]; // O(1)
  }

  return total; // O(1)
}

// Test avec un grand tableau
const largeArray = Array.from({ length: 10000 }, (_, i) => i + 1);
console.time("calculateSum Large");
console.log(calculateSum(largeArray)); // 50005000
console.timeEnd("calculateSum Large");

// Test avec un petit tableau
const smallArray = [1, 2, 3, 4, 5];
console.time("calculateSum Small");
console.log(calculateSum(smallArray)); // 15
console.timeEnd("calculateSum Small");
```

**Complexité : O(n)**

La boucle domine la complexité.

---

### Exemple 2 : Trouver un Caractère Dupliqué dans une Chaîne

```javascript
function hasDuplicateChar(str) {
  for (let i = 0; i < str.length; i++) {
    // Boucle externe : n fois
    for (let j = i + 1; j < str.length; j++) {
      // Boucle interne
      if (str[i] === str[j]) {
        // O(1)
        return true;
      }
    }
  }
  return false;
}

console.log(hasDuplicateChar("abcdefg")); // false
console.log(hasDuplicateChar("bonjour")); // true (o apparaît deux fois)

const longString = "abcdefghijklmnopqrstuvwxyza"; // 27 caractères
console.time("hasDuplicateChar");
console.log(hasDuplicateChar(longString)); // true
console.timeEnd("hasDuplicateChar");
```

**Complexité : O(n²)**

Les boucles imbriquées rendent cette fonction quadratique.

---

### Exemple 3 : Vérifier une Propriété d'Objet

```javascript
function checkProperty(obj, prop) {
  return obj.hasOwnProperty(prop); // O(1)
}

const userProfile = {
  id: 1,
  username: "coder123",
  email: "coder@example.com",
  isAdmin: false,
};

console.log(checkProperty(userProfile, "username")); // true
console.log(checkProperty(userProfile, "password")); // false
```

**Complexité : O(1)**

L'accès direct par clé est constant.

---

### Exemple 4 : `push()` et `pop()` sur les Tableaux

```javascript
let myStack = [];

// Opérations push : O(1) amorti
myStack.push(10); // O(1)
myStack.push(20); // O(1)
myStack.push(30); // O(1)

console.log("Après push :", myStack); // [10, 20, 30]

// Opérations pop : O(1)
let poppedElement = myStack.pop(); // O(1)
console.log("Élément retiré :", poppedElement); // 30
console.log("Après pop :", myStack); // [10, 20]
```

**Complexité : O(1) amorti**

> 💡 **Amortissement**
>
> Occasionnellement, JavaScript doit réallouer de la mémoire pour le tableau (O(n)), mais cela arrive si rarement que le **coût amorti** reste O(1).

---

### Exemple 5 : `shift()` et `unshift()` sur les Tableaux

```javascript
let myQueue = [1, 2, 3];

// unshift : O(n) - ajouter au début
myQueue.unshift(0); // O(n) - tous les éléments doivent être décalés
console.log("Après unshift :", myQueue); // [0, 1, 2, 3]

// shift : O(n) - retirer du début
let shiftedElement = myQueue.shift(); // O(n) - tous les éléments doivent être décalés
console.log("Élément retiré :", shiftedElement); // 0
console.log("Après shift :", myQueue); // [1, 2, 3]
```

**Complexité : O(n)**

> ⚠️ **Attention**
>
> `shift()` et `unshift()` sont **beaucoup plus lents** que `push()` et `pop()` car ils nécessitent de déplacer tous les éléments du tableau.

**Pourquoi O(n) ?**

- `unshift(0)` : Place 0 à l'index 0, puis décale tous les anciens éléments d'une position vers la droite
- `shift()` : Retire l'élément à l'index 0, puis décale tous les éléments restants d'une position vers la gauche

---

## 📊 6. Récapitulatif des Complexités

### 6.1 Tableau Récapitulatif

| Opération                          | Complexité | Exemple                            |
| ---------------------------------- | ---------- | ---------------------------------- |
| **Affectation de variable**        | O(1)       | `let x = 10;`                      |
| **Opérations arithmétiques**       | O(1)       | `let sum = 5 + 3;`                 |
| **Accès tableau/objet**            | O(1)       | `arr[5]`, `obj.name`               |
| **push(), pop()**                  | O(1)       | `arr.push(10)`, `arr.pop()`        |
| **Boucle simple**                  | O(n)       | `for (let i = 0; i < n; i++)`      |
| **Recherche linéaire**             | O(n)       | `arr.indexOf(x)`, `arr.includes()` |
| **shift(), unshift()**             | O(n)       | `arr.shift()`, `arr.unshift(0)`    |
| **Boucles imbriquées (2 niveaux)** | O(n²)      | Boucle dans une boucle             |
| **Recherche binaire**              | O(log n)   | Sur un tableau trié                |

---

### 6.2 Comparaison Visuelle

**Pour n = 1000 :**

```
O(1)      : 1 opération
O(log n)  : ~10 opérations
O(n)      : 1 000 opérations
O(n log n): ~10 000 opérations
O(n²)     : 1 000 000 opérations
O(2ⁿ)     : ... nombre astronomique
```

---

## 💪 Exercices Pratiques

### Exercice 1 : Identifier les Opérations en Temps Constant

Pour chacune des opérations suivantes, déterminez si c'est O(1) et expliquez pourquoi.

```javascript
// A
Math.pow(2, 10);

// B
document.getElementById("my-element");

// C
myArray[myArray.length - 1];

// D
let result = 100 / 0;
```

<details>
<summary>💡 Voir la solution</summary>

**A. Math.pow(2, 10)** : **O(1)**

- Avec des arguments constants, c'est une opération en temps constant
- **Note** : Si l'exposant était très grand (genre 10^6), cela pourrait devenir plus complexe, mais pour les valeurs JavaScript standards, c'est O(1)

**B. document.getElementById("my-element")** : **O(1)**

- L'accès par ID dans le DOM est optimisé avec une hash table
- Recherche directe par clé

**C. myArray[myArray.length - 1]** : **O(1)**

- `myArray.length` : O(1)
- Accès par index : O(1)
- Total : O(1)

**D. let result = 100 / 0** : **O(1)**

- Division est une opération arithmétique constante
- Résultat : `Infinity` en JavaScript

</details>

---

### Exercice 2 : Analyser une Boucle Linéaire

Analysez cette fonction :

```javascript
function findMax(numbers) {
  if (numbers.length === 0) {
    return undefined;
  }

  let max = numbers[0];
  for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
      max = numbers[i];
    }
  }
  return max;
}
```

**Questions :**

a. Quelle est la complexité Big O de `findMax` ?

b. Si le tableau `numbers` a 1000 éléments, combien de comparaisons (`numbers[i] > max`) sont effectuées dans le pire cas ?

c. Si le tableau a 1 000 000 d'éléments, combien de comparaisons sont effectuées ?

<details>
<summary>💡 Voir la solution</summary>

**a. Complexité : O(n)** où n = `numbers.length`

**Analyse :**

- `numbers.length === 0` : O(1)
- `max = numbers[0]` : O(1)
- Boucle `for` : n-1 itérations (commence à i=1)
  - `numbers[i] > max` : O(1) - (n-1) fois
  - `max = numbers[i]` : O(1) - au maximum (n-1) fois
- `return max` : O(1)

**Total : O(1) + (n-1) × O(1) = O(n)**

**b. Pour 1000 éléments :**

La boucle commence à `i = 1` et se termine à `i = 999`, donc **999 comparaisons**.

**c. Pour 1 000 000 d'éléments :**

La boucle effectue **999 999 comparaisons**.

**Observation :** Le nombre de comparaisons croît linéairement avec n.

</details>

---

### Exercice 3 : Évaluer la Complexité Quadratique

Analysez cette fonction :

```javascript
function areThereDuplicates(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      if (i !== j && arr[i] === arr[j]) {
        return true;
      }
    }
  }
  return false;
}
```

**Questions :**

a. Quelle est la complexité Big O de `areThereDuplicates` ?

b. Décrivez un scénario pour un tableau où cette fonction effectuerait le nombre maximum d'opérations.

c. Comment `areThereDuplicates` se compare-t-elle à `hasDuplicateChar` (qui utilisait `j = i + 1`) ? Ont-elles la même complexité Big O ? Expliquez.

<details>
<summary>💡 Voir la solution</summary>

**a. Complexité : O(n²)** où n = `arr.length`

**Analyse :**

- Boucle externe : n itérations
- Boucle interne : n itérations pour chaque itération externe
- Total : n × n = **n² comparaisons**

**b. Scénario du pire cas :**

Un tableau **sans doublons**, par exemple `[1, 2, 3, 4, 5]`.

Dans ce cas, la fonction doit vérifier **toutes les paires possibles** avant de retourner `false` :

- Pour n = 5 : 5 × 5 = 25 comparaisons

**c. Comparaison avec `hasDuplicateChar` (j = i + 1) :**

**Même complexité Big O : O(n²)**

**Différences subtiles :**

- `areThereDuplicates` : n² comparaisons (boucle interne complète)
- `hasDuplicateChar` : n²/2 comparaisons (boucle interne commence à i+1)

**En notation Big O :**

- n² et n²/2 se simplifient tous deux en **O(n²)** (on ignore les constantes)

**Conclusion :** Même complexité asymptotique, mais `hasDuplicateChar` est **2 fois plus rapide** en pratique.

</details>

---

### Exercice 4 : Analyser les Méthodes de Tableaux

Déterminez la complexité Big O pour ces opérations JavaScript courantes. Supposez que `arr` a n éléments.

```javascript
// A
arr.slice(0, arr.length / 2);

// B
arr.splice(5, 1);

// C
arr.concat([4, 5, 6]);

// D
arr.map((item) => item * 2);
```

<details>
<summary>💡 Voir la solution</summary>

**A. arr.slice(0, arr.length / 2)** : **O(n)**

- `slice()` crée un **nouveau tableau** avec une portion des éléments
- Doit copier n/2 éléments → O(n/2) → simplifié en **O(n)**

**B. arr.splice(5, 1)** : **O(n)**

- `splice()` retire un élément à l'index 5
- Tous les éléments après l'index 5 doivent être **décalés vers la gauche**
- Dans le pire cas (retrait au début), c'est O(n)

**C. arr.concat([4, 5, 6])** : **O(n + m)**

- `concat()` crée un **nouveau tableau** combinant les deux tableaux
- Doit copier tous les éléments de `arr` (n éléments) et du tableau `[4, 5, 6]` (m éléments)
- Total : **O(n + m)**
- Si m est petit et constant (comme 3), on peut simplifier en O(n)

**D. arr.map(item => item \* 2)** : **O(n)**

- `map()` parcourt **tous les éléments** du tableau une fois
- Applique une fonction O(1) à chaque élément
- Total : n × O(1) = **O(n)**

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1 : Temps Constant

Laquelle de ces opérations est **O(1)** ?

- [ ] A. `arr.indexOf(target)`
- [ ] B. `arr[0]`
- [ ] C. `arr.forEach(x => console.log(x))`
- [ ] D. `arr.filter(x => x > 10)`

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication :**

- **A. arr.indexOf(target)** : O(n) - doit parcourir le tableau
- **B. arr[0]** : **O(1)** - accès direct par index
- **C. arr.forEach(...)** : O(n) - parcourt tous les éléments
- **D. arr.filter(...)** : O(n) - parcourt tous les éléments

</details>

---

### Question 2 : Boucles Simples

Quelle est la complexité de ce code ?

```javascript
function processArray(arr) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(arr[i] * 2);
  }
  return result;
}
```

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

**Explication :**

- La boucle `for` itère **n fois** (où n = arr.length)
- À chaque itération :
  - `arr[i] * 2` : O(1)
  - `result.push(...)` : O(1) amorti
- Total : n × O(1) = **O(n)**

</details>

---

### Question 3 : Boucles Imbriquées

Quelle est la complexité de ce code ?

```javascript
function createPairs(arr) {
  let pairs = [];
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      pairs.push([arr[i], arr[j]]);
    }
  }
  return pairs;
}
```

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n²)
- [ ] D. O(2ⁿ)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

**Explication :**

- Boucle externe : n itérations
- Boucle interne : (n-1) + (n-2) + ... + 1 = n(n-1)/2 itérations
- Total : n²/2 → simplifié en **O(n²)**

**Même si la boucle interne commence à i+1 (ce qui réduit de moitié les opérations), la complexité reste O(n²).**

</details>

---

### Question 4 : Méthodes de Tableaux

Parmi ces méthodes, laquelle est **O(1)** ?

- [ ] A. `arr.shift()`
- [ ] B. `arr.push(x)`
- [ ] C. `arr.unshift(x)`
- [ ] D. `arr.splice(0, 1)`

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication :**

- **A. arr.shift()** : O(n) - retire du début, tous les éléments doivent être décalés
- **B. arr.push(x)** : **O(1)** - ajoute à la fin, pas de décalage
- **C. arr.unshift(x)** : O(n) - ajoute au début, tous les éléments doivent être décalés
- **D. arr.splice(0, 1)** : O(n) - retire au début, tous les éléments doivent être décalés

</details>

---

### Question 5 : Recherche

Un tableau trié de 1 000 000 d'éléments. Combien de comparaisons **au maximum** faut-il pour trouver un élément avec la **recherche binaire** ?

- [ ] A. 10
- [ ] B. 20
- [ ] C. 1 000
- [ ] D. 1 000 000

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication :**

La recherche binaire a une complexité **O(log₂ n)**.

**Calcul :**

- log₂(1 000 000) ≈ 19,93
- Donc environ **20 comparaisons maximum**

**Comparaison avec la recherche linéaire :**

- Linéaire : 1 000 000 comparaisons (pire cas)
- Binaire : 20 comparaisons (pire cas)

**La recherche binaire est 50 000 fois plus rapide !**

</details>

---

### Question 6 : Opérations sur Chaînes

Quelle est la complexité de cette opération ?

```javascript
let str = "";
for (let i = 0; i < n; i++) {
  str += "x";
}
```

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n²)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

**Explication :**

En JavaScript, la concaténation de chaînes avec `+=` crée une **nouvelle chaîne** à chaque itération.

**Analyse détaillée :**

- Itération 1 : copier 0 caractères + ajouter 1 → 1 opération
- Itération 2 : copier 1 caractère + ajouter 1 → 2 opérations
- Itération 3 : copier 2 caractères + ajouter 1 → 3 opérations
- ...
- Itération n : copier (n-1) caractères + ajouter 1 → n opérations

**Total : 1 + 2 + 3 + ... + n = n(n+1)/2 ≈ n²/2 → O(n²)**

**Meilleure approche :**

```javascript
let arr = [];
for (let i = 0; i < n; i++) {
  arr.push("x");
}
let str = arr.join(""); // O(n) au lieu de O(n²)
```

</details>

---

### Question 7 : Complexité Globale

Quelle est la complexité de ce code ?

```javascript
function process(arr) {
  // Étape 1
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }

  // Étape 2
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      console.log(arr[i], arr[j]);
    }
  }
}
```

- [ ] A. O(n)
- [ ] B. O(n²)
- [ ] C. O(n³)
- [ ] D. O(n + n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication :**

**Analyse :**

- Étape 1 : O(n) - boucle simple
- Étape 2 : O(n²) - boucles imbriquées

**Total : O(n) + O(n²)**

**Simplification Big O :**

Quand on additionne des complexités, on garde **le terme dominant** :

- O(n) + O(n²) = **O(n²)**

**Pourquoi ?**

Pour n = 1000 :

- O(n) = 1 000 opérations
- O(n²) = 1 000 000 opérations
- Total : 1 001 000 ≈ 1 000 000

Le terme n² **domine largement**, donc on simplifie en **O(n²)**.

</details>

---

## 📌 Récapitulatif de la Leçon

### Points Clés à Retenir

1. **Opérations O(1)** : Temps constant, indépendant de n
   - Affectation de variables
   - Opérations arithmétiques
   - Accès tableau/objet par index/clé
   - `push()`, `pop()`

2. **Opérations O(n)** : Temps linéaire, proportionnel à n
   - Boucles simples
   - Recherche linéaire (`indexOf`, `includes`)
   - `map()`, `filter()`, `forEach()`
   - `shift()`, `unshift()`

3. **Opérations O(n²)** : Temps quadratique, croissance très rapide
   - Boucles imbriquées
   - Opérations sur matrices
   - Comparaison de toutes les paires

4. **Opérations O(log n)** : Temps logarithmique, très efficace
   - Recherche binaire (sur données triées)
   - Arbres binaires de recherche équilibrés

5. **Règles d'Analyse**
   - Identifier le terme dominant
   - Ignorer les constantes et termes inférieurs
   - Considérer le pire cas (généralement)

6. **Méthodes de Tableaux à Connaître**
   - **Rapides** : `push()`, `pop()`, `arr[i]`
   - **Lentes** : `shift()`, `unshift()`, `splice()`

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous savez maintenant analyser la complexité des opérations JavaScript fondamentales. Cette compétence est **essentielle** pour :

- Écrire du code performant
- Identifier les goulots d'étranglement
- Choisir les bonnes structures de données
- Anticiper les problèmes de performance

### Ce Que Vous Avez Appris

Dans cette leçon, vous avez maîtrisé :

- L'analyse des opérations de base (affectation, arithmétique, accès)
- La reconnaissance des patterns de complexité (boucles simples/imbriquées)
- La comparaison des méthodes de tableaux JavaScript
- L'application de Big O à du code réel

## ➡️ Prochaine Étape : Leçon 6

### Ce qui vous attend

La prochaine leçon, **« Mise en Place d'une Étude de Cas - Optimisation d'un Gestionnaire de Tâches »**, est l'endroit où la théorie rencontre la pratique.

**Vous découvrirez :**

- Comment analyser un système simple existant pour y déceler des faiblesses.
- L'identification des **goulots d'étranglement** de performance dans une application réelle.
- L'application de la notation Big O pour prédire les problèmes de scalabilité.

### Préparez-vous !

C'est le moment de voir comment les concepts de complexité s'appliquent à un vrai projet, et de préparer le terrain pour les optimisations que nous apprendrons dans les modules suivants.

---

## 🔗 Ressources Complémentaires

### Documentation

- [MDN - Array Methods](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [JavaScript.info - Arrays](https://javascript.info/array)
- [JavaScript.info - Array Methods](https://javascript.info/array-methods)

### Outils de Visualisation

- [Visualgo - Algorithmes Visuels](https://visualgo.net/)
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)

### Pour Aller Plus Loin

- **Recherche Binaire** : Algorithme fondamental à maîtriser
- **Structures de Données Avancées** : Hash Tables, Arbres (Modules 3-5)
- **Algorithmes de Tri** : Tri Fusion, Tri Rapide (Module 4)

---

**Prêt pour la Leçon 6 ?** 🚀

Rendez-vous dans la prochaine leçon pour mettre en pratique vos connaissances sur une étude de cas concrète : l'optimisation d'un gestionnaire de tâches !

---

<div align="center">

**Leçon 5 sur 42 - Module 1 : Fondements des algorithmes et révision de JavaScript**

[⬅️ Leçon 4 : Notation Big O](./lecon-4-notation-big-o.md) | [Retour au sommaire](./README.md) | [Leçon 6 : Étude de Cas - Gestionnaire de Tâches ➡️](./lecon-6-etude-cas-gestionnaire-taches.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
