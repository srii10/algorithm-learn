##### Leçon 33 sur 42

# Programmation Dynamique : Sous-problèmes Chevauchants et Sous-structure Optimale

**Module 6** : Paradigmes Avancés de Conception d'Algorithmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Expliquer les notions de sous-problèmes chevauchants et de sous-structure optimale
- Identifier si un problème est adapté à la programmation dynamique
- Illustrer ces propriétés avec des exemples concrets (Fibonacci, rendu de monnaie, LIS...)
- Implémenter la mémoïsation (top-down) en JavaScript
- Analyser pourquoi certains problèmes ne sont pas adaptés à la programmation dynamique
- Préparer la transition vers la tabulation (bottom-up)

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- Leçon 31 : Principes des algorithmes gloutons
- Leçon 32 : Limites du glouton et introduction à la DP
- Savoir manipuler les fonctions et tableaux en JavaScript
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Pourquoi la Programmation Dynamique ?

Vous êtes-vous déjà demandé pourquoi certains algorithmes récursifs deviennent rapidement inefficaces ? Ou pourquoi, dans certains problèmes, la solution optimale semble pouvoir se construire à partir de solutions plus petites ?

La **programmation dynamique** (PD) est une technique qui permet de transformer des algorithmes inefficaces en solutions rapides et élégantes, à condition que le problème possède deux propriétés fondamentales :

- **Sous-problèmes chevauchants** : On recalcule souvent les mêmes sous-cas.
- **Sous-structure optimale** : La solution globale s'appuie sur des solutions optimales à des sous-problèmes.

Prenons l'exemple du calcul de la suite de Fibonacci :

```
fib(5)
├─ fib(4)
│  ├─ fib(3)
│  │  ├─ fib(2)
│  │  │  ├─ fib(1)
│  │  │  └─ fib(0)
│  │  └─ fib(1)
│  └─ fib(2)
│     ├─ fib(1)
│     └─ fib(0)
└─ fib(3)
  ├─ fib(2)
  │  ├─ fib(1)
  │  └─ fib(0)
  └─ fib(1)
```

On voit que `fib(2)` et `fib(1)` sont calculés plusieurs fois !

> **Point Clé**
>
> La programmation dynamique, c'est comme garder en mémoire les réponses déjà trouvées pour ne pas refaire le même travail inutilement. C'est la clé pour passer d'une solution exponentielle à une solution linéaire ou quadratique !

---

## 📦 Les deux piliers de la Programmation Dynamique

La PD n'est pas une baguette magique : elle ne fonctionne que si le problème possède **les deux propriétés suivantes**.

### 1. Sous-problèmes chevauchants

Un problème a des sous-problèmes chevauchants si, en le résolvant naïvement (souvent par récursion), on retombe plusieurs fois sur les mêmes calculs.

**Exemple 1 : Suite de Fibonacci**

```javascript
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
```

Pour `fib(5)`, on recalcule `fib(3)` et `fib(2)` plusieurs fois. Pour `fib(30)`, le nombre de calculs explose !

**Exemple 2 : Rendu de monnaie (minimum de pièces)**

Pour chaque montant, on essaie toutes les combinaisons : le nombre minimal de pièces pour 12 centimes avec [1, 5, 10] dépend du nombre minimal pour 11, 7, 2, etc. Ces sous-problèmes reviennent dans plusieurs branches.

**Exemple 3 : Binôme de Newton (C(n, k))**

La formule C(n, k) = C(n-1, k-1) + C(n-1, k) recalcule souvent les mêmes valeurs pour des n et k identiques.

**Exemple 4 : Tâches avec dépendances**

Si plusieurs tâches dépendent d'une même sous-tâche, son coût sera recalculé à chaque fois, sauf si on le mémorise.

---

### 2. Sous-structure optimale

Un problème possède une sous-structure optimale si la solution optimale globale peut être construite à partir de solutions optimales à ses sous-problèmes.

**Exemple : Plus court chemin dans un graphe acyclique**

Si le plus court chemin de S à D passe par X, alors le chemin S→X et X→D doivent eux-mêmes être les plus courts chemins pour leurs sous-problèmes respectifs.

**Exemple : Plus longue sous-suite croissante (LIS)**

Pour chaque position, la meilleure sous-suite croissante se construit à partir des meilleures sous-suites des positions précédentes.

**Contre-exemple : Chemin le plus long avec cycles**

La sous-structure optimale n'est pas garantie si on peut repasser plusieurs fois par le même sommet (cycle).

---

## 📝 Micro-Exercice #1 : Reconnaître les propriétés

