##### Leçon 2 sur 42

# Introduction à JavaScript pour le Développement d'Algorithmes

**Module 1** : Fondements des algorithmes et révision de JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Déclarer et utiliser des variables avec `let` et `const` de manière appropriée
- Identifier et manipuler les types de données fondamentaux en JavaScript
- Implémenter la logique conditionnelle avec `if/else` et `switch`
- Utiliser les boucles `for` et `while` pour des opérations répétitives
- Créer et utiliser des fonctions (déclarations, expressions, arrow functions)
- Manipuler des tableaux et objets pour stocker et traiter des données

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- Avoir complété la Leçon 1
- Avoir un environnement JavaScript (Node.js ou navigateur)

---

## 🚀 Introduction : JavaScript, notre outil pour concrétiser les algorithmes

Maintenant que nous avons établi ce qu'est un **algorithme** – une séquence précise d'étapes conçue pour résoudre un problème – notre prochaine étape cruciale est de nous équiper de l'**outil principal** que nous utiliserons pour implémenter ces algorithmes : **JavaScript**.

### Pourquoi JavaScript ?

JavaScript possède plusieurs avantages qui en font un excellent langage pour comprendre, construire et analyser des algorithmes :

- **Polyvalence** : Fonctionne sur le web, les serveurs (Node.js), les applications mobiles et desktop
- **Facilité d'apprentissage** : Syntaxe claire et accessible aux débutants
- **Écosystème riche** : Vaste collection de bibliothèques et outils
- **Disponibilité immédiate** : Présent dans tous les navigateurs web modernes
- **Interactivité** : Résultats instantanés dans la console du navigateur

### Objectif de cette leçon

Cette leçon servira de **révision ciblée** des concepts fondamentaux de JavaScript indispensables au développement d'algorithmes. Nous nous concentrerons sur les **briques essentielles** :

1. **Variables et types de données** : Pour gérer l'information
2. **Structures de contrôle** : Pour diriger le flux d'exécution
3. **Fonctions** : Pour organiser la logique
4. **Tableaux et objets** : Pour manipuler des collections de données

> **Point Clé**
>
> Maîtriser ces fondamentaux JavaScript est **essentiel** pour traduire vos algorithmes conceptuels en code exécutable et efficace.

---

## 📦 Variables et Types de Données : Les Fondations

Au cœur de tout algorithme se trouve la **manipulation de données**. En JavaScript, les variables sont des **noms symboliques** qui contiennent des valeurs, et les types de données classifient le **type de valeur** qu'une variable peut stocker.

---

### Déclarer des Variables : `let` et `const`

