##### Leçon 24 sur 42

# Pratique : Utiliser la Récursion pour les Opérations sur Tableaux

**Module 4** : Algorithmes de Recherche et Introduction à la Récursion

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Implémenter la **somme récursive** d'un tableau avec deux approches (slice vs index)
- Trouver le **maximum/minimum** d'un tableau récursivement
- Créer des fonctions de **transformation** récursives (doubler, filtrer)
- Appliquer ces patterns à notre **étude de cas** de gestion de tâches
- Comparer les **avantages et inconvénients** des approches récursives vs itératives
- Choisir la **bonne approche** selon le contexte

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçons 21-23 complétées** : Maîtriser les fonctions récursives et la pile d'appels
- **Module 2 complété** : Comprendre les tableaux et leurs opérations
- **Méthodes de tableau** : Connaître `slice()`, `map()`, `filter()`, `reduce()`
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : La Récursion en Action

Dans les leçons précédentes, vous avez appris les fondements de la récursion. Maintenant, il est temps de mettre ces connaissances en pratique sur des problèmes concrets !

La récursion est particulièrement élégante pour traiter les tableaux car ils ont une **structure auto-similaire** : un tableau peut être vu comme un premier élément suivi d'un sous-tableau (le reste).

```
[5, 3, 8, 2] = 5 + [3, 8, 2]
             = 5 + 3 + [8, 2]
             = 5 + 3 + 8 + [2]
             = 5 + 3 + 8 + 2 + []
```

Ce pattern s'applique à de nombreuses opérations : somme, recherche, transformation, filtrage...

> **Point Clé**
>
> Traiter un tableau récursivement suit toujours le même pattern : **traiter le premier élément** + **récursion sur le reste**. Ce pattern est la clé pour résoudre une multitude de problèmes sur les tableaux de manière élégante et lisible.

---

## 💻 Opération 1 : Somme Récursive d'un Tableau

Calculer la somme des éléments est l'opération récursive la plus fondamentale sur un tableau.

---

### Approche 1 : Avec `slice()` (Simple mais moins performante)

```javascript
/**
 * Calcule la somme des éléments d'un tableau récursivement.
 * Approche avec slice() - crée un nouveau tableau à chaque appel.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - La somme de tous les éléments.
 */
function sommeTableau(tableau) {
  // Cas de base 1 : Tableau vide → somme = 0
  if (tableau.length === 0) {
    return 0;
  }

  // Cas de base 2 : Un seul élément → somme = cet élément
  if (tableau.length === 1) {
    return tableau[0];
  }

  // Appel récursif : premier élément + somme du reste
  // slice(1) crée un nouveau tableau sans le premier élément
  return tableau[0] + sommeTableau(tableau.slice(1));
}

// Tests avec les notes des élèves
const notesChermann = [15, 18, 12, 16, 14];
console.log("Total notes Chermann :", sommeTableau(notesChermann)); // 75

const notesIngrid = [17, 19, 15];
console.log("Total notes Ingrid :", sommeTableau(notesIngrid)); // 51

console.log("Tableau vide :", sommeTableau([])); // 0
```

**Inconvénient :** `slice(1)` crée un **nouveau tableau** à chaque appel récursif, ce qui consomme de la mémoire.

---

### Approche 2 : Avec Index (Plus performante)

```javascript
/**
 * Calcule la somme des éléments d'un tableau récursivement.
 * Approche avec index - ne crée pas de nouveaux tableaux.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @param {number} index - L'index actuel (par défaut 0).
 * @returns {number} - La somme de tous les éléments.
 */
function sommeTableauIndex(tableau, index = 0) {
  // Cas de base : index atteint la fin du tableau
  if (index >= tableau.length) {
    return 0;
  }

  // Appel récursif : élément actuel + somme à partir de l'index suivant
  return tableau[index] + sommeTableauIndex(tableau, index + 1);
}

// Tests
const prixCourses = [25, 30, 15, 8, 12];
console.log("Total courses :", sommeTableauIndex(prixCourses)); // 90

const scoresSarr = [1250, 980, 1420, 1150];
console.log("Total scores Sarr :", sommeTableauIndex(scoresSarr)); // 4800
```

