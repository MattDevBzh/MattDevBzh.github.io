---
layout: post
title: "Méthodes et fonctions en C# : Les recettes secrètes de votre café"
date: 2025-01-31
---

Dans un café, chaque barista a ses **recettes secrètes** : comment obtenir la mousse parfaite, préparer l'espresso idéal, ou calculer rapidement les prix. En programmation C#, les **méthodes et fonctions** sont ces recettes réutilisables qui rendent notre code organisé et efficace ! ☕

Découvrons ensemble comment créer vos propres "recettes de code" !

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une méthode ?

Une **méthode** est un bloc de code réutilisable qui effectue une tâche spécifique. C'est comme une recette de cuisine :

- 📝 **Nom** : "Préparer un cappuccino"
- 🥛 **Ingrédients** (paramètres) : café, lait, sucre
- 🔄 **Étapes** : le code de la méthode
- ☕ **Résultat** : le cappuccino fini (valeur de retour)

---

## 1. Méthodes de base : Sans paramètres ni retour

### Syntaxe
```csharp
[modificateur] [type_retour] NomMethode()
{
    // Corps de la méthode
}
```

### Exemple : Actions simples du café
```csharp
class BaristaCafe
{
    // Méthode pour afficher le message d'accueil
    public static void AfficherAccueil()
    {
        Console.WriteLine("☕ Bienvenue dans notre café !");
        Console.WriteLine("Nous préparons le meilleur café de la ville !");
        Console.WriteLine("Que puis-je vous servir aujourd'hui ?");
    }

    // Méthode pour nettoyer la machine
    public static void NettoyerMachine()
    {
        Console.WriteLine("🧹 Nettoyage de la machine à café...");
        Console.WriteLine("1. Vidange du marc de café");
        Console.WriteLine("2. Rinçage des conduits");
        Console.WriteLine("3. Nettoyage de la buse vapeur");
        Console.WriteLine("✅ Machine propre et prête !");
    }

    // Méthode pour fermer le café
    public static void FermerCafe()
    {
        Console.WriteLine("🌙 Procédure de fermeture...");
        Console.WriteLine("- Arrêt des machines");
        Console.WriteLine("- Nettoyage des surfaces");
        Console.WriteLine("- Fermeture de la caisse");
        Console.WriteLine("✅ Café fermé. À demain !");
    }

    static void Main()
    {
        AfficherAccueil();
        Console.WriteLine();
        
        NettoyerMachine();
        Console.WriteLine();
        
        FermerCafe();
    }
}
```

---

## 2. Méthodes avec paramètres : Personnaliser les recettes

### Exemple : Préparation personnalisée de café
```csharp
class PreparationCafe
{
    // Méthode avec un paramètre
    public static void PreparerEspresso(string client)
    {
        Console.WriteLine($"☕ Préparation d'un espresso pour {client}");
        Console.WriteLine("- Moudre 18g de grains arabica");
        Console.WriteLine("- Tasser la mouture");
        Console.WriteLine("- Extraction 25 secondes");
        Console.WriteLine($"✅ Espresso prêt pour {client} !");
    }

    // Méthode avec plusieurs paramètres
    public static void PreparerCappuccino(string client, bool avecSucre, string typeLait)
    {
        Console.WriteLine($"☕ Préparation d'un cappuccino pour {client}");
        Console.WriteLine("- Préparer un espresso");
        Console.WriteLine($"- Chauffer le {typeLait}");
        Console.WriteLine("- Créer la mousse de lait");
        
        if (avecSucre)
        {
            Console.WriteLine("- Ajouter du sucre");
        }
        
        Console.WriteLine("- Verser la mousse délicatement");
        Console.WriteLine($"✅ Cappuccino prêt pour {client} !");
    }

    // Méthode avec paramètres de différents types
    public static void PreparerCommande(string client, string typeCafe, int quantite, double taille)
    {
        Console.WriteLine($"📋 Commande pour {client}:");
        Console.WriteLine($"   Type: {typeCafe}");
        Console.WriteLine($"   Quantité: {quantite}");
        Console.WriteLine($"   Taille: {taille}cl");
        
        for (int i = 1; i <= quantite; i++)
        {
            Console.WriteLine($"🔄 Préparation n°{i}...");
        }
        
        Console.WriteLine($"✅ {quantite} {typeCafe} de {taille}cl prêts !");
    }

    static void Main()
    {
        PreparerEspresso("Marie");
        Console.WriteLine();
        
        PreparerCappuccino("Paul", true, "lait d'avoine");
        Console.WriteLine();
        
        PreparerCommande("Julie", "Latte", 2, 25.0);
    }
}
```

