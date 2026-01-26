##### Leçon 31 sur 42

# Algorithmes Gloutons : Stratégie et Résolution de Problèmes Simples

**Module 6** : Paradigmes Avancés de Conception d'Algorithmes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le **principe des algorithmes gloutons** (choix localement optimal)
- Identifier les **deux propriétés** nécessaires (choix glouton + sous-structure optimale)
- Reconnaître quand un algorithme glouton **fonctionne** ou **échoue**
- Appliquer la stratégie gloutonne au **problème de la monnaie**
- Résoudre le **problème de sélection d'activités**
- Comprendre le **problème du sac à dos fractionnaire**

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Module 5 complété** : Arbres et parcours de graphes
- **Module 3** : Algorithmes de tri
- **Complexité algorithmique** : Notation Big O
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : La Stratégie du "Meilleur Choix Immédiat"

Imaginez que vous êtes dans un supermarché et que vous voulez remplir votre panier avec les produits les plus intéressants, mais vous avez un budget limité. Une stratégie simple serait de **toujours prendre le produit le moins cher** qui rentre dans votre budget, puis de répéter jusqu'à épuisement du budget.

C'est exactement le principe d'un **algorithme glouton** (greedy algorithm) : faire le **meilleur choix local** à chaque étape, en espérant que cela mène à la **meilleure solution globale**.

> **Point Clé**
>
> Un algorithme glouton ne revient **jamais** sur ses décisions. Une fois qu'un choix est fait, il est définitif. Cette simplicité est à la fois sa force (rapidité) et sa faiblesse (pas toujours optimal).

---

## 📦 Principe des Algorithmes Gloutons

Un algorithme glouton construit une solution **étape par étape**, en choisissant à chaque étape l'option qui semble la meilleure **sur le moment**.

---

### La Stratégie Gloutonne

```
ALGORITHME GLOUTON :

1. TANT QUE le problème n'est pas résolu :
   a. Évaluer toutes les options disponibles
   b. Choisir la MEILLEURE option selon un critère défini
   c. Ajouter ce choix à la solution
   d. Réduire le problème en tenant compte du choix fait

2. Retourner la solution construite
```

---

### Caractéristiques Clés

| Caractéristique  | Description                                 |
| ---------------- | ------------------------------------------- |
| **Choix local**  | Décision basée uniquement sur l'état actuel |
| **Irréversible** | Pas de retour en arrière (backtracking)     |
| **Incrémental**  | Solution construite progressivement         |
| **Simple**       | Généralement facile à implémenter           |
| **Rapide**       | Souvent en O(n) ou O(n log n)               |

---

### Les Deux Propriétés Essentielles

Pour qu'un algorithme glouton donne une solution **optimale**, deux propriétés doivent être satisfaites :

#### 1. Propriété du Choix Glouton

> Le meilleur choix local contribue à une solution globale optimale.

Si vous faites le meilleur choix maintenant, vous pouvez atteindre la meilleure solution finale en continuant à faire des choix gloutons sur le sous-problème restant.

#### 2. Sous-Structure Optimale

> Une solution optimale au problème contient des solutions optimales à ses sous-problèmes.

Si vous divisez le problème après un choix glouton, la solution optimale du problème original combine le choix glouton avec une solution optimale du sous-problème.

---

### Visualisation : Glouton vs Optimal

```
Arbre de décision pour un problème :

                    [Problème]
                   /    |    \
                [A]    [B]   [C]    ← Choix possibles
               / \     / \    / \
             [D][E]  [F][G] [H][I]

GLOUTON : Choisit toujours le "meilleur" à chaque niveau
          Si A semble meilleur → choisit A → puis E si meilleur
          Résultat : A → E (peut-être sous-optimal)

OPTIMAL : Explore tous les chemins pour trouver le meilleur
          Résultat : B → G (vraiment optimal)

Le glouton fonctionne SI le meilleur choix local
mène toujours au meilleur résultat global !
```

---

## 📝 Micro-Exercice #1 : Identifier un Problème Glouton

**Objectif :** Reconnaître si un problème est adapté à une approche gloutonne.

**Instructions :** Pour chaque scénario, dites si une approche gloutonne est appropriée :

1. Trouver le chemin le plus court dans un graphe pondéré
2. Rendre la monnaie avec des pièces de 1€, 2€, 5€, 10€, 20€, 50€
3. Trouver la plus longue sous-séquence commune de deux chaînes
4. Sélectionner le maximum d'activités non-chevauchantes

<details>
<summary>💡 Voir la solution</summary>

```
1. Chemin le plus court : NON glouton (sauf Dijkstra pour certains cas)
   → Le choix local (arête la plus courte) ne garantit pas le chemin global optimal

2. Rendre la monnaie (système euro) : OUI glouton
   → Les dénominations sont conçues pour que le glouton fonctionne

3. Plus longue sous-séquence commune : NON glouton
   → Nécessite la programmation dynamique

4. Sélection d'activités : OUI glouton
   → Choisir l'activité qui finit le plus tôt est optimal
```

</details>

---

## 💶 Application : Le Problème de la Monnaie

Le problème classique : rendre une somme donnée avec le **minimum de pièces**.

---

### Scénario : Caissier dans un magasin belge

Ingrid est caissière dans un magasin à Bruxelles. Elle doit rendre **78 centimes** à un client en utilisant le moins de pièces possible.

