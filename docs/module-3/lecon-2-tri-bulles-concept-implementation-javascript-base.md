##### Leçon 14 sur 42

# Tri à Bulles : Concept et Implémentation JavaScript de Base

**Module 3** : Techniques de Tri Essentielles

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **concept fondamental** du tri à bulles et sa métaphore des bulles qui remontent
- **Visualiser** le fonctionnement pas à pas de l'algorithme
- **Implémenter** le tri à bulles de base en JavaScript
- **Optimiser** l'implémentation avec le drapeau d'échange (swapped flag)
- **Analyser** la complexité temporelle et spatiale de l'algorithme
- Identifier les **cas d'utilisation** appropriés pour cet algorithme

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 13 complétée** : Comprendre les concepts fondamentaux du tri et les critères d'évaluation
- **Module 1** : Maîtriser la notation Big O et l'analyse de complexité
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Les Bulles qui Remontent

Imaginez un aquarium rempli de bulles d'air de différentes tailles. Naturellement, les plus grosses bulles remontent plus rapidement vers la surface tandis que les plus petites restent en bas. C'est exactement cette métaphore qui donne son nom au **tri à bulles** (Bubble Sort).

Le tri à bulles est l'un des algorithmes de tri les plus simples et les plus intuitifs à comprendre. Il fonctionne en **parcourant répétitivement** la liste, en **comparant les éléments adjacents** et en les **échangeant** s'ils sont dans le mauvais ordre. Ce processus continue jusqu'à ce que la liste soit entièrement triée.

Pourquoi étudier cet algorithme alors qu'il n'est pas le plus efficace ?

- C'est un excellent **outil pédagogique** pour comprendre les mécanismes de tri
- Il illustre parfaitement les concepts de **comparaison** et d'**échange**
- Il introduit l'idée d'**optimisation** d'algorithme avec le drapeau d'échange
- Il peut être efficace sur de **petits ensembles de données** ou des listes **presque triées**

> **Point Clé**
>
> Le tri à bulles tire son nom de la façon dont les éléments "remontent" progressivement vers leur position finale, comme des bulles d'air dans l'eau. À chaque passage, le plus grand élément non trié "flotte" vers sa position correcte à la fin du tableau.

---

## 📦 Le Concept du Tri à Bulles

Le tri à bulles est un algorithme de tri basé sur la **comparaison** qui parcourt la liste de manière répétitive, compare les éléments adjacents, et les échange s'ils sont dans le mauvais ordre. Ce processus est répété jusqu'à ce que plus aucun échange ne soit nécessaire, indiquant que la liste est triée.

---

### Mécanisme de Base

**Comment ça fonctionne :**

1. **Comparer** chaque paire d'éléments adjacents
2. **Échanger** si le premier élément est plus grand que le second (pour un tri ascendant)
3. **Répéter** le parcours jusqu'à ce qu'aucun échange ne soit nécessaire

**Caractéristiques clés :**

- **Simple à comprendre** et à implémenter
- **Tri en place** : ne nécessite pas de mémoire supplémentaire
- **Stable** : préserve l'ordre relatif des éléments égaux
- **Inefficace** pour les grands ensembles de données (O(n²))

---

### Visualisation Complète

Prenons un exemple concret pour visualiser le tri à bulles. Considérons le tableau suivant et trions-le en ordre croissant :

```javascript
const tableau = [64, 34, 25, 12, 22, 11, 90];
```

**État initial :**

```
[64, 34, 25, 12, 22, 11, 90]
 ^   ^
```

---

#### Première Passe

| Étape | Comparaison | Action              | Résultat                         |
| ----- | ----------- | ------------------- | -------------------------------- |
| 1     | 64 > 34 ?   | Oui → Échanger      | [**34, 64**, 25, 12, 22, 11, 90] |
| 2     | 64 > 25 ?   | Oui → Échanger      | [34, **25, 64**, 12, 22, 11, 90] |
| 3     | 64 > 12 ?   | Oui → Échanger      | [34, 25, **12, 64**, 22, 11, 90] |
| 4     | 64 > 22 ?   | Oui → Échanger      | [34, 25, 12, **22, 64**, 11, 90] |
| 5     | 64 > 11 ?   | Oui → Échanger      | [34, 25, 12, 22, **11, 64**, 90] |
| 6     | 64 > 90 ?   | Non → Pas d'échange | [34, 25, 12, 22, 11, **64, 90**] |

**Après la première passe :** `[34, 25, 12, 22, 11, 64, 90]`

> **Observation** : Le plus grand élément (90) est maintenant à sa position finale. C'est la "bulle" qui a remonté jusqu'en haut !

---

#### Deuxième Passe

