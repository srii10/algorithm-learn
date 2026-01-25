##### Leçon 12 sur 42

# Pratique : Utiliser Piles/Files pour la Priorisation des Tâches dans l'Étude de Cas

**Module 2** : Structures de Données Essentielles en JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Appliquer les structures de données Pile et File dans des scénarios réels de gestion de tâches
- Implémenter un système d'annulation/rétablissement (Undo/Redo) en utilisant des piles
- Créer un système de traitement séquentiel avec des files
- Concevoir un gestionnaire de tâches avec priorisation utilisant plusieurs files
- Combiner Piles et Files pour résoudre des problèmes complexes de gestion de tâches

---

### ⏱️ Durée estimée : 3h - 3h30

---

## 📚 Prérequis

- Avoir compris le principe LIFO et l'implémentation des Piles avec des tableaux (Leçon 10)
- Avoir compris le principe FIFO et l'implémentation des Files avec des tableaux (Leçon 11)
- Maîtriser les bases de la manipulation des tableaux en JavaScript

---

## 🚀 Introduction : Application pratique des Piles et Files dans la gestion de tâches

Dans les leçons précédentes, nous avons exploré les structures de données **Pile** (LIFO) et **File** (FIFO). Maintenant, il est temps de mettre en pratique ces connaissances dans des scénarios réels.

Cette leçon vous guidera à travers trois applications concrètes :

1. **Système d'annulation/rétablissement** : Utiliser des piles pour gérer l'historique des actions
2. **Traitement séquentiel de tâches** : Utiliser des files pour traiter les tâches dans l'ordre d'arrivée
3. **Gestionnaire de tâches avec priorisation** : Combiner plusieurs files pour gérer des tâches de différentes priorités

Ces exemples vous montreront comment choisir la bonne structure de données pour résoudre des problèmes spécifiques de gestion de tâches.

---

## 📖 Révision : Piles et Files

Avant de plonger dans les applications pratiques, revoyons rapidement les concepts clés.

### Rappel : Qu'est-ce qu'une Pile (Stack) ?

Une **Pile** est une structure de données qui suit le principe **LIFO** (Last-In, First-Out).

**Caractéristiques principales :**

- Le dernier élément ajouté est le premier à être retiré
- Comme une pile d'assiettes : on ajoute et retire par le dessus
- Deux opérations principales : `push()` (empiler) et `pop()` (dépiler)

**Exemple visuel :**

```
     [Assiette 3]  ← Dernier ajouté (sommet)
     [Assiette 2]
     [Assiette 1]  ← Premier ajouté (fond)
```

### Rappel : Qu'est-ce qu'une File (Queue) ?

Une **File** est une structure de données qui suit le principe **FIFO** (First-In, First-Out).

**Caractéristiques principales :**

- Le premier élément ajouté est le premier à être retiré
- Comme une file d'attente à la caisse : premier arrivé, premier servi
- Deux opérations principales : `enqueue()` (enfiler) et `dequeue()` (défiler)

**Exemple visuel :**

```
Premier arrivé → [Client 1] [Client 2] [Client 3] ← Dernier arrivé
                      ↓
                 Premier servi
```

---

## 💻 Implémentation des Piles et Files avec des Tableaux JavaScript

### Classe TaskStack (Pile de Tâches)

```javascript
class TaskStack {
  constructor() {
    this.items = [];
  }

  // Ajouter une tâche au sommet de la pile
  push(task) {
    this.items.push(task);
    console.log(`Tâche ajoutée : ${task.description}`);
  }

  // Retirer et retourner la tâche du sommet
  pop() {
    if (this.isEmpty()) {
      console.log("La pile est vide, aucune tâche à retirer.");
      return null;
    }
    const task = this.items.pop();
    console.log(`Tâche retirée : ${task.description}`);
    return task;
  }

  // Voir la tâche au sommet sans la retirer
  peek() {
    if (this.isEmpty()) {
      console.log("La pile est vide.");
      return null;
    }
    return this.items[this.items.length - 1];
  }

  // Vérifier si la pile est vide
  isEmpty() {
    return this.items.length === 0;
  }

  // Obtenir le nombre de tâches
  size() {
    return this.items.length;
  }

  // Afficher toutes les tâches
  display() {
    if (this.isEmpty()) {
      console.log("La pile est vide.");
      return;
    }
    console.log("Tâches dans la pile (du sommet au fond) :");
    for (let i = this.items.length - 1; i >= 0; i--) {
      console.log(`  ${i + 1}. ${this.items[i].description}`);
    }
  }
}
```

### Classe TaskQueue (File de Tâches)

