##### Leçon 3 sur 42

# Mesurer l'Efficacité des Algorithmes : Complexité Temporelle et Spatiale

**Module 1** : Fondements des algorithmes et révision de JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Définir ce qu'est l'efficacité algorithmique et pourquoi elle est importante
- Distinguer la complexité temporelle de la complexité spatiale
- Compter les opérations fondamentales pour évaluer le temps d'exécution
- Analyser l'utilisation de la mémoire d'un algorithme
- Identifier les patterns de complexité (constant, linéaire, quadratique)
- Appliquer ces concepts pour comparer différents algorithmes

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- Avoir complété la Leçon 1 : Qu'est-ce qu'un algorithme ?
- Avoir complété la Leçon 2 : Introduction à JavaScript
- Maîtriser les boucles, conditions et tableaux en JavaScript

---

## 🚀 Introduction : Pourquoi l'efficacité est cruciale

Imaginez que vous développez une application de recherche de contacts. Vous avez deux approches possibles :

- **Approche A** : Parcourir tous les contacts un par un jusqu'à trouver le bon
- **Approche B** : Utiliser une structure de données optimisée qui permet de trouver directement le contact

Les deux approches donnent le **même résultat correct**. Mais l'Approche A prend 10 secondes avec 10 000 contacts, tandis que l'Approche B prend 0,1 seconde. Quelle approche préféreriez-vous utiliser ?

Lorsqu'on écrit des algorithmes, notre objectif principal est souvent de **résoudre un problème correctement**. Cependant, dans le monde du développement logiciel, la **correction n'est qu'une pièce du puzzle**. Un algorithme peut produire la bonne réponse, mais s'il prend un temps déraisonnablement long ou consomme trop de mémoire, il devient **pratiquement inutile** dans une application réelle.

**Pourquoi l'efficacité algorithmique est-elle importante ?**

- **Expérience utilisateur** : Les applications lentes frustrent les utilisateurs
- **Scalabilité** : À mesure que les données augmentent, vos algorithmes doivent suivre
- **Coûts** : Des algorithmes plus rapides = moins de ressources serveur = coûts réduits
- **Performance** : Applications réactives et fluides

> **Point Clé**
>
> Comprendre l'efficacité algorithmique vous permet d'écrire des programmes qui non seulement **fonctionnent**, mais qui **performent** bien, offrant une expérience utilisateur fluide et utilisant de manière optimale les ressources informatiques.

---

## 📊 Qu'est-ce que l'Efficacité Algorithmique ?

L'**efficacité algorithmique** fait référence aux propriétés d'un algorithme concernant la quantité de **ressources computationnelles** qu'il utilise. Les deux ressources principales sur lesquelles nous nous concentrons sont :

### 1. Le Temps (Complexité Temporelle)

**Combien de temps l'algorithme prend-il pour s'exécuter ?**

### 2. L'Espace (Complexité Spatiale)

**Quelle quantité de mémoire l'algorithme utilise-t-il ?**

**Distinction importante :**