**Avantage :** Pas de création de tableaux intermédiaires = plus efficace en mémoire.

---

### Comparaison des Deux Approches

| Critère            | Approche `slice()` | Approche Index           |
| ------------------ | ------------------ | ------------------------ |
| **Lisibilité**     | Plus intuitive     | Paramètre supplémentaire |
| **Performance**    | O(n²) en mémoire   | O(n) en mémoire          |
| **Recommandation** | Petits tableaux    | Grands tableaux          |

---

## 📝 Micro-Exercice #1 : Produit Récursif

**Objectif :** Adapter le pattern de somme pour calculer un produit.

**Instructions :** Implémentez `produitTableau(tableau)` qui calcule le produit de tous les éléments.

```javascript
// Exemples attendus :
produitTableau([1, 2, 3, 4]); // 24
produitTableau([5, 2, 10]); // 100
produitTableau([]); // 1 (produit vide = 1)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function produitTableau(tableau) {
  // Cas de base : tableau vide → produit = 1
  if (tableau.length === 0) {
    return 1;
  }

  // Appel récursif : premier élément × produit du reste
  return tableau[0] * produitTableau(tableau.slice(1));
}

// Tests
console.log(produitTableau([1, 2, 3, 4])); // 24
console.log(produitTableau([5, 2, 10])); // 100
console.log(produitTableau([])); // 1
```

**Différence clé :** Le cas de base retourne **1** (élément neutre de la multiplication) au lieu de 0.

</details>

---

## 💻 Opération 2 : Trouver le Maximum Récursivement

Trouver le plus grand élément d'un tableau est un excellent exercice de récursion.

---

### Approche 1 : Avec `slice()`

```javascript
/**
 * Trouve le maximum d'un tableau récursivement.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - Le maximum du tableau.
 * @throws {Error} - Si le tableau est vide.
 */
function maximum(tableau) {
  // Cas erreur : tableau vide
  if (tableau.length === 0) {
    throw new Error("Impossible de trouver le maximum d'un tableau vide.");
  }

  // Cas de base : un seul élément = c'est le max
  if (tableau.length === 1) {
    return tableau[0];
  }

  // Appel récursif : comparer le premier avec le max du reste
  const maxDuReste = maximum(tableau.slice(1));

  // Retourner le plus grand
  return tableau[0] > maxDuReste ? tableau[0] : maxDuReste;
}

// Tests avec les scores de Prudence
const scoresPrudence = [85, 92, 78, 95, 88];
console.log("Meilleur score de Prudence :", maximum(scoresPrudence)); // 95

const temperatures = [22, 28, 31, 25, 29];
console.log("Température maximale :", maximum(temperatures)); // 31
```

---

### Approche 2 : Avec Index et Accumulateur

```javascript
/**
 * Trouve le maximum d'un tableau récursivement.
 * Approche avec index et accumulateur - plus performante.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @param {number} index - L'index actuel.
 * @param {number} maxActuel - Le maximum trouvé jusqu'ici.
 * @returns {number} - Le maximum du tableau.
 */
function maximumIndex(tableau, index = 0, maxActuel = -Infinity) {
  // Cas erreur : tableau vide
  if (tableau.length === 0) {
    throw new Error("Impossible de trouver le maximum d'un tableau vide.");
  }

  // Cas de base : on a parcouru tout le tableau
  if (index >= tableau.length) {
    return maxActuel;
  }

  // Mettre à jour le maximum si l'élément actuel est plus grand
  const nouveauMax = tableau[index] > maxActuel ? tableau[index] : maxActuel;

  // Appel récursif avec l'index suivant
  return maximumIndex(tableau, index + 1, nouveauMax);
}

// Tests
const notesGermain = [14, 16, 19, 12, 17];
console.log("Meilleure note de Germain :", maximumIndex(notesGermain)); // 19

const ventes = [1200, 980, 1500, 1100, 1350];
console.log("Meilleure vente :", maximumIndex(ventes)); // 1500
```

---

### Fonction Minimum (Adaptation)

