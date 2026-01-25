##### Leçon 16 sur 42

# Tri par Insertion : Concept et Implémentation JavaScript Pratique

**Module 3** : Techniques de Tri Essentielles

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **concept fondamental** du tri par insertion et sa métaphore du tri de cartes
- **Visualiser** le fonctionnement pas à pas avec le mécanisme de décalage
- **Implémenter** le tri par insertion en JavaScript (ascendant et descendant)
- **Analyser** la complexité temporelle et comprendre pourquoi il excelle sur les données presque triées
- **Comparer** le tri par insertion avec les tris à bulles et par sélection
- Identifier les **cas d'utilisation réels** où le tri par insertion est optimal

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 14 complétée** : Comprendre le tri à bulles et ses optimisations
- **Leçon 15 complétée** : Maîtriser le tri par sélection pour pouvoir comparer les trois approches
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : Trier Comme un Joueur de Cartes

Avez-vous déjà joué aux cartes ? Observez comment vous triez naturellement votre main : vous prenez une carte à la fois et vous l'**insérez** à sa place correcte parmi les cartes que vous tenez déjà. Vous ne comparez pas toutes les cartes entre elles, vous cherchez simplement où glisser la nouvelle carte dans votre main déjà ordonnée.

C'est exactement ainsi que fonctionne le **tri par insertion** (Insertion Sort). Il construit le tableau trié **un élément à la fois**, en prenant chaque élément de la partie non triée et en l'insérant à sa position correcte dans la partie triée.

Cette approche intuitive présente des avantages uniques :

- **Très efficace** sur les tableaux presque triés (O(n) dans le meilleur cas)
- **Stable** : préserve l'ordre relatif des éléments égaux
- **En place** : ne nécessite pas de mémoire supplémentaire
- **Adaptatif** : plus les données sont triées, plus il est rapide
- **Idéal pour les petits tableaux** ou l'insertion en temps réel

> **Point Clé**
>
> Le tri par insertion est le seul des trois algorithmes élémentaires (bulles, sélection, insertion) qui combine à la fois la **stabilité** et l'**adaptativité**. C'est pourquoi des algorithmes hybrides comme Timsort (utilisé par Python et Java) l'utilisent pour trier les petites partitions.

---

## 📦 Le Concept du Tri par Insertion

Le tri par insertion divise conceptuellement le tableau en deux parties :

1. **Sous-tableau trié** : Commence avec le premier élément (un seul élément est toujours trié)
2. **Sous-tableau non trié** : Contient les éléments restants à insérer

À chaque itération, l'algorithme prend le premier élément du sous-tableau non trié et l'**insère** à sa position correcte dans le sous-tableau trié, en **décalant** les éléments plus grands vers la droite.

---

### Mécanisme de Base

**Comment ça fonctionne :**

1. **Considérer** le premier élément comme déjà trié
2. **Prendre** le prochain élément du sous-tableau non trié
3. **Comparer** avec les éléments du sous-tableau trié (de droite à gauche)
4. **Décaler** les éléments plus grands vers la droite
5. **Insérer** l'élément à la position libérée
6. **Répéter** jusqu'à ce que tous les éléments soient insérés

**Caractéristiques clés :**

- **Stable** : préserve l'ordre relatif des éléments égaux
- **Adaptatif** : O(n) pour les tableaux presque triés
- **En place** : complexité spatiale O(1)
- **Efficace pour petits tableaux** : moins d'overhead que les algorithmes complexes
- **O(n²) dans le pire cas** : tableau trié en ordre inverse

---

### La Différence Clé : Décalage vs Échange

Contrairement au tri à bulles et au tri par sélection qui utilisent des **échanges**, le tri par insertion utilise des **décalages** :

```javascript
// Tri à bulles / Sélection : ÉCHANGE (2 écritures)
[tableau[i], tableau[j]] = [tableau[j], tableau[i]];

// Tri par insertion : DÉCALAGE (1 écriture par élément)
tableau[j + 1] = tableau[j]; // Décaler vers la droite
// ... puis une seule insertion finale
tableau[position] = valeur;
```

Cette différence rend le tri par insertion plus efficace en termes d'écritures mémoire.

---

### Visualisation Complète

Prenons un exemple concret pour visualiser le tri par insertion. Considérons le tableau suivant :

```javascript
const tableau = [5, 2, 4, 6, 1, 3];
```

**État initial :**

```
[5, 2, 4, 6, 1, 3]
 └┘ └─ non trié ┘
trié
```

Le premier élément (5) est considéré comme trié par défaut.

---

#### Itération 1 : Insérer 2

| Étape | Action                            | État du tableau          |
| ----- | --------------------------------- | ------------------------ |
| 1     | Prendre `currentValue = 2`        | [5, **2**, 4, 6, 1, 3]   |
| 2     | Comparer 2 avec 5 : 2 < 5         | Décaler 5 vers la droite |
| 3     | Décaler : tableau[1] = 5          | [5, **5**, 4, 6, 1, 3]   |
| 4     | Plus d'éléments à gauche (j = -1) | Position trouvée : 0     |
| 5     | Insérer : tableau[0] = 2          | [**2**, 5, 4, 6, 1, 3]   |

**Après itération 1 :**

```
[2, 5, 4, 6, 1, 3]
 └──┘ └ non trié ┘
 trié
```

---

#### Itération 2 : Insérer 4

