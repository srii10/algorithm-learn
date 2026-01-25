##### Leçon 10 sur 42

# Piles : Principe LIFO et Implémentation Basée sur Tableaux

**Module 2** : Structures de Données Essentielles en JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le principe **LIFO** (Last In, First Out)
- Identifier les **cas d'usage réels** des piles
- Implémenter une **pile complète** avec un tableau JavaScript
- Maîtriser les **opérations fondamentales** d'une pile
- Analyser la **complexité temporelle** des opérations
- Résoudre des **problèmes pratiques** utilisant des piles

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

Avant de commencer cette leçon, vous devez maîtriser :

- **Leçon 7 : Tableaux - Listes Dynamiques et Opérations de Base** - Compréhension des opérations sur les tableaux JavaScript (push, pop, length)
- **Leçon 2 : Introduction à JavaScript** - Connaissance de la syntaxe JavaScript, des classes ES6 et de la programmation orientée objet
- **Leçon 4 : Notation Big O** - Capacité à analyser la complexité temporelle des algorithmes

---

## 🚀 Introduction : Les Piles, Structures LIFO Fondamentales

## 1. 📦 Qu'est-ce qu'une Pile ?

### 1.1 Définition

Une **pile** (stack en anglais) est une structure de données linéaire qui suit un ordre spécifique d'opérations connu sous le nom de **Last-In, First-Out (LIFO)**. Cela signifie que le dernier élément ajouté à la pile est toujours le premier à être retiré.

Imaginez une pile d'assiettes :

```
    [Assiette 3] ← Sommet (dernier ajouté, premier retiré)
    [Assiette 2]
    [Assiette 1] ← Base (premier ajouté, dernier retiré)
```

- Vous ne pouvez **ajouter** une assiette qu'**au sommet**
- Vous ne pouvez **retirer** une assiette que **du sommet**
- Vous ne pouvez **pas accéder** directement aux assiettes du milieu ou de la base

### 1.2 Caractéristiques Clés

| Caractéristique         | Description                                            |
| ----------------------- | ------------------------------------------------------ |
| **Principe**            | LIFO (Last In, First Out)                              |
| **Point d'accès**       | Sommet uniquement                                      |
| **Opérations de base**  | push (ajouter), pop (retirer), peek (consulter)        |
| **Accès aux éléments**  | Aucun accès direct aux éléments internes               |
| **Ordre de traitement** | L'ordre de sortie est l'inverse de l'ordre d'insertion |

### 1.3 Visualisation Conceptuelle

Prenons un exemple avec des nombres :

```
Séquence d'opérations :
1. Ajouter 'A' → [A]
2. Ajouter 'B' → [A, B] (B au sommet)
3. Ajouter 'C' → [A, B, C] (C au sommet)
4. Retirer un élément → Retire 'C' (le dernier ajouté)

Résultat : [A, B]
```

Le dernier élément ajouté (`C`) est le premier retiré. C'est le cœur du principe LIFO.

---

## 2. 🔄 Le Principe LIFO

### 2.1 LIFO Expliqué en Détail

Le principe **Last-In, First-Out (LIFO)** définit comment les éléments sont accédés et gérés dans une pile :

- Quand un élément est **ajouté**, il est placé au "sommet" de la pile
- Quand un élément est **retiré**, c'est toujours celui qui est actuellement au "sommet"

Ce mécanisme d'ordonnancement strict est ce qui différencie une pile des autres structures comme les files ou les tableaux.

### 2.2 Séquence d'Opérations Détaillée

Analysons étape par étape :

```javascript
// État initial : pile vide
[]

// Opération 1 : push('A')
['A'] ← Sommet

// Opération 2 : push('B')
['A', 'B'] ← Sommet

// Opération 3 : push('C')
['A', 'B', 'C'] ← Sommet

// Opération 4 : pop()
// Retire 'C' (dernier ajouté)
['A', 'B'] ← Sommet (maintenant 'B')

// Opération 5 : pop()
// Retire 'B'
['A'] ← Sommet (maintenant 'A')

// Opération 6 : pop()
// Retire 'A'
[] ← Pile vide
```

**Observation clé :** L'ordre de sortie (`C`, `B`, `A`) est **l'inverse** de l'ordre d'entrée (`A`, `B`, `C`).

### 2.3 LIFO vs FIFO

Il est important de distinguer LIFO (pile) de FIFO (file) :

**LIFO - Last In, First Out (Pile)**

```
Ajout:
     [3]
     [2]      →      [4]  ← Nouveau sommet
     [1]             [3]
                     [2]
                     [1]

Retrait:
     [4]  ← Retiré en premier
     [3]      →      [3]  ← Nouveau sommet
     [2]             [2]
     [1]             [1]
```

**FIFO - First In, First Out (File)**

```
Entrée:           Sortie:
  [C][B][A] ←     → [A] (premier entré, premier sorti)
```

---

## 3. 🌍 Exemples Réels de Piles

### 3.1 Historique du Navigateur (Bouton "Retour")

Lorsque vous naviguez sur le web, chaque nouvelle page visitée est "poussée" sur une pile. Quand vous cliquez sur le bouton "Retour", le navigateur "dépile" la page la plus récemment visitée.

