##### Leçon 27 sur 42

# Graphes : Concepts, Sommets, Arêtes et Représentations

**Module 5** : Arbres et Parcours de Graphes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre la **définition** et les **composants** d'un graphe (sommets et arêtes)
- Distinguer les graphes **orientés** et **non orientés**
- Comprendre le concept d'**arêtes pondérées**
- Implémenter une **matrice d'adjacence** en JavaScript
- Implémenter une **liste d'adjacence** en JavaScript
- Choisir la **représentation appropriée** selon le contexte

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 26 complétée** : Arbres de Recherche Binaires
- **Tableaux 2D** : Manipuler des matrices en JavaScript
- **Objets JavaScript** : Utiliser des objets comme dictionnaires
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Au-delà des Arbres

Dans les leçons précédentes, vous avez découvert les **arbres**, des structures hiérarchiques où chaque nœud a un parent unique (sauf la racine). Mais que faire quand les relations ne sont pas hiérarchiques ?

Pensez à vos **réseaux sociaux** : vos amis ne sont pas organisés en hiérarchie ! Chermann peut être ami avec Ingrid et Prudence, et Ingrid peut aussi être amie avec Prudence, formant un **triangle** de relations. Les arbres ne peuvent pas représenter cela.

C'est là qu'interviennent les **graphes** : une structure plus générale qui permet de modéliser **n'importe quelle relation** entre des éléments.

> **Point Clé**
>
> Un **arbre est un cas particulier de graphe** (un graphe connexe sans cycles). Les graphes généralisent les arbres en permettant des cycles, plusieurs chemins entre deux nœuds, et des connexions multiples.

---

## 📦 Définition et Composants d'un Graphe

Un graphe est défini par deux ensembles : les **sommets** et les **arêtes**.

---

### Les Sommets (Vertices ou Nœuds)

Les **sommets** représentent les entités individuelles du graphe. Chaque sommet peut contenir des données.

```
Exemples de sommets :
• Réseau social → Chaque personne est un sommet
• Carte routière → Chaque ville est un sommet
• Réseau informatique → Chaque ordinateur est un sommet
• Site web → Chaque page est un sommet
```

**Notation :** On utilise souvent V (de _Vertex_) pour désigner l'ensemble des sommets. |V| représente le nombre de sommets.

---

### Les Arêtes (Edges ou Liens)

Les **arêtes** représentent les connexions entre les sommets. Une arête relie toujours **deux sommets**.

```
Exemples d'arêtes :
• Réseau social → L'amitié entre deux personnes
• Carte routière → La route entre deux villes
• Réseau informatique → Le câble entre deux ordinateurs
• Site web → Le lien hypertexte d'une page vers une autre
```

**Notation :** On utilise E (de _Edge_) pour désigner l'ensemble des arêtes. |E| représente le nombre d'arêtes.

---

### Visualisation : Graphe Simple

```
    [Chermann]---[Ingrid]
        |   \      /
        |    \    /
        |     \  /
    [Prudence]-[Germain]

Sommets (V) : {Chermann, Ingrid, Prudence, Germain}
Arêtes (E) : {(Chermann,Ingrid), (Chermann,Prudence),
              (Chermann,Germain), (Ingrid,Germain),
              (Prudence,Germain)}

|V| = 4 sommets
|E| = 5 arêtes
```

---

## 📊 Types d'Arêtes et de Graphes

La nature des arêtes détermine le type de graphe.

---

### Arêtes Non Orientées (Graphe Non Orienté)

Une arête **non orientée** est bidirectionnelle : si A est connecté à B, alors B est connecté à A.

```
Graphe Non Orienté :
    [A]----[B]

Si A est lié à B, alors B est lié à A.
La relation est SYMÉTRIQUE.
```

**Exemples concrets :**

- **Amitiés** : Si Chermann est ami avec Ingrid, Ingrid est amie avec Chermann
- **Routes** : Si une route va de Bruxelles à Anvers, on peut aussi aller d'Anvers à Bruxelles
- **Connexions Bluetooth** : Si appareil A est appairé à B, B est appairé à A

---

### Arêtes Orientées (Graphe Orienté / Digraphe)

Une arête **orientée** (ou arc) a une direction : A vers B n'implique pas B vers A.

```
Graphe Orienté (Digraphe) :
    [A]---->[B]

A pointe vers B (A→B)
Mais B NE POINTE PAS forcément vers A !
```

**Exemples concrets :**

- **Abonnements** : Chermann suit Ingrid sur Twitter, mais Ingrid ne suit pas forcément Chermann
- **Liens web** : La page "Accueil" contient un lien vers "Contact", mais "Contact" n'a pas forcément de lien vers "Accueil"
- **Prérequis** : Le cours CS101 est prérequis pour CS201, pas l'inverse

---

### Arêtes Pondérées (Graphe Pondéré)

Une arête peut avoir un **poids** (ou coût) qui représente une valeur numérique associée à la connexion.

```
Graphe Pondéré :
    [Bruxelles]--50km--[Anvers]
          \
           55km
            \
          [Gand]

Les arêtes ont des valeurs (distances, coûts, temps, etc.)
```

**Exemples concrets :**

- **Distance** : Kilomètres entre deux villes
- **Temps** : Minutes de trajet entre deux points
- **Coût** : Prix d'un billet d'avion entre deux aéroports
- **Bande passante** : Débit d'une connexion réseau

---

### Tableau Récapitulatif des Types

