---
layout: post
title: "Boucles et itérations en C# : Automatiser la préparation de vos cafés"
date: 2025-01-28
---

![Illustration boucles et itérations](/assets/images/boucles-illustration.svg)

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

### Syntaxe
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

### Syntaxe
```csharp
while (condition)
{
    // Code à répéter
}
```

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

La boucle `foreach` est parfaite pour traiter chaque élément d'une collection.

### Syntaxe
```csharp
foreach (type element in collection)
{
    // Utiliser element
}
```

### Exemple : Afficher tous les produits
```csharp
string[] menuCafes = {"Espresso", "Americano", "Cappuccino", "Latte", "Macchiato", "Mocha"};

Console.WriteLine("☕ === NOTRE CARTE ===");

foreach (string cafe in menuCafes)
{
    Console.WriteLine($"- {cafe}");
}
```

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

## Exercices pratiques

### Exercice 1 : Calcul de moyenne
Créez un programme qui calcule la note moyenne d'évaluation de différents cafés.

### Exercice 2 : Jeu de devinette
Créez un jeu où l'utilisateur doit deviner le prix d'un café. Utilisez une boucle `do...while` pour permettre plusieurs tentatives.

### Exercice 3 : Générateur de facture
Créez un programme qui génère une facture pour plusieurs commandes en utilisant `foreach`.

---

## Conclusion

Les boucles sont les **outils d'automatisation** de la programmation ! Elles nous permettent de :

- ✅ **Répéter efficacement** des tâches avec `for`
- ✅ **Traiter des conditions dynamiques** avec `while`
- ✅ **Parcourir des collections** avec `foreach`
- ✅ **Contrôler l'exécution** avec `break` et `continue`

Comme un café qui sert des dizaines de clients avec la même qualité, les boucles garantissent la répétition fiable de nos processus !

**Prochaine étape :** Nous découvrirons les collections et tableaux pour organiser et gérer efficacement nos données de café ! ☕

---

*Pratiquez ces exemples et créez vos propres scénarios. Comme la préparation du café parfait, la maîtrise des boucles vient avec la répétition ! 🚀*