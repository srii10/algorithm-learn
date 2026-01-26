##### Leçon 29 sur 42

# Algorithme de Parcours en Largeur (BFS) en JavaScript

**Module 5** : Arbres et Parcours de Graphes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **principe du BFS** (exploration niveau par niveau)
- Utiliser une **file (queue)** pour implémenter le BFS
- Implémenter le **parcours BFS** complet en JavaScript
- Trouver le **chemin le plus court** dans un graphe non pondéré
- Analyser la **complexité** temporelle O(V + E) et spatiale O(V)
- Appliquer le BFS à des **problèmes réels**

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 28 complétée** : Implémentations des graphes (Liste d'adjacence)
- **Module 2** : Files (Queues) et principe FIFO
- **Set JavaScript** : Utiliser Set pour le suivi des visites
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Explorer Niveau par Niveau

Imaginez que vous cherchez quelqu'un dans un immeuble. Deux stratégies s'offrent à vous :

1. **Explorer étage par étage** (BFS) : Vérifier toutes les portes du rez-de-chaussée, puis toutes celles du 1er étage, puis du 2ème...
2. **Explorer escalier par escalier** (DFS) : Monter directement au dernier étage par un escalier, puis redescendre et essayer un autre escalier...

Le **BFS (Breadth-First Search)** utilise la première stratégie : il explore tous les voisins d'un niveau avant de passer au niveau suivant.

> **Point Clé**
>
> Le BFS garantit de trouver le **chemin le plus court** (en nombre d'arêtes) dans un graphe non pondéré. C'est parce qu'il explore tous les chemins de longueur 1 avant ceux de longueur 2, et ainsi de suite.

---

## 📦 Principe du BFS : La File (Queue)

Le BFS utilise une **file** (queue) pour gérer l'ordre de visite des sommets.

---

### Rappel : Structure FIFO

Une **file** suit le principe **FIFO** (First In, First Out) :

- Le premier élément ajouté est le premier retiré
- Comme une file d'attente au supermarché !

```
File :  [A] [B] [C] [D]
         ↑           ↑
      Premier    Dernier
      sorti      ajouté

Opérations :
- enqueue(E) → [A] [B] [C] [D] [E]  (ajouter à la fin)
- dequeue()  → [B] [C] [D] [E]     (retirer du début, retourne A)
```

---

### Algorithme BFS Pas à Pas

```
1. INITIALISATION :
   - Créer une file vide
   - Créer un ensemble "visités" vide
   - Ajouter le sommet de départ à la file
   - Marquer le sommet de départ comme visité

2. EXPLORATION (tant que la file n'est pas vide) :
   a. Retirer le premier élément de la file (dequeue)
   b. Traiter ce sommet (l'afficher, l'ajouter au résultat...)
   c. Pour chaque voisin non visité :
      - Le marquer comme visité
      - L'ajouter à la file (enqueue)

3. TERMINAISON :
   - La file est vide = tous les sommets accessibles ont été visités
```

---

### Visualisation : BFS sur un Graphe Simple

```
Graphe :
        [A]
       /   \
     [B]   [C]
     / \     \
   [D] [E]   [F]
         \   /
          [G]

BFS depuis A :

Étape 0 : File = [A], Visités = {A}
          → Retirer A, ajouter ses voisins B et C

Étape 1 : File = [B, C], Visités = {A, B, C}
          → Retirer B, ajouter ses voisins D et E

Étape 2 : File = [C, D, E], Visités = {A, B, C, D, E}
          → Retirer C, ajouter son voisin F

Étape 3 : File = [D, E, F], Visités = {A, B, C, D, E, F}
          → Retirer D (pas de nouveaux voisins)

Étape 4 : File = [E, F], Visités = {A, B, C, D, E, F}
          → Retirer E, ajouter G

Étape 5 : File = [F, G], Visités = {A, B, C, D, E, F, G}
          → Retirer F (G déjà visité)

Étape 6 : File = [G], Visités = {A, B, C, D, E, F, G}
          → Retirer G (pas de nouveaux voisins)

Étape 7 : File = [], TERMINÉ !

Ordre de visite : A → B → C → D → E → F → G
                  Niveau 0 → Niveau 1 → Niveau 2 → Niveau 3
```

---

## 💻 Implémentation du BFS en JavaScript

Implémentons le BFS avec notre classe `GrapheListeAdjacence` de la leçon précédente.

---

### Représentation du Graphe (Liste d'Adjacence)

```javascript
// Graphe simple représenté comme un objet
const graphe = {
  A: ["B", "C"],
  B: ["A", "D", "E"],
  C: ["A", "F"],
  D: ["B"],
  E: ["B", "F"],
  F: ["C", "E"],
};

// Visualisation :
//       [A]
//      /   \
//    [B]   [C]
//    / \     \
//  [D] [E]---[F]
```

---

### Fonction BFS Basique

```javascript
/**
 * Effectue un parcours en largeur (BFS) sur un graphe.
 * @param {Object} graphe - Le graphe représenté en liste d'adjacence.
 * @param {string} depart - Le sommet de départ.
 * @returns {string[]} - L'ordre de visite des sommets.
 */
function parcoursBFS(graphe, depart) {
  // Vérifier que le sommet de départ existe
  if (!graphe[depart]) {
    console.error(`Le sommet "${depart}" n'existe pas dans le graphe.`);
    return [];
  }

  const file = [depart]; // File initialisée avec le départ
  const visites = new Set(); // Ensemble des sommets visités
  const resultat = []; // Ordre de visite

  visites.add(depart); // Marquer le départ comme visité

  while (file.length > 0) {
    // Retirer le premier élément de la file (FIFO)
    const sommetActuel = file.shift();

    // Traiter le sommet (l'ajouter au résultat)
    resultat.push(sommetActuel);

    // Parcourir tous les voisins
    const voisins = graphe[sommetActuel] || [];

    for (const voisin of voisins) {
      // Si le voisin n'a pas encore été visité
      if (!visites.has(voisin)) {
        visites.add(voisin); // Le marquer comme visité
        file.push(voisin); // L'ajouter à la file
      }
    }
  }

  return resultat;
}

