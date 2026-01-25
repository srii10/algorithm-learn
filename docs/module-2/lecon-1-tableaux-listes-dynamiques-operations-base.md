##### Leçon 7 sur 42

# Tableaux : Listes Dynamiques et Opérations de Base

**Module 2** : Structures de Données Essentielles en JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre ce qu'est un tableau et ses caractéristiques en JavaScript
- Créer et initialiser des tableaux avec différentes méthodes
- Accéder, modifier et manipuler les éléments d'un tableau
- Utiliser les opérations de base : `push()`, `pop()`, `shift()`, `unshift()`
- Rechercher des éléments avec `indexOf()`, `lastIndexOf()` et `includes()`
- Parcourir des tableaux avec différentes techniques d'itération

---

### ⏱️ Durée estimée : 2h - 3h

---

## 📚 Prérequis

- **Leçon 2 : Introduction à JavaScript pour le Développement d'Algorithmes** - Variables, fonctions, boucles
- **Leçon 4 : Notation Big O** - Compréhension de la complexité algorithmique
- **Environnement de développement** : Node.js ou navigateur avec console

---

## 🚀 Introduction : Les Tableaux, Collections Dynamiques Essentielles

Imaginez que vous gérez une liste de courses. Vous ajoutez des articles au fur et à mesure que vous y pensez, vous en retirez quand vous les achetez, et parfois vous vérifiez si un article spécifique est déjà dans votre liste. Comment organiseriez-vous cette information ?

En programmation, les **tableaux** (arrays en anglais) sont exactement cela : des **collections ordonnées** qui vous permettent de stocker et gérer plusieurs valeurs dans une seule structure. Ils sont omniprésents dans le développement logiciel et constituent la base de nombreuses structures de données plus complexes.

**Pourquoi les tableaux sont-ils si importants ?**

- **Stockage structuré** : Organisez des collections de données de manière ordonnée
- **Accès efficace** : Récupérez n'importe quel élément instantanément grâce aux index
- **Flexibilité** : En JavaScript, les tableaux sont dynamiques et s'adaptent automatiquement
- **Fondation solide** : Base de structures de données plus avancées (piles, files, listes)

Dans cette leçon, nous allons explorer en profondeur les tableaux JavaScript, en partant des bases jusqu'aux opérations essentielles. Vous comprendrez non seulement **comment** utiliser les tableaux, mais aussi **pourquoi** certaines opérations sont plus efficaces que d'autres.

> **Point Clé**
>
> Les tableaux JavaScript sont des structures de données **dynamiques** et **hétérogènes** qui peuvent contenir n'importe quel type de données. Contrairement à d'autres langages, vous n'avez pas besoin de déclarer leur taille à l'avance ni de vous limiter à un seul type d'éléments.

---

## 📦 Qu'est-ce qu'un Tableau ?

Un **tableau** (array) est une structure de données qui stocke une collection **ordonnée** d'éléments. Chaque élément est identifié par un **index numérique** qui commence à zéro.

---

### Concept Fondamental

Visualisez un tableau comme une série de boîtes numérotées, côte à côte :

```
Index:    0       1       2       3       4
        ┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐
Valeur: │ 10│   │ 20│   │ 30│   │ 40│   │ 50│
        └───┘   └───┘   └───┘   └───┘   └───┘
```

**Caractéristiques clés des tableaux JavaScript :**

- **Indexation par zéro** : Le premier élément est à l'index 0
- **Taille dynamique** : La taille peut augmenter ou diminuer automatiquement
- **Types hétérogènes** : Peut contenir différents types de données
- **Objets spéciaux** : En réalité, ce sont des objets avec des méthodes intégrées

**Exemple simple :**

```javascript
// Un tableau de nombres
let nombres = [10, 20, 30, 40, 50];

// Accès au premier élément (index 0)
console.log(nombres[0]); // Affiche: 10

// Accès au troisième élément (index 2)
console.log(nombres[2]); // Affiche: 30

// La propriété length indique le nombre d'éléments
console.log(nombres.length); // Affiche: 5
```

> **Note importante :**
>
> L'indexation commence à **zéro**, pas à un ! C'est une convention dans la plupart des langages de programmation. Le dernier élément d'un tableau de longueur `n` est donc à l'index `n-1`.

---

### Nature Dynamique des Tableaux JavaScript

Contrairement à des langages comme C ou Java où les tableaux ont une taille fixe, **les tableaux JavaScript sont dynamiques**. Ils s'agrandissent automatiquement quand vous ajoutez des éléments et peuvent être réduits si nécessaire.

```javascript
let panierAchats = []; // Commence vide
console.log(panierAchats.length); // Affiche: 0

// Ajout d'éléments - le tableau grandit automatiquement
panierAchats.push("Ordinateur");
panierAchats.push("Souris");
panierAchats.push("Clavier");

console.log(panierAchats); // ["Ordinateur", "Souris", "Clavier"]
console.log(panierAchats.length); // Affiche: 3

// Le tableau peut aussi contenir différents types
let melange = [42, "texte", true, null, { nom: "Chermann" }];
console.log(melange); // [42, "texte", true, null, {nom: "Chermann"}]
```

Cette flexibilité simplifie considérablement le développement, car vous n'avez pas à gérer manuellement la mémoire ou la taille du tableau.

---

## 🏗️ Création et Initialisation de Tableaux