| Étape | Comparaison | Action              | Résultat                         |
| ----- | ----------- | ------------------- | -------------------------------- |
| 1     | 34 > 25 ?   | Oui → Échanger      | [**25, 34**, 12, 22, 11, 64, 90] |
| 2     | 34 > 12 ?   | Oui → Échanger      | [25, **12, 34**, 22, 11, 64, 90] |
| 3     | 34 > 22 ?   | Oui → Échanger      | [25, 12, **22, 34**, 11, 64, 90] |
| 4     | 34 > 11 ?   | Oui → Échanger      | [25, 12, 22, **11, 34**, 64, 90] |
| 5     | 34 > 64 ?   | Non → Pas d'échange | [25, 12, 22, 11, **34, 64**, 90] |

**Après la deuxième passe :** `[25, 12, 22, 11, 34, 64, 90]`

> **Observation** : Maintenant 64 et 90 sont à leurs positions finales. On peut ignorer ces positions dans les passes suivantes !

---

#### Troisième Passe

| Étape | Comparaison | Action              | Résultat                         |
| ----- | ----------- | ------------------- | -------------------------------- |
| 1     | 25 > 12 ?   | Oui → Échanger      | [**12, 25**, 22, 11, 34, 64, 90] |
| 2     | 25 > 22 ?   | Oui → Échanger      | [12, **22, 25**, 11, 34, 64, 90] |
| 3     | 25 > 11 ?   | Oui → Échanger      | [12, 22, **11, 25**, 34, 64, 90] |
| 4     | 25 > 34 ?   | Non → Pas d'échange | [12, 22, 11, **25, 34**, 64, 90] |

**Après la troisième passe :** `[12, 22, 11, 25, 34, 64, 90]`

---

#### Quatrième Passe

| Étape | Comparaison | Action              | Résultat                         |
| ----- | ----------- | ------------------- | -------------------------------- |
| 1     | 12 > 22 ?   | Non → Pas d'échange | [**12, 22**, 11, 25, 34, 64, 90] |
| 2     | 22 > 11 ?   | Oui → Échanger      | [12, **11, 22**, 25, 34, 64, 90] |
| 3     | 22 > 25 ?   | Non → Pas d'échange | [12, 11, **22, 25**, 34, 64, 90] |

**Après la quatrième passe :** `[12, 11, 22, 25, 34, 64, 90]`

---

#### Cinquième Passe

| Étape | Comparaison | Action              | Résultat                         |
| ----- | ----------- | ------------------- | -------------------------------- |
| 1     | 12 > 11 ?   | Oui → Échanger      | [**11, 12**, 22, 25, 34, 64, 90] |
| 2     | 12 > 22 ?   | Non → Pas d'échange | [11, **12, 22**, 25, 34, 64, 90] |

**Après la cinquième passe :** `[11, 12, 22, 25, 34, 64, 90]`

---

#### Sixième Passe (Vérification)

| Étape | Comparaison | Action              | Résultat                         |
| ----- | ----------- | ------------------- | -------------------------------- |
| 1     | 11 > 12 ?   | Non → Pas d'échange | [**11, 12**, 22, 25, 34, 64, 90] |

**Aucun échange effectué** → Le tableau est trié !

**Résultat final :** `[11, 12, 22, 25, 34, 64, 90]`

---

## 📝 Micro-Exercice #1 : Tracer une Passe

**Objectif :** Comprendre le mécanisme de comparaison et d'échange.

**Instructions :** Effectuez manuellement la **première passe** du tri à bulles sur le tableau suivant. Notez chaque comparaison et échange.

```javascript
const scores = [45, 23, 78, 12, 56];
```

<details>
<summary>💡 Voir la solution</summary>

**Première passe sur `[45, 23, 78, 12, 56]` :**

| Étape | Comparaison | Action              | Résultat                 |
| ----- | ----------- | ------------------- | ------------------------ |
| 1     | 45 > 23 ?   | Oui → Échanger      | [**23, 45**, 78, 12, 56] |
| 2     | 45 > 78 ?   | Non → Pas d'échange | [23, **45, 78**, 12, 56] |
| 3     | 78 > 12 ?   | Oui → Échanger      | [23, 45, **12, 78**, 56] |
| 4     | 78 > 56 ?   | Oui → Échanger      | [23, 45, 12, **56, 78**] |

**Résultat après la première passe :** `[23, 45, 12, 56, 78]`

**Explication :**

- 4 comparaisons effectuées (n-1 pour un tableau de taille n)
- 3 échanges réalisés
- Le plus grand élément (78) est maintenant à sa position finale

</details>

---

## 💻 Implémentation de Base en JavaScript

Maintenant que nous comprenons le concept, implémentons le tri à bulles en JavaScript.

---

### Version Simple

```javascript
/**
 * Tri à bulles - Implémentation de base
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié (modifié en place)
 */
function triBulles(tableau) {
  const n = tableau.length;

  // Parcourir tous les éléments du tableau
  for (let i = 0; i < n - 1; i++) {
    // Les i derniers éléments sont déjà en place
    for (let j = 0; j < n - 1 - i; j++) {
      // Comparer les éléments adjacents
      if (tableau[j] > tableau[j + 1]) {
        // Échanger si l'élément actuel est plus grand que le suivant
        const temp = tableau[j];
        tableau[j] = tableau[j + 1];
        tableau[j + 1] = temp;
      }
    }
  }

  return tableau;
}

// Test
const nombres = [64, 34, 25, 12, 22, 11, 90];
console.log("Avant tri:", nombres);
triBulles(nombres);
console.log("Après tri:", nombres);
// Après tri: [11, 12, 22, 25, 34, 64, 90]
```

