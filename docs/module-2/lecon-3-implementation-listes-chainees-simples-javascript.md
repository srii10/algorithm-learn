##### Leçon 9 sur 42

# Implémentation de Listes Chaînées Simples en JavaScript

**Module 2** : Structures de Données Essentielles en JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Définir et implémenter une classe `Node` pour représenter un nœud de liste chaînée
- Créer une classe `SinglyLinkedList` complète avec les propriétés head, tail et length
- Implémenter la méthode `push()` pour ajouter des éléments à la fin de la liste
- Implémenter la méthode `pop()` pour retirer des éléments de la fin de la liste
- Implémenter les méthodes `shift()` et `unshift()` pour manipuler le début de la liste
- Analyser la complexité temporelle de chaque opération

---

### ⏱️ Durée estimée : 3h00 - 3h30

---

## 📚 Prérequis

Avant de commencer cette leçon, assurez-vous de maîtriser :

- **Leçon 8** : Listes Chaînées - Concepts, Types et Parcours
- Les classes JavaScript (ES6+)
- Les références et pointeurs en JavaScript
- La notation Big O pour l'analyse de complexité

---

## 🚀 Introduction

### Du Concept à la Pratique

Dans la leçon précédente, vous avez découvert les **concepts théoriques** des listes chaînées : leur structure, leurs types, et comment les parcourir. Maintenant, il est temps de passer à la **pratique** !

Dans cette leçon, vous allez **construire de zéro** une liste chaînée simple entièrement fonctionnelle en JavaScript. Vous apprendrez à :

- Créer la structure de base d'un nœud
- Assembler les nœuds pour former une liste
- Implémenter les opérations fondamentales (ajout, suppression)
- Gérer les cas limites (liste vide, un seul élément)

### Pourquoi Implémenter Nous-Mêmes ?

Bien que JavaScript n'ait pas de liste chaînée native (contrairement aux tableaux), implémenter cette structure vous-même vous permet de :

1. **Comprendre en profondeur** comment les structures de données fonctionnent
2. **Maîtriser les références** et la manipulation de pointeurs
3. **Préparer le terrain** pour des structures plus complexes (arbres, graphes)
4. **Développer votre pensée algorithmique**

### Point Clé à Retenir

> **Une implémentation de liste chaînée nécessite deux composants : une classe `Node` pour représenter chaque élément, et une classe `SinglyLinkedList` pour gérer l'ensemble de la structure avec ses opérations.**

---

## 1. 🏗️ Comprendre la Structure d'un Nœud

### 1.1 Qu'est-ce qu'un Nœud ?

Un nœud est le **bloc de construction fondamental** d'une liste chaînée. Chaque nœud contient :

1. **Les données** : La valeur que vous souhaitez stocker
2. **Une référence `next`** : Un pointeur vers le nœud suivant

Imaginez un wagon de train :

- Le wagon transporte des marchandises (les **données**)
- Le wagon est attaché au wagon suivant par un crochet (la **référence next**)

### 1.2 Implémentation de la Classe Node

Voici comment créer une classe `Node` en JavaScript :

```javascript
class Node {
  constructor(value) {
    this.value = value; // Les données stockées dans ce nœud
    this.next = null; // Référence au nœud suivant (initialement null)
  }
}
```

**Analyse de la structure :**

- **`value`** : Peut contenir n'importe quel type de données (nombre, chaîne, objet, etc.)
- **`next`** : Initialisé à `null` car un nœud créé n'est pas encore lié à un autre

### 1.3 Créer des Nœuds Individuels

```javascript
// Exemple 1 : Créer un nœud simple
const firstNode = new Node(10);
console.log(firstNode);
// Output: Node { value: 10, next: null }

console.log(firstNode.value); // 10
console.log(firstNode.next); // null
```

**Visualisation :**

```
[10 | null]
```

Le nœud contient la valeur 10 et `next` est `null` (pas de nœud suivant).

### 1.4 Relier des Nœuds Manuellement

Avant d'implémenter notre classe de liste, voyons comment relier des nœuds manuellement :

```javascript
// Créer trois nœuds séparés
const nodeA = new Node("Pomme");
const nodeB = new Node("Banane");
const nodeC = new Node("Cerise");

// Les relier manuellement
nodeA.next = nodeB; // Pomme → Banane
nodeB.next = nodeC; // Banane → Cerise
// nodeC.next reste null (fin de la liste)

console.log(nodeA);
// Node {
//   value: 'Pomme',
//   next: Node {
//     value: 'Banane',
//     next: Node { value: 'Cerise', next: null }
//   }
// }

// Accéder aux valeurs en suivant les liens
console.log(nodeA.value); // "Pomme"
console.log(nodeA.next.value); // "Banane"
console.log(nodeA.next.next.value); // "Cerise"
```

**Visualisation :**

```
[Pomme | •]--→[Banane | •]--→[Cerise | null]
   nodeA         nodeB          nodeC
```

La propriété `next` établit la **chaîne** qui forme la liste chaînée.

---

## 📝 Micro-Exercice #1 : Créer et Lier des Nœuds

**Objectif** : Pratiquer la création et la liaison de nœuds.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

// À FAIRE : Créez trois nœuds avec les valeurs 100, 200, 300
// Reliez-les pour former une chaîne : 100 → 200 → 300

// Votre code ici
let node1 = // ...
let node2 = // ...
let node3 = // ...

// Testez votre chaîne
console.log(node1.value);           // Devrait afficher 100
console.log(node1.next.value);      // Devrait afficher 200
console.log(node1.next.next.value); // Devrait afficher 300
console.log(node3.next);            // Devrait afficher null
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

// Créer les trois nœuds
let node1 = new Node(100);
let node2 = new Node(200);
let node3 = new Node(300);

// Relier les nœuds
node1.next = node2;
node2.next = node3;

// Tester la chaîne
console.log(node1.value); // 100
console.log(node1.next.value); // 200
console.log(node1.next.next.value); // 300
console.log(node3.next); // null

