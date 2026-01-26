##### Leçon 28 sur 42

# Implémentations Liste d'Adjacence et Matrice en JavaScript

**Module 5** : Arbres et Parcours de Graphes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Implémenter une **classe Matrice d'Adjacence** complète et robuste
- Implémenter une **classe Liste d'Adjacence** complète et robuste
- Gérer les graphes **orientés, non orientés et pondérés**
- Ajouter et **supprimer** des arêtes efficacement
- Analyser la **complexité** de chaque opération
- Choisir la **représentation optimale** selon le cas d'usage

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 27 complétée** : Concepts des graphes (sommets, arêtes, types)
- **Tableaux 2D** : Créer et manipuler des matrices
- **Map JavaScript** : Utiliser les Maps comme dictionnaires
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : De la Théorie à la Pratique

Dans la leçon précédente, vous avez découvert les **concepts** des graphes et leurs deux représentations principales. Cette leçon se concentre sur l'**implémentation complète** de ces structures en JavaScript.

Nous allons créer des classes **réutilisables** et **robustes** que vous pourrez utiliser dans vos projets futurs, notamment pour les algorithmes de parcours (BFS, DFS) que nous verrons dans les prochaines leçons.

> **Point Clé**
>
> Une bonne implémentation de graphe doit être **flexible** (supporter différents types de sommets), **robuste** (gérer les erreurs), et **efficace** (optimiser les opérations fréquentes). C'est ce que nous allons construire ensemble.

---

## 📖 Rappel : Terminologie des Graphes

Avant de plonger dans le code, révisons rapidement les termes clés :

| Terme                         | Définition                     | Exemple                   |
| ----------------------------- | ------------------------------ | ------------------------- |
| **Sommet (Vertex)**           | Entité du graphe               | Une ville, un utilisateur |
| **Arête (Edge)**              | Connexion entre deux sommets   | Une route, une amitié     |
| **Graphe Non Orienté**        | Arêtes bidirectionnelles       | Amitiés (symétriques)     |
| **Graphe Orienté (Digraphe)** | Arêtes unidirectionnelles      | Abonnements TikTok        |
| **Graphe Pondéré**            | Arêtes avec valeurs numériques | Routes avec distances     |
| **Degré d'un sommet**         | Nombre d'arêtes connectées     | Nombre d'amis             |

---

## 💻 Implémentation 1 : Matrice d'Adjacence

La **matrice d'adjacence** représente un graphe comme un tableau 2D de taille V × V.

---

### Rappel du Fonctionnement

```
Graphe avec 4 sommets et arêtes (0,1), (0,2), (1,2), (2,3) :

      0   1   2   3
    +---+---+---+---+
  0 | 0 | 1 | 1 | 0 |   → sommet 0 connecté à 1 et 2
    +---+---+---+---+
  1 | 1 | 0 | 1 | 0 |   → sommet 1 connecté à 0 et 2
    +---+---+---+---+
  2 | 1 | 1 | 0 | 1 |   → sommet 2 connecté à 0, 1 et 3
    +---+---+---+---+
  3 | 0 | 0 | 1 | 0 |   → sommet 3 connecté à 2 seulement
    +---+---+---+---+
```

**Pour un graphe non orienté :** La matrice est **symétrique** (matrice[i][j] === matrice[j][i])

**Pour un graphe orienté :** La matrice peut être **asymétrique**

---

### Classe Complète : GrapheMatriceAdjacence

```javascript
/**
 * Représente un graphe via une Matrice d'Adjacence.
 * Supporte les graphes orientés/non orientés et pondérés/non pondérés.
 */
class GrapheMatriceAdjacence {
  /**
   * Crée un nouveau graphe.
   * @param {number} nombreSommets - Nombre de sommets (fixe).
   * @param {boolean} oriente - True si le graphe est orienté.
   */
  constructor(nombreSommets, oriente = false) {
    this.nombreSommets = nombreSommets;
    this.oriente = oriente;

    // Initialiser une matrice V × V remplie de 0
    this.matrice = Array(nombreSommets)
      .fill(null)
      .map(() => Array(nombreSommets).fill(0));
  }

  /**
   * Valide qu'un indice de sommet est valide.
   * @param {number} sommet - L'indice à valider.
   * @returns {boolean} - True si valide.
   */
  _estSommetValide(sommet) {
    return sommet >= 0 && sommet < this.nombreSommets;
  }

  /**
   * Ajoute une arête entre deux sommets.
   * @param {number} source - Sommet source.
   * @param {number} destination - Sommet destination.
   * @param {number} poids - Poids de l'arête (1 par défaut).
   * @returns {boolean} - True si l'ajout a réussi.
   */
  ajouterArete(source, destination, poids = 1) {
    // Validation des sommets
    if (!this._estSommetValide(source) || !this._estSommetValide(destination)) {
      console.error(
        `Indice de sommet invalide : source=${source}, destination=${destination}`,
      );
      return false;
    }

    // Ajouter l'arête
    this.matrice[source][destination] = poids;

    // Si non orienté, ajouter aussi dans l'autre sens
    if (!this.oriente) {
      this.matrice[destination][source] = poids;
    }

    return true;
  }

  /**
   * Supprime une arête entre deux sommets.
   * @param {number} source - Sommet source.
   * @param {number} destination - Sommet destination.
   * @returns {boolean} - True si la suppression a réussi.
   */
  supprimerArete(source, destination) {
    if (!this._estSommetValide(source) || !this._estSommetValide(destination)) {
      console.error(`Indice de sommet invalide`);
      return false;
    }

    // Supprimer l'arête (mettre à 0)
    this.matrice[source][destination] = 0;

    if (!this.oriente) {
      this.matrice[destination][source] = 0;
    }

    return true;
  }

  /**
   * Vérifie si une arête existe.
   * @param {number} source - Sommet source.
   * @param {number} destination - Sommet destination.
   * @returns {boolean} - True si l'arête existe.
   */
  existeArete(source, destination) {
    if (!this._estSommetValide(source) || !this._estSommetValide(destination)) {
      return false;
    }
    return this.matrice[source][destination] !== 0;
  }

  /**
   * Obtient le poids d'une arête.
   * @param {number} source - Sommet source.
   * @param {number} destination - Sommet destination.
   * @returns {number|null} - Le poids ou null si pas d'arête.
   */
  obtenirPoids(source, destination) {
    if (!this._estSommetValide(source) || !this._estSommetValide(destination)) {
      return null;
    }
    const poids = this.matrice[source][destination];
    return poids !== 0 ? poids : null;
  }

  /**
   * Retourne tous les voisins d'un sommet.
   * @param {number} sommet - Le sommet.
   * @returns {number[]} - Liste des indices des voisins.
   */
  obtenirVoisins(sommet) {
    if (!this._estSommetValide(sommet)) {
      return [];
    }

    const voisins = [];
    for (let i = 0; i < this.nombreSommets; i++) {
      if (this.matrice[sommet][i] !== 0) {
        voisins.push(i);
      }
    }
    return voisins;
  }

  /**
   * Calcule le degré d'un sommet.
   * Pour un graphe orienté, retourne le degré sortant.
   * @param {number} sommet - Le sommet.
   * @returns {number} - Le degré du sommet.
   */
  obtenirDegre(sommet) {
    return this.obtenirVoisins(sommet).length;
  }

  /**
   * Compte le nombre total d'arêtes.
   * @returns {number} - Nombre d'arêtes.
   */
  compterAretes() {
    let count = 0;
    for (let i = 0; i < this.nombreSommets; i++) {
      for (let j = 0; j < this.nombreSommets; j++) {
        if (this.matrice[i][j] !== 0) {
          count++;
        }
      }
    }
    // Pour un graphe non orienté, diviser par 2 (chaque arête comptée 2 fois)
    return this.oriente ? count : count / 2;
  }

  /**
   * Affiche la matrice d'adjacence.
   */
  afficher() {
    console.log("Matrice d'Adjacence :");
    console.log(
      "    " +
        Array.from({ length: this.nombreSommets }, (_, i) => i).join("  "),
    );
    console.log("   +" + "---+".repeat(this.nombreSommets));

    for (let i = 0; i < this.nombreSommets; i++) {
      const ligne = this.matrice[i].map((v) => String(v).padStart(2)).join(" ");
      console.log(` ${i} | ${ligne} |`);
    }
  }
}
```

