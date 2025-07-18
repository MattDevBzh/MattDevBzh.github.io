---
layout: post
title: "Conditions et structures de contrôle en C# : Prendre les bonnes décisions dans votre café"
date: 2025-01-27
---

Dans la programmation comme dans un café, il faut constamment prendre des décisions ! **Quel café servir selon les préférences du client ? Que faire si la machine est en panne ?** Les structures de contrôle en C# nous permettent de gérer ces situations. ☕

Découvrons ensemble comment programmer la logique de décision avec des exemples tirés de la gestion d'un café !

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une structure de contrôle ?

Une **structure de contrôle** détermine l'ordre d'exécution des instructions dans un programme. C'est comme les règles de fonctionnement de votre café :

- **Si** le client commande un cappuccino **alors** préparer du lait moussé
- **Si** il n'y a plus de grains **alors** commander un réapprovisionnement
- **Selon** l'heure de la journée **choisir** le menu approprié

---

## 1. La condition simple : `if`

La structure `if` permet d'exécuter du code seulement si une condition est vraie.

### Syntaxe de base
```csharp
if (condition)
{
    // Code à exécuter si la condition est vraie
}
```

### Exemple : Vérifier la disponibilité du café
```csharp
int stockCafe = 50; // grammes restants
int grammesPourEspresso = 18;

if (stockCafe >= grammesPourEspresso)
{
    Console.WriteLine("✅ Espresso disponible !");
    stockCafe = stockCafe - grammesPourEspresso;
    Console.WriteLine($"Stock restant : {stockCafe}g");
}
```

### ⚠️ Erreurs courantes avec if

```csharp
// ❌ ERREUR : Utiliser = au lieu de ==
int stock = 10;
if (stock = 5) // ERREUR ! Assigne 5 au lieu de comparer !
{
    Console.WriteLine("Stock égal à 5");
}

// ❌ ERREUR : Oublier les accolades
if (stock > 0)
    Console.WriteLine("Stock disponible");
    Console.WriteLine("Cette ligne s'exécute TOUJOURS !"); // Pas dans le if !

// ✅ CORRECT : Bonnes pratiques
if (stock == 5) // ✅ Comparaison avec ==
{
    Console.WriteLine("Stock égal à 5");
}

if (stock > 0) // ✅ Toujours utiliser des accolades
{
    Console.WriteLine("Stock disponible");
    Console.WriteLine("Cette ligne est dans le if");
}
```

### Exemple : Gestion de l'heure d'ouverture
```csharp
int heureActuelle = 8;
int heureOuverture = 7;
int heureFermeture = 19;

if (heureActuelle >= heureOuverture && heureActuelle < heureFermeture)
{
    Console.WriteLine("☕ Le café est ouvert ! Bienvenue !");
}
```

---

## 2. La condition alternative : `if...else`

Quand on a deux choix possibles, on utilise `if...else`.

### Syntaxe
```csharp
if (condition)
{
    // Code si la condition est vraie
}
else
{
    // Code si la condition est fausse
}
```

### Exemple : Recommandation selon la taille de tasse
```csharp
string tailleTasse = "Grande";
double prixBase = 2.50;
double prixFinal;

if (tailleTasse == "Grande")
{
    prixFinal = prixBase + 0.50;
    Console.WriteLine($"☕ Tasse grande sélectionnée. Prix : {prixFinal}€");
}
else
{
    prixFinal = prixBase;
    Console.WriteLine($"☕ Tasse normale sélectionnée. Prix : {prixFinal}€");
}
```

### Exemple : Gestion de stock
```csharp
int stockGrains = 30;
int stockMinimum = 50;

if (stockGrains >= stockMinimum)
{
    Console.WriteLine("✅ Stock suffisant pour la journée");
}
else
{
    Console.WriteLine("⚠️ Stock faible ! Commander des grains urgentement");
    Console.WriteLine($"Il manque {stockMinimum - stockGrains}g de café");
}
```

---

## 3. Les conditions multiples : `if...else if...else`

Pour gérer plusieurs possibilités, on enchaîne les conditions.