**Analyse du code :**

1. **Boucle externe (`i`)** : Contrôle le nombre de passes. Après chaque passe, un élément de plus est à sa position finale.

2. **Boucle interne (`j`)** : Parcourt le tableau pour comparer et échanger les éléments adjacents. On s'arrête à `n - 1 - i` car les `i` derniers éléments sont déjà triés.

3. **Échange** : Utilise une variable temporaire pour échanger deux éléments.

---

### Échange avec Déstructuration ES6

JavaScript moderne offre une syntaxe plus élégante pour l'échange :

```javascript
/**
 * Tri à bulles avec syntaxe ES6
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triBullesES6(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - 1 - i; j++) {
      if (tableau[j] > tableau[j + 1]) {
        // Échange avec déstructuration - plus élégant !
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
      }
    }
  }

  return tableau;
}

// Test
console.log(triBullesES6([5, 2, 8, 1, 9]));
// [1, 2, 5, 8, 9]
```

> **Astuce ES6**
>
> La déstructuration `[a, b] = [b, a]` permet d'échanger deux valeurs en une seule ligne, sans variable temporaire. C'est plus lisible et moins sujet aux erreurs.

---

## 📝 Micro-Exercice #2 : Implémenter le Tri Descendant

**Objectif :** Adapter l'algorithme pour trier en ordre décroissant.

**Instructions :** Modifiez la fonction `triBulles` pour trier le tableau en ordre descendant (du plus grand au plus petit).

```javascript
function triBullesDescendant(tableau) {
  // Votre implémentation ici
}

// Test attendu
console.log(triBullesDescendant([64, 34, 25, 12, 22, 11, 90]));
// [90, 64, 34, 25, 22, 12, 11]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri à bulles descendant (du plus grand au plus petit)
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié en ordre décroissant
 */
function triBullesDescendant(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - 1 - i; j++) {
      // Inverser la condition : échanger si l'élément est PLUS PETIT
      if (tableau[j] < tableau[j + 1]) {
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
      }
    }
  }

  return tableau;
}

// Tests
console.log(triBullesDescendant([64, 34, 25, 12, 22, 11, 90]));
// [90, 64, 34, 25, 22, 12, 11]

console.log(triBullesDescendant([5, 2, 8, 1, 9]));
// [9, 8, 5, 2, 1]
```

**Explication :**

La seule modification est d'inverser la condition de comparaison :

- **Ascendant** : `if (tableau[j] > tableau[j + 1])` - échanger si plus grand
- **Descendant** : `if (tableau[j] < tableau[j + 1])` - échanger si plus petit

Ainsi, les plus petits éléments "remontent" vers la fin au lieu des plus grands.

</details>

---

## ⚡ Optimisation : Le Drapeau d'Échange

L'implémentation de base effectue toujours le même nombre de passes, même si le tableau est déjà trié. Nous pouvons l'optimiser en détectant quand aucun échange n'a été effectué pendant une passe.

---

### Le Problème

```javascript
// Tableau déjà trié
const tableauTrie = [1, 2, 3, 4, 5];

// L'implémentation de base fera quand même 4 passes complètes !
// C'est du gaspillage de ressources.
```

---

### La Solution : Le Drapeau "swapped"

```javascript
/**
 * Tri à bulles optimisé avec détection d'arrêt précoce
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triBullesOptimise(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    // Drapeau pour suivre si un échange a été effectué
    let echangeEffectue = false;

    for (let j = 0; j < n - 1 - i; j++) {
      if (tableau[j] > tableau[j + 1]) {
        // Échanger les éléments
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
        // Marquer qu'un échange a eu lieu
        echangeEffectue = true;
      }
    }

    // Si aucun échange n'a été fait, le tableau est trié
    if (!echangeEffectue) {
      console.log(`Arrêt précoce après ${i + 1} passe(s)`);
      break;
    }
  }

  return tableau;
}

// Test avec tableau déjà trié
console.log("Test 1 - Tableau trié:");
triBullesOptimise([1, 2, 3, 4, 5]);
// Arrêt précoce après 1 passe(s)
// [1, 2, 3, 4, 5]

// Test avec tableau inversé
console.log("\nTest 2 - Tableau inversé:");
triBullesOptimise([5, 4, 3, 2, 1]);
// Pas d'arrêt précoce - toutes les passes nécessaires
// [1, 2, 3, 4, 5]

// Test avec tableau presque trié
console.log("\nTest 3 - Tableau presque trié:");
triBullesOptimise([1, 2, 4, 3, 5]);
// Arrêt précoce après 2 passe(s)
// [1, 2, 3, 4, 5]
```

**Avantages de l'optimisation :**