| Type de Graphe          | Arêtes             | Direction | Poids | Exemple             |
| ----------------------- | ------------------ | --------- | ----- | ------------------- |
| **Non orienté**         | Bidirectionnelles  | Non       | Non   | Amitiés Facebook    |
| **Orienté**             | Unidirectionnelles | Oui       | Non   | Abonnements Twitter |
| **Pondéré non orienté** | Bidirectionnelles  | Non       | Oui   | Carte routière      |
| **Pondéré orienté**     | Unidirectionnelles | Oui       | Oui   | Vols aériens        |

---

## 📝 Micro-Exercice #1 : Identifier les Types

**Objectif :** Reconnaître les types de graphes selon le contexte.

**Instructions :** Pour chaque scénario, identifiez si le graphe est orienté/non orienté et pondéré/non pondéré.

1. Un réseau de métro où chaque station est connectée aux adjacentes
2. Un flux de travail où certaines tâches dépendent d'autres
3. Un réseau de livraison avec le temps entre chaque point

<details>
<summary>💡 Voir la solution</summary>

1. **Réseau de métro** : **Non orienté, non pondéré** (on peut aller dans les deux sens, distance uniforme entre stations adjacentes)

2. **Flux de travail** : **Orienté, non pondéré** (Tâche A avant Tâche B → direction, pas de notion de "quantité")

3. **Réseau de livraison** : **Non orienté (ou orienté), pondéré** (temps de trajet = poids, la direction dépend si les routes sont à sens unique ou non)

</details>

---

## 💻 Représentation 1 : La Matrice d'Adjacence

Une **matrice d'adjacence** est un tableau 2D où chaque cellule indique s'il existe une arête entre deux sommets.

---

### Structure d'une Matrice d'Adjacence

Pour un graphe de V sommets, on crée une matrice V × V :

- `matrice[i][j] = 1` : Il existe une arête de i vers j
- `matrice[i][j] = 0` : Pas d'arête de i vers j

```
Exemple : Graphe avec 4 sommets et arêtes (0,1), (0,2), (1,2), (2,3)

      0   1   2   3
    +---+---+---+---+
  0 | 0 | 1 | 1 | 0 |
    +---+---+---+---+
  1 | 1 | 0 | 1 | 0 |
    +---+---+---+---+
  2 | 1 | 1 | 0 | 1 |
    +---+---+---+---+
  3 | 0 | 0 | 1 | 0 |
    +---+---+---+---+

matrice[0][1] = 1 → arête entre 0 et 1
matrice[0][3] = 0 → pas d'arête entre 0 et 3
```

---

### Propriétés Importantes

**Graphe Non Orienté :**

- La matrice est **symétrique** : `matrice[i][j] === matrice[j][i]`
- La diagonale est 0 (pas de boucles simples)

**Graphe Orienté :**

- La matrice peut être **asymétrique**
- `matrice[i][j] = 1` n'implique pas `matrice[j][i] = 1`

**Graphe Pondéré :**

- Au lieu de 1, on stocke le **poids** de l'arête
- `0` ou `Infinity` pour indiquer l'absence d'arête

---

### Implémentation en JavaScript

```javascript
/**
 * Classe représentant un graphe via une matrice d'adjacence.
 */
class GrapheMatrice {
  /**
   * Crée un graphe avec un nombre fixe de sommets.
   * @param {number} nombreSommets - Le nombre de sommets du graphe.
   * @param {boolean} oriente - True si le graphe est orienté.
   */
  constructor(nombreSommets, oriente = false) {
    this.nombreSommets = nombreSommets;
    this.oriente = oriente;
    // Créer une matrice V×V initialisée à 0
    this.matrice = [];
    for (let i = 0; i < nombreSommets; i++) {
      this.matrice.push(new Array(nombreSommets).fill(0));
    }
  }

  /**
   * Ajoute une arête entre deux sommets.
   * @param {number} source - Sommet source.
   * @param {number} destination - Sommet destination.
   * @param {number} poids - Poids de l'arête (1 par défaut).
   */
  ajouterArete(source, destination, poids = 1) {
    this.matrice[source][destination] = poids;
    // Si non orienté, ajouter aussi dans l'autre sens
    if (!this.oriente) {
      this.matrice[destination][source] = poids;
    }
  }

  /**
   * Vérifie s'il existe une arête entre deux sommets.
   * @param {number} source - Sommet source.
   * @param {number} destination - Sommet destination.
   * @returns {boolean} - True si l'arête existe.
   */
  existeArete(source, destination) {
    return this.matrice[source][destination] !== 0;
  }

  /**
   * Retourne les voisins d'un sommet.
   * @param {number} sommet - Le sommet dont on cherche les voisins.
   * @returns {number[]} - Liste des sommets voisins.
   */
  obtenirVoisins(sommet) {
    const voisins = [];
    for (let i = 0; i < this.nombreSommets; i++) {
      if (this.matrice[sommet][i] !== 0) {
        voisins.push(i);
      }
    }
    return voisins;
  }

  /**
   * Affiche la matrice d'adjacence.
   */
  afficher() {
    console.log("Matrice d'adjacence :");
    console.log(
      "   " +
        Array.from({ length: this.nombreSommets }, (_, i) => i).join("  "),
    );
    console.log("  +" + "---+".repeat(this.nombreSommets));
    for (let i = 0; i < this.nombreSommets; i++) {
      console.log(i + " | " + this.matrice[i].join("  ") + " |");
    }
  }
}

// Test : Graphe non orienté
const graphe = new GrapheMatrice(4);
graphe.ajouterArete(0, 1);
graphe.ajouterArete(0, 2);
graphe.ajouterArete(1, 2);
graphe.ajouterArete(2, 3);

graphe.afficher();
/*
   0  1  2  3
  +---+---+---+---+
0 | 0  1  1  0 |
1 | 1  0  1  0 |
2 | 1  1  0  1 |
3 | 0  0  1  0 |
*/

console.log("Arête entre 0 et 1 ?", graphe.existeArete(0, 1)); // true
console.log("Arête entre 0 et 3 ?", graphe.existeArete(0, 3)); // false
console.log("Voisins de 2 :", graphe.obtenirVoisins(2)); // [0, 1, 3]
```

