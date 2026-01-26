##### Leçon 26 sur 42

# Arbres de Recherche Binaires (BST) : Insertion et Recherche en JavaScript

**Module 5** : Arbres et Parcours de Graphes

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre la **propriété d'ordre** des arbres de recherche binaires (BST)
- Implémenter une **classe BST complète** en JavaScript
- **Insérer** des éléments tout en maintenant la propriété BST
- **Rechercher** efficacement une valeur dans un BST
- Analyser la **complexité** des opérations (O(log n) vs O(n))
- Gérer les **cas limites** (doublons, arbre vide)

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

- **Leçon 25 complétée** : Terminologie des arbres (nœud, racine, feuille, hauteur)
- **Module 4** : Comprendre la récursion et la recherche binaire
- **Classes JavaScript** : Savoir créer des classes avec constructeur et méthodes
- Environnement JavaScript fonctionnel

---

## 🚀 Introduction : La Puissance de l'Ordre

Dans la leçon précédente, vous avez découvert les différents types d'arbres. Parmi eux, l'**Arbre de Recherche Binaire** (Binary Search Tree ou BST) est particulièrement puissant grâce à sa **propriété d'ordre**.

Imaginez une bibliothèque où les livres sont rangés dans n'importe quel ordre : trouver un livre spécifique nécessiterait de parcourir chaque étagère. Maintenant, imaginez cette même bibliothèque avec les livres **triés par titre** : vous pourriez immédiatement savoir dans quelle section chercher !

C'est exactement ce que fait un BST :

- Si la valeur cherchée est **plus petite** → aller à **gauche**
- Si la valeur cherchée est **plus grande** → aller à **droite**

À chaque étape, on **élimine la moitié** des possibilités restantes !

> **Point Clé**
>
> Un BST combine la structure hiérarchique des arbres avec la propriété d'ordre de la recherche binaire. Cela permet des opérations de recherche, insertion et suppression en **O(log n)** dans le cas moyen, contre O(n) pour une liste chaînée.

---

## 📦 Structure d'un Arbre de Recherche Binaire

Un BST est un arbre binaire avec une **propriété d'ordre** stricte.

---

### La Propriété Fondamentale du BST

Pour **chaque nœud** d'un BST :

- Tous les nœuds du **sous-arbre gauche** ont des valeurs **inférieures**
- Tous les nœuds du **sous-arbre droit** ont des valeurs **supérieures**

```
          [50]
         /    \
      [30]    [70]
      /  \    /  \
   [20] [40][60] [80]
```

**Vérification :**

- Pour 50 : gauche (30, 20, 40) < 50 < droite (70, 60, 80)
- Pour 30 : gauche (20) < 30 < droite (40)
- Pour 70 : gauche (60) < 70 < droite (80)

---

### Classe Noeud en JavaScript

La brique de base d'un BST est le **nœud** :

```javascript
/**
 * Représente un nœud dans un Arbre de Recherche Binaire.
 */
class Noeud {
  /**
   * Crée un nouveau nœud.
   * @param {number} valeur - La valeur stockée dans le nœud.
   */
  constructor(valeur) {
    this.valeur = valeur; // La donnée stockée
    this.gauche = null; // Référence vers l'enfant gauche
    this.droite = null; // Référence vers l'enfant droit
  }
}

// Exemple : créer un nœud
const noeud = new Noeud(50);
console.log(noeud);
// Noeud { valeur: 50, gauche: null, droite: null }
```

---

### Classe ArbreRechercheBinaire

L'arbre lui-même est une classe avec une référence vers la **racine** :

```javascript
/**
 * Représente un Arbre de Recherche Binaire (BST).
 */
class ArbreRechercheBinaire {
  /**
   * Crée un nouvel arbre vide.
   */
  constructor() {
    this.racine = null; // L'arbre est initialement vide
  }

  // Les méthodes insert() et rechercher() seront ajoutées
}

// Exemple : créer un arbre vide
const arbre = new ArbreRechercheBinaire();
console.log(arbre.racine); // null (arbre vide)
```