// Test
const grapheSimple = {
  A: ["B", "C"],
  B: ["A", "D", "E"],
  C: ["A", "F"],
  D: ["B"],
  E: ["B", "F"],
  F: ["C", "E"],
};

console.log("BFS depuis A :", parcoursBFS(grapheSimple, "A"));
// ['A', 'B', 'C', 'D', 'E', 'F']

console.log("BFS depuis D :", parcoursBFS(grapheSimple, "D"));
// ['D', 'B', 'A', 'E', 'C', 'F']
```

---

### Explication du Code

| Ligne                       | Explication                                           |
| --------------------------- | ----------------------------------------------------- |
| `const file = [depart]`     | Initialise la file avec le sommet de départ           |
| `const visites = new Set()` | Set pour vérifier en O(1) si un sommet est visité     |
| `file.shift()`              | Retire et retourne le **premier** élément (FIFO)      |
| `visites.add(voisin)`       | Marque AVANT d'ajouter à la file (évite les doublons) |
| `file.push(voisin)`         | Ajoute à la **fin** de la file                        |

> **Attention**
>
> On marque un sommet comme visité **avant** de l'ajouter à la file, pas quand on le retire. Cela évite d'ajouter le même sommet plusieurs fois à la file.

---

## 📝 Micro-Exercice #1 : Tracer un BFS

**Objectif :** Comprendre l'ordre de visite du BFS.

**Instructions :** Tracez manuellement le BFS sur ce graphe en partant de 'X' :

```javascript
const graphe = {
  X: ["Y", "Z"],
  Y: ["X", "W"],
  Z: ["X", "W"],
  W: ["Y", "Z"],
};
```

<details>
<summary>💡 Voir la solution</summary>

```
Étape 0 : File = [X], Visités = {X}
          → Retirer X, ajouter Y et Z

Étape 1 : File = [Y, Z], Visités = {X, Y, Z}
          → Retirer Y, ajouter W

Étape 2 : File = [Z, W], Visités = {X, Y, Z, W}
          → Retirer Z (W déjà visité)

Étape 3 : File = [W], Visités = {X, Y, Z, W}
          → Retirer W (voisins déjà visités)

Étape 4 : File = [], TERMINÉ !

Ordre de visite : X → Y → Z → W
```

</details>

---

## 💻 Trouver le Chemin le Plus Court avec BFS

Le BFS peut être modifié pour trouver le **chemin le plus court** entre deux sommets.

---

### Pourquoi BFS Trouve le Chemin le Plus Court ?

Le BFS explore les sommets **niveau par niveau** :

1. D'abord tous les sommets à distance 1
2. Puis tous les sommets à distance 2
3. Etc.

Donc quand on atteint la destination pour la première fois, c'est forcément par le chemin le plus court !

```
Graphe :          Distances depuis A :
    [A]               A = 0
   /   \              B = 1, C = 1
 [B]   [C]            D = 2, E = 2, F = 2
 / \     \            G = 3
[D][E]---[F]
      \   /
       [G]

Chemin le plus court A → G :
  - A → B → E → G (3 arêtes)
  - A → C → F → G (3 arêtes)

Les deux sont optimaux !
```

---

### Implémentation : Chemin le Plus Court

```javascript
/**
 * Trouve le chemin le plus court entre deux sommets (BFS).
 * @param {Object} graphe - Le graphe en liste d'adjacence.
 * @param {string} depart - Sommet de départ.
 * @param {string} arrivee - Sommet d'arrivée.
 * @returns {string[]|null} - Le chemin ou null si aucun chemin.
 */