```javascript
class TaskQueue {
  constructor() {
    this.items = [];
  }

  // Ajouter une tâche à la fin de la file
  enqueue(task) {
    this.items.push(task);
    console.log(`Tâche ajoutée à la file : ${task.description}`);
  }

  // Retirer et retourner la première tâche
  dequeue() {
    if (this.isEmpty()) {
      console.log("La file est vide, aucune tâche à retirer.");
      return null;
    }
    const task = this.items.shift();
    console.log(`Tâche retirée de la file : ${task.description}`);
    return task;
  }

  // Voir la première tâche sans la retirer
  front() {
    if (this.isEmpty()) {
      console.log("La file est vide.");
      return null;
    }
    return this.items[0];
  }

  // Vérifier si la file est vide
  isEmpty() {
    return this.items.length === 0;
  }

  // Obtenir le nombre de tâches
  size() {
    return this.items.length;
  }

  // Afficher toutes les tâches
  display() {
    if (this.isEmpty()) {
      console.log("La file est vide.");
      return;
    }
    console.log("Tâches dans la file (de la tête à la queue) :");
    this.items.forEach((task, index) => {
      console.log(`  ${index + 1}. ${task.description}`);
    });
  }
}
```

---

## 🎯 Application Pratique 1 : Fonctionnalité Annuler/Rétablir (Undo/Redo)

### Contexte du Problème

Dans une application de gestion de tâches, les utilisateurs doivent pouvoir :

- **Annuler** (Undo) leurs dernières actions
- **Rétablir** (Redo) les actions annulées

C'est un scénario parfait pour utiliser des **piles** car :

- L'action la plus récente doit être annulée en premier (LIFO)
- Les actions rétablies doivent l'être dans l'ordre inverse de l'annulation

### Solution avec des Piles

Nous utiliserons **deux piles** :

1. **Pile d'historique** : Stocke toutes les actions effectuées
2. **Pile de rétablissement** : Stocke les actions annulées

```javascript
class TaskHistory {
  constructor() {
    this.historyStack = new TaskStack(); // Pour Undo
    this.redoStack = new TaskStack(); // Pour Redo
  }

  // Enregistrer une nouvelle action
  recordAction(action) {
    this.historyStack.push(action);
    // Vider la pile de rétablissement car une nouvelle action invalide l'historique redo
    this.redoStack = new TaskStack();
    console.log(`Action enregistrée : ${action.description}`);
  }

  // Annuler la dernière action
  undo() {
    if (this.historyStack.isEmpty()) {
      console.log("Rien à annuler.");
      return null;
    }

    const action = this.historyStack.pop();
    this.redoStack.push(action);
    console.log(`Action annulée : ${action.description}`);
    return action;
  }

  // Rétablir la dernière action annulée
  redo() {
    if (this.redoStack.isEmpty()) {
      console.log("Rien à rétablir.");
      return null;
    }

    const action = this.redoStack.pop();
    this.historyStack.push(action);
    console.log(`Action rétablie : ${action.description}`);
    return action;
  }

  // Afficher l'historique actuel
  displayHistory() {
    console.log("\n--- Historique des Actions ---");
    this.historyStack.display();
    console.log("\n--- Actions Annulées (disponibles pour Redo) ---");
    this.redoStack.display();
  }
}
```

### Exemple d'Utilisation

```javascript
// Créer un gestionnaire d'historique
const taskHistory = new TaskHistory();

// Enregistrer des actions
taskHistory.recordAction({
  id: 1,
  description: "Créer une nouvelle tâche 'Faire les courses'",
});
taskHistory.recordAction({
  id: 2,
  description: "Marquer 'Appeler le médecin' comme terminée",
});
taskHistory.recordAction({
  id: 3,
  description: "Supprimer la tâche 'Ancienne réunion'",
});

taskHistory.displayHistory();

// Annuler les deux dernières actions
console.log("\n=== Annulation de 2 actions ===");
taskHistory.undo();
taskHistory.undo();

taskHistory.displayHistory();

// Rétablir une action
console.log("\n=== Rétablissement d'une action ===");
taskHistory.redo();

taskHistory.displayHistory();

// Enregistrer une nouvelle action (cela vide la pile de redo)
console.log("\n=== Nouvelle action ===");
taskHistory.recordAction({
  id: 4,
  description: "Modifier la priorité de 'Finir le rapport'",
});

taskHistory.displayHistory();
```

### Résultat Attendu

