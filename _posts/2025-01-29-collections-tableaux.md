---
layout: post
title: "Collections et tableaux en C# : Organiser l'inventaire de votre café"
date: 2025-01-29
---

<svg width="400" height="200" viewBox="0 0 400 200" xmlns="http://www.w3.org/2000/svg">
  <!-- Background -->
  <rect width="400" height="200" fill="#f8f9fa"/>
  
  <!-- Array/Collection representation -->
  <g>
    <!-- Array structure -->
    <rect x="80" y="80" width="240" height="60" fill="none" stroke="#333" stroke-width="2"/>
    
    <!-- Array elements -->
    <rect x="85" y="85" width="35" height="50" fill="#8B4513" stroke="#333"/>
    <rect x="125" y="85" width="35" height="50" fill="#D2691E" stroke="#333"/>
    <rect x="165" y="85" width="35" height="50" fill="#CD853F" stroke="#333"/>
    <rect x="205" y="85" width="35" height="50" fill="#A0522D" stroke="#333"/>
    <rect x="245" y="85" width="35" height="50" fill="#8B4513" stroke="#333"/>
    <rect x="285" y="85" width="35" height="50" fill="#D2691E" stroke="#333"/>
    
    <!-- Array labels -->
    <text x="102" y="110" fill="white" font-family="Arial" font-size="8" text-anchor="middle">Arabica</text>
    <text x="142" y="110" fill="white" font-family="Arial" font-size="8" text-anchor="middle">Robusta</text>
    <text x="182" y="110" fill="white" font-family="Arial" font-size="8" text-anchor="middle">Moka</text>
    <text x="222" y="110" fill="white" font-family="Arial" font-size="8" text-anchor="middle">Kona</text>
    <text x="262" y="110" fill="white" font-family="Arial" font-size="8" text-anchor="middle">Blue M.</text>
    <text x="302" y="110" fill="white" font-family="Arial" font-size="8" text-anchor="middle">Espresso</text>
    
    <!-- Indices -->
    <text x="102" y="155" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">[0]</text>
    <text x="142" y="155" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">[1]</text>
    <text x="182" y="155" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">[2]</text>
    <text x="222" y="155" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">[3]</text>
    <text x="262" y="155" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">[4]</text>
    <text x="302" y="155" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">[5]</text>
    
    <!-- Array name -->
    <text x="50" y="110" fill="#333" font-family="Arial" font-size="12" font-weight="bold">grains[]</text>
  </g>
  
  <!-- Title -->
  <text x="200" y="25" fill="#333" font-family="Arial" font-size="16" font-weight="bold" text-anchor="middle">Collections et Tableaux</text>
  <text x="200" y="45" fill="#666" font-family="Arial" font-size="12" text-anchor="middle">Organiser l'inventaire de votre café ☕</text>
  <text x="200" y="185" fill="#666" font-family="Arial" font-size="10" text-anchor="middle">string[] grains = {"Arabica", "Robusta", "Moka", "Kona", "Blue Mountain", "Espresso"}</text>
</svg>

Un café bien géré, c'est un café où tout est **organisé et facilement accessible** ! Comme les étagères de grains, les collections de tasses ou la liste des clients fidèles. En C#, les **collections et tableaux** nous permettent de stocker et organiser efficacement nos données. ☕

Découvrons ensemble comment gérer l'inventaire complet de notre café virtuel !

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une collection ?

Une **collection** est un conteneur qui peut stocker plusieurs éléments du même type. C'est comme :

- 📦 **Un bac de grains** contenant différentes variétés
- 📋 **Une liste de commandes** en attente
- 🏪 **Un inventaire de produits** avec leurs prix
- 👥 **Un fichier clients** avec leurs préférences

---

## 1. Les tableaux (`Array`) : Des cases fixes

Un tableau a une **taille fixe** définie à la création. C'est comme un portoir à tasses qui a exactement 20 emplacements.

### Déclaration et initialisation
```csharp
// Déclaration avec taille
string[] menuCafes = new string[5];

// Initialisation avec valeurs
string[] varietesGrains = {"Arabica", "Robusta", "Liberica", "Excelsa"};

// Déclaration et initialisation en une fois
double[] prixMenu = new double[] {2.50, 4.00, 4.50, 3.00, 3.80};
```

