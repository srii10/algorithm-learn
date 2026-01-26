##### Leçon 32 sur 42

# Implémentation d'un Algorithme Glouton en JavaScript : Le Problème de la Monnaie

**Module 6** : Paradigmes Avancés de Conception d'Algorithmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Implémenter un **algorithme glouton complet** en JavaScript
- Comprendre l'importance du **tri préalable** dans les algorithmes gloutons
- Gérer les **cas limites** (montant nul, négatif, impossible)
- Analyser quand le glouton **réussit** vs quand il **échoue**
- Créer des **tests robustes** pour valider l'implémentation
- Préparer la transition vers la **programmation dynamique**

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- **Leçon 31 complétée** : Principes des algorithmes gloutons
- **Module 3** : Algorithmes de tri
- **JavaScript** : Manipulation de tableaux et objets
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : Du Concept à l'Implémentation

Dans la leçon précédente, nous avons découvert les **principes** des algorithmes gloutons. Aujourd'hui, nous passons à la **pratique** avec une implémentation complète et robuste du problème de la monnaie.

Nous allons construire une solution étape par étape, en gérant tous les cas particuliers et en comprenant profondément pourquoi chaque ligne de code est nécessaire.

> **Point Clé**
>
> Une bonne implémentation d'algorithme ne se limite pas à la logique principale. Elle doit aussi gérer les **entrées invalides**, les **cas limites**, et fournir des **informations utiles** pour le débogage.

---

## 📦 Rappel : Le Problème de la Monnaie

Le problème consiste à rendre une somme donnée avec le **minimum de pièces/billets**.

---

### Énoncé Formel

```
ENTRÉE :
- Un montant M à rendre
- Un ensemble de dénominations D = {d₁, d₂, ..., dₙ}

SORTIE :
- Le nombre minimum de pièces/billets pour atteindre M
- Le détail de chaque dénomination utilisée
```

---

### Stratégie Gloutonne Rappel

> À chaque étape, choisir la **plus grande dénomination** qui ne dépasse pas le montant restant.

```
1. Trier les dénominations par ordre DÉCROISSANT
2. Pour chaque dénomination (de la plus grande à la plus petite) :
   a. Tant que le montant restant ≥ cette dénomination :
      - Prendre une pièce/un billet de cette dénomination
      - Soustraire sa valeur du montant restant
3. Retourner le résultat
```

---

## 💻 Implémentation Étape par Étape

Construisons notre algorithme progressivement.

---

### Étape 1 : Structure de Base

```javascript
/**
 * Rend la monnaie avec un algorithme glouton.
 * @param {number[]} denominations - Les dénominations disponibles.
 * @param {number} montant - Le montant à rendre.
 * @returns {Object} - Le résultat avec détails.
 */
function rendreMonnaieGlouton(denominations, montant) {
  // TODO: Validation des entrées
  // TODO: Tri des dénominations
  // TODO: Algorithme glouton
  // TODO: Construction du résultat
}
```

---

### Étape 2 : Validation des Entrées

```javascript
function rendreMonnaieGlouton(denominations, montant) {
  // === VALIDATION DES ENTRÉES ===

  // Vérifier que les dénominations sont un tableau non vide
  if (!Array.isArray(denominations) || denominations.length === 0) {
    throw new Error("Les dénominations doivent être un tableau non vide.");
  }

  // Vérifier que toutes les dénominations sont des nombres positifs
  for (const denom of denominations) {
    if (typeof denom !== "number" || denom <= 0 || !Number.isInteger(denom)) {
      throw new Error(
        `Dénomination invalide : ${denom}. Doit être un entier positif.`,
      );
    }
  }

  // Gérer le montant nul
  if (montant === 0) {
    return {
      nombreTotal: 0,
      detail: {},
      piecesUtilisees: [],
      reste: 0,
      succes: true,
    };
  }

  // Gérer le montant négatif
  if (montant < 0) {
    throw new Error("Le montant ne peut pas être négatif.");
  }

  // Suite de l'algorithme...
}
```

---

### Étape 3 : Tri des Dénominations

```javascript
function rendreMonnaieGlouton(denominations, montant) {
  // Validation (voir ci-dessus)...

  // === TRI DES DÉNOMINATIONS (DÉCROISSANT) ===
  // Créer une copie pour ne pas modifier l'original
  const denominationsTriees = [...denominations].sort((a, b) => b - a);

  console.log("Dénominations triées :", denominationsTriees);
  // Exemple : [50, 20, 10, 5, 2, 1] pour les centimes euro

  // Suite de l'algorithme...
}
```

> **Attention**
>
> Le tri est **crucial** pour l'algorithme glouton. Si les dénominations ne sont pas triées par ordre décroissant, l'algorithme ne choisira pas toujours la plus grande pièce disponible.

---

### Étape 4 : Algorithme Glouton Principal

```javascript
function rendreMonnaieGlouton(denominations, montant) {
  // Validation et tri (voir ci-dessus)...
  const denominationsTriees = [...denominations].sort((a, b) => b - a);

  // === ALGORITHME GLOUTON ===
  let restant = montant;
  let nombreTotal = 0;
  const detail = {}; // Compteur par dénomination
  const piecesUtilisees = []; // Liste des pièces utilisées

  for (const denom of denominationsTriees) {
    // Tant qu'on peut prendre cette dénomination
    while (restant >= denom) {
      // Prendre une pièce de cette dénomination
      restant -= denom;
      nombreTotal++;

      // Mettre à jour le compteur
      detail[denom] = (detail[denom] || 0) + 1;

      // Ajouter à la liste des pièces
      piecesUtilisees.push(denom);
    }
  }

  // Suite : construction du résultat...
}
```

