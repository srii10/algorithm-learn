##### Leçon 13 sur 42

# Introduction au Tri : Pourquoi Ordonner les Données ?

**Module 3** : Techniques de Tri Essentielles

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre ce qu'est le **tri** et pourquoi il est fondamental en informatique
- Identifier les **avantages** d'avoir des données ordonnées
- Reconnaître les différents **critères de tri** (numérique, alphabétique, chronologique, personnalisé)
- Comprendre les notions de **complexité temporelle et spatiale** appliquées au tri
- Distinguer un algorithme de tri **stable** d'un algorithme **instable**
- Appliquer ces concepts à des scénarios réels comme notre **étude de cas de gestion de tâches**

---

### ⏱️ Durée estimée : 2h - 2h30

---

## 📚 Prérequis

- **Module 1 complété** : Comprendre la notation Big O et l'analyse de complexité (Leçons 3-5)
- **Module 2 complété** : Maîtriser les tableaux et leurs opérations de base (Leçon 7)
- Environnement JavaScript fonctionnel (Node.js ou console du navigateur)

---

## 🚀 Introduction : L'Art d'Organiser l'Information

Avez-vous déjà essayé de trouver un mot dans un dictionnaire qui serait organisé de manière aléatoire ? Imaginez devoir parcourir chaque page, chaque mot, jusqu'à trouver celui que vous cherchez. Ce serait un cauchemar, n'est-ce pas ?

Le **tri** est le processus d'arrangement des éléments d'une liste dans un ordre particulier. Cet ordre peut être numérique, alphabétique, chronologique, ou basé sur des critères spécifiques. L'objectif principal du tri est de **faciliter la recherche**, la fusion de données, ou d'autres opérations de traitement en organisant les données dans une séquence prévisible.

Dans notre quotidien numérique, le tri est partout :

- Votre boîte mail affiche les messages du plus récent au plus ancien
- Un site e-commerce trie les produits par prix ou popularité
- Votre liste de contacts est ordonnée alphabétiquement
- Les résultats de recherche Google sont triés par pertinence

Dans ce module, nous allons explorer les algorithmes de tri les plus importants, comprendre leur fonctionnement, et apprendre à choisir le bon algorithme selon le contexte.

> **Point Clé**
>
> Le tri est l'une des opérations les plus fondamentales en informatique. Des données bien ordonnées peuvent transformer une recherche de O(n) en O(log n), soit une amélioration drastique des performances !

---

## 📦 Le Besoin de Données Ordonnées

Organiser les données dans un ordre spécifique est fondamental pour améliorer l'efficacité de nombreuses tâches informatiques. Des données non triées conduisent souvent à des opérations moins efficaces, rendant difficile la localisation, l'analyse ou le traitement rapide de l'information.

---

### Améliorer les Opérations de Recherche

Quand les données sont triées, trouver un élément spécifique devient **significativement plus rapide**.

**Exemple concret (Données non triées) :**

Considérons une base de données clients d'une entreprise contenant des millions d'enregistrements sans ordre particulier. Si un client appelle avec une question, trouver son dossier par nom ou ID nécessiterait de parcourir chaque enregistrement jusqu'à trouver une correspondance. C'est une **recherche linéaire**, extrêmement lente pour de grands ensembles de données.

```javascript
// Recherche linéaire dans des données non triées - O(n)
function rechercheLineaire(clients, idRecherche) {
  for (let i = 0; i < clients.length; i++) {
    if (clients[i].id === idRecherche) {
      return clients[i]; // Trouvé !
    }
  }
  return null; // Non trouvé
}

// Avec 1 million de clients, on peut devoir faire 1 million de comparaisons !
```

**Exemple concret (Données triées) :**

Si cette même base de données était triée alphabétiquement par nom ou numériquement par ID, trouver un client spécifique pourrait être fait beaucoup plus rapidement avec des algorithmes comme la **recherche binaire** (couverte dans le Module 4).

```javascript
// Recherche binaire dans des données triées - O(log n)
function rechercheBinaire(clientsTries, idRecherche) {
  let debut = 0;
  let fin = clientsTries.length - 1;

  while (debut <= fin) {
    const milieu = Math.floor((debut + fin) / 2);

    if (clientsTries[milieu].id === idRecherche) {
      return clientsTries[milieu]; // Trouvé !
    } else if (clientsTries[milieu].id < idRecherche) {
      debut = milieu + 1; // Chercher dans la moitié supérieure
    } else {
      fin = milieu - 1; // Chercher dans la moitié inférieure
    }
  }
  return null; // Non trouvé
}

// Avec 1 million de clients triés, maximum ~20 comparaisons suffisent !
```

> **Point Clé**
>
> Avec la recherche binaire sur des données triées, vous éliminez la moitié des données restantes à chaque comparaison. Pour 1 million d'éléments : log₂(1 000 000) ≈ 20 comparaisons au lieu de 1 000 000 !

---

### Faciliter la Fusion et l'Analyse des Données

Le tri est un **prérequis** pour de nombreuses tâches de traitement de données, notamment celles impliquant la combinaison de plusieurs ensembles ou l'exécution d'opérations analytiques.

**Exemple (Fusion de données) :**

Deux départements différents d'une grande chaîne de distribution maintiennent des listes séparées de leurs produits les plus vendus du mois. Si les deux listes sont triées par ID produit ou par volume de ventes, les fusionner en une seule liste complète sans doublons et dans un ordre cohérent est un processus simple.

```javascript
// Fusion de deux listes triées - O(n + m)
function fusionnerListesTriees(liste1, liste2) {
  const resultat = [];
  let i = 0;
  let j = 0;

  while (i < liste1.length && j < liste2.length) {
    if (liste1[i].id < liste2[j].id) {
      resultat.push(liste1[i]);
      i++;
    } else if (liste1[i].id > liste2[j].id) {
      resultat.push(liste2[j]);
      j++;
    } else {
      // Même ID : éviter les doublons, combiner les données
      resultat.push({
        ...liste1[i],
        ventesTotales: liste1[i].ventes + liste2[j].ventes,
      });
      i++;
      j++;
    }
  }

  // Ajouter les éléments restants
  while (i < liste1.length) resultat.push(liste1[i++]);
  while (j < liste2.length) resultat.push(liste2[j++]);

  return resultat;
}
```