Il existe plusieurs façons de créer des tableaux en JavaScript. Explorons les méthodes les plus courantes.

---

### Méthode 1 : Notation Littérale (Recommandée)

La façon la plus simple et la plus utilisée est la **notation littérale** avec des crochets `[]`.

```javascript
// Tableau vide
let tableauVide = [];
console.log(tableauVide); // []

// Tableau avec des nombres
let scores = [85, 92, 78, 95, 88];
console.log(scores); // [85, 92, 78, 95, 88]

// Tableau avec des chaînes de caractères
let fruits = ["Pomme", "Banane", "Orange"];
console.log(fruits); // ["Pomme", "Banane", "Orange"]

// Tableau avec des types mixtes (possible mais à éviter si non nécessaire)
let donneesMixtes = [1, "hello", true, null, { id: 1 }];
console.log(donneesMixtes); // [1, "hello", true, null, {id: 1}]
```

**Pourquoi cette méthode est recommandée ?**

- Plus **concise** et **lisible**
- Syntaxe **moderne** et **claire**
- **Performante** et directe

---

### Méthode 2 : Constructeur `Array()`

Le constructeur `Array()` offre deux comportements différents selon le nombre d'arguments :

```javascript
// 1. Avec UN seul argument numérique : crée un tableau vide de cette longueur
let tableauCinqElements = new Array(5);
console.log(tableauCinqElements); // [empty × 5] ou [undefined, undefined, undefined, undefined, undefined]
console.log(tableauCinqElements.length); // 5

// 2. Avec plusieurs arguments : crée un tableau avec ces éléments
let couleurs = new Array("Rouge", "Vert", "Bleu");
console.log(couleurs); // ["Rouge", "Vert", "Bleu"]
```

**Piège Courant :**

```javascript
// Un seul nombre : crée un tableau de cette longueur (VIDE)
let t1 = new Array(3);
console.log(t1); // [empty × 3]
console.log(t1[0]); // undefined

// Avec crochets : crée un tableau contenant ce nombre
let t2 = [3];
console.log(t2); // [3]
console.log(t2[0]); // 3

// Multiple arguments : crée un tableau avec ces éléments
let t3 = new Array(1, 2, 3);
console.log(t3); // [1, 2, 3]
```

> **Conseil :**
>
> Préférez la **notation littérale `[]`** dans la plupart des cas. Utilisez `new Array()` uniquement si vous avez une raison spécifique, comme créer un tableau d'une longueur prédéfinie.

---

## 📝 Micro-Exercice #1 : Créer des Tableaux

**Objectif :** Maîtriser la création de tableaux avec différentes méthodes

**Instructions :**

1. Créez un tableau vide nommé `listeCoursesVide`
2. Créez un tableau `couleursPrimaires` contenant "Rouge", "Vert", "Bleu"
3. Créez un tableau `notes` avec les valeurs 85, 92, 78, 95
4. Créez un tableau de 10 emplacements vides en utilisant `new Array()`

<details>
<summary>💡 Voir la solution</summary>

```javascript
// 1. Tableau vide avec notation littérale
let listeCoursesVide = [];
console.log(listeCoursesVide); // []

// 2. Tableau de chaînes de caractères
let couleursPrimaires = ["Rouge", "Vert", "Bleu"];
console.log(couleursPrimaires); // ["Rouge", "Vert", "Bleu"]

// 3. Tableau de nombres
let notes = [85, 92, 78, 95];
console.log(notes); // [85, 92, 78, 95]

// 4. Tableau avec longueur prédéfinie
let tableauVide = new Array(10);
console.log(tableauVide.length); // 10
console.log(tableauVide); // [empty × 10]
```

**Explication :**

- La notation littérale `[]` est la plus directe et lisible
- Les éléments sont séparés par des virgules
- `new Array(10)` crée un tableau avec 10 emplacements vides (undefined)
- Chaque méthode a son utilité selon le contexte

</details>

---

## 🔍 Accès et Modification d'Éléments

Une fois qu'un tableau est créé, vous devez pouvoir **accéder** à ses éléments et les **modifier**.

---

### Accès par Index

L'accès à un élément se fait en utilisant son **index entre crochets**.

```javascript
let animaux = ["Lion", "Tigre", "Ours", "Loup"];

// Accès au premier élément (index 0)
console.log(animaux[0]); // "Lion"

// Accès au troisième élément (index 2)
console.log(animaux[2]); // "Ours"

// Accès au dernier élément
console.log(animaux[animaux.length - 1]); // "Loup"

// Accès à un index inexistant retourne undefined
console.log(animaux[10]); // undefined
```

**Formule pour le dernier élément :**

```javascript
// Dernier élément = tableau[longueur - 1]
let dernierElement = animaux[animaux.length - 1];
```

**Complexité :** O(1) - Accès instantané, peu importe la taille du tableau !

---

### Modification par Index

Pour modifier un élément, assignez une nouvelle valeur à un index spécifique.

```javascript
let scores = [85, 92, 78, 95];
console.log("Scores originaux:", scores); // [85, 92, 78, 95]

// Modifier le deuxième score (index 1)
scores[1] = 88;
console.log("Scores modifiés:", scores); // [85, 88, 78, 95]

// Ajouter un élément au-delà de la longueur actuelle
scores[5] = 100;
console.log("Après ajout à l'index 5:", scores);
// [85, 88, 78, 95, undefined, 100]
console.log("Nouvelle longueur:", scores.length); // 6
```