Nous ne mesurons pas le temps en **secondes** ou **millisecondes** (qui varient selon l'ordinateur, le langage, etc.), mais plutôt **comment le nombre d'opérations croît** à mesure que la taille de l'entrée augmente.

---

## ⏱️ Complexité Temporelle : À Quelle Vitesse s'Exécute-t-il ?

### Définition

La **complexité temporelle** mesure la quantité de temps qu'un algorithme prend pour se terminer en fonction de la **longueur de son entrée**.

### Ce que nous évaluons

- Pas le temps exact en secondes
- Le **taux de croissance** du temps d'exécution
- Comment le nombre d'opérations augmente avec la taille de l'entrée

---

### Analogie : Deux Façons de Trier des Livres

Imaginez que vous devez trier une pile de livres par ordre alphabétique :

**Méthode A (Tri par Insertion)** :

- Pour une petite pile de 10 livres : très rapide
- Pour 100 livres : commence à ralentir
- Pour 1 000 livres : devient très lent

**Méthode B (Tri Fusion)** :

- Pour 10 livres : légèrement plus lent que A
- Pour 100 livres : plus rapide que A
- Pour 1 000 livres : **beaucoup plus rapide** que A

La complexité temporelle nous aide à **prédire ce comportement** sans avoir à exécuter le code sur toutes les tailles d'entrée possibles !

---

### Exemple Réel 1 : Recherche de Contact

**Scénario :** Application de contacts sur smartphone avec 500 contacts.

**Algorithme Naïf** :

```
Pour chaque lettre tapée dans la recherche :
  Parcourir les 500 contacts un par un
  Vérifier si le nom correspond

Résultat : 500 vérifications par lettre tapée
```

**Algorithme Optimisé** :

```
Créer un index alphabétique au démarrage
Pour chaque lettre tapée :
  Consulter directement la section alphabétique

Résultat : Quelques vérifications seulement, quel que soit le nombre total de contacts
```

> **Important**
>
> Le temps de recherche ne croît **pas linéairement** avec le nombre de contacts grâce à l'algorithme optimisé. C'est la magie de choisir le bon algorithme !

---

### Exemple Réel 2 : Chargement d'un Fil d'Actualité

**Scénario :** Plateforme de réseau social chargeant votre fil d'actualité.

**Approche Inefficace** :

```javascript
// Pour chaque utilisateur suivi (ex: 1000 personnes)
//   Télécharger TOUS leurs posts
//   Trier tous les posts
//   Filtrer les posts non pertinents
//   Afficher le résultat

// Temps : Très long, complexité élevée
```

**Approche Efficace** :

```javascript
// Pré-traiter les données côté serveur
// Utiliser un moteur de recommandations
// Charger seulement les posts les plus pertinents et récents
// Charger par lots (pagination)

// Temps : Rapide et constant, même avec des milliers d'abonnements
```

La plateforme moderne utilise des algorithmes sophistiqués qui maintiennent un temps de chargement **relativement constant** même si vous suivez des milliers de personnes.

---

## 💾 Complexité Spatiale : Quelle Quantité de Mémoire Utilise-t-il ?

### Définition

La **complexité spatiale** mesure la quantité de **mémoire (ou espace)** qu'un algorithme nécessite pour s'exécuter jusqu'à son terme.

### Ce qui est inclus

- Mémoire pour les valeurs d'entrée
- Variables temporaires
- Structures de données additionnelles créées par l'algorithme

---

### Pourquoi est-ce important ?

#### 1. Contraintes de Ressources

Les smartphones, systèmes embarqués et navigateurs web ont une **mémoire limitée**. Manquer de mémoire peut faire **crasher** l'application.

#### 2. Impact sur les Performances

Une utilisation excessive de la mémoire peut indirectement impacter les performances (cache misses, swap vers stockage plus lent).

#### 3. Scalabilité

Comme pour le temps, un algorithme peut fonctionner avec de petites entrées mais **épuiser la mémoire** pour des ensembles de données plus grands.

---

### Exemple Réel 1 : Éditeur d'Images - Annuler/Refaire

**Scénario :** Application d'édition photo en ligne.

**Approche Inefficace (Mauvaise Complexité Spatiale)** :

```javascript
// Stocker une copie COMPLÈTE de l'image après chaque modification

let historique = [];
function appliquerFiltre(image, filtre) {
  const nouvelleImage = copierImage(image); // Copie complète !
  appliquerModification(nouvelleImage, filtre);
  historique.push(nouvelleImage); // Stocke la copie complète
  return nouvelleImage;
}

// Pour une image de 10 Mo éditée 10 fois :
// Mémoire utilisée : 10 Mo × 10 = 100 Mo
```

**Approche Efficace (Bonne Complexité Spatiale)** :

```javascript
// Stocker seulement les COMMANDES/CHANGEMENTS

let commandesHistorique = [];
function appliquerFiltre(image, filtre) {
  commandesHistorique.push({ action: "filtre", type: filtre });
  appliquerModification(image, filtre);
  return image;
}

// Pour annuler : appliquer la commande inverse
// Mémoire utilisée : quelques Ko pour stocker les commandes
```

---

### Exemple Réel 2 : Historique de Chat en Ligne

**Scénario :** Application de messagerie avec des années d'historique.

**Approche Inefficace** :

```javascript
// Télécharger et stocker TOUT l'historique de chat
// dès l'ouverture de la conversation

function ouvrirChat(amiId) {
  const toutLhistorique = telechargerHistoriqueComplet(amiId);
  // Si 10 000 messages → beaucoup de mémoire
  afficher(toutLhistorique);
}
```

**Approche Efficace** :

```javascript
// Charger seulement une portion récente
// Charger plus au scroll (chargement à la demande)

function ouvrirChat(amiId) {
  const messagesRecents = telechargerDerniers50Messages(amiId);
  // Toujours ~50 messages en mémoire
  afficher(messagesRecents);
}

function scrollVersLeHaut() {
  chargerPlus50MessagesAnterieurs();
  // Optionnellement supprimer les plus anciens messages de la mémoire
}
```

---

## 🔢 Mesurer l'Efficacité : Compter les Opérations

Pour comprendre la complexité temporelle et spatiale, nous comptons souvent les **opérations fondamentales** qu'un algorithme effectue ou les **unités de mémoire** qu'il consomme.

### Opérations à Compter (Complexité Temporelle)

Lorsqu'on évalue la complexité temporelle, nous cherchons les opérations qui contribuent le plus au temps d'exécution :

- Opérations arithmétiques (`+`, `-`, `*`, `/`)
- Comparaisons (`>`, `<`, `===`, `!==`)
- Affectations (`x = 5`)
- Accès aux éléments d'un tableau (`arr[i]`)
- Appels de fonctions

**Focus principal :** Le nombre de fois qu'une opération clé est exécutée dans une boucle ou un appel récursif.

---

## 📝 Micro-Exercice #1 : Identifier les Opérations

**Objectif :** S'entraîner à identifier les opérations fondamentales dans du code JavaScript.

**Instructions :** Pour le code suivant, listez toutes les opérations fondamentales :

```javascript
function calculerMoyenne(notes) {
  let somme = 0;
  for (let i = 0; i < notes.length; i++) {
    somme = somme + notes[i];
  }
  const moyenne = somme / notes.length;
  return moyenne;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Opérations identifiées :**

1. `let somme = 0;` → 1 affectation
2. `let i = 0;` → 1 affectation
3. `i < notes.length;` → Comparaison répétée (n+1 fois si n = notes.length)
4. `i++` → Incrémentation répétée (n fois)
5. `notes[i]` → Accès tableau répété (n fois)
6. `somme + notes[i]` → Addition répétée (n fois)
7. `somme = ...` → Affectation répétée (n fois)
8. `somme / notes.length` → 1 division
9. `const moyenne = ...` → 1 affectation
10. `return moyenne` → 1 retour

**Total approximatif :** 4 + 4n opérations (où n = notes.length)

**Conclusion :** Le nombre d'opérations croît **linéairement** avec la taille du tableau.

</details>

---

## 💻 Exemple 1 : Sommer les Éléments d'un Tableau

Analysons en détail une fonction simple qui calcule la somme de tous les éléments d'un tableau.

```javascript
function sommerTableau(arr) {
  let total = 0; // Opération 1: Affectation

  for (let i = 0; i < arr.length; i++) {
    // i = 0              : 1 affectation (une fois)
    // i < arr.length     : n+1 comparaisons
    // i++                : n incrémentations

    total += arr[i];
    // arr[i]             : n accès tableau
    // total + arr[i]     : n additions
    // total = ...        : n affectations
  }

  return total; // Opération finale: Retour
}

// Tests
const petitTableau = [1, 2, 3]; // n = 3
const grandTableau = [10, 20, 30, 40, 50]; // n = 5

console.log(sommerTableau(petitTableau)); // 6
console.log(sommerTableau(grandTableau)); // 150
```

### 📊 Analyse Détaillée

**Décompte des opérations :**

| Opération                   | Nombre d'exécutions |
| --------------------------- | ------------------- |
| `total = 0`                 | 1                   |
| `i = 0`                     | 1                   |
| `i < arr.length`            | n + 1               |
| `i++`                       | n                   |
| `arr[i]` (accès)            | n                   |
| `total + arr[i]`            | n                   |
| `total = ...` (affectation) | n                   |
| `return total`              | 1                   |

**Total : 1 + 1 + (n+1) + n + n + n + n + 1 = 5n + 4**

**Observations :**

- Si `n = 3` → `5×3 + 4 = 19` opérations
- Si `n = 5` → `5×5 + 4 = 29` opérations
- Si `n = 100` → `5×100 + 4 = 504` opérations

> **Point Clé**
>
> À mesure que n augmente, le terme **5n** domine largement le **+4**. Cette relation **linéaire** est essentielle pour comprendre la complexité temporelle. Le temps d'exécution croît **proportionnellement** à la taille de l'entrée n.

---

## 💻 Exemple 2 : Recherche dans une Matrice (Boucles Imbriquées)

Considérons une fonction qui vérifie si une valeur spécifique existe dans une "matrice" (un tableau de tableaux).

```javascript
function trouverValeurDansMatrice(matrice, valeur) {
  // Soit R le nombre de lignes (matrice.length)
  // Soit C le nombre de colonnes (matrice[r].length)

  for (let r = 0; r < matrice.length; r++) {
    // Boucle externe
    for (let c = 0; c < matrice[r].length; c++) {
      // Boucle interne
      if (matrice[r][c] === valeur) {
        // Comparaison + accès
        return true; // Trouvé !
      }
    }
  }
  return false; // Non trouvé
}

// Test
const matrice1 = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
]; // 3 lignes × 3 colonnes = 9 éléments

