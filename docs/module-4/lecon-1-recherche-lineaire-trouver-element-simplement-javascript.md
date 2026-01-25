##### Leçon 19 sur 42

# Recherche Linéaire : Trouver un Élément Simplement en JavaScript

**Module 4** : Algorithmes de Recherche et Introduction à la Récursion

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **concept fondamental** de la recherche linéaire et son mécanisme de parcours séquentiel
- **Implémenter** la recherche linéaire en JavaScript pour différents types de données
- **Analyser** la complexité temporelle O(n) et spatiale O(1) de l'algorithme
- **Identifier** les cas d'utilisation appropriés et les cas limites (tableau vide, occurrences multiples)
- **Adapter** l'algorithme pour des comparaisons personnalisées (objets, insensibilité à la casse)
- **Appliquer** la recherche linéaire à notre étude de cas de gestion de tâches

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- **Module 1 complété** : Maîtriser la notation Big O et l'analyse de complexité
- **Module 2 complété** : Comprendre les tableaux et leurs opérations de base
- **Module 3 complété** : Connaître les algorithmes de tri et l'importance des données ordonnées
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : La Quête de l'Élément Perdu

Avez-vous déjà cherché vos clés dans un sac désorganisé ? Vous sortez chaque objet, un par un, jusqu'à trouver ce que vous cherchez. Ou encore, avez-vous feuilleté un livre page par page pour retrouver un passage particulier ? Félicitations, vous avez effectué une **recherche linéaire** sans le savoir !

La **recherche linéaire** (ou recherche séquentielle) est l'algorithme de recherche le plus simple et le plus intuitif. Elle consiste à parcourir une collection d'éléments **un par un**, du début à la fin, jusqu'à trouver l'élément recherché ou avoir parcouru toute la collection.

Pourquoi étudier cet algorithme "basique" ?

- C'est la **base** de tous les algorithmes de recherche
- Elle fonctionne sur des données **non triées** (contrairement à la recherche binaire)
- Elle est **universelle** : fonctionne avec n'importe quel type de données
- Elle sert de **référence** pour comparer les performances d'autres algorithmes
- Dans certains cas, elle reste **la meilleure option** (petits tableaux, recherche unique)

Dans cette leçon, nous allons explorer en profondeur cet algorithme fondamental, l'implémenter en JavaScript, et découvrir comment l'adapter à différents contextes pratiques.

> **Point Clé**
>
> La recherche linéaire est la méthode la plus directe pour trouver un élément. Simple mais efficace, elle constitue le fondement sur lequel nous construirons notre compréhension d'algorithmes de recherche plus sophistiqués comme la recherche binaire.

---

## 📦 Fonctionnement de la Recherche Linéaire

La recherche linéaire repose sur un principe très simple : **vérifier chaque élément** de la collection jusqu'à trouver ce qu'on cherche.

---

### Mécanisme de Base

Le cœur de la recherche linéaire consiste à itérer à travers chaque élément d'un tableau, un par un, et à le comparer avec la valeur recherchée (la "cible"). Si une correspondance est trouvée, l'index de cet élément est retourné. Si la boucle se termine sans trouver de correspondance, cela signifie que la valeur cible n'est pas présente dans le tableau.

**Étapes détaillées :**

1. **Commencer au début** : La recherche débute au premier élément du tableau (index 0)
2. **Comparer** : L'élément courant est comparé avec la valeur cible
3. **Correspondance trouvée** : Si l'élément courant correspond à la cible, retourner son index
4. **Pas de correspondance** : Sinon, passer à l'élément suivant
5. **Fin du tableau** : Si la fin du tableau est atteinte sans correspondance, indiquer que la cible n'est pas présente (typiquement en retournant -1)

**Caractéristiques clés :**

- **Simple à comprendre** et à implémenter
- **Fonctionne sur des données non triées**
- **Universelle** : fonctionne avec tous types de données
- **Espace constant** : O(1) en complexité spatiale
- **Peut être lente pour de grandes collections** : O(n) en complexité temporelle

---

### Visualisation avec un Exemple Concret

Considérons un tableau de nombres : `[10, 5, 20, 15, 30]`. Si la valeur cible est **20** :