```javascript
// Simulation de l'historique du navigateur
Pile d'historique :
  1. Visite google.com       → [google.com]
  2. Visite github.com       → [google.com, github.com]
  3. Visite stackoverflow.com → [google.com, github.com, stackoverflow.com]

Clic sur "Retour" :
  4. Pop() → Retourne à github.com
     Pile : [google.com, github.com]

Clic sur "Retour" :
  5. Pop() → Retourne à google.com
     Pile : [google.com]
```

La page visitée en dernier est celle vers laquelle vous revenez en premier.

### 3.2 Fonction Annuler/Refaire dans les Logiciels

La plupart des éditeurs de texte, outils de conception graphique et autres applications implémentent Annuler/Refaire avec des piles.

```javascript
// Pile d'actions pour l'Annuler
Actions effectuées :
  1. Écrire "Bonjour"        → [Écrire "Bonjour"]
  2. Mettre en gras          → [Écrire "Bonjour", Mettre en gras]
  3. Ajouter un paragraphe   → [Écrire "Bonjour", Mettre en gras, Ajouter paragraphe]

Ctrl+Z (Annuler) :
  4. Pop() → Annule "Ajouter paragraphe"
     Pile : [Écrire "Bonjour", Mettre en gras]
```

Chaque action est poussée sur une "pile d'annulation". Quand vous sélectionnez "Annuler", la dernière action est dépilée et inversée. Une "pile de refaire" séparée pourrait stocker les actions annulées.

### 3.3 Scénario Hypothétique : Gestionnaire de Tâches

Dans notre étude de cas de gestion de tâches, imaginons une fonctionnalité pour suivre les tâches les plus récentes sur lesquelles l'utilisateur s'est concentré.

```javascript
// Pile de "focus" pour les tâches
Opérations :
  1. Travail sur "Tâche A"   → ["Tâche A"]
  2. Passage à "Tâche B"     → ["Tâche A", "Tâche B"]
  3. Passage à "Tâche C"     → ["Tâche A", "Tâche B", "Tâche C"]

"Retour à la tâche précédente" :
  4. Pop() → Retourne à "Tâche B"
     Pile : ["Tâche A", "Tâche B"]
```

Cela permet à l'utilisateur de revenir rapidement à la tâche la plus récente sur laquelle il travaillait.

---

## 📝 Micro-Exercice #1 : Comprendre le Principe LIFO

**Objectif :** Prédire le comportement d'une pile

Soit la séquence d'opérations suivante :

```javascript
// Opération 1: push("Rouge")
// Opération 2: push("Vert")
// Opération 3: push("Bleu")
// Opération 4: pop()
// Opération 5: push("Jaune")
// Opération 6: pop()
// Opération 7: pop()
```

**Questions :**

1. Quel est l'état de la pile après l'opération 3 ?
2. Quelle valeur est retournée par l'opération 4 (premier pop) ?
3. Quel est l'état final de la pile après toutes les opérations ?
4. Dans quel ordre les valeurs sont-elles retirées par les pop ?

<details>
<summary>💡 Voir la solution</summary>

**Traçons l'évolution étape par étape :**

```
Opération 1: push("Rouge")
["Rouge"] ← Sommet

Opération 2: push("Vert")
["Rouge", "Vert"] ← Sommet

Opération 3: push("Bleu")
["Rouge", "Vert", "Bleu"] ← Sommet
```

**Question 1 : État après opération 3**

```
["Rouge", "Vert", "Bleu"] ← Sommet
```

**Opération 4 : pop()**

```
Valeur retirée : "Bleu"
État après : ["Rouge", "Vert"] ← Sommet
```

**Question 2 : Valeur retournée par le premier pop**
**Réponse : "Bleu"**

**Opération 5 : push("Jaune")**

```
["Rouge", "Vert", "Jaune"] ← Sommet
```

**Opération 6 : pop()**

```
Valeur retirée : "Jaune"
État après : ["Rouge", "Vert"] ← Sommet
```

**Opération 7 : pop()**

```
Valeur retirée : "Vert"
État après : ["Rouge"] ← Sommet
```

**Question 3 : État final**

```
["Rouge"]
```

**Question 4 : Ordre des valeurs retirées**
Les valeurs retirées dans l'ordre sont : **"Bleu", "Jaune", "Vert"**

**Points clés :**

- Chaque pop retire l'élément au **sommet** (le dernier ajouté)
- L'ordre de sortie reflète l'ordre inverse d'insertion pour les éléments consécutifs
- Il faut toujours vérifier si la pile est vide avant un pop

</details>

---

## 4. 🔧 Opérations Fondamentales

Bien que les piles puissent être implémentées de diverses manières, les opérations de base restent cohérentes :

### 4.1 Vue d'Ensemble des Opérations

| Opération   | Description                                       | Complexité |
| ----------- | ------------------------------------------------- | ---------- |
| `push()`    | Ajoute un élément au sommet de la pile            | O(1)       |
| `pop()`     | Retire et retourne l'élément du sommet de la pile | O(1)       |
| `peek()`    | Retourne l'élément au sommet sans le retirer      | O(1)       |
| `isEmpty()` | Vérifie si la pile est vide                       | O(1)       |
| `size()`    | Retourne le nombre d'éléments dans la pile        | O(1)       |
| `clear()`   | Vide tous les éléments de la pile                 | O(1)       |

Toutes ces opérations sont en **O(1)** - temps constant ! C'est l'un des grands avantages des piles.

### 4.2 Description Détaillée des Opérations

**`push(element)`**

Ajoute un élément au sommet de la pile.

