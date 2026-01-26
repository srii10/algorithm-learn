##### Leçon 35 sur 42

# Tabulation : Programmation Dynamique Bottom-Up en JavaScript

**Module 6** : Paradigmes Avancés de Conception d'Algorithmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Expliquer le principe de la tabulation (bottom-up DP) et la distinguer de la mémoïsation (top-down DP)
- Construire et remplir un tableau (1D ou 2D) pour résoudre un problème de DP
- Implémenter des solutions tabulées pour des problèmes classiques (Fibonacci, rendu de monnaie, LCS...)
- Optimiser l'espace mémoire d'une solution tabulée quand c'est possible
- Identifier les cas où la tabulation est préférable à la mémoïsation
- Comprendre les limites et conditions d'application de la tabulation

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- Leçon 34 : Mémoïsation (top-down DP)
- Savoir manipuler les tableaux en JavaScript
- Comprendre les bases de la récursivité et des sous-problèmes
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Pourquoi la tabulation ?

Après avoir découvert la mémoïsation (top-down), il est temps d'explorer l'autre grand paradigme de la programmation dynamique : la **tabulation** (bottom-up). Cette approche consiste à construire la solution de façon itérative, en partant des cas les plus simples pour aller vers le problème global.

> **Point Clé**
>
> La tabulation permet d'éviter la récursivité et le risque de stack overflow, tout en offrant souvent de meilleures performances grâce à l'accès séquentiel en mémoire.

---

## 📦 Principe de la Tabulation

La tabulation repose sur une construction **itérative** : on remplit un tableau (souvent appelé `dp`) où chaque case correspond à un sous-problème. On commence par les cas de base, puis on "remonte" jusqu'à la solution globale.

### Différence fondamentale avec la mémoïsation

> **Question de réflexion**
>
> Quelle est la différence principale d'approche entre la tabulation (bottom-up DP) et la mémoïsation (top-down DP) ?

**Résumé** :

- Mémoïsation : on part du problème global, on descend récursivement, on mémorise au fur et à mesure (top-down)
- Tabulation : on part des cas de base, on construit la solution de bas en haut, sans récursion (bottom-up)

---

## 💻 Exemple 1 : Suite de Fibonacci (tabulation)

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

**Analyse :**

- On évite la récursivité et le cache est explicite
- On peut optimiser l'espace à O(1) car on n'a besoin que des deux dernières valeurs

> **Astuce optimisation mémoire**
>
> Comment la complexité spatiale d'une solution tabulée peut-elle parfois passer de O(N) à O(1) ?
>
> **Réponse** : Si chaque case ne dépend que d'un nombre fixe de précédentes (ex : Fibonacci dépend de i-1 et i-2), on peut ne garder que ces valeurs en mémoire.

---

## 📝 Micro-Exercice #2 : Optimiser Fibonacci en espace O(1)

**Objectif :** Réduire la complexité spatiale de Fibonacci à O(1).

**Instructions :** Modifie `fibonacciTabulation` pour utiliser seulement **deux variables** (prev et curr) au lieu d'un tableau complet.

**Signature** : `function fibonacciOptimise(n) { ... }`

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Fibonacci avec tabulation optimisée en espace O(1)
 *
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(1) - seulement 2 variables au lieu d'un tableau
 */
function fibonacciOptimise(n) {
  if (n <= 1) return n;

  let prev = 0; // dp[i-2]
  let curr = 1; // dp[i-1]

  for (let i = 2; i <= n; i++) {
    const next = prev + curr; // dp[i] = dp[i-1] + dp[i-2]
    prev = curr; // Décaler : i-2 devient i-1
    curr = next; // Décaler : i-1 devient i
  }

  return curr;
}

