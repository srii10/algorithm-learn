# 📘 Leçon 6 : Mise en Place d'une Étude de Cas - Optimisation d'un Gestionnaire de Tâches

**Module 1** : Fondements des algorithmes et révision de JavaScript

---

## 🎯 Objectifs d'Apprentissage

À la fin de cette leçon, vous serez capable de :

- Comprendre l'importance d'une étude de cas pratique en algorithmique
- Identifier les goulots d'étranglement de performance dans une application réelle
- Analyser la complexité d'opérations courantes (ajout, recherche, mise à jour)
- Mettre en place une architecture de code pour tester des optimisations
- Prévoir les problèmes de performance avant qu'ils ne surviennent

---

### ⏱️ Durée estimée : 2h30 - 3h

---

## 📚 Prérequis

Avant de commencer cette leçon, assurez-vous de maîtriser :

- La notation Big O (Leçon 4)
- L'analyse des opérations JavaScript (Leçon 5)
- Les tableaux et objets JavaScript
- Les bases du DOM JavaScript

---

## 🚀 Introduction

Dans les leçons précédentes, vous avez appris la **théorie** de l'analyse algorithmique. Maintenant, il est temps de passer à la **pratique** !

### Pourquoi une Étude de Cas ?

Apprendre les algorithmes uniquement en théorie, c'est comme apprendre à conduire sans jamais monter dans une voiture. Une étude de cas vous permet de :

1. **Voir l'impact réel** des algorithmes sur la performance
2. **Expérimenter** avec différentes solutions
3. **Mesurer** les améliorations concrètes
4. **Comprendre** quand et pourquoi optimiser

### Notre Projet : Un Gestionnaire de Tâches

Nous allons construire et optimiser un **gestionnaire de tâches** (task manager) - une fonctionnalité omniprésente dans les applications web modernes.

**Exemples réels :**

- Trello, Asana, Todoist : Gestion de projets
- Jira : Suivi de tickets pour les développeurs
- Système de tickets de support client
- Planificateur de livraisons pour la logistique

---

## 📦 1. Comprendre la Fonctionnalité de Gestion de Tâches

### 1.1 Les Fonctionnalités de Base

Notre gestionnaire de tâches permettra aux utilisateurs de :

1. **Ajouter de nouvelles tâches** avec titre, description, date d'échéance et priorité
2. **Afficher les tâches** dans une liste
3. **Marquer les tâches comme complétées**
4. **Modifier les tâches** existantes
5. **Supprimer les tâches**

### 1.2 Structure d'une Tâche

Chaque tâche sera représentée par un objet JavaScript :

```javascript
/**
 * @typedef {Object} Task
 * @property {number} id - Identifiant unique de la tâche
 * @property {string} title - Le nom de la tâche
 * @property {string} description - Description détaillée
 * @property {string} dueDate - Date d'échéance (format 'YYYY-MM-DD')
 * @property {string} priority - Niveau d'importance ('Low', 'Medium', 'High', 'Urgent')
 * @property {boolean} isCompleted - Statut de complétion
 */

// Exemple de tâche
const exampleTask = {
  id: 1,
  title: "Faire les courses",
  description: "Lait, œufs, pain",
  dueDate: "2026-01-20",
  priority: "High",
  isCompleted: false,
};
```

---

## 💻 2. Implémentation Initiale (Version Simple)

### 2.1 Structure de Données : Un Tableau Simple

Pour commencer, nous allons stocker toutes les tâches dans un **tableau JavaScript** simple.

```javascript
// task-manager.js

// Tableau global pour stocker les tâches
let tasks = [];

// Compteur pour générer des IDs uniques
let nextTaskId = 1;

/**
 * Génère un ID unique pour une nouvelle tâche
 * @returns {number} L'ID généré
 */
function generateTaskId() {
  return nextTaskId++;
}
```

**Analyse de Complexité :**

- `generateTaskId()` : **O(1)** - simple incrémentation

---

### 2.2 Fonction : Ajouter une Tâche