- **Entrée :** L'élément à ajouter
- **Sortie :** Généralement, retourne la nouvelle taille ou la pile elle-même
- **Effet secondaire :** Modifie la pile

**`pop()`**

Retire et retourne l'élément du sommet de la pile.

- **Entrée :** Aucune
- **Sortie :** L'élément retiré
- **Effet secondaire :** Modifie la pile
- **Cas limite :** Si la pile est vide, retourne `null` ou lève une erreur

**`peek()` (ou `top()`)**

Retourne l'élément au sommet de la pile sans le retirer.

- **Entrée :** Aucune
- **Sortie :** L'élément au sommet
- **Effet secondaire :** Aucun (lecture seule)
- **Cas limite :** Si la pile est vide, retourne `null`

**`isEmpty()`**

Vérifie si la pile contient des éléments.

- **Entrée :** Aucune
- **Sortie :** `true` si vide, `false` sinon
- **Effet secondaire :** Aucun

**`size()`**

Retourne le nombre d'éléments dans la pile.

- **Entrée :** Aucune
- **Sortie :** Un nombre entier représentant la taille
- **Effet secondaire :** Aucun

---

## 5. 💻 Implémentation avec un Tableau

### 5.1 Pourquoi Utiliser un Tableau ?

L'implémentation d'une pile avec un tableau JavaScript est simple et efficace car les tableaux supportent nativement des opérations qui imitent le comportement LIFO, principalement `push()` et `pop()`.

**Avantages :**

- **Simplicité :** Les méthodes de tableau sont déjà optimisées
- **Performance :** `push()` et `pop()` sont en O(1)
- **Familiarité :** Utilise des concepts JavaScript standard

### 5.2 Structure de Base

Voici notre classe `Stack` complète :

```javascript
class Stack {
  constructor() {
    this.items = []; // Un tableau pour stocker les éléments de la pile
  }

  // Ajoute un élément au sommet de la pile
  push(element) {
    this.items.push(element); // Utilise la méthode push du tableau
    console.log(`Poussé: ${element}. Pile: [${this.items.join(", ")}]`);
  }

  // Retire et retourne l'élément du sommet de la pile
  pop() {
    if (this.isEmpty()) {
      console.log("La pile est vide, impossible de dépiler.");
      return null; // Ou lever une erreur
    }
    const removedElement = this.items.pop(); // Utilise la méthode pop du tableau
    console.log(`Dépilé: ${removedElement}. Pile: [${this.items.join(", ")}]`);
    return removedElement;
  }

  // Retourne l'élément au sommet de la pile sans le retirer
  peek() {
    if (this.isEmpty()) {
      console.log("La pile est vide, aucun élément à consulter.");
      return null;
    }
    // Accède au dernier élément du tableau
    const topElement = this.items[this.items.length - 1];
    console.log(`Consulté: ${topElement}. Sommet de la pile.`);
    return topElement;
  }

  // Vérifie si la pile est vide
  isEmpty() {
    const empty = this.items.length === 0;
    console.log(`La pile est-elle vide ? ${empty}`);
    return empty;
  }

  // Retourne le nombre d'éléments dans la pile
  size() {
    const currentSize = this.items.length;
    console.log(`Taille de la pile: ${currentSize}`);
    return currentSize;
  }

  // Vide tous les éléments de la pile
  clear() {
    this.items = [];
    console.log("Pile vidée.");
  }

  // Méthode auxiliaire pour afficher le contenu de la pile
  printStack() {
    console.log(`Pile actuelle: [${this.items.join(", ")}]`);
  }
}
```

### 5.3 Explication de l'Implémentation

**`constructor()`**

Initialise un tableau JavaScript vide `this.items` qui contiendra les éléments de la pile. Le tableau `items` représente directement la pile.

**`push(element)`**

La méthode intégrée `push()` du tableau ajoute l'élément à la fin du tableau. Cette fin du tableau est traitée comme le "sommet" de notre pile, s'alignant parfaitement avec le principe LIFO.

**`pop()`**

La méthode intégrée `pop()` du tableau retire et retourne le dernier élément du tableau. Puisque le dernier élément ajouté a été poussé à la fin, `pop()` retire effectivement l'élément du "sommet" de notre pile. Une vérification est incluse pour éviter de dépiler une pile vide.

**`peek()`**

Pour voir l'élément du sommet sans le retirer, nous accédons simplement au dernier élément du tableau avec `this.items[this.items.length - 1]`. Une vérification pour une pile vide est ajoutée.

**`isEmpty()`**

Vérifie si le tableau `items` a une longueur de 0. Si c'est le cas, la pile est vide.

**`size()`**

Retourne la longueur actuelle du tableau `items`, qui correspond au nombre d'éléments dans la pile.

### 5.4 Démonstration Complète