---

## 3. Méthodes avec valeur de retour : Obtenir un résultat

### Exemple : Calculs pour le café
```csharp
class CalculsCafe
{
    // Méthode qui retourne un prix
    public static double CalculerPrix(string typeCafe, string taille)
    {
        double prixBase = typeCafe switch
        {
            "Espresso" => 2.50,
            "Cappuccino" => 4.00,
            "Latte" => 4.50,
            "Americano" => 3.00,
            _ => 2.00 // Prix par défaut
        };

        double multiplicateur = taille switch
        {
            "S" => 0.8,
            "M" => 1.0,
            "L" => 1.3,
            "XL" => 1.6,
            _ => 1.0
        };

        return prixBase * multiplicateur;
    }

    // Méthode qui retourne du texte
    public static string ObtenirRecommandation(int heure)
    {
        if (heure >= 6 && heure < 10)
        {
            return "☀️ Espresso pour bien commencer la journée !";
        }
        else if (heure >= 10 && heure < 14)
        {
            return "☕ Cappuccino parfait pour la pause matinale !";
        }
        else if (heure >= 14 && heure < 17)
        {
            return "🥛 Latte onctueux pour l'après-midi !";
        }
        else
        {
            return "🌙 Décaféiné pour une soirée relaxante !";
        }
    }

    // Méthode qui retourne un booléen
    public static bool PeutPreparerCafe(string typeCafe, int stockCafe, int stockLait)
    {
        int cafeNecessaire = typeCafe switch
        {
            "Espresso" => 18,
            "Americano" => 18,
            "Cappuccino" => 18,
            "Latte" => 20,
            _ => 15
        };

        int laitNecessaire = typeCafe switch
        {
            "Cappuccino" => 60,
            "Latte" => 150,
            _ => 0
        };

        return stockCafe >= cafeNecessaire && stockLait >= laitNecessaire;
    }

    // Méthode qui retourne un objet complexe
    public static (double prix, int tempsPreparation, string difficulte) 
        ObtenirInfosCafe(string typeCafe)
    {
        return typeCafe switch
        {
            "Espresso" => (2.50, 30, "Facile"),
            "Cappuccino" => (4.00, 120, "Moyenne"),
            "Latte" => (4.50, 90, "Moyenne"),
            "Americano" => (3.00, 45, "Facile"),
            _ => (2.00, 60, "Inconnue")
        };
    }

    static void Main()
    {
        // Test des calculs de prix
        string cafe = "Cappuccino";
        string taille = "L";
        double prix = CalculerPrix(cafe, taille);
        Console.WriteLine($"Prix {cafe} {taille}: {prix:C2}");
        
        // Test des recommandations
        int heureActuelle = 14;
        string recommandation = ObtenirRecommandation(heureActuelle);
        Console.WriteLine($"À {heureActuelle}h: {recommandation}");
        
        // Test de disponibilité
        bool disponible = PeutPreparerCafe("Cappuccino", 50, 100);
        Console.WriteLine($"Cappuccino disponible: {(disponible ? "Oui" : "Non")}");
        
        // Test des infos complexes
        var (prixInfo, temps, difficulte) = ObtenirInfosCafe("Latte");
        Console.WriteLine($"Latte: {prixInfo:C2}, {temps}s, {difficulte}");
    }
}
```