console.log(trouverValeurDansMatrice(matrice1, 5)); // true
console.log(trouverValeurDansMatrice(matrice1, 10)); // false
```

### Analyse de la Complexité

**Soit :**

- R = nombre de lignes
- C = nombre de colonnes
- Pour simplifier, supposons R ≈ C ≈ n

**Opérations :**

- **Boucle externe** : S'exécute R fois
  - Comparaisons : R + 1
  - Incrémentations : R

- **Boucle interne** : Pour chaque itération de la boucle externe, s'exécute C fois
  - Comparaisons : R × (C + 1)
  - Incrémentations : R × C

- **Comparaison `if`** : Exécutée R × C fois dans le pire cas
  - Accès tableau : 2 accès (`matrice[r]` puis `[c]`)

**Total d'opérations dominantes : R × C**

Si R = C = n, alors **n × n = n²** opérations.

**Comparaison avec l'exemple précédent :**

| Taille (n) | Linéaire (5n) | Quadratique (n²) |
| ---------- | ------------- | ---------------- |
| 10         | 50            | 100              |
| 100        | 500           | **10 000**       |
| 1000       | 5000          | **1 000 000**    |

> **Important**
>
> La complexité **quadratique** (n²) croît **beaucoup plus rapidement** que la complexité linéaire (n). Pour n = 100, n² est déjà **20 fois plus grand** que 5n !

---

## 📝 Micro-Exercice #2 : Analyser une Fonction

**Objectif :** Analyser la complexité temporelle d'une fonction avec boucle imbriquée.

**Instructions :** Analysez cette fonction et déterminez combien d'opérations elle effectue en fonction de n.

```javascript
function afficherPaires(n) {
  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
      console.log(`Paire: (${i}, ${j})`);
    }
  }
}
```

<details>
<summary>💡 Voir la solution</summary>

**Analyse :**

- **Boucle externe** : S'exécute `n` fois (de 1 à n)
- **Boucle interne** : Pour chaque itération externe, s'exécute `n` fois
- **console.log** : Exécuté `n × n` fois

**Total d'opérations dominantes : n²**

**Exemple concret :**

Si `n = 3` :

```
Paire: (1, 1), (1, 2), (1, 3)
Paire: (2, 1), (2, 2), (2, 3)
Paire: (3, 1), (3, 2), (3, 3)
```

Total : 9 paires affichées = 3²

**Conclusion :** Cette fonction a une complexité temporelle **quadratique** (n²).

</details>

---

## 💾 Analyser la Complexité Spatiale

Pour la complexité spatiale, nous examinons la quantité de **mémoire additionnelle** dont un algorithme a besoin au-delà de l'entrée elle-même. Cette mémoire "extra" est souvent appelée **espace auxiliaire**.

### Unités de Mémoire à Compter

- **Variables** (`let total = 0`)
- **Structures de données** (nouveaux tableaux, objets)
- **Pile d'appels de fonctions** (pour les fonctions récursives)

---

## 💻 Exemple 3 : Espace Constant - Somme d'un Tableau (Revisité)

```javascript
function sommerTableau(arr) {
  let total = 0; // Stocke 1 nombre
  for (let i = 0; i < arr.length; i++) {
    // Stocke 1 nombre (i)
    total += arr[i];
  }
  return total;
}
```

### Analyse Spatiale

**Mémoire utilisée :**

- `total` : espace pour 1 nombre
- `i` : espace pour 1 nombre
- **Total : 2 nombres** (quantité fixe)

**Observation importante :**

Peu importe la taille du tableau `arr` (10, 100, ou 1 000 000 éléments), cette fonction n'utilise **jamais plus que 2 variables**.

Elle ne crée **aucun nouveau tableau** ou objet dont la taille dépend de `arr.length`.

> **Point Clé**
>
> Cette fonction a une complexité spatiale **constante** : la mémoire additionnelle ne croît **pas** avec la taille de l'entrée.

---

## 💻 Exemple 4 : Espace Linéaire - Créer un Tableau Inversé

```javascript
function inverserTableau(arr) {
  const tableauInverse = []; // Crée un nouveau tableau vide

  for (let i = arr.length - 1; i >= 0; i--) {
    tableauInverse.push(arr[i]); // Ajoute des éléments au nouveau tableau
  }

  return tableauInverse;
}