// Visualisation complète
console.log(node1);
// Node {
//   value: 100,
//   next: Node {
//     value: 200,
//     next: Node { value: 300, next: null }
//   }
// }
```

**Explication :**

- Chaque nœud est créé indépendamment avec `new Node(value)`
- Les liens sont établis en assignant la référence d'un nœud à la propriété `next` d'un autre
- La chaîne se forme : 100 → 200 → 300 → null
</details>

---

## 2. 📋 Implémenter la Classe SinglyLinkedList

### 2.1 Structure de Base

Pour gérer une collection de nœuds efficacement, nous créons une classe `SinglyLinkedList` qui encapsule la logique de gestion de la liste.

```javascript
class SinglyLinkedList {
  constructor() {
    this.head = null; // Le premier nœud de la liste
    this.tail = null; // Le dernier nœud de la liste
    this.length = 0; // Le nombre de nœuds dans la liste
  }
}
```

**Propriétés :**

- **`head`** : Référence au premier nœud (point d'entrée de la liste)
- **`tail`** : Référence au dernier nœud (pour ajouts efficaces à la fin)
- **`length`** : Compteur du nombre de nœuds (pour connaître la taille en O(1))

**État initial :**

```javascript
const myList = new SinglyLinkedList();
console.log(myList);
// SinglyLinkedList { head: null, tail: null, length: 0 }
```

Une liste nouvellement créée est **vide** :

- `head` et `tail` sont `null` (aucun nœud)
- `length` est `0`

### 2.2 Pourquoi Trois Propriétés ?

| Propriété  | Utilité                                | Complexité |
| ---------- | -------------------------------------- | ---------- |
| **head**   | Point d'entrée pour parcourir la liste | O(1) accès |
| **tail**   | Permet d'ajouter à la fin en O(1)      | O(1) ajout |
| **length** | Connaître la taille sans parcourir     | O(1) accès |

Sans `tail`, ajouter à la fin nécessiterait de parcourir toute la liste (O(n)).
Sans `length`, obtenir la taille nécessiterait de compter tous les nœuds (O(n)).

---

## 3. ➕ Ajouter des Éléments : La Méthode `push()`

### 3.1 Concept

La méthode `push()` ajoute un nouveau nœud **à la fin** de la liste. C'est l'opération d'ajout la plus courante.

**Deux scénarios à gérer :**

1. **Liste vide** : Le nouveau nœud devient à la fois `head` et `tail`
2. **Liste non vide** : Le nouveau nœud devient le nouveau `tail`

### 3.2 Implémentation Complète

```javascript
class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(value) {
    // 1. Créer un nouveau nœud
    const newNode = new Node(value);

    // 2. Vérifier si la liste est vide
    if (!this.head) {
      // Cas 1 : Liste vide
      this.head = newNode; // Le nouveau nœud devient le head
      this.tail = newNode; // ET le tail
    } else {
      // Cas 2 : Liste non vide
      this.tail.next = newNode; // Lier l'ancien tail au nouveau nœud
      this.tail = newNode; // Le nouveau nœud devient le nouveau tail
    }

    // 3. Incrémenter la longueur
    this.length++;

    // 4. Retourner la liste (utile pour le chaînage)
    return this;
  }
}
```

### 3.3 Analyse Pas à Pas

**Scénario 1 : Ajout à une liste vide**

```javascript
const myList = new SinglyLinkedList();
console.log("Liste initiale:", myList);
// SinglyLinkedList { head: null, tail: null, length: 0 }

myList.push("Premier");
console.log("Après push('Premier'):", myList);
// head: Node { value: 'Premier', next: null }
// tail: Node { value: 'Premier', next: null }
// length: 1
```

**Visualisation :**

```
Avant push:
head: null
tail: null

Après push("Premier"):
head → [Premier | null] ← tail
```

Les deux `head` et `tail` pointent vers le même nœud.

---

**Scénario 2 : Ajout à une liste non vide**

```javascript
myList.push("Deuxième");
console.log("Après push('Deuxième'):", myList);
// head: Node { value: 'Premier', next: Node { value: 'Deuxième', next: null } }
// tail: Node { value: 'Deuxième', next: null }
// length: 2

console.log("head.value:", myList.head.value); // "Premier"
console.log("tail.value:", myList.tail.value); // "Deuxième"
console.log("head.next.value:", myList.head.next.value); // "Deuxième"
```

**Visualisation :**

```
Avant push("Deuxième"):
head → [Premier | null] ← tail

Étape 1: newNode.next = null
         [Deuxième | null]

Étape 2: tail.next = newNode
head → [Premier | •]--→[Deuxième | null] ← tail

Étape 3: tail = newNode
head → [Premier | •]--→[Deuxième | null] ← tail
```

---

**Scénario 3 : Ajouts multiples**

```javascript
myList.push("Troisième");
console.log("head.value:", myList.head.value); // "Premier"
console.log("tail.value:", myList.tail.value); // "Troisième"
console.log("length:", myList.length); // 3
```

**Visualisation finale :**

```
head → [Premier | •]--→[Deuxième | •]--→[Troisième | null] ← tail
```

### 3.4 Complexité Temporelle

**Analyse :**

- Créer un nouveau nœud : **O(1)**
- Vérifier si la liste est vide : **O(1)**
- Mettre à jour les liens : **O(1)**
- Incrémenter la longueur : **O(1)**

**Complexité totale : O(1)** - Temps constant !

C'est l'un des **avantages majeurs** des listes chaînées par rapport aux tableaux pour l'ajout au début.

---

## 📝 Micro-Exercice #2 : Tester la Méthode push()

**Objectif** : Comprendre le comportement de `push()`.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }
}

// À FAIRE : Prédisez les résultats avant d'exécuter
const playlist = new SinglyLinkedList();

console.log("1. Longueur initiale:", playlist.length);

playlist.push("Chanson A");
console.log("2. Après push('Chanson A'):");
console.log("   head.value:", playlist.head.value);
console.log("   tail.value:", playlist.tail.value);
console.log("   length:", playlist.length);

playlist.push("Chanson B");
console.log("3. Après push('Chanson B'):");
console.log("   head.value:", playlist.head.value);
console.log("   tail.value:", playlist.tail.value);
console.log("   head.next.value:", playlist.head.next.value);
console.log("   length:", playlist.length);

playlist.push("Chanson C");
console.log("4. Après push('Chanson C'):");
console.log("   head.value:", playlist.head.value);
console.log("   tail.value:", playlist.tail.value);
console.log("   length:", playlist.length);

// Question : Que vaut playlist.head.next.next.value ?
console.log("5. playlist.head.next.next.value:", playlist.head.next.next.value);
```

<details>
<summary>💡 Voir la solution</summary>

**Résultats attendus :**

```
1. Longueur initiale: 0

2. Après push('Chanson A'):
   head.value: Chanson A
   tail.value: Chanson A
   length: 1

3. Après push('Chanson B'):
   head.value: Chanson A
   tail.value: Chanson B
   head.next.value: Chanson B
   length: 2

4. Après push('Chanson C'):
   head.value: Chanson A
   tail.value: Chanson C
   length: 3

5. playlist.head.next.next.value: Chanson C
```

**Explication :**

1. La liste commence vide (length = 0)
2. Premier push : "Chanson A" devient à la fois head et tail
3. Deuxième push : head reste "Chanson A", tail devient "Chanson B"
4. Troisième push : head reste "Chanson A", tail devient "Chanson C"
5. Pour accéder à "Chanson C" depuis head : `head.next.next`

**Structure finale :**

```
head → [Chanson A | •]--→[Chanson B | •]--→[Chanson C | null] ← tail
```

</details>

---

## 4. ➖ Retirer des Éléments : La Méthode `pop()`

### 4.1 Concept

La méthode `pop()` retire et retourne le **dernier nœud** de la liste. C'est plus complexe que `push()` car nous devons :

1. Trouver le **second-to-last** nœud (avant-dernier)
2. Faire pointer `tail` vers ce nœud
3. Définir son `next` à `null`

**Trois scénarios à gérer :**