---

## 4. Paramètres optionnels et nommés

### Exemple : Commande flexible
```csharp
class CommandeFlexible
{
    // Méthode avec paramètres optionnels
    public static void PreparerBoisson(
        string typeCafe,
        string client = "Client",
        string taille = "M",
        bool avecSucre = false,
        string typeLait = "lait entier",
        double temperature = 70.0)
    {
        Console.WriteLine($"☕ Préparation de {typeCafe} pour {client}");
        Console.WriteLine($"   Taille: {taille}");
        Console.WriteLine($"   Sucre: {(avecSucre ? "Oui" : "Non")}");
        Console.WriteLine($"   Lait: {typeLait}");
        Console.WriteLine($"   Température: {temperature}°C");
        Console.WriteLine("✅ Boisson prête !");
    }

    // Méthode avec paramètres par référence
    public static void MettreAJourStock(ref int stockCafe, ref int stockLait, string typeCafe)
    {
        Console.WriteLine($"📦 Mise à jour du stock pour {typeCafe}");
        Console.WriteLine($"   Stock avant - Café: {stockCafe}g, Lait: {stockLait}ml");
        
        // Consommation selon le type de café
        switch (typeCafe)
        {
            case "Espresso":
                stockCafe -= 18;
                break;
            case "Cappuccino":
                stockCafe -= 18;
                stockLait -= 60;
                break;
            case "Latte":
                stockCafe -= 20;
                stockLait -= 150;
                break;
        }
        
        Console.WriteLine($"   Stock après - Café: {stockCafe}g, Lait: {stockLait}ml");
    }

    // Méthode avec paramètres de sortie
    public static bool CalculerCommande(string[] produits, double[] prix, 
        out double total, out int nombreItems)
    {
        total = 0;
        nombreItems = 0;
        
        if (produits.Length != prix.Length)
        {
            return false; // Erreur dans les données
        }
        
        for (int i = 0; i < produits.Length; i++)
        {
            total += prix[i];
            nombreItems++;
            Console.WriteLine($"   {produits[i]}: {prix[i]:C2}");
        }
        
        return true; // Succès
    }

    static void Main()
    {
        // Utilisation avec paramètres par défaut
        PreparerBoisson("Cappuccino");
        Console.WriteLine();
        
        // Utilisation avec quelques paramètres personnalisés
        PreparerBoisson("Latte", "Marie", "L");
        Console.WriteLine();
        
        // Utilisation avec paramètres nommés
        PreparerBoisson(
            typeCafe: "Espresso",
            client: "Paul",
            avecSucre: true,
            temperature: 80.0);
        Console.WriteLine();
        
        // Test avec paramètres par référence
        int stock_cafe = 100;
        int stock_lait = 500;
        MettreAJourStock(ref stock_cafe, ref stock_lait, "Cappuccino");
        Console.WriteLine();
        
        // Test avec paramètres de sortie
        string[] commande = {"Espresso", "Cappuccino", "Latte"};
        double[] prixCommande = {2.50, 4.00, 4.50};
        
        if (CalculerCommande(commande, prixCommande, out double total, out int items))
        {
            Console.WriteLine($"💰 Total: {total:C2} pour {items} articles");
        }
    }
}
```

---

## 5. Surcharge de méthodes : Plusieurs versions

