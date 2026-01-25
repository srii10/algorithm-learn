##### Leçon 4 sur 42

# Comprendre la Notation Big O avec des Exemples Pratiques

**Module 1** : Fondements des algorithmes et révision de JavaScript

---

## 🎯 Objectifs d'Apprentissage

À la fin de cette leçon, vous serez capable de :

- **Comprendre** la notation Big O et son rôle dans l'analyse algorithmique
- **Identifier** les complexités temporelles courantes (O(1), O(log n), O(n), O(n log n), O(n²), etc.)
- **Analyser** des fragments de code JavaScript pour déterminer leur complexité Big O
- **Comparer** différents algorithmes en fonction de leur efficacité asymptotique
- **Appliquer** les règles de simplification de la notation Big O
- **Visualiser** la croissance des différentes complexités avec des exemples concrets

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

Avant de commencer cette leçon, assurez-vous de maîtriser :

- Les concepts de base des algorithmes (Leçon 1)
- Les structures de contrôle JavaScript : boucles, conditions (Leçon 2)
- Les concepts de complexité temporelle et spatiale (Leçon 3)
- Le comptage d'opérations dans un algorithme (Leçon 3)

---

## 🚀 Introduction

Dans la leçon précédente, nous avons appris à compter les opérations d'un algorithme et avons découvert que certains algorithmes effectuent **n** opérations, d'autres **n²**, et d'autres encore un nombre constant d'opérations.

Mais compter précisément les opérations devient vite fastidieux et peu pratique. Imaginez devoir calculer que votre algorithme effectue exactement **5n² + 3n + 17** opérations !

### Le Problème du Comptage Précis

```javascript
function exempleComplexe(arr) {
  let compteur = 0; // 1 opération

  for (let i = 0; i < arr.length; i++) {
    compteur += arr[i]; // n opérations
  }

  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      console.log(arr[i] + arr[j]); // n² opérations
    }
  }

  return compteur; // 1 opération
}

// Nombre total d'opérations : n² + n + 2
```

**Questions qui se posent :**

- Doit-on vraiment compter chaque petite opération ?
- Les constantes (comme +2) sont-elles importantes ?
- Comment comparer rapidement deux algorithmes ?

### La Solution : La Notation Big O

La **notation Big O** est un langage mathématique qui nous permet de décrire l'efficacité d'un algorithme de manière **simplifiée** et **universelle**.

Au lieu de dire : "Mon algorithme effectue 5n² + 3n + 17 opérations"

On dit simplement : "Mon algorithme est en **O(n²)**"

### Pourquoi "Big O" ?

Le "O" signifie **"Order of"** (Ordre de), car on s'intéresse à **l'ordre de grandeur** de la croissance du temps d'exécution, et non aux détails précis.

**Analogie du voyage :**

Imaginons que vous planifiez un voyage en voiture de De Panne (côte belge) à Arlon (sud de la Belgique) - d'un bout à l'autre du pays.

- **Comptage précis** : "Le trajet fait exactement 276,3 km, je vais consommer 18,2 litres d'essence, traverser 47 communes, et il y a 31 virages à plus de 90°."
- **Notation Big O** : "C'est un trajet d'environ **280 km**. Je prévois environ **3 heures** de route."

La notation Big O capture l'**essentiel** : l'ordre de grandeur qui domine quand les données augmentent.

Dans cette leçon, nous allons maîtriser cette notation puissante qui est au cœur de l'analyse algorithmique moderne.

---

## 📦 1. Qu'est-ce que la Notation Big O ?

### 1.1 Définition Formelle

La **notation Big O** décrit le **comportement asymptotique** d'un algorithme, c'est-à-dire comment le temps d'exécution (ou l'espace mémoire) **croît** lorsque la taille des données **tend vers l'infini**.

**Notation mathématique :**

Un algorithme est en **O(f(n))** si son temps d'exécution est au maximum proportionnel à **f(n)** pour des valeurs suffisamment grandes de **n**.

**En termes simples :**

Big O répond à la question : **"Que se passe-t-il quand mes données deviennent TRÈS grandes ?"**

### 1.2 Le Comportement Asymptotique

Le terme **"asymptotique"** signifie qu'on s'intéresse au comportement **à long terme**, quand **n devient très grand**.

**Exemple concret :**

Considérons deux algorithmes :

- **Algorithme A** : effectue **100n** opérations
- **Algorithme B** : effectue **n²** opérations

**Pour de petites valeurs :**

- n = 10 : A fait 1 000 opérations, B fait 100 opérations → B est plus rapide
- n = 50 : A fait 5 000 opérations, B fait 2 500 opérations → B est encore plus rapide

**Mais pour de grandes valeurs :**

- n = 1 000 : A fait 100 000 opérations, B fait 1 000 000 opérations → A est 10× plus rapide
- n = 10 000 : A fait 1 000 000 opérations, B fait 100 000 000 opérations → A est 100× plus rapide !

**Conclusion :** Bien que B soit plus rapide au début, **A devient largement supérieur** quand n augmente. On dit que A est en **O(n)** et B est en **O(n²)**.

### 1.3 Visualisation de la Croissance

Imaginons une bibliothèque qui s'agrandit au fil du temps :

| Nombre de livres (n) | O(1) Constant | O(log n) Logarithmique | O(n) Linéaire | O(n²) Quadratique |
| -------------------- | ------------- | ---------------------- | ------------- | ----------------- |
| 10                   | 1             | 3                      | 10            | 100               |
| 100                  | 1             | 7                      | 100           | 10 000            |
| 1 000                | 1             | 10                     | 1 000         | 1 000 000         |
| 10 000               | 1             | 13                     | 10 000        | 100 000 000       |

**Observation clé :**

- O(1) ne change jamais (génial !)
- O(log n) croît très lentement (excellent !)
- O(n) croît proportionnellement (acceptable)
- O(n²) **explose** rapidement (dangereux !)

---

### 📝 Micro-Exercice 1 : Comprendre l'Asymptotique

Deux algorithmes de recherche dans un tableau :

- **Algorithme X** : 5n + 100 opérations
- **Algorithme Y** : n² opérations

**Question 1 :** Pour n = 10, lequel est plus rapide ?

**Question 2 :** Pour n = 1 000, lequel est plus rapide ?

**Question 3 :** Quelle est la complexité Big O de chaque algorithme ?

<details>
<summary>Voir les réponses</summary>

**Réponse 1 :** Pour n = 10

- Algorithme X : 5(10) + 100 = **150 opérations**
- Algorithme Y : 10² = **100 opérations**
- **Y est plus rapide** pour n = 10

**Réponse 2 :** Pour n = 1 000

- Algorithme X : 5(1 000) + 100 = **5 100 opérations**
- Algorithme Y : 1 000² = **1 000 000 opérations**
- **X est environ 200× plus rapide** pour n = 1 000 !

**Réponse 3 :** Complexité Big O

- Algorithme X : **O(n)** (linéaire)
- Algorithme Y : **O(n²)** (quadratique)

**Leçon importante :** Les constantes (comme +100) et les coefficients (comme ×5) deviennent négligeables face à la différence entre n et n² quand n devient grand. C'est pourquoi Big O ignore ces détails.

</details>

---

## 📦 2. Les Complexités Temporelles Courantes

Passons en revue les complexités Big O que vous rencontrerez le plus souvent, de la plus efficace à la moins efficace.

### 2.1 O(1) - Temps Constant

**Définition :** L'algorithme effectue **toujours le même nombre d'opérations**, peu importe la taille des données.

**Caractéristique :** Le meilleur scénario possible ! Le temps d'exécution ne dépend pas de n.

**Exemples JavaScript :**

