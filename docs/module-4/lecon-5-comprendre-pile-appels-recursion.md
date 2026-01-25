##### Leçon 23 sur 42

# Comprendre la Pile d'Appels (Call Stack) en Récursion

**Module 4** : Algorithmes de Recherche et Introduction à la Récursion

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le fonctionnement de la **pile d'appels** (call stack) en JavaScript
- Expliquer le principe **LIFO** (Last-In, First-Out) appliqué aux appels de fonctions
- Tracer **manuellement** l'état de la pile pendant l'exécution récursive
- Comprendre pourquoi et comment survient l'erreur **Stack Overflow**
- Utiliser les **outils de débogage** pour visualiser la pile d'appels
- Identifier et corriger les problèmes de récursion **infinie**

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- **Leçons 21-22 complétées** : Maîtriser les fonctions récursives de base
- **Concepts de pile** : Comprendre la structure de données pile (LIFO)
- **Fonctions JavaScript** : Savoir comment les fonctions sont appelées et retournent des valeurs
- Environnement JavaScript avec accès aux outils de débogage

---

## 🚀 Introduction : Dans les Coulisses de JavaScript

Quand vous appelez une fonction en JavaScript, que se passe-t-il réellement en coulisses ? Comment JavaScript "se souvient-il" où reprendre l'exécution après qu'une fonction se termine ? La réponse réside dans une structure de données appelée la **pile d'appels** (call stack).

Imaginez une pile d'assiettes dans un restaurant :

- Chaque nouvelle assiette est placée **sur le dessus** de la pile
- On retire toujours l'assiette du **dessus** en premier
- On ne peut pas accéder aux assiettes du milieu sans retirer celles du dessus

C'est exactement le principe **LIFO** (Last-In, First-Out) : le dernier élément ajouté est le premier retiré.

Dans le contexte des fonctions :

- Chaque appel de fonction **empile** un nouveau "cadre" (frame)
- Quand une fonction se termine, son cadre est **dépilé**
- L'exécution reprend là où elle s'était arrêtée

> **Point Clé**
>
> La pile d'appels est le mécanisme qui permet à JavaScript de gérer les appels de fonctions imbriqués et les appels récursifs. Comprendre son fonctionnement est essentiel pour déboguer les fonctions récursives et éviter les erreurs de type "Stack Overflow".

---

## 📦 Fonctionnement de la Pile d'Appels

La pile d'appels est une structure de données utilisée par JavaScript pour suivre les appels de fonctions. Chaque appel crée un **cadre d'exécution** (stack frame) contenant les informations de la fonction.

---

### Qu'est-ce qu'un Cadre d'Exécution ?

Chaque cadre contient :

| Élément               | Description                                |
| --------------------- | ------------------------------------------ |
| **Arguments**         | Les valeurs passées à la fonction          |
| **Variables locales** | Les variables déclarées dans la fonction   |
| **Adresse de retour** | Où reprendre l'exécution après le `return` |
| **Contexte `this`**   | La valeur de `this` dans la fonction       |

---

### Exemple Simple : Appels de Fonctions

```javascript
function saluer(nom) {
  console.log(`Bonjour, ${nom} !`);
}

function sePresenter(personne) {
  saluer(personne); // Appelle saluer
  console.log(`Enchanté de vous rencontrer, ${personne}.`);
}

sePresenter("Chermann"); // Démarre le processus
```

---

### Traçage de la Pile

Suivons l'évolution de la pile pendant l'exécution :

