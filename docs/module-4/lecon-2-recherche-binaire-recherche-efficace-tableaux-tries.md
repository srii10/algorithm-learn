##### Leçon 20 sur 42

# Recherche Binaire : Recherche Efficace dans les Tableaux Triés

**Module 4** : Algorithmes de Recherche et Introduction à la Récursion

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **principe fondamental** de la recherche binaire et son approche "diviser pour régner"
- Expliquer pourquoi les **données triées** sont une exigence absolue pour cet algorithme
- **Implémenter** la recherche binaire de manière itérative en JavaScript
- **Analyser** la complexité temporelle O(log n) et comprendre son avantage sur O(n)
- **Comparer** la recherche binaire avec la recherche linéaire et choisir la méthode appropriée
- Appliquer la recherche binaire à des **cas pratiques** comme l'indexation de bases de données

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 19 complétée** : Maîtriser la recherche linéaire et sa complexité O(n)
- **Module 3 complété** : Comprendre les algorithmes de tri et l'importance des données ordonnées
- **Module 1 complété** : Maîtriser la notation Big O, notamment O(log n)
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Le Pouvoir de la Division

Imaginez que vous dSarrz trouver le mot "algorithme" dans un dictionnaire de 1000 pages. Allez-vous vraiment commencer à la page 1 et feuilleter chaque page une par une ? Bien sûr que non ! Vous ouvrez le dictionnaire au milieu, regardez si vous êtes avant ou après la lettre "A", puis vous répétez le processus dans la moitié pertinente.

C'est exactement le principe de la **recherche binaire** : au lieu de vérifier chaque élément un par un comme dans la recherche linéaire, nous **divisons par deux** l'espace de recherche à chaque étape.

Le résultat est spectaculaire :

- Pour **1 million d'éléments** : recherche linéaire = jusqu'à 1 000 000 comparaisons
- Pour **1 million d'éléments** : recherche binaire = maximum **~20** comparaisons !

C'est la différence entre chercher pendant des heures et trouver en quelques secondes. Mais il y a un prix à payer : les données **doivent être triées**. Dans cette leçon, nous allons explorer en profondeur cet algorithme puissant et comprendre pourquoi il est si efficace.

> **Point Clé**
>
> La recherche binaire illustre parfaitement le principe "diviser pour régner" : en éliminant systématiquement la moitié des possibilités à chaque étape, on atteint une efficacité logarithmique O(log n) qui surpasse largement la recherche linéaire O(n) pour les grands ensembles de données.

---

## 📦 Concepts Fondamentaux de la Recherche Binaire

La recherche binaire repose sur le principe fondamental de **"diviser pour régner"**. Pour qu'elle fonctionne, les données **doivent être triées**.

---

### L'Exigence de Données Triées

L'exigence stricte de la recherche binaire est que le tableau d'entrée doit être trié en ordre croissant (ou décroissant). Sans données triées, la logique d'élimination de la moitié de l'espace de recherche devient invalide.

**Pourquoi le tri est-il nécessaire ?**

Considérons la recherche du nombre **5** :

```
Tableau NON trié : [10, 2, 8, 5, 1]
                           ↑
                      Milieu = 8

Question : 5 est-il à gauche ou à droite de 8 ?
Réponse : IMPOSSIBLE à déterminer sans vérifier tous les éléments !

---

Tableau TRIÉ : [1, 2, 5, 8, 10]
                      ↑
                 Milieu = 5

Question : 5 est-il à gauche ou à droite de 5 ?
Réponse : C'est 5 ! Trouvé directement.
```

**Caractéristiques clés :**

- **Données triées** : Exigence absolue et non négociable
- **Diviser pour régner** : Élimination de la moitié à chaque étape
- **Complexité O(log n)** : Drastiquement plus rapide que O(n)
- **Espace O(1)** : Version itérative en espace constant
- **Coût du tri** : Si les données ne sont pas triées, il faut les trier d'abord

---

### Mécanisme de Base

L'algorithme fonctionne en trois étapes répétées :

1. **Examiner l'élément du milieu** du tableau (ou sous-tableau courant)
2. **Comparer** avec la valeur cible :
   - Si égal → Trouvé ! Retourner l'index
   - Si cible < milieu → Chercher dans la moitié gauche
   - Si cible > milieu → Chercher dans la moitié droite
3. **Répéter** jusqu'à trouver ou jusqu'à épuisement de l'espace de recherche

---

### Visualisation Complète

Recherchons le nombre **23** dans le tableau trié :

