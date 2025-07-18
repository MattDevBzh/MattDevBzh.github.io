---
layout: post
title: "Les variables et types de données : les bases de la programmation"
date: 2025-01-18
---

**Les variables** sont les fondations de tout programme informatique. Imaginez-les comme des tasses étiquetées dans votre café préféré : chacune peut contenir quelque chose de différent, et l'étiquette vous dit ce qu'elle contient !

Dans cet article, nous allons découvrir ensemble les concepts fondamentaux des variables et types de données à travers l'univers familier du café. ☕

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une variable ?

Une **variable** est un espace de stockage dans la mémoire de l'ordinateur qui porte un nom et peut contenir une valeur. C'est comme un conteneur étiqueté dans votre cuisine où vous rangez différents ingrédients.

**Exemple concret :**
```javascript
let nomCafe = "Espresso";
let prix = 2.50;
let estDisponible = true;
```

Ici, nous avons créé trois "contenants" :
- `nomCafe` : contient le texte "Espresso"
- `prix` : contient le nombre 2.50
- `estDisponible` : contient la valeur vraie/fausse `true`

---

## Les types de données fondamentaux

### 🔤 Les chaînes de caractères (String)

Les **strings** stockent du texte, comme le nom d'un café ou une description.

```javascript
let nomClient = "Marie";
let typeCafe = "Cappuccino";
let tailleTasse = "Grande";
let description = "Un délicieux mélange arabica avec une mousse de lait onctueuse";
```

**Utilisation pratique :**
```javascript
console.log("Bonjour " + nomClient + ", votre " + typeCafe + " est prêt !");
// Affiche : "Bonjour Marie, votre Cappuccino est prêt !"
```

### 🔢 Les nombres (Number)

Les **numbers** stockent des valeurs numériques : prix, quantités, températures...

```javascript
let prixCafe = 3.20;        // Prix en euros
let quantiteGrains = 500;   // Grammes de café
let temperature = 92.5;     // Température de l'eau en °C
let nombreClients = 15;     // Clients dans la file d'attente
```

**Opérations mathématiques :**
```javascript
let total = prixCafe * nombreClients;
let resteGrains = quantiteGrains - 50; // Après une préparation
```

### ✅ Les booléens (Boolean)

Les **booleans** ne peuvent avoir que deux valeurs : `true` (vrai) ou `false` (faux). Parfait pour des états on/off !

```javascript
let machineAllumee = true;      // La machine à café est allumée
let stockVide = false;          // Il reste du café en stock
let clientSatisfait = true;     // Le client a aimé son café
let fermetureMagasin = false;   // Le café est encore ouvert
```

**Utilisation dans des conditions :**
```javascript
if (stockVide === true) {
    console.log("Attention : plus de café en stock !");
}
```

---

## Bonnes pratiques pour nommer les variables

### ✅ Noms explicites et clairs
```javascript
// 👍 Bon
let prixLatteGrand = 4.50;
let nombreCafesVendus = 25;

// 👎 Éviter
let p = 4.50;
let n = 25;
```

### ✅ Convention camelCase
En JavaScript, on utilise le **camelCase** : première lettre minuscule, puis majuscule à chaque nouveau mot.

```javascript
let temperatureEauOptimale = 93;
let tempsPreparationEspresso = 25; // en secondes
let quantiteGrainsParTasse = 18;   // en grammes
```

### ✅ Noms de constantes en MAJUSCULES
Pour les valeurs qui ne changent jamais :

```javascript
const PRIX_ESPRESSO = 2.50;
const TEMPERATURE_IDEALE = 92;
const GRAMMES_PAR_TASSE = 18;
```

---

## Exemple pratique : Système de commande de café

Créons un petit système pour gérer les commandes d'un café :