JavaScript moderne propose deux mots-clés principaux pour déclarer des variables : `let` et `const`. Les utiliser (plutôt que l'ancien `var`) est considéré comme une **bonne pratique** en raison de leur comportement de **portée de bloc** (_block-scoping_), ce qui aide à prévenir les erreurs courantes.

---

#### `let` : Pour les valeurs qui changent

Déclare une variable **locale à portée de bloc**, pouvant être initialisée et **réassignée** plus tard. Idéale pour les valeurs qui évoluent pendant l'exécution d'un algorithme (compteurs, résultats intermédiaires).

```javascript
// Exemple avec 'let'
let compteur = 0; // Déclare 'compteur' et l'initialise à 0
console.log(compteur); // Affiche : 0

compteur = 10; // 'compteur' peut être réassigné
console.log(compteur); // Affiche : 10

let message = "Bonjour";
if (true) {
  let message = "Monde"; // Ce 'message' est local au bloc 'if'
  console.log(message); // Affiche : Monde
}
console.log(message); // Affiche : Bonjour (le 'message' extérieur est inchangé)
```

**Caractéristiques de `let` :**

- Portée de bloc (entre `{ }`)
- Peut être réassigné
- Doit être déclaré avant utilisation (pas de hoisting accessible)

---

#### `const` : Pour les valeurs constantes

Déclare une variable **locale à portée de bloc** qui **doit être initialisée** lors de sa déclaration. Une fois assignée, sa valeur **ne peut pas être réassignée**. Idéale pour les valeurs qui doivent rester constantes, améliorant la lisibilité et prévenant les modifications accidentelles.

```javascript
// Exemple avec 'const'
const MAX_ITEMS = 100; // Déclare une constante
console.log(MAX_ITEMS); // Affiche : 100

// MAX_ITEMS = 200; // ERREUR : TypeError: Assignment to constant variable.

const nomAlgorithme = "Recherche Binaire";
console.log(nomAlgorithme); // Affiche : Recherche Binaire
```

**Note importante pour les objets et tableaux :**

Avec `const`, la **variable** ne peut pas être réassignée à un nouvel objet/tableau, mais le **contenu** de l'objet/tableau peut être modifié.

```javascript
const monTableau = [1, 2, 3];
monTableau.push(4); // Autorisé : modification du contenu
console.log(monTableau); // Affiche : [1, 2, 3, 4]

// monTableau = [5, 6]; // ERREUR : TypeError: Assignment to constant variable.
```

**Règle simple :**

- Utilisez `const` **par défaut**
- Utilisez `let` **uniquement si vous devez réassigner** la variable

---

## 📊 Types de Données Essentiels

JavaScript offre plusieurs types de données intégrés pour représenter différents types d'informations. Pour le développement d'algorithmes, comprendre `number`, `string`, `boolean`, `null` et `undefined` est fondamental.

---

### 1. `number` : Nombres

Représente les nombres **entiers** et à **virgule flottante**. JavaScript ne fait pas de distinction entre eux, traitant tous les nombres comme des valeurs flottantes à double précision sur 64 bits.

**Utilisation :** Calculs, indexation, comptage

```javascript
let valeurEntiere = 10; // Un entier
let valeurFlottante = 3.14159; // Un nombre à virgule flottante
let valeurNegative = -5; // Nombre négatif

let somme = valeurEntiere + valeurFlottante; // Opérations arithmétiques
console.log(somme); // Affiche : 13.14159

let produit = 5 * 2;
let quotient = 10 / 3; // La division peut résulter en un nombre flottant
let reste = 10 % 3; // Opérateur modulo, utile pour tester pair/impair

console.log(`Produit: ${produit}, Quotient: ${quotient}, Reste: ${reste}`);
// Affiche : Produit: 10, Quotient: 3.3333333333333335, Reste: 1
```

**Opérateurs arithmétiques principaux :**

| Opérateur | Description    | Exemple  | Résultat |
| --------- | -------------- | -------- | -------- |
| `+`       | Addition       | `5 + 3`  | `8`      |
| `-`       | Soustraction   | `5 - 3`  | `2`      |
| `*`       | Multiplication | `5 * 3`  | `15`     |
| `/`       | Division       | `10 / 4` | `2.5`    |
| `%`       | Modulo (reste) | `10 % 3` | `1`      |
| `**`      | Exponentiation | `2 ** 3` | `8`      |

---

### 2. `string` : Chaînes de caractères

Représente des **données textuelles**. Les chaînes sont des séquences de caractères et sont **immuables** (leur contenu ne peut pas être modifié après création, mais vous pouvez créer de nouvelles chaînes basées sur les existantes).

**Utilisation :** Traitement de texte, recherche de motifs, formatage de sortie

```javascript
let guillemetsSimples = "Bonjour";
let guillemetsDoubles = "Monde";
let templateLiteral = `Bienvenue, ${guillemetsSimples} ${guillemetsDoubles}!`; // Template literal

console.log(templateLiteral); // Affiche : Bienvenue, Bonjour Monde!
console.log(templateLiteral.length); // Affiche : 28 (nombre de caractères)

let premierCaractere = templateLiteral[0]; // Accès à un caractère par index (commence à 0)
console.log(premierCaractere); // Affiche : B

let sousChaine = templateLiteral.slice(12, 19); // Extraction d'une partie de la chaîne
console.log(sousChaine); // Affiche : Bonjour
```

**Méthodes de chaînes courantes :**

| Méthode                 | Description                          | Exemple                                 |
| ----------------------- | ------------------------------------ | --------------------------------------- |
| `.length`               | Longueur de la chaîne                | `"Bonjour".length` → `7`                |
| `.toUpperCase()`        | Convertir en majuscules              | `"bonjour".toUpperCase()` → `"BONJOUR"` |
| `.toLowerCase()`        | Convertir en minuscules              | `"BONJOUR".toLowerCase()` → `"bonjour"` |
| `.slice(debut, fin)`    | Extraire une sous-chaîne             | `"Bonjour".slice(3, 7)` → `"jour"`      |
| `.includes(sousChaine)` | Vérifier si contient une sous-chaîne | `"Bonjour".includes("jour")` → `true`   |
| `.split(separateur)`    | Diviser en tableau                   | `"a,b,c".split(",")` → `["a","b","c"]`  |

**Template Literals (Littéraux de gabarit) :**

Utilisez les backticks (`` ` ``) pour :

- Interpoler des variables avec `${variable}`
- Créer des chaînes multi-lignes facilement

```javascript
const nom = "Chermann";
const age = 43;
const presentation = `Je m'appelle ${nom} et j'ai ${age} ans.`;
console.log(presentation); // Affiche : Je m'appelle Chermann et j'ai 43 ans.
```

---

### 3. `boolean` : Valeurs logiques

Représente une entité **logique** et peut avoir l'une de ces deux valeurs : `true` (vrai) ou `false` (faux).

**Utilisation :** Logique conditionnelle, contrôle de flux, prise de décision

```javascript
let algorithmeTermine = false;
let donneesDisponibles = true;

if (donneesDisponibles && !algorithmeTermine) {
  // Utilisation d'opérateurs logiques
  console.log("Traitement des données...");
  algorithmeTermine = true; // Mise à jour de la valeur booléenne
}

if (algorithmeTermine) {
  console.log("Algorithme terminé.");
}
```

**Opérateurs logiques :**

| Opérateur | Description | Exemple           | Résultat |
| --------- | ----------- | ----------------- | -------- |
| `&&`      | ET logique  | `true && false`   | `false`  |
| `\|\|`    | OU logique  | `true \|\| false` | `true`   |
| `!`       | NON logique | `!true`           | `false`  |

**Opérateurs de comparaison :**

| Opérateur | Description               | Exemple    | Résultat |
| --------- | ------------------------- | ---------- | -------- |
| `===`     | Égalité stricte           | `5 === 5`  | `true`   |
| `!==`     | Inégalité stricte         | `5 !== 3`  | `true`   |
| `>`       | Supérieur à               | `10 > 5`   | `true`   |
| `<`       | Inférieur à               | `3 < 5`    | `true`   |
| `>=`      | Supérieur ou égal à       | `5 >= 5`   | `true`   |
| `<=`      | Inférieur ou égal à       | `3 <= 5`   | `true`   |
| `==`      | Égalité avec conversion   | `5 == "5"` | `true`   |
| `!=`      | Inégalité avec conversion | `5 != "3"` | `true`   |

**Recommandation :** Utilisez toujours `===` et `!==` (égalité stricte) plutôt que `==` et `!=` pour éviter les conversions de types implicites inattendues.

---

### 4. `null` et `undefined` : Absence de valeur

Ces deux types représentent l'**absence de valeur**, mais avec des nuances différentes.

#### `undefined`

Une variable qui a été **déclarée mais pas encore assignée** est `undefined`. Signifie également l'absence d'une propriété d'objet ou d'un paramètre de fonction.

#### `null`

Une **absence intentionnelle** de toute valeur d'objet. C'est une valeur primitive utilisée pour indiquer qu'une variable ne pointe vers aucun objet.

```javascript
let variableNonAssignee;
console.log(variableNonAssignee); // Affiche : undefined

let donnees = null; // Définir explicitement les données à null
console.log(donnees); // Affiche : null

if (variableNonAssignee === undefined) {
  console.log("La variable est undefined.");
}

if (donnees === null) {
  console.log("Les données sont explicitement null.");
}

// Souvent, vous pouvez vérifier les deux :
let donneesManquantes = null; // Ou undefined
if (donneesManquantes == null) {
  // L'opérateur == considère null et undefined comme égaux
  console.log("Les données sont soit null soit undefined.");
}
```

**Différences clés :**

| Aspect            | `undefined`                        | `null`                         |
| ----------------- | ---------------------------------- | ------------------------------ |
| **Type**          | `undefined`                        | `object` (anomalie historique) |
| **Signification** | Non initialisé, absence par défaut | Absence intentionnelle         |
| **Utilisation**   | Automatique par JavaScript         | Assignation manuelle explicite |

---

## 📝 Micro-Exercice #1 : Types de Données

**Instructions :** Pour chaque déclaration, indiquez le type de données et si `let` ou `const` est approprié.

```javascript
// 1.
const PI = 3.14159;

// 2.
let compteur = 0;

// 3.
let utilisateurConnecte = true;

// 4.
const MESSAGE_BIENVENUE = "Bonjour!";

// 5.
let resultat;
```

<details>
<summary>💡 Voir les réponses</summary>

1. **Type :** `number`, **Mot-clé :** `const` ✅ (valeur mathématique constante)
2. **Type :** `number`, **Mot-clé :** `let` ✅ (compteur qui va changer)
3. **Type :** `boolean`, **Mot-clé :** `let` ✅ (statut qui peut changer)
4. **Type :** `string`, **Mot-clé :** `const` ✅ (message qui ne change pas)
5. **Type :** `undefined`, **Mot-clé :** `let` ✅ (sera assigné plus tard)

</details>

## 🔀 Maîtriser le Flux de Contrôle : Diriger le Chemin de Votre Algorithme

Les algorithmes sont rarement linéaires ; ils impliquent des **décisions** et des **répétitions**. Les instructions de contrôle de flux vous permettent de dicter l'**ordre d'exécution** des instructions, permettant à vos algorithmes de répondre dynamiquement à différentes entrées et conditions.

---

### Instructions Conditionnelles : `if/else` et `switch`

Les instructions conditionnelles permettent à votre algorithme d'exécuter différents blocs de code en fonction de l'**évaluation d'une condition** (`true` ou `false`).

---

#### `if` / `else if` / `else`

C'est la manière la plus courante de gérer la logique conditionnelle.

**Structure :**

```javascript
if (condition1) {
  // Code exécuté si condition1 est vraie
} else if (condition2) {
  // Code exécuté si condition1 est fausse ET condition2 est vraie
} else {
  // Code exécuté si toutes les conditions précédentes sont fausses
}
```

**Exemple 1 : Déterminer si un nombre est positif, négatif ou zéro**

```javascript
function verifierNombre(num) {
  if (num > 0) {
    console.log(`${num} est positif.`);
  } else if (num < 0) {
    console.log(`${num} est négatif.`);
  } else {
    console.log(`${num} est zéro.`);
  }
}

verifierNombre(5); // Affiche : 5 est positif.
verifierNombre(-3); // Affiche : -3 est négatif.
verifierNombre(0); // Affiche : 0 est zéro.
```

**Exemple 2 : Vérifier les limites d'un tableau avant d'accéder à un élément**

```javascript
const monTableau = [10, 20, 30];
const index = 1;

if (index >= 0 && index < monTableau.length) {
  console.log(`Élément à l'index ${index}: ${monTableau[index]}`);
} else {
  console.log(`L'index ${index} est hors limites pour le tableau.`);
}
// Affiche : Élément à l'index 1: 20
```

---

#### `switch` : Pour les choix multiples

Utile lorsque vous avez **plusieurs chemins d'exécution possibles** basés sur la valeur d'une **seule variable**. Plus structuré qu'une longue chaîne de `else if` pour des valeurs discrètes spécifiques.

**Structure :**

```javascript
switch (expression) {
  case valeur1:
    // Code si expression === valeur1
    break;
  case valeur2:
    // Code si expression === valeur2
    break;
  default:
  // Code si aucune valeur ne correspond
}
```

**Important :** Chaque bloc `case` nécessite un `break` pour éviter le "fall-through" (passage au case suivant).

**Exemple : Assigner un jour de la semaine basé sur un numéro**

```javascript
function obtenirNomJour(numeroJour) {
  let nomJour;
  switch (numeroJour) {
    case 1:
      nomJour = "Lundi";
      break;
    case 2:
      nomJour = "Mardi";
      break;
    case 3:
      nomJour = "Mercredi";
      break;
    case 4:
      nomJour = "Jeudi";
      break;
    case 5:
      nomJour = "Vendredi";
      break;
    case 6:
    case 7: // Plusieurs cases peuvent partager le même bloc
      nomJour = "Week-end";
      break;
    default:
      nomJour = "Numéro de jour invalide";
  }
  console.log(`Jour ${numeroJour}: ${nomJour}`);
}

obtenirNomJour(3); // Affiche : Jour 3: Mercredi
obtenirNomJour(6); // Affiche : Jour 6: Week-end
obtenirNomJour(9); // Affiche : Jour 9: Numéro de jour invalide
```

---

### Constructions de Boucles : `for` et `while`

Les boucles sont **essentielles** pour les algorithmes impliquant des tâches répétitives : itérer sur des collections de données, effectuer des opérations un nombre spécifique de fois, ou continuer un processus jusqu'à ce qu'une condition soit remplie.

---

#### Boucle `for` : Nombre d'itérations connu

La boucle `for` est généralement utilisée lorsque vous connaissez (ou pouvez facilement déterminer) le **nombre d'itérations** requis.

**Structure :**

```javascript
for (initialisation; condition; incrémentation) {
  // Code exécuté à chaque itération
}
```

**Composants :**

1. **Initialisation** : Exécutée une seule fois au début
2. **Condition** : Vérifiée avant chaque itération
3. **Incrémentation** : Exécutée après chaque itération

**Exemple 1 : Compter de 1 à 5**

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(`Compte : ${i}`);
}
// Affiche :
// Compte : 1
// Compte : 2
// Compte : 3
// Compte : 4
// Compte : 5
```

**Exemple 2 : Itérer sur un tableau (courant dans les algorithmes)**

```javascript
const fruits = ["pomme", "banane", "cerise"];

for (let i = 0; i < fruits.length; i++) {
  console.log(`Fruit à l'index ${i}: ${fruits[i]}`);
}
// Affiche :
// Fruit à l'index 0: pomme
// Fruit à l'index 1: banane
// Fruit à l'index 2: cerise
```

**Exemple 3 : Sommer les nombres de 1 à 10**

```javascript
let sommeTotale = 0;

for (let i = 1; i <= 10; i++) {
  sommeTotale += i; // Équivalent à : sommeTotale = sommeTotale + i;
}

console.log(`Somme de 1 à 10 : ${sommeTotale}`);
// Affiche : Somme de 1 à 10 : 55
```

---

#### Boucle `while` : Nombre d'itérations inconnu

La boucle `while` exécute un bloc de code de manière répétée **tant qu'une condition spécifiée reste vraie**. Idéale lorsque le nombre d'itérations n'est pas connu à l'avance.

**Structure :**

```javascript
while (condition) {
  // Code exécuté tant que condition est vraie
}
```

**Important :** Assurez-vous que la condition finisse par devenir `false` pour éviter une **boucle infinie**.

**Exemple 1 : Doubler un nombre jusqu'à ce qu'il soit supérieur à 100**

```javascript
let num = 5;

while (num <= 100) {
  console.log(`Nombre actuel : ${num}`);
  num *= 2; // Double le nombre. Équivalent à : num = num * 2;
}

console.log(`Nombre final : ${num}`);
// Affiche :
// Nombre actuel : 5
// Nombre actuel : 10
// Nombre actuel : 20
// Nombre actuel : 40
// Nombre actuel : 80
// Nombre final : 160
```

**Exemple 2 : Trouver le premier nombre pair dans une séquence aléatoire**

```javascript
let nombrePairTrouve = false;
let tentatives = 0;

while (!nombrePairTrouve && tentatives < 10) {
  let nombreAleatoire = Math.floor(Math.random() * 100) + 1; // Nombre entre 1 et 100
  console.log(`Tentative ${tentatives + 1}: Généré ${nombreAleatoire}`);

  if (nombreAleatoire % 2 === 0) {
    console.log(`Trouvé un nombre pair : ${nombreAleatoire}`);
    nombrePairTrouve = true; // Ceci termine la boucle
  }
  tentatives++;
}

if (!nombrePairTrouve) {
  console.log("Impossible de trouver un nombre pair en 10 tentatives.");
}
```

---

## 📝 Micro-Exercice #2 : Boucles

**Problème :** Écrivez une boucle `for` qui affiche tous les nombres **pairs** de 0 à 20 (inclus).

<details>
<summary>💡 Voir la solution</summary>

```javascript
for (let i = 0; i <= 20; i++) {
  if (i % 2 === 0) {
    // Vérifier si le nombre est pair
    console.log(i);
  }
}

// Ou plus efficacement :
for (let i = 0; i <= 20; i += 2) {
  console.log(i);
}
```

</details>

---

## 🔧 Fonctions : Encapsuler la Logique Algorithmique

Les fonctions sont des **blocs de construction fondamentaux** en JavaScript, vous permettant d'**encapsuler** une logique spécifique ou une séquence d'opérations dans une **unité réutilisable**.

**Avantages des fonctions :**

- **Réutilisabilité** : Écrivez une fois, utilisez plusieurs fois
- **Lisibilité** : Code plus clair et organisé
- **Modularité** : Décomposer les problèmes complexes en parties gérables
- **Maintenabilité** : Plus facile à tester et corriger

---

### Définir et Appeler des Fonctions

Il existe plusieurs façons de définir des fonctions en JavaScript. Commençons par la méthode traditionnelle.

---

#### Déclaration de Fonction

Une fonction **nommée** définie avec le mot-clé `function`. Ces fonctions sont **hoisted** (hissées), ce qui signifie qu'elles peuvent être appelées **avant** leur déclaration dans le code.

```javascript
// Déclaration de fonction
function saluer(nom) {
  return `Bonjour, ${nom}!`; // 'return' renvoie une valeur depuis la fonction
}

// Appel de la fonction
let messageBienvenue = saluer("Chermann");
console.log(messageBienvenue); // Affiche : Bonjour, Chermann!
```

**Exemple : Fonction pour une tâche algorithmique courante - élever au carré**

```javascript
function auCarre(nombre) {
  return nombre * nombre;
}

console.log(auCarre(7)); // Affiche : 49
```

**Structure :**

```javascript
function nomFonction(parametre1, parametre2) {
  // Corps de la fonction
  return valeurDeRetour; // Optionnel
}
```

**Note :** Si une fonction ne retourne pas explicitement une valeur, elle retourne implicitement `undefined`.

---

#### Expression de Fonction

Une fonction définie comme partie d'une **expression**, souvent assignée à une variable. Ces fonctions **ne sont pas hoisted** et ne peuvent être appelées qu'**après** leur définition.

```javascript
// Expression de fonction
const additionner = function (a, b) {
  return a + b;
};

let resultatSomme = additionner(10, 5);
console.log(resultatSomme); // Affiche : 15
```

---

### Fonctions Fléchées : Syntaxe Concise

Introduites dans ES6 (ECMAScript 2015), les **fonctions fléchées** (`=>`) offrent une syntaxe plus **concise** pour écrire des expressions de fonction, particulièrement pour les fonctions simples.

**Syntaxe de base :**

```javascript
const nomFonction = (param1, param2) => {
  // Corps de la fonction
  return valeur;
};
```

**Exemple : Fonction fléchée vs fonction traditionnelle**

```javascript
// Fonction classique
const multiplierClassique = function (x, y) {
  return x * y;
};
console.log(multiplierClassique(4, 6)); // Affiche : 24

// Fonction fléchée équivalente
const multiplierFleche = (x, y) => x * y; // Syntaxe concise pour un seul return
console.log(multiplierFleche(4, 6)); // Affiche : 24
```

**Variantes de syntaxe :**

```javascript
// 1. Avec un seul paramètre, les parenthèses sont optionnelles
const doubler = (n) => n * 2;
// Ou :
const doubler2 = (n) => n * 2;

// 2. Sans paramètres, les parenthèses sont obligatoires
const direBonjour = () => console.log("Bonjour!");
direBonjour(); // Affiche : Bonjour!

// 3. Avec plusieurs lignes, utiliser des accolades et 'return'
const calculerAire = (longueur, largeur) => {
  const aire = longueur * largeur;
  console.log(`Calcul de l'aire pour ${longueur}x${largeur}`);
  return aire;
};
console.log(calculerAire(10, 5));
// Affiche :
// Calcul de l'aire pour 10x5
// 50
```

**Quand utiliser les fonctions fléchées ?**

- Pour des opérations courtes et simples
- Comme callbacks dans des méthodes de tableau (`.map()`, `.filter()`, etc.)
- Quand vous voulez une syntaxe concise

---

## 📝 Micro-Exercice #3 : Fonctions

**Problème :** Créez une fonction fléchée nommée `estPair` qui prend un nombre en paramètre et retourne `true` si le nombre est pair, `false` sinon.

<details>
<summary>💡 Voir la solution</summary>

```javascript
const estPair = (nombre) => nombre % 2 === 0;

// Tests
console.log(estPair(4)); // true
console.log(estPair(7)); // false
console.log(estPair(0)); // true
```

</details>

## 📚 Travailler avec des Collections : Tableaux et Objets

Les algorithmes opèrent fréquemment sur des **collections de données**. JavaScript fournit deux structures principales :

- **Tableaux** (_arrays_) : Pour les listes ordonnées
- **Objets** (_objects_) : Pour les paires clé-valeur non ordonnées

---

### Tableaux : Collections Ordonnées de Données

Un tableau est un type d'objet spécial utilisé pour stocker une **collection ordonnée** de valeurs. Chaque valeur (élément) a un **index numérique**, commençant à `0`. Les tableaux sont **dynamiques** : leur taille peut changer.

---

#### Créer des Tableaux

```javascript
const tableauVide = [];
const nombres = [1, 2, 3, 4, 5];
const donneesMixtes = [1, "bonjour", true, null];
```

---

#### Accéder aux Éléments

Les éléments sont accessibles via leur **index** (commence à 0).

```javascript
const couleurs = ["rouge", "vert", "bleu"];

console.log(couleurs[0]); // Affiche : rouge
console.log(couleurs[2]); // Affiche : bleu

// Accéder à un index hors limites retourne undefined
console.log(couleurs[3]); // Affiche : undefined
```

---

#### Propriété `length`

Retourne le **nombre d'éléments** dans le tableau.

```javascript
const items = [10, 20, 30, 40];
console.log(items.length); // Affiche : 4
```

---

#### Méthodes de Manipulation de Base

Les tableaux disposent de **méthodes intégrées** pour ajouter, retirer et modifier des éléments.

##### `push()` : Ajouter à la fin

Ajoute un ou plusieurs éléments à la **fin** du tableau et retourne la nouvelle longueur.

```javascript
const taches = ["Faire les courses", "Payer les factures"];
taches.push("Promener le chien");
console.log(taches);
// Affiche : ["Faire les courses", "Payer les factures", "Promener le chien"]
```

---

##### `pop()` : Retirer de la fin

Retire le **dernier** élément du tableau et le retourne.

```javascript
const pile = [10, 20, 30];
const elementRetire = pile.pop();

console.log(elementRetire); // Affiche : 30
console.log(pile); // Affiche : [10, 20]
```

---

##### `unshift()` : Ajouter au début

Ajoute un ou plusieurs éléments au **début** du tableau et retourne la nouvelle longueur.

```javascript
const file = ["Tâche A", "Tâche B"];
file.unshift("Tâche C");
console.log(file);
// Affiche : ["Tâche C", "Tâche A", "Tâche B"]
```

---

##### `shift()` : Retirer du début

Retire le **premier** élément du tableau et le retourne.

```javascript
const fileTraitee = ["Tâche C", "Tâche A", "Tâche B"];
const tacheSuivante = fileTraitee.shift();

console.log(tacheSuivante); // Affiche : Tâche C
console.log(fileTraitee); // Affiche : ["Tâche A", "Tâche B"]
```

---

#### Itérer sur les Tableaux

La boucle `for` est couramment utilisée pour traiter chaque élément d'un tableau.

```javascript
const scores = [85, 90, 78, 92];

for (let i = 0; i < scores.length; i++) {
  console.log(`Score à l'index ${i}: ${scores[i]}`);
}
// Affiche :
// Score à l'index 0: 85
// Score à l'index 1: 90
// Score à l'index 2: 78
// Score à l'index 3: 92
```

**Alternative moderne :** Boucle `for...of`

```javascript
for (const score of scores) {
  console.log(`Score: ${score}`);
}
```

---

### Objets : Paires Clé-Valeur

Les objets en JavaScript sont des **collections non ordonnées** de paires clé-valeur, où les clés sont typiquement des chaînes (ou symboles) et les valeurs peuvent être de n'importe quel type.

**Utilisation :** Représenter des entités avec des propriétés, paramètres de configuration, mappings

---

#### Créer des Objets

```javascript
const objetVide = {};

const utilisateur = {
  nom: "Chermann KING",
  age: 42,
  estActif: true,
  email: "chermann.king@example.com",
};
```

---

#### Accéder aux Propriétés

Deux notations possibles : **point** (`.`) ou **crochets** (`[]`).

```javascript
console.log(utilisateur.nom); // Affiche : Chermann KING (notation point)
console.log(utilisateur["age"]); // Affiche : 42 (notation crochets)

// Notation crochets utile pour propriétés dynamiques
const nomPropriete = "email";
console.log(utilisateur[nomPropriete]); // Affiche : chermann.king@example.com
```

---

#### Modifier et Ajouter des Propriétés

```javascript
utilisateur.age = 43; // Modifier une propriété existante
utilisateur.ville = "Charleroi"; // Ajouter une nouvelle propriété

console.log(utilisateur);
// Affiche : { nom: 'Chermann KING', age: 43, estActif: true, email: 'chermann.king@example.com', ville: 'Charleroi' }
```

---

#### Vérifier l'Existence d'une Propriété

Utiliser l'opérateur `in` ou la méthode `hasOwnProperty()`.

```javascript
console.log("nom" in utilisateur); // Affiche : true
console.log(utilisateur.hasOwnProperty("email")); // Affiche : true
console.log("codePostal" in utilisateur); // Affiche : false
```

---

#### Parcourir les Propriétés d'un Objet

Utiliser la boucle `for...in` :

```javascript
for (const cle in utilisateur) {
  console.log(`${cle}: ${utilisateur[cle]}`);
}
// Affiche :
// nom: Chermann KING
// age: 43
// estActif: true
// email: chermann.king@example.com
// ville: Charleroi
```

---

## 📊 Tableau Récapitulatif : Tableaux vs Objets

| Aspect            | Tableaux                          | Objets                  |
| ----------------- | --------------------------------- | ----------------------- |
| **Structure**     | Liste ordonnée                    | Collection non ordonnée |
| **Accès**         | Par index numérique (0, 1...)     | Par clé (chaîne)        |
| **Utilisation**   | Séquences, listes                 | Entités, configurations |
| **Méthodes clés** | `push`, `pop`, `shift`, `unshift` | Notation point/crochets |
| **Itération**     | `for`, `for...of`                 | `for...in`              |

---

## 💻 Application Pratique : Implémenter des Constructions Algorithmiques de Base

Combinons ces concepts fondamentaux pour résoudre quelques tâches algorithmiques courantes. Ces exemples démontrent comment utiliser ensemble les briques que nous avons étudiées.

---

### Exemple 1 : Trouver l'Élément Maximum dans un Tableau

Cet algorithme nécessite d'itérer sur un tableau, comparer des valeurs, et utiliser une variable pour suivre la plus grande valeur trouvée.

```javascript
/**
 * Trouve le nombre maximum dans un tableau de nombres.
 * @param {number[]} arr Le tableau d'entrée de nombres.
 * @returns {number | undefined} Le nombre maximum, ou undefined si le tableau est vide.
 */
function trouverMax(arr) {
  if (arr.length === 0) {
    console.log("Le tableau est vide, pas d'élément maximum.");
    return undefined; // Gérer le cas limite : tableau vide
  }

  let elementMax = arr[0]; // Supposer que le premier élément est le maximum initialement

  // Itérer sur le reste du tableau à partir du deuxième élément
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > elementMax) {
      // Si l'élément actuel est plus grand que le max actuel
      elementMax = arr[i]; // Mettre à jour elementMax
    }
  }

  return elementMax; // Retourner l'élément maximum final
}