function cheminPlusCourtBFS(graphe, depart, arrivee) {
  // Cas trivial : départ = arrivée
  if (depart === arrivee) {
    return [depart];
  }

  // Vérification des sommets
  if (!graphe[depart] || !graphe[arrivee]) {
    return null;
  }

  // La file stocke des CHEMINS, pas juste des sommets
  const file = [[depart]];
  const visites = new Set();
  visites.add(depart);

  while (file.length > 0) {
    // Retirer le premier chemin
    const cheminActuel = file.shift();

    // Le dernier sommet du chemin actuel
    const sommetActuel = cheminActuel[cheminActuel.length - 1];

    // Parcourir les voisins
    const voisins = graphe[sommetActuel] || [];

    for (const voisin of voisins) {
      if (!visites.has(voisin)) {
        // Créer un nouveau chemin en ajoutant le voisin
        const nouveauChemin = [...cheminActuel, voisin];

        // Si on a atteint la destination
        if (voisin === arrivee) {
          return nouveauChemin; // Chemin le plus court trouvé !
        }

        visites.add(voisin);
        file.push(nouveauChemin);
      }
    }
  }

  // Aucun chemin trouvé
  return null;
}

// Tests
const reseauVilles = {
  Bruxelles: ["Anvers", "Gand", "Namur"],
  Anvers: ["Bruxelles", "Gand", "Liège"],
  Gand: ["Bruxelles", "Anvers", "Bruges"],
  Namur: ["Bruxelles", "Liège"],
  Liège: ["Anvers", "Namur"],
  Bruges: ["Gand", "Ostende"],
  Ostende: ["Bruges"],
};

console.log(
  "Bruxelles → Liège :",
  cheminPlusCourtBFS(reseauVilles, "Bruxelles", "Liège"),
);
// ['Bruxelles', 'Anvers', 'Liège'] ou ['Bruxelles', 'Namur', 'Liège']

console.log(
  "Bruxelles → Ostende :",
  cheminPlusCourtBFS(reseauVilles, "Bruxelles", "Ostende"),
);
// ['Bruxelles', 'Gand', 'Bruges', 'Ostende']

console.log(
  "Ostende → Namur :",
  cheminPlusCourtBFS(reseauVilles, "Ostende", "Namur"),
);
// ['Ostende', 'Bruges', 'Gand', 'Bruxelles', 'Namur']
```

---

### Alternative : Utiliser un Map de Prédécesseurs

Une approche plus efficace en mémoire utilise un **Map de prédécesseurs** :

```javascript
/**
 * Trouve le chemin le plus court avec un Map de prédécesseurs.
 * @param {Object} graphe - Le graphe en liste d'adjacence.
 * @param {string} depart - Sommet de départ.
 * @param {string} arrivee - Sommet d'arrivée.
 * @returns {string[]|null} - Le chemin ou null.
 */
function cheminPlusCourtBFS_V2(graphe, depart, arrivee) {
  if (depart === arrivee) return [depart];
  if (!graphe[depart] || !graphe[arrivee]) return null;

  const file = [depart];
  const predecesseur = new Map(); // Stocke : sommet → sommet précédent
  predecesseur.set(depart, null);

  while (file.length > 0) {
    const sommetActuel = file.shift();

    for (const voisin of graphe[sommetActuel] || []) {
      if (!predecesseur.has(voisin)) {
        predecesseur.set(voisin, sommetActuel);

        if (voisin === arrivee) {
          // Reconstruire le chemin en remontant les prédécesseurs
          return reconstruireChemin(predecesseur, depart, arrivee);
        }

        file.push(voisin);
      }
    }
  }

  return null;
}

/**
 * Reconstruit le chemin depuis le Map de prédécesseurs.
 */
function reconstruireChemin(predecesseur, depart, arrivee) {
  const chemin = [];
  let sommet = arrivee;

  while (sommet !== null) {
    chemin.unshift(sommet); // Ajouter au début
    sommet = predecesseur.get(sommet);
  }

  return chemin;
}

// Test
console.log(
  "V2 - Bruxelles → Ostende :",
  cheminPlusCourtBFS_V2(reseauVilles, "Bruxelles", "Ostende"),
);
// ['Bruxelles', 'Gand', 'Bruges', 'Ostende']
```

---

## 📝 Micro-Exercice #2 : Chemin le Plus Court

**Objectif :** Utiliser le BFS pour trouver des chemins.

**Instructions :** Dans le graphe suivant, trouvez le chemin le plus court de 'A' à 'G' :

```javascript
const graphe = {
  A: ["B", "C"],
  B: ["A", "D", "E"],
  C: ["A", "F"],
  D: ["B", "G"],
  E: ["B", "G"],
  F: ["C", "G"],
  G: ["D", "E", "F"],
};
```

<details>
<summary>💡 Voir la solution</summary>

```
Exploration BFS depuis A :

