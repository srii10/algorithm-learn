##### Leçon 15 sur 42

# Tri par Sélection : Concept et Implémentation JavaScript de Base

**Module 3** : Techniques de Tri Essentielles

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **concept fondamental** du tri par sélection et sa logique de "recherche du minimum"
- **Visualiser** le fonctionnement pas à pas de l'algorithme avec les sous-tableaux triés et non triés
- **Implémenter** le tri par sélection en JavaScript (ascendant et descendant)
- **Analyser** la complexité temporelle et spatiale de l'algorithme
- **Comparer** le tri par sélection avec le tri à bulles et identifier leurs différences clés
- Comprendre pourquoi le tri par sélection est **instable** et ses implications pratiques

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 13 complétée** : Comprendre les concepts fondamentaux du tri et la notion de stabilité
- **Leçon 14 complétée** : Maîtriser le tri à bulles pour pouvoir comparer les approches
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Choisir le Meilleur à Chaque Tour

Imaginez que vous êtes un entraîneur de basketball qui doit constituer son équipe de départ. Vous avez une file de joueurs devant vous, et à chaque tour, vous **sélectionnez le meilleur joueur restant** pour le placer dans votre équipe. C'est exactement cette stratégie de "sélection du meilleur" qui donne son nom au **tri par sélection** (Selection Sort).

Contrairement au tri à bulles qui fait "remonter" progressivement les éléments, le tri par sélection adopte une approche plus directe : à chaque passe, il **trouve l'élément minimum** dans la partie non triée et le **place directement** à sa position finale dans la partie triée.

Cette approche présente des caractéristiques intéressantes :

- L'algorithme effectue **très peu d'échanges** (au maximum n-1)
- Il maintient une **frontière claire** entre la partie triée et non triée
- Sa logique est **intuitive** et facile à comprendre
- Il est particulièrement utile quand les **opérations d'écriture sont coûteuses**

> **Point Clé**
>
> Le tri par sélection se distingue par son nombre minimal d'échanges : là où le tri à bulles peut effectuer jusqu'à n(n-1)/2 échanges dans le pire cas, le tri par sélection n'en fait jamais plus de n-1. Cette caractéristique le rend intéressant dans les contextes où l'écriture en mémoire est coûteuse.

---

## 📦 Le Concept du Tri par Sélection

Le tri par sélection est un algorithme de tri basé sur la **comparaison** qui fonctionne en maintenant deux sous-tableaux dans le tableau donné :

1. **Sous-tableau trié** : Les éléments déjà placés à leur position finale (au début du tableau)
2. **Sous-tableau non trié** : Les éléments restants à trier

À chaque passe, l'algorithme **sélectionne** l'élément minimum du sous-tableau non trié et l'échange avec le premier élément de ce sous-tableau, étendant ainsi le sous-tableau trié d'un élément.

---

### Mécanisme de Base

**Comment ça fonctionne :**

1. **Initialiser** le sous-tableau trié comme vide (index 0)
2. **Trouver** l'élément minimum dans le sous-tableau non trié
3. **Échanger** cet élément avec le premier élément du sous-tableau non trié
4. **Étendre** le sous-tableau trié d'un élément
5. **Répéter** jusqu'à ce que tous les éléments soient triés

**Caractéristiques clés :**

- **Simple à comprendre** et à implémenter
- **Tri en place** : ne nécessite pas de mémoire supplémentaire (O(1))
- **Nombre minimal d'échanges** : au maximum n-1 échanges
- **Instable** : peut changer l'ordre relatif des éléments égaux
- **Inefficace** pour les grands ensembles de données (O(n²))

---

### Visualisation Complète

Prenons un exemple concret pour visualiser le tri par sélection. Considérons le tableau suivant et trions-le en ordre croissant :

```javascript
const tableau = [64, 25, 12, 22, 11];
```

**État initial :**

```
[64, 25, 12, 22, 11]
 └── non trié ────┘
```

---

#### Première Passe

| Étape | Action                                        | Détails                           |
| ----- | --------------------------------------------- | --------------------------------- |
| 1     | Chercher le minimum dans [64, 25, 12, 22, 11] | Minimum trouvé : **11** (index 4) |
| 2     | Échanger avec le premier élément              | Échanger arr[0]=64 avec arr[4]=11 |
| 3     | Résultat                                      | [**11**, 25, 12, 22, 64]          |

**Après la première passe :**

```
[11, 25, 12, 22, 64]
 └─┘ └─ non trié ─┘
trié
```

> **Observation** : Le plus petit élément (11) est maintenant à sa position finale. La partie triée contient 1 élément.

---

#### Deuxième Passe

| Étape | Action                                    | Détails                           |
| ----- | ----------------------------------------- | --------------------------------- |
| 1     | Chercher le minimum dans [25, 12, 22, 64] | Minimum trouvé : **12** (index 2) |
| 2     | Échanger avec le premier élément non trié | Échanger arr[1]=25 avec arr[2]=12 |
| 3     | Résultat                                  | [11, **12**, 25, 22, 64]          |

**Après la deuxième passe :**

```
[11, 12, 25, 22, 64]
 └────┘ └ non trié ┘
 trié
```

---

#### Troisième Passe

| Étape | Action                                    | Détails                           |
| ----- | ----------------------------------------- | --------------------------------- |
| 1     | Chercher le minimum dans [25, 22, 64]     | Minimum trouvé : **22** (index 3) |
| 2     | Échanger avec le premier élément non trié | Échanger arr[2]=25 avec arr[3]=22 |
| 3     | Résultat                                  | [11, 12, **22**, 25, 64]          |

