##### Leçon 11 sur 42

# Files : Principe FIFO et Implémentation Basée sur Tableaux

**Module 2** : Structures de Données Essentielles en JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre le principe FIFO (First-In, First-Out) des files
- Implémenter une file en JavaScript avec des tableaux
- Distinguer les files des piles (FIFO vs LIFO)
- Maîtriser les opérations fondamentales : enqueue, dequeue, peek
- Analyser la complexité temporelle des différentes implémentations
- Reconnaître les applications pratiques des files

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

Avant de commencer cette leçon, vous devez maîtriser :

- [Les opérations sur les tableaux JavaScript (push, shift, length)](./lecon-1-tableaux-listes-dynamiques-operations-base.md)
- Les classes ES6 et la syntaxe orientée objet
- La notation Big O et l'analyse de complexité
- [Le Principe LIFO des piles (leçon précédente)](./lecon-4-piles-principe-lifo-implementation-tableaux.md)

---

## 🚀 Introduction : Les Files, Structures FIFO Essentielles

Imaginez une file d'attente au guichet d'un cinéma. La **première personne arrivée** est la **première servie**. Si Chermann arrive à 14h00, Ingrid à 14h05 et Prudence à 14h10, ils seront servis dans cet ordre exact : Chermann → Ingrid → Prudence.

C'est exactement le principe d'une **file (queue)** en programmation : une structure de données linéaire qui suit le principe **FIFO (First-In, First-Out)**. Le premier élément ajouté sera toujours le premier retiré.

**Différence avec une pile** :

- **Pile (Stack)** : LIFO = Last-In, First-Out = comme une pile d'assiettes
- **File (Queue)** : FIFO = First-In, First-Out = comme une file d'attente

Les files sont omniprésentes en informatique : gestion des tâches dans un système d'exploitation, traitement des requêtes sur un serveur web, files de messages dans les applications distribuées, etc.

---

## 1️⃣ Principe FIFO : Le Cœur des Files

### Définition

Une **file (queue)** est une structure de données linéaire où :

- Les éléments sont **ajoutés à l'arrière** (rear/tail)
- Les éléments sont **retirés de l'avant** (front/head)
- L'ordre de traitement respecte **l'ordre d'arrivée**

### Visualisation du Principe FIFO

```
              ENQUEUE (ajouter)
                     ↓
    ┌──────────────────────────────────┐
    │  ARRIÈRE (Rear)    AVANT (Front) │
    │       ←              ←           │
    │    [D] [C] [B] [A]               │
    │                     ↑            │
    └─────────────────────┼────────────┘
                          │
                    DEQUEUE (retirer)

Ordre d'ajout : A → B → C → D
Ordre de retrait : A → B → C → D
```

### Exemple Concret : Centre d'Appels

```javascript
// Simulation d'un centre d'appels
const centreAppels = [];

// Les clients appellent dans cet ordre :
centreAppels.push("Client A - 14h00"); // Premier arrivé
centreAppels.push("Client B - 14h05");
centreAppels.push("Client C - 14h10");
centreAppels.push("Client D - 14h15"); // Dernier arrivé

console.log("File d'attente :", centreAppels);
// ["Client A - 14h00", "Client B - 14h05", "Client C - 14h10", "Client D - 14h15"]

// Un conseiller se libère et prend le premier appel
const premierClient = centreAppels.shift(); // Client A (premier arrivé)
console.log("En cours de traitement :", premierClient);
// En cours de traitement : Client A - 14h00

console.log("File d'attente restante :", centreAppels);
// ["Client B - 14h05", "Client C - 14h10", "Client D - 14h15"]
```

**Principe clé** : Le client A, arrivé en premier, est servi en premier. C'est FIFO !

---

## 2️⃣ Opérations Fondamentales d'une File

### Les 6 Opérations Essentielles

| Opération     | Description                                  | Complexité |
| ------------- | -------------------------------------------- | ---------- |
| **enqueue()** | Ajouter un élément à l'arrière de la file    | O(1)       |
| **dequeue()** | Retirer un élément de l'avant de la file     | Variable   |
| **peek()**    | Consulter le premier élément sans le retirer | O(1)       |
| **isEmpty()** | Vérifier si la file est vide                 | O(1)       |
| **size()**    | Obtenir le nombre d'éléments dans la file    | O(1)       |
| **clear()**   | Vider complètement la file                   | O(1)       |

---

### Opération 1 : `enqueue(element)` - Enfiler

**Ajouter un élément à l'arrière** de la file.

```javascript
// Avant enqueue(40)
File : [10, 20, 30]
       ↑          ↑
     Front      Rear

// Après enqueue(40)
File : [10, 20, 30, 40]
       ↑              ↑
     Front          Rear
```

**Exemple pratique** :

```javascript
const fileImpression = [];

// Un utilisateur envoie des documents à l'impression
function imprimerDocument(nomDocument) {
  fileImpression.push(nomDocument); // enqueue
  console.log(`${nomDocument} ajouté à la file d'impression.`);
}

imprimerDocument("Rapport.docx");
imprimerDocument("Présentation.pptx");
imprimerDocument("Image.jpg");

console.log("File d'impression :", fileImpression);
// ["Rapport.docx", "Présentation.pptx", "Image.jpg"]
```

---

### Opération 2 : `dequeue()` - Défiler

**Retirer et retourner l'élément à l'avant** de la file.

```javascript
// Avant dequeue()
File : [10, 20, 30, 40]
       ↑
    Élément retiré

// Après dequeue() → retourne 10
File : [20, 30, 40]
       ↑
     Front
```

**Exemple pratique** :

```javascript
// L'imprimante traite les documents dans l'ordre
function imprimerProchainDocument() {
  if (fileImpression.length === 0) {
    console.log("Aucun document en attente.");
    return null;
  }

  const document = fileImpression.shift(); // dequeue
  console.log(`Impression en cours : ${document}`);
  return document;
}

imprimerProchainDocument(); // Impression en cours : Rapport.docx
imprimerProchainDocument(); // Impression en cours : Présentation.pptx

console.log("File d'impression restante :", fileImpression);
// ["Image.jpg"]
```

---

### Opération 3 : `peek()` - Consulter

**Voir l'élément à l'avant sans le retirer**.

```javascript
// peek() retourne 20 sans modifier la file
File : [20, 30, 40]
       ↑
    peek() = 20
```

**Exemple pratique** :

```javascript
function voirProchainDocument() {
  if (fileImpression.length === 0) {
    return "Aucun document";
  }
  return fileImpression[0]; // peek
}

console.log("Prochain document :", voirProchainDocument());
// Prochain document : Image.jpg

console.log("File inchangée :", fileImpression);
// ["Image.jpg"] ← La file n'a pas été modifiée
```

---

### Opération 4 : `isEmpty()` - Est-elle vide ?

**Vérifier si la file contient des éléments**.

```javascript
function fileEstVide() {
  return fileImpression.length === 0;
}

console.log(fileEstVide()); // false (contient "Image.jpg")

imprimerProchainDocument(); // Retire "Image.jpg"