| Étape | Action                     | État du tableau          |
| ----- | -------------------------- | ------------------------ |
| 1     | Prendre `currentValue = 4` | [2, 5, **4**, 6, 1, 3]   |
| 2     | Comparer 4 avec 5 : 4 < 5  | Décaler 5 vers la droite |
| 3     | Décaler : tableau[2] = 5   | [2, 5, **5**, 6, 1, 3]   |
| 4     | Comparer 4 avec 2 : 4 > 2  | Stop ! Position trouvée  |
| 5     | Insérer : tableau[1] = 4   | [2, **4**, 5, 6, 1, 3]   |

**Après itération 2 :**

```
[2, 4, 5, 6, 1, 3]
 └──────┘ └ non ┘
  trié      trié
```

---

#### Itération 3 : Insérer 6

| Étape | Action                     | État du tableau        |
| ----- | -------------------------- | ---------------------- |
| 1     | Prendre `currentValue = 6` | [2, 4, 5, **6**, 1, 3] |
| 2     | Comparer 6 avec 5 : 6 > 5  | Stop ! Pas de décalage |
| 3     | L'élément reste à sa place | [2, 4, 5, **6**, 1, 3] |

**Après itération 3 :**

```
[2, 4, 5, 6, 1, 3]
 └────────┘  └──┘
    trié     non
             trié
```

> **Observation** : Quand l'élément est déjà plus grand que tous les éléments triés, aucun décalage n'est nécessaire. C'est pourquoi le tri par insertion est O(n) sur un tableau déjà trié !

---

#### Itération 4 : Insérer 1

| Étape | Action                             | État du tableau        |
| ----- | ---------------------------------- | ---------------------- |
| 1     | Prendre `currentValue = 1`         | [2, 4, 5, 6, **1**, 3] |
| 2     | Comparer 1 avec 6 : 1 < 6, décaler | [2, 4, 5, 6, **6**, 3] |
| 3     | Comparer 1 avec 5 : 1 < 5, décaler | [2, 4, 5, **5**, 6, 3] |
| 4     | Comparer 1 avec 4 : 1 < 4, décaler | [2, 4, **4**, 5, 6, 3] |
| 5     | Comparer 1 avec 2 : 1 < 2, décaler | [2, **2**, 4, 5, 6, 3] |
| 6     | Plus d'éléments à gauche (j = -1)  | Position trouvée : 0   |
| 7     | Insérer : tableau[0] = 1           | [**1**, 2, 4, 5, 6, 3] |

**Après itération 4 :**

```
[1, 2, 4, 5, 6, 3]
 └───────────┘ └┘
     trié      non
               trié
```

---

#### Itération 5 : Insérer 3

| Étape | Action                             | État du tableau         |
| ----- | ---------------------------------- | ----------------------- |
| 1     | Prendre `currentValue = 3`         | [1, 2, 4, 5, 6, **3**]  |
| 2     | Comparer 3 avec 6 : 3 < 6, décaler | [1, 2, 4, 5, 6, **6**]  |
| 3     | Comparer 3 avec 5 : 3 < 5, décaler | [1, 2, 4, 5, **5**, 6]  |
| 4     | Comparer 3 avec 4 : 3 < 4, décaler | [1, 2, 4, **4**, 5, 6]  |
| 5     | Comparer 3 avec 2 : 3 > 2          | Stop ! Position trouvée |
| 6     | Insérer : tableau[2] = 3           | [1, 2, **3**, 4, 5, 6]  |

**Résultat final :**

```
[1, 2, 3, 4, 5, 6]
 └──────────────┘
       trié
```

---

## 📝 Micro-Exercice #1 : Tracer les Décalages

**Objectif :** Comprendre le mécanisme de décalage.

**Instructions :** Pour le tableau `[12, 11, 13, 5, 6]`, tracez l'**itération 3** (insertion de 5). Notez chaque décalage effectué.

```javascript
// État avant itération 3 : [11, 12, 13, 5, 6]
// (après avoir inséré 11 et 13)
// Élément à insérer : 5
```

<details>
<summary>💡 Voir la solution</summary>

**Itération 3 : Insérer 5 dans [11, 12, 13, 5, 6]**

| Étape | Action                      | État du tableau         |
| ----- | --------------------------- | ----------------------- |
| 1     | `currentValue = 5`          | [11, 12, 13, **5**, 6]  |
| 2     | Comparer 5 avec 13 : 5 < 13 | Décaler 13              |
| 3     | `tableau[3] = 13`           | [11, 12, 13, **13**, 6] |
| 4     | Comparer 5 avec 12 : 5 < 12 | Décaler 12              |
| 5     | `tableau[2] = 12`           | [11, 12, **12**, 13, 6] |
| 6     | Comparer 5 avec 11 : 5 < 11 | Décaler 11              |
| 7     | `tableau[1] = 11`           | [11, **11**, 12, 13, 6] |
| 8     | j = -1, fin de boucle       | Position trouvée : 0    |
| 9     | `tableau[0] = 5`            | [**5**, 11, 12, 13, 6]  |

**Explication :**

- 3 décalages ont été effectués (13, 12, 11)
- 5 a été inséré à l'index 0 (début du tableau)
- Total d'écritures : 4 (3 décalages + 1 insertion)

</details>

---

## 💻 Implémentation de Base en JavaScript

Maintenant que nous comprenons le concept, implémentons le tri par insertion en JavaScript.

---

### Version Standard