---

### Exemple Visuel : BST avec les Valeurs 50, 30, 70, 20, 40, 60, 80

```
        50 (racine)
       /  \
      30   70
     / \   / \
   20  40 60  80

Propriétés :
- Hauteur : 2
- Nombre de nœuds : 7
- Feuilles : 20, 40, 60, 80
- Nœuds internes : 50, 30, 70
```

---

## 💻 Insertion dans un BST

L'insertion consiste à trouver le **bon emplacement** pour un nouveau nœud tout en maintenant la propriété BST.

---

### Algorithme d'Insertion

1. **Si l'arbre est vide** : Le nouveau nœud devient la racine
2. **Sinon**, à partir de la racine :
   - Si valeur < nœud actuel → aller à **gauche**
   - Si valeur > nœud actuel → aller à **droite**
3. **Répéter** jusqu'à trouver un emplacement vide (null)
4. **Insérer** le nouveau nœud à cet emplacement

---

### Exemple Pas à Pas : Insérer 50, 30, 70, 20, 40

**Étape 1 : Insérer 50**

```
Arbre vide → 50 devient la racine

    [50]
```

**Étape 2 : Insérer 30**

```
30 < 50 → aller à gauche
Gauche est vide → insérer 30

    [50]
    /
  [30]
```

**Étape 3 : Insérer 70**

```
70 > 50 → aller à droite
Droite est vide → insérer 70

    [50]
    /  \
  [30] [70]
```

**Étape 4 : Insérer 20**

```
20 < 50 → aller à gauche (vers 30)
20 < 30 → aller à gauche
Gauche de 30 est vide → insérer 20

      [50]
      /  \
    [30] [70]
    /
  [20]
```

**Étape 5 : Insérer 40**

```
40 < 50 → aller à gauche (vers 30)
40 > 30 → aller à droite
Droite de 30 est vide → insérer 40

      [50]
      /  \
    [30] [70]
    /  \
  [20] [40]
```

---

### Implémentation de la Méthode `inserer()`

```javascript
class Noeud {
  constructor(valeur) {
    this.valeur = valeur;
    this.gauche = null;
    this.droite = null;
  }
}

class ArbreRechercheBinaire {
  constructor() {
    this.racine = null;
  }

  /**
   * Insère une nouvelle valeur dans le BST.
   * @param {number} valeur - La valeur à insérer.
   * @returns {ArbreRechercheBinaire} - L'arbre pour chaînage.
   */
  inserer(valeur) {
    const nouveauNoeud = new Noeud(valeur);

    // Cas 1 : Arbre vide - le nouveau nœud devient la racine
    if (this.racine === null) {
      this.racine = nouveauNoeud;
      return this;
    }

    // Cas 2 : Parcourir l'arbre pour trouver l'emplacement
    let actuel = this.racine;

    while (true) {
      // Gestion des doublons : on ignore
      if (valeur === actuel.valeur) {
        return undefined;
      }

      // Valeur plus petite → aller à gauche
      if (valeur < actuel.valeur) {
        if (actuel.gauche === null) {
          // Emplacement trouvé !
          actuel.gauche = nouveauNoeud;
          return this;
        }
        // Continuer à gauche
        actuel = actuel.gauche;
      }
      // Valeur plus grande → aller à droite
      else {
        if (actuel.droite === null) {
          // Emplacement trouvé !
          actuel.droite = nouveauNoeud;
          return this;
        }
        // Continuer à droite
        actuel = actuel.droite;
      }
    }
  }
}

// Test
const arbre = new ArbreRechercheBinaire();
arbre.inserer(50);
arbre.inserer(30);
arbre.inserer(70);
arbre.inserer(20);
arbre.inserer(40);

console.log(arbre.racine.valeur); // 50
console.log(arbre.racine.gauche.valeur); // 30
console.log(arbre.racine.droite.valeur); // 70
console.log(arbre.racine.gauche.gauche.valeur); // 20
console.log(arbre.racine.gauche.droite.valeur); // 40
```

---

