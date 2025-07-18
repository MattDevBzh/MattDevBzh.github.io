---
layout: post
title: "Boucles et itérations en C# : Automatiser la préparation de vos cafés"
date: 2025-01-28
---

Dans un café animé, certaines tâches se répètent sans cesse : **préparer plusieurs espressos, servir une file de clients, nettoyer les tasses...** En programmation C#, les **boucles** nous permettent d'automatiser ces actions répétitives ! ☕

Découvrons ensemble comment utiliser les boucles pour gérer efficacement les tâches répétitives de notre café virtuel.

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une boucle ?

Une **boucle** est une structure qui permet de répéter un bloc de code plusieurs fois. C'est comme avoir un barista infatigable qui peut :

- Préparer 50 cafés identiques
- Servir tous les clients en file d'attente
- Nettoyer toutes les tasses de la journée
- Vérifier le stock de chaque produit

---

## 1. La boucle `for` : Répéter un nombre précis de fois

La boucle `for` est parfaite quand on sait exactement combien de fois répéter une action.

### Syntaxe simple
```csharp
for (initialisation; condition; incrémentation)
{
    // Code à répéter
}
```

### Exemple : Préparer plusieurs espressos
```csharp
int nombreEspressos = 5;

Console.WriteLine("☕ Préparation de la commande groupe");

for (int i = 1; i <= nombreEspressos; i++)
{
    Console.WriteLine($"Espresso n°{i} en cours...");
    Console.WriteLine("- Moudre 18g de grains");
    Console.WriteLine("- Tasser le café");
    Console.WriteLine("- Extraction 25 secondes");
    Console.WriteLine($"✅ Espresso n°{i} terminé !");
    Console.WriteLine();
}

Console.WriteLine($"🎉 Commande terminée ! {nombreEspressos} espressos prêts");
```

### ⚠️ Erreurs courantes avec la boucle for

```csharp
// ❌ ERREUR #1 : Boucle infinie par oubli d'incrémentation
for (int i = 0; i < 5; /* i++ oublié ! */)
{
    Console.WriteLine("Cette boucle ne finira jamais !");
    // Le programme reste bloqué ici !
}

// ❌ ERREUR #2 : Condition mal écrite
for (int i = 0; i <= 5; i++) // ⚠️ <= au lieu de < = 6 tours au lieu de 5 !
{
    Console.WriteLine($"Tour {i}"); // 0, 1, 2, 3, 4, 5
}

// ❌ ERREUR #3 : Confusion entre index et nombre d'éléments
string[] cafes = {"Espresso", "Cappuccino", "Latte"}; // 3 éléments
for (int i = 0; i <= cafes.Length; i++) // ❌ <= cafes.Length !
{
    Console.WriteLine(cafes[i]); // PLANTAGE à i=3 !
}

// ✅ CORRECT : Les bonnes pratiques
string[] cafes = {"Espresso", "Cappuccino", "Latte"};
for (int i = 0; i < cafes.Length; i++) // < (pas <=)
{
    Console.WriteLine($"{i + 1}. {cafes[i]}"); // Numérotation à partir de 1
}
```

**Règles d'or pour la boucle for :**
1. **Toujours incrémenter** le compteur (`i++`)
2. **Utiliser `<`** pour éviter les dépassements
3. **Commencer à 0** pour les tableaux et listes

### Exemple : Calcul du chiffre d'affaires journalier
```csharp
double[] ventesParHeure = {120.50, 89.30, 156.80, 203.45, 178.90, 134.20, 95.60, 87.30};
double totalJournee = 0;

Console.WriteLine("📊 Calcul du chiffre d'affaires :");

for (int heure = 0; heure < ventesParHeure.Length; heure++)
{
    totalJournee += ventesParHeure[heure];
    Console.WriteLine($"Heure {heure + 8}h : {ventesParHeure[heure]:C2}");
}

Console.WriteLine($"\n💰 Total de la journée : {totalJournee:C2}");
```

### Exemple : Inventaire produits
```csharp
string[] produits = {"Espresso", "Cappuccino", "Latte", "Americano", "Macchiato"};
double[] prix = {2.50, 4.00, 4.50, 3.00, 3.80};

Console.WriteLine("📋 MENU DU JOUR");
Console.WriteLine("================");

for (int i = 0; i < produits.Length; i++)
{
    Console.WriteLine($"{i + 1}. {produits[i]} - {prix[i]:C2}");
}
```

---

## 2. La boucle `while` : Répéter tant qu'une condition est vraie

