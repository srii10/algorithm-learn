##### Leçon 37 sur 42

# Révision des Stratégies de Conception d'Algorithmes

**Module 7** : Applications d'Algorithmes et Résolution de Problèmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Expliquer les trois paradigmes majeurs : Diviser pour Régner, Glouton, Programmation Dynamique
- Implémenter chaque paradigme en JavaScript avec analyse Big O
- Identifier les propriétés nécessaires pour appliquer chaque stratégie
- Reconnaître les pièges classiques et savoir les éviter
- Choisir le bon paradigme en fonction du problème posé

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- [Maîtrise des algorithmes de tri](../module-3/lecon-1-introduction-tri-pourquoi-ordonner-donnees.md) (Module 3)
- [Connaissance des algorithmes gloutons](../module-6/lecon-1-introduction-algorithmes-gloutons-choix-optimal-local.md) (Module 6)
- [Compréhension de la programmation dynamique](../module-6/lecon-4-fondements-programmation-dynamique-sous-problemes-memoisation.md) (Module 6)
- Notation Big O et analyse de complexité

---

## 🚀 Introduction : Penser Comme un Architecte d'Algorithmes

Imaginez que vous devez construire un pont. Vous ne commencez pas par poser des briques au hasard : vous choisissez d'abord une **méthode de construction** adaptée au terrain, aux contraintes et aux matériaux disponibles.

En algorithmique, c'est la même chose. Face à un problème, les développeurs expérimentés ne codent pas immédiatement : ils identifient d'abord **quel paradigme de conception** s'applique. Cette capacité à reconnaître le bon pattern est ce qui distingue un développeur junior d'un développeur senior.

**Les trois paradigmes fondamentaux sont :**

- **Diviser pour Régner** : Décomposer, résoudre, combiner
- **Algorithmes Gloutons** : Toujours prendre le meilleur choix local
- **Programmation Dynamique** : Mémoriser pour ne jamais recalculer

> **Point Clé**
>
> Chaque paradigme a des **conditions d'application** précises. Utiliser le mauvais paradigme peut mener à une solution incorrecte ou inefficace. Cette leçon vous apprendra à faire le bon choix.

---

## 🧩 Paradigme 1 : Diviser pour Régner (Divide and Conquer)

### Principe Fondamental

La stratégie **Diviser pour Régner** se décompose en trois étapes :

1. **Diviser** : Fractionner le problème en sous-problèmes plus petits
2. **Régner** : Résoudre chaque sous-problème (souvent récursivement)
3. **Combiner** : Fusionner les solutions pour obtenir la solution globale

```
        Problème Original
              |
     +--------+--------+
     |                 |
Sous-problème 1   Sous-problème 2
     |                 |
  Solution 1       Solution 2
     |                 |
     +--------+--------+
              |
       Solution Finale
```

### Complexité Big O Typique

| Algorithme              | Temps                        | Espace   | Caractéristique        |
| ----------------------- | ---------------------------- | -------- | ---------------------- |
| Tri Fusion (Merge Sort) | **O(n log n)**               | O(n)     | Toujours stable        |
| Tri Rapide (Quick Sort) | O(n log n) moyen, O(n²) pire | O(log n) | In-place               |
| Recherche Binaire       | **O(log n)**                 | O(1)     | Requiert tableau trié  |
| Exponentiation Rapide   | **O(log n)**                 | O(1)     | Puissance en temps log |

### Exemple 1 : Tri Fusion (Merge Sort)

```javascript
/**
 * Tri Fusion - Diviser pour Régner
 * Complexité temporelle : O(n log n) - toujours garanti
 * Complexité spatiale : O(n) - tableau auxiliaire nécessaire
 *
 * @param {number[]} arr - Tableau à trier
 * @returns {number[]} - Tableau trié
 */
function mergeSort(arr) {
  // Cas de base : un tableau de 0 ou 1 élément est déjà trié
  if (arr.length <= 1) {
    return arr;
  }

  // DIVISER : Couper le tableau en deux moitiés
  const milieu = Math.floor(arr.length / 2);
  const gauche = arr.slice(0, milieu);
  const droite = arr.slice(milieu);

  // RÉGNER : Trier récursivement chaque moitié
  const gaucheTriee = mergeSort(gauche);
  const droiteTriee = mergeSort(droite);

  // COMBINER : Fusionner les deux moitiés triées
  return fusionner(gaucheTriee, droiteTriee);
}

/**
 * Fusionne deux tableaux triés en un seul tableau trié
 * Complexité : O(n) où n = taille des deux tableaux combinés
 */
function fusionner(gauche, droite) {
  const resultat = [];
  let i = 0,
    j = 0;

  // Comparer élément par élément
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
  return resultat.concat(gauche.slice(i)).concat(droite.slice(j));
}

// Tests
console.log(mergeSort([38, 27, 43, 3, 9, 82, 10]));
// [3, 9, 10, 27, 38, 43, 82]

console.log(mergeSort([5, 1, 4, 2, 8]));
// [1, 2, 4, 5, 8]
```

**Analyse Big O :**

- **Temps O(n log n)** : On divise log(n) fois, et chaque niveau nécessite O(n) opérations de fusion
- **Espace O(n)** : Le tableau auxiliaire pour la fusion

---

### Exemple 2 : Recherche Binaire