| Scénario             | Sans optimisation | Avec optimisation |
| -------------------- | ----------------- | ----------------- |
| Tableau trié         | n-1 passes        | 1 passe           |
| Tableau presque trié | n-1 passes        | ~2-3 passes       |
| Tableau inversé      | n-1 passes        | n-1 passes        |

> **Point Clé**
>
> L'optimisation avec le drapeau d'échange améliore le **meilleur cas** de O(n²) à O(n), rendant le tri à bulles efficace pour les tableaux déjà triés ou presque triés.

---

## 📝 Micro-Exercice #3 : Compter les Opérations

**Objectif :** Analyser le nombre d'opérations effectuées.

**Instructions :** Modifiez la fonction pour compter et afficher le nombre de comparaisons et d'échanges effectués.

```javascript
function triBullesAvecStats(tableau) {
  // Votre implémentation ici
  // Doit retourner un objet avec le tableau trié et les statistiques
}

// Test attendu
const resultat = triBullesAvecStats([64, 34, 25, 12, 22, 11, 90]);
// { tableau: [11, 12, 22, 25, 34, 64, 90], comparaisons: X, echanges: Y, passes: Z }
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri à bulles avec statistiques d'opérations
 * @param {number[]} tableau - Le tableau à trier
 * @returns {Object} - Tableau trié et statistiques
 */
function triBullesAvecStats(tableau) {
  const n = tableau.length;
  let comparaisons = 0;
  let echanges = 0;
  let passes = 0;

  for (let i = 0; i < n - 1; i++) {
    let echangeEffectue = false;
    passes++;

    for (let j = 0; j < n - 1 - i; j++) {
      comparaisons++; // Compter chaque comparaison

      if (tableau[j] > tableau[j + 1]) {
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
        echanges++; // Compter chaque échange
        echangeEffectue = true;
      }
    }

    if (!echangeEffectue) {
      break;
    }
  }

  return {
    tableau: tableau,
    comparaisons: comparaisons,
    echanges: echanges,
    passes: passes,
  };
}

// Tests
console.log("Tableau aléatoire:");
console.log(triBullesAvecStats([64, 34, 25, 12, 22, 11, 90]));
// { tableau: [11, 12, 22, 25, 34, 64, 90], comparaisons: 21, echanges: 16, passes: 6 }

console.log("\nTableau déjà trié:");
console.log(triBullesAvecStats([1, 2, 3, 4, 5]));
// { tableau: [1, 2, 3, 4, 5], comparaisons: 4, echanges: 0, passes: 1 }

console.log("\nTableau inversé:");
console.log(triBullesAvecStats([5, 4, 3, 2, 1]));
// { tableau: [1, 2, 3, 4, 5], comparaisons: 10, echanges: 10, passes: 4 }
```

**Explication :**

- **Comparaisons** : Toujours effectuées à chaque itération de la boucle interne
- **Échanges** : Seulement quand la condition est vraie
- **Passes** : Nombre de fois que la boucle externe s'exécute

Les statistiques montrent clairement l'impact de l'état initial du tableau sur les performances.

</details>

---

## 📊 Analyse de Complexité

Comprendre la complexité du tri à bulles est essentiel pour savoir quand l'utiliser (ou l'éviter).

---

### Complexité Temporelle

| Cas              | Complexité | Description                           |
| ---------------- | ---------- | ------------------------------------- |
| **Meilleur cas** | O(n)       | Tableau déjà trié (avec optimisation) |
| **Cas moyen**    | O(n²)      | Éléments dans un ordre aléatoire      |
| **Pire cas**     | O(n²)      | Tableau trié en ordre inverse         |

**Pourquoi O(n²) ?**

```javascript
// Pour un tableau de n éléments :
// - Passe 1 : n-1 comparaisons
// - Passe 2 : n-2 comparaisons
// - Passe 3 : n-3 comparaisons
// - ...
// - Passe n-1 : 1 comparaison

// Total = (n-1) + (n-2) + ... + 2 + 1
//       = n(n-1)/2
//       = (n² - n)/2
//       ≈ O(n²)
```

---

### Complexité Spatiale

| Aspect            | Complexité |
| ----------------- | ---------- |
| Espace auxiliaire | O(1)       |

Le tri à bulles est un algorithme **en place** : il ne nécessite qu'une quantité constante de mémoire supplémentaire (quelques variables pour l'échange et les indices).

---

### Comparaison avec d'Autres Algorithmes

| Algorithme        | Temps (moyen) | Espace   | Stable |
| ----------------- | ------------- | -------- | ------ |
| Tri à bulles      | O(n²)         | O(1)     | Oui    |
| Tri par insertion | O(n²)         | O(1)     | Oui    |
| Tri par sélection | O(n²)         | O(1)     | Non    |
| Tri fusion        | O(n log n)    | O(n)     | Oui    |
| Tri rapide        | O(n log n)    | O(log n) | Non    |

---

## 💻 Application Pratique : Tri d'Objets

Le tri à bulles peut être adapté pour trier des objets selon différents critères.

---

### Exemple 1 : Trier des Étudiants par Note