const nombres1 = [3, 1, 4, 1, 5, 9, 2, 6];
console.log(`Élément max dans [${nombres1}]: ${trouverMax(nombres1)}`);
// Affiche : Élément max dans [3,1,4,1,5,9,2,6]: 9

const nombres2 = [-10, -5, -20];
console.log(`Élément max dans [${nombres2}]: ${trouverMax(nombres2)}`);
// Affiche : Élément max dans [-10,-5,-20]: -5

const tableauVide = [];
console.log(`Élément max dans []: ${trouverMax(tableauVide)}`);
// Affiche : Le tableau est vide, pas d'élément maximum. Élément max dans []: undefined
```

---

### Exemple 2 : Inverser une Chaîne de Caractères

Cet algorithme démontre l'itération de chaîne et la construction d'une nouvelle chaîne.

```javascript
/**
 * Inverse une chaîne de caractères donnée.
 * @param {string} str La chaîne d'entrée.
 * @returns {string} La chaîne inversée.
 */
function inverserChaine(str) {
  let inverse = ""; // Initialiser une chaîne vide pour construire l'inverse

  // Boucle sur la chaîne d'entrée du dernier caractère au premier
  for (let i = str.length - 1; i >= 0; i--) {
    inverse += str[i]; // Ajouter chaque caractère à la chaîne 'inverse'
  }

  return inverse;
}

