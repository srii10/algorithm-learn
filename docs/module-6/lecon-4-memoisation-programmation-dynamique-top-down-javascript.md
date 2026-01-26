##### Leçon 34 sur 42

# Mémoïsation : Programmation Dynamique Top-Down en JavaScript

**Module 6** : Paradigmes Avancés de Conception d'Algorithmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Expliquer le principe de la mémoïsation et son lien avec la programmation dynamique
- Transformer une fonction récursive inefficace en version mémoïsée
- Implémenter la mémoïsation pour différents types de problèmes (Fibonacci, factorielle, rendu de monnaie, etc.)
- Utiliser des structures de cache adaptées (objet, tableau, clé composée)
- Identifier les cas où la mémoïsation apporte un gain réel
- Comprendre les limites et pièges de la mémoïsation

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- Leçon 33 : Sous-problèmes chevauchants et sous-structure optimale
- Savoir écrire des fonctions récursives en JavaScript
- Comprendre les bases des objets et tableaux en JavaScript
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Pourquoi la mémoïsation ?

Tu as déjà vu que certains algorithmes récursifs recalculent sans cesse les mêmes sous-problèmes, rendant leur exécution très lente. La **mémoïsation** est une technique qui permet de transformer ces algorithmes en solutions rapides, en stockant les résultats déjà calculés dans un cache.

> **Point Clé**
>
> La mémoïsation, c'est comme garder un carnet de notes : dès qu'on a résolu un sous-problème, on note la réponse pour ne plus jamais refaire le même calcul.

---

## 📦 Principe de la Mémoïsation

### Mémoïsation vs Cache général : quelle différence ?

> **À retenir**
>
> La mémoïsation est un **cache spécialisé** : elle stocke les résultats de fonctions pures (mêmes entrées → même sortie) pour éviter de recalculer les mêmes sous-problèmes. Un cache général peut concerner n'importe quelle donnée (fichiers, requêtes, etc.), alors que la mémoïsation cible spécifiquement l'optimisation d'appels de fonctions récursives ou coûteuses.

**Résumé** :

- Mémoïsation = cache automatique pour les sous-problèmes d'une fonction
- Cache général = stockage manuel de n'importe quelle donnée (pas forcément lié à la récursivité ou à la DP)

La mémoïsation consiste à **étendre une fonction récursive** avec un cache (objet ou tableau). Avant de calculer un résultat, la fonction vérifie si ce résultat est déjà dans le cache :

- Si oui, elle le retourne immédiatement (gain de temps)
- Sinon, elle le calcule, le stocke dans le cache, puis le retourne

Ce principe permet de ne jamais résoudre deux fois le même sous-problème.

---

## 💻 Exemple 1 : Fibonacci naïf vs mémoïsé

```javascript
// Version naïve (exponentielle)
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

// Version mémoïsée (linéaire)
function fibonacciMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
  return memo[n];
}

console.log(fibonacciMemo(10)); // 55
console.log(fibonacciMemo(50)); // 12586269025 (très rapide)
```

**Analyse :**

- La version naïve recalcule `fibonacci(3)` plusieurs fois, la version mémoïsée ne le fait qu'une seule fois.
- Pour `fibonacci(50)`, la version naïve est inutilisable, la version mémoïsée est instantanée.

---

## 📝 Micro-Exercice #1 : Visualiser le cache

**Objectif :** Comprendre comment le cache évolue lors de l'exécution.

**Instructions :** Ajoute un `console.log(memo)` dans la fonction `fibonacciMemo` et observe l'évolution du cache pour `n = 6`.

<details>
<summary>💡 Voir la solution</summary>

Le cache se remplit progressivement :

```
{ '2': 1, '3': 2, '4': 3, '5': 5, '6': 8 }
```

Chaque valeur n'est calculée qu'une seule fois.

</details>

---

## 💻 Exemple 2 : Factorielle mémoïsée

La factorielle n'a pas de sous-problèmes chevauchants dans un seul appel, mais si on appelle plusieurs fois la fonction avec les mêmes arguments, le cache est utile.