---

### Avantages et Inconvénients

| Avantages                        | Inconvénients                         |
| -------------------------------- | ------------------------------------- |
| Vérification d'arête en **O(1)** | Espace **O(V²)** même si peu d'arêtes |
| Simple à implémenter             | Ajouter/supprimer un sommet coûteux   |
| Idéal pour graphes **denses**    | Inefficace pour graphes **creux**     |

---

## 💻 Représentation 2 : La Liste d'Adjacence

Une **liste d'adjacence** représente un graphe comme une collection de listes où chaque sommet a la liste de ses voisins.

---

### Structure d'une Liste d'Adjacence

Pour chaque sommet, on stocke la liste des sommets auxquels il est connecté :

```
Exemple : Même graphe avec arêtes (0,1), (0,2), (1,2), (2,3)

0: [1, 2]      → Sommet 0 est connecté à 1 et 2
1: [0, 2]      → Sommet 1 est connecté à 0 et 2
2: [0, 1, 3]   → Sommet 2 est connecté à 0, 1 et 3
3: [2]         → Sommet 3 est connecté à 2 seulement
```

---

### Implémentation en JavaScript

```javascript
/**
 * Classe représentant un graphe via une liste d'adjacence.
 */
class GrapheListe {
  /**
   * Crée un nouveau graphe.
   * @param {boolean} oriente - True si le graphe est orienté.
   */
  constructor(oriente = false) {
    this.oriente = oriente;
    // Map : sommet → liste de voisins
    this.listeAdjacence = new Map();
  }

  /**
   * Ajoute un sommet au graphe.
   * @param {string|number} sommet - Le sommet à ajouter.
   */
  ajouterSommet(sommet) {
    if (!this.listeAdjacence.has(sommet)) {
      this.listeAdjacence.set(sommet, []);
    }
  }

  /**
   * Ajoute une arête entre deux sommets.
   * @param {string|number} source - Sommet source.
   * @param {string|number} destination - Sommet destination.
   */
  ajouterArete(source, destination) {
    // S'assurer que les sommets existent
    this.ajouterSommet(source);
    this.ajouterSommet(destination);

    // Ajouter la connexion
    this.listeAdjacence.get(source).push(destination);

    // Si non orienté, ajouter dans l'autre sens
    if (!this.oriente) {
      this.listeAdjacence.get(destination).push(source);
    }
  }

  /**
   * Vérifie s'il existe une arête entre deux sommets.
   * @param {string|number} source - Sommet source.
   * @param {string|number} destination - Sommet destination.
   * @returns {boolean} - True si l'arête existe.
   */
  existeArete(source, destination) {
    const voisins = this.listeAdjacence.get(source);
    return voisins ? voisins.includes(destination) : false;
  }

  /**
   * Retourne les voisins d'un sommet.
   * @param {string|number} sommet - Le sommet.
   * @returns {Array} - Liste des voisins.
   */
  obtenirVoisins(sommet) {
    return this.listeAdjacence.get(sommet) || [];
  }

  /**
   * Retourne tous les sommets du graphe.
   * @returns {Array} - Liste de tous les sommets.
   */
  obtenirSommets() {
    return Array.from(this.listeAdjacence.keys());
  }

  /**
   * Affiche la liste d'adjacence.
   */
  afficher() {
    console.log("Liste d'adjacence :");
    for (const [sommet, voisins] of this.listeAdjacence) {
      console.log(`${sommet}: [${voisins.join(", ")}]`);
    }
  }
}

// Test : Graphe non orienté avec des noms
const reseauAmis = new GrapheListe();
reseauAmis.ajouterArete("Chermann", "Ingrid");
reseauAmis.ajouterArete("Chermann", "Prudence");
reseauAmis.ajouterArete("Chermann", "Germain");
reseauAmis.ajouterArete("Ingrid", "Germain");
reseauAmis.ajouterArete("Prudence", "Germain");

reseauAmis.afficher();
/*
Liste d'adjacence :
Chermann: [Ingrid, Prudence, Germain]
Ingrid: [Chermann, Germain]
Prudence: [Chermann, Germain]
Germain: [Chermann, Ingrid, Prudence]
*/

console.log("\nVoisins de Chermann :", reseauAmis.obtenirVoisins("Chermann"));
// [Ingrid, Prudence, Germain]

console.log(
  "Chermann et Ingrid amis ?",
  reseauAmis.existeArete("Chermann", "Ingrid"),
);
// true

console.log(
  "Ingrid et Prudence amis ?",
  reseauAmis.existeArete("Ingrid", "Prudence"),
);
// false
```

---

### Avantages et Inconvénients