**Attention :** Si vous assignez une valeur à un index au-delà de la longueur actuelle, JavaScript crée des emplacements vides (`undefined`) entre le dernier élément existant et le nouvel élément.

**Complexité :** O(1) - Modification instantanée

---

### Propriété `length`

La propriété `length` retourne le nombre d'éléments dans le tableau. C'est une propriété **modifiable**.

```javascript
let inventaire = ["Ordinateur", "Souris", "Clavier", "Moniteur"];
console.log("Longueur initiale:", inventaire.length); // 4

// Utiliser length pour ajouter à la fin
inventaire[inventaire.length] = "Webcam";
console.log("Après ajout:", inventaire);
// ["Ordinateur", "Souris", "Clavier", "Moniteur", "Webcam"]
console.log("Nouvelle longueur:", inventaire.length); // 5

// Réduire la longueur tronque le tableau
inventaire.length = 3;
console.log("Après truncation:", inventaire);
// ["Ordinateur", "Souris", "Clavier"]

// Vider complètement le tableau
inventaire.length = 0;
console.log("Après vidage:", inventaire); // []
```

**Complexité :** O(1) pour lire `length`, O(n) pour modifier si on réduit la taille

---

## 📝 Micro-Exercice #2 : Accès et Modification

**Objectif :** Pratiquer l'accès et la modification d'éléments de tableau

**Instructions :**

Soit le tableau suivant :

```javascript
let temperatures = [22, 25, 19, 28, 24];
```

1. Affichez la première température
2. Affichez la dernière température
3. Modifiez la température du troisième jour (index 2) à 21
4. Ajoutez une température de 26 à la fin en utilisant `length`
5. Affichez le tableau final et sa longueur

<details>
<summary>💡 Voir la solution</summary>

```javascript
let temperatures = [22, 25, 19, 28, 24];

// 1. Première température (index 0)
console.log("Première température:", temperatures[0]); // 22

// 2. Dernière température (length - 1)
console.log("Dernière température:", temperatures[temperatures.length - 1]); // 24

// 3. Modifier l'élément à l'index 2
temperatures[2] = 21;
console.log("Après modification:", temperatures); // [22, 25, 21, 28, 24]

// 4. Ajouter à la fin avec length
temperatures[temperatures.length] = 26;
console.log("Après ajout:", temperatures); // [22, 25, 21, 28, 24, 26]

// 5. Afficher le tableau final et sa longueur
console.log("Tableau final:", temperatures);
console.log("Longueur finale:", temperatures.length); // 6
```

**Explication :**

- `tableau[0]` accède toujours au premier élément
- `tableau[tableau.length - 1]` accède toujours au dernier élément
- Assigner à `tableau[longueur]` ajoute un élément à la fin
- Toutes ces opérations sont en temps constant O(1)

</details>

---

## ➕➖ Opérations de Base : Ajouter et Retirer des Éléments

JavaScript fournit des méthodes intégrées pour manipuler les tableaux. Comprendre leur comportement et leur performance est crucial.

---

### `push()` - Ajouter à la Fin

La méthode `push()` ajoute un ou plusieurs éléments **à la fin** du tableau et retourne la **nouvelle longueur**.

```javascript
let taches = ["Faire les courses", "Payer les factures"];
console.log("Tâches initiales:", taches); // ["Faire les courses", "Payer les factures"]

// Ajouter un élément
let nouvelleLongueur = taches.push("Nettoyer la chambre");
console.log("Après push:", taches);
// ["Faire les courses", "Payer les factures", "Nettoyer la chambre"]
console.log("Nouvelle longueur:", nouvelleLongueur); // 3

// Ajouter plusieurs éléments en une seule fois
taches.push("Appeler maman", "Lire un livre");
console.log("Après push multiple:", taches);
// ["Faire les courses", "Payer les factures", "Nettoyer la chambre", "Appeler maman", "Lire un livre"]
```

**Caractéristiques :**

- **Complexité :** O(1) - Temps constant (amorti)
- **Retourne** la nouvelle longueur
- **Modifie** le tableau original
- **Rapide** et efficace

---

### `pop()` - Retirer de la Fin

La méthode `pop()` retire et **retourne** le dernier élément du tableau.

```javascript
let file = ["Chermann", "Ingrid", "Prudence", "Marshall"];
console.log("File initiale:", file); // ["Chermann", "Ingrid", "Prudence", "Marshall"]

// Retirer le dernier élément
let dernierRetire = file.pop();
console.log("Élément retiré:", dernierRetire); // "Marshall"
console.log("File après pop:", file); // ["Chermann", "Ingrid", "Prudence"]

// pop() sur un tableau vide retourne undefined
let vide = [];
console.log(vide.pop()); // undefined
```

**Caractéristiques :**

- **Complexité :** O(1) - Temps constant
- **Retourne** l'élément retiré
- **Modifie** le tableau original
- **Rapide** et efficace

---

### `unshift()` - Ajouter au Début

La méthode `unshift()` ajoute un ou plusieurs éléments **au début** du tableau et retourne la **nouvelle longueur**.

```javascript
let nombres = [30, 40, 50];
console.log("Nombres initiaux:", nombres); // [30, 40, 50]

// Ajouter au début
let nouvelleLongueur = nombres.unshift(20);
console.log("Après unshift:", nombres); // [20, 30, 40, 50]
console.log("Nouvelle longueur:", nouvelleLongueur); // 4

// Ajouter plusieurs éléments au début
nombres.unshift(0, 10);
console.log("Après unshift multiple:", nombres); // [0, 10, 20, 30, 40, 50]
```