**Exemple (Analyse de données) :**

Un analyste financier veut identifier les tendances des cours boursiers sur l'année passée. Si les données (prix et date) sont triées chronologiquement, il est facile de visualiser les mouvements de prix, calculer des moyennes mobiles, ou identifier des patterns dans le temps.

```javascript
// Calcul de moyenne mobile sur données triées chronologiquement
function calculerMoyenneMobile(coursTries, periode) {
  const moyennes = [];

  for (let i = periode - 1; i < coursTries.length; i++) {
    let somme = 0;
    for (let j = i - periode + 1; j <= i; j++) {
      somme += coursTries[j].prix;
    }
    moyennes.push({
      date: coursTries[i].date,
      moyenne: somme / periode,
    });
  }

  return moyennes;
}
```

---

### Améliorer les Performances des Algorithmes

De nombreux algorithmes fonctionnent plus efficacement, ou même **nécessitent**, que leurs données d'entrée soient triées.

**Structures de données :**

Certaines structures comme les **arbres binaires de recherche** (Module 5) reposent sur des principes de tri pour leur organisation interne, assurant une insertion, suppression et récupération efficaces des éléments.

**Algorithmes d'optimisation :**

Les algorithmes qui trouvent le minimum ou maximum, ou ceux qui identifient les doublons, performent souvent beaucoup mieux sur des données triées.

```javascript
// Trouver les doublons dans un tableau trié - O(n)
function trouverDoublonsTrie(tableauTrie) {
  const doublons = [];

  for (let i = 1; i < tableauTrie.length; i++) {
    // On compare simplement les éléments adjacents !
    if (tableauTrie[i] === tableauTrie[i - 1]) {
      if (!doublons.includes(tableauTrie[i])) {
        doublons.push(tableauTrie[i]);
      }
    }
  }

  return doublons;
}

// Exemple
const nombres = [1, 2, 2, 3, 4, 4, 4, 5];
console.log(trouverDoublonsTrie(nombres)); // [2, 4]
```

```javascript
// Trouver les doublons dans un tableau NON trié - O(n²) naïf
function trouverDoublonsNonTrie(tableau) {
  const doublons = [];

  for (let i = 0; i < tableau.length; i++) {
    for (let j = i + 1; j < tableau.length; j++) {
      if (tableau[i] === tableau[j] && !doublons.includes(tableau[i])) {
        doublons.push(tableau[i]);
      }
    }
  }

  return doublons;
}
```

---

## 📝 Micro-Exercice #1 : Identifier le Besoin de Tri

**Objectif :** Reconnaître quand le tri est bénéfique ou nécessaire.

**Instructions :** Pour chaque scénario ci-dessous, déterminez si le tri est bénéfique ou nécessaire, et si oui, quel critère utiliser.

1. Afficher une liste d'emails non lus dans une boîte de réception
2. Trouver le score moyen des étudiants d'une classe
3. Organiser les contacts dans un carnet d'adresses téléphonique
4. Traiter les transactions d'un grand livre bancaire pour calculer le solde quotidien
5. Afficher les 10 articles les plus chers d'un inventaire
6. Afficher les commentaires sur un article de blog

<details>
<summary>💡 Voir la solution</summary>

1. **Emails non lus** : Tri **chronologique descendant** (plus récent en premier) - Bénéfique pour voir les nouveaux messages en priorité

2. **Score moyen** : Le tri n'est **pas nécessaire** pour calculer une moyenne (on parcourt simplement tous les éléments). Cependant, un tri pourrait être utile pour identifier la médiane ou les extrêmes.

3. **Contacts téléphoniques** : Tri **alphabétique ascendant** (A-Z) - Essentiel pour retrouver rapidement un contact

4. **Transactions bancaires** : Tri **chronologique ascendant** (du plus ancien au plus récent) - Nécessaire pour calculer le solde progressif jour après jour

5. **Articles les plus chers** : Tri **numérique descendant** par prix - Nécessaire pour identifier le top 10

6. **Commentaires de blog** : Tri **chronologique** (ascendant pour ordre de conversation, ou descendant pour voir les plus récents) - Le choix dépend de l'UX souhaitée

**Explication :** Le tri est particulièrement utile quand on doit :

- Rechercher efficacement des éléments
- Afficher des données dans un ordre logique pour l'utilisateur
- Identifier des extrêmes (min, max, top N)
- Fusionner ou comparer des ensembles de données

</details>

---

## 📊 Critères Communs pour Trier les Données

Les critères utilisés pour le tri dépendent entièrement du problème spécifique à résoudre et du type de données impliquées.

---

### Ordre Numérique

**Ordre ascendant :** Arrangeant les nombres du plus petit au plus grand (ex: 1, 5, 10, 22).

```javascript
const prix = [29.99, 9.99, 49.99, 19.99];

// Tri ascendant (croissant)
prix.sort((a, b) => a - b);
console.log(prix); // [9.99, 19.99, 29.99, 49.99]
```

**Ordre descendant :** Arrangeant les nombres du plus grand au plus petit (ex: 22, 10, 5, 1).

```javascript
const scores = [85, 92, 78, 95, 88];

// Tri descendant (décroissant) pour un classement
scores.sort((a, b) => b - a);
console.log(scores); // [95, 92, 88, 85, 78]
```

**Cas d'usage :**

- Tri ascendant : afficher les prix du moins cher au plus cher
- Tri descendant : tableaux de classement (meilleur score en premier)

---

### Ordre Alphabétique

**Ordre ascendant (A-Z) :** Arrangeant les chaînes selon l'ordre lexicographique des caractères.