```javascript
/**
 * Ajoute une nouvelle tâche au tableau global
 * @param {string} title
 * @param {string} description
 * @param {string} dueDate
 * @param {string} priority
 * @returns {Task} La tâche nouvellement créée
 */
function addTask(title, description, dueDate, priority) {
  const newTask = {
    id: generateTaskId(),
    title: title,
    description: description,
    dueDate: dueDate,
    priority: priority,
    isCompleted: false,
  };

  tasks.push(newTask); // Ajouter à la fin du tableau
  return newTask;
}
```

**Analyse de Complexité :**

- `tasks.push()` : **O(1) amorti** - ajout à la fin d'un tableau
- **Complexité totale : O(1)**

---

### 2.3 Fonction : Marquer une Tâche comme Complétée

```javascript
/**
 * Marque une tâche comme complétée en utilisant son ID
 * @param {number} taskId
 * @returns {boolean} true si trouvée et mise à jour, false sinon
 */
function completeTask(taskId) {
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === taskId) {
      tasks[i].isCompleted = true;
      return true;
    }
  }
  return false; // Tâche non trouvée
}
```

**Analyse de Complexité :**

- Boucle `for` : parcourt jusqu'à **n** éléments (où n = `tasks.length`)
- **Complexité : O(n)** - recherche linéaire

> **Premier Goulot d'Étranglement Identifié !**
>
> Avec 10 000 tâches, marquer une tâche comme complétée peut nécessiter 10 000 comparaisons dans le pire cas.

---

### 2.4 Fonction : Récupérer Toutes les Tâches

```javascript
/**
 * Récupère toutes les tâches
 * @returns {Task[]} Tableau de toutes les tâches
 */
function getAllTasks() {
  return tasks;
}
```

**Analyse de Complexité :**

- **O(1)** - retourne simplement la référence au tableau

**Mais attention :** Dans une vraie application, on voudrait souvent trier ou filtrer les tâches. Cela changerait la complexité !

---

### 2.5 Fonction : Trouver une Tâche par ID

```javascript
/**
 * Trouve une tâche spécifique par son ID
 * @param {number} taskId
 * @returns {Task|null} La tâche trouvée ou null
 */
function findTaskById(taskId) {
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === taskId) {
      return tasks[i];
    }
  }
  return null; // Non trouvée
}
```

**Analyse de Complexité :**

- **O(n)** - recherche linéaire

> **Deuxième Goulot d'Étranglement !**
>
> Chaque recherche de tâche nécessite de parcourir potentiellement tout le tableau.

---

## 📝 Micro-Exercice #1 : Analyser la Complexité

Analysez la complexité de cette fonction hypothétique :

```javascript
function deleteTask(taskId) {
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === taskId) {
      tasks.splice(i, 1); // Retire l'élément à l'index i
      return true;
    }
  }
  return false;
}
```

<details>
<summary>💡 Voir la solution</summary>

**Complexité : O(n)**

**Analyse détaillée :**

1. **Recherche** : Boucle `for` jusqu'à trouver l'élément → O(n)
2. **Suppression** : `tasks.splice(i, 1)` → O(n)
   - Doit décaler tous les éléments après l'index `i` vers la gauche

**Total : O(n) + O(n) = O(n)** (on garde le terme dominant)

**Observation :** Même si on trouve la tâche rapidement, `splice()` reste coûteux !

</details>

---

## 🔍 3. Identifier les Opportunités d'Optimisation

### 3.1 Problème #1 : Affichage Trié des Tâches

**Scénario :**

Un utilisateur veut voir ses tâches dans un ordre spécifique :

1. Par **date d'échéance** (les plus urgentes en premier)
2. Par **priorité** (Urgent > High > Medium > Low)
3. Ou une **combinaison** des deux

**Implémentation naïve :**

```javascript
function getAllTasksSortedByDueDate() {
  // Crée une copie pour ne pas modifier l'original
  const sortedTasks = [...tasks];

  // Tri par date d'échéance
  sortedTasks.sort((a, b) => {
    return new Date(a.dueDate) - new Date(b.dueDate);
  });

  return sortedTasks;
}
```