---

### Étape 5 : Construction du Résultat

```javascript
function rendreMonnaieGlouton(denominations, montant) {
  // Validation, tri et algorithme (voir ci-dessus)...

  // === CONSTRUCTION DU RÉSULTAT ===
  const succes = restant === 0;

  if (!succes) {
    console.warn(
      `Attention : Impossible de rendre exactement ${montant}. ` +
        `Reste : ${restant}. ` +
        `Vérifiez les dénominations disponibles.`,
    );
  }

  return {
    nombreTotal: nombreTotal,
    detail: detail,
    piecesUtilisees: piecesUtilisees,
    reste: restant,
    succes: succes,
    montantOriginal: montant,
  };
}
```

---

## 💻 Implémentation Complète

Voici l'implémentation finale avec toutes les fonctionnalités.

```javascript
/**
 * Algorithme glouton pour le problème de la monnaie.
 * Trouve le nombre minimum de pièces/billets pour rendre un montant donné.
 *
 * ATTENTION : L'optimalité n'est garantie que pour certains systèmes monétaires
 * (comme l'euro). Pour des systèmes arbitraires, utilisez la programmation dynamique.
 *
 * @param {number[]} denominations - Tableau des dénominations disponibles (en centimes).
 * @param {number} montant - Montant à rendre (en centimes).
 * @returns {Object} Résultat contenant :
 *   - nombreTotal: Nombre total de pièces/billets
 *   - detail: Objet avec le compte de chaque dénomination
 *   - piecesUtilisees: Tableau des pièces dans l'ordre de sélection
 *   - reste: Montant non rendu (0 si succès)
 *   - succes: Booléen indiquant si le montant a été entièrement rendu
 *   - montantOriginal: Le montant demandé initialement
 */
function rendreMonnaieGlouton(denominations, montant) {
  // === VALIDATION DES ENTRÉES ===
  if (!Array.isArray(denominations) || denominations.length === 0) {
    throw new Error("Les dénominations doivent être un tableau non vide.");
  }

  for (const denom of denominations) {
    if (typeof denom !== "number" || denom <= 0 || !Number.isInteger(denom)) {
      throw new Error(
        `Dénomination invalide : ${denom}. Doit être un entier positif.`,
      );
    }
  }

  if (montant === 0) {
    return {
      nombreTotal: 0,
      detail: {},
      piecesUtilisees: [],
      reste: 0,
      succes: true,
      montantOriginal: 0,
    };
  }

  if (montant < 0) {
    throw new Error("Le montant ne peut pas être négatif.");
  }

  if (!Number.isInteger(montant)) {
    throw new Error("Le montant doit être un entier (en centimes).");
  }

  // === TRI DES DÉNOMINATIONS (DÉCROISSANT) ===
  const denominationsTriees = [...denominations].sort((a, b) => b - a);

  // === ALGORITHME GLOUTON ===
  let restant = montant;
  let nombreTotal = 0;
  const detail = {};
  const piecesUtilisees = [];

  for (const denom of denominationsTriees) {
    while (restant >= denom) {
      restant -= denom;
      nombreTotal++;
      detail[denom] = (detail[denom] || 0) + 1;
      piecesUtilisees.push(denom);
    }
  }

  // === RÉSULTAT ===
  const succes = restant === 0;

  if (!succes) {
    console.warn(
      `Attention : Impossible de rendre exactement ${montant} centimes. Reste : ${restant}.`,
    );
  }

  return {
    nombreTotal,
    detail,
    piecesUtilisees,
    reste: restant,
    succes,
    montantOriginal: montant,
  };
}
```

---

## 📝 Micro-Exercice #1 : Comprendre le Code

**Objectif :** Analyser le flux d'exécution.

**Instructions :** Pour l'appel `rendreMonnaieGlouton([50, 20, 10, 5, 2, 1], 78)`, tracez :

1. L'état de `restant` après chaque itération de la boucle `for`
2. Le contenu de `detail` à la fin
3. Le contenu de `piecesUtilisees` à la fin

<details>
<summary>💡 Voir la solution</summary>

```
Dénominations triées : [50, 20, 10, 5, 2, 1]
Montant initial : 78

denom = 50 :
  - 78 >= 50 → prendre 50, restant = 28
  - 28 < 50 → passer à la suivante

denom = 20 :
  - 28 >= 20 → prendre 20, restant = 8
  - 8 < 20 → passer à la suivante

denom = 10 :
  - 8 < 10 → passer à la suivante

denom = 5 :
  - 8 >= 5 → prendre 5, restant = 3
  - 3 < 5 → passer à la suivante

denom = 2 :
  - 3 >= 2 → prendre 2, restant = 1
  - 1 < 2 → passer à la suivante

denom = 1 :
  - 1 >= 1 → prendre 1, restant = 0
  - 0 < 1 → FIN

RÉSULTAT :
- detail = { 50: 1, 20: 1, 5: 1, 2: 1, 1: 1 }
- piecesUtilisees = [50, 20, 5, 2, 1]
- nombreTotal = 5
```

