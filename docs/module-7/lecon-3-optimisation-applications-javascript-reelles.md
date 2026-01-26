##### Leçon 39 sur 42

# Optimisation d'Applications JavaScript Réelles

**Module 7** : Applications d'Algorithmes et Résolution de Problèmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Identifier et analyser les goulots d'étranglement de performance dans une application JavaScript
- Utiliser les outils de profilage pour diagnostiquer les problèmes de performance et de mémoire
- Choisir et implémenter les structures de données et algorithmes adaptés pour optimiser le code
- Appliquer des techniques concrètes d'optimisation (filtrage, indexation, asynchronisme, Web Workers)
- Éviter les pièges courants lors de l'optimisation de code JavaScript

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- Modules précédents (Big O, structures de données, DP, patterns de résolution)
- Savoir utiliser les outils de développement du navigateur (Chrome DevTools, Node.js Inspector)

---

## 🚀 Introduction : Pourquoi optimiser du JavaScript réel ?

Vous avez déjà développé des fonctionnalités qui "marchent", mais… l’application rame, la page met du temps à s’afficher, ou le serveur Node.js sature ?

L’optimisation algorithmique permet de passer d’un code fonctionnel à un code **performant, scalable et robuste**.

- Améliorer l’expérience utilisateur (UI plus fluide)
- Réduire la charge serveur et les coûts
- Gérer de grands volumes de données sans ralentissement

> **Point Clé**
>
> L’optimisation commence par l’identification des vrais problèmes (profilage), puis le choix des bons algorithmes et structures de données.

---

## 📦 Identifier les goulots d’étranglement

Avant d’optimiser, il faut savoir **où** optimiser. Les ralentissements peuvent venir du front (UI), du back (Node.js), ou de traitements de données.

### Outils de profilage

- **Chrome DevTools** (Performance Panel) : analyse du temps CPU, rendering, scripts lents, GC…
- **Node.js Inspector** : profilage serveur, analyse des routes/API lentes

**Exemple :**
Si une interaction utilisateur déclenche systématiquement 500ms de script, le flame chart permet d’identifier la fonction responsable.

---

## 📝 Micro-Exercice #1 : Repérer un hotspot

**Objectif :** Savoir lire un flame chart pour repérer une fonction lente.

**Instructions :**

1. Ouvre Chrome DevTools > Performance.
2. Lance un enregistrement pendant une action lente.
3. Repère la fonction la plus longue dans le flame chart.

<details>
<summary>💡 Voir la solution</summary>

La fonction la plus large/longue dans le flame chart est le hotspot à optimiser en priorité.

</details>

---

## 📦 Analyser les hotspots et la mémoire

Un hotspot est un code très sollicité ou très coûteux.

- **Nombre d’appels** : une fonction rapide mais appelée 10 000 fois peut devenir un problème
- **Temps d’exécution** : une fonction rare mais très lente aussi
- **Fuites mémoire** : objets non libérés, croissance continue de la mémoire

> **Question**
>
> Comment profiler la mémoire d’une application JavaScript pour détecter des fuites ?
>
> **Réponse** :
>
> - Utiliser l’onglet "Memory" de Chrome DevTools pour prendre des snapshots, suivre l’évolution de la mémoire, et repérer les objets non collectés après suppression.

---

## 📦 Choisir les bons algorithmes et structures de données

### Impact de la complexité (Big O)

- O(N^2) sur 10 000 éléments = 100 millions d’opérations !
- O(N log N) = 130 000 opérations pour 10 000 éléments

**Exemple :**
Recherche dans une liste de tâches :

- O(N) : Array.filter sur 10 000 tâches à chaque frappe
- O(1) ou O(log N) : Map pour accès direct, tableau trié pour recherche binaire

---

## 📝 Micro-Exercice #2 : Comparer deux approches

**Objectif :** Comprendre l’impact du choix de structure

**Instructions :**