```
Tableau : [10, 5, 20, 15, 30]
Cible   : 20

Étape 1 : Vérifier l'index 0
┌─────┬─────┬─────┬─────┬─────┐
│ 10  │  5  │ 20  │ 15  │ 30  │
└─────┴─────┴─────┴─────┴─────┘
  ↑
  10 === 20 ? Non → Continuer

Étape 2 : Vérifier l'index 1
┌─────┬─────┬─────┬─────┬─────┐
│ 10  │  5  │ 20  │ 15  │ 30  │
└─────┴─────┴─────┴─────┴─────┘
        ↑
        5 === 20 ? Non → Continuer

Étape 3 : Vérifier l'index 2
┌─────┬─────┬─────┬─────┬─────┐
│ 10  │  5  │ 20  │ 15  │ 30  │
└─────┴─────┴─────┴─────┴─────┘
              ↑
              20 === 20 ? Oui → Retourner 2
```

**Résultat** : L'élément 20 est trouvé à l'**index 2**. La recherche s'arrête immédiatement.

---

### Recherche Infructueuse

Si la valeur cible était **25** (absente du tableau) :

```
Étape 1 : 10 === 25 ? Non
Étape 2 : 5 === 25 ? Non
Étape 3 : 20 === 25 ? Non
Étape 4 : 15 === 25 ? Non
Étape 5 : 30 === 25 ? Non

Fin du tableau atteinte → Retourner -1 (non trouvé)
```

---

## 📝 Micro-Exercice #1 : Tracer une Recherche

**Objectif :** Comprendre le mécanisme pas à pas de la recherche linéaire.

**Instructions :** Tracez les étapes de la recherche linéaire pour trouver **"banane"** dans le tableau suivant. Combien de comparaisons sont nécessaires ?

```javascript
const fruits = ["pomme", "banane", "orange", "raisin"];
```

<details>
<summary>💡 Voir la solution</summary>

**Recherche de "banane" :**

| Étape | Index | Élément  | Comparaison             | Résultat |
| ----- | ----- | -------- | ----------------------- | -------- |
| 1     | 0     | "pomme"  | "pomme" === "banane" ?  | Non      |
| 2     | 1     | "banane" | "banane" === "banane" ? | Oui      |

**Résultat** : Trouvé à l'index **1** après **2 comparaisons**.

**Explication :** La recherche commence à l'index 0, compare "pomme" avec "banane" (pas de correspondance), puis passe à l'index 1 où "banane" correspond. La fonction retourne immédiatement l'index 1.

</details>

---

## 💻 Implémentation en JavaScript

Maintenant que nous comprenons le concept, implémentons la recherche linéaire en JavaScript.

---

### Version de Base

L'implémentation utilise typiquement une boucle `for` pour itérer à travers le tableau.

```javascript
/**
 * Implémente une recherche linéaire pour trouver une valeur cible dans un tableau.
 * @param {Array<any>} arr - Le tableau à parcourir.
 * @param {any} target - La valeur à rechercher.
 * @returns {number} - L'index de la valeur cible si trouvée, sinon -1.
 */
function linearSearch(arr, target) {
  // Itérer à travers le tableau du premier au dernier élément
  for (let i = 0; i < arr.length; i++) {
    // Vérifier si l'élément courant correspond à la cible
    if (arr[i] === target) {
      // Si correspondance trouvée, retourner son index
      return i;
    }
  }
  // Si la boucle se termine, la cible n'a pas été trouvée
  return -1;
}

// Exemple 1 : Recherche d'un nombre
const numbers = [4, 2, 7, 1, 9, 5];
console.log("Recherche de 7 dans numbers:", linearSearch(numbers, 7));
// Output: 2 (index de 7)

console.log("Recherche de 10 dans numbers:", linearSearch(numbers, 10));
// Output: -1 (10 n'est pas dans le tableau)

// Exemple 2 : Recherche d'une chaîne
const fruits = ["pomme", "banane", "orange", "raisin"];
console.log(
  "Recherche de 'banane' dans fruits:",
  linearSearch(fruits, "banane"),
);
// Output: 1

console.log("Recherche de 'kiwi' dans fruits:", linearSearch(fruits, "kiwi"));
// Output: -1

// Exemple 3 : Recherche d'un booléen
const booleans = [true, false, true, false];
console.log("Recherche de true dans booleans:", linearSearch(booleans, true));
// Output: 0 (première occurrence)
```

**Analyse du code :**

1. **Fonction `linearSearch`** : Prend un tableau (`arr`) et une valeur cible (`target`) en entrée
2. **Boucle `for`** : Itère de `i = 0` jusqu'à `arr.length - 1`
3. **Comparaison `===`** : Utilise l'opérateur d'égalité stricte (type + valeur)
4. **Retour anticipé** : Dès qu'une correspondance est trouvée, la fonction retourne immédiatement
5. **Retour par défaut** : Si la boucle se termine sans correspondance, retourne -1