```javascript
// Démonstration de l'implémentation Stack
const maPile = new Stack();

console.log("--- État initial ---");
maPile.isEmpty(); // Sortie: La pile est-elle vide ? true
maPile.size(); // Sortie: Taille de la pile: 0
maPile.printStack(); // Sortie: Pile actuelle: []

console.log("\n--- Opérations push ---");
maPile.push(10); // Poussé: 10. Pile: [10]
maPile.push(20); // Poussé: 20. Pile: [10, 20]
maPile.push(30); // Poussé: 30. Pile: [10, 20, 30]

console.log("\n--- Après les push ---");
maPile.printStack(); // Sortie: Pile actuelle: [10, 20, 30]
maPile.size(); // Sortie: Taille de la pile: 3
maPile.isEmpty(); // Sortie: La pile est-elle vide ? false

console.log("\n--- Opération peek ---");
maPile.peek(); // Consulté: 30. Sommet de la pile.

console.log("\n--- Opérations pop ---");
maPile.pop(); // Dépilé: 30. Pile: [10, 20]
maPile.peek(); // Consulté: 20. Sommet de la pile.
maPile.pop(); // Dépilé: 20. Pile: [10]
maPile.pop(); // Dépilé: 10. Pile: []
maPile.pop(); // La pile est vide, impossible de dépiler.
maPile.isEmpty(); // Sortie: La pile est-elle vide ? true
maPile.printStack(); // Sortie: Pile actuelle: []
```

**Analyse de la sortie :**

```
--- État initial ---
La pile est-elle vide ? true
Taille de la pile: 0
Pile actuelle: []

--- Opérations push ---
Poussé: 10. Pile: [10]
Poussé: 20. Pile: [10, 20]
Poussé: 30. Pile: [10, 20, 30]

--- Après les push ---
Pile actuelle: [10, 20, 30]
Taille de la pile: 3
La pile est-elle vide ? false

--- Opération peek ---
Consulté: 30. Sommet de la pile.

--- Opérations pop ---
Dépilé: 30. Pile: [10, 20]
Consulté: 20. Sommet de la pile.
Dépilé: 20. Pile: [10]
Dépilé: 10. Pile: []
La pile est vide, impossible de dépiler.
La pile est-elle vide ? true
Pile actuelle: []
```

### 5.5 Analyse de Complexité

Cette implémentation basée sur un tableau est efficace pour la plupart des utilisations pratiques grâce à l'optimisation des méthodes intégrées de JavaScript pour ajouter/retirer des éléments à la fin.

| Opération   | Complexité | Justification                        |
| ----------- | ---------- | ------------------------------------ |
| `push()`    | O(1)       | Ajout à la fin d'un tableau (amorti) |
| `pop()`     | O(1)       | Retrait à la fin d'un tableau        |
| `peek()`    | O(1)       | Accès direct par index               |
| `isEmpty()` | O(1)       | Vérification de la longueur          |
| `size()`    | O(1)       | Propriété `length` du tableau        |
| `clear()`   | O(1)       | Réassignation de tableau             |

**Pourquoi "amorti" pour `push()` ?**

Occasionnellement, si le tableau interne doit être redimensionné (doublé), cela prend O(n). Mais ces redimensionnements sont rares, donc en moyenne, c'est O(1).

---

## 📝 Micro-Exercice #2 : Implémenter et Tester

**Objectif :** Manipuler une pile et observer son comportement

**Instructions :**

1. Créez une instance de `Stack`
2. Poussez les valeurs suivantes : "Chat", "Chien", "Oiseau", "Poisson"
3. Affichez la taille de la pile
4. Consultez le sommet avec `peek()`
5. Dépilez deux éléments
6. Affichez la pile
7. Poussez "Lapin"
8. Affichez l'élément au sommet
9. Videz la pile et vérifiez qu'elle est vide

<details>
<summary>💡 Voir la solution</summary>

```javascript
// Créer une instance
const animauxPile = new Stack();

// 1. Pousser des valeurs
animauxPile.push("Chat");
// Poussé: Chat. Pile: [Chat]
animauxPile.push("Chien");
// Poussé: Chien. Pile: [Chat, Chien]
animauxPile.push("Oiseau");
// Poussé: Oiseau. Pile: [Chat, Chien, Oiseau]
animauxPile.push("Poisson");
// Poussé: Poisson. Pile: [Chat, Chien, Oiseau, Poisson]

// 2. Afficher la taille
animauxPile.size();
// Taille de la pile: 4

// 3. Consulter le sommet
animauxPile.peek();
// Consulté: Poisson. Sommet de la pile.

// 4. Dépiler deux éléments
animauxPile.pop();
// Dépilé: Poisson. Pile: [Chat, Chien, Oiseau]
animauxPile.pop();
// Dépilé: Oiseau. Pile: [Chat, Chien]

// 5. Afficher la pile
animauxPile.printStack();
// Pile actuelle: [Chat, Chien]

// 6. Pousser "Lapin"
animauxPile.push("Lapin");
// Poussé: Lapin. Pile: [Chat, Chien, Lapin]

// 7. Afficher le sommet
animauxPile.peek();
// Consulté: Lapin. Sommet de la pile.

// 8. Vider la pile
animauxPile.clear();
// Pile vidée.

// 9. Vérifier qu'elle est vide
animauxPile.isEmpty();
// La pile est-elle vide ? true
```

**Observations :**

- Les éléments sont retirés dans l'ordre **inverse** de leur ajout (LIFO)
- `peek()` permet de voir le sommet **sans modifier** la pile
- `clear()` vide instantanément la pile
- Toutes les opérations sont **rapides** (O(1))

</details>

---

## 6. 💪 Exercices Pratiques

### Exercice 1 : Inverser une Chaîne

Utilisez la classe `Stack` pour écrire une fonction JavaScript `reverseString(str)` qui prend une chaîne en entrée et retourne la chaîne inversée.

**Indice :** Parcourez la chaîne d'entrée en poussant chaque caractère sur la pile. Ensuite, dépilez les caractères et concaténez-les pour former la chaîne inversée.