### Syntaxe
```csharp
if (condition1)
{
    // Code pour condition1
}
else if (condition2)
{
    // Code pour condition2  
}
else if (condition3)
{
    // Code pour condition3
}
else
{
    // Code par défaut
}
```

### Exemple : Menu selon l'heure
```csharp
int heure = 14;

if (heure >= 6 && heure < 11)
{
    Console.WriteLine("🌅 Menu petit-déjeuner");
    Console.WriteLine("- Espresso + croissant : 4€");
    Console.WriteLine("- Cappuccino + pain au chocolat : 5€");
}
else if (heure >= 11 && heure < 14)
{
    Console.WriteLine("☀️ Menu déjeuner");
    Console.WriteLine("- Café + sandwich : 8€");
    Console.WriteLine("- Americano + salade : 9€");
}
else if (heure >= 14 && heure < 17)
{
    Console.WriteLine("🍰 Menu goûter");
    Console.WriteLine("- Latte + part de gâteau : 6€");
    Console.WriteLine("- Thé + muffin : 5€");
}
else
{
    Console.WriteLine("🌙 Menu soirée");
    Console.WriteLine("- Décaféiné + tisane : 3€");
}
```

### Exemple : Classification des clients
```csharp
int nombreVisites = 15;
string typeClient;
double remise;

if (nombreVisites >= 50)
{
    typeClient = "Client VIP ⭐";
    remise = 0.20; // 20% de remise
}
else if (nombreVisites >= 20)
{
    typeClient = "Client fidèle 💖";
    remise = 0.10; // 10% de remise
}
else if (nombreVisites >= 5)
{
    typeClient = "Client régulier ☕";
    remise = 0.05; // 5% de remise
}
else
{
    typeClient = "Nouveau client 👋";
    remise = 0.0; // Pas de remise
}

Console.WriteLine($"Type : {typeClient}");
Console.WriteLine($"Remise applicable : {remise * 100}%");
```

---

## 4. L'instruction `switch` : Choisir parmi plusieurs options

Quand on a plusieurs valeurs précises à tester, `switch` est plus lisible que de multiples `if...else if`.

### Syntaxe
```csharp
switch (variable)
{
    case valeur1:
        // Code pour valeur1
        break;
    case valeur2:
        // Code pour valeur2
        break;
    default:
        // Code par défaut
        break;
}
```

### Exemple : Préparation selon le type de café
```csharp
string typeCafe = "Cappuccino";

switch (typeCafe)
{
    case "Espresso":
        Console.WriteLine("☕ Préparation Espresso :");
        Console.WriteLine("- 18g de café moulu");
        Console.WriteLine("- 30ml d'eau chaude");
        Console.WriteLine("- Extraction en 25 secondes");
        break;
        
    case "Americano":
        Console.WriteLine("☕ Préparation Americano :");
        Console.WriteLine("- 1 dose d'espresso");
        Console.WriteLine("- 120ml d'eau chaude");
        break;
        
    case "Cappuccino":
        Console.WriteLine("☕ Préparation Cappuccino :");
        Console.WriteLine("- 1 dose d'espresso");
        Console.WriteLine("- 60ml de lait");
        Console.WriteLine("- Mousser le lait");
        break;
        
    case "Latte":
        Console.WriteLine("☕ Préparation Latte :");
        Console.WriteLine("- 1 dose d'espresso");
        Console.WriteLine("- 180ml de lait");
        Console.WriteLine("- Mousse légère");
        break;
        
    default:
        Console.WriteLine("❌ Type de café non reconnu");
        Console.WriteLine("Cafés disponibles : Espresso, Americano, Cappuccino, Latte");
        break;
}
```