```javascript
// Exemple 1 : Accès à un élément de tableau par son index
function obtenirPremierElement(arr) {
  return arr[0]; // 1 opération, toujours
}

// Exemple 2 : Accès à une propriété d'objet
function obtenirNom(utilisateur) {
  return utilisateur.nom; // 1 opération, toujours
}

// Exemple 3 : Opération arithmétique
function additionner(a, b) {
  return a + b; // 1 opération, toujours
}

// Exemple 4 : Plusieurs opérations constantes
function calculerMoyenne(a, b) {
  const somme = a + b; // Opération 1
  const moyenne = somme / 2; // Opération 2
  return moyenne; // Opération 3
}
// Total : 3 opérations constantes → O(1)
```

**Analogie :** Prendre un livre sur votre bureau. Peu importe le nombre de livres dans votre bibliothèque, prendre le livre sur votre bureau prend toujours le même temps.

**Graphique de croissance :**

```
Temps
  |
  |████████████████████████  (ligne plate)
  |
  +-------------------------→ Taille des données (n)
```

---

### 2.2 O(log n) - Temps Logarithmique

**Définition :** Le temps d'exécution croît **logarithmiquement** avec la taille des données. À chaque étape, on **divise le problème en deux**.

**Caractéristique :** Extrêmement efficace ! Même avec des milliards de données, il ne faut que ~30 opérations.

**L'algorithme classique : La Recherche Binaire**

```javascript
// Recherche binaire dans un tableau TRIÉ
function rechercheBinaire(arr, cible) {
  let gauche = 0;
  let droite = arr.length - 1;

  while (gauche <= droite) {
    const milieu = Math.floor((gauche + droite) / 2);

    if (arr[milieu] === cible) {
      return milieu; // Trouvé !
    }

    if (arr[milieu] < cible) {
      gauche = milieu + 1; // Chercher dans la moitié droite
    } else {
      droite = milieu - 1; // Chercher dans la moitié gauche
    }
  }

  return -1; // Non trouvé
}

// Exemple d'utilisation
const nombres = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];
console.log(rechercheBinaire(nombres, 13)); // → 6
```

**Pourquoi O(log n) ?**

À chaque itération, on **divise l'espace de recherche par 2**.

- Tableau de 1 000 éléments : maximum **10 comparaisons** (car 2^10 = 1 024)
- Tableau de 1 000 000 éléments : maximum **20 comparaisons** (car 2^20 ≈ 1 000 000)
- Tableau de 1 000 000 000 éléments : maximum **30 comparaisons** !

**Analogie :** Chercher un mot dans le dictionnaire. Vous ouvrez au milieu, puis au milieu de la moitié appropriée, etc. Vous ne lisez jamais toutes les pages.

**Autres exemples O(log n) :**

- Arbres binaires de recherche équilibrés
- Algorithmes de type "diviser pour régner"

---

### 2.3 O(n) - Temps Linéaire

**Définition :** Le temps d'exécution croît **proportionnellement** à la taille des données.

**Caractéristique :** Acceptable et très courant. Si vous doublez les données, vous doublez le temps.

**Exemples JavaScript :**

```javascript
// Exemple 1 : Parcourir un tableau
function sommeTableau(arr) {
  let total = 0;

  for (let i = 0; i < arr.length; i++) {
    total += arr[i]; // Opération effectuée n fois
  }

  return total;
}

// Exemple 2 : Recherche linéaire
function rechercherElement(arr, cible) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === cible) {
      return i;
    }
  }
  return -1;
}

// Exemple 3 : Trouver le maximum
function trouverMaximum(arr) {
  if (arr.length === 0) return null;

  let max = arr[0];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }

  return max;
}

// Exemple 4 : Filtrer un tableau
function filtrerNombresPairs(arr) {
  const pairs = [];

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 === 0) {
      pairs.push(arr[i]);
    }
  }

  return pairs;
}
```

**Analogie :** Lire tous les livres d'une bibliothèque, un par un. Si la bibliothèque a 100 livres, ça prend 100 unités de temps. Si elle en a 1 000, ça prend 1 000 unités.

**Règle importante :** Une seule boucle qui parcourt n éléments = O(n)

---

### 📝 Micro-Exercice 2 : Identifier O(1), O(log n) et O(n)

Pour chacune des fonctions suivantes, déterminez la complexité temporelle :

```javascript
// Fonction A
function fonctionA(arr) {
  return arr[arr.length - 1];
}

// Fonction B
function fonctionB(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}

// Fonction C
function fonctionC(n) {
  let compteur = 1;
  while (compteur < n) {
    compteur = compteur * 2;
  }
  return compteur;
}
```

<details>
<summary>Voir les réponses</summary>

**Fonction A : O(1)**

- Accède directement au dernier élément du tableau
- Nombre d'opérations : 1 (toujours constant)
- Ne dépend pas de la taille du tableau

**Fonction B : O(n)**

- Parcourt tous les éléments du tableau une fois
- Nombre d'opérations : n (proportionnel à la taille)
- Boucle simple qui itère n fois

**Fonction C : O(log n)**

- À chaque itération, on **double** le compteur
- Le compteur atteint n après log₂(n) itérations
- Exemple : pour n = 1 000, seulement ~10 itérations
- C'est l'inverse de la division par 2 de la recherche binaire

</details>

---

### 2.4 O(n log n) - Temps Linéarithmique

**Définition :** Combinaison de O(n) et O(log n). Souvent le résultat d'algorithmes qui **divisent le problème** (log n) puis **traitent chaque partie** (n).

**Caractéristique :** Très efficace pour les problèmes complexes. C'est la meilleure complexité possible pour le tri par comparaison.

**L'algorithme classique : Le Tri Fusion (Merge Sort)**

```javascript
function triFusion(arr) {
  // Cas de base : tableau de 0 ou 1 élément déjà trié
  if (arr.length <= 1) {
    return arr;
  }

  // Diviser le tableau en deux moitiés (log n niveaux)
  const milieu = Math.floor(arr.length / 2);
  const gauche = arr.slice(0, milieu);
  const droite = arr.slice(milieu);

  // Trier récursivement chaque moitié
  return fusionner(triFusion(gauche), triFusion(droite));
}

function fusionner(gauche, droite) {
  const resultat = [];
  let i = 0;
  let j = 0;

  // Fusionner les deux tableaux triés (O(n) pour chaque niveau)
  while (i < gauche.length && j < droite.length) {
    if (gauche[i] < droite[j]) {
      resultat.push(gauche[i]);
      i++;
    } else {
      resultat.push(droite[j]);
      j++;
    }
  }

  // Ajouter les éléments restants
  return resultat.concat(gauche.slice(i)).concat(droite.slice(j));
}

// Exemple d'utilisation
const nombres = [64, 34, 25, 12, 22, 11, 90];
console.log(triFusion(nombres)); // → [11, 12, 22, 25, 34, 64, 90]
```

**Pourquoi O(n log n) ?**

1. On divise le tableau en deux à chaque niveau (**log n niveaux** de récursion)
2. À chaque niveau, on traite **tous les n éléments** lors de la fusion
3. Total : **n × log n** opérations

**Visualisation pour n = 8 éléments :**

```
Niveau 0:  [64, 34, 25, 12, 22, 11, 90, 5]           ← 8 éléments à traiter
              ↙                           ↘
Niveau 1:  [64, 34, 25, 12]        [22, 11, 90, 5]   ← 8 éléments à traiter
            ↙         ↘             ↙           ↘
Niveau 2: [64,34]  [25,12]      [22,11]     [90,5]   ← 8 éléments à traiter
          ↙   ↘    ↙   ↘        ↙   ↘       ↙   ↘
Niveau 3: [64][34][25][12]    [22][11]   [90] [5]    ← 8 éléments à traiter

3 niveaux (log₂ 8 = 3) × 8 éléments par niveau = 24 opérations
```

**Autres algorithmes O(n log n) :**

- Tri rapide (Quick Sort) en moyenne
- Tri par tas (Heap Sort)
- Certains algorithmes de traitement de données

**Analogie :** Organiser une bibliothèque en divisant les livres en sections, puis en organisant chaque section individuellement.

---

### 2.5 O(n²) - Temps Quadratique