```javascript
const numbers = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91];
//               0  1  2   3   4   5   6   7   8   9  (indices)
```

```
État initial : low = 0, high = 9

=== ITÉRATION 1 ===
┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
│  2 │  5 │  8 │ 12 │ 16 │ 23 │ 38 │ 56 │ 72 │ 91 │
└────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
  0    1    2    3    4    5    6    7    8    9
  ↑                   ↑                        ↑
 low                 mid                     high

mid = Math.floor((0 + 9) / 2) = 4
numbers[4] = 16

23 > 16 → Chercher à DROITE → low = mid + 1 = 5

=== ITÉRATION 2 ===
┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
│  2 │  5 │  8 │ 12 │ 16 │ 23 │ 38 │ 56 │ 72 │ 91 │
└────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
                            5    6    7    8    9
                            ↑         ↑         ↑
                           low       mid      high

mid = Math.floor((5 + 9) / 2) = 7
numbers[7] = 56

23 < 56 → Chercher à GAUCHE → high = mid - 1 = 6

=== ITÉRATION 3 ===
┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
│  2 │  5 │  8 │ 12 │ 16 │ 23 │ 38 │ 56 │ 72 │ 91 │
└────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
                           5    6
                           ↑    ↑
                      low/mid  high

mid = Math.floor((5 + 6) / 2) = 5
numbers[5] = 23

23 === 23 → TROUVÉ à l'index 5 !
```

**Résultat** : Trouvé en seulement **3 comparaisons** au lieu de 6 avec la recherche linéaire !

---

## 📝 Micro-Exercice #1 : Tracer une Recherche

**Objectif :** Comprendre le mécanisme de réduction de l'espace de recherche.

**Instructions :** Tracez les étapes de la recherche binaire pour trouver **60** dans le tableau suivant. Notez les valeurs de `low`, `high`, `mid` et `arr[mid]` à chaque itération.

```javascript
const arr = [10, 20, 30, 40, 50, 60, 70, 80];
//            0   1   2   3   4   5   6   7
```

<details>
<summary>💡 Voir la solution</summary>

**Recherche de 60 :**

| Itération | low | high | mid | arr[mid] | Comparaison | Action   |
| --------- | --- | ---- | --- | -------- | ----------- | -------- |
| 1         | 0   | 7    | 3   | 40       | 60 > 40     | low = 4  |
| 2         | 4   | 7    | 5   | 60       | 60 === 60   | Trouvé ! |

**Résultat** : Trouvé à l'index **5** après **2 comparaisons**.

**Détail des étapes :**

1. **Itération 1** : `mid = Math.floor((0 + 7) / 2) = 3`, `arr[3] = 40`. Comme 60 > 40, on cherche à droite : `low = 4`.
2. **Itération 2** : `mid = Math.floor((4 + 7) / 2) = 5`, `arr[5] = 60`. Trouvé !

</details>

---

## 📊 Complexité Temporelle : Pourquoi O(log n) ?

La complexité temporelle de la recherche binaire est **O(log n)**. Cette complexité logarithmique représente une amélioration significative par rapport à O(n) de la recherche linéaire.

---

### Comprendre la Complexité Logarithmique

À chaque étape, l'algorithme réduit l'espace de recherche **de moitié** :

```
Départ    : n éléments
Après 1 comparaison : n/2 éléments
Après 2 comparaisons : n/4 éléments
Après 3 comparaisons : n/8 éléments
...
Après k comparaisons : n/2^k éléments
```

La recherche s'arrête quand `n/2^k = 1`, c'est-à-dire quand `n = 2^k`.

En résolvant pour k : **k = log₂(n)**

| Taille du tableau (n) | Comparaisons max (log₂ n) | Recherche linéaire (n) |
| --------------------- | ------------------------- | ---------------------- |
| 10                    | ~4                        | 10                     |
| 100                   | ~7                        | 100                    |
| 1 000                 | ~10                       | 1 000                  |
| 10 000                | ~14                       | 10 000                 |
| 100 000               | ~17                       | 100 000                |
| 1 000 000             | ~20                       | 1 000 000              |

> **Point Clé**
>
> Pour **1 million d'éléments**, la recherche binaire nécessite au maximum **~20 comparaisons** contre **1 000 000** pour la recherche linéaire. C'est une amélioration de **50 000x** !

---

### Comparaison des Complexités