```javascript
/**
 * Recherche Binaire - Diviser pour Régner
 * Complexité temporelle : O(log n) - division par 2 à chaque étape
 * Complexité spatiale : O(1) version itérative, O(log n) récursive
 *
 * @param {number[]} arr - Tableau TRIÉ
 * @param {number} cible - Valeur recherchée
 * @returns {number} - Index de la cible ou -1 si non trouvée
 */
function rechercheBinaire(arr, cible) {
  let gauche = 0;
  let droite = arr.length - 1;

  while (gauche <= droite) {
    // DIVISER : Trouver le milieu
    const milieu = Math.floor((gauche + droite) / 2);

    // RÉGNER : Comparer et choisir la moitié pertinente
    if (arr[milieu] === cible) {
      return milieu; // Trouvé !
    } else if (arr[milieu] < cible) {
      gauche = milieu + 1; // Chercher à droite
    } else {
      droite = milieu - 1; // Chercher à gauche
    }
  }

  return -1; // Non trouvé
}

// Tests
const tableauTrie = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];

console.log(rechercheBinaire(tableauTrie, 7)); // 3 (index)
console.log(rechercheBinaire(tableauTrie, 1)); // 0 (premier élément)
console.log(rechercheBinaire(tableauTrie, 19)); // 9 (dernier élément)
console.log(rechercheBinaire(tableauTrie, 8)); // -1 (non trouvé)
```

**Pourquoi O(log n) ?**

- À chaque itération, on élimine **la moitié** des éléments
- Pour n=1000 : max 10 comparaisons (2¹⁰ = 1024)
- Pour n=1 000 000 : max 20 comparaisons (2²⁰ ≈ 1M)

---

## 📝 Micro-Exercice 1 : Somme d'un Tableau (Diviser pour Régner)

**Objectif :** Implémenter une fonction qui calcule la somme d'un tableau en utilisant Diviser pour Régner.

**Instructions :**

1. Diviser le tableau en deux moitiés
2. Calculer récursivement la somme de chaque moitié
3. Combiner en additionnant les deux sommes

```javascript
function sommeTableau(arr) {
  // TODO: Implémenter avec Diviser pour Régner
}

// Tests
console.log(sommeTableau([1, 2, 3, 4, 5])); // Devrait retourner 15
console.log(sommeTableau([10, 20, 30])); // Devrait retourner 60
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Somme d'un tableau avec Diviser pour Régner
 * Complexité temporelle : O(n) - on visite chaque élément une fois
 * Complexité spatiale : O(log n) - profondeur de la pile d'appels
 *
 * @param {number[]} arr - Tableau de nombres
 * @returns {number} - Somme de tous les éléments
 */
function sommeTableau(arr) {
  // Cas de base : tableau vide
  if (arr.length === 0) {
    return 0;
  }

  // Cas de base : un seul élément
  if (arr.length === 1) {
    return arr[0];
  }

  // DIVISER : Couper en deux
  const milieu = Math.floor(arr.length / 2);
  const gauche = arr.slice(0, milieu);
  const droite = arr.slice(milieu);

  // RÉGNER et COMBINER : Somme des deux moitiés
  return sommeTableau(gauche) + sommeTableau(droite);
}

// Tests
console.log(sommeTableau([1, 2, 3, 4, 5])); // 15
console.log(sommeTableau([10, 20, 30])); // 60
console.log(sommeTableau([])); // 0
console.log(sommeTableau([42])); // 42
```

**Explication :**

- Diviser pour Régner n'est pas optimal ici (une simple boucle suffit)
- Mais cet exercice illustre le pattern : diviser → résoudre → combiner
- Complexité O(n) car chaque élément est visité exactement une fois

</details>

---

## 🧩 Paradigme 2 : Algorithmes Gloutons (Greedy)

### Principe Fondamental

Un algorithme **glouton** fait à chaque étape le **choix localement optimal**, espérant que cela mène à une solution **globalement optimale**.

**Conditions nécessaires :**

1. **Propriété du choix glouton** : Le meilleur choix local mène à la solution optimale
2. **Sous-structure optimale** : La solution contient des solutions optimales de sous-problèmes

**Attention** : Ces conditions ne sont PAS toujours vérifiées ! Un glouton peut donner une solution incorrecte.

### Complexité Big O Typique

| Algorithme                               | Temps          | Espace | Optimalité      |
| ---------------------------------------- | -------------- | ------ | --------------- |
| Rendu de monnaie (système canonique)     | **O(n)**       | O(1)   | Optimal         |
| Rendu de monnaie (système non-canonique) | O(n)           | O(1)   | **Non optimal** |
| Sélection d'activités                    | **O(n log n)** | O(1)   | Optimal         |
| Huffman Coding                           | **O(n log n)** | O(n)   | Optimal         |

### Exemple 1 : Rendu de Monnaie (Glouton)

```javascript
/**
 * Rendu de monnaie - Algorithme Glouton
 * Complexité temporelle : O(n) où n = nombre de types de pièces
 * Complexité spatiale : O(k) où k = nombre de pièces utilisées
 *
 * IMPORTANT : Ne fonctionne que pour les systèmes CANONIQUES
 * (Euro, Dollar, etc.) où le glouton donne toujours l'optimal
 *
 * @param {number} montant - Montant à rendre
 * @param {number[]} pieces - Types de pièces disponibles (triées décroissant)
 * @returns {number[]} - Liste des pièces utilisées
 */
function renduMonnaieGlouton(
  montant,
  pieces = [200, 100, 50, 20, 10, 5, 2, 1],
) {
  const resultat = [];
  let reste = montant;

  // Pour chaque type de pièce (du plus grand au plus petit)
  for (const piece of pieces) {
    // Prendre autant de cette pièce que possible (choix glouton)
    while (reste >= piece) {
      resultat.push(piece);
      reste -= piece;
    }
  }

  // Vérifier si le montant a été entièrement rendu
  if (reste > 0) {
    console.log(`Impossible de rendre exactement ${montant} centimes`);
    return null;
  }

  return resultat;
}

// Tests avec système Euro (canonique - glouton optimal)
console.log(renduMonnaieGlouton(289));
// [200, 50, 20, 10, 5, 2, 2] = 7 pièces

console.log(renduMonnaieGlouton(47));
// [20, 20, 5, 2] = 4 pièces

// Analyse
console.log(
  `Nombre de pièces pour 289 centimes: ${renduMonnaieGlouton(289).length}`,
);
// 7 pièces
```