**Analyse de Complexité :**

- `[...tasks]` : O(n) - copie du tableau
- `sortedTasks.sort()` : **O(n log n)** - algorithme de tri intégré
- **Total : O(n log n)**

**Le Problème :**

Si `getAllTasksSortedByDueDate()` est appelé **à chaque fois** que l'utilisateur charge la page ou change de filtre, on trie **à répétition** les mêmes données.

> **Opportunité d'Optimisation**
>
> Dans les leçons futures, nous verrons comment **maintenir l'ordre** des tâches au lieu de re-trier constamment.

---

### 3.2 Problème #2 : Recherche Répétée

**Scénario :**

Dans un système de support client, les agents marquent des tickets comme "résolus" **des centaines de fois par jour**.

Chaque appel à `completeTask(id)` fait une recherche **O(n)**.

**Exemple de charge :**

- 10 000 tickets actifs
- 500 mises à jour par jour
- Chaque mise à jour : recherche O(n)

**Total d'opérations quotidiennes :** 500 × 10 000 = **5 000 000 comparaisons**

> **Opportunité d'Optimisation**
>
> Nous verrons comment utiliser des **hash tables** (objets JavaScript) pour réduire la recherche à **O(1)**.

---

### 3.3 Problème #3 : Suppression Coûteuse

**Scénario :**

Un gestionnaire de projet supprime plusieurs tâches obsolètes en une seule session.

Chaque suppression avec `splice()` :

- Recherche : O(n)
- Décalage des éléments : O(n)

**Pour supprimer 100 tâches d'un tableau de 10 000 :**

- Environ **1 000 000 d'opérations**

> **Opportunité d'Optimisation**
>
> Nous explorerons des structures de données comme les **listes chaînées** où la suppression est O(1).

---

## 📂 4. Configuration du Projet

### 4.1 Structure des Fichiers

```
project-root/
├── index.html           # Interface utilisateur
├── scripts/
│   ├── task-manager.js  # Logique de gestion des tâches
│   └── main.js          # Connexion entre HTML et task-manager.js
└── styles/
    └── main.css         # Styles CSS de base
```

---

### 4.2 Fichier : `index.html`

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Gestionnaire de Tâches - Étude de Cas</title>
    <link rel="stylesheet" href="styles/main.css" />
  </head>
  <body>
    <h1>📋 Mon Gestionnaire de Tâches</h1>

    <div id="task-list-container">
      <!-- Les tâches seront affichées ici -->
    </div>

    <script src="scripts/task-manager.js"></script>
    <script src="scripts/main.js"></script>
  </body>
</html>
```

---

### 4.3 Fichier : `scripts/task-manager.js`

```javascript
// scripts/task-manager.js

// Tableau global pour stocker les tâches
let tasks = [];
let nextTaskId = 1;

function generateTaskId() {
  return nextTaskId++;
}

/**
 * @typedef {Object} Task
 * @property {number} id
 * @property {string} title
 * @property {string} description
 * @property {string} dueDate
 * @property {string} priority - 'Low' | 'Medium' | 'High' | 'Urgent'
 * @property {boolean} isCompleted
 */

/**
 * Ajoute une nouvelle tâche
 */
function addTask(title, description, dueDate, priority) {
  const newTask = {
    id: generateTaskId(),
    title: title,
    description: description,
    dueDate: dueDate,
    priority: priority,
    isCompleted: false,
  };

  tasks.push(newTask);
  return newTask;
}

/**
 * Marque une tâche comme complétée
 */
function completeTask(taskId) {
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === taskId) {
      tasks[i].isCompleted = true;
      return true;
    }
  }
  return false;
}

/**
 * Récupère toutes les tâches
 */
function getAllTasks() {
  return tasks;
}

/**
 * Trouve une tâche par ID
 */
function findTaskById(taskId) {
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === taskId) {
      return tasks[i];
    }
  }
  return null;
}
```

---

### 4.4 Fichier : `scripts/main.js`

```javascript
// scripts/main.js