### Exemple : Stock de grains par origine
```csharp
// Inventaire des grains par pays
string[] origines = {"Colombie", "Éthiopie", "Guatemala", "Jamaïque", "Yemen"};
int[] stockKilos = {25, 18, 12, 8, 15};

Console.WriteLine("☕ === STOCK DE GRAINS PAR ORIGINE ===");

for (int i = 0; i < origines.Length; i++)
{
    Console.WriteLine($"{origines[i]} : {stockKilos[i]} kg");
    
    if (stockKilos[i] < 10)
    {
        Console.WriteLine($"   ⚠️ Stock faible pour {origines[i]} !");
    }
}

// Calcul du stock total
int stockTotal = 0;
foreach (int stock in stockKilos)
{
    stockTotal += stock;
}

Console.WriteLine($"\n📊 Stock total : {stockTotal} kg");
```

### Exemple : Ventes par jour de la semaine
```csharp
string[] joursSemaine = {"Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche"};
double[] ventesJour = {320.50, 385.20, 410.80, 445.30, 520.90, 680.40, 580.70};

Console.WriteLine("📊 === VENTES HEBDOMADAIRES ===");

// Affichage des ventes
for (int i = 0; i < joursSemaine.Length; i++)
{
    Console.WriteLine($"{joursSemaine[i]} : {ventesJour[i]:C2}");
}

// Jour avec le plus de ventes
double maxVentes = ventesJour[0];
int jourMax = 0;

for (int i = 1; i < ventesJour.Length; i++)
{
    if (ventesJour[i] > maxVentes)
    {
        maxVentes = ventesJour[i];
        jourMax = i;
    }
}

Console.WriteLine($"\n🏆 Meilleur jour : {joursSemaine[jourMax]} ({maxVentes:C2})");
```

---

## 2. Les tableaux multidimensionnels : Organiser en grille

### Tableau à 2 dimensions : Menu avec prix et stocks
```csharp
// [produit, 0=prix, 1=stock]
double[,] inventaireCafe = {
    {2.50, 50},  // Espresso : 2.50€, 50 unités
    {4.00, 35},  // Cappuccino : 4.00€, 35 unités  
    {4.50, 28},  // Latte : 4.50€, 28 unités
    {3.00, 42},  // Americano : 3.00€, 42 unités
    {3.80, 31}   // Macchiato : 3.80€, 31 unités
};

string[] nomsProduits = {"Espresso", "Cappuccino", "Latte", "Americano", "Macchiato"};

Console.WriteLine("📋 === INVENTAIRE DÉTAILLÉ ===");
Console.WriteLine("Produit      | Prix   | Stock");
Console.WriteLine("-------------|--------|-------");

for (int i = 0; i < nomsProduits.Length; i++)
{
    double prix = inventaireCafe[i, 0];
    double stock = inventaireCafe[i, 1];
    
    Console.WriteLine($"{nomsProduits[i],-12} | {prix,6:C2} | {stock,5}");
}
```

### Exemple : Planning des baristas
```csharp
string[,] planningBaristas = {
    {"Marie", "Paul", "Julie"},    // Lundi
    {"Paul", "Tom", "Marie"},      // Mardi
    {"Julie", "Marie", "Paul"},    // Mercredi
    {"Tom", "Julie", "Marie"},     // Jeudi
    {"Marie", "Paul", "Tom"}       // Vendredi
};

string[] jours = {"Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi"};
string[] horaires = {"Matin", "Après-midi", "Soir"};

Console.WriteLine("👥 === PLANNING DES BARISTAS ===");

for (int jour = 0; jour < 5; jour++)
{
    Console.WriteLine($"\n📅 {jours[jour]} :");
    
    for (int creneau = 0; creneau < 3; creneau++)
    {
        Console.WriteLine($"  {horaires[creneau]} : {planningBaristas[jour, creneau]}");
    }
}
```

---

## 3. Les listes (`List<T>`) : Taille dynamique

Les listes peuvent grandir ou diminuer selon les besoins. C'est comme une étagère extensible !