## 📝 Micro-Exercice #1 : Construire un BST

**Objectif :** Pratiquer l'insertion manuelle dans un BST.

**Instructions :** Dessinez l'arbre résultant de l'insertion des valeurs suivantes dans l'ordre : **15, 10, 20, 8, 12, 17, 25**

<details>
<summary>💡 Voir la solution</summary>

```
Insertion de 15 : racine
        [15]

Insertion de 10 : 10 < 15 → gauche
        [15]
        /
      [10]

Insertion de 20 : 20 > 15 → droite
        [15]
        /  \
      [10] [20]

Insertion de 8 : 8 < 15 → gauche, 8 < 10 → gauche
        [15]
        /  \
      [10] [20]
      /
     [8]

Insertion de 12 : 12 < 15 → gauche, 12 > 10 → droite
        [15]
        /  \
      [10] [20]
      /  \
     [8] [12]

Insertion de 17 : 17 > 15 → droite, 17 < 20 → gauche
        [15]
        /  \
      [10] [20]
      /  \  /
     [8][12][17]

Insertion de 25 : 25 > 15 → droite, 25 > 20 → droite
          [15]
         /    \
       [10]   [20]
       /  \   /  \
      [8][12][17][25]
```

</details>

---

## 💻 Recherche dans un BST

La recherche exploite la propriété d'ordre pour trouver une valeur **rapidement**.

---

### Algorithme de Recherche

1. **Commencer** à la racine
2. **Comparer** la valeur cherchée avec le nœud actuel :
   - Si égale → **Trouvé !**
   - Si plus petite → aller à **gauche**
   - Si plus grande → aller à **droite**
3. **Répéter** jusqu'à trouver ou atteindre null
4. Si on atteint **null** → La valeur **n'existe pas**

---

### Exemple : Rechercher 40 dans le BST

```
      [50]
      /  \
    [30] [70]
    /  \
  [20] [40]

Recherche de 40 :
1. À 50 : 40 < 50 → aller à gauche
2. À 30 : 40 > 30 → aller à droite
3. À 40 : 40 === 40 → TROUVÉ !

Comparaisons : 3 (au lieu de 5 avec une recherche linéaire)
```

---

### Exemple : Rechercher 35 (valeur absente)

```
Recherche de 35 :
1. À 50 : 35 < 50 → aller à gauche
2. À 30 : 35 > 30 → aller à droite
3. À 40 : 35 < 40 → aller à gauche
4. Gauche de 40 est null → NON TROUVÉ
```

---

### Implémentation des Méthodes de Recherche

```javascript
class ArbreRechercheBinaire {
  constructor() {
    this.racine = null;
  }

  // ... méthode inserer() vue précédemment ...

  /**
   * Recherche une valeur et retourne le nœud si trouvé.
   * @param {number} valeur - La valeur à rechercher.
   * @returns {Noeud|null} - Le nœud trouvé ou null.
   */
  trouver(valeur) {
    // Arbre vide → pas trouvé
    if (this.racine === null) return null;

    let actuel = this.racine;

    while (actuel !== null) {
      // Valeur plus petite → aller à gauche
      if (valeur < actuel.valeur) {
        actuel = actuel.gauche;
      }
      // Valeur plus grande → aller à droite
      else if (valeur > actuel.valeur) {
        actuel = actuel.droite;
      }
      // Valeur égale → TROUVÉ !
      else {
        return actuel;
      }
    }

    // Atteint null → non trouvé
    return null;
  }

  /**
   * Vérifie si une valeur existe dans l'arbre.
   * @param {number} valeur - La valeur à vérifier.
   * @returns {boolean} - true si présent, false sinon.
   */
  contient(valeur) {
    if (this.racine === null) return false;

    let actuel = this.racine;

    while (actuel !== null) {
      if (valeur < actuel.valeur) {
        actuel = actuel.gauche;
      } else if (valeur > actuel.valeur) {
        actuel = actuel.droite;
      } else {
        return true; // Trouvé !
      }
    }

    return false; // Non trouvé
  }
}

// Tests
const arbre = new ArbreRechercheBinaire();
[50, 30, 70, 20, 40, 60, 80].forEach((v) => arbre.inserer(v));

console.log("Recherche de 40 :", arbre.trouver(40));
// Noeud { valeur: 40, gauche: null, droite: null }

console.log("Contient 40 ?", arbre.contient(40)); // true
console.log("Contient 35 ?", arbre.contient(35)); // false
console.log("Contient 80 ?", arbre.contient(80)); // true
console.log("Contient 100 ?", arbre.contient(100)); // false
```