/**
 * Affiche les tâches dans le DOM
 * @param {Task[]} tasksToRender
 */
function renderTasks(tasksToRender) {
  const container = document.getElementById("task-list-container");
  container.innerHTML = ""; // Effacer le contenu précédent

  if (tasksToRender.length === 0) {
    container.innerHTML = "<p>Aucune tâche trouvée.</p>";
    return;
  }

  const ul = document.createElement("ul");

  tasksToRender.forEach((task) => {
    const li = document.createElement("li");
    li.className = task.isCompleted ? "completed" : "";

    li.innerHTML = `
            <strong>${task.title}</strong>
            <span class="priority priority-${task.priority.toLowerCase()}">${
              task.priority
            }</span>
            <span class="due-date">Échéance: ${task.dueDate}</span>
            <p>${task.description}</p>
            <button onclick="handleCompleteTask(${task.id})">
                ${task.isCompleted ? "Annuler" : "Marquer comme complété"}
            </button>
        `;

    ul.appendChild(li);
  });

  container.appendChild(ul);
}

/**
 * Gère le clic sur le bouton "Marquer comme complété"
 */
function handleCompleteTask(taskId) {
  const task = findTaskById(taskId);
  if (task) {
    task.isCompleted = !task.isCompleted; // Toggle
    console.log(`Tâche ${taskId} mise à jour: ${task.isCompleted}`);
    renderTasks(getAllTasks());
  }
}

/**
 * Initialisation au chargement de la page
 */
document.addEventListener("DOMContentLoaded", () => {
  // Ajouter des tâches de démonstration
  if (tasks.length === 0) {
    addTask("Faire les courses", "Lait, œufs, pain", "2026-01-20", "High");
    addTask(
      "Planifier réunion",
      "Sync équipe sur projet X",
      "2026-01-22",
      "Medium",
    );
    addTask(
      "Payer facture électricité",
      "Échéance fin du mois",
      "2026-01-30",
      "Urgent",
    );
    addTask(
      "Lire chapitre algorithmes",
      "Module 1, leçon 6",
      "2026-01-25",
      "Low",
    );
    addTask("Préparer présentation", "Revue Q4", "2026-01-28", "High");
    addTask(
      "Appeler plombier",
      "Fuite dans la salle de bain",
      "2026-01-21",
      "Urgent",
    );
  }

  renderTasks(getAllTasks());
});

// Exposer findTaskById pour handleCompleteTask
if (typeof window !== "undefined") {
  window.findTaskById = findTaskById;
}
```

---

### 4.5 Fichier : `styles/main.css`

```css
/* styles/main.css */

body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  margin: 20px;
  background-color: #f7f9fc;
  color: #333;
}

h1 {
  color: #2c3e50;
  text-align: center;
}

#task-list-container ul {
  list-style: none;
  padding: 0;
  max-width: 800px;
  margin: 0 auto;
}

#task-list-container li {
  background-color: #ffffff;
  border: 1px solid #e1e8ed;
  border-left: 5px solid #3498db;
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

#task-list-container li:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

#task-list-container li.completed {
  background-color: #d5f4e6;
  border-left-color: #27ae60;
  opacity: 0.8;
}

#task-list-container li.completed strong {
  text-decoration: line-through;
  color: #7f8c8d;
}

.priority {
  display: inline-block;
  padding: 3px 8px;
  border-radius: 4px;
  font-size: 0.85em;
  font-weight: bold;
  margin-left: 10px;
}

.priority-urgent {
  background-color: #e74c3c;
  color: white;
}

.priority-high {
  background-color: #f39c12;
  color: white;
}

.priority-medium {
  background-color: #3498db;
  color: white;
}

.priority-low {
  background-color: #95a5a6;
  color: white;
}

.due-date {
  display: inline-block;
  margin-left: 10px;
  font-size: 0.9em;
  color: #7f8c8d;
}

#task-list-container button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 8px 15px;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
  font-size: 0.9em;
  transition: background-color 0.3s;
}