| Avantages                        | Inconvénients                             |
| -------------------------------- | ----------------------------------------- |
| Espace **O(V + E)** efficace     | Vérification d'arête **O(degré)**         |
| Facile d'ajouter des sommets     | Moins pratique pour certains algorithmes  |
| Idéal pour graphes **creux**     | Parcourir tous les voisins peut être lent |
| Itération rapide sur les voisins |                                           |

---

## 📝 Micro-Exercice #2 : Convertir une Représentation

**Objectif :** Comprendre l'équivalence entre les deux représentations.

**Instructions :** Convertissez cette matrice d'adjacence en liste d'adjacence :

```
      0   1   2
    +---+---+---+
  0 | 0 | 1 | 1 |
    +---+---+---+
  1 | 1 | 0 | 0 |
    +---+---+---+
  2 | 1 | 0 | 0 |
    +---+---+---+
```

<details>
<summary>💡 Voir la solution</summary>

```
Liste d'adjacence équivalente :

0: [1, 2]   // matrice[0][1]=1 et matrice[0][2]=1
1: [0]      // matrice[1][0]=1
2: [0]      // matrice[2][0]=1

Graphe visuel :
    [0]
   /   \
 [1]   [2]
```

</details>

---

## 💻 Graphes Pondérés : Représentations

Les graphes pondérés nécessitent de stocker les **poids** des arêtes.

---

### Liste d'Adjacence Pondérée

Chaque voisin est stocké avec son poids :

```javascript
/**
 * Classe représentant un graphe pondéré via une liste d'adjacence.
 */
class GraphePondere {
  constructor(oriente = false) {
    this.oriente = oriente;
    this.listeAdjacence = new Map();
  }

  ajouterSommet(sommet) {
    if (!this.listeAdjacence.has(sommet)) {
      this.listeAdjacence.set(sommet, []);
    }
  }

  /**
   * Ajoute une arête pondérée.
   * @param {string} source - Sommet source.
   * @param {string} destination - Sommet destination.
   * @param {number} poids - Poids de l'arête.
   */
  ajouterArete(source, destination, poids) {
    this.ajouterSommet(source);
    this.ajouterSommet(destination);

    // Stocker l'objet {voisin, poids}
    this.listeAdjacence.get(source).push({
      voisin: destination,
      poids: poids,
    });

    if (!this.oriente) {
      this.listeAdjacence.get(destination).push({
        voisin: source,
        poids: poids,
      });
    }
  }

  /**
   * Obtient le poids d'une arête.
   * @returns {number|null} - Le poids ou null si pas d'arête.
   */
  obtenirPoids(source, destination) {
    const voisins = this.listeAdjacence.get(source);
    if (!voisins) return null;

    const arete = voisins.find((v) => v.voisin === destination);
    return arete ? arete.poids : null;
  }

  afficher() {
    console.log("Graphe Pondéré :");
    for (const [sommet, voisins] of this.listeAdjacence) {
      const connexions = voisins
        .map((v) => `${v.voisin}(${v.poids})`)
        .join(", ");
      console.log(`${sommet}: [${connexions}]`);
    }
  }
}

// Exemple : Réseau de trajets avec distances (km)
const trajets = new GraphePondere();
trajets.ajouterArete("Bruxelles", "Anvers", 50);
trajets.ajouterArete("Bruxelles", "Gand", 55);
trajets.ajouterArete("Anvers", "Gand", 60);
trajets.ajouterArete("Anvers", "Liège", 120);

trajets.afficher();
/*
Graphe Pondéré :
Bruxelles: [Anvers(50), Gand(55)]
Anvers: [Bruxelles(50), Gand(60), Liège(120)]
Gand: [Bruxelles(55), Anvers(60)]
Liège: [Anvers(120)]
*/

console.log(
  "Distance Bruxelles-Anvers :",
  trajets.obtenirPoids("Bruxelles", "Anvers"),
); // 50
console.log(
  "Distance Bruxelles-Liège :",
  trajets.obtenirPoids("Bruxelles", "Liège"),
); // null
```

---

### Matrice d'Adjacence Pondérée

On stocke les poids dans la matrice, avec `0` ou `Infinity` pour l'absence d'arête :

```javascript
/**
 * Matrice d'adjacence pondérée.
 */
class GrapheMatricePonderee {
  constructor(sommets) {
    this.sommets = sommets; // Ex: ["Bruxelles", "Anvers", "Gand"]
    this.indices = {}; // Mapping nom → index

    sommets.forEach((s, i) => (this.indices[s] = i));

    const n = sommets.length;
    // Initialiser avec Infinity (pas de connexion)
    this.matrice = Array.from({ length: n }, () => Array(n).fill(Infinity));
    // Distance à soi-même = 0
    for (let i = 0; i < n; i++) {
      this.matrice[i][i] = 0;
    }
  }

  ajouterArete(source, destination, poids) {
    const i = this.indices[source];
    const j = this.indices[destination];
    this.matrice[i][j] = poids;
    this.matrice[j][i] = poids; // Non orienté
  }

  obtenirPoids(source, destination) {
    const i = this.indices[source];
    const j = this.indices[destination];
    return this.matrice[i][j];
  }

  afficher() {
    console.log("        " + this.sommets.join("    "));
    for (let i = 0; i < this.sommets.length; i++) {
      const ligne = this.matrice[i]
        .map((v) => (v === Infinity ? "∞" : String(v).padStart(3)))
        .join("  ");
      console.log(`${this.sommets[i].padEnd(8)} ${ligne}`);
    }
  }
}

// Exemple
const reseau = new GrapheMatricePonderee([
  "Bruxelles",
  "Anvers",
  "Gand",
  "Liège",
]);
reseau.ajouterArete("Bruxelles", "Anvers", 50);
reseau.ajouterArete("Bruxelles", "Gand", 55);
reseau.ajouterArete("Anvers", "Gand", 60);
reseau.ajouterArete("Anvers", "Liège", 120);

reseau.afficher();
/*
          Bruxelles  Anvers  Gand  Liège
Bruxelles       0       50    55      ∞
Anvers         50        0    60    120
Gand           55       60     0      ∞
Liège           ∞      120     ∞      0
*/
```