```
ÉTAPE 1 : Démarrage du script
┌─────────────────────────────┐
│ Contexte Global             │ ← Sommet de la pile
└─────────────────────────────┘

ÉTAPE 2 : sePresenter("Chermann") est appelée
┌──────────────────────────────────┐
│ sePresenter(personne="Chermann") │ ← Sommet
├──────────────────────────────────┤
│ Contexte Global                  │
└──────────────────────────────────┘

ÉTAPE 3 : saluer("Chermann") est appelée depuis sePresenter
┌──────────────────────────────────┐
│ saluer(nom="Chermann")           │ ← Sommet
├──────────────────────────────────┤
│ sePresenter(personne="Chermann") │
├──────────────────────────────────┤
│ Contexte Global                  │
└──────────────────────────────────┘

ÉTAPE 4 : saluer termine et retourne
┌──────────────────────────────────┐
│ sePresenter(personne="Chermann") │ ← Sommet (saluer dépilée)
├──────────────────────────────────┤
│ Contexte Global                  │
└──────────────────────────────────┘

ÉTAPE 5 : sePresenter termine et retourne
┌─────────────────────────────┐
│ Contexte Global             │ ← Sommet (sePresenter dépilée)
└─────────────────────────────┘

ÉTAPE 6 : Le script termine
(Pile vide)
```

---

### Tableau Récapitulatif

| Étape | Action                            | État de la Pile                 |
| ----- | --------------------------------- | ------------------------------- |
| 1     | Script démarre                    | `[Global]`                      |
| 2     | `sePresenter("Chermann")` appelée | `[Global, sePresenter]`         |
| 3     | `saluer("Chermann")` appelée      | `[Global, sePresenter, saluer]` |
| 4     | `saluer` termine                  | `[Global, sePresenter]`         |
| 5     | `sePresenter` termine             | `[Global]`                      |
| 6     | Script termine                    | `[]`                            |

---

## 📝 Micro-Exercice #1 : Tracer des Appels Simples

**Objectif :** Comprendre l'ordre d'empilement et de dépilement.

**Instructions :** Tracez l'état de la pile pour le code suivant :

```javascript
function multiplier(a, b) {
  return a * b;
}

function calculer(x, y) {
  let resultat = multiplier(x, y);
  return resultat + 10;
}

console.log(calculer(5, 3));
```

<details>
<summary>💡 Voir la solution</summary>

| Étape | Action                     | Pile                             |
| ----- | -------------------------- | -------------------------------- |
| 1     | Script démarre             | `[Global]`                       |
| 2     | `calculer(5, 3)` appelée   | `[Global, calculer]`             |
| 3     | `multiplier(5, 3)` appelée | `[Global, calculer, multiplier]` |
| 4     | `multiplier` retourne 15   | `[Global, calculer]`             |
| 5     | `calculer` retourne 25     | `[Global]`                       |
| 6     | `console.log(25)`          | Script termine                   |

**Explication :**

- `calculer(5, 3)` appelle `multiplier(5, 3)`
- `multiplier` calcule 5 × 3 = 15 et retourne
- `calculer` reçoit 15, calcule 15 + 10 = 25 et retourne
- Le résultat 25 est affiché

</details>

---

## 🔄 La Pile d'Appels en Récursion

La pile d'appels est **particulièrement critique** pour comprendre la récursion. Chaque appel récursif ajoute un nouveau cadre à la pile jusqu'au cas de base.

---

### Exemple : La Factorielle

Rappelons notre fonction factorielle :

```javascript
function factorielle(n) {
  // Cas de base
  if (n === 0) {
    return 1;
  }
  // Appel récursif
  return n * factorielle(n - 1);
}

console.log(factorielle(3)); // 6
```

---

### Traçage Complet de factorielle(3)

**Phase de DESCENTE** (empilage) :

```
ÉTAPE 1 : factorielle(3) appelée
┌──────────────────────────┐
│ factorielle(n=3)         │ ← n≠0, retourne 3 * factorielle(2)
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘

ÉTAPE 2 : factorielle(2) appelée
┌──────────────────────────┐
│ factorielle(n=2)         │ ← n≠0, retourne 2 * factorielle(1)
├──────────────────────────┤
│ factorielle(n=3)         │ (en attente de factorielle(2))
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘

ÉTAPE 3 : factorielle(1) appelée
┌──────────────────────────┐
│ factorielle(n=1)         │ ← n≠0, retourne 1 * factorielle(0)
├──────────────────────────┤
│ factorielle(n=2)         │ (en attente)
├──────────────────────────┤
│ factorielle(n=3)         │ (en attente)
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘

ÉTAPE 4 : factorielle(0) appelée - CAS DE BASE ATTEINT !
┌──────────────────────────┐
│ factorielle(n=0)         │ ← CAS DE BASE : retourne 1
├──────────────────────────┤
│ factorielle(n=1)         │ (en attente)
├──────────────────────────┤
│ factorielle(n=2)         │ (en attente)
├──────────────────────────┤
│ factorielle(n=3)         │ (en attente)
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘
```