| Aspect               | Recherche Linéaire | Recherche Binaire |
| -------------------- | ------------------ | ----------------- |
| **Temps (meilleur)** | O(1)               | O(1)              |
| **Temps (moyen)**    | O(n)               | O(log n)          |
| **Temps (pire)**     | O(n)               | O(log n)          |
| **Espace**           | O(1)               | O(1) (itératif)   |
| **Données triées**   | Non requises       | **Requises**      |

---

## 📝 Micro-Exercice #2 : Calculer les Comparaisons

**Objectif :** Comprendre l'impact de la complexité logarithmique.

**Instructions :** Pour un tableau de **1024 éléments**, combien de comparaisons maximum sont nécessaires avec :

1. La recherche linéaire ?
2. La recherche binaire ?

<details>
<summary>💡 Voir la solution</summary>

**Réponses :**

1. **Recherche linéaire** : Maximum **1024** comparaisons (O(n))
2. **Recherche binaire** : Maximum **10** comparaisons (O(log n))

**Calcul pour la recherche binaire :**

log₂(1024) = 10 (car 2¹⁰ = 1024)

**Explication :**

- Après 1 comparaison : 512 éléments restants
- Après 2 comparaisons : 256 éléments restants
- Après 3 comparaisons : 128 éléments restants
- Après 4 comparaisons : 64 éléments restants
- Après 5 comparaisons : 32 éléments restants
- Après 6 comparaisons : 16 éléments restants
- Après 7 comparaisons : 8 éléments restants
- Après 8 comparaisons : 4 éléments restants
- Après 9 comparaisons : 2 éléments restants
- Après 10 comparaisons : 1 élément restant

La recherche binaire est **102.4x plus rapide** pour ce cas !

</details>

---

## 💻 Implémentation en JavaScript

L'implémentation de la recherche binaire utilise typiquement une boucle qui met continuellement à jour les pointeurs `low` et `high`.

---

### Version Itérative

L'approche itérative utilise une boucle `while` qui continue tant que `low` est inférieur ou égal à `high`.

```javascript
/**
 * Implémente une recherche binaire itérative.
 * @param {Array<number>} arr - Le tableau TRIÉ à parcourir.
 * @param {number} target - La valeur à rechercher.
 * @returns {number} - L'index de la cible si trouvée, sinon -1.
 */
function binarySearch(arr, target) {
  // Initialiser les pointeurs de début et de fin
  let low = 0;
  let high = arr.length - 1;

  // Continuer tant que l'espace de recherche est valide
  while (low <= high) {
    // Calculer l'index du milieu
    // Note : low + Math.floor((high - low) / 2) évite le débordement d'entier
    let mid = low + Math.floor((high - low) / 2);

    // Vérifier si l'élément du milieu est la cible
    if (arr[mid] === target) {
      return mid; // Trouvé ! Retourner l'index
    }

    // Si la cible est plus grande, chercher dans la moitié droite
    if (arr[mid] < target) {
      low = mid + 1;
    }
    // Si la cible est plus petite, chercher dans la moitié gauche
    else {
      high = mid - 1;
    }
  }

  // La cible n'a pas été trouvée
  return -1;
}

// Tests avec différents cas
const sortedNumbers = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91];

console.log(binarySearch(sortedNumbers, 23)); // 5 (trouvé à l'index 5)
console.log(binarySearch(sortedNumbers, 12)); // 3 (trouvé à l'index 3)
console.log(binarySearch(sortedNumbers, 91)); // 9 (trouvé à l'index 9)
console.log(binarySearch(sortedNumbers, 2)); // 0 (trouvé à l'index 0)
console.log(binarySearch(sortedNumbers, 100)); // -1 (non trouvé)
console.log(binarySearch(sortedNumbers, 1)); // -1 (non trouvé)

// Cas limites
console.log(binarySearch([], 5)); // -1 (tableau vide)
console.log(binarySearch([7], 7)); // 0 (élément unique trouvé)
console.log(binarySearch([7], 9)); // -1 (élément unique non trouvé)
```

**Analyse du code :**

1. **Initialisation** : `low = 0` et `high = arr.length - 1` définissent l'espace de recherche initial
2. **Condition de boucle** : `low <= high` garantit qu'il reste des éléments à vérifier
3. **Calcul de mid** : `low + Math.floor((high - low) / 2)` évite le débordement d'entier
4. **Comparaison** : Trois cas possibles - trouvé, chercher à droite, chercher à gauche
5. **Retour -1** : Si la boucle se termine, la cible n'existe pas

---

### Pourquoi cette Formule pour `mid` ?

```javascript
// Potentiel problème de débordement dans d'autres langages
let mid = Math.floor((low + high) / 2);

// Version sûre
let mid = low + Math.floor((high - low) / 2);
```