**Après la troisième passe :**

```
[11, 12, 22, 25, 64]
 └────────┘  └ non ┘
   trié       trié
```

---

#### Quatrième Passe

| Étape | Action                            | Détails                           |
| ----- | --------------------------------- | --------------------------------- |
| 1     | Chercher le minimum dans [25, 64] | Minimum trouvé : **25** (index 3) |
| 2     | L'élément est déjà à sa place     | Pas d'échange nécessaire          |
| 3     | Résultat                          | [11, 12, 22, **25**, 64]          |

**Après la quatrième passe :**

```
[11, 12, 22, 25, 64]
 └────────────┘  └┘
     trié      dernier
               élément
```

> **Observation** : Le dernier élément (64) est automatiquement à sa place correcte après n-1 passes.

**Résultat final :** `[11, 12, 22, 25, 64]`

---

## 📝 Micro-Exercice #1 : Tracer une Passe

**Objectif :** Comprendre le mécanisme de recherche du minimum et d'échange.

**Instructions :** Effectuez manuellement les **deux premières passes** du tri par sélection sur le tableau suivant. Notez l'index du minimum trouvé et l'échange effectué à chaque passe.

```javascript
const scores = [45, 23, 78, 12, 56];
```

<details>
<summary>💡 Voir la solution</summary>

**Première passe sur `[45, 23, 78, 12, 56]` :**

| Étape | Action              | Détails                               |
| ----- | ------------------- | ------------------------------------- |
| 1     | Chercher le minimum | Parcours : 45 → 23 → 78 → **12** → 56 |
| 2     | Minimum trouvé      | **12** à l'index 3                    |
| 3     | Échanger            | arr[0]=45 ↔ arr[3]=12                 |
| 4     | Résultat            | [**12**, 23, 78, 45, 56]              |

**Deuxième passe sur `[12, 23, 78, 45, 56]` :**

| Étape | Action                                    | Détails                          |
| ----- | ----------------------------------------- | -------------------------------- |
| 1     | Chercher le minimum dans [23, 78, 45, 56] | Parcours : **23** → 78 → 45 → 56 |
| 2     | Minimum trouvé                            | **23** à l'index 1               |
| 3     | L'élément est déjà à sa place             | Pas d'échange                    |
| 4     | Résultat                                  | [12, **23**, 78, 45, 56]         |

**Explication :**

- À la première passe, on parcourt tout le tableau pour trouver 12 (le plus petit), puis on l'échange avec 45
- À la deuxième passe, 23 est déjà le minimum de la partie non triée, donc aucun échange n'est nécessaire
- La partie triée grandit d'un élément à chaque passe : [12] → [12, 23]

</details>

---

## 💻 Implémentation de Base en JavaScript

Maintenant que nous comprenons le concept, implémentons le tri par sélection en JavaScript.

---

### Version Simple

```javascript
/**
 * Tri par sélection - Implémentation de base
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié (modifié en place)
 */
function triSelection(tableau) {
  const n = tableau.length;

  // Boucle externe : parcourir le tableau jusqu'à l'avant-dernier élément
  // Chaque itération place le plus petit élément restant à sa position correcte
  for (let i = 0; i < n - 1; i++) {
    // Supposer que l'élément actuel est le minimum
    let indexMin = i;

    // Boucle interne : trouver le vrai minimum dans la partie non triée
    for (let j = i + 1; j < n; j++) {
      // Si on trouve un élément plus petit, mettre à jour indexMin
      if (tableau[j] < tableau[indexMin]) {
        indexMin = j;
      }
    }

    // Échanger seulement si le minimum n'est pas déjà à la position i
    if (indexMin !== i) {
      const temp = tableau[i];
      tableau[i] = tableau[indexMin];
      tableau[indexMin] = temp;
    }
  }

  return tableau;
}

// Test
const nombres = [64, 25, 12, 22, 11];
console.log("Avant tri:", [...nombres]);
triSelection(nombres);
console.log("Après tri:", nombres);
// Après tri: [11, 12, 22, 25, 64]
```

**Analyse du code :**

1. **Boucle externe (`i`)** : Représente la frontière entre les parties triée et non triée. Après l'itération `i`, les éléments de 0 à `i` sont triés.

2. **Variable `indexMin`** : Stocke l'index du plus petit élément trouvé dans la partie non triée. Initialisée à `i` (on suppose que le premier élément non trié est le minimum).

3. **Boucle interne (`j`)** : Parcourt la partie non triée (de `i+1` à `n-1`) pour trouver le vrai minimum.

4. **Échange conditionnel** : On n'échange que si le minimum trouvé n'est pas déjà à la position `i`, évitant les échanges inutiles.

---

### Version avec Déstructuration ES6

```javascript
/**
 * Tri par sélection avec syntaxe ES6
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triSelectionES6(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      if (tableau[j] < tableau[indexMin]) {
        indexMin = j;
      }
    }

    // Échange avec déstructuration ES6
    if (indexMin !== i) {
      [tableau[i], tableau[indexMin]] = [tableau[indexMin], tableau[i]];
    }
  }

  return tableau;
}

// Test
console.log(triSelectionES6([5, 2, 8, 1, 9]));
// [1, 2, 5, 8, 9]
```

> **Astuce ES6**
>
> La déstructuration `[a, b] = [b, a]` permet d'échanger deux valeurs élégamment. Notez que l'échange conditionnel `if (indexMin !== i)` est une optimisation importante qui évite des opérations inutiles.

---

## 📝 Micro-Exercice #2 : Implémenter le Tri Descendant