**Objectif :** Identifier si un problème possède les deux propriétés nécessaires à la PD.

**Instructions :** Pour chaque problème ci-dessous, indiquez s'il possède :

1. Des sous-problèmes chevauchants
2. Une sous-structure optimale

- a) Calcul du n-ième terme de la suite de Fibonacci
- b) Recherche du plus court chemin dans un graphe sans cycle
- c) Recherche du plus long chemin dans un graphe avec cycles

<details>
<summary>💡 Voir la solution</summary>

- a) Oui (chevauchement) / Oui (sous-structure optimale)
- b) Oui (chevauchement si plusieurs chemins) / Oui (sous-structure optimale)
- c) Non (pas de sous-structure optimale à cause des cycles)

</details>

---

## 💻 Implémentation : Mémoïsation (Top-Down)

La **mémoïsation** consiste à stocker les résultats des sous-problèmes déjà calculés pour éviter de les recalculer. On parle de "top-down" car on part du problème global et on descend vers les sous-problèmes.

### Exemple 1 : Fibonacci avec mémoïsation

```javascript
const memo = {};
function fibonacciMemo(n) {
  if (n <= 1) return n;
  if (memo[n] !== undefined) return memo[n];
  memo[n] = fibonacciMemo(n - 1) + fibonacciMemo(n - 2);
  return memo[n];
}
console.log(fibonacciMemo(10)); // 55
```

**Analyse visuelle :**

Au lieu de recalculer `fib(3)` plusieurs fois, on le mémorise dès le premier calcul. Pour `fib(30)`, on passe de plus d'un million d'appels à seulement 30 !

**Exemple 2 : Minimum de pièces pour rendre la monnaie**

```javascript
function minPiecesMemo(montant, pieces, memo = {}) {
  if (montant === 0) return 0;
  if (montant < 0) return Infinity;
  if (memo[montant] !== undefined) return memo[montant];
  let min = Infinity;
  for (const p of pieces) {
    min = Math.min(min, 1 + minPiecesMemo(montant - p, pieces, memo));
  }
  memo[montant] = min;
  return min;
}
console.log(minPiecesMemo(12, [1, 5, 10])); // 3 (10+1+1)
```

**Exemple 3 : Binôme de Newton (C(n, k))**

```javascript
function binomeMemo(n, k, memo = {}) {
  const key = `${n},${k}`;
  if (k === 0 || k === n) return 1;
  if (memo[key] !== undefined) return memo[key];
  memo[key] = binomeMemo(n - 1, k - 1, memo) + binomeMemo(n - 1, k, memo);
  return memo[key];
}
console.log(binomeMemo(4, 2)); // 6
```

---

## 📝 Micro-Exercice #2 : Mémoïsation sur le rendu de monnaie

**Objectif :** Adapter la fonction de rendu de monnaie pour utiliser la mémoïsation.