---

### Cas Limites et Considérations

**Tableau vide :**

```javascript
const emptyArray = [];
console.log("Recherche dans un tableau vide:", linearSearch(emptyArray, 5));
// Output: -1

// Explication : La condition i < arr.length est immédiatement fausse (0 < 0),
// donc la boucle ne s'exécute jamais et la fonction retourne -1.
```

**Occurrences multiples :**

```javascript
const repeatedNumbers = [1, 5, 2, 5, 8];
console.log(
  "Recherche de 5 dans repeatedNumbers:",
  linearSearch(repeatedNumbers, 5),
);
// Output: 1 (première occurrence)

// La recherche linéaire retourne l'index de la PREMIÈRE occurrence.
// Les occurrences suivantes ne sont pas considérées après la première trouvée.
```

**Types de données :**

```javascript
// La recherche linéaire fonctionne avec n'importe quel type de données
// tant que l'opérateur === peut correctement évaluer l'égalité.

// Nombres
console.log(linearSearch([1, 2, 3], 2)); // 1

// Chaînes
console.log(linearSearch(["a", "b", "c"], "b")); // 1

// Booléens
console.log(linearSearch([false, true], true)); // 1

// Note : Pour comparer des objets par valeur (et non par référence),
// une logique de comparaison personnalisée serait nécessaire.
```

---

## 📝 Micro-Exercice #2 : Implémenter une Variante

**Objectif :** Adapter l'algorithme pour rechercher depuis la fin du tableau.

**Instructions :** Écrivez une fonction `reverseLinearSearch` qui recherche de la fin vers le début. Elle doit retourner l'index de la **dernière occurrence** de la valeur cible.

```javascript
function reverseLinearSearch(arr, target) {
  // Votre implémentation ici
}

// Tests attendus :
// reverseLinearSearch([1, 5, 2, 5, 8], 5) devrait retourner 3
// reverseLinearSearch([1, 2, 3], 7) devrait retourner -1
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recherche linéaire inversée (de la fin vers le début).
 * Retourne l'index de la dernière occurrence de la cible.
 * @param {Array<any>} arr - Le tableau à parcourir.
 * @param {any} target - La valeur à rechercher.
 * @returns {number} - L'index de la dernière occurrence, sinon -1.
 */
function reverseLinearSearch(arr, target) {
  // Parcourir de la fin vers le début
  for (let i = arr.length - 1; i >= 0; i--) {
    if (arr[i] === target) {
      return i;
    }
  }
  return -1;
}

// Tests
console.log(reverseLinearSearch([1, 5, 2, 5, 8], 5)); // 3
console.log(reverseLinearSearch([1, 2, 3], 7)); // -1
console.log(reverseLinearSearch([5, 5, 5], 5)); // 2 (dernière occurrence)
```

**Explication :**

- La boucle commence à `arr.length - 1` (dernier index valide)
- Elle décrémente `i` jusqu'à 0
- La première correspondance trouvée en partant de la fin est automatiquement la dernière occurrence

</details>

---

## 📊 Complexité Temporelle et Spatiale

Rappelons-nous du Module 1 que la complexité temporelle et spatiale mesure l'efficacité d'un algorithme.

---

### Complexité Temporelle (Notation Big O)

La performance de la recherche linéaire dépend de la taille du tableau et de la position de l'élément cible.

| Cas              | Complexité | Description                                              |
| ---------------- | ---------- | -------------------------------------------------------- |
| **Meilleur cas** | O(1)       | L'élément cible est le premier du tableau                |
| **Cas moyen**    | O(n)       | L'élément est quelque part au milieu (~n/2 comparaisons) |
| **Pire cas**     | O(n)       | L'élément est le dernier ou n'est pas présent            |

**Analyse détaillée :**

- **Meilleur cas O(1)** : L'élément cible est le premier élément. Une seule comparaison, retour immédiat.
- **Pire cas O(n)** : L'élément est le dernier ou absent. L'algorithme doit itérer à travers tous les n éléments.
- **Cas moyen O(n)** : En moyenne, l'élément sera trouvé au milieu (~n/2 comparaisons). La notation Big O ignore les constantes, donc O(n).

**Conclusion** : La complexité temporelle est **O(n)**, où n est le nombre d'éléments.

---

### Complexité Spatiale (Notation Big O)

