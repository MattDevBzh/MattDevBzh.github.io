---
layout: post
title: "Les variables et types de données : les bases de la programmation en C#"
date: 2025-01-18
---

**Les variables** sont les fondations de tout programme informatique. Imaginez-les comme des tasses étiquetées dans votre café préféré : chacune peut contenir quelque chose de différent, et l'étiquette vous dit ce qu'elle contient !

Dans cet article, nous allons découvrir ensemble les concepts fondamentaux des variables et types de données en C# à travers l'univers familier du café. ☕

**Objectif de cet article :** Comprendre comment stocker et manipuler des informations dans votre programme.

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une variable ?

Une **variable** est un espace de stockage dans la mémoire de l'ordinateur qui porte un nom et peut contenir une valeur. C'est comme un conteneur étiqueté dans votre cuisine où vous rangez différents ingrédients.

**Exemple concret :**
```csharp
string nomCafe = "Espresso";
double prix = 2.50;
bool estDisponible = true;
```

Ici, nous avons créé trois "contenants" :
- `nomCafe` : contient le texte "Espresso"
- `prix` : contient le nombre 2.50
- `estDisponible` : contient la valeur vraie/fausse `true`

### ⚠️ Erreurs courantes des débutants

```csharp
// ❌ ERREUR : Nom sans déclaration de type
nomCafe = "Espresso"; // Manque le type "string"

// ❌ ERREUR : Type incorrect
string prix = 2.50; // Prix est un nombre, pas du texte !

// ❌ ERREUR : Nom avec espaces
string nom cafe = "Espresso"; // Les espaces sont interdits !

// ✅ CORRECT : Declaration complète
string nomCafe = "Espresso";
double prix = 2.50;
bool estDisponible = true;
```

---

## Les types de données fondamentaux

### 🔤 Les chaînes de caractères (string)

Les **string** stockent du texte, comme le nom d'un café ou une description.

```csharp
string nomClient = "Marie";
string typeCafe = "Cappuccino";
string tailleTasse = "Grande";
string description = "Un délicieux mélange arabica avec une mousse de lait onctueuse";
```

**Utilisation pratique :**
```csharp
Console.WriteLine("Bonjour " + nomClient + ", votre " + typeCafe + " est prêt !");
// Affiche : "Bonjour Marie, votre Cappuccino est prêt !"

// Ou avec l'interpolation de chaînes (plus moderne) :
Console.WriteLine($"Bonjour {nomClient}, votre {typeCafe} est prêt !");
```

### 🔢 Les nombres (int, double, decimal)

Les **nombres** stockent des valeurs numériques : prix, quantités, températures...

```csharp
double prixCafe = 3.20;        // Prix en euros (avec décimales)
int quantiteGrains = 500;      // Grammes de café (nombre entier)
decimal temperature = 92.5m;   // Température précise (pour calculs financiers)
int nombreClients = 15;        // Clients dans la file d'attente
```

**Opérations mathématiques :**
```csharp
double total = prixCafe * nombreClients;
int resteGrains = quantiteGrains - 50; // Après une préparation
double moyenne = total / nombreClients;
```

### ⚠️ Pièges avec les nombres

```csharp
// ❌ PIÈGE : Division entière
int resultat = 5 / 2; // = 2 (pas 2.5 !)

// ✅ CORRECT : Division avec décimales
double resultat = 5.0 / 2.0; // = 2.5

// ❌ PIÈGE : Débordement
int tresGrand = 2000000000;
int tropGrand = tresGrand * 2; // Débordement !

// ✅ CORRECT : Utiliser long pour de grands nombres
long tresGrand = 2000000000L;
long correct = tresGrand * 2;
```

### ✅ Les booléens (bool)

Les **bool** ne peuvent avoir que deux valeurs : `true` (vrai) ou `false` (faux). Parfait pour des états on/off !

```csharp
bool machineAllumee = true;      // La machine à café est allumée
bool stockVide = false;          // Il reste du café en stock
bool clientSatisfait = true;     // Le client a aimé son café
bool fermetureMagasin = false;   // Le café est encore ouvert
```

**Utilisation dans des conditions :**
```csharp
if (stockVide == true) // ou simplement: if (stockVide)
{
    Console.WriteLine("Attention : plus de café en stock !");
}
```

---

## Bonnes pratiques pour nommer les variables

### ✅ Noms explicites et clairs
```csharp
// 👍 Bon
double prixLatteGrand = 4.50;
int nombreCafesVendus = 25;

// 👎 Éviter
double p = 4.50;
int n = 25;
```