console.log(fileEstVide()); // true (file vide maintenant)
```

---

### Opération 5 : `size()` - Taille

**Obtenir le nombre d'éléments dans la file**.

```javascript
imprimerDocument("Contrat.pdf");
imprimerDocument("Facture.xlsx");

console.log("Nombre de documents en attente :", fileImpression.length);
// Nombre de documents en attente : 2
```

---

## 3️⃣ Implémentation Complète d'une File en JavaScript

### Version 1 : Implémentation Simple avec `push()` et `shift()`

```javascript
class File {
  constructor() {
    this.items = []; // Tableau pour stocker les éléments
  }

  // Ajouter un élément à l'arrière de la file
  enqueue(element) {
    this.items.push(element); // O(1) amortized
    console.log(`Enfilé : ${element}. File : [${this.items.join(", ")}]`);
  }

  // Retirer un élément de l'avant de la file
  dequeue() {
    if (this.isEmpty()) {
      console.log("La file est vide, impossible de défiler.");
      return null;
    }
    const elementRetire = this.items.shift(); // O(n) - inefficace !
    console.log(`Défilé : ${elementRetire}. File : [${this.items.join(", ")}]`);
    return elementRetire;
  }

  // Consulter le premier élément sans le retirer
  peek() {
    if (this.isEmpty()) {
      console.log("La file est vide, aucun élément à consulter.");
      return null;
    }
    const premierElement = this.items[0];
    console.log(`Consulté : ${premierElement}. Premier dans la file.`);
    return premierElement;
  }

  // Vérifier si la file est vide
  isEmpty() {
    const vide = this.items.length === 0;
    console.log(`La file est-elle vide ? ${vide}`);
    return vide;
  }

  // Obtenir la taille de la file
  size() {
    const taille = this.items.length;
    console.log(`Taille de la file : ${taille}`);
    return taille;
  }

  // Vider la file
  clear() {
    this.items = [];
    console.log("File vidée.");
  }

  // Afficher la file
  printFile() {
    console.log(`File actuelle : [${this.items.join(", ")}]`);
  }
}
```

### Démonstration Pratique

```javascript
console.log("=== DÉMONSTRATION DE LA FILE ===\n");

const maFile = new File();

// Test 1 : File vide
maFile.isEmpty(); // La file est-elle vide ? true

// Test 2 : Ajouter des éléments
maFile.enqueue(10); // Enfilé : 10. File : [10]
maFile.enqueue(20); // Enfilé : 20. File : [10, 20]
maFile.enqueue(30); // Enfilé : 30. File : [10, 20, 30]

maFile.printFile(); // File actuelle : [10, 20, 30]

// Test 3 : Consulter sans retirer
maFile.peek(); // Consulté : 10. Premier dans la file.

// Test 4 : Retirer des éléments (FIFO)
maFile.dequeue(); // Défilé : 10. File : [20, 30]
maFile.dequeue(); // Défilé : 20. File : [30]

// Test 5 : Ajouter encore
maFile.enqueue(40); // Enfilé : 40. File : [30, 40]
maFile.enqueue(50); // Enfilé : 50. File : [30, 40, 50]

maFile.size(); // Taille de la file : 3

// Test 6 : Vider la file
maFile.dequeue(); // Défilé : 30. File : [40, 50]
maFile.dequeue(); // Défilé : 40. File : [50]
maFile.dequeue(); // Défilé : 50. File : []

// Test 7 : Tenter de défiler une file vide
maFile.dequeue(); // La file est vide, impossible de défiler.

maFile.isEmpty(); // La file est-elle vide ? true
```

### Problème de Performance avec `shift()`

```javascript
// PROBLÈME : shift() a une complexité O(n)
// Chaque appel à shift() réindexe TOUS les éléments du tableau !

const grandeFille = new File();

// Ajouter 1000 éléments
for (let i = 0; i < 1000; i++) {
  grandeFille.enqueue(i);
}

// Retirer tous les éléments (très inefficace !)
console.time("Défilement de 1000 éléments avec shift()");
while (!grandeFille.isEmpty()) {
  grandeFille.dequeue(); // Chaque dequeue() est O(n) !
}
console.timeEnd("Défilement de 1000 éléments avec shift()");
// Résultat typique : ~15-30ms (dépend du système)

// Complexité totale : O(n) × n éléments = O(n²)
```

**Pourquoi `shift()` est lent ?**

```
Avant shift() :
Index:  0   1   2   3
       [A] [B] [C] [D]

Après shift() → retire A
Tous les éléments doivent être déplacés !
       [B] [C] [D]
        ↑   ↑   ↑
Index:  0   1   2

Coût : O(n) car il faut déplacer n-1 éléments
```

---

## 4️⃣ Implémentation Optimisée avec des Pointeurs

### Version 2 : File Optimisée avec `front` et `rear`

Au lieu de déplacer tous les éléments avec `shift()`, on utilise deux **pointeurs** :

- **`front`** : indice du premier élément
- **`rear`** : indice où ajouter le prochain élément

```javascript
class FileOptimisee {
  constructor() {
    this.items = {}; // Objet comme hash map (plus performant)
    this.front = 0; // Indice du premier élément
    this.rear = 0; // Indice du prochain ajout
  }

  // Ajouter un élément à l'arrière - O(1)
  enqueue(element) {
    this.items[this.rear] = element;
    this.rear++;
    console.log(`Enfilé : ${element}`);
  }

  // Retirer un élément de l'avant - O(1)
  dequeue() {
    if (this.isEmpty()) {
      console.log("La file est vide, impossible de défiler.");
      return null;
    }

    const elementRetire = this.items[this.front];
    delete this.items[this.front]; // Supprimer la propriété
    this.front++;
    console.log(`Défilé : ${elementRetire}`);
    return elementRetire;
  }

  // Consulter le premier élément - O(1)
  peek() {
    if (this.isEmpty()) {
      return "File vide";
    }
    return this.items[this.front];
  }

  // Vérifier si vide - O(1)
  isEmpty() {
    return this.rear === this.front;
  }

  // Obtenir la taille - O(1)
  size() {
    return this.rear - this.front;
  }

  // Afficher la file
  printFile() {
    let str = "";
    for (let i = this.front; i < this.rear; i++) {
      str += this.items[i] + " ";
    }
    console.log(`File : ${str.trim()}`);
  }
}
```

### Test de Performance

```javascript
console.log("\n=== COMPARAISON DE PERFORMANCE ===\n");

// Test avec la file optimisée
const fileRapide = new FileOptimisee();

console.time("Défilement de 10 000 éléments avec pointeurs");
for (let i = 0; i < 10000; i++) {
  fileRapide.enqueue(i);
}
while (!fileRapide.isEmpty()) {
  fileRapide.dequeue();
}
console.timeEnd("Défilement de 10 000 éléments avec pointeurs");
// Résultat typique : ~5-10ms