**Pièces disponibles** : 50c, 20c, 10c, 5c, 2c, 1c

---

### Stratégie Gloutonne

> À chaque étape, choisir la **plus grande pièce** qui ne dépasse pas le montant restant.

```
Montant à rendre : 78 centimes

Étape 1 : Plus grande pièce ≤ 78c → 50c
          Rendre 50c. Reste : 78 - 50 = 28c

Étape 2 : Plus grande pièce ≤ 28c → 20c
          Rendre 20c. Reste : 28 - 20 = 8c

Étape 3 : Plus grande pièce ≤ 8c → 5c
          Rendre 5c. Reste : 8 - 5 = 3c

Étape 4 : Plus grande pièce ≤ 3c → 2c
          Rendre 2c. Reste : 3 - 2 = 1c

Étape 5 : Plus grande pièce ≤ 1c → 1c
          Rendre 1c. Reste : 1 - 1 = 0c

Résultat : 50c + 20c + 5c + 2c + 1c = 5 pièces
```

---

### Implémentation en JavaScript

```javascript
/**
 * Rend la monnaie avec le minimum de pièces (algorithme glouton).
 * @param {number} montant - Montant à rendre en centimes.
 * @param {number[]} pieces - Pièces disponibles (triées par ordre décroissant).
 * @returns {Object} - Résultat avec le détail et le nombre total de pièces.
 */
function rendreMonnaieGlouton(montant, pieces) {
  // S'assurer que les pièces sont triées par ordre décroissant
  const piecesTries = [...pieces].sort((a, b) => b - a);

  const resultat = {};
  let restant = montant;
  let totalPieces = 0;

  for (const piece of piecesTries) {
    if (restant >= piece) {
      const nombrePieces = Math.floor(restant / piece);
      resultat[piece] = nombrePieces;
      restant -= nombrePieces * piece;
      totalPieces += nombrePieces;
    }
  }

  return {
    detail: resultat,
    totalPieces: totalPieces,
    resteNonRendu: restant,
  };
}

// Test avec les pièces euro
const piecesEuro = [50, 20, 10, 5, 2, 1]; // centimes

console.log("Rendre 78 centimes :");
console.log(rendreMonnaieGlouton(78, piecesEuro));
// { detail: { 50: 1, 20: 1, 5: 1, 2: 1, 1: 1 }, totalPieces: 5, resteNonRendu: 0 }

console.log("\nRendre 99 centimes :");
console.log(rendreMonnaieGlouton(99, piecesEuro));
// { detail: { 50: 1, 20: 2, 5: 1, 2: 2 }, totalPieces: 6, resteNonRendu: 0 }

console.log("\nRendre 1€47 (147 centimes) :");
console.log(rendreMonnaieGlouton(147, piecesEuro));
// { detail: { 50: 2, 20: 2, 5: 1, 2: 1 }, totalPieces: 6, resteNonRendu: 0 }
```

---

### Pourquoi ça Fonctionne avec l'Euro ?

Le système monétaire de l'euro est **conçu** pour que l'algorithme glouton fonctionne :

- Chaque grande pièce est un multiple ou proche des petites
- 50 = 2×20 + 10 = 5×10 = 10×5...
- Pas de "trous" problématiques dans les dénominations

---

### Contre-Exemple : Quand le Glouton Échoue

Considérons un système monétaire hypothétique avec des pièces de **{1, 3, 4}** centimes.
Objectif : rendre **6 centimes**.

```
GLOUTON :
- Plus grande pièce ≤ 6 → 4c. Reste : 6 - 4 = 2c
- Plus grande pièce ≤ 2 → 1c. Reste : 2 - 1 = 1c
- Plus grande pièce ≤ 1 → 1c. Reste : 1 - 1 = 0c

Résultat glouton : 4c + 1c + 1c = 3 pièces

OPTIMAL :
- 3c + 3c = 2 pièces

Le glouton a échoué car le système {1, 3, 4} ne satisfait pas
la propriété du choix glouton !
```

```javascript
// Démonstration de l'échec du glouton
const piecesProblematiques = [4, 3, 1];

console.log("\nSystème {1, 3, 4} - Rendre 6 centimes :");
console.log(rendreMonnaieGlouton(6, piecesProblematiques));
// { detail: { 4: 1, 1: 2 }, totalPieces: 3, resteNonRendu: 0 }
// Le glouton trouve 3 pièces, mais 2 pièces de 3 seraient mieux !
```

> **Attention**
>
> L'algorithme glouton pour la monnaie ne fonctionne **pas toujours**. Il dépend des dénominations disponibles. Pour un système arbitraire, la **programmation dynamique** est nécessaire (vue dans les leçons suivantes).

---

## 📝 Micro-Exercice #2 : Tester le Glouton

**Objectif :** Comprendre les limites de l'algorithme glouton.

**Instructions :** Avec le système de pièces **{1, 5, 8, 10}**, rendez **17 centimes** :

1. Appliquez l'algorithme glouton
2. Trouvez la solution optimale
3. Expliquez pourquoi le glouton échoue (ou réussit)

<details>
<summary>💡 Voir la solution</summary>