```javascript
/**
 * Tri à bulles générique avec fonction de comparaison
 * @param {Array} tableau - Le tableau à trier
 * @param {Function} comparateur - Fonction de comparaison
 * @returns {Array} - Le tableau trié
 */
function triBullesGenerique(tableau, comparateur) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    let echangeEffectue = false;

    for (let j = 0; j < n - 1 - i; j++) {
      // Utiliser la fonction de comparaison personnalisée
      if (comparateur(tableau[j], tableau[j + 1]) > 0) {
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
        echangeEffectue = true;
      }
    }

    if (!echangeEffectue) break;
  }

  return tableau;
}

// Données de test
const etudiants = [
  { nom: "Chermann", note: 85 },
  { nom: "Prudence", note: 92 },
  { nom: "Germain", note: 78 },
  { nom: "Sarr", note: 92 },
  { nom: "Ingrid", note: 88 },
];

// Tri par note croissante
const parNoteAsc = triBullesGenerique(
  [...etudiants],
  (a, b) => a.note - b.note,
);
console.log("Par note (croissant):");
console.log(parNoteAsc.map((e) => `${e.nom}: ${e.note}`));
// ['Germain: 78', 'Chermann: 85', 'Ingrid: 88', 'Prudence: 92', 'Sarr: 92']

// Tri par note décroissante
const parNoteDesc = triBullesGenerique(
  [...etudiants],
  (a, b) => b.note - a.note,
);
console.log("\nPar note (décroissant):");
console.log(parNoteDesc.map((e) => `${e.nom}: ${e.note}`));
// ['Prudence: 92', 'Sarr: 92', 'Ingrid: 88', 'Chermann: 85', 'Germain: 78']

// Tri alphabétique par nom
const parNom = triBullesGenerique([...etudiants], (a, b) =>
  a.nom.localeCompare(b.nom),
);
console.log("\nPar nom (alphabétique):");
console.log(parNom.map((e) => e.nom));
// ['Chermann', 'Germain', 'Ingrid', 'Prudence', 'Sarr']
```

---

### Exemple 2 : Tri Multi-Critères (Stabilité)

Grâce à sa stabilité, le tri à bulles préserve l'ordre relatif des éléments égaux :

```javascript
const employes = [
  { nom: "Chermann", dept: "RH", salaire: 70000 },
  { nom: "Prudence", dept: "Engineering", salaire: 80000 },
  { nom: "Germain", dept: "Engineering", salaire: 80000 },
  { nom: "Ingrid", dept: "RH", salaire: 75000 },
];

// Premier tri : par département
triBullesGenerique(employes, (a, b) => a.dept.localeCompare(b.dept));
console.log("Après tri par département:");
console.log(employes.map((e) => `${e.nom} (${e.dept})`));
// Engineering: Prudence, Germain | RH: Chermann, Ingrid

// Second tri : par salaire (le tri stable préserve l'ordre des départements pour salaires égaux)
triBullesGenerique(employes, (a, b) => a.salaire - b.salaire);
console.log("\nAprès tri par salaire (stable):");
console.log(employes.map((e) => `${e.nom}: ${e.salaire}€ (${e.dept})`));
// Chermann: 70000€ (RH)
// Ingrid: 75000€ (RH)
// Prudence: 80000€ (Engineering) <- Prudence reste avant Germain
// Germain: 80000€ (Engineering)
```

**Analyse :** Prudence et Germain ont le même salaire. Grâce à la stabilité du tri à bulles, leur ordre après le tri par département est préservé.

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension du tri à bulles, implémentez les problèmes suivants.

---

### Exercice 1 : Tri de Chaînes de Caractères

**Objectif :** Adapter le tri à bulles pour les chaînes.

**Instructions :** Triez une liste de noms alphabétiquement.

```javascript
const noms = ["Destinée", "Sing", "Chermann", "Prudence", "Germain"];

// Votre solution ici
// Résultat attendu: ['Chermann', 'Destinée', 'Germain', 'Prudence', 'Sing']
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri à bulles pour chaînes de caractères
 * @param {string[]} tableau - Le tableau de chaînes à trier
 * @returns {string[]} - Le tableau trié alphabétiquement
 */
function triBullesChaines(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    let echangeEffectue = false;

    for (let j = 0; j < n - 1 - i; j++) {
      // Utiliser localeCompare pour une comparaison correcte
      if (tableau[j].localeCompare(tableau[j + 1]) > 0) {
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
        echangeEffectue = true;
      }
    }

    if (!echangeEffectue) break;
  }

  return tableau;
}

// Test
const noms = ["Destinée", "Sing", "Chermann", "Prudence", "Germain"];
console.log(triBullesChaines(noms));
// ['Chermann', 'Destinée', 'Germain', 'Prudence', 'Sing']
```

**Explication :**

- On utilise `localeCompare()` au lieu de `>` pour comparer les chaînes
- `localeCompare()` gère correctement les accents et caractères spéciaux
- Le reste de l'algorithme reste identique

</details>

---

### Exercice 2 : Visualisation Pas à Pas

