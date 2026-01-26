##### Leçon 36 sur 42

# Pratique : Résoudre un Problème Classique de Programmation Dynamique (ex. : Fibonacci, Sac à Dos)

**Module 6** : Paradigmes Avancés de Conception d'Algorithmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Appliquer la programmation dynamique (mémoïsation et tabulation) à des problèmes classiques
- Comparer les approches naïve, mémoïsation et tabulation sur Fibonacci
- Résoudre le problème du sac à dos 0/1 avec une table DP et l'optimiser en espace
- Analyser les compromis temps/espace des différentes approches
- Comprendre les limites des approches gloutonnes pour le sac à dos
- Identifier les cas où la DP est la meilleure solution

---

### ⏱️ Durée estimée : 2h

---

## 📚 Prérequis

- Comprendre la récursivité et les sous-problèmes
- Savoir manipuler les tableaux en JavaScript
- Avoir suivi les leçons sur la mémoïsation et la tabulation

---

## 🚀 Introduction

La programmation dynamique (DP) est une technique puissante pour résoudre des problèmes d'optimisation en les décomposant en sous-problèmes qui se recoupent. Après avoir étudié la théorie, passons à la pratique sur deux classiques : la suite de Fibonacci et le sac à dos 0/1.

> **Point Clé**
>
> La programmation dynamique brille sur des problèmes avec **sous-problèmes chevauchants** et **sous-structure optimale**. Pour chaque problème, on peut choisir entre **mémoïsation** (top-down, récursif avec cache) et **tabulation** (bottom-up, itératif). Le bon choix dépend du contexte : mémoïsation pour la simplicité et le calcul partiel, tabulation pour éviter la récursion et optimiser l'espace.

---

## 🧩 Problème 1 : Suite de Fibonacci

La suite de Fibonacci commence par 0 et 1, puis chaque nombre est la somme des deux précédents : 0, 1, 1, 2, 3, 5, 8, 13...

### 1️ Approche naïve (récursive)

```javascript
function fibonacciNaive(n) {
  if (n <= 1) return n;
  return fibonacciNaive(n - 1) + fibonacciNaive(n - 2);
}
console.log(fibonacciNaive(6)); // 8
```

> **Complexité** : O(2^n) (beaucoup de calculs redondants)

---

### 2️ Mémoïsation (Top-Down DP)

```javascript
function fibonacciMemoization(n) {
  const memo = new Array(n + 1).fill(-1);
  function calculate(k) {
    if (k <= 1) return k;
    if (memo[k] !== -1) return memo[k];
    memo[k] = calculate(k - 1) + calculate(k - 2);
    return memo[k];
  }
  return calculate(n);
}
console.log(fibonacciMemoization(10)); // 55
```

> 💡 **Astuce** : On évite les recalculs, complexité O(n)

---

### 3️ Tabulation (Bottom-Up DP)

```javascript
function fibonacciTabulation(n) {
  if (n <= 1) return n;
  const dp = new Array(n + 1);
  dp[0] = 0;
  dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
console.log(fibonacciTabulation(10)); // 55
```

> **Optimisation mémoire** :
>
> On peut réduire l'espace à O(1) en ne gardant que les deux dernières valeurs.

---

## 📝 Micro-Exercice #1 : Comparer les performances de Fibonacci

**Objectif :** Mesurer empiriquement la différence de performance entre les 3 approches.

**Instructions :** Implémente une fonction `comparerFibonacci(n)` qui mesure le temps d'exécution des 3 versions (naïve, mémoïsation, tabulation) pour `n = 35` et affiche les résultats.

**Astuce** : Utilise `console.time()` et `console.timeEnd()` pour mesurer le temps.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function comparerFibonacci(n) {
  console.log(`\n=== Comparaison Fibonacci(${n}) ===\n`);

  // Naïve (attention : très lent pour n > 40)
  console.time("Naïve");
  const resNaive = fibonacciNaive(n);
  console.timeEnd("Naïve");
  console.log(`Résultat naïve: ${resNaive}`);

  // Mémoïsation
  console.time("Mémoïsation");
  const resMemo = fibonacciMemoization(n);
  console.timeEnd("Mémoïsation");
  console.log(`Résultat mémoïsation: ${resMemo}`);

  // Tabulation
  console.time("Tabulation");
  const resTab = fibonacciTabulation(n);
  console.timeEnd("Tabulation");
  console.log(`Résultat tabulation: ${resTab}`);
}