Niveau 0 : A
Niveau 1 : B, C
Niveau 2 : D, E, F (voisins de B et C)
Niveau 3 : G (premier voisin non visité de D, E, ou F)

Chemins possibles de longueur 3 :
- A → B → D → G
- A → B → E → G
- A → C → F → G

Tous ont la même longueur (3 arêtes) = chemin le plus court !

console.log(cheminPlusCourtBFS(graphe, 'A', 'G'));
// ['A', 'B', 'D', 'G'] (selon l'ordre de la liste d'adjacence)
```

</details>

---

## 📊 Analyse de Complexité

Analysons les performances du BFS.

---

### Complexité Temporelle : O(V + E)

| Opération               | Complexité   | Explication                                                   |
| ----------------------- | ------------ | ------------------------------------------------------------- |
| Visite de chaque sommet | O(V)         | Chaque sommet est enfilé/défilé une seule fois                |
| Parcours des arêtes     | O(E)         | Chaque arête est examinée une fois (deux fois si non orienté) |
| **Total**               | **O(V + E)** | Linéaire par rapport à la taille du graphe                    |

---

### Complexité Spatiale : O(V)

| Structure   | Taille max | Explication                                     |
| ----------- | ---------- | ----------------------------------------------- |
| File        | O(V)       | Dans le pire cas, tous les sommets dans la file |
| Set visités | O(V)       | Stocke tous les sommets visités                 |
| Résultat    | O(V)       | Liste de tous les sommets                       |
| **Total**   | **O(V)**   |                                                 |

---

### Cas Particuliers

```
Graphe "ÉTOILE" (pire cas pour la file) :
      [B]
       |
[C]--[A]--[D]
       |
      [E]