---

### Piège du Glouton : Système Non-Canonique

```javascript
/**
 * Démonstration de l'échec du glouton
 * avec un système de pièces NON canonique
 */
function demonstrationEchecGlouton() {
  // Système non-canonique : pièces de 1, 3, 4
  const piecesNonCanoniques = [4, 3, 1];
  const montant = 6;

  // Solution gloutonne
  const solutionGlouton = [];
  let reste = montant;

  for (const piece of piecesNonCanoniques) {
    while (reste >= piece) {
      solutionGlouton.push(piece);
      reste -= piece;
    }
  }

  console.log("=== Système NON canonique [4, 3, 1] ===");
  console.log(`Montant à rendre: ${montant}`);
  console.log(`Solution GLOUTONNE: [${solutionGlouton}]`);
  console.log(`Nombre de pièces (glouton): ${solutionGlouton.length}`);
  // Solution gloutonne: [4, 1, 1] = 3 pièces

  console.log("\nSolution OPTIMALE: [3, 3]");
  console.log("Nombre de pièces (optimal): 2");
  // Solution optimale: [3, 3] = 2 pièces

  console.log("\nLe glouton donne 3 pièces au lieu de 2 !");
  console.log(
    "→ Pour les systèmes non-canoniques, utiliser la Programmation Dynamique",
  );
}

demonstrationEchecGlouton();
```

---

### Exemple 2 : Sélection d'Activités

```javascript
/**
 * Sélection d'activités - Algorithme Glouton
 * Problème : Maximiser le nombre d'activités non-chevauchantes
 *
 * Complexité temporelle : O(n log n) - tri + parcours linéaire
 * Complexité spatiale : O(1) - tri en place possible
 *
 * @param {Array<{debut: number, fin: number, nom: string}>} activites
 * @returns {Array} - Activités sélectionnées
 */
function selectionActivites(activites) {
  // Trier par heure de FIN (choix glouton)
  // Pourquoi ? Libère le plus tôt possible pour d'autres activités
  const activitesTriees = [...activites].sort((a, b) => a.fin - b.fin);

  const selection = [];
  let derniereFin = 0;

  for (const activite of activitesTriees) {
    // Si l'activité commence après la fin de la dernière sélectionnée
    if (activite.debut >= derniereFin) {
      selection.push(activite);
      derniereFin = activite.fin;
    }
  }

  return selection;
}

// Test
const activites = [
  { nom: "Réunion A", debut: 1, fin: 4 },
  { nom: "Réunion B", debut: 3, fin: 5 },
  { nom: "Réunion C", debut: 0, fin: 6 },
  { nom: "Réunion D", debut: 5, fin: 7 },
  { nom: "Réunion E", debut: 3, fin: 9 },
  { nom: "Réunion F", debut: 5, fin: 9 },
  { nom: "Réunion G", debut: 6, fin: 10 },
  { nom: "Réunion H", debut: 8, fin: 11 },
  { nom: "Réunion I", debut: 8, fin: 12 },
  { nom: "Réunion J", debut: 2, fin: 14 },
  { nom: "Réunion K", debut: 12, fin: 16 },
];

const resultat = selectionActivites(activites);
console.log("Activités sélectionnées:");
resultat.forEach((a) => console.log(`  ${a.nom}: ${a.debut}h - ${a.fin}h`));
console.log(`Total: ${resultat.length} activités`);
// Réunion A: 1h - 4h
// Réunion D: 5h - 7h
// Réunion H: 8h - 11h
// Réunion K: 12h - 16h
// Total: 4 activités
```

---

## 📝 Micro-Exercice 2 : Fractional Knapsack (Sac à Dos Fractionnaire)

**Objectif :** Implémenter l'algorithme glouton pour le sac à dos fractionnaire.

**Contexte :** Contrairement au 0/1 Knapsack, on peut prendre une **fraction** d'un objet.