**Attention - Performance :**

```javascript
// unshift() doit décaler TOUS les éléments existants
// Visualisation :
// Avant:  [30, 40, 50]
//          ↓   ↓   ↓  (décalage vers la droite)
// Après: [20, 30, 40, 50]
```

**Caractéristiques :**

- **Complexité :** O(n) - Linéaire (doit décaler tous les éléments)
- **Retourne** la nouvelle longueur
- **Modifie** le tableau original
- **Plus lent** que `push()` pour les grands tableaux

---

### `shift()` - Retirer du Début

La méthode `shift()` retire et **retourne** le premier élément du tableau.

```javascript
let file = ["Chermann", "Ingrid", "Prudence", "Marshall"];
console.log("File initiale:", file); // ["Chermann", "Ingrid", "Prudence", "Marshall"]

// Retirer le premier élément
let premierRetire = file.shift();
console.log("Élément retiré:", premierRetire); // "Chermann"
console.log("File après shift:", file); // ["Ingrid", "Prudence", "Marshall"]

// shift() sur un tableau vide retourne undefined
let vide = [];
console.log(vide.shift()); // undefined
```

**Attention - Performance :**

```javascript
// shift() doit décaler TOUS les éléments restants
// Visualisation :
// Avant:  [Chermann, Ingrid, Prudence, Marshall]
//         (retire Chermann)
//                 Ingrid → Prudence → Marshall (décalage vers la gauche)
// Après:  [Ingrid, Prudence, Marshall]
```

**Caractéristiques :**

- **Complexité :** O(n) - Linéaire (doit décaler tous les éléments)
- **Retourne** l'élément retiré
- **Modifie** le tableau original
- **Plus lent** que `pop()` pour les grands tableaux

---

### Comparaison des Performances

| Opération   | Complexité | Position | Performance |
| ----------- | ---------- | -------- | ----------- |
| `push()`    | O(1)       | Fin      | Rapide      |
| `pop()`     | O(1)       | Fin      | Rapide      |
| `unshift()` | O(n)       | Début    | Lent        |
| `shift()`   | O(n)       | Début    | Lent        |

> **Règle d'Or :**
>
> Préférez **`push()` et `pop()`** (fin du tableau) plutôt que **`unshift()` et `shift()`** (début du tableau) pour de meilleures performances, surtout avec des tableaux volumineux.

---

## 📝 Micro-Exercice #3 : Opérations d'Ajout/Retrait

**Objectif :** Comprendre l'impact des différentes opérations

**Instructions :**

Analysez le code suivant et déterminez :

1. L'état final du tableau
2. La complexité temporelle totale

```javascript
let pile = [];

pile.push(1); // Opération 1
pile.push(2); // Opération 2
pile.push(3); // Opération 3
pile.pop(); // Opération 4
pile.unshift(0); // Opération 5
pile.shift(); // Opération 6

// Quel est l'état final de pile ?
// Quelle est la complexité temporelle globale ?
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
let pile = [];

// Opération 1 : push(1) - O(1)
pile.push(1);
console.log("Après push(1):", pile); // [1]

// Opération 2 : push(2) - O(1)
pile.push(2);
console.log("Après push(2):", pile); // [1, 2]

// Opération 3 : push(3) - O(1)
pile.push(3);
console.log("Après push(3):", pile); // [1, 2, 3]

// Opération 4 : pop() - O(1)
pile.pop();
console.log("Après pop():", pile); // [1, 2]

// Opération 5 : unshift(0) - O(n)
pile.unshift(0);
console.log("Après unshift(0):", pile); // [0, 1, 2]

// Opération 6 : shift() - O(n)
pile.shift();
console.log("Après shift():", pile); // [1, 2]

// État final : [1, 2]
```

**Analyse de complexité :**

- Opérations 1-4 : O(1) + O(1) + O(1) + O(1) = O(1)
- Opération 5 : O(n) - décale tous les éléments à droite
- Opération 6 : O(n) - décale tous les éléments à gauche
- **Complexité totale : O(n)**

**Explication :**

Les opérations `push()` et `pop()` sont très rapides (O(1)) car elles travaillent à la fin du tableau. En revanche, `unshift()` et `shift()` sont plus lentes (O(n)) car elles doivent réorganiser tous les éléments existants. La complexité globale est donc dominée par les opérations O(n).

</details>

---

## 🔎 Recherche d'Éléments

JavaScript offre plusieurs méthodes pour trouver des éléments dans un tableau.

---

### `indexOf()` - Trouver le Premier Index

La méthode `indexOf()` retourne l'**index de la première occurrence** d'un élément, ou **-1** s'il n'est pas trouvé.

```javascript
let fruits = ["Pomme", "Banane", "Orange", "Banane"];

console.log(fruits.indexOf("Banane")); // 1 (première occurrence)
console.log(fruits.indexOf("Orange")); // 2
console.log(fruits.indexOf("Kiwi")); // -1 (non trouvé)

// Recherche à partir d'un index spécifique
console.log(fruits.indexOf("Banane", 2)); // 3 (cherche à partir de l'index 2)
```

**Caractéristiques :**

- **Complexité :** O(n) - Doit parcourir le tableau
- **Retourne** l'index ou -1
- **Sensible à la casse** pour les chaînes