**Objectif :** Adapter l'algorithme pour trier en ordre décroissant.

**Instructions :** Modifiez la fonction `triSelection` pour trier le tableau en ordre descendant (du plus grand au plus petit). Indice : au lieu de chercher le **minimum**, cherchez le **maximum**.

```javascript
function triSelectionDescendant(tableau) {
  // Votre implémentation ici
}

// Test attendu
console.log(triSelectionDescendant([64, 25, 12, 22, 11]));
// [64, 25, 22, 12, 11]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri par sélection descendant (du plus grand au plus petit)
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié en ordre décroissant
 */
function triSelectionDescendant(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    // Chercher l'index du MAXIMUM au lieu du minimum
    let indexMax = i;

    for (let j = i + 1; j < n; j++) {
      // Inverser la condition : chercher le plus grand
      if (tableau[j] > tableau[indexMax]) {
        indexMax = j;
      }
    }

    // Échanger si nécessaire
    if (indexMax !== i) {
      [tableau[i], tableau[indexMax]] = [tableau[indexMax], tableau[i]];
    }
  }

  return tableau;
}

// Tests
console.log(triSelectionDescendant([64, 25, 12, 22, 11]));
// [64, 25, 22, 12, 11]

console.log(triSelectionDescendant([5, 2, 8, 1, 9]));
// [9, 8, 5, 2, 1]
```

**Explication :**

Les modifications apportées :

- Renommer `indexMin` en `indexMax` pour la clarté
- Inverser la condition de comparaison : `tableau[j] > tableau[indexMax]` au lieu de `<`

Ainsi, à chaque passe, on sélectionne le **plus grand** élément restant et on le place au début de la partie non triée.

</details>

---

## 📊 Analyse de Complexité

Comprendre la complexité du tri par sélection est essentiel pour savoir quand l'utiliser.

---

### Complexité Temporelle

| Cas              | Complexité | Description                      |
| ---------------- | ---------- | -------------------------------- |
| **Meilleur cas** | O(n²)      | Tableau déjà trié                |
| **Cas moyen**    | O(n²)      | Éléments dans un ordre aléatoire |
| **Pire cas**     | O(n²)      | Tableau trié en ordre inverse    |

**Pourquoi O(n²) dans TOUS les cas ?**

```javascript
// Pour un tableau de n éléments :
// - Passe 1 : n-1 comparaisons pour trouver le minimum
// - Passe 2 : n-2 comparaisons
// - Passe 3 : n-3 comparaisons
// - ...
// - Passe n-1 : 1 comparaison

// Total = (n-1) + (n-2) + ... + 2 + 1
//       = n(n-1)/2
//       ≈ O(n²)
```

> **Note importante**
>
> Contrairement au tri à bulles optimisé qui peut atteindre O(n) dans le meilleur cas (tableau déjà trié), le tri par sélection effectue **toujours** le même nombre de comparaisons, quelle que soit l'organisation initiale des données. Il n'y a pas d'optimisation possible pour les tableaux déjà triés.

---

### Complexité Spatiale

| Aspect            | Complexité |
| ----------------- | ---------- |
| Espace auxiliaire | O(1)       |

Le tri par sélection est un algorithme **en place** : il ne nécessite qu'une quantité constante de mémoire supplémentaire (quelques variables pour l'index et l'échange).

---

### Nombre d'Échanges

| Cas     | Échanges              |
| ------- | --------------------- |
| Minimum | 0 (tableau déjà trié) |
| Maximum | n-1                   |

C'est l'un des **points forts** du tri par sélection : le nombre d'échanges est toujours linéaire (O(n)), contrairement au tri à bulles qui peut effectuer O(n²) échanges.

---

## 🔄 Comparaison avec le Tri à Bulles

| Critère          | Tri par Sélection         | Tri à Bulles                    |
| ---------------- | ------------------------- | ------------------------------- |
| **Comparaisons** | O(n²) - toujours n(n-1)/2 | O(n²) pire/moyen, O(n) meilleur |
| **Échanges**     | O(n) - au maximum n-1     | O(n²) pire/moyen, O(1) meilleur |
| **Meilleur cas** | O(n²)                     | O(n) avec optimisation          |
| **Stabilité**    | Instable                  | Stable                          |
| **Mémoire**      | O(1)                      | O(1)                            |

**Quand préférer le tri par sélection ?**

- Quand les **opérations d'écriture** (échanges) sont coûteuses (ex: écriture sur mémoire flash)
- Quand on a besoin d'un algorithme simple avec un **nombre prévisible d'échanges**
- Quand la **stabilité n'est pas importante**

**Quand préférer le tri à bulles ?**

- Quand les données sont **presque triées** (meilleur cas O(n))
- Quand la **stabilité est importante**
- Quand on veut pouvoir **détecter** si le tableau est déjà trié

---

## ⚠️ L'Instabilité du Tri par Sélection

Un point crucial à comprendre : le tri par sélection est **instable**. Cela signifie qu'il peut modifier l'ordre relatif des éléments ayant la même valeur.

---

### Exemple Illustratif

```javascript
const cartes = [
  { valeur: 5, couleur: "♥" }, // Position originale 0
  { valeur: 3, couleur: "♠" }, // Position originale 1
  { valeur: 5, couleur: "♦" }, // Position originale 2
  { valeur: 2, couleur: "♣" }, // Position originale 3
];
```

Si on trie par valeur avec le tri par sélection :