```javascript
const fruits = ["Banane", "Cerise", "Pomme", "Abricot"];

// Tri alphabétique A-Z
fruits.sort((a, b) => a.localeCompare(b));
console.log(fruits); // ['Abricot', 'Banane', 'Cerise', 'Pomme']
```

**Ordre descendant (Z-A) :** Arrangeant les chaînes en ordre lexicographique inverse.

```javascript
const noms = ["Chermann", "Ingrid", "Prudence", "Germain"];

// Tri alphabétique Z-A
noms.sort((a, b) => b.localeCompare(a));
console.log(noms); // ['Prudence', 'Ingrid', 'Germain', 'Chermann']
```

**Cas d'usage :**

- Tri A-Z : annuaires, listes de contacts, entrées de dictionnaire
- Tri Z-A : moins courant, utilisé pour des besoins d'affichage spécifiques

---

### Ordre Chronologique

**Ordre ascendant (Plus ancien au plus récent) :**

```javascript
const evenements = [
  { nom: "Réunion", date: new Date("2024-01-15") },
  { nom: "Deadline", date: new Date("2024-01-05") },
  { nom: "Lancement", date: new Date("2024-02-01") },
];

// Tri chronologique ascendant
evenements.sort((a, b) => a.date - b.date);
console.log(evenements.map((e) => e.nom));
// ['Deadline', 'Réunion', 'Lancement']
```

**Ordre descendant (Plus récent au plus ancien) :**

```javascript
const publications = [
  { titre: "Article A", publie: new Date("2024-01-10") },
  { titre: "Article B", publie: new Date("2024-01-20") },
  { titre: "Article C", publie: new Date("2024-01-05") },
];

// Tri chronologique descendant (plus récent en premier)
publications.sort((a, b) => b.publie - a.publie);
console.log(publications.map((p) => p.titre));
// ['Article B', 'Article A', 'Article C']
```

**Cas d'usage :**

- Ascendant : logs d'événements, analyse de données historiques
- Descendant : fils d'actualités, boîtes de réception email, activités récentes

---

### Ordre Personnalisé

Parfois, les données doivent être triées selon des critères qui ne sont pas strictement numériques, alphabétiques ou chronologiques, mais plutôt définis par une **logique métier** ou des exigences applicatives spécifiques.