---

### `lastIndexOf()` - Trouver le Dernier Index

La méthode `lastIndexOf()` retourne l'**index de la dernière occurrence** d'un élément.

```javascript
let nombres = [1, 2, 3, 2, 1];

console.log(nombres.lastIndexOf(2)); // 3 (dernière occurrence)
console.log(nombres.lastIndexOf(1)); // 4
console.log(nombres.lastIndexOf(5)); // -1 (non trouvé)

// Recherche en arrière à partir d'un index
console.log(nombres.lastIndexOf(2, 2)); // 1 (cherche en arrière depuis l'index 2)
```

**Caractéristiques :**

- **Complexité :** O(n) - Parcourt le tableau en sens inverse
- **Retourne** l'index ou -1

---

### `includes()` - Vérifier la Présence

La méthode `includes()` vérifie si un élément existe dans le tableau et retourne **true** ou **false**.

```javascript
let animaux = ["Chat", "Chien", "Oiseau"];

console.log(animaux.includes("Chat")); // true
console.log(animaux.includes("Poisson")); // false

// Recherche à partir d'un index
console.log(animaux.includes("Chat", 1)); // false (cherche à partir de l'index 1)
```

**Différence clé avec `indexOf()` :**

```javascript
let valeurs = [1, 2, NaN, 4];

// indexOf() ne peut pas trouver NaN
console.log(valeurs.indexOf(NaN)); // -1

// includes() peut trouver NaN
console.log(valeurs.includes(NaN)); // true
```

**Caractéristiques :**

- **Complexité :** O(n) - Parcourt le tableau
- **Retourne** un booléen (true/false)
- **Peut détecter NaN** contrairement à indexOf()

**Quand utiliser quoi ?**

```javascript
// Pour vérifier la présence : includes() est plus lisible
if (animaux.includes("Chat")) {
  console.log("Il y a un chat !");
}

// Pour obtenir la position : indexOf()
let position = animaux.indexOf("Chien");
if (position !== -1) {
  console.log(`Le chien est à la position ${position}`);
}
```

---

## 🔄 Parcourir des Tableaux

Parcourir un tableau signifie visiter chaque élément pour effectuer une opération.

---

### Boucle `for` Classique

La boucle `for` traditionnelle offre un contrôle total.

```javascript
let produits = ["Moniteur", "Souris", "Clavier"];

for (let i = 0; i < produits.length; i++) {
  console.log(`Produit à l'index ${i}: ${produits[i]}`);
}

// Affichage :
// Produit à l'index 0: Moniteur
// Produit à l'index 1: Souris
// Produit à l'index 2: Clavier

// Parcours en arrière
for (let i = produits.length - 1; i >= 0; i--) {
  console.log(produits[i]);
}
// Affichage: Clavier, Souris, Moniteur
```

**Avantages :**

- Contrôle total sur l'index
- Peut utiliser `break` et `continue`
- Peut modifier l'index pendant la boucle
- **Complexité :** O(n)

---

### Boucle `for...of`

Syntaxe moderne et élégante pour parcourir les **valeurs** directement.

```javascript
let villes = ["Addis Abeba", "Libreville", "Dakar"];

for (let ville of villes) {
  console.log(`Visite de: ${ville}`);
}

// Affichage :
// Visite de: Addis Abeba
// Visite de: Libreville
// Visite de: Dakar
```

**Avantages :**

- Syntaxe très **lisible**
- Évite les erreurs d'index
- Peut utiliser `break` et `continue`
- **Complexité :** O(n)

**Inconvénient :**

- Pas d'accès direct à l'index (sauf avec `entries()`)

---

### Méthode `forEach()`

Approche fonctionnelle pour exécuter une fonction sur chaque élément.

```javascript
let temperatures = [22, 25, 19, 28];

temperatures.forEach(function (temp, index) {
  console.log(`Température du jour ${index + 1}: ${temp}°C`);
});

// Affichage :
// Température du jour 1: 22°C
// Température du jour 2: 25°C
// Température du jour 3: 19°C
// Température du jour 4: 28°C

// Version arrow function (plus concise)
temperatures.forEach((temp) => console.log(`${temp}°C`));
```

**Avantages :**

- Syntaxe **fonctionnelle** et élégante
- Accès facile à la valeur ET l'index
- **Complexité :** O(n)

**Inconvénients :**

- Ne peut pas utiliser `break` ou `continue`
- Ne peut pas retourner de valeur directement

---

### Comparaison des Méthodes de Parcours

```javascript
let tableau = [10, 20, 30, 40, 50];

// 1. for - Le plus flexible
for (let i = 0; i < tableau.length; i++) {
  // Accès à l'index : i
  // Accès à la valeur : tableau[i]
  // Peut utiliser break, continue
}

// 2. for...of - Syntaxe moderne et claire
for (let valeur of tableau) {
  // Accès direct à la valeur
  // Peut utiliser break, continue
  // Pas d'index (sauf avec .entries())
}