**Définition :** Le temps d'exécution est proportionnel au **carré** de la taille des données.

**Caractéristique :** Acceptable pour de petites données, mais devient rapidement problématique.

**Indicateur classique :** Boucles imbriquées où chaque boucle parcourt n éléments.

**Exemples JavaScript :**

```javascript
// Exemple 1 : Tri à bulles (Bubble Sort)
function triABulles(arr) {
  const n = arr.length;

  // Boucle externe : n itérations
  for (let i = 0; i < n; i++) {
    // Boucle interne : n itérations pour chaque i
    for (let j = 0; j < n - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        // Échanger les éléments
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }

  return arr;
}

// Exemple 2 : Trouver tous les doublons
function trouverDoublons(arr) {
  const doublons = [];

  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j] && !doublons.includes(arr[i])) {
        doublons.push(arr[i]);
      }
    }
  }

  return doublons;
}

// Exemple 3 : Comparer tous les couples
function comparerTousCouples(arr) {
  const comparaisons = [];

  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      comparaisons.push([arr[i], arr[j]]);
    }
  }

  return comparaisons;
}
// Si arr a 100 éléments, cette fonction fait 10 000 comparaisons !
```

**Comptage des opérations :**

Pour des boucles imbriquées :

```javascript
for (let i = 0; i < n; i++) {
  // n itérations
  for (let j = 0; j < n; j++) {
    // n itérations pour chaque i
    // Opération simple
  }
}
// Total : n × n = n² opérations
```

**Impact de la croissance :**

| n (éléments) | Opérations (n²) | Temps estimé (1 op = 1µs) |
| ------------ | --------------- | ------------------------- |
| 10           | 100             | 0.1 ms                    |
| 100          | 10 000          | 10 ms                     |
| 1 000        | 1 000 000       | 1 seconde                 |
| 10 000       | 100 000 000     | 100 secondes              |

**Analogie :** Comparer chaque personne d'une salle avec toutes les autres personnes pour voir si elles se connaissent. Avec 100 personnes, ça fait 10 000 comparaisons !

---

### 2.6 O(2^n) - Temps Exponentiel

**Définition :** Le temps d'exécution **double** à chaque ajout d'un élément.

**Caractéristique :** **DANGER !** Devient rapidement inutilisable, même pour de petites valeurs de n.

**L'exemple classique : Suite de Fibonacci récursive (naïve)**

```javascript
function fibonacci(n) {
  // Cas de base
  if (n <= 1) {
    return n;
  }

  // Calcul récursif : deux appels pour chaque appel
  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(5)); // → 5 (rapide)
console.log(fibonacci(10)); // → 55 (encore rapide)
console.log(fibonacci(30)); // → 832040 (commence à ralentir)
console.log(fibonacci(40)); // → attend plusieurs secondes...
console.log(fibonacci(50)); // → vous pouvez aller prendre un café
```

**Pourquoi O(2^n) ?**

Chaque appel de fonction génère **deux nouveaux appels** :

```
                    fibonacci(5)
                   /            \
           fibonacci(4)          fibonacci(3)
           /          \           /         \
    fibonacci(3)  fibonacci(2) fibonacci(2) fibonacci(1)
      /      \      /      \     /      \
    ...      ...  ...     ... ...      ...
```

Pour fibonacci(n), on fait environ 2^n appels de fonction !

**Impact catastrophique :**

| n   | Opérations (≈2^n) | Temps estimé (1 op = 1µs) |
| --- | ----------------- | ------------------------- |
| 10  | 1 024             | 1 ms                      |
| 20  | 1 048 576         | 1 seconde                 |
| 30  | 1 073 741 824     | 18 minutes                |
| 40  | 1 099 511 627 776 | 12 jours !                |

**Autres exemples O(2^n) :**

- Générer tous les sous-ensembles d'un ensemble
- Problèmes de force brute sans optimisation
- Certains algorithmes récursifs mal optimisés

**Analogie :** Une chaîne de lettres où chaque personne doit envoyer le message à deux autres personnes. Après 30 itérations, plus d'un milliard de personnes sont impliquées !

---

### 2.7 O(n!) - Temps Factoriel

**Définition :** Le temps d'exécution croît de manière **factorielle** : n! = n × (n-1) × (n-2) × ... × 1

**Caractéristique :** **EXTRÊMEMENT DANGEREUX !** Pratiquement inutilisable au-delà de n = 10-12.

**L'exemple classique : Générer toutes les permutations**

```javascript
function genererPermutations(arr) {
  const resultat = [];

  // Cas de base
  if (arr.length === 0) {
    return [[]];
  }

  // Pour chaque élément, générer toutes les permutations du reste
  for (let i = 0; i < arr.length; i++) {
    const element = arr[i];
    const reste = arr.slice(0, i).concat(arr.slice(i + 1));
    const permutationsReste = genererPermutations(reste);

    for (let perm of permutationsReste) {
      resultat.push([element, ...perm]);
    }
  }

  return resultat;
}

// Exemple
console.log(genererPermutations([1, 2, 3]));
// → [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
// 3! = 6 permutations
```

**Impact catastrophique :**

| n   | n! (permutations) | Temps estimé (1 op = 1µs) |
| --- | ----------------- | ------------------------- |
| 5   | 120               | 0.12 ms                   |
| 10  | 3 628 800         | 3.6 secondes              |
| 12  | 479 001 600       | 8 minutes                 |
| 15  | 1 307 674 368 000 | 15 jours                  |
| 20  | 2.4 × 10^18       | 77 000 ans !              |

**Le problème du voyageur de commerce :**

Un problème classique en O(n!) : trouver le plus court chemin qui visite n villes exactement une fois.

Avec seulement **20 villes**, tester toutes les routes possibles prendrait **77 000 ans** !

**Analogie :** Organiser un emploi du temps où chaque tâche peut être faite dans n'importe quel ordre. Avec 10 tâches, il y a plus de 3 millions d'ordres possibles à considérer.

---

### 📝 Micro-Exercice 3 : Comparer les Complexités

Classez ces complexités de la **plus efficace** à la **moins efficace** pour n = 1 000 000 :

- A. O(n²)
- B. O(1)
- C. O(n log n)
- D. O(log n)
- E. O(n)
- F. O(2^n)

**Question bonus :** Calculez le nombre approximatif d'opérations pour chaque complexité avec n = 1 000 000.

<details>
<summary>Voir les réponses</summary>

**Classement (du plus efficace au moins efficace) :**

1. **B. O(1)** - Temps constant
2. **D. O(log n)** - Temps logarithmique
3. **E. O(n)** - Temps linéaire
4. **C. O(n log n)** - Temps linéarithmique
5. **A. O(n²)** - Temps quadratique
6. **F. O(2^n)** - Temps exponentiel (catastrophique !)

**Nombre d'opérations pour n = 1 000 000 :**

- O(1) : **1** opération
- O(log n) : **≈ 20** opérations (log₂ 1 000 000 ≈ 19.93)
- O(n) : **1 000 000** opérations
- O(n log n) : **≈ 20 000 000** opérations
- O(n²) : **1 000 000 000 000** opérations (1 trillion !)
- O(2^n) : **2^1000000** opérations (un nombre avec ~300 000 chiffres - littéralement impossible)

**Visualisation des différences :**

```
O(1)         : █
O(log n)     : ████
O(n)         : ████████████████████ (échelle : 1 barre = 50 000 ops)
O(n log n)   : ████████████████████████████████████████ (400 barres)
O(n²)        : [ne rentre pas sur la page - 20 millions de barres]
O(2^n)       : [dépasse la capacité de calcul de l'univers entier]
```

**Leçon essentielle :** La différence entre les complexités devient **dramatique** pour les grandes valeurs de n. C'est pourquoi choisir le bon algorithme est crucial !

</details>

---

## 📦 3. Les Règles de Simplification de Big O

Maintenant que nous connaissons les complexités courantes, apprenons les **règles** pour simplifier les expressions complexes.

