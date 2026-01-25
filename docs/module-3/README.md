# 📘 Module 3 : Techniques de Tri Essentielles

<div align="center">

**Durée estimée : 15-18 heures**

_Maîtriser les algorithmes de tri fondamentaux et avancés_

</div>

---

## 🎯 Objectifs du Module

Ce module vous enseigne les algorithmes de tri essentiels, des plus simples aux plus efficaces. À la fin de ce module, vous serez capable de :

- ✅ Comprendre pourquoi le tri est une opération fondamentale en informatique
- ✅ Implémenter les trois algorithmes de tri élémentaires (Bulles, Sélection, Insertion)
- ✅ Maîtriser le paradigme "Diviser pour Régner" avec le tri fusion
- ✅ Comprendre le rôle du pivot et le partitionnement dans le tri rapide
- ✅ Analyser et comparer la complexité des différents algorithmes
- ✅ Choisir l'algorithme de tri approprié selon le contexte

---

## 📚 Leçons du Module

### [Leçon 13 : Introduction au Tri - Pourquoi Ordonner les Données ?](./lecon-1-introduction-tri-pourquoi-ordonner-donnees.md)

**Durée : 2h - 2h30**

Introduction aux concepts fondamentaux du tri : définition, avantages des données ordonnées, critères de tri et notions de stabilité.

**Concepts clés :**

- Définition et importance du tri en informatique
- Critères de tri (numérique, alphabétique, chronologique, personnalisé)
- Complexité temporelle et spatiale des algorithmes de tri
- Notion de stabilité des algorithmes
- Utilisation de `sort()` en JavaScript

---

### [Leçon 14 : Tri à Bulles - Concept et Implémentation JavaScript de Base](./lecon-2-tri-bulles-concept-implementation-javascript-base.md)

**Durée : 2h30 - 3h**

Premier algorithme de tri : comprendre le mécanisme des "bulles qui remontent" et implémenter l'optimisation avec le drapeau d'échange.

**Concepts clés :**

- Mécanisme de comparaison et d'échange des éléments adjacents
- Visualisation pas à pas de l'algorithme
- Optimisation avec le drapeau "swapped"
- Complexité O(n²) et cas d'utilisation appropriés
- Stabilité du tri à bulles

---

### [Leçon 15 : Tri par Sélection - Concept et Implémentation JavaScript de Base](./lecon-3-tri-selection-concept-implementation-javascript-base.md)

**Durée : 2h30 - 3h**

Deuxième algorithme élémentaire : sélectionner le minimum à chaque passe et le placer à sa position finale.

**Concepts clés :**

- Mécanisme de recherche du minimum
- Sous-tableaux triés et non triés
- Nombre minimal d'échanges (n-1 maximum)
- Instabilité de l'algorithme et ses implications
- Comparaison avec le tri à bulles

---

### [Leçon 16 : Tri par Insertion - Concept et Implémentation JavaScript Pratique](./lecon-4-tri-insertion-concept-implementation-javascript-pratique.md)

**Durée : 2h30 - 3h**

Troisième algorithme élémentaire : trier comme on organise une main de cartes, en insérant chaque élément à sa place.

**Concepts clés :**

- Métaphore du tri de cartes
- Mécanisme de décalage vs échange
- Adaptativité : O(n) pour les tableaux presque triés
- Stabilité et efficacité pour les petits tableaux
- Utilisation dans les algorithmes hybrides (Timsort)

---

### [Leçon 17 : Tri Fusion (Merge Sort) - Stratégie Diviser pour Régner](./lecon-5-tri-fusion-strategie-diviser-regner-javascript.md)

**Durée : 3h - 3h30**

Premier algorithme avancé : découvrir le paradigme "Diviser pour Régner" et atteindre une complexité O(n log n).

**Concepts clés :**

- Paradigme "Diviser pour Régner" (Divide and Conquer)
- Fonctions `mergeSort` et `merge`
- Récursivité et cas de base
- Complexité temporelle O(n log n) garantie
- Complexité spatiale O(n) et stabilité

---

### [Leçon 18 : Tri Rapide (Quick Sort) - Sélection du Pivot et Partitionnement](./lecon-6-tri-rapide-selection-pivot-partitionnement-javascript.md)

**Durée : 2h30 - 3h**

Comprendre le cœur du tri rapide : le choix du pivot et le mécanisme de partitionnement de Lomuto.

**Concepts clés :**

- Rôle crucial du pivot dans les performances
- Stratégies de sélection (premier, dernier, médiane de trois, aléatoire)
- Schéma de partitionnement de Lomuto
- Analyse du pire cas et comment l'éviter
- Comparaison avec le tri fusion

---

## 🎓 Compétences Acquises

À la fin de ce module, vous aurez acquis les compétences suivantes :

### 1. **Maîtrise des Algorithmes de Tri**

- Implémenter les cinq algorithmes de tri étudiés
- Comprendre leurs mécanismes internes (comparaison, échange, décalage)
- Visualiser et tracer leur exécution pas à pas

### 2. **Analyse de Complexité**

- Évaluer la complexité temporelle (meilleur, moyen, pire cas)
- Comprendre la complexité spatiale (tri en place vs mémoire auxiliaire)
- Comparer O(n²) vs O(n log n) et leurs implications pratiques

### 3. **Critères de Choix**

- Identifier la stabilité d'un algorithme et son importance
- Reconnaître l'adaptativité (performance sur données presque triées)
- Choisir l'algorithme approprié selon le contexte