```javascript
/**
 * Trouve le minimum d'un tableau récursivement.
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {number} - Le minimum du tableau.
 */
function minimum(tableau) {
  if (tableau.length === 0) {
    throw new Error("Impossible de trouver le minimum d'un tableau vide.");
  }

  if (tableau.length === 1) {
    return tableau[0];
  }

  const minDuReste = minimum(tableau.slice(1));
  return tableau[0] < minDuReste ? tableau[0] : minDuReste;
}

// Test
const ages = [25, 32, 19, 45, 28];
console.log("Âge minimum :", minimum(ages)); // 19
```

---

## 📝 Micro-Exercice #2 : Moyenne Récursive

**Objectif :** Combiner somme récursive et longueur pour calculer une moyenne.

**Instructions :** Implémentez `moyenne(tableau)` qui calcule la moyenne des éléments.

```javascript
// Exemples attendus :
moyenne([10, 20, 30]); // 20
moyenne([5]); // 5
moyenne([]); // 0
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function moyenne(tableau) {
  if (tableau.length === 0) {
    return 0;
  }

  // Utiliser notre somme récursive
  const total = sommeTableau(tableau);
  return total / tableau.length;
}

// Tests
console.log(moyenne([10, 20, 30])); // 20
console.log(moyenne([5])); // 5
console.log(moyenne([])); // 0

// Moyenne des notes de Sing
const notesSing = [15, 17, 14, 16, 18];
console.log("Moyenne de Sing :", moyenne(notesSing)); // 16
```

</details>

---

## 💻 Opération 3 : Transformation Récursive (Map)

La récursion peut transformer chaque élément d'un tableau, comme la méthode `map()`.

---

### Exemple : Doubler les Éléments

```javascript
/**
 * Double chaque élément d'un tableau récursivement.
 * Équivalent récursif de : tableau.map(x => x * 2)
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {Array<number>} - Nouveau tableau avec les éléments doublés.
 */
function doublerTableau(tableau) {
  // Cas de base : tableau vide → retourner tableau vide
  if (tableau.length === 0) {
    return [];
  }

  // Doubler le premier élément
  const premierDouble = tableau[0] * 2;

  // Récursivement doubler le reste
  const resteDouble = doublerTableau(tableau.slice(1));

  // Combiner : premier élément doublé + reste doublé
  return [premierDouble, ...resteDouble];
}

// Tests
const prix = [10, 25, 15, 30];
console.log("Prix originaux :", prix);
console.log("Prix doublés :", doublerTableau(prix)); // [20, 50, 30, 60]

const points = [5, 10, 15];
console.log("Points doublés :", doublerTableau(points)); // [10, 20, 30]
```

---

### Fonction Map Générique

```javascript
/**
 * Applique une fonction à chaque élément d'un tableau récursivement.
 * Équivalent récursif de : tableau.map(fn)
 * @param {Array<any>} tableau - Le tableau à transformer.
 * @param {Function} fn - La fonction de transformation.
 * @returns {Array<any>} - Nouveau tableau transformé.
 */
function mapRecursif(tableau, fn) {
  // Cas de base
  if (tableau.length === 0) {
    return [];
  }

  // Appliquer fn au premier élément + récursion sur le reste
  return [fn(tableau[0]), ...mapRecursif(tableau.slice(1), fn)];
}

// Tests avec différentes transformations
const nombres = [1, 2, 3, 4, 5];

// Tripler
console.log(
  "Triplés :",
  mapRecursif(nombres, (x) => x * 3),
); // [3, 6, 9, 12, 15]

// Carrés
console.log(
  "Carrés :",
  mapRecursif(nombres, (x) => x * x),
); // [1, 4, 9, 16, 25]

// Texte
const prenoms = ["Chermann", "Ingrid", "Prudence"];
console.log(
  "Majuscules :",
  mapRecursif(prenoms, (p) => p.toUpperCase()),
);
// ["CHERMANN", "INGRID", "PRUDENCE"]
```

---

## 💻 Opération 4 : Filtrage Récursif

Le filtrage récursif permet de sélectionner les éléments qui satisfont une condition.

---

### Exemple : Filtrer les Nombres Pairs