| Aspect                | Complexité |
| --------------------- | ---------- |
| **Espace auxiliaire** | O(1)       |

La recherche linéaire utilise une quantité **constante** d'espace supplémentaire :

- Le compteur de boucle (`i`)
- Les paramètres de fonction (`arr`, `target`)

Elle ne crée aucune nouvelle structure de données proportionnelle à n.

---

### Comparaison avec d'Autres Algorithmes

| Algorithme             | Temps (moyen) | Données triées requises ? | Espace |
| ---------------------- | ------------- | ------------------------- | ------ |
| **Recherche linéaire** | O(n)          | Non                       | O(1)   |
| Recherche binaire      | O(log n)      | Oui                       | O(1)   |
| Table de hachage       | O(1)          | Non                       | O(n)   |

> **Point Clé**
>
> Pour un tableau de **1 million d'éléments** :
>
> - Recherche linéaire : jusqu'à **1 000 000** comparaisons
> - Recherche binaire : maximum **~20** comparaisons (log₂(1 000 000) ≈ 20)
>
> Cependant, la recherche binaire nécessite que les données soient **triées** au préalable !

---

## 📝 Micro-Exercice #3 : Compter les Opérations

**Objectif :** Mesurer empiriquement le nombre de comparaisons effectuées.

**Instructions :** Modifiez la fonction pour compter et retourner le nombre de comparaisons.

```javascript
function linearSearchWithCount(arr, target) {
  // Votre implémentation ici
  // Doit retourner un objet : { index: X, comparisons: Y }
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recherche linéaire avec compteur de comparaisons.
 * @param {Array<any>} arr - Le tableau à parcourir.
 * @param {any} target - La valeur à rechercher.
 * @returns {Object} - { index, comparisons, found }
 */
function linearSearchWithCount(arr, target) {
  let comparisons = 0;

  for (let i = 0; i < arr.length; i++) {
    comparisons++; // Incrémenter avant chaque comparaison

    if (arr[i] === target) {
      return {
        index: i,
        comparisons: comparisons,
        found: true,
      };
    }
  }

  return {
    index: -1,
    comparisons: comparisons,
    found: false,
  };
}

// Tests
console.log(linearSearchWithCount([10, 20, 30, 40, 50], 30));
// { index: 2, comparisons: 3, found: true }

console.log(linearSearchWithCount([10, 20, 30, 40, 50], 60));
// { index: -1, comparisons: 5, found: false }

// Test avec un grand tableau
const largeArray = Array.from({ length: 10000 }, (_, i) => i);
console.log(linearSearchWithCount(largeArray, 9999));
// { index: 9999, comparisons: 10000, found: true }
```

**Explication :**

- Nous ajoutons un compteur `comparisons` initialisé à 0
- Avant chaque comparaison avec la cible, nous incrémentons le compteur
- Cela permet de vérifier empiriquement la complexité O(n)

</details>

---

## 💻 Application Pratique : Étude de Cas

Appliquons la recherche linéaire à notre étude de cas continue de gestion de tâches.

---

### Exemple 1 : Recherche de Tâche par Titre

Imaginons un scénario où les utilisateurs veulent trouver une tâche spécifique par son titre.

```javascript
const tasks = [
  { id: 101, title: "Review pull request", status: "pending" },
  { id: 102, title: "Fix login bug", status: "in-progress" },
  { id: 103, title: "Write unit tests", status: "pending" },
  { id: 104, title: "Deploy to production", status: "completed" },
  { id: 105, title: "Update documentation", status: "pending" },
];

/**
 * Recherche une tâche par son titre dans un tableau d'objets tâche.
 * @param {Array<Object>} tasksArr - Le tableau d'objets tâche.
 * @param {string} targetTitle - Le titre de la tâche à rechercher.
 * @returns {Object|null} - L'objet tâche si trouvé, sinon null.
 */
function findTaskByTitle(tasksArr, targetTitle) {
  for (let i = 0; i < tasksArr.length; i++) {
    // Accéder à la propriété 'title' de chaque objet tâche
    if (tasksArr[i].title === targetTitle) {
      // Retourner l'objet tâche complet si le titre correspond
      return tasksArr[i];
    }
  }
  // Si aucune tâche avec le titre correspondant n'est trouvée
  return null;
}

// Recherche d'une tâche existante
const foundTask1 = findTaskByTitle(tasks, "Write unit tests");
console.log("Tâche trouvée 'Write unit tests':", foundTask1);
// Output: { id: 103, title: 'Write unit tests', status: 'pending' }

// Recherche d'une tâche inexistante
const foundTask2 = findTaskByTitle(tasks, "Develop new feature");
console.log("Tâche trouvée 'Develop new feature':", foundTask2);
// Output: null
```