La boucle `while` continue tant qu'une condition reste vraie. Parfaite pour traiter une file d'attente !

### Syntaxe simple
```csharp
while (condition)
{
    // Code à répéter
}
```

### Exemple : Servir une file d'attente
```csharp
int clientsEnAttente = 8;

Console.WriteLine($"👥 {clientsEnAttente} clients en attente");
Console.WriteLine("Début du service...\n");

while (clientsEnAttente > 0)
{
    Console.WriteLine($"☕ Service du client n°{9 - clientsEnAttente}");
    Console.WriteLine("- Prendre la commande");
    Console.WriteLine("- Préparer le café");
    Console.WriteLine("- Servir le client");
    
    clientsEnAttente--; // IMPORTANT : modifier la condition !
    
    Console.WriteLine($"✅ Client servi ! Plus que {clientsEnAttente} en attente\n");
}

Console.WriteLine("🎉 Tous les clients ont été servis !");
```

### ⚠️ Pièges mortels avec while

```csharp
// ❌ PIÈGE MORTEL #1 : Boucle infinie par oubli de modification
int clients = 5;
while (clients > 0)
{
    Console.WriteLine("Service en cours...");
    // clients--; // OUBLIÉ ! La boucle ne finira JAMAIS !
}

// ❌ PIÈGE #2 : Condition qui ne peut jamais être fausse
int compteur = 0;
while (compteur >= 0) // Sera TOUJOURS vrai !
{
    compteur++; // On augmente au lieu de diminuer !
    Console.WriteLine($"Compteur : {compteur}");
    // Cette boucle ne s'arrêtera jamais !
}

// ❌ PIÈGE #3 : Modification incorrecte de la condition
string reponse = "oui";
while (reponse == "oui")
{
    Console.WriteLine("Voulez-vous continuer ? (oui/non)");
    // reponse = Console.ReadLine(); // OUBLIÉ !
    // La boucle ne peut jamais s'arrêter
}

// ✅ CORRECT : Toujours modifier la condition dans la boucle
int clients = 5;
while (clients > 0)
{
    Console.WriteLine($"Service du client {clients}");
    clients--; // ✅ On modifie la condition !
}
```

**Règles d'or pour while :**
1. **Toujours modifier** la variable de condition dans la boucle
2. **Tester la condition** avant d'écrire la boucle
3. **Prévoir une sortie** de secours si possible

### Exemple : Servir la file d'attente
```csharp
int clientsEnAttente = 8;
int clientServi = 0;

Console.WriteLine($"☕ Début du service - {clientsEnAttente} clients en attente");

while (clientsEnAttente > 0)
{
    clientServi++;
    clientsEnAttente--;
    
    Console.WriteLine($"🔄 Service du client n°{clientServi}");
    Console.WriteLine($"   Clients restants : {clientsEnAttente}");
    
    // Simulation du temps de service
    System.Threading.Thread.Sleep(500);
}

Console.WriteLine("✅ Tous les clients ont été servis !");
```

### Exemple : Remplir la machine jusqu'au niveau optimal
```csharp
int niveauEau = 20;        // Niveau actuel en %
int niveauOptimal = 100;   // Niveau souhaité
int ajoutParEtape = 15;    // % ajouté à chaque fois

Console.WriteLine($"💧 Niveau d'eau initial : {niveauEau}%");

while (niveauEau < niveauOptimal)
{
    niveauEau += ajoutParEtape;
    
    // Ne pas dépasser 100%
    if (niveauEau > niveauOptimal)
        niveauEau = niveauOptimal;
    
    Console.WriteLine($"💧 Remplissage... Niveau : {niveauEau}%");
}

Console.WriteLine("✅ Réservoir d'eau plein !");
```

### Exemple : Recherche de grain spécifique
```csharp
string[] grainsDisponibles = {"Arabica Colombie", "Robusta Vietnam", "Arabica Éthiopie", "Blend Maison"};
string grainRecherche = "Arabica Éthiopie";
int index = 0;
bool trouve = false;

Console.WriteLine($"🔍 Recherche de : {grainRecherche}");

while (index < grainsDisponibles.Length && !trouve)
{
    Console.WriteLine($"Vérification : {grainsDisponibles[index]}");
    
    if (grainsDisponibles[index] == grainRecherche)
    {
        trouve = true;
        Console.WriteLine($"✅ Trouvé à la position {index + 1} !");
    }
    else
    {
        index++;
    }
}

if (!trouve)
{
    Console.WriteLine("❌ Grain non trouvé dans le stock");
}
```