1. **Liste vide** : Retourner `undefined`
2. **Un seul nœud** : Réinitialiser `head` et `tail` à `null`
3. **Plusieurs nœuds** : Trouver l'avant-dernier et mettre à jour `tail`

### 4.2 Implémentation Complète

```javascript
class SinglyLinkedList {
  // ... (constructor et push comme avant) ...

  pop() {
    // Cas 1 : Liste vide
    if (!this.head) {
      return undefined;
    }

    // Variables pour parcourir la liste
    let current = this.head;
    let newTail = current;

    // Cas 2 : Un seul nœud (head === tail)
    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      // Cas 3 : Plusieurs nœuds - Trouver l'avant-dernier
      while (current.next) {
        newTail = current; // newTail suit current
        current = current.next; // Avancer current
      }
      // À la sortie de la boucle :
      // - current est le dernier nœud (à retirer)
      // - newTail est l'avant-dernier nœud

      this.tail = newTail; // Mettre à jour tail
      this.tail.next = null; // Couper le lien vers l'ancien tail
    }

    // Décrémenter la longueur
    this.length--;

    // Retourner le nœud retiré
    return current;
  }
}
```

### 4.3 Analyse Pas à Pas

**Scénario 1 : Pop sur liste vide**

```javascript
const emptyList = new SinglyLinkedList();
const result = emptyList.pop();
console.log(result); // undefined
console.log(emptyList.length); // 0
```

Simple : retourne `undefined` sans modifier la liste.

---

**Scénario 2 : Pop sur liste avec un seul élément**

```javascript
const singleList = new SinglyLinkedList();
singleList.push("Unique");

console.log("Avant pop:");
console.log("head.value:", singleList.head.value); // "Unique"
console.log("tail.value:", singleList.tail.value); // "Unique"
console.log("length:", singleList.length); // 1

const popped = singleList.pop();

console.log("Après pop:");
console.log("Valeur retirée:", popped.value); // "Unique"
console.log("head:", singleList.head); // null
console.log("tail:", singleList.tail); // null
console.log("length:", singleList.length); // 0
```

**Visualisation :**

```
Avant pop:
head → [Unique | null] ← tail

Après pop:
head: null
tail: null
```

---

**Scénario 3 : Pop sur liste avec plusieurs éléments**

```javascript
const shoppingList = new SinglyLinkedList();
shoppingList.push("Lait");
shoppingList.push("Pain");
shoppingList.push("Œufs");

// État initial : Lait → Pain → Œufs
console.log("Longueur initiale:", shoppingList.length); // 3
console.log("tail.value:", shoppingList.tail.value); // "Œufs"

// Premier pop
const popped1 = shoppingList.pop();
console.log("\n1er pop:");
console.log("Retiré:", popped1.value); // "Œufs"
console.log("Nouvelle longueur:", shoppingList.length); // 2
console.log("Nouveau tail.value:", shoppingList.tail.value); // "Pain"
console.log("head.value:", shoppingList.head.value); // "Lait"

// Deuxième pop
const popped2 = shoppingList.pop();
console.log("\n2ème pop:");
console.log("Retiré:", popped2.value); // "Pain"
console.log("Nouvelle longueur:", shoppingList.length); // 1
console.log("Nouveau tail.value:", shoppingList.tail.value); // "Lait"
console.log("head.value:", shoppingList.head.value); // "Lait"
console.log("head === tail:", shoppingList.head === shoppingList.tail); // true

// Troisième pop
const popped3 = shoppingList.pop();
console.log("\n3ème pop:");
console.log("Retiré:", popped3.value); // "Lait"
console.log("Nouvelle longueur:", shoppingList.length); // 0
console.log("head:", shoppingList.head); // null
console.log("tail:", shoppingList.tail); // null
```

**Visualisation du parcours pour le 1er pop :**

```
État initial:
head → [Lait | •]--→[Pain | •]--→[Œufs | null] ← tail

Étape 1 - Initialisation:
current = head  (Lait)
newTail = head  (Lait)

Étape 2 - Première itération (current.next existe):
newTail = current   (Lait)
current = current.next   (Pain)

Étape 3 - Deuxième itération (current.next existe):
newTail = current   (Pain)
current = current.next   (Œufs)

Étape 4 - Condition de sortie (current.next === null):
- current pointe vers Œufs (le nœud à retirer)
- newTail pointe vers Pain (l'avant-dernier)

Étape 5 - Mise à jour:
this.tail = newTail   (Pain)
this.tail.next = null (couper le lien vers Œufs)

Résultat final:
head → [Lait | •]--→[Pain | null] ← tail
```

### 4.4 Complexité Temporelle

**Analyse :**

- Parcourir jusqu'à l'avant-dernier nœud : **O(n)**
- Mettre à jour les références : **O(1)**
- Décrémenter la longueur : **O(1)**

**Complexité totale : O(n)** - Linéaire !

**Pourquoi O(n) ?**

Contrairement à `push()`, `pop()` nécessite de **parcourir toute la liste** pour trouver l'avant-dernier nœud. Dans une liste de n éléments, nous devons faire n-1 étapes.

**Comparaison avec les tableaux :**

| Opération         | Tableau | Liste Chaînée |
| ----------------- | ------- | ------------- |
| Ajouter à la fin  | O(1)    | O(1)          |
| Retirer de la fin | O(1)    | O(n)          |

Pour les listes chaînées, `pop()` est plus lent. C'est un **compromis** : les listes chaînées excellent dans d'autres opérations.

---

## 5. 🔄 Méthodes Supplémentaires

Maintenant que vous maîtrisez `push()` et `pop()`, implémentons deux autres méthodes importantes :

### 5.1 La Méthode `shift()` - Retirer du Début

La méthode `shift()` retire et retourne le **premier nœud** de la liste.

**Avantage** : Plus simple et rapide que `pop()` !

```javascript
class SinglyLinkedList {
  // ... (méthodes précédentes) ...

  shift() {
    // Cas 1 : Liste vide
    if (!this.head) {
      return undefined;
    }

    // Sauvegarder le head actuel
    const removedNode = this.head;

    // Cas 2 : Un seul nœud
    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      // Cas 3 : Plusieurs nœuds
      this.head = this.head.next; // Avancer head au nœud suivant
    }

    // Décrémenter la longueur
    this.length--;

    // Retourner le nœud retiré
    return removedNode;
  }
}
```

**Exemple d'utilisation :**

```javascript
const queue = new SinglyLinkedList();
queue.push("Premier");
queue.push("Deuxième");
queue.push("Troisième");

// État : Premier → Deuxième → Troisième

const removed1 = queue.shift();
console.log("Retiré:", removed1.value); // "Premier"
console.log("Nouveau head:", queue.head.value); // "Deuxième"
console.log("Longueur:", queue.length); // 2

const removed2 = queue.shift();
console.log("Retiré:", removed2.value); // "Deuxième"
console.log("Nouveau head:", queue.head.value); // "Troisième"
console.log("Longueur:", queue.length); // 1
```

**Visualisation :**