// Tester
comparerFibonacci(35);

/* Résultats typiques :
Naïve: ~1500ms (varie selon la machine)
Mémoïsation: ~1ms
Tabulation: ~0.5ms

Gain : Mémoïsation et Tabulation sont ~1500x plus rapides !
*/
```

**Observations** :

- **Naïve** : Exponentiel O(2^n) → devient inutilisable au-delà de n=40
- **Mémoïsation** : Linéaire O(n) → rapide mais utilise la pile d'appels
- **Tabulation** : Linéaire O(n) → souvent le plus rapide grâce à la localité mémoire

</details>

---

## ❓ Choisir entre mémoïsation et tabulation ?

> **Question**
>
> Comment décider d'utiliser la mémoïsation ou la tabulation pour un problème de DP donné ?
>
> **Réponse** :
>
> - Si la structure du problème se prête à une construction itérative (bottom-up), la tabulation est souvent plus efficace (meilleure localité mémoire, pas de stack overflow).
> - Si la solution naturelle est récursive et que la profondeur d'appel n'est pas un problème, la mémoïsation est plus simple à implémenter.
> - Pour les problèmes où l'ordre de calcul importe (ex : reconstruction de solution), la tabulation peut être préférable.

---

## 🧩 Problème 2 : Sac à dos 0/1 (Knapsack)

**Énoncé** : On dispose d'un sac de capacité W et de n objets (poids et valeurs). Chaque objet peut être pris ou non (pas de fractions). Trouver la valeur maximale transportable.

### 1️ Tabulation (table DP 2D)

```javascript
function knapsack01(weights, values, W) {
  const n = weights.length;
  const dp = Array(n + 1)
    .fill(0)
    .map(() => Array(W + 1).fill(0));
  for (let i = 1; i <= n; i++) {
    for (let w = 1; w <= W; w++) {
      const wi = weights[i - 1],
        vi = values[i - 1];
      if (wi > w) {
        dp[i][w] = dp[i - 1][w];
      } else {
        dp[i][w] = Math.max(dp[i - 1][w], vi + dp[i - 1][w - wi]);
      }
    }
  }
  return dp[n][W];
}
console.log(knapsack01([1, 3, 4, 5], [1, 4, 5, 7], 7)); // 9
```

---

### 2️ Optimisation mémoire (table 1D)

```javascript
function knapsack01SpaceOptimized(weights, values, W) {
  const n = weights.length;
  const dp = Array(W + 1).fill(0);
  for (let i = 0; i < n; i++) {
    const wi = weights[i],
      vi = values[i];
    for (let w = W; w >= wi; w--) {
      dp[w] = Math.max(dp[w], vi + dp[w - wi]);
    }
  }
  return dp[W];
}
console.log(knapsack01SpaceOptimized([1, 3, 4, 5], [1, 4, 5, 7], 7)); // 9
```

---

## 📝 Micro-Exercice #2 : Tracer la table DP du sac à dos

**Objectif :** Comprendre le remplissage de la table DP en traçant manuellement un exemple simple.

**Instructions :** Pour les objets suivants et une capacité W=5 :

- Objet 0 : poids=2, valeur=3
- Objet 1 : poids=3, valeur=4
- Objet 2 : poids=4, valeur=5

Trace la table DP `dp[i][w]` où `i` représente les objets considérés (0 à 3) et `w` la capacité (0 à 5).

**Astuce** : Utilise la formule `dp[i][w] = Math.max(dp[i-1][w], valeur[i-1] + dp[i-1][w-poids[i-1]])` si `poids[i-1] <= w`, sinon `dp[i][w] = dp[i-1][w]`.

<details>
<summary>💡 Voir la solution</summary>

**Table DP complète :**

```
     w=0  w=1  w=2  w=3  w=4  w=5