**Phase de REMONTÉE** (dépilement) :

```
ÉTAPE 5 : factorielle(0) retourne 1
┌──────────────────────────┐
│ factorielle(n=1)         │ ← Reçoit 1, calcule 1 * 1 = 1
├──────────────────────────┤
│ factorielle(n=2)         │
├──────────────────────────┤
│ factorielle(n=3)         │
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘

ÉTAPE 6 : factorielle(1) retourne 1
┌──────────────────────────┐
│ factorielle(n=2)         │ ← Reçoit 1, calcule 2 * 1 = 2
├──────────────────────────┤
│ factorielle(n=3)         │
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘

ÉTAPE 7 : factorielle(2) retourne 2
┌──────────────────────────┐
│ factorielle(n=3)         │ ← Reçoit 2, calcule 3 * 2 = 6
├──────────────────────────┤
│ Contexte Global          │
└──────────────────────────┘

ÉTAPE 8 : factorielle(3) retourne 6
┌──────────────────────────┐
│ Contexte Global          │ ← Reçoit 6, affiche 6
└──────────────────────────┘
```

---

### Tableau Récapitulatif

| Étape | Pile (sommet à droite)                         | Action         | Valeur retournée |
| ----- | ---------------------------------------------- | -------------- | ---------------- |
| 1     | `[Global, fact(3)]`                            | Empile fact(3) | -                |
| 2     | `[Global, fact(3), fact(2)]`                   | Empile fact(2) | -                |
| 3     | `[Global, fact(3), fact(2), fact(1)]`          | Empile fact(1) | -                |
| 4     | `[Global, fact(3), fact(2), fact(1), fact(0)]` | Cas de base    | **1**            |
| 5     | `[Global, fact(3), fact(2), fact(1)]`          | Dépile fact(0) | **1**            |
| 6     | `[Global, fact(3), fact(2)]`                   | Dépile fact(1) | **1**            |
| 7     | `[Global, fact(3)]`                            | Dépile fact(2) | **2**            |
| 8     | `[Global]`                                     | Dépile fact(3) | **6**            |

---

## 📝 Micro-Exercice #2 : Tracer la Pile Récursive

**Objectif :** Tracer la pile pour une fonction de somme récursive.

**Instructions :** Tracez l'état de la pile pour `sommeJusqua(4)` :

```javascript
function sommeJusqua(n) {
  if (n === 1) {
    return 1;
  }
  return n + sommeJusqua(n - 1);
}
console.log(sommeJusqua(4)); // 10
```

<details>
<summary>💡 Voir la solution</summary>

**Phase de descente :**

| Étape | Pile                                               | Action                  |
| ----- | -------------------------------------------------- | ----------------------- |
| 1     | `[Global, somme(4)]`                               | 4 ≠ 1, appelle somme(3) |
| 2     | `[Global, somme(4), somme(3)]`                     | 3 ≠ 1, appelle somme(2) |
| 3     | `[Global, somme(4), somme(3), somme(2)]`           | 2 ≠ 1, appelle somme(1) |
| 4     | `[Global, somme(4), somme(3), somme(2), somme(1)]` | CAS DE BASE             |

**Phase de remontée :**

| Étape | Pile                                     | Calcul | Retour |
| ----- | ---------------------------------------- | ------ | ------ |
| 5     | `[Global, somme(4), somme(3), somme(2)]` | -      | 1      |
| 6     | `[Global, somme(4), somme(3)]`           | 2 + 1  | 3      |
| 7     | `[Global, somme(4)]`                     | 3 + 3  | 6      |
| 8     | `[Global]`                               | 4 + 6  | **10** |

