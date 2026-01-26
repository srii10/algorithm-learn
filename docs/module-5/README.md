# Module 5 : Arbres et Parcours de Graphes

## 📋 Vue d'ensemble

Ce module introduit les **structures de données non-linéaires** fondamentales : les arbres et les graphes. Vous apprendrez à les représenter, les manipuler et les parcourir efficacement avec les algorithmes BFS et DFS.

---

## 🎯 Objectifs du Module

À la fin de ce module, vous serez capable de :

- ✅ Comprendre la **terminologie** et les **types d'arbres**
- ✅ Implémenter et utiliser les **Arbres de Recherche Binaires (BST)**
- ✅ Représenter des **graphes** avec matrices et listes d'adjacence
- ✅ Implémenter le **parcours en largeur (BFS)**
- ✅ Implémenter le **parcours en profondeur (DFS)**
- ✅ Choisir le bon algorithme selon le problème

---

## 📚 Leçons du Module

| # | Leçon | Durée | Statut |
|---|-------|-------|--------|
| 25 | [Arbres : Terminologie, Types et Cas d'Usage](./lecon-1-arbres-terminologie-types-cas-usage.md) | 2h | ✅ |
| 26 | [Arbres de Recherche Binaires : Insertion et Recherche](./lecon-2-arbres-recherche-binaires-insertion-recherche-javascript.md) | 2h30 | ✅ |
| 27 | [Graphes : Concepts, Sommets, Arêtes et Représentations](./lecon-3-graphes-concepts-sommets-aretes-representations.md) | 2h30 | ✅ |
| 28 | [Implémentations Liste d'Adjacence et Matrice](./lecon-4-implementations-liste-adjacence-matrice-javascript.md) | 2h30 | ✅ |
| 29 | [Algorithme de Parcours en Largeur (BFS)](./lecon-5-algorithme-parcours-largeur-bfs-javascript.md) | 2h30 | ✅ |
| 30 | [Algorithme de Parcours en Profondeur (DFS)](./lecon-6-algorithme-parcours-profondeur-dfs-javascript.md) | 2h30 | ✅ |

**Durée totale estimée : ~14h30**

---

## 📊 Progression

```
Module 5 : [██████████] 100% (6/6 leçons)
```

---

## 🧠 Compétences Acquises

### Arbres

| Compétence | Description |
|------------|-------------|
| **Terminologie** | Nœud, racine, feuille, profondeur, hauteur |
| **Types d'arbres** | Binaire, BST, complet, parfait |
| **BST** | Insertion, recherche, complexité O(log n) |
| **Cas d'usage** | Systèmes de fichiers, DOM, indexation BD |

### Graphes

| Compétence | Description |
|------------|-------------|
| **Concepts** | Sommets, arêtes, orienté/non-orienté, pondéré |
| **Représentations** | Matrice d'adjacence, liste d'adjacence |
| **Trade-offs** | Quand utiliser chaque représentation |

### Algorithmes de Parcours

| Algorithme | Structure | Usage principal |
|------------|-----------|-----------------|
| **BFS** | File (Queue) | Chemin le plus court |
| **DFS** | Pile (Stack) | Exploration, détection cycles |
| **Pré-ordre** | Récursion | Copier un arbre |
| **In-ordre** | Récursion | BST trié |
| **Post-ordre** | Récursion | Supprimer un arbre |

---

## 📈 Complexités des Algorithmes

| Algorithme | Temps | Espace | Notes |
|------------|-------|--------|-------|
| **BST Insertion** | O(log n) moyen, O(n) pire | O(1) | Pire cas : arbre déséquilibré |
| **BST Recherche** | O(log n) moyen, O(n) pire | O(1) | |
| **BFS** | O(V + E) | O(V) | V=sommets, E=arêtes |
| **DFS** | O(V + E) | O(V) | |

---

## 🔗 Comparaison BFS vs DFS

| Critère | BFS | DFS |
|---------|-----|-----|
| **Structure** | File (FIFO) | Pile (LIFO) |
| **Exploration** | Niveau par niveau | En profondeur |
| **Chemin le + court** | ✅ Garanti (non pondéré) | ❌ Non garanti |
| **Détection cycles** | Possible | ✅ Idéal |
| **Mémoire** | Plus pour graphes larges | Plus pour graphes profonds |
| **Implémentation** | Itératif | Récursif ou itératif |

---

## 🗺️ Carte Conceptuelle

```
                    STRUCTURES NON-LINÉAIRES
                            |
            +---------------+---------------+
            |                               |
         ARBRES                          GRAPHES
            |                               |
    +-------+-------+               +-------+-------+
    |               |               |               |
 Binaire          BST          Orienté        Non-orienté
    |               |               |               |
    |        +------+------+       |               |
    |        |             |       |               |
    |    Insertion     Recherche   |               |
    |                              |               |
    +-------+------+---------------+-------+-------+
                   |
            PARCOURS/TRAVERSAL
                   |
        +----------+----------+
        |                     |
       BFS                   DFS
    (File)               (Pile/Récursion)
        |                     |
   Chemin court     +----+----+----+
                    |    |         |
                 Pré  In-ordre  Post
```

---

## 📚 Prérequis

- ✅ **Module 1** : Bases JavaScript
- ✅ **Module 2** : Structures linéaires (Files, Piles)
- ✅ **Module 4** : Récursion

---

## 🔗 Ressources Complémentaires

### Visualisation

- 🔗 [Visualgo - BST](https://visualgo.net/en/bst)
- 🔗 [Visualgo - BFS/DFS](https://visualgo.net/en/dfsbfs)

### Pratique

- 💻 [LeetCode - Trees](https://leetcode.com/tag/tree/)
- 💻 [LeetCode - Graph](https://leetcode.com/tag/graph/)
- 💻 [HackerRank - Trees](https://www.hackerrank.com/domains/data-structures?filters%5Bsubdomains%5D%5B%5D=trees)

---

## ➡️ Prochaine Étape

**Module 6 : Paradigmes Algorithmiques**

Vous maîtrisez maintenant les structures de données fondamentales et avancées. Le Module 6 vous apprendra les grandes stratégies de conception d'algorithmes :

- 🎯 Algorithmes Gloutons (Greedy)
- 🔀 Diviser pour Régner
- 💡 Programmation Dynamique

---

<div align="center">

**Module 5 sur 7 - Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"**

[⬅️ Module 4 : Recherche et Récursion](../module-4/README.md) | [Retour au sommaire](../../README.md) | [Module 6 : Paradigmes Algorithmiques ➡️](../module-6/README.md)

</div>