// Comparé à shift() : ~1500-3000ms pour 10 000 éléments
// Gain : 150× à 300× plus rapide !
```

### Comparaison des Deux Implémentations

| Critère              | Version `push()`/`shift()` | Version Pointeurs | Meilleure  |
| -------------------- | -------------------------- | ----------------- | ---------- |
| **enqueue()**        | O(1)                       | O(1)              | =          |
| **dequeue()**        | O(n)                       | O(1)              | Pointeurs  |
| **peek()**           | O(1)                       | O(1)              | =          |
| **isEmpty()**        | O(1)                       | O(1)              | =          |
| **size()**           | O(1)                       | O(1)              | =          |
| **Simplicité**       | Très simple                | Plus complexe     | push/shift |
| **Performance**      | O(n²) pour n dequeue       | O(n) pour n       | Pointeurs  |
| **Mémoire**          | Compact                    | Croissance        | push/shift |
| **Usage recommandé** | Petites files (<100)       | Grandes files     | -          |

**Recommandation** :

- **Petites files** (< 100 éléments) : Version simple avec `push()`/`shift()`
- **Grandes files** ou **usage intensif** : Version optimisée avec pointeurs

---

## 5️⃣ Pile vs File : Les Différences Clés

### Comparaison Visuelle

```
PILE (Stack) - LIFO                FILE (Queue) - FIFO
═══════════════════                ════════════════════

   push()  ↓                           enqueue() ↓
   ┌───────┐                           ┌──────────────┐
   │   D   │ ← Sommet (Top)            │ A  B  C  D   │
   ├───────┤                           └──┬───────────┘
   │   C   │                              ↑
   ├───────┤                           dequeue()
   │   B   │
   ├───────┤                        Ordre d'ajout : A→B→C→D
   │   A   │ ← Base                 Ordre de retrait : A→B→C→D
   └───────┘                         Premier arrivé = Premier sorti
      ↑
   pop()

Ordre d'ajout : A→B→C→D
Ordre de retrait : D→C→B→A
Dernier arrivé = Premier sorti
```

### Tableau Comparatif

| Aspect                  | Pile (Stack)          | File (Queue)                 |
| ----------------------- | --------------------- | ---------------------------- |
| **Principe**            | LIFO                  | FIFO                         |
| **Ajout**               | push() au sommet      | enqueue() à l'arrière        |
| **Retrait**             | pop() du sommet       | dequeue() de l'avant         |
| **Consultation**        | peek() au sommet      | peek() à l'avant             |
| **Métaphore**           | Pile d'assiettes      | File d'attente au cinéma     |
| **Applications**        | Annuler/Refaire       | Traitement des tâches        |
|                         | Historique navigateur | Gestion des requêtes serveur |
|                         | Appels de fonctions   | Files de messages            |
| **Complexité optimale** | Toutes O(1)           | enqueue O(1), dequeue O(1)\* |

\*avec implémentation optimisée

---

## 6️⃣ Applications Réelles des Files

### Application 1 : Ordonnancement des Processus

**Contexte** : Les systèmes d'exploitation utilisent des files pour gérer les processus en attente d'exécution.

```javascript
class GestionnaireProcessus {
  constructor() {
    this.fileAttente = new FileOptimisee();
    this.processusEnCours = null;
  }

  ajouterProcessus(nomProcessus, priorite = "normale") {
    const processus = {
      nom: nomProcessus,
      priorite: priorite,
      horodatage: new Date().toLocaleTimeString(),
    };
    this.fileAttente.enqueue(processus);
    console.log(`Processus ajouté : ${nomProcessus} (${priorite})`);
  }

  executerProchainProcessus() {
    if (this.fileAttente.isEmpty()) {
      console.log("Tous les processus ont été exécutés.");
      return null;
    }

    this.processusEnCours = this.fileAttente.dequeue();
    console.log(`Exécution : ${this.processusEnCours.nom}`);
    console.log(`   Créé à : ${this.processusEnCours.horodatage}`);
    return this.processusEnCours;
  }

  afficherFileAttente() {
    console.log(`${this.fileAttente.size()} processus en attente.`);
  }
}

// Utilisation
const os = new GestionnaireProcessus();

os.ajouterProcessus("Navigateur Chrome");
os.ajouterProcessus("Éditeur de texte");
os.ajouterProcessus("Lecteur de musique");
os.ajouterProcessus("Mise à jour système", "haute");

os.afficherFileAttente(); // 4 processus en attente.

// Le CPU exécute les processus dans l'ordre d'arrivée
os.executerProchainProcessus(); // Exécution : Navigateur Chrome
os.executerProchainProcessus(); // Exécution : Éditeur de texte
```

---

### Application 2 : Serveur Web et File de Requêtes

**Contexte** : Un serveur web reçoit plusieurs requêtes simultanées. Il les traite dans l'ordre d'arrivée.

```javascript
class ServeurWeb {
  constructor(capaciteMaximale = 100) {
    this.fileRequetes = new FileOptimisee();
    this.capaciteMax = capaciteMaximale;
    this.nombreRequetesTraitees = 0;
  }

  recevoirRequete(client, url) {
    if (this.fileRequetes.size() >= this.capaciteMax) {
      console.log(`Serveur surchargé ! Requête de ${client} rejetée.`);
      return false;
    }

    const requete = {
      client: client,
      url: url,
      timestamp: Date.now(),
    };

    this.fileRequetes.enqueue(requete);
    console.log(`Requête reçue : ${client} → ${url}`);
    return true;
  }

  traiterProchaineRequete() {
    if (this.fileRequetes.isEmpty()) {
      console.log("Aucune requête en attente.");
      return null;
    }

    const requete = this.fileRequetes.dequeue();
    const tempsAttente = Date.now() - requete.timestamp;

    console.log(`   Traitement : ${requete.url}`);
    console.log(`   Client : ${requete.client}`);
    console.log(`   Temps d'attente : ${tempsAttente}ms`);

    this.nombreRequetesTraitees++;
    return requete;
  }

  afficherStatistiques() {
    console.log("\n STATISTIQUES DU SERVEUR");
    console.log(`   Requêtes en attente : ${this.fileRequetes.size()}`);
    console.log(`   Requêtes traitées : ${this.nombreRequetesTraitees}`);
    console.log(
      `   Capacité restante : ${this.capaciteMax - this.fileRequetes.size()}`,
    );
  }
}

// Simulation
const serveur = new ServeurWeb(5);

// Arrivée de requêtes
serveur.recevoirRequete("Chermann", "/accueil");
serveur.recevoirRequete("Ingrid", "/produits");
serveur.recevoirRequete("Prudence", "/contact");

// Le serveur traite les requêtes dans l'ordre FIFO
serveur.traiterProchaineRequete(); // Traitement : /accueil (Chermann)
serveur.traiterProchaineRequete(); // Traitement : /produits (Ingrid)

// Nouvelles requêtes arrivent
serveur.recevoirRequete("Diana", "/panier");
serveur.recevoirRequete("Eve", "/commande");

serveur.afficherStatistiques();
//    STATISTIQUES DU SERVEUR
//    Requêtes en attente : 3
//    Requêtes traitées : 2
//    Capacité restante : 2
```

---

### Application 3 : File de Messages (Message Queue)

**Contexte** : Systèmes distribués où des services communiquent de manière asynchrone.

```javascript
class FileMessages {
  constructor(nomFile) {
    this.nom = nomFile;
    this.messages = new FileOptimisee();
    this.abonnes = [];
  }