// 3. forEach - Approche fonctionnelle
tableau.forEach((valeur, index) => {
  // Accès à la valeur ET l'index
  // Ne peut PAS utiliser break, continue
  // Style déclaratif
});
```

**Recommandations :**

- **Performance critique** : `for` classique
- **Lisibilité** : `for...of` ou `forEach()`
- **Besoin de l'index** : `for` ou `forEach()`
- **Besoin de break** : `for` ou `for...of`

---

## 📝 Micro-Exercice #4 : Parcourir et Calculer

**Objectif :** Maîtriser le parcours de tableaux

**Instructions :**

Soit le tableau suivant :

```javascript
let donnees = [10, 20, 30, 40, 50];
```

1. Utilisez une boucle `for` pour calculer la somme de tous les éléments
2. Utilisez `for...of` pour afficher chaque valeur multipliée par 2
3. Utilisez `forEach()` pour trouver le plus grand élément

<details>
<summary>💡 Voir la solution</summary>

```javascript
let donnees = [10, 20, 30, 40, 50];

// 1. Calculer la somme avec for
let somme = 0;
for (let i = 0; i < donnees.length; i++) {
  somme += donnees[i];
}
console.log("Somme totale:", somme); // 150

// 2. Afficher chaque valeur × 2 avec for...of
console.log("Valeurs multipliées par 2:");
for (let valeur of donnees) {
  console.log(valeur * 2);
}
// Affiche: 20, 40, 60, 80, 100

// 3. Trouver le maximum avec forEach()
let maximum = donnees[0]; // Initialiser avec le premier élément
donnees.forEach((valeur) => {
  if (valeur > maximum) {
    maximum = valeur;
  }
});
console.log("Valeur maximale:", maximum); // 50
```

**Explication :**

- La boucle `for` est idéale pour des calculs avec accumulation
- `for...of` rend le code très lisible pour des opérations simples
- `forEach()` est parfait pour des transformations ou recherches
- Toutes ces approches ont une complexité O(n)

</details>

---

## 💻 Application Pratique : Gestionnaire de Tâches Simple

Mettons en pratique nos connaissances avec une application concrète : un gestionnaire de tâches basique.

---

### Contexte

Nous allons créer un système simple pour gérer une liste de tâches. Cette application permettra d'ajouter des tâches, de les retirer, et de les afficher.

```javascript
// Initialiser notre liste de tâches
let listeTaches = [];

// Fonction pour ajouter une tâche
function ajouterTache(description) {
  listeTaches.push(description);
  console.log(`Tâche ajoutée: "${description}"`);
  console.log(`Total: ${listeTaches.length} tâche(s)`);
}

// Fonction pour retirer la dernière tâche
function retirerDerniereTache() {
  if (listeTaches.length > 0) {
    let tacheRetiree = listeTaches.pop();
    console.log(`Tâche retirée: "${tacheRetiree}"`);
    console.log(`Total: ${listeTaches.length} tâche(s)`);
  } else {
    console.log("Aucune tâche à retirer.");
  }
}

// Fonction pour afficher toutes les tâches
function afficherTaches() {
  if (listeTaches.length === 0) {
    console.log("Aucune tâche dans la liste.");
    return;
  }

  console.log("Liste des tâches :");
  listeTaches.forEach((tache, index) => {
    console.log(`  ${index + 1}. ${tache}`);
  });
  console.log(`Total: ${listeTaches.length} tâche(s)`);
}

// Fonction pour vérifier si une tâche existe
function tacheExiste(description) {
  return listeTaches.includes(description);
}

// Démonstration d'utilisation
console.log("=== GESTIONNAIRE DE TÂCHES ===\n");

ajouterTache("Finir le module 2 leçon 1");
ajouterTache("Réviser les concepts du module 1");
ajouterTache("Planifier les devoirs de la semaine");

console.log("\n--- État actuel ---");
afficherTaches();

console.log("\n--- Retirer une tâche ---");
retirerDerniereTache();

console.log("\n--- État après retrait ---");
afficherTaches();

console.log("\n--- Vérification ---");
console.log(
  "La tâche 'Réviser...' existe ?",
  tacheExiste("Réviser les concepts du module 1"),
); // true
console.log(
  "La tâche 'Faire du sport' existe ?",
  tacheExiste("Faire du sport"),
); // false
```

**Analyse de l'implémentation :**

| Opération           | Méthode utilisée | Complexité | Raison                      |
| ------------------- | ---------------- | ---------- | --------------------------- |
| Ajouter une tâche   | `push()`         | O(1)       | Ajout à la fin, rapide      |
| Retirer une tâche   | `pop()`          | O(1)       | Retrait de la fin, rapide   |
| Afficher les tâches | `forEach()`      | O(n)       | Parcours complet nécessaire |
| Vérifier existence  | `includes()`     | O(n)       | Recherche linéaire          |

**Points clés :**

- Utilisation de `push()` et `pop()` pour des opérations efficaces
- `forEach()` pour un parcours clair et lisible
- `includes()` pour des vérifications simples
- Gestion des cas limites (tableau vide)

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension des tableaux, implémentez les problèmes suivants.

---

### Exercice 1 : Gestionnaire de Liste de Courses

**Objectif :** Manipuler un tableau avec les opérations de base

**Instructions :**

1. Créez un tableau vide `listeCourses`
2. Ajoutez "Lait", "Pain", "Œufs" à la liste avec `push()`
3. Ajoutez "Fromage" au début avec `unshift()`
4. Retirez le dernier élément avec `pop()` et affichez-le
5. Affichez la liste finale et sa longueur

**Exemple :**

```javascript
// Votre code ici
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
// 1. Créer un tableau vide
let listeCourses = [];
console.log("Liste initiale:", listeCourses); // []