---

## 📝 Micro-Exercice #2 : Tracer une Recherche

**Objectif :** Comprendre le chemin parcouru lors d'une recherche.

**Instructions :** Dans cet arbre, tracez le chemin pour rechercher la valeur **17** :

```
        [15]
       /    \
     [10]   [20]
     /  \   /  \
    [8][12][17][25]
```

<details>
<summary>💡 Voir la solution</summary>

```
Recherche de 17 :
1. À 15 : 17 > 15 → aller à DROITE
2. À 20 : 17 < 20 → aller à GAUCHE
3. À 17 : 17 === 17 → TROUVÉ !

Chemin parcouru : 15 → 20 → 17
Nombre de comparaisons : 3
```

**Observation :** Avec une recherche linéaire dans [8, 10, 12, 15, 17, 20, 25], il faudrait 5 comparaisons pour trouver 17.

</details>

---

## 📊 Analyse de Complexité

La complexité des opérations sur un BST dépend de sa **forme**.

---

### Complexité Temporelle

| Opération       | Meilleur cas | Cas moyen | Pire cas |
| --------------- | ------------ | --------- | -------- |
| **Insertion**   | O(1)         | O(log n)  | O(n)     |
| **Recherche**   | O(1)         | O(log n)  | O(n)     |
| **Suppression** | O(1)         | O(log n)  | O(n)     |

---

### Cas Moyen : Arbre Équilibré (O(log n))

Quand l'arbre est **équilibré**, sa hauteur est environ log₂(n).

```
Arbre équilibré (7 nœuds, hauteur 2) :
          [50]
         /    \
       [30]   [70]
       /  \   /  \
     [20][40][60][80]

Recherche de 80 : 3 comparaisons (log₂(7) ≈ 2.8)
```

---

### Pire Cas : Arbre Dégénéré (O(n))

Si les valeurs sont insérées **dans l'ordre**, l'arbre devient une liste chaînée !

```
Insertion de : 10, 20, 30, 40, 50 (ordre croissant)

[10]
  \
  [20]
    \
    [30]
      \
      [40]
        \
        [50]

Recherche de 50 : 5 comparaisons = O(n)
```

> **Attention**
>
> L'ordre d'insertion affecte la forme de l'arbre ! Pour éviter le pire cas, on utilise des **arbres équilibrés** comme les AVL ou les arbres rouge-noir, qui maintiennent automatiquement l'équilibre.

---

### Comparaison avec d'Autres Structures

| Structure            | Recherche | Insertion | Avantage           |
| -------------------- | --------- | --------- | ------------------ |
| **Tableau non trié** | O(n)      | O(1)      | Insertion rapide   |
| **Tableau trié**     | O(log n)  | O(n)      | Recherche rapide   |
| **Liste chaînée**    | O(n)      | O(1)      | Insertion flexible |
| **BST équilibré**    | O(log n)  | O(log n)  | Bon compromis      |

---

## 📝 Micro-Exercice #3 : Identifier le Pire Cas

**Objectif :** Reconnaître quand un BST devient inefficace.

**Instructions :** Dessinez l'arbre résultant de l'insertion de : **5, 10, 15, 20, 25** (dans cet ordre). Quelle est sa hauteur ? Combien de comparaisons pour trouver 25 ?

<details>
<summary>💡 Voir la solution</summary>