  publier(message, expediteur) {
    const messageComplet = {
      contenu: message,
      expediteur: expediteur,
      timestamp: new Date().toISOString(),
      id: Math.random().toString(36).substr(2, 9),
    };

    this.messages.enqueue(messageComplet);
    console.log(`   Message publié par ${expediteur} dans "${this.nom}"`);
    console.log(`   Contenu : ${message}`);
  }

  consommer() {
    if (this.messages.isEmpty()) {
      console.log("Aucun message à consommer.");
      return null;
    }

    const message = this.messages.dequeue();
    console.log(`   Message consommé :`);
    console.log(`   De : ${message.expediteur}`);
    console.log(`   Contenu : ${message.contenu}`);
    console.log(`   ID : ${message.id}`);
    return message;
  }

  afficherNombreMessages() {
    console.log(
      `${this.messages.size()} message(s) en attente dans "${this.nom}"`,
    );
  }
}

// Exemple : File de messages pour traitement d'images
const fileTraitementImages = new FileMessages("traitement-images");

// Un utilisateur upload 3 images
fileTraitementImages.publier("Redimensionner photo1.jpg", "User123");
fileTraitementImages.publier("Appliquer filtre photo2.jpg", "User456");
fileTraitementImages.publier("Convertir photo3.png", "User789");

fileTraitementImages.afficherNombreMessages();
// 3 message(s) en attente dans "traitement-images"

// Un worker consomme les messages dans l'ordre FIFO
fileTraitementImages.consommer(); // Redimensionner photo1.jpg
fileTraitementImages.consommer(); // Appliquer filtre photo2.jpg

fileTraitementImages.afficherNombreMessages();
// 1 message(s) en attente dans "traitement-images"
```

---

## 📝 Micro-Exercice #1 : Comprendre le Principe FIFO

**Question** : Soit une file initialement vide. On effectue les opérations suivantes :

```javascript
file.enqueue("A");
file.enqueue("B");
file.dequeue();
file.enqueue("C");
file.enqueue("D");
file.dequeue();
```

Quel est le contenu final de la file, du front au rear ?

<details>
<summary>💡 Cliquez pour voir la réponse</summary>

**Réponse** : `["C", "D"]`

**Trace d'exécution** :

```
1. enqueue("A")     → File : [A]
2. enqueue("B")     → File : [A, B]
3. dequeue()        → Retire A → File : [B]
4. enqueue("C")     → File : [B, C]
5. enqueue("D")     → File : [B, C, D]
6. dequeue()        → Retire B → File : [C, D]
```

**État final** :

```
File : [C, D]
       ↑     ↑
     Front  Rear
```

**Principe FIFO** :

- A ajouté en premier → retiré en premier (étape 3)
- B ajouté en deuxième → retiré en deuxième (étape 6)
- C et D restent dans l'ordre d'ajout

</details>

---

## 📝 Micro-Exercice #2 : Identifier Pile vs File

**Question** : Pour chacun des scénarios suivants, indiquez s'il est plus approprié d'utiliser une **Pile (Stack)** ou une **File (Queue)** :

1. Traitement des documents envoyés à une imprimante
2. Fonction "Annuler" dans un éditeur de texte
3. Gestion des appels dans un centre de support technique
4. Navigation arrière/avant dans un navigateur web
5. Traitement des requêtes par un serveur web
6. Évaluation d'une expression mathématique avec parenthèses

<details>
<summary>💡 Cliquez pour voir la réponse</summary>

| Scénario                    | Structure | Justification                                                         |
| --------------------------- | --------- | --------------------------------------------------------------------- |
| 1. Documents à l'imprimante | **File**  | Premier document envoyé = premier imprimé (FIFO)                      |
| 2. Fonction "Annuler"       | **Pile**  | Annuler la dernière action effectuée (LIFO)                           |
| 3. Appels centre de support | **File**  | Premier appelant = premier servi (FIFO)                               |
| 4. Navigation navigateur    | **Pile**  | Page précédente = dernière visitée (LIFO)                             |
| 5. Requêtes serveur web     | **File**  | Première requête reçue = première traitée (FIFO)                      |
| 6. Expression mathématique  | **Pile**  | Parenthèses internes traitées en dernier ouvert, premier fermé (LIFO) |

**Règle générale** :

- **FIFO (File)** : Quand l'ordre d'arrivée détermine l'ordre de traitement (équité, traitement séquentiel)
- **LIFO (Pile)** : Quand il faut revenir en arrière ou traiter l'élément le plus récent en premier

</details>

---

## 🧮 Exercices Pratiques

### Exercice 1 : Simulation d'une File d'Attente de Documents

**Contexte** : Vous devez simuler une file d'impression dans un bureau.

**Mission** : En utilisant la classe `File` (première implémentation avec `push()`/`shift()`), créez un programme qui :

1. Crée une nouvelle instance de File
2. Enfile trois documents : "Rapport.docx", "Présentation.pptx", "Image.jpg"
3. Affiche l'état de la file
4. Défile le premier document et affiche son nom
5. Enfile un nouveau document : "Contrat.pdf"
6. Consulte (peek) le prochain document à imprimer sans le retirer
7. Affiche l'état final de la file et sa taille

<details>
<summary>💡 voir la solution</summary>

```javascript
// Utilisation de la classe File définie précédemment
const fileImpression = new File();

console.log("=== SIMULATION FILE D'IMPRESSION ===\n");

// Étape 1 : Vérifier si la file est vide
fileImpression.isEmpty(); // La file est-elle vide ? true

// Étape 2 : Ajouter trois documents
fileImpression.enqueue("Rapport.docx");
// Enfilé : Rapport.docx. File : [Rapport.docx]

fileImpression.enqueue("Présentation.pptx");
// Enfilé : Présentation.pptx. File : [Rapport.docx, Présentation.pptx]

fileImpression.enqueue("Image.jpg");
// Enfilé : Image.jpg. File : [Rapport.docx, Présentation.pptx, Image.jpg]

// Étape 3 : Afficher l'état actuel
fileImpression.printFile();
// File actuelle : [Rapport.docx, Présentation.pptx, Image.jpg]

// Étape 4 : Imprimer le premier document (dequeue)
const premierDoc = fileImpression.dequeue();
// Défilé : Rapport.docx. File : [Présentation.pptx, Image.jpg]
console.log(`\nDocument imprimé : ${premierDoc}\n`);

// Étape 5 : Ajouter un nouveau document
fileImpression.enqueue("Contrat.pdf");
// Enfilé : Contrat.pdf. File : [Présentation.pptx, Image.jpg, Contrat.pdf]

// Étape 6 : Consulter le prochain document sans le retirer
const prochainDoc = fileImpression.peek();
// Consulté : Présentation.pptx. Premier dans la file.
console.log(`\nProchain document à imprimer : ${prochainDoc}\n`);

// Étape 7 : Afficher l'état final
fileImpression.printFile();
// File actuelle : [Présentation.pptx, Image.jpg, Contrat.pdf]