```
GLOUTON :
- Plus grande ≤ 17 → 10c. Reste : 7c
- Plus grande ≤ 7 → 5c. Reste : 2c
- Plus grande ≤ 2 → 1c. Reste : 1c
- Plus grande ≤ 1 → 1c. Reste : 0c

Résultat glouton : 10 + 5 + 1 + 1 = 4 pièces

OPTIMAL :
- 8c + 8c + 1c = 3 pièces

Le glouton échoue car choisir 10c empêche d'utiliser
deux pièces de 8c qui seraient plus efficaces.
```

</details>

---

## 📅 Application : Le Problème de Sélection d'Activités

Un problème classique où l'algorithme glouton est **optimal** !

---

### Scénario

Germain organise une journée de team-building à Anvers. Il a une liste d'activités possibles avec leurs horaires, mais il ne peut en faire qu'**une à la fois**. Il veut **maximiser le nombre d'activités**.

---

### Les Activités Disponibles

| Activité               | Début | Fin   | Durée |
| ---------------------- | ----- | ----- | ----- |
| Visite du port         | 9h00  | 11h00 | 2h    |
| Musée MAS              | 10h00 | 12h00 | 2h    |
| Déjeuner gastronomique | 11h30 | 13h30 | 2h    |
| Balade en bateau       | 13h00 | 15h00 | 2h    |
| Zoo d'Anvers           | 14h00 | 17h00 | 3h    |
| Cathédrale             | 15h30 | 17h00 | 1h30  |
| Dîner                  | 18h00 | 20h00 | 2h    |

---

### Stratégie Gloutonne : Choisir par Fin la Plus Tôt

> À chaque étape, choisir l'activité qui **se termine le plus tôt** parmi celles qui ne chevauchent pas les activités déjà choisies.

**Pourquoi "fin la plus tôt" ?**

- Terminer tôt laisse le **maximum de temps** pour les activités suivantes
- Intuitivement : ne pas "bloquer" la suite de la journée

---

### Application Pas à Pas

```
1. Trier par heure de FIN (croissant) :
   - Visite du port (9h-11h)
   - Musée MAS (10h-12h)
   - Déjeuner (11h30-13h30)
   - Balade en bateau (13h-15h)
   - Cathédrale (15h30-17h)
   - Zoo (14h-17h)
   - Dîner (18h-20h)

2. Sélection gloutonne :

   Visite du port (9h-11h)
      → Fin à 11h. Prochaine activité doit commencer ≥ 11h

   Musée MAS (10h-12h)
      → Commence à 10h < 11h. CONFLIT !

   Déjeuner (11h30-13h30)
      → Commence à 11h30 ≥ 11h. OK !
      → Fin à 13h30. Prochaine activité doit commencer ≥ 13h30

   Balade en bateau (13h-15h)
      → Commence à 13h < 13h30. CONFLIT !

   Cathédrale (15h30-17h)
      → Commence à 15h30 ≥ 13h30. OK !
      → Fin à 17h. Prochaine activité doit commencer ≥ 17h

   Zoo (14h-17h)
      → Commence à 14h < 17h. CONFLIT !

   Dîner (18h-20h)
      → Commence à 18h ≥ 17h. OK !

3. Résultat : 4 activités
   - Visite du port (9h-11h)
   - Déjeuner (11h30-13h30)
   - Cathédrale (15h30-17h)
   - Dîner (18h-20h)
```

---

### Implémentation en JavaScript

```javascript
/**
 * Sélectionne le maximum d'activités non-chevauchantes.
 * @param {Array} activites - Liste d'activités {nom, debut, fin}.
 * @returns {Array} - Activités sélectionnées.
 */
function selectionActivites(activites) {
  // Trier par heure de fin (croissant)
  const activitesTriees = [...activites].sort((a, b) => a.fin - b.fin);

  const selection = [];
  let derniereFinHeure = 0;

  for (const activite of activitesTriees) {
    // Si l'activité commence après (ou à) la fin de la dernière
    if (activite.debut >= derniereFinHeure) {
      selection.push(activite);
      derniereFinHeure = activite.fin;
    }
  }

  return selection;
}

// Activités de la journée (heures en décimal pour simplifier)
const activitesAnvers = [
  { nom: "Visite du port", debut: 9, fin: 11 },
  { nom: "Musée MAS", debut: 10, fin: 12 },
  { nom: "Déjeuner gastronomique", debut: 11.5, fin: 13.5 },
  { nom: "Balade en bateau", debut: 13, fin: 15 },
  { nom: "Zoo d'Anvers", debut: 14, fin: 17 },
  { nom: "Cathédrale", debut: 15.5, fin: 17 },
  { nom: "Dîner", debut: 18, fin: 20 },
];

console.log("=== Sélection d'Activités - Journée à Anvers ===\n");

const selection = selectionActivites(activitesAnvers);

console.log(`Nombre d'activités sélectionnées : ${selection.length}\n`);
console.log("Planning optimal :");
selection.forEach((a, i) => {
  console.log(`${i + 1}. ${a.nom} (${a.debut}h - ${a.fin}h)`);
});