En JavaScript, ce n'est pas un problème car les nombres sont représentés en virgule flottante. Cependant, dans des langages comme C ou Java avec des entiers 32 bits, `low + high` pourrait dépasser la valeur maximale. C'est une bonne pratique à adopter.

---

### Version avec Visualisation

```javascript
/**
 * Recherche binaire avec affichage des étapes
 */
function binarySearchVisual(arr, target) {
  console.log(`\nRecherche de ${target} dans [${arr.join(", ")}]`);
  console.log("─".repeat(60));

  let low = 0;
  let high = arr.length - 1;
  let iteration = 0;

  while (low <= high) {
    iteration++;
    let mid = low + Math.floor((high - low) / 2);

    console.log(`\n   Itération ${iteration}:`);
    console.log(`   low=${low}, high=${high}, mid=${mid}`);
    console.log(`   arr[${mid}] = ${arr[mid]}`);

    if (arr[mid] === target) {
      console.log(`${target} === ${arr[mid]} → TROUVÉ !`);
      console.log(`\nTrouvé à l'index ${mid} en ${iteration} itération(s)`);
      return mid;
    }

    if (arr[mid] < target) {
      console.log(`   ${target} > ${arr[mid]} → Chercher à DROITE`);
      low = mid + 1;
    } else {
      console.log(`   ${target} < ${arr[mid]} → Chercher à GAUCHE`);
      high = mid - 1;
    }
  }

  console.log(`\nNon trouvé après ${iteration} itération(s)`);
  return -1;
}

// Test
binarySearchVisual([2, 5, 8, 12, 16, 23, 38, 56, 72, 91], 23);
```

---

## 📝 Micro-Exercice #3 : Gérer les Cas Limites

**Objectif :** Vérifier la robustesse de l'implémentation.

**Instructions :** Que retourne `binarySearch` pour les cas suivants ? Réfléchissez avant d'exécuter le code.

```javascript
binarySearch([], 5); // ?
binarySearch([5], 5); // ?
binarySearch([5], 10); // ?
binarySearch([1, 2, 3], 0); // ?
binarySearch([1, 2, 3], 4); // ?
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
binarySearch([], 5); // -1 (tableau vide, low=0 > high=-1)
binarySearch([5], 5); // 0  (trouvé immédiatement)
binarySearch([5], 10); // -1 (10 > 5, low=1 > high=0)
binarySearch([1, 2, 3], 0); // -1 (0 < 1, high devient -1)
binarySearch([1, 2, 3], 4); // -1 (4 > 3, low devient 3 > high=2)
```

**Explication :**

1. **Tableau vide** : `high = -1`, la condition `low <= high` est fausse dès le départ
2. **Élément unique trouvé** : `mid = 0`, `arr[0] === 5`, retourne 0
3. **Élément unique non trouvé** : `mid = 0`, `10 > 5`, `low = 1 > high = 0`, boucle terminée
4. **Cible avant le début** : La cible est toujours plus petite, `high` devient négatif
5. **Cible après la fin** : La cible est toujours plus grande, `low` dépasse `high`

</details>

---

## 💻 Application Pratique : Étude de Cas

Appliquons la recherche binaire à des scénarios réels.

---

### Exemple 1 : Recherche dans un Dictionnaire

Simulons la recherche d'un mot dans un dictionnaire (liste triée alphabétiquement) :

```javascript
/**
 * Recherche binaire dans un dictionnaire de mots triés.
 * @param {Array<string>} dictionary - Liste de mots triés alphabétiquement.
 * @param {string} word - Le mot à rechercher.
 * @returns {number} - L'index du mot si trouvé, sinon -1.
 */
function searchDictionary(dictionary, word) {
  let low = 0;
  let high = dictionary.length - 1;

  // Normaliser la recherche (insensible à la casse)
  const targetWord = word.toLowerCase();

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);
    const currentWord = dictionary[mid].toLowerCase();

    if (currentWord === targetWord) {
      return mid;
    }

    // Comparaison lexicographique
    if (currentWord < targetWord) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return -1;
}

// Dictionnaire français trié alphabétiquement
const dictionnaire = [
  "algorithme", // 0
  "binaire", // 1
  "complexite", // 2
  "donnees", // 3
  "efficace", // 4
  "fonction", // 5
  "graphe", // 6
  "hachage", // 7
  "iteration", // 8
  "javascript", // 9
  "lineaire", // 10
  "noeud", // 11
  "objet", // 12
  "recursion", // 13
  "tableau", // 14
];