```javascript
function sacADosFractionnaire(capacite, objets) {
  // objets = [{nom, poids, valeur}, ...]
  // Trier par ratio valeur/poids décroissant
  // Prendre autant que possible de chaque objet
  // TODO: Implémenter
}

// Test
const objets = [
  { nom: "Or", poids: 10, valeur: 60 },
  { nom: "Argent", poids: 20, valeur: 100 },
  { nom: "Bronze", poids: 30, valeur: 120 },
];
console.log(sacADosFractionnaire(50, objets));
// Devrait retourner 240 (Or complet + Argent complet + 2/3 Bronze)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Sac à dos fractionnaire - Algorithme Glouton
 * Complexité temporelle : O(n log n) - dominé par le tri
 * Complexité spatiale : O(n) - copie pour le tri
 *
 * Le glouton est OPTIMAL pour le fractionnaire (pas pour 0/1)
 *
 * @param {number} capacite - Capacité maximale du sac
 * @param {Array<{nom: string, poids: number, valeur: number}>} objets
 * @returns {number} - Valeur maximale atteignable
 */
function sacADosFractionnaire(capacite, objets) {
  // Calculer le ratio valeur/poids pour chaque objet
  const objetsAvecRatio = objets.map((obj) => ({
    ...obj,
    ratio: obj.valeur / obj.poids,
  }));

  // Trier par ratio décroissant (choix glouton)
  objetsAvecRatio.sort((a, b) => b.ratio - a.ratio);

  let valeurTotale = 0;
  let capaciteRestante = capacite;
  const selection = [];

  for (const obj of objetsAvecRatio) {
    if (capaciteRestante === 0) break;

    if (obj.poids <= capaciteRestante) {
      // Prendre l'objet en entier
      valeurTotale += obj.valeur;
      capaciteRestante -= obj.poids;
      selection.push({ ...obj, fraction: 1 });
    } else {
      // Prendre une fraction de l'objet
      const fraction = capaciteRestante / obj.poids;
      valeurTotale += obj.valeur * fraction;
      selection.push({ ...obj, fraction });
      capaciteRestante = 0;
    }
  }

  console.log("Sélection:");
  selection.forEach((s) => {
    console.log(
      `  ${s.nom}: ${(s.fraction * 100).toFixed(0)}% (valeur: ${(s.valeur * s.fraction).toFixed(1)})`,
    );
  });

  return valeurTotale;
}

// Test
const objets = [
  { nom: "Or", poids: 10, valeur: 60 }, // ratio = 6
  { nom: "Argent", poids: 20, valeur: 100 }, // ratio = 5
  { nom: "Bronze", poids: 30, valeur: 120 }, // ratio = 4
];

const valeurMax = sacADosFractionnaire(50, objets);
console.log(`\nValeur maximale: ${valeurMax}`);
// Sélection:
//   Or: 100% (valeur: 60)
//   Argent: 100% (valeur: 100)
//   Bronze: 67% (valeur: 80)
// Valeur maximale: 240
```

**Explication :**

- Le ratio Or = 60/10 = 6 est le meilleur → on prend tout (10kg, valeur 60)
- Le ratio Argent = 100/20 = 5 → on prend tout (20kg, valeur 100)
- Reste 20kg de capacité, Bronze pèse 30kg → on prend 20/30 = 66.7%
- Valeur Bronze partiel = 120 × 0.667 = 80
- Total = 60 + 100 + 80 = 240

</details>

---

## 🧩 Paradigme 3 : Programmation Dynamique (DP)

### Principe Fondamental

La **Programmation Dynamique** résout les problèmes en :

1. Identifiant les **sous-problèmes chevauchants** (mêmes calculs répétés)
2. Stockant leurs solutions pour éviter les recalculs (**mémoïsation** ou **tabulation**)

**Conditions nécessaires :**

1. **Sous-problèmes chevauchants** : Les mêmes sous-problèmes apparaissent plusieurs fois
2. **Sous-structure optimale** : La solution optimale contient des solutions optimales de sous-problèmes

### Comparaison des Approches

| Aspect            | Mémoïsation (Top-Down)       | Tabulation (Bottom-Up)          |
| ----------------- | ---------------------------- | ------------------------------- |
| Direction         | Récursif (haut → bas)        | Itératif (bas → haut)           |
| Complexité temps  | O(n)                         | O(n)                            |
| Complexité espace | O(n) cache + O(n) pile       | O(n) table                      |
| Avantage          | Ne calcule que le nécessaire | Pas de risque de stack overflow |
| Inconvénient      | Stack overflow possible      | Calcule tous les sous-problèmes |

### Exemple 1 : Fibonacci - Les Deux Approches

```javascript
/**
 * Fibonacci NAÏF (sans DP)
 * Complexité temporelle : O(2^n) - EXPONENTIELLE !
 * Complexité spatiale : O(n) - pile d'appels
 *
 * Ne JAMAIS utiliser en production
 */
function fibonacciNaif(n) {
  if (n <= 1) return n;
  return fibonacciNaif(n - 1) + fibonacciNaif(n - 2);
}

/**
 * Fibonacci avec MÉMOÏSATION (Top-Down)
 * Complexité temporelle : O(n) - chaque valeur calculée une fois
 * Complexité spatiale : O(n) - cache + pile d'appels
 */
function fibonacciMemo(n, memo = {}) {
  // Vérifier le cache
  if (n in memo) return memo[n];

  // Cas de base
  if (n <= 1) return n;

  // Calculer et stocker
  memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
  return memo[n];
}

/**
 * Fibonacci avec TABULATION (Bottom-Up)
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(n) pour la table, O(1) optimisé
 */
function fibonacciTab(n) {
  if (n <= 1) return n;

  // Table de bas en haut
  const table = [0, 1];

  for (let i = 2; i <= n; i++) {
    table[i] = table[i - 1] + table[i - 2];
  }

  return table[n];
}

/**
 * Fibonacci OPTIMISÉ (espace O(1))
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(1) - seulement 2 variables
 */
function fibonacciOptimise(n) {
  if (n <= 1) return n;

  let prev2 = 0;
  let prev1 = 1;

  for (let i = 2; i <= n; i++) {
    const current = prev1 + prev2;
    prev2 = prev1;
    prev1 = current;
  }

  return prev1;
}

// Comparaison de performance
console.log("=== Comparaison Fibonacci ===");
console.log(`fib(40) mémoïsation: ${fibonacciMemo(40)}`); // Instantané
console.log(`fib(40) tabulation: ${fibonacciTab(40)}`); // Instantané
console.log(`fib(40) optimisé: ${fibonacciOptimise(40)}`); // Instantané
// console.log(`fib(40) naïf: ${fibonacciNaif(40)}`);         // ~1 minute !

console.log("\n=== Complexités Big O ===");
console.log("Naïf:        O(2^n) temps, O(n) espace - INUTILISABLE");
console.log("Mémoïsation: O(n) temps, O(n) espace");
console.log("Tabulation:  O(n) temps, O(n) espace");
console.log("Optimisé:    O(n) temps, O(1) espace - IDÉAL");
```

---

### Exemple 2 : Rendu de Monnaie avec DP