### Exemple : Calcul du prix selon la taille
```csharp
string taille = "L";
double prixBase = 3.0;
double prixFinal;

switch (taille)
{
    case "S":
        prixFinal = prixBase - 0.5;
        Console.WriteLine($"Taille S - Prix : {prixFinal}€");
        break;
        
    case "M":
        prixFinal = prixBase;
        Console.WriteLine($"Taille M - Prix : {prixFinal}€");
        break;
        
    case "L":
        prixFinal = prixBase + 0.5;
        Console.WriteLine($"Taille L - Prix : {prixFinal}€");
        break;
        
    case "XL":
        prixFinal = prixBase + 1.0;
        Console.WriteLine($"Taille XL - Prix : {prixFinal}€");
        break;
        
    default:
        prixFinal = prixBase;
        Console.WriteLine($"Taille inconnue, prix standard M : {prixFinal}€");
        break;
}
```

---

## 5. Les opérateurs de comparaison

### Opérateurs de base
```csharp
int stock = 100;
int minimum = 50;

// Égalité
bool estEgal = stock == minimum;           // false

// Différence  
bool estDifferent = stock != minimum;      // true

// Comparaisons
bool estSuperieur = stock > minimum;       // true
bool estInferieur = stock < minimum;       // false
bool estSuperieurEgal = stock >= minimum;  // true
bool estInferieurEgal = stock <= minimum;  // false
```

### Opérateurs logiques
```csharp
bool machineAllumee = true;
bool stockSuffisant = true;
bool clientPresent = false;

// ET logique (&&) - toutes les conditions doivent être vraies
bool peutServir = machineAllumee && stockSuffisant;  // true

// OU logique (||) - au moins une condition doit être vraie  
bool ouvert = clientPresent || stockSuffisant;       // true

// NON logique (!) - inverse la valeur
bool machineFermee = !machineAllumee;               // false
```

### Exemple pratique : Validation de commande
```csharp
int stockCafe = 200;     // grammes
int stockLait = 500;     // millilitres
bool machineMarche = true;
string commande = "Cappuccino";

bool peutPreparerCappuccino = machineMarche && 
                             stockCafe >= 18 && 
                             stockLait >= 60;

if (commande == "Cappuccino" && peutPreparerCappuccino)
{
    Console.WriteLine("✅ Cappuccino en préparation !");
}
else if (commande == "Cappuccino" && !peutPreparerCappuccino)
{
    Console.WriteLine("❌ Impossible de préparer le cappuccino :");
    
    if (!machineMarche)
        Console.WriteLine("- Machine en panne");
    if (stockCafe < 18)
        Console.WriteLine("- Pas assez de café");
    if (stockLait < 60)
        Console.WriteLine("- Pas assez de lait");
}
```

---

## 6. Exemple complet : Système de commande

Assemblons tout dans un système de gestion de commandes :