### Déclaration et manipulation de base
```csharp
using System.Collections.Generic;

// Création d'une liste vide
List<string> commandesEnCours = new List<string>();

// Création avec valeurs initiales
List<string> clientsVIP = new List<string> {"Marie Dupont", "Paul Martin", "Julie Leblanc"};

// Ajout d'éléments
commandesEnCours.Add("Cappuccino pour Table 3");
commandesEnCours.Add("2 Espressos pour Emporter");
commandesEnCours.Add("Latte Art pour Marie");

// Affichage
Console.WriteLine("📋 === COMMANDES EN COURS ===");
for (int i = 0; i < commandesEnCours.Count; i++)
{
    Console.WriteLine($"{i + 1}. {commandesEnCours[i]}");
}
```

### Exemple : Gestion dynamique du stock
```csharp
List<string> produitsManquants = new List<string>();
Dictionary<string, int> stocks = new Dictionary<string, int>
{
    {"Café Arabica", 25},
    {"Lait entier", 8},
    {"Sucre blanc", 15},
    {"Tasses carton", 45},
    {"Couvercles", 12}
};

Console.WriteLine("🔍 === VÉRIFICATION DU STOCK ===");

foreach (var produit in stocks)
{
    Console.WriteLine($"{produit.Key} : {produit.Value} unités");
    
    if (produit.Value < 20)
    {
        produitsManquants.Add(produit.Key);
        Console.WriteLine($"   ⚠️ Stock faible !");
    }
}

Console.WriteLine($"\n📦 === COMMANDE À PASSER ({produitsManquants.Count} produits) ===");
foreach (string produit in produitsManquants)
{
    Console.WriteLine($"- {produit}");
}
```

### Exemple : File d'attente dynamique
```csharp
class Client
{
    public string Nom { get; set; }
    public string Commande { get; set; }
    public DateTime HeureCommande { get; set; }
}

List<Client> fileAttente = new List<Client>();

// Arrivée de clients
fileAttente.Add(new Client { Nom = "Sophie", Commande = "Cappuccino", HeureCommande = DateTime.Now });
fileAttente.Add(new Client { Nom = "Marc", Commande = "Espresso", HeureCommande = DateTime.Now.AddMinutes(1) });
fileAttente.Add(new Client { Nom = "Emma", Commande = "Latte", HeureCommande = DateTime.Now.AddMinutes(2) });

Console.WriteLine("👥 === FILE D'ATTENTE ===");
for (int i = 0; i < fileAttente.Count; i++)
{
    var client = fileAttente[i];
    Console.WriteLine($"{i + 1}. {client.Nom} - {client.Commande} ({client.HeureCommande:HH:mm})");
}

// Servir le premier client
if (fileAttente.Count > 0)
{
    Client clientServi = fileAttente[0];
    fileAttente.RemoveAt(0);
    Console.WriteLine($"\n✅ {clientServi.Nom} servi(e) ! Plus que {fileAttente.Count} clients en attente.");
}
```

---

## 4. Les dictionnaires (`Dictionary<K,V>`) : Clé-valeur

Les dictionnaires stockent des paires clé-valeur. Parfait pour associer des informations !

### Exemple : Carte des prix
```csharp
Dictionary<string, double> cartePrix = new Dictionary<string, double>
{
    {"Espresso", 2.50},
    {"Cappuccino", 4.00},
    {"Latte", 4.50},
    {"Americano", 3.00},
    {"Macchiato", 3.80},
    {"Mocha", 5.00}
};

Console.WriteLine("💰 === CARTE DES PRIX ===");
foreach (var item in cartePrix)
{
    Console.WriteLine($"{item.Key,-12} : {item.Value:C2}");
}

// Recherche d'un prix
string cafeRecherche = "Latte";
if (cartePrix.ContainsKey(cafeRecherche))
{
    Console.WriteLine($"\n🔍 Prix du {cafeRecherche} : {cartePrix[cafeRecherche]:C2}");
}
else
{
    Console.WriteLine($"\n❌ {cafeRecherche} non trouvé dans la carte");
}
```

