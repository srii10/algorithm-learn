##### Leçon 21 sur 42

# Introduction à la Récursion : Cas de Base et Appels Récursifs

**Module 4** : Algorithmes de Recherche et Introduction à la Récursion

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **concept fondamental** de la récursion : une fonction qui s'appelle elle-même
- Identifier et définir le **cas de base** qui termine la récursion
- Concevoir des **appels récursifs** qui réduisent progressivement le problème
- Tracer l'**exécution pas à pas** d'une fonction récursive
- Reconnaître les **erreurs courantes** comme les boucles infinies et le stack overflow
- Implémenter des fonctions récursives simples comme la **factorielle** et la **somme de tableau**

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçons 19-20 complétées** : Maîtriser les algorithmes de recherche linéaire et binaire
- **Module 1 complété** : Comprendre les fonctions JavaScript et leur fonctionnement
- **Concepts de base** : Savoir ce qu'est une pile (stack) et comment fonctionne la mémoire
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Se Regarder dans un Miroir Face à un Miroir

Avez-vous déjà placé deux miroirs face à face ? L'image se répète à l'infini, chaque reflet contenant un reflet plus petit. C'est exactement le principe de la **récursion** en programmation !

La **récursion** est une technique où une fonction **s'appelle elle-même** pour résoudre un problème. Cela peut sembler étrange au premier abord - comment une fonction peut-elle utiliser sa propre définition pour se définir ? C'est comme définir le mot "récursion" par : "voir récursion".

Mais ne vous inquiétez pas ! La clé réside dans deux éléments essentiels :