```javascript
/**
 * Rendu de monnaie - Programmation Dynamique
 * Trouve le NOMBRE MINIMUM de pièces (fonctionne pour tout système)
 *
 * Complexité temporelle : O(montant × nombre_de_pièces)
 * Complexité spatiale : O(montant)
 *
 * @param {number} montant - Montant à rendre
 * @param {number[]} pieces - Types de pièces disponibles
 * @returns {number} - Nombre minimum de pièces (-1 si impossible)
 */
function renduMonnaieDP(montant, pieces) {
  // Table : dp[i] = nombre minimum de pièces pour rendre i centimes
  // Initialiser avec Infinity (montant impossible)
  const dp = new Array(montant + 1).fill(Infinity);
  dp[0] = 0; // 0 pièces pour 0 centimes

  // Pour chaque montant de 1 à montant
  for (let m = 1; m <= montant; m++) {
    // Essayer chaque type de pièce
    for (const piece of pieces) {
      if (piece <= m && dp[m - piece] !== Infinity) {
        dp[m] = Math.min(dp[m], dp[m - piece] + 1);
      }
    }
  }

  return dp[montant] === Infinity ? -1 : dp[montant];
}

// Test avec système non-canonique
console.log("=== Système NON canonique [1, 3, 4] ===");
const piecesNC = [1, 3, 4];

console.log(`Montant 6:`);
console.log(`  DP (optimal): ${renduMonnaieDP(6, piecesNC)} pièces`); // 2 (3+3)
console.log(`  Glouton donnerait: 3 pièces (4+1+1)`);

console.log(`\nMontant 11:`);
console.log(`  DP (optimal): ${renduMonnaieDP(11, piecesNC)} pièces`); // 3 (4+4+3)

// Test avec système Euro
console.log("\n=== Système Euro ===");
const piecesEuro = [1, 2, 5, 10, 20, 50, 100, 200];
console.log(`Montant 289: ${renduMonnaieDP(289, piecesEuro)} pièces`); // 7
```

---

## 📝 Micro-Exercice 3 : Monter l'Escalier

**Objectif :** Compter le nombre de façons de monter un escalier de n marches (1 ou 2 marches à la fois).

```javascript
function monterEscalier(n) {
  // TODO: Implémenter avec mémoïsation OU tabulation
}

// Tests
console.log(monterEscalier(3)); // 3 façons: (1+1+1), (1+2), (2+1)
console.log(monterEscalier(5)); // 8 façons
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Nombre de façons de monter un escalier
 * On peut monter 1 ou 2 marches à la fois
 *
 * Relation de récurrence : ways(n) = ways(n-1) + ways(n-2)
 * (soit on vient de n-1 avec 1 pas, soit de n-2 avec 2 pas)
 *
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(n) avec tabulation, O(1) optimisé
 */

// Version mémoïsation
function monterEscalierMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 2) return n; // 1 façon pour 1 marche, 2 façons pour 2 marches

  memo[n] = monterEscalierMemo(n - 1, memo) + monterEscalierMemo(n - 2, memo);
  return memo[n];
}

// Version tabulation
function monterEscalierTab(n) {
  if (n <= 2) return n;

  const dp = [0, 1, 2]; // dp[i] = façons d'atteindre marche i

  for (let i = 3; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp[n];
}

// Version optimisée O(1) espace
function monterEscalier(n) {
  if (n <= 2) return n;

  let prev2 = 1; // façons pour marche 1
  let prev1 = 2; // façons pour marche 2

  for (let i = 3; i <= n; i++) {
    const current = prev1 + prev2;
    prev2 = prev1;
    prev1 = current;
  }

  return prev1;
}

// Tests
console.log("Façons de monter l'escalier:");
console.log(`  3 marches: ${monterEscalier(3)}`); // 3
console.log(`  5 marches: ${monterEscalier(5)}`); // 8
console.log(`  10 marches: ${monterEscalier(10)}`); // 89

// Détail pour n=3:
// (1+1+1), (1+2), (2+1) = 3 façons ✓
```

**Explication :**

- C'est exactement Fibonacci décalé ! ways(n) = fib(n+1)
- Pour atteindre la marche n, on vient soit de n-1 (1 pas) soit de n-2 (2 pas)
- Donc ways(n) = ways(n-1) + ways(n-2)

</details>

---

## 📝 Micro-Exercice 4 : Choisir le Bon Paradigme

**Objectif :** Pour chaque problème, identifier le paradigme approprié.

| Problème                                                   | Paradigme | Justification |
| ---------------------------------------------------------- | --------- | ------------- |
| Trouver un élément dans un tableau trié                    | ?         | ?             |
| Rendre la monnaie avec minimum de pièces (système inconnu) | ?         | ?             |
| Sélectionner le maximum de réunions sans chevauchement     | ?         | ?             |
| Calculer le n-ième nombre de Fibonacci                     | ?         | ?             |
| Trier un million d'éléments                                | ?         | ?             |

<details>
<summary>💡 Voir la solution</summary>

| Problème                                 | Paradigme                   | Justification                                                      |
| ---------------------------------------- | --------------------------- | ------------------------------------------------------------------ |
| Trouver un élément dans un tableau trié  | **Diviser pour Régner**     | Recherche binaire O(log n)                                         |
| Rendre la monnaie avec minimum de pièces | **Programmation Dynamique** | Sous-problèmes chevauchants, système potentiellement non-canonique |
| Maximum de réunions sans chevauchement   | **Glouton**                 | Propriété du choix glouton prouvée (trier par fin)                 |
| N-ième Fibonacci                         | **Programmation Dynamique** | Sous-problèmes chevauchants évidents                               |
| Trier un million d'éléments              | **Diviser pour Régner**     | Merge Sort O(n log n) stable et prévisible                         |