---

### Exemples d'Utilisation

#### Exemple 1 : Graphe Non Orienté

```javascript
// Créer un graphe non orienté avec 4 sommets
const grapheNonOriente = new GrapheMatriceAdjacence(4);

// Ajouter des arêtes
grapheNonOriente.ajouterArete(0, 1);
grapheNonOriente.ajouterArete(0, 2);
grapheNonOriente.ajouterArete(1, 2);
grapheNonOriente.ajouterArete(2, 3);

grapheNonOriente.afficher();
/*
Matrice d'Adjacence :
    0  1  2  3
   +---+---+---+---+
 0 |  0  1  1  0 |
 1 |  1  0  1  0 |
 2 |  1  1  0  1 |
 3 |  0  0  1  0 |
*/

console.log("Arête (0,1) existe ?", grapheNonOriente.existeArete(0, 1)); // true
console.log("Arête (0,3) existe ?", grapheNonOriente.existeArete(0, 3)); // false
console.log("Voisins de 2 :", grapheNonOriente.obtenirVoisins(2)); // [0, 1, 3]
console.log("Degré de 2 :", grapheNonOriente.obtenirDegre(2)); // 3
console.log("Nombre d'arêtes :", grapheNonOriente.compterAretes()); // 4
```

#### Exemple 2 : Graphe Orienté

```javascript
// Créer un graphe orienté avec 3 sommets
const grapheOriente = new GrapheMatriceAdjacence(3, true);

// Ajouter des arêtes (direction : source → destination)
grapheOriente.ajouterArete(0, 1); // 0 → 1
grapheOriente.ajouterArete(1, 2); // 1 → 2
grapheOriente.ajouterArete(2, 0); // 2 → 0

grapheOriente.afficher();
/*
Matrice d'Adjacence :
    0  1  2
   +---+---+---+
 0 |  0  1  0 |    → 0 pointe vers 1
 1 |  0  0  1 |    → 1 pointe vers 2
 2 |  1  0  0 |    → 2 pointe vers 0
*/

console.log("Arête (0,1) existe ?", grapheOriente.existeArete(0, 1)); // true
console.log("Arête (1,0) existe ?", grapheOriente.existeArete(1, 0)); // false !
```

#### Exemple 3 : Graphe Pondéré (Distances entre Villes Belges)

```javascript
// Graphe pondéré : distances en km entre villes belges
// Sommets : 0=Bruxelles, 1=Anvers, 2=Gand, 3=Liège
const routesBelgique = new GrapheMatriceAdjacence(4);

routesBelgique.ajouterArete(0, 1, 50); // Bruxelles - Anvers : 50 km
routesBelgique.ajouterArete(0, 2, 55); // Bruxelles - Gand : 55 km
routesBelgique.ajouterArete(1, 2, 60); // Anvers - Gand : 60 km
routesBelgique.ajouterArete(1, 3, 120); // Anvers - Liège : 120 km

routesBelgique.afficher();
/*
    0   1   2   3
   +---+---+---+---+
 0 |  0  50  55   0 |  Bruxelles
 1 | 50   0  60 120 |  Anvers
 2 | 55  60   0   0 |  Gand
 3 |  0 120   0   0 |  Liège
*/

console.log(
  "Distance Bruxelles-Anvers :",
  routesBelgique.obtenirPoids(0, 1),
  "km",
); // 50 km
console.log("Distance Bruxelles-Liège :", routesBelgique.obtenirPoids(0, 3)); // null (pas de route directe)
```

---

## 📝 Micro-Exercice #1 : Matrice d'Adjacence

**Objectif :** Créer et manipuler une matrice d'adjacence.

**Instructions :**

1. Créez un graphe orienté pondéré de 4 sommets
2. Ajoutez les arêtes : 0→1 (poids 2), 0→2 (poids 5), 1→3 (poids 1), 2→1 (poids 3), 3→0 (poids 4)
3. Vérifiez si l'arête 2→0 existe