**Objectif :** Créer une fonction qui affiche chaque étape du tri.

**Instructions :** Implémentez une version du tri à bulles qui affiche l'état du tableau après chaque échange.

```javascript
function triBullesVisuel(tableau) {
  // Votre implémentation ici
  // Doit afficher chaque étape
}

// Test
triBullesVisuel([4, 2, 5, 1]);
// Devrait afficher quelque chose comme :
// État initial: [4, 2, 5, 1]
// Échange 4 ↔ 2: [2, 4, 5, 1]
// Échange 5 ↔ 1: [2, 4, 1, 5]
// ...
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri à bulles avec visualisation détaillée
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triBullesVisuel(tableau) {
  const n = tableau.length;

  console.log(`État initial: [${tableau.join(", ")}]`);
  console.log("---");

  for (let i = 0; i < n - 1; i++) {
    console.log(`Passe ${i + 1}:`);
    let echangeEffectue = false;

    for (let j = 0; j < n - 1 - i; j++) {
      const comparison = `Comparer ${tableau[j]} et ${tableau[j + 1]}`;

      if (tableau[j] > tableau[j + 1]) {
        console.log(`  ${comparison} → Échanger`);
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
        console.log(`  Résultat: [${tableau.join(", ")}]`);
        echangeEffectue = true;
      } else {
        console.log(`  ${comparison} → OK`);
      }
    }

    if (!echangeEffectue) {
      console.log("  Aucun échange - Tableau trié !");
      break;
    }
    console.log("---");
  }

  console.log(`\nRésultat final: [${tableau.join(", ")}]`);
  return tableau;
}

// Test
triBullesVisuel([4, 2, 5, 1]);
```

**Sortie attendue :**

```
État initial: [4, 2, 5, 1]
---
Passe 1:
  Comparer 4 et 2 → Échanger
  Résultat: [2, 4, 5, 1]
  Comparer 4 et 5 → OK
  Comparer 5 et 1 → Échanger
  Résultat: [2, 4, 1, 5]
---
Passe 2:
  Comparer 2 et 4 → OK
  Comparer 4 et 1 → Échanger
  Résultat: [2, 1, 4, 5]
---
Passe 3:
  Comparer 2 et 1 → Échanger
  Résultat: [1, 2, 4, 5]
---
Passe 4:
  Aucun échange - Tableau trié !

Résultat final: [1, 2, 4, 5]
```

</details>

---

### Exercice 3 : Tri de Produits par Prix

**Objectif :** Appliquer le tri à un cas réel d'e-commerce.

**Instructions :** Triez une liste de produits par prix croissant, puis par prix décroissant.

```javascript
const produits = [
  { nom: "Laptop", prix: 999 },
  { nom: "Souris", prix: 29 },
  { nom: "Clavier", prix: 79 },
  { nom: "Écran", prix: 299 },
  { nom: "Webcam", prix: 89 },
];

// Votre solution ici
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri à bulles pour objets avec critère personnalisé
 * @param {Array} tableau - Le tableau d'objets à trier
 * @param {string} propriete - La propriété sur laquelle trier
 * @param {boolean} descendant - true pour tri décroissant
 * @returns {Array} - Le tableau trié
 */
function trierProduitsParPrix(tableau, descendant = false) {
  // Créer une copie pour ne pas modifier l'original
  const copie = [...tableau];
  const n = copie.length;

  for (let i = 0; i < n - 1; i++) {
    let echangeEffectue = false;

    for (let j = 0; j < n - 1 - i; j++) {
      const condition = descendant
        ? copie[j].prix < copie[j + 1].prix
        : copie[j].prix > copie[j + 1].prix;

      if (condition) {
        [copie[j], copie[j + 1]] = [copie[j + 1], copie[j]];
        echangeEffectue = true;
      }
    }

    if (!echangeEffectue) break;
  }

  return copie;
}

// Données de test
const produits = [
  { nom: "Laptop", prix: 999 },
  { nom: "Souris", prix: 29 },
  { nom: "Clavier", prix: 79 },
  { nom: "Écran", prix: 299 },
  { nom: "Webcam", prix: 89 },
];

// Tri par prix croissant
const prixAsc = trierProduitsParPrix(produits, false);
console.log("Prix croissant:");
prixAsc.forEach((p) => console.log(`  ${p.nom}: ${p.prix}€`));
// Souris: 29€
// Clavier: 79€
// Webcam: 89€
// Écran: 299€
// Laptop: 999€

// Tri par prix décroissant
const prixDesc = trierProduitsParPrix(produits, true);
console.log("\nPrix décroissant:");
prixDesc.forEach((p) => console.log(`  ${p.nom}: ${p.prix}€`));
// Laptop: 999€
// Écran: 299€
// Webcam: 89€
// Clavier: 79€
// Souris: 29€
```

</details>

---

### Exercice 4 : Détection de Tableau Presque Trié

**Objectif :** Utiliser les statistiques pour analyser un tableau.