#task-list-container button:hover {
  background-color: #2980b9;
}

#task-list-container li.completed button {
  background-color: #27ae60;
}

#task-list-container li.completed button:hover {
  background-color: #229954;
}

#task-list-container p {
  margin: 10px 0;
  font-size: 0.95em;
  color: #555;
}
```

---

## 🧪 5. Tester l'Application

### 5.1 Lancer l'Application

1. Créez les fichiers dans la structure ci-dessus
2. Ouvrez `index.html` dans votre navigateur
3. Vous devriez voir 6 tâches affichées

### 5.2 Tester les Fonctionnalités

- **Cliquez sur "Marquer comme complété"** : La tâche devient verte et barrée
- **Ouvrez la console du navigateur (F12)** : Vous verrez les logs de mise à jour

---

## 💪 Exercices Pratiques

### Exercice 1 : Analyser la Performance de `addTask`

**Question :**

En utilisant les concepts de Big O, quelle est la complexité temporelle de `addTask()` ?

Supposez que `tasks.push()` est une opération en temps constant O(1) (ce qui est généralement vrai en JavaScript, avec un coût amorti).

<details>
<summary>💡 Voir la solution</summary>

**Complexité : O(1)**

**Analyse :**

- `generateTaskId()` : O(1) - simple incrémentation
- Création de l'objet `newTask` : O(1) - affectations constantes
- `tasks.push(newTask)` : O(1) amorti

**Total : O(1) + O(1) + O(1) = O(1)**

**Note sur l'amortissement :**

Occasionnellement, JavaScript doit réallouer de la mémoire pour le tableau (O(n)), mais cela arrive si rarement que le coût **amorti** reste O(1).

</details>

---

### Exercice 2 : Analyser la Performance de `completeTask`

**Questions :**

a. Quelle est la complexité temporelle dans le **pire cas** ?

b. Quelle est la complexité temporelle dans le **meilleur cas** ?

c. Décrivez un scénario où `completeTask` exhibe son pire cas.

<details>
<summary>💡 Voir la solution</summary>

**a. Pire cas : O(n)**

- Si la tâche recherchée est à la **fin du tableau** ou **n'existe pas**, la boucle parcourt **tous les n éléments**.

**b. Meilleur cas : O(1)**

- Si la tâche recherchée est le **premier élément** (`tasks[0]`), la boucle s'arrête immédiatement.

**c. Scénario du pire cas :**

Imaginons un tableau de 10 000 tâches :

```javascript
// Ajouter 10 000 tâches
for (let i = 0; i < 10000; i++) {
  addTask(`Tâche ${i}`, "Description", "2026-01-30", "Medium");
}

// Chercher la dernière tâche (ID 10000)
completeTask(10000); // Parcourt les 10 000 éléments → O(n)

// Chercher une tâche inexistante
completeTask(99999); // Parcourt les 10 000 éléments → O(n)
```

</details>

---

### Exercice 3 : Simuler la Croissance des Données

**Instructions :**

Modifiez `task-manager.js` pour ajouter **1000, 10 000, ou même 100 000 tâches** programmatiquement.

```javascript
// Ajouter à la fin de task-manager.js (avant de charger main.js)

// Simuler une grande quantité de tâches
function generateManyTasks(count) {
  const priorities = ["Low", "Medium", "High", "Urgent"];

  for (let i = 1; i <= count; i++) {
    const priority = priorities[Math.floor(Math.random() * priorities.length)];
    const dueDate = `2026-01-${Math.floor(Math.random() * 28) + 1}`;

    addTask(`Tâche générée ${i}`, `Description ${i}`, dueDate, priority);
  }

  console.log(`${count} tâches générées.`);
}

