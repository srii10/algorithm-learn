# 📖 Glossaire Complet - Algorithmes et Structures de Données

Ce glossaire regroupe tous les termes techniques, concepts algorithmiques et structures de données abordés dans la formation **« Algorithmes : des fondamentaux aux concepts avancés avec JavaScript »**. Les termes sont organisés par module pour faciliter la navigation et la révision.

---

## Table des Matières

- [Module 1 : Fondements des Algorithmes et JavaScript](#module-1--fondements-des-algorithmes-et-javascript)
- [Module 2 : Structures de Données Essentielles](#module-2--structures-de-données-essentielles)
- [Module 3 : Techniques de Tri Essentielles](#module-3--techniques-de-tri-essentielles)
- [Module 4 : Recherche et Récursion](#module-4--recherche-et-récursion)
- [Module 5 : Arbres et Parcours de Graphes](#module-5--arbres-et-parcours-de-graphes)
- [Module 6 : Paradigmes Avancés de Conception d'Algorithmes](#module-6--paradigmes-avancés-de-conception-dalgorithmes)
- [Module 7 : Révision et Pratique Avancée](#module-7--révision-et-pratique-avancée)
- [Termes Généraux](#-termes-généraux)
- [Tableaux Récapitulatifs](#-tableaux-récapitulatifs)

---

## Module 1 : Fondements des Algorithmes et JavaScript

### Algorithme

**Définition** : Séquence finie et ordonnée d'instructions claires et non ambiguës permettant de résoudre un problème ou d'accomplir une tâche spécifique.

**Caractéristiques** :

- **Finitude** : Se termine après un nombre fini d'étapes
- **Précision** : Chaque instruction est claire et sans ambiguïté
- **Entrée** : Zéro ou plusieurs données d'entrée
- **Sortie** : Au moins un résultat produit
- **Efficacité** : Utilise les ressources (temps, mémoire) de manière raisonnable

---

### Big O (Notation Big O)

**Définition** : Notation mathématique décrivant la **complexité asymptotique** d'un algorithme, c'est-à-dire comment le temps d'exécution ou l'espace mémoire croît en fonction de la taille de l'entrée (n).

**Complexités courantes** (du plus rapide au plus lent) :

- **O(1)** : Constant - Le temps d'exécution ne dépend pas de la taille de l'entrée
- **O(log n)** : Logarithmique - Double la taille de l'entrée = +1 opération (ex: recherche binaire)
- **O(n)** : Linéaire - Double la taille = double le temps (ex: parcours de tableau)
- **O(n log n)** : Quasi-linéaire - Complexité des meilleurs algorithmes de tri (merge sort, quick sort)
- **O(n²)** : Quadratique - Double la taille = 4× le temps (ex: tri à bulles)
- **O(2ⁿ)** : Exponentiel - Croissance très rapide, impraticable pour n > 30 (ex: Fibonacci naïf)
- **O(n!)** : Factorielle - Croissance encore plus rapide (ex: problème du voyageur de commerce brute force)

**Exemple** :

```javascript
// O(1) - Temps constant
function obtenirPremier(arr) {
  return arr[0];
}

// O(n) - Temps linéaire
function somme(arr) {
  let total = 0;
  for (let i = 0; i < arr.length; i++) {
    total += arr[i];
  }
  return total;
}

// O(n²) - Temps quadratique
function pairesDoublons(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      console.log(arr[i], arr[j]);
    }
  }
}
```

---

### Complexité Temporelle

**Définition** : Mesure du **nombre d'opérations** (ou du temps d'exécution) que nécessite un algorithme en fonction de la taille de l'entrée.

**Usage** : Permet de comparer l'efficacité de différents algorithmes et de prédire comment un algorithme évoluera avec des ensembles de données plus grands.

---

### Complexité Spatiale

**Définition** : Mesure de la **quantité de mémoire** utilisée par un algorithme en fonction de la taille de l'entrée, incluant les variables locales, les structures de données auxiliaires, et la pile d'appels (pour les algorithmes récursifs).

**Exemple** :

```javascript
// Complexité spatiale O(1) - Espace constant
function sommeTabulationOptimise(n) {
  let prev = 0,
    curr = 1;
  for (let i = 2; i <= n; i++) {
    let next = prev + curr;
    prev = curr;
    curr = next;
  }
  return curr;
}

// Complexité spatiale O(n) - Espace linéaire
function sommeTabulationTableau(n) {
  const dp = Array(n + 1).fill(0);
  dp[0] = 0;
  dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
```

---

### Efficacité Algorithmique

**Définition** : Mesure de la qualité d'un algorithme en termes de ressources consommées (temps d'exécution et mémoire). Un algorithme efficace minimise ces deux aspects tout en restant correct.

**Critères d'évaluation** :

- Vitesse d'exécution
- Utilisation de la mémoire
- Scalabilité (comportement avec de grandes données)
- Lisibilité et maintenabilité du code

---

### Scalabilité

**Définition** : Capacité d'un algorithme ou système à maintenir des performances acceptables lorsque la taille des données augmente significativement.

**Exemple** : Un algorithme O(n log n) est plus scalable qu'un algorithme O(n²) car il reste performant même avec de très grandes valeurs de n.

---

### Pire Cas, Meilleur Cas, Cas Moyen

**Définition** : Trois scénarios d'analyse de la complexité d'un algorithme :

- **Pire cas** : Situation où l'algorithme prend le plus de temps (généralement ce qu'on utilise pour Big O)
- **Meilleur cas** : Situation optimale où l'algorithme est le plus rapide
- **Cas moyen** : Performance attendue sur un échantillon représentatif de données

**Exemple avec la recherche linéaire** :

- **Meilleur cas** : O(1) - L'élément est en première position
- **Pire cas** : O(n) - L'élément est en dernière position ou absent
- **Cas moyen** : O(n/2) ≈ O(n) - L'élément est quelque part au milieu

---

### Pensée Algorithmique

**Définition** : Compétence cognitive permettant de décomposer un problème complexe en étapes logiques et séquentielles pour le résoudre de manière systématique.

**Étapes** :

1. **Comprendre** le problème
2. **Décomposer** en sous-problèmes plus simples
3. **Concevoir** une solution étape par étape
4. **Analyser** l'efficacité de la solution
5. **Optimiser** si nécessaire

---

## Module 2 : Structures de Données Essentielles

### Tableau (Array)

**Définition** : Structure de données **linéaire** qui stocke des éléments de manière **contiguë** en mémoire, accessibles par un **index numérique**.

**Caractéristiques en JavaScript** :

- Taille dynamique (peut grandir ou rétrécir)
- Peut contenir des types mixtes
- Indexation commence à 0

**Complexité des opérations** :

- **Accès par index** : O(1)
- **Recherche** : O(n)
- **Insertion en fin** : O(1) amortisé
- **Insertion au début/milieu** : O(n)
- **Suppression** : O(n)

---

### Liste Chaînée (Linked List)

**Définition** : Structure de données **linéaire** composée de **nœuds** où chaque nœud contient une valeur et une **référence** (pointeur) vers le nœud suivant.

**Types** :

- **Liste simplement chaînée** : Chaque nœud pointe uniquement vers le suivant
- **Liste doublement chaînée** : Chaque nœud pointe vers le suivant ET le précédent
- **Liste circulaire** : Le dernier nœud pointe vers le premier

**Complexité des opérations** :

- **Accès par index** : O(n)
- **Recherche** : O(n)
- **Insertion en tête** : O(1)
- **Insertion en fin** : O(n) pour simplement chaînée, O(1) avec pointeur tail
- **Suppression en tête** : O(1)

**Exemple de structure de nœud** :

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null; // Référence vers le nœud suivant
  }
}
```

**Avantages** :

- Insertion/suppression en tête très rapide O(1)
- Pas de redimensionnement comme les tableaux
- Taille dynamique sans limite

**Inconvénients** :

- Accès par index lent O(n)
- Utilise plus de mémoire (stockage des références)
- Mauvaise localité mémoire (cache CPU moins efficace)

---

### Pile (Stack)

**Définition** : Structure de données **LIFO** (Last In, First Out) où le dernier élément ajouté est le premier à être retiré. Comme une pile d'assiettes.

**Opérations principales** :

- **push(element)** : Ajouter un élément au sommet - O(1)
- **pop()** : Retirer l'élément au sommet - O(1)
- **peek()** / **top()** : Consulter l'élément au sommet sans le retirer - O(1)
- **isEmpty()** : Vérifier si la pile est vide - O(1)

**Cas d'usage** :

- Historique de navigation (bouton "Retour")
- Annuler/Refaire (Undo/Redo)
- Pile d'appels de fonctions (call stack)
- Évaluation d'expressions mathématiques
- Parcours en profondeur (DFS)

**Implémentation** :

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

---

### File (Queue)

**Définition** : Structure de données **FIFO** (First In, First Out) où le premier élément ajouté est le premier à être retiré. Comme une file d'attente au supermarché.

**Opérations principales** :

- **enqueue(element)** : Ajouter un élément à la fin - O(1)
- **dequeue()** : Retirer l'élément au début - O(1)
- **front()** / **peek()** : Consulter l'élément au début sans le retirer - O(1)
- **isEmpty()** : Vérifier si la file est vide - O(1)

**Cas d'usage** :

- File d'attente d'impressions
- Gestion de requêtes serveur
- Parcours en largeur (BFS)
- Tampons de données (buffers)
- Systèmes de messagerie (queues)

**Implémentation** :

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    return this.items.shift();
  }

  front() {
    return this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

---

### LIFO (Last In, First Out)

**Définition** : Principe de gestion où le dernier élément ajouté est le premier à être retiré. Caractéristique fondamentale des **piles**.

---

### FIFO (First In, First Out)

**Définition** : Principe de gestion où le premier élément ajouté est le premier à être retiré. Caractéristique fondamentale des **files**.

---

### Nœud (Node)

**Définition** : Élément de base d'une structure de données chaînée (liste chaînée, arbre, graphe) contenant :

- Une **valeur** (données stockées)
- Une ou plusieurs **références** vers d'autres nœuds

**Exemple** :

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null; // Pour liste chaînée simple
    // this.prev = null; // Pour liste doublement chaînée
  }
}
```

---

### Référence / Pointeur

**Définition** : Variable qui contient l'**adresse mémoire** d'un autre objet plutôt que la valeur elle-même. En JavaScript, les objets sont manipulés par référence.

**Exemple** :

```javascript
let noeud1 = { value: 10, next: null };
let noeud2 = { value: 20, next: null };
noeud1.next = noeud2; // noeud1.next pointe vers noeud2
```

---

## Module 3 : Techniques de Tri Essentielles

### Tri (Sorting)

**Définition** : Processus de **réorganisation** d'une collection d'éléments dans un ordre spécifique (croissant ou décroissant) selon un critère de comparaison.

**Importance** :

- Facilite la recherche (recherche binaire nécessite un tableau trié)
- Améliore la lisibilité des données
- Optimise certains algorithmes

---

### Tri à Bulles (Bubble Sort)

**Définition** : Algorithme de tri simple qui **compare** des paires d'éléments adjacents et les **échange** si nécessaire, répétant ce processus jusqu'à ce que le tableau soit trié.

**Complexité** :

- **Temps** : O(n²) dans le pire et le cas moyen, O(n) dans le meilleur cas (déjà trié avec optimisation)
- **Espace** : O(1) - Tri en place

**Principe** : Les éléments "remontent" comme des bulles vers leur position finale.

**Implémentation** :

```javascript
function triBulles(arr) {
  const n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    let echange = false;
    for (let j = 0; j < n - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]; // Échange
        echange = true;
      }
    }
    if (!echange) break; // Optimisation
  }
  return arr;
}
```

**Usage** : Pédagogique uniquement, inefficace en pratique.

---

### Tri par Sélection (Selection Sort)

**Définition** : Algorithme de tri qui **sélectionne** le plus petit élément non trié et le **place** à sa position finale, répétant ce processus pour tous les éléments.

**Complexité** :

- **Temps** : O(n²) dans tous les cas
- **Espace** : O(1) - Tri en place

**Principe** : Divise le tableau en deux parties (triée et non triée), et déplace progressivement les éléments de la partie non triée vers la partie triée.

**Implémentation** :

```javascript
function triSelection(arr) {
  const n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    let indexMin = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[indexMin]) {
        indexMin = j;
      }
    }
    if (indexMin !== i) {
      [arr[i], arr[indexMin]] = [arr[indexMin], arr[i]];
    }
  }
  return arr;
}
```

**Avantage** : Nombre minimal d'échanges (au plus n-1).

---

### Tri par Insertion (Insertion Sort)

**Définition** : Algorithme de tri qui **insère** chaque élément à sa position correcte dans une partie déjà triée du tableau, comme on trie des cartes à jouer.

**Complexité** :

- **Temps** : O(n²) dans le pire cas, O(n) dans le meilleur cas (déjà trié)
- **Espace** : O(1) - Tri en place

**Principe** : Construit progressivement une partie triée en insérant chaque nouvel élément à sa place.

**Implémentation** :

```javascript
function triInsertion(arr) {
  for (let i = 1; i < arr.length; i++) {
    let cle = arr[i];
    let j = i - 1;
    while (j >= 0 && arr[j] > cle) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = cle;
  }
  return arr;
}
```

**Avantages** :

- Efficace pour petits tableaux
- Efficace pour tableaux presque triés
- Stable (préserve l'ordre des éléments égaux)
- Tri en ligne (peut trier les données au fur et à mesure de leur arrivée)

---

### Tri Fusion (Merge Sort)

**Définition** : Algorithme de tri basé sur le paradigme **Diviser pour Régner** qui **divise** récursivement le tableau en deux moitiés, les trie séparément, puis **fusionne** les résultats.

**Complexité** :

- **Temps** : O(n log n) dans tous les cas
- **Espace** : O(n) - Nécessite des tableaux auxiliaires

**Principe** :

1. **Diviser** : Séparer le tableau en deux moitiés
2. **Régner** : Trier récursivement chaque moitié
3. **Combiner** : Fusionner les deux moitiés triées

**Implémentation** :

```javascript
function triFusion(arr) {
  if (arr.length <= 1) return arr;

  const milieu = Math.floor(arr.length / 2);
  const gauche = triFusion(arr.slice(0, milieu));
  const droite = triFusion(arr.slice(milieu));

  return fusionner(gauche, droite);
}

function fusionner(gauche, droite) {
  const resultat = [];
  let i = 0,
    j = 0;

  while (i < gauche.length && j < droite.length) {
    if (gauche[i] <= droite[j]) {
      resultat.push(gauche[i++]);
    } else {
      resultat.push(droite[j++]);
    }
  }

  return resultat.concat(gauche.slice(i)).concat(droite.slice(j));
}
```

**Avantages** :

- Garantie O(n log n) dans tous les cas
- Stable
- Bon pour trier de grandes données
- Parallélisable

**Inconvénient** : Utilise O(n) espace supplémentaire

---

### Tri Rapide (Quick Sort)

**Définition** : Algorithme de tri basé sur **Diviser pour Régner** qui sélectionne un **pivot**, partitionne le tableau en éléments < pivot et > pivot, puis trie récursivement chaque partition.

**Complexité** :

- **Temps** : O(n log n) en moyenne, O(n²) dans le pire cas (pivot mal choisi)
- **Espace** : O(log n) pour la pile d'appels récursifs

**Principe** :

1. **Choisir** un pivot (premier, dernier, aléatoire, médian)
2. **Partitionner** : Placer tous les éléments < pivot à gauche, > pivot à droite
3. **Récursion** : Trier récursivement gauche et droite

**Implémentation** :

```javascript
function triRapide(arr, debut = 0, fin = arr.length - 1) {
  if (debut < fin) {
    const indexPivot = partitionner(arr, debut, fin);
    triRapide(arr, debut, indexPivot - 1);
    triRapide(arr, indexPivot + 1, fin);
  }
  return arr;
}

function partitionner(arr, debut, fin) {
  const pivot = arr[fin];
  let i = debut - 1;

  for (let j = debut; j < fin; j++) {
    if (arr[j] < pivot) {
      i++;
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
  }

  [arr[i + 1], arr[fin]] = [arr[fin], arr[i + 1]];
  return i + 1;
}
```

**Avantages** :

- Très rapide en pratique (meilleur tri général)
- Tri en place (O(1) espace hors pile récursive)
- Cache-friendly (bonne localité mémoire)

**Inconvénients** :

- Pire cas O(n²) (peut être évité avec bon choix de pivot)
- Non stable

---

### Diviser pour Régner (Divide and Conquer)

**Définition** : Paradigme de conception d'algorithmes qui consiste à :

1. **Diviser** le problème en sous-problèmes plus petits
2. **Régner** en résolvant récursivement chaque sous-problème
3. **Combiner** les solutions pour obtenir la solution globale

**Exemples** : Tri fusion, tri rapide, recherche binaire, multiplication de matrices

---

### Pivot

**Définition** : Dans le tri rapide, élément choisi pour **partitionner** le tableau. Tous les éléments < pivot vont à gauche, tous les éléments > pivot vont à droite.

**Stratégies de choix** :

- Premier élément (simple mais peut donner O(n²))
- Dernier élément (standard)
- Élément du milieu
- Aléatoire (évite le pire cas)
- Médiane de trois (premier, milieu, dernier)

---

### Partitionnement (Partitioning)

**Définition** : Processus de réorganisation d'un tableau autour d'un pivot de sorte que tous les éléments inférieurs au pivot soient à gauche et tous les éléments supérieurs soient à droite.

**Utilisé dans** : Tri rapide, sélection du k-ième élément

---

### Tri Stable

**Définition** : Un algorithme de tri est dit **stable** s'il préserve l'ordre relatif des éléments égaux.

**Exemple** :

```javascript
// Données : [{nom: "Chermann", âge: 25}, {nom: "Prudence", âge: 25}]
// Tri stable par âge → L'ordre Chermann-Prudence est préservé
```

**Tris stables** : Tri fusion, tri par insertion, tri à bulles
**Tris non stables** : Tri rapide, tri par sélection, tri par tas

---

### Tri en Place (In-Place Sorting)

**Définition** : Algorithme de tri qui ne nécessite qu'une quantité **constante** O(1) de mémoire supplémentaire (hors structure de données d'entrée).

**Tris en place** : Tri rapide, tri par sélection, tri à bulles, tri par insertion
**Tris non en place** : Tri fusion (O(n) espace)

---

## Module 4 : Recherche et Récursion

### Recherche Linéaire (Linear Search)

**Définition** : Algorithme de recherche qui **parcourt** séquentiellement tous les éléments d'une collection jusqu'à trouver l'élément recherché.

**Complexité** :

- **Temps** : O(n) dans le pire cas
- **Espace** : O(1)

**Implémentation** :

```javascript
function rechercheLineaire(arr, cible) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === cible) {
      return i; // Index de l'élément trouvé
    }
  }
  return -1; // Élément non trouvé
}
```

**Avantages** :

- Fonctionne sur tableaux non triés
- Simple à implémenter

**Inconvénient** : Lent pour grandes collections

---

### Recherche Binaire (Binary Search)

**Définition** : Algorithme de recherche efficace qui fonctionne sur un **tableau trié** en divisant répétitivement l'espace de recherche par deux.

**Prérequis** : Le tableau DOIT être trié.

**Complexité** :

- **Temps** : O(log n)
- **Espace** : O(1) pour la version itérative, O(log n) pour la version récursive

**Principe** :

1. Comparer l'élément du milieu avec la cible
2. Si égal → trouvé
3. Si cible < milieu → chercher dans la moitié gauche
4. Si cible > milieu → chercher dans la moitié droite
5. Répéter jusqu'à trouver ou épuiser l'espace

**Implémentation itérative** :

```javascript
function rechercheBinaire(arr, cible) {
  let debut = 0;
  let fin = arr.length - 1;

  while (debut <= fin) {
    const milieu = Math.floor((debut + fin) / 2);

    if (arr[milieu] === cible) {
      return milieu;
    } else if (arr[milieu] < cible) {
      debut = milieu + 1;
    } else {
      fin = milieu - 1;
    }
  }

  return -1;
}
```

**Implémentation récursive** :

```javascript
function rechercheBinaireRecursive(
  arr,
  cible,
  debut = 0,
  fin = arr.length - 1,
) {
  if (debut > fin) return -1;

  const milieu = Math.floor((debut + fin) / 2);

  if (arr[milieu] === cible) return milieu;
  if (arr[milieu] < cible)
    return rechercheBinaireRecursive(arr, cible, milieu + 1, fin);
  return rechercheBinaireRecursive(arr, cible, debut, milieu - 1);
}
```

**Exemple de croissance** :

- 1 000 éléments → ~10 comparaisons maximum
- 1 000 000 éléments → ~20 comparaisons maximum
- 1 000 000 000 éléments → ~30 comparaisons maximum

---

### Récursion

**Définition** : Technique de programmation où une fonction **s'appelle elle-même** pour résoudre un problème en le décomposant en sous-problèmes plus petits et similaires.

**Composants essentiels** :

1. **Cas de base** : Condition d'arrêt qui termine la récursion
2. **Cas récursif** : Appel de la fonction sur un sous-problème plus petit

**Exemple - Factorielle** :

```javascript
function factorielle(n) {
  // Cas de base
  if (n === 0 || n === 1) return 1;

  // Cas récursif
  return n * factorielle(n - 1);
}
```

**Avantages** :

- Code plus élégant et lisible pour certains problèmes
- Naturelle pour structures récursives (arbres, graphes)
- Simplifie diviser-pour-régner

**Inconvénients** :

- Risque de stack overflow pour récursions profondes
- Peut être moins performante que les solutions itératives
- Consomme plus de mémoire (pile d'appels)

---

### Cas de Base (Base Case)

**Définition** : Condition qui **arrête** la récursion en retournant une valeur directe sans effectuer d'appel récursif supplémentaire.

**Importance** : Sans cas de base, la récursion s'exécuterait indéfiniment (récursion infinie → stack overflow).

**Exemple** :

```javascript
function fibonacci(n) {
  if (n <= 1) return n; // Cas de base
  return fibonacci(n - 1) + fibonacci(n - 2); // Cas récursif
}
```

---

### Pile d'Appels (Call Stack)

**Définition** : Structure de données de type **pile** utilisée par le runtime JavaScript pour gérer les appels de fonctions. Chaque appel de fonction ajoute un **cadre d'exécution** (stack frame) sur la pile.

**Fonctionnement** :

1. Appel de fonction → nouveau cadre ajouté sur la pile
2. Retour de fonction → cadre retiré de la pile
3. La pile suit l'ordre LIFO

**Limite** : Chaque navigateur/environnement a une limite de taille de pile (~10 000 à 100 000 appels). Dépasser cette limite cause un **stack overflow**.

**Exemple de dépassement** :

```javascript
function recurInfinie(n) {
  return recurInfinie(n + 1); // Pas de cas de base → stack overflow
}
```

---

### Stack Overflow

**Définition** : Erreur qui se produit lorsque la **pile d'appels** dépasse sa taille maximale, généralement causée par une récursion trop profonde ou infinie.

**Erreur JavaScript** : `RangeError: Maximum call stack size exceeded`

**Solutions** :

- Ajouter un cas de base
- Limiter la profondeur de récursion
- Utiliser une approche itérative
- Utiliser la mémoïsation pour éviter les appels redondants

---

### Récursion Terminale (Tail Recursion)

**Définition** : Forme optimisée de récursion où l'appel récursif est la **dernière opération** de la fonction (aucune opération après le retour de l'appel récursif).

**Exemple - Non terminale** :

```javascript
function factorielle(n) {
  if (n === 1) return 1;
  return n * factorielle(n - 1); // Multiplication APRÈS l'appel récursif
}
```

**Exemple - Terminale** :

```javascript
function factorielleTerminale(n, accumulateur = 1) {
  if (n === 1) return accumulateur;
  return factorielleTerminale(n - 1, n * accumulateur); // Appel récursif = dernière opération
}
```

**Avantage** : Certains compilateurs/interpréteurs peuvent optimiser la récursion terminale (Tail Call Optimization) pour éviter d'augmenter la pile d'appels.

**Note** : JavaScript moderne (ES6) spécifie l'optimisation des appels terminaux, mais peu de moteurs l'implémentent actuellement.

---

## Module 5 : Arbres et Parcours de Graphes

### Arbre (Tree)

**Définition** : Structure de données **hiérarchique** et **non linéaire** composée de nœuds connectés par des arêtes, avec un nœud **racine** unique et sans cycles.

**Caractéristiques** :

- Un nœud racine (root)
- Chaque nœud a zéro ou plusieurs enfants
- Chaque nœud (sauf la racine) a exactement un parent
- Aucun cycle (pas de boucle)

**Terminologie** :

- **Racine** : Nœud au sommet de l'arbre
- **Feuille** : Nœud sans enfants
- **Nœud interne** : Nœud avec au moins un enfant
- **Parent** : Nœud directement au-dessus
- **Enfant** : Nœud directement en-dessous
- **Frères/Siblings** : Nœuds partageant le même parent
- **Ancêtre** : Parent, grand-parent, etc.
- **Descendant** : Enfant, petit-enfant, etc.

---

### Arbre Binaire (Binary Tree)

**Définition** : Arbre où chaque nœud a **au maximum 2 enfants** (gauche et droite).

**Structure de nœud** :

```javascript
class NodeBinaire {
  constructor(value) {
    this.value = value;
    this.left = null; // Enfant gauche
    this.right = null; // Enfant droit
  }
}
```

**Types d'arbres binaires** :

- **Arbre binaire complet** : Tous les niveaux sont remplis sauf peut-être le dernier (rempli de gauche à droite)
- **Arbre binaire parfait** : Tous les niveaux sont complètement remplis
- **Arbre binaire dégénéré** : Chaque parent a un seul enfant (ressemble à une liste chaînée)

---

### Arbre Binaire de Recherche (Binary Search Tree - BST)

**Définition** : Arbre binaire avec la propriété suivante : pour chaque nœud, tous les éléments du **sous-arbre gauche** sont inférieurs à la valeur du nœud, et tous les éléments du **sous-arbre droit** sont supérieurs.

**Propriété BST** :

```
     10
    /  \
   5    15
  / \   / \
 3   7 12  20

Gauche < Nœud < Droite
```

**Complexité des opérations** (arbre équilibré) :

- **Recherche** : O(log n)
- **Insertion** : O(log n)
- **Suppression** : O(log n)

**Complexité pire cas** (arbre dégénéré) :

- Toutes les opérations : O(n)

**Implémentation - Insertion** :

```javascript
class BST {
  constructor() {
    this.root = null;
  }

  insert(value) {
    const newNode = new Node(value);

    if (!this.root) {
      this.root = newNode;
      return this;
    }

    let current = this.root;
    while (true) {
      if (value < current.value) {
        if (!current.left) {
          current.left = newNode;
          return this;
        }
        current = current.left;
      } else {
        if (!current.right) {
          current.right = newNode;
          return this;
        }
        current = current.right;
      }
    }
  }

  search(value) {
    let current = this.root;

    while (current) {
      if (value === current.value) return true;
      if (value < current.value) current = current.left;
      else current = current.right;
    }

    return false;
  }
}
```

---

### Profondeur (Depth)

**Définition** : Nombre d'arêtes depuis la **racine** jusqu'à un nœud donné.

**Exemple** :

```
     10        ← Profondeur 0 (racine)
    /  \
   5    15     ← Profondeur 1
  / \
 3   7         ← Profondeur 2
```

---

### Hauteur (Height)

**Définition** : Nombre d'arêtes sur le **plus long chemin** depuis un nœud jusqu'à une feuille.

**Hauteur de l'arbre** : Hauteur de la racine.

**Exemple** :

```
     10        ← Hauteur 2
    /  \
   5    15     ← Hauteur 1 (pour 5), Hauteur 0 (pour 15)
  / \
 3   7         ← Hauteur 0 (feuilles)
```

---

### Niveau (Level)

**Définition** : Ensemble des nœuds à la même profondeur. Le niveau de la racine est 0.

---

### Graphe (Graph)

**Définition** : Structure de données composée de **sommets** (vertices/nodes) connectés par des **arêtes** (edges). Plus général qu'un arbre (peut contenir des cycles).

**Types** :

- **Graphe orienté** : Les arêtes ont une direction (A → B ≠ B → A)
- **Graphe non orienté** : Les arêtes sont bidirectionnelles (A — B = B — A)
- **Graphe pondéré** : Les arêtes ont des poids/coûts
- **Graphe non pondéré** : Toutes les arêtes ont le même poids

**Applications** :

- Réseaux sociaux (amis, followers)
- Réseaux routiers (villes = sommets, routes = arêtes)
- Web (pages = sommets, liens = arêtes)
- Dépendances de packages

---

### Sommet / Nœud (Vertex / Node)

**Définition** : Entité individuelle dans un graphe, représentant un point ou un objet.

---

### Arête (Edge)

**Définition** : Connexion entre deux sommets dans un graphe.

**Types** :

- **Arête orientée** : A → B (direction définie)
- **Arête non orientée** : A — B (bidirectionnelle)
- **Arête pondérée** : Possède un poids/coût

---

### Liste d'Adjacence (Adjacency List)

**Définition** : Représentation d'un graphe où chaque sommet stocke une **liste** de ses voisins (sommets adjacents).

**Implémentation** :

```javascript
class Graphe {
  constructor() {
    this.listeAdjacence = {};
  }

  ajouterSommet(sommet) {
    if (!this.listeAdjacence[sommet]) {
      this.listeAdjacence[sommet] = [];
    }
  }

  ajouterArete(sommet1, sommet2) {
    this.listeAdjacence[sommet1].push(sommet2);
    this.listeAdjacence[sommet2].push(sommet1); // Pour graphe non orienté
  }
}

// Exemple :
// {
//   "A": ["B", "C"],
//   "B": ["A", "D"],
//   "C": ["A", "D"],
//   "D": ["B", "C"]
// }
```

**Avantages** :

- Espace efficace : O(V + E) où V = sommets, E = arêtes
- Rapide pour parcourir les voisins
- Bon pour graphes peu denses

---

### Matrice d'Adjacence (Adjacency Matrix)

**Définition** : Représentation d'un graphe par une **matrice 2D** où `matrice[i][j] = 1` si une arête existe entre le sommet i et le sommet j, sinon `0`.

**Implémentation** :

```javascript
class GrapheMatrice {
  constructor(nombreSommets) {
    this.matrice = Array(nombreSommets)
      .fill(0)
      .map(() => Array(nombreSommets).fill(0));
  }

  ajouterArete(i, j) {
    this.matrice[i][j] = 1;
    this.matrice[j][i] = 1; // Pour graphe non orienté
  }
}

// Exemple pour graphe A-B-C-D :
// [
//   [0, 1, 1, 0],  // A connecté à B et C
//   [1, 0, 0, 1],  // B connecté à A et D
//   [1, 0, 0, 1],  // C connecté à A et D
//   [0, 1, 1, 0]   // D connecté à B et C
// ]
```

**Avantages** :

- Vérification rapide si arête existe : O(1)
- Simple pour graphes denses

**Inconvénients** :

- Espace : O(V²) même si peu d'arêtes
- Inefficace pour graphes peu denses

---

### BFS - Parcours en Largeur (Breadth-First Search)

**Définition** : Algorithme de parcours de graphe qui explore les sommets **niveau par niveau**, en visitant tous les voisins d'un sommet avant de passer au niveau suivant.

**Principe** : Utilise une **file (Queue)** pour gérer l'ordre de visite.

**Complexité** :

- **Temps** : O(V + E) où V = sommets, E = arêtes
- **Espace** : O(V) pour la file et l'ensemble des visités

**Implémentation** :

```javascript
function BFS(graphe, depart) {
  const visites = new Set();
  const file = [depart];
  const resultat = [];

  visites.add(depart);

  while (file.length > 0) {
    const sommet = file.shift();
    resultat.push(sommet);

    for (const voisin of graphe.listeAdjacence[sommet]) {
      if (!visites.has(voisin)) {
        visites.add(voisin);
        file.push(voisin);
      }
    }
  }

  return resultat;
}
```

**Ordre de visite** :

```
     A
    / \
   B   C
  / \   \
 D   E   F

BFS depuis A : A → B → C → D → E → F
```

**Cas d'usage** :

- Trouver le **plus court chemin** (en nombre d'arêtes)
- Parcours niveau par niveau
- Réseau social (amis à distance k)
- Résolution de labyrinthes

---

### DFS - Parcours en Profondeur (Depth-First Search)

**Définition** : Algorithme de parcours de graphe qui explore en **profondeur** en suivant une branche jusqu'au bout avant de revenir en arrière (backtracking).

**Principe** : Utilise une **pile (Stack)** ou la **récursion** pour gérer l'ordre de visite.

**Complexité** :

- **Temps** : O(V + E)
- **Espace** : O(V) pour la pile/récursion et l'ensemble des visités

**Implémentation récursive** :

```javascript
function DFS(graphe, depart, visites = new Set(), resultat = []) {
  visites.add(depart);
  resultat.push(depart);

  for (const voisin of graphe.listeAdjacence[depart]) {
    if (!visites.has(voisin)) {
      DFS(graphe, voisin, visites, resultat);
    }
  }

  return resultat;
}
```

**Implémentation itérative** :

```javascript
function DFSIterative(graphe, depart) {
  const visites = new Set();
  const pile = [depart];
  const resultat = [];

  while (pile.length > 0) {
    const sommet = pile.pop();

    if (!visites.has(sommet)) {
      visites.add(sommet);
      resultat.push(sommet);

      for (const voisin of graphe.listeAdjacence[sommet]) {
        if (!visites.has(voisin)) {
          pile.push(voisin);
        }
      }
    }
  }

  return resultat;
}
```

**Ordre de visite** :

```
     A
    / \
   B   C
  / \   \
 D   E   F

DFS depuis A : A → B → D → E → C → F (récursif)
```

**Cas d'usage** :

- Détection de cycles
- Tri topologique
- Résolution de labyrinthes
- Parcours d'arbres (pré-ordre, en-ordre, post-ordre)
- Résolution de puzzles (Sudoku, échecs)

---

### Parcours Pré-ordre (Pre-order)

**Définition** : Parcours d'arbre qui visite les nœuds dans l'ordre : **Racine → Gauche → Droite**

**Implémentation** :

```javascript
function parcoursPreOrdre(node) {
  if (!node) return;
  console.log(node.value); // Visiter racine
  parcoursPreOrdre(node.left); // Parcourir gauche
  parcoursPreOrdre(node.right); // Parcourir droite
}
```

**Usage** : Créer une copie de l'arbre, évaluation d'expressions préfixées

---

### Parcours En-ordre (In-order)

**Définition** : Parcours d'arbre qui visite les nœuds dans l'ordre : **Gauche → Racine → Droite**

**Implémentation** :

```javascript
function parcoursEnOrdre(node) {
  if (!node) return;
  parcoursEnOrdre(node.left); // Parcourir gauche
  console.log(node.value); // Visiter racine
  parcoursEnOrdre(node.right); // Parcourir droite
}
```

**Usage** : Obtenir les valeurs d'un BST dans l'ordre trié

---

### Parcours Post-ordre (Post-order)

**Définition** : Parcours d'arbre qui visite les nœuds dans l'ordre : **Gauche → Droite → Racine**

**Implémentation** :

```javascript
function parcoursPostOrdre(node) {
  if (!node) return;
  parcoursPostOrdre(node.left); // Parcourir gauche
  parcoursPostOrdre(node.right); // Parcourir droite
  console.log(node.value); // Visiter racine
}
```

**Usage** : Supprimer un arbre, évaluation d'expressions postfixées

---

## Module 6 : Paradigmes Avancés de Conception d'Algorithmes

### Algorithme Glouton (Greedy Algorithm)

**Définition** : Paradigme de conception d'algorithmes qui fait le **meilleur choix localement optimal** à chaque étape, en espérant que cela mène à une **solution globalement optimale**.

**Propriétés nécessaires** :

1. **Propriété de choix glouton** : Un choix localement optimal mène à une solution globalement optimale
2. **Sous-structure optimale** : La solution optimale contient des solutions optimales de sous-problèmes

**Complexité** : Généralement O(n log n) à cause du tri initial

**Exemples classiques** :

- Problème de la monnaie (certains systèmes monétaires)
- Sélection d'activités
- Sac à dos fractionnaire
- Arbre couvrant minimal (Kruskal, Prim)
- Plus court chemin (Dijkstra)

**Implémentation - Rendu de monnaie** :

```javascript
function renduMonnaieGlouton(montant, pieces) {
  pieces.sort((a, b) => b - a); // Trier par ordre décroissant
  const resultat = [];

  for (const piece of pieces) {
    while (montant >= piece) {
      resultat.push(piece);
      montant -= piece;
    }
  }

  return resultat;
}

// Exemple : renduMonnaieGlouton(63, [25, 10, 5, 1])
// Résultat : [25, 25, 10, 1, 1, 1] (6 pièces)
```

**Avantages** :

- Simple à concevoir et implémenter
- Généralement rapide (O(n log n))
- Efficace pour certains problèmes

**Limitations** :

- Ne garantit PAS toujours la solution optimale
- Nécessite de prouver que le choix glouton fonctionne
- Ne fonctionne pas pour tous les problèmes (ex: sac à dos 0/1)

---

### Programmation Dynamique (Dynamic Programming - DP)

**Définition** : Paradigme de conception d'algorithmes qui résout des problèmes en les décomposant en **sous-problèmes chevauchants** et en **stockant les résultats** pour éviter les calculs redondants.

**Propriétés nécessaires** :

1. **Sous-problèmes chevauchants** : Le problème peut être décomposé en sous-problèmes réutilisés plusieurs fois
2. **Sous-structure optimale** : La solution optimale contient des solutions optimales de sous-problèmes

**Deux approches** :

- **Mémoïsation (Top-down)** : Récursif + cache
- **Tabulation (Bottom-up)** : Itératif + table DP

**Complexité** : Généralement O(n × k) où k dépend du problème

**Exemples classiques** :

- Fibonacci
- Sac à dos 0/1
- Plus longue sous-séquence commune (LCS)
- Rendu de monnaie (version optimale)
- Voyageur sur grille
- Coupe de bâton (rod cutting)

---

### Sous-problèmes Chevauchants (Overlapping Subproblems)

**Définition** : Propriété où un problème peut être décomposé en sous-problèmes qui sont **résolus plusieurs fois**. C'est l'opportunité d'optimiser avec la mémoïsation ou la tabulation.

**Exemple - Fibonacci** :

```
fib(5) appelle fib(4) et fib(3)
fib(4) appelle fib(3) et fib(2)
→ fib(3) est calculé 2 fois
→ fib(2) est calculé 3 fois
→ fib(1) est calculé 5 fois

Avec mémoïsation : chaque fib(n) n'est calculé qu'une seule fois
```

---

### Sous-structure Optimale (Optimal Substructure)

**Définition** : Propriété où la **solution optimale** d'un problème peut être construite à partir des **solutions optimales** de ses sous-problèmes.

**Exemple - Plus court chemin** :

```
Le plus court chemin de A à C passant par B =
  Plus court chemin de A à B + Plus court chemin de B à C
```

**Contre-exemple - Plus long chemin simple** :
Le plus long chemin simple ne possède PAS cette propriété car ajouter un sous-chemin optimal peut créer un cycle.

---

### Mémoïsation (Memoization)

**Définition** : Technique d'optimisation **top-down** (descendante) qui consiste à **cacher les résultats** des appels de fonction pour éviter de recalculer les mêmes sous-problèmes.

**Principe** : Récursion + Cache (Map/Object)

**Implémentation - Fibonacci** :

```javascript
function fibonacciMemo(n, memo = {}) {
  // Cas de base
  if (n <= 1) return n;

  // Vérifier le cache
  if (memo[n] !== undefined) return memo[n];

  // Calculer et stocker dans le cache
  memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);

  return memo[n];
}

// Complexité : O(2^n) → O(n)
```

**Avantages** :

- Approche naturelle (récursive)
- Ne calcule que les sous-problèmes nécessaires
- Facile à implémenter à partir d'une solution récursive naïve

**Inconvénients** :

- Utilise la pile d'appels (risque de stack overflow)
- Peut consommer plus de mémoire si tous les sous-problèmes sont explorés

---

### Tabulation

**Définition** : Technique de programmation dynamique **bottom-up** (ascendante) qui construit une **table DP** en résolvant les sous-problèmes des plus petits aux plus grands, de manière itérative.

**Principe** : Itération + Table DP (Array)

**Implémentation - Fibonacci** :

```javascript
function fibonacciTabulation(n) {
  if (n <= 1) return n;

  const dp = Array(n + 1);
  dp[0] = 0;
  dp[1] = 1;

  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp[n];
}

// Complexité : Temps O(n), Espace O(n)
```

**Avantages** :

- Pas de pile d'appels (pas de risque de stack overflow)
- Souvent plus rapide (meilleure localité mémoire)
- Contrôle total sur l'ordre de calcul

**Inconvénients** :

- Moins intuitif que la récursion
- Calcule tous les sous-problèmes même si certains ne sont pas nécessaires

---

### Table DP

**Définition** : Tableau (ou matrice) utilisé en tabulation pour **stocker les solutions** de tous les sous-problèmes, construit de bas en haut.

**Exemple - Sac à dos 0/1** :

```javascript
// dp[i][w] = valeur maximale avec les i premiers objets et capacité w
const dp = Array(n + 1)
  .fill(0)
  .map(() => Array(W + 1).fill(0));

for (let i = 1; i <= n; i++) {
  for (let w = 1; w <= W; w++) {
    if (weights[i - 1] <= w) {
      dp[i][w] = Math.max(
        dp[i - 1][w], // Ne pas prendre l'objet
        values[i - 1] + dp[i - 1][w - weights[i - 1]], // Prendre l'objet
      );
    } else {
      dp[i][w] = dp[i - 1][w];
    }
  }
}
```

---

### Sac à dos 0/1 (0/1 Knapsack)

**Définition** : Problème d'optimisation où on doit sélectionner des objets (chacun avec un poids et une valeur) pour maximiser la valeur totale sans dépasser une capacité donnée. Chaque objet peut être pris (1) ou non (0), pas de fractions.

**Formulation** :

- Entrée : n objets avec poids[i] et valeurs[i], capacité W
- Sortie : Valeur maximale réalisable

**Solution DP** :

```
dp[i][w] = max(
  dp[i-1][w],                      // Ne pas prendre l'objet i
  values[i] + dp[i-1][w-poids[i]]  // Prendre l'objet i
)
```

**Complexité** : O(nW) - Pseudo-polynomiale

**Note** : Contrairement au sac à dos fractionnaire, l'approche gloutonne ne fonctionne PAS pour le sac à dos 0/1.

---

### Sac à dos Fractionnaire (Fractional Knapsack)

**Définition** : Variante du sac à dos où on peut prendre des **fractions** d'objets. L'approche **gloutonne** (trier par ratio valeur/poids) donne la solution optimale.

**Complexité** : O(n log n) (à cause du tri)

---

### Complexité Pseudo-polynomiale

**Définition** : Complexité qui semble polynomiale mais dépend de la **valeur numérique** d'une entrée plutôt que de sa **taille en bits**.

**Exemple** : Le sac à dos 0/1 avec complexité O(nW) est pseudo-polynomial car W peut être exponentiel par rapport à sa taille en bits.

- Si W = 1000 (encodé sur ~10 bits), O(nW) semble raisonnable
- Si W = 10^9 (encodé sur ~30 bits), O(nW) devient impraticable

---

### Top-down vs Bottom-up

**Définition** : Deux approches de la programmation dynamique.

| Aspect             | Top-down (Mémoïsation)                | Bottom-up (Tabulation)                 |
| ------------------ | ------------------------------------- | -------------------------------------- |
| **Style**          | Récursif                              | Itératif                               |
| **Direction**      | Du problème vers les cas de base      | Des cas de base vers le problème       |
| **Structure**      | Cache (Map/Object)                    | Table DP (Array)                       |
| **Sous-problèmes** | Calcule uniquement ceux nécessaires   | Calcule tous les sous-problèmes        |
| **Pile d'appels**  | Oui (risque stack overflow)           | Non                                    |
| **Performance**    | Parfois plus lent (overhead récursif) | Souvent plus rapide (localité mémoire) |
| **Intuitivité**    | Plus naturel pour problèmes récursifs | Plus difficile à concevoir             |

---

## Module 7 : Révision et Pratique Avancée

### Pattern Two Pointers (Deux Pointeurs)

**Définition** : Technique algorithmique utilisant **deux pointeurs** qui parcourent une structure de données (souvent un tableau) pour résoudre un problème efficacement.

**Variantes** :

- **Pointeurs opposés** : Début et fin se rapprochent (ex: vérifier palindrome)
- **Pointeurs dans le même sens** : Deux pointeurs avancent à des vitesses différentes (ex: supprimer doublons)

**Exemple - Somme de deux nombres (tableau trié)** :

```javascript
function sommeDeux(arr, cible) {
  let gauche = 0;
  let droite = arr.length - 1;

  while (gauche < droite) {
    const somme = arr[gauche] + arr[droite];

    if (somme === cible) {
      return [gauche, droite];
    } else if (somme < cible) {
      gauche++;
    } else {
      droite--;
    }
  }

  return null;
}
```

**Complexité** : O(n) au lieu de O(n²) avec deux boucles imbriquées

---

### Pattern Sliding Window (Fenêtre Glissante)

**Définition** : Technique qui utilise une **fenêtre** (sous-ensemble contigu) qui se déplace sur les données pour optimiser le calcul d'agrégats.

**Principe** : Au lieu de recalculer tout à chaque étape, on retire l'élément qui sort de la fenêtre et on ajoute celui qui entre.

**Exemple - Somme maximale d'un sous-tableau de taille k** :

```javascript
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
    sommeActuelle = sommeActuelle - arr[i - k] + arr[i];
    sommeMax = Math.max(sommeMax, sommeActuelle);
  }

  return sommeMax;
}
```

**Complexité** : O(n) au lieu de O(n×k)

---

### Optimisation Prématurée

**Définition** : Pratique de tenter d'optimiser le code **trop tôt** dans le processus de développement, avant même de savoir si l'optimisation est nécessaire.

**Citation célèbre** : "Premature optimization is the root of all evil" - Donald Knuth

**Approche recommandée** :

1. **D'abord** : Écrire un code correct et lisible
2. **Ensuite** : Mesurer les performances (profiling)
3. **Enfin** : Optimiser uniquement les goulots d'étranglement identifiés

---

### Profiling (Profilage)

**Définition** : Processus de **mesure des performances** d'un programme pour identifier les parties qui consomment le plus de temps ou de mémoire (goulots d'étranglement).

**Outils JavaScript** :

- `console.time()` / `console.timeEnd()`
- Chrome DevTools Performance tab
- Node.js `--prof` flag
- `performance.now()`

**Exemple** :

```javascript
console.time("Tri");
triRapide(largeArray);
console.timeEnd("Tri");
// Tri: 15.234ms
```

---

### Goulot d'Étranglement (Bottleneck)

**Définition** : Partie d'un algorithme ou système qui **limite les performances globales**. C'est la section la plus lente qui détermine la vitesse totale.

**Identification** : Utiliser le profiling pour détecter où le code passe le plus de temps.

---

### Compromis Temps-Espace (Time-Space Tradeoff)

**Définition** : Principe selon lequel on peut souvent **échanger** de la mémoire contre du temps de calcul, ou vice versa.

**Exemples** :

- **Mémoïsation** : Utilise plus d'espace O(n) pour réduire le temps O(2^n) → O(n)
- **Tabulation optimisée** : Réduit l'espace O(n) → O(1) en gardant seulement les k dernières valeurs
- **Cache** : Stocke des résultats en mémoire pour éviter les recalculs

**Décision** : Dépend des contraintes du problème (mémoire limitée vs temps limité)

---

### Cache / Mise en Cache (Caching)

**Définition** : Technique de stockage temporaire de **résultats** ou **données fréquemment utilisées** pour améliorer les performances en évitant des calculs ou accès répétés.

**Types** :

- **Mémoïsation** : Cache des résultats de fonctions
- **Cache HTTP** : Stocke des réponses d'API
- **Cache navigateur** : Stocke des fichiers statiques

---

### Invariant de Boucle (Loop Invariant)

**Définition** : Propriété qui reste **vraie** avant et après chaque itération d'une boucle. Utilisé pour prouver la **correction** d'un algorithme.

**Exemple - Recherche linéaire** :

```javascript
function recherche(arr, cible) {
  for (let i = 0; i < arr.length; i++) {
    // Invariant : cible n'est pas dans arr[0...i-1]
    if (arr[i] === cible) return i;
  }
  return -1;
}
```

---

### Programmation Compétitive (Competitive Programming)

**Définition** : Sport intellectuel où les participants résolvent des **problèmes algorithmiques** sous contraintes de temps, testant la conception d'algorithmes, les structures de données et l'implémentation rapide.

**Plateformes** :

- LeetCode
- HackerRank
- Codeforces
- CodeChef
- AtCoder
- TopCoder

**Compétitions** :

- Google Code Jam
- Meta Hacker Cup
- ACM ICPC (International Collegiate Programming Contest)

---

### Complexité Amortie (Amortized Complexity)

**Définition** : Complexité **moyenne** d'une opération sur une **séquence** d'opérations, même si certaines opérations individuelles peuvent être coûteuses.

**Exemple - push() dans un tableau dynamique** :

- La plupart des push() sont O(1)
- Parfois, il faut redimensionner le tableau → O(n)
- **Complexité amortie** : O(1) car le redimensionnement est rare

---

## 🔗 Termes Généraux

### Correctness (Correction)

**Définition** : Propriété d'un algorithme qui **produit le résultat attendu** pour toutes les entrées valides.

**Preuves de correction** :

- Preuves mathématiques
- Invariants de boucle
- Induction mathématique
- Tests exhaustifs

---

### Déterministe

**Définition** : Un algorithme est **déterministe** si, pour une même entrée, il produit toujours la même sortie en suivant les mêmes étapes.

**Contraire** : Algorithme **probabiliste** ou **randomisé** (ex: Quick Sort avec pivot aléatoire)

---

### In-Situ / En Place (In-Place)

**Définition** : Un algorithme qui modifie la structure de données d'entrée **sans utiliser** de mémoire supplémentaire significative (seulement O(1) espace auxiliaire).

**Exemples** : Tri rapide, tri par insertion, tri à bulles

---

### Stable

**Définition** : Un algorithme de tri est **stable** s'il **préserve l'ordre relatif** des éléments ayant la même clé de tri.

**Exemple** :

```javascript
// Données : [{nom: "Chermann", âge: 43}, {nom: "Prudence", âge: 45}]
// Tri stable par âge → L'ordre Chermann-Prudence est préservé
```

**Tris stables** : Tri fusion, tri par insertion, tri à bulles
**Tris non stables** : Tri rapide, tri par sélection, tri par tas

---

### Itératif

**Définition** : Approche utilisant des **boucles** (for, while) pour répéter des opérations.

**Avantages** :

- Pas de pile d'appels
- Souvent plus rapide
- Pas de risque de stack overflow

---

### Récursif

**Définition** : Approche où une fonction **s'appelle elle-même** pour résoudre un problème.

**Avantages** :

- Code plus élégant pour problèmes naturellement récursifs
- Simplifie diviser-pour-régner

**Inconvénients** :

- Utilise la pile d'appels
- Risque de stack overflow

---

### Heuristique

**Définition** : Technique de résolution de problème utilisant une **approche pratique** ou un **raccourci** qui ne garantit pas la solution optimale mais fournit une solution satisfaisante rapidement.

**Exemples** :

- Algorithmes gloutons (heuristiques pour trouver de bonnes solutions)
- A\* (utilise une heuristique pour le pathfinding)

---

### NP-Complet

**Définition** : Classe de problèmes pour lesquels aucun algorithme polynomial n'est connu, mais une solution proposée peut être **vérifiée** en temps polynomial.

**Exemples** :

- Sac à dos 0/1
- Voyageur de commerce (TSP)
- Satisfiabilité booléenne (SAT)
- Coloration de graphe

**Implication** : Pour n grand, ces problèmes nécessitent des approches approximatives ou heuristiques.

---

### Complexité Asymptotique

**Définition** : Comportement d'un algorithme lorsque la taille de l'entrée **tend vers l'infini**. La notation Big O décrit la complexité asymptotique.

**Focus** : Termes dominants (on ignore les constantes et termes de moindre ordre)

**Exemple** :

```
5n² + 3n + 17 → O(n²)
```

---

## 📊 Tableaux Récapitulatifs

### Tableau des Complexités Big O

| Notation       | Nom            | Exemple           | n=10    | n=100  | n=1000  | Performance   |
| -------------- | -------------- | ----------------- | ------- | ------ | ------- | ------------- |
| **O(1)**       | Constante      | Accès tableau     | 1       | 1      | 1       | Excellente    |
| **O(log n)**   | Logarithmique  | Recherche binaire | 3       | 7      | 10      | Très bonne    |
| **O(n)**       | Linéaire       | Parcours tableau  | 10      | 100    | 1000    | Bonne         |
| **O(n log n)** | Quasi-linéaire | Tri fusion        | 30      | 700    | 10000   | Acceptable    |
| **O(n²)**      | Quadratique    | Tri à bulles      | 100     | 10000  | 1000000 | Passable      |
| **O(2ⁿ)**      | Exponentielle  | Fibonacci naïf    | 1024    | ~10³⁰  | ~10³⁰⁰  | Très mauvaise |
| **O(n!)**      | Factorielle    | Permutations      | 3628800 | ~10¹⁵⁷ | ~10²⁵⁶⁷ | Impraticable  |

---

### Comparaison des Algorithmes de Tri

| Algorithme        | Meilleur Cas | Cas Moyen  | Pire Cas   | Espace   | Stable | Usage              |
| ----------------- | ------------ | ---------- | ---------- | -------- | ------ | ------------------ |
| **Tri à Bulles**  | O(n)         | O(n²)      | O(n²)      | O(1)     | ✅     | Pédagogique        |
| **Tri Sélection** | O(n²)        | O(n²)      | O(n²)      | O(1)     | ❌     | Rarement           |
| **Tri Insertion** | O(n)         | O(n²)      | O(n²)      | O(1)     | ✅     | Petits tableaux    |
| **Tri Fusion**    | O(n log n)   | O(n log n) | O(n log n) | O(n)     | ✅     | Grandes données    |
| **Tri Rapide**    | O(n log n)   | O(n log n) | O(n²)      | O(log n) | ❌     | Général (meilleur) |

---

### Comparaison des Structures de Données

| Structure            | Accès    | Recherche | Insertion | Suppression | Espace |
| -------------------- | -------- | --------- | --------- | ----------- | ------ |
| **Tableau**          | O(1)     | O(n)      | O(n)      | O(n)        | O(n)   |
| **Liste Chaînée**    | O(n)     | O(n)      | O(1)\*    | O(1)\*      | O(n)   |
| **Pile**             | O(n)     | O(n)      | O(1)      | O(1)        | O(n)   |
| **File**             | O(n)     | O(n)      | O(1)      | O(1)        | O(n)   |
| **BST (équilibré)**  | O(log n) | O(log n)  | O(log n)  | O(log n)    | O(n)   |
| **Table de Hachage** | -        | O(1)\*\*  | O(1)\*\*  | O(1)\*\*    | O(n)   |

_\* En tête de liste
\*\* Cas moyen, pire cas O(n)_

---

### Comparaison Mémoïsation vs Tabulation

| Aspect             | Mémoïsation (Top-down)                  | Tabulation (Bottom-up)                                 |
| ------------------ | --------------------------------------- | ------------------------------------------------------ |
| **Approche**       | Récursive                               | Itérative                                              |
| **Direction**      | Problème → Cas de base                  | Cas de base → Problème                                 |
| **Stockage**       | Cache (Map/Object)                      | Table DP (Array)                                       |
| **Sous-problèmes** | Seulement nécessaires                   | Tous                                                   |
| **Pile d'appels**  | Oui (risque stack overflow)             | Non                                                    |
| **Implémentation** | Plus facile (ajouter cache à récursion) | Plus difficile                                         |
| **Performance**    | Overhead récursif                       | Meilleure localité mémoire                             |
| **Quand utiliser** | Structure récursive naturelle           | Grande profondeur, tous les sous-problèmes nécessaires |

---

## 🎓 Conclusion

Ce glossaire couvre les **42 leçons** des **7 modules** de la formation. Il est conçu pour être une **référence rapide** lors de vos révisions ou de la résolution de problèmes algorithmiques.

**Conseils d'utilisation** :

- 📖 Utilisez Ctrl+F / Cmd+F pour rechercher un terme spécifique
- 🔄 Révisez régulièrement les complexités et patterns
- 💡 Reliez les termes entre eux pour comprendre les connexions
- 🎯 Pratiquez avec des exemples de code pour chaque concept
- 📚 Référez-vous aux leçons complètes pour approfondir

**Modules complémentaires** :

- [README.md](README.md) - Vue d'ensemble du cours

---

**Dernière mise à jour** : 2026-01-24

**Bonne révision et bon codage !** 🚀