```javascript
/**
 * Filtre les nombres pairs d'un tableau récursivement.
 * Équivalent récursif de : tableau.filter(x => x % 2 === 0)
 * @param {Array<number>} tableau - Le tableau de nombres.
 * @returns {Array<number>} - Tableau contenant uniquement les nombres pairs.
 */
function filtrerPairs(tableau) {
  // Cas de base
  if (tableau.length === 0) {
    return [];
  }

  const premier = tableau[0];
  const resteFiltré = filtrerPairs(tableau.slice(1));

  // Si le premier est pair, l'inclure
  if (premier % 2 === 0) {
    return [premier, ...resteFiltré];
  } else {
    // Sinon, retourner uniquement le reste filtré
    return resteFiltré;
  }
}

// Tests
const nombres = [1, 2, 3, 4, 5, 6, 7, 8];
console.log("Nombres pairs :", filtrerPairs(nombres)); // [2, 4, 6, 8]

const loterie = [7, 14, 21, 28, 35];
console.log("Multiples de 7 pairs :", filtrerPairs(loterie)); // [14, 28]
```

---

### Fonction Filter Générique

```javascript
/**
 * Filtre un tableau selon une condition, récursivement.
 * Équivalent récursif de : tableau.filter(condition)
 * @param {Array<any>} tableau - Le tableau à filtrer.
 * @param {Function} condition - La fonction de test.
 * @returns {Array<any>} - Tableau filtré.
 */
function filterRecursif(tableau, condition) {
  // Cas de base
  if (tableau.length === 0) {
    return [];
  }

  const premier = tableau[0];
  const resteFiltré = filterRecursif(tableau.slice(1), condition);

  // Tester la condition
  if (condition(premier)) {
    return [premier, ...resteFiltré];
  } else {
    return resteFiltré;
  }
}

// Tests avec différentes conditions
const ages = [15, 22, 17, 30, 16, 25];

// Majeurs (>= 18)
console.log(
  "Majeurs :",
  filterRecursif(ages, (age) => age >= 18),
); // [22, 30, 25]

// Moins de 20 ans
console.log(
  "< 20 ans :",
  filterRecursif(ages, (age) => age < 20),
); // [15, 17, 16]

// Scores de Marc-Élie (garder les bons scores)
const scoresMarc = [45, 82, 67, 91, 53, 78];
console.log(
  "Scores >= 70 :",
  filterRecursif(scoresMarc, (s) => s >= 70),
); // [82, 91, 78]
```

---

## 📝 Micro-Exercice #3 : Compter les Occurrences

**Objectif :** Compter combien de fois une valeur apparaît dans un tableau.

**Instructions :** Implémentez `compterOccurrences(tableau, valeur)`.

```javascript
// Exemples attendus :
compterOccurrences([1, 2, 3, 2, 4, 2], 2); // 3
compterOccurrences(["pomme", "banane", "pomme"], "pomme"); // 2
compterOccurrences([1, 2, 3], 5); // 0
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function compterOccurrences(tableau, valeur) {
  // Cas de base
  if (tableau.length === 0) {
    return 0;
  }

  // 1 si correspondance, 0 sinon
  const compte = tableau[0] === valeur ? 1 : 0;

  // Ajouter les occurrences dans le reste
  return compte + compterOccurrences(tableau.slice(1), valeur);
}

// Tests
console.log(compterOccurrences([1, 2, 3, 2, 4, 2], 2)); // 3
console.log(compterOccurrences(["pomme", "banane", "pomme"], "pomme")); // 2
console.log(compterOccurrences([1, 2, 3], 5)); // 0

// Compter les votes pour Destinée
const votes = ["Destinée", "Sarr", "Destinée", "Ingrid", "Destinée"];
console.log("Votes pour Destinée :", compterOccurrences(votes, "Destinée")); // 3
```

</details>

---

## 💼 Application : Étude de Cas - Gestionnaire de Tâches

Appliquons nos fonctions récursives à notre étude de cas de gestion de tâches.

---

### Les Données