console.log(searchDictionary(dictionnaire, "hachage")); // 7
console.log(searchDictionary(dictionnaire, "recursion")); // 13
console.log(searchDictionary(dictionnaire, "python")); // -1 (non trouvé)
console.log(searchDictionary(dictionnaire, "ALGORITHME")); // 0 (insensible à la casse)
```

**Analyse de l'exemple :**

La comparaison lexicographique en JavaScript (`<` et `>` sur les chaînes) fonctionne directement pour les mots, ce qui rend l'adaptation de la recherche binaire très simple. Notez que les mots sont triés sans accents pour simplifier la comparaison.

---

### Exemple 2 : Indexation de Base de Données

Simulons comment une base de données utilise la recherche binaire pour trouver rapidement des enregistrements :

```javascript
/**
 * Simule un index de base de données avec recherche binaire.
 */
const usersIndex = [
  { id: 101, name: "Chermann" },
  { id: 105, name: "Ingrid" },
  { id: 112, name: "Prudence" },
  { id: 118, name: "Germain" },
  { id: 125, name: "Sarr" },
  { id: 130, name: "Sing" },
  { id: 142, name: "Destinée" },
  { id: 155, name: "Marc-Élie" },
];
// Note : L'index est trié par ID

/**
 * Recherche un utilisateur par ID en utilisant la recherche binaire.
 * @param {Array<Object>} index - Index trié par ID.
 * @param {number} targetId - L'ID à rechercher.
 * @returns {Object|null} - L'utilisateur si trouvé, sinon null.
 */
function findUserById(index, targetId) {
  let low = 0;
  let high = index.length - 1;

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);

    if (index[mid].id === targetId) {
      return index[mid];
    }

    if (index[mid].id < targetId) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return null;
}

// Tests
console.log(findUserById(usersIndex, 118));
// { id: 118, name: 'Germain' }

console.log(findUserById(usersIndex, 142));
// { id: 142, name: 'Destinée' }

console.log(findUserById(usersIndex, 200));
// null
```

**Application réelle :**

C'est exactement ainsi que fonctionnent les index de bases de données (comme les B-trees). Quand vous exécutez :

```sql
SELECT * FROM users WHERE id = 118;
```

La base de données n'examine pas chaque ligne - elle utilise une structure d'index similaire pour trouver rapidement l'enregistrement.

---

### Exemple 3 : Trouver la Position d'Insertion

Parfois, on veut trouver où **insérer** un élément pour maintenir l'ordre trié :

```javascript
/**
 * Trouve l'index où insérer un élément pour maintenir l'ordre trié.
 * @param {Array<number>} arr - Le tableau trié.
 * @param {number} target - La valeur à insérer.
 * @returns {number} - L'index d'insertion.
 */
function findInsertPosition(arr, target) {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);

    if (arr[mid] === target) {
      return mid; // L'élément existe déjà
    }

    if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  // 'low' est maintenant la position d'insertion correcte
  return low;
}

// Tests
const arr = [10, 20, 30, 40];

console.log(findInsertPosition(arr, 25)); // 2 (insérer avant 30)
console.log(findInsertPosition(arr, 5)); // 0 (insérer au début)
console.log(findInsertPosition(arr, 50)); // 4 (insérer à la fin)
console.log(findInsertPosition(arr, 30)); // 2 (existe déjà à l'index 2)
```

**Explication :**

Quand la boucle se termine sans trouver l'élément, `low` pointe vers la position où l'élément devrait être inséré pour maintenir l'ordre.

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension de la recherche binaire, implémentez les problèmes suivants.

---

### Exercice 1 : Tracer l'Algorithme

**Objectif :** Comprendre en profondeur le mécanisme de la recherche binaire.

**Instructions :** Pour le tableau `[10, 20, 30, 40, 50, 60, 70, 80]` et `target = 60`, tracez manuellement les étapes. Notez `low`, `high`, `mid`, `arr[mid]` pour chaque itération.

<details>
<summary>💡 Voir la solution</summary>

```
Tableau : [10, 20, 30, 40, 50, 60, 70, 80]
          [ 0,  1,  2,  3,  4,  5,  6,  7]  ← indices
Target : 60

ITÉRATION 1:
  low = 0, high = 7
  mid = Math.floor((0 + 7) / 2) = 3
  arr[3] = 40
  60 > 40 → low = mid + 1 = 4

ITÉRATION 2:
  low = 4, high = 7
  mid = Math.floor((4 + 7) / 2) = 5
  arr[5] = 60
  60 === 60 → TROUVÉ !