// Sortie :
// Nombre d'activités sélectionnées : 4
// Planning optimal :
// 1. Visite du port (9h - 11h)
// 2. Déjeuner gastronomique (11.5h - 13.5h)
// 3. Cathédrale (15.5h - 17h)
// 4. Dîner (18h - 20h)
```

---

### Pourquoi Cette Stratégie est Optimale ?

La **preuve** repose sur un argument d'échange :

1. Supposons qu'il existe une solution optimale O qui ne commence pas par l'activité qui finit le plus tôt (appelons-la A₁)
2. Soit A' la première activité de O. Comme A₁ finit avant ou en même temps que A', on peut **remplacer** A' par A₁
3. Cette nouvelle solution a **au moins** autant d'activités que O
4. Par récurrence, on peut transformer O en une solution qui utilise notre stratégie gloutonne

---

## 📝 Micro-Exercice #3 : Sélection d'Activités

**Objectif :** Appliquer l'algorithme de sélection d'activités.

**Instructions :** Sélectionnez le maximum d'activités parmi :

| Activité | Début | Fin |
| -------- | ----- | --- |
| L        | 1     | 3   |
| M        | 2     | 4   |
| N        | 0     | 5   |
| O        | 3     | 6   |
| P        | 5     | 8   |
| Q        | 7     | 9   |

<details>
<summary>💡 Voir la solution</summary>

```
1. Trier par fin : L(1-3), M(2-4), N(0-5), O(3-6), P(5-8), Q(7-9)

2. Sélection :
   L (1-3) → dernièreFin = 3
   M (2-4) → 2 < 3, CONFLIT
   N (0-5) → 0 < 3, CONFLIT
   O (3-6) → 3 ≥ 3, OK → dernièreFin = 6
   P (5-8) → 5 < 6, CONFLIT
   Q (7-9) → 7 ≥ 6, OK → dernièreFin = 9

3. Résultat : L, O, Q → 3 activités
```

</details>

---

## 🎒 Application : Le Sac à Dos Fractionnaire

Contrairement au problème du sac à dos 0/1 (programmation dynamique), le sac à dos **fractionnaire** peut être résolu avec un algorithme glouton !

---

### Scénario

Chermann fait une randonnée dans les Ardennes belges. Son sac peut supporter **15 kg** maximum. Il trouve des objets avec différentes valeurs au marché :

| Objet              | Poids (kg) | Valeur (€) | Ratio (€/kg) |
| ------------------ | ---------- | ---------- | ------------ |
| Chocolat belge     | 5          | 30         | 6.0          |
| Bières artisanales | 8          | 40         | 5.0          |
| Fromage de Herve   | 3          | 12         | 4.0          |
| Gaufres            | 4          | 20         | 5.0          |

**Particularité** : Il peut prendre des **fractions** d'objets (par exemple, la moitié des chocolats).

---

### Stratégie Gloutonne : Ratio Valeur/Poids

> Prendre en priorité les objets avec le **meilleur ratio valeur/poids**.

```
1. Calculer les ratios valeur/poids :
   - Chocolat : 30/5 = 6 €/kg
   - Bières : 40/8 = 5 €/kg
   - Fromage : 12/3 = 4 €/kg
   - Gaufres : 20/4 = 5 €/kg

2. Trier par ratio décroissant :
   1. Chocolat (6 €/kg)
   2. Bières (5 €/kg) / Gaufres (5 €/kg)
   3. Fromage (4 €/kg)

3. Remplir le sac (capacité : 15 kg) :

    Chocolat : 5 kg, 30€
      Capacité restante : 15 - 5 = 10 kg
      Valeur : 30€

    Bières : 8 kg, 40€
      Capacité restante : 10 - 8 = 2 kg
      Valeur : 30 + 40 = 70€

    Gaufres : 4 kg > 2 kg disponibles
      Prendre fraction : 2 kg / 4 kg = 0.5 (50%)
      Valeur fractionnaire : 0.5 × 20€ = 10€
      Capacité restante : 0 kg
      Valeur totale : 70 + 10 = 80€

4. Résultat : 80€ de valeur totale
   - 100% du Chocolat (5 kg)
   - 100% des Bières (8 kg)
   - 50% des Gaufres (2 kg)
```

---

### Implémentation en JavaScript

```javascript
/**
 * Résout le problème du sac à dos fractionnaire.
 * @param {Array} objets - Liste d'objets {nom, poids, valeur}.
 * @param {number} capacite - Capacité maximale du sac.
 * @returns {Object} - Solution avec détails et valeur totale.
 */
function sacAdosFractionnaire(objets, capacite) {
  // Calculer le ratio valeur/poids et trier par ratio décroissant
  const objetsAvecRatio = objets
    .map((obj) => ({
      ...obj,
      ratio: obj.valeur / obj.poids,
    }))
    .sort((a, b) => b.ratio - a.ratio);

  const selection = [];
  let capaciteRestante = capacite;
  let valeurTotale = 0;

  for (const obj of objetsAvecRatio) {
    if (capaciteRestante === 0) break;

    if (obj.poids <= capaciteRestante) {
      // Prendre l'objet entier
      selection.push({
        nom: obj.nom,
        fraction: 1,
        poidsPris: obj.poids,
        valeurPrise: obj.valeur,
      });
      capaciteRestante -= obj.poids;
      valeurTotale += obj.valeur;
    } else {
      // Prendre une fraction de l'objet
      const fraction = capaciteRestante / obj.poids;
      const valeurFraction = fraction * obj.valeur;

      selection.push({
        nom: obj.nom,
        fraction: fraction,
        poidsPris: capaciteRestante,
        valeurPrise: valeurFraction,
      });

      valeurTotale += valeurFraction;
      capaciteRestante = 0;
    }
  }

  return {
    selection: selection,
    valeurTotale: valeurTotale,
    poidsTotal: capacite - capaciteRestante,
  };
}