```
Avant shift():
head → [Premier | •]--→[Deuxième | •]--→[Troisième | null] ← tail

Après shift():
removedNode → [Premier | •] (détaché)
head → [Deuxième | •]--→[Troisième | null] ← tail
```

**Complexité : O(1)** - Temps constant ! Beaucoup plus rapide que `pop()`.

---

### 5.2 La Méthode `unshift()` - Ajouter au Début

La méthode `unshift()` ajoute un nouveau nœud **au début** de la liste.

```javascript
class SinglyLinkedList {
  // ... (méthodes précédentes) ...

  unshift(value) {
    // 1. Créer un nouveau nœud
    const newNode = new Node(value);

    // 2. Vérifier si la liste est vide
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      // 3. Lier le nouveau nœud au head actuel
      newNode.next = this.head;

      // 4. Mettre à jour head
      this.head = newNode;
    }

    // 5. Incrémenter la longueur
    this.length++;

    // 6. Retourner la liste
    return this;
  }
}
```

**Exemple d'utilisation :**

```javascript
const letters = new SinglyLinkedList();
letters.unshift("C");
console.log("Après unshift('C'):");
console.log("head.value:", letters.head.value); // "C"
console.log("tail.value:", letters.tail.value); // "C"
console.log("length:", letters.length); // 1

letters.unshift("B");
console.log("\nAprès unshift('B'):");
console.log("head.value:", letters.head.value); // "B"
console.log("tail.value:", letters.tail.value); // "C"
console.log("length:", letters.length); // 2

letters.unshift("A");
console.log("\nAprès unshift('A'):");
console.log("head.value:", letters.head.value); // "A"
console.log("tail.value:", letters.tail.value); // "C"
console.log("length:", letters.length); // 3

// Parcours de la liste
console.log("\nParcours:");
console.log(letters.head.value); // "A"
console.log(letters.head.next.value); // "B"
console.log(letters.head.next.next.value); // "C"
```

**Visualisation :**

```
Avant unshift("A"):
head → [B | •]--→[C | null] ← tail

Étape 1: Créer newNode
[A | null]

Étape 2: newNode.next = this.head
[A | •]--→[B | •]--→[C | null]

Étape 3: this.head = newNode
head → [A | •]--→[B | •]--→[C | null] ← tail
```

**Complexité : O(1)** - Temps constant !

---

### 5.3 Comparaison des Quatre Méthodes

| Méthode     | Position | Opération | Complexité | Performance |
| ----------- | -------- | --------- | ---------- | ----------- |
| `push()`    | Fin      | Ajouter   | O(1)       | Rapide      |
| `pop()`     | Fin      | Retirer   | O(n)       | Lent        |
| `unshift()` | Début    | Ajouter   | O(1)       | Rapide      |
| `shift()`   | Début    | Retirer   | O(1)       | Rapide      |

**Observations importantes :**

1. **Opérations au début** (shift/unshift) sont **très efficaces** - O(1)
2. **`pop()` est l'exception** - nécessite un parcours complet - O(n)
3. Les listes chaînées **excellent** pour les ajouts/retraits au début

**Comparaison avec les tableaux :**

| Opération         | Tableau | Liste Chaînée |
| ----------------- | ------- | ------------- |
| Ajouter au début  | O(n)    | O(1)          |
| Retirer du début  | O(n)    | O(1)          |
| Ajouter à la fin  | O(1)    | O(1)          |
| Retirer de la fin | O(1)    | O(n)          |

---

## 💪 Exercices Pratiques

### Exercice 1 : Implémenter une File (Queue)

**Objectif :** Utiliser une liste chaînée pour implémenter une file FIFO (First In, First Out).

Une file respecte le principe **"premier arrivé, premier servi"**. Les éléments sont ajoutés à la fin et retirés du début.

**Code de départ :**

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null; // Premier élément (équivalent à head)
    this.last = null; // Dernier élément (équivalent à tail)
    this.size = 0;
  }

  // À FAIRE : Implémenter enqueue() - Ajouter à la fin
  enqueue(value) {
    // Votre code ici
  }

  // À FAIRE : Implémenter dequeue() - Retirer du début
  dequeue() {
    // Votre code ici
  }
}

// Tests
const fileAttente = new Queue();
fileAttente.enqueue("Chermann");
fileAttente.enqueue("Ingrid");
fileAttente.enqueue("Prudence");

console.log("Taille:", fileAttente.size); // 3
console.log("Premier:", fileAttente.first.value); // "Chermann"
console.log("Dernier:", fileAttente.last.value); // "Prudence"

const servi1 = fileAttente.dequeue();
console.log("Servi:", servi1.value); // "Chermann"
console.log("Nouveau premier:", fileAttente.first.value); // "Ingrid"
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  // Ajouter à la fin - O(1)
  enqueue(value) {
    const newNode = new Node(value);

    if (!this.first) {
      // File vide
      this.first = newNode;
      this.last = newNode;
    } else {
      // File non vide
      this.last.next = newNode;
      this.last = newNode;
    }

    this.size++;
    return this.size;
  }

  // Retirer du début - O(1)
  dequeue() {
    if (!this.first) {
      // File vide
      return null;
    }

    const removedNode = this.first;

    if (this.first === this.last) {
      // Un seul élément
      this.last = null;
    }

    this.first = this.first.next;
    this.size--;

    return removedNode;
  }
}

// Tests complets
const fileAttente = new Queue();
console.log("File initiale vide:", fileAttente.size); // 0

fileAttente.enqueue("Chermann");
fileAttente.enqueue("Ingrid");
fileAttente.enqueue("Prudence");
fileAttente.enqueue("Marshall");

console.log("\nAprès enqueue de 4 personnes:");
console.log("Taille:", fileAttente.size); // 4
console.log("Premier:", fileAttente.first.value); // "Chermann"
console.log("Dernier:", fileAttente.last.value); // "Marshall"

const servi1 = fileAttente.dequeue();
console.log("\n1er dequeue:");
console.log("Servi:", servi1.value); // "Chermann"
console.log("Nouveau premier:", fileAttente.first.value); // "Ingrid"
console.log("Taille:", fileAttente.size); // 3

const servi2 = fileAttente.dequeue();
console.log("\n2ème dequeue:");
console.log("Servi:", servi2.value); // "Ingrid"
console.log("Nouveau premier:", fileAttente.first.value); // "Prudence"
console.log("Taille:", fileAttente.size); // 2

const servi3 = fileAttente.dequeue();
console.log("\n3ème dequeue:");
console.log("Servi:", servi3.value); // "Prudence"
console.log("Nouveau premier:", fileAttente.first.value); // "Marshall"
console.log("Taille:", fileAttente.size); // 1