---

## 📊 Comparaison des Représentations

Quelle représentation choisir ? Cela dépend du graphe et des opérations.

---

### Graphe Dense vs Graphe Creux

Un **graphe dense** a beaucoup d'arêtes (proche de V²).
Un **graphe creux** (sparse) a peu d'arêtes (proche de V).

```
Graphe DENSE :           Graphe CREUX :
(presque tout connecté)   (peu de connexions)

  [A]---[B]                [A]---[B]
   |\   /|
   | \ / |                 [C]   [D]
   |  X  |                      /
   | / \ |                [E]--[F]
   |/   \|
  [C]---[D]
```

---

### Critères de Choix

| Critère                      | Matrice | Liste    |
| ---------------------------- | ------- | -------- |
| **Espace**                   | O(V²)   | O(V + E) |
| **Vérifier si arête existe** | O(1)    | O(degré) |
| **Parcourir les voisins**    | O(V)    | O(degré) |
| **Ajouter une arête**        | O(1)    | O(1)     |
| **Ajouter un sommet**        | O(V²)   | O(1)     |
| **Supprimer une arête**      | O(1)    | O(degré) |

---

### Recommandations

**Utilisez une MATRICE quand :**

- Le graphe est **dense**
- Vous vérifiez fréquemment l'**existence d'arêtes**
- Le nombre de sommets est **fixe et petit**

**Utilisez une LISTE quand :**

- Le graphe est **creux** (sparse)
- Vous parcourez souvent les **voisins**
- Le nombre de sommets peut **changer**
- Vous devez économiser la **mémoire**

> **Point Clé**
>
> La plupart des graphes du monde réel sont **creux**. Un réseau social de 1 million d'utilisateurs n'a pas 1 trillion d'amitiés ! La **liste d'adjacence** est donc souvent préférable.

---

## 📝 Micro-Exercice #3 : Choisir la Représentation

**Objectif :** Développer l'intuition pour choisir la bonne structure.

**Instructions :** Pour chaque scénario, quelle représentation choisiriez-vous ?

1. Un petit jeu d'échecs où chaque case peut atteindre quelques autres cases
2. Un réseau social de 10 millions d'utilisateurs
3. Un tableau de distances entre 50 villes (toutes connectées)

<details>
<summary>💡 Voir la solution</summary>

1. **Échiquier** : **Matrice d'adjacence** - Nombre fixe de 64 cases, graphe relativement dense (chaque pièce a plusieurs mouvements possibles), vérification rapide si un mouvement est valide.

2. **Réseau social** : **Liste d'adjacence** - Graphe très creux (personne n'a des millions d'amis), besoin de parcourir les amis efficacement, économie de mémoire cruciale (10M × 10M = 100 trillions de cellules serait impossible).

3. **Distances entre villes** : **Matrice d'adjacence** - Graphe complet (toutes les villes connectées), nombre fixe de 50 villes (50² = 2500 cellules acceptable), besoin de lookup O(1) pour les distances.

</details>

---

## 💼 Application : Étude de Cas - Système de Recommandation

Construisons un mini-système de recommandation basé sur les préférences partagées.

---

### Scénario

Marc-Élie développe une application de recommandation de films. Il veut suggérer des films aux utilisateurs basés sur ce que des utilisateurs similaires ont aimé.

**Idée :** Si Chermann et Ingrid ont tous deux aimé "Matrix", et qu'Ingrid a aussi aimé "Inception", alors on peut recommander "Inception" à Chermann.

---

### Modélisation avec un Graphe Biparti

Un **graphe biparti** a deux types de sommets : ici, les **utilisateurs** et les **films**.

```
Utilisateurs           Films
[Chermann] ---------> [Matrix]
     \                   ^
      \                 /
       --> [Inception] <
            ^           \
           /             v
[Ingrid] -------------> [Interstellar]
     \
      --> [Matrix]
```

---

### Implémentation Complète