// 2. Ajouter des éléments à la fin
listeCourses.push("Lait");
listeCourses.push("Pain");
listeCourses.push("Œufs");
console.log("Après ajouts:", listeCourses);
// ["Lait", "Pain", "Œufs"]

// 3. Ajouter au début
listeCourses.unshift("Fromage");
console.log("Après unshift:", listeCourses);
// ["Fromage", "Lait", "Pain", "Œufs"]

// 4. Retirer le dernier et l'afficher
let dernierElement = listeCourses.pop();
console.log("Élément retiré:", dernierElement); // "Œufs"

// 5. Afficher le résultat final
console.log("Liste finale:", listeCourses);
// ["Fromage", "Lait", "Pain"]
console.log("Longueur finale:", listeCourses.length); // 3
```

**Explication de la solution :**

- `push()` ajoute efficacement à la fin (O(1))
- `unshift()` ajoute au début mais est plus lent (O(n))
- `pop()` retire et retourne le dernier élément (O(1))
- La liste finale contient 3 éléments après toutes les opérations

</details>

---

### Exercice 2 : Créateur de Playlist

**Objectif :** Rechercher et vérifier des éléments

**Instructions :**

Créez une playlist musicale et effectuez les opérations suivantes :

1. Créez un tableau `maPlaylist` avec trois titres : `['Chanson A', 'Chanson B', 'Chanson C']`
2. Ajoutez "Chanson D" à la fin
3. Retirez la première chanson de la playlist
4. Vérifiez si "Chanson B" est toujours dans la playlist avec `includes()`
5. Trouvez l'index de "Chanson D"
6. Affichez la playlist finale

<details>
<summary>💡 Voir la solution</summary>

```javascript
// 1. Créer la playlist initiale
let maPlaylist = ["Chanson A", "Chanson B", "Chanson C"];
console.log("Playlist initiale:", maPlaylist);

// 2. Ajouter à la fin
maPlaylist.push("Chanson D");
console.log("Après ajout de Chanson D:", maPlaylist);
// ["Chanson A", "Chanson B", "Chanson C", "Chanson D"]

// 3. Retirer la première chanson
let premiereRetiree = maPlaylist.shift();
console.log("Chanson retirée:", premiereRetiree); // "Chanson A"
console.log("Après shift:", maPlaylist);
// ["Chanson B", "Chanson C", "Chanson D"]

// 4. Vérifier la présence de Chanson B
let chansonBPresente = maPlaylist.includes("Chanson B");
console.log("Chanson B est présente ?", chansonBPresente); // true

// 5. Trouver l'index de Chanson D
let indexChansonD = maPlaylist.indexOf("Chanson D");
console.log("Index de Chanson D:", indexChansonD); // 2

// 6. Afficher la playlist finale
console.log("Playlist finale:", maPlaylist);
// ["Chanson B", "Chanson C", "Chanson D"]
console.log("Nombre de chansons:", maPlaylist.length); // 3
```

**Explication de la solution :**

- `shift()` retire le premier élément, mais nécessite O(n) pour réindexer
- `includes()` vérifie efficacement la présence d'un élément
- `indexOf()` retourne la position d'un élément (ou -1 si absent)
- La playlist contient 3 chansons après toutes les modifications

</details>

---

### Exercice 3 : Itération en Sens Inverse

**Objectif :** Parcourir un tableau en sens inverse

**Instructions :**

Soit le tableau `donnees = [10, 20, 30, 40, 50]`.

Utilisez une boucle `for` pour afficher chaque élément en ordre inverse (de 50 à 10), avec leur index.

<details>
<summary>💡 Voir la solution</summary>

```javascript
let donnees = [10, 20, 30, 40, 50];

console.log("Affichage en ordre inverse:");
for (let i = donnees.length - 1; i >= 0; i--) {
  console.log(`Index ${i}: ${donnees[i]}`);
}