### ✅ Convention camelCase en C#
```csharp
// 👍 Recommandé en C#
string nomCompletClient = "Marie Dupont";
bool machineEnService = true;
double prixTotalCommande = 15.75;
```

### ⚠️ Erreurs de nommage courantes

```csharp
// ❌ ERREUR : Commencer par un chiffre
int 1cafe = 10; // Interdit !

// ❌ ERREUR : Utiliser des mots réservés
string class = "Espresso"; // "class" est un mot réservé !

// ❌ ERREUR : Caractères spéciaux
string café-prix = "2.50"; // Le tiret est interdit !

// ✅ CORRECT : Noms valides
int premierCafe = 10;
string typeCafe = "Espresso";
double prixCafe = 2.50;
```

---

## Déclaration et modification des variables

### Comment déclarer une variable
```csharp
// Déclaration avec valeur initiale
string nomCafe = "Cappuccino";
int quantite = 2;

// Déclaration puis assignation
double prix;
prix = 4.50;

// Déclaration multiple du même type
int cafe1 = 1, cafe2 = 2, cafe3 = 3;
```

### Modification de variables
```csharp
int clientsEnAttente = 5;
Console.WriteLine($"Clients en attente : {clientsEnAttente}");

// Modification
clientsEnAttente = clientsEnAttente + 1; // Nouveau client arrive
clientsEnAttente += 1; // ✅ Équivalent, plus court
clientsEnAttente++; // ✅ Équivalent pour +1

Console.WriteLine($"Clients en attente : {clientsEnAttente}");
```

### Constantes (`const`) - ne peuvent pas changer
```csharp
const double PRIX_BASE_CAFE = 2.00;
const string NOM_CAFE = "Chez Marie";
// PRIX_BASE_CAFE = 2.50; // ❌ Erreur !
```

**Conseil :** Utilisez `const` pour les valeurs qui ne changent jamais, comme les prix de base ou le nom du café.

---

## 📋 Récapitulatif pour débutants

### Types de base en C#

| Type | Utilisation | Exemple |
|------|-------------|---------|
| `string` | Texte | `"Cappuccino"` |
| `int` | Nombres entiers | `25` |
| `double` | Nombres à décimales | `4.50` |
| `bool` | Vrai/Faux | `true`, `false` |
| `const` | Valeurs fixes | `const double PRIX = 2.50` |

### ⚠️ Erreurs fréquentes à éviter

1. **Oublier le type** : `nomCafe = "Test";` au lieu de `string nomCafe = "Test";`
2. **Mauvais type** : `string prix = 4.50;` au lieu de `double prix = 4.50;`
3. **Division entière** : `int resultat = 5 / 2;` donne 2 au lieu de 2.5
4. **Noms invalides** : espaces, chiffres au début, caractères spéciaux

---

## Exercice pratique

Essayez de créer des variables pour votre café imaginaire :

```csharp
class MonCafe
{
    static void Main()
    {
        // À vous de compléter !
        string nomVotreCafe = ""; // Le nom de votre café
        string specialiteMaison = ""; // Votre spécialité
        double prixSpecialite = 0.0; // Prix de votre spécialité
        bool ouvertAujourdHui = true; // Ouvert ou fermé ?

        // Calculez le prix pour 3 spécialités
        double prixTroisSpecialites = prixSpecialite * 3;

        Console.WriteLine($"Bienvenue chez {nomVotreCafe} !");
        Console.WriteLine($"Notre spécialité : {specialiteMaison} ({prixSpecialite:C2})");
        Console.WriteLine($"Prix pour 3 : {prixTroisSpecialites:C2}");
    }
}
```

---

## Conclusion

Les variables et types de données sont comme les ingrédients de base d'une recette de café :

- **Les strings** pour les noms et descriptions 📝
- **Les int/double** pour les quantités et prix 🔢  
- **Les bool** pour les états et conditions ✅

**Points clés à retenir :**
- ✅ **Toujours déclarer le type** de vos variables
- ✅ **Utiliser des noms explicites** pour faciliter la lecture
- ✅ **Choisir le bon type** selon l'utilisation
- ✅ **Attention à la division entière** avec `int`

Maîtriser ces concepts vous donnera les bases solides pour construire vos premiers programmes. Comme un bon barista qui connaît ses grains, un développeur qui maîtrise ses variables peut créer des applications extraordinaires !

**Prochaine étape :** Dans le prochain article, nous découvrirons les structures de contrôle pour prendre des décisions dans votre programme ! ☕

---