##### Leçon 1 sur 42

# Qu'est-ce qu'un algorithme ? Définir les étapes de résolution d'un problème

**Module 1** : Fondements des algorithmes et révision de JavaScript

---

## 🎯 Objectifs d'apprentissage

À la fin de cette leçon, vous serez capable de :

- Définir ce qu'est un algorithme et expliquer son importance en programmation
- Identifier et expliquer les 5 caractéristiques essentielles d'un algorithme
- Appliquer la pensée algorithmique pour décomposer un problème en étapes logiques
- Concevoir des algorithmes simples pour résoudre des problèmes du quotidien
- Distinguer un algorithme valide d'une simple liste d'instructions

---

### ⏱️ Durée estimée : 1h30 - 2h

---

## 📚 Prérequis

Aucun prérequis technique nécessaire ! Cette leçon est accessible à tous.

---

## 🚀 Introduction : Les algorithmes sont partout !

Bienvenue à la première leçon du cours **« Algorithmes : des fondamentaux aux concepts avancés avec JavaScript »** !

**Question pour vous :** Avez-vous déjà suivi une recette de cuisine ? Utilisé un GPS ? Préparé votre café du matin ?

Si oui, félicitations ! Vous avez déjà exécuté des algorithmes sans le savoir. 🎉

Dans le monde de l'informatique et de la programmation, les algorithmes constituent **la base sur laquelle reposent tous les logiciels**. Il ne s'agit pas seulement de formules mathématiques complexes réservées aux chercheurs ; en réalité, vous rencontrez et utilisez des algorithmes tous les jours sans même vous en rendre compte.

Que ce soit pour :

- Rechercher un itinéraire sur une carte
- Choisir vos vêtements en fonction de la météo
- Faire défiler votre fil d'actualité sur les réseaux sociaux
- Écouter des recommandations musicales personnalisées

...vous exécutez constamment une série d'étapes pour atteindre un objectif.

Cette leçon vous permettra de **comprendre ce qu'est un algorithme**, d'en définir les caractéristiques essentielles et d'illustrer en quoi **la pensée algorithmique** est une compétence fondamentale pour résoudre n'importe quel problème, que ce soit dans la vie quotidienne ou en programmation.

> **Point Clé**
>
> Comprendre ce concept en profondeur est la première étape cruciale pour devenir un programmeur plus compétent et créer des logiciels efficaces.

---

## 📖 Qu'est-ce qu'un algorithme exactement ?

### Définition simple

À la base, un algorithme est simplement une **séquence bien définie d'étapes ou d'instructions** utilisées pour résoudre un problème spécifique ou effectuer un calcul.

Considérez-le comme :