```
Action enregistrée : Créer une nouvelle tâche 'Faire les courses'
Action enregistrée : Marquer 'Appeler le médecin' comme terminée
Action enregistrée : Supprimer la tâche 'Ancienne réunion'

--- Historique des Actions ---
Tâches dans la pile (du sommet au fond) :
  3. Supprimer la tâche 'Ancienne réunion'
  2. Marquer 'Appeler le médecin' comme terminée
  1. Créer une nouvelle tâche 'Faire les courses'

--- Actions Annulées (disponibles pour Redo) ---
La pile est vide.

=== Annulation de 2 actions ===
Tâche retirée : Supprimer la tâche 'Ancienne réunion'
Action annulée : Supprimer la tâche 'Ancienne réunion'
Tâche retirée : Marquer 'Appeler le médecin' comme terminée
Action annulée : Marquer 'Appeler le médecin' comme terminée

--- Historique des Actions ---
Tâches dans la pile (du sommet au fond) :
  1. Créer une nouvelle tâche 'Faire les courses'

--- Actions Annulées (disponibles pour Redo) ---
Tâches dans la pile (du sommet au fond) :
  2. Marquer 'Appeler le médecin' comme terminée
  1. Supprimer la tâche 'Ancienne réunion'

=== Rétablissement d'une action ===
Tâche retirée : Marquer 'Appeler le médecin' comme terminée
Action rétablie : Marquer 'Appeler le médecin' comme terminée

--- Historique des Actions ---
Tâches dans la pile (du sommet au fond) :
  2. Marquer 'Appeler le médecin' comme terminée
  1. Créer une nouvelle tâche 'Faire les courses'

--- Actions Annulées (disponibles pour Redo) ---
Tâches dans la pile (du sommet au fond) :
  1. Supprimer la tâche 'Ancienne réunion'

=== Nouvelle action ===
Action enregistrée : Modifier la priorité de 'Finir le rapport'

--- Historique des Actions ---
Tâches dans la pile (du sommet au fond) :
  3. Modifier la priorité de 'Finir le rapport'
  2. Marquer 'Appeler le médecin' comme terminée
  1. Créer une nouvelle tâche 'Faire les courses'

--- Actions Annulées (disponibles pour Redo) ---
La pile est vide.
```

### Point Clé

Lorsqu'une nouvelle action est enregistrée après une annulation, la pile de rétablissement est vidée. C'est un comportement standard dans la plupart des applications, car une nouvelle action crée une nouvelle branche d'historique.

---

## 🎯 Application Pratique 2 : Traitement Séquentiel des Tâches

### Contexte du Problème

Dans une application, les notifications doivent être traitées dans l'ordre où elles arrivent :

- Première notification reçue = Première traitée
- Traitement équitable sans priorité

C'est un scénario parfait pour une **file** (principe FIFO).

### Solution avec une File

```javascript
class NotificationProcessor {
  constructor() {
    this.notificationQueue = new TaskQueue();
  }

  // Ajouter une notification à traiter
  addNotification(notification) {
    this.notificationQueue.enqueue(notification);
  }

  // Traiter la prochaine notification
  processNext() {
    const notification = this.notificationQueue.dequeue();
    if (notification) {
      console.log(`\nTraitement de la notification :`);
      console.log(`   Type : ${notification.type}`);
      console.log(`   Message : ${notification.message}`);
      console.log(`   Heure : ${notification.timestamp}`);
      return notification;
    }
    return null;
  }

  // Traiter toutes les notifications en attente
  processAll() {
    console.log("\n=== Traitement de toutes les notifications ===");
    let count = 0;
    while (!this.notificationQueue.isEmpty()) {
      this.processNext();
      count++;
    }
    console.log(`\n${count} notification(s) traitée(s).`);
  }

  // Afficher les notifications en attente
  displayPending() {
    console.log("\n--- Notifications en Attente ---");
    this.notificationQueue.display();
  }

  // Obtenir le nombre de notifications en attente
  getPendingCount() {
    return this.notificationQueue.size();
  }
}
```

### Exemple d'Utilisation

```javascript
// Créer un processeur de notifications
const processor = new NotificationProcessor();

// Ajouter plusieurs notifications
processor.addNotification({
  type: "Info",
  message: "Nouvelle tâche assignée : Réviser le code",
  timestamp: "10:15:00",
});

processor.addNotification({
  type: "Rappel",
  message: "Réunion d'équipe dans 15 minutes",
  timestamp: "10:16:30",
});

processor.addNotification({
  type: "Alerte",
  message: "Date limite approchante pour 'Rapport mensuel'",
  timestamp: "10:17:45",
});

processor.addNotification({
  type: "Info",
  message: "Commentaire ajouté sur votre tâche 'Design UI'",
  timestamp: "10:18:20",
});

// Afficher les notifications en attente
processor.displayPending();

// Traiter les deux premières notifications
console.log("\n=== Traitement manuel des 2 premières ===");
processor.processNext();
processor.processNext();

// Afficher ce qui reste
processor.displayPending();

// Traiter toutes les notifications restantes
processor.processAll();
```

### Résultat Attendu