**Instructions :** Implémentez une fonction `minPiecesMemo(montant, pieces, memo)` qui retourne le nombre minimal de pièces pour un montant donné, en utilisant un objet `memo` pour stocker les résultats intermédiaires.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function minPiecesMemo(montant, pieces, memo = {}) {
  if (montant === 0) return 0;
  if (montant < 0) return Infinity;
  if (memo[montant] !== undefined) return memo[montant];
  let min = Infinity;
  for (const p of pieces) {
    min = Math.min(min, 1 + minPiecesMemo(montant - p, pieces, memo));
  }
  memo[montant] = min;
  return min;
}
console.log(minPiecesMemo(12, [1, 5, 10])); // 3 (10+1+1)
```

</details>

---

## 💡 Application concrète : Gestion de dépendances de tâches

**Cas réel : Gestion de dépendances de tâches**

Supposons que tu dois réaliser la tâche A, qui dépend de B et C, et B dépend aussi de C. Si tu calcules le coût de C à chaque fois, tu perds du temps. Avec la PD, tu calcules le coût de C une seule fois et tu le réutilises pour B et A.

```javascript
const dependances = {
  A: ["B", "C"],
  B: ["C"],
  C: [],
};
const couts = { A: 3, B: 2, C: 1 };
function coutTotal(tache, memo = {}) {
  if (memo[tache] !== undefined) return memo[tache];
  let total = couts[tache];
  for (const dep of dependances[tache]) {
    total += coutTotal(dep, memo);
  }
  memo[tache] = total;
  return total;
}
console.log(coutTotal("A")); // 6 (A=3, B=2, C=1, C n'est compté qu'une fois)
```

---

## 📊 Comparaison : Mémoïsation vs Tabulation

| Approche    | Description                   | Avantages             | Inconvénients           |
| ----------- | ----------------------------- | --------------------- | ----------------------- |
| Mémoïsation | Top-down, récursif avec cache | Simple, naturel       | Stack overflow possible |
| Tabulation  | Bottom-up, itératif           | Pas de stack overflow | Parfois moins intuitif  |

---

## 📝 Micro-Exercice #3 : Analyse de la sous-structure optimale

**Objectif :** Vérifier si un problème possède la sous-structure optimale.

**Instructions :** Pour le problème de la plus longue sous-suite croissante (LIS), expliquez pourquoi la solution optimale globale dépend des solutions optimales aux sous-problèmes.

<details>
<summary>💡 Voir la solution</summary>

Pour chaque position i, la meilleure sous-suite croissante se construit à partir des meilleures sous-suites des positions précédentes. L'optimalité globale dépend donc de l'optimalité locale à chaque étape.

</details>

---

## 💪 Exercices Pratiques

Pour t'entraîner, voici des exercices progressifs et concrets :

---

### Exercice 1 : Binôme de Newton (coefficients binomiaux)

**Objectif :** Identifier les sous-problèmes chevauchants et visualiser l'arbre de récursion.

**Instructions :** Dessine l'arbre de récursion pour C(4,2) et repère les sous-problèmes calculés plusieurs fois. Implémente la version mémoïsée et compare le nombre d'appels.

<details>
<summary>💡 Voir la solution</summary>

Arbre de récursion :

```
C(4,2)
├─ C(3,1)
│  ├─ C(2,0)
│  └─ C(2,1)
│     ├─ C(1,0)
│     └─ C(1,1)
└─ C(3,2)
   ├─ C(2,1)
   │  ├─ C(1,0)
   │  └─ C(1,1)
   └─ C(2,2)