// Test
const objetsMarcheArdennes = [
  { nom: "Chocolat belge", poids: 5, valeur: 30 },
  { nom: "Bières artisanales", poids: 8, valeur: 40 },
  { nom: "Fromage de Herve", poids: 3, valeur: 12 },
  { nom: "Gaufres", poids: 4, valeur: 20 },
];

console.log("=== Sac à Dos Fractionnaire - Randonnée Ardennes ===\n");

const resultat = sacAdosFractionnaire(objetsMarcheArdennes, 15);

console.log("Objets sélectionnés :");
resultat.selection.forEach((item) => {
  const pourcentage = (item.fraction * 100).toFixed(0);
  console.log(
    `  - ${item.nom}: ${pourcentage}% (${item.poidsPris}kg, ${item.valeurPrise.toFixed(2)}€)`,
  );
});

console.log(`\nValeur totale : ${resultat.valeurTotale.toFixed(2)}€`);
console.log(`Poids total : ${resultat.poidsTotal}kg / 15kg`);

// Sortie :
// Objets sélectionnés :
//   - Chocolat belge: 100% (5kg, 30.00€)
//   - Bières artisanales: 100% (8kg, 40.00€)
//   - Gaufres: 50% (2kg, 10.00€)
// Valeur totale : 80.00€
// Poids total : 15kg / 15kg
```

---

### Différence avec le Sac à Dos 0/1

| Aspect                 | Fractionnaire | 0/1                     |
| ---------------------- | ------------- | ----------------------- |
| **Objets**             | Divisibles    | Entiers uniquement      |
| **Algorithme**         | Glouton       | Programmation dynamique |
| **Complexité**         | O(n log n)    | O(n × W)                |
| **Optimalité glouton** | Garantie      | Non garantie            |

> **Point Clé**
>
> Le sac à dos **fractionnaire** est résolu optimalement par un algorithme glouton car on peut toujours "compléter" le sac avec une fraction de l'objet le plus rentable. Le sac à dos **0/1** ne permet pas cela, donc le glouton peut échouer.

---

## 📊 Analyse de Complexité des Algorithmes Gloutons

Les algorithmes gloutons sont généralement **efficaces** grâce à leur simplicité.

---

### Complexités Typiques

| Problème                    | Étape dominante     | Complexité |
| --------------------------- | ------------------- | ---------- |
| **Monnaie (euro)**          | Parcours des pièces | O(n)       |
| **Sélection d'activités**   | Tri par fin         | O(n log n) |
| **Sac à dos fractionnaire** | Tri par ratio       | O(n log n) |

---

### Pourquoi les Gloutons sont Rapides ?

1. **Pas de backtracking** : On ne revient jamais en arrière
2. **Décision unique** : Un seul choix par élément
3. **Tri préalable** : Souvent en O(n log n), puis parcours en O(n)

```
Comparaison avec d'autres paradigmes :

GLOUTON :        O(n) ou O(n log n)
                 Simple, rapide, pas toujours optimal

FORCE BRUTE :    O(2^n) ou O(n!)
                 Explore tout, toujours optimal, très lent

PROG. DYNAMIQUE: O(n × W) ou O(n²)
                 Plus lent, mais optimal pour plus de problèmes
```

---

## 💼 Étude de Cas : Planning d'une Équipe

Prudence est manager d'une équipe de développeurs à Gand. Elle doit assigner des tâches pour maximiser la productivité de la semaine.

---

### Les Tâches Disponibles

| Tâche           | Priorité | Temps estimé | Deadline (jour) |
| --------------- | -------- | ------------ | --------------- |
| Bug critique    | 10       | 2h           | 1               |
| Feature A       | 7        | 4h           | 2               |
| Refactoring     | 5        | 3h           | 3               |
| Documentation   | 3        | 2h           | 5               |
| Tests unitaires | 6        | 3h           | 2               |
| Code review     | 4        | 1h           | 1               |

---

### Stratégie 1 : Par Priorité Décroissante

```javascript
function planifierParPriorite(taches) {
  return [...taches].sort((a, b) => b.priorite - a.priorite);
}

const taches = [
  { nom: "Bug critique", priorite: 10, temps: 2, deadline: 1 },
  { nom: "Feature A", priorite: 7, temps: 4, deadline: 2 },
  { nom: "Refactoring", priorite: 5, temps: 3, deadline: 3 },
  { nom: "Documentation", priorite: 3, temps: 2, deadline: 5 },
  { nom: "Tests unitaires", priorite: 6, temps: 3, deadline: 2 },
  { nom: "Code review", priorite: 4, temps: 1, deadline: 1 },
];

console.log(
  "Par priorité :",
  planifierParPriorite(taches).map((t) => t.nom),
);
// Bug critique, Feature A, Tests unitaires, Refactoring, Code review, Documentation
```

---

### Stratégie 2 : Par Deadline la Plus Proche

```javascript
function planifierParDeadline(taches) {
  return [...taches].sort((a, b) => a.deadline - b.deadline);
}