```
Tâche ajoutée à la file : Nouvelle tâche assignée : Réviser le code
Tâche ajoutée à la file : Réunion d'équipe dans 15 minutes
Tâche ajoutée à la file : Date limite approchante pour 'Rapport mensuel'
Tâche ajoutée à la file : Commentaire ajouté sur votre tâche 'Design UI'

--- Notifications en Attente ---
Tâches dans la file (de la tête à la queue) :
  1. Nouvelle tâche assignée : Réviser le code
  2. Réunion d'équipe dans 15 minutes
  3. Date limite approchante pour 'Rapport mensuel'
  4. Commentaire ajouté sur votre tâche 'Design UI'

=== Traitement manuel des 2 premières ===
Tâche retirée de la file : Nouvelle tâche assignée : Réviser le code

 Traitement de la notification :
   Type : Info
   Message : Nouvelle tâche assignée : Réviser le code
   Heure : 10:15:00
Tâche retirée de la file : Réunion d'équipe dans 15 minutes

 Traitement de la notification :
   Type : Rappel
   Message : Réunion d'équipe dans 15 minutes
   Heure : 10:16:30

--- Notifications en Attente ---
Tâches dans la file (de la tête à la queue) :
  1. Date limite approchante pour 'Rapport mensuel'
  2. Commentaire ajouté sur votre tâche 'Design UI'

=== Traitement de toutes les notifications ===
Tâche retirée de la file : Date limite approchante pour 'Rapport mensuel'

 Traitement de la notification :
   Type : Alerte
   Message : Date limite approchante pour 'Rapport mensuel'
   Heure : 10:17:45
Tâche retirée de la file : Commentaire ajouté sur votre tâche 'Design UI'

 Traitement de la notification :
   Type : Info
   Message : Commentaire ajouté sur votre tâche 'Design UI'
   Heure : 10:18:20

 2 notification(s) traitée(s).
```

### Avantages de l'Approche FIFO

- **Équité** : Toutes les notifications sont traitées dans l'ordre d'arrivée
- **Prévisibilité** : Les utilisateurs savent que leurs notifications seront traitées séquentiellement
- **Simplicité** : Logique claire et facile à comprendre

---

## 🎯 Application Pratique 3 : Exécution de Tâches avec Priorisation

### Contexte du Problème

Dans une application de gestion de tâches avancée, nous avons besoin de :

- Gérer des tâches de différentes priorités (Haute, Moyenne, Basse)
- Traiter les tâches prioritaires en premier
- Maintenir l'ordre FIFO au sein de chaque niveau de priorité

### Solution : Combiner Plusieurs Files

Nous utiliserons **trois files distinctes**, une pour chaque niveau de priorité.

```javascript
class PrioritizedTaskManager {
  constructor() {
    this.highPriorityQueue = new TaskQueue();
    this.mediumPriorityQueue = new TaskQueue();
    this.lowPriorityQueue = new TaskQueue();
  }

  // Ajouter une tâche selon sa priorité
  addTask(task) {
    switch (task.priority.toLowerCase()) {
      case "haute":
        this.highPriorityQueue.enqueue(task);
        break;
      case "moyenne":
        this.mediumPriorityQueue.enqueue(task);
        break;
      case "basse":
        this.lowPriorityQueue.enqueue(task);
        break;
      default:
        console.log(
          `Priorité inconnue "${task.priority}". Ajout en priorité basse.`,
        );
        this.lowPriorityQueue.enqueue(task);
    }
  }

  // Traiter la prochaine tâche (en respectant les priorités)
  processNextTask() {
    let task = null;

    // Vérifier d'abord la file haute priorité
    if (!this.highPriorityQueue.isEmpty()) {
      task = this.highPriorityQueue.dequeue();
      console.log(`\nTraitement de tâche HAUTE priorité :`);
    }
    // Puis la file moyenne priorité
    else if (!this.mediumPriorityQueue.isEmpty()) {
      task = this.mediumPriorityQueue.dequeue();
      console.log(`\nTraitement de tâche MOYENNE priorité :`);
    }
    // Enfin la file basse priorité
    else if (!this.lowPriorityQueue.isEmpty()) {
      task = this.lowPriorityQueue.dequeue();
      console.log(`\nTraitement de tâche BASSE priorité :`);
    } else {
      console.log("\nAucune tâche en attente.");
      return null;
    }

    console.log(`   Description : ${task.description}`);
    console.log(`   Assignée à : ${task.assignedTo}`);
    console.log(`   Date limite : ${task.deadline}`);

    return task;
  }

  // Traiter toutes les tâches en respectant les priorités
  processAllTasks() {
    console.log("\n========== Traitement de Toutes les Tâches ==========");
    let count = 0;

    while (!this.isEmpty()) {
      this.processNextTask();
      count++;
    }

    console.log(`\nTotal : ${count} tâche(s) traitée(s).`);
  }

  // Vérifier si toutes les files sont vides
  isEmpty() {
    return (
      this.highPriorityQueue.isEmpty() &&
      this.mediumPriorityQueue.isEmpty() &&
      this.lowPriorityQueue.isEmpty()
    );
  }

  // Afficher le statut de toutes les files
  displayStatus() {
    console.log("\n========== Statut des Files de Tâches ==========");

    console.log("\nTâches HAUTE Priorité :");
    this.highPriorityQueue.display();

    console.log("\nTâches MOYENNE Priorité :");
    this.mediumPriorityQueue.display();

    console.log("\nTâches BASSE Priorité :");
    this.lowPriorityQueue.display();

    const totalTasks =
      this.highPriorityQueue.size() +
      this.mediumPriorityQueue.size() +
      this.lowPriorityQueue.size();
    console.log(`\nTotal des tâches en attente : ${totalTasks}`);
  }

  // Obtenir le nombre total de tâches
  getTotalTasks() {
    return (
      this.highPriorityQueue.size() +
      this.mediumPriorityQueue.size() +
      this.lowPriorityQueue.size()
    );
  }
}
```