1. Implémente une recherche de tâche par ID avec un tableau (Array) puis avec un Map.
2. Compare le temps d’exécution pour 10 000 tâches.

<details>
<summary>💡 Voir la solution</summary>

Array : O(N) pour chaque recherche. Map : O(1) en moyenne.

</details>

---

### Tableaux comparatifs : structures de données

| Structure       | Accès    | Insertion | Suppression | Recherche |
| --------------- | -------- | --------- | ----------- | --------- |
| Array           | O(1)     | O(1)/O(N) | O(N)        | O(N)      |
| Object          | O(1)\*   | O(1)\*    | O(1)\*      | O(1)\*    |
| Map             | O(1)     | O(1)      | O(1)        | O(1)      |
| Set             | O(1)     | O(1)      | O(1)        | O(1)      |
| Linked List     | O(N)     | O(1)      | O(1)        | O(N)      |
| BST (équilibré) | O(log N) | O(log N)  | O(log N)    | O(log N)  |

\*En moyenne, dépend de la clé et de la distribution

> **Question**
>
> Comment choisir entre un objet JavaScript simple et un Map pour du stockage clé-valeur ?
>
> **Réponse** :
>
> - Map gère nativement tout type de clé, conserve l’ordre d’insertion, et évite les collisions avec les clés héritées d’Object. Pour des clés dynamiques ou non-string, Map est préférable. Object reste adapté pour des structures simples et fixes.

---

## 📦 Implémenter efficacement : techniques concrètes

### Éviter les calculs redondants

- Utiliser la mémoïsation (Module 6)
- Stocker les résultats intermédiaires

### Optimiser les boucles

- Déplacer les calculs constants hors de la boucle
- Éviter les appels de fonction inutiles dans la boucle

> **Question**
>
> Quels sont les pièges courants lors de l’optimisation des boucles JavaScript ?
>
> **Réponse** :
>
> - Modifier la taille du tableau pendant l’itération, oublier les cas limites (tableau vide), faire des appels coûteux dans la boucle, ne pas sortir tôt si possible.

---

## 📝 Micro-Exercice #3 : Boucle optimisée

**Objectif :** Réécrire une boucle pour éviter les calculs inutiles

**Instructions :**

1. Prends une boucle qui calcule la longueur d’un tableau à chaque itération.
2. Optimise-la pour ne calculer la longueur qu’une fois.

<details>
<summary>💡 Voir la solution</summary>

Stocker la longueur dans une variable avant la boucle.

</details>

---

### Asynchronisme et Web Workers

- Utiliser async/await ou Promises pour les tâches I/O
- Web Workers pour les calculs lourds côté client (éviter de bloquer l’UI)

> **Question**
>
> Quand faut-il envisager d’utiliser les Web Workers pour optimiser les performances ?
>
> **Réponse** :
>
> - Pour les traitements CPU intensifs (gros calculs, parsing, compression) qui risquent de bloquer le thread principal et de rendre l’UI non réactive.

---

## 📦 Exemples pratiques d’optimisation

### Exemple 1 : Filtrage de tâches (version naïve vs optimisée)

**Problème** : Filtrer des tâches par statut dans une liste de 10 000 tâches.

```javascript
// Version naïve : O(N) à chaque recherche
const taches = [
  { id: 1, titre: "Faire les courses", statut: "en_cours", priorite: 2 },
  { id: 2, titre: "Réviser les algos", statut: "terminee", priorite: 1 },
  // ... 10 000 tâches
];

/**
 * Filtre les tâches par statut - VERSION NAÏVE
 * Complexité : O(N) pour chaque appel
 */
function filtrerTachesNaif(taches, statut) {
  return taches.filter((t) => t.statut === statut);
}

// À chaque frappe dans la recherche : O(N) !
const enCours = filtrerTachesNaif(taches, "en_cours");
const terminees = filtrerTachesNaif(taches, "terminee");
```