</details>

---

## 📊 Tableau Récapitulatif des Complexités

| Paradigme               | Algorithme Typique        | Temps          | Espace   | Quand l'utiliser        |
| ----------------------- | ------------------------- | -------------- | -------- | ----------------------- |
| **Diviser pour Régner** | Merge Sort                | O(n log n)     | O(n)     | Problème décomposable   |
|                         | Quick Sort                | O(n log n) moy | O(log n) | Tri in-place            |
|                         | Recherche Binaire         | O(log n)       | O(1)     | Recherche dans trié     |
| **Glouton**             | Rendu monnaie (canonique) | O(n)           | O(1)     | Choix local = optimal   |
|                         | Sélection activités       | O(n log n)     | O(1)     | Maximiser quantité      |
|                         | Huffman                   | O(n log n)     | O(n)     | Compression             |
| **Prog. Dynamique**     | Fibonacci                 | O(n)           | O(1)     | Sous-pb chevauchants    |
|                         | Sac à dos 0/1             | O(nW)          | O(W)     | Optimisation contrainte |
|                         | Rendu monnaie (général)   | O(nM)          | O(M)     | Minimum de pièces       |

---

## 💪 Exercices Pratiques

### Exercice 1 : Maximum de Sous-Tableau (Kadane - DP)

Implémenter l'algorithme de Kadane pour trouver la somme maximale d'un sous-tableau contigu.

```javascript
function maxSousTableau(arr) {
  // Indice : dp[i] = max sous-tableau se terminant à i
  // TODO: Implémenter
}

// Tests
console.log(maxSousTableau([-2, 1, -3, 4, -1, 2, 1, -5, 4])); // 6 ([4,-1,2,1])
console.log(maxSousTableau([1, 2, 3, 4])); // 10 (tout le tableau)
console.log(maxSousTableau([-1, -2, -3])); // -1 (le moins négatif)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Algorithme de Kadane - Maximum Subarray
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(1)
 *
 * @param {number[]} arr - Tableau de nombres
 * @returns {number} - Somme maximale d'un sous-tableau contigu
 */
function maxSousTableau(arr) {
  if (arr.length === 0) return 0;

  let maxActuel = arr[0]; // Max du sous-tableau se terminant ici
  let maxGlobal = arr[0]; // Max trouvé jusqu'à présent

  for (let i = 1; i < arr.length; i++) {
    // Soit on étend le sous-tableau précédent, soit on recommence ici
    maxActuel = Math.max(arr[i], maxActuel + arr[i]);
    maxGlobal = Math.max(maxGlobal, maxActuel);
  }

  return maxGlobal;
}

// Tests
console.log(maxSousTableau([-2, 1, -3, 4, -1, 2, 1, -5, 4])); // 6
console.log(maxSousTableau([1, 2, 3, 4])); // 10
console.log(maxSousTableau([-1, -2, -3])); // -1
```

</details>

---

### Exercice 2 : Puissance Rapide (Diviser pour Régner)

Calculer x^n en O(log n) au lieu de O(n).

```javascript
function puissanceRapide(x, n) {
  // Indice : x^n = (x^(n/2))^2 si n pair
  //          x^n = x * (x^((n-1)/2))^2 si n impair
  // TODO: Implémenter
}

// Tests
console.log(puissanceRapide(2, 10)); // 1024
console.log(puissanceRapide(3, 5)); // 243
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Exponentiation rapide - Diviser pour Régner
 * Complexité temporelle : O(log n)
 * Complexité spatiale : O(log n) récursif, O(1) itératif
 *
 * @param {number} x - Base
 * @param {number} n - Exposant (entier >= 0)
 * @returns {number} - x^n
 */
function puissanceRapide(x, n) {
  // Cas de base
  if (n === 0) return 1;
  if (n === 1) return x;

  // Diviser : calculer x^(n/2)
  const moitie = puissanceRapide(x, Math.floor(n / 2));

  // Combiner
  if (n % 2 === 0) {
    return moitie * moitie; // x^n = (x^(n/2))^2
  } else {
    return moitie * moitie * x; // x^n = x * (x^(n/2))^2
  }
}

// Tests
console.log(puissanceRapide(2, 10)); // 1024
console.log(puissanceRapide(3, 5)); // 243
console.log(puissanceRapide(2, 0)); // 1
console.log(puissanceRapide(5, 3)); // 125
```

</details>

---

### Exercice 3 : Problème du Sac à Dos 0/1 (DP)

```javascript
function sacADos01(capacite, objets) {
  // objets = [{poids, valeur}, ...]
  // Contrairement au fractionnaire, on prend l'objet entier ou pas du tout
  // TODO: Implémenter avec tabulation
}

// Test
const objets = [
  { poids: 2, valeur: 3 },
  { poids: 3, valeur: 4 },
  { poids: 4, valeur: 5 },
  { poids: 5, valeur: 6 },
];
console.log(sacADos01(8, objets)); // Devrait retourner 10
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Sac à dos 0/1 - Programmation Dynamique
 * Complexité temporelle : O(n × W) où W = capacité
 * Complexité spatiale : O(n × W), optimisable à O(W)
 *
 * @param {number} capacite - Capacité maximale
 * @param {Array<{poids: number, valeur: number}>} objets
 * @returns {number} - Valeur maximale atteignable
 */
function sacADos01(capacite, objets) {
  const n = objets.length;

  // dp[i][w] = valeur max avec les i premiers objets et capacité w
  const dp = Array(n + 1)
    .fill(null)
    .map(() => Array(capacite + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    const { poids, valeur } = objets[i - 1];

    for (let w = 0; w <= capacite; w++) {
      // Ne pas prendre l'objet i
      dp[i][w] = dp[i - 1][w];

      // Prendre l'objet i (si possible)
      if (poids <= w) {
        dp[i][w] = Math.max(dp[i][w], dp[i - 1][w - poids] + valeur);
      }
    }
  }

  return dp[n][capacite];
}

// Test
const objets = [
  { poids: 2, valeur: 3 },
  { poids: 3, valeur: 4 },
  { poids: 4, valeur: 5 },
  { poids: 5, valeur: 6 },
];
console.log(sacADos01(8, objets)); // 10 (objets de poids 3 et 5)
```