**Explication :** La pile atteint une profondeur de 4 niveaux avant de commencer à dépiler et calculer les résultats.

</details>

---

## 💥 L'Erreur Stack Overflow

La pile d'appels a une **taille limitée**. Si une fonction récursive n'atteint jamais son cas de base, elle empile indéfiniment des cadres jusqu'à dépasser la limite.

---

### Qu'est-ce qui Cause un Stack Overflow ?

| Cause                       | Description                                     |
| --------------------------- | ----------------------------------------------- |
| **Pas de cas de base**      | La fonction n'a aucune condition d'arrêt        |
| **Cas de base incorrect**   | La condition ne sera jamais vraie               |
| **Réduction incorrecte**    | Le paramètre ne se rapproche pas du cas de base |
| **Récursion trop profonde** | Le problème nécessite trop d'appels             |

---

### Exemple 1 : Récursion Infinie (Pas de Cas de Base)

```javascript
// DANGER : Cette fonction n'a pas de cas de base !
function boucleInfinie() {
  boucleInfinie(); // S'appelle indéfiniment
}

// NE PAS EXÉCUTER - causera un Stack Overflow !
// boucleInfinie();
```

**Ce qui se passe :**

```
┌──────────────────────┐
│ boucleInfinie()      │
├──────────────────────┤
│ boucleInfinie()      │
├──────────────────────┤
│ boucleInfinie()      │
├──────────────────────┤
│ ... (des milliers)   │
├──────────────────────┤
│  STACK OVERFLOW !    │
└──────────────────────┘
```

---

### Exemple 2 : Réduction Incorrecte

```javascript
// DANGER : n augmente au lieu de diminuer !
function compteARebours(n) {
  console.log(n);
  if (n > 0) {
    compteARebours(n + 1); // Erreur : n+1 au lieu de n-1 !
  }
}

// NE PAS EXÉCUTER avec une valeur positive !
// compteARebours(5); // Stack Overflow !
```

**Le problème :** `n` s'éloigne du cas de base au lieu de s'en rapprocher.

---

### Exemple 3 : Cas de Base Jamais Atteint

```javascript
// DANGER : Le cas de base teste n === 0, mais n commence à 1
// et diminue de 2, donc n passera de 1 à -1, -3, -5...
function casBaseManque(n) {
  if (n === 0) {
    // Jamais vrai pour n = 1, -1, -3, -5...
    return 0;
  }
  return n + casBaseManque(n - 2);
}

// casBaseManque(5); // Stack Overflow car 5→3→1→-1→-3→...
```

**La correction :**

```javascript
// CORRECT : Utiliser <= au lieu de ===
function casBaseCorrige(n) {
  if (n <= 0) {
    // Maintenant atteint pour n = 0, -1, -2...
    return 0;
  }
  return n + casBaseCorrige(n - 2);
}

console.log(casBaseCorrige(5)); // 5 + 3 + 1 + 0 = 9
```

---

### Limite de la Pile en JavaScript

La taille de la pile varie selon les environnements :

| Environnement | Limite approximative                   |
| ------------- | -------------------------------------- |
| Chrome        | ~10 000 - 15 000 appels                |
| Firefox       | ~30 000 - 50 000 appels                |
| Node.js       | ~10 000 - 15 000 appels (configurable) |

> **Attention**
>
> Même avec un cas de base correct, si votre problème nécessite plus d'appels que la limite, vous aurez un Stack Overflow. Dans ce cas, préférez une solution itérative ou utilisez la récursion terminale (tail recursion).

---

## 📝 Micro-Exercice #3 : Identifier le Problème

**Objectif :** Diagnostiquer et corriger une récursion problématique.

**Instructions :** Cette fonction cause un Stack Overflow. Pourquoi ? Comment la corriger ?

```javascript
function compteurBroken(n) {
  console.log(n);
  if (n > 0) {
    compteurBroken(n + 1); // Ligne problématique
  }
}
// compteurBroken(5);
```

<details>
<summary>💡 Voir la solution</summary>