</details>

---

## 🧪 Tests et Cas d'Utilisation

Testons notre implémentation avec différents scénarios.

---

### Test 1 : Système Euro (Glouton Optimal)

```javascript
// Pièces et billets euro en centimes
const denominationsEuro = [
  50000,
  20000,
  10000,
  5000,
  2000,
  1000, // Billets : 500€, 200€, 100€, 50€, 20€, 10€
  500,
  200,
  100, // Billets/Pièces : 5€, 2€, 1€
  50,
  20,
  10,
  5,
  2,
  1, // Pièces : 50c, 20c, 10c, 5c, 2c, 1c
];

console.log("=== Test 1 : Système Euro ===\n");

// Test avec 347,86€ (34786 centimes)
const resultat1 = rendreMonnaieGlouton(denominationsEuro, 34786);
console.log("Rendre 347,86€ :");
console.log(`  Nombre total : ${resultat1.nombreTotal} pièces/billets`);
console.log("  Détail :", resultat1.detail);
console.log(`  Succès : ${resultat1.succes}`);

// Sortie attendue :
// Rendre 347,86€ :
//   Nombre total : 10 pièces/billets
//   Détail : { 20000: 1, 10000: 1, 5000: 1, 2000: 2, 500: 1, 200: 1, 50: 1, 20: 1, 10: 1, 5: 1, 1: 1 }
//   Succès : true
```

---

### Test 2 : Petits Montants

```javascript
// Pièces uniquement (centimes)
const piecesEuro = [50, 20, 10, 5, 2, 1];

console.log("\n=== Test 2 : Petits Montants ===\n");

// Test avec 99 centimes
const resultat2 = rendreMonnaieGlouton(piecesEuro, 99);
console.log("Rendre 99 centimes :");
console.log(
  `  Pièces : ${resultat2.piecesUtilisees.join(" + ")} = ${
    resultat2.montantOriginal
  }c`,
);
console.log(`  Nombre : ${resultat2.nombreTotal}`);

// Sortie :
// Rendre 99 centimes :
//   Pièces : 50 + 20 + 20 + 5 + 2 + 2 = 99c
//   Nombre : 6
```

---

### Test 3 : Système Problématique (Glouton Non Optimal)

```javascript
console.log("\n=== Test 3 : Système Problématique ===\n");

// Système où le glouton ÉCHOUE
const systemeProblematique = [1, 3, 4];

// Rendre 6 centimes
const resultat3 = rendreMonnaieGlouton(systemeProblematique, 6);
console.log("Système {1, 3, 4} - Rendre 6 centimes :");
console.log(
  `  Glouton : ${resultat3.piecesUtilisees.join(" + ")} = ${
    resultat3.nombreTotal
  } pièces`,
);
console.log(`  OPTIMAL serait : 3 + 3 = 2 pièces`);
console.log(`  → Le glouton n'est PAS optimal ici !`);

// Sortie :
// Système {1, 3, 4} - Rendre 6 centimes :
//   Glouton : 4 + 1 + 1 = 3 pièces
//   OPTIMAL serait : 3 + 3 = 2 pièces
//   → Le glouton n'est PAS optimal ici !
```

---

### Test 4 : Montant Impossible

```javascript
console.log("\n=== Test 4 : Montant Impossible ===\n");

// Système sans pièce de 1
const systemeSansPieceDe1 = [5, 10, 20];

// Rendre 7 centimes (impossible sans pièce de 1 ou 2)
const resultat4 = rendreMonnaieGlouton(systemeSansPieceDe1, 7);
console.log("Système {5, 10, 20} - Rendre 7 centimes :");
console.log(
  `  Pièces utilisées : ${resultat4.piecesUtilisees.join(" + ") || "aucune"}`,
);
console.log(`  Reste non rendu : ${resultat4.reste} centimes`);
console.log(`  Succès : ${resultat4.succes}`);

// Sortie :
// Système {5, 10, 20} - Rendre 7 centimes :
//   Pièces utilisées : 5
//   Reste non rendu : 2 centimes
//   Succès : false
```

---

### Test 5 : Cas Limites

```javascript
console.log("\n=== Test 5 : Cas Limites ===\n");

// Montant nul
const resultat5a = rendreMonnaieGlouton(piecesEuro, 0);
console.log("Montant 0 :", resultat5a);
// { nombreTotal: 0, detail: {}, piecesUtilisees: [], reste: 0, succes: true }

// Erreurs attendues
try {
  rendreMonnaieGlouton(piecesEuro, -10);
} catch (e) {
  console.log("Montant négatif :", e.message);
}
// "Le montant ne peut pas être négatif."