**Exemple : Système de Gestion de Tâches (Intégration de l'Étude de Cas)**

Dans notre étude de cas de gestion de tâches, les tâches pourraient être triées selon plusieurs critères :

- **Tri primaire :** Par niveau de priorité (Haute, Moyenne, Basse)
- **Tri secondaire :** Pour les tâches de même priorité, tri par date d'échéance
- **Tri tertiaire :** Si priorité et échéance identiques, tri par date de création

```javascript
const taches = [
  {
    titre: "Corriger bug critique",
    priorite: "Haute",
    echeance: new Date("2024-01-20"),
    creation: new Date("2024-01-15"),
  },
  {
    titre: "Mettre à jour docs",
    priorite: "Basse",
    echeance: new Date("2024-01-14"),
    creation: new Date("2024-01-10"),
  },
  {
    titre: "Review code",
    priorite: "Moyenne",
    echeance: new Date("2024-01-22"),
    creation: new Date("2024-01-12"),
  },
  {
    titre: "Déployer version",
    priorite: "Haute",
    echeance: new Date("2024-01-18"),
    creation: new Date("2024-01-14"),
  },
];

// Définir l'ordre des priorités
const ordrePriorite = { Haute: 1, Moyenne: 2, Basse: 3 };

// Tri multi-critères personnalisé
taches.sort((a, b) => {
  // 1. Tri primaire par priorité
  if (ordrePriorite[a.priorite] !== ordrePriorite[b.priorite]) {
    return ordrePriorite[a.priorite] - ordrePriorite[b.priorite];
  }

  // 2. Tri secondaire par date d'échéance
  if (a.echeance.getTime() !== b.echeance.getTime()) {
    return a.echeance - b.echeance;
  }

  // 3. Tri tertiaire par date de création
  return a.creation - b.creation;
});

console.log(taches.map((t) => `${t.priorite}: ${t.titre}`));
// ['Haute: Déployer version', 'Haute: Corriger bug critique',
//  'Moyenne: Review code', 'Basse: Mettre à jour docs']
```

Ce tri multi-niveaux garantit que les tâches les plus critiques et urgentes apparaissent en haut de la liste.

---

## 📝 Micro-Exercice #2 : Tri Personnalisé

**Objectif :** Implémenter une fonction de comparaison personnalisée.

**Instructions :** Triez la liste de produits suivante selon ces règles :

1. Les produits en stock avant les produits épuisés
2. Pour les produits en stock, tri par prix ascendant
3. Pour les produits épuisés, tri alphabétique par nom

```javascript
const produits = [
  { nom: "Laptop", prix: 999, enStock: true },
  { nom: "Souris", prix: 29, enStock: false },
  { nom: "Clavier", prix: 79, enStock: true },
  { nom: "Écran", prix: 299, enStock: false },
  { nom: "Webcam", prix: 89, enStock: true },
];

// Votre fonction de tri ici
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
const produits = [
  { nom: "Laptop", prix: 999, enStock: true },
  { nom: "Souris", prix: 29, enStock: false },
  { nom: "Clavier", prix: 79, enStock: true },
  { nom: "Écran", prix: 299, enStock: false },
  { nom: "Webcam", prix: 89, enStock: true },
];

produits.sort((a, b) => {
  // 1. Produits en stock en premier
  if (a.enStock !== b.enStock) {
    return a.enStock ? -1 : 1; // true avant false
  }

  // 2. Si même statut de stock
  if (a.enStock) {
    // En stock : tri par prix ascendant
    return a.prix - b.prix;
  } else {
    // Épuisé : tri alphabétique
    return a.nom.localeCompare(b.nom);
  }
});

console.log(produits);
// [
//   { nom: 'Clavier', prix: 79, enStock: true },
//   { nom: 'Webcam', prix: 89, enStock: true },
//   { nom: 'Laptop', prix: 999, enStock: true },
//   { nom: 'Écran', prix: 299, enStock: false },
//   { nom: 'Souris', prix: 29, enStock: false }
// ]
```

**Explication :**

1. On compare d'abord le statut `enStock` - les produits en stock (true) passent avant
2. Pour les produits en stock, on compare les prix (croissant)
3. Pour les produits épuisés, on compare les noms alphabétiquement

</details>

---

## ⚙️ Considérations Pratiques pour le Tri

Si les avantages du tri sont clairs, il existe des considérations pratiques concernant les **performances** et la **stabilité** que les développeurs doivent prendre en compte.

---

### Performance (Complexité Temporelle et Spatiale)

Les algorithmes de tri diffèrent significativement dans leur efficacité, surtout quand la taille des données croît. Comme vu dans le Module 1, comprendre la complexité temporelle et spatiale est crucial pour choisir le bon algorithme.

**Complexité temporelle :**

| Algorithme     | Meilleur cas | Cas moyen  | Pire cas   |
| -------------- | ------------ | ---------- | ---------- |
| Bubble Sort    | O(n)         | O(n²)      | O(n²)      |
| Insertion Sort | O(n)         | O(n²)      | O(n²)      |
| Selection Sort | O(n²)        | O(n²)      | O(n²)      |
| Merge Sort     | O(n log n)   | O(n log n) | O(n log n) |
| Quick Sort     | O(n log n)   | O(n log n) | O(n²)      |
| Heap Sort      | O(n log n)   | O(n log n) | O(n log n) |
| Counting Sort  | O(n + k)     | O(n + k)   | O(n + k)   |
| Radix Sort     | O(d × n)     | O(d × n)   | O(d × n)   |

> **Note importante**
>
> Les algorithmes simples comme Bubble Sort ont une complexité O(n²) : si vous doublez la taille des données, le temps de traitement **quadruple**. Les algorithmes avancés comme Merge Sort avec O(n log n) sont beaucoup plus scalables pour de grands ensembles de données.

**Complexité spatiale :**

Mesure la quantité de stockage temporaire qu'un algorithme nécessite.

| Algorithme     | Espace auxiliaire |
| -------------- | ----------------- |
| Bubble Sort    | O(1)              |
| Insertion Sort | O(1)              |
| Selection Sort | O(1)              |
| Merge Sort     | O(n)              |
| Quick Sort     | O(log n)          |
| Heap Sort      | O(1)              |

Certains algorithmes peuvent trier "en place" sans nécessiter beaucoup de mémoire supplémentaire (O(1)), tandis que d'autres nécessitent un espace significatif (O(n) pour Merge Sort).

---

### Stabilité des Algorithmes de Tri

Un algorithme de tri est considéré **stable** s'il maintient l'ordre relatif des éléments ayant des valeurs égales.

**Exemple illustratif :**

Considérons une liste de tâches où chaque tâche a une priorité et une date de création :

```javascript
const taches = [
  { nom: "Tâche A", priorite: "Moyenne", creation: "2024-01-05" },
  { nom: "Tâche B", priorite: "Haute", creation: "2024-01-01" },
  { nom: "Tâche C", priorite: "Moyenne", creation: "2024-01-03" },
  { nom: "Tâche D", priorite: "Basse", creation: "2024-01-02" },
];
```

Si nous trions cette liste par priorité (Basse, Moyenne, Haute) :

**Résultat avec tri STABLE :**

```javascript
// L'ordre original entre A et C (tous deux 'Moyenne') est PRÉSERVÉ
// A était avant C dans la liste originale, donc A reste avant C
[
  { nom: "Tâche D", priorite: "Basse" }, // Seul élément Basse
  { nom: "Tâche A", priorite: "Moyenne" }, // A était AVANT C originellement
  { nom: "Tâche C", priorite: "Moyenne" }, // C était APRÈS A originellement
  { nom: "Tâche B", priorite: "Haute" }, // Seul élément Haute
];
```

**Résultat possible avec tri INSTABLE :**

```javascript
// L'ordre entre A et C peut être INVERSÉ arbitrairement
[
  { nom: "Tâche D", priorite: "Basse" },
  { nom: "Tâche C", priorite: "Moyenne" }, // C avant A - ordre changé !
  { nom: "Tâche A", priorite: "Moyenne" },
  { nom: "Tâche B", priorite: "Haute" },
];
```

**Pourquoi la stabilité est importante :**

La stabilité est cruciale quand les éléments ont plusieurs attributs et que maintenir leur ordre relatif original pour certains attributs est important.

Par exemple, si vous triez d'abord une liste de produits par catégorie, puis par prix, un tri stable garantira que les produits de même catégorie et même prix restent dans leur ordre original.

| Algorithme     | Stable ? |
| -------------- | -------- |
| Bubble Sort    | Oui      |
| Insertion Sort | Oui      |
| Merge Sort     | Oui      |
| Selection Sort | Non      |
| Quick Sort     | Non      |
| Heap Sort      | Non      |

---

## 📝 Micro-Exercice #3 : Stabilité du Tri

**Objectif :** Comprendre l'impact de la stabilité.

**Instructions :** Vous avez une liste d'employés triée par département (alphabétiquement). Vous voulez ensuite trier par salaire (croissant) tout en gardant les employés du même département groupés si possible.

```javascript
const employes = [
  { nom: "Chermann", dept: "RH", salaire: 70000 },
  { nom: "Prudence", dept: "Engineering", salaire: 80000 },
  { nom: "Ingrid", dept: "RH", salaire: 75000 },
  { nom: "Germain", dept: "Engineering", salaire: 80000 },
];

// La liste est déjà triée par département : Engineering, Engineering, RH, RH
// (alphabétiquement)
```

1. Quel serait l'ordre final avec un tri **stable** par salaire ?
2. Quel serait un ordre **possible** avec un tri instable ?

<details>
<summary>💡 Voir la solution</summary>

**Après tri initial par département (alphabétique) :**

```javascript
[
  { nom: "Prudence", dept: "Engineering", salaire: 80000 },
  { nom: "Germain", dept: "Engineering", salaire: 80000 },
  { nom: "Chermann", dept: "RH", salaire: 70000 },
  { nom: "Ingrid", dept: "RH", salaire: 75000 },
];
```

**1. Tri STABLE par salaire (croissant) :**

```javascript
[
  { nom: "Chermann", dept: "RH", salaire: 70000 }, // Plus petit salaire
  { nom: "Ingrid", dept: "RH", salaire: 75000 },
  { nom: "Prudence", dept: "Engineering", salaire: 80000 }, // Prudence AVANT Germain
  { nom: "Germain", dept: "Engineering", salaire: 80000 }, // (ordre original préservé)
];
```

Prudence et Germain ont le même salaire (80000). Un tri stable préserve leur ordre original : Prudence était avant Germain après le tri par département.

**2. Tri INSTABLE par salaire (ordre possible) :**

```javascript
[
  { nom: "Chermann", dept: "RH", salaire: 70000 },
  { nom: "Ingrid", dept: "RH", salaire: 75000 },
  { nom: "Germain", dept: "Engineering", salaire: 80000 }, // Germain AVANT Prudence !
  { nom: "Prudence", dept: "Engineering", salaire: 80000 }, // Ordre inversé
];
```

Un tri instable peut inverser l'ordre de Prudence et Germain puisqu'ils ont le même salaire.

**Impact pratique :** Si vous voulez que les employés du même département restent groupés après un tri par salaire, vous devez utiliser un tri stable ou trier par les deux critères simultanément.

</details>

---

## 💻 Application Pratique : Préparation au Tri

Avant d'implémenter des algorithmes de tri complexes, voyons comment JavaScript gère le tri nativement.

---

### La Méthode `sort()` de JavaScript

JavaScript fournit une méthode `sort()` intégrée pour les tableaux. Cependant, elle a des **comportements surprenants** qu'il faut connaître.

```javascript
// Comportement par défaut de sort() - ATTENTION !
const nombres = [10, 2, 30, 21, 5];
nombres.sort();
console.log(nombres); // [10, 2, 21, 30, 5] - INCORRECT !

// Pourquoi ? Par défaut, sort() convertit en chaînes et trie alphabétiquement !
// "10" < "2" car '1' < '2' en comparaison de caractères
```

**Solution : Toujours fournir une fonction de comparaison**

```javascript
// Tri numérique correct
const nombres = [10, 2, 30, 21, 5];
nombres.sort((a, b) => a - b);
console.log(nombres); // [2, 5, 10, 21, 30] - CORRECT !

// Comment ça Destinéehe ?
// La fonction de comparaison retourne :
// - Un nombre négatif si a doit venir AVANT b
// - Un nombre positif si a doit venir APRÈS b
// - Zéro si a et b sont égaux
```

---

### Fonction de Comparaison Détaillée

```javascript
/**
 * Fonction de comparaison pour le tri
 * @param {*} a - Premier élément à comparer
 * @param {*} b - Deuxième élément à comparer
 * @returns {number} - Négatif (a avant b), Positif (a après b), Zéro (égaux)
 */
function comparerNombres(a, b) {
  if (a < b) {
    return -1; // a vient avant b
  } else if (a > b) {
    return 1; // a vient après b
  } else {
    return 0; // égaux, ordre préservé
  }
}

// Équivalent simplifié pour les nombres :
const comparerNombresSimple = (a, b) => a - b;

// Exemples
console.log(comparerNombresSimple(5, 10)); // -5 (négatif : 5 avant 10)
console.log(comparerNombresSimple(10, 5)); // 5 (positif : 10 après 5)
console.log(comparerNombresSimple(7, 7)); // 0 (égaux)
```

---

### Tri d'Objets

```javascript
const utilisateurs = [
  { nom: "Sing", age: 16 },
  { nom: "Chermann", age: 43 },
  { nom: "Destinée", age: 14 },
];

// Tri par âge (croissant)
utilisateurs.sort((a, b) => a.age - b.age);
console.log(utilisateurs);
// [{ nom: 'Destinée', age: 14 }, { nom: 'Sing', age: 16 }, { nom: 'Chermann', age: 43 }]

// Tri par nom (alphabétique)
utilisateurs.sort((a, b) => a.nom.localeCompare(b.nom));
console.log(utilisateurs);
// [{ nom: 'Chermann', age: 43 }, { nom: 'Destinée', age: 14 }, { nom: 'Sing', age: 16 }]
```

> **Note importante**
>
> La méthode `sort()` de JavaScript modifie le tableau **en place** (mutation). Si vous voulez préserver le tableau original, créez d'abord une copie : `const copie = [...original].sort(...)`.

---

## 💪 Exercices Pratiques

Pour solidifier votre compréhension des concepts de tri, implémentez les problèmes suivants.

---

### Exercice 1 : Trier des Étudiants

**Objectif :** Pratiquer le tri multi-critères.

**Instructions :** Triez la liste d'étudiants selon ces règles :

1. Par note (décroissant - meilleure note en premier)
2. En cas d'égalité de notes, par nom (alphabétique)

```javascript
const etudiants = [
  { nom: "Germain", note: 85 },
  { nom: "Sarr", note: 92 },
  { nom: "Ingrid", note: 85 },
  { nom: "Chermann", note: 92 },
  { nom: "Prudence", note: 78 },
];

// Votre solution ici
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
const etudiants = [
  { nom: "Germain", note: 85 },
  { nom: "Sarr", note: 92 },
  { nom: "Ingrid", note: 85 },
  { nom: "Chermann", note: 92 },
  { nom: "Prudence", note: 78 },
];

etudiants.sort((a, b) => {
  // 1. Tri primaire par note (décroissant)
  if (b.note !== a.note) {
    return b.note - a.note;
  }
  // 2. Tri secondaire par nom (alphabétique)
  return a.nom.localeCompare(b.nom);
});

console.log(etudiants);
// [
//   { nom: 'Chermann', note: 92 },
//   { nom: 'Sarr', note: 92 },
//   { nom: 'Germain', note: 85 },
//   { nom: 'Ingrid', note: 85 },
//   { nom: 'Prudence', note: 78 }
// ]
```

**Explication :**

- Les notes 92 sont en premier (décroissant)
- Chermann vient avant Sarr (alphabétique)
- Les notes 85 suivent
- Germain vient avant Ingrid (alphabétique)
- Prudence avec 78 est dernier

</details>

---

### Exercice 2 : Tri de Fichiers

**Objectif :** Implémenter un tri personnalisé complexe.

**Instructions :** Triez une liste de fichiers selon ces règles :

1. Les dossiers avant les fichiers
2. Les dossiers triés alphabétiquement
3. Les fichiers triés par taille (décroissant)

```javascript
const fichiers = [
  { nom: "document.pdf", type: "fichier", taille: 1400 },
  { nom: "Images", type: "dossier", taille: 0 },
  { nom: "photo.jpg", type: "fichier", taille: 5000 },
  { nom: "Documents", type: "dossier", taille: 0 },
  { nom: "notes.txt", type: "fichier", taille: 500 },
];

// Votre solution ici
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
const fichiers = [
  { nom: "document.pdf", type: "fichier", taille: 1400 },
  { nom: "Images", type: "dossier", taille: 0 },
  { nom: "photo.jpg", type: "fichier", taille: 5000 },
  { nom: "Documents", type: "dossier", taille: 0 },
  { nom: "notes.txt", type: "fichier", taille: 500 },
];

fichiers.sort((a, b) => {
  // 1. Dossiers avant fichiers
  if (a.type !== b.type) {
    return a.type === "dossier" ? -1 : 1;
  }

  // 2. Si même type
  if (a.type === "dossier") {
    // Dossiers : tri alphabétique
    return a.nom.localeCompare(b.nom);
  } else {
    // Fichiers : tri par taille décroissant
    return b.taille - a.taille;
  }
});

console.log(fichiers);
// [
//   { nom: 'Documents', type: 'dossier', taille: 0 },
//   { nom: 'Images', type: 'dossier', taille: 0 },
//   { nom: 'photo.jpg', type: 'fichier', taille: 5000 },
//   { nom: 'document.pdf', type: 'fichier', taille: 1400 },
//   { nom: 'notes.txt', type: 'fichier', taille: 500 }
// ]
```

**Explication :**

- Les dossiers (Documents, Images) apparaissent en premier, triés A-Z
- Les fichiers suivent, triés par taille décroissante

</details>

---

### Exercice 3 : Vérifier si un Tableau est Trié

**Objectif :** Créer une fonction utilitaire de vérification.

**Instructions :** Implémentez une fonction qui vérifie si un tableau est trié (ascendant ou descendant).

```javascript
function estTrie(tableau, ordre = "asc") {
  // Votre implémentation ici
}

// Tests
console.log(estTrie([1, 2, 3, 4, 5])); // true (ascendant)
console.log(estTrie([5, 4, 3, 2, 1], "desc")); // true (descendant)
console.log(estTrie([1, 3, 2, 4, 5])); // false
console.log(estTrie([1, 1, 2, 2, 3])); // true (égalités acceptées)
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Vérifie si un tableau est trié
 * @param {Array} tableau - Le tableau à vérifier
 * @param {string} ordre - 'asc' pour ascendant, 'desc' pour descendant
 * @returns {boolean} - true si le tableau est trié selon l'ordre spécifié
 */
function estTrie(tableau, ordre = "asc") {
  // Tableau vide ou avec un seul élément est toujours trié
  if (tableau.length <= 1) {
    return true;
  }

  for (let i = 1; i < tableau.length; i++) {
    if (ordre === "asc") {
      // Ascendant : chaque élément >= précédent
      if (tableau[i] < tableau[i - 1]) {
        return false;
      }
    } else {
      // Descendant : chaque élément <= précédent
      if (tableau[i] > tableau[i - 1]) {
        return false;
      }
    }
  }

  return true;
}

// Tests
console.log(estTrie([1, 2, 3, 4, 5])); // true
console.log(estTrie([5, 4, 3, 2, 1], "desc")); // true
console.log(estTrie([1, 3, 2, 4, 5])); // false
console.log(estTrie([1, 1, 2, 2, 3])); // true
console.log(estTrie([])); // true (cas limite)
console.log(estTrie([42])); // true (cas limite)
```

**Explication :**

- On parcourt le tableau en comparant chaque élément avec le précédent
- Pour l'ordre ascendant, on vérifie que chaque élément n'est pas inférieur au précédent
- Pour l'ordre descendant, on vérifie que chaque élément n'est pas supérieur au précédent
- Les égalités sont acceptées dans les deux cas

</details>

---

### Exercice 4 : Tri de Tâches (Étude de Cas)

**Objectif :** Appliquer le tri à notre étude de cas de gestion de tâches.

**Instructions :** Implémentez une fonction `trierTaches` qui accepte une liste de tâches et un critère de tri.

```javascript
const taches = [
  {
    id: 1,
    titre: "Réviser code",
    priorite: "Moyenne",
    echeance: "2024-01-14",
    terminee: false,
  },
  {
    id: 2,
    titre: "Corriger bug",
    priorite: "Haute",
    echeance: "2024-01-20",
    terminee: false,
  },
  {
    id: 3,
    titre: "Écrire tests",
    priorite: "Basse",
    echeance: "2024-01-30",
    terminee: true,
  },
  {
    id: 4,
    titre: "Déployer",
    priorite: "Haute",
    echeance: "2024-01-22",
    terminee: false,
  },
];

function trierTaches(taches, critere) {
  // Critères possibles : 'priorite', 'echeance', 'titre', 'statut'
  // Votre implémentation ici
}
```

<details>
<summary>💡 Voir la solution</summary>

```javascript
/**
 * Trie une liste de tâches selon différents critères
 * @param {Array} taches - Liste des tâches
 * @param {string} critere - Critère de tri
 * @returns {Array} - Nouvelle liste triée (ne modifie pas l'original)
 */
function trierTaches(taches, critere) {
  // Créer une copie pour ne pas modifier l'original
  const copie = [...taches];

  const ordrePriorite = { Haute: 1, Moyenne: 2, Basse: 3 };

  switch (critere) {
    case "priorite":
      // Haute > Moyenne > Basse
      return copie.sort(
        (a, b) => ordrePriorite[a.priorite] - ordrePriorite[b.priorite],
      );

    case "echeance":
      // Plus proche en premier
      return copie.sort((a, b) => new Date(a.echeance) - new Date(b.echeance));

    case "titre":
      // Alphabétique A-Z
      return copie.sort((a, b) => a.titre.localeCompare(b.titre));

    case "statut":
      // Non terminées en premier, puis par priorité
      return copie.sort((a, b) => {
        if (a.terminee !== b.terminee) {
          return a.terminee ? 1 : -1; // false avant true
        }
        return ordrePriorite[a.priorite] - ordrePriorite[b.priorite];
      });

    default:
      return copie;
  }
}

// Tests
const taches = [
  {
    id: 1,
    titre: "Réviser code",
    priorite: "Moyenne",
    echeance: "2024-01-14",
    terminee: false,
  },
  {
    id: 2,
    titre: "Corriger bug",
    priorite: "Haute",
    echeance: "2024-01-20",
    terminee: false,
  },
  {
    id: 3,
    titre: "Écrire tests",
    priorite: "Basse",
    echeance: "2024-01-30",
    terminee: true,
  },
  {
    id: 4,
    titre: "Déployer",
    priorite: "Haute",
    echeance: "2024-01-22",
    terminee: false,
  },
];

console.log("Par priorité:");
console.log(trierTaches(taches, "priorite").map((t) => t.titre));
// ['Corriger bug', 'Déployer', 'Réviser code', 'Écrire tests']

console.log("\nPar échéance:");
console.log(trierTaches(taches, "echeance").map((t) => t.titre));
// ['Corriger bug', 'Déployer', 'Réviser code', 'Écrire tests']

console.log("\nPar statut:");
console.log(
  trierTaches(taches, "statut").map(
    (t) => `${t.titre} (${t.terminee ? "✓" : "○"})`,
  ),
);
// ['Corriger bug (○)', 'Déployer (○)', 'Réviser code (○)', 'Écrire tests (✓)']
```

**Explication :**

- On utilise `[...taches]` pour créer une copie et éviter de modifier l'original
- Chaque critère a sa propre logique de comparaison
- Pour le statut, on combine deux critères : terminée et priorité

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1

Quel est l'avantage principal de trier les données avant d'effectuer une recherche ?

- [ ] A. Le tri rend les données plus lisibles pour les humains
- [ ] B. Le tri permet d'utiliser des algorithmes de recherche plus efficaces comme la recherche binaire
- [ ] C. Le tri réduit la taille des données en mémoire
- [ ] D. Le tri supprime automatiquement les doublons

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Le tri permet d'utiliser des algorithmes de recherche comme la recherche binaire qui opère en O(log n) au lieu de O(n) pour une recherche linéaire. Sur un million d'éléments, cela représente environ 20 comparaisons au lieu d'un million.

</details>

---

### Question 2

Quelle est la complexité temporelle dans le pire cas du tri Bubble Sort ?

- [ ] A. O(n)
- [ ] B. O(n log n)
- [ ] C. O(n²)
- [ ] D. O(log n)

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Bubble Sort a une complexité de O(n²) dans le pire cas, ce qui signifie que si vous doublez la taille des données, le temps de traitement quadruple. C'est pourquoi il n'est pas adapté aux grands ensembles de données.

</details>

---

### Question 3

Qu'est-ce qu'un algorithme de tri "stable" ?

- [ ] A. Un algorithme qui ne plante jamais
- [ ] B. Un algorithme qui maintient l'ordre relatif des éléments ayant des valeurs égales
- [ ] C. Un algorithme qui utilise peu de mémoire
- [ ] D. Un algorithme qui fonctionne sur tous les types de données

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Un algorithme stable préserve l'ordre original des éléments qui ont la même valeur de tri. Par exemple, si Chermann et Prudence ont la même note et qu'Chermann apparaissait avant Prudence dans la liste originale, un tri stable par note gardera Chermann avant Prudence.

</details>

---

### Question 4

Que retourne `[10, 2, 30].sort()` en JavaScript sans fonction de comparaison ?

- [ ] A. [2, 10, 30]
- [ ] B. [30, 10, 2]
- [ ] C. [10, 2, 30]
- [ ] D. [10, 2, 30] ou [2, 30, 10] selon le navigateur

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Par défaut, `sort()` convertit les éléments en chaînes de caractères et les trie alphabétiquement. "10" vient avant "2" car le caractère '1' a un code inférieur à '2'. Pour un tri numérique correct, utilisez : `sort((a, b) => a - b)`.

</details>

---

### Question 5

Dans une fonction de comparaison pour `sort()`, que signifie un retour négatif ?

- [ ] A. Les deux éléments sont égaux
- [ ] B. Le premier élément doit venir après le second
- [ ] C. Le premier élément doit venir avant le second
- [ ] D. Une erreur s'est produite

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Dans une fonction de comparaison `(a, b) => ...` :

- Retour négatif : a vient AVANT b
- Retour positif : a vient APRÈS b
- Retour zéro : ordre préservé (égaux)

</details>

---

### Question 6

Parmi ces algorithmes, lesquels sont stables ? (Plusieurs réponses possibles)

- [ ] A. Bubble Sort
- [ ] B. Quick Sort
- [ ] C. Merge Sort
- [ ] D. Insertion Sort

<details>
<summary>Voir la réponse</summary>

**Réponses : A, C, D**

- **Bubble Sort** : Stable - Ne permute que si strictement supérieur
- **Quick Sort** : Instable - Le partitionnement peut réorganiser les égaux
- **Merge Sort** : Stable - La fusion préserve l'ordre des égaux
- **Insertion Sort** : Stable - Insère avant les éléments strictement plus grands

</details>

---

### Question 7

Pour trier des tâches d'abord par priorité (Haute, Moyenne, Basse) puis par date d'échéance, quelle approche est correcte ?

- [ ] A. Faire deux appels successifs à `sort()`
- [ ] B. Utiliser une seule fonction de comparaison qui vérifie les deux critères
- [ ] C. Utiliser `filter()` puis `sort()`
- [ ] D. Les approches A et B donnent le même résultat si le tri est stable

<details>
<summary>Voir la réponse</summary>

**Réponse : D**

Avec un tri **stable**, vous pouvez :

1. Trier d'abord par date d'échéance
2. Puis trier par priorité (le tri stable préservera l'ordre des dates pour les priorités égales)

Ou utiliser une seule fonction de comparaison qui vérifie les deux critères, ce qui est généralement plus efficace et fonctionne indépendamment de la stabilité.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Définition du Tri

Le tri est le processus d'arrangement des éléments dans un ordre spécifique (numérique, alphabétique, chronologique, ou personnalisé) pour faciliter les opérations ultérieures.

### 2. Avantages des Données Triées

Les données triées permettent des recherches plus rapides (O(log n) vs O(n)), facilitent la fusion de données, et améliorent les performances de nombreux algorithmes.

### 3. Critères de Tri

Les données peuvent être triées selon des critères variés : numérique (ascendant/descendant), alphabétique (A-Z/Z-A), chronologique, ou selon une logique métier personnalisée.

### 4. Complexité Temporelle

Les algorithmes simples (Bubble, Insertion) ont une complexité O(n²), tandis que les algorithmes avancés (Merge, Quick) atteignent O(n log n) en moyenne.

### 5. Complexité Spatiale

Certains algorithmes trient "en place" avec O(1) d'espace supplémentaire, tandis que d'autres comme Merge Sort nécessitent O(n) d'espace auxiliaire.

### 6. Stabilité

Un tri stable préserve l'ordre relatif des éléments égaux. C'est important pour le tri multi-critères où l'ordre original a une signification.

### 7. `sort()` en JavaScript

La méthode `sort()` native convertit en chaînes par défaut. Utilisez toujours une fonction de comparaison : `(a, b) => a - b` pour les nombres.

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez posé les fondations essentielles pour comprendre le tri en informatique.

### Ce que vous avez appris aujourd'hui

- Pourquoi le tri est une opération fondamentale en informatique
- Les différents critères de tri et comment les implémenter
- L'importance de la complexité temporelle et spatiale
- La notion de stabilité des algorithmes de tri
- Comment utiliser correctement `sort()` en JavaScript

### Compétences acquises

Vous êtes maintenant capable de :

- Identifier quand le tri est nécessaire ou bénéfique dans un problème
- Choisir le bon critère de tri selon le contexte
- Implémenter des fonctions de comparaison personnalisées en JavaScript

### Pourquoi c'est important

> 📌 **Point Clé**
>
> Comprendre les principes du tri vous prépare à choisir le bon algorithme selon vos besoins. Dans les prochaines leçons, nous implémenterons ces algorithmes de A à Z, en commençant par les plus simples pour bien comprendre leurs mécanismes avant de passer aux plus efficaces.

---

## ➡️ Prochaine Étape : Leçon 14

### Ce qui vous attend

La prochaine leçon, **« Tri à Bulles (Bubble Sort) »**, vous fera découvrir votre premier algorithme de tri en détail.

**Vous découvrirez :**

- Le mécanisme du tri à bulles et sa logique de "bulles qui remontent"
- L'implémentation complète en JavaScript avec optimisations
- L'analyse de sa complexité et ses cas d'utilisation
- Pourquoi cet algorithme simple n'est pas adapté aux grands ensembles de données

### Préparez-vous !

Bubble Sort est un excellent point de départ pédagogique : simple à comprendre, il illustre parfaitement les concepts de comparaison et d'échange qui sont à la base de nombreux algorithmes de tri plus sophistiqués.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Visualgo - Sorting](https://visualgo.net/en/sorting) - Visualisation interactive des algorithmes de tri
- [MDN - Array.prototype.sort()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) - Documentation officielle
- [Sorting Algorithms Animations](https://www.toptal.com/developers/sorting-algorithms) - Comparaison visuelle des performances

### Outils de pratique

- **[JS Bin](https://jsbin.com/)** : Testez rapidement vos fonctions de tri
- **[Big-O Cheat Sheet](https://www.bigocheatsheet.com/)** : Référence rapide des complexités

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les exercices pratiques
- Expérimenter avec les exemples dans votre console

> 💡 **Conseil**
>
> Pour bien assimiler les concepts de tri, essayez de trier manuellement un petit jeu de cartes par valeur. Observez les opérations que vous faites naturellement : comparer deux cartes, les échanger, parcourir le jeu... Ce sont exactement les opérations que font les algorithmes de tri !

---

**Prêt pour la Leçon 14 ?** 🚀

Rendez-vous dans la prochaine leçon pour implémenter votre premier algorithme de tri : le Bubble Sort !

---

<div align="center">

**Leçon 13 sur 42 - Module 3 : Techniques de Tri Essentielles**

[⬅️ Leçon 12 : Pratique : Utiliser Piles/Files pour la Priorisation des Tâches dans l'Étude de Cas](../module-2/lecon-6-pratique-utiliser-piles-files-priorisation-taches-etude-cas.md) | [Retour au sommaire](./README.md) | [Leçon 14 : Tri à Bulles : Concept et Implémentation JavaScript de Base ➡️](./lecon-2-tri-bulles-concept-implementation-javascript-base.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