const taille = fileImpression.size();
// Taille de la file : 3
console.log(`\nNombre total de documents en attente : ${taille}`);
```

**Sortie attendue** :

```
=== SIMULATION FILE D'IMPRESSION ===

La file est-elle vide ? true
Enfilé : Rapport.docx. File : [Rapport.docx]
Enfilé : Présentation.pptx. File : [Rapport.docx, Présentation.pptx]
Enfilé : Image.jpg. File : [Rapport.docx, Présentation.pptx, Image.jpg]
File actuelle : [Rapport.docx, Présentation.pptx, Image.jpg]
Défilé : Rapport.docx. File : [Présentation.pptx, Image.jpg]

Document imprimé : Rapport.docx

Enfilé : Contrat.pdf. File : [Présentation.pptx, Image.jpg, Contrat.pdf]
Consulté : Présentation.pptx. Premier dans la file.

Prochain document à imprimer : Présentation.pptx

File actuelle : [Présentation.pptx, Image.jpg, Contrat.pdf]
Taille de la file : 3

Nombre total de documents en attente : 3
```

**Concepts démontrés** :

- Principe FIFO : "Rapport.docx" ajouté en premier, retiré en premier
- `enqueue()` ajoute toujours à la fin
- `dequeue()` retire toujours du début
- `peek()` consulte sans modifier la file

</details>

---

### Exercice 2 : Priorisation de Tâches

**Contexte** : Vous développez un système de traitement de tâches simple.

**Mission** : En utilisant la classe `FileOptimisee`, créez un gestionnaire de tâches qui :

1. Initialise une file optimisée
2. Enfile 4 tâches représentées par des chaînes de caractères :
   - "Sauvegarde base de données"
   - "Requête utilisateur A"
   - "Vérification santé système"
   - "Requête utilisateur B"
3. Simule le traitement des deux premières tâches (dequeue)
4. Enfile une nouvelle tâche prioritaire : "Mise à jour sécurité critique"
5. Affiche la tâche suivante avec `peek()` sans la retirer
6. Défile toutes les tâches restantes et affiche la file après chaque retrait
7. Vérifie que la file est vide

<details>
<summary>💡 voir la solution</summary>

```javascript
console.log("=== GESTIONNAIRE DE TÂCHES ===\n");

// Étape 1 : Initialiser la file
const gestionnaireTaches = new FileOptimisee();

// Étape 2 : Ajouter 4 tâches
console.log("Ajout des tâches initiales :\n");

gestionnaireTaches.enqueue("Sauvegarde base de données");
// Enfilé : Sauvegarde base de données

gestionnaireTaches.enqueue("Requête utilisateur A");
// Enfilé : Requête utilisateur A

gestionnaireTaches.enqueue("Vérification santé système");
// Enfilé : Vérification santé système

gestionnaireTaches.enqueue("Requête utilisateur B");
// Enfilé : Requête utilisateur B

gestionnaireTaches.printFile();
// File : Sauvegarde base de données Requête utilisateur A Vérification santé système Requête utilisateur B

console.log(`Nombre de tâches : ${gestionnaireTaches.size()}\n`);
// Nombre de tâches : 4

// Étape 3 : Traiter les deux premières tâches
console.log("Traitement des deux premières tâches :\n");

const tache1 = gestionnaireTaches.dequeue();
console.log(`   Tâche traitée : ${tache1}`);

const tache2 = gestionnaireTaches.dequeue();
console.log(`   Tâche traitée : ${tache2}\n`);

gestionnaireTaches.printFile();
// File : Vérification santé système Requête utilisateur B

// Étape 4 : Ajouter une nouvelle tâche prioritaire
console.log("\nNouvelle tâche critique ajoutée :\n");
gestionnaireTaches.enqueue("Mise à jour sécurité critique");
// Enfilé : Mise à jour sécurité critique

gestionnaireTaches.printFile();
// File : Vérification santé système Requête utilisateur B Mise à jour sécurité critique

// Étape 5 : Consulter la prochaine tâche sans la retirer
console.log("\nProchaine tâche à traiter :");
const prochaineTache = gestionnaireTaches.peek();
console.log(`   ${prochaineTache}\n`);
// Vérification santé système

// Étape 6 : Traiter toutes les tâches restantes
console.log("Traitement de toutes les tâches restantes :\n");

while (!gestionnaireTaches.isEmpty()) {
  const tache = gestionnaireTaches.dequeue();
  console.log(`   Tâche traitée : ${tache}`);
  gestionnaireTaches.printFile();
}

// Étape 7 : Vérifier que la file est vide
console.log("\nVérification finale :");
console.log(`   File vide ? ${gestionnaireTaches.isEmpty()}`);
// File vide ? true

console.log(`   Nombre de tâches restantes : ${gestionnaireTaches.size()}`);
// Nombre de tâches restantes : 0
```

**Sortie complète** :

```
=== GESTIONNAIRE DE TÂCHES ===

Ajout des tâches initiales :

Enfilé : Sauvegarde base de données
Enfilé : Requête utilisateur A
Enfilé : Vérification santé système
Enfilé : Requête utilisateur B
File : Sauvegarde base de données Requête utilisateur A Vérification santé système Requête utilisateur B
Nombre de tâches : 4

Traitement des deux premières tâches :

Défilé : Sauvegarde base de données
   Tâche traitée : Sauvegarde base de données
Défilé : Requête utilisateur A
   Tâche traitée : Requête utilisateur A

File : Vérification santé système Requête utilisateur B

Nouvelle tâche critique ajoutée :

Enfilé : Mise à jour sécurité critique
File : Vérification santé système Requête utilisateur B Mise à jour sécurité critique

Prochaine tâche à traiter :
   Vérification santé système

Traitement de toutes les tâches restantes :

Défilé : Vérification santé système
   Tâche traitée : Vérification santé système
File : Requête utilisateur B Mise à jour sécurité critique
Défilé : Requête utilisateur B
   Tâche traitée : Requête utilisateur B
File : Mise à jour sécurité critique
Défilé : Mise à jour sécurité critique
   Tâche traitée : Mise à jour sécurité critique
File :

Vérification finale :
   File vide ? true
   Nombre de tâches restantes : 0