try {
  rendreMonnaieGlouton([], 50);
} catch (e) {
  console.log("Tableau vide :", e.message);
}
// "Les dénominations doivent être un tableau non vide."
```

---

## 📊 Analyse de Complexité

Analysons les performances de notre implémentation.

---

### Complexité Temporelle

| Étape             | Complexité         | Explication                        |
| ----------------- | ------------------ | ---------------------------------- |
| Validation        | O(n)               | Parcourir toutes les dénominations |
| Tri               | O(n log n)         | Tri JavaScript (TimSort)           |
| Boucle principale | O(n × M/min_denom) | Au pire, M/1 = M itérations        |
| **Total**         | **O(n log n + M)** | Dominé par le tri ou le montant    |

Où :

- `n` = nombre de dénominations
- `M` = montant à rendre
- `min_denom` = plus petite dénomination

---

### Complexité Spatiale

| Structure           | Taille       | Explication                    |
| ------------------- | ------------ | ------------------------------ |
| denominationsTriees | O(n)         | Copie du tableau               |
| detail              | O(n)         | Au max n clés                  |
| piecesUtilisees     | O(M)         | Au max M pièces (si denom = 1) |
| **Total**           | **O(n + M)** |                                |

---

### Optimisation : Calcul Direct

Pour éviter la boucle `while`, on peut calculer directement le nombre de pièces :

```javascript
function rendreMonnaieGloutonOptimise(denominations, montant) {
  // Validation...
  const denominationsTriees = [...denominations].sort((a, b) => b - a);

  let restant = montant;
  let nombreTotal = 0;
  const detail = {};
  const piecesUtilisees = [];

  for (const denom of denominationsTriees) {
    if (restant >= denom) {
      // Calcul DIRECT au lieu de la boucle while
      const nombrePieces = Math.floor(restant / denom);

      detail[denom] = nombrePieces;
      nombreTotal += nombrePieces;
      restant -= nombrePieces * denom;

      // Pour piecesUtilisees, on doit quand même boucler
      for (let i = 0; i < nombrePieces; i++) {
        piecesUtilisees.push(denom);
      }
    }
  }

  return {
    nombreTotal,
    detail,
    piecesUtilisees,
    reste: restant,
    succes: restant === 0,
    montantOriginal: montant,
  };
}

// Cette version a une complexité O(n log n) seulement !
// (Le tri domine, la boucle principale est O(n))
```

---

## 📝 Micro-Exercice #2 : Optimisation

**Objectif :** Comprendre la différence de complexité.

**Instructions :** Pour rendre 1 000 000 centimes (10 000€) avec le système euro standard, combien d'itérations fait :

1. La version avec `while` ?
2. La version optimisée avec `Math.floor` ?

<details>
<summary>💡 Voir la solution</summary>

```
Dénominations : [50000, 20000, 10000, 5000, 2000, 1000, 500, 200, 100, 50, 20, 10, 5, 2, 1]
Montant : 1 000 000 centimes

VERSION AVEC WHILE :
- 50000 : 1000000 / 50000 = 20 itérations
- Reste 0, donc les autres dénominations = 0 itérations
- Total : 20 itérations du while + 15 itérations du for = 35

VERSION OPTIMISÉE :
- 15 itérations du for seulement (une par dénomination)
- Chaque itération fait UN calcul Math.floor
- Total : 15 itérations

Dans le pire cas (montant en centimes uniquement) :
- Version while : 1 000 000 itérations !
- Version optimisée : 15 itérations

L'optimisation est significative pour les grands montants !
```

</details>

---

## 💼 Application : Caisse Automatique

Créons une classe complète pour simuler une caisse automatique.

---

### Classe CaisseAutomatique

```javascript
/**
 * Classe simulant une caisse automatique.
 * Gère le rendu de monnaie et le stock de pièces/billets.
 */
class CaisseAutomatique {
  constructor(stockInitial = {}) {
    // Stock : { dénomination: quantité }
    this.stock = { ...stockInitial };
    this.historique = [];
  }

  /**
   * Initialise le stock avec des quantités par défaut.
   */
  initialiserStock() {
    // Stock typique d'une caisse belge (en centimes)
    this.stock = {
      50000: 2, // 2 × 500€
      20000: 5, // 5 × 200€
      10000: 10, // 10 × 100€
      5000: 20, // 20 × 50€
      2000: 30, // 30 × 20€
      1000: 50, // 50 × 10€
      500: 50, // 50 × 5€
      200: 100, // 100 × 2€
      100: 100, // 100 × 1€
      50: 100, // 100 × 50c
      20: 100, // 100 × 20c
      10: 100, // 100 × 10c
      5: 100, // 100 × 5c
      2: 100, // 100 × 2c
      1: 200, // 200 × 1c
    };
    console.log("Stock initialisé.");
  }

  /**
   * Rend la monnaie en tenant compte du stock disponible.
   * @param {number} montant - Montant à rendre en centimes.
   * @returns {Object} - Résultat de la transaction.
   */
  rendreMonnaie(montant) {
    if (montant <= 0) {
      return { succes: false, message: "Montant invalide." };
    }

    // Dénominations triées par ordre décroissant
    const denominations = Object.keys(this.stock)
      .map(Number)
      .sort((a, b) => b - a);

    let restant = montant;
    const rendu = {};
    const piecesRendues = [];

    for (const denom of denominations) {
      while (restant >= denom && this.stock[denom] > 0) {
        restant -= denom;
        this.stock[denom]--;
        rendu[denom] = (rendu[denom] || 0) + 1;
        piecesRendues.push(denom);
      }
    }

    const transaction = {
      montantDemande: montant,
      montantRendu: montant - restant,
      reste: restant,
      succes: restant === 0,
      detail: rendu,
      piecesRendues: piecesRendues,
      timestamp: new Date().toISOString(),
    };

    // Enregistrer dans l'historique
    this.historique.push(transaction);

    if (!transaction.succes) {
      // Annuler la transaction : remettre les pièces en stock
      for (const [denom, qte] of Object.entries(rendu)) {
        this.stock[Number(denom)] += qte;
      }
      transaction.message = "Stock insuffisant pour rendre la monnaie exacte.";
    }

    return transaction;
  }