```javascript
/**
 * Système de recommandation basé sur les graphes.
 */
class SystemeRecommandation {
  constructor() {
    this.listeAdjacence = new Map();
    this.utilisateurs = new Set();
    this.films = new Set();
  }

  /**
   * Ajoute une préférence utilisateur → film.
   */
  ajouterPreference(utilisateur, film) {
    // Ajouter aux ensembles
    this.utilisateurs.add(utilisateur);
    this.films.add(film);

    // Créer les entrées si nécessaire
    if (!this.listeAdjacence.has(utilisateur)) {
      this.listeAdjacence.set(utilisateur, []);
    }
    if (!this.listeAdjacence.has(film)) {
      this.listeAdjacence.set(film, []);
    }

    // Graphe biparti non orienté
    this.listeAdjacence.get(utilisateur).push(film);
    this.listeAdjacence.get(film).push(utilisateur);
  }

  /**
   * Retourne les films aimés par un utilisateur.
   */
  obtenirFilmsAimes(utilisateur) {
    return this.listeAdjacence.get(utilisateur) || [];
  }

  /**
   * Retourne les utilisateurs ayant aimé un film.
   */
  obtenirAmateursFilm(film) {
    return this.listeAdjacence.get(film) || [];
  }

  /**
   * Trouve les utilisateurs similaires (ayant au moins 1 film en commun).
   */
  trouverUtilisateursSimilaires(utilisateur) {
    const filmsAimes = this.obtenirFilmsAimes(utilisateur);
    const similaires = new Set();

    for (const film of filmsAimes) {
      const amateurs = this.obtenirAmateursFilm(film);
      for (const amateur of amateurs) {
        if (amateur !== utilisateur) {
          similaires.add(amateur);
        }
      }
    }

    return Array.from(similaires);
  }

  /**
   * Recommande des films basés sur les utilisateurs similaires.
   */
  recommanderFilms(utilisateur) {
    const filmsAimes = new Set(this.obtenirFilmsAimes(utilisateur));
    const similaires = this.trouverUtilisateursSimilaires(utilisateur);
    const recommandations = new Map(); // film → score

    for (const utilisateurSimilaire of similaires) {
      const leursFilms = this.obtenirFilmsAimes(utilisateurSimilaire);
      for (const film of leursFilms) {
        // Ne pas recommander ce que l'utilisateur a déjà vu
        if (!filmsAimes.has(film)) {
          const score = recommandations.get(film) || 0;
          recommandations.set(film, score + 1);
        }
      }
    }

    // Trier par score décroissant
    return Array.from(recommandations.entries())
      .sort((a, b) => b[1] - a[1])
      .map(([film, score]) => ({ film, score }));
  }

  /**
   * Affiche le graphe.
   */
  afficher() {
    console.log("\n=== Graphe de Préférences ===");
    console.log("Utilisateurs :");
    for (const u of this.utilisateurs) {
      console.log(`  ${u} aime: [${this.obtenirFilmsAimes(u).join(", ")}]`);
    }
    console.log("\nFilms :");
    for (const f of this.films) {
      console.log(
        `  ${f} aimé par: [${this.obtenirAmateursFilm(f).join(", ")}]`,
      );
    }
  }
}

// Utilisation
const systeme = new SystemeRecommandation();

// Préférences
systeme.ajouterPreference("Chermann", "Matrix");
systeme.ajouterPreference("Chermann", "Inception");
systeme.ajouterPreference("Ingrid", "Matrix");
systeme.ajouterPreference("Ingrid", "Interstellar");
systeme.ajouterPreference("Ingrid", "Dune");
systeme.ajouterPreference("Prudence", "Inception");
systeme.ajouterPreference("Prudence", "Interstellar");
systeme.ajouterPreference("Germain", "Dune");
systeme.ajouterPreference("Germain", "Matrix");

systeme.afficher();

console.log("\n=== Recommandations pour Chermann ===");
const similaires = systeme.trouverUtilisateursSimilaires("Chermann");
console.log("Utilisateurs similaires :", similaires);
// [Ingrid, Prudence, Germain]

const recommandations = systeme.recommanderFilms("Chermann");
console.log("Films recommandés :");
recommandations.forEach((r) => console.log(`  ${r.film} (score: ${r.score})`));
/*
Films recommandés :
  Interstellar (score: 2)  // Aimé par Ingrid ET Prudence
  Dune (score: 2)          // Aimé par Ingrid ET Germain
*/
```

---

### Analyse du Graphe

```
                    [Matrix]
                   /   |   \
             Chermann Ingrid Germain
                |      |
            [Inception][Interstellar]
                |          |
             Prudence   Prudence + Ingrid
                           |
                        [Dune]
                           |
                      Ingrid + Germain
```

**Pourquoi Interstellar et Dune ont le score 2 ?**

- Chermann est similaire à Ingrid (via Matrix) et Prudence (via Inception)
- Interstellar est aimé par Ingrid ET Prudence → score 2
- Dune est aimé par Ingrid ET Germain → score 2

---

## 💪 Exercices Pratiques

Consolidez vos connaissances avec ces exercices progressifs.

---

### Exercice 1 : Modéliser un Système de Cours

**Objectif :** Créer un graphe orienté de prérequis.

**Instructions :**
Modélisez le système de prérequis suivant avec une liste d'adjacence :

- CS101 est prérequis pour CS201 et CS202
- MA101 est prérequis pour CS201
- CS201 est prérequis pour CS305
- CS202 est prérequis pour CS305

<details>
<summary>💡 Voir la solution</summary>

```javascript
const prerequis = new GrapheListe(true); // Orienté

prerequis.ajouterArete("CS101", "CS201");
prerequis.ajouterArete("CS101", "CS202");
prerequis.ajouterArete("MA101", "CS201");
prerequis.ajouterArete("CS201", "CS305");
prerequis.ajouterArete("CS202", "CS305");

prerequis.afficher();
/*
Liste d'adjacence :
CS101: [CS201, CS202]
CS201: [CS305]
MA101: [CS201]
CS202: [CS305]
CS305: []
*/

// Pour suivre CS305, quels cours sont nécessaires ?
// CS101 → CS201 → CS305 OU CS101 → CS202 → CS305
// Plus MA101 → CS201 (pour CS201)
```

</details>

---

### Exercice 2 : Réseau de Livraison Pondéré

**Objectif :** Implémenter une matrice d'adjacence pondérée.

**Instructions :**
Créez une matrice pour ce réseau de livraison (temps en minutes) :

