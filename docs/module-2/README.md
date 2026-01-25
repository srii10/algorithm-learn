# 📘 Module 2 : Structures de Données Essentielles en JavaScript

<div align="center">

**Durée estimée : 15-18 heures**

_Maîtriser les structures de données linéaires fondamentales_

</div>

---

## 🎯 Objectifs du Module

Ce module vous enseigne les structures de données linéaires essentielles qui constituent la base de la programmation algorithmique. À la fin de ce module, vous serez capable de :

- ✅ Manipuler et optimiser les opérations sur les tableaux JavaScript
- ✅ Comprendre et implémenter des listes chaînées simples
- ✅ Créer et utiliser des piles (stacks) avec le principe LIFO
- ✅ Créer et utiliser des files (queues) avec le principe FIFO
- ✅ Choisir la structure de données appropriée selon le contexte
- ✅ Appliquer ces structures dans des scénarios réels de gestion de tâches

---

## 📚 Leçons du Module

### [Leçon 7 : Tableaux - Listes Dynamiques et Opérations de Base](./lecon-1-tableaux-listes-dynamiques-operations-base.md)

**Durée : 2h - 3h**

Exploration approfondie des tableaux JavaScript : création, manipulation, et analyse des opérations fondamentales pour comprendre leur efficacité.

**Concepts clés :**

- Caractéristiques des tableaux JavaScript
- Accès et modification d'éléments
- Opérations de base : `push()`, `pop()`, `shift()`, `unshift()`
- Recherche d'éléments : `indexOf()`, `includes()`
- Techniques de parcours et itération
- Analyse de complexité des opérations

---

### [Leçon 8 : Listes Chaînées - Concepts, Types et Parcours](./lecon-2-listes-chainees-concepts-types-parcours.md)

**Durée : 2h30 - 3h**

Introduction aux listes chaînées : une alternative aux tableaux offrant des avantages pour certaines opérations. Découverte des différents types et techniques de parcours.

**Concepts clés :**

- Structure fondamentale d'un nœud
- Types de listes chaînées (simple, doublement chaînée, circulaire)
- Parcours de listes chaînées
- Avantages vs inconvénients par rapport aux tableaux
- Applications pratiques dans les systèmes réels
- Analyse de complexité du parcours

---

### [Leçon 9 : Implémentation de Listes Chaînées Simples en JavaScript](./lecon-3-implementation-listes-chainees-simples-javascript.md)

**Durée : 3h - 3h30**

Implémentation complète d'une liste chaînée simple en JavaScript : de la classe Node jusqu'aux opérations d'ajout et de suppression.

**Concepts clés :**

- Classe `Node` pour représenter un nœud
- Classe `SinglyLinkedList` avec propriétés head, tail, length
- Méthode `push()` pour ajouter à la fin
- Méthode `pop()` pour retirer de la fin
- Méthodes `shift()` et `unshift()` pour le début
- Analyse de complexité de chaque opération

---

### [Leçon 10 : Piles - Principe LIFO et Implémentation Basée sur Tableaux](./lecon-4-piles-principe-lifo-implementation-tableaux.md)

**Durée : 2h30 - 3h**

Comprendre le principe LIFO (Last-In, First-Out) et implémenter une pile complète avec toutes ses opérations fondamentales.

**Concepts clés :**

- Principe LIFO (Last-In, First-Out)
- Cas d'usage réels des piles
- Implémentation complète avec tableaux
- Opérations fondamentales : push, pop, peek
- Analyse de complexité temporelle
- Résolution de problèmes pratiques

---

### [Leçon 11 : Files - Principe FIFO et Implémentation avec Tableaux](./lecon-5-files-principe-fifo-implementation-tableaux.md)

**Durée : 2h30 - 3h**

Découverte du principe FIFO (First-In, First-Out) et implémentation de files avec deux approches : simple et optimisée.

**Concepts clés :**

- Principe FIFO (First-In, First-Out)
- Opérations fondamentales : enqueue, dequeue, peek
- Implémentation simple avec `push()` et `shift()`
- Implémentation optimisée avec pointeurs
- Comparaison des performances
- Applications réelles (ordonnancement, serveurs, messages)

---

### [Leçon 12 : Pratique - Utiliser Piles/Files pour la Priorisation des Tâches](./lecon-6-pratique-utiliser-piles-files-priorisation-taches-etude-cas.md)

**Durée : 3h - 3h30**

Application pratique des piles et files dans des scénarios réels : système d'annulation/rétablissement, traitement séquentiel et gestion de tâches avec priorisation.

**Concepts clés :**