  /**
   * Affiche l'état actuel du stock.
   */
  afficherStock() {
    console.log("\n=== État du Stock ===");
    const denominations = Object.keys(this.stock)
      .map(Number)
      .sort((a, b) => b - a);

    let valeurTotale = 0;
    for (const denom of denominations) {
      const qte = this.stock[denom];
      const valeur = denom * qte;
      valeurTotale += valeur;

      const nomDenom =
        denom >= 100 ? `${(denom / 100).toFixed(0)}€` : `${denom}c`;

      console.log(
        `  ${nomDenom.padStart(6)} : ${qte.toString().padStart(3)} pièces (${(
          valeur / 100
        ).toFixed(2)}€)`,
      );
    }
    console.log(`  ${"─".repeat(35)}`);
    console.log(`  Total : ${(valeurTotale / 100).toFixed(2)}€\n`);
  }

  /**
   * Affiche l'historique des transactions.
   */
  afficherHistorique() {
    console.log("\n=== Historique des Transactions ===");
    for (const trans of this.historique) {
      const statut = trans.succes ? "✅" : "❌";
      console.log(
        `${statut} ${(trans.montantDemande / 100).toFixed(2)}€ → Rendu: ${(
          trans.montantRendu / 100
        ).toFixed(2)}€`,
      );
    }
    console.log();
  }
}
```

---

### Utilisation de la Classe

```javascript
// Créer une caisse
const caisse = new CaisseAutomatique();
caisse.initialiserStock();
caisse.afficherStock();

console.log("=== Transactions ===\n");

// Transaction 1 : Rendre 3,47€
const t1 = caisse.rendreMonnaie(347);
console.log("Rendre 3,47€ :");
console.log(
  `  Pièces : ${t1.piecesRendues
    .map((p) => (p >= 100 ? `${p / 100}€` : `${p}c`))
    .join(" + ")}`,
);
console.log(`  Succès : ${t1.succes}`);

// Transaction 2 : Rendre 12,99€
const t2 = caisse.rendreMonnaie(1299);
console.log("\nRendre 12,99€ :");
console.log(
  `  Pièces : ${t2.piecesRendues
    .map((p) => (p >= 100 ? `${p / 100}€` : `${p}c`))
    .join(" + ")}`,
);
console.log(`  Succès : ${t2.succes}`);

// Afficher le stock après les transactions
caisse.afficherStock();
caisse.afficherHistorique();
```

---

## 📝 Micro-Exercice #3 : Étendre la Classe

**Objectif :** Ajouter une fonctionnalité à la classe.

**Instructions :** Ajoutez une méthode `rechargerStock(denom, quantite)` qui permet d'ajouter des pièces/billets au stock.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Recharge le stock d'une dénomination spécifique.
 * @param {number} denom - La dénomination à recharger (en centimes).
 * @param {number} quantite - Nombre de pièces/billets à ajouter.
 */
rechargerStock(denom, quantite) {
  if (!Number.isInteger(denom) || denom <= 0) {
    throw new Error("Dénomination invalide.");
  }
  if (!Number.isInteger(quantite) || quantite <= 0) {
    throw new Error("Quantité invalide.");
  }

  // Créer la dénomination si elle n'existe pas
  if (!(denom in this.stock)) {
    this.stock[denom] = 0;
  }

  this.stock[denom] += quantite;

  const nomDenom = denom >= 100
    ? `${(denom / 100).toFixed(0)}€`
    : `${denom}c`;

  console.log(`Stock rechargé : +${quantite} × ${nomDenom}`);
}

// Utilisation
caisse.rechargerStock(100, 50);  // +50 pièces de 1€
caisse.rechargerStock(1, 100);   // +100 pièces de 1c
```

</details>

---

## 🔄 Transition vers la Programmation Dynamique

Le problème de la monnaie illustre parfaitement quand le glouton **échoue** et pourquoi la **programmation dynamique** est nécessaire.

---

### Rappel : Quand le Glouton Échoue

```javascript
// Système problématique : {1, 5, 8}
// Rendre 11 centimes

// GLOUTON : 8 + 1 + 1 + 1 = 4 pièces ❌
// OPTIMAL : 5 + 5 + 1 = 3 pièces ✅

// Système problématique : {1, 3, 4}
// Rendre 6 centimes

// GLOUTON : 4 + 1 + 1 = 3 pièces ❌
// OPTIMAL : 3 + 3 = 2 pièces ✅
```

---

### Pourquoi le Glouton Échoue ?

Le glouton choisit **localement** la plus grande pièce, mais cette décision peut **bloquer** une meilleure solution globale.