---

## 3. La boucle `do...while` : Exécuter au moins une fois

Cette boucle exécute le code au moins une fois, puis vérifie la condition.

### Syntaxe
```csharp
do
{
    // Code à répéter
} while (condition);
```

### Exemple : Menu interactif
```csharp
string choix;

do
{
    Console.WriteLine("\n☕ === MENU CAFÉ ===");
    Console.WriteLine("1. Commander un café");
    Console.WriteLine("2. Voir le stock");
    Console.WriteLine("3. Afficher les ventes");
    Console.WriteLine("4. Quitter");
    Console.Write("Votre choix : ");
    
    choix = Console.ReadLine();
    
    switch (choix)
    {
        case "1":
            Console.WriteLine("☕ Commande enregistrée !");
            break;
        case "2":
            Console.WriteLine("📦 Stock : 250g café, 500ml lait");
            break;
        case "3":
            Console.WriteLine("💰 Ventes du jour : 450€");
            break;
        case "4":
            Console.WriteLine("👋 À bientôt !");
            break;
        default:
            Console.WriteLine("❌ Choix invalide !");
            break;
    }
    
} while (choix != "4");
```

### Exemple : Validation de saisie
```csharp
int quantite;
string saisie;

do
{
    Console.Write("Combien de cafés voulez-vous ? (1-10) : ");
    saisie = Console.ReadLine();
    
    if (!int.TryParse(saisie, out quantite))
    {
        Console.WriteLine("❌ Veuillez saisir un nombre !");
    }
    else if (quantite < 1 || quantite > 10)
    {
        Console.WriteLine("❌ Quantité doit être entre 1 et 10 !");
    }
    
} while (quantite < 1 || quantite > 10);

Console.WriteLine($"✅ Commande validée : {quantite} café(s)");
```

---

## 4. La boucle `foreach` : Parcourir des collections

La boucle `foreach` est parfaite pour traiter chaque élément d'une collection. Plus simple et plus sûre que `for` !

### Syntaxe simple
```csharp
foreach (type element in collection)
{
    // Utiliser element
}
```

### Exemple : Afficher le menu
```csharp
string[] menuCafes = {"Espresso", "Americano", "Cappuccino", "Latte", "Macchiato"};

Console.WriteLine("☕ === NOTRE CARTE ===");

foreach (string cafe in menuCafes)
{
    Console.WriteLine($"- {cafe}");
}
```

### ⚠️ Erreurs courantes avec foreach

```csharp
// ❌ ERREUR #1 : Essayer de modifier la collection pendant le parcours
List<string> clients = new List<string> {"Marie", "Paul", "Julie"};

foreach (string client in clients)
{
    if (client == "Paul")
    {
        clients.Remove(client); // ERREUR ! Modifie la collection en cours de parcours
    }
}

// ❌ ERREUR #2 : Essayer de modifier l'élément actuel
int[] prix = {2, 4, 3, 5};
foreach (int p in prix)
{
    p = p * 2; // ❌ N'a AUCUN effet sur le tableau !
}

// ✅ CORRECT : Solutions pour modifier
// Solution 1 : Utiliser for pour modifier les éléments
for (int i = 0; i < prix.Length; i++)
{
    prix[i] = prix[i] * 2; // ✅ Modifie vraiment le tableau
}

// Solution 2 : Créer une nouvelle collection pour les suppressions
List<string> clients = new List<string> {"Marie", "Paul", "Julie"};
List<string> clientsASupprimer = new List<string>();

foreach (string client in clients)
{
    if (client == "Paul")
    {
        clientsASupprimer.Add(client);
    }
}

foreach (string client in clientsASupprimer)
{
    clients.Remove(client); // ✅ Suppression sécurisée
}
```

**Avantages de foreach :**
- ✅ Plus simple à écrire
- ✅ Pas de risque de dépasser les limites
- ✅ Plus lisible
- ✅ Fonctionne avec toutes les collections

### Exemple : Calcul de stock total
```csharp
int[] stockParProduit = {45, 32, 28, 51, 19, 37}; // en unités
string[] nomsProduits = {"Café grain", "Lait", "Sucre", "Cups", "Couvercles", "Serviettes"};
int stockTotal = 0;

Console.WriteLine("📦 === ÉTAT DU STOCK ===");

for (int i = 0; i < stockParProduit.Length; i++)
{
    Console.WriteLine($"{nomsProduits[i]} : {stockParProduit[i]} unités");
    stockTotal += stockParProduit[i];
}

Console.WriteLine($"\n📊 Stock total : {stockTotal} articles");

// Utilisation de foreach pour les alertes
Console.WriteLine("\n⚠️ === ALERTES STOCK ===");
foreach (int stock in stockParProduit)
{
    if (stock < 30)
    {
        Console.WriteLine($"Stock faible détecté : {stock} unités");
    }
}
```