i=0   0    0    0    0    0    0   (aucun objet)
i=1   0    0    3    3    3    3   (objet 0: p=2, v=3)
i=2   0    0    3    4    4    7   (objets 0-1: p=3, v=4)
i=3   0    0    3    4    5    7   (objets 0-2: p=4, v=5)
```

**Détail du remplissage** :

1. **Ligne i=0** : Aucun objet disponible → toutes les valeurs sont 0

2. **Ligne i=1** (objet 0: poids=2, valeur=3) :
   - w=0,1 : Capacité insuffisante → `dp[1][w] = dp[0][w] = 0`
   - w=2,3,4,5 : On peut prendre l'objet 0 → `dp[1][w] = max(dp[0][w], 3 + dp[0][w-2]) = max(0, 3) = 3`

3. **Ligne i=2** (objet 1: poids=3, valeur=4) :
   - w=0,1,2 : Capacité insuffisante → `dp[2][w] = dp[1][w]`
   - w=3 : `dp[2][3] = max(dp[1][3], 4 + dp[1][0]) = max(3, 4) = 4`
   - w=4 : `dp[2][4] = max(dp[1][4], 4 + dp[1][1]) = max(3, 4) = 4`
   - w=5 : `dp[2][5] = max(dp[1][5], 4 + dp[1][2]) = max(3, 4+3) = 7` ← Prendre objets 0 ET 1

4. **Ligne i=3** (objet 2: poids=4, valeur=5) :
   - w=0,1,2,3 : Capacité insuffisante → `dp[3][w] = dp[2][w]`
   - w=4 : `dp[3][4] = max(dp[2][4], 5 + dp[2][0]) = max(4, 5) = 5`
   - w=5 : `dp[3][5] = max(dp[2][5], 5 + dp[2][1]) = max(7, 5) = 7` ← Garder objets 0 ET 1

**Résultat final** : `dp[3][5] = 7` (valeur maximale = 7, en prenant les objets 0 et 1)

**Code pour vérification** :

```javascript
function knapsack01Debug(weights, values, W) {
  const n = weights.length;
  const dp = Array(n + 1)
    .fill(0)
    .map(() => Array(W + 1).fill(0));

  console.log("Table DP du sac à dos :");
  console.log(
    "Objets:",
    weights.map((w, i) => `(p=${w}, v=${values[i]})`).join(", "),
  );
  console.log("Capacité W =", W);
  console.log("");

  // Remplir la table
  for (let i = 1; i <= n; i++) {
    for (let w = 1; w <= W; w++) {
      const wi = weights[i - 1];
      const vi = values[i - 1];

      if (wi > w) {
        dp[i][w] = dp[i - 1][w];
      } else {
        dp[i][w] = Math.max(dp[i - 1][w], vi + dp[i - 1][w - wi]);
      }
    }
  }

  // Afficher la table
  console.log(
    "     ",
    Array.from({ length: W + 1 }, (_, i) => `w=${i}`).join("  "),
  );
  for (let i = 0; i <= n; i++) {
    console.log(
      `i=${i}  `,
      dp[i].map((v) => v.toString().padStart(3)).join("  "),
    );
  }

  console.log("\nValeur maximale:", dp[n][W]);
  return dp[n][W];
}

// Tester
knapsack01Debug([2, 3, 4], [3, 4, 5], 5); // 7
```

**Observations** :

- Chaque case `dp[i][w]` représente la **valeur maximale** pour les `i` premiers objets avec capacité `w`
- On construit la solution **de bas en haut** (bottom-up) en combinant les sous-problèmes
- La décision à chaque étape : **prendre ou ne pas prendre** l'objet courant

</details>

---

## ❓ Compromis temps/espace pour le sac à dos

> **Question**
>
> Quels sont les compromis spécifiques entre temps et espace dans les solutions mémoïsées et tabulées du sac à dos ?
>
> **Réponse** :
>
> - Les deux approches ont une complexité en temps O(nW) (n = objets, W = capacité).
> - La tabulation classique utilise O(nW) d'espace (table 2D), mais peut être optimisée à O(W) (table 1D).
> - La mémoïsation peut consommer plus de mémoire si tous les sous-problèmes sont explorés, mais parfois moins si certains états sont inaccessibles.

---

## ❓ Peut-on résoudre le sac à dos 0/1 avec une approche gloutonne ?

> **Question**
>
> Peut-on résoudre le problème du sac à dos 0/1 avec une approche gloutonne, et pourquoi ?
>
> **Réponse** :
> Non. L'approche gloutonne (prendre les objets au meilleur ratio valeur/poids) ne garantit pas l'optimalité pour le sac à dos 0/1. Il existe des cas où la solution optimale nécessite de ne pas prendre l'objet au meilleur ratio.

---

## ❓ Et si on pouvait prendre des fractions d'objets ? (Fractional Knapsack)

> **Question**
>
> Que se passe-t-il si on autorise les fractions d'objets (sac à dos fractionnaire) ? La DP reste-t-elle la meilleure solution ?
>
> **Réponse** :
> Dans ce cas, l'approche gloutonne (prendre d'abord les objets au meilleur ratio valeur/poids, même partiellement) donne toujours la solution optimale, en O(n log n). La DP n'est plus nécessaire.

---

## 💪 Exercices pratiques

### Exercice 1 : Fibonacci avec mémo objet

Modifie la fonction `fibonacciMemoization` pour utiliser un objet `memo` au lieu d'un tableau.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function fibonacciMemoizationObject(n, memo = {}) {
  if (n <= 1) return n;
  if (memo[n] !== undefined) return memo[n];
  memo[n] =
    fibonacciMemoizationObject(n - 1, memo) +
    fibonacciMemoizationObject(n - 2, memo);
  return memo[n];
}
console.log(fibonacciMemoizationObject(7)); // 13
```