### 3.1 Règle 1 : Ignorer les Constantes

**Règle :** Les coefficients multiplicatifs sont ignorés dans la notation Big O.

**Pourquoi ?** Parce que Big O s'intéresse au **taux de croissance**, pas aux détails constants.

**Exemples :**

```javascript
// Fonction A : 3n opérations
function fonctionA(arr) {
  console.log(arr[0]); // 1 opération
  console.log(arr[0]); // 1 opération
  console.log(arr[0]); // 1 opération

  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]); // n opérations
  }
}
// Total : 3 + n opérations
// Big O : O(n) - on ignore la constante 3
```

```javascript
// Fonction B : 5n opérations
function fonctionB(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]); // n opérations
    console.log(arr[i] * 2); // n opérations
    console.log(arr[i] * 3); // n opérations
    console.log(arr[i] * 4); // n opérations
    console.log(arr[i] * 5); // n opérations
  }
}
// Total : 5n opérations
// Big O : O(n) - on ignore le coefficient 5
```

**Justification mathématique :**

Quand n devient très grand, la différence entre 5n et n est négligeable par rapport à la différence entre n et n².

- Pour n = 1 000 000 : 5n = 5 000 000
- Pour n = 1 000 000 : n² = 1 000 000 000 000

La différence entre 5n et n (5 millions vs 1 million) est **minuscule** comparée à la différence entre n et n² (1 million vs 1 trillion).

**Exemples de simplification :**

- O(2n) → **O(n)**
- O(500) → **O(1)**
- O(13n²) → **O(n²)**
- O(½n) → **O(n)**

---

### 3.2 Règle 2 : Garder Seulement le Terme Dominant

**Règle :** Dans une expression avec plusieurs termes, on garde **seulement le terme qui croît le plus vite**.

**Pourquoi ?** Le terme dominant "écrase" tous les autres quand n devient grand.

**Exemples :**

```javascript
// Fonction avec n² + n
function fonctionComplexe(arr) {
  // Première boucle : n opérations
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }

  // Boucles imbriquées : n² opérations
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      console.log(arr[i] + arr[j]);
    }
  }
}
// Total : n² + n opérations
// Big O : O(n²) - on garde seulement n², le terme dominant
```

**Visualisation de la domination :**

Pour n = 1 000 :

- n² = 1 000 000
- n = 1 000
- n² + n = 1 001 000

Le terme n² représente **99,9%** du total ! Le terme n est négligeable.

**Hiérarchie de domination :**

```
O(1) << O(log n) << O(n) << O(n log n) << O(n²) << O(n³) << O(2^n) << O(n!)
```

Le symbole `<<` signifie "est dominé par" ou "croît beaucoup plus lentement que".

**Exemples de simplification :**

- O(n² + n) → **O(n²)**
- O(n² + 1000n + 5000) → **O(n²)**
- O(n log n + n) → **O(n log n)**
- O(2^n + n³) → **O(2^n)**
- O(5 + log n + n) → **O(n)**

---

### 3.3 Règle 3 : Analyser le Pire Cas

**Règle :** Par défaut, Big O décrit la complexité dans le **pire scénario** possible.

**Pourquoi ?** Pour garantir une borne supérieure fiable. On veut savoir : "Dans le pire des cas, combien de temps mon algorithme va-t-il prendre ?"

**Exemple : Recherche linéaire**

```javascript
function rechercherElement(arr, cible) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === cible) {
      return i; // Trouvé ! On s'arrête ici
    }
  }
  return -1; // Non trouvé
}
```

**Analyse des différents cas :**

1. **Meilleur cas** : l'élément est en première position → 1 opération → O(1)
2. **Cas moyen** : l'élément est quelque part au milieu → n/2 opérations → O(n)
3. **Pire cas** : l'élément est en dernière position ou absent → n opérations → **O(n)**

**On dit que la recherche linéaire est en O(n)**, car c'est sa complexité dans le pire cas.

**Autre exemple : Tri à bulles optimisé**

```javascript
function triABullesOptimise(arr) {
  let echange = true;

  while (echange) {
    echange = false;

    for (let i = 0; i < arr.length - 1; i++) {
      if (arr[i] > arr[i + 1]) {
        [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
        echange = true;
      }
    }
  }

  return arr;
}
```

**Analyse :**

- **Meilleur cas** : tableau déjà trié → 1 passage → O(n)
- **Pire cas** : tableau trié à l'envers → n passages × n comparaisons → **O(n²)**

**On dit que le tri à bulles est en O(n²)**, même s'il peut être plus rapide dans certains cas.

**Notation complémentaire :**

- **O(f(n))** : borne supérieure (pire cas) - LA PLUS UTILISÉE
- **Ω(f(n))** (Omega) : borne inférieure (meilleur cas)
- **Θ(f(n))** (Theta) : borne exacte (meilleur cas = pire cas)

Dans ce cours, quand on dit "Big O", on parle toujours du **pire cas**.

---

### 📝 Micro-Exercice 4 : Appliquer les Règles de Simplification

Pour chacune des expressions suivantes, simplifiez-la en utilisant les règles de Big O :

1. O(5n + 3)
2. O(n² + 100n + 500)
3. O(2n² + n log n)
4. O(log n + 1)
5. O(3)
6. O(n³ + n² + n + 1)

<details>
<summary>Voir les réponses</summary>

**1. O(5n + 3) → O(n)**

- Règle 1 : Ignorer la constante 5 devant n
- Règle 2 : Le terme n domine la constante 3
- Résultat : O(n)

**2. O(n² + 100n + 500) → O(n²)**

- Règle 2 : n² domine 100n et 500
- Même si le coefficient de n est grand (100), n² finit toujours par dominer
- Pour n = 1000 : n² = 1 000 000 vs 100n = 100 000
- Résultat : O(n²)

**3. O(2n² + n log n) → O(n²)**

- Règle 1 : Ignorer le coefficient 2
- Règle 2 : n² domine n log n
- Pour n = 1000 : n² = 1 000 000 vs n log n ≈ 10 000
- Résultat : O(n²)

**4. O(log n + 1) → O(log n)**

- Règle 2 : log n domine la constante 1
- Pour n = 1000 : log n ≈ 10 vs 1
- Résultat : O(log n)

**5. O(3) → O(1)**

- Règle 1 : Toute constante devient O(1)
- Peu importe que ce soit 3, 100, ou 1 000 000
- Résultat : O(1)

**6. O(n³ + n² + n + 1) → O(n³)**

- Règle 2 : n³ domine tous les autres termes
- Pour n = 100 :
  - n³ = 1 000 000
  - n² = 10 000 (1% de n³)
  - n = 100 (0.01% de n³)
  - 1 = négligeable
- Résultat : O(n³)

**Astuce générale :** Cherchez le terme avec la plus grande puissance ou la fonction qui croît le plus vite, ignorez tout le reste !

</details>

---

## 📦 4. Analyser la Complexité de Code JavaScript Réel

Maintenant, pratiquons l'analyse de complexité sur des exemples concrets.

### 4.1 Méthodologie d'Analyse en 4 Étapes

**Étape 1 :** Identifier les boucles et leur profondeur
**Étape 2 :** Déterminer combien d'itérations fait chaque boucle
**Étape 3 :** Multiplier les complexités des boucles imbriquées
**Étape 4 :** Appliquer les règles de simplification

### 4.2 Exemple 1 : Une Boucle Simple

```javascript
function imprimerElements(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}
```

**Analyse :**

- 1 boucle qui parcourt n éléments
- Chaque itération fait une opération O(1)
- **Complexité : O(n)**

### 4.3 Exemple 2 : Deux Boucles Consécutives

```javascript
function deuxBoucles(arr) {
  // Première boucle
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }

  // Deuxième boucle
  for (let j = 0; j < arr.length; j++) {
    console.log(arr[j] * 2);
  }
}
```

**Analyse :**