### Exemple : Préférences des clients
```csharp
Dictionary<string, List<string>> preferencesClients = new Dictionary<string, List<string>>
{
    {"Marie", new List<string> {"Cappuccino", "Sucre brun", "Lait d'avoine"}},
    {"Paul", new List<string> {"Espresso", "Sans sucre", "Double dose"}},
    {"Julie", new List<string> {"Latte", "Vanille", "Lait écrémé"}},
    {"Tom", new List<string> {"Americano", "Miel", "Grande taille"}}
};

Console.WriteLine("💡 === PRÉFÉRENCES CLIENTS ===");

foreach (var client in preferencesClients)
{
    Console.WriteLine($"\n👤 {client.Key} :");
    foreach (string preference in client.Value)
    {
        Console.WriteLine($"   • {preference}");
    }
}

// Personnaliser une commande
string clientActuel = "Marie";
if (preferencesClients.ContainsKey(clientActuel))
{
    Console.WriteLine($"\n☕ Préparation personnalisée pour {clientActuel} :");
    foreach (string pref in preferencesClients[clientActuel])
    {
        Console.WriteLine($"✓ {pref}");
    }
}
```

---

## 5. Les HashSet : Collections uniques

Un HashSet ne contient pas de doublons. Parfait pour les listes d'allergènes ou d'ingrédients !

### Exemple : Gestion des allergènes
```csharp
HashSet<string> allergenesPresents = new HashSet<string>();

// Ajouter des allergènes
allergenesPresents.Add("Lait");
allergenesPresents.Add("Gluten");
allergenesPresents.Add("Fruits à coque");
allergenesPresents.Add("Lait"); // Sera ignoré (doublon)

Console.WriteLine("⚠️ === ALLERGÈNES PRÉSENTS ===");
foreach (string allergene in allergenesPresents)
{
    Console.WriteLine($"- {allergene}");
}

Console.WriteLine($"\nNombre d'allergènes différents : {allergenesPresents.Count}");

// Vérifier la présence d'un allergène
string allergeneTest = "Lait";
if (allergenesPresents.Contains(allergeneTest))
{
    Console.WriteLine($"\n⚠️ Attention : Produits contenant du {allergeneTest} !");
}
```

---

## 6. LINQ : Requêtes sur les collections

LINQ (Language Integrated Query) permet de faire des requêtes sophistiquées sur les collections.

### Exemple : Analyses de ventes
```csharp
using System.Linq;

class Vente
{
    public string Produit { get; set; }
    public double Prix { get; set; }
    public DateTime Date { get; set; }
    public string Client { get; set; }
}

List<Vente> ventesJour = new List<Vente>
{
    new Vente { Produit = "Cappuccino", Prix = 4.00, Date = DateTime.Today.AddHours(8), Client = "Marie" },
    new Vente { Produit = "Espresso", Prix = 2.50, Date = DateTime.Today.AddHours(9), Client = "Paul" },
    new Vente { Produit = "Latte", Prix = 4.50, Date = DateTime.Today.AddHours(10), Client = "Julie" },
    new Vente { Produit = "Cappuccino", Prix = 4.00, Date = DateTime.Today.AddHours(11), Client = "Tom" },
    new Vente { Produit = "Americano", Prix = 3.00, Date = DateTime.Today.AddHours(12), Client = "Emma" }
};

// Ventes de plus de 3€
var ventesCheres = ventesJour.Where(v => v.Prix > 3.00);
Console.WriteLine("💰 === VENTES > 3€ ===");
foreach (var vente in ventesCheres)
{
    Console.WriteLine($"{vente.Produit} - {vente.Prix:C2} ({vente.Client})");
}

// Ventes groupées par produit
var ventesParProduit = ventesJour.GroupBy(v => v.Produit);
Console.WriteLine("\n📊 === VENTES PAR PRODUIT ===");
foreach (var groupe in ventesParProduit)
{
    int quantite = groupe.Count();
    double total = groupe.Sum(v => v.Prix);
    Console.WriteLine($"{groupe.Key} : {quantite} unités, {total:C2}");
}

// Chiffre d'affaires total
double totalJournee = ventesJour.Sum(v => v.Prix);
Console.WriteLine($"\n💰 Total journée : {totalJournee:C2}");

// Produit le plus vendu
var produitPopulaire = ventesJour.GroupBy(v => v.Produit)
                                .OrderByDescending(g => g.Count())
                                .First();
Console.WriteLine($"🏆 Produit populaire : {produitPopulaire.Key} ({produitPopulaire.Count()} ventes)");
```