</details>

---

### Exercice 4 : Déterminer le Paradigme

Pour chaque problème, déterminez le meilleur paradigme et justifiez :

1. **Trouver le chemin le plus court dans un graphe pondéré**
2. **Compter le nombre de chemins dans une grille (haut-gauche vers bas-droite)**
3. **Compresser un texte avec des codes de longueur variable**
4. **Inverser une liste chaînée**

<details>
<summary>💡 Voir la solution</summary>

1. **Chemin le plus court** → **Glouton (Dijkstra)** si poids positifs, ou **DP (Bellman-Ford)** si poids négatifs
   - Dijkstra : choix glouton du sommet le plus proche

2. **Nombre de chemins dans grille** → **Programmation Dynamique**
   - Sous-problèmes chevauchants : paths(i,j) = paths(i-1,j) + paths(i,j-1)
   - Complexité O(m×n)

3. **Compression avec codes variables** → **Glouton (Huffman)**
   - Propriété du choix glouton : fusionner les symboles les moins fréquents

4. **Inverser une liste chaînée** → **Aucun des trois** (simple itération O(n))
   - Ce n'est pas un problème d'optimisation, juste une manipulation de pointeurs

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la complexité temporelle de la recherche binaire ?**

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(log n)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : C. O(log n)**

À chaque étape, on divise l'espace de recherche par 2. Pour n éléments, il faut log₂(n) divisions maximum.

</details>

---

### Question 2

**Quelles sont les deux propriétés nécessaires pour appliquer la Programmation Dynamique ?**

- [ ] A. Sous-problèmes chevauchants uniquement
- [ ] B. Sous-structure optimale uniquement
- [ ] C. Sous-problèmes chevauchants ET sous-structure optimale
- [ ] D. Propriété du choix glouton

<details>
<summary>Voir la réponse</summary>

**Réponse : C. Sous-problèmes chevauchants ET sous-structure optimale**

- **Sous-problèmes chevauchants** : Les mêmes sous-problèmes sont calculés plusieurs fois
- **Sous-structure optimale** : La solution optimale contient des solutions optimales de sous-problèmes

Sans les deux, la DP n'est pas applicable ou pas efficace.

</details>

---

### Question 3

**Pour le système de pièces [1, 3, 4], quel paradigme donne le nombre minimum de pièces pour rendre 6 centimes ?**

- [ ] A. Glouton (donne 2 pièces)
- [ ] B. Glouton (donne 3 pièces)
- [ ] C. Programmation Dynamique (donne 2 pièces)
- [ ] D. Diviser pour Régner

<details>
<summary>Voir la réponse</summary>

**Réponse : C. Programmation Dynamique (donne 2 pièces)**

- **Glouton** : 4 + 1 + 1 = 3 pièces (choix local mais pas optimal)
- **DP** : 3 + 3 = 2 pièces (explore toutes les possibilités)

Le système [1, 3, 4] n'est pas canonique, donc le glouton échoue.

</details>

---

### Question 4

**Quelle est la différence principale entre mémoïsation et tabulation ?**

- [ ] A. Mémoïsation est plus rapide
- [ ] B. Tabulation utilise moins de mémoire
- [ ] C. Mémoïsation est top-down (récursif), tabulation est bottom-up (itératif)
- [ ] D. Tabulation ne peut pas résoudre tous les problèmes DP

<details>
<summary>Voir la réponse</summary>

**Réponse : C. Mémoïsation est top-down (récursif), tabulation est bottom-up (itératif)**

- **Mémoïsation** : Commence par le problème principal, résout les sous-problèmes à la demande (récursif + cache)
- **Tabulation** : Résout d'abord les plus petits sous-problèmes, puis construit vers le problème principal (itératif + table)

Les deux ont la même complexité temporelle, mais des compromis différents (pile vs mémoire).

</details>

---

### Question 5

**Pour le tri fusion (Merge Sort), quelle étape a la complexité O(n) ?**

- [ ] A. Diviser le tableau en deux
- [ ] B. Fusionner deux tableaux triés
- [ ] C. Les deux
- [ ] D. Aucune

<details>
<summary>Voir la réponse</summary>

**Réponse : B. Fusionner deux tableaux triés**

- **Diviser** : O(1) - juste calculer l'index du milieu
- **Fusionner** : O(n) - parcourir tous les éléments des deux moitiés

La complexité totale O(n log n) vient de : log(n) niveaux de récursion × O(n) fusion par niveau.

</details>

---

### Question 6

**Quel algorithme utilise le principe "toujours prendre la pièce de plus grande valeur possible" ?**

- [ ] A. Programmation Dynamique
- [ ] B. Diviser pour Régner
- [ ] C. Algorithme Glouton
- [ ] D. Recherche exhaustive

<details>
<summary>Voir la réponse</summary>

**Réponse : C. Algorithme Glouton**

Le principe de prendre "le meilleur choix local à chaque étape" est la définition même d'un algorithme glouton. Pour le rendu de monnaie, on prend la plus grande pièce possible tant qu'elle ne dépasse pas le montant restant.

</details>