```
Arbre dégénéré (insertion en ordre croissant) :

[5]
  \
  [10]
    \
    [15]
      \
      [20]
        \
        [25]

Hauteur : 4 (au lieu de 2 pour un arbre équilibré)
Comparaisons pour trouver 25 : 5 (pire cas O(n))

Comparaison avec un arbre équilibré contenant les mêmes valeurs :
        [15]
       /    \
     [10]   [20]
     /        \
    [5]      [25]

Hauteur : 2
Comparaisons pour trouver 25 : 3
```

</details>

---

## 💼 Application : Étude de Cas - Annuaire de Contacts

Utilisons un BST pour gérer un annuaire de contacts trié par nom.

---

### Scénario

Sing veut créer un annuaire où elle peut rapidement :

- Ajouter de nouveaux contacts
- Rechercher un contact par son nom

---

### Implémentation Complète

```javascript
/**
 * Représente un contact dans l'annuaire.
 */
class NoeudContact {
  constructor(nom, telephone) {
    this.nom = nom;
    this.telephone = telephone;
    this.gauche = null;
    this.droite = null;
  }
}

/**
 * Annuaire de contacts utilisant un BST.
 */
class Annuaire {
  constructor() {
    this.racine = null;
  }

  /**
   * Ajoute un nouveau contact.
   * @param {string} nom - Le nom du contact.
   * @param {string} telephone - Le numéro de téléphone.
   */
  ajouterContact(nom, telephone) {
    const nouveauContact = new NoeudContact(nom, telephone);

    if (this.racine === null) {
      this.racine = nouveauContact;
      return;
    }

    let actuel = this.racine;

    while (true) {
      // Comparaison alphabétique
      const comparaison = nom.localeCompare(actuel.nom);

      if (comparaison === 0) {
        // Mise à jour du numéro si contact existe déjà
        actuel.telephone = telephone;
        return;
      }

      if (comparaison < 0) {
        // Nom vient avant alphabétiquement → gauche
        if (actuel.gauche === null) {
          actuel.gauche = nouveauContact;
          return;
        }
        actuel = actuel.gauche;
      } else {
        // Nom vient après alphabétiquement → droite
        if (actuel.droite === null) {
          actuel.droite = nouveauContact;
          return;
        }
        actuel = actuel.droite;
      }
    }
  }

  /**
   * Recherche un contact par son nom.
   * @param {string} nom - Le nom à rechercher.
   * @returns {NoeudContact|null} - Le contact trouvé ou null.
   */
  rechercherContact(nom) {
    let actuel = this.racine;

    while (actuel !== null) {
      const comparaison = nom.localeCompare(actuel.nom);

      if (comparaison === 0) {
        return actuel; // Trouvé !
      } else if (comparaison < 0) {
        actuel = actuel.gauche;
      } else {
        actuel = actuel.droite;
      }
    }

    return null; // Non trouvé
  }

  /**
   * Affiche tous les contacts triés (parcours infixe).
   */
  afficherTous(noeud = this.racine) {
    if (noeud === null) return;

    this.afficherTous(noeud.gauche);
    console.log(`${noeud.nom}: ${noeud.telephone}`);
    this.afficherTous(noeud.droite);
  }
}

// Utilisation
const annuaire = new Annuaire();

// Ajouter les contacts (ordre d'insertion quelconque)
annuaire.ajouterContact("Germain", "06 12 34 56 78");
annuaire.ajouterContact("Chermann", "04 98 76 54 32");
annuaire.ajouterContact("Prudence", "07 71 22 33 44");
annuaire.ajouterContact("Ingrid", "06 55 66 77 88");
annuaire.ajouterContact("Destinée", "06 99 88 77 66");

console.log("=== Tous les contacts (triés) ===");
annuaire.afficherTous();
// Chermann: 04 98 76 54 32
// Destinée: 06 99 88 77 66
// Germain: 06 12 34 56 78
// Ingrid: 06 55 66 77 88
// Prudence: 07 71 22 33 44

console.log("\n=== Recherches ===");
const ingrid = annuaire.rechercherContact("Ingrid");
console.log("Ingrid trouvée :", ingrid?.telephone); // 06 55 66 77 88

const marc = annuaire.rechercherContact("Marc-Élie");
console.log("Marc-Élie trouvé :", marc); // null
```