```javascript
/**
 * Tri par insertion - Implémentation standard
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié (modifié en place)
 */
function triInsertion(tableau) {
  // Commencer à l'index 1 car l'élément à l'index 0 est déjà "trié"
  for (let i = 1; i < tableau.length; i++) {
    // Sauvegarder l'élément à insérer
    const valeurCourante = tableau[i];

    // Index du dernier élément de la partie triée
    let j = i - 1;

    // Décaler les éléments plus grands vers la droite
    // tant qu'on n'a pas trouvé la position d'insertion
    while (j >= 0 && tableau[j] > valeurCourante) {
      tableau[j + 1] = tableau[j]; // Décaler vers la droite
      j--; // Passer à l'élément précédent
    }

    // Insérer l'élément à sa position correcte
    tableau[j + 1] = valeurCourante;
  }

  return tableau;
}

// Tests
const nombres = [5, 2, 4, 6, 1, 3];
console.log("Avant tri:", [...nombres]);
triInsertion(nombres);
console.log("Après tri:", nombres);
// Après tri: [1, 2, 3, 4, 5, 6]
```

**Analyse du code :**

1. **Boucle externe (`i`)** : Parcourt les éléments à insérer, en commençant à l'index 1.

2. **`valeurCourante`** : Sauvegarde l'élément à insérer car il sera écrasé lors des décalages.

3. **Boucle while** : Deux conditions d'arrêt :
   - `j >= 0` : Ne pas dépasser le début du tableau
   - `tableau[j] > valeurCourante` : Continuer tant que l'élément à gauche est plus grand

4. **Décalage** : `tableau[j + 1] = tableau[j]` déplace chaque élément d'une position vers la droite.

5. **Insertion finale** : `tableau[j + 1] = valeurCourante` place l'élément à sa position correcte.

---

### Version avec Affichage des Étapes

```javascript
/**
 * Tri par insertion avec visualisation
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triInsertionVisuel(tableau) {
  console.log(`État initial: [${tableau.join(", ")}]`);
  console.log("─".repeat(50));

  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];
    let j = i - 1;
    let decalages = 0;

    console.log(`\nInsérer ${valeurCourante}:`);
    console.log(`  Partie triée: [${tableau.slice(0, i).join(", ")}]`);

    while (j >= 0 && tableau[j] > valeurCourante) {
      tableau[j + 1] = tableau[j];
      decalages++;
      console.log(`  Décaler ${tableau[j]} vers la droite`);
      j--;
    }

    tableau[j + 1] = valeurCourante;

    if (decalages === 0) {
      console.log(`  Déjà à la bonne place !`);
    } else {
      console.log(`  Insérer ${valeurCourante} à l'index ${j + 1}`);
    }

    console.log(`  Résultat: [${tableau.join(", ")}]`);
  }

  console.log("─".repeat(50));
  console.log(`\nTableau trié: [${tableau.join(", ")}]`);
  return tableau;
}

// Test
triInsertionVisuel([5, 2, 4, 6, 1, 3]);
```

**Sortie :**

```
État initial: [5, 2, 4, 6, 1, 3]
────────────────────────────────────

Insérer 2:
  Partie triée: [5]
  Décaler 5 vers la droite
  Insérer 2 à l'index 0
  Résultat: [2, 5, 4, 6, 1, 3]

Insérer 4:
  Partie triée: [2, 5]
  Décaler 5 vers la droite
  Insérer 4 à l'index 1
  Résultat: [2, 4, 5, 6, 1, 3]

Insérer 6:
  Partie triée: [2, 4, 5]
  Déjà à la bonne place !
  Résultat: [2, 4, 5, 6, 1, 3]

Insérer 1:
  Partie triée: [2, 4, 5, 6]
  Décaler 6 vers la droite
  Décaler 5 vers la droite
  Décaler 4 vers la droite
  Décaler 2 vers la droite
  Insérer 1 à l'index 0
  Résultat: [1, 2, 4, 5, 6, 3]

Insérer 3:
  Partie triée: [1, 2, 4, 5, 6]
  Décaler 6 vers la droite
  Décaler 5 vers la droite
  Décaler 4 vers la droite
  Insérer 3 à l'index 2
  Résultat: [1, 2, 3, 4, 5, 6]
────────────────────────────────────

Tableau trié: [1, 2, 3, 4, 5, 6]
```

---

## 📝 Micro-Exercice #2 : Implémenter le Tri Descendant

**Objectif :** Adapter l'algorithme pour trier en ordre décroissant.

**Instructions :** Modifiez la fonction `triInsertion` pour trier le tableau du plus grand au plus petit.

```javascript
function triInsertionDescendant(tableau) {
  // Votre implémentation ici
}

// Test attendu
console.log(triInsertionDescendant([5, 2, 4, 6, 1, 3]));
// [6, 5, 4, 3, 2, 1]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri par insertion descendant (du plus grand au plus petit)
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié en ordre décroissant
 */
function triInsertionDescendant(tableau) {
  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];
    let j = i - 1;

    // Inverser la condition : décaler les éléments PLUS PETITS
    while (j >= 0 && tableau[j] < valeurCourante) {
      tableau[j + 1] = tableau[j];
      j--;
    }

    tableau[j + 1] = valeurCourante;
  }

  return tableau;
}

// Tests
console.log(triInsertionDescendant([5, 2, 4, 6, 1, 3]));
// [6, 5, 4, 3, 2, 1]