```javascript
// Version optimisée : Indexation avec Map
/**
 * Construit un index par statut - Complexité : O(N) une seule fois
 *
 * @param {Array} taches - Liste des tâches
 * @returns {Map<string, Array>} - Index statut → tâches
 */
function construireIndexStatut(taches) {
  const index = new Map();

  for (const tache of taches) {
    const statut = tache.statut;
    if (!index.has(statut)) {
      index.set(statut, []);
    }
    index.get(statut).push(tache);
  }

  return index;
}

/**
 * Filtre les tâches par statut - VERSION OPTIMISÉE
 * Complexité : O(1) pour chaque appel (après indexation)
 */
function filtrerTachesOptimise(index, statut) {
  return index.get(statut) || [];
}

// Indexation initiale : O(N) une fois
const indexStatut = construireIndexStatut(taches);

// Recherches : O(1) à chaque fois !
const enCours = filtrerTachesOptimise(indexStatut, "en_cours");
const terminees = filtrerTachesOptimise(indexStatut, "terminee");
```

**Gain de performance** :

- **Naïf** : 10 000 itérations × 100 recherches = **1 000 000 opérations**
- **Optimisé** : 10 000 (indexation) + 100 (recherches) = **10 100 opérations**
- **Gain** : ~100x plus rapide !

---

### Exemple 2 : Indexation multi-critères pour filtrage rapide

**Problème** : Filtrer par statut ET priorité simultanément.

```javascript
/**
 * Construit des index multiples pour différents critères
 * Complexité : O(N) pour la construction
 *
 * @param {Array} taches - Liste des tâches
 * @returns {Object} - Objets avec index par statut, priorité, assigné
 */
function construireIndexMultiples(taches) {
  const indexStatut = new Map();
  const indexPriorite = new Map();
  const indexAssigne = new Map();

  for (const tache of taches) {
    // Index par statut
    if (!indexStatut.has(tache.statut)) {
      indexStatut.set(tache.statut, []);
    }
    indexStatut.get(tache.statut).push(tache);

    // Index par priorité
    if (!indexPriorite.has(tache.priorite)) {
      indexPriorite.set(tache.priorite, []);
    }
    indexPriorite.get(tache.priorite).push(tache);

    // Index par utilisateur assigné
    if (tache.assigneA) {
      if (!indexAssigne.has(tache.assigneA)) {
        indexAssigne.set(tache.assigneA, []);
      }
      indexAssigne.get(tache.assigneA).push(tache);
    }
  }

  return { indexStatut, indexPriorite, indexAssigne };
}

/**
 * Filtre par plusieurs critères avec intersection
 * Complexité : O(M + P) où M et P sont les tailles des sous-ensembles
 *
 * @param {Object} indexes - Index construits
 * @param {Object} filtres - Critères de filtrage
 * @returns {Array} - Tâches filtrées
 */
function filtrerMultiCriteres(indexes, filtres) {
  const { statut, priorite, assigneA } = filtres;

  // Récupérer les ensembles pour chaque critère
  const ensembles = [];

  if (statut) {
    ensembles.push(new Set(indexes.indexStatut.get(statut) || []));
  }
  if (priorite !== undefined) {
    ensembles.push(new Set(indexes.indexPriorite.get(priorite) || []));
  }
  if (assigneA) {
    ensembles.push(new Set(indexes.indexAssigne.get(assigneA) || []));
  }

  if (ensembles.length === 0) return [];

  // Intersection des ensembles (garder seulement les tâches présentes dans tous)
  let resultat = ensembles[0];
  for (let i = 1; i < ensembles.length; i++) {
    resultat = new Set(
      [...resultat].filter((tache) => ensembles[i].has(tache)),
    );
  }

  return Array.from(resultat);
}

// Utilisation
const indexes = construireIndexMultiples(taches);

// Filtrer : statut="en_cours" ET priorite=1
const tachesUrgentes = filtrerMultiCriteres(indexes, {
  statut: "en_cours",
  priorite: 1,
});

// Filtrer : assigneA="alice" ET statut="terminee"
const tachesAliceTerminees = filtrerMultiCriteres(indexes, {
  assigneA: "alice",
  statut: "terminee",
});
```