### Exemple : Différentes façons de préparer un café
```csharp
class PreparationSurchargee
{
    // Version simple
    public static void PreparerCafe()
    {
        Console.WriteLine("☕ Préparation d'un café standard");
        Console.WriteLine("   Type: Espresso");
        Console.WriteLine("   Taille: M");
        Console.WriteLine("✅ Café prêt !");
    }

    // Version avec type
    public static void PreparerCafe(string typeCafe)
    {
        Console.WriteLine($"☕ Préparation d'un {typeCafe}");
        Console.WriteLine("   Taille: M");
        Console.WriteLine("✅ Café prêt !");
    }

    // Version avec type et taille
    public static void PreparerCafe(string typeCafe, string taille)
    {
        Console.WriteLine($"☕ Préparation d'un {typeCafe} taille {taille}");
        Console.WriteLine("✅ Café prêt !");
    }

    // Version avec type, taille et personnalisation
    public static void PreparerCafe(string typeCafe, string taille, bool avecSucre)
    {
        Console.WriteLine($"☕ Préparation d'un {typeCafe} taille {taille}");
        Console.WriteLine($"   Sucre: {(avecSucre ? "Avec" : "Sans")}");
        Console.WriteLine("✅ Café prêt !");
    }

    // Version avec quantité
    public static void PreparerCafe(string typeCafe, int quantite)
    {
        Console.WriteLine($"☕ Préparation de {quantite}x {typeCafe}");
        for (int i = 1; i <= quantite; i++)
        {
            Console.WriteLine($"   Café n°{i} en cours...");
        }
        Console.WriteLine($"✅ {quantite} cafés prêts !");
    }

    // Version complète avec objet
    public static void PreparerCafe(CommandeCafe commande)
    {
        Console.WriteLine($"☕ Préparation pour {commande.Client}");
        Console.WriteLine($"   Type: {commande.TypeCafe}");
        Console.WriteLine($"   Taille: {commande.Taille}");
        Console.WriteLine($"   Quantité: {commande.Quantite}");
        Console.WriteLine($"   Options: {string.Join(", ", commande.Options)}");
        Console.WriteLine("✅ Commande complète prête !");
    }

    public class CommandeCafe
    {
        public string Client { get; set; }
        public string TypeCafe { get; set; }
        public string Taille { get; set; }
        public int Quantite { get; set; }
        public List<string> Options { get; set; } = new List<string>();
    }

    static void Main()
    {
        // Test des différentes surcharges
        PreparerCafe(); // Version de base
        Console.WriteLine();
        
        PreparerCafe("Cappuccino"); // Avec type
        Console.WriteLine();
        
        PreparerCafe("Latte", "L"); // Avec type et taille
        Console.WriteLine();
        
        PreparerCafe("Espresso", "M", true); // Avec sucre
        Console.WriteLine();
        
        PreparerCafe("Americano", 3); // Quantité multiple
        Console.WriteLine();
        
        // Version avec objet complet
        var commande = new CommandeCafe
        {
            Client = "Marie",
            TypeCafe = "Cappuccino",
            Taille = "L",
            Quantite = 2,
            Options = new List<string> {"Sucre de canne", "Lait d'avoine", "Extra mousse"}
        };
        
        PreparerCafe(commande);
    }
}
```

---

## 6. Méthodes récursives : S'appeler soi-même