**Problème :** La fonction appelle `compteurBroken(n + 1)` au lieu de `compteurBroken(n - 1)`. Donc n augmente (6, 7, 8, 9...) et ne sera jamais ≤ 0.

**Correction :**

```javascript
function compteurCorrige(n) {
  console.log(n);
  if (n > 0) {
    compteurCorrige(n - 1); // Maintenant n diminue vers 0
  }
}

compteurCorrige(5);
// Affiche : 5, 4, 3, 2, 1, 0
```

**Explication :** L'appel récursif doit **toujours** rapprocher le paramètre du cas de base. Ici, le cas de base est `n <= 0`, donc n doit diminuer à chaque appel.

</details>

---

## 💻 Application Pratique : Visualiser la Pile

Voyons comment visualiser et déboguer la pile d'appels en pratique.

---

### Exemple 1 : Traçage de Fibonacci

La fonction Fibonacci génère un arbre d'appels plus complexe :

```javascript
function fibonacci(n) {
  if (n <= 0) return 0;
  if (n === 1) return 1;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(4)); // 3
```

**Arbre d'appels pour fibonacci(4) :**

```
fibonacci(4)
├── fibonacci(3)          ← Premier appel récursif
│   ├── fibonacci(2)
│   │   ├── fibonacci(1) → 1
│   │   └── fibonacci(0) → 0
│   │   └── retourne 1
│   └── fibonacci(1) → 1
│   └── retourne 2
└── fibonacci(2)          ← Deuxième appel récursif
    ├── fibonacci(1) → 1
    └── fibonacci(0) → 0
    └── retourne 1
└── retourne 3
```

**Observation clé :** La pile ne contient jamais plus de 4 niveaux simultanément (profondeur maximale), mais `fibonacci(2)` est calculé **2 fois** !

---

### Exemple 2 : Utiliser console.trace()

JavaScript offre `console.trace()` pour afficher l'état de la pile :

```javascript
function niveau3() {
  console.trace("Pile d'appels actuelle");
}

function niveau2() {
  niveau3();
}

function niveau1() {
  niveau2();
}

niveau1();
```

**Sortie dans la console :**

```
Trace: Pile d'appels actuelle
    at niveau3 (script.js:2:11)
    at niveau2 (script.js:6:3)
    at niveau1 (script.js:10:3)
    at Object.<anonymous> (script.js:13:1)
```

---

### Exemple 3 : Fonction Récursive avec Traçage

Ajoutons du traçage à notre factorielle pour visualiser la pile :

```javascript
function factorielleTracee(n, profondeur = 0) {
  const indentation = "  ".repeat(profondeur);
  console.log(`${indentation}→ factorielle(${n}) appelée`);

  if (n === 0) {
    console.log(`${indentation}← factorielle(0) retourne 1 (cas de base)`);
    return 1;
  }

  const resultat = n * factorielleTracee(n - 1, profondeur + 1);
  console.log(`${indentation}← factorielle(${n}) retourne ${resultat}`);
  return resultat;
}

console.log("Résultat final :", factorielleTracee(4));
```

**Sortie :**

```
→ factorielle(4) appelée
  → factorielle(3) appelée
    → factorielle(2) appelée
      → factorielle(1) appelée
        → factorielle(0) appelée
        ← factorielle(0) retourne 1 (cas de base)
      ← factorielle(1) retourne 1
    ← factorielle(2) retourne 2
  ← factorielle(3) retourne 6
← factorielle(4) retourne 24
Résultat final : 24
```

**Analyse :** L'indentation montre visuellement la profondeur de la pile. On voit clairement la descente puis la remontée.

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension de la pile d'appels, complétez les exercices suivants.

---

### Exercice 1 : Tracer la Pile (Basique)

**Objectif :** Tracer manuellement l'état de la pile.

**Instructions :** Tracez l'état de la pile pour le code suivant :

```javascript
function multiplier(a, b) {
  return a * b;
}

function calculer(x, y) {
  let resultat = multiplier(x, y);
  return resultat + 10;
}

console.log(calculer(5, 3));
```