### Exemple d'Utilisation

```javascript
// Créer un gestionnaire de tâches avec priorisation
const taskManager = new PrioritizedTaskManager();

// Ajouter des tâches avec différentes priorités
taskManager.addTask({
  description: "Corriger le bug critique de production",
  priority: "Haute",
  assignedTo: "Alice",
  deadline: "Aujourd'hui 17h00",
});

taskManager.addTask({
  description: "Mettre à jour la documentation",
  priority: "Basse",
  assignedTo: "Bob",
  deadline: "Vendredi",
});

taskManager.addTask({
  description: "Réviser le code de la nouvelle fonctionnalité",
  priority: "Moyenne",
  assignedTo: "Charlie",
  deadline: "Mercredi",
});

taskManager.addTask({
  description: "Résoudre le problème de sécurité signalé",
  priority: "Haute",
  assignedTo: "Diana",
  deadline: "Aujourd'hui 15h00",
});

taskManager.addTask({
  description: "Préparer la réunion d'équipe",
  priority: "Moyenne",
  assignedTo: "Eve",
  deadline: "Jeudi",
});

taskManager.addTask({
  description: "Nettoyer le code inutilisé",
  priority: "Basse",
  assignedTo: "Frank",
  deadline: "Mois prochain",
});

// Afficher le statut initial
taskManager.displayStatus();

// Traiter quelques tâches manuellement
console.log("\n========== Traitement Manuel de 3 Tâches ==========");
taskManager.processNextTask();
taskManager.processNextTask();
taskManager.processNextTask();

// Afficher le statut après traitement partiel
taskManager.displayStatus();

// Traiter toutes les tâches restantes
taskManager.processAllTasks();

// Vérifier le statut final
taskManager.displayStatus();
```

### Résultat Attendu

```
Tâche ajoutée à la file : Corriger le bug critique de production
Tâche ajoutée à la file : Mettre à jour la documentation
Tâche ajoutée à la file : Réviser le code de la nouvelle fonctionnalité
Tâche ajoutée à la file : Résoudre le problème de sécurité signalé
Tâche ajoutée à la file : Préparer la réunion d'équipe
Tâche ajoutée à la file : Nettoyer le code inutilisé

========== Statut des Files de Tâches ==========

Tâches HAUTE Priorité :
Tâches dans la file (de la tête à la queue) :
  1. Corriger le bug critique de production
  2. Résoudre le problème de sécurité signalé

Tâches MOYENNE Priorité :
Tâches dans la file (de la tête à la queue) :
  1. Réviser le code de la nouvelle fonctionnalité
  2. Préparer la réunion d'équipe

Tâches BASSE Priorité :
Tâches dans la file (de la tête à la queue) :
  1. Mettre à jour la documentation
  2. Nettoyer le code inutilisé

Total des tâches en attente : 6

========== Traitement Manuel de 3 Tâches ==========
Tâche retirée de la file : Corriger le bug critique de production

Traitement de tâche HAUTE priorité :
   Description : Corriger le bug critique de production
   Assignée à : Alice
   Date limite : Aujourd'hui 17h00
Tâche retirée de la file : Résoudre le problème de sécurité signalé

Traitement de tâche HAUTE priorité :
   Description : Résoudre le problème de sécurité signalé
   Assignée à : Diana
   Date limite : Aujourd'hui 15h00
Tâche retirée de la file : Réviser le code de la nouvelle fonctionnalité

Traitement de tâche MOYENNE priorité :
   Description : Réviser le code de la nouvelle fonctionnalité
   Assignée à : Charlie
   Date limite : Mercredi

========== Statut des Files de Tâches ==========

Tâches HAUTE Priorité :
La file est vide.

Tâches MOYENNE Priorité :
Tâches dans la file (de la tête à la queue) :
  1. Préparer la réunion d'équipe

Tâches BASSE Priorité :
Tâches dans la file (de la tête à la queue) :
  1. Mettre à jour la documentation
  2. Nettoyer le code inutilisé

Total des tâches en attente : 3

========== Traitement de Toutes les Tâches ==========
Tâche retirée de la file : Préparer la réunion d'équipe

Traitement de tâche MOYENNE priorité :
   Description : Préparer la réunion d'équipe
   Assignée à : Eve
   Date limite : Jeudi
Tâche retirée de la file : Mettre à jour la documentation

Traitement de tâche BASSE priorité :
   Description : Mettre à jour la documentation
   Assignée à : Bob
   Date limite : Vendredi
Tâche retirée de la file : Nettoyer le code inutilisé

Traitement de tâche BASSE priorité :
   Description : Nettoyer le code inutilisé
   Assignée à : Frank
   Date limite : Mois prochain

Total : 3 tâche(s) traitée(s).

========== Statut des Files de Tâches ==========

Tâches HAUTE Priorité :
La file est vide.

Tâches MOYENNE Priorité :
La file est vide.

Tâches BASSE Priorité :
La file est vide.

Total des tâches en attente : 0
```