BFS depuis A :
File = [A] → [B, C, D, E] (tous les voisins ajoutés d'un coup)
Taille max de la file = V-1 = O(V)


Graphe "LIGNE" (file reste petite) :
[A]--[B]--[C]--[D]--[E]

BFS depuis A :
File = [A] → [B] → [C] → [D] → [E]
Taille max de la file = 1 ou 2
```

---

## 📝 Micro-Exercice #3 : Analyser la Complexité

**Objectif :** Estimer le temps d'exécution du BFS.

**Instructions :** Pour un graphe de 1 000 sommets et 5 000 arêtes, combien d'opérations (approximativement) le BFS effectuera-t-il ?

<details>
<summary>💡 Voir la solution</summary>

```
Complexité : O(V + E)

V = 1 000 sommets
E = 5 000 arêtes

Opérations ≈ V + E = 1 000 + 5 000 = 6 000

C'est très rapide ! Le BFS est efficace pour les graphes de taille moyenne.

Note : Pour un graphe de 1 million de sommets et 10 millions d'arêtes,
ce serait environ 11 millions d'opérations, toujours gérable.
```

</details>

---

## 💼 Application : Étude de Cas - Degrés de Séparation

Utilisons le BFS pour calculer les **degrés de séparation** dans un réseau social.

---

### Scénario

Prudence veut savoir combien de "degrés de séparation" la séparent de ses contacts. Un degré = une connexion directe. Deux degrés = ami d'ami, etc.

C'est le fameux concept des **"six degrés de séparation"** !

---

### Implémentation Complète

```javascript
/**
 * Calcule les degrés de séparation depuis une personne.
 */
class ReseauSocial {
  constructor() {
    this.connexions = {};
  }

  /**
   * Ajoute une amitié bidirectionnelle.
   */
  ajouterAmitie(personne1, personne2) {
    if (!this.connexions[personne1]) {
      this.connexions[personne1] = [];
    }
    if (!this.connexions[personne2]) {
      this.connexions[personne2] = [];
    }
    this.connexions[personne1].push(personne2);
    this.connexions[personne2].push(personne1);
  }

  /**
   * Calcule le degré de séparation entre deux personnes.
   * @returns {number} - Le nombre de degrés, ou -1 si non connectés.
   */
  degresSeparation(personne1, personne2) {
    if (personne1 === personne2) return 0;
    if (!this.connexions[personne1] || !this.connexions[personne2]) {
      return -1;
    }

    const file = [[personne1, 0]]; // [personne, distance]
    const visites = new Set();
    visites.add(personne1);

    while (file.length > 0) {
      const [actuel, distance] = file.shift();

      for (const ami of this.connexions[actuel] || []) {
        if (ami === personne2) {
          return distance + 1;
        }

        if (!visites.has(ami)) {
          visites.add(ami);
          file.push([ami, distance + 1]);
        }
      }
    }

    return -1; // Pas connectés
  }

  /**
   * Trouve toutes les personnes à exactement N degrés.
   */
  personnesADistance(depart, distance) {
    const file = [[depart, 0]];
    const visites = new Set();
    const resultat = [];
    visites.add(depart);

    while (file.length > 0) {
      const [actuel, dist] = file.shift();

      if (dist === distance) {
        resultat.push(actuel);
        continue; // Ne pas explorer plus loin
      }

      for (const ami of this.connexions[actuel] || []) {
        if (!visites.has(ami)) {
          visites.add(ami);
          file.push([ami, dist + 1]);
        }
      }
    }

    return resultat;
  }

  /**
   * Affiche le réseau.
   */
  afficher() {
    console.log("=== Réseau Social ===");
    for (const [personne, amis] of Object.entries(this.connexions)) {
      console.log(`${personne}: [${amis.join(", ")}]`);
    }
  }
}

// Créer le réseau
const reseau = new ReseauSocial();

// Ajouter les connexions
reseau.ajouterAmitie("Chermann", "Ingrid");
reseau.ajouterAmitie("Chermann", "Prudence");
reseau.ajouterAmitie("Ingrid", "Germain");
reseau.ajouterAmitie("Ingrid", "Sarr");
reseau.ajouterAmitie("Prudence", "Sing");
reseau.ajouterAmitie("Germain", "Destinée");
reseau.ajouterAmitie("Sarr", "Marc-Élie");
reseau.ajouterAmitie("Sing", "Marc-Élie");

reseau.afficher();

console.log("\n=== Degrés de Séparation ===");
console.log(
  `Chermann → Ingrid : ${reseau.degresSeparation("Chermann", "Ingrid")} degré(s)`,
);
// 1 (amis directs)

console.log(
  `Chermann → Germain : ${reseau.degresSeparation("Chermann", "Germain")} degré(s)`,
);
// 2 (Chermann → Ingrid → Germain)

console.log(
  `Chermann → Destinée : ${reseau.degresSeparation("Chermann", "Destinée")} degré(s)`,
);
// 3 (Chermann → Ingrid → Germain → Destinée)

console.log(
  `Chermann → Marc-Élie : ${reseau.degresSeparation("Chermann", "Marc-Élie")} degré(s)`,
);
// 3 (Chermann → Ingrid → Sarr → Marc-Élie ou via Prudence)

console.log("\n=== Personnes à Distance 2 de Chermann ===");
console.log(reseau.personnesADistance("Chermann", 2));
// ["Germain", "Sarr", "Sing"]
```

---

### Visualisation du Réseau

```
                [Destinée]
                    |
               [Germain]
                    |
    [Prudence]---[Chermann]---[Ingrid]---[Sarr]
        |                                   |
      [Sing]------------------------[Marc-Élie]

Distances depuis Chermann :
- Distance 0 : Chermann
- Distance 1 : Ingrid, Prudence
- Distance 2 : Germain, Sarr, Sing
- Distance 3 : Destinée, Marc-Élie
```

---

## 🌍 Applications Réelles du BFS

Le BFS est utilisé dans de nombreux domaines.

---

### 1. GPS et Navigation

Trouver le chemin avec le **moins d'intersections** (pas forcément le plus court en distance).

```javascript
// Exemple simplifié de navigation
const intersections = {
  "Place Rogier": ["Gare du Nord", "Place de Brouckère"],
  "Gare du Nord": ["Place Rogier", "Botanique"],
  "Place de Brouckère": ["Place Rogier", "Bourse", "De Brouckère"],
  Botanique: ["Gare du Nord", "Madou"],
  Bourse: ["Place de Brouckère", "Grand-Place"],
  "De Brouckère": ["Place de Brouckère", "Grand-Place"],
  Madou: ["Botanique", "Arts-Loi"],
  "Grand-Place": ["Bourse", "De Brouckère"],
  "Arts-Loi": ["Madou"],
};

console.log(cheminPlusCourtBFS(intersections, "Place Rogier", "Grand-Place"));
// ['Place Rogier', 'Place de Brouckère', 'Bourse', 'Grand-Place']
```

---

### 2. Robots d'Indexation Web (Web Crawlers)

Les moteurs de recherche utilisent le BFS pour explorer les pages web niveau par niveau.

```javascript
// Simulation d'un web crawler
function crawlerBFS(pageDepart, maxPages = 10) {
  const pages = {
    "https://exemple.be": [
      "https://exemple.be/contact",
      "https://exemple.be/produits",
    ],
    "https://exemple.be/contact": [
      "https://exemple.be",
      "https://exemple.be/formulaire",
    ],
    "https://exemple.be/produits": [
      "https://exemple.be",
      "https://exemple.be/produit-1",
    ],
    "https://exemple.be/formulaire": [],
    "https://exemple.be/produit-1": ["https://exemple.be/produits"],
  };

  const file = [pageDepart];
  const indexees = new Set();
  const ordre = [];

  while (file.length > 0 && ordre.length < maxPages) {
    const page = file.shift();

    if (!indexees.has(page)) {
      indexees.add(page);
      ordre.push(page);
      console.log(`Indexation de : ${page}`);

      const liens = pages[page] || [];
      for (const lien of liens) {
        if (!indexees.has(lien)) {
          file.push(lien);
        }
      }
    }
  }

  return ordre;
}

crawlerBFS("https://exemple.be");
```

---

### 3. Diffusion en Réseau (Broadcasting)

Envoyer un message à tous les nœuds d'un réseau.

```javascript
// Simulation de diffusion réseau
function diffuserMessage(reseau, source, message) {
  console.log(`\nDiffusion depuis ${source}: "${message}"`);

  const file = [[source, 0]];
  const recus = new Set();
  recus.add(source);

  while (file.length > 0) {
    const [noeud, hop] = file.shift();
    console.log(`  Hop ${hop}: ${noeud} reçoit le message`);

    for (const voisin of reseau[noeud] || []) {
      if (!recus.has(voisin)) {
        recus.add(voisin);
        file.push([voisin, hop + 1]);
      }
    }
  }

  return recus.size;
}

const reseauOrdinateurs = {
  Serveur: ["PC1", "PC2", "Routeur"],
  PC1: ["Serveur", "Imprimante"],
  PC2: ["Serveur"],
  Routeur: ["Serveur", "PC3", "PC4"],
  PC3: ["Routeur"],
  PC4: ["Routeur"],
  Imprimante: ["PC1"],
};

diffuserMessage(reseauOrdinateurs, "Serveur", "Mise à jour disponible");
```

---

## 💪 Exercices Pratiques

Consolidez vos connaissances avec ces exercices progressifs.

---

### Exercice 1 : BFS sur un Graphe Déconnecté

**Objectif :** Comprendre le comportement du BFS avec des composantes non connectées.

**Instructions :** Exécutez le BFS depuis 'A' sur ce graphe. Quels sommets seront visités ?

```javascript
const grapheDeconnecte = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A"],
  D: ["B"],
  X: ["Y"], // Composante séparée
  Y: ["X"],
};
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
console.log(parcoursBFS(grapheDeconnecte, "A"));
// ['A', 'B', 'C', 'D']