```
État initial : [5♥, 3♠, 5♦, 2♣]

Passe 1 : Minimum = 2♣ (index 3)
          Échanger avec index 0 : [2♣, 3♠, 5♦, 5♥]
          5♥ est maintenant APRÈS 5♦ !

Passe 2 : Minimum = 3♠ (index 1)
          Déjà en place

Passe 3 : Minimum = 5♦ (index 2)
          Déjà en place

Résultat final : [2♣, 3♠, 5♦, 5♥]
```

**Problème :** Dans le tableau original, `5♥` était **avant** `5♦`. Après le tri, `5♥` est **après** `5♦`. L'ordre relatif des deux 5 a été inversé. C'est pourquoi on dit que le tri par sélection est **instable**.

```javascript
// Démonstration en JavaScript
function triSelectionInstable(tableau, cle) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      if (tableau[j][cle] < tableau[indexMin][cle]) {
        indexMin = j;
      }
    }

    if (indexMin !== i) {
      [tableau[i], tableau[indexMin]] = [tableau[indexMin], tableau[i]];
    }
  }

  return tableau;
}

const cartes = [
  { valeur: 5, couleur: "♥", ordre: 1 },
  { valeur: 3, couleur: "♠", ordre: 2 },
  { valeur: 5, couleur: "♦", ordre: 3 },
  { valeur: 2, couleur: "♣", ordre: 4 },
];

console.log("Avant tri:");
cartes.forEach((c) =>
  console.log(`  ${c.valeur}${c.couleur} (ordre: ${c.ordre})`),
);

triSelectionInstable(cartes, "valeur");

console.log("\nAprès tri par valeur:");
cartes.forEach((c) =>
  console.log(`  ${c.valeur}${c.couleur} (ordre: ${c.ordre})`),
);
// Les deux 5 ont changé d'ordre relatif !
```

> **Point Clé**
>
> L'instabilité du tri par sélection vient du fait que l'échange place le minimum trouvé directement à sa position finale, "projetant" l'élément remplacé à une position arbitraire. Si cet élément a la même valeur qu'un autre, leur ordre relatif peut être perturbé.

---

## 📝 Micro-Exercice #3 : Compter les Opérations

**Objectif :** Analyser le nombre d'opérations effectuées.

**Instructions :** Modifiez la fonction pour compter et afficher le nombre de comparaisons et d'échanges effectués.

```javascript
function triSelectionAvecStats(tableau) {
  // Votre implémentation ici
  // Doit retourner un objet avec le tableau trié et les statistiques
}

// Test attendu
const resultat = triSelectionAvecStats([64, 25, 12, 22, 11]);
// { tableau: [11, 12, 22, 25, 64], comparaisons: 10, echanges: X }
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri par sélection avec statistiques d'opérations
 * @param {number[]} tableau - Le tableau à trier
 * @returns {Object} - Tableau trié et statistiques
 */
function triSelectionAvecStats(tableau) {
  const n = tableau.length;
  let comparaisons = 0;
  let echanges = 0;

  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      comparaisons++; // Compter chaque comparaison

      if (tableau[j] < tableau[indexMin]) {
        indexMin = j;
      }
    }

    if (indexMin !== i) {
      [tableau[i], tableau[indexMin]] = [tableau[indexMin], tableau[i]];
      echanges++; // Compter chaque échange
    }
  }

  return {
    tableau: tableau,
    comparaisons: comparaisons,
    echanges: echanges,
  };
}

// Tests
console.log("Tableau aléatoire:");
console.log(triSelectionAvecStats([64, 25, 12, 22, 11]));
// { tableau: [11, 12, 22, 25, 64], comparaisons: 10, echanges: 3 }

console.log("\nTableau déjà trié:");
console.log(triSelectionAvecStats([1, 2, 3, 4, 5]));
// { tableau: [1, 2, 3, 4, 5], comparaisons: 10, echanges: 0 }

console.log("\nTableau inversé:");
console.log(triSelectionAvecStats([5, 4, 3, 2, 1]));
// { tableau: [1, 2, 3, 4, 5], comparaisons: 10, echanges: 2 }
```

**Explication :**

- **Comparaisons** : Toujours n(n-1)/2 = 10 pour 5 éléments, quelle que soit l'organisation initiale
- **Échanges** : Variable selon l'état initial
  - Tableau trié : 0 échanges (les minimums sont déjà en place)
  - Tableau inversé : seulement 2 échanges (1↔5, puis 2↔4)
  - Tableau aléatoire : quelques échanges

Le nombre constant de comparaisons confirme que le tri par sélection est toujours O(n²).

</details>

---

## 💻 Application Pratique : Tri d'Objets

Le tri par sélection peut être adapté pour trier des objets selon différents critères.

---

### Exemple 1 : Trier des Produits par Prix

```javascript
/**
 * Tri par sélection générique avec fonction de comparaison
 * @param {Array} tableau - Le tableau à trier
 * @param {Function} comparateur - Fonction de comparaison (a, b) => boolean
 * @returns {Array} - Le tableau trié
 */
function triSelectionGenerique(tableau, comparateur) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      // Utiliser la fonction de comparaison personnalisée
      if (comparateur(tableau[j], tableau[indexMin])) {
        indexMin = j;
      }
    }

    if (indexMin !== i) {
      [tableau[i], tableau[indexMin]] = [tableau[indexMin], tableau[i]];
    }
  }

  return tableau;
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
const parPrixAsc = triSelectionGenerique(
  [...produits],
  (a, b) => a.prix < b.prix,
);
console.log("Par prix (croissant):");
parPrixAsc.forEach((p) => console.log(`  ${p.nom}: ${p.prix}€`));
// Souris: 29€, Clavier: 79€, Webcam: 89€, Écran: 299€, Laptop: 999€

// Tri par prix décroissant
const parPrixDesc = triSelectionGenerique(
  [...produits],
  (a, b) => a.prix > b.prix,
);
console.log("\nPar prix (décroissant):");
parPrixDesc.forEach((p) => console.log(`  ${p.nom}: ${p.prix}€`));
// Laptop: 999€, Écran: 299€, Webcam: 89€, Clavier: 79€, Souris: 29€
```