---

## 7. Exemple complet : Système de gestion de café

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Produit
{
    public string Nom { get; set; }
    public double Prix { get; set; }
    public int Stock { get; set; }
    public List<string> Ingredients { get; set; }
}

class Commande
{
    public string Client { get; set; }
    public List<string> Produits { get; set; }
    public DateTime Heure { get; set; }
    public double Total { get; set; }
}

class GestionCafe
{
    private Dictionary<string, Produit> catalogue;
    private List<Commande> commandesJour;
    private HashSet<string> clientsVIP;

    public GestionCafe()
    {
        InitialiserCatalogue();
        commandesJour = new List<Commande>();
        clientsVIP = new HashSet<string> {"Marie", "Paul", "Julie"};
    }

    private void InitialiserCatalogue()
    {
        catalogue = new Dictionary<string, Produit>
        {
            ["Espresso"] = new Produit 
            { 
                Nom = "Espresso", 
                Prix = 2.50, 
                Stock = 50,
                Ingredients = new List<string> {"Café arabica", "Eau"}
            },
            ["Cappuccino"] = new Produit 
            { 
                Nom = "Cappuccino", 
                Prix = 4.00, 
                Stock = 35,
                Ingredients = new List<string> {"Café arabica", "Lait", "Mousse de lait"}
            },
            ["Latte"] = new Produit 
            { 
                Nom = "Latte", 
                Prix = 4.50, 
                Stock = 28,
                Ingredients = new List<string> {"Café arabica", "Lait", "Mousse légère"}
            }
        };
    }

    public void AfficherCatalogue()
    {
        Console.WriteLine("☕ === CATALOGUE ===");
        Console.WriteLine("Produit      | Prix   | Stock | Ingrédients");
        Console.WriteLine("-------------|--------|-------|------------------");
        
        foreach (var item in catalogue)
        {
            var produit = item.Value;
            string ingredients = string.Join(", ", produit.Ingredients);
            Console.WriteLine($"{produit.Nom,-12} | {produit.Prix,6:C2} | {produit.Stock,5} | {ingredients}");
        }
    }

    public bool PasserCommande(string client, List<string> produitsCommandes)
    {
        // Vérifier la disponibilité
        foreach (string produitNom in produitsCommandes)
        {
            if (!catalogue.ContainsKey(produitNom) || catalogue[produitNom].Stock <= 0)
            {
                Console.WriteLine($"❌ {produitNom} non disponible");
                return false;
            }
        }

        // Calculer le total
        double total = produitsCommandes.Sum(p => catalogue[p].Prix);
        
        // Remise VIP
        if (clientsVIP.Contains(client))
        {
            total *= 0.9; // 10% de remise
            Console.WriteLine($"🌟 Remise VIP appliquée pour {client} !");
        }

        // Créer la commande
        var commande = new Commande
        {
            Client = client,
            Produits = new List<string>(produitsCommandes),
            Heure = DateTime.Now,
            Total = total
        };

        // Décrémenter le stock
        foreach (string produitNom in produitsCommandes)
        {
            catalogue[produitNom].Stock--;
        }

        commandesJour.Add(commande);
        
        Console.WriteLine($"✅ Commande enregistrée pour {client}");
        Console.WriteLine($"   Produits : {string.Join(", ", produitsCommandes)}");
        Console.WriteLine($"   Total : {total:C2}");
        
        return true;
    }