// Test
const original = [1, 2, 3, 4, 5];
const inverse = inverserTableau(original);
console.log(inverse); // [5, 4, 3, 2, 1]
```

### Analyse Spatiale

**Mémoire utilisée :**

- `tableauInverse` : Nouveau tableau qui va contenir n éléments
- `i` : 1 nombre (variable de boucle)

**Si l'entrée `arr` a n éléments :**

- `tableauInverse` contiendra également n éléments à la fin
- La mémoire additionnelle croît **proportionnellement** à n

> **Point Clé**
>
> Cette fonction a une complexité spatiale **linéaire** (n) : la mémoire additionnelle croît directement avec la taille de l'entrée.

---

## 📝 Micro-Exercice #3 : Complexité Spatiale

**Objectif :** Identifier la complexité spatiale d'une fonction.

**Instructions :** Analysez la mémoire utilisée par cette fonction :

```javascript
function doublerValeurs(nombres) {
  const doubles = [];
  for (let i = 0; i < nombres.length; i++) {
    doubles.push(nombres[i] * 2);
  }
  return doubles;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Analyse Spatiale :**

**Mémoire utilisée :**

- `doubles` : Nouveau tableau qui contiendra n éléments (où n = nombres.length)
- `i` : 1 nombre (variable de boucle)

**Conclusion :**

Cette fonction crée un nouveau tableau `doubles` de la **même taille** que le tableau d'entrée.

**Complexité spatiale : Linéaire (n)**

La mémoire additionnelle requise croît proportionnellement à la taille de `nombres`.

**Exemple :**

- Si `nombres` a 10 éléments → `doubles` aura 10 éléments
- Si `nombres` a 1000 éléments → `doubles` aura 1000 éléments

</details>

---

## 💻 Exemples Pratiques et Démonstrations

Consolidons notre compréhension avec des exemples JavaScript concrets, en nous concentrant sur le comptage conceptuel des opérations et de la mémoire.

---

### Exemple 1 : Temps et Espace **Constants**

Une fonction dont les performances (temps ou espace) ne dépendent **pas** de la taille de son entrée est dite de complexité **constante**.

```javascript
/**
 * Obtenir le premier élément d'un tableau
 * @param {Array} arr - Tableau d'entrée
 * @returns {*} Premier élément du tableau
 */
function obtenirPremierElement(arr) {
  // COMPLEXITÉ TEMPORELLE :
  // - arr[0]        : 1 accès tableau
  // - return arr[0] : 1 retour
  // Total : Nombre fixe d'opérations, quel que soit arr.length
  // → TEMPS CONSTANT

  // COMPLEXITÉ SPATIALE :
  // - Aucune variable ou structure créée dépendant de arr.length
  // → ESPACE CONSTANT

  return arr[0];
}

// Tests
console.log(obtenirPremierElement([10, 20, 30, 40, 50])); // 10
console.log(obtenirPremierElement([1])); // 1
console.log(obtenirPremierElement([99, 88, 77])); // 99
```

**Analyse :**

Que le tableau ait **1 élément ou 1 million d'éléments**, cette fonction effectue toujours exactement **2 opérations** :

1. Accéder à `arr[0]`
2. Retourner la valeur

Le nombre d'opérations **ne change pas** avec `arr.length`.

**Complexité :**

- **Temps : Constant**
- **Espace : Constant**

---

### Exemple 2 : Temps et Espace **Linéaires**

Lorsque le nombre d'opérations ou la quantité de mémoire croît **directement proportionnellement** à la taille de l'entrée n, on parle de complexité **linéaire**.

```javascript
/**
 * Créer une copie d'un tableau
 * @param {Array} arr - Tableau à copier
 * @returns {Array} Copie du tableau
 */
function copierTableau(arr) {
  const nouveauArr = []; // ESPACE : Crée un nouveau tableau vide

  for (let i = 0; i < arr.length; i++) {
    // TEMPS : Boucle s'exécute n fois
    nouveauArr.push(arr[i]);
    // - arr[i]              : 1 accès tableau
    // - push()              : 1 opération (temps constant amorti)
  }

  return nouveauArr; // ESPACE : nouveauArr contiendra n éléments
}

// Tests
console.log(copierTableau([1, 2, 3, 4])); // [1, 2, 3, 4]
console.log(copierTableau(["a", "b", "c", "d", "e", "f"])); // ['a', 'b', 'c', 'd', 'e', 'f']
```

**Analyse :**

- **Temps :** La boucle s'exécute `arr.length` (n) fois. À chaque itération :
  - `arr[i]` : accès constant
  - `push()` : opération constante (en moyenne)
  - **Total : n opérations** → Temps **linéaire**

- **Espace :** Un nouveau tableau `nouveauArr` est créé et contiendra finalement n éléments
  - **Mémoire requise : proportionnelle à n** → Espace **linéaire**

**Complexité :**

- **Temps : Linéaire (n)**
- **Espace : Linéaire (n)**

---

### Exemple 3 : Temps **Quadratique**, Espace **Constant**

Lorsque les opérations impliquent des **boucles imbriquées** où chaque boucle itère sur la taille de l'entrée n, le nombre d'opérations peut croître avec **n × n** (n au carré), conduisant à une complexité **quadratique**.

```javascript
/**
 * Vérifier s'il y a des éléments dupliqués dans un tableau
 * @param {Array} arr - Tableau à vérifier
 * @returns {boolean} true si duplicatas, false sinon
 */
function aDuplicats(arr) {
  // Soit n = arr.length

  for (let i = 0; i < arr.length; i++) {
    // Boucle externe : n fois
    for (let j = i + 1; j < arr.length; j++) {
      // Boucle interne : ~n fois
      // Comparaisons totales dans le pire cas : environ n×n / 2

      if (arr[i] === arr[j]) {
        // Comparaison + 2 accès tableau
        return true; // Sort immédiatement si duplicata trouvé
      }
    }
  }

  // Si aucun duplicata après avoir vérifié toutes les paires
  return false;
}

// Tests
console.log(aDuplicats([1, 2, 3, 4, 5])); // false
console.log(aDuplicats([1, 2, 3, 2, 5])); // true (trouvé 2)
console.log(aDuplicats(["a", "b", "c"])); // false
console.log(aDuplicats(["x", "y", "x"])); // true (trouvé x)
```

**Analyse :**

- **Temps :**
  - Boucle externe : s'exécute n fois
  - Boucle interne : s'exécute (n-1) + (n-2) + ... + 1 fois
  - Total de comparaisons `if` : environ **n² / 2**
  - À mesure que n augmente, le terme **n²** domine
  - → Temps **quadratique (n²)**

- **Espace :**
  - Variables `i` et `j` : quantité fixe
  - Aucune nouvelle structure de données créée dépendant de n
  - → Espace **constant**

**Complexité :**

- **Temps : Quadratique (n²)**
- **Espace : Constant**

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension de la complexité temporelle et spatiale, analysez les fonctions JavaScript suivantes. Pour chaque fonction, décrivez sa complexité temporelle conceptuelle et sa complexité spatiale.

---

### Exercice 1 : Trouver l'Élément Maximum

**Objectif :** Analyser les complexités d'une fonction de recherche de maximum.

**Instructions :** Analysez la complexité temporelle et spatiale de cette fonction :

```javascript
function trouverMax(nombres) {
  if (nombres.length === 0) {
    return undefined;
  }

  let maximum = nombres[0];
  for (let i = 1; i < nombres.length; i++) {
    if (nombres[i] > maximum) {
      maximum = nombres[i];
    }
  }

  return maximum;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Analyse de la Complexité Temporelle :**

1. `maximum = nombres[0]` : 1 affectation
2. Boucle : `nombres.length - 1` itérations
3. Dans chaque itération :
   - `nombres[i] > maximum` : 1 comparaison + 1 accès tableau
   - `maximum = nombres[i]` : potentiellement 1 affectation

**Total d'opérations : proportionnel à `nombres.length` (n)**

**→ Complexité temporelle : Linéaire (n)**

**Analyse de la Complexité Spatiale :**

- Variables `maximum` et `i` : quantité fixe de mémoire
- Aucune nouvelle structure de données créée dépendant de `nombres.length`

**→ Complexité spatiale : Constante**

**Résumé :**

- ⏱️ **Temps : O(n)** - Linéaire
- 💾 **Espace : O(1)** - Constant

</details>

---

### Exercice 2 : Concaténer des Chaînes dans un Tableau

**Objectif :** Comprendre la complexité de la concaténation de chaînes.

**Instructions :** Analysez cette fonction qui concatène toutes les chaînes d'un tableau :

```javascript
function concatenerChaines(chaines) {
  let resultat = "";
  for (let i = 0; i < chaines.length; i++) {
    resultat += chaines[i]; // Concaténation de chaîne
  }
  return resultat;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Analyse de la Complexité Temporelle :**

⚠️ **Attention : La concaténation de chaînes est délicate !**

- `resultat = ""` : 1 affectation
- Boucle : `chaines.length` (n) itérations
- **`resultat += chaines[i]`** : Cette opération est **coûteuse**

  En JavaScript (et dans beaucoup de langages), la concaténation de chaînes crée une **nouvelle chaîne** à chaque fois :
  - Si `resultat` a une longueur L_r et `chaines[i]` a une longueur L_s
  - Créer `resultat + chaines[i]` prend un temps proportionnel à **L_r + L_s**
  - À mesure que `resultat` grandit, cette opération devient plus lente

**Dans le pire cas :**

Si toutes les chaînes ont une longueur k :

- Itération 1 : copier k caractères
- Itération 2 : copier k + k = 2k caractères
- Itération 3 : copier 2k + k = 3k caractères
- ...
- Itération n : copier (n-1)k + k = nk caractères

**Total : k + 2k + 3k + ... + nk = k × (1 + 2 + 3 + ... + n) = k × n²/2**

**→ Complexité temporelle : Quadratique (n²)** dans le pire cas

**Analyse de la Complexité Spatiale :**

- `resultat` : Une nouvelle chaîne créée, dont la longueur finale est la somme des longueurs de toutes les chaînes
- Si chaque chaîne a une longueur k, `resultat` aura une longueur n×k

**→ Complexité spatiale : Linéaire (n)** (proportionnelle à la longueur totale)

**Résumé :**

- ⏱️ **Temps : O(n²)** - Quadratique (à cause de la concaténation répétée)
- 💾 **Espace : O(n)** - Linéaire

**💡 Meilleure Approche :**

```javascript
function concatenerChaines(chaines) {
  return chaines.join(""); // Méthode plus efficace en O(n)
}
```

</details>

---

### Exercice 3 : Somme de Toutes les Paires

**Objectif :** Analyser une fonction avec double boucle et stockage.

**Instructions :** Analysez les complexités de cette fonction :

```javascript
function sommeDePaires(nombres) {
  const paires = [];
  for (let i = 0; i < nombres.length; i++) {
    for (let j = 0; j < nombres.length; j++) {
      paires.push([nombres[i], nombres[j]]);
    }
  }
  return paires;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Analyse de la Complexité Temporelle :**

- **Boucle externe** : `nombres.length` (n) itérations
- **Boucle interne** : `nombres.length` (n) itérations pour chaque itération externe
- **`paires.push(...)`** : Exécuté n × n fois

**Total d'opérations : proportionnel à n²**

**→ Complexité temporelle : Quadratique (n²)**

**Analyse de la Complexité Spatiale :**

- `paires` : Nouveau tableau créé
- Contiendra n × n sous-tableaux (chacun avec 2 éléments)
- Nombre total d'éléments stockés : **n²**

**→ Complexité spatiale : Quadratique (n²)**

**Exemple concret :**

Si `nombres = [1, 2, 3]` (n = 3) :

```javascript
paires = [
  [1, 1],
  [1, 2],
  [1, 3],
  [2, 1],
  [2, 2],
  [2, 3],
  [3, 1],
  [3, 2],
  [3, 3],
];
// 9 paires = 3²
```

**Résumé :**

- ⏱️ **Temps : O(n²)** - Quadratique
- 💾 **Espace : O(n²)** - Quadratique

</details>

---

### Exercice 4 : Filtrer les Nombres Pairs

**Objectif :** Analyser une fonction de filtrage.

**Instructions :** Analysez les complexités de cette fonction :

```javascript
function filtrerPairs(nombres) {
  const pairs = [];
  for (let i = 0; i < nombres.length; i++) {
    if (nombres[i] % 2 === 0) {
      pairs.push(nombres[i]);
    }
  }
  return pairs;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Analyse de la Complexité Temporelle :**

- Boucle : s'exécute n fois (où n = nombres.length)
- Dans chaque itération :
  - `nombres[i]` : 1 accès
  - `nombres[i] % 2` : 1 opération modulo
  - Comparaison avec 0 : 1 comparaison
  - `push()` : parfois exécuté (temps constant)

**Total : proportionnel à n**

**→ Complexité temporelle : Linéaire (n)**

**Analyse de la Complexité Spatiale :**

- `pairs` : Nouveau tableau
- Dans le pire cas (tous les nombres sont pairs), `pairs` contiendra n éléments
- Dans le meilleur cas (aucun nombre pair), `pairs` sera vide

**→ Complexité spatiale : Linéaire (n)** dans le pire cas

**Résumé :**

- ⏱️ **Temps : O(n)** - Linéaire
- 💾 **Espace : O(n)** - Linéaire (pire cas)

</details>

---

## ✅ Quiz de Validation des Connaissances

Testez votre compréhension de cette leçon avec ce quiz !

---

### Question 1

**Qu'est-ce que la complexité temporelle mesure ?**

- [ ] A. Le temps exact en secondes qu'un algorithme prend pour s'exécuter
- [ ] B. Comment le nombre d'opérations croît en fonction de la taille de l'entrée
- [ ] C. La vitesse du processeur de l'ordinateur
- [ ] D. Le nombre de lignes de code dans la fonction

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La complexité temporelle mesure **comment le nombre d'opérations croît** à mesure que la taille de l'entrée augmente, et non le temps exact en secondes (qui dépend du matériel).

</details>

---

### Question 2

**Quelle est la différence entre complexité temporelle et complexité spatiale ?**

- [ ] A. La complexité temporelle concerne le temps, la spatiale concerne l'espace mémoire
- [ ] B. La complexité temporelle est toujours plus importante que la spatiale
- [ ] C. Elles mesurent exactement la même chose
- [ ] D. La complexité spatiale ne s'applique qu'aux tableaux

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

La **complexité temporelle** mesure le temps d'exécution (nombre d'opérations), tandis que la **complexité spatiale** mesure la mémoire utilisée.

Les deux sont importantes selon le contexte de l'application.

</details>

---

### Question 3

**Quelle est la complexité temporelle de cette fonction ?**

```javascript
function afficherElements(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}
```

- [ ] A. Constante
- [ ] B. Linéaire
- [ ] C. Quadratique
- [ ] D. Logarithmique

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La boucle s'exécute `arr.length` fois (n fois). Le nombre d'opérations croît **proportionnellement** à la taille du tableau.

**Complexité temporelle : Linéaire (n)**

</details>

---

### Question 4

**Quelle est la complexité temporelle d'une fonction avec deux boucles imbriquées qui parcourent toutes deux un tableau de taille n ?**

- [ ] A. Constante
- [ ] B. Linéaire (n)
- [ ] C. Quadratique (n²)
- [ ] D. Cubique (n³)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Deux boucles imbriquées qui parcourent chacune n éléments :

- Boucle externe : n itérations
- Boucle interne : n itérations pour chaque itération externe
- Total : n × n = **n²** opérations

**Complexité temporelle : Quadratique (n²)**

</details>

---

### Question 5

**Quelle fonction a une complexité spatiale constante ?**

- [ ] A. Une fonction qui crée un nouveau tableau de la même taille que l'entrée
- [ ] B. Une fonction qui utilise seulement quelques variables, quel que soit la taille de l'entrée
- [ ] C. Une fonction qui duplique chaque élément d'un tableau
- [ ] D. Une fonction qui stocke tous les résultats intermédiaires

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Une complexité spatiale **constante** signifie que la mémoire utilisée **ne croît pas** avec la taille de l'entrée.

Une fonction qui utilise seulement quelques variables (nombre fixe), indépendamment de la taille de l'entrée, a une complexité spatiale constante.

</details>

---

### Question 6

**Pourquoi l'efficacité algorithmique est-elle importante ? (Plusieurs réponses possibles)**

- [ ] A. Pour améliorer l'expérience utilisateur avec des applications rapides
- [ ] B. Pour permettre aux algorithmes de fonctionner avec de grandes quantités de données
- [ ] C. Pour réduire les coûts de ressources serveur
- [ ] D. Uniquement pour les applications scientifiques complexes

<details>
<summary>Voir la réponse</summary>

**Réponses : A, B, C**

L'efficacité algorithmique est importante pour :

- **Expérience utilisateur** (A) : Applications réactives et rapides
- **Scalabilité** (B) : Gérer de grandes quantités de données
- **Coûts** (C) : Moins de ressources = coûts réduits

L'option D est fausse : l'efficacité est importante pour **tous types d'applications**, pas seulement scientifiques.

</details>

---

### Question 7

**Quelle affirmation est vraie concernant la concaténation de chaînes en JavaScript ?**

- [ ] A. C'est toujours une opération à temps constant
- [ ] B. La concaténation répétée dans une boucle peut mener à une complexité quadratique
- [ ] C. Elle n'affecte jamais les performances
- [ ] D. Elle utilise toujours moins de mémoire que les tableaux

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

En JavaScript, la concaténation de chaînes avec `+=` dans une boucle crée une **nouvelle chaîne** à chaque itération. À mesure que la chaîne résultante grandit, chaque concaténation devient plus coûteuse, menant à une complexité **quadratique (n²)**.

**Exemple :**

```javascript
let resultat = "";
for (let i = 0; i < n; i++) {
  resultat += "x"; // Devient de plus en plus lent
}
```

**Meilleure approche :** Utiliser `array.join()` pour une complexité linéaire.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Efficacité Algorithmique

L'**efficacité** mesure les ressources computationnelles qu'un algorithme utilise : principalement le **temps** (complexité temporelle) et la **mémoire** (complexité spatiale).

### 2. Complexité Temporelle

Mesure **comment le nombre d'opérations croît** avec la taille de l'entrée, et non le temps exact en secondes. Focus sur le **taux de croissance**.

### 3. Complexité Spatiale

Mesure **la quantité de mémoire additionnelle** (espace auxiliaire) nécessaire, au-delà de l'entrée elle-même.

### 4. Compter les Opérations

Pour évaluer la complexité temporelle, on compte les **opérations fondamentales** : comparaisons, affectations, accès tableau, opérations arithmétiques.

### 5. Patterns de Complexité

- **Constant** : Nombre fixe d'opérations/mémoire, quel que soit n
- **Linéaire (n)** : Croissance proportionnelle à n
- **Quadratique (n²)** : Boucles imbriquées, croissance rapide

### 6. Pièges Courants

- **Concaténation de chaînes** répétée : Peut causer une complexité quadratique
- **Boucles imbriquées** : Attention à la multiplication des itérations
- **Création de structures** : Les nouveaux tableaux/objets augmentent la complexité spatiale

### 7. Pourquoi c'est Important

- **Expérience utilisateur** : Applications rapides et réactives
- **Scalabilité** : Gérer de grandes quantités de données
- **Coûts** : Optimisation des ressources serveur
- **Performance** : Logiciels efficaces et professionnels

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous venez de franchir une étape cruciale dans votre compréhension des algorithmes !

### Ce que vous avez appris aujourd'hui

Vous comprenez désormais que **l'efficacité algorithmique** ne se limite pas à écrire du code qui fonctionne, mais à écrire du code qui **performe** bien. Vous avez acquis les compétences suivantes :

- Comprendre la différence entre complexité temporelle et spatiale
- Compter les opérations fondamentales d'un algorithme
- Analyser la mémoire utilisée par un algorithme
- Identifier les patterns de complexité (constant, linéaire, quadratique)
- Reconnaître les pièges de performance courants

### Compétences acquises

Vous êtes maintenant capable de :

- Analyser conceptuellement l'efficacité de vos algorithmes
- Comparer différentes approches pour résoudre un problème
- Identifier les goulots d'étranglement de performance
- Prédire comment un algorithme se comportera avec de grandes données

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Comprendre l'efficacité algorithmique est la **fondation** pour devenir un développeur compétent. Cela vous permet de passer de "mon code fonctionne" à "mon code fonctionne **et** performe bien, même avec des millions d'utilisateurs". Cette compétence est essentielle pour construire des applications **scalables** et offrir une **excellente expérience utilisateur**.

### La prochaine étape

Dans la prochaine leçon, nous formaliserons ces concepts avec la **notation Big O**, qui fournit un langage mathématique standard pour décrire la complexité des algorithmes. Vous apprendrez à exprimer ces complexités de manière rigoureuse et universelle.

---

## ➡️ Prochaine Étape : Leçon 4

### Ce qui vous attend

Vous avez une idée intuitive de la complexité. La prochaine leçon, **« Comprendre la Notation Big O avec des Exemples Pratiques »**, vous donnera un langage standard pour la décrire.

**Vous découvrirez :**

- Le rôle et la définition de la notation **Big O**.
- Les complexités courantes comme **O(1)**, **O(n)**, et **O(n²)** avec des exemples visuels.
- Les règles de simplification pour ignorer les détails et se concentrer sur l'essentiel.

### Préparez-vous !

La notation Big O est le standard de l'industrie pour discuter de la performance des algorithmes. La maîtriser est indispensable pour tout développeur sérieux.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Complexité algorithmique expliquée - Khan Academy](https://fr.khanacademy.org/computing/computer-science/algorithms) - Cours interactif gratuit
- [Visualgo - Visualisation d'algorithmes](https://visualgo.net/fr) - Voir les algorithmes en action
- [JavaScript Algorithms Repository](https://github.com/trekhleb/javascript-algorithms) - Implémentations d'algorithmes en JavaScript

### Outils de pratique

- **[JSBench.me](https://jsbench.me/)** : Comparer les performances de différents codes JavaScript
- **[Replit](https://replit.com/)** : Tester vos algorithmes en ligne

### Livres recommandés

- **"Grokking Algorithms"** de Aditya Bhargava - Introduction visuelle aux algorithmes (disponible en français : "Les Algorithmes pour les Nuls")

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques et micro-exercices
- Expérimenter avec les exemples dans votre console
- Modifier les exemples pour tester différentes tailles d'entrée

> 💡 **Conseil**
>
> Pour bien maîtriser la complexité algorithmique, **pratiquez le comptage d'opérations** sur du code que vous écrivez au quotidien. Demandez-vous toujours : "Comment cette fonction va-t-elle se comporter si mes données sont 10× ou 100× plus grandes ?"

---

**Prêt pour la Leçon 4 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir la notation Big O et formaliser tout ce que vous venez d'apprendre !

---

<div align="center">

**Leçon 3 sur 42 - Module 1 : Fondements des algorithmes et révision de JavaScript**

[⬅️ Leçon 2 : Introduction à JavaScript](./lecon-2-introduction-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 4 : Notation Big O ➡️](./lecon-4-notation-big-o.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