const chaineOriginale1 = "javascript";
console.log(
  `Original: "${chaineOriginale1}", Inversé: "${inverserChaine(
    chaineOriginale1,
  )}"`,
);
// Affiche : Original: "javascript", Inversé: "tpircsavaj"

const chaineOriginale2 = "bonjour";
console.log(
  `Original: "${chaineOriginale2}", Inversé: "${inverserChaine(
    chaineOriginale2,
  )}"`,
);
// Affiche : Original: "bonjour", Inversé : "ruojnob"

const chaineOriginale3 = "a";
console.log(
  `Original: "${chaineOriginale3}", Inversé: "${inverserChaine(
    chaineOriginale3,
  )}"`,
);
// Affiche : Original: "a", Inversé: "a"

const chaineVide = "";
console.log(
  `Original: "${chaineVide}", Inversé: "${inverserChaine(chaineVide)}"`,
);
// Affiche : Original: "", Inversé: ""
```

---

### Exemple 3 : Calculer la Factorielle avec une Boucle

Démontre le calcul itératif et les vérifications conditionnelles.

```javascript
/**
 * Calcule la factorielle d'un entier non négatif.
 * La factorielle de n (n!) est le produit de tous les entiers positifs <= n.
 * 0! est défini comme 1.
 * @param {number} n L'entier non négatif d'entrée.
 * @returns {number | string} La factorielle de n, ou un message d'erreur pour entrée invalide.
 */