</details>

---

### Exercice 2 : Sac à dos avec traçage des objets

Modifie la fonction du sac à dos pour afficher les objets sélectionnés.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function knapsack01WithItems(weights, values, W) {
  const n = weights.length;
  const dp = Array(n + 1)
    .fill(0)
    .map(() => Array(W + 1).fill(0));
  for (let i = 1; i <= n; i++) {
    const wi = weights[i - 1],
      vi = values[i - 1];
    for (let w = 1; w <= W; w++) {
      if (wi > w) {
        dp[i][w] = dp[i - 1][w];
      } else {
        dp[i][w] = Math.max(dp[i - 1][w], vi + dp[i - 1][w - wi]);
      }
    }
  }
  const items = [];
  let w = W,
    i = n;
  while (i > 0 && w > 0) {
    if (dp[i][w] !== dp[i - 1][w]) {
      items.push({
        poids: weights[i - 1],
        valeur: values[i - 1],
        index: i - 1,
      });
      w -= weights[i - 1];
    }
    i--;
  }
  console.log("Valeur max :", dp[n][W]);
  console.log("Objets sélectionnés :", items.reverse());
  return dp[n][W];
}
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Pourquoi la DP est-elle efficace pour Fibonacci et le sac à dos ?**

- [ ] A. Car il n'y a pas de sous-problèmes
- [ ] B. Car les sous-problèmes se recoupent et la solution globale dépend de solutions optimales de sous-problèmes
- [ ] C. Car la DP est toujours la plus rapide

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

</details>

---

### Question 2

**Quelle est la complexité en temps de la solution tabulée du sac à dos 0/1 ?**

- [ ] A. O(n)
- [ ] B. O(W)
- [ ] C. O(nW)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

</details>

---

### Question 3

**L'approche gloutonne est-elle optimale pour le sac à dos 0/1 ?**

- [ ] A. Oui
- [ ] B. Non

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

</details>

---

### Question 4

**Comment peut-on optimiser la complexité spatiale du sac à dos de O(nW) à O(W) ?**

- [ ] A. En utilisant la récursion au lieu de la tabulation
- [ ] B. En utilisant une table 1D au lieu d'une table 2D et en parcourant w de droite à gauche
- [ ] C. En triant les objets par poids
- [ ] D. Ce n'est pas possible

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication** :

On peut optimiser l'espace en utilisant une **table 1D** `dp[w]` au lieu d'une table 2D `dp[i][w]`. L'astuce est de parcourir `w` **de droite à gauche** (de W vers 0) pour éviter d'utiliser des valeurs déjà mises à jour dans la même itération.

```javascript
// Table 2D : O(nW) en espace
const dp = Array(n + 1)
  .fill(0)
  .map(() => Array(W + 1).fill(0));

// Table 1D : O(W) en espace
const dp = Array(W + 1).fill(0);
for (let i = 0; i < n; i++) {
  // IMPORTANT : parcourir de droite à gauche
  for (let w = W; w >= weights[i]; w--) {
    dp[w] = Math.max(dp[w], values[i] + dp[w - weights[i]]);
  }
}
```

Le parcours **de droite à gauche** garantit qu'on utilise les valeurs de l'itération précédente (objet i-1) et non celles déjà mises à jour (objet i).