console.log(triInsertionDescendant([10, 8, 20, 15, 7]));
// [20, 15, 10, 8, 7]
```

**Explication :**

La seule modification est d'inverser la condition de comparaison dans la boucle while :

- **Ascendant** : `tableau[j] > valeurCourante` (décaler les plus grands)
- **Descendant** : `tableau[j] < valeurCourante` (décaler les plus petits)

</details>

---

## 📊 Analyse de Complexité

Comprendre la complexité du tri par insertion révèle ses forces uniques.

---

### Complexité Temporelle

| Cas              | Complexité | Description                      |
| ---------------- | ---------- | -------------------------------- |
| **Meilleur cas** | O(n)       | Tableau déjà trié                |
| **Cas moyen**    | O(n²)      | Éléments dans un ordre aléatoire |
| **Pire cas**     | O(n²)      | Tableau trié en ordre inverse    |

**Pourquoi O(n) dans le meilleur cas ?**

```javascript
// Tableau déjà trié : [1, 2, 3, 4, 5]
// À chaque itération :
// - On compare l'élément courant avec le dernier élément trié
// - La condition tableau[j] > valeurCourante est FAUSSE
// - La boucle while ne s'exécute jamais
// - Une seule comparaison par élément = O(n)
```

**Pourquoi O(n²) dans le pire cas ?**

```javascript
// Tableau inversé : [5, 4, 3, 2, 1]
// Pour insérer chaque élément :
// - On doit décaler TOUS les éléments déjà triés
// - Itération 1 : 1 décalage
// - Itération 2 : 2 décalages
// - Itération 3 : 3 décalages
// - ...
// Total = 1 + 2 + 3 + ... + (n-1) = n(n-1)/2 = O(n²)
```

---

### Complexité Spatiale

| Aspect            | Complexité |
| ----------------- | ---------- |
| Espace auxiliaire | O(1)       |

Le tri par insertion est **en place** : il n'utilise qu'une variable temporaire (`valeurCourante`) quelle que soit la taille du tableau.

---

### L'Adaptativité : La Force Unique

Le tri par insertion est **adaptatif** : sa performance s'améliore avec le degré de tri initial des données.

```javascript
// Mesure du nombre de décalages selon l'état initial
function triInsertionAvecStats(tableau) {
  let comparaisons = 0;
  let decalages = 0;

  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];
    let j = i - 1;

    while (j >= 0 && tableau[j] > valeurCourante) {
      comparaisons++;
      tableau[j + 1] = tableau[j];
      decalages++;
      j--;
    }
    comparaisons++; // La comparaison qui a arrêté la boucle

    tableau[j + 1] = valeurCourante;
  }

  return { tableau, comparaisons, decalages };
}

// Tests
console.log("Tableau trié:", triInsertionAvecStats([1, 2, 3, 4, 5]));
// { comparaisons: 4, decalages: 0 }

console.log("Presque trié:", triInsertionAvecStats([1, 2, 4, 3, 5]));
// { comparaisons: 5, decalages: 1 }

console.log("Inversé:", triInsertionAvecStats([5, 4, 3, 2, 1]));
// { comparaisons: 14, decalages: 10 }
```

---

## 🔄 Comparaison des Trois Algorithmes Élémentaires

| Critère          | Tri à Bulles | Tri par Sélection | Tri par Insertion |
| ---------------- | ------------ | ----------------- | ----------------- |
| **Meilleur cas** | O(n)\*       | O(n²)             | O(n)              |
| **Cas moyen**    | O(n²)        | O(n²)             | O(n²)             |
| **Pire cas**     | O(n²)        | O(n²)             | O(n²)             |
| **Espace**       | O(1)         | O(1)              | O(1)              |
| **Stabilité**    | Stable       | Instable          | Stable            |
| **Adaptatif**    | Oui\*        | Non               | Oui               |
| **Échanges**     | O(n²)        | O(n)              | O(n²) décalages   |
| **Cas d'usage**  | Pédagogie    | Écriture coûteuse | Presque trié      |

\*Avec optimisation (drapeau swapped)

> **Point Clé**
>
> Le tri par insertion est généralement le meilleur choix parmi les trois algorithmes élémentaires pour les données du monde réel, car celles-ci sont souvent **partiellement ordonnées**. C'est pourquoi il est utilisé dans les algorithmes hybrides modernes.

---

## 📝 Micro-Exercice #3 : Tri de Chaînes de Caractères

**Objectif :** Adapter le tri par insertion pour les chaînes.

**Instructions :** Triez alphabétiquement un tableau de mots.

```javascript
function triInsertionChaines(tableau) {
  // Votre implémentation ici
}

// Test
const mots = ["banane", "pomme", "cherry", "date"];
console.log(triInsertionChaines(mots));
// ["pomme", "banane", "cherry", "date"]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri par insertion pour chaînes de caractères
 * @param {string[]} tableau - Le tableau de chaînes à trier
 * @returns {string[]} - Le tableau trié alphabétiquement
 */
function triInsertionChaines(tableau) {
  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];
    let j = i - 1;

    // Utiliser localeCompare pour une comparaison correcte
    while (j >= 0 && tableau[j].localeCompare(valeurCourante) > 0) {
      tableau[j + 1] = tableau[j];
      j--;
    }

    tableau[j + 1] = valeurCourante;
  }

  return tableau;
}

// Tests
const mots = ["banane", "pomme", "cherry", "date"];
console.log(triInsertionChaines([...mots]));
// ["pomme", "banane", "cherry", "date"]