```javascript
// Exemple d'utilisation :
console.log(reverseString("bonjour")); // Sortie attendue: "ruojnob"
console.log(reverseString("JavaScript")); // Sortie attendue: "tpircSavaJ"
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function reverseString(str) {
  const pile = new Stack();

  // Pousser chaque caractère sur la pile
  for (let char of str) {
    pile.push(char);
  }

  // Dépiler pour construire la chaîne inversée
  let reversed = "";
  while (!pile.isEmpty()) {
    reversed += pile.pop();
  }

  return reversed;
}

// Tests
console.log(reverseString("bonjour")); // "ruojnob"
console.log(reverseString("JavaScript")); // "tpircSavaJ"
console.log(reverseString("A")); // "A"
console.log(reverseString("")); // ""
```

**Explication détaillée pour "bonjour" :**

```
Étape 1: Pousser chaque caractère
  Push 'b' → Pile: ['b']
  Push 'o' → Pile: ['b', 'o']
  Push 'n' → Pile: ['b', 'o', 'n']
  Push 'j' → Pile: ['b', 'o', 'n', 'j']
  Push 'o' → Pile: ['b', 'o', 'n', 'j', 'o']
  Push 'u' → Pile: ['b', 'o', 'n', 'j', 'o', 'u']
  Push 'r' → Pile: ['b', 'o', 'n', 'j', 'o', 'u', 'r']

Étape 2: Dépiler et construire la chaîne inversée
  Pop 'r' → reversed = "r"
  Pop 'u' → reversed = "ru"
  Pop 'o' → reversed = "ruo"
  Pop 'j' → reversed = "ruoj"
  Pop 'n' → reversed = "ruojn"
  Pop 'o' → reversed = "ruojno"
  Pop 'b' → reversed = "ruojnob"

Résultat: "ruojnob"
```

**Complexité :**

- **Temps :** O(n) - Deux parcours (push et pop)
- **Espace :** O(n) - La pile stocke tous les caractères

**Pourquoi utiliser une pile ?**
La pile inverse naturellement l'ordre (LIFO), parfait pour cette tâche !

</details>

---

### Exercice 2 : Vérifier les Parenthèses Équilibrées

Écrivez une fonction JavaScript `isBalanced(expression)` qui prend une chaîne contenant une expression arithmétique avec des parenthèses, accolades et crochets (`()`, `{}`, `[]`) et détermine si les parenthèses sont équilibrées.

Une expression est équilibrée si :

- Chaque crochet ouvrant a un crochet fermant correspondant
- Les crochets sont correctement imbriqués

**Indice :** Parcourez l'expression. Si vous rencontrez un crochet ouvrant, poussez-le sur la pile. Si vous rencontrez un crochet fermant, dépilez un élément de la pile et vérifiez s'il correspond au crochet ouvrant. Si la pile est vide à la fin et que tous les crochets correspondent, l'expression est équilibrée.

```javascript
// Exemple d'utilisation :
console.log(isBalanced("{[()]}")); // Sortie attendue: true
console.log(isBalanced("([{}])")); // Sortie attendue: true
console.log(isBalanced("({[})")); // Sortie attendue: false (mal appariés)
console.log(isBalanced("(()")); // Sortie attendue: false (non fermé)
console.log(isBalanced("})")); // Sortie attendue: false (fermant sans ouverture)
console.log(isBalanced("")); // Sortie attendue: true (chaîne vide est équilibrée)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function isBalanced(expression) {
  const pile = new Stack();
  const openingBrackets = ["(", "[", "{"];
  const closingBrackets = [")", "]", "}"];
  const pairs = {
    ")": "(",
    "]": "[",
    "}": "{",
  };

  for (let char of expression) {
    // Si c'est un symbole ouvrant, empiler
    if (openingBrackets.includes(char)) {
      pile.push(char);
    }
    // Si c'est un symbole fermant
    else if (closingBrackets.includes(char)) {
      // Vérifier si la pile est vide (pas d'ouverture correspondante)
      if (pile.isEmpty()) {
        return false;
      }

      // Vérifier si le symbole fermant correspond au dernier ouvrant
      const lastOpening = pile.pop();
      if (lastOpening !== pairs[char]) {
        return false;
      }
    }
  }

  // À la fin, la pile doit être vide (tous les symboles sont appariés)
  return pile.isEmpty();
}

// Tests
console.log(isBalanced("{[()]}")); // true
console.log(isBalanced("([{}])")); // true
console.log(isBalanced("({[})")); // false (mauvais ordre)
console.log(isBalanced("(()")); // false (non équilibré)
console.log(isBalanced("})")); // false (trop de fermants)
console.log(isBalanced("")); // true (vide est équilibré)
console.log(isBalanced("{[()]}")); // true
```

**Traçage pour `"{[()]}"`:**

```
Expression: { [ ( ) ] }

Étape 1: Caractère '{'
  Action: Push '{'
  Pile: ['{']

Étape 2: Caractère '['
  Action: Push '['
  Pile: ['{', '[']

Étape 3: Caractère '('
  Action: Push '('
  Pile: ['{', '[', '(']

Étape 4: Caractère ')'
  Action: Pop → '(' correspond à ')'
  Pile: ['{', '[']

Étape 5: Caractère ']'
  Action: Pop → '[' correspond à ']'
  Pile: ['{']

Étape 6: Caractère '}'
  Action: Pop → '{' correspond à '}'
  Pile: []

Résultat: Pile vide → true (équilibré)
```