### Exemple : Traitement des commandes en attente
```csharp
class Commande
{
    public string Client { get; set; }
    public string Produit { get; set; }
    public double Prix { get; set; }
}

List<Commande> commandesEnAttente = new List<Commande>
{
    new Commande { Client = "Marie", Produit = "Cappuccino", Prix = 4.00 },
    new Commande { Client = "Paul", Produit = "Espresso", Prix = 2.50 },
    new Commande { Client = "Julie", Produit = "Latte", Prix = 4.50 },
    new Commande { Client = "Tom", Produit = "Americano", Prix = 3.00 }
};

Console.WriteLine("📋 === TRAITEMENT DES COMMANDES ===");
double totalVentes = 0;

foreach (Commande cmd in commandesEnAttente)
{
    Console.WriteLine($"🔄 Préparation de {cmd.Produit} pour {cmd.Client}");
    Console.WriteLine($"   Prix : {cmd.Prix:C2}");
    totalVentes += cmd.Prix;
    
    // Simulation du temps de préparation
    System.Threading.Thread.Sleep(800);
    
    Console.WriteLine($"✅ {cmd.Produit} prêt pour {cmd.Client} !");
    Console.WriteLine();
}

Console.WriteLine($"💰 Total des ventes : {totalVentes:C2}");
```

---

## 5. Contrôle des boucles : `break` et `continue`

### `break` : Sortir de la boucle
```csharp
int[] stockProduits = {50, 30, 15, 8, 45, 32};
string[] nomsProduits = {"Café", "Lait", "Sucre", "Tasses", "Couvercles", "Serviettes"};

Console.WriteLine("🔍 Recherche du premier produit en rupture :");

for (int i = 0; i < stockProduits.Length; i++)
{
    Console.WriteLine($"Vérification {nomsProduits[i]} : {stockProduits[i]} unités");
    
    if (stockProduits[i] < 10)
    {
        Console.WriteLine($"⚠️ RUPTURE DÉTECTÉE : {nomsProduits[i]} !");
        Console.WriteLine("Arrêt de la vérification.");
        break; // Sort de la boucle
    }
}
```

### `continue` : Passer à l'itération suivante
```csharp
int[] commandesParHeure = {5, 12, 8, 0, 15, 23, 18, 9};

Console.WriteLine("📊 Rapport des heures d'activité :");

for (int heure = 0; heure < commandesParHeure.Length; heure++)
{
    if (commandesParHeure[heure] == 0)
    {
        Console.WriteLine($"Heure {heure + 8}h : Fermé");
        continue; // Passe à l'heure suivante
    }
    
    Console.WriteLine($"Heure {heure + 8}h : {commandesParHeure[heure]} commandes");
    
    if (commandesParHeure[heure] > 20)
    {
        Console.WriteLine("   🔥 Heure de pointe !");
    }
}
```

---

## 6. Boucles imbriquées : Boucles dans des boucles

### Exemple : Menu par catégorie
```csharp
string[,] menuCategories = {
    {"CAFÉS CHAUDS", "Espresso", "Americano", "Cappuccino"},
    {"CAFÉS FROIDS", "Iced Coffee", "Frappé", "Cold Brew"},
    {"THÉS", "Earl Grey", "Thé Vert", "Tisane"}
};

Console.WriteLine("☕ === MENU COMPLET ===");

for (int categorie = 0; categorie < 3; categorie++)
{
    Console.WriteLine($"\n📋 {menuCategories[categorie, 0]}");
    Console.WriteLine(new string('-', menuCategories[categorie, 0].Length + 4));
    
    for (int produit = 1; produit < 4; produit++)
    {
        Console.WriteLine($"  • {menuCategories[categorie, produit]}");
    }
}
```