const prenoms = ["Destinée", "Sing", "Chermann", "Prudence"];
console.log(triInsertionChaines([...prenoms]));
// ["Chermann", "Destinée", "Prudence", "Sing"]
```

**Explication :**

- `localeCompare()` retourne un nombre négatif si la première chaîne vient avant, positif si après
- La condition `localeCompare() > 0` signifie que `tableau[j]` vient après `valeurCourante` alphabétiquement
- Cette méthode gère correctement les accents et caractères spéciaux

</details>

---

## 💻 Application Pratique : Cas d'Utilisation Réels

Le tri par insertion brille dans des scénarios spécifiques où ses caractéristiques sont avantageuses.

---

### Exemple 1 : Maintenir une Liste Triée en Temps Réel

Imaginez un système de classement où de nouveaux scores arrivent en continu :

```javascript
/**
 * Classe pour maintenir un classement trié en temps réel
 */
class Classement {
  constructor() {
    this.scores = [];
  }

  /**
   * Ajoute un nouveau score en maintenant l'ordre
   * Utilise le principe du tri par insertion
   * @param {Object} entree - { joueur: string, score: number }
   */
  ajouterScore(entree) {
    // Si la liste est vide, simplement ajouter
    if (this.scores.length === 0) {
      this.scores.push(entree);
      return;
    }

    // Trouver la position d'insertion (tri descendant par score)
    let position = this.scores.length;
    for (let i = this.scores.length - 1; i >= 0; i--) {
      if (this.scores[i].score >= entree.score) {
        position = i + 1;
        break;
      }
      if (i === 0) {
        position = 0;
      }
    }

    // Insérer à la position trouvée
    this.scores.splice(position, 0, entree);
  }

  afficher() {
    console.log("Classement:");
    this.scores.forEach((e, i) => {
      console.log(`  ${i + 1}. ${e.joueur}: ${e.score} pts`);
    });
  }
}

// Simulation
const leaderboard = new Classement();
leaderboard.ajouterScore({ joueur: "Chermann", score: 1500 });
leaderboard.ajouterScore({ joueur: "Prudence", score: 2200 });
leaderboard.ajouterScore({ joueur: "Germain", score: 1800 });
leaderboard.ajouterScore({ joueur: "Ingrid", score: 1950 });
leaderboard.ajouterScore({ joueur: "Sing", score: 2100 });

leaderboard.afficher();
// Classement:
//   1. Prudence: 2200 pts
//   2. Sing: 2100 pts
//   3. Ingrid: 1950 pts
//   4. Germain: 1800 pts
//   5. Chermann: 1500 pts
```

---

### Exemple 2 : Tri de Petits Tableaux

Les algorithmes hybrides modernes utilisent le tri par insertion pour les petites partitions :

```javascript
/**
 * Fonction utilitaire qui choisit l'algorithme selon la taille
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triAdaptatif(tableau) {
  const SEUIL = 10; // Seuil typique pour utiliser insertion sort

  if (tableau.length <= SEUIL) {
    console.log(`Tableau de ${tableau.length} éléments → Tri par insertion`);
    return triInsertion([...tableau]);
  } else {
    console.log(`Tableau de ${tableau.length} éléments → Algorithme avancé`);
    // Ici on utiliserait Merge Sort ou Quick Sort
    // Pour l'exemple, on utilise sort() natif
    return [...tableau].sort((a, b) => a - b);
  }
}

// Fonction tri par insertion
function triInsertion(tableau) {
  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];
    let j = i - 1;
    while (j >= 0 && tableau[j] > valeurCourante) {
      tableau[j + 1] = tableau[j];
      j--;
    }
    tableau[j + 1] = valeurCourante;
  }
  return tableau;
}

// Tests
console.log(triAdaptatif([5, 2, 8, 1, 9]));
// Tableau de 5 éléments → Tri par insertion

console.log(triAdaptatif([5, 2, 8, 1, 9, 3, 7, 4, 6, 10, 11, 12, 15, 13, 14]));
// Tableau de 15 éléments → Algorithme avancé
```

---

### Exemple 3 : Tri de Tâches avec Priorité et Insertion

```javascript
/**
 * Gestionnaire de tâches avec insertion triée par priorité
 */
class GestionnaireTaches {
  constructor() {
    this.taches = [];
  }

  /**
   * Ajoute une tâche en maintenant l'ordre par priorité
   * @param {Object} tache - { titre: string, priorite: number }
   */
  ajouterTache(tache) {
    // Insertion triée par priorité (1 = urgente)
    let j = this.taches.length - 1;

    while (j >= 0 && this.taches[j].priorite > tache.priorite) {
      j--;
    }

    // Insérer après l'élément trouvé
    this.taches.splice(j + 1, 0, tache);
  }

  afficher() {
    console.log("📋 Liste des tâches:");
    this.taches.forEach((t) => {
      const emoji = t.priorite === 1 ? "🔴" : t.priorite === 2 ? "🟡" : "🟢";
      console.log(`  ${emoji} [P${t.priorite}] ${t.titre}`);
    });
  }
}

// Utilisation
const gestionnaire = new GestionnaireTaches();
gestionnaire.ajouterTache({ titre: "Écrire documentation", priorite: 3 });
gestionnaire.ajouterTache({ titre: "Corriger bug critique", priorite: 1 });
gestionnaire.ajouterTache({ titre: "Review code", priorite: 2 });
gestionnaire.ajouterTache({ titre: "Mettre à jour dépendances", priorite: 3 });
gestionnaire.ajouterTache({ titre: "Déployer en production", priorite: 1 });