- Une **recette détaillée** (avec ingrédients et étapes)
- Un **manuel d'assemblage** (pour monter un meuble)
- Un **guide de navigation** (pour aller d'un point A à un point B)

Lorsqu'il est suivi **à la lettre**, il mène systématiquement au résultat souhaité.

### Formule simple

```
ALGORITHME = ENTRÉES + ÉTAPES LOGIQUES → SORTIE
```

L'objectif est de **transformer une entrée donnée en une sortie souhaitée** en suivant ces étapes précises.

---

## 🔑 Les 5 Caractéristiques Essentielles d'un Algorithme

Pour qu'un ensemble d'instructions soit considéré comme un **véritable algorithme**, il doit posséder ces 5 caractéristiques clés :

### 1. Entrées bien définies

Un algorithme doit clairement spécifier le **type de données ou d'informations** qu'il s'attend à recevoir au début.

**Pourquoi ?** Sans savoir par quoi vous commencez, vous ne pouvez pas définir les étapes nécessaires à son traitement.

**Exemple :**

- Algorithme de tri → Entrée : une liste de nombres
- Recette de gâteau → Entrée : farine, œufs, sucre, beurre

---

### 2. Sorties bien définies

Il doit également préciser clairement quel **type de résultat ou d'information** il produira une fois terminé.

**Pourquoi ?** Vous devez savoir ce que vous essayez d'accomplir pour considérer le problème comme résolu.

**Exemple :**

- Algorithme de tri → Sortie : liste triée par ordre croissant
- Recette de gâteau → Sortie : un gâteau cuit prêt à être dégusté

---

### 3. Finitude

Un algorithme doit **s'arrêter après un nombre fini d'étapes** pour toutes les entrées valides. Il ne peut pas s'exécuter indéfiniment ; il doit finir par s'arrêter.

**Pourquoi ?** Un processus qui ne se termine jamais n'est pas un algorithme, c'est une boucle infinie !

**Exemple valide :** Une recette de 12 étapes qui se termine
**Exemple invalide :** "Continuez à ajouter du sel jusqu'à ce que ce soit parfait" (subjectif et potentiellement infini)

---

### 4. Absence d'ambiguïté (Précision)

Chaque étape de l'algorithme doit être **claire, précise et sans ambiguïté**. Il ne doit y avoir aucune place pour l'interprétation, et chaque instruction ne doit avoir qu'**une seule signification**.

**Pourquoi ?** Toute personne (ou machine) suivant l'algorithme doit arriver au même résultat.

**Exemple ambigu :** "Mélangez les ingrédients jusqu'à ce qu'ils soient bien incorporés"

- Problème : Qu'est-ce que "bien incorporés" ? Pendant combien de temps ?

**Exemple précis :** "Mélangez les ingrédients pendant exactement 2 minutes à vitesse moyenne"

- Clair et mesurable

---

### 5. Efficacité (Faisabilité)

Chaque étape doit être **suffisamment simple** pour pouvoir être réalisée, au moins en principe, par un être humain à l'aide d'un crayon et d'une feuille de papier, ou par une machine.

**Pourquoi ?** L'opération doit être réalisable concrètement.

**Exemple inefficace :** "Trouvez le secret du bonheur éternel"

- Problème : Il n'existe pas de moyen clair et précis de réaliser cette étape

**Exemple efficace :** "Additionnez les deux nombres"

- Opération basique et réalisable

---

## 📊 Tableau Récapitulatif des 5 Caractéristiques

| Caractéristique           | Question à se poser                   | Exemple valide               | Exemple invalide            |
| ------------------------- | ------------------------------------- | ---------------------------- | --------------------------- |
| **Entrées bien définies** | Quelles données en entrée ?           | Liste de nombres `[5, 3, 8]` | "Des données"               |
| **Sorties bien définies** | Quel résultat attendu ?               | Liste triée `[3, 5, 8]`      | "Un bon résultat"           |
| **Finitude**              | L'algorithme se termine-t-il ?        | 10 étapes précises           | "Répétez indéfiniment"      |
| **Absence d'ambiguïté**   | Les instructions sont-elles claires ? | "Comparez A et B"            | "Mélangez bien"             |
| **Efficacité**            | Les étapes sont-elles réalisables ?   | "Additionnez 2 + 3"          | "Trouvez le sens de la vie" |

---

## 📝 Micro-Exercice #1 : Identifier les Caractéristiques

**Instructions :** Pour chacune des instructions suivantes, identifiez quelle(s) caractéristique(s) d'un algorithme elle pourrait violer :

1. "Ajoutez du sel jusqu'à ce que ça goûte bon"
2. "Parcourez tous les nombres possibles pour trouver le plus grand"
3. "Divisez le nombre par zéro"
4. "Si la condition est vraie, faites quelque chose d'approprié"

<details>
<summary>💡 Voir les réponses</summary>

1. **Absence d'ambiguïté** - "ça goûte bon" est subjectif
2. **Finitude** - "tous les nombres possibles" est infini
3. **Efficacité** - Division par zéro impossible
4. **Absence d'ambiguïté** - "quelque chose d'approprié" n'est pas précis

</details>

---

## 🎯 Exemple Concret #1 : Préparer une Tasse de Café

Illustrons ces caractéristiques à l'aide d'un exemple simple et quotidien : **préparer une tasse de café**.

### Définition du problème

- **Problème :** Vous voulez une tasse de café chaud
- **Entrées :** Café moulu, eau, cafetière (ou machine à café), tasse, sucre (optionnel), lait (optionnel)
- **Sortie :** Une tasse de café chaud préparée

---

### Algorithme : Comment préparer une tasse de café

```
DÉBUT

1. Remplir le réservoir d'eau
   └─> Verser 200ml d'eau fraîche dans le réservoir de la cafetière

2. Ajouter le café moulu
   └─> Placer 1 cuillère à soupe de café moulu dans le filtre

3. Placer le filtre dans la cafetière
   └─> Insérer le porte-filtre contenant le café dans son emplacement

4. Allumer la cafetière
   └─> Appuyer sur le bouton "Marche" ou "Start"

5. Attendre la fin du cycle
   └─> Observer le voyant lumineux ou écouter le signal sonore indiquant que le café est prêt

6. Verser le café dans la tasse
   └─> Verser délicatement le café de la cafetière dans votre tasse

7. [OPTIONNEL] Ajouter du sucre
   └─> Si désiré, ajouter 1 ou 2 cuillères à café de sucre et remuer pendant 10 secondes

8. [OPTIONNEL] Ajouter du lait
   └─> Si désiré, ajouter 20ml de lait et remuer pendant 10 secondes

9. Servir
   └─> Le café est prêt à être dégusté

FIN
```

---

### Vérification des 5 caractéristiques

| Caractéristique         | Validation                                                                                  |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| **Entrées**             | Clairement définies (eau, café moulu, tasse, etc.)                                          |
| **Sorties**             | Clairement définies (une tasse de café chaud)                                               |
| **Finitude**            | Oui, il y a 9 étapes maximum, l'algorithme se termine                                       |
| **Absence d'ambiguïté** | Chaque étape est claire ; pas de confusion entre "remplir le réservoir" et "verser le café" |
| **Efficacité**          | Chaque étape est une action basique et réalisable                                           |

---

## 🗺️ Exemple Concret #2 : Trouver un itinéraire avec GPS

Réfléchissez à la manière dont une **application GPS** (comme Google Maps, Waze) vous aide à vous rendre d'un endroit à un autre.

### Définition du problème

- **Problème :** Vous devez vous rendre de votre emplacement actuel à une destination
- **Entrées :**
  - Vos coordonnées géographiques actuelles (latitude, longitude)
  - Les coordonnées de votre destination souhaitée
  - Données actuelles sur le trafic en temps réel
  - Données cartographiques du réseau routier
  - Limitations de vitesse
- **Sortie :**
  - Une série d'indications détaillées (turn-by-turn)
  - Une heure d'arrivée estimée
  - Une représentation visuelle de l'itinéraire sur la carte

---

### Algorithme (simplifié haut niveau) : Navigation GPS

```
DÉBUT Navigation GPS

1. Recevoir la position actuelle
   └─> Obtenir les coordonnées GPS actuelles de l'utilisateur via satellite

2. Recevoir la destination
   └─> Obtenir les coordonnées de la destination saisie par l'utilisateur

3. Accéder aux données cartographiques
   └─> Charger les données de la carte : routes, intersections, sens uniques, obstacles

4. Identifier les chemins possibles
   └─> Utiliser un algorithme de recherche de chemin pour trouver tous les itinéraires
       reliant la position actuelle à la destination

5. Évaluer les métriques pour chaque chemin
   Pour chaque itinéraire possible :
   ├─> Calculer la distance totale (en km)
   ├─> Estimer le temps de trajet (en tenant compte des limitations de vitesse)
   ├─> Intégrer les données de trafic en temps réel
   └─> Compter le nombre de virages et changements de direction

6. Sélectionner le chemin optimal
   └─> Choisir l'itinéraire qui minimise le temps de trajet
       (ou la distance selon les préférences utilisateur)

7. Générer des instructions détaillées
   └─> Convertir l'itinéraire en instructions claires :
       "Dans 200 mètres, tournez à gauche sur Avenue des Champs-Élysées"

8. Afficher l'itinéraire
   └─> Présenter visuellement l'itinéraire sur la carte avec ligne bleue

9. Fournir des conseils en temps réel
   En continu pendant le trajet :
   ├─> Mettre à jour la position de l'utilisateur
   ├─> Annoncer les virages à venir (audio + visuel)
   ├─> Surveiller les nouvelles données de trafic
   └─> Recalculer l'itinéraire si l'utilisateur dévie ou si un meilleur chemin apparaît

10. Arriver à destination
    └─> Terminer le guidage et afficher "Vous êtes arrivé"

FIN Navigation GPS
```

---

### Analyse de cet algorithme

Cet exemple, bien que **simplifié**, montre clairement comment un **problème complexe** est décomposé en une série d'**étapes bien définies, finies et efficaces** afin d'obtenir un résultat spécifique à partir d'entrées spécifiques.

> 📌 **À retenir**
>
> Même les applications les plus sophistiquées que vous utilisez quotidiennement ne sont que des algorithmes qui suivent des étapes logiques !

---

## 📝 Micro-Exercice #2 : Décomposer un Problème

**Instructions :** Choisissez l'une des activités suivantes et écrivez un algorithme simple (5-8 étapes) :

1. Se brosser les dents
2. Retirer de l'argent à un distributeur automatique (ATM)
3. Chercher un mot dans un dictionnaire papier

Assurez-vous que votre algorithme respecte les 5 caractéristiques !

---

## 🧮 Scénario Hypothétique : Trouver le Plus Petit Nombre dans une Liste

Imaginez que vous ayez une liste de nombres écrits sur un bout de papier, et que vous souhaitiez trouver le plus petit d'entre eux.

### Définition du problème

- **Problème :** Identifier la valeur minimale dans une liste donnée de nombres
- **Entrées :** Une liste de nombres (par exemple, `[5, 12, 3, 9, 1]`)
- **Sortie :** Le plus petit nombre de la liste d'entrée (par exemple, `1`)

---

### Algorithme : Trouver le Plus Petit Nombre

```
DÉBUT TrouverPlusPetitNombre

ENTRÉE : liste de nombres [5, 12, 3, 9, 1]

1. Initialiser la variable "plusPetit"
   └─> plusPetit = premier nombre de la liste
   └─> Exemple : plusPetit = 5

2. Pour chaque nombre restant dans la liste :

   a. Prendre le nombre suivant
      └─> Exemple : nombre_actuel = 12

   b. Comparer nombre_actuel avec plusPetit
      └─> Si nombre_actuel < plusPetit
          ALORS plusPetit = nombre_actuel

   c. Répéter jusqu'à avoir parcouru tous les nombres

3. Afficher le résultat
   └─> Le nombre dans plusPetit est le minimum de la liste

SORTIE : 1

FIN TrouverPlusPetitNombre
```

---

### Déroulement pas à pas (Trace d'exécution)

Voici comment l'algorithme s'exécute étape par étape avec la liste `[5, 12, 3, 9, 1]` :

| Étape              | Nombre actuel | plusPetit (avant) | Comparaison      | plusPetit (après) |
| ------------------ | ------------- | ----------------- | ---------------- | ----------------- |
| Initialisation     | 5             | -                 | -                | **5**             |
| 1                  | 12            | 5                 | 12 < 5 ? **Non** | **5**             |
| 2                  | 3             | 5                 | 3 < 5 ? **Oui**  | **3**             |
| 3                  | 9             | 3                 | 9 < 3 ? **Non**  | **3**             |
| 4                  | 1             | 3                 | 1 < 3 ? **Oui**  | **1**             |
| **Résultat final** |               |                   |                  | **1**             |

---

### Vérification des caractéristiques

Ce problème abstrait présente également **toutes les caractéristiques d'un algorithme** :

- **Entrées claires** : Une liste de nombres
- **Sortie souhaitée claire** : Un seul nombre (le minimum)
- **Nombre fini d'étapes** : On parcourt chaque nombre exactement une fois
- **Instructions sans ambiguïté** : Chaque comparaison est mathématiquement précise
- **Chaque étape est efficace** : Comparer deux nombres est une opération basique

---

## 🛠️ Le Processus de Résolution de Problèmes avec les Algorithmes

La **pensée algorithmique** est essentiellement une approche structurée de la résolution de problèmes. Avant même de commencer à réfléchir à l'écriture d'un code, vous devez définir systématiquement le problème et élaborer une stratégie pour le résoudre.

Ce processus peut être décomposé en **3 étapes clés** :

---

### Étape 1️ : Comprendre le Problème

> **C'est l'étape la plus cruciale et souvent négligée !**

Vous ne pouvez pas résoudre un problème que vous ne comprenez pas parfaitement.

#### Questions à se poser :

**a) Identifier les entrées**