**Traçage pour `"({[})"`:**

```
Expression: ( { [ } )

Étape 1: '(' → Push '(' → Pile: ['(']
Étape 2: '{' → Push '{' → Pile: ['(', '{']
Étape 3: '[' → Push '[' → Pile: ['(', '{', '[']
Étape 4: '}' → Pop '[' → '[' ≠ '{' → Retourne false
```

**Pourquoi une pile ?**

- Les symboles ouvrants sont traités dans l'ordre **inverse** de leur fermeture
- Le dernier symbole ouvert doit être le premier fermé (LIFO)
- Une pile est la structure parfaite pour ce problème

**Complexité :**

- **Temps :** O(n) - Un seul parcours de la chaîne
- **Espace :** O(n) - Dans le pire cas, tous les caractères sont des ouvrants

</details>

---

### Exercice 3 : Pile avec Capacité Limitée

Modifiez la classe `Stack` pour créer une `LimitedStack` qui a une capacité maximale. Si `push()` est appelé quand la pile est pleine, il ne doit pas ajouter l'élément et optionnellement afficher un message.

```javascript
class LimitedStack {
  constructor(capacity) {
    // Votre code ici : Initialiser le tableau items et la capacité
  }

  push(element) {
    // Votre code ici : Vérifier la capacité avant de pousser
  }

  // Les autres méthodes (pop, peek, isEmpty, size) peuvent être similaires à la classe Stack originale
}

// Exemple d'utilisation :
const limitedStack = new LimitedStack(3);
limitedStack.push(1);
limitedStack.push(2);
limitedStack.push(3);
limitedStack.push(4); // Devrait afficher un message que la pile est pleine et ne pas ajouter 4
console.log(limitedStack.size()); // Sortie attendue: 3
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class LimitedStack {
  constructor(capacity) {
    this.items = [];
    this.capacity = capacity; // Capacité maximale
  }

  push(element) {
    // Vérifier si la pile est pleine
    if (this.items.length >= this.capacity) {
      console.log(
        `Pile pleine ! Impossible d'ajouter ${element}. Capacité max: ${this.capacity}`,
      );
      return false;
    }

    this.items.push(element);
    console.log(`Poussé: ${element}. Pile: [${this.items.join(", ")}]`);
    return true;
  }

  pop() {
    if (this.isEmpty()) {
      console.log("La pile est vide, impossible de dépiler.");
      return null;
    }
    const removedElement = this.items.pop();
    console.log(`Dépilé: ${removedElement}. Pile: [${this.items.join(", ")}]`);
    return removedElement;
  }

  peek() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  isFull() {
    return this.items.length === this.capacity;
  }

  getCapacity() {
    return this.capacity;
  }

  printStack() {
    console.log(
      `Pile [${this.items.length}/${this.capacity}]: [${this.items.join(", ")}]`,
    );
  }
}

// Tests
const limitedStack = new LimitedStack(3);

console.log("--- Test de capacité limitée ---");
limitedStack.push(1); // Poussé: 1. Pile: [1]
limitedStack.push(2); // Poussé: 2. Pile: [1, 2]
limitedStack.push(3); // Poussé: 3. Pile: [1, 2, 3]
limitedStack.printStack(); // Pile [3/3]: [1, 2, 3]

limitedStack.push(4);
// Pile pleine ! Impossible d'ajouter 4. Capacité max: 3

console.log("\nTaille:", limitedStack.size()); // 3
console.log("Pleine?", limitedStack.isFull()); // true

limitedStack.pop(); // Dépilé: 3. Pile: [1, 2]
console.log("Pleine?", limitedStack.isFull()); // false

limitedStack.push(4); // Poussé: 4. Pile: [1, 2, 4]
limitedStack.printStack(); // Pile [3/3]: [1, 2, 4]
```

**Résultat de l'exécution :**

```
--- Test de capacité limitée ---
Poussé: 1. Pile: [1]
Poussé: 2. Pile: [1, 2]
Poussé: 3. Pile: [1, 2, 3]
Pile [3/3]: [1, 2, 3]
Pile pleine ! Impossible d'ajouter 4. Capacité max: 3

Taille: 3
Pleine? true
Dépilé: 3. Pile: [1, 2]
Pleine? false
Poussé: 4. Pile: [1, 2, 4]
Pile [3/3]: [1, 2, 4]
```

**Points clés :**

- **Vérification de capacité** avant chaque `push()`
- **Méthode `isFull()`** pour vérifier l'état
- **Gestion d'erreur** avec retour `false` et message
- **Utile pour** : Limiter l'utilisation mémoire, simuler des buffers fixes

**Applications :**

- Buffer de taille fixe pour traitement de données
- Historique d'annulation limité (ex: 50 dernières actions)
- Cache avec limite de taille

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

Quelle est la complexité temporelle de l'opération `push()` sur une pile implémentée avec un tableau JavaScript ?

- [ ] A) O(1)
- [ ] B) O(log n)
- [ ] C) O(n)
- [ ] D) O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : A) O(1)**

**Explication :**

L'opération `push()` sur une pile basée sur un tableau JavaScript utilise `array.push()`, qui ajoute un élément à la fin du tableau en temps constant (amorti).

```javascript
push(element) {
  this.items.push(element); // O(1) amorti
}
```

**Pourquoi O(1) ?**

- Pas besoin de décaler d'autres éléments
- Pas de parcours du tableau
- Ajout direct à la fin

**Pourquoi "amorti" ?**

Occasionnellement, si le tableau interne doit être redimensionné (doublé), cela prend O(n). Mais ces redimensionnements sont rares, donc en moyenne sur plusieurs opérations, c'est O(1).

**Pourquoi pas les autres ?**

- **O(log n)** : Complexité de recherche binaire, non applicable
- **O(n)** : Nécessiterait un parcours complet
- **O(n²)** : Nécessiterait des boucles imbriquées

</details>

---

### Question 2

Quel est l'ordre de sortie d'une pile après ces opérations :
`push(10), push(20), pop(), push(30), push(40), pop(), pop()` ?

- [ ] A) 10, 20, 30
- [ ] B) 20, 40, 30
- [ ] C) 40, 30, 20
- [ ] D) 30, 40, 10

<details>
<summary>Voir la réponse</summary>

**Réponse : B) 20, 40, 30**

**Traçage étape par étape :**

```
État initial: []