const servi4 = fileAttente.dequeue();
console.log("\n4ème dequeue:");
console.log("Servi:", servi4.value); // "Marshall"
console.log("Premier:", fileAttente.first); // null
console.log("Dernier:", fileAttente.last); // null
console.log("Taille:", fileAttente.size); // 0
```

**Explication :**

- **`enqueue()`** utilise la même logique que `push()` - ajoute à la fin en O(1)
- **`dequeue()`** utilise la même logique que `shift()` - retire du début en O(1)
- Une file est **parfaitement adaptée** à une liste chaînée : toutes les opérations sont O(1) !

**Applications réelles :**

- Files d'attente de serveurs (traitement de requêtes)
- Systèmes d'impression (ordre des documents)
- Gestion de processus dans les OS
</details>

---

### Exercice 2 : Implémenter une Pile (Stack)

**Objectif :** Utiliser une liste chaînée pour implémenter une pile LIFO (Last In, First Out).

Une pile respecte le principe **"dernier arrivé, premier servi"**. Les éléments sont ajoutés et retirés du même côté (le sommet).

**Code de départ :**

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.top = null; // Sommet de la pile
    this.size = 0;
  }

  // À FAIRE : Implémenter push() - Ajouter au sommet
  push(value) {
    // Votre code ici
  }

  // À FAIRE : Implémenter pop() - Retirer du sommet
  pop() {
    // Votre code ici
  }
}

// Tests
const pile = new Stack();
pile.push("Assiette 1");
pile.push("Assiette 2");
pile.push("Assiette 3");

console.log("Taille:", pile.size); // 3
console.log("Sommet:", pile.top.value); // "Assiette 3"

const retiree = pile.pop();
console.log("Retirée:", retiree.value); // "Assiette 3"
console.log("Nouveau sommet:", pile.top.value); // "Assiette 2"
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.top = null;
    this.size = 0;
  }

  // Ajouter au sommet - O(1)
  push(value) {
    const newNode = new Node(value);

    if (!this.top) {
      // Pile vide
      this.top = newNode;
    } else {
      // Pile non vide
      newNode.next = this.top; // Le nouveau nœud pointe vers l'ancien sommet
      this.top = newNode; // Le nouveau nœud devient le sommet
    }

    this.size++;
    return this.size;
  }

  // Retirer du sommet - O(1)
  pop() {
    if (!this.top) {
      // Pile vide
      return null;
    }

    const removedNode = this.top;
    this.top = this.top.next; // Descendre au nœud suivant
    this.size--;

    return removedNode;
  }

  // Optionnel : Voir le sommet sans retirer
  peek() {
    return this.top ? this.top.value : null;
  }
}

// Tests complets
const pile = new Stack();
console.log("Pile initiale vide:", pile.size); // 0

pile.push("Assiette 1");
pile.push("Assiette 2");
pile.push("Assiette 3");
pile.push("Assiette 4");

console.log("\nAprès push de 4 assiettes:");
console.log("Taille:", pile.size); // 4
console.log("Sommet:", pile.top.value); // "Assiette 4"
console.log("peek():", pile.peek()); // "Assiette 4"

const retiree1 = pile.pop();
console.log("\n1er pop:");
console.log("Retirée:", retiree1.value); // "Assiette 4"
console.log("Nouveau sommet:", pile.top.value); // "Assiette 3"
console.log("Taille:", pile.size); // 3

const retiree2 = pile.pop();
console.log("\n2ème pop:");
console.log("Retirée:", retiree2.value); // "Assiette 3"
console.log("Nouveau sommet:", pile.top.value); // "Assiette 2"
console.log("Taille:", pile.size); // 2

// Vider la pile
pile.pop(); // Assiette 2
pile.pop(); // Assiette 1
console.log("\nPile vidée:");
console.log("Sommet:", pile.top); // null
console.log("Taille:", pile.size); // 0
console.log("peek():", pile.peek()); // null
```

**Explication :**

- **`push()`** utilise la logique de `unshift()` - ajoute au début (sommet) en O(1)
- **`pop()`** utilise la logique de `shift()` - retire du début (sommet) en O(1)
- Une pile est également **parfaitement adaptée** à une liste chaînée !

**Visualisation d'une pile :**

```
Après push("A"), push("B"), push("C"):

top → [C | •]
       ↓
      [B | •]
       ↓
      [A | null]

Après pop():

top → [B | •]
       ↓
      [A | null]
```

**Applications réelles :**

- Fonction "Annuler" (Undo) dans les éditeurs
- Historique de navigation (bouton retour)
- Évaluation d'expressions mathématiques
- Gestion de la pile d'appels dans les programmes
</details>

---

### Exercice 3 : Méthode `get()` - Accéder par Index

**Objectif :** Implémenter une méthode `get(index)` qui retourne le nœud à une position donnée.

```javascript
class SinglyLinkedList {
  // ... (méthodes précédentes) ...

  // À FAIRE : Implémenter get(index)
  get(index) {
    // Vérifier si l'index est valide
    // Parcourir la liste jusqu'à l'index
    // Retourner le nœud trouvé
  }
}

// Tests
const list = new SinglyLinkedList();
list.push(10);
list.push(20);
list.push(30);
list.push(40);

console.log(list.get(0).value); // 10
console.log(list.get(2).value); // 30
console.log(list.get(5)); // null (index hors limites)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  // Accéder à un nœud par index - O(n)
  get(index) {
    // Vérifier si l'index est valide
    if (index < 0 || index >= this.length) {
      return null;
    }

    // Parcourir jusqu'à l'index
    let current = this.head;
    let counter = 0;

    while (counter < index) {
      current = current.next;
      counter++;
    }

    return current;
  }
}

// Tests complets
const list = new SinglyLinkedList();
list.push(10);
list.push(20);
list.push(30);
list.push(40);
list.push(50);

console.log("Liste complète:");
console.log("Index 0:", list.get(0).value); // 10
console.log("Index 1:", list.get(1).value); // 20
console.log("Index 2:", list.get(2).value); // 30
console.log("Index 3:", list.get(3).value); // 40
console.log("Index 4:", list.get(4).value); // 50

console.log("\nIndex invalides:");
console.log("Index -1:", list.get(-1)); // null
console.log("Index 5:", list.get(5)); // null
console.log("Index 10:", list.get(10)); // null

// Utiliser get() avec d'autres méthodes
console.log("\nUtilisation combinée:");
const middleNode = list.get(2);
console.log("Nœud du milieu:", middleNode.value); // 30
console.log("Nœud suivant:", middleNode.next.value); // 40
```

**Explication :**

- **Validation** : Vérifie que `index` est dans [0, length-1]
- **Parcours** : Avance de `head` jusqu'à l'index voulu
- **Complexité** : O(n) car nécessite un parcours
- **Comparaison** : Les tableaux font ceci en O(1) avec `array[index]`

**Utilité :**
Cette méthode servira de base pour d'autres opérations comme :

- `set(index, value)` : Modifier la valeur à un index
- `insert(index, value)` : Insérer à un index spécifique
- `remove(index)` : Supprimer à un index spécifique
</details>

---

## 🌍 Application Réelle : Gestionnaire de Playlist

Créons une application complète de gestion de playlist musicale utilisant une liste chaînée.