**Instructions :** Créez une fonction qui détermine si un tableau est "presque trié" (moins de 10% d'échanges par rapport au pire cas).

```javascript
function estPresqueTrie(tableau) {
  // Votre implémentation ici
  // Retourner true si moins de 10% d'échanges nécessaires
}

// Tests
console.log(estPresqueTrie([1, 2, 3, 4, 5])); // true (0 échanges)
console.log(estPresqueTrie([1, 2, 4, 3, 5])); // true (1 échange)
console.log(estPresqueTrie([5, 4, 3, 2, 1])); // false (10 échanges - pire cas)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Détermine si un tableau est "presque trié"
 * @param {number[]} tableau - Le tableau à analyser
 * @returns {Object} - Résultat de l'analyse
 */
function estPresqueTrie(tableau) {
  const copie = [...tableau]; // Ne pas modifier l'original
  const n = copie.length;

  // Calculer le pire cas : n(n-1)/2 échanges
  const pireCas = (n * (n - 1)) / 2;
  let echanges = 0;

  // Compter les échanges nécessaires
  for (let i = 0; i < n - 1; i++) {
    let echangeEffectue = false;

    for (let j = 0; j < n - 1 - i; j++) {
      if (copie[j] > copie[j + 1]) {
        [copie[j], copie[j + 1]] = [copie[j + 1], copie[j]];
        echanges++;
        echangeEffectue = true;
      }
    }

    if (!echangeEffectue) break;
  }

  const pourcentage = (echanges / pireCas) * 100;
  const presqueTrie = pourcentage < 10;

  return {
    presqueTrie: presqueTrie,
    echanges: echanges,
    pireCas: pireCas,
    pourcentage: pourcentage.toFixed(2) + "%",
  };
}

// Tests
console.log("Tableau trié:", estPresqueTrie([1, 2, 3, 4, 5]));
// { presqueTrie: true, echanges: 0, pireCas: 10, pourcentage: '0.00%' }

console.log("Presque trié:", estPresqueTrie([1, 2, 4, 3, 5]));
// { presqueTrie: true, echanges: 1, pireCas: 10, pourcentage: '10.00%' }

console.log("Inversé:", estPresqueTrie([5, 4, 3, 2, 1]));
// { presqueTrie: false, echanges: 10, pireCas: 10, pourcentage: '100.00%' }

console.log("Mélangé:", estPresqueTrie([3, 1, 4, 5, 2]));
// { presqueTrie: false, echanges: 5, pireCas: 10, pourcentage: '50.00%' }
```

**Explication :**

- Le pire cas pour n éléments est n(n-1)/2 échanges (tableau complètement inversé)
- On compte les échanges réels effectués
- Si les échanges représentent moins de 10% du pire cas, le tableau est considéré "presque trié"

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**D'où vient le nom "tri à bulles" ?**

- [ ] A. L'algorithme a été inventé dans une bulle de savon
- [ ] B. Les éléments "remontent" vers leur position comme des bulles d'air
- [ ] C. Le code ressemble à des bulles
- [ ] D. L'algorithme utilise une structure de données appelée "bulle"

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le nom vient de la façon dont les éléments les plus grands "remontent" progressivement vers la fin du tableau à chaque passe, comme des bulles d'air qui remontent à la surface de l'eau.

</details>

---

### Question 2

**Quelle est la complexité temporelle du tri à bulles dans le pire cas ?**

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n²)
- [ ] D. O(2ⁿ)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Dans le pire cas (tableau inversé), le tri à bulles effectue n(n-1)/2 comparaisons et échanges, ce qui donne une complexité de O(n²).

</details>

---

### Question 3

**Quel est l'avantage de l'optimisation avec le drapeau "swapped" ?**

- [ ] A. Réduit la complexité spatiale
- [ ] B. Permet un arrêt précoce si le tableau est déjà trié
- [ ] C. Rend l'algorithme instable
- [ ] D. Augmente le nombre de comparaisons

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le drapeau "swapped" permet de détecter quand aucun échange n'a été effectué pendant une passe, indiquant que le tableau est trié. Cela améliore le meilleur cas de O(n²) à O(n).

</details>

---

### Question 4

**Le tri à bulles est-il un algorithme stable ?**

- [ ] A. Non, il ne préserve pas l'ordre des éléments égaux
- [ ] B. Oui, car il n'échange que les éléments strictement supérieurs
- [ ] C. Ça dépend de l'implémentation
- [ ] D. La stabilité n'est pas applicable au tri à bulles

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri à bulles est stable car il n'échange deux éléments que si le premier est strictement supérieur au second. Les éléments égaux ne sont jamais échangés, préservant leur ordre relatif original.

</details>

---

### Question 5

**Après une passe complète du tri à bulles (ascendant), que pouvons-nous garantir ?**

- [ ] A. Le plus petit élément est à sa position finale
- [ ] B. Le plus grand élément est à sa position finale
- [ ] C. La moitié du tableau est triée
- [ ] D. Tous les éléments sont triés

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Après chaque passe, le plus grand élément non encore trié "remonte" jusqu'à sa position finale à la fin de la portion non triée du tableau.