---

### Exemple 2 : Trier des Chaînes Alphabétiquement

```javascript
/**
 * Tri par sélection pour chaînes de caractères
 * @param {string[]} tableau - Le tableau de chaînes à trier
 * @returns {string[]} - Le tableau trié alphabétiquement
 */
function triSelectionChaines(tableau) {
  const n = tableau.length;

  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      // Utiliser localeCompare pour une comparaison correcte
      if (tableau[j].localeCompare(tableau[indexMin]) < 0) {
        indexMin = j;
      }
    }

    if (indexMin !== i) {
      [tableau[i], tableau[indexMin]] = [tableau[indexMin], tableau[i]];
    }
  }

  return tableau;
}

// Test
const prenoms = ["Destinée", "Sing", "Chermann", "Prudence", "Germain"];
console.log("Avant tri:", prenoms);
triSelectionChaines(prenoms);
console.log("Après tri:", prenoms);
// ['Chermann', 'Destinée', 'Germain', 'Prudence', 'Sing']
```

---

### Exemple 3 : Visualisation Pas à Pas

```javascript
/**
 * Tri par sélection avec visualisation détaillée
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triSelectionVisuel(tableau) {
  const n = tableau.length;

  console.log(`État initial: [${tableau.join(", ")}]`);
  console.log("─".repeat(50));

  for (let i = 0; i < n - 1; i++) {
    console.log(`\nPasse ${i + 1}:`);
    console.log(
      `  Partie triée: [${tableau.slice(0, i).join(", ") || "vide"}]`,
    );
    console.log(`  Partie non triée: [${tableau.slice(i).join(", ")}]`);

    let indexMin = i;

    // Recherche du minimum
    for (let j = i + 1; j < n; j++) {
      if (tableau[j] < tableau[indexMin]) {
        indexMin = j;
      }
    }

    console.log(`  Minimum trouvé: ${tableau[indexMin]} (index ${indexMin})`);

    if (indexMin !== i) {
      console.log(`  Échanger: ${tableau[i]} ↔ ${tableau[indexMin]}`);
      [tableau[i], tableau[indexMin]] = [tableau[indexMin], tableau[i]];
      console.log(`  Résultat: [${tableau.join(", ")}]`);
    } else {
      console.log(`  Déjà en place, pas d'échange`);
    }
  }

  console.log("─".repeat(50));
  console.log(`\nRésultat final: [${tableau.join(", ")}]`);
  return tableau;
}

// Test
triSelectionVisuel([64, 25, 12, 22, 11]);
```

**Sortie :**

```
État initial: [64, 25, 12, 22, 11]
──────────────────────────────────────────────────

Passe 1:
  Partie triée: [vide]
  Partie non triée: [64, 25, 12, 22, 11]
  Minimum trouvé: 11 (index 4)
  Échanger: 64 ↔ 11
  Résultat: [11, 25, 12, 22, 64]

Passe 2:
  Partie triée: [11]
  Partie non triée: [25, 12, 22, 64]
  Minimum trouvé: 12 (index 2)
  Échanger: 25 ↔ 12
  Résultat: [11, 12, 25, 22, 64]

Passe 3:
  Partie triée: [11, 12]
  Partie non triée: [25, 22, 64]
  Minimum trouvé: 22 (index 3)
  Échanger: 25 ↔ 22
  Résultat: [11, 12, 22, 25, 64]

Passe 4:
  Partie triée: [11, 12, 22]
  Partie non triée: [25, 64]
  Minimum trouvé: 25 (index 3)
  Déjà en place, pas d'échange
──────────────────────────────────────────────────

Résultat final: [11, 12, 22, 25, 64]
```

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension du tri par sélection, implémentez les problèmes suivants.

---

### Exercice 1 : Tracer l'Algorithme

**Objectif :** Comprendre l'exécution pas à pas.

**Instructions :** Tracez manuellement l'exécution du tri par sélection avec le tableau `[8, 3, 5, 1, 9, 2]`. Notez l'état du tableau après chaque passe.

```javascript
// Tableau initial : [8, 3, 5, 1, 9, 2]
// Après Passe 1 : ?
// Après Passe 2 : ?
// Après Passe 3 : ?
// Après Passe 4 : ?
// Après Passe 5 : ?
```

<details>
<summary>💡 Voir la solution</summary>

```
Tableau initial : [8, 3, 5, 1, 9, 2]

Passe 1 :
  - Chercher min dans [8, 3, 5, 1, 9, 2] → 1 (index 3)
  - Échanger 8 ↔ 1
  - Résultat : [1, 3, 5, 8, 9, 2]

Passe 2 :
  - Chercher min dans [3, 5, 8, 9, 2] → 2 (index 5)
  - Échanger 3 ↔ 2
  - Résultat : [1, 2, 5, 8, 9, 3]

Passe 3 :
  - Chercher min dans [5, 8, 9, 3] → 3 (index 5)
  - Échanger 5 ↔ 3
  - Résultat : [1, 2, 3, 8, 9, 5]

Passe 4 :
  - Chercher min dans [8, 9, 5] → 5 (index 5)
  - Échanger 8 ↔ 5
  - Résultat : [1, 2, 3, 5, 9, 8]