```
Arbre de décision pour {1, 3, 4} et montant 6 :

                    [6]
                   / | \
                [2] [3] [5]    ← Après avoir choisi 4, 3, ou 1
                /|  /|\ /|\
               ...  ... ...

Glouton : choisit 4 → reste 2 → doit utiliser 2 × 1
          Chemin : 6 → 2 → 1 → 0 (3 pièces)

Optimal : choisit 3 → reste 3 → choisit 3 → reste 0
          Chemin : 6 → 3 → 0 (2 pièces)

Le glouton ne "voit" pas que 3+3 est meilleur que 4+1+1
```

---

### Aperçu de la Programmation Dynamique

La programmation dynamique résout ce problème en explorant **toutes** les possibilités de manière intelligente :

```javascript
// Aperçu (détaillé dans les leçons suivantes)
function coinChangeDP(denominations, montant) {
  // dp[i] = nombre minimum de pièces pour rendre i
  const dp = new Array(montant + 1).fill(Infinity);
  dp[0] = 0;

  for (let i = 1; i <= montant; i++) {
    for (const denom of denominations) {
      if (denom <= i && dp[i - denom] + 1 < dp[i]) {
        dp[i] = dp[i - denom] + 1;
      }
    }
  }

  return dp[montant] === Infinity ? -1 : dp[montant];
}

// Test sur le système problématique
console.log("DP pour {1, 3, 4}, montant 6 :", coinChangeDP([1, 3, 4], 6));
// 2 (3 + 3) ✅ - Trouve l'optimal !
```

---

### Comparaison : Glouton vs Programmation Dynamique

| Aspect                | Glouton                | Programmation Dynamique         |
| --------------------- | ---------------------- | ------------------------------- |
| **Approche**          | Choix local optimal    | Explore tous les sous-problèmes |
| **Optimalité**        | Pas toujours           | Toujours (si applicable)        |
| **Complexité temps**  | O(n log n)             | O(n × M)                        |
| **Complexité espace** | O(n + M)               | O(M)                            |
| **Quand l'utiliser**  | Systèmes "bien conçus" | Systèmes quelconques            |

---

## 💪 Exercices Pratiques

Consolidez vos connaissances avec ces exercices progressifs.

---

### Exercice 1 : Retourner le Tableau des Pièces

**Objectif :** Modifier la fonction pour retourner les pièces dans un format plus lisible.

**Instructions :** Créez une fonction qui retourne une chaîne formatée comme "2 × 50c + 1 × 20c + 3 × 1c".

<details>
<summary>💡 Voir la solution</summary>

```javascript
function formaterResultat(resultat) {
  const parties = [];

  // Trier les dénominations par ordre décroissant
  const denoms = Object.keys(resultat.detail)
    .map(Number)
    .sort((a, b) => b - a);

  for (const denom of denoms) {
    const qte = resultat.detail[denom];
    if (qte > 0) {
      const nomDenom =
        denom >= 100 ? `${(denom / 100).toFixed(0)}€` : `${denom}c`;
      parties.push(`${qte} × ${nomDenom}`);
    }
  }

  return parties.join(" + ");
}

// Test
const piecesEuro = [50, 20, 10, 5, 2, 1];
const resultat = rendreMonnaieGlouton(piecesEuro, 78);
console.log(formaterResultat(resultat));
// "1 × 50c + 1 × 20c + 1 × 5c + 1 × 2c + 1 × 1c"
```

</details>

---

### Exercice 2 : Vérifier l'Optimalité du Système

**Objectif :** Créer une fonction qui teste si un système monétaire est "glouton-optimal".

**Instructions :** Comparez le résultat glouton avec une recherche exhaustive pour tous les montants de 1 à N.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Vérifie si un système monétaire est glouton-optimal.
 * @param {number[]} denominations - Les dénominations du système.
 * @param {number} maxMontant - Tester jusqu'à ce montant.
 * @returns {Object} - Résultat avec les cas où le glouton échoue.
 */
function verifierSystemeGlouton(denominations, maxMontant = 100) {
  const casEchec = [];

  for (let montant = 1; montant <= maxMontant; montant++) {
    const glouton = rendreMonnaieGlouton(denominations, montant);
    const optimal = coinChangeDP(denominations, montant);

    if (glouton.nombreTotal !== optimal) {
      casEchec.push({
        montant,
        glouton: glouton.nombreTotal,
        optimal: optimal,
      });
    }
  }

  return {
    estOptimal: casEchec.length === 0,
    casEchec: casEchec.slice(0, 5), // Premiers cas d'échec
  };
}

// Tests
console.log("Système Euro :", verifierSystemeGlouton([1, 2, 5, 10, 20, 50]));
// { estOptimal: true, casEchec: [] }