<details>
<summary>💡 Voir la solution</summary>

| Étape | Action                      | Pile                                       |
| ----- | --------------------------- | ------------------------------------------ |
| 1     | Script démarre              | `[Global]`                                 |
| 2     | `calculer(5, 3)` appelée    | `[Global, calculer(5,3)]`                  |
| 3     | `multiplier(5, 3)` appelée  | `[Global, calculer(5,3), multiplier(5,3)]` |
| 4     | `multiplier` retourne 15    | `[Global, calculer(5,3)]`                  |
| 5     | `calculer` calcule 15+10=25 | `[Global, calculer(5,3)]`                  |
| 6     | `calculer` retourne 25      | `[Global]`                                 |
| 7     | `console.log(25)`           | Script termine                             |

</details>

---

### Exercice 2 : Tracer la Pile (Récursif)

**Objectif :** Tracer une fonction de puissance récursive.

**Instructions :** Tracez l'état de la pile pour `puissance(2, 3)` :

```javascript
function puissance(base, exposant) {
  if (exposant === 0) {
    return 1;
  }
  return base * puissance(base, exposant - 1);
}

console.log(puissance(2, 3)); // 8
```

<details>
<summary>💡 Voir la solution</summary>

**Phase de descente :**

| Étape | Pile                                                                       | Action                        |
| ----- | -------------------------------------------------------------------------- | ----------------------------- |
| 1     | `[Global, puissance(2,3)]`                                                 | 3 ≠ 0, appelle puissance(2,2) |
| 2     | `[Global, puissance(2,3), puissance(2,2)]`                                 | 2 ≠ 0, appelle puissance(2,1) |
| 3     | `[Global, puissance(2,3), puissance(2,2), puissance(2,1)]`                 | 1 ≠ 0, appelle puissance(2,0) |
| 4     | `[Global, puissance(2,3), puissance(2,2), puissance(2,1), puissance(2,0)]` | CAS DE BASE                   |

**Phase de remontée :**

| Étape | Pile                                                       | Calcul | Retour |
| ----- | ---------------------------------------------------------- | ------ | ------ |
| 5     | `[Global, puissance(2,3), puissance(2,2), puissance(2,1)]` | -      | 1      |
| 6     | `[Global, puissance(2,3), puissance(2,2)]`                 | 2 × 1  | 2      |
| 7     | `[Global, puissance(2,3)]`                                 | 2 × 2  | 4      |
| 8     | `[Global]`                                                 | 2 × 4  | **8**  |

</details>

---

### Exercice 3 : Identifier et Corriger

**Objectif :** Diagnostiquer un problème de récursion.

**Instructions :** Cette fonction cause un Stack Overflow. Identifiez le problème et proposez une correction.

```javascript
function compteARebours(n) {
  console.log(n);
  if (n > 0) {
    compteARebours(n + 1); // Ligne problématique
  }
}
```

<details>
<summary>💡 Voir la solution</summary>

**Problème :** La ligne `compteARebours(n + 1)` fait que n **augmente** au lieu de **diminuer**. Le cas de base `n > 0` ne sera jamais faux car n va 5, 6, 7, 8...

**Correction :**

```javascript
function compteARebours(n) {
  console.log(n);
  if (n > 0) {
    compteARebours(n - 1); // n diminue vers 0
  }
}

compteARebours(5);
// Affiche : 5, 4, 3, 2, 1, 0
```

**Règle :** L'appel récursif doit toujours rapprocher le paramètre du cas de base !

</details>

---

### Exercice 4 : Ajouter du Traçage

**Objectif :** Ajouter du traçage pour visualiser la pile.

**Instructions :** Modifiez cette fonction pour afficher l'indentation selon la profondeur :