- Quelles données ou informations votre algorithme recevra-t-il ?
- De quel type sont-elles ? (nombres, texte, liste, etc.)
- Y a-t-il des contraintes ?
  - Exemple : les nombres doivent être positifs, les listes ne peuvent pas être vides

**b) Identifier les sorties**

- Quel est le résultat souhaité ?
- Quel format doit-il avoir ?
- Que se passe-t-il si l'entrée n'est pas valide ou s'il n'y a pas de solution ?

**c) Clarifier les contraintes et les cas limites**

- Quelles sont les limites du problème ?
- Y a-t-il des conditions particulières ?
- Exemples de questions à se poser :
  - "Si je trie des nombres, que se passe-t-il si la liste ne contient qu'un seul nombre ?"
  - "Ou aucun nombre du tout ?"
  - "Que se passe-t-il s'il y a des nombres en double ?"

**d) Décomposer les problèmes complexes**

- Pour les problèmes plus importants, essayez de les diviser en **sous-problèmes** plus petits et plus faciles à gérer
- Cela rend la tâche globale moins intimidante et révèle souvent des solutions plus simples

---

### Étape 2️ : Concevoir l'Algorithme

Une fois que vous avez **bien compris le problème**, vous pouvez commencer à élaborer un plan pour le résoudre. C'est là que la créativité et la pensée logique entrent en jeu.