```javascript
const taches = [
  {
    id: 1,
    titre: "Réviser JavaScript",
    priorite: 3,
    terminee: true,
    heures: 4,
  },
  {
    id: 2,
    titre: "Apprendre la récursion",
    priorite: 5,
    terminee: true,
    heures: 3,
  },
  {
    id: 3,
    titre: "Faire les exercices",
    priorite: 4,
    terminee: false,
    heures: 2,
  },
  { id: 4, titre: "Projet personnel", priorite: 2, terminee: false, heures: 8 },
  {
    id: 5,
    titre: "Lire la documentation",
    priorite: 3,
    terminee: true,
    heures: 1,
  },
];
```

---

### Opération 1 : Calculer le Temps Total Travaillé

```javascript
/**
 * Calcule le temps total des tâches terminées.
 * @param {Array<Object>} taches - Liste des tâches.
 * @returns {number} - Heures totales des tâches terminées.
 */
function tempsTermine(taches) {
  if (taches.length === 0) {
    return 0;
  }

  const premiere = taches[0];
  const reste = tempsTermine(taches.slice(1));

  // Ajouter les heures seulement si la tâche est terminée
  return premiere.terminee ? premiere.heures + reste : reste;
}

console.log("Heures travaillées :", tempsTermine(taches)); // 8 (4+3+1)
```

---

### Opération 2 : Filtrer les Tâches par Priorité

```javascript
/**
 * Filtre les tâches avec une priorité >= seuil.
 * @param {Array<Object>} taches - Liste des tâches.
 * @param {number} seuilPriorite - Priorité minimale.
 * @returns {Array<Object>} - Tâches urgentes.
 */
function tachesUrgentes(taches, seuilPriorite) {
  if (taches.length === 0) {
    return [];
  }

  const premiere = taches[0];
  const resteFiltre = tachesUrgentes(taches.slice(1), seuilPriorite);

  if (premiere.priorite >= seuilPriorite) {
    return [premiere, ...resteFiltre];
  }
  return resteFiltre;
}

const urgentes = tachesUrgentes(taches, 4);
console.log("Tâches urgentes (priorité >= 4) :");
urgentes.forEach((t) =>
  console.log(`  - ${t.titre} (priorité: ${t.priorite})`),
);
// - Apprendre la récursion (priorité: 5)
// - Faire les exercices (priorité: 4)
```

---

### Opération 3 : Extraire les Titres des Tâches

```javascript
/**
 * Extrait les titres de toutes les tâches.
 * @param {Array<Object>} taches - Liste des tâches.
 * @returns {Array<string>} - Liste des titres.
 */
function extraireTitres(taches) {
  if (taches.length === 0) {
    return [];
  }

  return [taches[0].titre, ...extraireTitres(taches.slice(1))];
}

console.log("Tous les titres :", extraireTitres(taches));
// ["Réviser JavaScript", "Apprendre la récursion", "Faire les exercices", ...]
```

---

### Opération 4 : Trouver la Tâche la Plus Prioritaire

```javascript
/**
 * Trouve la tâche avec la plus haute priorité.
 * @param {Array<Object>} taches - Liste des tâches.
 * @returns {Object|null} - La tâche la plus prioritaire.
 */
function tachePlusPrioritaire(taches) {
  if (taches.length === 0) {
    return null;
  }

  if (taches.length === 1) {
    return taches[0];
  }

  const premiere = taches[0];
  const plusPrioritaireDuReste = tachePlusPrioritaire(taches.slice(1));

  return premiere.priorite > plusPrioritaireDuReste.priorite
    ? premiere
    : plusPrioritaireDuReste;
}

const topTache = tachePlusPrioritaire(taches);
console.log("Tâche la plus prioritaire :", topTache.titre);
// "Apprendre la récursion"
```

---

## 💪 Exercices Pratiques

Pour consolider vos compétences, complétez les exercices suivants.

---

### Exercice 1 : Longueur Récursive

**Objectif :** Calculer la longueur d'un tableau SANS utiliser `.length`.

**Instructions :** Implémentez `longueurRecursive(tableau)`.