Passe 5 :
  - Chercher min dans [9, 8] → 8 (index 5)
  - Échanger 9 ↔ 8
  - Résultat : [1, 2, 3, 5, 8, 9]

Tableau final : [1, 2, 3, 5, 8, 9]
```

**Statistiques :**

- 5 passes (n-1 pour n=6)
- 15 comparaisons (5+4+3+2+1)
- 5 échanges

</details>

---

### Exercice 2 : Tri de Tâches par Priorité

**Objectif :** Appliquer le tri par sélection à l'étude de cas.

**Instructions :** Triez une liste de tâches par priorité (Haute avant Moyenne avant Basse).

```javascript
const taches = [
  { titre: "Réviser code", priorite: "Moyenne" },
  { titre: "Corriger bug", priorite: "Haute" },
  { titre: "Écrire tests", priorite: "Basse" },
  { titre: "Déployer", priorite: "Haute" },
  { titre: "Documentation", priorite: "Basse" },
];

function trierTachesParPriorite(taches) {
  // Votre implémentation ici
}

// Résultat attendu : Haute, Haute, Moyenne, Basse, Basse
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trie les tâches par priorité (Haute > Moyenne > Basse)
 * @param {Array} taches - Liste des tâches
 * @returns {Array} - Tâches triées par priorité
 */
function trierTachesParPriorite(taches) {
  // Définir l'ordre des priorités
  const ordrePriorite = { Haute: 1, Moyenne: 2, Basse: 3 };

  const n = taches.length;

  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      // Comparer selon l'ordre de priorité
      if (
        ordrePriorite[taches[j].priorite] <
        ordrePriorite[taches[indexMin].priorite]
      ) {
        indexMin = j;
      }
    }

    if (indexMin !== i) {
      [taches[i], taches[indexMin]] = [taches[indexMin], taches[i]];
    }
  }

  return taches;
}

// Test
const taches = [
  { titre: "Réviser code", priorite: "Moyenne" },
  { titre: "Corriger bug", priorite: "Haute" },
  { titre: "Écrire tests", priorite: "Basse" },
  { titre: "Déployer", priorite: "Haute" },
  { titre: "Documentation", priorite: "Basse" },
];

trierTachesParPriorite(taches);

console.log("Tâches triées par priorité:");
taches.forEach((t) => console.log(`  [${t.priorite}] ${t.titre}`));
// [Haute] Corriger bug
// [Haute] Déployer
// [Moyenne] Réviser code
// [Basse] Écrire tests
// [Basse] Documentation
```

**Explication :**

- On utilise un objet `ordrePriorite` pour mapper les priorités à des valeurs numériques
- La priorité "Haute" a la valeur 1 (la plus petite), donc elle sera triée en premier
- Le tri par sélection place les éléments avec les plus petites valeurs de priorité au début

</details>

---

### Exercice 3 : Trouver les K Plus Petits Éléments

**Objectif :** Optimiser le tri par sélection pour un cas particulier.

**Instructions :** Implémentez une fonction qui trouve les K plus petits éléments d'un tableau en utilisant le principe du tri par sélection, mais en s'arrêtant après K passes.

```javascript
function kPlusPetits(tableau, k) {
  // Votre implémentation ici
}

// Tests
console.log(kPlusPetits([64, 25, 12, 22, 11], 3));
// [11, 12, 22]

console.log(kPlusPetits([9, 4, 7, 1, 3, 8], 2));
// [1, 3]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trouve les K plus petits éléments d'un tableau
 * @param {number[]} tableau - Le tableau source
 * @param {number} k - Nombre d'éléments à trouver
 * @returns {number[]} - Les K plus petits éléments, triés
 */
function kPlusPetits(tableau, k) {
  // Créer une copie pour ne pas modifier l'original
  const copie = [...tableau];
  const n = copie.length;

  // Limiter k à la taille du tableau
  k = Math.min(k, n);

  // Effectuer seulement k passes au lieu de n-1
  for (let i = 0; i < k; i++) {
    let indexMin = i;

    for (let j = i + 1; j < n; j++) {
      if (copie[j] < copie[indexMin]) {
        indexMin = j;
      }
    }

    if (indexMin !== i) {
      [copie[i], copie[indexMin]] = [copie[indexMin], copie[i]];
    }
  }

  // Retourner les k premiers éléments
  return copie.slice(0, k);
}

// Tests
console.log(kPlusPetits([64, 25, 12, 22, 11], 3));
// [11, 12, 22]

console.log(kPlusPetits([9, 4, 7, 1, 3, 8], 2));
// [1, 3]

console.log(kPlusPetits([5, 2, 8, 1, 9], 1));
// [1]

console.log(kPlusPetits([3, 1, 4], 5));
// [1, 3, 4] (k limité à n)
```

**Explication :**

Cette optimisation exploite le fait que le tri par sélection place les éléments à leur position finale un par un. Après k passes, les k premiers éléments sont les k plus petits, triés.

**Complexité :** O(k × n) au lieu de O(n²), ce qui est significativement meilleur quand k << n.

</details>

---

### Exercice 4 : Comparer Tri à Bulles et Tri par Sélection

**Objectif :** Analyser empiriquement les performances des deux algorithmes.

**Instructions :** Créez une fonction qui compare le tri à bulles et le tri par sélection sur un même tableau, en comptant les comparaisons et échanges.

```javascript
function comparerAlgorithmes(tableau) {
  // Votre implémentation ici
  // Retourner un objet avec les statistiques des deux algorithmes
}