### Exemple : Calculs en cascade
```csharp
class MethodesRecursives
{
    // Factorielle - calcul de remise progressive
    public static int CalculerRemiseProgressive(int nombreVisites)
    {
        if (nombreVisites <= 1)
        {
            return 0; // Pas de remise pour 1 visite ou moins
        }
        
        return 2 + CalculerRemiseProgressive(nombreVisites - 1);
    }

    // Fibonacci - calcul de popularité d'un café
    public static int CalculerPopularite(int semaine)
    {
        if (semaine <= 1)
        {
            return 1; // Popularité de base
        }
        
        return CalculerPopularite(semaine - 1) + CalculerPopularite(semaine - 2);
    }

    // Affichage en cascade du menu
    public static void AfficherSousMenus(string[] categories, int niveau = 0)
    {
        if (niveau >= categories.Length)
        {
            return; // Fin de la récursion
        }
        
        // Indentation selon le niveau
        string indentation = new string(' ', niveau * 2);
        Console.WriteLine($"{indentation}📂 {categories[niveau]}");
        
        // Appel récursif pour le niveau suivant
        AfficherSousMenus(categories, niveau + 1);
    }

    // Calcul récursif de commandes groupées
    public static double CalculerPrixGroupe(List<double> prix, int index = 0)
    {
        if (index >= prix.Count)
        {
            return 0; // Fin de la liste
        }
        
        // Prix actuel + prix des éléments suivants
        return prix[index] + CalculerPrixGroupe(prix, index + 1);
    }

    static void Main()
    {
        // Test remise progressive
        int visites = 5;
        int remise = CalculerRemiseProgressive(visites);
        Console.WriteLine($"Remise pour {visites} visites: {remise}%");
        Console.WriteLine();
        
        // Test popularité
        int semaine = 6;
        int popularite = CalculerPopularite(semaine);
        Console.WriteLine($"Popularité semaine {semaine}: {popularite}");
        Console.WriteLine();
        
        // Test menu en cascade
        string[] menus = {"Boissons", "Cafés", "Espressos", "Simple", "Double"};
        Console.WriteLine("Menu hiérarchique:");
        AfficherSousMenus(menus);
        Console.WriteLine();
        
        // Test prix groupé
        var prixCommande = new List<double> {2.50, 4.00, 4.50, 3.00};
        double total = CalculerPrixGroupe(prixCommande);
        Console.WriteLine($"Total commande groupe: {total:C2}");
    }
}
```

---

## 7. Méthodes d'extension : Étendre les types existants

### Exemple : Extensions pour les chaînes de café
```csharp
using System;

// Les méthodes d'extension doivent être dans une classe statique
public static class ExtensionsCafe
{
    // Extension pour formater les noms de café
    public static string FormatNomCafe(this string nom)
    {
        if (string.IsNullOrWhiteSpace(nom))
            return "☕ Café sans nom";
        
        return $"☕ {nom.Trim().ToUpperInvariant()}";
    }

    // Extension pour vérifier si c'est un café chaud
    public static bool EstCafeChaud(this string typeCafe)
    {
        string[] cafesChauds = {"espresso", "cappuccino", "latte", "americano", "macchiato"};
        return Array.Exists(cafesChauds, cafe => 
            cafe.Equals(typeCafe, StringComparison.OrdinalIgnoreCase));
    }

    // Extension pour calculer les calories approximatives
    public static int CalculerCalories(this string typeCafe)
    {
        return typeCafe.ToLower() switch
        {
            "espresso" => 5,
            "americano" => 10,
            "cappuccino" => 80,
            "latte" => 120,
            "macchiato" => 90,
            "mocha" => 200,
            _ => 50 // Valeur par défaut
        };
    }

    // Extension pour obtenir le temps de préparation
    public static TimeSpan ObtenirTempsPreparation(this string typeCafe)
    {
        return typeCafe.ToLower() switch
        {
            "espresso" => TimeSpan.FromSeconds(30),
            "americano" => TimeSpan.FromSeconds(45),
            "cappuccino" => TimeSpan.FromMinutes(2),
            "latte" => TimeSpan.FromSeconds(90),
            "macchiato" => TimeSpan.FromSeconds(75),
            _ => TimeSpan.FromMinutes(1)
        };
    }

    // Extension pour List<string> - formater une commande
    public static string FormatCommande(this List<string> items)
    {
        if (items.Count == 0)
            return "Commande vide";
        
        return $"Commande: {string.Join(", ", items)} ({items.Count} article{(items.Count > 1 ? "s" : "")})";
    }
}

class UtilisationExtensions
{
    static void Main()
    {
        // Test des extensions sur string
        string cafe1 = "cappuccino";
        string cafe2 = "  LATTE  ";
        string cafe3 = "";

        Console.WriteLine("=== EXTENSIONS DE CHAÎNES ===");
        Console.WriteLine(cafe1.FormatNomCafe());
        Console.WriteLine(cafe2.FormatNomCafe());
        Console.WriteLine(cafe3.FormatNomCafe());
        Console.WriteLine();

        // Test est café chaud
        Console.WriteLine("=== VÉRIFICATION CAFÉ CHAUD ===");
        string[] cafes = {"Espresso", "Iced Coffee", "Cappuccino", "Smoothie"};
        foreach (string cafe in cafes)
        {
            bool chaud = cafe.EstCafeChaud();
            Console.WriteLine($"{cafe}: {(chaud ? "🔥 Chaud" : "🧊 Froid")}");
        }
        Console.WriteLine();

        // Test calories et temps
        Console.WriteLine("=== INFORMATIONS NUTRITIONNELLES ===");
        string[] typesCafes = {"Espresso", "Cappuccino", "Latte", "Mocha"};
        foreach (string type in typesCafes)
        {
            int calories = type.CalculerCalories();
            TimeSpan temps = type.ObtenirTempsPreparation();
            Console.WriteLine($"{type}: {calories} cal, {temps.TotalSeconds}s de préparation");
        }
        Console.WriteLine();

        // Test extension sur List
        Console.WriteLine("=== FORMATAGE DE COMMANDES ===");
        var commande1 = new List<string> {"Espresso", "Cappuccino"};
        var commande2 = new List<string> {"Latte", "Americano", "Macchiato"};
        var commande3 = new List<string>();

        Console.WriteLine(commande1.FormatCommande());
        Console.WriteLine(commande2.FormatCommande());
        Console.WriteLine(commande3.FormatCommande());
    }
}
```