```javascript
// Exemples attendus :
longueurRecursive([1, 2, 3]); // 3
longueurRecursive([]); // 0
longueurRecursive(["a"]); // 1
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function longueurRecursive(tableau) {
  // Cas de base : tableau "vide" quand on ne peut plus slice
  try {
    tableau[0]; // Tester si on peut accéder au premier élément
    // Si le tableau est vide, slice(1) donnera []
    if (tableau.slice(1).length === tableau.length) {
      // Alternative sans utiliser length :
      return 0;
    }
  } catch {
    return 0;
  }

  // Meilleure approche : utiliser slice pour "réduire"
  // Le cas de base est déterminé par le comportement de slice
}

// Version plus simple avec une astuce
function longueurRecursive(tableau) {
  // On peut détecter un tableau vide avec slice
  const [premier, ...reste] = tableau;

  // Si premier est undefined et reste est vide, tableau est vide
  if (premier === undefined) {
    return 0;
  }

  return 1 + longueurRecursive(reste);
}

// Tests
console.log(longueurRecursive([1, 2, 3])); // 3
console.log(longueurRecursive([])); // 0
console.log(longueurRecursive(["a"])); // 1
```

</details>

---

### Exercice 2 : Contient un Élément

**Objectif :** Vérifier si un élément existe dans un tableau.

**Instructions :** Implémentez `contientElement(tableau, element)`.

```javascript
// Exemples attendus :
contientElement([1, 2, 3], 2); // true
contientElement([1, 2, 3], 5); // false
contientElement([], 10); // false
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function contientElement(tableau, element) {
  // Cas de base : tableau vide → élément non trouvé
  if (tableau.length === 0) {
    return false;
  }

  // Si le premier correspond, trouvé !
  if (tableau[0] === element) {
    return true;
  }

  // Sinon, chercher dans le reste
  return contientElement(tableau.slice(1), element);
}

// Tests
console.log(contientElement([1, 2, 3], 2)); // true
console.log(contientElement([1, 2, 3], 5)); // false
console.log(contientElement([], 10)); // false

// Test avec les prénoms du cours
const equipe = ["Chermann", "Ingrid", "Prudence", "Germain"];
console.log(contientElement(equipe, "Ingrid")); // true
console.log(contientElement(equipe, "Marc")); // false
```

</details>

---

### Exercice 3 : Aplatir un Tableau (Shallow)

**Objectif :** Aplatir un tableau imbriqué d'un niveau.

**Instructions :** Implémentez `aplatir(tableau)`.

```javascript
// Exemples attendus :
aplatir([1, [2, 3], 4]); // [1, 2, 3, 4]
aplatir([1, [2, [3]], 4]); // [1, 2, [3], 4] (un seul niveau)
aplatir([]); // []
aplatir([1, 2, 3]); // [1, 2, 3]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function aplatir(tableau) {
  // Cas de base
  if (tableau.length === 0) {
    return [];
  }

  const premier = tableau[0];
  const resteAplati = aplatir(tableau.slice(1));

  // Si le premier est un tableau, l'étaler
  if (Array.isArray(premier)) {
    return [...premier, ...resteAplati];
  } else {
    return [premier, ...resteAplati];
  }
}

// Tests
console.log(aplatir([1, [2, 3], 4])); // [1, 2, 3, 4]
console.log(aplatir([1, [2, [3]], 4])); // [1, 2, [3], 4]
console.log(aplatir([])); // []
console.log(aplatir([1, 2, 3])); // [1, 2, 3]
```

</details>

---

### Exercice 4 : Inverser un Tableau

**Objectif :** Inverser l'ordre des éléments d'un tableau.

**Instructions :** Implémentez `inverserTableau(tableau)`.

```javascript
// Exemples attendus :
inverserTableau([1, 2, 3]); // [3, 2, 1]
inverserTableau(["a", "b"]); // ["b", "a"]
inverserTableau([]); // []
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
function inverserTableau(tableau) {
  // Cas de base
  if (tableau.length === 0) {
    return [];
  }

  // Le premier va à la fin, le reste inversé va devant
  return [...inverserTableau(tableau.slice(1)), tableau[0]];
}

// Tests
console.log(inverserTableau([1, 2, 3])); // [3, 2, 1]
console.log(inverserTableau(["a", "b"])); // ["b", "a"]
console.log(inverserTableau([])); // []

// Test avec les prénoms
const ordre = ["Chermann", "Ingrid", "Prudence"];
console.log(inverserTableau(ordre)); // ["Prudence", "Ingrid", "Chermann"]
```