// Test
const resultat = comparerAlgorithmes([5, 2, 8, 1, 9, 3]);
console.log(resultat);
// {
//   bulles: { comparaisons: X, echanges: Y },
//   selection: { comparaisons: X, echanges: Y }
// }
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Compare le tri à bulles et le tri par sélection
 * @param {number[]} tableau - Le tableau à trier
 * @returns {Object} - Statistiques des deux algorithmes
 */
function comparerAlgorithmes(tableau) {
  // Tri à bulles avec comptage
  function triBullesStats(arr) {
    const copie = [...arr];
    const n = copie.length;
    let comparaisons = 0;
    let echanges = 0;

    for (let i = 0; i < n - 1; i++) {
      let echangeEffectue = false;

      for (let j = 0; j < n - 1 - i; j++) {
        comparaisons++;
        if (copie[j] > copie[j + 1]) {
          [copie[j], copie[j + 1]] = [copie[j + 1], copie[j]];
          echanges++;
          echangeEffectue = true;
        }
      }

      if (!echangeEffectue) break;
    }

    return { comparaisons, echanges };
  }

  // Tri par sélection avec comptage
  function triSelectionStats(arr) {
    const copie = [...arr];
    const n = copie.length;
    let comparaisons = 0;
    let echanges = 0;

    for (let i = 0; i < n - 1; i++) {
      let indexMin = i;

      for (let j = i + 1; j < n; j++) {
        comparaisons++;
        if (copie[j] < copie[indexMin]) {
          indexMin = j;
        }
      }

      if (indexMin !== i) {
        [copie[i], copie[indexMin]] = [copie[indexMin], copie[i]];
        echanges++;
      }
    }

    return { comparaisons, echanges };
  }

  return {
    bulles: triBullesStats(tableau),
    selection: triSelectionStats(tableau),
  };
}

// Tests
console.log("Tableau aléatoire [5, 2, 8, 1, 9, 3]:");
console.log(comparerAlgorithmes([5, 2, 8, 1, 9, 3]));

console.log("\nTableau trié [1, 2, 3, 4, 5]:");
console.log(comparerAlgorithmes([1, 2, 3, 4, 5]));

console.log("\nTableau inversé [5, 4, 3, 2, 1]:");
console.log(comparerAlgorithmes([5, 4, 3, 2, 1]));
```

**Résultats typiques :**

```
Tableau aléatoire [5, 2, 8, 1, 9, 3]:
{
  bulles: { comparaisons: 15, echanges: 7 },
  selection: { comparaisons: 15, echanges: 4 }
}

Tableau trié [1, 2, 3, 4, 5]:
{
  bulles: { comparaisons: 4, echanges: 0 },     // Arrêt précoce !
  selection: { comparaisons: 10, echanges: 0 }  // Toujours n(n-1)/2
}

