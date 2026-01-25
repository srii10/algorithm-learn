##### Leçon 8 sur 42

# Listes Chaînées : Concepts, Types et Parcours

**Module 2** : Structures de Données Essentielles en JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre la structure fondamentale d'un nœud de liste chaînée
- Distinguer les trois types de listes chaînées (simple, doublement chaînée, circulaire)
- Parcourir une liste chaînée en utilisant des références de nœuds
- Identifier les avantages et inconvénients des listes chaînées par rapport aux tableaux
- Reconnaître les applications pratiques des listes chaînées dans les systèmes réels
- Analyser la complexité temporelle des opérations de parcours de listes chaînées

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

Avant de commencer cette leçon, assurez-vous de maîtriser :

- **Leçon 7** : Tableaux - Listes Dynamiques et Opérations de Base
- Les objets JavaScript et les références en mémoire
- Les concepts de base de la notation Big O
- La manipulation de pointeurs et de références en JavaScript

---

## 🚀 Introduction

### Analogie du Monde Réel

Imaginez une **chasse au trésor** où chaque indice vous mène au suivant. Vous commencez avec le premier indice, qui contient des informations et vous indique où trouver le deuxième indice. Le deuxième indice contient également des informations et pointe vers le troisième, et ainsi de suite jusqu'à ce que vous atteigniez le trésor final.

C'est exactement ainsi qu'une **liste chaînée** fonctionne en programmation ! Contrairement aux tableaux où tous les éléments sont stockés côte à côte en mémoire (comme des livres sur une étagère), une liste chaînée est une collection d'éléments dispersés en mémoire, chacun "pointant" vers l'emplacement du suivant.

### Point Clé à Retenir

> **Une liste chaînée est une structure de données linéaire où chaque élément (appelé "nœud") contient deux parties : les données elles-mêmes et une référence (ou "lien") vers le nœud suivant dans la séquence.**

Cette structure simple mais puissante offre des avantages significatifs pour certaines opérations, notamment l'insertion et la suppression d'éléments, tout en présentant des compromis par rapport aux tableaux.

---

## 1. 📦 Les Concepts Fondamentaux des Listes Chaînées

### 1.1 Qu'est-ce qu'une Liste Chaînée ?

Une **liste chaînée** est une structure de données qui consiste en une séquence de **nœuds**, où chaque nœud contient :

1. **Des données** : La valeur ou l'information que vous souhaitez stocker
2. **Une référence** (ou "pointeur") : Un lien vers le nœud suivant dans la séquence

Contrairement aux tableaux, les listes chaînées ne stockent pas leurs éléments dans des emplacements mémoire contigus. Au lieu de cela, chaque nœud peut être situé n'importe où en mémoire, et les nœuds sont connectés via des références.

### 1.2 Structure d'un Nœud

Voici comment nous représentons un nœud en JavaScript :

```javascript
// Structure de base d'un nœud de liste chaînée
class Node {
  constructor(data) {
    this.data = data; // Les données stockées dans ce nœud
    this.next = null; // Référence au nœud suivant (initialement null)
  }
}
```

**Exemple de création de nœuds :**

```javascript
// Créer trois nœuds indépendants
let node1 = new Node("Chermann");
let node2 = new Node("Ingrid");
let node3 = new Node("Prudence");

// À ce stade, les nœuds existent mais ne sont pas connectés
console.log(node1); // Node { data: "Chermann", next: null }
console.log(node2); // Node { data: "Ingrid", next: null }
console.log(node3); // Node { data: "Prudence", next: null }
```

### 1.3 Relier les Nœuds

Pour créer une liste chaînée, nous devons relier ces nœuds en définissant leurs références `next` :

```javascript
// Relier les nœuds pour former une liste chaînée
node1.next = node2; // node1 pointe vers node2
node2.next = node3; // node2 pointe vers node3
// node3.next reste null (fin de la liste)

// Maintenant nous avons une liste chaînée : Chermann -> Ingrid -> Prudence -> null
```

**Représentation visuelle :**

```
[Chermann | •]--→[Ingrid | •]--→[Prudence | •]--→ null
   node1           node2          node3
```

### 1.4 Le Nœud "Head" (Tête)

Dans une liste chaînée, nous gardons une référence au **premier nœud**, appelé le **head** (tête). C'est notre point d'entrée dans la liste :

```javascript
// Le head est notre point d'accès à toute la liste
let head = node1;

console.log(head.data); // "Chermann"
console.log(head.next.data); // "Ingrid"
console.log(head.next.next.data); // "Prudence"
```

### 1.5 Le Nœud "Tail" (Queue)

Le **tail** (queue) est le dernier nœud de la liste. Il est identifiable car sa propriété `next` est `null` :

```javascript
// node3 est le tail car next est null
console.log(node3.next === null); // true
```

---

### 📝 Micro-Exercice #1 : Créer et Relier des Nœuds

**Objectif** : Créer une petite liste chaînée de villes africaines.

```javascript
// À FAIRE : Créez trois nœuds avec les villes suivantes
// "Addis Abeba", "Libreville", "Dakar"
// Reliez-les pour former une liste chaînée

class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

// Votre code ici
let ville1 = // ...
let ville2 = // ...
let ville3 = // ...

// Reliez les nœuds

// Testez votre liste
console.log(ville1.data);           // Devrait afficher "Addis Abeba"
console.log(ville1.next.data);      // Devrait afficher "Libreville"
console.log(ville1.next.next.data); // Devrait afficher "Dakar"
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

// Créer les trois nœuds
let ville1 = new Node("Addis Abeba");
let ville2 = new Node("Libreville");
let ville3 = new Node("Dakar");

// Relier les nœuds
ville1.next = ville2;
ville2.next = ville3;

// Tester la liste
console.log(ville1.data); // "Addis Abeba"
console.log(ville1.next.data); // "Libreville"
console.log(ville1.next.next.data); // "Dakar"
console.log(ville3.next); // null (fin de la liste)
```

**Explication :**

- Chaque nœud est créé avec une ville
- Les liens `next` connectent les nœuds dans l'ordre
- Le dernier nœud (ville3) a `next = null`, indiquant la fin de la liste
</details>

---

## 2. 🔗 Les Trois Types de Listes Chaînées

Il existe trois types principaux de listes chaînées, chacun avec ses propres caractéristiques et cas d'usage.

### 2.1 Liste Chaînée Simple (Singly Linked List)

C'est le type le plus basique que nous avons déjà vu. Chaque nœud contient des données et une référence vers le **nœud suivant** uniquement.

**Structure d'un nœud :**

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null; // Une seule référence : vers le nœud suivant
  }
}
```

**Caractéristiques :**

- Parcours dans **un seul sens** (de la tête vers la queue)
- Utilisation mémoire minimale (une seule référence par nœud)
- Pas de parcours inverse possible directement
- Pour accéder au nœud précédent, il faut repartir du début

**Représentation visuelle :**

```
HEAD
 ↓