function calculerFactorielle(n) {
  // Gérer l'entrée invalide : nombres négatifs
  if (n < 0) {
    return "La factorielle n'est pas définie pour les nombres négatifs.";
  }

  // Cas de base : La factorielle de 0 est 1
  if (n === 0) {
    return 1;
  }

  let resultat = 1; // Initialiser le résultat à 1

  // Multiplier le résultat par chaque entier de 1 à n
  for (let i = 1; i <= n; i++) {
    resultat *= i; // Équivalent à : resultat = resultat * i;
  }

  return resultat;
}

console.log(`Factorielle de 5: ${calculerFactorielle(5)}`);
// Affiche : Factorielle de 5: 120 (5 * 4 * 3 * 2 * 1)

console.log(`Factorielle de 0: ${calculerFactorielle(0)}`);
// Affiche : Factorielle de 0: 1

console.log(`Factorielle de 1: ${calculerFactorielle(1)}`);
// Affiche : Factorielle de 1: 1

console.log(`Factorielle de 10: ${calculerFactorielle(10)}`);
// Affiche : Factorielle de 10: 3628800

console.log(`Factorielle de -3: ${calculerFactorielle(-3)}`);
// Affiche : Factorielle de -3: La factorielle n'est pas définie pour les nombres négatifs.
```

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension de ces concepts fondamentaux JavaScript, implémentez les problèmes suivants. Ces exercices s'appuient directement sur les exemples et concepts que nous avons couverts.

---

### Exercice 1 : Somme des Éléments d'un Tableau

**Objectif :** Comprendre l'itération de tableau et l'accumulation

**Instructions :** Écrivez une fonction appelée `sommeTableau` qui prend un tableau de nombres en entrée et retourne la somme de tous ses éléments.

**Exemple :**

```javascript
sommeTableau([1, 2, 3, 4]); // devrait retourner 10
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function sommeTableau(arr) {
  let somme = 0;
  for (let i = 0; i < arr.length; i++) {
    somme += arr[i];
  }
  return somme;
}