---

### Structure de l'Arbre Résultant

```
          [Germain]
          /        \
   [Chermann]    [Prudence]
         \        /
      [Destinée][Ingrid]
```

**Avantages :**

- Contacts automatiquement triés
- Recherche rapide par nom
- Ajout efficace de nouveaux contacts

---

## 💪 Exercices Pratiques

Pour solidifier votre maîtrise des BST, complétez les exercices suivants.

---

### Exercice 1 : Construire un BST Personnalisé

**Objectif :** Créer un BST et vérifier sa structure.

**Instructions :**

1. Créez un nouveau BST
2. Insérez les valeurs : 20, 10, 30, 5, 15, 25, 35, 2, 7, 12, 18
3. Vérifiez la structure en affichant les enfants de la racine

<details>
<summary>💡 Voir la solution</summary>

```javascript
const arbre = new ArbreRechercheBinaire();
[20, 10, 30, 5, 15, 25, 35, 2, 7, 12, 18].forEach((v) => arbre.inserer(v));

console.log("Racine :", arbre.racine.valeur); // 20
console.log("Gauche :", arbre.racine.gauche.valeur); // 10
console.log("Droite :", arbre.racine.droite.valeur); // 30

// Structure complète :
/*
              [20]
            /      \
         [10]      [30]
         /  \      /  \
       [5] [15]  [25] [35]
       / \  / \
      [2][7][12][18]
*/
```

</details>

---

### Exercice 2 : Défi de Recherche

**Objectif :** Pratiquer la recherche dans un BST.

**Instructions :** En utilisant le BST de l'exercice 1, effectuez ces recherches et notez le nombre de comparaisons :

1. Rechercher 18
2. Rechercher 21 (absent)
3. Rechercher 2
4. Rechercher 20

<details>
<summary>💡 Voir la solution</summary>

```javascript
// 1. Rechercher 18
console.log("18 :", arbre.contient(18)); // true
// Chemin : 20 → 10 → 15 → 18 (4 comparaisons)

// 2. Rechercher 21 (absent)
console.log("21 :", arbre.contient(21)); // false
// Chemin : 20 → 30 → 25 → null (3 comparaisons)

// 3. Rechercher 2
console.log("2 :", arbre.contient(2)); // true
// Chemin : 20 → 10 → 5 → 2 (4 comparaisons)

// 4. Rechercher 20
console.log("20 :", arbre.contient(20)); // true
// Chemin : 20 (1 comparaison - c'est la racine !)
```

</details>

---

### Exercice 3 : Gestion des Doublons

**Objectif :** Modifier le comportement pour les doublons.

**Instructions :** Modifiez la méthode `inserer()` pour placer les doublons dans le sous-arbre **droit** (au lieu de les ignorer).

<details>
<summary>💡 Voir la solution</summary>

```javascript
inserer(valeur) {
  const nouveauNoeud = new Noeud(valeur);

  if (this.racine === null) {
    this.racine = nouveauNoeud;
    return this;
  }

  let actuel = this.racine;

  while (true) {
    // MODIFIÉ : Les doublons vont à droite (au lieu d'être ignorés)
    if (valeur <= actuel.valeur) { // <= au lieu de <
      if (actuel.gauche === null) {
        actuel.gauche = nouveauNoeud;
        return this;
      }
      actuel = actuel.gauche;
    } else {
      if (actuel.droite === null) {
        actuel.droite = nouveauNoeud;
        return this;
      }
      actuel = actuel.droite;
    }
  }
}

// Test avec doublons
const arbre = new ArbreRechercheBinaire();
arbre.inserer(10);
arbre.inserer(10); // Doublon → va à gauche
console.log(arbre.racine.gauche.valeur); // 10
```

**Note :** Une autre approche serait d'ajouter un compteur dans chaque nœud.

</details>

---

### Exercice 4 : Compter les Nœuds

**Objectif :** Ajouter une méthode récursive pour compter les nœuds.