// Affichage :
// Index 4: 50
// Index 3: 40
// Index 2: 30
// Index 1: 20
// Index 0: 10
```

**Explication de la solution :**

- On initialise `i` avec `donnees.length - 1` (dernier index)
- La condition `i >= 0` assure qu'on s'arrête au premier élément
- Le décrement `i--` fait reculer dans le tableau
- Complexité : O(n) - on visite chaque élément une fois

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quel est l'index du premier élément d'un tableau en JavaScript ?**

- [ ] A. 1
- [ ] B. 0
- [ ] C. -1
- [ ] D. Dépend de la longueur du tableau

<details>
<summary>Voir la réponse</summary>

**Réponse : B. 0**

En JavaScript (et dans la plupart des langages de programmation), l'indexation des tableaux commence à **zéro**. Le premier élément est donc à l'index 0, le deuxième à l'index 1, etc.

</details>

---

### Question 2

**Quelle est la complexité temporelle de l'opération `push()` sur un tableau JavaScript ?**

- [ ] A. O(n)
- [ ] B. O(log n)
- [ ] C. O(1)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C. O(1)**

L'opération `push()` ajoute un élément à la **fin** du tableau en **temps constant** O(1). JavaScript maintient une référence à la fin du tableau, donc l'ajout ne nécessite pas de parcourir ou de décaler les éléments existants.

</details>

---

### Question 3

**Que retourne le code suivant ?**

```javascript
let arr = [10, 20, 30];
arr[5] = 60;
console.log(arr.length);
```

- [ ] A. 3
- [ ] B. 4
- [ ] C. 5
- [ ] D. 6

<details>
<summary>Voir la réponse</summary>

**Réponse : D. 6**

Lorsque vous assignez une valeur à un index qui dépasse la longueur actuelle du tableau, JavaScript **agrandit automatiquement** le tableau. La propriété `length` reflète toujours l'index le plus élevé + 1.

</details>

---

### Question 4

**Parmi les opérations suivantes, lesquelles ont une complexité O(n) ? (Plusieurs réponses possibles)**

- [ ] A. `push()`
- [ ] B. `shift()`
- [ ] C. `pop()`
- [ ] D. `unshift()`
- [ ] E. `indexOf()`

<details>
<summary>Voir la réponse</summary>

**Réponses : B, D, E**

- `shift()` : O(n) - retire au début, doit décaler tous les éléments restants
- `unshift()` : O(n) - ajout au début, doit décaler tous les éléments existants
- `indexOf()` : O(n) - recherche linéaire, doit parcourir le tableau

En revanche, `push()` et `pop()` sont O(1) car ils opèrent à la fin du tableau.

</details>

---

### Question 5

**Quel est le résultat du code suivant ?**

```javascript
let a = [1, 2, 3];
let b = a;
b.push(4);
console.log(a.length);
```

- [ ] A. 3
- [ ] B. 4
- [ ] C. undefined
- [ ] D. Erreur

<details>
<summary>Voir la réponse</summary>

**Réponse : B. 4**

En JavaScript, les tableaux sont des **objets** et sont passés **par référence**. Lorsque vous écrivez `let b = a`, vous ne créez pas une copie du tableau, mais une **nouvelle référence** vers le même tableau en mémoire. Modifier `b` modifie aussi `a`.

</details>

---

## 📌 Récapitulatif en 8 Points Clés

### 1. Tableaux Dynamiques

Les tableaux JavaScript sont **dynamiques** : leur taille s'ajuste automatiquement sans gestion manuelle de la mémoire.

### 2. Indexation par Zéro

Le premier élément d'un tableau est à l'**index 0**, le dernier à l'index `length - 1`.

### 3. Opérations Rapides à la Fin

`push()` et `pop()` opèrent en **temps constant O(1)** - préférez-les pour de meilleures performances.

### 4. Opérations Lentes au Début

`unshift()` et `shift()` opèrent en **temps linéaire O(n)** - évitez-les pour les grands tableaux.

### 5. Accès Direct par Index

L'accès et la modification par index (`arr[i]`) sont en **O(1)** - instantanés.

### 6. Recherche Linéaire

`indexOf()`, `lastIndexOf()` et `includes()` ont une complexité **O(n)**.

### 7. Parcours avec Itération

Trois approches : boucle `for`, `for...of`, `forEach()` - toutes en **O(n)**.

### 8. Passage par Référence

Les tableaux sont passés **par référence** : utilisez le spread operator `[...arr]` pour créer de vraies copies.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez terminé la première leçon sur les tableaux !

### Ce que vous avez appris aujourd'hui

- **Création et initialisation** de tableaux
- **Accès et modification** d'éléments par index
- **Opérations de base** et leur complexité
- **Recherche d'éléments**
- **Parcours de tableaux**
- **Nature dynamique** des tableaux JavaScript

### Compétences acquises

Vous êtes maintenant capable de :

- Choisir la méthode d'ajout/retrait appropriée
- Analyser la complexité temporelle des opérations
- Manipuler efficacement des collections de données

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Les tableaux sont la **fondation** de nombreuses structures de données plus avancées. Maîtriser leurs opérations et comprendre leur performance est crucial pour devenir un développeur efficace.

---

## ➡️ Prochaine Étape : Leçon 8

### Ce qui vous attend

La prochaine leçon, **« Listes Chaînées : Concepts, Types et Parcours »**, vous introduira à une structure de données alternative aux tableaux.

**Vous découvrirez :**

- **Structure des listes chaînées** et leurs avantages
- **Comparaison** avec les tableaux
- **Types de listes** : simples, doubles, circulaires

### Préparez-vous !

Les listes chaînées excellent dans des situations où les tableaux montrent leurs limites : insertions et suppressions fréquentes au milieu de la collection !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [MDN - Array](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array) - Documentation officielle
- [JavaScript.info - Arrays](https://javascript.info/array) - Tutoriel interactif
- [Visualgo - Array](https://visualgo.net/en/array) - Visualisation interactive

### Outils de pratique

- **[Replit](https://replit.com/)** : Environnement en ligne
- **[LeetCode](https://leetcode.com/tag/array/)** : Problèmes d'algorithmes

---

## 💬 Feedback et Questions

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Les tableaux sont partout en JavaScript ! Entraînez-vous en créant de petits projets : gestionnaire de contacts, calculatrice de statistiques, jeu de devinette, etc.

---

**Prêt pour la Leçon 8 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir les listes chaînées !

---

<div align="center">

**Leçon 7 sur 42 - Module 2 : Structures de Données Essentielles en JavaScript**

[⬅️ Leçon 6 : Mise en Place d'une Étude de Cas - Optimisation d'un Gestionnaire de Tâches](../module-1/lecon-6-etude-cas-gestionnaire-taches.md) | [Retour au sommaire](./README.md) | [Leçon 8 : Listes Chaînées - Concepts, Types et Parcours ➡️](./lecon-2-listes-chainees-concepts-types-parcours.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
