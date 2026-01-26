##### Leçon 41 sur 42 (Leçon 5 du Module 7)

# Réglage des Performances et Débogage d'Algorithmes en JavaScript

**Module 7** : Applications d'Algorithmes et Résolution de Problèmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Utiliser les outils de profilage pour identifier les goulots d’étranglement dans un algorithme JavaScript
- Appliquer des techniques de debugging pour corriger des bugs courants dans les algorithmes
- Reconnaître et corriger les erreurs classiques (off-by-one, base case, boucle infinie…)
- Optimiser la performance d’un algorithme en choisissant la bonne structure ou technique
- Mettre en place une démarche structurée d’analyse et de correction

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- Savoir implémenter des algorithmes classiques (tri, recherche, récursif)
- Connaître les structures de données de base (tableaux, listes, graphes)
- Savoir utiliser la console et les DevTools du navigateur

---

## 🚀 Introduction : Pourquoi profiler et débugger ?

Un algorithme peut être lent ou donner de mauvais résultats. Savoir **profiler** (mesurer) et **débugger** (corriger) est essentiel pour écrire du code robuste et efficace.

- Identifier les parties lentes (hot spots)
- Corriger les bugs logiques ou d’implémentation
- Améliorer la fiabilité et la maintenabilité

> **Point Clé**
>
> Le profilage et le debugging sont des compétences fondamentales pour tout développeur souhaitant progresser en algorithmique.

---

## 📦 Profilage d’algorithmes : outils et méthodes

Le profilage permet de mesurer le temps d’exécution, la mémoire utilisée, et de repérer les parties lentes.

### Mesurer avec console.time() et console.timeEnd()

```javascript
console.time("Array Sum");
let sum = 0;
const largeArray = Array.from({ length: 1000000 }, (_, i) => i);
for (let i = 0; i < largeArray.length; i++) {
  sum += largeArray[i];
}
console.timeEnd("Array Sum");
console.log("Somme :", sum);
```

---

## 📝 Micro-Exercice #1 : Profilage d’une fonction récursive

**Objectif :** Mesurer le temps d’exécution d’une fonction récursive

**Instructions :**