Résultat : Index 5, trouvé en 2 itérations
```

</details>

---

### Exercice 2 : Position d'Insertion

**Objectif :** Modifier la recherche binaire pour retourner la position d'insertion.

**Instructions :** Implémentez une fonction qui retourne l'index où insérer `target` pour maintenir l'ordre trié.

```javascript
// Exemple :
// findInsertPosition([10, 20, 30, 40], 25) → 2
// findInsertPosition([10, 20, 30, 40], 5)  → 0
// findInsertPosition([10, 20, 30, 40], 50) → 4
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trouve l'index d'insertion pour maintenir l'ordre trié.
 * @param {Array<number>} arr - Le tableau trié.
 * @param {number} target - La valeur à insérer.
 * @returns {number} - L'index d'insertion.
 */
function findInsertPosition(arr, target) {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);

    if (arr[mid] === target) {
      return mid; // L'élément existe, retourner sa position
    }

    if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  // Quand la boucle se termine, 'low' est la position d'insertion
  return low;
}

// Tests
console.log(findInsertPosition([10, 20, 30, 40], 25)); // 2
console.log(findInsertPosition([10, 20, 30, 40], 5)); // 0
console.log(findInsertPosition([10, 20, 30, 40], 50)); // 4
console.log(findInsertPosition([10, 20, 30, 40], 30)); // 2 (existe déjà)
```

**Explication :**

Quand la boucle se termine sans trouver l'élément :

- `low` pointe vers le premier élément plus grand que `target`
- C'est exactement l'endroit où `target` doit être inséré

</details>

---

### Exercice 3 : Recherche Binaire pour Chaînes

**Objectif :** Adapter la recherche binaire pour des chaînes de caractères.

**Instructions :** Implémentez une fonction `binarySearchStrings(arr, target)` qui effectue une recherche binaire sur un tableau de chaînes triées alphabétiquement.

```javascript
// Exemple :
const sortedWords = ["pomme", "banane", "raisin", "kiwi", "orange", "poire"];
// binarySearchStrings(sortedWords, "kiwi")  → 3
// binarySearchStrings(sortedWords, "mangue") → -1
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recherche binaire sur un tableau de chaînes triées.
 * @param {Array<string>} arr - Le tableau de chaînes trié alphabétiquement.
 * @param {string} target - La chaîne à rechercher.
 * @returns {number} - L'index si trouvé, sinon -1.
 */
function binarySearchStrings(arr, target) {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);

    // Comparaison directe des chaînes (lexicographique)
    if (arr[mid] === target) {
      return mid;
    }

    // En JavaScript, < et > fonctionnent lexicographiquement sur les chaînes
    if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return -1;
}

// Tests
const sortedWords = ["pomme", "banane", "raisin", "kiwi", "orange", "poire"];

console.log(binarySearchStrings(sortedWords, "kiwi")); // 3
console.log(binarySearchStrings(sortedWords, "mangue")); // -1
console.log(binarySearchStrings(sortedWords, "pomme")); // 0
console.log(binarySearchStrings(sortedWords, "poire")); // 5
console.log(binarySearchStrings(sortedWords, "abricot")); // -1
```

**Explication :**

En JavaScript, les opérateurs `<` et `>` comparent les chaînes lexicographiquement (ordre du dictionnaire). Donc "pomme" < "banane" est `true`, et "orange" > "kiwi" est aussi `true`.

</details>

---

### Exercice 4 : Compter les Occurrences

**Objectif :** Trouver le nombre d'occurrences d'un élément dans un tableau trié.

**Instructions :** Utilisez la recherche binaire pour trouver la première et la dernière occurrence d'un élément, puis calculez le nombre d'occurrences.

```javascript
// Exemple :
// countOccurrences([1, 2, 2, 2, 3, 4, 5], 2) → 3
// countOccurrences([1, 1, 1, 1, 1], 1) → 5
// countOccurrences([1, 2, 3, 4, 5], 6) → 0
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trouve le premier index d'un élément dans un tableau trié.
 */
function findFirst(arr, target) {
  let low = 0;
  let high = arr.length - 1;
  let result = -1;

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);

    if (arr[mid] === target) {
      result = mid;
      high = mid - 1; // Continuer à chercher à gauche
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return result;
}

/**
 * Trouve le dernier index d'un élément dans un tableau trié.
 */