- Première boucle : O(n)
- Deuxième boucle : O(n)
- Total : O(n) + O(n) = O(2n)
- Simplification : **O(n)** (on ignore le coefficient 2)

**Règle importante :** Boucles **consécutives** (l'une après l'autre) → on **additionne**, puis on simplifie.

### 4.4 Exemple 3 : Boucles Imbriquées

```javascript
function bouclesImbriquees(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      console.log(arr[i], arr[j]);
    }
  }
}
```

**Analyse :**

- Boucle externe : n itérations
- Boucle interne : n itérations **pour chaque** itération externe
- Total : n × n = n²
- **Complexité : O(n²)**

**Règle importante :** Boucles **imbriquées** (l'une dans l'autre) → on **multiplie**.

### 4.5 Exemple 4 : Boucle avec Croissance Exponentielle

```javascript
function croissanceExponentielle(n) {
  let operations = 0;

  for (let i = 1; i < n; i = i * 2) {
    operations++;
    console.log(i);
  }

  return operations;
}

// Exemple : croissanceExponentielle(16)
// Itérations : 1, 2, 4, 8, 16
// Nombre d'itérations : 5 (car 2^5 = 32 > 16)
```

**Analyse :**

- À chaque itération, i est **multiplié par 2**
- On cherche : combien de fois peut-on doubler avant d'atteindre n ?
- Réponse : log₂(n) fois
- **Complexité : O(log n)**

**Règle importante :** Si la variable de boucle est **multipliée** ou **divisée** par une constante → O(log n)

### 4.6 Exemple 5 : Cas Complexe - Boucle Partielle

```javascript
function triangulaire(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i; j < arr.length; j++) {
      console.log(arr[i], arr[j]);
    }
  }
}
```

**Analyse détaillée :**

Pour n = 4, voici les itérations :

```
i = 0 : j va de 0 à 3  → 4 itérations
i = 1 : j va de 1 à 3  → 3 itérations
i = 2 : j va de 2 à 3  → 2 itérations
i = 3 : j va de 3 à 3  → 1 itération
```

Total : 4 + 3 + 2 + 1 = 10 itérations

**Formule mathématique :**
Somme = n + (n-1) + (n-2) + ... + 1 = **n(n+1)/2** = **n²/2 + n/2**

En Big O :

- Terme dominant : n²/2
- Ignorer le coefficient 1/2 : n²
- **Complexité : O(n²)**

**Leçon :** Même si on ne fait que "la moitié" des opérations, c'est toujours O(n²) !

### 4.7 Exemple 6 : Fonction Récursive - Fibonacci

```javascript
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

**Analyse :**

- Chaque appel génère 2 nouveaux appels
- Profondeur de récursion : n niveaux
- Nombre total d'appels : environ 2^n
- **Complexité : O(2^n)** ← TRÈS INEFFICACE

**Version optimisée avec mémoïsation :**

```javascript
function fibonacciOptimise(n, memo = {}) {
  if (n <= 1) return n;

  // Si déjà calculé, retourner le résultat stocké
  if (memo[n]) return memo[n];

  // Calculer et stocker
  memo[n] = fibonacciOptimise(n - 1, memo) + fibonacciOptimise(n - 2, memo);
  return memo[n];
}
```

**Nouvelle analyse :**

- Chaque valeur de 0 à n est calculée **une seule fois**
- Stockée dans memo et réutilisée
- **Complexité : O(n)** ← BEAUCOUP MIEUX !

C'est un exemple parfait de comment un petit changement peut transformer O(2^n) en O(n).

### 4.8 Exemple 7 : Cas Trompeur - Complexité Cachée

```javascript
function concatenerTableaux(arr1, arr2) {
  return arr1.concat(arr2);
}
```

**Première impression :** O(1) - juste un appel de méthode !

**FAUX !** L'analyse correcte :

- `concat()` doit **copier tous les éléments** de arr1 et arr2
- Si arr1 a n éléments et arr2 a m éléments :
- **Complexité : O(n + m)**

**Leçon importante :** Attention aux méthodes intégrées ! Elles peuvent cacher de la complexité.

**Autres exemples de méthodes avec complexité cachée :**

```javascript
// slice() - copie une partie du tableau
const copie = arr.slice(); // O(n) - copie tous les éléments

// includes() - recherche linéaire
arr.includes(element); // O(n) - parcourt le tableau

// indexOf() - recherche linéaire
arr.indexOf(element); // O(n) - parcourt le tableau

// join() - concatène en chaîne
arr.join(","); // O(n) - traite chaque élément

// sort() - tri
arr.sort(); // O(n log n) - algorithme de tri

// reverse() - inverse
arr.reverse(); // O(n) - parcourt et échange
```

---

## 💻 Exemples Pratiques Complets

### Exemple Pratique 1 : Système de Recherche de Contacts

Vous développez une application de contacts et devez choisir entre deux approches.

**Approche A : Recherche Linéaire**

```javascript
class GestionnaireContactsLineaire {
  constructor() {
    this.contacts = [];
  }

  ajouterContact(nom, telephone) {
    this.contacts.push({ nom, telephone });
  }

  rechercherParNom(nom) {
    // Parcours linéaire
    for (let i = 0; i < this.contacts.length; i++) {
      if (this.contacts[i].nom === nom) {
        return this.contacts[i];
      }
    }
    return null;
  }
}

// Analyse : O(n) - doit potentiellement parcourir tous les contacts
```

**Approche B : Table de Hachage (Object)**

```javascript
class GestionnaireContactsOptimise {
  constructor() {
    this.contacts = {}; // Utilise un objet comme table de hachage
  }

  ajouterContact(nom, telephone) {
    this.contacts[nom] = telephone;
  }

  rechercherParNom(nom) {
    // Accès direct par clé
    return this.contacts[nom] || null;
  }
}

// Analyse : O(1) - accès direct à la clé
```

**Comparaison de performance :**

```javascript
// Test avec 100 000 contacts
const gestionnaireA = new GestionnaireContactsLineaire();
const gestionnaireB = new GestionnaireContactsOptimise();

// Remplir avec 100 000 contacts
for (let i = 0; i < 100000; i++) {
  const nom = `Contact${i}`;
  gestionnaireA.ajouterContact(nom, `06${i}`);
  gestionnaireB.ajouterContact(nom, `06${i}`);
}

// Rechercher le dernier contact (pire cas pour A)
console.time("Linéaire");
gestionnaireA.rechercherParNom("Contact99999");
console.timeEnd("Linéaire"); // → ~2-5ms

console.time("Optimisé");
gestionnaireB.rechercherParNom("Contact99999");
console.timeEnd("Optimisé"); // → ~0.01ms

// L'approche B est environ 200-500× plus rapide !
```

**Conclusion :** Quand vous avez besoin de recherches fréquentes, O(1) bat O(n) de manière spectaculaire.

---

### Exemple Pratique 2 : Détection de Doublons

Vous devez vérifier si un tableau contient des doublons.

**Approche Naïve : O(n²)**

```javascript
function aDesDoublonsNaif(arr) {
  // Comparer chaque élément avec tous les autres
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) {
        return true; // Doublon trouvé
      }
    }
  }
  return false;
}

// Analyse : O(n²) - boucles imbriquées
// Pour 10 000 éléments : ~50 millions de comparaisons
```

**Approche Optimisée : O(n)**

```javascript
function aDesDoublonsOptimise(arr) {
  const vus = new Set();

  for (let i = 0; i < arr.length; i++) {
    if (vus.has(arr[i])) {
      return true; // Doublon trouvé
    }
    vus.add(arr[i]);
  }

  return false;
}

// Analyse : O(n) - une seule boucle, Set.has() et Set.add() sont O(1)
// Pour 10 000 éléments : ~10 000 opérations
```

**Test de performance :**

```javascript
const tableau = [];
for (let i = 0; i < 10000; i++) {
  tableau.push(Math.floor(Math.random() * 5000)); // Doublons probables
}

