##### Leçon 38 sur 42

# Patterns Courants de Résolution de Problèmes Algorithmiques

**Module 7** : Applications d'Algorithmes et Résolution de Problèmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Reconnaître et appliquer les patterns classiques de résolution de problèmes (deux pointeurs, fenêtre glissante, fast & slow pointers, fusion d'intervalles)
- Choisir le pattern adapté selon la structure du problème
- Identifier les pièges et cas limites de chaque pattern
- Adapter chaque pattern à des cas concrets en JavaScript
- Naviguer efficacement entre les patterns pour résoudre des problèmes variés

---

### ⏱️ Durée estimée : 3h-3h30

---

## 📚 Prérequis

- Maîtrise des bases de JavaScript
- Savoir manipuler tableaux, chaînes, listes chaînées
- Avoir suivi les modules précédents (tri, recherche, DP, glouton)
- Comprendre la notation Big O (complexité temporelle et spatiale)

---

## 🚀 Introduction

Résoudre des problèmes algorithmiques efficacement, c'est souvent reconnaître des **patterns récurrents**. Ces schémas de pensée permettent d'aborder une grande variété de problèmes sans repartir de zéro à chaque fois. Maîtriser ces patterns, c'est gagner en rapidité, en clarté et en robustesse.

**Point Clé** : Les patterns algorithmiques sont des **modèles de résolution** éprouvés qui transforment des problèmes en apparence complexes en solutions élégantes et optimales. Chaque pattern a une **complexité caractéristique** (Big O) et s'applique à des structures de données spécifiques. Reconnaître le bon pattern, c'est souvent la différence entre une solution en O(n²) et une solution en O(n).

Dans cette leçon, nous allons explorer **4 patterns fondamentaux** qui couvrent la majorité des problèmes d'entretiens techniques et de compétitions algorithmiques :