console.log(
  "Par deadline :",
  planifierParDeadline(taches).map((t) => t.nom),
);
// Bug critique, Code review, Feature A, Tests unitaires, Refactoring, Documentation
```

---

### Stratégie 3 : Par Ratio Priorité/Temps

```javascript
function planifierParRatio(taches) {
  return [...taches]
    .map((t) => ({ ...t, ratio: t.priorite / t.temps }))
    .sort((a, b) => b.ratio - a.ratio);
}

console.log("Par ratio P/T :");
const parRatio = planifierParRatio(taches);
parRatio.forEach((t) => {
  console.log(
    `  ${t.nom}: ${t.ratio.toFixed(2)} (P=${t.priorite}, T=${t.temps}h)`,
  );
});
// Bug critique: 5.00, Code review: 4.00, Tests unitaires: 2.00, ...
```

---

### Quelle Stratégie Choisir ?

| Objectif                           | Stratégie recommandée    |
| ---------------------------------- | ------------------------ |
| Maximiser la valeur totale         | Par priorité             |
| Respecter toutes les deadlines     | Par deadline (EDF)       |
| Meilleur retour sur investissement | Par ratio priorité/temps |

> **Conseil**
>
> En pratique, le choix de la stratégie gloutonne dépend du **critère d'optimisation**. Il n'y a pas de "meilleure" stratégie universelle !

---

## 💪 Exercices Pratiques

Consolidez vos connaissances avec ces exercices progressifs.

---

### Exercice 1 : Monnaie avec Système Euro

**Objectif :** Implémenter le rendu de monnaie en euros.

**Instructions :** Écrivez une fonction qui rend la monnaie pour un montant donné en utilisant les billets et pièces euro (500€, 200€, 100€, 50€, 20€, 10€, 5€, 2€, 1€, 50c, 20c, 10c, 5c, 2c, 1c). Testez avec 347,86€.

<details>
<summary>💡 Voir la solution</summary>

```javascript
function rendreMonnaieEuro(montantEuros) {
  // Convertir en centimes pour éviter les erreurs de virgule flottante
  let montantCentimes = Math.round(montantEuros * 100);

  // Toutes les valeurs en centimes
  const denominations = [
    { valeur: 50000, nom: "500€" },
    { valeur: 20000, nom: "200€" },
    { valeur: 10000, nom: "100€" },
    { valeur: 5000, nom: "50€" },
    { valeur: 2000, nom: "20€" },
    { valeur: 1000, nom: "10€" },
    { valeur: 500, nom: "5€" },
    { valeur: 200, nom: "2€" },
    { valeur: 100, nom: "1€" },
    { valeur: 50, nom: "50c" },
    { valeur: 20, nom: "20c" },
    { valeur: 10, nom: "10c" },
    { valeur: 5, nom: "5c" },
    { valeur: 2, nom: "2c" },
    { valeur: 1, nom: "1c" },
  ];

  const resultat = [];
  let totalPieces = 0;

  for (const denom of denominations) {
    if (montantCentimes >= denom.valeur) {
      const nombre = Math.floor(montantCentimes / denom.valeur);
      resultat.push({ denomination: denom.nom, nombre: nombre });
      montantCentimes -= nombre * denom.valeur;
      totalPieces += nombre;
    }
  }

  return { detail: resultat, total: totalPieces };
}

// Test
console.log(rendreMonnaieEuro(347.86));
// 1 × 200€, 1 × 100€, 2 × 20€, 1 × 5€, 1 × 2€, 1 × 50c, 1 × 20c, 1 × 10c, 1 × 5c, 1 × 1c
// Total : 10 billets/pièces
```

</details>

---

### Exercice 2 : Planification de Salles de Réunion

**Objectif :** Maximiser le nombre de réunions dans une salle.

**Instructions :** Une salle de réunion est disponible de 8h à 18h. Sélectionnez le maximum de réunions parmi :

| Réunion         | Début | Fin   |
| --------------- | ----- | ----- |
| Standup         | 9h00  | 9h30  |
| Planning        | 9h15  | 10h30 |
| Client A        | 10h00 | 11h30 |
| Démo            | 11h00 | 12h00 |
| Déjeuner équipe | 12h00 | 13h00 |
| Brainstorm      | 13h30 | 15h00 |
| Client B        | 14h00 | 16h00 |
| Rétro           | 15h30 | 17h00 |

<details>
<summary>💡 Voir la solution</summary>

```javascript
const reunions = [
  { nom: "Standup", debut: 9, fin: 9.5 },
  { nom: "Planning", debut: 9.25, fin: 10.5 },
  { nom: "Client A", debut: 10, fin: 11.5 },
  { nom: "Démo", debut: 11, fin: 12 },
  { nom: "Déjeuner équipe", debut: 12, fin: 13 },
  { nom: "Brainstorm", debut: 13.5, fin: 15 },
  { nom: "Client B", debut: 14, fin: 16 },
  { nom: "Rétro", debut: 15.5, fin: 17 },
];

const selection = selectionActivites(reunions);
console.log(`${selection.length} réunions sélectionnées :`);
selection.forEach((r) => console.log(`  - ${r.nom} (${r.debut}h - ${r.fin}h)`));