### Analyse du Comportement

1. **Ordre de traitement** : Les tâches HAUTE priorité sont toujours traitées en premier, suivies des MOYENNE, puis des BASSE.
2. **FIFO au sein de chaque priorité** : Dans la file haute priorité, "Corriger le bug" (ajouté en premier) est traité avant "Résoudre le problème de sécurité" (ajouté en second).
3. **Flexibilité** : On peut traiter les tâches manuellement une par une, ou toutes d'un coup.

---

## 📝 Micro-Exercice #1 : Historique de Navigation de Navigateur

Implémentez un système simplifié d'historique de navigation web avec les fonctionnalités suivantes :

**Fonctionnalités requises :**

- Enregistrer les URL visitées
- Bouton "Précédent" (Retour)
- Bouton "Suivant" (Avancer)
- Afficher l'URL actuelle

**Indications :**

- Utilisez deux piles : une pour l'historique de navigation et une pour les pages "suivantes"
- Quand l'utilisateur visite une nouvelle URL, videz la pile "suivant"

**Squelette de code :**

```javascript
class BrowserHistory {
  constructor() {
    this.backStack = new TaskStack(); // Pages précédentes
    this.forwardStack = new TaskStack(); // Pages suivantes
    this.currentPage = null;
  }

  // Visiter une nouvelle page
  visit(url) {
    // TODO: Implémenter la logique
  }

  // Aller à la page précédente
  goBack() {
    // TODO: Implémenter la logique
  }

  // Aller à la page suivante
  goForward() {
    // TODO: Implémenter la logique
  }

  // Afficher l'état actuel
  displayStatus() {
    // TODO: Implémenter la logique
  }
}

// Test
const browser = new BrowserHistory();
browser.visit("google.com");
browser.visit("facebook.com");
browser.visit("twitter.com");
browser.goBack();
browser.goBack();
browser.goForward();
browser.visit("linkedin.com");
browser.displayStatus();
```

**Résultat attendu :**

- Page actuelle : `linkedin.com`
- Historique précédent : `google.com`
- Aucune page "suivante" (car `visit()` a vidé la pile forward)

---

## 📝 Micro-Exercice #2 : File d'Impression

Créez un système de gestion de file d'impression pour une imprimante partagée.

**Fonctionnalités requises :**

- Ajouter des documents à imprimer
- Imprimer le prochain document
- Annuler un document spécifique en attente
- Afficher tous les documents en attente

**Indications :**

- Utilisez une File pour maintenir l'ordre d'arrivée
- Pour annuler un document, vous devrez peut-être parcourir la file

**Squelette de code :**

```javascript
class PrintQueue {
  constructor() {
    this.queue = new TaskQueue();
  }

  // Ajouter un document à la file
  addDocument(document) {
    // TODO: Implémenter
  }

  // Imprimer le prochain document
  printNext() {
    // TODO: Implémenter
  }

  // Annuler un document par son ID
  cancelDocument(documentId) {
    // TODO: Implémenter
    // Astuce : Vous devrez créer une file temporaire
  }

  // Afficher tous les documents en attente
  displayQueue() {
    // TODO: Implémenter
  }
}

// Test
const printer = new PrintQueue();
printer.addDocument({ id: 1, name: "Rapport.pdf", pages: 10 });
printer.addDocument({ id: 2, name: "Presentation.pptx", pages: 25 });
printer.addDocument({ id: 3, name: "Facture.docx", pages: 2 });
printer.cancelDocument(2);
printer.printNext();
printer.displayQueue();
```

---

## 📝 Micro-Exercice #3 : Gestionnaire de Tâches avec Deadlines

Étendez le `PrioritizedTaskManager` pour gérer automatiquement les priorités en fonction des deadlines.

**Fonctionnalités requises :**

- Les tâches avec deadline aujourd'hui → Haute priorité
- Les tâches avec deadline cette semaine → Moyenne priorité
- Les tâches avec deadline plus tard → Basse priorité
- Afficher les tâches groupées par deadline