#### Actions à effectuer :

**a) Brainstorming d'approches**

- Réfléchissez à différentes façons d'aborder le problème
- Il existe rarement un seul algorithme correct !

**b) Décrire les étapes dans un langage simple**

- Avant de vous préoccuper de la syntaxe spécifique du langage de programmation, décrivez vos étapes en **langage clair** (français naturel)
- Concentrez-vous sur la **logique**, pas sur le code
- Cela se fait souvent à l'aide de **"pseudocode"** (un mélange de langage naturel et de structure semblable à du code) ou d'**organigrammes**

**c) Penser au traitement des données**

- Comment allez-vous stocker et manipuler les données d'entrée ?
- (Même si nous n'aborderons pas encore les structures de données spécifiques comme les tableaux ou les listes chaînées, réfléchissez de manière générale à l'organisation des données)

**d) Détailler la logique étape par étape**

- Précisez la séquence d'opérations nécessaires pour transformer l'entrée en sortie

---

### Étape 3️ : Affiner l'Algorithme

Après avoir conçu une approche initiale, il est important de la **revoir et de l'améliorer**.

#### Actions d'amélioration :

**a) Tester mentalement avec des exemples**

- Parcourez votre algorithme mentalement en utilisant différentes entrées :
  - Cas typiques (normaux)
  - Cas limites (edge cases)
  - Entrées potentiellement problématiques
- Produit-il le résultat correct à chaque fois ?

**b) Simplifier les étapes**

- Certaines étapes peuvent-elles être combinées ou supprimées sans affecter le résultat ?
- Existe-t-il un moyen plus clair d'exprimer une instruction ?

**c) Envisager des alternatives**

- Existe-t-il d'autres moyens, peut-être plus simples ou plus directs, d'obtenir le même résultat ?
- **Note importante :** Pour l'instant, ne pensez pas encore à l'efficacité ou aux "meilleurs" algorithmes en termes de vitesse ou de mémoire (cela viendra dans les leçons suivantes)
- Concentrez-vous sur la **clarté logique** et l'**exactitude**

**d) Garantir l'absence d'ambiguïté**

- Vérifiez que chaque instruction est **parfaitement claire** et ne laisse aucune place à une mauvaise interprétation

---

## 📊 Schéma Récapitulatif : Les 3 Étapes de la Pensée Algorithmique

```
┌─────────────────────────────────────────────────────────────┐
│                  RÉSOLUTION DE PROBLÈMES                    │
│                   AVEC LES ALGORITHMES                      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
        ┌──────────────────────────────────┐
        │   1️   COMPRENDRE LE PROBLÈME     │
        │                                  │
        │   • Identifier les entrées       │
        │   • Identifier les sorties       │
        │   • Clarifier les contraintes    │
        │   • Décomposer si complexe       │
        └──────────────┬───────────────────┘
                       │
                       ▼
        ┌─────────────────────────────────────┐
        │   2️   CONCEVOIR L'ALGORITHME        │
        │                                     │
        │  • Brainstorming d'approches        │
        │  • Écrire en langage simple         │
        │  • Penser au traitement des données │
        │  • Détailler la logique étape/étape │
        └──────────────┬──────────────────────┘
                       │
                       ▼
        ┌─────────────────────────────────────┐
        │   3️   AFFINER L'ALGORITHME          │
        │                                     │
        │  • Tester avec des exemples         │
        │  • Simplifier les étapes            │
        │  • Envisager des alternatives       │
        │  • Garantir la clarté               │
        └──────────────┬──────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │   ALGORITHME   │
              │     FINAL      │
              └────────────────┘
```

---

## 💼 Exemple Concret : Traitement des Commandes Clients pour une Boutique en Ligne

Considérons un scénario pratique pour une petite boutique en ligne. Le propriétaire de la boutique a besoin d'un processus pour traiter les commandes.

### Définition du problème

- **Problème :** Traiter la commande en ligne d'un client, de sa soumission à son expédition
- **Entrées :**
  - Coordonnées du client (nom, adresse de livraison)
  - Articles commandés (références produit, quantités)
  - Informations de paiement (coordonnées bancaires)
  - Niveaux de stock actuels dans l'inventaire
- **Sortie :**
  - Commande confirmée
  - Inventaire mis à jour
  - Étiquette d'expédition générée
  - Paiement traité avec succès