**Explication :** Le premier élément est placé à la fin du résultat inversé du reste.

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quel est le cas de base pour la somme récursive d'un tableau ?**

- [ ] A. Tableau avec un élément
- [ ] B. Tableau vide (retourne 0)
- [ ] C. Tableau avec deux éléments
- [ ] D. Premier élément égal à 0

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le cas de base est le **tableau vide** qui retourne 0. Un tableau avec un élément peut aussi être un cas de base, mais le cas fondamental est le tableau vide.

</details>

---

### Question 2

**Pourquoi l'approche avec index est-elle plus performante que slice() ?**

- [ ] A. Elle est plus facile à écrire
- [ ] B. Elle évite de créer de nouveaux tableaux
- [ ] C. Elle utilise moins de paramètres
- [ ] D. Elle retourne plus vite

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

L'approche avec index **ne crée pas de nouveaux tableaux** à chaque appel récursif, ce qui économise de la mémoire et améliore les performances, surtout pour les grands tableaux.

</details>

---

### Question 3

**Quel est le résultat de `doublerTableau([2, 3, 5])` ?**

- [ ] A. [2, 3, 5]
- [ ] B. [4, 6, 10]
- [ ] C. 20
- [ ] D. [2, 2, 3, 3, 5, 5]

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

`doublerTableau` multiplie chaque élément par 2 : 2×2=4, 3×2=6, 5×2=10, donnant **[4, 6, 10]**.

</details>

---

### Question 4

**Dans le pattern récursif pour tableaux, que représente `[premier, ...reste]` ?**

- [ ] A. Le premier élément seulement
- [ ] B. Le dernier élément seulement
- [ ] C. Le premier élément suivi du résultat récursif du reste
- [ ] D. Une copie du tableau original

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La syntaxe `[premier, ...reste]` crée un nouveau tableau avec le **premier élément** suivi de tous les éléments du tableau `reste` (résultat récursif), ce qui permet de reconstruire le tableau transformé.

</details>

---

### Question 5

**Que retourne `filterRecursif([1, 2, 3, 4], x => x > 2)` ?**

- [ ] A. [1, 2]
- [ ] B. [3, 4]
- [ ] C. true
- [ ] D. 2

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La fonction filtre les éléments où x > 2, donc seuls **3 et 4** passent le test, retournant **[3, 4]**.

</details>

---

### Question 6

**Pour le produit récursif d'un tableau, que doit retourner le cas de base (tableau vide) ?**