---

## 8. Exemple complet : Système de café avec méthodes

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

public class SystemeCafeComplet
{
    // Propriétés de la classe
    private Dictionary<string, double> cartePrix;
    private Dictionary<string, int> stock;
    private List<Commande> commandesDuJour;

    // Constructeur
    public SystemeCafeComplet()
    {
        InitialiserDonnees();
        commandesDuJour = new List<Commande>();
    }

    // Méthode d'initialisation privée
    private void InitialiserDonnees()
    {
        cartePrix = new Dictionary<string, double>
        {
            {"Espresso", 2.50},
            {"Cappuccino", 4.00},
            {"Latte", 4.50},
            {"Americano", 3.00},
            {"Macchiato", 3.80}
        };

        stock = new Dictionary<string, int>
        {
            {"Espresso", 20},
            {"Cappuccino", 15},
            {"Latte", 12},
            {"Americano", 18},
            {"Macchiato", 10}
        };
    }

    // Méthode publique pour afficher le menu
    public void AfficherMenu()
    {
        Console.WriteLine("☕ === MENU DU CAFÉ ===");
        Console.WriteLine("Produit      | Prix   | Stock");
        Console.WriteLine("-------------|--------|-------");
        
        foreach (var item in cartePrix)
        {
            string produit = item.Key;
            double prix = item.Value;
            int stockProduit = stock.ContainsKey(produit) ? stock[produit] : 0;
            string disponibilite = stockProduit > 0 ? "✅" : "❌";
            
            Console.WriteLine($"{produit,-12} | {prix,6:C2} | {stockProduit,3} {disponibilite}");
        }
        Console.WriteLine();
    }

    // Méthode de validation privée
    private bool ValiderCommande(string produit, int quantite, out string erreur)
    {
        erreur = "";

        if (!cartePrix.ContainsKey(produit))
        {
            erreur = $"Produit '{produit}' non disponible";
            return false;
        }

        if (quantite <= 0)
        {
            erreur = "La quantité doit être positive";
            return false;
        }

        if (!stock.ContainsKey(produit) || stock[produit] < quantite)
        {
            erreur = $"Stock insuffisant pour {produit}";
            return false;
        }

        return true;
    }