```javascript
// Informations sur le café
const NOM_CAFE = "Le Grain d'Or";
let heureOuverture = 7;
let heureFermeture = 19;

// Informations produit
let espressoDisponible = true;
let prixEspresso = 2.50;
let stockGrains = 1000; // en grammes

// Commande client
let nomClient = "Pierre";
let typeCommande = "Espresso";
let taille = "Simple";
let quantiteCommandee = 2;

// Calculs
let prixTotal = prixEspresso * quantiteCommandee;
let grainsNecessaires = quantiteCommandee * 18; // 18g par espresso

// Vérifications
let assezDeStock = stockGrains >= grainsNecessaires;
let peutPreparerCommande = espressoDisponible && assezDeStock;

// Affichage
console.log("=== " + NOM_CAFE + " ===");
console.log("Client : " + nomClient);
console.log("Commande : " + quantiteCommandee + " " + typeCommande);
console.log("Prix total : " + prixTotal + "€");

if (peutPreparerCommande) {
    console.log("✅ Commande acceptée ! Préparation en cours...");
    stockGrains = stockGrains - grainsNecessaires;
    console.log("Stock restant : " + stockGrains + "g");
} else {
    console.log("❌ Désolé, impossible de préparer cette commande.");
}
```

---

## Modification et réassignation

Les variables peuvent changer de valeur au cours du programme :

```javascript
let stockLait = 500; // millilitres
console.log("Stock initial : " + stockLait + "ml");

// Après la préparation d'un cappuccino
stockLait = stockLait - 150;
console.log("Après cappuccino : " + stockLait + "ml");

// Livraison de lait
stockLait = stockLait + 1000;
console.log("Après livraison : " + stockLait + "ml");
```

**Raccourcis utiles :**
```javascript
stockLait -= 150;  // Équivaut à : stockLait = stockLait - 150
stockLait += 1000; // Équivaut à : stockLait = stockLait + 1000
```

---

## Variables vs Constantes

### Variables (`let`) - peuvent changer
```javascript
let clientsEnAttente = 5;
clientsEnAttente = clientsEnAttente + 1; // ✅ Possible
```

### Constantes (`const`) - ne peuvent pas changer
```javascript
const PRIX_BASE_CAFE = 2.00;
// PRIX_BASE_CAFE = 2.50; // ❌ Erreur !
```

**Conseil :** Utilisez `const` par défaut, et `let` seulement quand la valeur doit changer.

---

## Exercice pratique

Essayez de créer des variables pour votre café imaginaire :

```javascript
// À vous de compléter !
let nomVotreCafe = ""; // Le nom de votre café
let specialiteMaison = ""; // Votre spécialité
let prixSpecialite = 0; // Prix de votre spécialité
let ouvertAujourdHui = true; // Ouvert ou fermé ?

// Calculez le prix pour 3 spécialités
let prixTroisSpecialites = prixSpecialite * 3;

console.log("Bienvenue chez " + nomVotreCafe + " !");
console.log("Notre spécialité : " + specialiteMaison + " (" + prixSpecialite + "€)");
console.log("Prix pour 3 : " + prixTroisSpecialites + "€");
```

---

## Conclusion

Les variables et types de données sont comme les ingrédients de base d'une recette de café :

- **Les strings** pour les noms et descriptions 📝
- **Les numbers** pour les quantités et prix 🔢  
- **Les booleans** pour les états et conditions ✅

Maîtriser ces concepts vous donnera les bases solides pour construire vos premiers programmes. Comme un bon barista qui connaît ses grains, un développeur qui maîtrise ses variables peut créer des applications extraordinaires !

**Prochaine étape :** Dans le prochain article, nous découvrirons les fonctions - les "recettes" qui utilisent nos ingrédients (variables) pour créer quelque chose de délicieux ! ☕

---

*N'hésitez pas à expérimenter avec ces exemples et à créer vos propres variables sur le thème du café. L'apprentissage de la programmation, c'est comme apprendre à faire un bon café : il faut pratiquer ! 🚀*