- Système Undo/Redo avec deux piles
- Traitement séquentiel de notifications avec files
- Gestionnaire de tâches avec priorisation (plusieurs files)
- Combinaison de structures pour problèmes complexes
- Exercices pratiques (historique navigateur, file d'impression)
- Choix de la structure appropriée selon le contexte

---

## 🎓 Compétences Acquises

À la fin de ce module, vous aurez acquis les compétences suivantes :

### 1. **Maîtrise des Structures Linéaires**

- Comprendre les caractéristiques de chaque structure
- Choisir la structure appropriée selon les besoins
- Analyser les compromis entre différentes approches

### 2. **Implémentation de Structures de Données**

- Créer des classes pour représenter des structures
- Implémenter les opérations fondamentales
- Gérer les cas limites et les erreurs

### 3. **Analyse de Performance**

- Évaluer la complexité de chaque opération
- Comparer les implémentations (simple vs optimisée)
- Identifier les goulots d'étranglement

### 4. **Résolution de Problèmes**

- Appliquer les structures à des cas réels
- Combiner plusieurs structures pour des solutions complexes
- Optimiser les performances selon le contexte

---

## 📊 Progression Recommandée

**Rythme suggéré :** 2 leçons par semaine

```
Semaine 1 : Leçons 7-8 (Tableaux et Listes chaînées - Concepts)
Semaine 2 : Leçon 9 (Listes chaînées - Implémentation)
Semaine 3 : Leçons 10-11 (Piles et Files)
Semaine 4 : Leçon 12 (Application pratique)
```

**Conseils :**

- Implémentez vous-même chaque structure de données
- Testez vos implémentations avec différents cas
- Comparez vos solutions avec les exemples fournis
- Réalisez tous les exercices pratiques
- Expérimentez avec les différentes approches

---

## 💡 Avant de Passer au Module 3

Assurez-vous de maîtriser ces concepts avant de continuer :

- [ ] Je comprends la différence entre tableaux et listes chaînées
- [ ] Je peux implémenter une liste chaînée simple de zéro
- [ ] Je maîtrise le principe LIFO et peux implémenter une pile
- [ ] Je maîtrise le principe FIFO et peux implémenter une file
- [ ] Je sais comparer les performances de différentes implémentations
- [ ] Je peux choisir la structure appropriée pour un problème donné
- [ ] Je sais combiner plusieurs structures pour résoudre des problèmes complexes

Si vous avez répondu "oui" à toutes ces questions, vous êtes prêt pour le **Module 3 : Techniques de Tri Essentielles** !

---

## 🔗 Ressources Complémentaires du Module

### Outils en Ligne

- [Visualgo - Data Structures](https://visualgo.net/en/list) - Visualisation interactive des structures
- [Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) - Animations pédagogiques
- [JavaScript Array Methods](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array) - Documentation MDN

### Livres Recommandés

- **"Introduction to Algorithms"** de Cormen et al. - Chapitres sur les structures de données
- **"Data Structures and Algorithms in JavaScript"** de Michael McMillan
- **"Grokking Algorithms"** de Aditya Bhargava - Approche visuelle et accessible

### Vidéos

- [CS50 - Data Structures](https://www.youtube.com/watch?v=4IrUAqYKjIA) - Harvard University
- [Data Structures Easy to Advanced](https://www.youtube.com/watch?v=RBSGKlAvoiM) - freeCodeCamp
- [JavaScript Algorithms and Data Structures](https://www.youtube.com/watch?v=t2CEgPsws3U) - Traversy Media

---

## 💬 Besoin d'Aide ?

Si vous rencontrez des difficultés :

1. **Visualisez les opérations** - Dessinez les structures sur papier pour mieux comprendre
2. **Codez étape par étape** - Implémentez une méthode à la fois et testez-la
3. **Utilisez les visualiseurs** - Les outils en ligne vous aident à voir ce qui se passe
4. **Comparez avec les solutions** - Analysez les différences avec les exemples
5. **Pratiquez régulièrement** - La répétition est clé pour maîtriser les structures

---

## 🔄 Comparaison Rapide des Structures

| Opération              | Tableau  | Liste Chaînée | Pile        | File             |
| ---------------------- | -------- | ------------- | ----------- | ---------------- |
| **Accès**              | O(1)     | O(n)          | O(n)        | O(n)             |
| **Recherche**          | O(n)     | O(n)          | O(n)        | O(n)             |
| **Insertion début**    | O(n)     | O(1)          | N/A         | N/A              |
| **Insertion fin**      | O(1)     | O(1)          | O(1) (push) | O(1) (enqueue)   |
| **Suppression début**  | O(n)     | O(1)          | N/A         | O(1)\* (dequeue) |
| **Suppression fin**    | O(1)     | O(n)          | O(1) (pop)  | N/A              |
| **Utilise la mémoire** | Continue | Dispersée     | Continue    | Continue         |

\* O(1) avec implémentation optimisée

---

<div align="center">

**Module 2 sur 7 - Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"**

[⬅️ Module 1 : Fondements des Algorithmes et Révision de JavaScript](../module-1/README.md) | [Retour au sommaire principal](../../README.md) | [Module 3 : Techniques de Tri Essentielles ➡️](../module-3/README.md)

---

_42 leçons pour maîtriser les algorithmes avec JavaScript_

</div>