### Exemple : Grille d'évaluation qualité
```csharp
string[] criteres = {"Arôme", "Goût", "Acidité", "Corps"};
int[,] evaluations = {
    {8, 9, 7, 8},  // Arabica Colombie
    {7, 8, 6, 9},  // Robusta Vietnam  
    {9, 8, 8, 7},  // Arabica Éthiopie
    {8, 8, 7, 8}   // Blend Maison
};
string[] cafes = {"Arabica Colombie", "Robusta Vietnam", "Arabica Éthiopie", "Blend Maison"};

Console.WriteLine("⭐ === ÉVALUATION DES CAFÉS ===");

for (int cafe = 0; cafe < cafes.Length; cafe++)
{
    Console.WriteLine($"\n☕ {cafes[cafe]}");
    int total = 0;
    
    for (int critere = 0; critere < criteres.Length; critere++)
    {
        int note = evaluations[cafe, critere];
        Console.WriteLine($"  {criteres[critere]} : {note}/10");
        total += note;
    }
    
    double moyenne = (double)total / criteres.Length;
    Console.WriteLine($"  📊 Moyenne : {moyenne:F1}/10");
}
```

---

## 7. Exemple complet : Gestion d'une journée au café

```csharp
using System;
using System.Collections.Generic;

class ProgrammeJourneeCafe
{
    static void Main()
    {
        // Données de départ
        string[] produits = {"Espresso", "Cappuccino", "Latte", "Americano"};
        double[] prix = {2.50, 4.00, 4.50, 3.00};
        int[] stock = {100, 80, 70, 90}; // unités disponibles
        
        List<string> ventesDuJour = new List<string>();
        double chiffreAffaires = 0;
        
        Console.WriteLine("☕ === OUVERTURE DU CAFÉ ===");
        Console.WriteLine("Bonjour ! Voici notre menu :");
        
        // Affichage du menu avec foreach
        for (int i = 0; i < produits.Length; i++)
        {
            Console.WriteLine($"{i + 1}. {produits[i]} - {prix[i]:C2} (Stock: {stock[i]})");
        }
        
        // Simulation d'une journée de ventes
        Random random = new Random();
        int heuresOuverture = 8;
        
        Console.WriteLine("\n🔄 === DÉBUT DES VENTES ===");
        
        for (int heure = 0; heure < heuresOuverture; heure++)
        {
            Console.WriteLine($"\n⏰ Heure {heure + 8}h :");
            
            // Nombre aléatoire de clients par heure (1 à 5)
            int clientsThisHour = random.Next(1, 6);
            
            for (int client = 1; client <= clientsThisHour; client++)
            {
                // Client choisit un produit aléatoire
                int choix = random.Next(0, produits.Length);
                
                if (stock[choix] > 0)
                {
                    // Vente réussie
                    stock[choix]--;
                    chiffreAffaires += prix[choix];
                    ventesDuJour.Add(produits[choix]);
                    
                    Console.WriteLine($"  ✅ Client {client}: {produits[choix]} vendu ({prix[choix]:C2})");
                }
                else
                {
                    // Stock épuisé
                    Console.WriteLine($"  ❌ Client {client}: {produits[choix]} non disponible (rupture de stock)");
                }
            }
        }
        
        // Rapport de fin de journée
        Console.WriteLine("\n📊 === RAPPORT DE FIN DE JOURNÉE ===");
        Console.WriteLine($"💰 Chiffre d'affaires : {chiffreAffaires:C2}");
        Console.WriteLine($"📦 Total ventes : {ventesDuJour.Count} produits");
        
        // Comptage des ventes par produit avec foreach
        Console.WriteLine("\n📋 Détail des ventes :");
        foreach (string produit in produits)
        {
            int compteur = 0;
            foreach (string vente in ventesDuJour)
            {
                if (vente == produit)
                    compteur++;
            }
            Console.WriteLine($"  {produit} : {compteur} unités");
        }
        
        // Stock restant
        Console.WriteLine("\n📦 Stock restant :");
        for (int i = 0; i < produits.Length; i++)
        {
            Console.WriteLine($"  {produits[i]} : {stock[i]} unités");
            
            if (stock[i] < 10)
            {
                Console.WriteLine($"    ⚠️ Stock faible ! Réapprovisionner");
            }
        }
        
        Console.WriteLine("\n👋 Fermeture du café. À demain !");
    }
}
```

---

## 8. Performance et bonnes pratiques

### ✅ Évitez les boucles infinies
```csharp
// ❌ Danger : boucle infinie
// while (true) { /* ... */ }

// ✅ Ajoutez toujours une condition de sortie
int tentatives = 0;
int maxTentatives = 100;

while (tentatives < maxTentatives)
{
    // Votre code
    tentatives++;
    
    if (conditionDeSortie)
        break;
}
```