```javascript
class Song {
  constructor(title, artist) {
    this.title = title;
    this.artist = artist;
    this.next = null;
  }
}

class MusicPlaylist {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  // Ajouter une chanson à la fin
  addSong(title, artist) {
    const newSong = new Song(title, artist);

    if (!this.head) {
      this.head = newSong;
      this.tail = newSong;
    } else {
      this.tail.next = newSong;
      this.tail = newSong;
    }

    this.length++;
    console.log(`🎵 Ajouté: "${title}" - ${artist}`);
    return this;
  }

  // Retirer la dernière chanson
  removeLast() {
    if (!this.head) {
      console.log("La playlist est vide");
      return null;
    }

    let current = this.head;
    let newTail = current;

    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      while (current.next) {
        newTail = current;
        current = current.next;
      }
      this.tail = newTail;
      this.tail.next = null;
    }

    this.length--;
    console.log(`Retiré: "${current.title}" - ${current.artist}`);
    return current;
  }

  // Jouer la première chanson et la retirer
  playNext() {
    if (!this.head) {
      console.log("Aucune chanson à jouer");
      return null;
    }

    const song = this.head;
    console.log(`▶ Lecture en cours: "${song.title}" - ${song.artist}`);

    this.head = this.head.next;
    this.length--;

    if (this.length === 0) {
      this.tail = null;
    }

    return song;
  }

  // Afficher toute la playlist
  displayPlaylist() {
    if (!this.head) {
      console.log("Playlist vide");
      return;
    }

    console.log(
      `Playlist (${this.length} chanson${this.length > 1 ? "s" : ""}):`,
    );
    let current = this.head;
    let index = 1;

    while (current) {
      console.log(`  ${index}. "${current.title}" - ${current.artist}`);
      current = current.next;
      index++;
    }
  }

  // Obtenir le nombre de chansons
  getLength() {
    return this.length;
  }
}

// Utilisation de la playlist
console.log("=== GESTIONNAIRE DE PLAYLIST MUSICALE ===\n");

const maPlaylist = new MusicPlaylist();

// Ajouter des chansons
console.log("--- Ajout de chansons ---");
maPlaylist.addSong("Bohemian Rhapsody", "Queen");
maPlaylist.addSong("Imagine", "John Lennon");
maPlaylist.addSong("Hotel California", "Eagles");
maPlaylist.addSong("Billie Jean", "Michael Jackson");

console.log("\n--- État de la playlist ---");
maPlaylist.displayPlaylist();

console.log("\n--- Lecture des chansons ---");
maPlaylist.playNext(); // Bohemian Rhapsody
maPlaylist.playNext(); // Imagine

console.log("\n--- Playlist après lecture ---");
maPlaylist.displayPlaylist();

console.log("\n--- Retirer la dernière chanson ---");
maPlaylist.removeLast(); // Billie Jean

console.log("\n--- Playlist finale ---");
maPlaylist.displayPlaylist();
console.log(`\nTotal: ${maPlaylist.getLength()} chanson(s) restante(s)`);
```

**Sortie attendue :**

```
=== GESTIONNAIRE DE PLAYLIST MUSICALE ===

--- Ajout de chansons ---
  Ajouté: "Bohemian Rhapsody" - Queen
  Ajouté: "Imagine" - John Lennon
  Ajouté: "Hotel California" - Eagles
  Ajouté: "Billie Jean" - Michael Jackson

--- État de la playlist ---
  Playlist (4 chansons):
  1. "Bohemian Rhapsody" - Queen
  2. "Imagine" - John Lennon
  3. "Hotel California" - Eagles
  4. "Billie Jean" - Michael Jackson

--- Lecture des chansons ---
  Lecture en cours: "Bohemian Rhapsody" - Queen
  Lecture en cours: "Imagine" - John Lennon

--- Playlist après lecture ---
  Playlist (2 chansons):
  1. "Hotel California" - Eagles
  2. "Billie Jean" - Michael Jackson

--- Retirer la dernière chanson ---
  Retiré: "Billie Jean" - Michael Jackson

--- Playlist finale ---
  Playlist (1 chanson):
  1. "Hotel California" - Eagles

Total: 1 chanson(s) restante(s)
```

**Analyse de l'implémentation :**

| Opération        | Méthode             | Complexité | Utilité                |
| ---------------- | ------------------- | ---------- | ---------------------- |
| Ajouter chanson  | `addSong()`         | O(1)       | Construire la playlist |
| Jouer suivante   | `playNext()`        | O(1)       | Lecture séquentielle   |
| Retirer dernière | `removeLast()`      | O(n)       | Gérer la fin           |
| Afficher         | `displayPlaylist()` | O(n)       | Visualiser             |

> **Points clés :**
>
> - Utilise les concepts de file (FIFO) pour `playNext()`
> - Efficient pour l'ajout et la lecture séquentielle
> - Illustre une application pratique et concrète

---

## ❓ Quiz de Validation des Connaissances

### Question 1

Quelle est la complexité temporelle de la méthode `push()` dans une liste chaînée simple ?

- [ ] A) O(1)
- [ ] B) O(log n)
- [ ] C) O(n)
- [ ] D) O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : A) O(1)**

**Explication :**

La méthode `push()` ajoute un élément à la fin de la liste en temps constant car :

1. Nous maintenons une référence `tail` pointant vers le dernier nœud
2. Les opérations effectuées sont :
   - Créer un nouveau nœud : O(1)
   - Mettre à jour `tail.next` : O(1)
   - Mettre à jour `tail` : O(1)
   - Incrémenter `length` : O(1)

```javascript
push(value) {
  const newNode = new Node(value);  // O(1)
  if (!this.head) {
    this.head = newNode;            // O(1)
    this.tail = newNode;            // O(1)
  } else {
    this.tail.next = newNode;       // O(1)
    this.tail = newNode;            // O(1)
  }
  this.length++;                    // O(1)
  return this;
}
```

**Aucun parcours** de la liste n'est nécessaire, d'où la complexité O(1).

**Pourquoi pas les autres ?**

- **O(log n)** : C'est la complexité de recherche binaire, pas applicable ici
- **O(n)** : Ce serait le cas si nous devions parcourir toute la liste
- **O(n²)** : Ce serait avec des boucles imbriquées
</details>

---

### Question 2

Pourquoi la méthode `pop()` a-t-elle une complexité O(n) dans une liste chaînée simple ?

- [ ] A) Parce qu'elle doit créer un nouveau nœud
- [ ] B) Parce qu'elle doit parcourir la liste pour trouver l'avant-dernier nœud
- [ ] C) Parce qu'elle doit décaler tous les éléments
- [ ] D) Parce qu'elle doit trier la liste

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Parce qu'elle doit parcourir la liste pour trouver l'avant-dernier nœud**

**Explication :**

Dans une liste chaînée **simple**, chaque nœud ne connaît que le nœud **suivant** (pas le précédent). Pour retirer le dernier nœud, nous devons :

1. Trouver l'**avant-dernier nœud** pour le faire devenir le nouveau `tail`
2. Définir son `next` à `null` pour couper le lien avec l'ancien dernier nœud