---

### 1️ Comprendre le Problème : Questions Importantes

Avant de concevoir l'algorithme, identifions les **cas limites** et **situations problématiques** :

| Question                                                                       | Impact sur l'algorithme                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| Que faire si un article est en **rupture de stock** ?                          | Il faut informer le client, ne pas expédier, proposer remboursement ou réapprovisionnement |
| Que faire en cas d'**échec du paiement** ?                                     | Il faut informer le client, suspendre la commande, ne pas expédier                         |
| Comment gérer **plusieurs articles** dans une même commande ?                  | Traiter chaque article individuellement pour la vérification d'inventaire                  |
| Qu'en est-il des **frais d'expédition** ?                                      | Les calculer en fonction du poids et de la destination                                     |
| Que faire si le client veut **annuler après paiement** mais avant expédition ? | Prévoir un sous-algorithme "Annulation de commande"                                        |

---

### 2️ Concevoir l'Algorithme (Haut Niveau)

```
DÉBUT TraitementCommande

ENTRÉES :
  - infosClient (nom, adresse)
  - listeArticles (tableau d'objets avec référence et quantité)
  - infoPaiement (données carte bancaire)
  - inventaireActuel (stock disponible)

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 1 : Recevoir les détails de la commande            │
└──────────────────────────────────────────────────────────┘
   └─> Récupérer infosClient, listeArticles, infoPaiement

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 2 : Vérifier l'inventaire                          │
└──────────────────────────────────────────────────────────┘
   POUR CHAQUE article DANS listeArticles FAIRE

      a. Vérifier si quantité commandée <= stock disponible

      b. SI stock insuffisant ALORS
         ├─> Marquer l'article comme "RUPTURE DE STOCK"
         ├─> Envoyer notification au client
         └─> Demander action client (supprimer / substituer / attendre)

      c. SINON
         └─> Marquer l'article comme "DISPONIBLE"

   FIN POUR

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 3 : Traiter le paiement                            │
└──────────────────────────────────────────────────────────┘
   a. Calculer le montant total (articles + frais d'expédition)

   b. Tenter de débiter le moyen de paiement

   c. SI paiement échoue ALORS
      ├─> Envoyer notification au client
      ├─> Suspendre la commande
      └─> Demander nouveau moyen de paiement
      └─> ARRÊTER (ne pas continuer)

   d. SINON
      └─> Paiement confirmé, continuer

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 4 : Mettre à jour l'inventaire                     │
└──────────────────────────────────────────────────────────┘
   SI (stock suffisant ET paiement réussi) ALORS
      POUR CHAQUE article DANS listeArticles FAIRE
         └─> stock[article] = stock[article] - quantité commandée
      FIN POUR
   FIN SI

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 5 : Générer l'étiquette d'expédition               │
└──────────────────────────────────────────────────────────┘
   └─> Créer étiquette avec :
       - Adresse de livraison
       - Numéro de commande
       - Code-barres de suivi

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 6 : Préparer les articles                         │
└──────────────────────────────────────────────────────────┘
   └─> Emballer les articles dans un colis
   └─> Coller l'étiquette d'expédition

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 7 : Expédier la commande                          │
└──────────────────────────────────────────────────────────┘
   └─> Remettre le colis au transporteur (La Poste, Chronopost, etc.)

┌──────────────────────────────────────────────────────────┐
│ ÉTAPE 8 : Envoyer la confirmation                       │
└──────────────────────────────────────────────────────────┘
   └─> Envoyer email au client avec :
       - Confirmation de commande
       - Numéro de suivi
       - Date de livraison estimée

SORTIE : Commande traitée avec succès

FIN TraitementCommande
```

---

### 3️ Affiner l'Algorithme : Considérations

**Questions d'amélioration :**

1. **Séquentialité vs Parallélisation**
   - Les étapes 2 (vérification inventaire) et 3 (paiement) peuvent-elles être parallélisées ?
   - Non ! Le paiement doit attendre la confirmation du stock disponible

2. **Gestion des erreurs**
   - Que faire si l'étiquette d'expédition ne s'imprime pas ?
   - Que faire si le transporteur refuse le colis ?

3. **Extensions futures**
   - Ajouter un sous-algorithme "Annulation de commande"
   - Ajouter un sous-algorithme "Gestion des retours"

---

### Leçon de cet exemple

Ce processus montre comment passer d'un **objectif général** ("traiter une commande") à des **étapes spécifiques et logiques**, en anticipant les problèmes potentiels qui pourraient survenir en cours de route.

> 📌 **Point Clé**
>
> Un bon algorithme ne se contente pas de gérer le "cas parfait", il anticipe et gère également les cas d'erreur et les situations exceptionnelles !

---

## 📝 Micro-Exercice #3 : Appliquer les 3 Étapes

**Problème :** Concevoir un algorithme pour rechercher un livre dans une bibliothèque en ligne.

**Instructions :**

1. Appliquez l'**Étape 1** (Comprendre le problème) :
   - Identifiez les entrées
   - Identifiez les sorties
   - Listez 3 cas limites potentiels

2. Appliquez l'**Étape 2** (Concevoir) :
   - Écrivez un algorithme de 5-8 étapes en langage simple

3. Appliquez l'**Étape 3** (Affiner) :
   - Identifiez une étape qui pourrait être ambiguë et clarifiez-la

<details>
<summary>💡 Voir un exemple de solution</summary>

**Étape 1 - Comprendre :**

- Entrées : Titre du livre (texte)
- Sorties : Liste des livres correspondants (avec auteur, ISBN, disponibilité)
- Cas limites :
  1. Aucun livre trouvé
  2. Plusieurs éditions du même titre
  3. Titre mal orthographié