// X et Y ne sont PAS visités car ils ne sont pas
// connectés à A. Le BFS ne visite que les sommets
// accessibles depuis le sommet de départ.

// Pour visiter TOUS les sommets d'un graphe déconnecté,
// il faut lancer plusieurs BFS :
function parcoursBFSComplet(graphe) {
  const visites = new Set();
  const resultat = [];

  for (const sommet of Object.keys(graphe)) {
    if (!visites.has(sommet)) {
      const composante = parcoursBFS(graphe, sommet);
      composante.forEach((s) => visites.add(s));
      resultat.push(composante);
    }
  }

  return resultat;
}

console.log(parcoursBFSComplet(grapheDeconnecte));
// [['A', 'B', 'C', 'D'], ['X', 'Y']]
```

</details>

---

### Exercice 2 : Niveau de Chaque Sommet

**Objectif :** Modifier le BFS pour retourner le niveau (distance) de chaque sommet.

**Instructions :** Créez une fonction `niveauxBFS(graphe, depart)` qui retourne un Map avec le niveau de chaque sommet.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function niveauxBFS(graphe, depart) {
  const niveaux = new Map();
  niveaux.set(depart, 0);

  const file = [depart];

  while (file.length > 0) {
    const actuel = file.shift();
    const niveauActuel = niveaux.get(actuel);

    for (const voisin of graphe[actuel] || []) {
      if (!niveaux.has(voisin)) {
        niveaux.set(voisin, niveauActuel + 1);
        file.push(voisin);
      }
    }
  }

  return niveaux;
}

// Test
const graphe = {
  A: ["B", "C"],
  B: ["A", "D", "E"],
  C: ["A", "F"],
  D: ["B"],
  E: ["B", "F"],
  F: ["C", "E"],
};

const niveaux = niveauxBFS(graphe, "A");
console.log("Niveaux depuis A :");
for (const [sommet, niveau] of niveaux) {
  console.log(`  ${sommet}: niveau ${niveau}`);
}
// A: niveau 0
// B: niveau 1
// C: niveau 1
// D: niveau 2
// E: niveau 2
// F: niveau 2
```

</details>

---

### Exercice 3 : Vérifier si un Graphe est Biparti

**Objectif :** Utiliser le BFS pour vérifier si un graphe peut être colorié avec 2 couleurs.

Un graphe est **biparti** si on peut le colorier avec 2 couleurs telles que deux sommets adjacents n'ont jamais la même couleur.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function estBiparti(graphe, depart) {
  const couleurs = new Map();
  couleurs.set(depart, 0); // Couleur 0

  const file = [depart];

  while (file.length > 0) {
    const actuel = file.shift();
    const couleurActuelle = couleurs.get(actuel);
    const couleurOpposee = 1 - couleurActuelle; // 0 → 1, 1 → 0

    for (const voisin of graphe[actuel] || []) {
      if (!couleurs.has(voisin)) {
        couleurs.set(voisin, couleurOpposee);
        file.push(voisin);
      } else if (couleurs.get(voisin) === couleurActuelle) {
        // Conflit de couleur !
        return false;
      }
    }
  }

  return true;
}