console.time("Naïf O(n²)");
aDesDoublonsNaif(tableau);
console.timeEnd("Naïf O(n²)"); // → ~300-500ms

console.time("Optimisé O(n)");
aDesDoublonsOptimise(tableau);
console.timeEnd("Optimisé O(n)"); // → ~1-2ms

// L'approche optimisée est environ 200-300× plus rapide !
```

**Conclusion :** Utiliser la bonne structure de données (Set) peut transformer O(n²) en O(n).

---

### Exemple Pratique 3 : Tri de Données

Vous devez trier un tableau de nombres.

**Approche Naïve : Tri à Bulles O(n²)**

```javascript
function triBulles(arr) {
  const n = arr.length;
  let echanges;

  for (let i = 0; i < n; i++) {
    echanges = false;

    for (let j = 0; j < n - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        // Échanger
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        echanges = true;
      }
    }

    // Optimisation : si aucun échange, déjà trié
    if (!echanges) break;
  }

  return arr;
}

// Analyse : O(n²) dans le pire cas
```

**Approche Optimisée : Tri Natif O(n log n)**

```javascript
function triOptimise(arr) {
  return arr.sort((a, b) => a - b);
}

// Analyse : O(n log n) - JavaScript utilise Timsort (optimisé)
```

**Test de performance :**

```javascript
function genererTableauAleatoire(taille) {
  const arr = [];
  for (let i = 0; i < taille; i++) {
    arr.push(Math.floor(Math.random() * 1000));
  }
  return arr;
}

const tableau1 = genererTableauAleatoire(5000);
const tableau2 = [...tableau1]; // Copie

console.time("Tri à Bulles O(n²)");
triBulles(tableau1);
console.timeEnd("Tri à Bulles O(n²)"); // → ~500-800ms

console.time("Tri Natif O(n log n)");
triOptimise(tableau2);
console.timeEnd("Tri Natif O(n log n)"); // → ~1-3ms

// Le tri natif est environ 200-500× plus rapide !
```

**Conclusion :** Pour le tri, utilisez toujours les méthodes natives optimisées qui implémentent des algorithmes O(n log n).

---

### Exemple Pratique 4 : Calcul de Fibonacci Optimisé

Démonstration spectaculaire de l'impact de l'optimisation.

**Version Récursive Naïve : O(2^n)**

```javascript
function fibonacciRecursif(n) {
  if (n <= 1) return n;
  return fibonacciRecursif(n - 1) + fibonacciRecursif(n - 2);
}

// Essayez : fibonacciRecursif(40) prend plusieurs secondes !
```

**Version avec Mémoïsation : O(n)**

```javascript
function fibonacciMemo(n, memo = {}) {
  if (n <= 1) return n;
  if (memo[n]) return memo[n];

  memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
  return memo[n];
}

// fibonacciMemo(40) est instantané !
```

**Version Itérative : O(n) avec O(1) en espace**

```javascript
function fibonacciIteratif(n) {
  if (n <= 1) return n;

  let precedent = 0;
  let courant = 1;

  for (let i = 2; i <= n; i++) {
    const suivant = precedent + courant;
    precedent = courant;
    courant = suivant;
  }

  return courant;
}

// Optimal en temps ET en espace !
```

**Test de performance :**

```javascript
console.time("Récursif O(2^n) - n=40");
console.log(fibonacciRecursif(40));
console.timeEnd("Récursif O(2^n) - n=40"); // → ~3-5 secondes

console.time("Mémoïsation O(n) - n=40");
console.log(fibonacciMemo(40));
console.timeEnd("Mémoïsation O(n) - n=40"); // → ~0.5ms

console.time("Itératif O(n) - n=40");
console.log(fibonacciIteratif(40));
console.timeEnd("Itératif O(n) - n=40"); // → ~0.01ms

// La différence est de l'ordre de 100 000× !
```

**Conclusion :** L'optimisation algorithmique peut transformer un algorithme inutilisable en un algorithme ultra-rapide.

---

## 💪 Exercices Pratiques

### Exercice 1 : Analyse de Complexité

Pour chacune des fonctions suivantes, déterminez la complexité temporelle Big O.

```javascript
// Fonction A
function fonctionA(arr) {
  let somme = 0;
  for (let i = 0; i < arr.length; i++) {
    somme += arr[i];
  }
  return somme;
}

// Fonction B
function fonctionB(n) {
  let total = 0;
  for (let i = 1; i <= n; i = i * 2) {
    total += i;
  }
  return total;
}

// Fonction C
function fonctionC(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
  for (let j = 0; j < arr.length; j++) {
    console.log(arr[j]);
  }
}

// Fonction D
function fonctionD(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      for (let k = 0; k < arr.length; k++) {
        console.log(arr[i] + arr[j] + arr[k]);
      }
    }
  }
}

// Fonction E
function fonctionE(arr) {
  const premierElement = arr[0];
  const dernierElement = arr[arr.length - 1];
  return premierElement + dernierElement;
}

// Fonction F
function fonctionF(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i; j < arr.length; j++) {
      console.log(arr[i], arr[j]);
    }
  }
}
```

<details>
<summary>Voir les solutions</summary>

**Fonction A : O(n)**

- Une seule boucle qui parcourt n éléments
- Chaque opération dans la boucle est O(1)
- Complexité : O(n)

**Fonction B : O(log n)**

- La variable i est multipliée par 2 à chaque itération
- Nombre d'itérations : log₂(n)
- Complexité : O(log n)

**Fonction C : O(n)**

- Deux boucles **consécutives**, chacune en O(n)
- Total : O(n) + O(n) = O(2n)
- Simplification : O(n)

**Fonction D : O(n³)**

- Trois boucles **imbriquées**
- Chaque boucle parcourt n éléments
- Total : n × n × n = n³
- Complexité : O(n³)

**Fonction E : O(1)**

- Deux accès directs à des éléments du tableau
- Pas de boucle, nombre d'opérations constant
- Complexité : O(1)

**Fonction F : O(n²)**

- Deux boucles imbriquées
- La boucle interne part de i, mais fait en moyenne n/2 itérations
- Total : n × n/2 = n²/2
- Simplification : O(n²)

</details>

---

### Exercice 2 : Optimiser un Algorithme

Optimisez la fonction suivante qui calcule la somme des n premiers nombres pairs.

**Version Non Optimisée :**

```javascript
function sommePairs(n) {
  let somme = 0;
  let compteur = 0;
  let nombre = 0;

  while (compteur < n) {
    if (nombre % 2 === 0) {
      somme += nombre;
      compteur++;
    }
    nombre++;
  }

  return somme;
}

// Exemple : sommePairs(5) → 0 + 2 + 4 + 6 + 8 = 20
```

**Questions :**

1. Quelle est la complexité de cette version ?
2. Pouvez-vous l'optimiser pour obtenir O(1) ?

<details>
<summary>💡 Voir la solution</summary>

**1. Complexité de la version non optimisée : O(n)**

La boucle while fait environ 2n itérations (car on teste chaque nombre et garde seulement les pairs).

**2. Version optimisée O(1) :**

```javascript
function sommePairsOptimise(n) {
  // Formule mathématique : somme des n premiers pairs = n(n-1)
  // 0 + 2 + 4 + 6 + ... + 2(n-1) = 2(0 + 1 + 2 + ... + (n-1))
  // = 2 × (n-1)n/2 = n(n-1)

  return n * (n - 1);
}

// Exemple : sommePairsOptimise(5) → 5 × 4 = 20 ✓
```

**Explication :**

- Les n premiers nombres pairs sont : 0, 2, 4, 6, ..., 2(n-1)
- Leur somme = 2 × (0 + 1 + 2 + ... + (n-1))
- Formule de la somme : (n-1) × n / 2
- Résultat final : 2 × (n-1) × n / 2 = n(n-1)

**Test de performance :**

```javascript
console.time("Non optimisé O(n)");
sommePairs(1000000);
console.timeEnd("Non optimisé O(n)"); // → ~10-20ms