1. Implémente la fonction fibonacci(n) récursive.
2. Utilise console.time/console.timeEnd pour n = 20, 30, 40.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
console.time("fib40");
fibonacci(40);
console.timeEnd("fib40");
```

Le temps explose avec n !

</details>

---

### Utiliser les DevTools pour profiler

1. Ouvre les DevTools (F12)
2. Onglet "Performance" > Record > Exécute le code > Stop
3. Analyse le flame chart et les fonctions les plus coûteuses

> **Point Clé**
>
> Le flame chart permet de visualiser les fonctions qui consomment le plus de temps.

---

## 📦 Debugging d’algorithmes : techniques et pièges courants

### Inspection avec console.log()

```javascript
function findMax(arr) {
  console.log("Entrée :", arr);
  if (!Array.isArray(arr) || arr.length === 0) return undefined;
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    console.log("Compare", arr[i], "avec", max);
    if (arr[i] > max) {
      max = arr[i];
      console.log("Nouveau max :", max);
    }
  }
  return max;
}
findMax([3, 1, 4, 1, 5, 9, 2, 6]);
```

---

## 📝 Micro-Exercice #2 : Debugging d’une recherche binaire

**Objectif :** Repérer et corriger un bug off-by-one

**Instructions :**

1. Observe la fonction binarySearchBuggy ci-dessous.
2. Utilise console.log pour suivre low, high, mid.
3. Corrige le bug pour que la recherche fonctionne toujours.

```javascript
function binarySearchBuggy(arr, target) {
  let low = 0;
  let high = arr.length - 1;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      low = mid; // BUG ici
    } else {
      high = mid - 1;
    }
  }
  return -1;
}
// Corrige : remplacer low = mid; par low = mid + 1;
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function binarySearch(arr, target) {
  let low = 0;
  let high = arr.length - 1;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return -1;
}
```

</details>

---

### Utiliser les breakpoints et le pas-à-pas

1. Place un breakpoint dans la fonction à débugger (onglet Sources)
2. Exécute le code et observe les variables à chaque étape
3. Utilise Step Over, Step Into, Step Out pour naviguer

---

### Pièges classiques :

- Off-by-one (boucle trop ou pas assez)
- Boucle infinie (condition jamais atteinte)
- Mauvais cas de base en récursif
- Mauvaise utilisation d’une structure de données (push vs pop, etc.)

---

## 📝 Micro-Exercice #3 : Corriger une boucle infinie

**Objectif :** Identifier et corriger une boucle qui ne termine jamais

**Instructions :**

1. Observe la fonction suivante :

```javascript
function findElementIncorrect(arr, target) {
  let i = 0;
  while (i < arr.length) {
    if (arr[i] === target) return i;
    // i++ manquant !
  }
  return -1;
}
```

2. Corrige la fonction pour qu’elle termine toujours.

<details>
<summary>💡 Voir la solution</summary>

Ajouter i++ dans la boucle !

</details>

---

## 💻 Application Pratique : Debugging et tuning d’une fonctionnalité

### Exemple : Optimiser le filtrage et tri de tâches

```javascript
const tasks = [
  { id: 1, name: "Review code", status: "pending", priority: 2 },
  { id: 2, name: "Write report", status: "completed", priority: 1 },
  { id: 3, name: "Schedule meeting", status: "pending", priority: 3 },
  { id: 4, name: "Debug login flow", status: "pending", priority: 1 },
  { id: 5, name: "Plan sprint", status: "completed", priority: 3 },
  { id: 6, name: "Research new library", status: "pending", priority: 2 },
];
function filterAndSortTasksOptimized(taskList, statusFilter) {
  console.time("filterAndSortTasksOptimized");
  const filteredTasks = taskList.filter((task) => task.status === statusFilter);
  filteredTasks.sort((a, b) => a.priority - b.priority); // 1 = plus prioritaire
  console.timeEnd("filterAndSortTasksOptimized");
  return filteredTasks;
}
console.log(
  "Tâches triées (optimisé) :",
  filterAndSortTasksOptimized(tasks, "pending"),
);
```

**Analyse :**
Le passage de bubble sort à sort() améliore la performance. Attention à bien comprendre la signification du champ priority (1 = plus prioritaire ?).

---

## 💪 Exercices Pratiques

### Exercice 1 : Profilage de fibonacci

**Objectif :** Comparer la version naïve et la version mémoïsée

**Instructions :**

1. Implémente fibonacci(n) récursif et mémoïsé.
2. Profile les deux pour n = 20, 30, 40.

<details>
<summary>💡 Voir la solution</summary>

La version mémoïsée est beaucoup plus rapide pour n élevé !

</details>

---

### Exercice 2 : Correction d’une recherche binaire

**Objectif :** Corriger le bug off-by-one

**Instructions :**

1. Teste binarySearchBuggy sur plusieurs cas.
2. Corrige la fonction pour qu’elle fonctionne toujours.

<details>
<summary>💡 Voir la solution</summary>

Voir la correction dans le micro-exercice #2.

</details>

---

### Exercice 3 : Tuning d’un parcours de graphe

**Objectif :** Comparer matrice d’adjacence et liste d’adjacence

**Instructions :**

1. Implémente BFS ou DFS avec matrice puis liste d’adjacence.
2. Profile les deux pour un graphe sparse (1000 nœuds, 2000 arêtes).

<details>
<summary>💡 Voir la solution</summary>

La liste d’adjacence est bien plus efficace pour les graphes creux !

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quel outil permet de visualiser les fonctions les plus coûteuses dans un algorithme ?**

- [ ] A. console.log
- [ ] B. Flame chart des DevTools
- [ ] C. alert()
- [ ] D. prompt()

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le flame chart permet de repérer les hot spots.

</details>

---

### Question 2

**Quelle erreur est typique dans les boucles ?**

- [ ] A. Off-by-one
- [ ] B. Mauvais cas de base
- [ ] C. Mauvais tri
- [ ] D. Mauvais nom de variable

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

L’erreur off-by-one est très fréquente dans les boucles.

</details>

---

### Question 3

**Comment corriger une boucle infinie ?**

- [ ] A. Ajouter un break
- [ ] B. Vérifier la condition de sortie et l’incrément
- [ ] C. Utiliser sort()
- [ ] D. Changer le nom de la variable

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Il faut s’assurer que la condition de sortie sera atteinte.

</details>

---

### Question 4

**Pourquoi la version mémoïsée de fibonacci est-elle plus rapide ?**

- [ ] A. Elle utilise plus de mémoire
- [ ] B. Elle évite les calculs redondants
- [ ] C. Elle utilise sort()
- [ ] D. Elle est plus jolie

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La mémoïsation évite de recalculer les mêmes valeurs.

</details>

---

### Question 5

**Quelle est la meilleure approche pour déboguer un algorithme qui donne des résultats incorrects ?**

- [ ] A. Réécrire tout le code
- [ ] B. Utiliser console.log sur les variables intermédiaires et tester avec de petits cas
- [ ] C. Augmenter la puissance du serveur
- [ ] D. Changer de langage de programmation

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le débogage efficace consiste à tracer l'exécution avec des console.log, des breakpoints, et des cas de test simples pour comprendre où l'algorithme diverge du comportement attendu. Cela permet d'identifier précisément la ligne ou la logique problématique.

</details>

---

### Question 6

**Pourquoi est-il important de tester un algorithme avec des cas limites (edge cases) ?**

- [ ] A. Pour impressionner les collègues
- [ ] B. Pour détecter les bugs qui n'apparaissent que dans des situations particulières
- [ ] C. Pour augmenter le temps d'exécution
- [ ] D. Pour compliquer le code

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Les cas limites (tableaux vides, valeurs nulles, un seul élément, valeurs extrêmes) révèlent souvent des bugs cachés comme les off-by-one, divisions par zéro, ou accès hors limites. Tester ces cas garantit la robustesse de l'algorithme.

</details>

---

### Question 7

**Quelle technique permet de réduire la complexité temporelle de O(2^n) à O(n) pour Fibonacci ?**

- [ ] A. Utiliser plus de console.log
- [ ] B. Mémoïsation ou programmation dynamique
- [ ] C. Utiliser un ordinateur plus rapide
- [ ] D. Trier les nombres avant

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La mémoïsation stocke les résultats déjà calculés pour éviter les recalculs redondants, transformant l'algorithme récursif naïf O(2^n) en O(n). La programmation dynamique (approche bottom-up) obtient le même résultat. C'est un exemple classique d'optimisation algorithmique.

</details>

---

## 📌 Récapitulatif en 6 Points Clés

### 1. Profilage pour cibler l'optimisation

Toujours mesurer avant d’optimiser.

### 2. Debugging structuré

Utiliser console.log, breakpoints, et analyse des variables.

### 3. Corriger les bugs classiques

Off-by-one, boucle infinie, base case, etc.

### 4. Choix de la bonne structure

Adapter la structure de données à l’algorithme.

### 5. Optimisation progressive

Remplacer les algos naïfs par des versions efficaces.

### 6. Importance de la démarche

Profiler, analyser, corriger, valider.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Tu sais maintenant profiler, débugger et optimiser des algorithmes JavaScript comme un pro !

### Ce que tu as appris aujourd’hui

- Utiliser les outils de profilage
- Corriger les bugs courants
- Optimiser la performance d’un algorithme

### Compétences acquises

Tu es maintenant capable de :

- Diagnostiquer et corriger les problèmes de performance
- Appliquer une démarche rigoureuse de debugging
- Améliorer la robustesse de tes algos

### Pourquoi c’est important

> 📌 **Point Clé**
>
> Ces compétences sont essentielles pour tout développeur souhaitant écrire du code fiable et performant.

---

## ➡️ Prochaine Étape : Leçon 42

### Ce qui t’attend

La prochaine leçon, **« S’entraîner pour l’Algorithmique Avancée et la Programmation Compétitive »**, te donnera des pistes pour progresser encore plus loin !

**Tu découvriras :**

- Les ressources pour s’entraîner
- Les concours et challenges
- Les bonnes pratiques pour progresser

### Prépare-toi !

Tu vas passer du debugging à la performance de haut niveau !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [MDN - Profilage et debugging JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript/Debugging)
- [Google Chrome DevTools - Performance Profiling](https://developer.chrome.com/docs/devtools/evaluate-performance/)
- [OpenClassrooms - Déboguer du JavaScript](https://openclassrooms.com/fr/courses/6204541-planifiez-et-pilotez-un-projet-informatique/6272821-planifiez-les-taches-et-les-ressources)

### Outils de pratique

- **[JSBench.me](https://jsbench.me/)** : Comparer la performance de différents algorithmes
- **[Chrome DevTools](https://developer.chrome.com/docs/devtools/)** : Profilage et analyse de code

---

## 💬 Feedback et Questions

Tu as des questions sur cette leçon ? Un doute sur le debugging ou le tuning ?

N’hésite pas à :

- Relire les exemples et exercices
- Tester les codes dans ta console
- Demander de l’aide sur le forum du cours

> 💡 **Conseil**
>
> Prends toujours le temps de mesurer, d’analyser, puis d’optimiser : c’est la clé du progrès !

---

**Prêt pour la Leçon 42 ?** 🚀

Rendez-vous dans la prochaine leçon pour t’entraîner à l’algorithmique avancée !

---

<div align="center">

**Leçon 41 sur 42 - Module 7 : Applications d'Algorithmes et Résolution de Problèmes**

[⬅️ Leçon 40 : Étude de Cas Avancée : Appliquer des Algorithmes pour Améliorer l'Efficacité de la Gestion des Tâches](./lecon-4-etude-cas-avancee-appliquer-algorithmes-ameliorer-efficacite-gestion-taches.md) | [Retour au sommaire](./README.md) | [Leçon 42 : S’entraîner pour l’Algorithmique Avancée et la Programmation Compétitive ➡️](./lecon-6-prochaines-etapes-apprentissage-continu-ressources-programmation-competitive.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