push(10):
  Pile: [10]

push(20):
  Pile: [10, 20] ← Sommet

pop():
  Valeur retirée: 20 ← Premier élément de sortie
  Pile: [10]

push(30):
  Pile: [10, 30]

push(40):
  Pile: [10, 30, 40] ← Sommet

pop():
  Valeur retirée: 40 ← Deuxième élément de sortie
  Pile: [10, 30]

pop():
  Valeur retirée: 30 ← Troisième élément de sortie
  Pile: [10]
```

**Ordre de sortie : 20, 40, 30**

**Visualisation graphique :**

```
Opération       État de la pile        Sortie
─────────────────────────────────────────────────
push(10)        [10]                   -
push(20)        [10, 20]               -
pop()           [10]                   → 20
push(30)        [10, 30]               -
push(40)        [10, 30, 40]           -
pop()           [10, 30]               → 40
pop()           [10]                   → 30
```

**Pourquoi pas les autres ?**

- **A) 10, 20, 30** : 10 n'est jamais retiré
- **C) 40, 30, 20** : L'ordre est correct pour 40 et 30, mais 20 est retiré avant
- **D) 30, 40, 10** : L'ordre est inversé

</details>

---

### Question 3

Quelle structure de données JavaScript utilise pour gérer les appels de fonctions ?

- [ ] A) File (Queue)
- [ ] B) Pile (Stack)
- [ ] C) Liste chaînée
- [ ] D) Arbre

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Pile (Stack)**

**Explication :**

JavaScript utilise une **pile d'appels** (call stack) pour gérer l'exécution des fonctions. C'est un mécanisme LIFO :

- La dernière fonction appelée est la première exécutée (et terminée)
- Quand une fonction termine, elle est retirée du sommet de la pile
- Le contrôle retourne à la fonction appelante

**Exemple :**

```javascript
function a() {
  console.log("Début A");
  b();
  console.log("Fin A");
}

function b() {
  console.log("Début B");
  c();
  console.log("Fin B");
}

function c() {
  console.log("C");
}

a();
```

**Pile d'appels au fil du temps :**

```
Appel de a():
  [a] ← a commence

Appel de b() depuis a:
  [b]
  [a] ← a attend

Appel de c() depuis b:
  [c] ← c s'exécute (sommet)
  [b]
  [a]

c() termine:
  [b] ← b reprend
  [a]

b() termine:
  [a] ← a reprend

a() termine:
  [] ← Pile vide
```

**Sortie :**

```
Début A
Début B
C
Fin B
Fin A
```

**Débordement de pile :**

Si la pile d'appels devient trop profonde (récursion infinie), vous obtenez une **erreur de débordement** (stack overflow).

```javascript
function infinite() {
  infinite(); // Récursion sans condition d'arrêt
}

infinite();
// Erreur: RangeError: Maximum call stack size exceeded
```

</details>

---

### Question 4

Quelle est l'application la plus appropriée pour une pile ?

- [ ] A) Gestion d'une file d'attente à un guichet
- [ ] B) Fonction "Annuler" dans un éditeur de texte
- [ ] C) Liste de lecture musicale en continu
- [ ] D) Gestion FIFO des processus

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Fonction "Annuler" dans un éditeur de texte**

**Explication :**

La fonction "Annuler" (Undo) est l'application parfaite d'une pile car :

- La **dernière action** effectuée doit être la **première annulée** (LIFO)
- Chaque action est empilée au moment où elle est effectuée
- Ctrl+Z dépile la dernière action

**Exemple :**

```javascript
Actions:
  1. Écrire "Bonjour"  → Push
  2. Mettre en gras    → Push
  3. Ajouter un espace → Push

Pile: [Ajouter espace, Mettre en gras, Écrire "Bonjour"]

Undo (Ctrl+Z):
  Pop → Annule "Ajouter espace"
  Pop → Annule "Mettre en gras"
  Pop → Annule "Écrire Bonjour"