console.time("Optimisé O(1)");
sommePairsOptimise(1000000);
console.timeEnd("Optimisé O(1)"); // → ~0.001ms

// L'approche mathématique est environ 10 000× plus rapide !
```

**Leçon :** Parfois, une approche mathématique peut transformer O(n) en O(1).

</details>

---

### Exercice 3 : Choisir le Bon Algorithme

Vous devez implémenter une fonction qui vérifie si un tableau trié contient un élément donné.

**Question :** Entre la recherche linéaire O(n) et la recherche binaire O(log n), laquelle devez-vous choisir ? Implémentez les deux et comparez.

<details>
<summary>💡 Voir la solution</summary>

**Recherche Linéaire : O(n)**

```javascript
function rechercheLineaire(arr, cible) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === cible) {
      return i;
    }
  }
  return -1;
}
```

**Recherche Binaire : O(log n)**

```javascript
function rechercheBinaire(arr, cible) {
  let gauche = 0;
  let droite = arr.length - 1;

  while (gauche <= droite) {
    const milieu = Math.floor((gauche + droite) / 2);

    if (arr[milieu] === cible) {
      return milieu;
    }

    if (arr[milieu] < cible) {
      gauche = milieu + 1;
    } else {
      droite = milieu - 1;
    }
  }

  return -1;
}
```

**Comparaison de performance :**

```javascript
// Générer un tableau trié de 1 million d'éléments
const tableauTrie = [];
for (let i = 0; i < 1000000; i++) {
  tableauTrie.push(i);
}

// Chercher le dernier élément (pire cas)
const cible = 999999;

console.time("Recherche Linéaire O(n)");
rechercheLineaire(tableauTrie, cible);
console.timeEnd("Recherche Linéaire O(n)"); // → ~5-10ms

console.time("Recherche Binaire O(log n)");
rechercheBinaire(tableauTrie, cible);
console.timeEnd("Recherche Binaire O(log n)"); // → ~0.01ms

// La recherche binaire est environ 500-1000× plus rapide !
```

**Réponse :** Pour un tableau **trié**, utilisez toujours la **recherche binaire** car elle est exponentiellement plus rapide : O(log n) vs O(n).

**Important :** Si le tableau n'est PAS trié, vous devez utiliser la recherche linéaire OU trier d'abord (coût O(n log n)), puis utiliser la recherche binaire.

</details>

---

### Exercice 4 : Défi de Réflexion

Vous devez trouver tous les couples d'éléments dans un tableau dont la somme est égale à une cible.

**Exemple :**

```javascript
const arr = [2, 7, 11, 15, 3];
const cible = 9;
// Résultat : [[2, 7]] car 2 + 7 = 9
```

**Question :** Implémentez une solution O(n) en utilisant une structure de données appropriée.

<details>
<summary>💡 Voir la solution</summary>

**Solution Naïve : O(n²)**

```javascript
function trouverCouplesNaif(arr, cible) {
  const couples = [];

  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === cible) {
        couples.push([arr[i], arr[j]]);
      }
    }
  }

  return couples;
}

// Complexité : O(n²) - boucles imbriquées
```

**Solution Optimisée : O(n)**

```javascript
function trouverCouplesOptimise(arr, cible) {
  const couples = [];
  const vus = new Set();

  for (let i = 0; i < arr.length; i++) {
    const complement = cible - arr[i];

    // Vérifier si le complément a déjà été vu
    if (vus.has(complement)) {
      couples.push([complement, arr[i]]);
    }

    vus.add(arr[i]);
  }

  return couples;
}

// Complexité : O(n) - une seule boucle, Set.has() est O(1)
```

**Explication de l'algorithme O(n) :**

1. On parcourt le tableau une seule fois
2. Pour chaque élément, on cherche son "complément" : `cible - élément`
3. Si le complément est dans notre Set, on a trouvé un couple !
4. On ajoute l'élément courant au Set pour les recherches futures

**Exemple d'exécution :**

```javascript
arr = [2, 7, 11, 15, 3], cible = 9

Itération 1 : élément = 2, complément = 7
  vus = {} → 7 pas trouvé
  vus = {2}

Itération 2 : élément = 7, complément = 2
  vus = {2} → 2 trouvé ! ✓ Couple : [2, 7]
  vus = {2, 7}

Itération 3 : élément = 11, complément = -2
  vus = {2, 7} → -2 pas trouvé
  vus = {2, 7, 11}

Itération 4 : élément = 15, complément = -6
  vus = {2, 7, 11} → -6 pas trouvé
  vus = {2, 7, 11, 15}

Itération 5 : élément = 3, complément = 6
  vus = {2, 7, 11, 15} → 6 pas trouvé
  vus = {2, 7, 11, 15, 3}

Résultat : [[2, 7]]
```

**Test de performance :**

```javascript
const grandTableau = [];
for (let i = 0; i < 10000; i++) {
  grandTableau.push(Math.floor(Math.random() * 1000));
}

console.time("Naïf O(n²)");
trouverCouplesNaif(grandTableau, 500);
console.timeEnd("Naïf O(n²)"); // → ~300-500ms

console.time("Optimisé O(n)");
trouverCouplesOptimise(grandTableau, 500);
console.timeEnd("Optimisé O(n)"); // → ~1-2ms

// L'approche optimisée est environ 200-300× plus rapide !
```

**Leçon :** Utiliser un Set ou Map pour des recherches rapides peut transformer O(n²) en O(n).

</details>

---

## ✅ Quiz de Validation des Connaissances

Testez votre compréhension de la notation Big O avec ce quiz !

---

### Question 1

**Quelle est la définition de la notation Big O ?**

- [ ] A. Le temps exact qu'un algorithme prend pour s'exécuter
- [ ] B. Le nombre précis d'opérations effectuées par un algorithme
- [ ] C. Une description du comportement asymptotique de la complexité d'un algorithme
- [ ] D. La quantité de mémoire utilisée par un algorithme

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La notation Big O décrit le **comportement asymptotique**, c'est-à-dire comment la complexité croît lorsque la taille des données tend vers l'infini. Elle ne donne pas de temps exact ni de nombre précis d'opérations, mais plutôt un ordre de grandeur de la croissance.

</details>

---

### Question 2

**Quelle est la complexité temporelle de ce code ?**

```javascript
function mystere(arr) {
  let somme = 0;
  for (let i = 0; i < arr.length; i++) {
    somme += arr[i];
  }
  for (let j = 0; j < arr.length; j++) {
    somme += arr[j] * 2;
  }
  return somme;
}
```

- [ ] A. O(1)
- [ ] B. O(n)
- [ ] C. O(n²)
- [ ] D. O(2n)

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Bien qu'il y ait deux boucles, elles sont **consécutives** (l'une après l'autre), pas imbriquées.

- Première boucle : O(n)
- Deuxième boucle : O(n)
- Total : O(n) + O(n) = O(2n)
- Simplification : O(n) (on ignore le coefficient 2)

La réponse D serait techniquement correcte, mais en notation Big O, **on simplifie O(2n) en O(n)**.

</details>

---

### Question 3

**Dans l'échelle de complexité, quelle affirmation est VRAIE ?**

- [ ] A. O(n log n) est plus rapide que O(n²)
- [ ] B. O(n²) est plus rapide que O(n)
- [ ] C. O(2^n) est plus rapide que O(n!)
- [ ] D. O(1) est plus lent que O(log n)

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

Échelle de complexité (du plus rapide au plus lent) :
**O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2^n) < O(n!)**

Explication des autres options :

- B : FAUX - O(n) est plus rapide que O(n²)
- C : VRAI techniquement, mais A est également vrai et plus pertinent en pratique
- D : FAUX - O(1) est le plus rapide possible, plus rapide que O(log n)

</details>

---

### Question 4

**Quelle est la complexité de cette fonction récursive ?**

```javascript
function compter(n) {
  if (n <= 0) return;
  console.log(n);
  compter(n - 1);
}
```

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Cette fonction s'appelle récursivement **n fois** (décrémente de 1 à chaque appel jusqu'à atteindre 0).

Trace d'exécution pour compter(5) :

```
compter(5) → affiche 5
  compter(4) → affiche 4
    compter(3) → affiche 3
      compter(2) → affiche 2
        compter(1) → affiche 1
          compter(0) → retour