1. **Two Pointers** (Deux Pointeurs) - O(n) sur données triées
2. **Sliding Window** (Fenêtre Glissante) - O(n) pour sous-tableaux contigus
3. **Fast & Slow Pointers** (Lièvre & Tortue) - O(n) pour listes chaînées
4. **Merge Intervals** (Fusion d'Intervalles) - O(n log n) pour intervalles

---

## 🧩 Pattern 1 : Deux Pointeurs (Two-Pointer)

Technique utilisant **deux indices** pour parcourir un tableau ou une liste, souvent dans des directions opposées ou à des vitesses différentes. Idéal pour les recherches de paires, de sous-tableaux, ou de propriétés sur des données **triées**.

### Principes

- **Opposés** : un pointeur au début, un à la fin, ils convergent (ex : somme cible, palindrome)
- **Même direction** : les deux avancent, parfois à des vitesses différentes (ex : suppression de doublons, sous-séquences)

### Complexité

- **Temps** : O(n) - parcours unique du tableau
- **Espace** : O(1) - seulement deux pointeurs

### Exemple 1 : Somme cible dans un tableau trié

**Problème** : Trouver deux nombres dans un tableau trié qui somment à une valeur cible.

```javascript
/**
 * Trouve deux nombres dont la somme égale la cible dans un tableau trié.
 *
 * Complexité temporelle : O(n) - parcours unique avec deux pointeurs
 * Complexité spatiale : O(1) - seulement deux variables pour les indices
 *
 * Pourquoi O(n) ? Chaque élément est visité au plus une fois. Les pointeurs
 * convergent en se rapprochant, et on arrête dès qu'ils se croisent.
 *
 * @param {number[]} arr - Tableau trié d'entiers
 * @param {number} cible - Somme recherchée
 * @returns {number[]|null} - Indices des deux nombres, ou null si non trouvés
 *
 * @example
 * deuxSomme([1, 2, 3, 4, 6], 6); // [1, 3] (car 2 + 4 = 6)
 */
function deuxSomme(arr, cible) {
  let gauche = 0;
  let droite = arr.length - 1;

  // Les pointeurs convergent
  while (gauche < droite) {
    const somme = arr[gauche] + arr[droite];

    if (somme === cible) {
      return [gauche, droite]; // Trouvé !
    } else if (somme < cible) {
      gauche++; // Somme trop petite, augmenter le pointeur gauche
    } else {
      droite--; // Somme trop grande, diminuer le pointeur droit
    }
  }

  return null; // Aucune paire trouvée
}

// Tests
console.log(deuxSomme([1, 2, 3, 4, 6], 6)); // [1, 3]
console.log(deuxSomme([2, 5, 9, 11], 11)); // [0, 2]
console.log(deuxSomme([1, 2, 3, 4], 10)); // null
```

**Pourquoi ce pattern fonctionne ?**

- Le tableau est **trié** → on peut décider dans quelle direction déplacer les pointeurs
- Si la somme est trop petite → augmenter `gauche` augmente la somme
- Si la somme est trop grande → diminuer `droite` diminue la somme

### Exemple 2 : Vérifier si une chaîne est un palindrome

```javascript
/**
 * Vérifie si une chaîne est un palindrome (se lit de la même façon dans les deux sens).
 *
 * Complexité temporelle : O(n) - parcours jusqu'au milieu
 * Complexité spatiale : O(1) - seulement deux indices
 *
 * @param {string} str - Chaîne à vérifier
 * @returns {boolean} - true si palindrome, false sinon
 *
 * @example
 * estPalindrome("radar"); // true
 * estPalindrome("hello"); // false
 */
function estPalindrome(str) {
  let gauche = 0;
  let droite = str.length - 1;

  while (gauche < droite) {
    if (str[gauche] !== str[droite]) {
      return false; // Différence détectée
    }
    gauche++;
    droite--;
  }

  return true; // Palindrome confirmé
}

// Tests
console.log(estPalindrome("radar")); // true
console.log(estPalindrome("bonjour")); // false
console.log(estPalindrome("A")); // true (un seul caractère)
console.log(estPalindrome("")); // true (chaîne vide)
```

### Exemple 3 : Supprimer les doublons dans un tableau trié (en place)

```javascript
/**
 * Supprime les doublons d'un tableau trié en place.
 * Retourne la nouvelle longueur (les k premiers éléments sont uniques).
 *
 * Complexité temporelle : O(n) - parcours unique
 * Complexité spatiale : O(1) - modification en place
 *
 * Pattern : Deux pointeurs dans la même direction (slow & fast)
 *
 * @param {number[]} nums - Tableau trié à modifier
 * @returns {number} - Nouvelle longueur (éléments uniques)
 *
 * @example
 * const arr = [1, 1, 2, 2, 3, 4, 4];
 * const k = supprimerDoublons(arr); // 4
 * console.log(arr.slice(0, k)); // [1, 2, 3, 4]
 */
function supprimerDoublons(nums) {
  if (nums.length === 0) return 0;

  let lent = 0; // Pointeur sur le dernier élément unique

  // Pointeur rapide explore tous les éléments
  for (let rapide = 1; rapide < nums.length; rapide++) {
    if (nums[rapide] !== nums[lent]) {
      lent++;
      nums[lent] = nums[rapide]; // Copier l'élément unique
    }
  }

  return lent + 1; // Nouvelle longueur
}

// Tests
const arr1 = [1, 1, 2, 2, 3, 4, 4];
console.log(supprimerDoublons(arr1)); // 4
console.log(arr1.slice(0, 4)); // [1, 2, 3, 4]
```

> **Question**
>
> Comment choisir entre deux pointeurs en sens opposé ou dans le même sens pour un problème donné ?
>
> **Réponse** :
>
> - **Sens opposé** : quand on veut combiner des éléments du début et de la fin (ex : somme cible, palindrome sur tableau trié). Complexité O(n).
> - **Même sens** : quand on cherche des sous-séquences, des fenêtres mobiles, ou qu'on doit parcourir tout le tableau en filtrant (ex : suppression de doublons, fast & slow pointers). Complexité O(n).

---

## 📝 Micro-exercice 1 : Triplet de somme nulle

Implémentez une fonction qui trouve **tous les triplets uniques** dans un tableau dont la somme vaut zéro.

**Signature** : `function tripletsSommeZero(nums) { ... }`

**Exemple** :

```javascript
tripletsSommeZero([-1, 0, 1, 2, -1, -4]);
// [[-1, -1, 2], [-1, 0, 1]]
```

**Indice** : Triez d'abord le tableau, puis pour chaque élément, utilisez deux pointeurs pour trouver les deux autres.

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Trouve tous les triplets uniques de somme nulle.
 *
 * Complexité temporelle : O(n²) - tri O(n log n) + boucle O(n) × deux pointeurs O(n)
 * Complexité spatiale : O(1) - sans compter le tableau de résultat
 *
 * @param {number[]} nums - Tableau d'entiers
 * @returns {number[][]} - Liste des triplets
 */
function tripletsSommeZero(nums) {
  const resultat = [];
  nums.sort((a, b) => a - b); // Tri : O(n log n)

  for (let i = 0; i < nums.length - 2; i++) {
    // Éviter les doublons pour le premier élément
    if (i > 0 && nums[i] === nums[i - 1]) continue;

    let gauche = i + 1;
    let droite = nums.length - 1;

    while (gauche < droite) {
      const somme = nums[i] + nums[gauche] + nums[droite];

      if (somme === 0) {
        resultat.push([nums[i], nums[gauche], nums[droite]]);

        // Éviter les doublons pour les deux autres éléments
        while (gauche < droite && nums[gauche] === nums[gauche + 1]) gauche++;
        while (gauche < droite && nums[droite] === nums[droite - 1]) droite--;

        gauche++;
        droite--;
      } else if (somme < 0) {
        gauche++; // Somme trop petite
      } else {
        droite--; // Somme trop grande
      }
    }
  }

  return resultat;
}

// Tests
console.log(tripletsSommeZero([-1, 0, 1, 2, -1, -4]));
// [[-1, -1, 2], [-1, 0, 1]]

console.log(tripletsSommeZero([0, 0, 0, 0]));
// [[0, 0, 0]]
```

**Pourquoi O(n²) ?**

- Tri : O(n log n)
- Boucle externe : O(n)
- Pour chaque i, deux pointeurs : O(n)
- Total : O(n log n) + O(n²) = **O(n²)**

</details>

---

## 🧩 Pattern 2 : Fenêtre Glissante (Sliding Window)

Utilisé pour trouver des **sous-tableaux ou sous-chaînes contigus** répondant à un critère (somme, nombre de caractères distincts, etc.). La fenêtre peut être de taille **fixe** ou **variable**.

### Principes

- **Fenêtre fixe** : taille constante (ex : somme max de k éléments)
- **Fenêtre dynamique** : s'agrandit ou rétrécit selon les contraintes (ex : sous-chaîne la plus longue avec k caractères distincts)

### Complexité

- **Temps** : O(n) - chaque élément ajouté/retiré au plus une fois
- **Espace** : O(1) pour fenêtre fixe, O(k) pour fenêtre dynamique avec k éléments distincts

### Exemple 1 : Somme maximale d'une sous-liste de taille k (fenêtre fixe)

**Problème** : Trouver la somme maximale d'un sous-tableau de k éléments consécutifs.

```javascript
/**
 * Trouve la somme maximale d'un sous-tableau de taille k.
 *
 * Complexité temporelle : O(n) - parcours unique avec fenêtre glissante
 * Complexité spatiale : O(1) - seulement quelques variables
 *
 * Alternative naïve : O(n × k) - recalculer la somme pour chaque fenêtre
 * Sliding Window : O(n) - mise à jour incrémentale
 *
 * @param {number[]} arr - Tableau d'entiers
 * @param {number} k - Taille de la fenêtre
 * @returns {number} - Somme maximale
 *
 * @example
 * sommeMaxFenetre([2, 1, 5, 1, 3, 2], 3); // 9 (5 + 1 + 3)
 */
function sommeMaxFenetre(arr, k) {
  if (arr.length < k) return null;

  // Calculer la somme de la première fenêtre
  let sommeActuelle = 0;
  for (let i = 0; i < k; i++) {
    sommeActuelle += arr[i];
  }

  let sommeMax = sommeActuelle;

  // Faire glisser la fenêtre
  for (let i = k; i < arr.length; i++) {
    sommeActuelle += arr[i] - arr[i - k]; // Ajouter le nouveau, retirer l'ancien
    sommeMax = Math.max(sommeMax, sommeActuelle);
  }

  return sommeMax;
}

// Tests
console.log(sommeMaxFenetre([2, 1, 5, 1, 3, 2], 3)); // 9 (5 + 1 + 3)
console.log(sommeMaxFenetre([2, 3, 4, 1, 5], 2)); // 7 (3 + 4)
```

**Astuce** : Au lieu de recalculer toute la somme à chaque décalage (O(k)), on **retire l'élément sortant** et **ajoute l'élément entrant** → mise à jour en O(1).

### Exemple 2 : Plus longue sous-chaîne avec k caractères distincts (fenêtre dynamique)

```javascript
/**
 * Trouve la longueur de la plus longue sous-chaîne avec au plus k caractères distincts.
 *
 * Complexité temporelle : O(n) - chaque caractère ajouté/retiré au plus une fois
 * Complexité spatiale : O(k) - dictionnaire stockant au plus k caractères
 *
 * @param {string} str - Chaîne de caractères
 * @param {number} k - Nombre maximum de caractères distincts
 * @returns {number} - Longueur maximale
 *
 * @example
 * plusLongueSousChaineKDistinct("araaci", 2); // 4 ("araa")
 */
function plusLongueSousChaineKDistinct(str, k) {
  let debut = 0;
  let longueurMax = 0;
  const compteur = {}; // Dictionnaire {caractère: fréquence}

  for (let fin = 0; fin < str.length; fin++) {
    const charDroite = str[fin];

    // Ajouter le caractère à droite
    compteur[charDroite] = (compteur[charDroite] || 0) + 1;

    // Rétrécir la fenêtre si plus de k caractères distincts
    while (Object.keys(compteur).length > k) {
      const charGauche = str[debut];
      compteur[charGauche]--;
      if (compteur[charGauche] === 0) {
        delete compteur[charGauche];
      }
      debut++;
    }

    // Mettre à jour la longueur maximale
    longueurMax = Math.max(longueurMax, fin - debut + 1);
  }

  return longueurMax;
}

// Tests
console.log(plusLongueSousChaineKDistinct("araaci", 2)); // 4 ("araa")
console.log(plusLongueSousChaineKDistinct("araaci", 1)); // 2 ("aa")
console.log(plusLongueSousChaineKDistinct("cbbebi", 3)); // 5 ("cbbeb")
```

**Principe** : La fenêtre s'agrandit en ajoutant des éléments à droite, et se rétrécit en retirant des éléments à gauche quand la contrainte est violée.

### Exemple 3 : Plus petite sous-liste de somme ≥ S

```javascript
/**
 * Trouve la longueur de la plus petite sous-liste de somme ≥ S.
 *
 * Complexité temporelle : O(n) - fenêtre glissante
 * Complexité spatiale : O(1)
 *
 * @param {number[]} arr - Tableau d'entiers positifs
 * @param {number} S - Somme cible
 * @returns {number} - Longueur minimale (0 si impossible)
 *
 * @example
 * plusPetiteSousListeSomme([2, 1, 5, 2, 3, 2], 7); // 2 ([5, 2])
 */
function plusPetiteSousListeSomme(arr, S) {
  let longueurMin = Infinity;
  let somme = 0;
  let debut = 0;

  for (let fin = 0; fin < arr.length; fin++) {
    somme += arr[fin];

    // Rétrécir la fenêtre tant que la somme est suffisante
    while (somme >= S) {
      longueurMin = Math.min(longueurMin, fin - debut + 1);
      somme -= arr[debut];
      debut++;
    }
  }

  return longueurMin === Infinity ? 0 : longueurMin;
}

// Tests
console.log(plusPetiteSousListeSomme([2, 1, 5, 2, 3, 2], 7)); // 2 ([5, 2])
console.log(plusPetiteSousListeSomme([2, 1, 5, 2, 8], 7)); // 1 ([8])
console.log(plusPetiteSousListeSomme([3, 4, 1, 1, 6], 8)); // 3 ([3, 4, 1])
```

> **Question**
>
> Comment déterminer si la fenêtre doit être de taille fixe ou dynamique ?
>
> **Réponse** :
>
> - **Fenêtre fixe** : quand la contrainte porte sur la **taille** (ex : somme de k éléments). Complexité O(n).
> - **Fenêtre dynamique** : quand la contrainte porte sur le **contenu** (ex : au plus k caractères distincts, somme minimale ≥ S). Complexité O(n).

---

## 📝 Micro-exercice 2 : Plus longue sous-chaîne sans répétition

Implémentez une fonction qui trouve la longueur de la **plus longue sous-chaîne sans caractères répétés**.

**Signature** : `function plusLongueSousChaineUnique(str) { ... }`

**Exemple** :

```javascript
plusLongueSousChaineUnique("abcabcbb"); // 3 ("abc")
plusLongueSousChaineUnique("bbbbb"); // 1 ("b")
plusLongueSousChaineUnique("pwwkew"); // 3 ("wke")
```

**Indice** : Utilisez une fenêtre dynamique avec un Set pour détecter les répétitions.

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Trouve la longueur de la plus longue sous-chaîne sans répétition.
 *
 * Complexité temporelle : O(n) - fenêtre glissante
 * Complexité spatiale : O(min(n, m)) où m = taille de l'alphabet
 *
 * @param {string} str - Chaîne de caractères
 * @returns {number} - Longueur maximale
 */
function plusLongueSousChaineUnique(str) {
  let debut = 0;
  let longueurMax = 0;
  const ensemble = new Set();

  for (let fin = 0; fin < str.length; fin++) {
    const charDroite = str[fin];

    // Rétrécir la fenêtre tant qu'il y a une répétition
    while (ensemble.has(charDroite)) {
      ensemble.delete(str[debut]);
      debut++;
    }

    ensemble.add(charDroite);
    longueurMax = Math.max(longueurMax, fin - debut + 1);
  }

  return longueurMax;
}

// Tests
console.log(plusLongueSousChaineUnique("abcabcbb")); // 3 ("abc")
console.log(plusLongueSousChaineUnique("bbbbb")); // 1 ("b")
console.log(plusLongueSousChaineUnique("pwwkew")); // 3 ("wke")
console.log(plusLongueSousChaineUnique("")); // 0
```

**Pourquoi O(n) ?**

- Dans le pire cas, chaque caractère est ajouté et retiré une fois
- Le Set permet add/delete/has en O(1)
- Total : O(n)

</details>

---

## 🧩 Pattern 3 : Fast & Slow Pointers (Lièvre & Tortue)

Deux pointeurs avancent à des **vitesses différentes**, souvent sur des **listes chaînées**. Permet de détecter des cycles, trouver le milieu, etc.

### Principes

- **Détection de cycle** : si le rapide rattrape le lent, il y a un cycle
- **Recherche du milieu** : quand le rapide atteint la fin, le lent est au milieu

### Complexité

- **Temps** : O(n) - parcours de la liste
- **Espace** : O(1) - seulement deux pointeurs (contrairement à un Set qui serait O(n))

### Exemple 1 : Détection de cycle dans une liste chaînée

**Problème** : Déterminer si une liste chaînée contient un cycle.

```javascript
/**
 * Nœud d'une liste chaînée.
 */
class NoeudListe {
  constructor(valeur) {
    this.valeur = valeur;
    this.suivant = null;
  }
}

/**
 * Détecte si une liste chaînée contient un cycle.
 *
 * Complexité temporelle : O(n) - parcours de la liste
 * Complexité spatiale : O(1) - seulement deux pointeurs
 *
 * Alternative avec Set : O(n) temps, O(n) espace
 *
 * Algorithme de Floyd (Cycle Detection) :
 * - Lent avance de 1, rapide de 2
 * - Si rapide rattrape lent → cycle
 * - Si rapide atteint null → pas de cycle
 *
 * @param {NoeudListe} tete - Tête de la liste
 * @returns {boolean} - true si cycle, false sinon
 */
function aCycle(tete) {
  if (!tete || !tete.suivant) return false;

  let lent = tete;
  let rapide = tete;

  while (rapide && rapide.suivant) {
    lent = lent.suivant; // Avance de 1
    rapide = rapide.suivant.suivant; // Avance de 2

    if (lent === rapide) {
      return true; // Cycle détecté !
    }
  }

  return false; // Pas de cycle
}

// Tests
const n1 = new NoeudListe(1);
const n2 = new NoeudListe(2);
const n3 = new NoeudListe(3);
const n4 = new NoeudListe(4);

n1.suivant = n2;
n2.suivant = n3;
n3.suivant = n4;
// n4.suivant = n2; // Décommenter pour créer un cycle

console.log(aCycle(n1)); // false
n4.suivant = n2; // Créer un cycle
console.log(aCycle(n1)); // true
```

**Pourquoi ça marche ?**

- Si pas de cycle : rapide atteint la fin en O(n/2) = O(n)
- Si cycle : rapide "rattrape" lent dans le cycle en O(n)
- Dans un cycle de longueur C, rapide se rapproche de 1 à chaque tour → rattrapage en C tours max

### Exemple 2 : Trouver le milieu d'une liste chaînée

```javascript
/**
 * Trouve le nœud du milieu d'une liste chaînée.
 * Si la longueur est paire, retourne le second des deux nœuds centraux.
 *
 * Complexité temporelle : O(n) - parcours de la liste
 * Complexité spatiale : O(1) - deux pointeurs
 *
 * @param {NoeudListe} tete - Tête de la liste
 * @returns {NoeudListe} - Nœud du milieu
 *
 * @example
 * Liste : 1 → 2 → 3 → 4 → 5
 * Retourne : nœud 3
 *
 * Liste : 1 → 2 → 3 → 4
 * Retourne : nœud 3 (second milieu)
 */
function trouverMilieu(tete) {
  let lent = tete;
  let rapide = tete;

  while (rapide && rapide.suivant) {
    lent = lent.suivant;
    rapide = rapide.suivant.suivant;
  }

  return lent; // Lent est au milieu quand rapide atteint la fin
}

// Tests
const liste = new NoeudListe(1);
liste.suivant = new NoeudListe(2);
liste.suivant.suivant = new NoeudListe(3);
liste.suivant.suivant.suivant = new NoeudListe(4);
liste.suivant.suivant.suivant.suivant = new NoeudListe(5);

const milieu = trouverMilieu(liste);
console.log(milieu.valeur); // 3
```

### Exemple 3 : Nombre heureux (Happy Number)

Un nombre est "heureux" si en répétant le processus de somme des carrés de ses chiffres, on atteint 1. Sinon, on tombe dans un cycle.

```javascript
/**
 * Détermine si un nombre est "heureux".
 *
 * Complexité temporelle : O(log n) - nombre de chiffres diminue
 * Complexité spatiale : O(1) - deux pointeurs au lieu d'un Set
 *
 * Exemple : 19 est heureux
 * 1² + 9² = 82
 * 8² + 2² = 68
 * 6² + 8² = 100
 * 1² + 0² + 0² = 1
 *
 * @param {number} n - Nombre à tester
 * @returns {boolean} - true si heureux, false sinon
 */
function estNombreHeureux(n) {
  /**
   * Calcule la somme des carrés des chiffres.
   */
  function sommeCarresChiffres(num) {
    let somme = 0;
    while (num > 0) {
      const chiffre = num % 10;
      somme += chiffre * chiffre;
      num = Math.floor(num / 10);
    }
    return somme;
  }

  let lent = n;
  let rapide = n;

  do {
    lent = sommeCarresChiffres(lent); // Avance de 1
    rapide = sommeCarresChiffres(sommeCarresChiffres(rapide)); // Avance de 2

    if (rapide === 1) return true; // Heureux !
  } while (lent !== rapide);

  return false; // Cycle détecté, pas heureux
}

// Tests
console.log(estNombreHeureux(19)); // true
console.log(estNombreHeureux(2)); // false
console.log(estNombreHeureux(7)); // true
```

> **Question**
>
> Quels sont les pièges ou cas limites à surveiller avec le pattern fast & slow pointers, notamment pour la détection de cycle ?
>
> **Réponse** :
>
> - Attention aux **listes vides** ou à **un seul élément** (pas de cycle possible).
> - Bien vérifier les **conditions d'arrêt** (`rapide && rapide.suivant` non nuls) pour éviter `null.suivant`.
> - Risque de **boucle infinie** si la condition d'arrêt est mal codée.
> - Pour le nombre heureux, utiliser `do-while` car lent === rapide au départ.

---

## 📝 Micro-exercice 3 : Trouver le début du cycle

Si une liste chaînée contient un cycle, trouvez le **nœud où commence le cycle**.

**Signature** : `function debutCycleListe(tete) { ... }`

**Indice** : Utilisez Floyd's algorithm en deux phases :

1. Détection du cycle (fast & slow)
2. Trouver le point d'entrée (remettre un pointeur à la tête)

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Trouve le nœud où commence le cycle dans une liste chaînée.
 *
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(1)
 *
 * Algorithme de Floyd (Phase 2) :
 * 1. Détecter le cycle avec fast & slow
 * 2. Remettre un pointeur à la tête
 * 3. Avancer les deux d'un pas à la fois
 * 4. Ils se rencontrent au début du cycle
 *
 * @param {NoeudListe} tete - Tête de la liste
 * @returns {NoeudListe|null} - Nœud de début de cycle, ou null
 */
function debutCycleListe(tete) {
  if (!tete || !tete.suivant) return null;

  let lent = tete;
  let rapide = tete;

  // Phase 1 : Détection du cycle
  while (rapide && rapide.suivant) {
    lent = lent.suivant;
    rapide = rapide.suivant.suivant;

    if (lent === rapide) {
      // Cycle détecté !
      // Phase 2 : Trouver le point d'entrée
      let pointeur = tete;
      while (pointeur !== lent) {
        pointeur = pointeur.suivant;
        lent = lent.suivant;
      }
      return pointeur; // Début du cycle
    }
  }

  return null; // Pas de cycle
}

// Tests
const n1 = new NoeudListe(1);
const n2 = new NoeudListe(2);
const n3 = new NoeudListe(3);
const n4 = new NoeudListe(4);
const n5 = new NoeudListe(5);

n1.suivant = n2;
n2.suivant = n3;
n3.suivant = n4;
n4.suivant = n5;
n5.suivant = n3; // Cycle commence à n3

const debut = debutCycleListe(n1);
console.log(debut.valeur); // 3
```

**Pourquoi ça marche ?**

- Distance de tête au cycle = distance de rencontre au cycle (mathématiquement prouvé)
- Avancer deux pointeurs d'un pas garantit qu'ils se rencontrent au début du cycle

</details>

---

## 🧩 Pattern 4 : Fusion d'Intervalles (Merge Intervals)

Problèmes où il faut **fusionner, insérer ou trouver des intersections d'intervalles**. Souvent utilisé en planification, gestion de calendriers, etc.

### Principes

- **Tri préalable** : toujours trier les intervalles par début
- **Fusion** : comparer chaque intervalle au dernier fusionné

### Complexité

- **Temps** : O(n log n) - dominé par le tri
- **Espace** : O(n) - tableau de résultat (ou O(log n) si tri en place)

### Exemple 1 : Fusionner des intervalles qui se chevauchent

**Problème** : Étant donné une liste d'intervalles, fusionnez tous les intervalles qui se chevauchent.

```javascript
/**
 * Fusionne les intervalles qui se chevauchent.
 *
 * Complexité temporelle : O(n log n) - dominé par le tri
 * Complexité spatiale : O(n) - tableau de résultat
 *
 * @param {number[][]} intervalles - Liste d'intervalles [debut, fin]
 * @returns {number[][]} - Intervalles fusionnés
 *
 * @example
 * fusionnerIntervalles([[1,3],[2,6],[8,10],[15,18]]);
 * // [[1,6],[8,10],[15,18]]
 */
function fusionnerIntervalles(intervalles) {
  if (intervalles.length === 0) return [];

  // Tri par début d'intervalle : O(n log n)
  intervalles.sort((a, b) => a[0] - b[0]);

  const resultat = [intervalles[0]];

  for (let i = 1; i < intervalles.length; i++) {
    const dernierFusionne = resultat[resultat.length - 1];
    const actuel = intervalles[i];

    // Chevauchement ? Comparer la fin du dernier avec le début de l'actuel
    if (actuel[0] <= dernierFusionne[1]) {
      // Fusionner : étendre la fin au maximum des deux
      dernierFusionne[1] = Math.max(dernierFusionne[1], actuel[1]);
    } else {
      // Pas de chevauchement : ajouter l'intervalle
      resultat.push(actuel);
    }
  }

  return resultat;
}

// Tests
console.log(
  fusionnerIntervalles([
    [1, 3],
    [2, 6],
    [8, 10],
    [15, 18],
  ]),
);
// [[1,6],[8,10],[15,18]]

console.log(
  fusionnerIntervalles([
    [1, 4],
    [4, 5],
  ]),
);
// [[1,5]]

console.log(
  fusionnerIntervalles([
    [1, 4],
    [0, 4],
  ]),
);
// [[0,4]]
```

**Pourquoi trier ?** Sans tri, on peut rater des chevauchements. Exemple : `[[1,3],[8,10],[2,6]]` → sans tri, on rate que [2,6] chevauche [1,3].

### Exemple 2 : Insérer un intervalle dans une liste triée

```javascript
/**
 * Insère un nouvel intervalle dans une liste triée et fusionne si nécessaire.
 *
 * Complexité temporelle : O(n) - parcours unique
 * Complexité spatiale : O(n) - tableau de résultat
 *
 * @param {number[][]} intervalles - Liste triée d'intervalles
 * @param {number[]} nouveauIntervalle - Intervalle à insérer
 * @returns {number[][]} - Liste fusionnée
 *
 * @example
 * insererIntervalle([[1,3],[6,9]], [2,5]);
 * // [[1,5],[6,9]]
 */
function insererIntervalle(intervalles, nouveauIntervalle) {
  const resultat = [];
  let i = 0;
  const n = intervalles.length;

  // Ajouter tous les intervalles qui finissent avant le nouveau
  while (i < n && intervalles[i][1] < nouveauIntervalle[0]) {
    resultat.push(intervalles[i]);
    i++;
  }

  // Fusionner tous les intervalles qui chevauchent le nouveau
  while (i < n && intervalles[i][0] <= nouveauIntervalle[1]) {
    nouveauIntervalle[0] = Math.min(nouveauIntervalle[0], intervalles[i][0]);
    nouveauIntervalle[1] = Math.max(nouveauIntervalle[1], intervalles[i][1]);
    i++;
  }
  resultat.push(nouveauIntervalle);

  // Ajouter les intervalles restants
  while (i < n) {
    resultat.push(intervalles[i]);
    i++;
  }

  return resultat;
}

// Tests
console.log(
  insererIntervalle(
    [
      [1, 3],
      [6, 9],
    ],
    [2, 5],
  ),
);
// [[1,5],[6,9]]

console.log(
  insererIntervalle(
    [
      [1, 2],
      [3, 5],
      [6, 7],
      [8, 10],
      [12, 16],
    ],
    [4, 8],
  ),
);
// [[1,2],[3,10],[12,16]]
```

### Exemple 3 : Nombre minimum de salles de réunion nécessaires

```javascript
/**
 * Calcule le nombre minimum de salles de réunion nécessaires.
 *
 * Complexité temporelle : O(n log n) - tri des débuts et fins
 * Complexité spatiale : O(n) - tableaux de débuts et fins
 *
 * Algorithme :
 * 1. Trier les débuts et fins séparément
 * 2. Utiliser deux pointeurs
 * 3. Si réunion commence avant qu'une autre finisse → salle supplémentaire
 *
 * @param {number[][]} intervalles - Horaires des réunions
 * @returns {number} - Nombre minimum de salles
 *
 * @example
 * sallesReunionsMin([[0,30],[5,10],[15,20]]);
 * // 2 (une salle pour [0,30], une autre pour [5,10] et [15,20])
 */
function sallesReunionsMin(intervalles) {
  if (intervalles.length === 0) return 0;

  // Séparer et trier débuts et fins
  const debuts = intervalles.map((i) => i[0]).sort((a, b) => a - b);
  const fins = intervalles.map((i) => i[1]).sort((a, b) => a - b);

  let sallesNecessaires = 0;
  let sallesUtilisees = 0;
  let debutPtr = 0;
  let finPtr = 0;

  while (debutPtr < intervalles.length) {
    if (debuts[debutPtr] < fins[finPtr]) {
      // Nouvelle réunion commence avant qu'une autre finisse
      sallesUtilisees++;
      sallesNecessaires = Math.max(sallesNecessaires, sallesUtilisees);
      debutPtr++;
    } else {
      // Une réunion se termine, libérer une salle
      sallesUtilisees--;
      finPtr++;
    }
  }

  return sallesNecessaires;
}

// Tests
console.log(
  sallesReunionsMin([
    [0, 30],
    [5, 10],
    [15, 20],
  ]),
); // 2
console.log(
  sallesReunionsMin([
    [7, 10],
    [2, 4],
  ]),
); // 1
console.log(
  sallesReunionsMin([
    [1, 5],
    [8, 9],
    [8, 9],
  ]),
); // 2
```

> **Question**
>
> Que faire si les intervalles d'entrée ne sont pas triés ? Comment cela impacte-t-il l'approche ?
>
> **Réponse** :
>
> - Il faut d'abord **trier les intervalles par leur début**. Sans cela, la fusion peut rater des chevauchements.
> - Le tri ajoute une complexité de **O(n log n)**, ce qui devient la complexité dominante.
> - Le tri est donc une **étape indispensable** pour garantir la correction de l'algorithme.

---

## 📝 Micro-exercice 4 : Intersection de deux listes d'intervalles

Implémentez une fonction qui trouve **l'intersection** de deux listes d'intervalles triés.

**Signature** : `function intersectionIntervalles(list1, list2) { ... }`

**Exemple** :

```javascript
intersectionIntervalles(
  [
    [1, 3],
    [5, 6],
    [7, 9],
  ],
  [
    [2, 3],
    [5, 7],
  ],
);
// [[2,3],[5,6],[7,7]]
```

**Indice** : Utilisez deux pointeurs, un pour chaque liste. Calculez l'intersection entre les intervalles courants.

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Trouve l'intersection de deux listes d'intervalles triés.
 *
 * Complexité temporelle : O(n + m) - parcours des deux listes
 * Complexité spatiale : O(min(n, m)) - au pire, toutes les intersections
 *
 * @param {number[][]} list1 - Première liste d'intervalles
 * @param {number[][]} list2 - Deuxième liste d'intervalles
 * @returns {number[][]} - Intersections
 */
function intersectionIntervalles(list1, list2) {
  const resultat = [];
  let i = 0,
    j = 0;

  while (i < list1.length && j < list2.length) {
    const [debut1, fin1] = list1[i];
    const [debut2, fin2] = list2[j];

    // Calculer l'intersection
    const debutIntersection = Math.max(debut1, debut2);
    const finIntersection = Math.min(fin1, fin2);

    // Si intersection valide, l'ajouter
    if (debutIntersection <= finIntersection) {
      resultat.push([debutIntersection, finIntersection]);
    }

    // Avancer le pointeur de l'intervalle qui finit en premier
    if (fin1 < fin2) {
      i++;
    } else {
      j++;
    }
  }

  return resultat;
}

// Tests
console.log(
  intersectionIntervalles(
    [
      [1, 3],
      [5, 6],
      [7, 9],
    ],
    [
      [2, 3],
      [5, 7],
    ],
  ),
);
// [[2,3],[5,6],[7,7]]

console.log(
  intersectionIntervalles(
    [
      [1, 3],
      [5, 9],
    ],
    [
      [4, 6],
      [7, 10],
    ],
  ),
);
// [[5,6],[7,9]]
```

**Pourquoi O(n + m) ?**

- On parcourt chaque liste au plus une fois
- À chaque étape, on avance au moins un des deux pointeurs
- Total : O(n + m) où n et m sont les tailles des deux listes

</details>

---

## 📊 Tableau Récapitulatif des Complexités

| Pattern             | Complexité Temporelle | Complexité Spatiale | Quand l'utiliser ?                              |
| ------------------- | --------------------- | ------------------- | ----------------------------------------------- |
| **Two Pointers**    | O(n)                  | O(1)                | Données triées, recherche de paires, palindrome |
| **Sliding Window**  | O(n)                  | O(1) à O(k)         | Sous-tableaux contigus, fenêtre fixe/dynamique  |
| **Fast & Slow**     | O(n)                  | O(1)                | Listes chaînées, cycles, milieu                 |
| **Merge Intervals** | O(n log n)            | O(n)                | Intervalles, planification, calendriers         |

---

## 💪 Exercices Pratiques

### Exercice 1 : Carrés triés (Two Pointers)

Implémentez `carresTries(arr)` qui retourne les carrés d'un tableau trié (avec négatifs), triés en ordre croissant.

**Exemple** :

```javascript
carresTries([-4, -1, 0, 3, 10]);
// [0, 1, 9, 16, 100]
```

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Retourne les carrés d'un tableau trié, triés en ordre croissant.
 *
 * Complexité temporelle : O(n) - parcours unique avec deux pointeurs
 * Complexité spatiale : O(n) - tableau de résultat
 *
 * Alternative naïve : O(n log n) - calculer carrés puis trier
 *
 * @param {number[]} arr - Tableau trié avec négatifs
 * @returns {number[]} - Carrés triés
 */
function carresTries(arr) {
  const n = arr.length;
  const resultat = new Array(n);
  let gauche = 0;
  let droite = n - 1;

  // Remplir le résultat de droite à gauche (du plus grand au plus petit)
  for (let i = n - 1; i >= 0; i--) {
    const carreGauche = arr[gauche] ** 2;
    const carreDroit = arr[droite] ** 2;

    if (carreGauche > carreDroit) {
      resultat[i] = carreGauche;
      gauche++;
    } else {
      resultat[i] = carreDroit;
      droite--;
    }
  }

  return resultat;
}

// Tests
console.log(carresTries([-4, -1, 0, 3, 10])); // [0, 1, 9, 16, 100]
console.log(carresTries([-7, -3, 2, 3, 11])); // [4, 9, 9, 49, 121]
```

**Astuce** : Les plus grands carrés sont soit à gauche (négatifs), soit à droite (positifs). Comparer les deux extrémités et remplir le résultat de droite à gauche.

</details>

---

### Exercice 2 : Fruits dans des paniers (Sliding Window)

Vous avez des arbres avec des fruits, représentés par un tableau `fruits` où `fruits[i]` est le type de fruit de l'arbre `i`. Vous avez deux paniers et chaque panier ne peut contenir qu'un seul type de fruit. Trouvez le **nombre maximum de fruits** que vous pouvez collecter en ramassant des fruits d'arbres consécutifs.

**Exemple** :

```javascript
fruitsMaxDansPaniers([1, 2, 1]);
// 3 (ramasser tous)

fruitsMaxDansPaniers([0, 1, 2, 2]);
// 3 ([1, 2, 2])

fruitsMaxDansPaniers([1, 2, 3, 2, 2]);
// 4 ([2, 3, 2, 2])
```

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Trouve le nombre maximum de fruits collectables avec deux paniers.
 *
 * Complexité temporelle : O(n) - fenêtre glissante
 * Complexité spatiale : O(1) - au plus 3 types dans le dictionnaire
 *
 * Pattern : Sliding Window dynamique avec au plus 2 types distincts
 *
 * @param {number[]} fruits - Types de fruits sur les arbres
 * @returns {number} - Nombre maximum de fruits
 */
function fruitsMaxDansPaniers(fruits) {
  let debut = 0;
  let max = 0;
  const compteur = {};

  for (let fin = 0; fin < fruits.length; fin++) {
    const fruit = fruits[fin];
    compteur[fruit] = (compteur[fruit] || 0) + 1;

    // Rétrécir la fenêtre si plus de 2 types
    while (Object.keys(compteur).length > 2) {
      const fruitGauche = fruits[debut];
      compteur[fruitGauche]--;
      if (compteur[fruitGauche] === 0) {
        delete compteur[fruitGauche];
      }
      debut++;
    }

    max = Math.max(max, fin - debut + 1);
  }

  return max;
}

// Tests
console.log(fruitsMaxDansPaniers([1, 2, 1])); // 3
console.log(fruitsMaxDansPaniers([0, 1, 2, 2])); // 3
console.log(fruitsMaxDansPaniers([1, 2, 3, 2, 2])); // 4
```

**Observation** : Ce problème est identique à "plus longue sous-chaîne avec au plus 2 caractères distincts".

</details>

---

### Exercice 3 : Liste chaînée palindrome (Fast & Slow)

Déterminez si une liste chaînée est un palindrome.

**Exemple** :

```javascript
// Liste : 1 → 2 → 2 → 1
estPalindromeListe(liste); // true

// Liste : 1 → 2 → 3
estPalindromeListe(liste); // false
```

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Détermine si une liste chaînée est un palindrome.
 *
 * Complexité temporelle : O(n)
 * Complexité spatiale : O(1)
 *
 * Algorithme :
 * 1. Trouver le milieu avec fast & slow
 * 2. Inverser la seconde moitié
 * 3. Comparer les deux moitiés
 * 4. (Optionnel) Restaurer la liste
 *
 * @param {NoeudListe} tete - Tête de la liste
 * @returns {boolean} - true si palindrome
 */
function estPalindromeListe(tete) {
  if (!tete || !tete.suivant) return true;

  // 1. Trouver le milieu
  let lent = tete;
  let rapide = tete;

  while (rapide && rapide.suivant) {
    lent = lent.suivant;
    rapide = rapide.suivant.suivant;
  }

  // 2. Inverser la seconde moitié
  let precedent = null;
  let courant = lent;
  while (courant) {
    const suivant = courant.suivant;
    courant.suivant = precedent;
    precedent = courant;
    courant = suivant;
  }

  // 3. Comparer les deux moitiés
  let gauche = tete;
  let droite = precedent; // Tête de la seconde moitié inversée

  while (droite) {
    if (gauche.valeur !== droite.valeur) {
      return false;
    }
    gauche = gauche.suivant;
    droite = droite.suivant;
  }

  return true;
}

// Tests
const l1 = new NoeudListe(1);
l1.suivant = new NoeudListe(2);
l1.suivant.suivant = new NoeudListe(2);
l1.suivant.suivant.suivant = new NoeudListe(1);
console.log(estPalindromeListe(l1)); // true

const l2 = new NoeudListe(1);
l2.suivant = new NoeudListe(2);
console.log(estPalindromeListe(l2)); // false
```

</details>

---

### Exercice 4 : Intervalles d'employés (Merge Intervals)

Étant donné les horaires de travail de plusieurs employés (intervalles), trouvez les **plages horaires libres communes à tous**.

**Exemple** :

```javascript
const employe1 = [
  [1, 3],
  [5, 6],
];
const employe2 = [
  [2, 3],
  [6, 8],
];

plagesLibresCommunes([employe1, employe2]);
// [[3,5]] (plage libre entre 3 et 5 pour les deux)
```

<details>
<summary>💡 Solution</summary>

```javascript
/**
 * Trouve les plages libres communes à tous les employés.
 *
 * Complexité temporelle : O(n log n) - tri et fusion
 * Complexité spatiale : O(n) - intervalles fusionnés
 *
 * @param {number[][][]} employes - Horaires de chaque employé
 * @returns {number[][]} - Plages libres communes
 */
function plagesLibresCommunes(employes) {
  if (employes.length === 0) return [];

  // 1. Fusionner tous les intervalles occupés
  const tousIntervalles = employes.flat();
  tousIntervalles.sort((a, b) => a[0] - b[0]);

  const occupes = [];
  let courant = tousIntervalles[0];

  for (let i = 1; i < tousIntervalles.length; i++) {
    if (tousIntervalles[i][0] <= courant[1]) {
      courant[1] = Math.max(courant[1], tousIntervalles[i][1]);
    } else {
      occupes.push(courant);
      courant = tousIntervalles[i];
    }
  }
  occupes.push(courant);

  // 2. Trouver les gaps entre intervalles occupés
  const libres = [];
  for (let i = 0; i < occupes.length - 1; i++) {
    const fin = occupes[i][1];
    const debutSuivant = occupes[i + 1][0];
    if (fin < debutSuivant) {
      libres.push([fin, debutSuivant]);
    }
  }

  return libres;
}

// Tests
const employe1 = [
  [1, 3],
  [5, 6],
];
const employe2 = [
  [2, 3],
  [6, 8],
];
console.log(plagesLibresCommunes([employe1, employe2])); // [[3,5]]
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quand utiliser une fenêtre glissante de taille dynamique ?**

- [ ] A. Quand la taille est imposée
- [ ] B. Quand la contrainte porte sur le contenu
- [ ] C. Toujours

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La fenêtre glissante de taille **dynamique** est utilisée quand la contrainte porte sur le **contenu** (ex : au plus k caractères distincts, somme ≥ S). La fenêtre s'agrandit et se rétrécit selon les besoins.

La fenêtre **fixe** est utilisée quand la taille est imposée (ex : somme de k éléments).

</details>

---

### Question 2

**Pourquoi faut-il trier les intervalles avant de les fusionner ?**

- [ ] A. Pour l'efficacité
- [ ] B. Pour garantir la correction
- [ ] C. Les deux

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le tri est nécessaire pour **garantir la correction** (sans tri, on peut rater des chevauchements) ET pour **l'efficacité** (permettre un parcours linéaire en O(n) après le tri en O(n log n)).

</details>

---

### Question 3

**Quel est le principal piège du pattern fast & slow pointers ?**

- [ ] A. Oublier de vérifier les conditions d'arrêt
- [ ] B. Utiliser des listes triées
- [ ] C. Ne pas utiliser de pointeurs

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

Le principal piège est d'**oublier de vérifier** que `rapide` et `rapide.suivant` ne sont pas `null` avant d'accéder à `rapide.suivant.suivant`. Cela peut causer une erreur `Cannot read property 'suivant' of null`.

</details>

---

### Question 4

**Quelle est la complexité temporelle du pattern Two Pointers sur un tableau trié ?**

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

Le pattern Two Pointers sur un tableau trié a une complexité de **O(n)** car chaque élément est visité au plus une fois. Les pointeurs convergent en se rapprochant.

Alternative sans Two Pointers : O(n²) avec boucles imbriquées.

</details>

---

### Question 5

**Pourquoi le pattern Fast & Slow Pointers utilise-t-il O(1) en espace au lieu de O(n) ?**

- [ ] A. Parce qu'il utilise une récursion
- [ ] B. Parce qu'il utilise seulement deux pointeurs au lieu d'un Set
- [ ] C. Parce qu'il modifie la liste en place

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le pattern Fast & Slow utilise **seulement deux pointeurs** (variables) au lieu d'un **Set** qui stockerait tous les nœuds visités (O(n) en espace). C'est l'avantage principal de ce pattern pour la détection de cycles.

</details>

---

### Question 6

**Dans quel cas la fenêtre glissante ne fonctionne-t-elle PAS ?**

- [ ] A. Sous-tableau de somme maximale
- [ ] B. Plus longue sous-chaîne sans répétition
- [ ] C. Sous-séquence (non contiguë) de longueur maximale

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La fenêtre glissante nécessite des éléments **contigus** (sous-tableau ou sous-chaîne). Pour les **sous-séquences** (non contiguës), il faut utiliser d'autres techniques comme la programmation dynamique.

Exemple : Plus longue sous-séquence croissante → DP, pas fenêtre glissante.

</details>

---

### Question 7

**Quelle est la complexité spatiale du pattern Merge Intervals ?**

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le pattern Merge Intervals a une complexité spatiale de **O(n)** pour stocker le tableau de résultat (intervalles fusionnés). Si on compte le tri en place, cela peut être réduit à O(log n) pour la pile de récursion du tri.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Deux Pointeurs (Two-Pointer)

Parcourir efficacement des tableaux/listes avec deux indices. **Sens opposé** pour somme cible/palindrome (O(n)), **même sens** pour sous-séquences/filtrage (O(n)). Complexité spatiale O(1).

### 2. Fenêtre Glissante (Sliding Window)

Optimiser la recherche de sous-tableaux/chaînes contigus. **Taille fixe** pour contrainte de longueur (O(n)), **taille dynamique** pour contrainte de contenu (O(n)). Alternative naïve : O(n × k).

### 3. Fast & Slow Pointers

Deux pointeurs à vitesses différentes sur listes chaînées. Idéal pour **détecter des cycles** et **trouver le milieu** d'une liste. O(n) temps, O(1) espace (vs O(n) avec Set).

### 4. Fusion d'Intervalles

Gérer des plages, planification, calendriers. **Toujours trier** les intervalles par début (O(n log n)) avant de fusionner ou chercher des intersections (O(n) après tri).

### 5. Gestion des Cas Limites

Vérifier les tableaux vides, éléments uniques, listes sans cycle. Trier si nécessaire. Pour Fast & Slow, toujours vérifier `rapide && rapide.suivant`. Un pattern mal appliqué peut donner des résultats incorrects.

### 6. Adapter le Pattern au Problème

Analysez d'abord le problème, puis choisissez le pattern adapté. **Données triées + paires** → Two Pointers. **Sous-tableau contigu** → Sliding Window. **Liste chaînée + cycle** → Fast & Slow. **Intervalles** → Merge Intervals.

### 7. Combiner les Patterns

Les problèmes avancés nécessitent souvent **plusieurs patterns**. Exemple : Trouver le milieu d'une liste (Fast & Slow) puis vérifier si palindrome (Two Pointers). Maîtriser chaque pattern individuellement permet de les combiner efficacement.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez désormais les patterns fondamentaux pour aborder efficacement la majorité des problèmes algorithmiques courants.

### Ce que vous avez appris aujourd'hui

- Les quatre patterns essentiels : **Two Pointers** (O(n)), **Sliding Window** (O(n)), **Fast & Slow** (O(n), O(1) espace), **Merge Intervals** (O(n log n))
- Comment reconnaître quel pattern appliquer selon le problème (structure de données, contraintes, objectif)
- Les pièges courants et comment les éviter (cas limites, conditions d'arrêt, tri préalable)
- L'importance de la **complexité Big O** pour chaque pattern et comment l'analyser

### Compétences acquises

Vous êtes maintenant capable de :

- Identifier rapidement le pattern adapté à un problème (gain de temps en entretien)
- Implémenter efficacement chaque pattern en JavaScript avec la complexité optimale
- Combiner plusieurs patterns pour des problèmes complexes
- Justifier vos choix algorithmiques avec la notation Big O

---

## ➡️ Prochaine Étape : Leçon 39

### Ce qui vous attend

Dans la prochaine leçon, **« Optimisation d'Applications JavaScript Réelles »**, vous allez appliquer tous vos acquis algorithmiques à des cas concrets d'optimisation.

**Vous découvrirez :**

- Comment identifier les goulots d'étranglement dans une application
- Les techniques de profilage et de mesure de performance (Chrome DevTools, Performance API)
- L'optimisation des opérations courantes (boucles, manipulation de données, rendering)
- Les bonnes pratiques pour un code performant en production

### Préparez-vous !

Cette leçon vous montrera comment transformer vos connaissances algorithmiques en améliorations concrètes de performance. Préparez-vous à optimiser du vrai code !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [LeetCode - Patterns](https://leetcode.com/explore/learn/card/fun-with-arrays/) - Exercices pratiques par pattern
- [GeeksforGeeks - Two Pointers](https://www.geeksforgeeks.org/two-pointers-technique/) - Tutoriels détaillés
- [NeetCode](https://neetcode.io/) - Roadmap d'apprentissage des patterns
- [14 Patterns to Ace Any Coding Interview](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed) - Guide complet

### Outils utiles

- **[LeetCode](https://leetcode.com/)** : Exercices classés par pattern (filtrer par tags)
- **[AlgoExpert](https://www.algoexpert.io/)** : Vidéos et explications approfondies
- **[VisuAlgo](https://visualgo.net/)** : Visualisation interactive des algorithmes

### Pratique recommandée

Pour maîtriser ces patterns, résolvez **au moins 5 problèmes par pattern** sur LeetCode :

- **Two Pointers** : Container With Most Water, 3Sum, Trapping Rain Water
- **Sliding Window** : Longest Substring Without Repeating, Minimum Window Substring
- **Fast & Slow** : Linked List Cycle II, Happy Number, Palindrome Linked List
- **Merge Intervals** : Insert Interval, Meeting Rooms II, Non-overlapping Intervals

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques et micro-exercices
- Implémenter chaque pattern sur des problèmes LeetCode
- Analyser la complexité Big O de vos solutions

> 💡 **Conseil**
>
> La maîtrise des patterns vient avec la **pratique intensive**. Résolvez au moins 5 problèmes par pattern sur LeetCode avant de passer au suivant. Quand vous voyez un nouveau problème, posez-vous d'abord la question : **"Quel pattern s'applique ici ?"** Avec le temps, cette identification deviendra instantanée. Pensez toujours à la **complexité Big O** dès la conception de votre solution.

---

**Prêt pour la Leçon 39 ?** 🚀

Rendez-vous dans la prochaine leçon pour optimiser des applications JavaScript réelles !

---

<div align="center">

**Leçon 38 sur 42 - Module 7 : Applications d'Algorithmes et Résolution de Problèmes**

[⬅️ Leçon 37 : Révision des Stratégies de Conception d'Algorithmes](./lecon-1-revision-strategies-conception-algorithmes.md) | [Retour au sommaire](./README.md) | [Leçon 39 : Optimisation d'Applications JavaScript Réelles ➡️](./lecon-3-optimisation-applications-javascript-reelles.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