```

**Observations importantes** :

1. **FIFO strict** : Les tâches sont toujours traitées dans l'ordre d'arrivée
2. **Performance O(1)** : Avec `FileOptimisee`, toutes les opérations sont rapides
3. **Limite du FIFO** : La tâche "Mise à jour sécurité critique" ajoutée en dernier est traitée en dernier, même si elle est critique !

**Note** : Pour gérer les priorités réelles, il faudrait utiliser une **file de priorité (priority queue)** qui sera vue dans un module ultérieur.

</details>

---

### Exercice 3 : Gestion des Erreurs dans les Opérations de File

**Contexte** : Améliorer la robustesse de la gestion des files.

**Mission** : Modifiez la méthode `dequeue()` et `peek()` de l'une des classes (`File` ou `FileOptimisee`) pour :

1. `dequeue()` : Retourner un message d'erreur personnalisé `"Erreur : La file est vide."` au lieu de `null` quand on tente de défiler une file vide
2. `peek()` : Retourner `"Erreur : La file est vide."` au lieu de `null` quand on tente de consulter une file vide
3. Tester vos modifications en :
   - Créant une file vide
   - Tentant de faire `dequeue()` sur cette file vide
   - Tentant de faire `peek()` sur cette file vide
   - Ajoutant un élément
   - Faisant `dequeue()` normalement
   - Tentant à nouveau `dequeue()` et `peek()` sur la file vide

<details>
<summary>💡 voir la solution</summary>

```javascript
// Classe File modifiée avec gestion d'erreurs améliorée
class FileAvecGestionErreurs {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
    console.log(`Enfilé : ${element}`);
  }

  // Méthode modifiée avec message d'erreur personnalisé
  dequeue() {
    if (this.isEmpty()) {
      const messageErreur = "Erreur : La file est vide.";
      console.log(`${messageErreur}`);
      return messageErreur; // Retourne le message au lieu de null
    }

    const elementRetire = this.items.shift();
    console.log(`Défilé : ${elementRetire}`);
    return elementRetire;
  }

  // Méthode modifiée avec message d'erreur personnalisé
  peek() {
    if (this.isEmpty()) {
      const messageErreur = "Erreur : La file est vide.";
      console.log(`${messageErreur}`);
      return messageErreur; // Retourne le message au lieu de null
    }

    const premierElement = this.items[0];
    console.log(`Consulté : ${premierElement}`);
    return premierElement;
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  printFile() {
    if (this.isEmpty()) {
      console.log("File actuelle : [vide]");
    } else {
      console.log(`File actuelle : [${this.items.join(", ")}]`);
    }
  }
}

// === TESTS DE LA GESTION D'ERREURS ===

console.log("=== TEST DE GESTION DES ERREURS ===\n");

const maFile = new FileAvecGestionErreurs();

// Test 1 : Tenter dequeue sur file vide
console.log("Test 1 : dequeue() sur file vide");
const resultat1 = maFile.dequeue();
console.log(`Valeur retournée : "${resultat1}"`);
console.log(`Type : ${typeof resultat1}\n`);
// Erreur : La file est vide.
// Valeur retournée : "Erreur : La file est vide."
// Type : string

// Test 2 : Tenter peek sur file vide
console.log("Test 2 : peek() sur file vide");
const resultat2 = maFile.peek();
console.log(`Valeur retournée : "${resultat2}"`);
console.log(`Type : ${typeof resultat2}\n`);
// Erreur : La file est vide.
// Valeur retournée : "Erreur : La file est vide."
// Type : string

// Test 3 : Ajouter un élément
console.log("Test 3 : Ajouter un élément");
maFile.enqueue("Tâche importante");
maFile.printFile();
console.log();
// Enfilé : Tâche importante
// File actuelle : [Tâche importante]

// Test 4 : dequeue normal
console.log("Test 4 : dequeue() normal");
const resultat3 = maFile.dequeue();
console.log(`Valeur retournée : "${resultat3}"`);
maFile.printFile();
console.log();
// Défilé : Tâche importante
// Valeur retournée : "Tâche importante"
// File actuelle : [vide]

// Test 5 : Nouveau test sur file vide
console.log("Test 5 : dequeue() et peek() après vidage");
const resultat4 = maFile.dequeue();
const resultat5 = maFile.peek();
console.log(`dequeue() retourne : "${resultat4}"`);
console.log(`peek() retourne : "${resultat5}"`);
// Erreur : La file est vide.
// Erreur : La file est vide.
// dequeue() retourne : "Erreur : La file est vide."
// peek() retourne : "Erreur : La file est vide."

// === Utilisation pratique de la gestion d'erreurs ===

console.log("\n\n=== UTILISATION PRATIQUE ===\n");

const fileTraitement = new FileAvecGestionErreurs();

// Fonction qui traite en toute sécurité
function traiterProchaineFile(file) {
  const element = file.dequeue();

  if (element.startsWith("Erreur :")) {
    console.log("Impossible de traiter : file vide.\n");
    return false;
  }

  console.log(`Élément traité avec succès : ${element}\n`);
  return true;
}

// Ajouter des éléments
fileTraitement.enqueue("Document 1");
fileTraitement.enqueue("Document 2");

// Traiter tous les éléments + tenter un de trop
traiterProchaineFile(fileTraitement); // Document 1
traiterProchaineFile(fileTraitement); // Document 2
traiterProchaineFile(fileTraitement); // Impossible de traiter : file vide
```

**Avantages de cette approche** :

1. **Messages clairs** : Plus facile à déboguer
2. **Pas de valeurs `null` ambiguës** : On sait exactement ce qui s'est passé
3. **Vérification simple** : On peut tester si la chaîne commence par "Erreur :"
4. **Code défensif** : Évite les crashes quand on tente d'opérer sur une file vide

**Alternative avec exceptions** (approche plus avancée) :

```javascript
class FileAvecExceptions {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    if (this.isEmpty()) {
      throw new Error("Impossible de défiler : la file est vide.");
    }
    return this.items.shift();
  }

  peek() {
    if (this.isEmpty()) {
      throw new Error("Impossible de consulter : la file est vide.");
    }
    return this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}

// Utilisation avec try-catch
const fileSafe = new FileAvecExceptions();

try {
  fileSafe.dequeue(); // Lève une exception
} catch (error) {
  console.error(`Erreur capturée : ${error.message}`);
  // Erreur capturée : Impossible de défiler : la file est vide.
}
```

</details>

---

## ❓ Quiz de Validation des Connaissances

### Question 1 : Comprendre FIFO

Soit une file initialement vide. On effectue la séquence suivante :

```javascript
enqueue(5);
enqueue(10);
dequeue();
enqueue(15);
peek();
dequeue();
```

Quel élément est retourné par le dernier `dequeue()` ?

- [ ] A) 5
- [ ] B) 10
- [ ] C) 15
- [ ] D) null

<details>
<summary>Voir la réponse</summary>

**Réponse : B) 10**

**Explication détaillée** :

```
État initial : File = []

1. enqueue(5)    → File = [5]
2. enqueue(10)   → File = [5, 10]
3. dequeue()     → Retire 5 → File = [10]
4. enqueue(15)   → File = [10, 15]
5. peek()        → Consulte 10 (sans retirer) → File = [10, 15]
6. dequeue()     → Retire 10 → File = [15]
                    ↑
                 Retourne 10 ✅
```

**Principe FIFO appliqué** :

- Étape 3 : 5 est retiré en premier car il a été ajouté en premier
- Étape 6 : 10 est retiré car il est maintenant le premier dans la file
- 15 reste dans la file car il a été ajouté en dernier

</details>

---

### Question 2 : Complexité Temporelle

Dans l'implémentation simple d'une file utilisant `push()` et `shift()`, quelle est la complexité temporelle de l'opération `dequeue()` sur un tableau de taille n ?

- [ ] A) O(1)
- [ ] B) O(log n)
- [ ] C) O(n)
- [ ] D) O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : C) O(n)**

**Explication** :

La méthode `shift()` en JavaScript a une complexité **O(n)** car elle doit :

1. Retirer le premier élément à l'index 0
2. **Déplacer tous les éléments restants** d'un cran vers la gauche
3. Mettre à jour les indices de tous les éléments

**Visualisation** :

```
Avant shift() sur [10, 20, 30, 40, 50] :
Index :  0   1   2   3   4
        [10][20][30][40][50]