</details>

---

### Question 5

**Quelle différence pratique importante existe-t-il entre mémoïsation et tabulation pour de grandes valeurs de n ?**

- [ ] A. Aucune différence, elles ont la même complexité
- [ ] B. La mémoïsation peut causer un stack overflow, pas la tabulation
- [ ] C. La tabulation est toujours plus lente
- [ ] D. La mémoïsation utilise toujours moins de mémoire

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication** :

La **mémoïsation** utilise la récursion, ce qui empile les appels de fonction sur la pile d'appels (call stack). Pour de grandes valeurs de n (ex: Fibonacci(10000)), on risque un **stack overflow** (RangeError: Maximum call stack size exceeded).

La **tabulation** utilise des boucles itératives et ne dépend pas de la pile d'appels. Elle peut donc traiter des valeurs de n beaucoup plus grandes sans risque de stack overflow.

**Exemple** :

```javascript
// Mémoïsation : RISQUE de stack overflow pour n > ~10000
fibonacciMemoization(100000); // RangeError

// Tabulation : PAS de stack overflow
fibonacciTabulation(100000); // Fonctionne
```

**Autres différences** :

- **Localité mémoire** : La tabulation a souvent une meilleure localité mémoire (cache CPU)
- **Sous-problèmes calculés** : La mémoïsation ne calcule que les sous-problèmes nécessaires, la tabulation les calcule tous

</details>

---

### Question 6

**Pourquoi dit-on que la complexité O(nW) du sac à dos est "pseudo-polynomiale" ?**

- [ ] A. Parce que W peut être exponentiel par rapport à la taille de l'entrée
- [ ] B. Parce que l'algorithme n'est pas optimal
- [ ] C. Parce qu'on utilise un tableau
- [ ] D. C'est une erreur, la complexité est bien polynomiale

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

**Explication** :

La complexité O(nW) est dite **pseudo-polynomiale** car elle dépend de la **valeur numérique** de W, pas de sa **taille en bits**.

**Exemple concret** :

- Si W = 10, la complexité semble raisonnable : O(10n)
- Mais si W est encodé sur k bits, alors W peut aller jusqu'à 2^k
- Si W = 1 000 000 000 (encodé sur ~30 bits), alors O(nW) devient O(10^9 × n), ce qui est **exponentiel** par rapport à la taille de l'entrée (30 bits)

**Comparaison** :

| Complexité | Type               | Exemple                |
| ---------- | ------------------ | ---------------------- |
| **O(n)**   | Polynomiale vraie  | Parcours de tableau    |
| **O(nW)**  | Pseudo-polynomiale | Sac à dos avec W petit |
| **O(2^n)** | Exponentielle      | Fibonacci naïf         |

**Conséquence** : Le sac à dos 0/1 reste un problème **NP-complet**, même avec la programmation dynamique. L'algorithme DP est efficace en pratique pour des valeurs modérées de W, mais n'est pas polynomial au sens strict.

</details>

---

### Question 7

**Comment peut-on reconstruire la liste des objets sélectionnés dans le sac à dos après avoir rempli la table DP ?**

- [ ] A. C'est impossible sans recalculer tout
- [ ] B. En remontant dans la table DP depuis dp[n][W] et en vérifiant si la valeur a changé
- [ ] C. En triant les objets par valeur
- [ ] D. En gardant une deuxième table pour les choix

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

**Explication** :

On peut **reconstruire la solution** en remontant dans la table DP depuis `dp[n][W]` vers `dp[0][0]` en vérifiant si la valeur a changé par rapport à la ligne précédente.

**Algorithme de reconstruction** :