Tableau inversé [5, 4, 3, 2, 1]:
{
  bulles: { comparaisons: 10, echanges: 10 },   // Beaucoup d'échanges
  selection: { comparaisons: 10, echanges: 2 }  // Peu d'échanges
}
```

**Observations :**

- Le tri par sélection fait toujours moins (ou autant) d'échanges
- Le tri à bulles peut faire moins de comparaisons sur un tableau déjà trié
- Le tri par sélection fait toujours le même nombre de comparaisons

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la principale différence entre le tri par sélection et le tri à bulles ?**

- [ ] A. Le tri par sélection est plus rapide
- [ ] B. Le tri par sélection trouve le minimum et l'échange directement, tandis que le tri à bulles fait remonter les éléments par échanges successifs
- [ ] C. Le tri par sélection utilise plus de mémoire
- [ ] D. Le tri par sélection ne fonctionne qu'avec des nombres

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri par sélection parcourt la partie non triée pour trouver le minimum, puis l'échange directement avec le premier élément non trié. Le tri à bulles, lui, compare et échange les éléments adjacents, faisant "remonter" progressivement les plus grands éléments.

</details>

---

### Question 2

**Quelle est la complexité temporelle du tri par sélection dans le meilleur cas ?**

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n²)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Contrairement au tri à bulles optimisé qui peut atteindre O(n) dans le meilleur cas, le tri par sélection effectue **toujours** n(n-1)/2 comparaisons, quelle que soit l'organisation initiale des données. Il n'y a pas d'optimisation pour les tableaux déjà triés.

</details>

---

### Question 3

**Combien d'échanges au maximum le tri par sélection effectue-t-il pour un tableau de n éléments ?**

- [ ] A. n(n-1)/2
- [ ] B. n²
- [ ] C. n-1
- [ ] D. n

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le tri par sélection effectue au maximum n-1 échanges (un par passe), ce qui est l'un de ses avantages par rapport au tri à bulles qui peut effectuer jusqu'à n(n-1)/2 échanges.

</details>

---

### Question 4

**Le tri par sélection est-il un algorithme stable ?**

- [ ] A. Oui, il préserve toujours l'ordre des éléments égaux
- [ ] B. Non, l'échange direct peut modifier l'ordre relatif des éléments égaux
- [ ] C. Ça dépend de l'implémentation
- [ ] D. La stabilité ne s'applique pas au tri par sélection

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri par sélection est **instable**. Quand il échange le minimum trouvé avec le premier élément non trié, l'élément "déplacé" peut se retrouver après un élément de même valeur, modifiant leur ordre relatif original.

</details>

---

### Question 5

**Dans quelle situation le tri par sélection est-il préférable au tri à bulles ?**

- [ ] A. Quand le tableau est presque trié
- [ ] B. Quand les opérations d'écriture (échanges) sont coûteuses
- [ ] C. Quand la stabilité est importante
- [ ] D. Quand on veut détecter si le tableau est déjà trié

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri par sélection est préférable quand les opérations d'écriture sont coûteuses (ex: écriture sur mémoire flash) car il effectue au maximum n-1 échanges, contre potentiellement O(n²) pour le tri à bulles.

</details>

---

### Question 6

**Après la première passe du tri par sélection (ascendant), que pouvons-nous garantir ?**

- [ ] A. Le plus grand élément est à la fin
- [ ] B. Le plus petit élément est au début
- [ ] C. La moitié du tableau est triée
- [ ] D. Le tableau est complètement trié

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Après la première passe, le plus petit élément de tout le tableau est placé à la première position (index 0). La partie triée contient alors un seul élément.

</details>

---

### Question 7

**Quelle est la complexité spatiale du tri par sélection ?**

- [ ] A. O(n)
- [ ] B. O(n²)
- [ ] C. O(log n)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Le tri par sélection est un algorithme **en place** qui n'utilise qu'une quantité constante de mémoire supplémentaire (variables pour l'index du minimum et pour l'échange), d'où O(1).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Concept Fondamental

Le tri par sélection divise le tableau en deux parties : une partie triée (au début) et une partie non triée. À chaque passe, il sélectionne le minimum de la partie non triée et le place à la fin de la partie triée.

### 2. Mécanisme Simple

L'algorithme parcourt la partie non triée pour trouver l'index du minimum, puis échange cet élément avec le premier élément non trié. Après k passes, les k plus petits éléments sont triés.

### 3. Complexité Temporelle Constante

Le tri par sélection a une complexité de O(n²) dans **tous** les cas (meilleur, moyen, pire). Il effectue toujours n(n-1)/2 comparaisons, sans possibilité d'arrêt précoce.

### 4. Nombre Minimal d'Échanges

L'avantage majeur du tri par sélection est son nombre d'échanges : au maximum n-1, ce qui est optimal parmi les algorithmes de tri par comparaison simples.

### 5. Algorithme Instable

Le tri par sélection peut modifier l'ordre relatif des éléments égaux lors des échanges, ce qui le rend inadapté aux tris multi-critères nécessitant la préservation de l'ordre.

### 6. Tri en Place

Avec une complexité spatiale de O(1), le tri par sélection ne nécessite pas de mémoire supplémentaire significative.

### 7. Cas d'Utilisation

Idéal quand les opérations d'écriture sont coûteuses, pour les petits tableaux, ou à des fins pédagogiques. À éviter pour les grands ensembles de données ou quand la stabilité est requise.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maîtrisé le tri par sélection, un algorithme fondamental qui complète votre compréhension des techniques de tri simples.

### Ce que vous avez appris aujourd'hui

- Le concept du tri par sélection et sa logique de "recherche du minimum"
- La division du tableau en parties triée et non triée
- L'implémentation en JavaScript avec ses variantes
- L'analyse de complexité et la comparaison avec le tri à bulles
- La notion d'instabilité et ses implications

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter le tri par sélection pour différents types de données
- Choisir entre tri à bulles et tri par sélection selon le contexte
- Comprendre les compromis entre nombre de comparaisons et d'échanges

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Avec le tri à bulles et le tri par sélection, vous avez maintenant une vue complète de deux approches différentes du tri : l'une qui fait "remonter" les éléments (bulles), l'autre qui "sélectionne" directement le minimum (sélection). La prochaine étape sera le tri par insertion, qui adopte encore une autre stratégie !

---

## ➡️ Prochaine Étape : Leçon 16

### Ce qui vous attend

La prochaine leçon, **« Tri par Insertion (Insertion Sort) »**, vous présentera un algorithme qui construit le tableau trié un élément à la fois.

**Vous découvrirez :**

- Comment le tri par insertion fonctionne comme le tri de cartes en main
- Pourquoi il est souvent plus performant sur les tableaux presque triés
- La comparaison avec les tris à bulles et par sélection
- Quand et pourquoi utiliser le tri par insertion

### Préparez-vous !

Le tri par insertion complète le trio des algorithmes de tri "élémentaires" (O(n²)). Il est particulièrement intéressant car il combine les avantages des deux algorithmes précédents dans certains cas d'utilisation.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Selection Sort](https://visualgo.net/en/sorting) - Visualisation interactive
- [GeeksforGeeks - Selection Sort](https://www.geeksforgeeks.org/selection-sort/) - Tutoriel détaillé
- [Sorting Algorithms Visualized](https://www.toptal.com/developers/sorting-algorithms/selection-sort) - Comparaison visuelle

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
> Pour bien visualiser la différence entre tri à bulles et tri par sélection, prenez un jeu de cartes et triez-les avec chaque méthode. Comptez le nombre de comparaisons et d'échanges. Vous constaterez que le tri par sélection fait moins d'échanges mais ne peut pas profiter d'un jeu déjà presque trié !

---

**Prêt pour la Leçon 16 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir le tri par insertion !

---

<div align="center">

**Leçon 15 sur 42 - Module 3 : Techniques de Tri Essentielles**

[⬅️ Leçon 14 : Tri à Bulles : Concept et Implémentation JavaScript de Base](./lecon-2-tri-bulles-concept-implementation-javascript-base.md) | [Retour au sommaire](./README.md) | [Leçon 16 : Tri par Insertion : Concept et Implémentation JavaScript Pratique ➡️](./lecon-4-tri-insertion-concept-implementation-javascript-pratique.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