**Étape 2 - Concevoir :**

```
1. Recevoir le titre saisi par l'utilisateur
2. Rechercher dans la base de données tous les livres dont le titre contient le texte saisi
3. Pour chaque livre trouvé, vérifier sa disponibilité
4. Trier les résultats par pertinence (correspondance exacte en premier)
5. Afficher la liste des résultats avec titre, auteur, disponibilité
6. Si aucun résultat, proposer des suggestions de titres similaires
```

**Étape 3 - Affiner :**

- Étape 2 ambiguë : "contient le texte saisi"
- Clarification : "Rechercher en ignorant la casse (majuscules/minuscules) et les accents"

</details>

---

## 🌟 Pourquoi les Algorithmes Sont-ils Importants ?

Les algorithmes constituent le fondement de l'informatique et de la résolution de problèmes pour plusieurs raisons cruciales :

### 1. Automatisation

Les algorithmes nous permettent d'**automatiser des tâches complexes**, en les exécutant rapidement, avec précision et de manière répétée, **sans intervention humaine**.

**Exemple :**

- C'est ainsi que les ordinateurs peuvent effectuer des **millions de calculs par seconde**
- Ou trier de **grandes quantités de données** instantanément

---

### 2. Clarté et Communication

Un algorithme bien défini fournit un moyen **clair et sans ambiguïté** de décrire une solution.

**Pourquoi c'est essentiel ?**

- Vital pour les **équipes de développeurs** qui travaillent ensemble
- Permet de s'assurer que tout le monde comprend comment un problème particulier est résolu
- Facilite la **documentation** et la **maintenance** du code

---

### 3. Reproductibilité

Si un algorithme est **correctement conçu**, il devrait produire le **même résultat pour la même entrée** à chaque fois, peu importe qui l'exécute ou sur quelle machine compatible.

**Importance :**

- Cette **cohérence** est fondamentale pour la fiabilité d'un logiciel
- Permet de **détecter les bugs** facilement (si le résultat change, il y a un problème)

---

### 4. Fondation pour l'Efficacité

Bien que nous ne parlions pas encore d'efficacité dans cette leçon, comprendre la nature **étape par étape** des algorithmes est une **condition préalable** à l'évaluation ultérieure de la qualité d'un algorithme.

**Ce qui viendra ensuite :**

- Un algorithme clair peut être **analysé**, **amélioré** et **optimisé**
- On pourra comparer différentes approches et choisir la meilleure

---

### 5. Améliorer Vos Compétences en Codage

Pour vous, en tant qu'**apprenant**, maîtriser les algorithmes signifie développer une approche **systématique et logique** pour décomposer les problèmes.

**Bénéfices concrets :**

- Améliore considérablement votre capacité à écrire un code clair, correct et efficace
- Vous apprend à **penser comme un ordinateur**, étape par étape
- Développe votre capacité de **résolution de problèmes** en général
- Vous rend plus **autonome** face à de nouveaux défis

---

### 6. Application Universelle

Les algorithmes **ne se limitent pas aux ordinateurs**. Ils constituent la logique sous-jacente de presque tous les processus que nous suivons :

**Exemples dans différents domaines :**

- **Fabrication** : Chaînes d'assemblage automobile, processus de qualité
- **Médecine** : Protocoles de diagnostic, arbres de décision médicale
- **Cuisine** : Recettes professionnelles standardisées
- **Finance** : Calcul d'intérêts, algorithmes de trading
- **Éducation** : Méthodes pédagogiques structurées

> **Point Clé**
>
> Comprendre les algorithmes fournit un **cadre puissant** pour analyser et résoudre des problèmes dans **n'importe quel domaine** !

---

## 💪 Exercices et Activités Pratiques

Pour consolider votre compréhension des algorithmes en tant qu'étapes de résolution de problèmes, essayez ces activités :

---

### Exercice 1 : Algorithme des Tâches Quotidiennes

**Objectif :** Appliquer la pensée algorithmique à une activité familière

**Instructions :**

1. Choisissez **une tâche quotidienne** que vous effectuez régulièrement :
   - Préparer le petit-déjeuner
   - Vous préparer pour aller au travail/à l'école
   - Faire la lessive
   - Préparer un sac pour un voyage

2. Écrivez un **algorithme étape par étape** en langage clair pour cette tâche