gestionnaire.afficher();
// 📋 Liste des tâches:
//   🔴 [P1] Corriger bug critique
//   🔴 [P1] Déployer en production
//   🟡 [P2] Review code
//   🟢 [P3] Écrire documentation
//   🟢 [P3] Mettre à jour dépendances
```

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension du tri par insertion, implémentez les problèmes suivants.

---

### Exercice 1 : Afficher les Étapes d'Insertion

**Objectif :** Visualiser le processus de tri.

**Instructions :** Implémentez une fonction qui affiche l'état du tableau après chaque insertion.

```javascript
function triInsertionAvecEtapes(tableau) {
  // Votre implémentation ici
}

// Test avec [12, 11, 13, 5, 6]
// Sortie attendue :
// Array after inserting 11: [11, 12, 13, 5, 6]
// Array after inserting 13: [11, 12, 13, 5, 6]
// Array after inserting 5: [5, 11, 12, 13, 6]
// Array after inserting 6: [5, 6, 11, 12, 13]
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Tri par insertion avec affichage des étapes
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triInsertionAvecEtapes(tableau) {
  console.log(`État initial: [${tableau.join(", ")}]`);

  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];
    let j = i - 1;

    while (j >= 0 && tableau[j] > valeurCourante) {
      tableau[j + 1] = tableau[j];
      j--;
    }

    tableau[j + 1] = valeurCourante;
    console.log(
      `Après insertion de ${valeurCourante}: [${tableau.join(", ")}]`,
    );
  }

  console.log(`\nTableau final: [${tableau.join(", ")}]`);
  return tableau;
}

// Test
triInsertionAvecEtapes([12, 11, 13, 5, 6]);
// État initial: [12, 11, 13, 5, 6]
// Après insertion de 11: [11, 12, 13, 5, 6]
// Après insertion de 13: [11, 12, 13, 5, 6]
// Après insertion de 5: [5, 11, 12, 13, 6]
// Après insertion de 6: [5, 6, 11, 12, 13]
// Tableau final: [5, 6, 11, 12, 13]
```

</details>

---

### Exercice 2 : Tri d'Objets par Propriété

**Objectif :** Trier des objets complexes.

**Instructions :** Triez une liste d'étudiants par note (décroissant), puis par nom (alphabétique) en cas d'égalité.

```javascript
const etudiants = [
  { nom: "Chermann", note: 85 },
  { nom: "Prudence", note: 92 },
  { nom: "Germain", note: 85 },
  { nom: "Ingrid", note: 92 },
  { nom: "Sing", note: 78 },
];