**Le problème :** Il n'y a pas d'accès direct à l'avant-dernier nœud, donc nous devons **parcourir toute la liste** :

```javascript
pop() {
  // ...
  let current = this.head;
  let newTail = current;

  while (current.next) {  // ← Parcours O(n)
    newTail = current;
    current = current.next;
  }

  this.tail = newTail;
  this.tail.next = null;
  // ...
}
```

Dans le pire cas (liste de n éléments), nous faisons n-1 itérations.

**Visualisation :**

```
Pour pop() sur: [A]→[B]→[C]→[D]→null

Parcours nécessaire:
current = A, newTail = A
current = B, newTail = A
current = C, newTail = B
current = D, newTail = C  ← Trouvé l'avant-dernier !

Total : 3 étapes pour une liste de 4 éléments (n-1)
```

**Solution pour O(1) :** Une **liste doublement chaînée** avec des références `prev` permettrait un `pop()` en O(1).

**Pourquoi pas les autres ?**

- **Créer un nœud** : Non, `pop()` retire un nœud, ne crée pas
- **Décaler les éléments** : Non, c'est un problème des tableaux, pas des listes chaînées
- **Trier** : Non, `pop()` ne trie pas
</details>

---

### Question 3

Quelle combinaison de méthodes permet d'implémenter efficacement une **file (Queue)** ?

- [ ] A) `push()` pour enqueue, `pop()` pour dequeue
- [ ] B) `push()` pour enqueue, `shift()` pour dequeue
- [ ] C) `unshift()` pour enqueue, `pop()` pour dequeue
- [ ] D) `unshift()` pour enqueue, `shift()` pour dequeue

<details>
<summary>Voir la réponse</summary>

**Réponse : B) `push()` pour enqueue, `shift()` pour dequeue**

**Explication :**

Une **file (Queue)** respecte le principe **FIFO** (First In, First Out) : le premier élément ajouté est le premier retiré.

Pour implémenter cela efficacement :

1. **Enqueue (ajouter)** : Ajouter à la **fin** avec `push()` - O(1)
2. **Dequeue (retirer)** : Retirer du **début** avec `shift()` - O(1)

```javascript
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  enqueue(value) {
    // Utilise la logique de push()
    // Ajoute à la fin - O(1)
  }

  dequeue() {
    // Utilise la logique de shift()
    // Retire du début - O(1)
  }
}

// Utilisation
const queue = new Queue();
queue.enqueue("Premier"); // push à la fin
queue.enqueue("Deuxième");
queue.enqueue("Troisième");

queue.dequeue(); // shift du début → "Premier"
queue.dequeue(); // shift du début → "Deuxième"
```

**Visualisation :**

```
Enqueue:     enqueue()         enqueue()
            ↓                 ↓
[Premier] → [Deuxième] → [Troisième]
↑
Dequeue: dequeue()
```

**Complexité :**

- `push()` (enqueue) : **O(1)**
- `shift()` (dequeue) : **O(1)**

**Pourquoi pas les autres ?**

**A) push() + pop()** :

- `push()` : O(1)
- `pop()` : O(n)
- Ne respecte pas FIFO (dernier ajouté, dernier retiré = LIFO)

**C) unshift() + pop()** :

- Ne respecte pas FIFO (premier ajouté, dernier retiré)

**D) unshift() + shift()** :

- Les deux au début, ne forme pas une file
- Équivalent à une pile au début de la liste
</details>

---

### Question 4

Quel est l'avantage principal d'une liste chaînée par rapport à un tableau pour l'opération `unshift()` ?

- [ ] A) La liste chaînée utilise moins de mémoire
- [ ] B) La liste chaînée ne nécessite pas de décalage d'éléments
- [ ] C) La liste chaînée trie automatiquement les éléments
- [ ] D) La liste chaînée permet un accès plus rapide par index

<details>
<summary>Voir la réponse</summary>

**Réponse : B) La liste chaînée ne nécessite pas de décalage d'éléments**

**Explication :**

**Avec un tableau :**

Quand vous ajoutez un élément au début avec `unshift()`, tous les éléments existants doivent être **décalés** d'une position vers la droite :

```javascript
let arr = [30, 40, 50];
arr.unshift(20);

// Processus interne :
// 1. Créer plus d'espace
// 2. Décaler tous les éléments : 30→, 40→, 50→
// 3. Insérer 20 au début

// Résultat : [20, 30, 40, 50]
// Complexité : O(n) - doit toucher n éléments
```

**Visualisation du décalage :**

```
Avant:   [30][40][50]
Après:   [20][30][40][50]
         ↑  ↑   ↑   ↑
         ↑  └───┴───┘ Tous décalés!
         └─ Nouveau
```

---

**Avec une liste chaînée :**

Avec `unshift()` sur une liste chaînée, il suffit de :

1. Créer le nouveau nœud
2. Faire pointer son `next` vers l'ancien `head`
3. Mettre à jour `head`

```javascript
unshift(value) {
  const newNode = new Node(value);
  newNode.next = this.head;  // ← Juste un changement de pointeur!
  this.head = newNode;
  this.length++;
  return this;
}

// Complexité : O(1) - aucun décalage nécessaire!
```

**Visualisation :**

```
Avant:
head → [30 | •]→[40 | •]→[50 | null]

Étape 1: Créer newNode
[20 | null]

Étape 2: newNode.next = head
[20 | •]→[30 | •]→[40 | •]→[50 | null]

Étape 3: head = newNode
head → [20 | •]→[30 | •]→[40 | •]→[50 | null]

Aucun décalage! Juste 3 opérations O(1)!
```

**Comparaison :**

| Opération   | Tableau         | Liste Chaînée                  |
| ----------- | --------------- | ------------------------------ |
| `unshift()` | O(n) - Décalage | O(1) - Changement de pointeurs |

**Pourquoi pas les autres ?**

- **Moins de mémoire** : Faux, les listes chaînées utilisent plus de mémoire (références `next`)
- **Tri automatique** : Faux, aucune structure ne trie automatiquement
- **Accès par index** : Faux, les tableaux sont plus rapides (O(1) vs O(n))

**Conclusion :** L'avantage clé est l'**absence de décalage** grâce aux références dynamiques.

</details>

---

### Question 5

Considérez ce code. Que se passe-t-il ?

```javascript
const list = new SinglyLinkedList();
list.push(10);
list.push(20);
list.push(30);

const removedNode = list.pop();
console.log(removedNode.value);
console.log(list.length);
```

- [ ] A) `30` et `2`
- [ ] B) `10` et `2`
- [ ] C) `30` et `3`
- [ ] D) Erreur

<details>
<summary>Voir la réponse</summary>

**Réponse : A) `30` et `2`**

**Explication :**

Traçons l'exécution étape par étape :

**Étape 1 : Construire la liste**

```javascript
const list = new SinglyLinkedList();
// État: head: null, tail: null, length: 0

list.push(10);
// État: head → [10 | null] ← tail, length: 1

list.push(20);
// État: head → [10 | •]→[20 | null] ← tail, length: 2

list.push(30);
// État: head → [10 | •]→[20 | •]→[30 | null] ← tail, length: 3
```

