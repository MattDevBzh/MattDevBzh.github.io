---
layout: post
title: "Collections et tableaux en C# : Organiser l'inventaire de votre café"
date: 2025-01-29
---

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

### ⚠️ Erreurs courantes avec les tableaux

```csharp
// ❌ ERREUR #1 : Dépasser la taille du tableau
string[] cafes = {"Espresso", "Cappuccino", "Latte"};
Console.WriteLine(cafes[5]); // PLANTAGE ! Index 5 n'existe pas (max = 2)

// ❌ ERREUR #2 : Oublier que les index commencent à 0
string[] cafes = {"Espresso", "Cappuccino", "Latte"}; // 3 éléments
// Index valides : 0, 1, 2 (pas 1, 2, 3 !)

// ❌ ERREUR #3 : Essayer de changer la taille
string[] cafes = new string[3];
// cafes.Length = 5; // IMPOSSIBLE ! La taille est fixe

// ✅ CORRECT : Vérifier les limites
string[] cafes = {"Espresso", "Cappuccino", "Latte"};
int index = 2;
if (index >= 0 && index < cafes.Length)
{
    Console.WriteLine(cafes[index]); // Sécurisé !
}
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

### ⚠️ Pièges courants avec les listes

```csharp
// ❌ PIÈGE #1 : Modifier une liste pendant qu'on la parcourt
List<string> clients = new List<string> {"Marie", "Paul", "Julie"};
foreach (string client in clients)
{
    if (client == "Paul")
    {
        clients.Remove(client); // ERREUR ! Modifie la liste pendant le parcours
    }
}

// ✅ CORRECT : Utiliser une boucle for inverse ou une liste temporaire
for (int i = clients.Count - 1; i >= 0; i--)
{
    if (clients[i] == "Paul")
    {
        clients.RemoveAt(i); // OK !
    }
}

// ❌ PIÈGE #2 : Confondre Remove et RemoveAt
List<int> numeros = new List<int> {10, 20, 30};
numeros.Remove(1);    // Supprime la VALEUR 1 (pas l'index 1 !)
numeros.RemoveAt(1);  // Supprime l'élément à l'INDEX 1

// ❌ PIÈGE #3 : Accès à un index inexistant (comme les tableaux)
List<string> cafes = new List<string> {"Espresso"};
Console.WriteLine(cafes[5]); // PLANTAGE !

// ✅ CORRECT : Vérification avant accès
if (index >= 0 && index < cafes.Count)
{
    Console.WriteLine(cafes[index]);
}
```
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

Les dictionnaires stockent des paires clé-valeur. Parfait pour associer des informations ! C'est comme un carnet d'adresses : nom → téléphone.

### Exemple simple : Carte des prix
```csharp
Dictionary<string, double> cartePrix = new Dictionary<string, double>
{
    {"Espresso", 2.50},
    {"Cappuccino", 4.00},
    {"Latte", 4.50}
};

// Accès sécurisé à une valeur
string cafeRecherche = "Latte";
if (cartePrix.ContainsKey(cafeRecherche))
{
    Console.WriteLine($"Prix du {cafeRecherche} : {cartePrix[cafeRecherche]:C2}");
}
else
{
    Console.WriteLine($"{cafeRecherche} non disponible");
}
```

### ⚠️ Erreurs courantes avec les dictionnaires

```csharp
Dictionary<string, double> prix = new Dictionary<string, double>
{
    {"Espresso", 2.50},
    {"Cappuccino", 4.00}
};

// ❌ ERREUR #1 : Accès direct sans vérifier si la clé existe
double prixLatte = prix["Latte"]; // PLANTAGE ! Clé inexistante

// ❌ ERREUR #2 : Ajouter une clé qui existe déjà
prix.Add("Espresso", 3.00); // ERREUR ! Clé déjà présente

// ❌ ERREUR #3 : Clés avec casse différente
prix.Add("ESPRESSO", 3.00); // Considéré comme différent d'"Espresso"

// ✅ CORRECT : Vérifications appropriées
// Pour lire :
if (prix.ContainsKey("Latte"))
{
    Console.WriteLine($"Prix : {prix["Latte"]}");
}

// Pour ajouter/modifier :
prix["Latte"] = 4.50; // Ajoute si n'existe pas, modifie sinon