function trierEtudiants(etudiants) {
  // Votre implémentation ici
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trie les étudiants par note (desc) puis par nom (asc)
 * @param {Array} etudiants - Liste des étudiants
 * @returns {Array} - Liste triée
 */
function trierEtudiants(etudiants) {
  // Fonction de comparaison : retourne true si a doit venir après b
  function doitDecaler(a, b) {
    // D'abord comparer par note (descendant)
    if (a.note !== b.note) {
      return a.note > b.note; // Plus grande note = plus prioritaire
    }
    // Si notes égales, comparer par nom (ascendant)
    return a.nom.localeCompare(b.nom) < 0;
  }

  for (let i = 1; i < etudiants.length; i++) {
    const valeurCourante = etudiants[i];
    let j = i - 1;

    while (j >= 0 && doitDecaler(valeurCourante, etudiants[j])) {
      etudiants[j + 1] = etudiants[j];
      j--;
    }

    etudiants[j + 1] = valeurCourante;
  }

  return etudiants;
}

// Test
const etudiants = [
  { nom: "Chermann", note: 85 },
  { nom: "Prudence", note: 92 },
  { nom: "Germain", note: 85 },
  { nom: "Ingrid", note: 92 },
  { nom: "Sing", note: 78 },
];

trierEtudiants(etudiants);

console.log("Étudiants triés:");
etudiants.forEach((e) => console.log(`  ${e.nom}: ${e.note}`));
// Ingrid: 92 (I avant P alphabétiquement)
// Prudence: 92
// Chermann: 85 (C avant G alphabétiquement)
// Germain: 85
// Sing: 78
```

**Explication :**

- Le tri est **stable**, donc pour les notes égales, on utilise une comparaison secondaire par nom
- La fonction `doitDecaler` retourne true si `valeurCourante` doit être placé avant l'élément comparé

</details>

---

### Exercice 3 : Compter les Inversions

**Objectif :** Mesurer le "désordre" d'un tableau.

**Instructions :** Une **inversion** est une paire (i, j) où i < j mais tableau[i] > tableau[j]. Le nombre d'inversions correspond au nombre de décalages effectués par le tri par insertion.

```javascript
function compterInversions(tableau) {
  // Votre implémentation ici
  // Retourner le nombre d'inversions
}

// Tests
console.log(compterInversions([1, 2, 3, 4, 5])); // 0 (trié)
console.log(compterInversions([5, 4, 3, 2, 1])); // 10 (inversé)
console.log(compterInversions([2, 4, 1, 3, 5])); // 3
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Compte le nombre d'inversions dans un tableau
 * @param {number[]} tableau - Le tableau à analyser
 * @returns {number} - Nombre d'inversions
 */
function compterInversions(tableau) {
  const copie = [...tableau]; // Ne pas modifier l'original
  let inversions = 0;

  for (let i = 1; i < copie.length; i++) {
    const valeurCourante = copie[i];
    let j = i - 1;

    while (j >= 0 && copie[j] > valeurCourante) {
      copie[j + 1] = copie[j];
      inversions++; // Chaque décalage = une inversion
      j--;
    }

    copie[j + 1] = valeurCourante;
  }

  return inversions;
}

// Tests
console.log(compterInversions([1, 2, 3, 4, 5])); // 0
console.log(compterInversions([5, 4, 3, 2, 1])); // 10
console.log(compterInversions([2, 4, 1, 3, 5])); // 3

// Détail pour [2, 4, 1, 3, 5] :
// Inversions : (2,1), (4,1), (4,3) → 3 inversions
```

**Explication :**

Le nombre de décalages dans le tri par insertion est exactement égal au nombre d'inversions dans le tableau original. C'est pourquoi :

- Un tableau trié a 0 inversions → O(n) comparaisons
- Un tableau inversé a n(n-1)/2 inversions → O(n²) comparaisons

</details>

---

### Exercice 4 : Tri par Insertion Binaire

**Objectif :** Optimiser la recherche de position avec la recherche binaire.

**Instructions :** La partie triée est... triée ! On peut utiliser la recherche binaire pour trouver la position d'insertion plus rapidement.

```javascript
function triInsertionBinaire(tableau) {
  // Votre implémentation ici
  // Utiliser la recherche binaire pour trouver la position
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recherche binaire pour trouver la position d'insertion
 * @param {number[]} tableau - Le sous-tableau trié
 * @param {number} valeur - La valeur à insérer
 * @param {number} fin - L'index de fin (exclusif)
 * @returns {number} - L'index où insérer la valeur
 */
function trouverPositionBinaire(tableau, valeur, fin) {
  let debut = 0;

  while (debut < fin) {
    const milieu = Math.floor((debut + fin) / 2);

    if (tableau[milieu] <= valeur) {
      debut = milieu + 1;
    } else {
      fin = milieu;
    }
  }

  return debut;
}

/**
 * Tri par insertion avec recherche binaire
 * @param {number[]} tableau - Le tableau à trier
 * @returns {number[]} - Le tableau trié
 */
function triInsertionBinaire(tableau) {
  for (let i = 1; i < tableau.length; i++) {
    const valeurCourante = tableau[i];

    // Trouver la position avec recherche binaire
    const position = trouverPositionBinaire(tableau, valeurCourante, i);

    // Décaler les éléments
    for (let j = i; j > position; j--) {
      tableau[j] = tableau[j - 1];
    }

    // Insérer
    tableau[position] = valeurCourante;
  }

  return tableau;
}

// Tests
console.log(triInsertionBinaire([5, 2, 4, 6, 1, 3]));
// [1, 2, 3, 4, 5, 6]

console.log(triInsertionBinaire([64, 25, 12, 22, 11]));
// [11, 12, 22, 25, 64]
```

**Explication :**

- La recherche binaire réduit les comparaisons de O(n) à O(log n) par élément
- Cependant, le nombre de décalages reste O(n) par élément
- La complexité totale reste O(n²), mais avec moins de comparaisons
- Utile quand les comparaisons sont coûteuses (ex: objets complexes)

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle métaphore illustre le mieux le tri par insertion ?**

- [ ] A. Des bulles qui remontent dans l'eau
- [ ] B. Choisir le meilleur joueur à chaque tour
- [ ] C. Trier une main de cartes en insérant chaque nouvelle carte à sa place
- [ ] D. Diviser un problème en sous-problèmes

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le tri par insertion fonctionne exactement comme le tri naturel d'une main de cartes : on prend chaque nouvelle carte et on l'insère à sa position correcte parmi les cartes déjà triées.

</details>

---

### Question 2

**Quelle est la complexité temporelle du tri par insertion dans le meilleur cas ?**

- [ ] A. O(n²)
- [ ] B. O(n log n)
- [ ] C. O(n)
- [ ] D. O(1)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Dans le meilleur cas (tableau déjà trié), chaque élément est comparé une seule fois avec son prédécesseur, et aucun décalage n'est nécessaire. La complexité est donc O(n).

</details>

---

### Question 3

**Qu'est-ce qui différencie le tri par insertion du tri à bulles et du tri par sélection ?**

- [ ] A. Il utilise des échanges au lieu de décalages
- [ ] B. Il est adaptatif : sa performance dépend du degré de tri initial
- [ ] C. Il est instable
- [ ] D. Il nécessite plus de mémoire

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri par insertion est adaptatif : sur un tableau presque trié, il est proche de O(n), tandis que sur un tableau inversé, il est O(n²). Le tri par sélection fait toujours le même nombre de comparaisons.

</details>

---

### Question 4

**Le tri par insertion est-il un algorithme stable ?**

- [ ] A. Non, car il utilise des décalages
- [ ] B. Oui, car il n'échange jamais deux éléments égaux
- [ ] C. Ça dépend de l'implémentation
- [ ] D. La stabilité n'est pas applicable ici

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri par insertion est stable. Lors de l'insertion, un élément est placé **après** tous les éléments égaux déjà triés (grâce à la condition `tableau[j] > valeurCourante` et non `>=`), préservant ainsi l'ordre relatif des éléments égaux.

</details>

---

### Question 5

**Pourquoi le tri par insertion est-il préféré pour les petits tableaux dans les algorithmes hybrides ?**

- [ ] A. Car il a une meilleure complexité asymptotique
- [ ] B. Car il a moins d'overhead et de constantes que les algorithmes récursifs
- [ ] C. Car il utilise moins de mémoire
- [ ] D. Car il est plus facile à implémenter

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Pour les petits tableaux, les constantes et l'overhead des algorithmes récursifs (comme Merge Sort ou Quick Sort) dominent. Le tri par insertion, avec sa simplicité, est plus rapide en pratique pour les tableaux de moins de 10-20 éléments.

</details>

---

### Question 6

**Que se passe-t-il quand on insère un élément qui est déjà à sa bonne place ?**

- [ ] A. L'algorithme effectue quand même tous les décalages
- [ ] B. La boucle while ne s'exécute pas, aucun décalage n'est fait
- [ ] C. L'élément est supprimé puis réinséré
- [ ] D. Une erreur se produit

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Si l'élément à insérer est plus grand que tous les éléments de la partie triée, la condition `tableau[j] > valeurCourante` est immédiatement fausse, et la boucle while ne s'exécute jamais. L'élément reste à sa place sans aucun décalage.

</details>

---

### Question 7

**Combien de décalages sont nécessaires pour trier le tableau [5, 4, 3, 2, 1] par insertion ?**

- [ ] A. 4
- [ ] B. 5
- [ ] C. 10
- [ ] D. 20

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Pour un tableau inversé de n éléments, le nombre de décalages est n(n-1)/2 :

- Insérer 4 : 1 décalage
- Insérer 3 : 2 décalages
- Insérer 2 : 3 décalages
- Insérer 1 : 4 décalages

Total : 1 + 2 + 3 + 4 = 10 décalages

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Concept Fondamental

Le tri par insertion construit le tableau trié un élément à la fois, en insérant chaque élément à sa position correcte dans la partie déjà triée, comme le tri d'une main de cartes.

### 2. Mécanisme de Décalage

Contrairement aux échanges, le tri par insertion utilise des décalages : les éléments plus grands sont déplacés vers la droite pour faire place à l'élément à insérer.

### 3. Adaptativité

Le tri par insertion est adaptatif : O(n) pour un tableau trié, O(n²) pour un tableau inversé. Sa performance s'améliore avec le degré de tri initial des données.

### 4. Stabilité

Le tri par insertion est stable : il préserve l'ordre relatif des éléments égaux, ce qui est important pour les tris multi-critères.

### 5. Cas d'Utilisation Idéaux

- Petits tableaux (< 10-20 éléments)
- Données presque triées
- Insertion en temps réel dans une liste triée
- Partie des algorithmes hybrides (Timsort)

### 6. Complexité

- **Temps** : O(n) meilleur, O(n²) moyen/pire
- **Espace** : O(1) - en place

### 7. Comparaison

Parmi les trois algorithmes élémentaires, le tri par insertion est généralement le meilleur choix pour les données du monde réel car il combine stabilité, adaptativité et efficacité sur les petits tableaux.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maîtrisé le tri par insertion, complétant ainsi votre tour d'horizon des algorithmes de tri élémentaires.

### Ce que vous avez appris aujourd'hui

- Le concept du tri par insertion et sa métaphore du tri de cartes
- Le mécanisme de décalage et sa différence avec les échanges
- L'adaptativité unique de cet algorithme
- L'implémentation en JavaScript et ses variantes
- Les cas d'utilisation réels où il excelle

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter le tri par insertion pour différents types de données
- Choisir le bon algorithme élémentaire selon le contexte
- Maintenir une liste triée en temps réel avec insertion efficace

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Avec le tri à bulles, le tri par sélection et le tri par insertion, vous maîtrisez maintenant les trois algorithmes de tri élémentaires. La prochaine étape sera de découvrir des algorithmes plus efficaces qui utilisent des paradigmes différents, comme le **Divide and Conquer** avec le Tri Fusion (Merge Sort).

---

## ➡️ Prochaine Étape : Leçon 17

### Ce qui vous attend

La prochaine leçon, **« Tri Fusion (Merge Sort) : Diviser pour Régner »**, vous introduira à un paradigme de conception d'algorithmes puissant.

**Vous découvrirez :**

- Le paradigme "Diviser pour Régner" (Divide and Conquer)
- Un algorithme avec une complexité garantie de O(n log n)
- La récursivité appliquée au tri
- Le compromis espace/temps avec ce nouvel algorithme

### Préparez-vous !

Le Tri Fusion représente un saut conceptuel : au lieu de trier élément par élément, il divise le problème en sous-problèmes plus petits. C'est une technique fondamentale que vous retrouverez dans de nombreux algorithmes avancés.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Insertion Sort](https://visualgo.net/en/sorting) - Visualisation interactive
- [GeeksforGeeks - Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/) - Tutoriel détaillé
- [Sorting Algorithms Visualized](https://www.toptal.com/developers/sorting-algorithms/insertion-sort) - Comparaison visuelle

### Outils de pratique

- **[JS Bin](https://jsbin.com/)** : Testez vos implémentations en ligne
- **[Python Tutor (JavaScript)](https://pythontutor.com/javascript.html)** : Visualisez l'exécution pas à pas

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour vraiment comprendre le tri par insertion, prenez un jeu de cartes et triez-le en appliquant consciemment l'algorithme. Observez comment vous cherchez la position d'insertion et comment vous décalez les cartes pour faire de la place. C'est exactement ce que fait l'algorithme !

---

**Prêt pour la Leçon 17 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir le paradigme "Diviser pour Régner" avec le Tri Fusion !

---

<div align="center">

**Leçon 16 sur 42 - Module 3 : Techniques de Tri Essentielles**

[⬅️ Leçon 15 : Tri par Sélection : Concept et Implémentation JavaScript de Base](./lecon-3-tri-selection-concept-implementation-javascript-base.md) | [Retour au sommaire](./README.md) | [Leçon 17 : Tri Fusion (Merge Sort) : Stratégie Diviser pour Régner en JavaScript ➡️](./lecon-5-tri-fusion-strategie-diviser-regner-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