**Visualisation après les trois push :**

```
head → [10 | •]→[20 | •]→[30 | null] ← tail
       length: 3
```

---

**Étape 2 : Exécuter pop()**

```javascript
const removedNode = list.pop();
```

La méthode `pop()` :

1. Parcourt la liste pour trouver l'avant-dernier nœud (20)
2. Fait pointer `tail` vers ce nœud
3. Coupe le lien : `tail.next = null`
4. Décrémente `length` : 3 → 2
5. Retourne le nœud retiré (30)

**Visualisation après pop :**

```
head → [10 | •]→[20 | null] ← tail
       length: 2

removedNode → [30 | null] (détaché)
```

---

**Étape 3 : Affichages**

```javascript
console.log(removedNode.value); // 30 (valeur du nœud retiré)
console.log(list.length); // 2 (nouvelle longueur)
```

**Résumé :**

| Avant pop()         | Après pop()      |
| ------------------- | ---------------- |
| head → 10 → 20 → 30 | head → 10 → 20   |
| tail → 30           | tail → 20        |
| length: 3           | length: 2        |
|                     | removedNode → 30 |

**Pourquoi pas les autres ?**

- **B) `10` et `2`** : Faux, `pop()` retire à la **fin**, pas au début
- **C) `30` et `3`** : Faux, `length` est décrémenté
- **D) Erreur** : Faux, le code est valide

**Point clé :** `pop()` retire toujours le **dernier** élément (celui pointé par `tail`).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Structure de Base

Deux classes fondamentales : **`Node`** (contient `value` et `next`) et **`SinglyLinkedList`** (gère `head`, `tail`, et `length`). Les nœuds sont reliés dynamiquement via la propriété `next`.

### 2. Méthodes d'Ajout (push/unshift)

**`push()`** ajoute à la fin en **O(1)** grâce à la référence `tail`. **`unshift()`** ajoute au début en **O(1)** sans décalage d'éléments, contrairement aux tableaux.

### 3. Méthodes de Retrait (pop/shift)

**`shift()`** retire du début en **O(1)** (simple mise à jour de `head`). **`pop()`** retire de la fin en **O(n)** car il faut parcourir la liste pour trouver l'avant-dernier nœud.

### 4. Complexités Temporelles

| Méthode     | Complexité | Performance |
| ----------- | ---------- | ----------- |
| `push()`    | O(1)       | Rapide      |
| `unshift()` | O(1)       | Rapide      |
| `shift()`   | O(1)       | Rapide      |
| `pop()`     | O(n)       | Lent        |

### 5. Comparaison avec les Tableaux

Les listes chaînées excellent pour les **opérations au début** (O(1) vs O(n) pour les tableaux). Les tableaux sont meilleurs pour l'**accès par index** (O(1) vs O(n)) et le **retrait à la fin** (O(1) vs O(n)).

### 6. Applications Pratiques

**Files (Queues)** : `push()` + `shift()` = FIFO en O(1). **Piles (Stacks)** : `unshift()` + `shift()` = LIFO en O(1). Les listes chaînées sont parfaitement adaptées à ces structures.

### 7. Gestion des Cas Limites

Toujours vérifier si la liste est **vide** (`!this.head`). Gérer spécifiquement le cas d'un **seul élément** (`length === 1`). Maintenir la cohérence entre `head`, `tail`, et `length` après chaque opération.

---

## 🎓 Conclusion

Félicitations ! Vous avez maintenant une **implémentation complète** d'une liste chaînée simple en JavaScript.

### Ce que vous avez appris

Dans cette leçon, vous avez :

- Construit une classe `Node` pour représenter les nœuds
- Créé une classe `SinglyLinkedList` avec toutes les propriétés nécessaires
- Implémenté quatre méthodes fondamentales : `push()`, `pop()`, `shift()`, `unshift()`
- Analysé la complexité temporelle de chaque opération
- Compris les avantages et inconvénients par rapport aux tableaux
- Appliqué les concepts à des cas réels (files, piles, playlists)

### De la Théorie à la Maîtrise

Vous êtes passé de la **compréhension conceptuelle** (Leçon 8) à l'**implémentation pratique** (cette leçon). Maintenant, vous savez non seulement **comment** fonctionnent les listes chaînées, mais aussi **comment les construire**.

### Compétences Acquises

- **Manipulation de références** : Comprendre comment les pointeurs créent des structures
- **Gestion de la mémoire dynamique** : Allocation et liaison de nœuds
- **Analyse de complexité** : Évaluer les performances de vos algorithmes
- **Résolution de problèmes** : Gérer les cas limites et les scénarios spéciaux

---

## ➡️ Prochaine Étape : Leçon 10

### Ce qui vous attend

Dans la prochaine leçon, **« Piles : Principe LIFO et Implémentation Basée sur Tableaux »**, vous allez découvrir une structure de données fondamentale utilisée partout en programmation.

**Vous découvrirez :**

- Le principe **LIFO** (Last In, First Out) et ses applications
- Comment implémenter une pile avec un tableau JavaScript
- Les cas d'usage réels : historique de navigation, Undo/Redo, validation de parenthèses
- Les opérations `push()` et `pop()` en O(1)

### Préparez-vous !

Assurez-vous de bien maîtriser les méthodes de tableau `push()` et `pop()`. La pile est une structure simple mais puissante que vous utiliserez constamment en programmation.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Linked List Implementation in JavaScript](https://www.youtube.com/watch?v=ZBdE8DElQQU) - Tutoriel vidéo complet
- [Implementing Linked Lists in JavaScript](https://www.freecodecamp.org/news/implementing-a-linked-list-in-javascript/) - Guide FreeCodeCamp
- [Visualgo - Linked List Visualization](https://visualgo.net/en/list) - Visualisation interactive

### Outils utiles

- **[LeetCode - Linked List Problems](https://leetcode.com/tag/linked-list/)** : Exercices pour pratiquer
- **[HackerRank - Linked Lists](https://www.hackerrank.com/domains/data-structures/linked-lists)** : Défis progressifs

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices
- Tester votre implémentation avec différents cas limites (liste vide, un élément, plusieurs éléments)

> 💡 **Conseil**
>
> Avant de passer à la suite, assurez-vous que votre implémentation gère correctement tous les cas limites. Testez avec une liste vide, un seul élément, et plusieurs éléments. Vérifiez que `head`, `tail` et `length` sont toujours corrects après chaque opération !

---

**Prêt pour la Leçon 10 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir les piles et le principe LIFO !

---

<div align="center">

**Leçon 9 sur 42 - Module 2 : Structures de Données Essentielles en JavaScript**

[⬅️ Leçon 8 : Listes Chaînées - Concepts, Types et Parcours](./lecon-2-listes-chainees-concepts-types-parcours.md) | [Retour au sommaire](./README.md) | [Leçon 10 : Piles - Principe LIFO et Implémentation Basée sur Tableaux ➡️](./lecon-4-piles-principe-lifo-implementation-tableaux.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