// Décommenter pour tester
// generateManyTasks(1000);
// generateManyTasks(10000);
// generateManyTasks(100000); // Attention: Très lent !
```

**Questions d'Auto-Réflexion :**

1. Avec 1000 tâches, l'application est-elle toujours réactive ?
2. Avec 10 000 tâches, que remarquez-vous ?
3. Avec 100 000 tâches, que se passe-t-il ?
4. Quelles parties du code deviennent les plus lentes ?

<details>
<summary>💡 Observations attendues</summary>

**Avec 1 000 tâches :**

- L'affichage initial prend quelques millisecondes
- Cliquer sur "Marquer comme complété" reste réactif

**Avec 10 000 tâches :**

- L'affichage initial prend 100-500ms
- Cliquer sur un bouton peut prendre 50-100ms
- Le scrolling peut être moins fluide

**Avec 100 000 tâches :**

- L'affichage initial peut prendre **plusieurs secondes**
- Cliquer sur un bouton prend 500ms-1s
- Le navigateur peut devenir **non réactif**

**Parties les plus lentes :**

1. **`renderTasks()`** : O(n) - crée des éléments DOM pour chaque tâche
2. **`findTaskById()`** : O(n) - recherche linéaire
3. **`completeTask()`** : O(n) - recherche linéaire

</details>

---

### Exercice 4 : Mesurer le Temps d'Exécution

Ajoutez des mesures de performance pour quantifier les problèmes.

```javascript
// Dans main.js, modifier handleCompleteTask

function handleCompleteTask(taskId) {
  console.time(`completeTask-${taskId}`); // Démarrer le chronomètre

  const task = findTaskById(taskId);
  if (task) {
    task.isCompleted = !task.isCompleted;
    renderTasks(getAllTasks());
  }

  console.timeEnd(`completeTask-${taskId}`); // Arrêter et afficher
}
```

**Test :**

Générez 10 000 tâches, puis cliquez sur plusieurs boutons. Observez les temps dans la console.

---

## 📊 6. Tableau Récapitulatif des Complexités

| Opération        | Implémentation Actuelle | Complexité | Problème ?        |
| ---------------- | ----------------------- | ---------- | ----------------- |
| `addTask()`      | `array.push()`          | O(1)       | Efficace          |
| `completeTask()` | Recherche linéaire      | O(n)       | Lent avec n grand |
| `findTaskById()` | Recherche linéaire      | O(n)       | Lent avec n grand |
| `deleteTask()`   | `splice()`              | O(n)       | Lent avec n grand |
| `getAllTasks()`  | Retourne le tableau     | O(1)       | Mais pas de tri   |
| Tri des tâches   | `array.sort()`          | O(n log n) | À chaque appel    |

---

## 🎯 7. Scénarios d'Optimisation Futurs

### Scénario 1 : Système de Support Client

**Contexte :**

- 10 000 tickets actifs
- 50 agents
- Chaque agent résout 10 tickets/heure

**Problème actuel :**

- Chaque résolution nécessite `findTaskById()` : **O(n)**
- 500 résolutions/heure × 10 000 tickets = **5 000 000 comparaisons/heure**

**Optimisation future (Module 3) :**

Utiliser une **Hash Table** (objet JavaScript) :

```javascript
// Au lieu de:
const task = findTaskById(123); // O(n)