// Résultat : 5 réunions
// - Standup (9h - 9h30)
// - Démo (11h - 12h)
// - Déjeuner équipe (12h - 13h)
// - Brainstorm (13h30 - 15h)
// - Rétro (15h30 - 17h)
```

</details>

---

### Exercice 3 : Sac à Dos Fractionnaire - Livraison

**Objectif :** Maximiser les revenus d'une livraison.

**Instructions :** Un livreur a un vélo cargo de capacité 20 kg. Il doit choisir parmi :

| Colis        | Poids | Commission |
| ------------ | ----- | ---------- |
| Livres       | 6 kg  | 18€        |
| Électronique | 10 kg | 50€        |
| Vêtements    | 8 kg  | 24€        |
| Épicerie     | 4 kg  | 8€         |

<details>
<summary>💡 Voir la solution</summary>

```javascript
const colis = [
  { nom: "Livres", poids: 6, valeur: 18 }, // ratio: 3
  { nom: "Électronique", poids: 10, valeur: 50 }, // ratio: 5
  { nom: "Vêtements", poids: 8, valeur: 24 }, // ratio: 3
  { nom: "Épicerie", poids: 4, valeur: 8 }, // ratio: 2
];

const resultat = sacAdosFractionnaire(colis, 20);

// Ordre par ratio : Électronique (5), Livres (3), Vêtements (3), Épicerie (2)
// 1. Électronique : 10 kg, 50€ → reste 10 kg
// 2. Livres : 6 kg, 18€ → reste 4 kg
// 3. Vêtements : 4 kg / 8 kg = 50%, 12€
// Total : 50 + 18 + 12 = 80€

console.log("Valeur totale :", resultat.valeurTotale, "€");
// 80€
```

</details>

---

### Exercice 4 : Quand le Glouton Échoue

**Objectif :** Identifier les cas d'échec du glouton.

**Instructions :** Pour le problème du sac à dos 0/1 (pas de fractions), montrez que le glouton par ratio échoue avec :

- Capacité : 10 kg
- Objet A : 6 kg, 30€ (ratio 5)
- Objet B : 5 kg, 20€ (ratio 4)
- Objet C : 5 kg, 20€ (ratio 4)

<details>
<summary>💡 Voir la solution</summary>

```
GLOUTON (par ratio) :
1. A (ratio 5) : 6 kg, 30€ → reste 4 kg
2. B (ratio 4) : 5 kg > 4 kg → IMPOSSIBLE
3. C (ratio 4) : 5 kg > 4 kg → IMPOSSIBLE

Résultat glouton : A seul = 30€, 6 kg utilisés

OPTIMAL :
- B + C : 5 + 5 = 10 kg, 20 + 20 = 40€

Le glouton a choisi A (meilleur ratio) mais ça a "bloqué"
la capacité restante. Sans possibilité de fractionner,
le glouton n'est pas optimal pour le sac à dos 0/1 !
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

**Quelle est la caractéristique principale d'un algorithme glouton ?**

- [ ] A. Il explore toutes les solutions possibles
- [ ] B. Il fait le meilleur choix local à chaque étape
- [ ] C. Il revient en arrière si un choix est mauvais
- [ ] D. Il utilise une table de mémorisation

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Un algorithme glouton fait le **meilleur choix local** à chaque étape, sans considérer les conséquences futures et sans jamais revenir en arrière.

</details>

---

### Question 2

**Quelles sont les deux propriétés pour qu'un glouton soit optimal ?**

- [ ] A. Récursivité et mémorisation
- [ ] B. Choix glouton et sous-structure optimale
- [ ] C. Tri et parcours linéaire
- [ ] D. Diviser et régner

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