function findLast(arr, target) {
  let low = 0;
  let high = arr.length - 1;
  let result = -1;

  while (low <= high) {
    let mid = low + Math.floor((high - low) / 2);

    if (arr[mid] === target) {
      result = mid;
      low = mid + 1; // Continuer à chercher à droite
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return result;
}

/**
 * Compte les occurrences d'un élément.
 */
function countOccurrences(arr, target) {
  const first = findFirst(arr, target);
  if (first === -1) return 0;

  const last = findLast(arr, target);
  return last - first + 1;
}

// Tests
console.log(countOccurrences([1, 2, 2, 2, 3, 4, 5], 2)); // 3
console.log(countOccurrences([1, 1, 1, 1, 1], 1)); // 5
console.log(countOccurrences([1, 2, 3, 4, 5], 6)); // 0
console.log(countOccurrences([2, 2, 2, 2, 2], 2)); // 5
```

**Explication :**

Pour compter les occurrences en O(log n), on trouve la première occurrence (en continuant à chercher à gauche même après avoir trouvé) et la dernière occurrence (en continuant à chercher à droite).

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est l'exigence fondamentale pour utiliser la recherche binaire ?**

- [ ] A. Le tableau doit contenir uniquement des nombres
- [ ] B. Le tableau doit être trié
- [ ] C. Le tableau doit avoir une taille paire
- [ ] D. Le tableau doit contenir au moins 10 éléments

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La recherche binaire nécessite **absolument** que les données soient triées (ordre croissant ou décroissant). Sans tri, on ne peut pas déterminer si l'élément recherché est à gauche ou à droite du point milieu.

</details>

---

### Question 2

**Quelle est la complexité temporelle de la recherche binaire ?**

- [ ] A. O(1)
- [ ] B. O(n)
- [ ] C. O(log n)
- [ ] D. O(n log n)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La recherche binaire a une complexité de **O(log n)** car à chaque étape, elle réduit l'espace de recherche de moitié. Pour n éléments, il faut au maximum log₂(n) comparaisons.

</details>

---

### Question 3

**Pour un tableau de 1 million d'éléments, combien de comparaisons maximum la recherche binaire nécessite-t-elle ?**

- [ ] A. 10
- [ ] B. 20
- [ ] C. 1000
- [ ] D. 1 000 000

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

log₂(1 000 000) ≈ **20** comparaisons. C'est la puissance de la complexité logarithmique ! Comparé à la recherche linéaire qui nécessiterait jusqu'à 1 million de comparaisons.

</details>

---

### Question 4

**Dans l'implémentation itérative, que signifie la condition `low <= high` ?**

- [ ] A. Il reste des éléments à vérifier
- [ ] B. L'élément a été trouvé
- [ ] C. Le tableau est trié
- [ ] D. L'index est valide

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

La condition `low <= high` indique qu'il reste un **espace de recherche valide**. Quand `low > high`, l'espace de recherche est épuisé et l'élément n'existe pas dans le tableau.

</details>

---

### Question 5

**Pourquoi utilise-t-on `low + Math.floor((high - low) / 2)` au lieu de `Math.floor((low + high) / 2)` ?**

- [ ] A. C'est plus rapide
- [ ] B. C'est plus lisible
- [ ] C. Pour éviter le débordement d'entier
- [ ] D. Pour obtenir un résultat différent

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Dans des langages avec des entiers de taille fixe (comme C ou Java), `low + high` pourrait dépasser la valeur maximale (débordement d'entier). La formule `low + (high - low) / 2` évite ce problème en calculant d'abord la différence. Bien que JavaScript gère les grands nombres, c'est une bonne pratique.

</details>

---

### Question 6

**Quel est l'avantage principal de la recherche binaire sur la recherche linéaire ?**

- [ ] A. Elle ne nécessite pas de données triées
- [ ] B. Elle utilise moins de mémoire
- [ ] C. Elle est beaucoup plus rapide pour les grands tableaux
- [ ] D. Elle peut trouver plusieurs occurrences à la fois

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

L'avantage principal est la **vitesse** : O(log n) vs O(n). Pour un million d'éléments, ~20 comparaisons vs 1 million. Cependant, elle nécessite des données triées, ce qui est son inconvénient principal.

</details>

---

### Question 7

**Si la recherche binaire ne trouve pas l'élément, que retourne typiquement la fonction ?**

- [ ] A. 0
- [ ] B. null
- [ ] C. -1
- [ ] D. undefined

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Par convention, **-1** est retourné pour indiquer que l'élément n'a pas été trouvé. C'est cohérent avec les méthodes JavaScript comme `indexOf()`. Le choix de -1 est logique car c'est un index invalide.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe Diviser pour Régner

La recherche binaire divise l'espace de recherche par 2 à chaque étape, éliminant la moitié des éléments restants.

### 2. Exigence de Tri

Les données **doivent être triées** (ordre croissant ou décroissant). Sans tri, l'algorithme ne peut pas fonctionner.

### 3. Complexité O(log n)

La complexité logarithmique signifie que doubler la taille du tableau n'ajoute qu'une seule comparaison supplémentaire.

### 4. Formule du Milieu

`mid = low + Math.floor((high - low) / 2)` évite le débordement d'entier et garantit un calcul correct.

### 5. Condition de Boucle

`while (low <= high)` continue tant qu'il reste un espace de recherche valide. Quand `low > high`, l'élément n'existe pas.

### 6. Mise à Jour des Pointeurs

- Si `target > arr[mid]` : `low = mid + 1` (chercher à droite)
- Si `target < arr[mid]` : `high = mid - 1` (chercher à gauche)

### 7. Applications Pratiques

Utilisée dans les index de bases de données, les systèmes de fichiers, les dictionnaires, et partout où des recherches rapides sont nécessaires.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maîtrisé la recherche binaire, l'un des algorithmes les plus fondamentaux et puissants en informatique.

### Ce que vous avez appris aujourd'hui

- Le principe "diviser pour régner" et pourquoi il est si efficace
- L'exigence absolue de données triées et ses implications
- L'implémentation itérative complète en JavaScript
- L'analyse de la complexité O(log n) et sa supériorité sur O(n)
- Les applications pratiques comme l'indexation de bases de données

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter la recherche binaire de zéro en JavaScript
- Choisir entre recherche linéaire et binaire selon le contexte
- Adapter l'algorithme pour différents cas d'utilisation (insertion, occurrences)

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La recherche binaire n'est pas qu'un algorithme de plus - c'est une **façon de penser**. Le principe de réduire un problème de moitié à chaque étape s'applique à de nombreux domaines : recherche de bugs (bisection), optimisation de jeux vidéo (culling), et bien plus. Comprendre ce principe vous rendra meilleur développeur, pas seulement pour les recherches, mais pour la résolution de problèmes en général.

---

## ➡️ Prochaine Étape : Leçon 21

### Ce qui vous attend

La prochaine leçon, **« Introduction à la Récursion : Cas de Base et Appels Récursifs »**, introduit un concept fondamental qui transformera votre façon de résoudre des problèmes.

**Vous découvrirez :**

- Le principe de la **récursion** : une fonction qui s'appelle elle-même
- L'importance du **cas de base** pour éviter les boucles infinies
- Comment les problèmes se décomposent en **sous-problèmes similaires**
- L'implémentation de la recherche binaire **récursive**

### Préparez-vous !

La récursion est un concept qui peut sembler déroutant au début, mais qui ouvre des portes vers des solutions élégantes et puissantes. La recherche binaire que vous venez d'apprendre peut être exprimée de manière récursive de façon très naturelle !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Binary Search](https://visualgo.net/en/bst) - Visualisation interactive de la recherche binaire
- [MDN - Array.prototype.includes()](https://dSarrloper.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) - Comparaison avec les méthodes natives
- [Wikipedia - Binary Search](https://en.wikipedia.org/wiki/Binary_search_algorithm) - Analyse mathématique approfondie

### Outils de pratique

- **[LeetCode - Binary Search](https://leetcode.com/tag/binary-search/)** : Problèmes de recherche binaire
- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez l'exécution pas à pas

### Livres recommandés

- 📚 **"Introduction to Algorithms"** de Cormen et al. - Chapitre sur les algorithmes de recherche

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour vraiment maîtriser la recherche binaire, dessinez les étapes sur papier ! Prenez un tableau de 8-10 éléments, choisissez une cible, et tracez manuellement les valeurs de `low`, `high`, et `mid` à chaque itération. Cette visualisation vous aidera à comprendre intuitivement pourquoi l'algorithme fonctionne.

---

**Prêt pour la Leçon 21 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir la puissance de la récursion !

---

<div align="center">

**Leçon 20 sur 42 - Module 4 : Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Leçon 19 : Recherche Linéaire : Trouver un Élément Simplement en JavaScript](./lecon-1-recherche-lineaire-trouver-element-simplement-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 21 : Introduction à la Récursion : Cas de Base et Appels Récursifs ➡️](./lecon-3-introduction-recursion-cas-base-appels-recursifs.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