**Complexité** :

- **Sans index** : O(N) pour chaque filtrage → N × nombre de filtres
- **Avec index** : O(M + P) où M et P sont les tailles des sous-ensembles (généralement M, P << N)
- **Exemple** : 10 000 tâches, 500 "en_cours", 200 priorité 1 → intersection de 500 + 200 = 700 au lieu de 10 000

---

## 📝 Micro-Exercice #4 : Indexation

**Objectif :** Créer un index pour accélérer la recherche

**Instructions :**

1. Implémente une Map qui associe chaque statut à la liste des tâches correspondantes.
2. Utilise cet index pour filtrer rapidement les tâches par statut.

<details>
<summary>💡 Voir la solution</summary>

Voir la fonction buildIndexes et l’utilisation de Map dans l’exemple ci-dessus.

</details>

---

## 💪 Exercices Pratiques

Pour t’entraîner à optimiser des applications JavaScript, résous les problèmes suivants :

---

### Exercice 1 : Recherche de tâches par tags

**Objectif :** Filtrer efficacement les tâches par plusieurs tags

**Instructions :**

1. Implémente une fonction qui retourne les tâches ayant tous les tags demandés.
2. Propose une version optimisée avec indexation par tag.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Construit un index par tag
 * Complexité : O(N × T) où N = nombre de tâches, T = nombre moyen de tags par tâche
 *
 * @param {Array} taches - Liste des tâches avec propriété tags: string[]
 * @returns {Map<string, Set>} - Index tag → Set de tâches
 */
function construireIndexTags(taches) {
  const indexTags = new Map();

  for (const tache of taches) {
    for (const tag of tache.tags || []) {
      if (!indexTags.has(tag)) {
        indexTags.set(tag, new Set());
      }
      indexTags.get(tag).add(tache);
    }
  }

  return indexTags;
}

/**
 * Filtre les tâches ayant TOUS les tags demandés (intersection)
 * Complexité : O(M × K) où M = taille du plus petit ensemble, K = nombre de tags demandés
 *
 * @param {Map} indexTags - Index construit
 * @param {string[]} tagsRecherches - Tags à rechercher
 * @returns {Array} - Tâches ayant tous les tags
 */
function rechercherParTags(indexTags, tagsRecherches) {
  if (tagsRecherches.length === 0) return [];

  // Récupérer les ensembles pour chaque tag
  const ensembles = tagsRecherches
    .map((tag) => indexTags.get(tag))
    .filter((ens) => ens !== undefined);

  if (ensembles.length !== tagsRecherches.length) {
    return []; // Un tag n'existe pas
  }

  // Commencer par le plus petit ensemble (optimisation)
  ensembles.sort((a, b) => a.size - b.size);

  // Intersection : garder les tâches présentes dans tous les ensembles
  let resultat = new Set(ensembles[0]);

  for (let i = 1; i < ensembles.length; i++) {
    resultat = new Set(
      [...resultat].filter((tache) => ensembles[i].has(tache)),
    );

    // Optimisation : sortir tôt si l'intersection est vide
    if (resultat.size === 0) break;
  }

  return Array.from(resultat);
}

// Utilisation
const taches = [
  { id: 1, titre: "Bug login", tags: ["urgent", "bug", "frontend"] },
  { id: 2, titre: "Feature auth", tags: ["feature", "backend", "urgent"] },
  { id: 3, titre: "Fix UI", tags: ["bug", "frontend"] },
];

const indexTags = construireIndexTags(taches);