[A | •]--→[B | •]--→[C | •]--→ null
```

**Exemple complet :**

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  // Ajouter à la fin - O(n)
  append(data) {
    let newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
    this.size++;
  }

  // Afficher tous les éléments
  display() {
    let current = this.head;
    let result = [];
    while (current) {
      result.push(current.data);
      current = current.next;
    }
    console.log(result.join(" -> "));
  }
}

// Utilisation
let list = new SinglyLinkedList();
list.append("Marshall");
list.append("Chermann");
list.append("Ingrid");
list.display(); // Marshall -> Chermann -> Ingrid
```

### 2.2 Liste Doublement Chaînée (Doubly Linked List)

Une liste doublement chaînée ajoute une référence supplémentaire : chaque nœud pointe vers le **nœud suivant** ET le **nœud précédent**.

**Structure d'un nœud :**

```javascript
class DoublyNode {
  constructor(data) {
    this.data = data;
    this.next = null; // Référence vers le nœud suivant
    this.prev = null; // Référence vers le nœud précédent
  }
}
```

**Caractéristiques :**

- Parcours dans **les deux sens** (avant et arrière)
- Insertion/suppression plus facile (pas besoin de garder trace du nœud précédent)
- Utilisation mémoire plus importante (deux références par nœud)
- Opérations légèrement plus complexes (gérer deux liens)

**Représentation visuelle :**

```
      HEAD
       ↓
null ←[• | A | •]←→[• | B | •]←→[• | C | •]→ null
       ↕            ↕            ↕
     prev         prev         prev
```

**Exemple complet :**

```javascript
class DoublyNode {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // Ajouter à la fin - O(1) grâce au tail
  append(data) {
    let newNode = new DoublyNode(data);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }
    this.size++;
  }

  // Afficher dans les deux sens
  displayForward() {
    let current = this.head;
    let result = [];
    while (current) {
      result.push(current.data);
      current = current.next;
    }
    console.log("Forward:", result.join(" ↔ "));
  }

  displayBackward() {
    let current = this.tail;
    let result = [];
    while (current) {
      result.push(current.data);
      current = current.prev;
    }
    console.log("Backward:", result.join(" ↔ "));
  }
}

// Utilisation
let dlist = new DoublyLinkedList();
dlist.append("Prudence");
dlist.append("Marshall");
dlist.append("Ingrid");
dlist.displayForward(); // Forward: Prudence ↔ Marshall ↔ Ingrid
dlist.displayBackward(); // Backward: Ingrid ↔ Marshall ↔ Prudence
```

### 2.3 Liste Circulaire (Circular Linked List)

Une liste circulaire peut être simple ou doublement chaînée, avec une différence clé : le **dernier nœud pointe vers le premier** au lieu de pointer vers `null`.

**Structure d'un nœud (version simple) :**

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

**Caractéristiques :**

- Parcours cyclique infini (utile pour certaines applications)
- Accès rapide au début depuis la fin
- Risque de boucles infinies si mal implémenté
- Détection de la fin de liste nécessite une vérification spéciale

**Représentation visuelle :**

```
      HEAD
       ↓
    ┌→[A | •]--→[B | •]--→[C | •]┐
    │                            │
    └────────────────────────────┘
```

**Exemple complet :**

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  // Ajouter à la fin - O(n)
  append(data) {
    let newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
      newNode.next = newNode; // Pointe vers lui-même
    } else {
      let current = this.head;
      while (current.next !== this.head) {
        current = current.next;
      }
      current.next = newNode;
      newNode.next = this.head; // Le dernier pointe vers le premier
    }
    this.size++;
  }

  // Afficher n éléments (pour éviter la boucle infinie)
  display(count = this.size) {
    if (!this.head) return;

    let current = this.head;
    let result = [];
    for (let i = 0; i < count; i++) {
      result.push(current.data);
      current = current.next;
    }
    console.log(result.join(" → ") + " → (retour au début)");
  }
}