```

C(2,1) est calculé deux fois !

Version mémoïsée :

```javascript
function binomeMemo(n, k, memo = {}) {
  const key = `${n},${k}`;
  if (k === 0 || k === n) return 1;
  if (memo[key] !== undefined) return memo[key];
  memo[key] = binomeMemo(n - 1, k - 1, memo) + binomeMemo(n - 1, k, memo);
  return memo[key];
}
console.log(binomeMemo(4, 2)); // 6
```

Le nombre d'appels est considérablement réduit.

</details>

---

### Exercice 2 : Sous-structure optimale ou non ?

**Objectif :** Vérifier la sous-structure optimale sur le problème du "Maximum Product Subarray" et comprendre les limites de la PD.

**Instructions :** Est-ce que le produit maximal d'un sous-tableau [i...j] garantit que les sous-tableaux [i...k] et [k+1...j] sont optimaux ? Pourquoi ? Teste avec des exemples concrets.

<details>
<summary>💡 Voir la solution</summary>

Non, à cause des nombres négatifs, le produit optimal d'un sous-tableau n'est pas forcément composé de sous-produits optimaux. Par exemple, dans [2, -3, 4], le produit maximal est 4, mais le sous-tableau [2, -3] a un produit négatif. La sous-structure optimale ne s'applique pas toujours ici.

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle propriété distingue un problème adapté à la programmation dynamique d'un simple problème récursif ?**

- [ ] A. Il doit être résolu en O(1)
- [ ] B. Il doit avoir des sous-problèmes chevauchants
- [ ] C. Il doit avoir une solution unique
- [ ] D. Il doit être résolu par force brute

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Les sous-problèmes chevauchants sont essentiels pour appliquer la PD efficacement.

</details>

---

### Question 2

**Un problème peut-il avoir une sous-structure optimale sans sous-problèmes chevauchants ?**

- [ ] A. Oui
- [ ] B. Non

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

Certains problèmes (ex : tri fusion) ont une sous-structure optimale mais pas de sous-problèmes chevauchants, donc la PD n'est pas nécessaire.

</details>

---

### Question 3

**Quel est le principal inconvénient de la mémoïsation ?**

- [ ] A. Elle augmente la complexité temporelle
- [ ] B. Elle peut provoquer un dépassement de pile (stack overflow)
- [ ] C. Elle ne fonctionne qu'en Python
- [ ] D. Elle ne réduit pas la complexité

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La récursivité profonde peut provoquer un dépassement de pile.

</details>

---

### Question 4

**Pourquoi la PD n'est-elle pas adaptée à tous les problèmes ?**

- [ ] A. Parce qu'elle est trop lente
- [ ] B. Parce que tous les problèmes n'ont pas de sous-structure optimale
- [ ] C. Parce qu'elle ne fonctionne qu'en JavaScript
- [ ] D. Parce qu'elle nécessite des tableaux

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Sans sous-structure optimale, la PD ne garantit pas l'optimalité.

</details>

---

### Question 5

**Quelle différence principale entre mémoïsation et tabulation ?**

- [ ] A. La mémoïsation est itérative, la tabulation est récursive
- [ ] B. La mémoïsation stocke les résultats, la tabulation non
- [ ] C. La mémoïsation est top-down, la tabulation est bottom-up
- [ ] D. Il n'y a aucune différence

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La mémoïsation est top-down (récursive), la tabulation est bottom-up (itérative).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Sous-problèmes chevauchants

Éviter les calculs redondants en stockant les résultats intermédiaires (mémoïsation ou tabulation).

### 2. Sous-structure optimale

Construire la solution globale à partir de sous-solutions optimales, comme dans le plus court chemin ou la LIS.

### 3. Mémoïsation

Technique top-down pour accélérer la récursivité et réduire le nombre d'appels.

### 4. Tabulation

Technique bottom-up, plus sûre contre le stack overflow, et souvent plus rapide pour les grands problèmes.

### 5. Exemples classiques

Fibonacci, rendu de monnaie, binôme de Newton, LIS, gestion de dépendances, chemins dans un graphe acyclique.

### 6. Limites de la PD

Pas adaptée si le problème n'a pas de sous-structure optimale ou de sous-problèmes chevauchants (ex : certains problèmes de parcours avec cycles).

### 7. Préparation à la suite

La prochaine leçon portera sur la tabulation et la résolution de problèmes classiques comme le sac à dos, avec des exemples concrets et des schémas.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Tu maîtrises maintenant les fondements de la programmation dynamique et sais reconnaître quand l'appliquer !

### Ce que tu as appris aujourd'hui

- Identifier les deux propriétés clés de la PD
- Implémenter la mémoïsation en JavaScript
- Distinguer les problèmes adaptés ou non à la PD

### Compétences acquises

Tu es maintenant capable de :

- Analyser un problème pour détecter la PD
- Optimiser des algorithmes récursifs
- Préparer la transition vers la tabulation

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La programmation dynamique est incontournable pour résoudre efficacement de nombreux problèmes d'optimisation, en particulier en algorithmique avancée et en entretien technique !

---

## ➡️ Prochaine Étape : Leçon 34

### Ce qui t'attend

La prochaine leçon, **« Mémoïsation : Programmation Dynamique Top-Down en JavaScript »**, t'apprendra à implémenter la PD de façon systématique et à l'appliquer à des problèmes classiques.

**Tu découvriras :**

- Comment structurer la mémoïsation
- Des exemples concrets (Fibonacci, rendu de monnaie, LIS)
- Les pièges à éviter et les bonnes pratiques

### Prépare-toi !

La tabulation et la mémoïsation sont les deux faces de la PD. Maîtriser les deux te rendra beaucoup plus efficace pour résoudre des problèmes complexes !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Wikipedia - Programmation dynamique](https://fr.wikipedia.org/wiki/Programmation_dynamique)
- [MIT OpenCourseWare - Dynamic Programming](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/resources/lecture-19-dynamic-programming-i/)
- [JavaScript.info - Récursivité et mémoïsation](https://javascript.info/recursion)

### Outils de pratique

- **[LeetCode - Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)** : Problèmes classiques

---

## 💬 Feedback et Questions

Tu as des questions sur cette leçon ? Un doute sur la PD ?

N'hésite pas à :

- Relire les exemples et exercices
- Tester les codes dans ta console
- Demander de l'aide sur le forum du cours

> 💡 **Conseil**
>
> Prends le temps de bien comprendre les deux propriétés fondamentales avant de passer à la suite : c'est la clé pour progresser !

---

**Prêt pour la Leçon 34 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir la mémoïsation en profondeur !

---

<div align="center">

**Leçon 33 sur 42 - Module 6 : Paradigmes Avancés de Conception d'Algorithmes**

[⬅️ Leçon 32 : Implémentation d'un Algorithme Glouton en JavaScript](./lecon-2-implementation-algorithme-glouton-javascript-probleme-monnaie.md) | [Retour au sommaire](./README.md) | [Leçon 34 : Mémoïsation : Programmation Dynamique Top-Down en JavaScript ➡️](./lecon-4-memoisation-programmation-dynamique-top-down-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