```

**Pourquoi pas les autres ?**

**A) File d'attente à un guichet**

- Nécessite une **file (FIFO)**, pas une pile
- Le premier arrivé doit être le premier servi

**C) Liste de lecture musicale en continu**

- Nécessite une **file** ou une **liste circulaire**
- Les chansons sont jouées dans l'ordre d'ajout

**D) Gestion FIFO des processus**

- FIFO = File, pas Pile
- Les processus ne sont pas traités en LIFO

**Autres bonnes applications de piles :**

- Historique de navigation (bouton "Retour")
- Vérification de parenthèses équilibrées
- Évaluation d'expressions postfixes
- Pile d'appels de fonctions
- Backtracking dans les algorithmes

</details>

---

### Question 5

Quelle est la complexité spatiale d'une pile contenant n éléments ?

- [ ] A) O(1)
- [ ] B) O(log n)
- [ ] C) O(n)
- [ ] D) O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C) O(n)**

**Explication :**

Une pile contenant **n éléments** nécessite un espace proportionnel à **n**.

```javascript
const pile = new Stack();

// Ajouter n éléments
for (let i = 0; i < n; i++) {
  pile.push(i); // Chaque élément occupe de l'espace
}

// Espace total utilisé: O(n)
```

**Détails :**

- Chaque élément occupe un espace constant
- Pour n éléments : n × constant = **O(n)**

**Pourquoi pas les autres ?**

- **O(1)** : Espace constant, ne dépend pas de n (impossible pour n éléments)
- **O(log n)** : Espace logarithmique (arbres binaires équilibrés)
- **O(n²)** : Espace quadratique (matrices n×n)

**Comparaison :**

| Structure     | n éléments | Complexité spatiale |
| ------------- | ---------- | ------------------- |
| Pile          | n          | O(n)                |
| File          | n          | O(n)                |
| Liste chaînée | n          | O(n) + overhead     |
| Tableau       | n          | O(n)                |

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe LIFO

**Last In, First Out** : le dernier élément ajouté est le premier retiré. Le sommet est le seul point d'accès. L'ordre de sortie est l'**inverse** de l'ordre d'entrée.

### 2. Opérations Fondamentales

Toutes les opérations sont en **O(1)** : `push()` (ajouter au sommet), `pop()` (retirer du sommet), `peek()` (consulter sans retirer), `isEmpty()` (vérifier si vide), `size()` (nombre d'éléments).

### 3. Implémentation avec Tableau

Utilise les méthodes natives `array.push()` et `array.pop()`. Simple, efficace et optimisée en JavaScript. Le dernier élément du tableau représente le sommet de la pile.

### 4. Applications Réelles

Fonction **Undo/Redo** dans les éditeurs, **historique de navigation** (bouton retour), **vérification de parenthèses équilibrées**, et **pile d'appels de fonctions** (call stack JavaScript).

### 5. Avantages

Opérations **très rapides** (O(1)), **simple à implémenter**, utilisation mémoire **prévisible**, et structure **naturelle** pour de nombreux problèmes algorithmiques.

### 6. Limitations

Pas d'**accès direct** aux éléments internes, pas de **parcours facile**, et manipulation **limitée au sommet** uniquement. Choisir une autre structure si l'accès aléatoire est nécessaire.

### 7. Pile vs File

| Aspect  | Pile (LIFO)      | File (FIFO)    |
| ------- | ---------------- | -------------- |
| Ajout   | Sommet           | Fin            |
| Retrait | Sommet           | Début          |
| Usage   | Undo, historique | File d'attente |

---

## ➡️ Prochaine Étape : Leçon 11

### Ce qui vous attend

Dans la prochaine leçon, **« Files : Principe FIFO et Implémentation Basée sur Tableaux »**, vous allez découvrir la structure "opposée" à la pile : la file d'attente.

**Vous découvrirez :**

- Le principe **FIFO** (First In, First Out) et sa logique intuitive
- Comment implémenter une file avec un tableau JavaScript
- Les applications réelles : files d'attente, traitement de tâches, BFS
- La comparaison entre piles (LIFO) et files (FIFO)

### Préparez-vous !

Réfléchissez aux situations où l'ordre d'arrivée compte : une file d'attente au supermarché, les impressions dans une imprimante, les messages dans une messagerie. La file est partout !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [VisuAlgo - Stack](https://visualgo.net/en/list) - Visualisation animée des piles
- [MDN - Array.prototype.push()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/push) - Documentation officielle
- [Stack Visualizer](https://www.cs.usfca.edu/~galles/visualization/StackArray.html) - Outil pédagogique interactif

### Outils utiles

- **[LeetCode - Stack Problems](https://leetcode.com/tag/stack/)** : Exercices pour pratiquer
- **[HackerRank - Stacks](https://www.hackerrank.com/domains/data-structures?filters%5Bsubdomains%5D%5B%5D=stacks)** : Défis progressifs

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices
- Visualiser physiquement en empilant des objets réels (livres, assiettes)

> 💡 **Conseil**
>
> Pour bien ancrer le concept LIFO, prenez une pile d'assiettes chez vous et simulez les opérations `push()` et `pop()`. Vous ne pouvez ajouter ou retirer que l'assiette du dessus ! Cette manipulation concrète rend le concept immédiatement intuitif.

---

**Prêt pour la Leçon 11 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir les files et le principe FIFO !

---

<div align="center">

**Leçon 10 sur 42 - Module 2 : Structures de Données Essentielles en JavaScript**

[⬅️ Leçon 9 : Implémentation de Listes Chaînées Simples en JavaScript](./lecon-3-implementation-listes-chainees-simples-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 11 : Files - Principe FIFO et Implémentation Basée sur Tableaux ➡️](./lecon-5-files-principe-fifo-implementation-tableaux.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