    // Méthode de calcul privée
    private double CalculerTotal(string produit, int quantite, bool clientVIP = false)
    {
        double prixUnitaire = cartePrix[produit];
        double total = prixUnitaire * quantite;
        
        // Remise VIP
        if (clientVIP)
        {
            total *= 0.9; // 10% de remise
        }
        
        return total;
    }

    // Méthode publique principale
    public bool PasserCommande(string client, string produit, int quantite, bool clientVIP = false)
    {
        Console.WriteLine($"🔄 Traitement commande pour {client}...");
        
        // Validation
        if (!ValiderCommande(produit, quantite, out string erreur))
        {
            Console.WriteLine($"❌ Erreur: {erreur}");
            return false;
        }

        // Calcul
        double total = CalculerTotal(produit, quantite, clientVIP);
        
        // Création de la commande
        var commande = new Commande
        {
            Client = client,
            Produit = produit,
            Quantite = quantite,
            Total = total,
            Heure = DateTime.Now,
            EstVIP = clientVIP
        };

        // Mise à jour du stock
        stock[produit] -= quantite;
        
        // Ajout à l'historique
        commandesDuJour.Add(commande);

        // Confirmation
        AfficherConfirmationCommande(commande);
        return true;
    }

    // Méthode d'affichage privée
    private void AfficherConfirmationCommande(Commande commande)
    {
        Console.WriteLine("✅ Commande confirmée !");
        Console.WriteLine($"   Client: {commande.Client} {(commande.EstVIP ? "⭐" : "")}");
        Console.WriteLine($"   Produit: {commande.Quantite}x {commande.Produit}");
        Console.WriteLine($"   Total: {commande.Total:C2}");
        Console.WriteLine($"   Heure: {commande.Heure:HH:mm}");
        Console.WriteLine();
    }

    // Méthode d'analyse avec LINQ
    public void AfficherStatistiques()
    {
        if (!commandesDuJour.Any())
        {
            Console.WriteLine("📊 Aucune commande aujourd'hui");
            return;
        }

        Console.WriteLine("📊 === STATISTIQUES DU JOUR ===");
        
        // Chiffre d'affaires
        double totalCA = commandesDuJour.Sum(c => c.Total);
        Console.WriteLine($"💰 Chiffre d'affaires: {totalCA:C2}");
        
        // Nombre de commandes
        int nbCommandes = commandesDuJour.Count;
        Console.WriteLine($"📋 Nombre de commandes: {nbCommandes}");
        
        // Panier moyen
        double panierMoyen = totalCA / nbCommandes;
        Console.WriteLine($"🛒 Panier moyen: {panierMoyen:C2}");
        
        // Produit le plus vendu
        var produitPopulaire = commandesDuJour
            .GroupBy(c => c.Produit)
            .OrderByDescending(g => g.Sum(c => c.Quantite))
            .First();
        
        Console.WriteLine($"🏆 Produit populaire: {produitPopulaire.Key} ({produitPopulaire.Sum(c => c.Quantite)} unités)");
        
        // Clients VIP
        int clientsVIP = commandesDuJour.Count(c => c.EstVIP);
        Console.WriteLine($"⭐ Commandes VIP: {clientsVIP}");
        
        Console.WriteLine();
    }

    // Méthode utilitaire publique
    public void ReinitialiserStock()
    {
        Console.WriteLine("📦 Réapprovisionnement du stock...");
        
        foreach (var produit in cartePrix.Keys.ToList())
        {
            int ancienStock = stock[produit];
            stock[produit] = 20; // Stock standard
            Console.WriteLine($"   {produit}: {ancienStock} → {stock[produit]}");
        }
        
        Console.WriteLine("✅ Stock réapprovisionné !");
        Console.WriteLine();
    }

    // Classe interne pour les commandes
    public class Commande
    {
        public string Client { get; set; }
        public string Produit { get; set; }
        public int Quantite { get; set; }
        public double Total { get; set; }
        public DateTime Heure { get; set; }
        public bool EstVIP { get; set; }
    }