// Test - Graphe biparti (carré)
const grapheBiparti = {
  A: ["B", "D"],
  B: ["A", "C"],
  C: ["B", "D"],
  D: ["A", "C"],
};
console.log("Graphe carré biparti ?", estBiparti(grapheBiparti, "A")); // true

// Test - Graphe non biparti (triangle)
const grapheTriangle = {
  X: ["Y", "Z"],
  Y: ["X", "Z"],
  Z: ["X", "Y"],
};
console.log("Triangle biparti ?", estBiparti(grapheTriangle, "X")); // false
```

</details>

---

### Exercice 4 : Plus Court Chemin avec Obstacles

**Objectif :** Adapter le BFS pour une grille avec obstacles.

**Instructions :** Trouvez le plus court chemin dans une grille 5×5 avec des obstacles.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function cheminGrille(grille, depart, arrivee) {
  const [lignes, colonnes] = [grille.length, grille[0].length];
  const directions = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ]; // droite, bas, gauche, haut

  const file = [[depart, [depart]]];
  const visites = new Set();
  visites.add(`${depart[0]},${depart[1]}`);

  while (file.length > 0) {
    const [[x, y], chemin] = file.shift();

    if (x === arrivee[0] && y === arrivee[1]) {
      return chemin;
    }

    for (const [dx, dy] of directions) {
      const nx = x + dx;
      const ny = y + dy;
      const cle = `${nx},${ny}`;

      // Vérifier les limites et les obstacles
      if (
        nx >= 0 &&
        nx < lignes &&
        ny >= 0 &&
        ny < colonnes &&
        grille[nx][ny] === 0 &&
        !visites.has(cle)
      ) {
        visites.add(cle);
        file.push([
          [nx, ny],
          [...chemin, [nx, ny]],
        ]);
      }
    }
  }

  return null; // Pas de chemin
}

// Grille : 0 = libre, 1 = obstacle
const grille = [
  [0, 0, 0, 1, 0],
  [1, 1, 0, 1, 0],
  [0, 0, 0, 0, 0],
  [0, 1, 1, 1, 0],
  [0, 0, 0, 0, 0],
];

const chemin = cheminGrille(grille, [0, 0], [4, 4]);
console.log("Chemin :", chemin);
// [[0,0], [0,1], [0,2], [1,2], [2,2], [2,3], [2,4], [3,4], [4,4]]
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle structure de données est utilisée par le BFS ?**

- [ ] A. Une pile (Stack)
- [ ] B. Une file (Queue)
- [ ] C. Un arbre
- [ ] D. Une liste chaînée

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le BFS utilise une **file (Queue)** avec le principe FIFO pour garantir l'exploration niveau par niveau.

</details>

---

### Question 2

**Quelle est la complexité temporelle du BFS ?**

- [ ] A. O(V)
- [ ] B. O(E)
- [ ] C. O(V + E)
- [ ] D. O(V × E)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le BFS visite chaque sommet une fois (O(V)) et examine chaque arête une fois (O(E)), donc **O(V + E)**.

</details>

---

### Question 3

**Pourquoi le BFS garantit-il le chemin le plus court dans un graphe non pondéré ?**

- [ ] A. Il utilise une structure récursive
- [ ] B. Il explore tous les chemins de longueur N avant ceux de longueur N+1
- [ ] C. Il trie les arêtes par poids
- [ ] D. Il visite les sommets dans l'ordre alphabétique

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le BFS explore **niveau par niveau**, donc tous les chemins de longueur 1, puis tous ceux de longueur 2, etc. Le premier chemin trouvé vers la destination est forcément le plus court.

</details>

---

### Question 4

**Que se passe-t-il si on oublie de marquer les sommets comme visités ?**

- [ ] A. Le BFS sera plus rapide
- [ ] B. Le BFS ne trouvera pas tous les sommets
- [ ] C. Le BFS peut boucler indéfiniment
- [ ] D. Rien, c'est optionnel

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Sans marquer les visités, un sommet peut être ajouté plusieurs fois à la file, créant une **boucle infinie** si le graphe contient des cycles.

</details>

---

### Question 5

**Dans le BFS, quand marque-t-on un sommet comme visité ?**

- [ ] A. Quand on le retire de la file
- [ ] B. Quand on l'ajoute à la file
- [ ] C. Après avoir visité tous ses voisins
- [ ] D. Au début de l'algorithme

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

On marque un sommet comme visité **avant de l'ajouter** à la file. Cela évite d'ajouter le même sommet plusieurs fois depuis différents voisins.

</details>

---

### Question 6

**Si un graphe a 100 sommets et 500 arêtes, quelle est la taille maximale de la file durant le BFS ?**

- [ ] A. 100
- [ ] B. 500
- [ ] C. 600
- [ ] D. 50 000

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

La taille maximale de la file est **O(V) = 100**. Chaque sommet ne peut être dans la file qu'une seule fois (grâce au Set visités).

</details>

---

### Question 7

**Le BFS peut-il être utilisé pour un graphe orienté ?**

- [ ] A. Non, seulement pour les graphes non orientés
- [ ] B. Oui, sans modification
- [ ] C. Oui, mais avec des modifications majeures
- [ ] D. Seulement pour les graphes pondérés

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le BFS fonctionne **sans modification** pour les graphes orientés. On suit simplement les arêtes dans leur direction (de source vers destination).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe du BFS

Explorer **niveau par niveau** : tous les voisins directs, puis les voisins des voisins, etc.

### 2. Structure : File (Queue)

Utilise une file FIFO. `push()` pour ajouter, `shift()` pour retirer.

### 3. Set des Visités

Essential pour éviter les boucles infinies. Marquer AVANT d'ajouter à la file.

### 4. Complexité

Temps : O(V + E). Espace : O(V). Linéaire par rapport au graphe.

### 5. Chemin le Plus Court

BFS garantit le chemin avec le **moins d'arêtes** dans un graphe non pondéré.

### 6. Graphes Déconnectés

BFS ne visite que les sommets accessibles. Plusieurs BFS nécessaires pour un graphe déconnecté.

### 7. Applications

GPS, web crawlers, réseaux sociaux, diffusion réseau, jeux vidéo (pathfinding).

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant le parcours en largeur (BFS) !

### Ce que vous avez appris aujourd'hui

- Le principe du BFS : exploration **niveau par niveau**
- L'utilisation de la **file** pour gérer l'ordre de visite
- L'implémentation complète en **JavaScript**
- Comment trouver le **chemin le plus court**
- L'analyse de **complexité** O(V + E)
- Des **applications réelles** : réseaux sociaux, GPS, web crawlers

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter le BFS sur n'importe quel graphe
- Trouver le chemin le plus court dans un graphe non pondéré
- Calculer les distances depuis un sommet source
- Résoudre des problèmes de connectivité

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Le BFS est un algorithme **fondamental** en informatique. Google l'utilise pour indexer le web, Facebook pour suggérer des amis, les GPS pour planifier des itinéraires, et les jeux vidéo pour l'intelligence artificielle des personnages. Maîtriser le BFS, c'est ouvrir la porte à des millions d'applications !

---

## ➡️ Prochaine Étape : Leçon 30

### Ce qui vous attend

La prochaine leçon, **« Algorithme de Parcours en Profondeur (DFS) en JavaScript »**, vous apprendra une approche complémentaire au BFS.

**Vous découvrirez :**

- Le principe du **DFS** : explorer "en profondeur" d'abord
- L'utilisation d'une **pile** (ou récursion)
- La détection de **cycles** dans un graphe
- Quand utiliser DFS vs BFS

### Préparez-vous !

Alors que le BFS explore "en largeur", le DFS plonge "en profondeur" le plus loin possible avant de revenir en arrière. Ensemble, BFS et DFS sont les deux piliers de l'exploration des graphes !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - BFS](https://visualgo.net/en/dfsbfs) - Visualisation interactive BFS/DFS
- [Wikipedia - Breadth-First Search](https://en.wikipedia.org/wiki/Breadth-first_search) - Théorie approfondie
- [MIT OpenCourseWare - BFS](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/) - Cours MIT

### Outils de pratique

- **[LeetCode BFS Problems](https://leetcode.com/tag/breadth-first-search/)** : Exercices pratiques
- **[HackerRank Graph Theory](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=graph-theory)** : Défis algorithmiques

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Tracer le BFS sur papier avec différents graphes
- Expérimenter avec les exemples dans votre console
- Modifier les implémentations pour ajouter des fonctionnalités

> 💡 **Conseil**
>
> La meilleure façon de maîtriser le BFS est de **l'implémenter de zéro** plusieurs fois. Essayez de le coder sans regarder les solutions, puis comparez. Vous serez surpris de voir à quel point ça devient naturel après quelques essais !

---

**Prêt pour la Leçon 30 ?** 🚀

Rendez-vous dans la prochaine leçon pour apprendre le parcours en profondeur (DFS) !

---

<div align="center">

**Leçon 29 sur 42 - Module 5 : Arbres et Parcours de Graphes**

[⬅️ Leçon 28 : Implémentations Liste et Matrice](./lecon-4-implementations-liste-adjacence-matrice-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 30 : Parcours en Profondeur (DFS) ➡️](./lecon-6-algorithme-parcours-profondeur-dfs-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