3. Assurez-vous que vos étapes sont :
   - Claires et non ambiguës
   - Limitées en nombre (l'algorithme se termine)
   - Efficaces (réalisables)

4. Identifiez clairement :
   - Les **entrées** pour la tâche choisie
   - Les **sorties** (résultat final)

5. **Auto-réflexion :**
   - Si quelqu'un d'autre suivait vos instructions à la lettre, obtiendrait-il le résultat souhaité ?
   - Y a-t-il des hypothèses cachées que vous avez faites ?

---

### Exercice 2 : Algorithme de Calcul Simple (Sans Code !)

**Objectif :** Concevoir des algorithmes pour des problèmes computationnels simples

#### Problème 1 : Compter les Voyelles

Décrivez un algorithme permettant de **compter le nombre de voyelles** (a, e, i, o, u, y) dans un mot donné (sans distinction majuscules/minuscules).

- **Entrée :** Un seul mot (par exemple, "Algorithme")
- **Sortie :** Un nombre représentant le compte (par exemple, 4)

**Consigne :** Écrivez les étapes **sans utiliser la syntaxe d'un langage de programmation**. Concentrez-vous sur le déroulement logique.

<details>
<summary>💡 Voir un exemple de solution</summary>

```
DÉBUT CompterVoyelles

ENTRÉE : mot = "Algorithme"

1. Initialiser compteur = 0

2. Définir liste_voyelles = [a, e, i, o, u, y]

3. Convertir le mot en minuscules
   └─> mot = "algorithme"

4. Pour chaque lettre dans le mot :
   a. Vérifier si la lettre est dans liste_voyelles
   b. SI oui ALORS
      └─> compteur = compteur + 1

5. Afficher compteur

SORTIE : 4

FIN CompterVoyelles
```

</details>

---

#### Problème 2 : Pair ou Impair

Décrivez un algorithme permettant de **déterminer si un nombre donné est pair ou impair**.

- **Entrée :** Un nombre entier (par exemple, 7)
- **Sortie :** "Pair" ou "Impair"

<details>
<summary>💡 Voir un exemple de solution</summary>

```
DÉBUT PairOuImpair

ENTRÉE : nombre = 7

1. Calculer le reste de la division de nombre par 2
   └─> reste = nombre modulo 2
   └─> reste = 7 modulo 2 = 1

2. SI reste égale 0 ALORS
   └─> Afficher "Pair"
   SINON
   └─> Afficher "Impair"

SORTIE : "Impair"

FIN PairOuImpair
```

</details>

---

### Exercice 3 : Analyse de Système du Monde Réel

**Objectif :** Décomposer un système existant en étapes algorithmiques

**Problème :** Réfléchissez à la manière dont un **système de bibliothèque en ligne** pourrait fonctionner lorsque vous recherchez un livre.

**Tâche :**

1. Définissez les **entrées**, les **sorties** et les **principales étapes** d'un algorithme que le système de bibliothèque suivrait lorsque vous :
   - Tapez le titre d'un livre dans sa barre de recherche
   - Appuyez sur "Entrée"

2. **Que se passe-t-il en coulisses ?** Décrivez le processus en 8-10 étapes

3. **Envisagez les cas limites potentiels :**
   - Que faire si le livre est introuvable ?
   - Que faire s'il existe plusieurs éditions ?
   - Que faire si le titre est mal orthographié ?

---

## ✅ Quiz de Validation des Connaissances

Testez votre compréhension de cette leçon avec ce quiz !

---

### Question 1

**Quelle est la définition principale d'un algorithme en informatique et en programmation ?**

- [ ] A. Une formule mathématique complexe utilisée par les chercheurs avancés
- [ ] B. Une séquence bien définie d'étapes ou d'instructions utilisées pour résoudre un problème spécifique ou effectuer un calcul
- [ ] C. Un ensemble de commandes aléatoires qu'un ordinateur exécute pour générer une sortie
- [ ] D. Une description en langage naturel d'un énoncé de problème

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

Un algorithme est une séquence bien définie d'étapes ou d'instructions pour résoudre un problème spécifique.

</details>

---

### Question 2

**Parmi les éléments suivants, lesquels sont essentiels pour qu'un ensemble d'instructions soit considéré comme un véritable algorithme ? (Plusieurs réponses possibles)**

- [ ] A. Il doit se terminer après un nombre fini d'étapes pour toutes les entrées valides
- [ ] B. Il doit toujours produire un résultat unique, même pour des entrées différentes
- [ ] C. Chaque étape doit être claire, précise et sans ambiguïté
- [ ] D. Il doit clairement préciser le type de données qu'il s'attend à recevoir au début

<details>
<summary>Voir la réponse</summary>

**Réponses : A, C, D**

Les 3 caractéristiques essentielles parmi les 5 :

- Finitude (A)
- Absence d'ambiguïté (C)
- Entrées bien définies (D)

L'option B est fausse : un algorithme peut produire des sorties différentes pour des entrées différentes.

</details>

---

### Question 3

**Dans le contexte des caractéristiques des algorithmes, quelle affirmation décrit le mieux l'"efficacité" (faisabilité) ?**

- [ ] A. L'algorithme doit produire un résultat utile ou bénéfique pour l'utilisateur
- [ ] B. Chaque étape doit être suffisamment simple et réalisable par un être humain à l'aide d'un crayon et d'une feuille de papier, ou par une machine
- [ ] C. L'algorithme doit être capable de résoudre simultanément plusieurs problèmes sans rapport entre eux
- [ ] D. Il s'agit de la rapidité avec laquelle un algorithme accomplit sa tâche

<details>
<summary>Voir la réponse</summary>

**Réponse : B**

L'efficacité (ou faisabilité) signifie que chaque étape doit être basique et réalisable concrètement.

</details>

---

### Question 4

**Au cours de la phase "Comprendre le problème" de la conception d'un algorithme, quelles tâches essentielles doivent être effectuées ? (Plusieurs réponses possibles)**

- [ ] A. Identifier les données ou informations que l'algorithme recevra, y compris les types et les contraintes
- [ ] B. Commencer immédiatement à écrire le code pour voir si une solution émerge
- [ ] C. Préciser le résultat souhaité, son format et ce qui se passe en cas d'entrées non valides
- [ ] D. Décomposer les problèmes complexes en sous-problèmes plus petits et plus faciles à gérer

<details>
<summary>Voir la réponse</summary>

**Réponses : A, C, D**

La phase "Comprendre le problème" implique :

- Identifier les entrées (A)
- Identifier les sorties (C)
- Décomposer si nécessaire (D)

L'option B (écrire du code immédiatement) est une mauvaise pratique !

</details>

---

### Question 5

**Selon la leçon, pourquoi les algorithmes sont-ils considérés comme le fondement de l'informatique et de la résolution de problèmes ? (Plusieurs réponses possibles)**

- [ ] A. Ils fournissent un moyen clair et sans ambiguïté de décrire une solution, facilitant ainsi la communication entre les développeurs
- [ ] B. Ils sont exclusivement utilisés pour des calculs mathématiques avancés et non dans la vie quotidienne
- [ ] C. Ils permettent l'automatisation de tâches complexes, garantissant une exécution rapide et précise sans intervention humaine
- [ ] D. Ils posent les bases pour évaluer et améliorer ultérieurement l'efficacité d'un algorithme

<details>
<summary>Voir la réponse</summary>

**Réponses : A, C, D**

Les algorithmes sont importants car ils permettent :

- La clarté et communication (A)
- L'automatisation (C)
- L'optimisation future (D)

L'option B est fausse : les algorithmes sont présents partout dans la vie quotidienne !

</details>

---

## 📌 Récapitulatif en 5 Points Clés

### 1. Définition

Un **algorithme** est une séquence bien définie d'étapes pour résoudre un problème spécifique ou effectuer un calcul.

### 2. Les 5 Caractéristiques Essentielles

Un vrai algorithme possède :

- **Entrées** bien définies
- **Sorties** bien définies
- **Finitude** (se termine après un nombre fini d'étapes)
- **Absence d'ambiguïté** (instructions claires et précises)
- **Efficacité** (étapes réalisables)

### 3. Les 3 Étapes de Conception

- **Comprendre le problème** (entrées, sorties, contraintes, cas limites)
- **Concevoir l'algorithme** (brainstorming, pseudocode, logique)
- **Affiner l'algorithme** (tester, simplifier, clarifier)

### 4. Importance des Algorithmes

Les algorithmes sont essentiels pour :

- L'automatisation
- La clarté et communication
- La reproductibilité
- L'efficacité future
- Le développement des compétences en programmation
- L'application universelle dans tous les domaines

### 5. Pensée Algorithmique

La pensée algorithmique est une **compétence transférable** qui vous aide à :

- Décomposer des problèmes complexes
- Penser de manière structurée et logique
- Résoudre des problèmes dans n'importe quel domaine

---

## 🎓 Conclusion

**Félicitations !** 🎉 Vous avez franchi la première étape cruciale dans votre apprentissage des algorithmes !

### Ce que vous avez appris aujourd'hui

Vous comprenez désormais qu'un algorithme est **bien plus qu'un programme informatique complexe** ; c'est une **méthode précise, étape par étape**, permettant de résoudre n'importe quel problème, caractérisée par :

- Des entrées et sorties bien définies
- Une finitude garantie
- Des instructions sans ambiguïté
- Une efficacité pratique

### Comment vous avez progressé

Nous avons exploré comment cette approche de résolution de problèmes s'applique :

- Dans la **vie quotidienne** (préparer un café, utiliser un GPS)
- Dans des **scénarios concrets** (traitement de commandes e-commerce)
- Dans des **tâches informatiques conceptuelles** (trouver le minimum d'une liste)

### La fondation est posée

Cette compréhension fondamentale de ce qu'est un algorithme et de la manière de définir ses étapes de résolution de problèmes constitue **la base essentielle** de tout ce que nous aborderons ensuite.

---

## ➡️ Prochaine Étape : Leçon 2

### Ce qui vous attend

Dans la prochaine leçon, **« Introduction à JavaScript pour le Développement d'Algorithmes »**, nous allons nous équiper des outils nécessaires pour traduire nos idées algorithmiques en code fonctionnel.

**Vous découvrirez :**

- Les variables (`let`, `const`) et les types de données fondamentaux.
- Les structures de contrôle comme `if/else`, `switch` et les boucles.
- Comment créer et utiliser des fonctions pour organiser votre logique.

### Préparez-vous !

Maîtriser ces bases de JavaScript est l'étape indispensable pour commencer à implémenter et à tester l'efficacité de vos propres algorithmes.

---

## 🔗 Ressources Complémentaires

### Pour aller plus loin

- [Vidéo : C'est quoi un algorithme ?](https://www.youtube.com/watch?v=kk6YbA5I-Iw)
- [Article : Introduction aux algorithmes](https://www.lamsade.dauphine.fr/~mayag/Chapitre_1_Introduction_Algorithmique.pdf)
- [Jeu interactif : AlgoBot](https://www.algobot.be/) - Apprenez la logique algorithmique en jouant

### Outils utiles

- **[Draw.io](https://draw.io)** : Pour créer des organigrammes d'algorithmes
- **[Pseudocode Online](https://pseudoeditor.com/app)** : Pour écrire du pseudocode structuré

---

## 💬 Feedback et Questions

Vous avez des questions sur cette leçon ? Des difficultés sur un concept particulier ?

N'hésitez pas à :

- Relire les sections qui vous semblent floues
- Refaire les micro-exercices
- Pratiquer avec vos propres exemples du quotidien

> 💡 **Conseil**
>
> La maîtrise de la pensée algorithmique vient avec la **pratique régulière**. Prenez le temps de vraiment comprendre ces fondamentaux avant de passer à la suite !

---

**Prêt pour la Leçon 2 ?** 🚀

Rendez-vous dans la prochaine leçon pour découvrir JavaScript et commencer à écrire du code !

---

<div align="center">

**Leçon 1 sur 42 - Module 1 : Fondements des algorithmes et révision de JavaScript**

[Retour au sommaire](./README.md) | [Leçon 2 : Introduction à JavaScript ➡️](./lecon-2-introduction-javascript.md)

---

_Cours "Algorithmes : des Fondamentaux aux Concepts Avancés avec JavaScript"_

</div>