**Analyse de l'exemple :**

Cet exemple montre comment adapter la recherche linéaire pour des structures de données plus complexes (tableaux d'objets) en modifiant la logique de comparaison pour accéder à des propriétés spécifiques.

---

### Exemple 2 : Recherche Insensible à la Casse

Pour améliorer l'expérience utilisateur, rendons la recherche insensible à la casse :

```javascript
/**
 * Recherche une tâche par titre, insensible à la casse.
 * @param {Array<Object>} tasksArr - Le tableau d'objets tâche.
 * @param {string} targetTitle - Le titre à rechercher.
 * @returns {Object|null} - L'objet tâche si trouvé, sinon null.
 */
function findTaskByTitleCaseInsensitive(tasksArr, targetTitle) {
  // Convertir la cible en minuscules une seule fois
  const lowerCaseTargetTitle = targetTitle.toLowerCase();

  for (let i = 0; i < tasksArr.length; i++) {
    if (tasksArr[i].title.toLowerCase() === lowerCaseTargetTitle) {
      return tasksArr[i];
    }
  }
  return null;
}

// Tests
const foundTask3 = findTaskByTitleCaseInsensitive(tasks, "review pull request");
console.log("Recherche insensible à la casse:", foundTask3);
// Output: { id: 101, title: 'Review pull request', status: 'pending' }

const foundTask4 = findTaskByTitleCaseInsensitive(tasks, "WRITE UNIT TESTS");
console.log("Recherche en majuscules:", foundTask4);
// Output: { id: 103, title: 'Write unit tests', status: 'pending' }
```

---

### Exemple 3 : Suggestions d'Autocomplétion

Imaginons une fonctionnalité d'autocomplétion pour une barre de recherche :

```javascript
const dictionary = [
  "pomme",
  "abricot",
  "banane",
  "bandana",
  "cat",
  "car",
  "dog",
  "donut",
];

/**
 * Génère des suggestions d'autocomplétion basées sur un préfixe.
 * @param {Array<string>} list - La liste de mots à rechercher.
 * @param {string} prefix - Le préfixe de recherche.
 * @returns {Array<string>} - Un tableau de suggestions correspondantes.
 */
function getSuggestions(list, prefix) {
  const matchingSuggestions = [];
  // Standardiser le préfixe pour une recherche insensible à la casse
  const lowerCasePrefix = prefix.toLowerCase();

  for (let i = 0; i < list.length; i++) {
    const currentWord = list[i].toLowerCase();
    // Vérifier si le mot commence par le préfixe
    if (currentWord.startsWith(lowerCasePrefix)) {
      // Ajouter le mot original (avec sa casse) aux résultats
      matchingSuggestions.push(list[i]);
    }
  }

  return matchingSuggestions;
}

// Tests
console.log("Suggestions pour 'ap':", getSuggestions(dictionary, "ap"));
// Output: ['pomme', 'abricot']

console.log("Suggestions pour 'ban':", getSuggestions(dictionary, "ban"));
// Output: ['banane', 'bandana']

console.log("Suggestions pour 'c':", getSuggestions(dictionary, "c"));
// Output: ['cat', 'car']

console.log("Suggestions pour 'Z':", getSuggestions(dictionary, "Z"));
// Output: []
```

**Analyse de l'exemple :**

Cet exemple montre la recherche linéaire utilisée pour filtrer des éléments basés sur une correspondance partielle, un pattern courant dans les interfaces utilisateur.

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension de la recherche linéaire, implémentez les problèmes suivants.

---

### Exercice 1 : Trouver Toutes les Occurrences

**Objectif :** Modifier la recherche linéaire pour retourner tous les indices où la cible apparaît.

**Instructions :** Implémentez une fonction qui retourne un tableau de tous les indices où la valeur cible est trouvée. Si la cible n'est pas trouvée, retournez un tableau vide.

```javascript
// Exemple d'utilisation :
// findAllOccurrences([1, 5, 2, 5, 8, 5], 5) devrait retourner [1, 3, 5]
// findAllOccurrences([1, 2, 3], 7) devrait retourner []
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trouve tous les indices où la cible apparaît.
 * @param {Array<any>} arr - Le tableau à parcourir.
 * @param {any} target - La valeur à rechercher.
 * @returns {Array<number>} - Tableau des indices trouvés.
 */
function findAllOccurrences(arr, target) {
  const indices = [];

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      indices.push(i);
    }
  }

  return indices;
}

// Tests
console.log(findAllOccurrences([1, 5, 2, 5, 8, 5], 5)); // [1, 3, 5]
console.log(findAllOccurrences([1, 2, 3], 7)); // []
console.log(findAllOccurrences([7, 7, 7], 7)); // [0, 1, 2]
```

**Explication de la solution :**

- Au lieu de retourner immédiatement, nous ajoutons l'index à un tableau
- La boucle continue jusqu'à la fin pour trouver toutes les occurrences
- Un tableau vide est retourné si aucune correspondance n'est trouvée

</details>

---

### Exercice 2 : Recherche Inversée (Dernière Occurrence)

**Objectif :** Trouver la dernière occurrence d'un élément.

**Instructions :** Implémentez une fonction qui recherche de la fin vers le début et retourne l'index de la dernière occurrence.

```javascript
// Exemple d'utilisation :
// reverseLinearSearch([1, 5, 2, 5, 8], 5) devrait retourner 3
// reverseLinearSearch([1, 2, 3], 7) devrait retourner -1
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recherche de la fin vers le début.
 * @param {Array<any>} arr - Le tableau à parcourir.
 * @param {any} target - La valeur à rechercher.
 * @returns {number} - L'index de la dernière occurrence, ou -1.
 */
function reverseLinearSearch(arr, target) {
  for (let i = arr.length - 1; i >= 0; i--) {
    if (arr[i] === target) {
      return i;
    }
  }
  return -1;
}

// Tests
console.log(reverseLinearSearch([1, 5, 2, 5, 8], 5)); // 3
console.log(reverseLinearSearch([1, 2, 3], 7)); // -1
console.log(reverseLinearSearch([5, 1, 5], 5)); // 2
```

**Explication de la solution :**

- La boucle commence à l'index `arr.length - 1` et décrémente jusqu'à 0
- La première correspondance trouvée en partant de la fin est la dernière occurrence

</details>

---

### Exercice 3 : Recherche d'Utilisateur par Email

**Objectif :** Appliquer la recherche à un cas réel avec comparaison personnalisée.

**Instructions :** Implémentez une fonction qui trouve un utilisateur par son email. La recherche doit être insensible à la casse.

```javascript
const users = [
  { id: 1, name: "Alice", email: "alice@example.com" },
  { id: 2, name: "Bob", email: "bob@example.com" },
  { id: 3, name: "Charlie", email: "charlie@example.com" },
];

// Exemple d'utilisation :
// findUserByEmail(users, "Bob@example.com") devrait retourner { id: 2, name: "Bob", email: "bob@example.com" }
// findUserByEmail(users, "diana@example.com") devrait retourner null
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recherche un utilisateur par email (insensible à la casse).
 * @param {Array<Object>} users - Tableau d'objets utilisateur.
 * @param {string} email - L'email à rechercher.
 * @returns {Object|null} - L'utilisateur trouvé ou null.
 */
function findUserByEmail(users, email) {
  const normalizedEmail = email.toLowerCase();

  for (let i = 0; i < users.length; i++) {
    if (users[i].email.toLowerCase() === normalizedEmail) {
      return users[i];
    }
  }

  return null;
}

// Tests
const users = [
  { id: 1, name: "Alice", email: "alice@example.com" },
  { id: 2, name: "Bob", email: "bob@example.com" },
  { id: 3, name: "Charlie", email: "charlie@example.com" },
];

console.log(findUserByEmail(users, "Bob@example.com"));
// { id: 2, name: 'Bob', email: 'bob@example.com' }

console.log(findUserByEmail(users, "ALICE@EXAMPLE.COM"));
// { id: 1, name: 'Alice', email: 'alice@example.com' }

console.log(findUserByEmail(users, "diana@example.com"));
// null
```

**Explication de la solution :**

- L'email cible est normalisé en minuscules une seule fois avant la boucle
- Chaque email d'utilisateur est aussi converti en minuscules pour la comparaison
- L'objet utilisateur complet est retourné, pas seulement l'email

</details>

---

### Exercice 4 : Recherche avec Prédicat

**Objectif :** Créer une fonction de recherche générique avec une fonction de test personnalisée.

**Instructions :** Implémentez une fonction qui trouve le premier élément satisfaisant un prédicat (fonction de test).

```javascript
// Exemple d'utilisation :
const numbers = [1, 4, 9, 16, 25];
// findWithPredicate(numbers, x => x > 10) devrait retourner 16
// findWithPredicate(numbers, x => x % 2 === 0) devrait retourner 4
// findWithPredicate(numbers, x => x > 100) devrait retourner undefined
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trouve le premier élément satisfaisant le prédicat.
 * @param {Array<any>} arr - Le tableau à parcourir.
 * @param {Function} predicate - Fonction (element) => boolean.
 * @returns {any} - L'élément trouvé ou undefined.
 */
function findWithPredicate(arr, predicate) {
  for (let i = 0; i < arr.length; i++) {
    if (predicate(arr[i])) {
      return arr[i];
    }
  }
  return undefined;
}

// Tests
const numbers = [1, 4, 9, 16, 25];
console.log(findWithPredicate(numbers, (x) => x > 10)); // 16
console.log(findWithPredicate(numbers, (x) => x % 2 === 0)); // 4
console.log(findWithPredicate(numbers, (x) => x > 100)); // undefined

// Note : Cette fonction est équivalente à Array.prototype.find() !
console.log(numbers.find((x) => x > 10)); // 16
```

**Explication de la solution :**

- Le prédicat est une fonction qui prend un élément et retourne true/false
- Nous appliquons le prédicat à chaque élément jusqu'à en trouver un qui retourne true
- Cette approche est très flexible et équivalente à la méthode native `Array.prototype.find()`

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la complexité temporelle de la recherche linéaire dans le pire cas ?**

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Dans le pire cas (élément absent ou à la fin), la recherche linéaire doit parcourir tous les n éléments du tableau, effectuant n comparaisons. La complexité est donc O(n).

</details>

---

### Question 2

**La recherche linéaire nécessite-t-elle des données triées pour fonctionner ?**

- [ ] A. Oui, toujours
- [ ] B. Non, jamais
- [ ] C. Seulement pour les nombres
- [ ] D. Seulement pour les chaînes

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La recherche linéaire **ne nécessite pas** de données triées. C'est l'un de ses avantages par rapport à la recherche binaire qui, elle, requiert des données triées pour fonctionner correctement.

</details>

---

### Question 3

**Que retourne typiquement une fonction de recherche linéaire si l'élément n'est pas trouvé ?**

- [ ] A. 0
- [ ] B. undefined
- [ ] C. -1
- [ ] D. false

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Par convention, -1 est retourné pour indiquer que l'élément n'a pas été trouvé. C'est aussi le comportement des méthodes natives JavaScript comme `indexOf()`. Le choix de -1 est logique car c'est un index invalide (les index commencent à 0).

</details>

---

### Question 4

**Quelle est la complexité spatiale de la recherche linéaire ?**

- [ ] A. O(n)
- [ ] B. O(log n)
- [ ] C. O(n²)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

La recherche linéaire utilise une quantité **constante** de mémoire supplémentaire (quelques variables comme le compteur de boucle), indépendamment de la taille du tableau d'entrée. Elle ne crée pas de nouvelles structures de données proportionnelles à n.

</details>

---

### Question 5

**Si un tableau contient plusieurs occurrences de la valeur recherchée, laquelle la recherche linéaire standard retourne-t-elle ?**

- [ ] A. La dernière
- [ ] B. La première
- [ ] C. Une au hasard
- [ ] D. Toutes

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La recherche linéaire standard retourne l'index de la **première** occurrence trouvée, car elle s'arrête immédiatement dès qu'une correspondance est trouvée. Les occurrences suivantes ne sont pas examinées.

</details>

---

### Question 6

**Dans quel cas la recherche linéaire est-elle plus appropriée que la recherche binaire ?**

- [ ] A. Quand le tableau est trié
- [ ] B. Quand le tableau est très grand
- [ ] C. Quand le tableau n'est pas trié
- [ ] D. Quand on recherche plusieurs éléments simultanément

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La recherche linéaire est appropriée quand les données **ne sont pas triées**. La recherche binaire nécessite des données triées. Si le coût de trier le tableau est supérieur au coût d'une recherche linéaire (par exemple, pour une recherche unique), la recherche linéaire est préférable.

</details>

---

### Question 7

**Pour un tableau de 1000 éléments, combien de comparaisons au maximum la recherche linéaire effectue-t-elle ?**

- [ ] A. 10
- [ ] B. 100
- [ ] C. 500
- [ ] D. 1000

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Dans le pire cas, la recherche linéaire parcourt **tous les éléments** du tableau. Pour n = 1000, elle effectue au maximum 1000 comparaisons. C'est la nature même de la complexité O(n).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe Fondamental

La recherche linéaire parcourt les éléments un par un, du début à la fin, jusqu'à trouver l'élément recherché ou atteindre la fin du tableau.

### 2. Complexité Temporelle

O(n) dans le pire et moyen cas, O(1) dans le meilleur cas (élément en première position). Le temps d'exécution croît linéairement avec la taille du tableau.

### 3. Complexité Spatiale

O(1) - utilise une quantité constante de mémoire supplémentaire, indépendamment de la taille de l'entrée.

### 4. Données Non Triées

Fonctionne sur des données non triées, contrairement à la recherche binaire. C'est un avantage majeur dans de nombreuses situations.

### 5. Première Occurrence

Par défaut, retourne l'index de la première occurrence trouvée. Peut être modifié pour trouver toutes les occurrences ou la dernière.

### 6. Adaptabilité

Facilement adaptable pour des comparaisons personnalisées : objets, insensibilité à la casse, prédicats, correspondances partielles.

### 7. Cas d'Utilisation Idéaux

Petits tableaux, données non triées, recherche unique, cas où le tri serait plus coûteux que la recherche.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maîtrisé la recherche linéaire, l'algorithme de recherche le plus fondamental en informatique.

### Ce que vous avez appris aujourd'hui

- Le concept et le fonctionnement détaillé de la recherche linéair
- L'implémentation en JavaScript avec différentes variante
- L'analyse de complexité temporelle O(n) et spatiale O(1)
- La gestion des cas limites (tableau vide, occurrences multiples)
- L'adaptation pour des comparaisons personnalisées

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter la recherche linéaire de zéro en JavaScrip
- Adapter l'algorithme à différents types de données et comparaison
- Analyser quand utiliser la recherche linéaire vs d'autres méthodes

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La recherche linéaire est le **fondement** de tous les algorithmes de recherche. Comprendre ses forces et limitations vous permettra d'apprécier les optimisations offertes par des algorithmes plus avancés. De plus, dans de nombreux cas pratiques (petits tableaux, données non triées, recherche unique), elle reste la solution la plus simple et appropriée. Comme disait Donald Knuth : "Premature optimization is the root of all evil" - parfois, la solution simple est la meilleure !

---

## ➡️ Prochaine Étape : Leçon 20

### Ce qui vous attend

La prochaine leçon, **« Recherche Binaire : Recherche Efficace dans les Tableaux Triés »**, vous fera découvrir un algorithme beaucoup plus rapide pour les données triées !

**Vous découvrirez :**

- Le principe de **diviser pour régner** appliqué à la recherche
- Une complexité de **O(log n)** vs O(n) - une amélioration dramatique
- Pourquoi les données **triées** permettent cette optimisation
- L'implémentation itérative et récursive de l'algorithme

### Préparez-vous !

La recherche binaire est l'une des optimisations les plus impressionnantes en algorithmique. Pour 1 million d'éléments, elle réduit le nombre de comparaisons de **1 000 000 à seulement ~20** !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Searching](https://visualgo.net/en/sorting) - Visualisation interactive des algorithmes de recherche
- [MDN - Array.prototype.indexOf()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) - Méthode native de recherche linéaire
- [MDN - Array.prototype.find()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/find) - Recherche avec prédicat

### Outils de pratique

- **[JS Bin](https://jsbin.com/)** : Testez vos implémentations en ligne
- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez l'exécution pas à pas de votre code

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour bien ancrer la recherche linéaire dans votre esprit, prenez un jeu de cartes mélangé et cherchez une carte spécifique (par exemple, le 7 de cœur). Comptez combien de cartes vous devez retourner. Répétez l'expérience plusieurs fois et observez comment le nombre de cartes varie selon la position de la carte recherchée. C'est la recherche linéaire en action !

---

**Prêt pour la Leçon 20 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir la puissance de la recherche binaire !

---

<div align="center">

**Leçon 19 sur 42 - Module 4 : Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Leçon 18 : Tri Rapide (Quick Sort) : Sélection du Pivot et Partitionnement en JavaScript](../module-3/lecon-6-tri-rapide-selection-pivot-partitionnement-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 20 : Recherche Binaire : Recherche Efficace dans les Tableaux Triés ➡️](./lecon-2-recherche-binaire-recherche-efficace-tableaux-tries.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