- Dépôt A → Client X : 10 min
- Dépôt A → Client Y : 15 min
- Client X → Client Y : 5 min
- Client X → Client Z : 12 min
- Client Y → Dépôt B : 8 min
- Client Z → Dépôt B : 7 min

<details>
<summary>💡 Voir la solution</summary>

```javascript
const livraison = new GrapheMatricePonderee([
  "Dépôt A",
  "Dépôt B",
  "Client X",
  "Client Y",
  "Client Z",
]);

livraison.ajouterArete("Dépôt A", "Client X", 10);
livraison.ajouterArete("Dépôt A", "Client Y", 15);
livraison.ajouterArete("Client X", "Client Y", 5);
livraison.ajouterArete("Client X", "Client Z", 12);
livraison.ajouterArete("Client Y", "Dépôt B", 8);
livraison.ajouterArete("Client Z", "Dépôt B", 7);

livraison.afficher();
/*
         Dépôt A  Dépôt B  Client X  Client Y  Client Z
Dépôt A       0        ∞        10        15         ∞
Dépôt B       ∞        0         ∞         8         7
Client X     10        ∞         0         5        12
Client Y     15        8         5         0         ∞
Client Z      ∞        7        12         ∞         0
*/
```

</details>

---

### Exercice 3 : Degré des Sommets

**Objectif :** Calculer le degré (nombre de connexions) de chaque sommet.

**Instructions :**
Ajoutez une méthode `calculerDegre(sommet)` à la classe `GrapheListe`.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Calcule le degré d'un sommet (nombre de voisins).
 * @param {string|number} sommet - Le sommet.
 * @returns {number} - Le degré du sommet.
 */
calculerDegre(sommet) {
  const voisins = this.listeAdjacence.get(sommet);
  return voisins ? voisins.length : 0;
}

/**
 * Calcule le degré de tous les sommets.
 * @returns {Map} - Map sommet → degré.
 */
calculerTousDegres() {
  const degres = new Map();
  for (const [sommet, voisins] of this.listeAdjacence) {
    degres.set(sommet, voisins.length);
  }
  return degres;
}

// Test
const graphe = new GrapheListe();
graphe.ajouterArete("A", "B");
graphe.ajouterArete("A", "C");
graphe.ajouterArete("A", "D");
graphe.ajouterArete("B", "C");