### 4. **Paradigmes de Programmation**

- Maîtriser le paradigme "Diviser pour Régner"
- Comprendre la récursivité appliquée au tri
- Appliquer ces concepts à d'autres problèmes

---

## 📊 Progression Recommandée

**Rythme suggéré :** 2-3 leçons par semaine

```
Semaine 1 : Leçons 13-14 (Introduction et Tri à bulles)
Semaine 2 : Leçons 15-16 (Tri par sélection et insertion)
Semaine 3 : Leçons 17-18 (Tri fusion et tri rapide)
```

**Conseils :**

- Implémentez vous-même chaque algorithme avant de regarder la solution
- Tracez manuellement l'exécution sur papier avec de petits tableaux
- Comparez les performances avec différentes tailles de données
- Réalisez tous les exercices pratiques et quiz

---

## 💡 Avant de Passer au Module 4

Assurez-vous de maîtriser ces concepts avant de continuer :

- [ ] Je comprends pourquoi le tri est essentiel en informatique
- [ ] Je peux implémenter les trois tris élémentaires (bulles, sélection, insertion)
- [ ] Je sais expliquer la différence entre un tri stable et instable
- [ ] Je maîtrise le paradigme "Diviser pour Régner" et la récursivité
- [ ] Je peux implémenter le tri fusion avec ses fonctions `merge` et `mergeSort`
- [ ] Je comprends le rôle du pivot et le partitionnement de Lomuto
- [ ] Je sais comparer les complexités O(n²) et O(n log n)
- [ ] Je peux choisir l'algorithme approprié selon le contexte

Si vous avez répondu "oui" à toutes ces questions, vous êtes prêt pour le **Module 4 : Algorithmes de Recherche et Introduction à la Récursion** !

---

## 🔗 Ressources Complémentaires du Module

### Outils en Ligne

- [Visualgo - Sorting](https://visualgo.net/en/sorting) - Visualisation interactive de tous les algorithmes de tri
- [Sorting Algorithms Animations](https://www.toptal.com/developers/sorting-algorithms) - Comparaison visuelle des performances
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/) - Référence rapide des complexités

### Livres Recommandés

- **"Introduction to Algorithms"** de Cormen et al. - Chapitres sur le tri
- **"Grokking Algorithms"** de Aditya Bhargava - Approche visuelle accessible
- **"The Algorithm Design Manual"** de Steven Skiena - Applications pratiques

### Vidéos

- [MIT OpenCourseWare - Sorting](https://www.youtube.com/watch?v=Kg4bqzAqRBM) - Cours universitaire
- [CS50 - Algorithms](https://www.youtube.com/watch?v=yb0PY3LX2x8) - Harvard University
- [Sorting Algorithms Explained](https://www.youtube.com/watch?v=kPRA0W1kECg) - freeCodeCamp

---

## 💬 Besoin d'Aide ?

Si vous rencontrez des difficultés :

1. **Visualisez l'algorithme** - Tracez l'exécution sur papier ou utilisez les outils en ligne
2. **Comparez les approches** - Comprenez les différences entre chaque algorithme
3. **Testez avec de petits tableaux** - Commencez par 5-6 éléments avant de généraliser
4. **Expérimentez le code** - Modifiez les exemples pour observer les comportements
5. **Relisez les sections théoriques** - La compréhension du "pourquoi" aide le "comment"

---

## 🔄 Comparaison Rapide des Algorithmes de Tri

| Algorithme        | Temps (meilleur) | Temps (moyen) | Temps (pire) | Espace   | Stable |
| ----------------- | ---------------- | ------------- | ------------ | -------- | ------ |
| **Tri à bulles**  | O(n)             | O(n²)         | O(n²)        | O(1)     | ✅ Oui |
| **Tri sélection** | O(n²)            | O(n²)         | O(n²)        | O(1)     | ❌ Non |
| **Tri insertion** | O(n)             | O(n²)         | O(n²)        | O(1)     | ✅ Oui |
| **Tri fusion**    | O(n log n)       | O(n log n)    | O(n log n)   | O(n)     | ✅ Oui |
| **Tri rapide**    | O(n log n)       | O(n log n)    | O(n²)        | O(log n) | ❌ Non |

### Quand Utiliser Quel Algorithme ?

| Contexte                         | Algorithme Recommandé | Raison                              |
| -------------------------------- | --------------------- | ----------------------------------- |
| Petit tableau (< 10-20 éléments) | Tri par insertion     | Faible overhead, efficace           |
| Données presque triées           | Tri par insertion     | O(n) dans ce cas                    |
| Mémoire limitée                  | Tri rapide            | O(log n) espace vs O(n) pour fusion |
| Stabilité requise                | Tri fusion            | Stable et O(n log n) garanti        |
| Grande quantité de données       | Tri fusion / rapide   | O(n log n) vs O(n²)                 |
| Écriture mémoire coûteuse        | Tri par sélection     | Minimum d'échanges (n-1)            |

---

<div align="center">

**Module 3 sur 7 - Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"**

[⬅️ Module 2 : Structures de Données Essentielles en JavaScript](../module-2/README.md) | [Retour au sommaire principal](../../README.md) | [Module 4 : Algorithmes de Recherche et Introduction à la Récursion ➡️](../module-4/README.md)

---

_42 leçons pour maîtriser les algorithmes avec JavaScript_

</div>