// Tâches avec tags "urgent" ET "frontend"
const urgentFrontend = rechercherParTags(indexTags, ["urgent", "frontend"]);
console.log(urgentFrontend); // [{ id: 1, titre: "Bug login", ... }]
```

**Gain** : Au lieu de O(N × K) pour filtrer naïvement, on a O(M × K) où M << N (taille du plus petit ensemble).

</details>

---

### Exercice 2 : Comptage d'utilisateurs uniques

**Objectif :** Compter rapidement les utilisateurs uniques dans une fenêtre de temps

**Instructions :**

1. Implémente getUniqueUsersInWindow(events, start, end) avec un Set.
2. Propose une optimisation pour éviter de parcourir tous les events à chaque appel.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * VERSION NAÏVE : Parcourt tous les events à chaque appel
 * Complexité : O(N) pour chaque requête
 */
function getUniqueUsersInWindowNaif(events, start, end) {
  const utilisateursUniques = new Set();

  for (const event of events) {
    if (event.timestamp >= start && event.timestamp <= end) {
      utilisateursUniques.add(event.userId);
    }
  }

  return utilisateursUniques.size;
}

/**
 * VERSION OPTIMISÉE : Pré-indexe les events par timestamp
 * Complexité construction : O(N log N) - tri
 * Complexité requête : O(log N + M) où M = nombre d'events dans la fenêtre
 */
class EventsIndex {
  constructor(events) {
    // Trier les events par timestamp : O(N log N)
    this.events = events.sort((a, b) => a.timestamp - b.timestamp);
  }

  /**
   * Recherche binaire pour trouver le premier event >= start
   * Complexité : O(log N)
   */
  findFirstIndex(timestamp) {
    let gauche = 0;
    let droite = this.events.length;

    while (gauche < droite) {
      const milieu = Math.floor((gauche + droite) / 2);
      if (this.events[milieu].timestamp < timestamp) {
        gauche = milieu + 1;
      } else {
        droite = milieu;
      }
    }

    return gauche;
  }

  /**
   * Compte les utilisateurs uniques dans [start, end]
   * Complexité : O(log N + M) où M = nombre d'events dans la fenêtre
   */
  getUniqueUsersInWindow(start, end) {
    const startIndex = this.findFirstIndex(start);
    const utilisateursUniques = new Set();

    // Parcourir seulement les events dans la fenêtre : O(M)
    for (let i = startIndex; i < this.events.length; i++) {
      if (this.events[i].timestamp > end) break;
      utilisateursUniques.add(this.events[i].userId);
    }

    return utilisateursUniques.size;
  }
}

// Utilisation
const events = [
  { userId: 1, timestamp: 100 },
  { userId: 2, timestamp: 150 },
  { userId: 1, timestamp: 200 },
  { userId: 3, timestamp: 250 },
  { userId: 2, timestamp: 300 },
  // ... 10 000 events
];

const index = new EventsIndex(events);

// Requêtes rapides : O(log N + M) au lieu de O(N)
console.log(index.getUniqueUsersInWindow(100, 200)); // 2 (users 1 et 2)
console.log(index.getUniqueUsersInWindow(200, 300)); // 3 (users 1, 2, 3)
```

**Optimisation supplémentaire** : Pour des fenêtres glissantes (ex: dernières 24h), utiliser une structure de données avec insertion/suppression en O(1) comme une file à double entrée (deque) avec un Set pour les utilisateurs.

</details>

---

### Exercice 3 : Typeahead performant

**Objectif :** Accélérer la recherche de suggestions en temps réel

**Instructions :**

1. Propose une stratégie pour accélérer la recherche de titres de tâches sans Trie.
2. Implémente une version qui pré-indexe les préfixes courants.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * VERSION NAÏVE : Filtre tous les titres à chaque frappe
 * Complexité : O(N × L) où N = nombre de tâches, L = longueur moyenne des titres
 */
function typeaheadNaif(taches, prefixe) {
  const prefixeLower = prefixe.toLowerCase();
  return taches
    .filter((t) => t.titre.toLowerCase().startsWith(prefixeLower))
    .slice(0, 10); // Limiter à 10 résultats
}