```javascript
function factorielleMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n === 0 || n === 1) return 1;
  memo[n] = n * factorielleMemo(n - 1, memo);
  return memo[n];
}

console.log(factorielleMemo(5)); // 120
console.log(factorielleMemo(7)); // 5040 (réutilise 5! et 6!)
```

---

## 📝 Micro-Exercice #2 : Utilité du cache

**Objectif :** Montrer l'intérêt du cache même sans sous-problèmes chevauchants dans un seul appel.

**Instructions :** Appelle plusieurs fois `factorielleMemo` avec des valeurs croissantes et observe le nombre de calculs réellement effectués.

<details>
<summary>💡 Voir la solution</summary>

Le cache permet de ne recalculer que les nouvelles valeurs, les précédentes sont réutilisées.

</details>

---

## 💻 Exemple 3 : Rendu de monnaie (nombre de façons)

Problème : Combien de façons différentes de rendre une somme donnée avec un ensemble de pièces ?

```javascript
function nbFaconsRendre(montant, pieces, i = 0, memo = {}) {
  const key = `${montant}-${i}`;
  if (key in memo) return memo[key];
  if (montant === 0) return 1;
  if (montant < 0 || i >= pieces.length) return 0;
  // Inclure la pièce courante
  const avec = nbFaconsRendre(montant - pieces[i], pieces, i, memo);
  // Exclure la pièce courante
  const sans = nbFaconsRendre(montant, pieces, i + 1, memo);
  memo[key] = avec + sans;
  return memo[key];
}

console.log(nbFaconsRendre(5, [1, 2, 5])); // 4 façons
```

**Explication :**

- On utilise une clé composée (montant, index) pour mémoriser chaque sous-problème unique.
- Sans mémoïsation, le nombre d'appels explose pour de grands montants.

---

## 📝 Micro-Exercice #3 : Adapter la mémoïsation

**Objectif :** Savoir adapter la structure du cache selon le problème.

**Instructions :** Pour le problème du voyageur sur une grille m×n (déplacements droite/bas), implémente une fonction `voyageurGrille(m, n, memo)` qui utilise une clé composée pour mémoriser les sous-problèmes.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function voyageurGrille(m, n, memo = {}) {
  const key = `${m},${n}`;
  if (key in memo) return memo[key];
  if (m === 1 && n === 1) return 1;
  if (m === 0 || n === 0) return 0;
  memo[key] = voyageurGrille(m - 1, n, memo) + voyageurGrille(m, n - 1, memo);
  return memo[key];
}
console.log(voyageurGrille(3, 3)); // 6
```

</details>

---

## 💡 Applications concrètes de la mémoïsation

---

### Quand utiliser la mémoïsation dans tes applications JavaScript ?

> **Bonnes pratiques**
>
> Utilise la mémoïsation quand :
>
> - Ta fonction est **pure** (pas d'effets de bord)
> - Tu observes des **appels répétés** avec les mêmes arguments
> - Le coût de calcul est significatif (ex : calculs combinatoires, DP, parsing complexe)
> - Les entrées sont peu nombreuses ou raisonnablement bornées (pour éviter un cache trop gros)

**Exemples concrets** :

- Calculs mathématiques (Fibonacci, factorielle, combinatoire)
- Calculs de chemins (grille, graphe, IA de jeu)
- Optimisation de composants React (useMemo, useCallback)
- Mise en cache de résultats d'API ou de requêtes coûteuses

**À éviter** :

- Si chaque appel concerne un sous-problème unique (pas de répétition)
- Si la fonction a des effets de bord ou dépend d'un état externe

---

### Limites, risques et inconvénients de la mémoïsation

> **À surveiller**
>
> - **Surcharge mémoire** : un cache mal géré peut saturer la mémoire si trop de sous-problèmes différents sont stockés
> - **Bugs** : une clé de cache mal construite (ex : oubli d'un paramètre) peut donner des résultats incorrects
> - **Fonctions non pures** : la mémoïsation ne fonctionne pas si la fonction dépend d'un état externe ou a des effets de bord
> - **Pas de gain** : si chaque appel est unique, la mémoïsation n'apporte rien

**À retenir** :

- Toujours vérifier la pertinence du cache (taille, validité des clés)
- Nettoyer le cache si besoin (LRU, TTL, etc. dans des cas avancés)

> **Peut-on mémoïser une fonction sans sous-problèmes chevauchants ?**
>
> Oui : même si la factorielle n'a pas de sous-problèmes chevauchants dans un seul appel, la mémoïsation est utile si la fonction est appelée plusieurs fois avec les mêmes arguments (ex : dans un calcul de permutations, de combinaisons, etc.).
>
> **Résumé** : la mémoïsation optimise aussi les fonctions récursives "simples" si elles sont sollicitées plusieurs fois dans un programme.

- **Développement web** : Optimisation de calculs coûteux dans React (useMemo, useCallback)
- **Compilateurs** : Mémorisation de résultats d'analyse syntaxique ou de calculs intermédiaires
- **Jeux vidéo** : Pathfinding, IA, calculs de scores ou de chemins optimaux

---

## 💪 Exercices Pratiques

---

### Exercice 1 : Suite de Tribonacci mémoïsée

**Objectif :** Implémenter une version mémoïsée d'une suite à 3 termes.

**Instructions :** La suite de Tribonacci est définie par T(0)=0, T(1)=1, T(2)=1, puis T(n)=T(n-1)+T(n-2)+T(n-3). Implémente `tribonacciMemo(n, memo)` et teste avec n=4, 10, 25.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function tribonacciMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n === 0) return 0;
  if (n === 1 || n === 2) return 1;
  memo[n] =
    tribonacciMemo(n - 1, memo) +
    tribonacciMemo(n - 2, memo) +
    tribonacciMemo(n - 3, memo);
  return memo[n];
}
console.log(tribonacciMemo(4)); // 4
console.log(tribonacciMemo(10)); // 149
console.log(tribonacciMemo(25)); // 1389537
```