**Indications :**

- Ajoutez une méthode `categorizePriority(deadline)` qui retourne automatiquement la priorité
- Utilisez l'objet `Date` de JavaScript pour comparer les dates

**Squelette de code :**

```javascript
class SmartTaskManager extends PrioritizedTaskManager {
  // Déterminer la priorité en fonction de la deadline
  categorizePriority(deadlineString) {
    // TODO: Implémenter la logique de comparaison de dates
    // Retourner "Haute", "Moyenne", ou "Basse"
  }

  // Ajouter une tâche avec calcul automatique de priorité
  addSmartTask(task) {
    // TODO: Utiliser categorizePriority pour définir task.priority
    // Puis appeler this.addTask(task)
  }
}

// Test
const smartManager = new SmartTaskManager();
smartManager.addSmartTask({
  description: "Finir le projet X",
  deadline: "2024-01-15", // Aujourd'hui
  assignedTo: "Alice",
});

smartManager.addSmartTask({
  description: "Préparer la présentation",
  deadline: "2024-01-18", // Cette semaine
  assignedTo: "Bob",
});

smartManager.addSmartTask({
  description: "Réviser la documentation",
  deadline: "2024-02-01", // Mois prochain
  assignedTo: "Charlie",
});

smartManager.displayStatus();
```

---

## ❓ Quiz de Validation des Connaissances

### Question 1

Quelle structure de données est la plus appropriée pour implémenter un système Undo/Redo ?

- [ ] A) Une seule Pile
- [ ] B) Deux Piles
- [ ] C) Une seule File
- [ ] D) Deux Files

<details>
<summary>Voir la réponse</summary>

**Réponse : B) Deux Piles**

**Explication :** Nous avons besoin de deux piles :

- Une pile pour stocker l'historique des actions (pour Undo)
- Une pile pour stocker les actions annulées (pour Redo)

Le principe LIFO de la pile est parfait car on annule toujours la dernière action effectuée.

</details>

---

### Question 2

Dans le système de priorisation des tâches, si toutes les tâches haute priorité sont terminées, quelle file est vérifiée ensuite ?

- [ ] A) File basse priorité
- [ ] B) File moyenne priorité
- [ ] C) On choisit aléatoirement
- [ ] D) On attend de nouvelles tâches haute priorité

<details>
<summary>Voir la réponse</summary>

**Réponse : B) File moyenne priorité**

**Explication :** L'algorithme vérifie les files dans cet ordre :

1. Haute priorité (en premier)
2. Moyenne priorité (ensuite)
3. Basse priorité (en dernier)

Cela garantit que les tâches importantes sont toujours traitées avant les moins importantes.

</details>

---

### Question 3

Que se passe-t-il dans le système d'historique quand l'utilisateur effectue une nouvelle action après avoir annulé plusieurs actions ?

- [ ] A) La pile Redo est conservée
- [ ] B) La pile Redo est vidée
- [ ] C) La nouvelle action est ajoutée à la pile Redo
- [ ] D) Rien ne change

<details>
<summary>Voir la réponse</summary>

**Réponse : B) La pile Redo est vidée**

**Explication :** C'est un comportement standard dans les systèmes Undo/Redo :

- Quand une nouvelle action est effectuée après des annulations, on crée une nouvelle "branche" d'historique
- Les actions annulées précédemment ne peuvent plus être rétablies
- Cela évite les incohérences dans l'historique

Exemple :

1. Actions : A → B → C
2. Undo deux fois : A (pile Redo contient B, C)
3. Nouvelle action D : A → D (pile Redo est vidée)
</details>

---

### Question 4

Pourquoi utilise-t-on `shift()` pour retirer un élément d'une File mais `pop()` pour retirer d'une Pile ?

- [ ] A) C'est juste une convention de nommage
- [ ] B) `shift()` retire du début, `pop()` retire de la fin
- [ ] C) `shift()` est plus rapide que `pop()`
- [ ] D) Il n'y a pas de différence

<details>
<summary>Voir la réponse</summary>

**Réponse : B) `shift()` retire du début, `pop()` retire de la fin**

**Explication :**

- **File (FIFO)** : Le premier élément ajouté doit être le premier retiré → on retire du **début** avec `shift()`
- **Pile (LIFO)** : Le dernier élément ajouté doit être le premier retiré → on retire de la **fin** avec `pop()`

Illustration :

```
File : [1, 2, 3, 4] → shift() retire 1 (début)
Pile : [1, 2, 3, 4] → pop() retire 4 (fin)
```

**Note de performance :** `shift()` est plus lent que `pop()` car il nécessite de réindexer tous les éléments du tableau.

</details>

---

### Question 5

Dans une application de chat, les messages doivent être affichés dans l'ordre où ils ont été reçus. Quelle structure de données est la plus appropriée ?