<details>
<summary>💡 Voir la solution</summary>

```javascript
const graphe = new GrapheMatriceAdjacence(4, true); // orienté

graphe.ajouterArete(0, 1, 2);
graphe.ajouterArete(0, 2, 5);
graphe.ajouterArete(1, 3, 1);
graphe.ajouterArete(2, 1, 3);
graphe.ajouterArete(3, 0, 4);

graphe.afficher();
/*
    0  1  2  3
   +---+---+---+---+
 0 |  0  2  5  0 |
 1 |  0  0  0  1 |
 2 |  0  3  0  0 |
 3 |  4  0  0  0 |
*/

console.log("Arête 2→0 existe ?", graphe.existeArete(2, 0)); // false
console.log("Arête 3→0 existe ?", graphe.existeArete(3, 0)); // true
```

</details>

---

### Analyse de Complexité : Matrice d'Adjacence

| Opération           | Complexité | Explication                    |
| ------------------- | ---------- | ------------------------------ |
| **Espace**          | O(V²)      | Matrice V × V stockée          |
| **Ajouter arête**   | O(1)       | Accès direct matrice[i][j]     |
| **Supprimer arête** | O(1)       | Accès direct matrice[i][j] = 0 |
| **Vérifier arête**  | O(1)       | Accès direct matrice[i][j]     |
| **Obtenir voisins** | O(V)       | Parcourir toute la ligne       |
| **Compter arêtes**  | O(V²)      | Parcourir toute la matrice     |

---

### Quand Utiliser la Matrice d'Adjacence ?

**Recommandée pour :**