**Instructions :** Implémentez `compterNoeuds()` qui retourne le nombre total de nœuds dans l'arbre.

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Compte le nombre total de nœuds dans l'arbre.
 * @param {Noeud} noeud - Le nœud de départ (par défaut la racine).
 * @returns {number} - Le nombre de nœuds.
 */
compterNoeuds(noeud = this.racine) {
  // Cas de base : nœud null
  if (noeud === null) {
    return 0;
  }

  // Appel récursif : 1 (ce nœud) + nœuds à gauche + nœuds à droite
  return 1 + this.compterNoeuds(noeud.gauche) + this.compterNoeuds(noeud.droite);
}

// Test
const arbre = new ArbreRechercheBinaire();
[50, 30, 70, 20, 40, 60, 80].forEach(v => arbre.inserer(v));

console.log("Nombre de nœuds :", arbre.compterNoeuds()); // 7
```

</details>

---

## ❓ Quiz de Validation des Connaissanc

### Question 1

**Quelle est la propriété fondamentale d'un BST ?**

- [ ] A. Chaque nœud a exactement 2 enfants
- [ ] B. Gauche < Racine < Droite pour chaque nœud
- [ ] C. Toutes les feuilles sont au même niveau
- [ ] D. La racine contient la plus grande valeur

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Pour chaque nœud, tous les nœuds du **sous-arbre gauche** sont inférieurs, et tous les nœuds du **sous-arbre droit** sont supérieurs.

</details>

---

### Question 2

**Quelle est la complexité de recherche dans un BST équilibré ?**

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Dans un BST **équilibré**, la hauteur est environ log₂(n), donc la recherche est en **O(log n)**.

</details>

---

### Question 3

**Dans quel cas un BST a-t-il une complexité de recherche O(n) ?**

- [ ] A. Quand l'arbre est équilibré
- [ ] B. Quand l'arbre contient des doublons
- [ ] C. Quand l'arbre est dégénéré (en forme de liste)
- [ ] D. Quand l'arbre a plus de 100 nœuds

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un arbre **dégénéré** (tous les nœuds dans une seule branche) a une hauteur de n-1, donc la recherche devient **O(n)**.

</details>

---

### Question 4

**Si on insère 50, 25, 75 dans un BST vide, quelle est la structure ?**

- [ ] A. 50 à gauche de 25
- [ ] B. 75 à la racine
- [ ] C. 50 à la racine, 25 à gauche, 75 à droite
- [ ] D. 25 à la racine

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

50 est inséré en premier → **racine**. 25 < 50 → **gauche**. 75 > 50 → **droite**.

```
    [50]
    /  \
  [25] [75]
```

</details>

---

### Question 5

**Combien de comparaisons au maximum pour trouver une valeur dans un BST équilibré de 15 nœuds ?**

- [ ] A. 15
- [ ] B. 8
- [ ] C. 4
- [ ] D. 1

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Un BST équilibré de 15 nœuds a une hauteur de 3 (car 2⁴ - 1 = 15). Il faut donc au maximum **4 comparaisons** (hauteur + 1).

</details>

---

### Question 6

**Que retourne `arbre.trouver(valeur)` si la valeur n'existe pas ?**

- [ ] A. undefined
- [ ] B. false
- [ ] C. null
- [ ] D. -1

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

La méthode `trouver()` retourne le **nœud** si trouvé, ou **null** si la valeur n'existe pas dans l'arbre.

</details>

---

### Question 7

**Si on insère 10, 20, 30, 40, 50 dans cet ordre, quelle est la hauteur de l'arbre ?**

- [ ] A. 2
- [ ] B. 3
- [ ] C. 4
- [ ] D. 5

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

L'insertion en ordre croissant crée un arbre **dégénéré** (liste) :

```
[10]
  \
  [20]
    \
    [30]
      \
      [40]
        \
        [50]