// Pour obtenir avec valeur par défaut :
double prixDefault = prix.GetValueOrDefault("Thé", 2.00); // 2.00 si pas trouvé
```

### Conseils pour bien utiliser les dictionnaires

```csharp
// ✅ BONNE PRATIQUE : TryGetValue pour éviter les exceptions
Dictionary<string, double> prix = new Dictionary<string, double>
{
    {"Espresso", 2.50},
    {"Cappuccino", 4.00}
};

// Méthode sûre :
if (prix.TryGetValue("Latte", out double prixLatte))
{
    Console.WriteLine($"Prix trouvé : {prixLatte}");
}
else
{
    Console.WriteLine("Café non trouvé dans la carte");
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

## 📋 Récapitulatif pour débutants

### Quand utiliser quelle collection ?

| Situation | Collection à utiliser | Pourquoi ? |
|-----------|----------------------|------------|
| Taille fixe connue | `Array` | Plus rapide, mémoire optimisée |
| Taille variable | `List<T>` | Flexible, facile à utiliser |
| Recherche par clé | `Dictionary<K,V>` | Accès ultra-rapide |
| Éviter les doublons | `HashSet<T>` | Unicité garantie |

### ⚠️ Pièges les plus fréquents à éviter

1. **Index hors limites** : Toujours vérifier `index < collection.Count`
2. **Modifier pendant le parcours** : Utiliser une boucle `for` inverse
3. **Oublier que les index commencent à 0** : Premier élément = index 0
4. **Dictionnaire : accès direct sans vérification** : Utiliser `ContainsKey()` ou `TryGetValue()`
5. **Performance : créer des collections dans des boucles** : Réutiliser quand possible

### 🎯 Conseils pour bien commencer

```csharp
// ✅ TOUJOURS vérifier avant d'accéder
if (index >= 0 && index < liste.Count)
{
    var element = liste[index];
}

// ✅ TOUJOURS vérifier les clés de dictionnaire
if (dictionnaire.ContainsKey(cle))
{
    var valeur = dictionnaire[cle];
}

// ✅ UTILISER des noms explicites
List<string> nomsClients = new List<string>(); // ✅ Clair
List<string> data = new List<string>();        // ❌ Vague
```

---

## Exercice pratique simple

**Créez un mini-système de café avec :**
1. Liste des cafés disponibles
2. Stock de chaque café (dictionnaire)  
3. Commandes des clients

**Solution exemple :**
```csharp
class MiniCafeSystem
{
    static void Main()
    {
        // 1. Liste des cafés
        List<string> menuCafes = new List<string> {"Espresso", "Cappuccino", "Latte"};
        
        // 2. Stock
        Dictionary<string, int> stocks = new Dictionary<string, int>
        {
            {"Espresso", 10},
            {"Cappuccino", 5},
            {"Latte", 3}
        };
        
        // 3. Commandes
        List<string> commandes = new List<string>();
        
        // Exemple de commande
        string cafeVoulu = "Cappuccino";
        if (stocks.ContainsKey(cafeVoulu) && stocks[cafeVoulu] > 0)
        {
            commandes.Add(cafeVoulu);
            stocks[cafeVoulu]--;
            Console.WriteLine($"✅ {cafeVoulu} commandé ! Stock restant : {stocks[cafeVoulu]}");
        }
        else
        {
            Console.WriteLine($"❌ {cafeVoulu} non disponible");
        }
    }
}
```

---

## Conclusion

Les collections sont les **outils d'organisation** de la programmation ! Elles nous permettent de :

- ✅ **Stocker des données structurées** avec les tableaux
- ✅ **Gérer des listes dynamiques** avec `List<T>`
- ✅ **Associer des informations** avec `Dictionary<K,V>`
- ✅ **Éviter les erreurs courantes** en vérifiant les limites

**Points clés à retenir :**
- 🔍 **Vérifiez toujours** les index et les clés avant d'accéder
- 📏 **Choisissez la bonne collection** selon vos besoins
- 🎯 **Commencez simple** avec `List<T>` et `Dictionary<K,V>`
- ⚠️ **Attention aux modifications** pendant les parcours

**Prochaine étape :** Maintenant que vous savez organiser vos données, vous pouvez apprendre la gestion des erreurs pour créer des programmes robustes !

**Félicitations !** Vous savez maintenant organiser vos données comme un pro ! ☕

---