console.log("Système {1, 3, 4} :", verifierSystemeGlouton([1, 3, 4]));
// { estOptimal: false, casEchec: [{montant: 6, glouton: 3, optimal: 2}, ...] }
```

</details>

---

### Exercice 3 : Gestion des Euros et Centimes

**Objectif :** Créer une version qui accepte un montant en format "euros.centimes".

**Instructions :** La fonction doit accepter `12.47` pour représenter 12€47.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Rend la monnaie pour un montant en euros (format décimal).
 * @param {number} montantEuros - Montant en euros (ex: 12.47).
 * @returns {Object} - Résultat formaté.
 */
function rendreMonnaieEuros(montantEuros) {
  // Convertir en centimes (attention aux erreurs de virgule flottante)
  const montantCentimes = Math.round(montantEuros * 100);

  // Dénominations euro complètes
  const denominationsEuro = [
    50000,
    20000,
    10000,
    5000,
    2000,
    1000, // Billets
    500,
    200,
    100, // Pièces €
    50,
    20,
    10,
    5,
    2,
    1, // Pièces centimes
  ];

  const resultat = rendreMonnaieGlouton(denominationsEuro, montantCentimes);

  // Formater le résultat
  const formatage = {};
  for (const [denom, qte] of Object.entries(resultat.detail)) {
    const denomNum = Number(denom);
    const cle = denomNum >= 100 ? `${denomNum / 100}€` : `${denomNum}c`;
    formatage[cle] = qte;
  }

  return {
    ...resultat,
    detailFormate: formatage,
    montantEuros: montantEuros,
  };
}

// Test
const r = rendreMonnaieEuros(347.86);
console.log(`Rendre 347,86€ :`);
console.log(`  Total : ${r.nombreTotal} pièces/billets`);
console.log(`  Détail :`, r.detailFormate);
```

</details>

---

### Exercice 4 : Simulation de Distributeur

**Objectif :** Simuler un distributeur automatique complet.

**Instructions :** Créez une classe `Distributeur` avec :

- Un stock de produits avec prix
- Un système de paiement et rendu de monnaie
- Une gestion de l'historique

<details>
<summary>💡 Voir la solution</summary>