- Graphes **denses** (beaucoup d'arêtes)
- Vérifications fréquentes d'**existence d'arêtes**
- Nombre de sommets **fixe et connu**
- Algorithmes nécessitant un accès O(1) aux arêtes

**À éviter pour :**

- Graphes **creux** (peu d'arêtes)
- Graphes avec **beaucoup de sommets** (espace O(V²))
- Ajout/suppression dynamique de sommets

---

## 💻 Implémentation 2 : Liste d'Adjacence

La **liste d'adjacence** représente chaque sommet avec la liste de ses voisins.

---

### Rappel du Fonctionnement

```
Même graphe avec arêtes (0,1), (0,2), (1,2), (2,3) :

0: [1, 2]      → sommet 0 connecté à 1 et 2
1: [0, 2]      → sommet 1 connecté à 0 et 2
2: [0, 1, 3]   → sommet 2 connecté à 0, 1 et 3
3: [2]         → sommet 3 connecté à 2 seulement
```

**Avantage :** On ne stocke que les arêtes qui existent réellement !

---

### Classe Complète : GrapheListeAdjacence

```javascript
/**
 * Représente un graphe via une Liste d'Adjacence.
 * Supporte les graphes orientés/non orientés et pondérés/non pondérés.
 * Accepte des sommets de tout type (nombres, chaînes, objets).
 */
class GrapheListeAdjacence {
  /**
   * Crée un nouveau graphe.
   * @param {boolean} oriente - True si le graphe est orienté.
   */
  constructor(oriente = false) {
    this.oriente = oriente;
    // Map : sommet → tableau de {voisin, poids}
    this.listeAdjacence = new Map();
  }

  /**
   * Ajoute un sommet au graphe.
   * @param {any} sommet - Le sommet à ajouter.
   * @returns {boolean} - True si ajouté (false si existait déjà).
   */
  ajouterSommet(sommet) {
    if (this.listeAdjacence.has(sommet)) {
      return false; // Sommet existe déjà
    }
    this.listeAdjacence.set(sommet, []);
    return true;
  }

  /**
   * Supprime un sommet et toutes ses arêtes.
   * @param {any} sommet - Le sommet à supprimer.
   * @returns {boolean} - True si supprimé.
   */
  supprimerSommet(sommet) {
    if (!this.listeAdjacence.has(sommet)) {
      return false;
    }

    // Supprimer toutes les arêtes pointant vers ce sommet
    for (const [s, voisins] of this.listeAdjacence) {
      this.listeAdjacence.set(
        s,
        voisins.filter((v) => v.voisin !== sommet),
      );
    }

    // Supprimer le sommet lui-même
    this.listeAdjacence.delete(sommet);
    return true;
  }

  /**
   * Ajoute une arête entre deux sommets.
   * Crée les sommets s'ils n'existent pas.
   * @param {any} source - Sommet source.
   * @param {any} destination - Sommet destination.
   * @param {number} poids - Poids de l'arête (1 par défaut).
   * @returns {boolean} - True si ajouté.
   */
  ajouterArete(source, destination, poids = 1) {
    // S'assurer que les deux sommets existent
    this.ajouterSommet(source);
    this.ajouterSommet(destination);

    // Ajouter l'arête source → destination
    this.listeAdjacence.get(source).push({
      voisin: destination,
      poids: poids,
    });

    // Si non orienté, ajouter aussi destination → source
    if (!this.oriente) {
      this.listeAdjacence.get(destination).push({
        voisin: source,
        poids: poids,
      });
    }

    return true;
  }

  /**
   * Supprime une arête entre deux sommets.
   * @param {any} source - Sommet source.
   * @param {any} destination - Sommet destination.
   * @returns {boolean} - True si supprimé.
   */
  supprimerArete(source, destination) {
    if (!this.listeAdjacence.has(source)) {
      return false;
    }

    // Filtrer pour enlever l'arête
    const voisinsSource = this.listeAdjacence.get(source);
    const indexSource = voisinsSource.findIndex(
      (v) => v.voisin === destination,
    );

    if (indexSource === -1) {
      return false; // Arête n'existe pas
    }

    voisinsSource.splice(indexSource, 1);

    // Si non orienté, supprimer aussi dans l'autre sens
    if (!this.oriente && this.listeAdjacence.has(destination)) {
      const voisinsDest = this.listeAdjacence.get(destination);
      const indexDest = voisinsDest.findIndex((v) => v.voisin === source);
      if (indexDest !== -1) {
        voisinsDest.splice(indexDest, 1);
      }
    }

    return true;
  }

  /**
   * Vérifie si une arête existe.
   * @param {any} source - Sommet source.
   * @param {any} destination - Sommet destination.
   * @returns {boolean} - True si l'arête existe.
   */
  existeArete(source, destination) {
    if (!this.listeAdjacence.has(source)) {
      return false;
    }
    return this.listeAdjacence
      .get(source)
      .some((v) => v.voisin === destination);
  }

  /**
   * Obtient le poids d'une arête.
   * @param {any} source - Sommet source.
   * @param {any} destination - Sommet destination.
   * @returns {number|null} - Le poids ou null si pas d'arête.
   */
  obtenirPoids(source, destination) {
    if (!this.listeAdjacence.has(source)) {
      return null;
    }
    const arete = this.listeAdjacence
      .get(source)
      .find((v) => v.voisin === destination);
    return arete ? arete.poids : null;
  }

  /**
   * Retourne tous les voisins d'un sommet.
   * @param {any} sommet - Le sommet.
   * @returns {Array} - Liste des voisins avec leurs poids.
   */
  obtenirVoisins(sommet) {
    return this.listeAdjacence.get(sommet) || [];
  }

  /**
   * Retourne uniquement les identifiants des voisins (sans poids).
   * @param {any} sommet - Le sommet.
   * @returns {Array} - Liste des voisins.
   */
  obtenirVoisinsSimple(sommet) {
    const voisins = this.listeAdjacence.get(sommet);
    return voisins ? voisins.map((v) => v.voisin) : [];
  }

  /**
   * Calcule le degré d'un sommet.
   * @param {any} sommet - Le sommet.
   * @returns {number} - Le degré (nombre de voisins).
   */
  obtenirDegre(sommet) {
    const voisins = this.listeAdjacence.get(sommet);
    return voisins ? voisins.length : 0;
  }

  /**
   * Retourne tous les sommets du graphe.
   * @returns {Array} - Liste des sommets.
   */
  obtenirSommets() {
    return Array.from(this.listeAdjacence.keys());
  }

  /**
   * Compte le nombre de sommets.
   * @returns {number} - Nombre de sommets.
   */
  nombreSommets() {
    return this.listeAdjacence.size;
  }

  /**
   * Compte le nombre d'arêtes.
   * @returns {number} - Nombre d'arêtes.
   */
  nombreAretes() {
    let count = 0;
    for (const voisins of this.listeAdjacence.values()) {
      count += voisins.length;
    }
    // Pour un graphe non orienté, diviser par 2
    return this.oriente ? count : count / 2;
  }

  /**
   * Affiche la liste d'adjacence.
   */
  afficher() {
    console.log("Liste d'Adjacence :");
    for (const [sommet, voisins] of this.listeAdjacence) {
      const voisinsStr = voisins
        .map((v) => {
          return v.poids !== 1 ? `${v.voisin}(${v.poids})` : String(v.voisin);
        })
        .join(", ");
      console.log(`  ${sommet}: [${voisinsStr}]`);
    }
  }
}
```

---

### Exemples d'Utilisation

#### Exemple 1 : Réseau Social (Non Orienté)

```javascript
// Réseau d'amitié (non orienté)
const reseauAmis = new GrapheListeAdjacence();

// Ajouter des amitiés
reseauAmis.ajouterArete("Chermann", "Ingrid");
reseauAmis.ajouterArete("Chermann", "Prudence");
reseauAmis.ajouterArete("Chermann", "Germain");
reseauAmis.ajouterArete("Ingrid", "Germain");
reseauAmis.ajouterArete("Prudence", "Germain");

reseauAmis.afficher();
/*
Liste d'Adjacence :
  Chermann: [Ingrid, Prudence, Germain]
  Ingrid: [Chermann, Germain]
  Prudence: [Chermann, Germain]
  Germain: [Chermann, Ingrid, Prudence]
*/

console.log("Amis de Chermann :", reseauAmis.obtenirVoisinsSimple("Chermann"));
// ["Ingrid", "Prudence", "Germain"]

console.log("Nombre d'amis de Germain :", reseauAmis.obtenirDegre("Germain")); // 3

console.log(
  "Chermann et Ingrid amis ?",
  reseauAmis.existeArete("Chermann", "Ingrid"),
); // true
console.log(
  "Ingrid et Prudence amis ?",
  reseauAmis.existeArete("Ingrid", "Prudence"),
); // false
```

#### Exemple 2 : Abonnements TikTok (Orienté)

```javascript
// Abonnements TikTok (orienté : suivre ≠ être suivi)
const TikTok = new GrapheListeAdjacence(true); // orienté

// Chermann suit Ingrid et Prudence
TikTok.ajouterArete("Chermann", "Ingrid");
TikTok.ajouterArete("Chermann", "Prudence");

// Ingrid suit Chermann et Germain
TikTok.ajouterArete("Ingrid", "Chermann");
TikTok.ajouterArete("Ingrid", "Germain");

// Prudence ne suit personne de ce groupe

TikTok.afficher();
/*
Liste d'Adjacence :
  Chermann: [Ingrid, Prudence]
  Ingrid: [Chermann, Germain]
  Prudence: []
  Germain: []
*/

console.log("Chermann suit Ingrid ?", TikTok.existeArete("Chermann", "Ingrid")); // true
console.log("Ingrid suit Chermann ?", TikTok.existeArete("Ingrid", "Chermann")); // true
console.log(
  "Chermann suit Germain ?",
  TikTok.existeArete("Chermann", "Germain"),
); // false
console.log(
  "Prudence suit Chermann ?",
  TikTok.existeArete("Prudence", "Chermann"),
); // false
```

#### Exemple 3 : Réseau Routier Belge (Pondéré)

```javascript
// Distances entre villes belges (km)
const routesBelgique = new GrapheListeAdjacence();

routesBelgique.ajouterArete("Bruxelles", "Anvers", 50);
routesBelgique.ajouterArete("Bruxelles", "Gand", 55);
routesBelgique.ajouterArete("Bruxelles", "Liège", 100);
routesBelgique.ajouterArete("Anvers", "Gand", 60);
routesBelgique.ajouterArete("Anvers", "Liège", 120);
routesBelgique.ajouterArete("Gand", "Bruges", 50);

routesBelgique.afficher();
/*
Liste d'Adjacence :
  Bruxelles: [Anvers(50), Gand(55), Liège(100)]
  Anvers: [Bruxelles(50), Gand(60), Liège(120)]
  Gand: [Bruxelles(55), Anvers(60), Bruges(50)]
  Liège: [Bruxelles(100), Anvers(120)]
  Bruges: [Gand(50)]
*/

console.log(
  "Voisins de Bruxelles :",
  routesBelgique.obtenirVoisins("Bruxelles"),
);
// [{voisin: "Anvers", poids: 50}, {voisin: "Gand", poids: 55}, {voisin: "Liège", poids: 100}]

console.log(
  "Distance Bruxelles-Gand :",
  routesBelgique.obtenirPoids("Bruxelles", "Gand"),
  "km",
); // 55 km
console.log(
  "Distance Bruxelles-Bruges :",
  routesBelgique.obtenirPoids("Bruxelles", "Bruges"),
); // null
```

---

## 📝 Micro-Exercice #2 : Liste d'Adjacence

**Objectif :** Manipuler une liste d'adjacence avec suppression.

**Instructions :**

1. Créez le réseau d'amis de l'exemple 1
2. Supprimez l'amitié entre Chermann et Prudence
3. Vérifiez que l'arête n'existe plus dans les deux sens

<details>
<summary>💡 Voir la solution</summary>

```javascript
const reseau = new GrapheListeAdjacence();
reseau.ajouterArete("Chermann", "Ingrid");
reseau.ajouterArete("Chermann", "Prudence");
reseau.ajouterArete("Chermann", "Germain");

console.log("Avant suppression :");
reseau.afficher();
console.log("Chermann-Prudence ?", reseau.existeArete("Chermann", "Prudence")); // true

// Supprimer l'amitié
reseau.supprimerArete("Chermann", "Prudence");

console.log("\nAprès suppression :");
reseau.afficher();
console.log("Chermann-Prudence ?", reseau.existeArete("Chermann", "Prudence")); // false
console.log("Prudence-Chermann ?", reseau.existeArete("Prudence", "Chermann")); // false
```

</details>

---

### Analyse de Complexité : Liste d'Adjacence

| Opération           | Complexité | Explication                          |
| ------------------- | ---------- | ------------------------------------ |
| **Espace**          | O(V + E)   | Stocke chaque sommet et chaque arête |
| **Ajouter sommet**  | O(1)       | Ajout dans la Map                    |
| **Ajouter arête**   | O(1)       | Push dans le tableau                 |
| **Supprimer arête** | O(deg(v))  | Parcourir les voisins                |
| **Vérifier arête**  | O(deg(v))  | Parcourir les voisins                |
| **Obtenir voisins** | O(1)       | Accès direct au tableau              |
| **Compter arêtes**  | O(V + E)   | Parcourir tous les tableaux          |

> **Note :** deg(v) = degré du sommet v = nombre de voisins

---

### Quand Utiliser la Liste d'Adjacence ?

**Recommandée pour :**

- Graphes **creux** (sparse) - peu d'arêtes
- Graphes avec **beaucoup de sommets**
- Parcours fréquents des **voisins** (BFS, DFS)
- Ajout/suppression dynamique de **sommets**
- Sommets de **types variés** (chaînes, objets)

**À éviter pour :**

- Vérifications très fréquentes d'**existence d'arêtes** (O(deg) vs O(1))
- Graphes très **denses** où deg(v) ≈ V

---

## 📊 Comparaison Détaillée des Deux Représentations

### Tableau Comparatif

| Critère             | Matrice d'Adjacence | Liste d'Adjacence |
| ------------------- | ------------------- | ----------------- |
| **Espace**          | O(V²)               | O(V + E)          |
| **Ajouter arête**   | O(1)                | O(1)              |
| **Supprimer arête** | O(1)                | O(deg(v))         |
| **Vérifier arête**  | O(1)                | O(deg(v))         |
| **Obtenir voisins** | O(V)                | O(deg(v))         |
| **Ajouter sommet**  | O(V²)               | O(1)              |
| **Type de sommets** | Indices numériques  | Tout type         |
| **Graphe dense**    | Idéal               | Acceptable        |
| **Graphe creux**    | Gaspillage          | Idéal             |

---

### Visualisation : Graphe Dense vs Creux

```
GRAPHE DENSE (100 sommets, ~5000 arêtes)
E ≈ V² / 2

Matrice : 100 × 100 = 10 000 cellules
Liste   : 100 sommets + 5 000 arêtes = ~5 100 entrées

→ Matrice légèrement meilleure pour les lookups O(1)


GRAPHE CREUX (100 sommets, ~200 arêtes)
E << V²

Matrice : 100 × 100 = 10 000 cellules (98% vides !)
Liste   : 100 sommets + 200 arêtes = ~300 entrées

→ Liste 30x plus efficace en mémoire !
```

---

## 📝 Micro-Exercice #3 : Choisir la Bonne Représentation

**Objectif :** Développer l'intuition pour le choix de structure.

**Instructions :** Pour chaque scénario, quelle représentation choisiriez-vous ?

1. Facebook : 2 milliards d'utilisateurs, chacun ayant ~150 amis en moyenne
2. Jeu d'échecs : 64 cases, chaque case peut atteindre ~8 cases
3. Système GPS : Calcul de routes entre toutes les villes d'un pays

<details>
<summary>💡 Voir la solution</summary>

1. **Facebook** : **Liste d'Adjacence**
   - V = 2 milliards, E ≈ 150 milliards
   - Matrice : 4×10¹⁸ cellules → **impossible**
   - Liste : 2×10⁹ + 150×10⁹ entrées → **faisable**
   - Graphe très creux (150 amis << 2 milliards possibles)

2. **Jeu d'échecs** : **Matrice d'Adjacence**
   - V = 64, donc matrice 64×64 = 4 096 cellules
   - Petit graphe fixe
   - Vérifications fréquentes "ce mouvement est-il légal ?" → O(1)

3. **Système GPS** : **Liste d'Adjacence**
   - Milliers de villes, mais chaque ville connectée à ~5-10 autres
   - Graphe creux
   - Besoin de parcourir les voisins pour Dijkstra → Liste idéale

</details>

---

## 💼 Application : Étude de Cas - Planificateur de Trajets

Construisons un planificateur de trajets utilisant nos implémentations.

---

### Scénario

Destinée développe une application de planification de trajets en Belgique. Elle doit :

1. Stocker les routes entre les villes avec leurs distances
2. Trouver les villes accessibles depuis une ville donnée
3. Calculer la distance directe entre deux villes

---

### Implémentation avec Liste d'Adjacence

```javascript
/**
 * Planificateur de trajets pour la Belgique.
 */
class PlanificateurTrajets {
  constructor() {
    this.graphe = new GrapheListeAdjacence();
  }

  /**
   * Ajoute une route bidirectionnelle entre deux villes.
   * @param {string} villeA - Première ville.
   * @param {string} villeB - Deuxième ville.
   * @param {number} distance - Distance en km.
   */
  ajouterRoute(villeA, villeB, distance) {
    this.graphe.ajouterArete(villeA, villeB, distance);
  }

  /**
   * Retourne toutes les villes du réseau.
   * @returns {string[]} - Liste des villes.
   */
  obtenirVilles() {
    return this.graphe.obtenirSommets();
  }

  /**
   * Retourne les villes directement accessibles depuis une ville.
   * @param {string} ville - La ville de départ.
   * @returns {Array<{ville: string, distance: number}>}
   */
  obtenirDestinations(ville) {
    const voisins = this.graphe.obtenirVoisins(ville);
    return voisins.map((v) => ({
      ville: v.voisin,
      distance: v.poids,
    }));
  }

  /**
   * Obtient la distance directe entre deux villes.
   * @param {string} villeA - Ville de départ.
   * @param {string} villeB - Ville d'arrivée.
   * @returns {number|null} - Distance ou null si pas de route directe.
   */
  obtenirDistance(villeA, villeB) {
    return this.graphe.obtenirPoids(villeA, villeB);
  }

  /**
   * Vérifie si deux villes sont directement connectées.
   * @param {string} villeA - Première ville.
   * @param {string} villeB - Deuxième ville.
   * @returns {boolean}
   */
  sontConnectees(villeA, villeB) {
    return this.graphe.existeArete(villeA, villeB);
  }

  /**
   * Affiche le réseau routier.
   */
  afficherReseau() {
    console.log("=== Réseau Routier de Belgique ===\n");
    for (const ville of this.obtenirVilles()) {
      const destinations = this.obtenirDestinations(ville);
      console.log(`📍 ${ville} :`);
      destinations.forEach((d) => {
        console.log(`   → ${d.ville} : ${d.distance} km`);
      });
      console.log();
    }
  }
}

// Utilisation
const belgique = new PlanificateurTrajets();

// Ajouter les routes principales
belgique.ajouterRoute("Bruxelles", "Anvers", 50);
belgique.ajouterRoute("Bruxelles", "Gand", 55);
belgique.ajouterRoute("Bruxelles", "Liège", 100);
belgique.ajouterRoute("Bruxelles", "Namur", 65);
belgique.ajouterRoute("Anvers", "Gand", 60);
belgique.ajouterRoute("Anvers", "Liège", 120);
belgique.ajouterRoute("Gand", "Bruges", 50);
belgique.ajouterRoute("Namur", "Liège", 65);
belgique.ajouterRoute("Bruges", "Ostende", 25);

belgique.afficherReseau();

// Requêtes
console.log("=== Requêtes ===");
console.log("\nDestinations depuis Bruxelles :");
belgique.obtenirDestinations("Bruxelles").forEach((d) => {
  console.log(`  - ${d.ville} (${d.distance} km)`);
});

console.log(
  "\nBruxelles ↔ Bruges directement ?",
  belgique.sontConnectees("Bruxelles", "Bruges"),
); // false
console.log(
  "Gand ↔ Bruges directement ?",
  belgique.sontConnectees("Gand", "Bruges"),
); // true
console.log(
  "Distance Bruxelles → Anvers :",
  belgique.obtenirDistance("Bruxelles", "Anvers"),
  "km",
); // 50
```

---

### Sortie du Programme

```
=== Réseau Routier de Belgique ===

📍 Bruxelles :
   → Anvers : 50 km
   → Gand : 55 km
   → Liège : 100 km
   → Namur : 65 km

📍 Anvers :
   → Bruxelles : 50 km
   → Gand : 60 km
   → Liège : 120 km

📍 Gand :
   → Bruxelles : 55 km
   → Anvers : 60 km
   → Bruges : 50 km

📍 Liège :
   → Bruxelles : 100 km
   → Anvers : 120 km
   → Namur : 65 km

📍 Namur :
   → Bruxelles : 65 km
   → Liège : 65 km

📍 Bruges :
   → Gand : 50 km
   → Ostende : 25 km

📍 Ostende :
   → Bruges : 25 km

=== Requêtes ===

Destinations depuis Bruxelles :
  - Anvers (50 km)
  - Gand (55 km)
  - Liège (100 km)
  - Namur (65 km)

Bruxelles ↔ Bruges directement ? false
Gand ↔ Bruges directement ? true
Distance Bruxelles → Anvers : 50 km
```

---

## 💪 Exercices Pratiques

Consolidez vos connaissances avec ces exercices progressifs.

---

### Exercice 1 : Méthode getDegre pour la Matrice

**Objectif :** Ajouter une méthode pour calculer les degrés entrant et sortant dans un graphe orienté.

**Instructions :** Ajoutez les méthodes `obtenirDegreSortant(sommet)` et `obtenirDegreEntrant(sommet)` à la classe `GrapheMatriceAdjacence`.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Calcule le degré sortant (nombre d'arêtes partant du sommet).
 */
obtenirDegreSortant(sommet) {
  if (!this._estSommetValide(sommet)) return 0;

  let degre = 0;
  for (let j = 0; j < this.nombreSommets; j++) {
    if (this.matrice[sommet][j] !== 0) {
      degre++;
    }
  }
  return degre;
}

/**
 * Calcule le degré entrant (nombre d'arêtes arrivant au sommet).
 */
obtenirDegreEntrant(sommet) {
  if (!this._estSommetValide(sommet)) return 0;

  let degre = 0;
  for (let i = 0; i < this.nombreSommets; i++) {
    if (this.matrice[i][sommet] !== 0) {
      degre++;
    }
  }
  return degre;
}

// Test
const g = new GrapheMatriceAdjacence(3, true);
g.ajouterArete(0, 1);
g.ajouterArete(0, 2);
g.ajouterArete(1, 2);

console.log("Degré sortant de 0 :", g.obtenirDegreSortant(0)); // 2
console.log("Degré entrant de 2 :", g.obtenirDegreEntrant(2)); // 2
```

</details>

---

### Exercice 2 : Conversion Matrice → Liste

**Objectif :** Écrire une fonction qui convertit une matrice d'adjacence en liste d'adjacence.

**Instructions :** Créez une fonction `convertirMatriceEnListe(grapheMatrice)` qui prend un `GrapheMatriceAdjacence` et retourne un `GrapheListeAdjacence` équivalent.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function convertirMatriceEnListe(grapheMatrice) {
  const grapheListe = new GrapheListeAdjacence(grapheMatrice.oriente);

  // Ajouter tous les sommets
  for (let i = 0; i < grapheMatrice.nombreSommets; i++) {
    grapheListe.ajouterSommet(i);
  }

  // Ajouter les arêtes
  for (let i = 0; i < grapheMatrice.nombreSommets; i++) {
    for (let j = 0; j < grapheMatrice.nombreSommets; j++) {
      const poids = grapheMatrice.matrice[i][j];
      if (poids !== 0) {
        // Pour non orienté, éviter les doublons (ne traiter que i < j)
        if (grapheMatrice.oriente || i < j) {
          grapheListe.ajouterArete(i, j, poids);
        }
      }
    }
  }

  return grapheListe;
}

// Test
const matrice = new GrapheMatriceAdjacence(3);
matrice.ajouterArete(0, 1, 5);
matrice.ajouterArete(1, 2, 3);

console.log("Matrice originale :");
matrice.afficher();

const liste = convertirMatriceEnListe(matrice);
console.log("\nListe convertie :");
liste.afficher();
```

</details>

---

### Exercice 3 : Trouver les Sommets Isolés

**Objectif :** Identifier les sommets sans aucune connexion.

**Instructions :** Ajoutez une méthode `obtenirSommetsIsoles()` à la classe `GrapheListeAdjacence` qui retourne tous les sommets de degré 0.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Retourne tous les sommets sans connexion.
 * @returns {Array} - Liste des sommets isolés.
 */
obtenirSommetsIsoles() {
  const isoles = [];

  for (const [sommet, voisins] of this.listeAdjacence) {
    if (voisins.length === 0) {
      // Vérifier aussi que personne ne pointe vers ce sommet (pour orienté)
      let estIsole = true;
      if (this.oriente) {
        for (const [s, v] of this.listeAdjacence) {
          if (v.some(voisin => voisin.voisin === sommet)) {
            estIsole = false;
            break;
          }
        }
      }
      if (estIsole) {
        isoles.push(sommet);
      }
    }
  }

  return isoles;
}

// Test
const g = new GrapheListeAdjacence();
g.ajouterSommet("A");
g.ajouterSommet("B");
g.ajouterSommet("C"); // Isolé
g.ajouterArete("A", "B");

console.log("Sommets isolés :", g.obtenirSommetsIsoles()); // ["C"]
```

</details>

---

### Exercice 4 : Graphe Complet

**Objectif :** Créer une fonction qui génère un graphe complet (tous les sommets connectés).

**Instructions :** Écrivez `creerGrapheComplet(n)` qui crée un graphe non orienté où chaque sommet est connecté à tous les autres.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function creerGrapheComplet(n) {
  const graphe = new GrapheListeAdjacence();

  // Ajouter tous les sommets
  for (let i = 0; i < n; i++) {
    graphe.ajouterSommet(i);
  }

  // Connecter chaque paire de sommets
  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j < n; j++) {
      graphe.ajouterArete(i, j);
    }
  }

  return graphe;
}

// Test
const k4 = creerGrapheComplet(4);
k4.afficher();
/*
Liste d'Adjacence :
  0: [1, 2, 3]
  1: [0, 2, 3]
  2: [0, 1, 3]
  3: [0, 1, 2]
*/

console.log("Nombre d'arêtes K4 :", k4.nombreAretes()); // 6 (formule : n(n-1)/2)
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la complexité spatiale d'une matrice d'adjacence pour un graphe de 100 sommets ?**

- [ ] A. O(100)
- [ ] B. O(200)
- [ ] C. O(1 000)
- [ ] D. O(10 000)

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

La matrice d'adjacence a une complexité spatiale de **O(V²)**. Pour V = 100, c'est 100² = **10 000** cellules.

</details>

---

### Question 2

**Quelle opération est plus rapide avec une matrice qu'avec une liste d'adjacence ?**

- [ ] A. Parcourir tous les voisins
- [ ] B. Vérifier si une arête existe
- [ ] C. Ajouter un nouveau sommet
- [ ] D. Compter le nombre total de sommets

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Vérifier si une arête existe est **O(1)** avec une matrice (accès direct `matrice[i][j]`) contre **O(deg(v))** avec une liste.

</details>

---

### Question 3

**Pour un graphe creux de 10 000 sommets et 50 000 arêtes, quelle représentation est la plus efficace en mémoire ?**

- [ ] A. Matrice d'adjacence
- [ ] B. Liste d'adjacence
- [ ] C. Les deux sont équivalentes
- [ ] D. Impossible à déterminer

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

- Matrice : 10 000² = **100 millions** de cellules
- Liste : 10 000 + 50 000 = **60 000** entrées

La liste est environ **1 600 fois** plus efficace !

</details>

---

### Question 4

**Dans une liste d'adjacence pour un graphe non orienté, si A est voisin de B, alors :**

- [ ] A. B n'est pas forcément voisin de A
- [ ] B. B est automatiquement voisin de A
- [ ] C. On doit ajouter manuellement B→A
- [ ] D. L'arête est stockée une seule fois

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Dans un graphe **non orienté**, l'arête est bidirectionnelle. Notre implémentation ajoute automatiquement B dans la liste de A ET A dans la liste de B.

</details>

---

### Question 5

**Quelle est la complexité pour supprimer une arête dans une liste d'adjacence ?**

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(deg(v))
- [ ] D. O(V)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Pour supprimer une arête, il faut parcourir la liste des voisins du sommet source pour trouver l'arête à supprimer, ce qui prend **O(deg(v))** où deg(v) est le degré du sommet.

</details>

---

### Question 6

**Quel type de graphe convient le mieux à une matrice d'adjacence ?**

- [ ] A. Un graphe creux avec des millions de sommets
- [ ] B. Un réseau social avec des milliards d'utilisateurs
- [ ] C. Un petit graphe dense avec des vérifications fréquentes d'arêtes
- [ ] D. Un graphe dont les sommets sont des chaînes de caractères

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La matrice excelle pour les **petits graphes denses** avec des **vérifications O(1)** fréquentes. Les autres options nécessitent une liste d'adjacence.

</details>

---

### Question 7

**Quelle structure JavaScript est utilisée dans notre classe GrapheListeAdjacence pour stocker les voisins ?**

- [ ] A. Array de nombres
- [ ] B. Map de sommets → Array d'objets {voisin, poids}
- [ ] C. Object avec des propriétés
- [ ] D. Set de tuples

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Nous utilisons un **Map** où chaque clé est un sommet et la valeur est un **Array d'objets** `{voisin, poids}`. Cela permet des sommets de tout type et supporte les graphes pondérés.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Matrice d'Adjacence

Tableau 2D de taille V×V. Vérification d'arête en O(1), mais espace O(V²).

### 2. Liste d'Adjacence

Map de sommets vers tableaux de voisins. Espace O(V+E), idéal pour graphes creux.

### 3. Choix de Représentation

Dense + vérifications fréquentes → Matrice. Creux + parcours → Liste.

### 4. Graphes Orientés

Dans les deux représentations, les arêtes ont une direction (A→B ≠ B→A).

### 5. Graphes Pondérés

Matrice : stocker le poids dans la cellule. Liste : objets {voisin, poids}.

### 6. Opérations Clés

Ajouter/supprimer arête, vérifier existence, obtenir voisins, calculer degré.

### 7. Applications Réelles

Routes (pondéré), réseaux sociaux (creux), dépendances (orienté).

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant les deux implémentations de graphes !

### Ce que vous avez appris aujourd'hui

- Implémentation complète de la **matrice d'adjacence**
- Implémentation complète de la **liste d'adjacence**
- Gestion des graphes **orientés, non orientés et pondérés**
- Analyse de **complexité** de chaque opération
- **Critères de choix** entre les deux représentations
- Application à un **cas réel** (planificateur de trajets)

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter des graphes **robustes et réutilisables**
- Choisir la **représentation optimale** selon le contexte
- Manipuler des graphes (ajout, suppression, recherche)

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Ces implémentations sont la **fondation** des algorithmes de graphes. BFS, DFS, Dijkstra, et bien d'autres algorithmes dépendent directement de l'efficacité de ces opérations. Maîtriser ces structures vous prépare à résoudre des problèmes complexes comme la recherche de chemin, la détection de cycles, ou l'ordonnancement de tâches.

---

## ➡️ Prochaine Étape : Leçon 29

### Ce qui vous attend

La prochaine leçon, **« Algorithme de Parcours en Largeur (BFS) en JavaScript »**, vous apprendra à explorer systématiquement tous les sommets d'un graphe niveau par niveau.

**Vous découvrirez :**

- Le principe du **Breadth-First Search**
- L'utilisation d'une **file** (queue) pour le BFS
- Comment trouver le **chemin le plus court** (non pondéré)
- L'implémentation utilisant notre `GrapheListeAdjacence`

### Préparez-vous !

Le BFS est un algorithme fondamental utilisé dans les GPS, les réseaux sociaux (degrés de séparation), et les jeux vidéo (pathfinding). Vous utiliserez directement les classes créées dans cette leçon !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Graph Structures](https://visualgo.net/en/graphds) - Visualisation interactive
- [MDN - Map](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Map) - Documentation Map JavaScript
- [CS Dojo - Graph Data Structures](https://www.youtube.com/watch?v=gXgEDyodOJU) - Tutoriel vidéo

### Code source

Les classes complètes de cette leçon peuvent être réutilisées dans vos projets. Elles sont conçues pour être :

- **Flexibles** : Support de différents types de sommets
- **Robustes** : Validation des entrées
- **Efficaces** : Complexités optimisées

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Tester les exemples dans votre console
- Modifier les classes pour ajouter de nouvelles fonctionnalités

> 💡 **Conseil**
>
> Le meilleur moyen d'apprendre est de **coder** ! Créez votre propre graphe (votre réseau d'amis, les stations de métro de votre ville, etc.) et testez toutes les opérations. Essayez de convertir entre les deux représentations pour bien comprendre leurs différences.

---

**Prêt pour la Leçon 29 ?** 🚀

Rendez-vous dans la prochaine leçon pour apprendre le parcours en largeur (BFS) !

---

<div align="center">

**Leçon 28 sur 42 - Module 5 : Arbres et Parcours de Graphes**

[⬅️ Leçon 27 : Graphes - Concepts et Représentations](./lecon-3-graphes-concepts-sommets-aretes-representations.md) | [Retour au sommaire](./README.md) | [Leçon 29 : Parcours en Largeur (BFS) ➡️](./lecon-5-algorithme-parcours-largeur-bfs-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
