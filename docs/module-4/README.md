# Module 4 : Algorithmes de Recherche et Introduction à la Récursion

<div align="center">

![Module 4 - Recherche et Récursion](https://img.shields.io/badge/Module_4-Recherche_et_Récursion-orange)
![Niveau](https://img.shields.io/badge/Niveau-Intermédiaire-yellow)
![Leçons](https://img.shields.io/badge/Leçons-6-blue)
![Durée](https://img.shields.io/badge/Durée-15--18h-green)

</div>

---

## 📋 Vue d'Ensemble

Ce module vous introduit aux **algorithmes de recherche** fondamentaux et à la **récursion**, une technique de programmation puissante et élégante. Vous apprendrez à trouver efficacement des éléments dans des collections de données et à résoudre des problèmes en les décomposant en sous-problèmes identiques.

### 🎯 Objectifs du Module

À la fin de ce module, vous serez capable de :

- ✅ Implémenter et analyser la **recherche linéaire** (O(n))
- ✅ Implémenter et analyser la **recherche binaire** (O(log n))
- ✅ Comprendre et appliquer le concept de **récursion**
- ✅ Identifier les **cas de base** et les **appels récursifs**
- ✅ Comprendre le fonctionnement de la **pile d'appels**
- ✅ Éviter les erreurs **Stack Overflow**
- ✅ Appliquer la récursion aux **opérations sur tableaux**

---

## 📚 Leçons du Module

| # | Titre | Durée | Description |
|---|-------|-------|-------------|
| **19** | [Recherche Linéaire](./lecon-1-recherche-lineaire-trouver-element-simplement-javascript.md) | ~2h30 | Recherche séquentielle, complexité O(n), cas d'utilisation |
| **20** | [Recherche Binaire](./lecon-2-recherche-binaire-recherche-efficace-tableaux-tries.md) | ~2h30 | Recherche efficace dans les tableaux triés, O(log n) |
| **21** | [Introduction à la Récursion](./lecon-3-introduction-recursion-cas-base-appels-recursifs.md) | ~2h30 | Cas de base, appels récursifs, pensée récursive |
| **22** | [Fonctions Récursives en JavaScript](./lecon-4-implementation-fonctions-recursives-base-javascript.md) | ~2h30 | Factorielle, Fibonacci, somme de tableau |
| **23** | [Pile d'Appels et Récursion](./lecon-5-comprendre-pile-appels-recursion.md) | ~2h | Call stack, stack overflow, traçage |
| **24** | [Pratique : Récursion sur Tableaux](./lecon-6-pratique-utiliser-recursion-operations-tableaux.md) | ~3h | Map, filter, max/min récursifs, étude de cas |

---

## 🧠 Concepts Clés

### Algorithmes de Recherche

| Algorithme | Complexité Temps | Prérequis | Quand l'utiliser |
|------------|-----------------|-----------|------------------|
| **Linéaire** | O(n) | Aucun | Données non triées, petites collections |
| **Binaire** | O(log n) | Données triées | Grandes collections triées |

### Récursion

La récursion est une technique où une fonction **s'appelle elle-même** pour résoudre un problème en le décomposant en sous-problèmes plus petits.

**Structure d'une fonction récursive :**

```javascript
function recursive(param) {
  // 1. CAS DE BASE - Condition d'arrêt
  if (conditionSimple) {
    return resultatDirect;
  }
  
  // 2. APPEL RÉCURSIF - Réduction du problème
  return travail + recursive(paramReduit);
}
```

### Pile d'Appels (Call Stack)

- Fonctionne selon le principe **LIFO** (Last-In, First-Out)
- Chaque appel de fonction empile un **cadre d'exécution**
- Taille limitée (~10 000-15 000 appels)
- Récursion infinie = **Stack Overflow**

---

## 🔄 Comparaison : Recherche Linéaire vs Binaire

| Critère | Recherche Linéaire | Recherche Binaire |
|---------|-------------------|-------------------|
| **Complexité** | O(n) | O(log n) |
| **Prérequis** | Aucun | Tableau trié |
| **10 éléments** | Max 10 comparaisons | Max 4 comparaisons |
| **1 000 éléments** | Max 1 000 comparaisons | Max 10 comparaisons |
| **1 000 000 éléments** | Max 1 000 000 comparaisons | Max 20 comparaisons |

---

## 🎓 Compétences Acquises

### Après ce module, vous maîtrisez :

- 🔍 **Recherche linéaire** : Parcourir séquentiellement une collection
- 🎯 **Recherche binaire** : Diviser l'espace de recherche en deux
- 🔄 **Pensée récursive** : Décomposer un problème en sous-problèmes
- 📚 **Cas de base** : Identifier les conditions d'arrêt
- 📊 **Pile d'appels** : Comprendre comment JavaScript gère les fonctions
- ⚠️ **Stack overflow** : Prévenir les erreurs de récursion infinie
- 🛠️ **Patterns récursifs** : Map, filter, reduce sur tableaux

---

## 📈 Progression du Cours

```
Module 1 → Module 2 → Module 3 → [Module 4] → Module 5 → Module 6 → Module 7
Fondements   Structures   Tri        RECHERCHE    Arbres     Avancé     Applications
                                     RÉCURSION
```

### Prérequis

- ✅ **Module 1** : Complexité algorithmique (Big O)
- ✅ **Module 2** : Structures de données (tableaux)
- ✅ **Module 3** : Algorithmes de tri (contexte Diviser pour Régner)

### Ce qui vient ensuite

- **Module 5** : Arbres et Parcours de Graphes
  - Les arbres sont des structures **naturellement récursives**
  - Les parcours (DFS) utilisent la récursion ou une pile
  - Ce module prépare directement au Module 5

---

## 💡 Points Clés à Retenir

1. **Recherche binaire** ne fonctionne que sur des **données triées**
2. Chaque fonction récursive DOIT avoir un **cas de base**
3. L'appel récursif doit **réduire** le problème vers le cas de base
4. La pile d'appels a une **taille limitée**
5. L'approche **index** est plus performante que **slice()** pour les tableaux

---

## 🔗 Ressources Complémentaires

### Documentation

- [MDN - Recursion](https://developer.mozilla.org/fr/docs/Glossary/Recursion)
- [MDN - Call Stack](https://developer.mozilla.org/fr/docs/Glossary/Call_stack)
- [MDN - Array Methods](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array)

### Outils de Visualisation

- [Visualgo - Binary Search](https://visualgo.net/en/bst)
- [Python Tutor](https://pythontutor.com/javascript.html) - Visualisation de la pile

### Pratique

- [LeetCode - Binary Search](https://leetcode.com/tag/binary-search/)
- [HackerRank - Recursion](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=recursion)

---

## ⏭️ Prochaine Étape

**[Module 5 : Arbres et Parcours de Graphes](../module-5/README.md)**

Vous allez découvrir les structures de données arborescentes et les graphes, qui sont parmi les plus puissantes en informatique. La récursion que vous venez de maîtriser sera omniprésente !

---

<div align="center">

**Module 4 sur 7 - Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Module 3 : Techniques de Tri](../module-3/README.md) | [Retour au cours](../../README.md) | [Module 5 : Arbres et Graphes ➡️](../module-5/README.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