- [ ] A) Pile
- [ ] B) File
- [ ] C) Tableau simple
- [ ] D) Les trois conviennent

<details>
<summary>Voir la réponse</summary>

**Réponse : B) File**

**Explication :**

- Les messages doivent être affichés dans l'ordre d'arrivée (premier reçu = premier affiché)
- C'est exactement le principe **FIFO** de la File
- Une Pile (LIFO) afficherait les messages dans l'ordre inverse

Même si un tableau simple peut fonctionner, une File offre une abstraction plus claire et évite les erreurs de manipulation.

</details>

---

## 📌 Récapitulatif en 7 Points Clés

### 1. Système Undo/Redo avec Piles

Utilisez **deux piles** : une pour l'historique des actions (Undo), une pour les actions annulées (Redo). Quand une nouvelle action est effectuée, la pile Redo est vidée pour éviter les incohérences.

### 2. Traitement Séquentiel avec Files

Utilisez une **file FIFO** pour traiter les éléments dans l'ordre d'arrivée. Idéal pour les notifications, files d'impression, et tout système où l'équité du traitement est importante.

### 3. Priorisation avec Plusieurs Files

Combinez **plusieurs files** (une par niveau de priorité) pour gérer des tâches de différentes urgences. Vérifiez les files dans l'ordre décroissant de priorité : Haute → Moyenne → Basse.

### 4. Complexités Temporelles

| Opération | Pile | File (shift) |
| --------- | ---- | ------------ |
| Ajouter   | O(1) | O(1)         |
| Retirer   | O(1) | O(n)         |

Pour les files, envisagez une implémentation avec pointeurs pour obtenir O(1) sur toutes les opérations.

### 5. Choisir la Bonne Structure

**Pile** : pour l'historique, navigation arrière, Undo/Redo (LIFO). **File** : pour le traitement séquentiel, files d'attente, notifications (FIFO). Le choix dépend de l'ordre de traitement souhaité.

### 6. Combiner les Structures

N'hésitez pas à **combiner** piles et files : navigateur web (2 piles + état actuel), gestionnaire de tâches priorisé (3 files), éditeur avec historique (2 piles + file de commandes).

### 7. Règle d'Or

**LIFO (Pile)** quand le dernier élément doit être traité en premier. **FIFO (File)** quand le premier élément doit être traité en premier. Analysez toujours l'ordre de traitement requis avant de choisir.

---

## ➡️ Prochaine Étape : Leçon 13

### Ce qui vous attend

Dans la prochaine leçon, **« Introduction au Tri : Pourquoi Ordonner les Données ? »**, vous allez entamer un nouveau module passionnant sur les techniques de tri.

**Vous découvrirez :**

- Pourquoi le tri est une opération fondamentale en informatique
- Les différents critères de comparaison des algorithmes de tri
- Quand et pourquoi ordonner les données améliore les performances
- Comment le tri prépare le terrain pour des algorithmes plus efficaces (comme la recherche binaire)

### Préparez-vous !

Le Module 3 sur les techniques de tri vous donnera des outils essentiels pour optimiser vos algorithmes. Comprendre le tri, c'est comprendre comment organiser l'information pour la traiter plus efficacement.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Stack vs Queue - Comparaison](https://www.youtube.com/results?search_query=stack+vs+queue) - Récapitulatif vidéo
- [MDN : Array.prototype.shift()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) - Documentation officielle
- [Stack Overflow : Implementing a Queue in JavaScript](https://stackoverflow.com/questions/1590247/how-do-you-implement-a-stack-and-a-queue-in-javascript) - Discussion communautaire

### Outils utiles

- **[MDN : Array.prototype.pop()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)** : Référence pour les opérations de pile
- **[Visualgo](https://visualgo.net/en/list)** : Visualisation des structures de données

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices
- Expérimenter avec votre propre gestionnaire de tâches en ajoutant des fonctionnalités

> 💡 **Conseil**
>
> La vraie maîtrise vient quand vous pouvez **combiner** les structures. Essayez d'implémenter un mini-projet personnel utilisant piles ET files : un éditeur de texte avec Undo/Redo, un gestionnaire de tâches, ou un simulateur de file d'attente. C'est en construisant que vous ancrez vraiment les concepts !

---

**Prêt pour la Leçon 13 ?** 🚀

Rendez-vous dans la prochaine leçon pour aborder les techniques de tri essentielles !

---

<div align="center">

**Leçon 12 sur 42 - Module 2 : Structures de Données Essentielles en JavaScript**

[⬅️ Leçon 11 : Files - Principe FIFO et Implémentation Basée sur Tableaux](./lecon-5-files-principe-fifo-implementation-tableaux.md) | [Retour au sommaire](./README.md) | [Leçon 13 : Introduction au Tri - Pourquoi Ordonner les Données ? ➡️](../module-3/lecon-1-introduction-tri-pourquoi-ordonner-donnees.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