### ✅ Choisissez la bonne boucle
```csharp
// ✅ Utilisez for pour un nombre connu d'itérations
for (int i = 0; i < 10; i++) { /* ... */ }

// ✅ Utilisez while pour une condition dynamique
while (clientsEnAttente > 0) { /* ... */ }

// ✅ Utilisez foreach pour parcourir des collections
foreach (string item in liste) { /* ... */ }
```

### ✅ Optimisez les boucles imbriquées
```csharp
// ❌ Recalcul inutile à chaque itération
for (int i = 0; i < items.Length; i++)
{
    for (int j = 0; j < getExpensiveValue(); j++) // Coûteux !
    {
        // ...
    }
}

// ✅ Calculez une seule fois
int limite = getExpensiveValue();
for (int i = 0; i < items.Length; i++)
{
    for (int j = 0; j < limite; j++)
    {
        // ...
    }
}
```

---

## 📋 Récapitulatif pour débutants

### Quelle boucle choisir ?

| Situation | Boucle recommandée | Pourquoi ? |
|-----------|-------------------|------------|
| Nombre de répétitions connu | `for` | Plus claire, compteur automatique |
| Condition à vérifier | `while` | Flexibilité maximale |
| Parcours d'une collection | `foreach` | Plus simple et sûre |
| Au moins une exécution | `do...while` | Garantit une exécution |

### ⚠️ Pièges les plus dangereux à éviter

1. **Boucles infinies** : Toujours modifier la condition dans `while`
2. **Index hors limites** : Utiliser `<` (pas `<=`) dans les boucles `for`
3. **Modifier pendant le parcours** : Ne pas changer une collection dans `foreach`
4. **Oubli d'incrémentation** : Toujours avoir `i++` dans `for`

### 🎯 Conseils pour débuter

```csharp
// ✅ TESTEZ vos conditions avant d'écrire la boucle
int compteur = 5;
while (compteur > 0) // ✅ Condition claire
{
    Console.WriteLine(compteur);
    compteur--; // ✅ Modification claire
}

// ✅ PRÉFÉREZ foreach quand c'est possible
string[] cafes = {"Espresso", "Latte"};
foreach (string cafe in cafes) // ✅ Simple et sûr
{
    Console.WriteLine(cafe);
}

// ✅ UTILISEZ des noms de variables clairs
for (int numeroCafe = 1; numeroCafe <= 5; numeroCafe++) // ✅ Explicite
{
    Console.WriteLine($"Café n°{numeroCafe}");
}
```

---

## Exercice pratique simple

**Créez un programme de commande de café qui :**
1. Affiche le menu (foreach)
2. Demande le nombre de cafés (do...while pour validation)
3. Prépare chaque café (for)

**Solution exemple :**
```csharp
class ExerciceBoucles
{
    static void Main()
    {
        // 1. Affichage du menu
        string[] menu = {"Espresso", "Cappuccino", "Latte"};
        Console.WriteLine("☕ === MENU ===");
        foreach (string cafe in menu)
        {
            Console.WriteLine($"- {cafe}");
        }
        
        // 2. Validation de la quantité
        int quantite;
        do
        {
            Console.Write("Combien de cafés ? (1-5) : ");
        } while (!int.TryParse(Console.ReadLine(), out quantite) || 
                 quantite < 1 || quantite > 5);
        
        // 3. Préparation
        for (int i = 1; i <= quantite; i++)
        {
            Console.WriteLine($"☕ Préparation du café n°{i}...");
        }
        
        Console.WriteLine($"✅ {quantite} café(s) prêt(s) !");
    }
}
```

---

## Conclusion

Les boucles sont les **outils d'automatisation** de la programmation ! Elles nous permettent de :

- ✅ **Répéter efficacement** des tâches avec `for`
- ✅ **Traiter des conditions dynamiques** avec `while`
- ✅ **Parcourir des collections** avec `foreach`
- ✅ **Éviter les erreurs courantes** en suivant les bonnes pratiques

**Points clés à retenir :**
- 🔄 **Choisissez la bonne boucle** selon la situation
- ⚠️ **Attention aux boucles infinies** - toujours modifier la condition
- 🛡️ **foreach est plus sûr** que for pour parcourir des collections
- 🎯 **Testez vos conditions** avant d'écrire la boucle

**Prochaine étape :** Maintenant que vous maîtrisez les répétitions, vous pouvez apprendre les collections pour organiser vos données !

**Félicitations !** Vous savez maintenant automatiser vos tâches comme un pro ! ☕

---