// Utilisation
let clist = new CircularLinkedList();
clist.append("Lundi");
clist.append("Mardi");
clist.append("Mercredi");
clist.display(); // Lundi → Mardi → Mercredi → (retour au début)
clist.display(5); // Lundi → Mardi → Mercredi → Lundi → Mardi → (retour au début)
```

---

## 📝 Micro-Exercice #2 : Identifier le Type de Liste

**Objectif** : Analyser des structures de nœuds et identifier le type de liste chaînée.

Pour chaque structure de nœud suivante, identifiez s'il s'agit d'une liste simple, doublement chaînée, ou circulaire :

**Structure A :**

```javascript
class NodeA {
  constructor(data) {
    this.value = data;
    this.nextNode = null;
  }
}
// Le dernier nœud a nextNode = premier nœud
```

**Structure B :**

```javascript
class NodeB {
  constructor(data) {
    this.info = data;
    this.suivant = null;
    this.precedent = null;
  }
}
```

**Structure C :**

```javascript
class NodeC {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
// Le dernier nœud a next = null
```

<details>
<summary>💡 Voir la solution</summary>

**Structure A : Liste Circulaire Simple**

- Indices : Une seule référence (`nextNode`) mais le dernier nœud pointe vers le premier
- Type : Circulaire simple

**Structure B : Liste Doublement Chaînée**

- Indices : Deux références (`suivant` et `precedent`)
- Type : Doublement chaînée (peut être linéaire ou circulaire selon l'implémentation)

**Structure C : Liste Chaînée Simple**

- Indices : Une seule référence (`next`) et termine par `null`
- Type : Simple linéaire

**Points clés à retenir :**

- Une référence + `null` à la fin = **Simple**
- Deux références = **Doublement chaînée**
- Dernier nœud pointe vers le premier = **Circulaire**
</details>

---

## 3. 🚶 Parcours de Listes Chaînées

Le parcours d'une liste chaînée est une opération fondamentale qui consiste à visiter chaque nœud de la liste, du début à la fin.

### 3.1 Parcours de Base (Liste Simple)

L'algorithme de parcours suit ce schéma :

1. Commencer au nœud `head`
2. Tant que le nœud actuel n'est pas `null` :
   - Traiter les données du nœud actuel
   - Passer au nœud suivant (`current = current.next`)

**Code de parcours basique :**

```javascript
function traverseList(head) {
  let current = head;

  while (current !== null) {
    console.log(current.data); // Traiter les données
    current = current.next; // Passer au suivant
  }
}
```

**Complexité :** **O(n)** où n est le nombre de nœuds.

### 3.2 Parcours avec Accumulation

Souvent, nous voulons collecter ou transformer les données pendant le parcours :

```javascript
function collectValues(head) {
  let current = head;
  let values = [];

  while (current !== null) {
    values.push(current.data);
    current = current.next;
  }

  return values;
}

// Utilisation
let head = new Node(10);
head.next = new Node(20);
head.next.next = new Node(30);

console.log(collectValues(head)); // [10, 20, 30]
```

### 3.3 Parcours avec Condition

Parcourir jusqu'à trouver un élément spécifique :

```javascript
function findNode(head, targetValue) {
  let current = head;

  while (current !== null) {
    if (current.data === targetValue) {
      return current; // Trouvé !
    }
    current = current.next;
  }

  return null; // Non trouvé
}

// Utilisation
let node = findNode(head, 20);
if (node) {
  console.log("Trouvé:", node.data);
} else {
  console.log("Non trouvé");
}
```

**Complexité :**

- **Meilleur cas** : O(1) - l'élément est au début
- **Pire cas** : O(n) - l'élément est à la fin ou absent

### 3.4 Parcours Inverse (Liste Doublement Chaînée)

Avec une liste doublement chaînée, nous pouvons parcourir en sens inverse :

```javascript
function traverseBackward(tail) {
  let current = tail;

  while (current !== null) {
    console.log(current.data);
    current = current.prev; // Utiliser prev au lieu de next
  }
}
```

### 3.5 Parcours Récursif

Une approche élégante utilisant la récursion :

```javascript
function traverseRecursive(node) {
  // Cas de base : fin de la liste
  if (node === null) {
    return;
  }

  // Traiter le nœud actuel
  console.log(node.data);

  // Appel récursif sur le suivant
  traverseRecursive(node.next);
}

// Utilisation
traverseRecursive(head); // 10, 20, 30
```

**Note :** La version récursive utilise la pile d'appels, donc utilise O(n) d'espace mémoire supplémentaire.

---

## 📝 Micro-Exercice #3 : Compter les Nœuds

**Objectif** : Écrire une fonction qui compte le nombre de nœuds dans une liste chaînée.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

// À FAIRE : Implémenter cette fonction
function countNodes(head) {
  // Votre code ici
}

// Test
let head = new Node("A");
head.next = new Node("B");
head.next.next = new Node("C");
head.next.next.next = new Node("D");

console.log(countNodes(head)); // Devrait afficher 4
```

<details>
<summary>💡 Voir la solution</summary>

**Solution Itérative :**

```javascript
function countNodes(head) {
  let count = 0;
  let current = head;

  while (current !== null) {
    count++;
    current = current.next;
  }

  return count;
}
```

**Solution Récursive :**

```javascript
function countNodesRecursive(node) {
  // Cas de base : liste vide
  if (node === null) {
    return 0;
  }

  // 1 (nœud actuel) + nombre de nœuds restants
  return 1 + countNodesRecursive(node.next);
}
```

**Explication :**

- **Itérative** : Parcourt la liste avec une boucle `while`, incrémente un compteur
- **Récursive** : Chaque appel compte 1 nœud + le résultat du reste de la liste
- **Complexité** : O(n) pour les deux approches
- **Espace** : O(1) pour itérative, O(n) pour récursive (pile d'appels)

**Test :**

```javascript
let head = new Node("A");
head.next = new Node("B");
head.next.next = new Node("C");
head.next.next.next = new Node("D");

console.log(countNodes(head)); // 4
console.log(countNodesRecursive(head)); // 4
```

</details>

---

## 4. ⚖️ Comparaison : Listes Chaînées vs Tableaux

Comprendre les différences entre les listes chaînées et les tableaux est crucial pour choisir la structure de données appropriée.

### 4.1 Tableau Comparatif

| Aspect                   | Tableaux                        | Listes Chaînées                    |
| ------------------------ | ------------------------------- | ---------------------------------- |
| **Accès par index**      | O(1) - Direct                   | O(n) - Parcours nécessaire         |
| **Insertion au début**   | O(n) - Décalage requis          | O(1) - Juste changer head          |
| **Insertion à la fin**   | O(1) amortisé                   | O(n) simple, O(1) avec tail        |
| **Suppression au début** | O(n) - Décalage requis          | O(1) - Changer head                |
| **Suppression à la fin** | O(1)                            | O(n) - Trouver avant-dernier       |
| **Recherche**            | O(n) linéaire, O(log n) si trié | O(n) toujours                      |
| **Mémoire**              | Contigu, overhead minimal       | Dispersée, overhead des références |
| **Taille**               | Fixe (en JS dynamique)          | Dynamique naturellement            |
| **Cache CPU**            | Excellent                       | Médiocre                           |

### 4.2 Avantages des Listes Chaînées

**Insertion/Suppression au début : O(1)**

```javascript
// Ajouter au début d'une liste chaînée - O(1)
function prependLinkedList(head, data) {
  let newNode = new Node(data);
  newNode.next = head;
  return newNode; // Nouveau head
}

// Ajouter au début d'un tableau - O(n)
function prependArray(arr, data) {
  arr.unshift(data); // Doit décaler tous les éléments !
}
```

**Taille dynamique sans réallocation**

- Pas besoin de réallouer la mémoire quand la liste grandit
- Chaque nœud est alloué indépendamment

**Insertion/Suppression au milieu efficace (si on a la position)**

```javascript
// Insérer après un nœud donné - O(1)
function insertAfter(node, data) {
  let newNode = new Node(data);
  newNode.next = node.next;
  node.next = newNode;
}
```

### 4.3 Inconvénients des Listes Chaînées

**Pas d'accès direct par index**

```javascript
// Accéder au 100ème élément d'un tableau - O(1)
let element = array[99];

// Accéder au 100ème élément d'une liste chaînée - O(n)
let current = head;
for (let i = 0; i < 99; i++) {
  current = current.next;
}
let element = current.data;
```

**Overhead mémoire**

- Chaque nœud nécessite de la mémoire supplémentaire pour stocker les références
- Un tableau de 1000 nombres : ~4-8 Ko
- Une liste chaînée de 1000 nombres : ~12-24 Ko (selon l'architecture)

**Mauvaise localité de cache**

- Les nœuds sont dispersés en mémoire
- Le CPU ne peut pas prédire et précharger les données efficacement

### 4.4 Quand Utiliser Chaque Structure ?

**Utilisez un Tableau quand :**

- Vous avez besoin d'accès fréquent par index
- La taille est relativement stable
- Vous faites beaucoup de recherches
- La performance est critique et les données tiennent en cache

**Utilisez une Liste Chaînée quand :**

- Vous faites beaucoup d'insertions/suppressions au début
- La taille varie énormément et imprévisiblement
- Vous n'avez pas besoin d'accès par index
- Vous implémentez des structures comme des piles, files, ou graphes

---

## 📝 Micro-Exercice #4 : Analyser la Complexité

**Objectif** : Déterminer quelle structure de données est la plus efficace pour différentes opérations.

Pour chaque scénario, choisissez entre **Tableau** ou **Liste Chaînée** et justifiez avec la complexité :

**Scénario A :** Application de lecture de flux RSS où vous ajoutez constamment de nouveaux articles au début et supprimez les plus anciens à la fin.

**Scénario B :** Base de données d'étudiants où vous devez fréquemment accéder à l'étudiant numéro N pour afficher ses informations.

**Scénario C :** Historique du navigateur où vous ajoutez une nouvelle page à chaque visite et utilisez le bouton "Retour" pour supprimer la plus récente.

**Scénario D :** Liste de courses où vous ajoutez/supprimez des articles fréquemment n'importe où dans la liste.

<details>
<summary>💡 Voir la solution</summary>

**Scénario A : Liste Chaînée Doublement Chaînée**

- **Opérations** : Ajout au début (O(1)), suppression à la fin (O(1) avec tail)
- **Justification** : Avec une liste doublement chaînée et références head/tail, les deux opérations sont O(1)
- **Alternative tableau** : `unshift()` est O(n), `pop()` est O(1) → moins efficace

**Scénario B : Tableau**

- **Opérations** : Accès par index fréquent
- **Justification** : Tableau offre O(1) pour `array[N]`, liste chaînée nécessite O(N) parcours
- **Alternative liste** : Devrait parcourir N nœuds à chaque fois → très inefficace

**Scénario C : Liste Chaînée Simple (ou Pile)**

- **Opérations** : Ajout au début (O(1)), suppression au début (O(1))
- **Justification** : Comportement de pile (LIFO), liste chaînée parfaite
- **Alternative tableau** : `unshift()` et `shift()` sont tous deux O(n)
- **Note** : C'est exactement le cas d'usage d'une **pile** (stack)

**Scénario D : Cela Dépend**

- **Si ajout/suppression principalement au début/fin** : Liste chaînée doublement chaînée
- **Si accès par position fréquent** : Tableau
- **Compromis** : En réalité, pour une liste de courses, un tableau est souvent suffisant car la taille reste petite (< 100 éléments)
- **Considération pratique** : Pour de petites collections, la différence de performance est négligeable

**Leçon clé :**
Le choix dépend des **opérations dominantes** dans votre application. Analysez ce que vous faites le plus souvent !

</details>

---

## 5. 🌍 Applications Réelles des Listes Chaînées

Les listes chaînées sont utilisées dans de nombreux systèmes réels. Voici quelques exemples concrets :

### 5.1 Historique du Navigateur

Les navigateurs web utilisent des listes doublement chaînées pour implémenter l'historique de navigation :

```javascript
class HistoryNode {
  constructor(url, title) {
    this.url = url;
    this.title = title;
    this.prev = null; // Page précédente
    this.next = null; // Page suivante
  }
}

class BrowserHistory {
  constructor() {
    this.current = null;
  }

  // Visiter une nouvelle page
  visit(url, title) {
    let newPage = new HistoryNode(url, title);

    if (this.current) {
      this.current.next = newPage;
      newPage.prev = this.current;
    }

    this.current = newPage;
    console.log(`Visité: ${title}`);
  }

  // Bouton "Retour"
  back() {
    if (this.current && this.current.prev) {
      this.current = this.current.prev;
      console.log(`Retour à: ${this.current.title}`);
      return this.current;
    } else {
      console.log("Pas de page précédente");
      return null;
    }
  }

  // Bouton "Suivant"
  forward() {
    if (this.current && this.current.next) {
      this.current = this.current.next;
      console.log(` Suivant: ${this.current.title}`);
      return this.current;
    } else {
      console.logPas de page suivante");
      return null;
    }
  }
}

// Utilisation
let history = new BrowserHistory();
history.visit("https://google.com", "Google");
history.visit("https://github.com", "GitHub");
history.visit("https://stackoverflow.com", "Stack Overflow");

history.back(); // Retour à: GitHub
history.back(); // Retour à: Google
history.forward(); // Suivant: GitHub
```

### 5.2 Playlist Musicale

Les applications de musique utilisent souvent des listes circulaires pour les playlists en lecture continue :

```javascript
class Song {
  constructor(title, artist) {
    this.title = title;
    this.artist = artist;
    this.next = null;
  }
}

class CircularPlaylist {
  constructor() {
    this.current = null;
    this.size = 0;
  }

  addSong(title, artist) {
    let newSong = new Song(title, artist);

    if (!this.current) {
      this.current = newSong;
      newSong.next = newSong; // Pointe vers soi-même
    } else {
      // Trouver le dernier nœud
      let last = this.current;
      while (last.next !== this.current) {
        last = last.next;
      }
      last.next = newSong;
      newSong.next = this.current;
    }

    this.size++;
    console.log(`Ajouté: ${title} - ${artist}`);
  }

  play() {
    if (this.current) {
      console.log(`▶ Lecture: ${this.current.title} - ${this.current.artist}`);
    }
  }

  next() {
    if (this.current) {
      this.current = this.current.next;
      this.play();
    }
  }
}

// Utilisation
let playlist = new CircularPlaylist();
playlist.addSong("Pata Pata", "Miriam Makeba");
playlist.addSong("Zombie", "Fela Kuti");
playlist.addSong("Waka Waka", "Shakira");

playlist.play(); // ▶ Lecture: Pata Pata - Miriam Makeba
playlist.next(); // ▶ Lecture: Zombie - Fela Kuti
playlist.next(); // ▶ Lecture: Waka Waka - Shakira
playlist.next(); // ▶ Lecture: Pata Pata - Miriam Makeba (retour au début)
```

### 5.3 Système de Gestion de Tâches avec Priorités

Une file de tâches où chaque tâche peut être insérée à la position appropriée selon sa priorité :

```javascript
class Task {
  constructor(description, priority) {
    this.description = description;
    this.priority = priority; // 1 = haute, 2 = moyenne, 3 = basse
    this.next = null;
  }
}

class PriorityTaskQueue {
  constructor() {
    this.head = null;
  }

  // Insérer une tâche selon sa priorité
  addTask(description, priority) {
    let newTask = new Task(description, priority);

    // Cas 1 : Liste vide ou priorité plus haute que le head
    if (!this.head || priority < this.head.priority) {
      newTask.next = this.head;
      this.head = newTask;
      console.log(`Ajouté (priorité ${priority}): ${description}`);
      return;
    }

    // Cas 2 : Trouver la position d'insertion
    let current = this.head;
    while (current.next && current.next.priority <= priority) {
      current = current.next;
    }

    newTask.next = current.next;
    current.next = newTask;
    console.log(`Ajouté (priorité ${priority}): ${description}`);
  }

  // Exécuter la tâche la plus prioritaire
  executeNext() {
    if (!this.head) {
      console.log("Aucune tâche à exécuter");
      return null;
    }

    let task = this.head;
    this.head = this.head.next;
    console.log(
      `⚡ Exécution: ${task.description} (priorité ${task.priority})`,
    );
    return task;
  }

  // Afficher toutes les tâches
  displayAll() {
    if (!this.head) {
      console.log("Aucune tâche en attente");
      return;
    }

    console.log("Tâches en attente:");
    let current = this.head;
    let index = 1;
    while (current) {
      console.log(`  ${index}. [P${current.priority}] ${current.description}`);
      current = current.next;
      index++;
    }
  }
}

// Utilisation
let taskQueue = new PriorityTaskQueue();

taskQueue.addTask("Répondre aux emails", 2);
taskQueue.addTask("Corriger bug critique", 1);
taskQueue.addTask("Mettre à jour documentation", 3);
taskQueue.addTask("Réunion d'urgence", 1);

taskQueue.displayAll();
// Tâches en attente:
//   1. [P1] Corriger bug critique
//   2. [P1] Réunion d'urgence
//   3. [P2] Répondre aux emails
//   4. [P3] Mettre à jour documentation

taskQueue.executeNext(); // Exécution: Corriger bug critique (priorité 1)
taskQueue.executeNext(); // Exécution: Réunion d'urgence (priorité 1)
```

### 5.4 Autres Applications Courantes

**Systèmes d'exploitation :**

- Gestion des processus (liste de processus en attente)
- Allocation de mémoire (liste de blocs libres)

**Éditeurs de texte :**

- Fonction "Annuler/Refaire" (liste doublement chaînée)
- Gap buffer pour l'édition efficace

**Jeux vidéo :**

- Liste de sprites à afficher
- Gestion des objets de jeu

**Applications Web :**

- React Virtual DOM (structure arborescente basée sur des nœuds)
- Gestion de cache LRU (Least Recently Used)

---

## 📝 Exemples Pratiques

### Exemple Pratique 1 : Détection de Cycle dans une Liste

Un problème classique : détecter si une liste chaînée contient un cycle (un nœud qui pointe vers un nœud précédent).

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

// Algorithme de Floyd (Tortue et Lièvre)
function hasCycle(head) {
  if (!head || !head.next) return false;

  let slow = head; // Tortue : avance de 1
  let fast = head.next; // Lièvre : avance de 2

  while (fast && fast.next) {
    if (slow === fast) {
      return true; // Cycle détecté !
    }

    slow = slow.next;
    fast = fast.next.next;
  }

  return false; // Pas de cycle
}

// Test avec une liste normale
let a = new Node(1);
let b = new Node(2);
let c = new Node(3);
a.next = b;
b.next = c;

console.log(hasCycle(a)); // false

// Test avec un cycle
c.next = b; // Créer un cycle : 1 -> 2 -> 3 -> 2 -> 3 -> ...
console.log(hasCycle(a)); // true
```

**Complexité :**

- **Temps** : O(n)
- **Espace** : O(1) - pas de structure de données auxiliaire

### Exemple Pratique 2 : Inverser une Liste Chaînée

Inverser l'ordre des nœuds d'une liste chaînée.

```javascript
function reverseList(head) {
  let prev = null;
  let current = head;

  while (current !== null) {
    let nextTemp = current.next; // Sauvegarder le suivant
    current.next = prev; // Inverser le lien
    prev = current; // Avancer prev
    current = nextTemp; // Avancer current
  }

  return prev; // prev est le nouveau head
}

// Test
let head = new Node("A");
head.next = new Node("B");
head.next.next = new Node("C");

console.log("Avant inversion:");
// A -> B -> C -> null

let newHead = reverseList(head);

console.log("Après inversion:");
// C -> B -> A -> null
```

**Visualisation du processus :**

```
Étape initiale :
prev = null
current = A -> B -> C -> null

Itération 1 :
prev = A -> null
current = B -> C -> null

Itération 2 :
prev = B -> A -> null
current = C -> null

Itération 3 :
prev = C -> B -> A -> null
current = null (fin)
```

### Exemple Pratique 3 : Trouver le Milieu d'une Liste

Trouver le nœud du milieu en un seul parcours.

```javascript
function findMiddle(head) {
  if (!head) return null;

  let slow = head;
  let fast = head;

  // fast avance 2x plus vite que slow
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow; // slow est au milieu
}

// Test avec une liste de 5 éléments
let head = new Node(1);
head.next = new Node(2);
head.next.next = new Node(3);
head.next.next.next = new Node(4);
head.next.next.next.next = new Node(5);

let middle = findMiddle(head);
console.log(middle.data); // 3

// Test avec une liste de 6 éléments
head.next.next.next.next.next = new Node(6);
middle = findMiddle(head);
console.log(middle.data); // 4 (le second du milieu)
```

**Pourquoi ça marche ?**

- Quand `fast` atteint la fin, `slow` est au milieu
- Si la liste a n nœuds, `fast` fait n/2 sauts, donc `slow` aussi

---

## 💪 Exercices Pratiques

### Exercice 1 : Implémenter une Liste Chaînée Simple Complète

**Objectif :** Créer une classe `SinglyLinkedList` avec les méthodes suivantes :

- `append(data)` : Ajouter à la fin
- `prepend(data)` : Ajouter au début
- `insertAt(index, data)` : Insérer à une position donnée
- `deleteAt(index)` : Supprimer à une position donnée
- `find(data)` : Rechercher un élément
- `size()` : Retourner le nombre d'éléments
- `display()` : Afficher tous les éléments

**Code de départ :**

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this._size = 0;
  }

  // À FAIRE : Implémenter toutes les méthodes
}

// Tests
let list = new SinglyLinkedList();
list.append(10);
list.append(20);
list.prepend(5);
list.insertAt(2, 15);
console.log(list.size()); // 4
list.display(); // 5 -> 15 -> 10 -> 20
console.log(list.find(15)); // true
list.deleteAt(1);
list.display(); // 5 -> 10 -> 20
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this._size = 0;
  }

  // Ajouter à la fin - O(n)
  append(data) {
    let newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }

    this._size++;
  }

  // Ajouter au début - O(1)
  prepend(data) {
    let newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
    this._size++;
  }

  // Insérer à une position - O(n)
  insertAt(index, data) {
    if (index < 0 || index > this._size) {
      throw new Error("Index hors limites");
    }

    if (index === 0) {
      this.prepend(data);
      return;
    }

    let newNode = new Node(data);
    let current = this.head;
    let previous;
    let count = 0;

    while (count < index) {
      previous = current;
      current = current.next;
      count++;
    }

    newNode.next = current;
    previous.next = newNode;
    this._size++;
  }

  // Supprimer à une position - O(n)
  deleteAt(index) {
    if (index < 0 || index >= this._size) {
      throw new Error("Index hors limites");
    }

    if (index === 0) {
      this.head = this.head.next;
      this._size--;
      return;
    }

    let current = this.head;
    let previous;
    let count = 0;

    while (count < index) {
      previous = current;
      current = current.next;
      count++;
    }

    previous.next = current.next;
    this._size--;
  }

  // Rechercher un élément - O(n)
  find(data) {
    let current = this.head;

    while (current) {
      if (current.data === data) {
        return true;
      }
      current = current.next;
    }

    return false;
  }

  // Retourner la taille - O(1)
  size() {
    return this._size;
  }

  // Afficher tous les éléments - O(n)
  display() {
    let current = this.head;
    let result = [];

    while (current) {
      result.push(current.data);
      current = current.next;
    }

    console.log(result.join(" -> "));
  }
}

// Tests
let list = new SinglyLinkedList();
list.append(10);
list.append(20);
list.prepend(5);
list.insertAt(2, 15);
console.log("Taille:", list.size()); // Taille: 4
list.display(); // 5 -> 15 -> 10 -> 20
console.log("Trouve 15:", list.find(15)); // Trouve 15: true
console.log("Trouve 100:", list.find(100)); // Trouve 100: false
list.deleteAt(1);
list.display(); // 5 -> 10 -> 20
console.log("Taille finale:", list.size()); // Taille finale: 3
```

**Points clés :**

- Toujours vérifier si `head` est `null` pour les cas limites
- Gérer séparément les opérations au début (index 0)
- Maintenir un compteur `_size` pour éviter de parcourir à chaque fois
- Utiliser `previous` pour garder trace du nœud précédent lors des insertions/suppressions
</details>

---

### Exercice 2 : Fusionner Deux Listes Triées

**Objectif :** Fusionner deux listes chaînées triées en une seule liste triée.

```javascript
// Exemple :
// Liste 1 : 1 -> 3 -> 5
// Liste 2 : 2 -> 4 -> 6
// Résultat : 1 -> 2 -> 3 -> 4 -> 5 -> 6

function mergeSortedLists(head1, head2) {
  // Votre code ici
}

// Test
let list1 = new Node(1);
list1.next = new Node(3);
list1.next.next = new Node(5);

let list2 = new Node(2);
list2.next = new Node(4);
list2.next.next = new Node(6);

let merged = mergeSortedLists(list1, list2);
// Devrait afficher : 1 -> 2 -> 3 -> 4 -> 5 -> 6
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

function mergeSortedLists(head1, head2) {
  // Créer un nœud fictif pour faciliter la construction
  let dummy = new Node(0);
  let current = dummy;

  // Parcourir les deux listes simultanément
  while (head1 !== null && head2 !== null) {
    if (head1.data <= head2.data) {
      current.next = head1;
      head1 = head1.next;
    } else {
      current.next = head2;
      head2 = head2.next;
    }
    current = current.next;
  }

  // Ajouter les éléments restants
  if (head1 !== null) {
    current.next = head1;
  }
  if (head2 !== null) {
    current.next = head2;
  }

  return dummy.next; // Ignorer le nœud fictif
}

// Fonction utilitaire pour afficher une liste
function displayList(head) {
  let current = head;
  let result = [];
  while (current) {
    result.push(current.data);
    current = current.next;
  }
  console.log(result.join(" -> "));
}

// Test
let list1 = new Node(1);
list1.next = new Node(3);
list1.next.next = new Node(5);

let list2 = new Node(2);
list2.next = new Node(4);
list2.next.next = new Node(6);

console.log("Liste 1:");
displayList(list1); // 1 -> 3 -> 5

console.log("Liste 2:");
displayList(list2); // 2 -> 4 -> 6

let merged = mergeSortedLists(list1, list2);
console.log("Liste fusionnée:");
displayList(merged); // 1 -> 2 -> 3 -> 4 -> 5 -> 6
```

**Explication de l'algorithme :**

1. **Nœud fictif (dummy)** : Simplifie la logique en évitant de gérer le cas spécial du premier nœud
2. **Comparaison à chaque étape** : Compare les valeurs actuelles des deux listes
3. **Ajout du plus petit** : Ajoute le nœud avec la plus petite valeur à la liste résultat
4. **Éléments restants** : Une des listes peut se terminer avant l'autre, on attache le reste directement

**Complexité :**

- **Temps** : O(n + m) où n et m sont les tailles des deux listes
- **Espace** : O(1) - pas de nouvelle liste créée, on réutilise les nœuds existants

**Variante avec récursion :**

```javascript
function mergeSortedListsRecursive(head1, head2) {
  // Cas de base
  if (head1 === null) return head2;
  if (head2 === null) return head1;

  // Choisir le plus petit et récursion sur le reste
  if (head1.data <= head2.data) {
    head1.next = mergeSortedListsRecursive(head1.next, head2);
    return head1;
  } else {
    head2.next = mergeSortedListsRecursive(head1, head2.next);
    return head2;
  }
}
```

Cette version récursive est plus élégante mais utilise O(n + m) d'espace sur la pile d'appels.

</details>

---

### Exercice 3 : Supprimer les Doublons d'une Liste Non Triée

**Objectif :** Supprimer tous les nœuds en double d'une liste chaînée non triée.

```javascript
// Exemple :
// Entrée : 1 -> 3 -> 2 -> 3 -> 1 -> 4
// Sortie : 1 -> 3 -> 2 -> 4

function removeDuplicates(head) {
  // Votre code ici
}

// Test
let list = new Node(1);
list.next = new Node(3);
list.next.next = new Node(2);
list.next.next.next = new Node(3);
list.next.next.next.next = new Node(1);
list.next.next.next.next.next = new Node(4);

removeDuplicates(list);
// Devrait afficher : 1 -> 3 -> 2 -> 4
```

<details>
<summary>💡 Voir la solution</summary>

**Solution 1 : Avec Set (efficace)**

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

function removeDuplicates(head) {
  if (!head) return head;

  let seen = new Set();
  let current = head;
  let previous = null;

  while (current !== null) {
    if (seen.has(current.data)) {
      // Doublon trouvé, sauter ce nœud
      previous.next = current.next;
    } else {
      // Nouvelle valeur, l'ajouter au Set
      seen.add(current.data);
      previous = current;
    }
    current = current.next;
  }

  return head;
}

function displayList(head) {
  let current = head;
  let result = [];
  while (current) {
    result.push(current.data);
    current = current.next;
  }
  console.log(result.join(" -> "));
}

// Test
let list = new Node(1);
list.next = new Node(3);
list.next.next = new Node(2);
list.next.next.next = new Node(3);
list.next.next.next.next = new Node(1);
list.next.next.next.next.next = new Node(4);

console.log("Avant:");
displayList(list); // 1 -> 3 -> 2 -> 3 -> 1 -> 4

removeDuplicates(list);

console.log("Après:");
displayList(list); // 1 -> 3 -> 2 -> 4
```

**Complexité Solution 1 :**

- **Temps** : O(n) - un seul parcours
- **Espace** : O(n) - stockage des valeurs uniques dans le Set

---

**Solution 2 : Sans structure de données auxiliaire (moins efficace)**

```javascript
function removeDuplicatesNoBuffer(head) {
  if (!head) return head;

  let current = head;

  while (current !== null) {
    // Pour chaque nœud, parcourir le reste pour supprimer les doublons
    let runner = current;
    while (runner.next !== null) {
      if (runner.next.data === current.data) {
        runner.next = runner.next.next; // Supprimer le doublon
      } else {
        runner = runner.next;
      }
    }
    current = current.next;
  }

  return head;
}

// Test avec la même liste
let list2 = new Node(1);
list2.next = new Node(3);
list2.next.next = new Node(2);
list2.next.next.next = new Node(3);
list2.next.next.next.next = new Node(1);
list2.next.next.next.next.next = new Node(4);

console.log("Avant (solution 2):");
displayList(list2); // 1 -> 3 -> 2 -> 3 -> 1 -> 4

removeDuplicatesNoBuffer(list2);

console.log("Après (solution 2):");
displayList(list2); // 1 -> 3 -> 2 -> 4
```

**Complexité Solution 2 :**

- **Temps** : O(n²) - boucles imbriquées
- **Espace** : O(1) - pas de structure auxiliaire

---

**Comparaison des solutions :**

| Aspect      | Solution 1 (Set)                 | Solution 2 (Sans buffer)      |
| ----------- | -------------------------------- | ----------------------------- |
| Temps       | O(n)                             | O(n²)                         |
| Espace      | O(n)                             | O(1)                          |
| Cas d'usage | Préférable si mémoire disponible | Si contrainte mémoire stricte |

**Recommandation :** Utilisez la Solution 1 (avec Set) sauf si vous avez une contrainte mémoire très stricte.

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

Quelle est la complexité temporelle de l'accès au nème élément d'une liste chaînée simple ?

A) O(1)
B) O(log n)
C) O(n)
D) O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C) O(n)**

**Explication :**
Contrairement aux tableaux où l'accès par index est O(1), dans une liste chaînée, vous devez parcourir séquentiellement depuis le head jusqu'au nème nœud. Cela nécessite n-1 opérations `current = current.next`, d'où la complexité O(n).

```javascript
// Accéder au nème élément - O(n)
function getAt(head, n) {
  let current = head;
  for (let i = 0; i < n; i++) {
    if (!current) return null;
    current = current.next;
  }
  return current;
}
```

**Pourquoi pas les autres ?**

- **O(1)** : C'est la complexité pour les tableaux, pas les listes chaînées
- **O(log n)** : C'est la complexité de la recherche binaire (impossible sur liste chaînée)
- **O(n²)** : Ce serait le cas avec des boucles imbriquées, pas pour un simple accès
</details>

---

### Question 2

Quel type de liste chaînée est le PLUS approprié pour implémenter un historique de navigation web avec boutons "Retour" et "Suivant" ?

A) Liste chaînée simple
B) Liste doublement chaînée
C) Liste circulaire simple
D) Tableau

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Liste doublement chaînée**

**Explication :**
Un historique de navigation nécessite de se déplacer dans les **deux sens** :

- **Bouton "Retour"** : Aller vers le nœud précédent
- **Bouton "Suivant"** : Aller vers le nœud suivant

Une liste doublement chaînée possède les références `prev` et `next`, permettant de naviguer efficacement dans les deux directions en O(1).

```javascript
class HistoryNode {
  constructor(url) {
    this.url = url;
    this.prev = null; // ← Permet le bouton "Retour"
    this.next = null; // ← Permet le bouton "Suivant"
  }
}
```

**Pourquoi pas les autres ?**

- **Liste simple** : Pas de référence `prev`, impossible de revenir en arrière efficacement
- **Liste circulaire** : Pas adaptée car l'historique n'est pas cyclique
- **Tableau** : Moins efficace pour l'insertion/suppression (bien que possible)
</details>

---

### Question 3

Considérez ce code. Que se passe-t-il ?

```javascript
let node1 = new Node("A");
let node2 = new Node("B");
node1.next = node2;
node2.next = node1;
```

A) Cela crée une liste chaînée simple valide
B) Cela crée une liste circulaire avec 2 nœuds
C) Cela provoque une erreur
D) Les nœuds ne sont pas connectés

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Cela crée une liste circulaire avec 2 nœuds**

**Explication :**
Ce code crée une **boucle** entre deux nœuds :

- `node1.next` pointe vers `node2`
- `node2.next` pointe vers `node1`

Cela forme une liste circulaire à 2 nœuds : A → B → A → B → A → ...

**Représentation visuelle :**

```
    ┌─────┐
    ↓     ↑
[A | •]  [B | •]
```

**Danger :** Si vous parcourez cette liste sans condition d'arrêt, vous créerez une **boucle infinie** :

```javascript
let current = node1;
while (current !== null) {
  // ⚠️ current ne sera JAMAIS null !
  console.log(current.data);
  current = current.next;
}
// Affichera : A, B, A, B, A, B, ... à l'infini !
```

**Solution pour parcourir sans boucle infinie :**

```javascript
let current = node1;
let count = 0;
let maxIterations = 10;

while (current !== null && count < maxIterations) {
  console.log(current.data);
  current = current.next;
  count++;
}
```

**Pourquoi pas les autres ?**

- **Liste simple valide** : Une liste simple doit terminer par `null`, pas pointer en arrière
- **Erreur** : JavaScript permet de créer des références circulaires (contrairement à certains langages)
- **Pas connectés** : Les nœuds sont bien connectés, mais de manière circulaire
</details>

---

### Question 4

Quelle est la **principale raison** pour laquelle les listes chaînées sont moins efficaces que les tableaux pour la recherche séquentielle ?

A) Les listes chaînées ont une complexité O(n²) pour la recherche
B) La mauvaise localité de cache (cache locality) en mémoire
C) Les listes chaînées ne peuvent pas être parcourues séquentiellement
D) Les listes chaînées nécessitent plus de comparaisons

<details>
<summary>Voir la réponse</summary>

**Réponse : B) La mauvaise localité de cache (cache locality) en mémoire**

**Explication :**
Même si la recherche linéaire est O(n) pour les **deux** structures, les listes chaînées sont souvent **plus lentes en pratique** à cause de la **localité de cache** :

**Tableaux :**

```
Mémoire : [10][20][30][40][50] ← Tous contigus
          ↑
Le CPU précharge tout ce bloc dans le cache
```

**Listes Chaînées :**

```
Mémoire :
  Adresse 1000: [10 | 5000]
  Adresse 5000: [20 | 9000]  ← Dispersés en mémoire !
  Adresse 9000: [30 | 3000]

Le CPU doit constamment accéder à la RAM (plus lent)
```

**Différences concrètes :**

- **Tableau** : Accès mémoire prédictifs, le CPU précharge les données suivantes
- **Liste chaînée** : Accès mémoire imprévisibles, chaque `next` peut pointer n'importe où

**Impact réel :**
Sur des listes de 10,000 éléments :

- Recherche dans un tableau : ~0.1ms
- Recherche dans une liste chaînée : ~0.5ms (5x plus lent)

**Pourquoi pas les autres ?**

- **O(n²)** : Faux, la recherche est O(n) pour les deux
- **Pas de parcours séquentiel** : Faux, on peut parcourir avec `next`
- **Plus de comparaisons** : Faux, le même nombre de comparaisons
</details>

---

### Question 5

Vous devez implémenter une playlist musicale où l'utilisateur peut ajouter des chansons à la fin, revenir à la chanson précédente, ou passer à la suivante. Après la dernière chanson, la lecture revient automatiquement à la première. Quelle structure est la PLUS appropriée ?

A) Liste chaînée simple
B) Liste doublement chaînée linéaire
C) Liste doublement chaînée circulaire
D) Tableau circulaire

<details>
<summary>Voir la réponse</summary>

**Réponse : C) Liste doublement chaînée circulaire**

**Explication :**
Les exigences sont :

1. ✅ **Ajouter à la fin** : Nécessite un pointeur `tail` (O(1) avec tail)
2. ✅ **Revenir en arrière** : Nécessite `prev` (liste doublement chaînée)
3. ✅ **Passer au suivant** : Nécessite `next`
4. ✅ **Retour automatique au début** : Nécessite une structure circulaire

Une liste doublement chaînée circulaire remplit tous ces critères :

```javascript
class Song {
  constructor(title) {
    this.title = title;
    this.next = null;
    this.prev = null;
  }
}

class CircularPlaylist {
  constructor() {
    this.current = null;
  }

  // Ajouter une chanson - O(1) avec référence tail
  addSong(title) {
    let newSong = new Song(title);

    if (!this.current) {
      this.current = newSong;
      newSong.next = newSong;
      newSong.prev = newSong;
    } else {
      let tail = this.current.prev;
      tail.next = newSong;
      newSong.prev = tail;
      newSong.next = this.current;
      this.current.prev = newSong;
    }
  }

  // Suivant - O(1)
  next() {
    if (this.current) {
      this.current = this.current.next; // Automatiquement circulaire !
    }
  }

  // Précédent - O(1)
  previous() {
    if (this.current) {
      this.current = this.current.prev;
    }
  }
}

// Utilisation
let playlist = new CircularPlaylist();
playlist.addSong("Chanson 1");
playlist.addSong("Chanson 2");
playlist.addSong("Chanson 3");

playlist.next(); // Chanson 2
playlist.next(); // Chanson 3
playlist.next(); // Chanson 1 (retour au début automatique!)
playlist.previous(); // Chanson 3
```

**Pourquoi pas les autres ?**

- **Liste simple** : Pas de `prev`, impossible de revenir en arrière efficacement
- **Liste doublement chaînée linéaire** : Pas de retour automatique au début (termine par `null`)
- **Tableau circulaire** : Moins flexible pour l'ajout/suppression dynamique de chansons
</details>

---

## 📌 Récapitulatif en 8 Points Clés

### 1. Structure d'un Nœud

Chaque nœud contient des **données** et une **référence** vers le nœud suivant. Le dernier nœud pointe vers `null` (sauf dans les listes circulaires). Le premier nœud est appelé **head**, le dernier **tail**.

### 2. Types de Listes Chaînées

- **Simple** : Une référence (`next`), parcours unidirectionnel
- **Doublement chaînée** : Deux références (`next` et `prev`), parcours bidirectionnel
- **Circulaire** : Le dernier nœud pointe vers le premier, parcours infini

### 3. Complexités Temporelles Clés

- Accès par index : **O(n)** (vs O(1) pour tableaux)
- Insertion au début : **O(1)** (vs O(n) pour tableaux)
- Insertion à la fin : **O(n)** sans tail, **O(1)** avec tail
- Recherche : **O(n)** toujours

### 4. Parcours de Liste

Utiliser une boucle `while` avec condition `current !== null`. La technique du "coureur" (`slow` et `fast`) permet de trouver le milieu ou détecter les cycles.

### 5. Avantages des Listes Chaînées

- Insertion/suppression au début très efficace (O(1))
- Taille dynamique sans réallocation
- Pas de décalage d'éléments lors des insertions/suppressions

### 6. Inconvénients des Listes Chaînées

- Pas d'accès direct par index (O(n))
- Overhead mémoire des références
- Mauvaise localité de cache (performance réelle plus lente)

### 7. Applications Réelles

Historique de navigation (liste doublement chaînée), playlists musicales (liste circulaire), gestion de tâches avec priorités, systèmes d'exploitation (gestion de processus).

### 8. Patterns Algorithmiques Importants

Technique de la tortue et du lièvre (détection de cycle), inversion de liste, fusion de listes triées, suppression de doublons.

---

## 🎓 Conclusion

Les **listes chaînées** représentent un changement de paradigme par rapport aux tableaux. Plutôt que de stocker les données de manière contiguë, elles utilisent des **références** pour créer une chaîne d'éléments dispersés en mémoire.

### Ce que vous avez appris

Dans cette leçon, vous avez découvert :

La structure fondamentale des nœuds et des listes chaînées
Les trois types principaux de listes chaînées et leurs cas d'usage
Comment parcourir efficacement une liste chaînée
Les compromis entre listes chaînées et tableaux
Des algorithmes classiques (détection de cycle, inversion, fusion)
Des applications concrètes dans les systèmes réels

### Quand utiliser les listes chaînées ?

Privilégiez les listes chaînées lorsque :

- Vous faites **beaucoup d'insertions/suppressions au début**
- La **taille de votre collection est très variable**
- Vous n'avez **pas besoin d'accès par index**
- Vous implémentez des structures comme des **piles, files, ou graphes**

Privilégiez les tableaux lorsque :

- Vous avez besoin d'**accès fréquent par index**
- La **taille est relativement stable**
- La **performance est critique** et les données tiennent en cache
- Vous faites beaucoup de **recherches**

---

## ➡️ Prochaine Étape : Leçon 9

### Ce qui vous attend

Dans la prochaine leçon, **« Implémentation de Listes Chaînées Simples en JavaScript »**, vous allez passer de la théorie à la pratique en construisant une liste chaînée complète.

**Vous découvrirez :**

- Comment implémenter une classe complète `SinglyLinkedList` en JavaScript
- Les méthodes essentielles : insertion, suppression, recherche
- La gestion des cas limites et des erreurs
- L'optimisation des performances avec les pointeurs `head` et `tail`

### Préparez-vous !

Assurez-vous de bien comprendre la structure d'un nœud et le parcours avec une boucle `while`. Ces fondamentaux seront essentiels pour implémenter votre propre liste chaînée.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Linked Lists in 10 minutes](https://www.youtube.com/watch?v=WwfhLC16bis) - Introduction visuelle rapide
- [Why you should learn about Linked Lists](https://medium.com/basecs/whats-a-linked-list-anyway-part-1-d8b7e6508b9d) - Article détaillé
- [Visualgo - Linked List Visualization](https://visualgo.net/en/list) - Visualisation interactive

### Outils utiles

- **[Algorithm Visualizer](https://algorithm-visualizer.org/brute-force/linked-list-traversal)** : Animations pas-à-pas des opérations
- **[Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/LinkedList.html)** : Outil pédagogique de l'Université de San Francisco

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices
- Dessiner vos propres schémas de listes chaînées pour visualiser les connexions

> 💡 **Conseil**
>
> La meilleure façon de comprendre les listes chaînées est de les **dessiner**. Prenez un papier et tracez les nœuds avec leurs flèches pour chaque opération. Cette visualisation concrète ancre les concepts bien mieux que la simple lecture du code !

---

**Prêt pour la Leçon 9 ?** 🚀

Rendez-vous dans la prochaine leçon pour implémenter une liste chaînée complète en JavaScript !

---

<div align="center">

**Leçon 8 sur 42 - Module 2 : Structures de Données Essentielles en JavaScript**

[⬅️ Leçon 7 : Tableaux - Listes Dynamiques et Opérations de Base](./lecon-1-tableaux-listes-dynamiques-operations-base.md) | [Retour au sommaire](./README.md) | [Leçon 9 : Implémentation de Listes Chaînées Simples en JavaScript ➡️](./lecon-3-implementation-listes-chainees-simples-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