- Le **cas de base** : La condition qui arrête la récursion (sinon, elle continuerait à l'infini comme les miroirs !)
- L'**appel récursif** : L'appel de la fonction sur une version **plus petite** du problème

La récursion est omniprésente en informatique :

- **Structures de données** : Arbres, graphes, listes chaînées
- **Algorithmes** : Tri fusion, tri rapide, recherche binaire
- **Mathématiques** : Factorielle, suite de Fibonacci, fractales
- **Systèmes de fichiers** : Parcourir des dossiers et sous-dossiers

> **Point Clé**
>
> La récursion transforme un problème complexe en une série de problèmes identiques mais plus simples. Au lieu de résoudre le problème entier d'un coup, on résout la plus petite version possible (cas de base), puis on construit la solution en remontant.

---

## 📦 Le Cas de Base : La Clé pour Arrêter la Récursion

Le **cas de base** est la condition qui termine le processus récursif. Sans cas de base, une fonction récursive s'appellerait indéfiniment, causant une **erreur de débordement de pile** (stack overflow).

---

### Pourquoi le Cas de Base est-il Essentiel ?

Imaginez que vous descendez un escalier. Le cas de base, c'est le rez-de-chaussée : quand vous y arrivez, vous arrêtez de descendre. Sans rez-de-chaussée, vous descendriez... à l'infini !

```javascript
// DANGER : Fonction sans cas de base - boucle infinie !
function compteurInfini(n) {
  console.log(n);
  compteurInfini(n - 1); // S'appelle toujours, jamais d'arrêt !
}
// compteurInfini(5); // NE PAS EXÉCUTER - causera un stack overflow !

// CORRECT : Fonction avec cas de base
function compteur(n) {
  // Cas de base : quand n atteint 0, on s'arrête
  if (n <= 0) {
    console.log("Décollage !");
    return; // ARRÊT de la récursion
  }
  console.log(n);
  compteur(n - 1); // Appel récursif avec n plus petit
}

compteur(5);
// Affiche : 5, 4, 3, 2, 1, Décollage !
```

---

### Identifier le Cas de Base

Pour identifier un cas de base, posez-vous la question : **"Quelle est la version la plus simple du problème que je peux résoudre directement ?"**

**Exemples de cas de base :**

| Problème              | Cas de Base        | Raison                           |
| --------------------- | ------------------ | -------------------------------- |
| Factorielle de n      | n === 0 ou n === 1 | 0! = 1 et 1! = 1 par définition  |
| Somme d'un tableau    | Tableau vide       | La somme d'aucun élément est 0   |
| Longueur d'une chaîne | Chaîne vide        | Une chaîne vide a 0 caractères   |
| Recherche binaire     | low > high         | L'espace de recherche est épuisé |

---

### Exemple 1 : La Factorielle

La **factorielle** de n (notée n!) est le produit de tous les entiers de 1 à n :

```
5! = 5 × 4 × 3 × 2 × 1 = 120
4! = 4 × 3 × 2 × 1 = 24
3! = 3 × 2 × 1 = 6
2! = 2 × 1 = 2
1! = 1
0! = 1 (par définition mathématique)
```

**Quel est le cas de base ?**

- Le cas le plus simple est **0! = 1** ou **1! = 1**
- Ce sont des valeurs connues directement, sans calcul supplémentaire

```javascript
function factorielle(n) {
  // Cas de base : 0! = 1 (par définition mathématique)
  if (n === 0) {
    return 1;
  }
  // L'appel récursif sera ajouté plus tard...
}
```

---

### Exemple 2 : Somme d'un Tableau

**Quel est le cas de base pour calculer la somme d'un tableau ?**

- Un tableau **vide** a une somme de **0**
- Un tableau d'**un seul élément** a une somme égale à cet élément

```javascript
function sommeTableau(tableau) {
  // Cas de base 1 : tableau vide → somme = 0
  if (tableau.length === 0) {
    return 0;
  }
  // Cas de base 2 (optionnel) : un seul élément → retourner cet élément
  if (tableau.length === 1) {
    return tableau[0];
  }
  // L'appel récursif sera ajouté plus tard...
}
```

---

## 📝 Micro-Exercice #1 : Identifier les Cas de Base

**Objectif :** Reconnaître les cas de base appropriés pour différents problèmes.

**Instructions :** Pour chaque problème, identifiez le cas de base approprié.

1. **Inverser une chaîne de caractères** (`"bonjour"` → `"ruojnob"`)
2. **Compter les éléments d'une liste chaînée**
3. **Calculer la puissance** `x^n` (x élevé à la puissance n)

<details>
<summary>💡 Voir la solution</summary>

1. **Inverser une chaîne** :
   - Cas de base : Chaîne vide (`""`) ou chaîne d'un caractère (`"a"`)
   - Raison : Une chaîne vide inversée est vide, un caractère seul est déjà "inversé"

2. **Compter les éléments d'une liste chaînée** :
   - Cas de base : Nœud null (fin de la liste)
   - Raison : Quand on atteint la fin, on a compté 0 éléments supplémentaires

3. **Calculer x^n** :
   - Cas de base : n === 0
   - Raison : x^0 = 1 pour tout x (par définition mathématique)

**Explication :** Le cas de base est toujours la version la plus simple du problème, celle qu'on peut résoudre sans aucun calcul supplémentaire ou appel récursif.

</details>

---

## 🔄 L'Appel Récursif : Réduire le Problème

L'**appel récursif** est la partie où la fonction s'appelle elle-même avec une entrée **modifiée** et **plus petite**. Chaque appel doit se rapprocher du cas de base.

---

### Conception de l'Appel Récursif

Chaque appel récursif fait typiquement deux choses :

1. **Effectue un travail** sur l'entrée actuelle
2. **S'appelle** avec une entrée modifiée plus proche du cas de base

---

### La Relation Récursive de la Factorielle

Pour n!, nous savons que :

```
n! = n × (n-1)!

Par exemple :
5! = 5 × 4!
4! = 4 × 3!
3! = 3 × 2!
2! = 2 × 1!
1! = 1 × 0!
0! = 1 (cas de base)
```

Cette formule montre la **relation récursive** :

- Le **travail actuel** : multiplier par n
- L'**appel récursif** : `factorielle(n - 1)` (problème plus petit)

---

### Traçage de factorielle(3)

Suivons l'exécution pas à pas :

```
factorielle(3) appelle 3 × factorielle(2)
                              │
                              ↓
                        factorielle(2) appelle 2 × factorielle(1)
                                                      │
                                                      ↓
                                                factorielle(1) appelle 1 × factorielle(0)
                                                                              │
                                                                              ↓
                                                                        factorielle(0)
                                                                        Cas de base ! → retourne 1
                                                                              │
                                                                              ↑
                                                factorielle(1) reçoit 1, calcule 1 × 1 = 1 → retourne 1
                                                      │
                                                      ↑
                        factorielle(2) reçoit 1, calcule 2 × 1 = 2 → retourne 2
                              │
                              ↑
factorielle(3) reçoit 2, calcule 3 × 2 = 6 → retourne 6

Résultat final : 6
```

**Visualisation en tableau :**

| Appel          | n   | Action             | Résultat retourné |
| -------------- | --- | ------------------ | ----------------- |
| factorielle(3) | 3   | 3 × factorielle(2) | 3 × 2 = **6**     |
| factorielle(2) | 2   | 2 × factorielle(1) | 2 × 1 = **2**     |
| factorielle(1) | 1   | 1 × factorielle(0) | 1 × 1 = **1**     |
| factorielle(0) | 0   | Cas de base        | **1**             |

---

### La Relation Récursive de la Somme de Tableau

Pour un tableau `[5, 3, 8, 2]` :

```
somme([5, 3, 8, 2]) = 5 + somme([3, 8, 2])
                        = 5 + (3 + somme([8, 2]))
                        = 5 + (3 + (8 + somme([2])))
                        = 5 + (3 + (8 + (2 + somme([]))))
                        = 5 + (3 + (8 + (2 + 0)))  ← cas de base
                        = 5 + (3 + (8 + 2))
                        = 5 + (3 + 10)
                        = 5 + 13
                        = 18
```

**Relation récursive :**

- **Travail actuel** : prendre le premier élément
- **Appel récursif** : `somme(reste du tableau)`

---

## 📝 Micro-Exercice #2 : Concevoir l'Appel Récursif

**Objectif :** Formuler la relation récursive pour différents problèmes.

**Instructions :** Pour chaque problème, écrivez la relation récursive.

1. **Longueur d'une chaîne** : Comment exprimer `longueur("bonjour")` récursivement ?
2. **Puissance x^n** : Comment exprimer `puissance(2, 5)` récursivement ?

<details>
<summary>💡 Voir la solution</summary>

1. **Longueur d'une chaîne** :

   ```
   longueur("") = 0                          // Cas de base
   longueur("bonjour") = 1 + longueur("onjour")  // Appel récursif

   // Relation générale :
   longueur(chaine) = 1 + longueur(chaine sans le premier caractère)
   ```

2. **Puissance x^n** :

   ```
   puissance(x, 0) = 1                       // Cas de base : x^0 = 1
   puissance(2, 5) = 2 × puissance(2, 4)     // Appel récursif

   // Relation générale :
   puissance(x, n) = x × puissance(x, n-1)
   ```

**Explication :** La relation récursive exprime toujours le problème en termes d'une version plus petite de lui-même, plus un travail simple à effectuer.

</details>

---

## 💻 Implémentation en JavaScript

Maintenant que nous comprenons les concepts, implémentons des fonctions récursives complètes.

---

### La Fonction Factorielle

```javascript
/**
 * Calcule la factorielle d'un nombre n de manière récursive.
 * @param {number} n - Un entier non négatif.
 * @returns {number} - La factorielle de n (n!).
 */
function factorielle(n) {
  // Validation de l'entrée
  if (n < 0) {
    throw new Error(
      "La factorielle n'est pas définie pour les nombres négatifs.",
    );
  }

  // Cas de base : 0! = 1 (par définition mathématique)
  // C'est la condition qui arrête la récursion
  if (n === 0) {
    return 1;
  }

  // Appel récursif : n! = n × (n-1)!
  // La fonction s'appelle avec n-1, se rapprochant du cas de base
  return n * factorielle(n - 1);
}

// Tests
console.log("Factorielle de 5 :", factorielle(5)); // 120
console.log("Factorielle de 4 :", factorielle(4)); // 24
console.log("Factorielle de 3 :", factorielle(3)); // 6
console.log("Factorielle de 1 :", factorielle(1)); // 1
console.log("Factorielle de 0 :", factorielle(0)); // 1
```

**Analyse du code :**

1. **Validation** : On vérifie que n n'est pas négatif
2. **Cas de base** : `if (n === 0) return 1` - arrête la récursion
3. **Appel récursif** : `n * factorielle(n - 1)` - réduit le problème

---

### La Fonction Somme de Tableau

```javascript
/**
 * Calcule la somme des éléments d'un tableau de manière récursive.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - La somme de tous les éléments.
 */
function sommeTableau(tableau) {
  // Cas de base 1 : tableau vide → somme = 0
  // Un tableau sans éléments a une somme de zéro
  if (tableau.length === 0) {
    return 0;
  }

  // Cas de base 2 (optionnel) : un seul élément → retourner cet élément
  // Améliore la clarté conceptuelle
  if (tableau.length === 1) {
    return tableau[0];
  }

  // Appel récursif : premier élément + somme du reste
  // slice(1) crée un nouveau tableau sans le premier élément
  const premierElement = tableau[0];
  const resteTableau = tableau.slice(1);

  return premierElement + sommeTableau(resteTableau);
}

// Tests avec des valeurs en français
const notes = [15, 18, 12, 16, 14]; // Notes d'un élève
console.log("Somme des notes :", sommeTableau(notes)); // 75

const prix = [25, 30, 15]; // Prix en euros
console.log("Total des prix :", sommeTableau(prix)); // 70

console.log("Somme tableau vide :", sommeTableau([])); // 0
console.log("Somme un élément :", sommeTableau([42])); // 42
```

**Analyse du code :**

1. **Cas de base 1** : Tableau vide → retourne 0
2. **Cas de base 2** : Un seul élément → retourne cet élément
3. **Appel récursif** : `premier + somme(reste)` avec `slice(1)` pour réduire

---

### Visualisation de sommeTableau([5, 3, 8])

```
sommeTableau([5, 3, 8])
│
├── premierElement = 5
├── resteTableau = [3, 8]
└── return 5 + sommeTableau([3, 8])
                      │
                      ├── premierElement = 3
                      ├── resteTableau = [8]
                      └── return 3 + sommeTableau([8])
                                            │
                                            └── Cas de base : length === 1
                                                return 8
                                            │
                      └── return 3 + 8 = 11
                      │
└── return 5 + 11 = 16

Résultat : 16
```

---

## 📝 Micro-Exercice #3 : Implémenter une Fonction Récursive

**Objectif :** Mettre en pratique les concepts de cas de base et d'appel récursif.

**Instructions :** Implémentez une fonction `compteARebours(n)` qui affiche les nombres de n à 1, puis affiche "Décollage !".

```javascript
// Exemple d'utilisation :
compteARebours(5);
// Affiche : 5, 4, 3, 2, 1, Décollage !
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Affiche un compte à rebours de n à 1, puis "Décollage !".
 * @param {number} n - Le nombre de départ du compte à rebours.
 */
function compteARebours(n) {
  // Cas de base : quand n atteint 0, on affiche "Décollage !"
  if (n <= 0) {
    console.log("Décollage !");
    return; // Important : arrêter la récursion
  }

  // Afficher le nombre actuel
  console.log(n);

  // Appel récursif avec n-1 (se rapproche du cas de base)
  compteARebours(n - 1);
}

// Test
compteARebours(5);
// Affiche :
// 5
// 4
// 3
// 2
// 1
// Décollage !
```

**Explication :**

- **Cas de base** : `n <= 0` - on arrête et affiche "Décollage !"
- **Travail actuel** : `console.log(n)` - afficher le nombre
- **Appel récursif** : `compteARebours(n - 1)` - réduire n de 1

</details>

---

## 💻 Application Pratique : Étude de Cas

Appliquons la récursion à des problèmes concrets.

---

### Exemple 1 : Inverser une Chaîne de Caractères

Inversons la chaîne `"bonjour"` pour obtenir `"ruojnob"` :

```javascript
/**
 * Inverse une chaîne de caractères de manière récursive.
 * @param {string} chaine - La chaîne à inverser.
 * @returns {string} - La chaîne inversée.
 */
function inverserChaine(chaine) {
  // Cas de base : chaîne vide ou un seul caractère
  // Une chaîne vide ou d'un caractère est déjà "inversée"
  if (chaine.length <= 1) {
    return chaine;
  }

  // Appel récursif :
  // Prendre le premier caractère et le mettre à la fin
  // de la chaîne inversée du reste
  const premierCaractere = chaine[0];
  const reste = chaine.slice(1);

  return inverserChaine(reste) + premierCaractere;
}

// Tests avec des mots français
console.log(inverserChaine("bonjour")); // "ruojnob"
console.log(inverserChaine("pomme")); // "emmop"
console.log(inverserChaine("radar")); // "radar" (palindrome !)
console.log(inverserChaine("a")); // "a"
console.log(inverserChaine("")); // ""
```

**Traçage de `inverserChaine("abc")` :**

```
inverserChaine("abc")
  → inverserChaine("bc") + "a"
      → inverserChaine("c") + "b"
          → "c" (cas de base)
      → "c" + "b" = "cb"
  → "cb" + "a" = "cba"

Résultat : "cba"
```

---

### Exemple 2 : Calculer la Puissance

Calculons x^n de manière récursive :

```javascript
/**
 * Calcule x élevé à la puissance n de manière récursive.
 * @param {number} base - La base (x).
 * @param {number} exposant - L'exposant (n), doit être >= 0.
 * @returns {number} - Le résultat de x^n.
 */
function puissance(base, exposant) {
  // Validation
  if (exposant < 0) {
    throw new Error("L'exposant doit être positif ou nul.");
  }

  // Cas de base : x^0 = 1 pour tout x
  if (exposant === 0) {
    return 1;
  }

  // Appel récursif : x^n = x × x^(n-1)
  return base * puissance(base, exposant - 1);
}

// Tests
console.log("2^5 =", puissance(2, 5)); // 32
console.log("3^4 =", puissance(3, 4)); // 81
console.log("5^0 =", puissance(5, 0)); // 1
console.log("10^3 =", puissance(10, 3)); // 1000
```

**Traçage de `puissance(2, 4)` :**

| Appel           | base | exposant | Calcul              | Résultat       |
| --------------- | ---- | -------- | ------------------- | -------------- |
| puissance(2, 4) | 2    | 4        | 2 × puissance(2, 3) | 2 × 8 = **16** |
| puissance(2, 3) | 2    | 3        | 2 × puissance(2, 2) | 2 × 4 = **8**  |
| puissance(2, 2) | 2    | 2        | 2 × puissance(2, 1) | 2 × 2 = **4**  |
| puissance(2, 1) | 2    | 1        | 2 × puissance(2, 0) | 2 × 1 = **2**  |
| puissance(2, 0) | 2    | 0        | Cas de base         | **1**          |

---

### Exemple 3 : Compter les Éléments d'une Liste

Comptons le nombre d'éléments dans une liste (sans utiliser `.length`) :

```javascript
/**
 * Compte le nombre d'éléments dans un tableau de manière récursive.
 * @param {Array<any>} liste - Le tableau à compter.
 * @returns {number} - Le nombre d'éléments.
 */
function compterElements(liste) {
  // Cas de base : liste vide → 0 éléments
  if (liste.length === 0) {
    return 0;
  }

  // Appel récursif : 1 (pour l'élément actuel) + compter le reste
  return 1 + compterElements(liste.slice(1));
}

// Tests avec des listes françaises
const fruits = ["pomme", "banane", "orange", "fraise"];
console.log("Nombre de fruits :", compterElements(fruits)); // 4

const prenoms = ["Chermann", "Ingrid", "Prudence", "Germain"];
console.log("Nombre de prénoms :", compterElements(prenoms)); // 4

console.log("Liste vide :", compterElements([])); // 0
```

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension de la récursion, implémentez les problèmes suivants.

---

### Exercice 1 : Compte à Rebours

**Objectif :** Implémenter un compte à rebours récursif.

**Instructions :** Écrivez une fonction `compteARebours(n)` qui affiche les nombres de n à 1, puis "Décollage !".

```javascript
// Exemple d'utilisation :
compteARebours(3);
// Affiche : 3, 2, 1, Décollage !
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function compteARebours(n) {
  // Cas de base : quand n atteint 0
  if (n <= 0) {
    console.log("Décollage !");
    return;
  }

  // Afficher le nombre actuel
  console.log(n);

  // Appel récursif
  compteARebours(n - 1);
}

// Test
compteARebours(3);
// 3
// 2
// 1
// Décollage !
```

</details>

---

### Exercice 2 : Inverser une Chaîne

**Objectif :** Inverser une chaîne de caractères récursivement.

**Instructions :** Implémentez `inverserChaine(chaine)` qui retourne la chaîne inversée.

```javascript
// Exemple :
inverserChaine("bonjour"); // "ruojnob"
inverserChaine("kayak"); // "kayak" (palindrome)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function inverserChaine(chaine) {
  // Cas de base : chaîne vide ou un caractère
  if (chaine.length <= 1) {
    return chaine;
  }

  // Appel récursif : inverser le reste + premier caractère à la fin
  return inverserChaine(chaine.slice(1)) + chaine[0];
}

// Tests
console.log(inverserChaine("bonjour")); // "ruojnob"
console.log(inverserChaine("kayak")); // "kayak"
console.log(inverserChaine("a")); // "a"
console.log(inverserChaine("")); // ""
```

**Explication :**

- On prend le premier caractère et on le place à la fin
- On inverse récursivement le reste de la chaîne
- Le cas de base arrête quand il reste 0 ou 1 caractère

</details>

---

### Exercice 3 : Vérifier un Palindrome

**Objectif :** Déterminer si une chaîne est un palindrome (se lit pareil dans les deux sens).

**Instructions :** Implémentez `estPalindrome(chaine)` qui retourne `true` ou `false`.

```javascript
// Exemples :
estPalindrome("radar"); // true
estPalindrome("kayak"); // true
estPalindrome("bonjour"); // false
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function estPalindrome(chaine) {
  // Normaliser : minuscules et sans espaces
  const chaineNormalisee = chaine.toLowerCase().replace(/\s/g, "");

  // Cas de base : chaîne de 0 ou 1 caractère
  if (chaineNormalisee.length <= 1) {
    return true;
  }

  // Vérifier si premier et dernier caractères sont identiques
  const premier = chaineNormalisee[0];
  const dernier = chaineNormalisee[chaineNormalisee.length - 1];

  if (premier !== dernier) {
    return false;
  }

  // Appel récursif : vérifier la chaîne sans le premier et dernier caractère
  const milieu = chaineNormalisee.slice(1, -1);
  return estPalindrome(milieu);
}

// Tests
console.log(estPalindrome("radar")); // true
console.log(estPalindrome("kayak")); // true
console.log(estPalindrome("bonjour")); // false
console.log(estPalindrome("Été")); // false (à cause des accents)
console.log(estPalindrome("a")); // true
```

**Explication :**

- On compare le premier et le dernier caractère
- S'ils sont différents, ce n'est pas un palindrome
- S'ils sont identiques, on vérifie récursivement le reste (sans ces deux caractères)

</details>

---

### Exercice 4 : Somme des Chiffres

**Objectif :** Calculer la somme des chiffres d'un nombre.

**Instructions :** Implémentez `sommeChiffres(n)` qui retourne la somme des chiffres.

```javascript
// Exemples :
sommeChiffres(123); // 1 + 2 + 3 = 6
sommeChiffres(9876); // 9 + 8 + 7 + 6 = 30
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function sommeChiffres(n) {
  // Assurer que n est positif
  n = Math.abs(n);

  // Cas de base : un seul chiffre (n < 10)
  if (n < 10) {
    return n;
  }

  // Appel récursif :
  // Dernier chiffre (n % 10) + somme des chiffres restants (n / 10)
  const dernierChiffre = n % 10;
  const resteNombre = Math.floor(n / 10);

  return dernierChiffre + sommeChiffres(resteNombre);
}

// Tests
console.log(sommeChiffres(123)); // 6
console.log(sommeChiffres(9876)); // 30
console.log(sommeChiffres(5)); // 5
console.log(sommeChiffres(10000)); // 1
```

**Explication :**

- `n % 10` donne le dernier chiffre (ex: 123 % 10 = 3)
- `Math.floor(n / 10)` enlève le dernier chiffre (ex: 123 / 10 = 12)
- On additionne récursivement jusqu'à n'avoir qu'un seul chiffre

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Qu'est-ce que la récursion en programmation ?**

- [ ] A. Une boucle for qui s'exécute plusieurs fois
- [ ] B. Une fonction qui s'appelle elle-même
- [ ] C. Un type de variable spécial
- [ ] D. Une erreur de programmation

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La récursion est une technique où une **fonction s'appelle elle-même** pour résoudre un problème en le décomposant en sous-problèmes plus simples.

</details>

---

### Question 2

**Quel est le rôle du cas de base dans une fonction récursive ?**

- [ ] A. Accélérer l'exécution
- [ ] B. Arrêter la récursion pour éviter une boucle infinie
- [ ] C. Démarrer la récursion
- [ ] D. Calculer le résultat final

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le cas de base est la condition qui **arrête la récursion**. Sans lui, la fonction s'appellerait indéfiniment, causant un stack overflow (débordement de pile).

</details>

---

### Question 3

**Quel est le cas de base approprié pour la fonction factorielle ?**

- [ ] A. n === 10
- [ ] B. n === 0 ou n === 1
- [ ] C. n < 0
- [ ] D. n > 100

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le cas de base pour la factorielle est **n === 0** (car 0! = 1 par définition) ou **n === 1** (car 1! = 1). Ces valeurs peuvent être retournées directement sans calcul supplémentaire.

</details>

---

### Question 4

**Que se passe-t-il si une fonction récursive n'a pas de cas de base ?**

- [ ] A. Elle retourne undefined
- [ ] B. Elle s'exécute une seule fois
- [ ] C. Elle cause un stack overflow (débordement de pile)
- [ ] D. Elle s'exécute plus rapidement

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Sans cas de base, la fonction s'appelle indéfiniment, remplissant la pile d'appels jusqu'à ce qu'elle déborde (**stack overflow**). C'est une erreur fatale qui arrête le programme.

</details>

---

### Question 5

**Dans la relation récursive `n! = n × (n-1)!`, quelle partie représente l'appel récursif ?**

- [ ] A. n!
- [ ] B. n ×
- [ ] C. (n-1)!
- [ ] D. =

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

L'appel récursif est **(n-1)!** car c'est là que la fonction s'appelle elle-même avec une valeur plus petite. `n ×` est le travail effectué à chaque étape.

</details>

---

### Question 6

**Pour calculer la somme d'un tableau récursivement, quel est le cas de base le plus approprié ?**

- [ ] A. Le tableau contient 100 éléments
- [ ] B. Le tableau est trié
- [ ] C. Le tableau est vide
- [ ] D. Le premier élément est 0

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le cas de base est un **tableau vide**, car sa somme est simplement **0**. C'est la version la plus simple du problème qui peut être résolue directement.

</details>

---

### Question 7

**Quelle affirmation est VRAIE concernant l'appel récursif ?**

- [ ] A. Il doit toujours retourner le même résultat
- [ ] B. Il doit travailler sur une version plus petite du problème
- [ ] C. Il doit être placé au début de la fonction
- [ ] D. Il ne peut être appelé qu'une seule fois

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

L'appel récursif doit toujours travailler sur une **version plus petite** du problème, se rapprochant ainsi du cas de base. Sans cette réduction, la récursion ne se terminerait jamais.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Définition de la Récursion

La récursion est une technique où une fonction s'appelle elle-même pour résoudre un problème en le décomposant en sous-problèmes identiques mais plus simples.

### 2. Le Cas de Base

Le cas de base est la condition qui arrête la récursion. Il représente la version la plus simple du problème, résolue directement sans appel récursif.

### 3. L'Appel Récursif

L'appel récursif est l'appel de la fonction sur une version plus petite du problème. Chaque appel doit se rapprocher du cas de base.

### 4. Sans Cas de Base = Stack Overflow

Une fonction récursive sans cas de base s'appelle indéfiniment, remplissant la pile d'appels jusqu'au débordement (stack overflow).

### 5. Relation Récursive

La relation récursive exprime le problème en termes de lui-même : `factorielle(n) = n × factorielle(n-1)`.

### 6. Traçage de l'Exécution

Pour comprendre une fonction récursive, tracez les appels en descendant vers le cas de base, puis remontez en collectant les résultats.

### 7. Applications

La récursion est utilisée pour : factorielle, somme de tableau, inversion de chaîne, parcours d'arbres, algorithmes de tri (fusion, rapide).

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez franchi une étape majeure en maîtrisant les fondements de la récursion.

### Ce que vous avez appris aujourd'hui

- Le concept de récursion : une fonction qui s'appelle elle-même
- L'importance cruciale du cas de base pour éviter les boucles infinies
- La conception d'appels récursifs qui réduisent progressivement le problème
- L'implémentation de fonctions récursives simples (factorielle, somme, inversion)
- Le traçage pas à pas de l'exécution récursive

### Compétences acquises

Vous êtes maintenant capable de :

- Identifier le cas de base approprié pour un problème
- Formuler la relation récursive qui décompose le problème
- Implémenter des fonctions récursives simples en JavaScript

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La récursion n'est pas qu'une technique de programmation - c'est une **façon de penser**. Elle vous apprend à décomposer des problèmes complexes en parties plus simples. Cette compétence est fondamentale pour comprendre les structures de données avancées (arbres, graphes) et les algorithmes efficaces (tri fusion, tri rapide, recherche binaire récursive). Maîtriser la récursion, c'est maîtriser l'art de la résolution de problèmes.

---

## ➡️ Prochaine Étape : Leçon 22

### Ce qui vous attend

La prochaine leçon, **« Implémentation de Fonctions Récursives de Base en JavaScript »**, approfondira vos compétences avec des patterns récursifs plus avancés.

**Vous découvrirez :**

- La **récursion multiple** : quand une fonction s'appelle plusieurs fois (Fibonacci)
- La **récursion avec accumulateur** pour optimiser les performances
- Des patterns récursifs pour le **traitement de chaînes et tableaux**
- La **recherche binaire récursive** comparée à la version itérative

### Préparez-vous !

Vous allez passer de la compréhension à la maîtrise, en explorant des patterns récursifs qui vous permettront de résoudre des problèmes de plus en plus complexes avec élégance.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Recursion](https://visualgo.net/en/recursion) - Visualisation interactive de la récursion
- [MDN - Recursion](https://developer.mozilla.org/fr/docs/Glossary/Recursion) - Documentation MDN sur la récursion
- [FreeCodeCamp - Recursion](https://www.freecodecamp.org/news/recursion-in-javascript/) - Tutoriel approfondi

### Outils de pratique

- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez la pile d'appels récursifs
- **[Recursion Visualizer](https://recursion.vercel.app/)** : Outil pour visualiser les appels récursifs

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> La récursion peut sembler déroutante au début. Le meilleur moyen de la comprendre est de **tracer les appels à la main**. Prenez une feuille de papier, écrivez chaque appel récursif avec ses paramètres, descendez jusqu'au cas de base, puis remontez en calculant les résultats. Cette visualisation rendra la récursion beaucoup plus intuitive !

---

**Prêt pour la Leçon 22 ?** 🚀

Rendez-vous dans la prochaine leçon pour approfondir vos compétences récursives !

---

<div align="center">

**Leçon 21 sur 42 - Module 4 : Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Leçon 20 : Recherche Binaire : Recherche Efficace dans les Tableaux Triés](./lecon-2-recherche-binaire-recherche-efficace-tableaux-tries.md) | [Retour au sommaire](./README.md) | [Leçon 22 : Implémentation de Fonctions Récursives de Base en JavaScript ➡️](./lecon-4-implementation-fonctions-recursives-base-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