- [ ] A. 0
- [ ] B. 1
- [ ] C. null
- [ ] D. undefined

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Pour le produit, le cas de base doit retourner **1** (élément neutre de la multiplication), tout comme la somme retourne 0 (élément neutre de l'addition).

</details>

---

### Question 7

**Quelle est la complexité mémoire de l'approche avec slice() pour un tableau de n éléments ?**

- [ ] A. O(1)
- [ ] B. O(n)
- [ ] C. O(n²)
- [ ] D. O(log n)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Avec `slice()`, chaque appel crée un nouveau tableau. Pour n éléments : n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 éléments copiés au total, soit **O(n²)** en mémoire.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Pattern Universel

Récursion sur tableau = traiter le premier élément + récursion sur le reste (slice ou index).

### 2. Deux Approches

Slice() est plus lisible mais moins performante ; l'approche avec index évite de créer des tableaux.

### 3. Cas de Base Typiques

Tableau vide → 0 (somme), 1 (produit), [] (transformation), throw Error (max/min).

### 4. Transformation (Map)

`[fn(premier), ...mapRecursif(reste, fn)]` applique une fonction à chaque élément.

### 5. Filtrage (Filter)

Inclure ou exclure le premier élément selon une condition, puis récursion sur le reste.

### 6. Application Pratique

Ces patterns s'appliquent aux objets : filtrer des tâches, calculer des totaux, extraire des propriétés.

### 7. Performance

L'approche slice() a une complexité O(n²) en mémoire ; préférer l'index pour les grands tableaux.

---

## 🎓 Conclusion et Bilan du Module 4

**Félicitations !** 🎉 Vous avez terminé le **Module 4** !

### Ce que vous avez appris dans cette leçon

- Implémenter la somme et le produit récursifs avec deux approches
- Trouver le maximum/minimum d'un tableau récursivement
- Créer des fonctions map et filter récursives
- Appliquer ces patterns à un gestionnaire de tâches
- Choisir entre récursion et itération selon le contexte

### Bilan du Module 4 : Ce que vous maîtrisez maintenant

| Leçon  | Compétence acquise                                                  |
| ------ | ------------------------------------------------------------------- |
| **19** | Recherche linéaire - trouver un élément en O(n)                     |
| **20** | Recherche binaire - trouver en O(log n) dans un tableau trié        |
| **21** | Fondements de la récursion - cas de base et appels récursifs        |
| **22** | Implémentation de fonctions récursives classiques                   |
| **23** | Compréhension de la pile d'appels et prévention des stack overflows |
| **24** | Application pratique de la récursion aux tableaux                   |

### Pourquoi c'est important

> 📌 **Point Clé**
>
> La récursion est la **fondation** de nombreux algorithmes avancés que vous rencontrerez dans les prochains modules : parcours d'arbres, exploration de graphes, tri fusion, programmation dynamique. Maîtriser les patterns récursifs sur les tableaux vous prépare à aborder ces sujets complexes avec confiance.

---

## ➡️ Prochaine Étape : Leçon 25

### Ce qui vous attend

La prochaine leçon, **« Arbres : Terminologie, Types et Cas d'Usage »**, marque le début du **Module 5** et va exploiter pleinement vos compétences en récursion !

**Vous découvrirez :**

- Les **structures arborescentes** (arbres binaires, arbres de recherche)
- Les **parcours d'arbres** (préfixe, infixe, suffixe) - tous récursifs !
- Les **graphes** et leurs représentations
- Les algorithmes **DFS (profondeur)** et **BFS (largeur)**

### Préparez-vous !

La récursion que vous venez de maîtriser sera omniprésente dans le Module 5. Les arbres sont des structures **naturellement récursives** : un arbre est un nœud avec des sous-arbres (qui sont eux-mêmes des arbres).

---

## 📊 Comparaison : Récursion vs Itération

| Critère            | Récursion             | Itération            |
| ------------------ | --------------------- | -------------------- |
| **Lisibilité**     | Souvent plus élégante | Parfois plus directe |
| **Performance**    | Stack overhead        | Plus rapide          |
| **Mémoire**        | Pile d'appels         | Variables locales    |
| **Quand utiliser** | Structures récursives | Boucles simples      |
| **Exemples**       | Arbres, tri fusion    | Recherche linéaire   |

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [FreeCodeCamp - Recursion Tutorial](https://www.freecodecamp.org/news/recursion-in-javascript/) - Tutoriel complet
- [MDN - Array Methods](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array) - Méthodes itératives natives
- [Computerphile - Recursion](https://www.youtube.com/watch?v=Mv9NEXX1VHc) - Explication visuelle

### Outils de pratique

- **[Visualgo](https://visualgo.net/)** : Visualisation d'algorithmes
- **[Python Tutor](https://pythontutor.com/javascript.html)** : Tracer l'exécution pas à pas

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil Final**
>
> Pour consolider vos acquis, essayez de **ré-implémenter** les méthodes natives `map()`, `filter()`, `reduce()` et `find()` de manière récursive. C'est un excellent exercice qui vous aidera à penser de façon récursive dans n'importe quel contexte.

---

**Prêt pour la Leçon 25 ?** 🚀

Le monde des arbres et des graphes vous attend ! Ces structures de données sont parmi les plus puissantes et les plus utilisées en informatique.

---

<div align="center">

**Leçon 24 sur 42 - Module 4 : Algorithmes de Recherche et Introduction à la Récursion**

[⬅️ Leçon 23 : Comprendre la Pile d'Appels (Call Stack) en Récursion](./lecon-5-comprendre-pile-appels-recursion.md) | [Retour au sommaire](./README.md) | [Leçon 25 : Arbres : Terminologie, Types et Cas d'Usage ➡️](../module-5/lecon-1-arbres-terminologie-types-cas-usage.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