// Tests
console.log(sommeTableau([1, 2, 3, 4])); // 10
console.log(sommeTableau([10, 20, 30])); // 60
console.log(sommeTableau([])); // 0
```

</details>

---

### Exercice 2 : Compter les Voyelles dans une Chaîne

**Objectif :** Manipulation de chaînes et logique conditionnelle

**Instructions :** Écrivez une fonction appelée `compterVoyelles` qui prend une chaîne en entrée et retourne le nombre de voyelles (a, e, i, o, u, y, insensible à la casse) qu'elle contient.

**Exemple :**

```javascript
compterVoyelles("Programmation"); // devrait retourner 5
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function compterVoyelles(str) {
  const voyelles = ["a", "e", "i", "o", "u", "y"];
  let compteur = 0;
  const strMinuscule = str.toLowerCase();

  for (let i = 0; i < strMinuscule.length; i++) {
    if (voyelles.includes(strMinuscule[i])) {
      compteur++;
    }
  }

  return compteur;
}

// Tests
console.log(compterVoyelles("Programmation")); // 5
console.log(compterVoyelles("JavaScript")); // 3
console.log(compterVoyelles("xyz")); // 1 (y)
```

</details>

---

### Exercice 3 : Trouver l'Élément Minimum dans un Tableau

**Objectif :** Comparaison et gestion des cas limites

**Instructions :** Similaire à `trouverMax`, écrivez une fonction `trouverMin` qui prend un tableau de nombres et retourne le plus petit nombre. Gérez le cas du tableau vide.

**Exemple :**

```javascript
trouverMin([8, 3, 12, 1, 9]); // devrait retourner 1
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function trouverMin(arr) {
  if (arr.length === 0) {
    return undefined;
  }

  let elementMin = arr[0];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < elementMin) {
      elementMin = arr[i];
    }
  }

  return elementMin;
}