// Tests
console.log(fibonacciOptimise(10)); // 55
console.log(fibonacciOptimise(20)); // 6765
console.log(fibonacciOptimise(50)); // 12586269025
```

**Explication** :

- On ne garde que les **deux dernières valeurs** (prev et curr)
- À chaque itération, on calcule la suivante puis on décale
- **Gain** : de O(n) espace à O(1) espace, avec la même complexité temporelle O(n)

</details>

---

## 💻 Exemple 2 : Rendu de monnaie (minimum de pièces)

```javascript
function coinChangeTabulation(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  for (let i = 1; i <= amount; i++) {
    for (const coin of coins) {
      if (coin <= i) {
        dp[i] = Math.min(dp[i], 1 + dp[i - coin]);
      }
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
}
console.log(coinChangeTabulation([1, 2, 5], 11)); // 3
```

**Explication :**

- On construit la solution pour chaque montant de 1 à amount
- Chaque case dp[i] dépend des solutions pour les montants plus petits

---

## 📝 Micro-Exercice #3 : Tracer la table DP du rendu de monnaie

**Objectif :** Visualiser comment la table DP est construite pour le rendu de monnaie.

**Instructions :** Pour `coinChangeTabulation([1, 3, 4], 6)`, trace manuellement la table `dp` après chaque itération de `i` (montant). Identifie à quelle étape le minimum de pièces pour 6 est trouvé.

**Questions** :

1. Quelle est la valeur de `dp[6]` finalement ?
2. Quelle pièce a été utilisée en dernier pour atteindre 6 ?

<details>
<summary>💡 Voir la solution</summary>

**Table DP étape par étape** :

| i (montant)      | dp[0] | dp[1] | dp[2] | dp[3] | dp[4] | dp[5] | dp[6] | Explication          |
| ---------------- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | -------------------- |
| Init             | 0     | ∞     | ∞     | ∞     | ∞     | ∞     | ∞     | Montant 0 = 0 pièces |
| i=1 (coin=1)     | 0     | 1     | ∞     | ∞     | ∞     | ∞     | ∞     | 1 = une pièce de 1   |
| i=2 (coin=1)     | 0     | 1     | 2     | ∞     | ∞     | ∞     | ∞     | 2 = deux pièces de 1 |
| i=3 (coin=1,3)   | 0     | 1     | 2     | 1     | ∞     | ∞     | ∞     | 3 = une pièce de 3   |
| i=4 (coin=1,3,4) | 0     | 1     | 2     | 1     | 1     | ∞     | ∞     | 4 = une pièce de 4   |
| i=5 (coin=1,3,4) | 0     | 1     | 2     | 1     | 1     | 2     | ∞     | 5 = 4+1 = 2 pièces   |
| i=6 (coin=1,3,4) | 0     | 1     | 2     | 1     | 1     | 2     | 2     | 6 = 3+3 = 2 pièces   |

**Réponses** :

1. **dp[6] = 2** (minimum de 2 pièces)
2. **Pièces utilisées** : `[3, 3]` ou `[4, 1, 1]` (plusieurs solutions possibles avec 2 pièces minimum)

**Point clé** : La table se construit **incrémentalement**, chaque case utilisant les solutions des montants plus petits pour trouver l'optimum local.

</details>

---

## 💻 Exemple 3 : Plus longue sous-séquence commune (LCS)

```javascript
function lcsTabulation(text1, text2) {
  const m = text1.length;
  const n = text2.length;
  const dp = Array(m + 1)
    .fill(0)
    .map(() => Array(n + 1).fill(0));
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }
  return dp[m][n];
}
console.log(lcsTabulation("abcde", "ace")); // 3
```

---

## 📝 Micro-Exercice #1 : Visualiser la table DP

**Objectif :** Comprendre comment la table est remplie.

**Instructions :** Pour le problème du LCS, affiche la table dp après chaque itération principale (i) pour les chaînes "ab" et "acb".

<details>
<summary>💡 Voir la solution</summary>

La table se remplit ligne par ligne, chaque case dépendant de ses voisines à gauche, au-dessus et en diagonale.

</details>

---

## 💡 Quand préférer la tabulation à la mémoïsation ?

> **Question de réflexion**
>
> Quand la tabulation est-elle généralement préférable à la mémoïsation, et pourquoi ?

**Résumé** :

- Si la profondeur de récursion est trop grande (risque de stack overflow)
- Si on veut optimiser la performance (meilleure localité mémoire, moins d'appels de fonction)
- Si on veut facilement optimiser l'espace mémoire

---

## 💪 Exercices Pratiques

---

### Exercice 1 : Problème de l'escalier

**Objectif :** Compter le nombre de façons de monter un escalier de n marches (1 ou 2 à la fois).

**Instructions :** Implémente une solution tabulée pour ce problème. Indice : dp[i] = dp[i-1] + dp[i-2].

<details>
<summary>💡 Voir la solution</summary>

```javascript
function escalierTabulation(n) {
  if (n <= 1) return 1;
  const dp = new Array(n + 1);
  dp[0] = 1;
  dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
console.log(escalierTabulation(4)); // 5
```

</details>

---

### Exercice 2 : Coût minimal pour monter les marches

**Objectif :** Calculer le coût minimal pour atteindre le sommet d'un escalier avec un coût par marche.

**Instructions :** Implémente une solution tabulée pour ce problème. Indice : dp[i] = coût[i] + min(dp[i-1], dp[i-2]).

<details>
<summary>💡 Voir la solution</summary>

```javascript
function coutMinEscalier(cost) {
  const n = cost.length;
  const dp = new Array(n + 1);
  dp[0] = 0;
  dp[1] = 0;
  for (let i = 2; i <= n; i++) {
    dp[i] = Math.min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
  }
  return dp[n];
}
console.log(coutMinEscalier([10, 15, 20])); // 15
```

</details>

---

### Exercice 3 : Nombre de façons de rendre la monnaie (Coin Change II)

**Objectif :** Compter le nombre de combinaisons pour rendre un montant donné avec des pièces.

**Instructions :** Implémente une solution tabulée pour ce problème. Indice : dp[i] += dp[i - coin] pour chaque coin.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function nbFaconsMonnaie(amount, coins) {
  const dp = new Array(amount + 1).fill(0);
  dp[0] = 1;
  for (const coin of coins) {
    for (let i = coin; i <= amount; i++) {
      dp[i] += dp[i - coin];
    }
  }
  return dp[amount];
}
console.log(nbFaconsMonnaie(5, [1, 2, 5])); // 4
```

</details>

---

## 💡 Questions de réflexion et pièges courants

> **Peut-on appliquer la tabulation à des problèmes sans sous-structure optimale ou sous-problèmes chevauchants ?**
>
> Non : la tabulation (comme toute DP) ne fonctionne que si le problème possède ces deux propriétés. Sinon, il faut envisager d'autres approches (glouton, backtracking, etc.).

> **Optimisation mémoire avancée**
>
> Comment optimiser la complexité spatiale d'une solution tabulée de O(N) à O(1) ?
>
> **Réponse** : Si chaque case ne dépend que d'un nombre fixe de précédentes, on peut réutiliser quelques variables au lieu de tout le tableau (ex : Fibonacci, escalier).

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la différence principale entre tabulation et mémoïsation ?**

- [ ] A. Tabulation utilise la récursivité, mémoïsation non
- [ ] B. Tabulation construit la solution de bas en haut, mémoïsation de haut en bas
- [ ] C. Tabulation ne stocke rien, mémoïsation stocke tout
- [ ] D. Il n'y a aucune différence

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Tabulation = bottom-up, mémoïsation = top-down.

</details>

---

### Question 2

**Dans quel cas la tabulation est-elle préférable à la mémoïsation ?**

- [ ] A. Si la profondeur de récursion est trop grande
- [ ] B. Si on veut optimiser la mémoire
- [ ] C. Si on veut de meilleures performances
- [ ] D. Toutes les réponses

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

La tabulation est souvent préférable pour ces raisons.

</details>

---

### Question 3

**Comment peut-on parfois réduire l'espace mémoire d'une solution tabulée ?**

- [ ] A. En utilisant un Set
- [ ] B. En ne stockant que les valeurs nécessaires (O(1) au lieu de O(N))
- [ ] C. En supprimant la table dp
- [ ] D. En utilisant la récursivité

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

On peut réutiliser quelques variables si la dépendance est locale.

</details>

---

### Question 4

**La tabulation fonctionne-t-elle pour tous les problèmes ?**

- [ ] A. Oui
- [ ] B. Non, seulement si le problème a une sous-structure optimale et des sous-problèmes chevauchants

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Sinon, il faut d'autres techniques.

</details>

---

### Question 5

**Quelle est la complexité temporelle de `coinChangeTabulation([1, 2, 5], 11)` ?**

- [ ] A. O(n) où n = nombre de pièces
- [ ] B. O(amount)
- [ ] C. O(n × amount) où n = nombre de pièces
- [ ] D. O(amount²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

L'algorithme a **deux boucles imbriquées** :

- Boucle externe : parcourt tous les montants de 1 à `amount` → **O(amount)**
- Boucle interne : parcourt toutes les pièces → **O(n)**

**Total** : O(amount × n) où n = nombre de types de pièces

**Exemple** : Pour `amount = 11` et `[1, 2, 5]` (3 pièces), on fait 11 × 3 = 33 itérations.

</details>

---

### Question 6

**Pourquoi la tabulation est-elle préférable à la mémoïsation pour éviter le stack overflow ?**

- [ ] A. Parce qu'elle utilise moins de mémoire
- [ ] B. Parce qu'elle n'utilise pas de récursion
- [ ] C. Parce qu'elle est plus rapide
- [ ] D. Parce qu'elle est plus facile à coder

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La tabulation utilise une **approche itérative** (boucles for) au lieu de la **récursion**. Cela évite d'empiler des appels de fonction qui peuvent causer un **stack overflow** pour de grandes valeurs de n.

**Exemple** :

- **Mémoïsation** : `fib(10000)` → stack overflow (trop d'appels récursifs empilés)
- **Tabulation** : `fibTabulation(10000)` → fonctionne sans problème (simple boucle for)

**Avantage supplémentaire** : Meilleure localité mémoire (accès séquentiel au tableau) = plus efficace pour le CPU.

</details>

---

### Question 7

**Comment optimiser l'espace d'un problème de tabulation 1D (comme Fibonacci) ?**

- [ ] A. Utiliser un tableau plus petit
- [ ] B. Ne garder que les k dernières valeurs nécessaires
- [ ] C. Utiliser des nombres plus petits
- [ ] D. Utiliser la récursion à la place

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Si chaque case `dp[i]` ne dépend que d'un **nombre fixe k de cases précédentes**, on peut ne garder que ces k valeurs au lieu de tout le tableau.

**Exemples** :

- **Fibonacci** : `dp[i] = dp[i-1] + dp[i-2]` → garder seulement 2 valeurs → **O(n) → O(1)**
- **Escalier** : `dp[i] = dp[i-1] + dp[i-2]` → garder seulement 2 valeurs → **O(n) → O(1)**
- **Coin Change** : `dp[i]` dépend de plusieurs `dp[i-coin]` → difficile à optimiser, rester en O(amount)

**Pattern général** : Si dépendance locale (i-1, i-2, etc.), on peut souvent optimiser à O(1) ou O(k).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Tabulation = bottom-up, mémoïsation = top-down

### 2. On construit la solution itérativement, sans récursivité

### 3. On peut optimiser l'espace mémoire dans certains cas

### 4. La tabulation évite le stack overflow

### 5. Elle est idéale pour les problèmes à sous-structure optimale et sous-problèmes chevauchants

### 6. On peut traiter des problèmes 1D (Fibonacci), 2D (LCS), etc.

### 7. Bien choisir entre tabulation et mémoïsation selon le contexte

---

## 🎓 Conclusion

**Félicitations !** 🎉 Tu sais maintenant implémenter la programmation dynamique par tabulation, et tu comprends quand et comment l'utiliser !

### Ce que tu as appris aujourd'hui

- Le principe de la tabulation
- L'implémentation concrète en JavaScript
- Les cas d'usage, optimisations et limites

### Compétences acquises

Tu es maintenant capable de :

- Résoudre des problèmes de DP en bottom-up
- Optimiser l'espace mémoire quand c'est possible
- Choisir la bonne approche selon le problème

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La tabulation est un outil fondamental pour résoudre efficacement de nombreux problèmes d'optimisation, et une compétence clé pour tout développeur d'algorithmes !

---

## ➡️ Prochaine Étape : Leçon 36

### Ce qui t'attend

La prochaine leçon, **« Pratique : Résoudre un Problème Classique de Programmation Dynamique (ex. : Fibonacci, Sac à Dos) »**, t'apprendra à appliquer la mémoïsation et la tabulation sur des problèmes concrets.

**Tu découvriras :**

- Comment choisir la bonne approche
- Des exemples détaillés (sac à dos, LIS, etc.)
- Les pièges à éviter et les bonnes pratiques

### Prépare-toi !

Tu vas consolider ta maîtrise de la programmation dynamique.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Wikipedia - Programmation dynamique](https://fr.wikipedia.org/wiki/Programmation_dynamique)
- [MIT OpenCourseWare - Dynamic Programming](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/resources/lecture-19-dynamic-programming-i/)
- [JavaScript.info - Tableaux et algorithmes](https://javascript.info/array)

### Outils de pratique

- **[LeetCode - Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)** : Problèmes classiques

---

## 💬 Feedback et Questions

Tu as des questions sur cette leçon ? Un doute sur la tabulation ?

N'hésite pas à :

- Relire les exemples et exercices
- Tester les codes dans ta console
- Demander de l'aide sur le forum du cours

> 💡 **Conseil**
>
> Prends le temps de bien comprendre la construction de la table DP et d'expérimenter sur différents problèmes : c'est la clé pour progresser !

---

**Prêt pour la Leçon 36 ?** 🚀

Rendez-vous dans la prochaine leçon pour mettre en pratique la programmation dynamique !

---

<div align="center">

**Leçon 35 sur 42 - Module 6 : Paradigmes Avancés de Conception d'Algorithmes**

[⬅️ Leçon 34 : Mémoïsation : Programmation Dynamique Top-Down en JavaScript](./lecon-4-memoisation-programmation-dynamique-top-down-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 36 : Pratique : Résoudre un Problème Classique de Programmation Dynamique ➡️](./lecon-6-pratique-resoudre-probleme-classique-programmation-dynamique-fibonacci-sac-dos.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