/**
 * VERSION OPTIMISÉE : Pré-indexe les préfixes courts
 * Complexité construction : O(N × L × P) où P = longueur max des préfixes indexés
 * Complexité requête : O(M) où M = nombre de tâches avec ce préfixe
 */
class TypeaheadIndex {
  constructor(taches, prefixLength = 3) {
    this.prefixLength = prefixLength;
    this.indexPrefixes = new Map(); // préfixe → Set de tâches

    // Construire l'index
    for (const tache of taches) {
      const titreLower = tache.titre.toLowerCase();

      // Indexer tous les préfixes jusqu'à prefixLength
      for (
        let len = 1;
        len <= Math.min(prefixLength, titreLower.length);
        len++
      ) {
        const prefixe = titreLower.substring(0, len);

        if (!this.indexPrefixes.has(prefixe)) {
          this.indexPrefixes.set(prefixe, new Set());
        }
        this.indexPrefixes.get(prefixe).add(tache);
      }

      // Pour les préfixes plus longs, indexer par mots
      const mots = titreLower.split(/\s+/);
      for (const mot of mots) {
        for (let len = 1; len <= Math.min(prefixLength, mot.length); len++) {
          const prefixe = mot.substring(0, len);

          if (!this.indexPrefixes.has(prefixe)) {
            this.indexPrefixes.set(prefixe, new Set());
          }
          this.indexPrefixes.get(prefixe).add(tache);
        }
      }
    }
  }

  /**
   * Recherche de suggestions avec le préfixe
   * Complexité : O(M + M log M) où M = nombre de résultats
   */
  search(prefixe, limit = 10) {
    const prefixeLower = prefixe.toLowerCase();

    // Si le préfixe est court, utiliser l'index
    if (prefixeLower.length <= this.prefixLength) {
      const resultats = this.indexPrefixes.get(prefixeLower);
      if (!resultats) return [];

      // Trier par pertinence (titre qui commence par le préfixe en premier)
      return Array.from(resultats)
        .sort((a, b) => {
          const aStarts = a.titre.toLowerCase().startsWith(prefixeLower);
          const bStarts = b.titre.toLowerCase().startsWith(prefixeLower);
          if (aStarts && !bStarts) return -1;
          if (!aStarts && bStarts) return 1;
          return a.titre.localeCompare(b.titre);
        })
        .slice(0, limit);
    }

    // Pour les préfixes longs, utiliser l'index du préfixe court puis filtrer
    const prefixeCourt = prefixeLower.substring(0, this.prefixLength);
    const candidats = this.indexPrefixes.get(prefixeCourt);

    if (!candidats) return [];

    return Array.from(candidats)
      .filter((t) => t.titre.toLowerCase().includes(prefixeLower))
      .sort((a, b) => {
        const aStarts = a.titre.toLowerCase().startsWith(prefixeLower);
        const bStarts = b.titre.toLowerCase().startsWith(prefixeLower);
        if (aStarts && !bStarts) return -1;
        if (!aStarts && bStarts) return 1;
        return a.titre.localeCompare(b.titre);
      })
      .slice(0, limit);
  }
}

// Utilisation
const taches = [
  { id: 1, titre: "Faire les courses" },
  { id: 2, titre: "Faire du sport" },
  { id: 3, titre: "Finir le projet" },
  { id: 4, titre: "Réviser les algorithmes" },
  { id: 5, titre: "Appeler le dentiste" },
  // ... 10 000 tâches
];

const typeahead = new TypeaheadIndex(taches, 3);