```javascript
function sommeTableau(tableau) {
  if (tableau.length === 0) {
    return 0;
  }
  return tableau[0] + sommeTableau(tableau.slice(1));
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function sommeTableauTracee(tableau, profondeur = 0) {
  const indent = "  ".repeat(profondeur);
  console.log(`${indent}→ sommeTableau([${tableau}]) appelée`);

  if (tableau.length === 0) {
    console.log(`${indent}← retourne 0 (cas de base)`);
    return 0;
  }

  const premier = tableau[0];
  const reste = tableau.slice(1);
  const sommeReste = sommeTableauTracee(reste, profondeur + 1);
  const resultat = premier + sommeReste;

  console.log(`${indent}← retourne ${premier} + ${sommeReste} = ${resultat}`);
  return resultat;
}

console.log("Total :", sommeTableauTracee([5, 3, 8]));
```

**Sortie :**

```
→ sommeTableau([5,3,8]) appelée
  → sommeTableau([3,8]) appelée
    → sommeTableau([8]) appelée
      → sommeTableau([]) appelée
      ← retourne 0 (cas de base)
    ← retourne 8 + 0 = 8
  ← retourne 3 + 8 = 11
← retourne 5 + 11 = 16
Total : 16
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quel principe régit le fonctionnement de la pile d'appels ?**

- [ ] A. FIFO (First-In, First-Out)
- [ ] B. LIFO (Last-In, First-Out)
- [ ] C. Aléatoire
- [ ] D. Alphabétique

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La pile d'appels fonctionne selon le principe **LIFO** : la dernière fonction empilée est la première à être dépilée. C'est comme une pile d'assiettes.

</details>

---

### Question 2

**Que contient un cadre d'exécution (stack frame) ?**

- [ ] A. Uniquement le nom de la fonction
- [ ] B. Les arguments, variables locales et adresse de retour
- [ ] C. Toutes les fonctions du programme
- [ ] D. Le code source de la fonction

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Un cadre d'exécution contient les **arguments**, les **variables locales**, l'**adresse de retour** et le contexte `this` de la fonction.

</details>

---

### Question 3

**Qu'est-ce qui cause une erreur Stack Overflow ?**

- [ ] A. Trop de variables dans une fonction
- [ ] B. Une fonction qui ne retourne pas de valeur
- [ ] C. Une récursion sans cas de base ou avec trop d'appels
- [ ] D. Un tableau trop grand

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le Stack Overflow survient quand la pile dépasse sa limite, généralement à cause d'une **récursion infinie** (pas de cas de base) ou d'une récursion trop profonde.

</details>

---

### Question 4

**Dans `factorielle(3)`, combien de cadres sont empilés au maximum ?**

- [ ] A. 3
- [ ] B. 4
- [ ] C. 5
- [ ] D. 6

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

**5 cadres** : Contexte Global, factorielle(3), factorielle(2), factorielle(1), factorielle(0). Le cas de base (n=0) est le dernier empilé avant le dépilement.

</details>

---

### Question 5

**Quelle commande JavaScript affiche la pile d'appels actuelle ?**

- [ ] A. console.log()
- [ ] B. console.stack()
- [ ] C. console.trace()
- [ ] D. console.pile()

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

`console.trace()` affiche la **pile d'appels** au moment de son exécution, montrant la chaîne des fonctions qui ont mené à ce point.

</details>

---

### Question 6

**Quelle est la taille approximative de la pile d'appels dans Chrome ?**

- [ ] A. 100 appels
- [ ] B. 1 000 appels
- [ ] C. 10 000 - 15 000 appels
- [ ] D. 1 000 000 appels

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Chrome limite la pile à environ **10 000 - 15 000 appels**. Cette limite varie selon les navigateurs et peut être configurée dans Node.js.

</details>

---

### Question 7

**Comment éviter un Stack Overflow dans une récursion ?**

- [ ] A. Utiliser plus de variables locales
- [ ] B. S'assurer que le cas de base sera atteint
- [ ] C. Ajouter des console.log()
- [ ] D. Utiliser des nombres plus petits

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La clé est de **s'assurer que le cas de base sera atteint** : chaque appel récursif doit rapprocher le paramètre du cas de base. Sans cela, la récursion est infinie.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe LIFO

La pile d'appels fonctionne selon le principe Last-In, First-Out : la dernière fonction empilée est la première dépilée.

### 2. Cadre d'Exécution

Chaque appel de fonction crée un cadre contenant les arguments, variables locales et l'adresse de retour.

### 3. Descente et Remontée

En récursion, la pile croît pendant la descente vers le cas de base, puis décroît pendant la remontée avec les calculs.

### 4. Stack Overflow

Se produit quand la pile dépasse sa limite (10 000-15 000 appels), généralement à cause d'une récursion infinie.

### 5. Causes de Récursion Infinie

Pas de cas de base, cas de base incorrect, ou paramètre qui s'éloigne du cas de base au lieu de s'en rapprocher.

### 6. console.trace()

Outil de débogage qui affiche l'état actuel de la pile d'appels.

### 7. Traçage Manuel

Technique essentielle pour comprendre et déboguer : dessiner l'état de la pile à chaque étape.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous comprenez maintenant les mécanismes internes de JavaScript lors de l'exécution récursive !

### Ce que vous avez appris aujourd'hui

- Le fonctionnement de la pile d'appels selon le principe LIFO
- La structure d'un cadre d'exécution (stack frame)
- Comment tracer manuellement l'état de la pile
- Les causes et la prévention des erreurs Stack Overflow
- L'utilisation de `console.trace()` pour le débogage
- Les techniques de traçage pour visualiser la récursion

### Compétences acquises

Vous êtes maintenant capable de :

- Tracer manuellement l'exécution d'une fonction récursive
- Diagnostiquer et corriger les problèmes de récursion infinie
- Utiliser les outils de débogage pour visualiser la pile

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Comprendre la pile d'appels est **fondamental** pour tout développeur. Au-delà de la récursion, ce mécanisme intervient dans la gestion des événements asynchrones (callback queue), les erreurs (stack trace), et le débogage en général. Un développeur qui comprend la pile peut lire une stack trace d'erreur et identifier immédiatement la chaîne d'appels qui a causé le problème.

---

## ➡️ Prochaine Étape : Leçon 24

### Ce qui vous attend

La prochaine leçon, **« Pratique : Utiliser la Récursion pour les Opérations sur Tableaux »**, mettra en application tous les concepts de récursion appris.

**Vous découvrirez :**

- Des **patterns récursifs avancés** pour manipuler les tableaux
- Comment **filtrer**, **mapper** et **réduire** récursivement
- L'application à notre **étude de cas** de gestion de tâches
- Des **comparaisons** entre approches récursives et itératives

### Préparez-vous !

Cette leçon finale du module mettra en pratique tout ce que vous avez appris sur la récursion dans des contextes réalistes !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [JavaScript Visualizer](https://ui.dev/javascript-visualizer/) - Visualisation de la pile d'appels en temps réel
- [MDN - Call Stack](https://developer.mozilla.org/fr/docs/Glossary/Call_stack) - Documentation officielle
- [Loupe - Event Loop Visualizer](http://latentflip.com/loupe/) - Comprendre la pile et la boucle d'événements

### Outils de pratique

- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez la pile d'appels pas à pas
- **Chrome DevTools** : Utilisez l'onglet Sources avec des breakpoints pour observer la pile

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour vraiment maîtriser la pile d'appels, utilisez les outils de débogage de votre navigateur ! Mettez un **breakpoint** dans une fonction récursive et observez la section "Call Stack" dans l'onglet Sources. Vous verrez la pile grandir et rétrécir en temps réel, ce qui rend le concept beaucoup plus concret.

---

**Prêt pour la Leçon 24 ?** 🚀

Rendez-vous dans la prochaine leçon pour appliquer la récursion aux opérations sur tableaux !

---

<div align="center">

**Leçon 23 sur 42 - Module 4 : Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Leçon 22 : Implémentation de Fonctions Récursives de Base en JavaScript](./lecon-4-implementation-fonctions-recursives-base-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 24 : Pratique : Utiliser la Récursion pour les Opérations sur Tableaux ➡️](./lecon-6-pratique-utiliser-recursion-operations-tableaux.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