    // Méthode principale pour tester
    static void Main()
    {
        var cafe = new SystemeCafeComplet();
        
        Console.WriteLine("☕ === SYSTÈME DE CAFÉ COMPLET ===\n");
        
        // Afficher le menu initial
        cafe.AfficherMenu();
        
        // Simuler des commandes
        cafe.PasserCommande("Marie", "Cappuccino", 2, true);  // VIP
        cafe.PasserCommande("Paul", "Espresso", 1);
        cafe.PasserCommande("Julie", "Latte", 3);
        cafe.PasserCommande("Tom", "Americano", 1);
        cafe.PasserCommande("Emma", "Macchiato", 2, true);    // VIP
        
        // Commande qui échoue
        cafe.PasserCommande("Alex", "Cappuccino", 20);        // Stock insuffisant
        
        // Afficher les statistiques
        cafe.AfficherStatistiques();
        
        // Afficher le stock actuel
        cafe.AfficherMenu();
        
        // Réapprovisionner
        cafe.ReinitialiserStock();
        cafe.AfficherMenu();
    }
}
```

---

## 9. Bonnes pratiques pour les méthodes

### ✅ Nommage clair et expressif
```csharp
// ✅ Bon - nom explicite
public static double CalculerPrixAvecRemise(double prixBase, double tauxRemise)

// ❌ Éviter - nom peu clair
public static double Calc(double p, double r)
```

### ✅ Une responsabilité par méthode
```csharp
// ✅ Bon - une seule responsabilité
public static double CalculerPrix(string produit, int quantite)
public static void AfficherCommande(Commande commande)
public static bool ValiderStock(string produit, int quantite)

// ❌ Éviter - trop de responsabilités
public static void TraiterTout(string produit, int quantite, string client)
{
    // Calcul + Affichage + Validation + Stockage = trop !
}
```

### ✅ Paramètres raisonnables
```csharp
// ✅ Bon - paramètres clairs
public static void CreerCommande(string client, string produit, int quantite)

// ❌ Éviter - trop de paramètres
public static void CreerCommande(string client, string produit, int quantite, 
    string taille, bool sucre, string lait, double temp, bool vip, string notes)
```

### ✅ Gestion d'erreurs appropriée
```csharp
// ✅ Bon - validation et gestion d'erreurs
public static double CalculerPrix(string produit, int quantite)
{
    if (string.IsNullOrWhiteSpace(produit))
        throw new ArgumentException("Produit requis");
    
    if (quantite <= 0)
        throw new ArgumentOutOfRangeException(nameof(quantite));
    
    // Calcul...
}
```

---

## Exercices pratiques

### Exercice 1 : Calculatrice de café
Créez une classe avec des méthodes pour calculer différents aspects d'une commande (prix, temps, calories).

### Exercice 2 : Générateur de recettes
Créez des méthodes qui génèrent automatiquement des recettes de café selon les ingrédients disponibles.

### Exercice 3 : Système de fidélité
Créez des méthodes surchargées pour calculer les points de fidélité selon différents critères.

---

## Conclusion

Les méthodes sont les **recettes réutilisables** de la programmation ! Elles nous permettent de :

- ✅ **Organiser le code** en blocs logiques
- ✅ **Réutiliser des fonctionnalités** sans duplication
- ✅ **Paramétrer les comportements** selon les besoins
- ✅ **Faciliter la maintenance** et les tests
- ✅ **Améliorer la lisibilité** du code

Comme un barista expert qui maîtrise toutes ses recettes, un développeur qui sait créer de bonnes méthodes peut construire des applications élégantes et efficaces !

**Félicitations !** Vous avez maintenant découvert les concepts fondamentaux de la programmation C# à travers l'univers du café ! ☕

---

*Continuez à pratiquer ces concepts et à créer vos propres méthodes. La programmation, comme l'art du café, se perfectionne avec la pratique et la passion ! 🚀*