</details>

---

### Question 6

**Quelle est la complexité spatiale du tri à bulles ?**

- [ ] A. O(n)
- [ ] B. O(n²)
- [ ] C. O(log n)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Le tri à bulles est un algorithme en place qui n'utilise qu'une quantité constante de mémoire supplémentaire (quelques variables pour les indices et l'échange), d'où O(1).

</details>

---

### Question 7

**Quand le tri à bulles peut-il être un bon choix ? (Plusieurs réponses possibles)**

- [ ] A. Pour de très petits tableaux (< 10 éléments)
- [ ] B. Pour des tableaux presque triés
- [ ] C. Pour trier des millions d'éléments
- [ ] D. Pour des fins pédagogiques

<details>
<summary>Voir la réponse</summary>

**Réponses : A, B, D**

Le tri à bulles est approprié pour :

- **A** : Les petits tableaux où la simplicité prime sur l'efficacité
- **B** : Les tableaux presque triés (avec optimisation, O(n) dans le meilleur cas)
- **D** : L'apprentissage des concepts de tri

Il n'est PAS adapté pour **C** (grands ensembles) car sa complexité O(n²) le rend très lent.

</details>

---

## 📌 Récapitulatif en 6 Points Clés

### 1. Concept Fondamental

Le tri à bulles compare et échange les éléments adjacents de manière répétitive, faisant "remonter" les plus grands éléments vers leur position finale.

### 2. Mécanisme Simple

À chaque passe, on parcourt le tableau en comparant les paires adjacentes et en les échangeant si nécessaire. Après k passes, les k plus grands éléments sont en place.

### 3. Optimisation avec Drapeau

Le drapeau "swapped" permet un arrêt précoce si aucun échange n'est effectué, améliorant le meilleur cas de O(n²) à O(n).

### 4. Complexité

- **Temps** : O(n²) en moyenne et pire cas, O(n) au meilleur cas (avec optimisation)
- **Espace** : O(1) - tri en place

### 5. Stabilité

Le tri à bulles est stable : il préserve l'ordre relatif des éléments égaux, ce qui est utile pour les tris multi-critères.

### 6. Cas d'Utilisation

Idéal pour l'apprentissage, les petits tableaux, ou les données presque triées. À éviter pour les grands ensembles de données.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maîtrisé le tri à bulles, votre premier algorithme de tri complet.

### Ce que vous avez appris aujourd'hui

- Le concept du tri à bulles et sa métaphore des bulles
- Comment visualiser et tracer l'exécution de l'algorithme
- L'implémentation de base et optimisée en JavaScript
- L'analyse de complexité et les cas d'utilisation appropriés

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter le tri à bulles pour des nombres et des objets
- Optimiser l'algorithme avec la détection d'arrêt précoce
- Adapter l'algorithme pour différents critères de tri

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Bien que le tri à bulles ne soit pas l'algorithme le plus efficace, le comprendre parfaitement vous donne une base solide pour aborder des algorithmes plus complexes. Les concepts de comparaison, d'échange et d'optimisation que vous avez appris s'appliquent à tous les algorithmes de tri.

---

## ➡️ Prochaine Étape : Leçon 15

### Ce qui vous attend

La prochaine leçon, **« Tri par Sélection (Selection Sort) »**, vous présentera un algorithme avec une approche différente.

**Vous découvrirez :**

- Comment sélectionner le minimum à chaque passe
- Une logique différente du tri à bulles
- Comparaison avec le tri à bulles en termes de performances
- Quand préférer un algorithme à l'autre

### Préparez-vous !

Le tri par sélection offre une perspective différente sur le problème du tri. Contrairement au tri à bulles qui fait "remonter" les grands éléments, il "place" directement chaque élément à sa position finale.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Bubble Sort](https://visualgo.net/en/sorting) - Visualisation interactive
- [GeeksforGeeks - Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/) - Tutoriel détaillé
- [Sorting Algorithms Visualized](https://www.toptal.com/developers/sorting-algorithms/bubble-sort) - Comparaison visuelle

### Outils de pratique

- **[JS Bin](https://jsbin.com/)** : Testez vos implémentations en ligne
- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez l'exécution pas à pas

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour bien assimiler le tri à bulles, prenez 5 cartes numérotées et triez-les manuellement en appliquant l'algorithme. Comptez le nombre de comparaisons et d'échanges. Puis mélangez différemment et recommencez. Vous verrez concrètement l'impact de l'état initial sur les performances !

---

**Prêt pour la Leçon 15 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir le tri par sélection !

---

<div align="center">

**Leçon 14 sur 42 - Module 3 : Techniques de Tri Essentielles**

[⬅️ Leçon 13 : Introduction au Tri : Pourquoi Ordonner les Données ?](./lecon-1-introduction-tri-pourquoi-ordonner-donnees.md) | [Retour au sommaire](./README.md) | [Leçon 15 : Tri par Sélection : Concept et Implémentation JavaScript de Base ➡️](./lecon-3-tri-selection-concept-implementation-javascript-base.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