    public void AfficherStatistiques()
    {
        Console.WriteLine("\n📊 === STATISTIQUES DU JOUR ===");
        
        if (commandesJour.Count == 0)
        {
            Console.WriteLine("Aucune commande aujourd'hui.");
            return;
        }

        // Chiffre d'affaires
        double ca = commandesJour.Sum(c => c.Total);
        Console.WriteLine($"💰 Chiffre d'affaires : {ca:C2}");
        
        // Nombre de commandes
        Console.WriteLine($"📋 Nombre de commandes : {commandesJour.Count}");
        
        // Produits les plus vendus
        var produitsVendus = commandesJour.SelectMany(c => c.Produits)
                                         .GroupBy(p => p)
                                         .OrderByDescending(g => g.Count());
        
        Console.WriteLine("\n🏆 Top des ventes :");
        foreach (var groupe in produitsVendus.Take(3))
        {
            Console.WriteLine($"   {groupe.Key} : {groupe.Count()} unités");
        }
        
        // Clients les plus actifs
        var clientsActifs = commandesJour.GroupBy(c => c.Client)
                                       .OrderByDescending(g => g.Count());
        
        Console.WriteLine("\n👥 Clients les plus actifs :");
        foreach (var groupe in clientsActifs.Take(3))
        {
            Console.WriteLine($"   {groupe.Key} : {groupe.Count()} commandes");
        }
    }

    static void Main()
    {
        GestionCafe cafe = new GestionCafe();
        
        // Afficher le catalogue
        cafe.AfficherCatalogue();
        
        // Passer quelques commandes
        Console.WriteLine("\n🔄 === SIMULATION DE COMMANDES ===");
        
        cafe.PasserCommande("Marie", new List<string> {"Cappuccino", "Espresso"});
        cafe.PasserCommande("Paul", new List<string> {"Latte"});
        cafe.PasserCommande("Julie", new List<string> {"Cappuccino"});
        cafe.PasserCommande("Tom", new List<string> {"Espresso", "Espresso"});
        
        // Afficher les statistiques
        cafe.AfficherStatistiques();
        
        Console.WriteLine("\n📦 === STOCK RESTANT ===");
        cafe.AfficherCatalogue();
    }
}
```

---

## 8. Bonnes pratiques et performance

### ✅ Choisir la bonne collection
```csharp
// ✅ Tableau pour taille fixe connue
string[] joursSemaine = new string[7];

// ✅ List<T> pour taille variable
List<string> commandesDuJour = new List<string>();

// ✅ Dictionary<K,V> pour recherche rapide par clé
Dictionary<string, double> prix = new Dictionary<string, double>();

// ✅ HashSet<T> pour unicité
HashSet<string> allergenesPresents = new HashSet<string>();
```

### ✅ Initialiser avec la bonne capacité
```csharp
// ❌ La liste va grandir 100 fois
List<string> commandes = new List<string>();
for (int i = 0; i < 100; i++)
{
    commandes.Add($"Commande {i}");
}

// ✅ Meilleure performance
List<string> commandes = new List<string>(100); // Capacité initiale
```

### ✅ Utiliser LINQ avec modération
```csharp
// ✅ Simple et lisible
var ventesCheres = ventes.Where(v => v.Prix > 5.00).ToList();

// ❌ Trop complexe, difficile à déboguer
var resultat = ventes.Where(v => v.Prix > 3)
                    .GroupBy(v => v.Client)
                    .Where(g => g.Count() > 2)
                    .SelectMany(g => g.Select(v => v.Produit))
                    .Distinct()
                    .OrderBy(p => p);
```

---

## Exercices pratiques

### Exercice 1 : Gestionnaire de stock
Créez un système qui gère un inventaire avec alerte automatique pour les stocks faibles.

### Exercice 2 : Analyseur de préférences
Créez un programme qui analyse les préférences des clients et recommande des produits.

### Exercice 3 : Planificateur de tournées
Créez un système qui organise les livraisons de grains selon les distances.

---

## Conclusion

Les collections sont les **outils d'organisation** de la programmation ! Elles nous permettent de :

- ✅ **Stocker des données structurées** avec les tableaux
- ✅ **Gérer des listes dynamiques** avec `List<T>`
- ✅ **Associer des informations** avec `Dictionary<K,V>`
- ✅ **Garantir l'unicité** avec `HashSet<T>`
- ✅ **Analyser les données** avec LINQ

Comme un café bien organisé où chaque produit a sa place, les collections nous aident à structurer nos programmes efficacement !

**Prochaine étape :** Nous découvrirons la gestion des exceptions pour traiter les erreurs avec élégance ! ☕

---

*Expérimentez avec ces collections et créez vos propres systèmes de gestion. Un bon développeur, c'est comme un bon gestionnaire de café : il sait organiser ses données ! 🚀*