</details>

---

### Exercice 2 : Voyageur sur une grille

**Objectif :** Calculer le nombre de chemins sur une grille m×n.

**Instructions :** Implémente `voyageurGrille(m, n, memo)` et teste avec (1,1), (2,3), (3,2), (3,3), (18,18).

<details>
<summary>💡 Voir la solution</summary>

Voir micro-exercice #3 ci-dessus. Pour (18,18), le résultat est 2333606220.

</details>

---

### Exercice 3 : Peut-on atteindre la somme ?

**Objectif :** Déterminer si une somme cible peut être atteinte avec des combinaisons de nombres.

**Instructions :** Implémente `peutSomme(cible, nombres, memo)` qui retourne true si la somme cible peut être atteinte, false sinon. Teste avec les cas du cours.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function peutSomme(cible, nombres, memo = {}) {
  if (cible in memo) return memo[cible];
  if (cible === 0) return true;
  if (cible < 0) return false;
  for (const n of nombres) {
    if (peutSomme(cible - n, nombres, memo)) {
      memo[cible] = true;
      return true;
    }
  }
  memo[cible] = false;
  return false;
}
console.log(peutSomme(7, [2, 3])); // true
console.log(peutSomme(7, [2, 4])); // false
console.log(peutSomme(300, [7, 14])); // false
```

</details>

---

## 📊 Tableau Récapitulatif des Complexités

Voici un résumé des problèmes vus avec leur complexité **avant** et **après** mémoïsation :

| Problème             | Sans Mémoïsation | Avec Mémoïsation | Gain                     | Espace Mémoire |
| -------------------- | ---------------- | ---------------- | ------------------------ | -------------- |
| **Fibonacci**        | O(2^n)           | O(n)             | Exponentiel → Linéaire   | O(n)           |
| **Factorielle**      | O(n)             | O(n)             | Aucun (déjà linéaire)    | O(n)           |
| **Rendu de Monnaie** | O(k^n)           | O(n × k)         | Exponentiel → Polynomial | O(n)           |
| **Voyageur Grille**  | O(2^(m+n))       | O(m × n)         | Exponentiel → Polynomial | O(m × n)       |
| **Peut-on Somme**    | O(k^n)           | O(n × k)         | Exponentiel → Polynomial | O(n)           |

**Légende** :

- **n** : taille du problème (montant, position grille, etc.)
- **k** : nombre d'options (pièces, nombres disponibles)
- **m, n** : dimensions d'une grille

**Points clés** :

- La mémoïsation transforme des complexités **exponentielles** en complexités **polynomiales** ou **linéaires**
- Le coût mémoire est **O(taille du cache)** = nombre de sous-problèmes uniques
- Sans mémoïsation, des problèmes comme `fibonacci(40)` prendraient des **heures**
- Avec mémoïsation, `fibonacci(1000)` s'exécute en **millisecondes**

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Pourquoi la mémoïsation accélère-t-elle les fonctions récursives ?**

- [ ] A. Parce qu'elle utilise des boucles
- [ ] B. Parce qu'elle évite de recalculer les mêmes sous-problèmes
- [ ] C. Parce qu'elle utilise des promesses
- [ ] D. Parce qu'elle change la complexité spatiale

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La mémoïsation évite les calculs redondants.

</details>

---

### Question 2

**Dans quel cas la mémoïsation n'apporte-t-elle aucun gain ?**

- [ ] A. Si la fonction n'est jamais appelée
- [ ] B. Si chaque appel concerne un sous-problème différent
- [ ] C. Si le cache est mal initialisé
- [ ] D. Toutes les réponses

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Si chaque appel concerne un sous-problème unique, la mémoïsation ne sert à rien.

</details>

---

### Question 3

**Quelle structure de données est la plus adaptée pour mémoriser les résultats de sous-problèmes avec plusieurs paramètres ?**

- [ ] A. Un tableau simple
- [ ] B. Un objet avec des clés composées
- [ ] C. Une chaîne de caractères
- [ ] D. Un Set

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

On utilise souvent une clé composée (ex : "m,n") pour mémoriser les sous-problèmes à plusieurs paramètres.

</details>

---

### Question 4

**Quel est le principal risque d'une mauvaise gestion du cache en mémoïsation ?**

- [ ] A. Stack overflow
- [ ] B. Résultats incorrects
- [ ] C. Mémoire saturée
- [ ] D. Toutes les réponses

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Un cache mal géré peut causer des bugs, des surcoûts mémoire ou des erreurs de pile.

</details>

---

### Question 5

**Quelle est la complexité spatiale de la mémoïsation pour le problème de Fibonacci ?**

- [ ] A. O(1) - constante
- [ ] B. O(log n) - logarithmique
- [ ] C. O(n) - linéaire
- [ ] D. O(n²) - quadratique

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La mémoïsation de Fibonacci nécessite un cache de taille **O(n)** car on stocke au plus n valeurs (de 0 à n). C'est le trade-off temps/espace : on gagne en temps (O(2^n) → O(n)) mais on utilise O(n) d'espace supplémentaire.

**Détail** :

- Cache : O(n) pour stocker les résultats
- Pile d'appels : O(n) dans le pire cas (profondeur de récursion)
- Total : O(n) espace

</details>

---

### Question 6

**Dans quel cas la mémoïsation n'apporte-t-elle AUCUN gain de performance ?**

- [ ] A. Quand chaque appel récursif a des paramètres différents et uniques
- [ ] B. Quand le problème a des sous-problèmes chevauchants
- [ ] C. Quand le problème a une sous-structure optimale
- [ ] D. Quand on utilise JavaScript

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

La mémoïsation n'aide que si on **recalcule les mêmes sous-problèmes plusieurs fois**. Si chaque appel est unique (pas de chevauchement), le cache ne sera jamais réutilisé et on paiera le coût de gestion du cache pour rien.

**Exemple** :

- **Factorielle** : Chaque appel `fact(n)` appelle `fact(n-1)` une seule fois → pas de chevauchement → mémoïsation inutile
- **Fibonacci** : `fib(n)` recalcule `fib(n-2)` plusieurs fois → chevauchement important → mémoïsation efficace

</details>

---

### Question 7

**Comment gérer la mémoïsation pour une fonction avec plusieurs paramètres (ex: `f(m, n)`) ?**

- [ ] A. Utiliser deux caches séparés
- [ ] B. Créer une clé composée comme "m,n" ou "m-n"
- [ ] C. Ne mémoïser qu'un seul paramètre
- [ ] D. Mémoïser seulement si m = n

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Pour des fonctions multi-paramètres, on crée une **clé composée** unique qui combine tous les paramètres.

**Exemples** :

```javascript
// Option 1 : Chaîne concaténée
const cle = `${m},${n}`;
if (cle in memo) return memo[cle];