// Utiliser:
const taskMap = {
  123: { id: 123, title: "...", ... },
  124: { id: 124, title: "...", ... }
};
const task = taskMap[123]; // O(1) !
```

---

### Scénario 2 : Planificateur de Livraisons

**Contexte :**

- 5 000 colis à livrer
- Besoin d'afficher les livraisons par **priorité + date d'échéance**

**Problème actuel :**

- Tri complet à chaque changement de filtre : **O(n log n)**

**Optimisation future (Module 4) :**

Maintenir les tâches **déjà triées** avec des algorithmes de tri efficaces ou des structures de données comme les **heaps**.

---

## ✅ Quiz de Validation

### Question 1 : Complexité de `addTask`

Quelle est la complexité de `addTask()` ?

- [ ] A. O(1)
- [ ] B. O(log n)
- [ ] C. O(n)
- [ ] D. O(n²)

<details>
<summary>Voir la réponse</summary>

**Réponse : A**

`addTask()` utilise `push()` qui est **O(1) amorti**.

</details>

---

### Question 2 : Pire Cas de `findTaskById`

Dans quel cas `findTaskById(id)` prend-il le plus de temps ?

- [ ] A. Quand l'ID est le premier élément
- [ ] B. Quand l'ID est au milieu du tableau
- [ ] C. Quand l'ID est le dernier élément ou inexistant
- [ ] D. Le temps est toujours constant

<details>
<summary>Voir la réponse</summary>

**Réponse : C**

Pire cas : parcourir **tout le tableau** (n éléments) → **O(n)**.

</details>

---

### Question 3 : Problème de Performance

Avec 100 000 tâches, quelle opération devient la plus problématique ?

- [ ] A. Ajouter une nouvelle tâche
- [ ] B. Afficher toutes les tâches dans le DOM
- [ ] C. Générer un ID unique
- [ ] D. Créer un objet tâche

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

`renderTasks()` doit créer **100 000 éléments DOM**, ce qui est **O(n)** et très coûteux pour le navigateur.

</details>

---

## 📌 Récapitulatif de la Leçon

### Points Clés

1. **Étude de Cas Établie**
   - Gestionnaire de tâches réaliste
   - Fonctionnalités de base implémentées

2. **Goulots d'Étranglement Identifiés**
   - Recherche linéaire : O(n)
   - Tri répété : O(n log n)
   - Suppression avec `splice()` : O(n)

3. **Architecture de Projet**
   - Structure de fichiers claire
   - Séparation logique/présentation
   - Prêt pour optimisations futures

4. **Mesures de Performance**
   - Utilisation de `console.time()`
   - Tests avec grandes quantités de données

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez maintenant une base solide pour explorer les algorithmes et structures de données.

### Ce Que Vous Avez Appris

1. Comment analyser un problème réel avec Big O
2. Comment identifier les goulots d'étranglement
3. Comment mettre en place un projet pour tester des optimisations
4. L'importance de mesurer avant d'optimiser

### Prochaines Étapes

Dans les **modules suivants**, nous utiliserons cette étude de cas pour :

- **Module 2** : Structures de données avancées (Hash Tables, Listes Chaînées)
- **Module 3** : Algorithmes de tri et de recherche
- **Module 4** : Optimisation avec des structures spécialisées

**À faire avant la prochaine leçon :**

- Testez l'application avec différentes quantités de tâches
- Mesurez les temps d'exécution
- Réfléchissez à des solutions possibles

---

## 🔗 Ressources Complémentaires

### Documentation

- [MDN - Performance API](https://developer.mozilla.org/fr/docs/Web/API/Performance)
- [Chrome DevTools - Performance](https://developer.chrome.com/docs/devtools/performance/)

### Outils

- [Visualgo - Visualisation d'algorithmes](https://visualgo.net/)
- [JS Benchmark](https://jsbench.me/)

---

## ➡️ Prochaine Étape : Leçon 7 - Les Tableaux

### Ce qui vous attend

Nous entrons dans le Module 2 ! La prochaine leçon, **« Tableaux : Listes Dynamiques et Opérations de Base »**, est la première d'une série sur les structures de données fondamentales.

**Vous découvrirez :**

- Comment créer, initialiser et manipuler des tableaux en JavaScript.
- La différence de performance cruciale entre `push`/`pop` (rapide) et `shift`/`unshift` (lent).
- Des méthodes essentielles pour rechercher et parcourir des éléments.

### Préparez-vous !

Les tableaux sont la structure de données la plus utilisée. Les maîtriser est la première étape pour construire des algorithmes plus complexes et performants.

---

<div align="center">

**Leçon 6 sur 42 - Module 1 : Fondements des algorithmes et révision de JavaScript**

[⬅️ Leçon 5 : Analyse des Opérations JavaScript Simples](./lecon-5-analyse-operations-javascript.md) | [Retour au sommaire](./README.md) | [Leçon 7 : Tableaux - Listes Dynamiques et Opérations de Base ➡️](../module-2/lecon-1-tableaux-listes-dynamiques-operations-base.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