console.log("Degré de A :", graphe.calculerDegre("A")); // 3
console.log("Degré de B :", graphe.calculerDegre("B")); // 2
console.log("Degré de D :", graphe.calculerDegre("D")); // 1
```

</details>

---

### Exercice 4 : Choix de Représentation

**Objectif :** Justifier le choix de structure.

**Instructions :**
Pour un graphe de 10 000 sommets et 100 000 arêtes, quelle représentation choisiriez-vous ? Calculez l'espace mémoire approximatif pour chaque option.

<details>
<summary>💡 Voir la solution</summary>

**Analyse :**

**Matrice d'adjacence :**

- Espace = V² = 10 000² = 100 000 000 cellules
- Si chaque cellule = 1 octet → 100 Mo
- Si chaque cellule = 4 octets (int) → 400 Mo

**Liste d'adjacence :**

- Espace = O(V + E) = 10 000 + 100 000 = 110 000 entrées
- Chaque entrée ≈ 8 octets (pointeur/référence) → ~1 Mo

**Ratio E/V² = 100 000 / 100 000 000 = 0.001 = 0.1%**

Le graphe est très **creux** (seulement 0.1% des arêtes possibles existent).

**Choix : Liste d'adjacence**

- Économie de mémoire : ~100x moins
- Parcours des voisins efficace
- Le graphe est sparse

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la différence fondamentale entre un arbre et un graphe ?**

- [ ] A. Un arbre a des nœuds, un graphe a des sommets
- [ ] B. Un graphe peut avoir des cycles, un arbre non
- [ ] C. Un arbre est plus rapide qu'un graphe
- [ ] D. Un graphe est toujours orienté

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Un **arbre** est un graphe connexe **sans cycles**. Un graphe général peut contenir des **cycles** (chemins fermés).

</details>

---

### Question 2

**Dans un graphe non orienté, si A est connecté à B, alors :**

- [ ] A. B peut être connecté à A ou non
- [ ] B. B est automatiquement connecté à A
- [ ] C. On doit explicitement ajouter B→A
- [ ] D. La connexion n'existe que dans un sens

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Dans un graphe **non orienté**, les arêtes sont bidirectionnelles. Si A-B existe, alors B-A existe automatiquement.

</details>

---

### Question 3

**Quelle est la complexité spatiale d'une matrice d'adjacence ?**

- [ ] A. O(V)
- [ ] B. O(E)
- [ ] C. O(V + E)
- [ ] D. O(V²)

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Une matrice d'adjacence est un tableau 2D de taille V × V, donc **O(V²)** quel que soit le nombre d'arêtes.

</details>

---

### Question 4

**Quelle représentation est préférable pour un graphe creux ?**

- [ ] A. Matrice d'adjacence
- [ ] B. Liste d'adjacence
- [ ] C. Les deux sont équivalentes
- [ ] D. Aucune des deux

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La **liste d'adjacence** utilise O(V + E) d'espace, ce qui est bien plus efficace qu'O(V²) pour un graphe creux où E << V².

</details>

---

### Question 5

**Comment vérifier si une arête existe entre deux sommets en O(1) ?**

- [ ] A. Avec une liste d'adjacence
- [ ] B. Avec une matrice d'adjacence
- [ ] C. Ce n'est pas possible
- [ ] D. Avec les deux représentations

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La **matrice d'adjacence** permet de vérifier `matrice[i][j]` en **O(1)**. La liste d'adjacence nécessite de parcourir la liste des voisins.

</details>

---

### Question 6

**Dans un graphe pondéré, que représente le poids d'une arête ?**

- [ ] A. Le nombre de sommets connectés
- [ ] B. Une valeur numérique associée à la connexion
- [ ] C. La direction de l'arête
- [ ] D. Le degré du sommet

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le **poids** est une valeur numérique (distance, coût, temps, etc.) associée à l'arête, représentant un attribut de la connexion.

</details>

---

### Question 7

**Quel type de graphe modélise les abonnements sur un réseau social (suivre quelqu'un) ?**

- [ ] A. Non orienté non pondéré
- [ ] B. Non orienté pondéré
- [ ] C. Orienté non pondéré
- [ ] D. Orienté pondéré

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un abonnement est **unidirectionnel** (A suit B n'implique pas B suit A), donc **orienté**. Il n'y a pas de notion de "quantité" donc **non pondéré**.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Définition d'un Graphe

Un graphe G = (V, E) est composé de **sommets** (V) et d'**arêtes** (E) qui connectent des paires de sommets.

### 2. Types d'Arêtes

- **Non orientées** : bidirectionnelles (amitiés)
- **Orientées** : unidirectionnelles (abonnements)
- **Pondérées** : avec une valeur numérique (distances)

### 3. Matrice d'Adjacence

Tableau 2D de taille V×V. `matrice[i][j] = 1` si arête existe. Espace O(V²), lookup O(1).

### 4. Liste d'Adjacence

Dictionnaire où chaque sommet a la liste de ses voisins. Espace O(V+E), lookup O(degré).

### 5. Graphe Dense vs Creux

Dense = beaucoup d'arêtes → matrice. Creux (sparse) = peu d'arêtes → liste.

### 6. Arbres vs Graphes

Un arbre est un graphe **connexe sans cycles**. Les graphes sont plus généraux et peuvent contenir des cycles.

### 7. Applications

Réseaux sociaux, cartes routières, systèmes de recommandation, dépendances logicielles, et bien plus.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant les concepts fondamentaux des graphes !

### Ce que vous avez appris aujourd'hui

- Les composants d'un graphe : sommets et arêtes
- Les différents types : orienté, non orienté, pondéré
- La matrice d'adjacence et son implémentation
- La liste d'adjacence et son implémentation
- Comment choisir la bonne représentation
- Une application concrète (système de recommandation)

### Compétences acquises

Vous êtes maintenant capable de :

- Modéliser des relations avec des graphes
- Implémenter les deux représentations en JavaScript
- Choisir la structure adaptée au contexte

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Les graphes sont **omniprésents** en informatique : réseaux sociaux (2+ milliards de nœuds sur Facebook), GPS et navigation, Internet (routing), recommandations (Netflix, Amazon), détection de fraude, bioinformatique (réseaux de protéines). Maîtriser les graphes ouvre la porte à la résolution de problèmes complexes du monde réel.

---

## ➡️ Prochaine Étape : Leçon 28

### Ce qui vous attend

La prochaine leçon, **« Implémentations Liste d'Adjacence et Matrice en JavaScript »**, approfondira les implémentations que nous avons introduites dans cette leçon.

**Vous découvrirez :**

- Des implémentations **plus complètes** et **robustes** des deux représentations
- Des méthodes avancées : **suppression d'arêtes**, **calcul de degré**, **vérification de connexité**
- Une **analyse détaillée** des complexités pour chaque opération
- Des **cas d'usage réels** : routes, réseaux sociaux, systèmes de recommandation

### Préparez-vous !

Cette leçon vous fournira des classes **réutilisables** et **complètes** pour manipuler des graphes dans vos projets JavaScript !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Graph](https://visualgo.net/en/graphds) - Visualisation interactive
- [Wikipedia - Graph Theory](https://en.wikipedia.org/wiki/Graph_theory) - Théorie approfondie
- [CS50 - Graphs](https://cs50.harvard.edu/x/2024/) - Cours Harvard

### Outils de pratique

- **[Graph Visualizer](https://www.cs.usfca.edu/~galles/visualization/ConnectedComponent.html)** : Visualisez les opérations
- **[LeetCode Graph Problems](https://leetcode.com/tag/graph/)** : Exercices pratiques

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Dessiner des graphes sur papier pour visualiser
- Expérimenter avec les implémentations JavaScript

> 💡 **Conseil**
>
> Pour bien comprendre les graphes, **pratiquez** ! Modélisez des situations de votre quotidien : vos trajets (sommets = lieux, arêtes = routes), votre réseau d'amis, les dépendances entre vos projets. Plus vous modélisez, plus les graphes deviennent naturels.

---

**Prêt pour la Leçon 28 ?** 🚀

Rendez-vous dans la prochaine leçon pour apprendre le parcours en largeur (BFS) !

---

<div align="center">

**Leçon 27 sur 42 - Module 5 : Arbres et Parcours de Graphes**

[⬅️ Leçon 26 : BST - Insertion et Recherche](./lecon-2-arbres-recherche-binaires-insertion-recherche-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 28 : Implémentations Liste d'Adjacence et Matrice en JavaScript ➡️](./lecon-4-implementations-liste-adjacence-matrice-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