// Option 2 : Objet imbriqué
if (!memo[m]) memo[m] = {};
if (memo[m][n]) return memo[m][n];
```

**Cas d'usage** : Voyageur sur grille (m, n), plus longue sous-séquence commune (i, j), etc.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. La mémoïsation évite les calculs redondants

### 2. Elle transforme une récursivité inefficace en solution rapide

### 3. Le cache doit être adapté au problème (clé simple ou composée)

### 4. Elle s'applique surtout aux problèmes à sous-problèmes chevauchants

### 5. Elle ne sert à rien si chaque appel est unique

### 6. Attention à la gestion mémoire et à la validité du cache

### 7. C'est la porte d'entrée vers la tabulation (bottom-up)

---

## 🎓 Conclusion

**Félicitations !** 🎉 Tu sais maintenant transformer une fonction récursive inefficace en version mémoïsée, et tu comprends quand et comment utiliser cette technique !

### Ce que tu as appris aujourd'hui

- Le principe de la mémoïsation
- L'implémentation concrète en JavaScript
- Les cas d'usage et les limites

### Compétences acquises

Tu es maintenant capable de :

- Optimiser des fonctions récursives avec un cache
- Adapter la structure du cache au problème
- Préparer la transition vers la tabulation

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La mémoïsation est un outil fondamental pour rendre de nombreux algorithmes utilisables en pratique, et une compétence clé pour tout développeur d'algorithmes !

---

## ➡️ Prochaine Étape : Leçon 35

### Ce qui t'attend

La prochaine leçon, **« Tabulation : Programmation Dynamique Bottom-Up en JavaScript »**, t'apprendra à aborder les problèmes de façon itérative et à construire les solutions du bas vers le haut.

**Tu découvriras :**

- Comment structurer la tabulation
- Des exemples concrets (Fibonacci, rendu de monnaie, LIS)
- Les avantages et inconvénients par rapport à la mémoïsation

### Prépare-toi !

La tabulation complète ta boîte à outils pour la programmation dynamique.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Wikipedia - Mémoïsation](https://fr.wikipedia.org/wiki/M%C3%A9mo%C3%AFsation)
- [MIT OpenCourseWare - Dynamic Programming](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/resources/lecture-19-dynamic-programming-i/)
- [JavaScript.info - Récursivité et mémoïsation](https://javascript.info/recursion)

### Outils de pratique

- **[LeetCode - Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)** : Problèmes classiques

---

## 💬 Feedback et Questions

Tu as des questions sur cette leçon ? Un doute sur la mémoïsation ?

N'hésite pas à :

- Relire les exemples et exercices
- Tester les codes dans ta console
- Demander de l'aide sur le forum du cours

> 💡 **Conseil**
>
> Prends le temps de bien comprendre le fonctionnement du cache et d'expérimenter sur différents problèmes : c'est la clé pour progresser !

---

**Prêt pour la Leçon 35 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir la tabulation !

---

<div align="center">

**Leçon 34 sur 42 - Module 6 : Paradigmes Avancés de Conception d'Algorithmes**

[⬅️ Leçon 33 : Programmation Dynamique : Sous-problèmes Chevauchants et Sous-structure Optimale](./lecon-3-programmation-dynamique-sous-problemes-chevauchants-sous-structure-optimale.md) | [Retour au sommaire](./README.md) | [Leçon 35 : Tabulation : Programmation Dynamique Bottom-Up en JavaScript ➡️](./lecon-5-tabulation-programmation-dynamique-bottom-up-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