---

### Question 7

**Quelle est la complexité spatiale optimisée pour calculer Fibonacci(n) ?**

- [ ] A. O(n²)
- [ ] B. O(n)
- [ ] C. O(log n)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : D. O(1)**

On n'a besoin que des deux valeurs précédentes :

```javascript
let prev2 = 0,
  prev1 = 1;
for (let i = 2; i <= n; i++) {
  const current = prev1 + prev2;
  prev2 = prev1;
  prev1 = current;
}
```

Cela donne O(n) en temps et O(1) en espace.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Diviser pour Régner

Décomposer un problème en sous-problèmes **indépendants**, les résoudre récursivement, puis combiner. Complexité typique **O(n log n)**. Exemples : Merge Sort, Quick Sort, Recherche Binaire.

### 2. Algorithmes Gloutons

Faire le **choix localement optimal** à chaque étape. Rapide **O(n)** ou **O(n log n)** mais ne garantit pas toujours l'optimalité globale. Vérifier la **propriété du choix glouton** avant d'utiliser.

### 3. Programmation Dynamique

Stocker les solutions de **sous-problèmes chevauchants** pour éviter les recalculs. Transforme **O(2ⁿ)** en **O(n)** ou **O(n²)**. Deux approches : mémoïsation (top-down) et tabulation (bottom-up).

### 4. Analyse Big O Systématique

Chaque algorithme doit être accompagné de son analyse de complexité temporelle ET spatiale. C'est le critère principal de comparaison et de choix.

### 5. Conditions d'Application

- **Diviser pour Régner** : Problème décomposable en sous-problèmes similaires
- **Glouton** : Propriété du choix glouton + sous-structure optimale
- **DP** : Sous-problèmes chevauchants + sous-structure optimale

### 6. Pièges Classiques

Le glouton peut échouer (systèmes non-canoniques). La DP sans optimisation d'espace peut dépasser la mémoire. Diviser pour Régner avec mauvais pivot (Quick Sort) peut devenir O(n²).

### 7. Choisir le Bon Paradigme

Analysez d'abord le problème : indépendance des sous-problèmes → Diviser pour Régner. Choix local optimal → Glouton. Sous-problèmes qui se répètent → DP. Le bon choix transforme un problème "impossible" en solution élégante.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez désormais les trois paradigmes fondamentaux de conception d'algorithmes.

### Ce que vous avez appris aujourd'hui

- Les trois stratégies : Diviser pour Régner, Glouton, Programmation Dynamique
- L'analyse Big O de chaque approche
- Les conditions d'application et les pièges à éviter
- Comment choisir le bon paradigme selon le problème

### Compétences acquises

Vous êtes maintenant capable de :

- Analyser un problème et identifier le paradigme approprié
- Implémenter chaque paradigme en JavaScript avec les bonnes complexités
- Reconnaître quand un glouton va échouer et utiliser la DP à la place

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Ces paradigmes sont la base de 90% des algorithmes que vous rencontrerez en entretien technique et en production. Les maîtriser, c'est avoir une boîte à outils mentale pour résoudre presque n'importe quel problème algorithmique.

---

## ➡️ Prochaine Étape : Leçon 38

### Ce qui vous attend

Dans la prochaine leçon, **« Patterns Courants de Résolution de Problèmes Algorithmiques »**, vous allez découvrir les schémas de pensée les plus utilisés pour résoudre efficacement des problèmes.

**Vous découvrirez :**

- Le pattern **Deux Pointeurs** (Two-Pointer) - O(n) au lieu de O(n²)
- Le pattern **Fenêtre Glissante** (Sliding Window) - sous-tableaux en O(n)
- Le pattern **Fast & Slow Pointers** - détection de cycles en O(1) espace
- Le pattern **Fusion d'Intervalles** - planification optimale

### Préparez-vous !

Ces patterns sont complémentaires aux paradigmes. Tandis que les paradigmes vous disent **comment penser**, les patterns vous donnent des **recettes prêtes à l'emploi** pour des problèmes récurrents.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [MIT OpenCourseWare - Introduction to Algorithms](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) - Cours universitaire complet
- [Wikipedia - Diviser pour régner](<https://fr.wikipedia.org/wiki/Diviser_pour_r%C3%A9gner_(informatique)>) - Référence théorique
- [Visualgo - Sorting Algorithms](https://visualgo.net/en/sorting) - Visualisation interactive

### Outils de pratique

- **[LeetCode](https://leetcode.com/)** : Filtrer par tag "Dynamic Programming", "Greedy", "Divide and Conquer"
- **[HackerRank](https://www.hackerrank.com/domains/algorithms)** : Exercices classés par paradigme

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices avec des valeurs différentes
- Implémenter le même problème avec différents paradigmes pour comparer

> 💡 **Conseil**
>
> La meilleure façon de maîtriser ces paradigmes est de **résoudre des problèmes**. Commencez par identifier le paradigme avant de coder. Avec le temps, vous reconnaîtrez instantanément quel pattern appliquer, comme un musicien reconnaît une gamme.

---

**Prêt pour la Leçon 38 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir les patterns de résolution de problèmes !

---

<div align="center">

**Leçon 37 sur 42 - Module 7 : Applications d'Algorithmes et Résolution de Problèmes**

[⬅️ Leçon 36 : Pratique - Résoudre un Problème Classique de Programmation Dynamique](../module-6/lecon-6-pratique-resoudre-probleme-classique-programmation-dynamique-fibonacci-sac-dos.md) | [Retour au sommaire](./README.md) | [Leçon 38 : Patterns Courants de Résolution de Problèmes Algorithmiques ➡️](./lecon-2-patterns-courants-resolution-problemes-algorithmiques.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