```javascript
class Distributeur {
  constructor() {
    this.produits = {
      A1: { nom: "Eau", prix: 150 }, // 1,50€
      A2: { nom: "Soda", prix: 200 }, // 2,00€
      B1: { nom: "Chips", prix: 180 }, // 1,80€
      B2: { nom: "Barre choco", prix: 120 }, // 1,20€
    };
    this.caisse = new CaisseAutomatique();
    this.caisse.initialiserStock();
  }

  acheter(code, montantInsere) {
    const produit = this.produits[code];
    if (!produit) {
      return { succes: false, message: `Produit ${code} inconnu.` };
    }

    if (montantInsere < produit.prix) {
      const manque = produit.prix - montantInsere;
      return {
        succes: false,
        message: `Montant insuffisant. Manque ${(manque / 100).toFixed(2)}€.`,
      };
    }

    const aRendre = montantInsere - produit.prix;
    let rendu = null;

    if (aRendre > 0) {
      rendu = this.caisse.rendreMonnaie(aRendre);
      if (!rendu.succes) {
        return { succes: false, message: "Impossible de rendre la monnaie." };
      }
    }

    return {
      succes: true,
      produit: produit.nom,
      prix: `${(produit.prix / 100).toFixed(2)}€`,
      monnaieRendue: rendu ? `${(aRendre / 100).toFixed(2)}€` : "0€",
      message: `Merci ! Voici votre ${produit.nom}.`,
    };
  }
}

// Utilisation
const distributeur = new Distributeur();
console.log(distributeur.acheter("A1", 200)); // Eau à 1,50€, payé 2€
// { succes: true, produit: 'Eau', monnaieRendue: '0.50€', ... }
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Pourquoi trie-t-on les dénominations par ordre décroissant ?**

- [ ] A. Pour améliorer la lisibilité du code
- [ ] B. Pour que le glouton choisisse d'abord la plus grande dénomination
- [ ] C. Pour réduire la complexité spatiale
- [ ] D. C'est optionnel, le résultat serait identique

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri par ordre **décroissant** est essentiel pour que l'algorithme glouton choisisse toujours la **plus grande dénomination** possible d'abord. C'est le cœur de la stratégie gloutonne pour ce problème.

</details>

---

### Question 2

**Quelle est la complexité temporelle de l'implémentation optimisée ?**

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n × M)
- [ ] D. O(M)

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

L'implémentation optimisée a une complexité de **O(n log n)** dominée par le tri. La boucle principale est O(n) car elle ne fait qu'un calcul par dénomination grâce à `Math.floor`.

</details>

---

### Question 3

**Que retourne la fonction si le montant ne peut pas être rendu exactement ?**

- [ ] A. Une erreur est levée
- [ ] B. Le résultat avec `succes: false` et le reste non rendu
- [ ] C. `null`
- [ ] D. Le montant original

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La fonction retourne un objet avec `succes: false` et `reste > 0` indiquant le montant qui n'a pas pu être rendu. Cela permet à l'appelant de gérer ce cas.

</details>

---

### Question 4

**Pourquoi utilise-t-on `[...denominations].sort()` au lieu de `denominations.sort()` ?**

- [ ] A. Pour des raisons de performance
- [ ] B. Pour ne pas modifier le tableau original
- [ ] C. C'est équivalent, c'est juste une préférence de style
- [ ] D. Pour éviter les erreurs de type

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

L'opérateur spread `[...]` crée une **copie** du tableau. Cela évite de modifier le tableau original passé en paramètre, ce qui serait un effet de bord indésirable.

</details>

---

### Question 5

**Avec le système {1, 5, 8}, combien de pièces le glouton utilise-t-il pour 11 centimes ?**

- [ ] A. 2 pièces
- [ ] B. 3 pièces
- [ ] C. 4 pièces
- [ ] D. 5 pièces

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Le glouton choisit : 8 + 1 + 1 + 1 = **4 pièces** (une pièce de 8, trois pièces de 1). L'optimal serait 5 + 5 + 1 = 3 pièces.

</details>

---

### Question 6

**Quel type de système monétaire garantit l'optimalité du glouton ?**

- [ ] A. Tout système avec une pièce de 1
- [ ] B. Un système où chaque dénomination est divisible par la suivante
- [ ] C. Un système "canonique" comme l'euro ou le dollar
- [ ] D. Aucun système ne garantit l'optimalité

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Les systèmes monétaires "canoniques" comme l'euro ou le dollar sont **conçus** pour que le glouton soit optimal. Ce n'est pas le cas de systèmes arbitraires comme {1, 3, 4}.

</details>

---

### Question 7

**Quelle approche faut-il utiliser pour un système monétaire arbitraire ?**

- [ ] A. Force brute
- [ ] B. Algorithme glouton avec backtracking
- [ ] C. Programmation dynamique
- [ ] D. Tri topologique

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La **programmation dynamique** garantit de trouver la solution optimale pour n'importe quel système monétaire, même ceux où le glouton échoue.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Tri Essentiel

Toujours trier les dénominations par **ordre décroissant** avant d'appliquer l'algorithme glouton.

### 2. Validation des Entrées

Gérer les cas limites : montant nul, négatif, dénominations invalides.

### 3. Structure du Résultat

Retourner un objet complet : nombre total, détail par dénomination, liste des pièces, statut de succès.

### 4. Optimisation avec Math.floor

Calculer directement le nombre de pièces au lieu de boucler avec `while`.

### 5. Gestion du Stock

En pratique, tenir compte du stock disponible de chaque dénomination.

### 6. Limites du Glouton

Fonctionne pour les systèmes "canoniques" (euro, dollar), mais pas pour tous les systèmes.

### 7. Transition vers la Programmation Dynamique

Pour les systèmes arbitraires, la programmation dynamique est nécessaire.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant l'implémentation d'un algorithme glouton pour le problème de la monnaie !

### Ce que vous avez appris aujourd'hui

- Implémenter un algorithme glouton **complet et robuste**
- Gérer les **cas limites** et les entrées invalides
- **Optimiser** l'algorithme avec le calcul direct
- Créer une **classe métier** (CaisseAutomatique)
- Comprendre les **limites** du glouton
- Préparer la transition vers la **programmation dynamique**

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter des algorithmes gloutons en JavaScript
- Valider et tester vos implémentations
- Créer des applications réalistes (caisse, distributeur)
- Identifier quand le glouton n'est pas suffisant

### Pourquoi c'est important

> 📌 **Point Clé**
>
> L'implémentation robuste d'algorithmes est une compétence clé en développement. Les algorithmes gloutons sont utilisés dans de nombreux domaines : optimisation de ressources, planification, compression de données (Huffman), routage réseau (Dijkstra)... Mais savoir reconnaître leurs limites est tout aussi important !

---

## ➡️ Prochaine Étape : Leçon 33

### Ce qui vous attend

La prochaine leçon, **« Programmation Dynamique : Sous-Problèmes Chevauchants et Sous-Structure Optimale »**, vous introduira à ce paradigme puissant.

**Vous découvrirez :**

- Les **deux propriétés** de la programmation dynamique
- Le concept de **sous-problèmes chevauchants**
- La **mémorisation** pour éviter les calculs redondants
- Comment résoudre les problèmes où le glouton échoue

### Préparez-vous !

La programmation dynamique est plus complexe que le glouton, mais elle résout une classe beaucoup plus large de problèmes. Elle est incontournable pour les entretiens techniques et l'optimisation avancée !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Wikipedia - Coin Problem](https://en.wikipedia.org/wiki/Change-making_problem) - Théorie du problème
- [MIT OpenCourseWare](https://ocw.mit.edu/courses/6-046j-design-and-analysis-of-algorithms-spring-2015/) - Cours algorithmique
- [JavaScript.info](https://javascript.info/) - Référence JavaScript

### Outils de pratique

- **[LeetCode - Coin Change](https://leetcode.com/problems/coin-change/)** : Le problème classique
- **[HackerRank - The Coin Change Problem](https://www.hackerrank.com/challenges/coin-change)** : Variantes

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ?

N'hésitez pas à :

- Tester avec différents systèmes monétaires
- Chercher des contre-exemples où le glouton échoue
- Implémenter votre propre classe de caisse

> 💡 **Conseil**
>
> La meilleure façon de maîtriser l'implémentation d'algorithmes est de **coder sans regarder la solution**, puis de comparer. Essayez de recréer la fonction `rendreMonnaieGlouton` de mémoire !

---

**Prêt pour la Leçon 33 ?** 🚀

La programmation dynamique vous attend pour résoudre les problèmes les plus complexes !

---

<div align="center">

**Leçon 32 sur 42 - Module 6 : Paradigmes Avancés de Conception d'Algorithmes**

[⬅️ Leçon 31 : Algorithmes Gloutons](./lecon-1-algorithmes-gloutons-strategie-resolution-problemes-simples.md) | [Retour au sommaire](./README.md) | [Leçon 33 : Programmation Dynamique - Concepts ➡️](./lecon-3-programmation-dynamique-sous-problemes-chevauchants-sous-structure-optimale.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