```

Hauteur = **4** (nombre d'arêtes de la racine à la feuille la plus profonde).

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Propriété BST

Pour chaque nœud : sous-arbre gauche < nœud < sous-arbre droit. Cette propriété permet des opérations efficaces.

### 2. Structure en JavaScript

Un BST utilise une classe Noeud (valeur, gauche, droite) et une classe ArbreRechercheBinaire (racine).

### 3. Insertion

Parcourir l'arbre en comparant : si valeur < actuel → gauche, sinon → droite. Insérer quand on atteint null.

### 4. Recherche

Même logique que l'insertion : comparer et choisir la direction jusqu'à trouver ou atteindre null.

### 5. Complexité O(log n)

Dans un BST équilibré, insertion et recherche sont en O(log n) car on élimine la moitié des nœuds à chaque pas.

### 6. Pire Cas O(n)

Un arbre dégénéré (insertion en ordre) devient une liste chaînée avec complexité O(n).

### 7. Applications

Annuaires, indexation de bases de données, dictionnaires triés, tout ce qui nécessite recherche + insertion efficaces.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous maîtrisez maintenant les Arbres de Recherche Binaires !

### Ce que vous avez appris aujourd'hui

- La propriété d'ordre fondamentale des BST
- L'implémentation complète en JavaScript (Noeud + BST)
- L'algorithme d'insertion et son fonctionnement pas à pas
- L'algorithme de recherche (trouver et contient)
- L'analyse de complexité et les cas limites
- L'application à un cas réel (annuaire de contacts)

### Compétences acquises

Vous êtes maintenant capable de :

- Implémenter un BST complet en JavaScript
- Insérer et rechercher des valeurs efficacement
- Analyser quand un BST sera performant ou non

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Les BST sont la base de nombreuses structures de données avancées (AVL, Rouge-Noir, B-trees). Comprendre comment ils fonctionnent vous prépare aux index de bases de données, aux systèmes de fichiers, et à tout système nécessitant des recherches rapides dans des données triées.

---

## ➡️ Prochaine Étape : Leçon 27

### Ce qui vous attend

La prochaine leçon, **« Graphes : Concepts, Sommets, Arêtes et Représentations »**, vous introduira à une structure encore plus générale que les arbres.

**Vous découvrirez :**

- La définition des **graphes** et leur différence avec les arbres
- Les concepts de **sommets**, **arêtes**, et **voisins**
- Les différents **types de graphes** (orientés, non orientés, pondérés)
- Les **représentations** en JavaScript (matrice et liste d'adjacence)

### Préparez-vous !

Les graphes généralisent les arbres : au lieu d'une hiérarchie stricte, chaque nœud peut être connecté à n'importe quel autre. C'est essentiel pour modéliser les réseaux sociaux, les cartes routières, et bien plus !

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - BST](https://visualgo.net/en/bst) - Visualisation interactive
- [Wikipedia - Binary Search Tree](https://en.wikipedia.org/wiki/Binary_search_tree) - Théorie approfondie
- [CS50 - Binary Search Trees](https://cs50.harvard.edu/x/2024/shorts/binary_search_trees/) - Cours Harvard

### Outils de pratique

- **[BST Visualizer](https://www.cs.usfca.edu/~galles/visualization/BST.html)** : Visualisez insertions et recherches
- **[LeetCode BST Problems](https://leetcode.com/tag/binary-search-tree/)** : Exercices pratiques

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Tracer manuellement des insertions sur papier
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour vraiment maîtriser les BST, **implémentez-les de zéro** sans regarder le code. Commencez par la classe Noeud, puis la classe BST avec `inserer()`, et enfin `trouver()`. Si vous bloquez, relisez la section concernée puis réessayez.

---

**Prêt pour la Leçon 27 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir les graphes !

---

<div align="center">

**Leçon 26 sur 42 - Module 5 : Arbres et Parcours de Graphes**

[⬅️ Leçon 25 : Arbres - Terminologie, Types et Cas d'Usage](./lecon-1-arbres-terminologie-types-cas-usage.md) | [Retour au sommaire](./README.md) | [Leçon 27 : Graphes - Concepts et Représentations ➡️](./lecon-3-graphes-concepts-sommets-aretes-representations.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