La **propriété du choix glouton** (le choix local mène à l'optimal global) et la **sous-structure optimale** (une solution optimale contient des solutions optimales aux sous-problèmes).

</details>

---

### Question 3

**Pourquoi l'algorithme glouton de la monnaie échoue-t-il avec les pièces {1, 3, 4} pour 6 centimes ?**

- [ ] A. Les pièces ne sont pas triées
- [ ] B. Le choix de 4 empêche d'utiliser deux pièces de 3
- [ ] C. Il n'y a pas assez de pièces de 1
- [ ] D. Le système ne contient pas de pièce de 2

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le glouton choisit d'abord 4 (plus grande pièce ≤ 6), puis 1+1. Résultat : 3 pièces. Mais 3+3 = 2 pièces serait optimal. Le choix de 4 "bloque" la meilleure solution.

</details>

---

### Question 4

**Quelle stratégie utilise-t-on pour le problème de sélection d'activités ?**

- [ ] A. Choisir l'activité la plus longue
- [ ] B. Choisir l'activité qui commence le plus tôt
- [ ] C. Choisir l'activité qui se termine le plus tôt
- [ ] D. Choisir l'activité avec le plus de valeur

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

On choisit l'activité qui **se termine le plus tôt** parmi celles qui ne chevauchent pas les activités déjà sélectionnées. Cela maximise le temps restant pour d'autres activités.

</details>

---

### Question 5

**Pour le sac à dos fractionnaire, quel critère utilise-t-on ?**

- [ ] A. Le poids le plus léger
- [ ] B. La valeur la plus élevée
- [ ] C. Le ratio valeur/poids le plus élevé
- [ ] D. Le nombre d'objets maximum

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

On trie les objets par **ratio valeur/poids décroissant** et on prend en priorité ceux qui offrent le plus de "valeur par kilo".

</details>

---

### Question 6

**Quelle est la complexité typique d'un algorithme glouton ?**

- [ ] A. O(n!)
- [ ] B. O(2^n)
- [ ] C. O(n log n) ou O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Les algorithmes gloutons sont généralement **O(n log n)** (si un tri est nécessaire) ou **O(n)** (si les données sont déjà triées ou si aucun tri n'est requis).

</details>

---

### Question 7

**Le sac à dos 0/1 peut-il être résolu optimalement par un glouton ?**

- [ ] A. Oui, toujours
- [ ] B. Non, jamais
- [ ] C. Seulement si les poids sont égaux
- [ ] D. Seulement si on peut prendre des fractions

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le sac à dos **0/1** (objets entiers uniquement) ne peut **pas** être résolu optimalement par un glouton. Il nécessite la **programmation dynamique** car le choix glouton peut bloquer de meilleures combinaisons.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe Glouton

Faire le **meilleur choix local** à chaque étape, sans revenir en arrière.

### 2. Deux Propriétés Nécessaires

- **Choix glouton** : Le choix local mène à l'optimal global
- **Sous-structure optimale** : Solution optimale = choix + solution optimale du sous-problème

### 3. Monnaie (Euro)

Glouton optimal pour les systèmes monétaires bien conçus (euro, dollar). Pas toujours optimal pour des systèmes arbitraires.

### 4. Sélection d'Activités

Trier par **fin croissante**, choisir l'activité qui finit le plus tôt. Garantit le maximum d'activités.

### 5. Sac à Dos Fractionnaire

Trier par **ratio valeur/poids décroissant**. Prendre les objets (ou fractions) les plus rentables.

### 6. Complexité

Généralement **O(n log n)** (tri) ou **O(n)** (parcours). Rapide et simple !

### 7. Limites

Le glouton n'est **pas toujours optimal**. Pour le sac à dos 0/1 ou la monnaie avec certains systèmes, il faut la **programmation dynamique**.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez découvert le premier paradigme algorithmique avancé : les **algorithmes gloutons** !

### Ce que vous avez appris aujourd'hui

- Le **principe glouton** : choix local optimal
- Les **deux propriétés** nécessaires pour l'optimalité
- Le problème de la **monnaie** et ses limites
- La **sélection d'activités** (stratégie de la fin la plus tôt)
- Le **sac à dos fractionnaire** (stratégie du meilleur ratio)
- Quand le glouton **fonctionne** vs quand il **échoue**

### Compétences acquises

Vous êtes maintenant capable de :

- Identifier si un problème peut être résolu par un glouton
- Choisir la bonne stratégie gloutonne selon le problème
- Implémenter des algorithmes gloutons efficaces
- Reconnaître les cas où le glouton échoue

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Les algorithmes gloutons sont parmi les plus **simples** et les plus **efficaces** quand ils fonctionnent. De nombreux algorithmes célèbres sont gloutons : Dijkstra, Kruskal, Prim, Huffman... Mais savoir quand ils **ne fonctionnent pas** est tout aussi crucial. La programmation dynamique, que vous découvrirez ensuite, résout les problèmes où le glouton échoue !

---

## ➡️ Prochaine Étape : Leçon 32

### Ce qui vous attend

La prochaine leçon, **« Implémentation d'un Algorithme Glouton en JavaScript : Le Problème de la Monnaie »**, approfondira :

**Vous découvrirez :**

- Une **implémentation complète** du problème de la monnaie
- L'analyse détaillée des **cas de succès et d'échec**
- Des **optimisations** et variantes
- La transition vers la **programmation dynamique**

### Préparez-vous !

Vous avez maintenant les bases des algorithmes gloutons. La prochaine leçon mettra en pratique ces concepts avec des implémentations plus poussées et vous préparera à la programmation dynamique !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Wikipedia - Greedy Algorithm](https://en.wikipedia.org/wiki/Greedy_algorithm) - Théorie approfondie
- [MIT OpenCourseWare - Greedy Algorithms](https://ocw.mit.edu/courses/6-046j-design-and-analysis-of-algorithms-spring-2015/) - Cours MIT
- [Visualgo - Greedy](https://visualgo.net/en) - Visualisations interactives

### Outils de pratique

- **[LeetCode - Greedy](https://leetcode.com/tag/greedy/)** : Exercices pratiques
- **[HackerRank - Greedy](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=greedy)** : Défis algorithmiques

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ?

N'hésitez pas à :

- Tester différentes stratégies gloutonnes sur le même problème
- Chercher des contre-exemples pour mieux comprendre les limites
- Comparer les résultats avec une approche exhaustive

> 💡 **Conseil**
>
> Pour maîtriser les algorithmes gloutons, pratiquez à identifier **quel critère** optimiser à chaque étape. C'est souvent le tri préalable (par valeur, par fin, par ratio...) qui détermine le succès ou l'échec du glouton !

---

**Prêt pour la Leçon 32 ?** 🚀

Rendez-vous dans la prochaine leçon pour approfondir le problème de la monnaie et préparer la transition vers la programmation dynamique !

---

<div align="center">

**Leçon 31 sur 42 - Module 6 : Paradigmes Avancés de Conception d'Algorithmes**

[⬅️ Module 5 : Arbres et Graphes](../module-5/README.md) | [Retour au sommaire](./README.md) | [Leçon 32 : Implémentation Glouton - Monnaie ➡️](./lecon-2-implementation-algorithme-glouton-javascript-probleme-monnaie.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