```csharp
using System;

class ProgrammeCafe
{
    static void Main()
    {
        // État du café
        int stockCafe = 150;        // grammes
        int stockLait = 800;        // ml
        bool machineMarche = true;
        int heure = 10;
        
        // Commande client
        string nomClient = "Sophie";
        string typeCommande = "Cappuccino";
        string taille = "L";
        
        Console.WriteLine("=== ☕ CAFÉ DU COIN ☕ ===");
        Console.WriteLine($"Client : {nomClient}");
        Console.WriteLine($"Commande : {typeCommande} taille {taille}");
        Console.WriteLine();
        
        // Vérifier l'heure d'ouverture
        if (heure < 7 || heure > 19)
        {
            Console.WriteLine("❌ Désolé, nous sommes fermés !");
            Console.WriteLine("Horaires : 7h - 19h");
            return;
        }
        
        // Déterminer les besoins selon la commande
        int cafeNecessaire = 0;
        int laitNecessaire = 0;
        double prixBase = 0;
        
        switch (typeCommande)
        {
            case "Espresso":
                cafeNecessaire = 18;
                laitNecessaire = 0;
                prixBase = 2.5;
                break;
                
            case "Americano":
                cafeNecessaire = 18;
                laitNecessaire = 0;
                prixBase = 3.0;
                break;
                
            case "Cappuccino":
                cafeNecessaire = 18;
                laitNecessaire = 60;
                prixBase = 4.0;
                break;
                
            case "Latte":
                cafeNecessaire = 18;
                laitNecessaire = 150;
                prixBase = 4.5;
                break;
                
            default:
                Console.WriteLine("❌ Type de café non disponible");
                return;
        }
        
        // Ajuster le prix selon la taille
        double prixFinal = prixBase;
        if (taille == "L")
        {
            prixFinal += 0.5;
            cafeNecessaire += 3;
            laitNecessaire = (int)(laitNecessaire * 1.3);
        }
        else if (taille == "XL")
        {
            prixFinal += 1.0;
            cafeNecessaire += 6;
            laitNecessaire = (int)(laitNecessaire * 1.6);
        }
        
        // Vérifications
        bool stockOk = stockCafe >= cafeNecessaire && stockLait >= laitNecessaire;
        
        if (!machineMarche)
        {
            Console.WriteLine("❌ Machine en maintenance, désolé !");
        }
        else if (!stockOk)
        {
            Console.WriteLine("❌ Stock insuffisant :");
            if (stockCafe < cafeNecessaire)
                Console.WriteLine($"- Café manquant : {cafeNecessaire - stockCafe}g");
            if (stockLait < laitNecessaire)
                Console.WriteLine($"- Lait manquant : {laitNecessaire - stockLait}ml");
        }
        else
        {
            // Préparer la commande
            Console.WriteLine("✅ Commande acceptée !");
            Console.WriteLine($"Prix : {prixFinal}€");
            Console.WriteLine();
            Console.WriteLine("🔄 Préparation en cours...");
            
            // Décrémenter le stock
            stockCafe -= cafeNecessaire;
            stockLait -= laitNecessaire;
            
            Console.WriteLine($"☕ {typeCommande} {taille} prêt pour {nomClient} !");
            Console.WriteLine($"Stock restant - Café : {stockCafe}g, Lait : {stockLait}ml");
        }
    }
}
```

---

## 7. Conseils et bonnes pratiques

### ✅ Utilisez des noms explicites
```csharp
// 👍 Bon
if (stockCafe >= cafeNecessairePourEspresso)

// 👎 Éviter  
if (x >= y)
```

### ✅ Groupez les conditions complexes
```csharp
bool stockSuffisant = stockCafe >= 18 && stockLait >= 60;
bool peutServir = machineMarche && stockSuffisant;

if (peutServir)
{
    // Préparer le café
}
```

### ✅ Préférez `switch` pour de multiples valeurs exactes
```csharp
// 👍 Plus lisible avec switch
switch (typeCafe)
{
    case "Espresso": /* ... */ break;
    case "Latte": /* ... */ break;
}

// 👎 Moins lisible avec if/else
if (typeCafe == "Espresso") { /* ... */ }
else if (typeCafe == "Latte") { /* ... */ }
```

---

## Exercices pratiques

### Exercice 1 : Menu dynamique
Créez un programme qui affiche un menu différent selon l'heure :
- 6h-11h : Petit-déjeuner
- 11h-15h : Déjeuner  
- 15h-18h : Goûter
- 18h-22h : Soirée

### Exercice 2 : Calculateur de remise
Créez un système de fidélité avec :
- 0-4 visites : Aucune remise
- 5-19 visites : 5% de remise
- 20-49 visites : 10% de remise
- 50+ visites : 15% de remise

### Exercice 3 : Vérificateur de stock
Créez un programme qui vérifie si on peut préparer une commande selon le stock disponible.

---

## Conclusion

Les structures de contrôle sont les **fondations de la logique** en programmation ! Elles nous permettent de :

- ✅ **Prendre des décisions** avec `if/else`
- ✅ **Gérer plusieurs options** avec `switch`  
- ✅ **Combiner des conditions** avec les opérateurs logiques

Comme un bon barista qui s'adapte aux demandes de ses clients, un développeur utilise les structures de contrôle pour créer des programmes intelligents et réactifs !

**Prochaine étape :** Nous découvrirons les boucles pour automatiser les tâches répétitives - parfait pour préparer plusieurs cafés d'affilée ! ☕

---

*N'hésitez pas à expérimenter avec ces exemples et à créer vos propres scénarios de café. La programmation, comme l'art du café, se maîtrise avec la pratique ! 🚀*