// Tests
console.log(trouverMin([8, 3, 12, 1, 9])); // 1
console.log(trouverMin([-5, -10, -3])); // -10
console.log(trouverMin([])); // undefined
```

</details>

---

### Exercice 4 : Créer un Objet depuis des Tableaux Clé-Valeur

**Objectif :** Manipulation d'objets et de tableaux

**Instructions :** Écrivez une fonction `creerObjet` qui prend deux tableaux de longueur égale en entrée : un pour les clés (chaînes) et un pour les valeurs. Elle devrait retourner un objet où chaque paire clé-valeur est formée à partir d'éléments correspondants dans les tableaux d'entrée.

**Exemple :**

```javascript
creerObjet(["a", "b"], [1, 2]); // devrait retourner { a: 1, b: 2 }
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function creerObjet(cles, valeurs) {
  const objet = {};

  for (let i = 0; i < cles.length; i++) {
    objet[cles[i]] = valeurs[i];
  }

  return objet;
}

// Tests
console.log(creerObjet(["a", "b"], [1, 2])); // { a: 1, b: 2 }
console.log(creerObjet(["nom", "age"], ["Alice", 25])); // { nom: 'Alice', age: 25 }
console.log(creerObjet([], [])); // {}
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la différence principale entre `let` et `const` en JavaScript ?**

- [ ] A. `let` est utilisé pour les nombres et `const` pour les chaînes de caractères
- [ ] B. `let` permet la réassignation de valeur tandis que `const` crée une variable dont la valeur ne peut pas être réassignée
- [ ] C. `const` est plus rapide que `let` en termes de performance
- [ ] D. Il n'y a aucune différence, ce sont des synonymes

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

`let` permet de réassigner une nouvelle valeur à la variable, tandis que `const` crée une variable dont la référence ne peut pas être changée après l'initialisation.

</details>

---

### Question 2

**Parmi les affirmations suivantes sur les types de données en JavaScript, lesquelles sont vraies ? (Plusieurs réponses possibles)**