// Recherche rapide : O(M) au lieu de O(N)
console.log(typeahead.search("fai")); // ["Faire les courses", "Faire du sport"]
console.log(typeahead.search("pro")); // ["Finir le projet"]
console.log(typeahead.search("algo")); // ["Réviser les algorithmes"]
```

**Gains** :

- **Naïf** : O(N × L) pour chaque frappe (10 000 × 20 = 200 000 opérations)
- **Optimisé** : O(M) où M << N (ex: 50 tâches au lieu de 10 000)
- **Ratio** : ~200x plus rapide pour des recherches courantes !

**Trade-off** :

- **Mémoire** : Index supplémentaire (O(N × P × L))
- **Temps** : Construction initiale plus longue
- **Bénéfice** : Recherches ultra-rapides en production

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Comment choisir entre un objet JavaScript simple et un Map pour du stockage clé-valeur ?**

- [ ] A. Map gère tout type de clé et conserve l’ordre d’insertion
- [ ] B. Object ne gère que des clés string/symbol
- [ ] C. Map évite les collisions avec les clés héritées
- [ ] D. Toutes les réponses

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Map est plus flexible et sûr pour des clés dynamiques ou non-string.

</details>

---

### Question 2

**Quels sont les pièges courants lors de l’optimisation des boucles JavaScript ?**

- [ ] A. Modifier la taille du tableau pendant l’itération
- [ ] B. Oublier les cas limites (tableau vide)
- [ ] C. Faire des appels coûteux dans la boucle
- [ ] D. Toutes les réponses

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Tous ces pièges peuvent impacter la performance ou la robustesse.

</details>

---

### Question 3

**Quand utiliser les Web Workers pour optimiser une application JavaScript ?**

- [ ] A. Pour les tâches I/O simples
- [ ] B. Pour les calculs CPU intensifs qui bloquent l’UI
- [ ] C. Pour les requêtes réseau
- [ ] D. Pour le rendu graphique

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Web Workers sont faits pour déporter les calculs lourds hors du thread principal.

</details>

---

### Question 4

**Comment profiler la mémoire d’une application JavaScript pour détecter des fuites ?**

- [ ] A. Utiliser l’onglet "Memory" de Chrome DevTools
- [ ] B. Prendre des snapshots mémoire
- [ ] C. Surveiller les objets non collectés
- [ ] D. Toutes les réponses

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Toutes ces actions sont nécessaires pour détecter les fuites mémoire.

</details>

---

### Question 5

**Quel est le principal avantage de l'indexation multi-critères pour le filtrage de données ?**

- [ ] A. Réduire la mémoire utilisée
- [ ] B. Éviter les boucles imbriquées
- [ ] C. Accélérer les recherches en pré-calculant les sous-ensembles
- [ ] D. Simplifier le code

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

L'indexation multi-critères permet de pré-calculer les sous-ensembles pour chaque critère, transformant des recherches O(N) en O(M) où M << N. Le coût mémoire supplémentaire est compensé par les gains de performance sur les requêtes fréquentes.

</details>

---

### Question 6

**Quelle est la meilleure complexité pour une recherche dans une fenêtre de temps sur des events triés par timestamp ?**

- [ ] A. O(N) - parcourir tous les events
- [ ] B. O(N log N) - trier puis parcourir
- [ ] C. O(log N + M) - recherche binaire + parcours de la fenêtre
- [ ] D. O(M²) - parcours quadratique de la fenêtre

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Avec des events pré-triés, une recherche binaire trouve le début de la fenêtre en O(log N), puis on parcourt seulement les M events dans la fenêtre. Total : O(log N + M) où M << N généralement.

</details>

---

### Question 7

**Pourquoi utiliser un Set pour l'intersection d'ensembles plutôt qu'un Array ?**

- [ ] A. Set consomme moins de mémoire
- [ ] B. Set.has() est O(1) vs Array.includes() O(N)
- [ ] C. Set est plus facile à lire
- [ ] D. Set trie automatiquement

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Set.has() a une complexité O(1) en moyenne grâce au hash, tandis qu'Array.includes() doit parcourir le tableau en O(N). Pour des intersections sur des ensembles de taille M et P, cela passe de O(M × P) à O(M + P).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Profilage avant optimisation

Toujours mesurer avant d’optimiser pour cibler les vrais problèmes.

### 2. Choix des structures de données

Adapter la structure à l’usage pour gagner en performance.

### 3. Big O en pratique

Comprendre l’impact réel de la complexité sur les données réelles.

### 4. Boucles et calculs redondants

Optimiser les boucles et éviter les répétitions inutiles.

### 5. Asynchronisme et Web Workers

Utiliser l’asynchronisme et les Web Workers pour garder l’UI fluide.

### 6. Indexation et pré-calcul

Pré-indexer les données pour accélérer les recherches fréquentes.

### 7. Pièges courants à éviter

Toujours tester les cas limites et surveiller la mémoire.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Tu sais maintenant optimiser des applications JavaScript réelles en combinant analyse, choix d’algorithmes, structures de données et techniques avancées.

### Ce que tu as appris aujourd’hui

- Identifier et profiler les goulots d’étranglement
- Choisir la bonne structure de données
- Implémenter des optimisations concrètes

### Compétences acquises

Tu es maintenant capable de :

- Diagnostiquer et corriger les problèmes de performance
- Appliquer des techniques d’optimisation avancées
- Adapter tes choix à des cas réels

### Pourquoi c’est important

> 📌 **Point Clé**
>
> L’optimisation algorithmique transforme un code "qui marche" en code **scalable** et **robuste** pour des applications réelles.

---

## ➡️ Prochaine Étape : Leçon 40

### Ce qui t’attend

La prochaine leçon, **« Étude de Cas Avancée : Appliquer les Algorithmes pour Améliorer l’Efficacité de la Gestion de Tâches »**, te montrera comment combiner toutes les techniques vues pour optimiser un projet complet.

**Tu découvriras :**

- Comment structurer une optimisation de bout en bout
- L’analyse d’un cas réel complexe
- Les bonnes pratiques pour industrialiser l’optimisation

### Prépare-toi !

Tu vas passer de l’optimisation locale à l’optimisation globale d’une application !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [MDN - Optimisation des performances JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript/Performance)
- [Google Chrome DevTools - Performance Profiling](https://developer.chrome.com/docs/devtools/evaluate-performance/)
- [Node.js - Guide de Profilage](https://nodejs.org/en/docs/guides/simple-profiling/)
- [JavaScript.info - Structures de données](https://javascript.info/keys-values-entries)

### Outils de pratique

- **[JSBench.me](https://jsbench.me/)** : Comparer la performance de différents algorithmes
- **[Chrome DevTools](https://developer.chrome.com/docs/devtools/)** : Profilage et analyse de code

---

## 💬 Feedback et Questions

Tu as des questions sur cette leçon ? Un doute sur une technique d’optimisation ?

N’hésite pas à :

- Relire les exemples et exercices
- Tester les codes dans ta console
- Demander de l’aide sur le forum du cours

> 💡 **Conseil**
>
> Prends toujours le temps de mesurer avant d’optimiser, et privilégie la clarté du code avant la micro-optimisation !

---

**Prêt pour la Leçon 40 ?** 🚀

Rendez-vous dans la prochaine leçon pour une étude de cas complète sur l’optimisation d’une application !

---

<div align="center">

**Leçon 39 sur 42 - Module 7 : Applications d'Algorithmes et Résolution de Problèmes**

[⬅️ Leçon 38 : Patterns Courants de Résolution de Problèmes Algorithmiques](./lecon-2-patterns-courants-resolution-problemes-algorithmiques.md) | [Retour au sommaire](./README.md) | [Leçon 40 : Étude de Cas Avancée : Appliquer les Algorithmes pour Améliorer l’Efficacité de la Gestion de Tâches ➡️](./lecon-4-etude-cas-avancee-appliquer-algorithmes-ameliorer-efficacite-gestion-taches.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