Après shift() → retire 10 :
TOUS les éléments doivent être déplacés !

        [20][30][40][50]
         ↑   ↑   ↑   ↑
Index :  0   1   2   3

Opérations :
- items[1] → items[0]  (20 déplacé)
- items[2] → items[1]  (30 déplacé)
- items[3] → items[2]  (40 déplacé)
- items[4] → items[3]  (50 déplacé)

Total : n-1 déplacements = O(n)
```

**Pourquoi c'est un problème ?**

Si vous effectuez `dequeue()` n fois de suite :

```
Complexité totale = n × O(n) = O(n²)
```

**Solution** : Utiliser l'implémentation optimisée avec pointeurs `front` et `rear` pour obtenir O(1) !

</details>

---

### Question 3 : File vs Pile

Parmi les applications suivantes, laquelle utilise typiquement une **file** et non une **pile** ?

- [ ] A) Fonction "Annuler" (Undo) dans un éditeur de texte
- [ ] B) Gestion des processus en attente dans un système d'exploitation
- [ ] C) Historique de navigation d'un navigateur web
- [ ] D) Appels de fonctions récursives

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Gestion des processus en attente dans un système d'exploitation**

**Explication** :

| Application                  | Structure | Principe                                                    |
| ---------------------------- | --------- | ----------------------------------------------------------- |
| **A) Fonction Annuler**      | **Pile**  | Annuler la dernière action = LIFO                           |
| **B) Processus OS**          | **File**  | Premier processus arrivé = premier exécuté = **FIFO**       |
| **C) Historique navigateur** | **Pile**  | Retour à la page précédente = dernière visitée = LIFO       |
| **D) Appels récursifs**      | **Pile**  | Call stack : dernière fonction appelée = première retournée |

**Pourquoi les processus utilisent une file ?**

```
CPU Scheduler (Ordonnanceur)
============================

File de processus prêts :
┌─────────────────────────────┐
│ [P1][P2][P3][P4][P5]        │
│  ↑                    ↑     │
│ Front              Rear     │
└─────────────────────────────┘

Le CPU prend P1 (premier arrivé) pour l'exécuter.
C'est équitable : chaque processus attend son tour dans l'ordre d'arrivée.

Si on utilisait une PILE :
- P5 serait exécuté en premier (dernier arrivé)
- P1 attendrait indéfiniment ← PROBLÈME (starvation) !
```

**Équité FIFO** : Garantit qu'aucun processus n'attend indéfiniment.

</details>

---

### Question 4 : Implémentation Optimisée

Dans l'implémentation optimisée d'une file utilisant des pointeurs `front` et `rear`, qu'arrive-t-il à la mémoire lorsque de nombreux éléments sont ajoutés puis retirés ?

- [ ] A) La mémoire est automatiquement libérée après chaque `dequeue()`
- [ ] B) La structure interne continue de croître même si la file logique est vide
- [ ] C) La mémoire est compactée automatiquement tous les 100 éléments
- [ ] D) Aucun problème de mémoire ne peut survenir avec cette implémentation

<details>
<summary>Voir la réponse</summary>

**Réponse : B) La structure interne continue de croître même si la file logique est vide**

**Explication** :

Avec l'implémentation utilisant des pointeurs :

```javascript
class FileOptimisee {
  constructor() {
    this.items = {}; // Objet comme hash map
    this.front = 0; // Pointeur vers le front
    this.rear = 0; // Pointeur vers le rear
  }

  enqueue(element) {
    this.items[this.rear] = element;
    this.rear++; // Rear continue d'augmenter
  }

  dequeue() {
    const element = this.items[this.front];
    delete this.items[this.front]; // Supprime la propriété
    this.front++; // Front continue d'augmenter
    return element;
  }
}
```

**Problème de croissance mémoire** :

```
Scénario : Ajouter 1000 éléments, puis tous les retirer

Après 1000 enqueue() :
items = { 0: val, 1: val, ..., 999: val }
front = 0
rear = 1000

Après 1000 dequeue() :
items = {}  ← Objet vide MAIS...
front = 1000  ← Front a augmenté !
rear = 1000   ← Rear aussi !

Prochain enqueue() :
items = { 1000: val }  ← Commence à 1000, pas à 0 !
rear = 1001

Résultat : Les indices continuent de croître indéfiniment !
```

**Conséquences** :

1. **Croissance des indices** : `front` et `rear` peuvent devenir très grands
2. **Fragmentation mémoire** : L'objet `items` peut avoir des "trous" (indices supprimés)
3. **Pas de recyclage** : Les anciens indices ne sont jamais réutilisés

**Solutions possibles** :

```javascript
// Solution 1 : Reset périodique quand la file est vide
dequeue() {
  if (this.isEmpty()) {
    return null;
  }

  const element = this.items[this.front];
  delete this.items[this.front];
  this.front++;

  // Si la file devient vide, reset les pointeurs
  if (this.front === this.rear) {
    this.front = 0;
    this.rear = 0;
  }

  return element;
}

// Solution 2 : Reconstruction périodique
reconstructIfNeeded() {
  const THRESHOLD = 1000;

  if (this.front > THRESHOLD) {
    const newItems = {};
    let index = 0;

    for (let i = this.front; i < this.rear; i++) {
      newItems[index++] = this.items[i];
    }

    this.items = newItems;
    this.rear = this.rear - this.front;
    this.front = 0;
  }
}
```

**Comparaison avec push/shift** :

| Aspect                 | push/shift           | Pointeurs front/rear     |
| ---------------------- | -------------------- | ------------------------ |
| **Complexité dequeue** | O(n)                 | O(1)                     |
| **Mémoire**            | Compact              | Peut croître             |
| **Gestion**            | Automatique          | Nécessite reset manuel   |
| **Meilleur usage**     | Petites files (<100) | Grandes files avec reset |

**Conclusion** : L'implémentation avec pointeurs est plus rapide mais nécessite une gestion de la mémoire plus attentive, surtout pour des applications longue durée.

</details>

---

### Question 5 : Application Pratique

Un serveur web reçoit les requêtes suivantes dans cet ordre :

1. GET /home (Client A)
2. POST /api/data (Client B)
3. GET /about (Client C)
4. GET /contact (Client A)

Si le serveur traite les requêtes avec une file FIFO, dans quel ordre seront-elles exécutées ?

- [ ] A) A → B → C → A
- [ ] B) A → A → B → C
- [ ] C) C → B → A → A
- [ ] D) B → A → C → A

<details>
<summary>Voir la réponse</summary>

**Réponse : A) A → B → C → A**

**Explication** :

Une file respecte le principe **FIFO (First-In, First-Out)** : les requêtes sont traitées **dans l'ordre d'arrivée**, indépendamment du client.

**Trace d'exécution** :

```
File de requêtes du serveur
============================