```

Total : **n appels** → O(n)

</details>

---

### Question 5

**Après simplification Big O, que devient O(5n² + 3n + 100) ?**

- [ ] A. O(n²)
- [ ] B. O(5n²)
- [ ] C. O(n)
- [ ] D. O(n² + n)

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

Règles de simplification appliquées :

1. **Ignorer les constantes** : O(5n² + 3n + 100) → O(n² + n)
2. **Garder le terme dominant** : O(n² + n) → O(n²)

Le terme n² domine le terme n, car pour de grandes valeurs de n :

- n = 1000 : n² = 1 000 000 vs n = 1 000 (n² est 1000× plus grand)
- Le terme constant 100 est complètement négligeable

Résultat final : **O(n²)**

</details>

---

### Question 6

**Quelle structure de données offre un accès en O(1) en moyenne ?**

- [ ] A. Tableau (Array) avec recherche linéaire
- [ ] B. Liste chaînée
- [ ] C. Table de hachage (Object/Map)
- [ ] D. Arbre binaire non équilibré

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Comparaison des structures :

- **C. Table de hachage (Object/Map)** : O(1) en moyenne pour accès, insertion, suppression par clé ✓
- A. Tableau avec recherche linéaire : O(n) pour rechercher un élément
- B. Liste chaînée : O(n) pour accéder à un élément (doit parcourir)
- D. Arbre binaire non équilibré : O(n) dans le pire cas (peut devenir une liste)

**Exemple concret :**

```javascript
const map = { alice: 25, bob: 30 };
const age = map["alice"]; // O(1) - accès direct par clé
```

</details>

---

### Question 7

**Quel algorithme a typiquement une complexité de O(n log n) ?**

- [ ] A. Recherche linéaire
- [ ] B. Tri à bulles (Bubble Sort)
- [ ] C. Tri fusion (Merge Sort)
- [ ] D. Accès à un élément de tableau par index

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Comparaison des complexités :

- A. Recherche linéaire : O(n)
- B. Tri à bulles : O(n²)
- **C. Tri fusion : O(n log n)** ✓
- D. Accès par index : O(1)

Le tri fusion divise le problème en deux à chaque niveau (**log n niveaux**), et à chaque niveau, traite tous les **n éléments**, d'où n × log n = O(n log n).

Autres algorithmes en O(n log n) : Tri rapide (en moyenne), Tri par tas.

</details>

---

## 📌 Récapitulatif de la Leçon

Félicitations ! Vous maîtrisez maintenant la notation Big O. Voici les points essentiels à retenir :

### Points Clés

1. **La notation Big O décrit la croissance asymptotique** d'un algorithme quand les données deviennent très grandes.

2. **Les complexités courantes**, de la plus efficace à la moins efficace :
   - O(1) - Constant : toujours excellent
   - O(log n) - Logarithmique : excellent
   - O(n) - Linéaire : bon, acceptable
   - O(n log n) - Linéarithmique : acceptable pour problèmes complexes
   - O(n²) - Quadratique : attention, peut devenir lent
   - O(2^n) - Exponentiel : éviter absolument
   - O(n!) - Factoriel : pratiquement inutilisable

3. **Les règles de simplification** :
   - Ignorer les constantes : O(5n) → O(n)
   - Garder le terme dominant : O(n² + n) → O(n²)
   - Analyser le pire cas par défaut

4. **Indicateurs pratiques** :
   - Une boucle simple : probablement O(n)
   - Boucles imbriquées : probablement O(n²) ou O(n³)
   - Division en deux répétée : probablement O(log n)
   - Accès direct : probablement O(1)
   - Récursion avec deux appels : attention à O(2^n)

5. **Choisir la bonne structure de données** peut transformer la complexité :
   - Array + recherche linéaire : O(n)
   - Set/Map + recherche : O(1)
   - Tableau trié + recherche binaire : O(log n)

6. **L'optimisation peut avoir un impact spectaculaire** :
   - Fibonacci naïf : O(2^n) → inutilisable
   - Fibonacci avec mémoïsation : O(n) → ultra rapide
   - Différence : jusqu'à 100 000× plus rapide !

7. **Attention aux méthodes cachées** : les méthodes intégrées comme `.sort()`, `.concat()`, `.includes()` ont leur propre complexité qu'il faut considérer.

8. **Big O n'est pas tout** : pour de petites données, un algorithme O(n²) simple peut être plus rapide qu'un O(n log n) complexe à cause des constantes. Mais pour de **grandes données**, Big O domine tout.

---

## 🎓 Conclusion

La notation Big O est le **langage universel** de l'analyse algorithmique. Maîtriser Big O vous permet de :

- **Comparer** des algorithmes objectivement
- **Prédire** les performances sur de grandes données
- **Optimiser** votre code de manière ciblée
- **Communiquer** efficacement sur la complexité

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Comprendre la notation Big O vous donne le super-pouvoir de prédire l'avenir : comment votre code se comportera-t-il non pas avec 10, mais avec 10 millions d'utilisateurs.

---

## ➡️ Prochaine Étape : Leçon 5

### Ce qui vous attend

Maintenant que vous parlez le langage de la complexité, la prochaine leçon, **« Analyse des Opérations JavaScript Simples avec Big O »**, vous apprendra à l'appliquer à du code concret.

**Vous découvrirez :**

- La complexité des opérations de base comme l'accès à un tableau (`arr[i]`).
- Pourquoi certaines méthodes de tableau (`shift`) sont plus lentes que d'autres (`push`).
- Comment évaluer rapidement la complexité d'un bloc de code en identifiant ses opérations clés.

### Préparez-vous !

Cette leçon vous donnera les réflexes pour analyser n'importe quel morceau de code JavaScript et estimer sa performance sans même avoir à l'exécuter.

---

## 🔗 Ressources Complémentaires

### Lectures Recommandées

- **Introduction to Algorithms** (CLRS) - Le livre de référence
- **Grokking Algorithms** - Approche visuelle et accessible
- **Big-O Cheat Sheet** - [bigocheatsheet.com](https://www.bigocheatsheet.com/)

### Outils de Visualisation

- **VisuAlgo** - [visualgo.net](https://visualgo.net) - Visualisations animées d'algorithmes
- **Algorithm Visualizer** - [algorithm-visualizer.org](https://algorithm-visualizer.org)

### Ressources JavaScript

- [MDN Web Docs - Performance](https://developer.mozilla.org/en-US/docs/Web/Performance)
- [JavaScript.info - Data Structures](https://javascript.info/data-types)

### Pratique Interactive

- **LeetCode** - Problèmes avec analyse de complexité
- **HackerRank** - Défis algorithmiques
- **Codewars** - Katas de programmation

---

## 💬 Vous Avez Aimé Cette Leçon ?

Votre feedback est précieux pour améliorer ce cours ! Partagez vos impressions :

- Cette leçon était-elle claire et utile ?
- Quels concepts aimeriez-vous approfondir ?
- Avez-vous trouvé des erreurs ou des imprécisions ?
- Suggestions pour améliorer les explications ou exemples ?

---

**Prêt pour la Leçon 5 ?** 🚀

Rendez-vous dans la prochaine leçon pour apprendre à analyser concrètement vos opérations JavaScript !

---

<div align="center">

**Leçon 4 sur 42 - Module 1 : Fondements des algorithmes et révision de JavaScript**

[⬅️ Leçon 3 : Complexité des Algorithmes](./lecon-3-complexite-algorithmes.md) | [Retour au sommaire](./README.md) | [Leçon 5 : Analyse des Opérations JavaScript ➡️](./lecon-5-analyse-operations-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