- [ ] A. `typeof null` renvoie `"object"` (c'est une bizarrerie historique de JavaScript)
- [ ] B. `undefined` signifie qu'une variable a été déclarée mais n'a pas encore reçu de valeur
- [ ] C. JavaScript fait une distinction stricte entre les nombres entiers et les nombres décimaux
- [ ] D. Les chaînes de caractères peuvent être créées avec des guillemets simples, doubles ou des backticks

<details>
<summary>Voir la réponse</summary>

**Réponses : A, B, D**

Les affirmations vraies sont :

- `typeof null` renvoie effectivement `"object"` (A) - c'est un bug historique de JavaScript
- `undefined` indique une variable déclarée mais non initialisée (B)
- Les chaînes peuvent utiliser `'`, `"` ou `` ` `` (D)

L'option C est fausse : JavaScript a un seul type `number` pour tous les nombres.

</details>

---

### Question 3

**Quel est le résultat de ce code JavaScript ?**

```javascript
let score = 75;
let resultat;

if (score >= 90) {
  resultat = "Excellent";
} else if (score >= 70) {
  resultat = "Bien";
} else {
  resultat = "À améliorer";
}

console.log(resultat);
```

- [ ] A. "Excellent"
- [ ] B. "Bien"
- [ ] C. "À améliorer"
- [ ] D. `undefined`

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le score est 75, donc :

- `score >= 90` est faux (75 < 90)
- `score >= 70` est vrai (75 >= 70)

Le code entre dans le deuxième `else if` et `resultat` prend la valeur `"Bien"`.

</details>

---

### Question 4

**Quelle boucle est la plus appropriée pour itérer sur tous les éléments d'un tableau ?**

- [ ] A. `while` - car elle est plus rapide
- [ ] B. `for` - car elle permet d'accéder facilement à l'index de chaque élément
- [ ] C. Les deux sont équivalentes et le choix dépend de la lisibilité du code
- [ ] D. Aucune - il faut toujours utiliser `forEach()`

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Les deux boucles peuvent être utilisées pour itérer sur un tableau. Le choix dépend de :

- La **lisibilité** : `for` est plus direct quand on a besoin de l'index
- Le **contexte** : `while` est utile quand la condition d'arrêt est plus complexe

Il n'y a pas de différence significative de performance. Les méthodes comme `forEach()`, `map()`, etc. sont également valides mais ne sont pas la seule option.

</details>

---

### Question 5

**Quelles sont les caractéristiques des fonctions fléchées (arrow functions) en JavaScript ? (Plusieurs réponses possibles)**

- [ ] A. Elles utilisent la syntaxe `() => { }`
- [ ] B. Elles permettent un retour implicite quand il n'y a qu'une seule expression
- [ ] C. Elles sont toujours plus rapides que les fonctions traditionnelles
- [ ] D. Elles peuvent omettre les parenthèses autour du paramètre s'il n'y en a qu'un seul

<details>
<summary>Voir la réponse</summary>

**Réponses : A, B, D**

Les caractéristiques correctes sont :

- Syntaxe `() => { }` (A)
- Retour implicite pour une seule expression : `x => x * 2` (B)
- Parenthèses optionnelles avec un seul paramètre : `x => x * 2` au lieu de `(x) => x * 2` (D)

L'option C est fausse : il n'y a pas de différence de performance significative.

</details>

---

### Question 6

**Quelle méthode de tableau JavaScript ajoute un élément à la fin du tableau ?**

- [ ] A. `shift()`
- [ ] B. `unshift()`
- [ ] C. `push()`
- [ ] D. `pop()`

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Les méthodes de manipulation de tableau :

- `push()` : ajoute à la **fin**
- `pop()` : retire de la **fin**
- `unshift()` : ajoute au **début**
- `shift()` : retire du **début**

</details>

---

### Question 7

**Comment accéder à la valeur de la propriété `nom` dans l'objet suivant ?**

```javascript
const utilisateur = {
  nom: "Marie",
  age: 25,
  ville: "Bruxelles",
};
```

- [ ] A. `utilisateur[nom]`
- [ ] B. `utilisateur.nom` ou `utilisateur["nom"]`
- [ ] C. `utilisateur->nom`
- [ ] D. `utilisateur::nom`

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Il y a deux syntaxes valides pour accéder aux propriétés d'un objet :

- **Notation point** : `utilisateur.nom`
- **Notation crochet** : `utilisateur["nom"]`

L'option A est incorrecte car il manque les guillemets autour de `nom`.
Les options C et D utilisent des syntaxes d'autres langages (C++, PHP).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Variables et Types

- Utilisez `const` par défaut, `let` pour la réassignation
- Types essentiels : `number`, `string`, `boolean`, `null`, `undefined`

### 2. Structures Conditionnelles

- `if/else` pour les décisions
- `switch` pour les choix multiples sur une même variable

### 3. Boucles

- `for` : Nombre d'itérations connu
- `while` : Nombre d'itérations inconnu

### 4. Fonctions

- Déclarations et expressions de fonctions
- Fonctions fléchées pour syntaxe concise
- Encapsulent la logique réutilisable

### 5. Tableaux

- Collections ordonnées avec index numériques
- Méthodes : `push`, `pop`, `shift`, `unshift`
- Itération avec boucles `for`

### 6. Objets

- Collections de paires clé-valeur
- Accès par notation point ou crochets
- Itération avec `for...in`

### 7. Mise en Pratique

- Traduire les algorithmes conceptuels en code
- Gérer les cas limites et erreurs
- Combiner les concepts pour résoudre des problèmes

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maintenant une base solide en JavaScript pour le développement d'algorithmes !

### Ce que vous avez appris aujourd'hui

Dans cette leçon, nous avons revu les **blocs de construction fondamentaux** de JavaScript indispensables au développement d'algorithmes :

**Variables** avec `let` et `const`
**Types de données** essentiels (number, string, boolean, null, undefined)
**Contrôle de flux** avec `if/else` et `switch`
**Boucles** `for` et `while`
**Fonctions** traditionnelles et fléchées
**Tableaux** et **objets** pour les collections de données

### Compétences acquises

Vous êtes maintenant capable de :

Traduire des étapes algorithmiques abstraites en code JavaScript concret et fonctionnel
Manipuler des données avec les types appropriés
Implémenter une logique de décision et de répétition
Organiser votre code avec des fonctions réutilisables
Travailler avec des collections de données

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La capacité à traduire des étapes algorithmiques abstraites en code JavaScript fonctionnel est la **base** sur laquelle toute conception d'algorithme plus avancée sera construite.

Ces concepts seront **constamment appliqués, affinés et combinés** pour résoudre des problèmes de plus en plus complexes.

---

## ➡️ Prochaine Étape : Leçon 3

### Ce qui vous attend

Maintenant que vous pouvez écrire du code, la prochaine leçon, **« Mesurer l'Efficacité des Algorithmes : Complexité Temporelle et Spatiale »**, vous apprendra à évaluer si votre code est performant.

**Vous découvrirez :**

- La différence fondamentale entre la **complexité temporelle** (vitesse) et **spatiale** (mémoire).
- Comment analyser le pire, le meilleur et le cas moyen d'un algorithme.
- Une introduction aux ordres de grandeur pour comparer différentes solutions.

### Préparez-vous !

Comprendre comment mesurer l'efficacité est ce qui sépare un développeur qui écrit du code "qui marche" d'un développeur qui conçoit des solutions "performantes et scalables".

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [JavaScript pour Débutants - Grafikart](https://grafikart.fr/formations/javascript)
- [MDN Web Docs - JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript)
- [JavaScript Quiz - W3Schools](https://www.w3schools.com/js/js_quiz.asp)

### Outils de pratique

- **[JSFiddle](https://jsfiddle.net/)** : Éditeur JavaScript en ligne
- **[Node.js](https://nodejs.org/)** : Pour exécuter JavaScript localement
- **[Console du navigateur](https://developer.mozilla.org/fr/docs/Learn/Common_questions/What_are_browser_developer_tools)** : F12 dans Chrome/Firefox

### Livres recommandés

- **"Eloquent JavaScript"** de Marijn Haverbeke (gratuit en ligne)
- **"JavaScript: The Good Parts"** de Douglas Crockford

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> La maîtrise de JavaScript vient avec la **pratique régulière**. Essayez de coder un petit algorithme chaque jour pour renforcer ces fondamentaux !

---

**Prêt pour la Leçon 3 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir comment mesurer l'efficacité de vos algorithmes !

---

<div align="center">

**Leçon 2 sur 42 - Module 1 : Fondements des algorithmes et révision de JavaScript**

[⬅️ Leçon 1 : Qu'est-ce qu'un algorithme ?](./lecon-1-quest-ce-qu-un-algorithme.md) | [Retour au sommaire](./README.md) | [Leçon 3 : Complexité des Algorithmes ➡️](./lecon-3-complexite-algorithmes.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