```javascript
function knapsackWithItems(weights, values, W) {
  const n = weights.length;
  const dp = Array(n + 1)
    .fill(0)
    .map(() => Array(W + 1).fill(0));

  // Remplir la table DP (comme d'habitude)
  for (let i = 1; i <= n; i++) {
    for (let w = 1; w <= W; w++) {
      if (weights[i - 1] > w) {
        dp[i][w] = dp[i - 1][w];
      } else {
        dp[i][w] = Math.max(
          dp[i - 1][w],
          values[i - 1] + dp[i - 1][w - weights[i - 1]],
        );
      }
    }
  }

  // Reconstruire la solution
  const items = [];
  let i = n;
  let w = W;

  while (i > 0 && w > 0) {
    // Si la valeur a changé, l'objet i-1 a été pris
    if (dp[i][w] !== dp[i - 1][w]) {
      items.push(i - 1); // Ajouter l'index de l'objet
      w -= weights[i - 1]; // Réduire la capacité
    }
    i--;
  }

  return {
    valeurMax: dp[n][W],
    objets: items.reverse(), // Inverser pour avoir l'ordre original
  };
}

// Tester
const result = knapsackWithItems([1, 3, 4, 5], [1, 4, 5, 7], 7);
console.log("Valeur max:", result.valeurMax); // 9
console.log("Objets sélectionnés:", result.objets); // [1, 2] (objets aux index 1 et 2)
```

**Principe** :

1. Si `dp[i][w] ≠ dp[i-1][w]`, alors l'objet i-1 a été **pris**
2. On soustrait le poids de cet objet de la capacité courante : `w -= weights[i-1]`
3. On remonte d'une ligne : `i--`
4. On répète jusqu'à `i = 0` ou `w = 0`

**Complexité** : O(n) pour la reconstruction, après O(nW) pour remplir la table.

</details>

---

## 📌 Récapitulatif en 7 points clés

### 1. La DP permet d'éviter les calculs redondants

### 2. Mémoïsation = top-down, tabulation = bottom-up

### 3. Les deux approches sont O(nW) pour le sac à dos

### 4. On peut optimiser l'espace à O(W) pour le sac à dos

### 5. L'approche gloutonne n'est pas optimale pour le sac à dos 0/1

### 6. Pour le sac à dos fractionnaire, le glouton est optimal

### 7. Savoir choisir la bonne approche selon le problème

---

## 🎓 Conclusion

Dans cette leçon, tu as appliqué la programmation dynamique à des problèmes concrets, comparé les approches, et compris les subtilités de chaque méthode. Tu es prêt à aborder des problèmes plus complexes !

---

## ➡️ Prochaine Étape : Leçon 37

### Ce qui vous attend

Dans la prochaine leçon, **« Révision des Stratégies de Conception d'Algorithmes »**, vous allez entamer le dernier module du cours avec une révision complète des paradigmes algorithmiques.

**Vous découvrirez :**

- Une révision approfondie de **Diviser pour Régner**, **Glouton** et **Programmation Dynamique**
- Comment choisir le bon paradigme selon le problème
- Les pièges et erreurs courantes à éviter
- Des critères de décision pour sélectionner la meilleure approche

### Préparez-vous !

Ce module final consolidera tous vos acquis et vous préparera à appliquer ces techniques à des problèmes réels. Vous avez maintenant toutes les bases nécessaires pour devenir un véritable expert en algorithmique !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [VisuAlgo - Knapsack](https://visualgo.net/en/dp) - Visualisation interactive du sac à dos
- [Wikipedia - Problème du sac à dos](https://fr.wikipedia.org/wiki/Probl%C3%A8me_du_sac_%C3%A0_dos) - Référence théorique
- [LeetCode - Dynamic Programming](https://leetcode.com/tag/dynamic-programming/) - Exercices pour pratiquer

### Outils utiles

- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez l'exécution pas à pas
- **[JS Bin](https://jsbin.com/)** : Testez vos implémentations en ligne

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec différentes valeurs de poids et capacités pour le sac à dos

> 💡 **Conseil**
>
> La programmation dynamique demande de la pratique pour être maîtrisée. Essayez de résoudre d'autres problèmes classiques comme le plus long sous-séquence commune (LCS) ou le problème de la découpe de tige. Chaque problème résolu renforce votre intuition pour reconnaître les patterns DP !

---

**Prêt pour la Leçon 37 ?** 🚀

Rendez-vous dans la prochaine leçon pour réviser les stratégies de conception d'algorithmes !

---

<div align="center">

**Leçon 36 sur 42 - Module 6 : Paradigmes Avancés de Conception d'Algorithmes**

[⬅️ Leçon 35 : Tabulation - Programmation Dynamique Bottom-Up en JavaScript](./lecon-5-tabulation-programmation-dynamique-bottom-up-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 37 : Révision des Stratégies de Conception d'Algorithmes ➡️](../module-7/lecon-1-revision-strategies-conception-algorithmes.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