État initial : File = []

1️ Arrivée : GET /home (Client A)
   File = [A: /home]

2️ Arrivée : POST /api/data (Client B)
   File = [A: /home, B: /api/data]

3️ Arrivée : GET /about (Client C)
   File = [A: /home, B: /api/data, C: /about]

4️ Arrivée : GET /contact (Client A)
   File = [A: /home, B: /api/data, C: /about, A: /contact]
              ↑                                       ↑
            Front                                   Rear

Traitement (dequeue dans l'ordre) :
====================================

1. Traite A: /home       → File = [B, C, A]
2. Traite B: /api/data   → File = [C, A]
3. Traite C: /about      → File = [A]
4. Traite A: /contact    → File = []

Ordre final : A → B → C → A
```

**Propriétés importantes** :

1. **Équité** : Chaque requête est traitée dans son ordre d'arrivée
2. **Pas de priorité** : Le Client A n'est pas traité en premier juste parce qu'il a fait deux requêtes
3. **Prédictibilité** : L'ordre est garanti et immuable

**Pourquoi pas les autres options ?**

- **B) A → A → B → C** : Impliquerait que toutes les requêtes de A sont groupées (violation de FIFO)
- **C) C → B → A → A** : Ordre inverse (serait LIFO, comme une pile)
- **D) B → A → C → A** : Ordre arbitraire (pas de structure de données cohérente)

**Code JavaScript simulant ce comportement** :

```javascript
class ServeurWeb {
  constructor() {
    this.fileRequetes = new FileOptimisee();
  }

  recevoirRequete(client, url, methode) {
    const requete = { client, url, methode };
    this.fileRequetes.enqueue(requete);
    console.log(`Requête reçue : ${methode} ${url} (${client})`);
  }

  traiterProchaineRequete() {
    if (this.fileRequetes.isEmpty()) {
      console.log("💤 Aucune requête en attente.");
      return null;
    }

    const requete = this.fileRequetes.dequeue();
    console.log(
      `Traitement : ${requete.methode} ${requete.url} (${requete.client})`,
    );
    return requete;
  }
}

// Simulation
const serveur = new ServeurWeb();

serveur.recevoirRequete("Client A", "/home", "GET");
serveur.recevoirRequete("Client B", "/api/data", "POST");
serveur.recevoirRequete("Client C", "/about", "GET");
serveur.recevoirRequete("Client A", "/contact", "GET");

console.log("\nTraitement des requêtes :\n");

serveur.traiterProchaineRequete(); // Client A : GET /home
serveur.traiterProchaineRequete(); // Client B : POST /api/data
serveur.traiterProchaineRequete(); // Client C : GET /about
serveur.traiterProchaineRequete(); // Client A : GET /contact
```

**Avantages du FIFO pour un serveur** :

- **Équité** : Aucun client n'est favorisé
- **Prédictibilité** : Les clients savent que leur requête sera traitée dans l'ordre
- **Simplicité** : Pas de logique de priorité complexe
- **Limitation** : Les requêtes urgentes ne peuvent pas passer devant (nécessiterait une file de priorité)

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Principe FIFO

**First-In, First-Out** : le premier élément ajouté est le premier retiré. Comme une file d'attente au cinéma, le premier arrivé est le premier servi.

### 2. Opérations Fondamentales

`enqueue()` ajoute à l'arrière (O(1)), `dequeue()` retire de l'avant (O(n) avec shift, O(1) optimisé), `peek()` consulte sans retirer (O(1)), `isEmpty()`, `size()` et `clear()` en O(1).

### 3. Implémentation Simple

Utilise `push()` et `shift()` natifs de JavaScript. Simple à comprendre mais `shift()` est **O(n)** car il décale tous les éléments. Adapté pour les petites files (< 100 éléments).

### 4. Implémentation Optimisée

Utilise des pointeurs `front` et `rear` avec un objet. Toutes les opérations en **O(1)** mais nécessite une gestion de la mémoire. Idéal pour les grandes files ou l'usage intensif.

### 5. File vs Pile

**File (FIFO)** : ajout à l'arrière, retrait à l'avant (file d'attente). **Pile (LIFO)** : ajout et retrait au sommet (pile d'assiettes). Choisir selon l'ordre de traitement souhaité.

### 6. Applications Réelles

Ordonnancement de **processus OS**, gestion des **requêtes serveur web**, **files de messages** dans les systèmes distribués, **traitement asynchrone** des tâches.

### 7. Critères de Choix

Petites files (< 100) : `push()`/`shift()` pour la simplicité. Grandes files ou usage intensif : pointeurs pour la performance. En production : utiliser des bibliothèques spécialisées.

---

## ➡️ Prochaine Étape : Leçon 12

### Ce qui vous attend

Dans la prochaine leçon, **« Pratique : Utiliser Piles/Files pour la Priorisation des Tâches »**, vous allez mettre en pratique tout ce que vous avez appris sur les piles et les files dans un projet concret.

**Vous découvrirez :**

- Comment combiner piles et files dans une application complète
- L'implémentation d'un système de gestion de tâches avec historique
- L'utilisation des files pour le traitement séquentiel des tâches
- ↩L'utilisation des piles pour la fonctionnalité Undo/Redo

### Préparez-vous !

Assurez-vous de bien maîtriser les opérations de base des piles (`push`, `pop`) et des files (`enqueue`, `dequeue`). Cette leçon pratique vous montrera comment ces structures simples peuvent créer des applications puissantes.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Queue Data Structure Visualization](https://www.youtube.com/results?search_query=queue+data+structure+visualization) - Visualisation animée
- [MDN : Array Methods (push, shift)](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array) - Documentation officielle
- [Visualgo - Visualisation des Files](https://visualgo.net/en/list) - Outil interactif

### Outils utiles

- **[Stack vs Queue - Comparaison](https://www.youtube.com/results?search_query=stack+vs+queue)** : Vidéos comparatives
- **[Wikipedia : File (structure de données)](<https://fr.wikipedia.org/wiki/File_(structure_de_donn%C3%A9es)>)** : Référence théorique

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices
- Comparer les performances entre `push/shift` et l'implémentation avec pointeurs

> 💡 **Conseil**
>
> Pensez à des exemples concrets de files dans la vie réelle : la file d'attente à la caisse, les impressions en attente, les messages dans une messagerie. Chaque fois que l'ordre d'arrivée détermine l'ordre de traitement, vous avez une file FIFO !

---

**Prêt pour la Leçon 12 ?** 🚀

Rendez-vous dans la prochaine leçon pour mettre en pratique les piles et les files !

---

<div align="center">

**Leçon 11 sur 42 - Module 2 : Structures de Données Essentielles en JavaScript**

[⬅️ Leçon 10 : Piles - Principe LIFO et Implémentation Basée sur Tableaux](./lecon-4-piles-principe-lifo-implementation-tableaux.md) | [Retour au sommaire](./README.md) | [Leçon 12 : Pratique - Utiliser Piles/Files pour la Priorisation des Tâches ➡️](./lecon-6-pratique-utiliser-piles-files-priorisation-taches-etude-cas.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
