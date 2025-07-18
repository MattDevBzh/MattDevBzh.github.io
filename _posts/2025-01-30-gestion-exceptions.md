---
layout: post
title: "Gestion des exceptions en C# : Gérer les pannes de votre café avec élégance"
date: 2025-01-30
---

Dans un café, tout ne se passe pas toujours comme prévu ! **Machine en panne, stock épuisé, commande incorrecte...** En programmation C#, les **exceptions** nous permettent de gérer ces situations inattendues avec élégance et professionnalisme. ☕

Découvrons ensemble comment transformer les problèmes en solutions grâce à la gestion d'exceptions !

## Sommaire
* TOC
{:toc}

---

## Qu'est-ce qu'une exception ?

Une **exception** est un événement inattendu qui interrompt le cours normal d'un programme. C'est comme :

- ⚡ **Panne de courant** pendant la préparation d'un café
- 📦 **Stock vide** alors qu'un client commande
- 🔧 **Machine en maintenance** non signalée
- 💳 **Carte bancaire refusée** au moment du paiement

Sans gestion appropriée, ces problèmes peuvent faire "planter" votre programme !

---

## 1. La structure `try...catch` : Attraper les erreurs

La structure `try...catch` permet d'essayer une opération et de gérer les erreurs qui peuvent survenir.

### Syntaxe de base
```csharp
try
{
    // Code qui peut générer une exception
}
catch (TypeException ex)
{
    // Gestion de l'erreur
}
```

### Exemple : Division par zéro dans le calcul de prix
```csharp
double calculerPrixUnitaire(double prixTotal, int quantite)
{
    try
    {
        double prixUnitaire = prixTotal / quantite;
        Console.WriteLine($"Prix unitaire : {prixUnitaire:C2}");
        return prixUnitaire;
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine("❌ Erreur : Impossible de diviser par zéro !");
        Console.WriteLine("Vérifiez que la quantité est supérieure à 0.");
        return 0;
    }
}

// Test
calculerPrixUnitaire(15.50, 0); // Va déclencher l'exception
calculerPrixUnitaire(15.50, 3); // Fonctionne normalement
```

### Exemple : Accès à un index inexistant
```csharp
string[] menuCafes = {"Espresso", "Cappuccino", "Latte"};

void afficherCafe(int index)
{
    try
    {
        Console.WriteLine($"Café sélectionné : {menuCafes[index]}");
    }
    catch (IndexOutOfRangeException ex)
    {
        Console.WriteLine($"❌ Erreur : Index {index} n'existe pas !");
        Console.WriteLine($"Indices valides : 0 à {menuCafes.Length - 1}");
        
        // Afficher le menu complet
        Console.WriteLine("Menu disponible :");
        for (int i = 0; i < menuCafes.Length; i++)
        {
            Console.WriteLine($"  {i}. {menuCafes[i]}");
        }
    }
}

// Test
afficherCafe(1);  // Fonctionne
afficherCafe(5);  // Déclenche l'exception
```

---

## 2. Plusieurs types d'exceptions : `catch` multiples

Un même bloc `try` peut avoir plusieurs `catch` pour différents types d'erreurs.

### Exemple : Gestion complète d'une commande
```csharp
class GestionCommande
{
    private Dictionary<string, double> prix = new Dictionary<string, double>
    {
        {"Espresso", 2.50},
        {"Cappuccino", 4.00},
        {"Latte", 4.50}
    };
    
    private Dictionary<string, int> stock = new Dictionary<string, int>
    {
        {"Espresso", 10},
        {"Cappuccino", 5},
        {"Latte", 0}
    };

    public void PasserCommande(string produit, int quantite, string carteCredit)
    {
        try
        {
            // Vérifier que le produit existe
            if (!prix.ContainsKey(produit))
            {
                throw new ArgumentException($"Produit '{produit}' introuvable");
            }
            
            // Vérifier le stock
            if (stock[produit] < quantite)
            {
                throw new InvalidOperationException($"Stock insuffisant pour {produit}");
            }
            
            // Simuler une erreur de carte
            if (string.IsNullOrEmpty(carteCredit))
            {
                throw new ArgumentNullException(nameof(carteCredit), "Carte de crédit requise");
            }
            
            // Calculer le total
            double total = prix[produit] * quantite;
            
            // Simuler le paiement
            if (carteCredit == "CARTE_REFUSEE")
            {
                throw new InvalidOperationException("Paiement refusé par la banque");
            }
            
            // Commande réussie
            stock[produit] -= quantite;
            Console.WriteLine($"✅ Commande réussie !");
            Console.WriteLine($"   Produit : {quantite}x {produit}");
            Console.WriteLine($"   Total : {total:C2}");
            Console.WriteLine($"   Stock restant : {stock[produit]}");
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine($"❌ Erreur de produit : {ex.Message}");
            Console.WriteLine("Produits disponibles :");
            foreach (var p in prix.Keys)
            {
                Console.WriteLine($"  - {p} ({prix[p]:C2})");
            }
        }
        catch (ArgumentNullException ex)
        {
            Console.WriteLine($"❌ Erreur de saisie : {ex.Message}");
            Console.WriteLine("Veuillez fournir une carte de crédit valide.");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine($"❌ Erreur d'opération : {ex.Message}");
            
            if (ex.Message.Contains("Stock"))
            {
                Console.WriteLine($"Stock disponible pour {produit} : {stock[produit]} unités");
            }
            else if (ex.Message.Contains("Paiement"))
            {
                Console.WriteLine("Veuillez essayer avec une autre carte ou payer en espèces.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Erreur inattendue : {ex.Message}");
            Console.WriteLine("Veuillez contacter le support technique.");
        }
    }
}

// Tests
var gestion = new GestionCommande();

gestion.PasserCommande("Cappuccino", 2, "1234-5678-9012-3456");  // ✅ Succès
gestion.PasserCommande("Mocha", 1, "1234-5678-9012-3456");       // ❌ Produit inexistant
gestion.PasserCommande("Latte", 1, "1234-5678-9012-3456");       // ❌ Stock insuffisant
gestion.PasserCommande("Espresso", 1, null);                     // ❌ Carte manquante
gestion.PasserCommande("Espresso", 1, "CARTE_REFUSEE");          // ❌ Paiement refusé
```

---

## 3. Le bloc `finally` : Nettoyage garanti

Le bloc `finally` s'exécute toujours, qu'il y ait eu exception ou non. Parfait pour le nettoyage !

### Exemple : Gestion d'une machine à café
```csharp
class MachineACafe
{
    private bool machineAllumee = false;
    private bool enPreparation = false;

    public void PreparerCafe(string typeCafe)
    {
        try
        {
            Console.WriteLine("🔄 Démarrage de la machine...");
            machineAllumee = true;
            
            Console.WriteLine($"☕ Préparation du {typeCafe}...");
            enPreparation = true;
            
            // Simuler des erreurs possibles
            if (typeCafe == "ERREUR_GRAIN")
            {
                throw new InvalidOperationException("Plus de grains de café !");
            }
            
            if (typeCafe == "ERREUR_EAU")
            {
                throw new InvalidOperationException("Réservoir d'eau vide !");
            }
            
            // Simulation du temps de préparation
            System.Threading.Thread.Sleep(2000);
            
            Console.WriteLine($"✅ {typeCafe} prêt !");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine($"❌ Erreur de préparation : {ex.Message}");
            Console.WriteLine("Veuillez vérifier la machine avant de recommencer.");
        }
        finally
        {
            // Nettoyage toujours exécuté
            if (enPreparation)
            {
                Console.WriteLine("🧹 Nettoyage de la machine en cours...");
                enPreparation = false;
            }
            
            if (machineAllumee)
            {
                Console.WriteLine("🔌 Arrêt de la machine...");
                machineAllumee = false;
            }
            
            Console.WriteLine("✅ Machine prête pour la prochaine commande.\n");
        }
    }
}

// Tests
var machine = new MachineACafe();

machine.PreparerCafe("Espresso");       // ✅ Succès
machine.PreparerCafe("ERREUR_GRAIN");   // ❌ Erreur mais nettoyage
machine.PreparerCafe("ERREUR_EAU");     // ❌ Erreur mais nettoyage
```

---

## 4. Créer des exceptions personnalisées

Pour des erreurs spécifiques à votre application, créez vos propres exceptions.

### Exemple : Exceptions métier pour un café
```csharp
// Exception personnalisée pour stock insuffisant
public class StockInsuffisantException : Exception
{
    public string Produit { get; }
    public int StockDisponible { get; }
    public int QuantiteDemandee { get; }

    public StockInsuffisantException(string produit, int stockDisponible, int quantiteDemandee)
        : base($"Stock insuffisant pour {produit}. Disponible: {stockDisponible}, Demandé: {quantiteDemandee}")
    {
        Produit = produit;
        StockDisponible = stockDisponible;
        QuantiteDemandee = quantiteDemandee;
    }
}

// Exception pour machine en panne
public class MachineEnPanneException : Exception
{
    public string TypeMachine { get; }
    public string CodeErreur { get; }

    public MachineEnPanneException(string typeMachine, string codeErreur, string message)
        : base(message)
    {
        TypeMachine = typeMachine;
        CodeErreur = codeErreur;
    }
}

// Exception pour client non autorisé
public class ClientNonAutoriseException : Exception
{
    public string NomClient { get; }
    public string Raison { get; }

    public ClientNonAutoriseException(string nomClient, string raison)
        : base($"Client {nomClient} non autorisé: {raison}")
    {
        NomClient = nomClient;
        Raison = raison;
    }
}

// Utilisation
class CafeAvecExceptionsPersonnalisees
{
    private Dictionary<string, int> stock = new Dictionary<string, int>
    {
        {"Espresso", 5},
        {"Cappuccino", 2}
    };
    
    private HashSet<string> clientsBannis = new HashSet<string> {"ClientProblematique"};

    public void TraiterCommande(string client, string produit, int quantite)
    {
        try
        {
            // Vérifier le client
            if (clientsBannis.Contains(client))
            {
                throw new ClientNonAutoriseException(client, "Client banni pour impayés");
            }
            
            // Vérifier le stock
            if (!stock.ContainsKey(produit) || stock[produit] < quantite)
            {
                int stockDisponible = stock.ContainsKey(produit) ? stock[produit] : 0;
                throw new StockInsuffisantException(produit, stockDisponible, quantite);
            }
            
            // Simuler une panne de machine
            Random random = new Random();
            if (random.Next(1, 10) == 1) // 10% de chance de panne
            {
                throw new MachineEnPanneException("Broyeur", "ERR_001", "Grains coincés dans le broyeur");
            }
            
            // Traitement réussi
            stock[produit] -= quantite;
            Console.WriteLine($"✅ Commande traitée pour {client}");
            Console.WriteLine($"   {quantite}x {produit}");
            Console.WriteLine($"   Stock restant : {stock[produit]}");
        }
        catch (ClientNonAutoriseException ex)
        {
            Console.WriteLine($"🚫 Accès refusé : {ex.Message}");
            Console.WriteLine($"   Client : {ex.NomClient}");
            Console.WriteLine($"   Raison : {ex.Raison}");
        }
        catch (StockInsuffisantException ex)
        {
            Console.WriteLine($"📦 {ex.Message}");
            Console.WriteLine($"   Suggestion : Commander {ex.QuantiteDemandee - ex.StockDisponible} unités supplémentaires");
        }
        catch (MachineEnPanneException ex)
        {
            Console.WriteLine($"🔧 Panne machine : {ex.Message}");
            Console.WriteLine($"   Machine : {ex.TypeMachine}");
            Console.WriteLine($"   Code erreur : {ex.CodeErreur}");
            Console.WriteLine($"   Action : Contacter le technicien");
        }
    }
}

// Test
var cafe = new CafeAvecExceptionsPersonnalisees();

cafe.TraiterCommande("Marie", "Espresso", 2);           // ✅ Possible
cafe.TraiterCommande("Paul", "Cappuccino", 5);          // ❌ Stock insuffisant
cafe.TraiterCommande("ClientProblematique", "Latte", 1); // ❌ Client banni
```

---

## 5. Validation et exceptions préventives

Il vaut mieux valider les données avant qu'elles causent des erreurs.

### Exemple : Validation robuste de commande
```csharp
public class ValidateurCommande
{
    public static void ValiderCommande(string client, string produit, int quantite, double montant)
    {
        // Validation du nom client
        if (string.IsNullOrWhiteSpace(client))
        {
            throw new ArgumentException("Le nom du client ne peut pas être vide", nameof(client));
        }
        
        if (client.Length < 2)
        {
            throw new ArgumentException("Le nom du client doit contenir au moins 2 caractères", nameof(client));
        }
        
        // Validation du produit
        if (string.IsNullOrWhiteSpace(produit))
        {
            throw new ArgumentException("Le nom du produit ne peut pas être vide", nameof(produit));
        }
        
        // Validation de la quantité
        if (quantite <= 0)
        {
            throw new ArgumentOutOfRangeException(nameof(quantite), "La quantité doit être supérieure à 0");
        }
        
        if (quantite > 10)
        {
            throw new ArgumentOutOfRangeException(nameof(quantite), "Maximum 10 unités par commande");
        }
        
        // Validation du montant
        if (montant < 0)
        {
            throw new ArgumentOutOfRangeException(nameof(montant), "Le montant ne peut pas être négatif");
        }
        
        if (montant > 1000)
        {
            throw new ArgumentOutOfRangeException(nameof(montant), "Montant maximum : 1000€");
        }
    }
}

// Service de commande sécurisé
public class ServiceCommande
{
    public void CreerCommande(string client, string produit, int quantite, double montant)
    {
        try
        {
            // Validation préventive
            ValidateurCommande.ValiderCommande(client, produit, quantite, montant);
            
            Console.WriteLine($"✅ Commande validée :");
            Console.WriteLine($"   Client : {client}");
            Console.WriteLine($"   Produit : {quantite}x {produit}");
            Console.WriteLine($"   Montant : {montant:C2}");
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine($"❌ Erreur de validation : {ex.Message}");
            Console.WriteLine($"   Paramètre : {ex.ParamName}");
        }
        catch (ArgumentOutOfRangeException ex)
        {
            Console.WriteLine($"❌ Valeur hors limites : {ex.Message}");
            Console.WriteLine($"   Paramètre : {ex.ParamName}");
        }
    }
}

// Tests de validation
var service = new ServiceCommande();

service.CreerCommande("Marie", "Cappuccino", 2, 8.00);    // ✅ Valide
service.CreerCommande("", "Espresso", 1, 2.50);           // ❌ Nom vide
service.CreerCommande("A", "Latte", 1, 4.50);             // ❌ Nom trop court
service.CreerCommande("Paul", "", 1, 3.00);               // ❌ Produit vide
service.CreerCommande("Julie", "Americano", 0, 3.00);     // ❌ Quantité invalide
service.CreerCommande("Tom", "Mocha", 15, 75.00);         // ❌ Trop de quantité
service.CreerCommande("Emma", "Latte", 2, -5.00);         // ❌ Montant négatif
```

---

## 6. Logging et traçabilité des erreurs

Il est important de garder une trace des erreurs pour le débogage.

### Exemple : Système de logs d'erreurs
```csharp
using System.IO;

public class LoggerErreurs
{
    private static string cheminLog = "erreurs_cafe.log";

    public static void EcrireErreur(Exception ex, string contexte)
    {
        string ligneLog = $"[{DateTime.Now:yyyy-MM-dd HH:mm:ss}] {contexte} - {ex.GetType().Name}: {ex.Message}";
        
        try
        {
            File.AppendAllText(cheminLog, ligneLog + Environment.NewLine);
        }
        catch
        {
            // Si on ne peut pas écrire dans le fichier, au moins afficher
            Console.WriteLine($"ERREUR LOG: {ligneLog}");
        }
    }

    public static void AfficherLogs()
    {
        try
        {
            if (File.Exists(cheminLog))
            {
                string contenu = File.ReadAllText(cheminLog);
                Console.WriteLine("📋 === HISTORIQUE DES ERREURS ===");
                Console.WriteLine(contenu);
            }
            else
            {
                Console.WriteLine("✅ Aucune erreur enregistrée");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Impossible de lire le fichier de log : {ex.Message}");
        }
    }
}

public class CafeAvecLogs
{
    private Dictionary<string, int> stock = new Dictionary<string, int>
    {
        {"Espresso", 3},
        {"Cappuccino", 1}
    };

    public void PreparerCafe(string produit, string client)
    {
        try
        {
            if (!stock.ContainsKey(produit))
            {
                throw new ArgumentException($"Produit {produit} non disponible");
            }
            
            if (stock[produit] <= 0)
            {
                throw new InvalidOperationException($"Stock épuisé pour {produit}");
            }
            
            stock[produit]--;
            Console.WriteLine($"✅ {produit} préparé pour {client}");
        }
        catch (Exception ex)
        {
            // Log de l'erreur
            string contexte = $"Préparation café - Client: {client}, Produit: {produit}";
            LoggerErreurs.EcrireErreur(ex, contexte);
            
            // Affichage utilisateur
            Console.WriteLine($"❌ Erreur : {ex.Message}");
        }
    }
}

// Test avec logging
var cafeLog = new CafeAvecLogs();

cafeLog.PreparerCafe("Espresso", "Marie");      // ✅ Succès
cafeLog.PreparerCafe("Latte", "Paul");          // ❌ Produit inexistant (loggé)
cafeLog.PreparerCafe("Cappuccino", "Julie");    // ✅ Succès
cafeLog.PreparerCafe("Cappuccino", "Tom");      // ❌ Stock épuisé (loggé)

// Afficher l'historique
LoggerErreurs.AfficherLogs();
```

---

## 7. Exemple complet : Système robuste de café

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Exceptions personnalisées
public class CafeException : Exception
{
    public CafeException(string message) : base(message) { }
    public CafeException(string message, Exception innerException) : base(message, innerException) { }
}

public class StockEpuiseException : CafeException
{
    public string Produit { get; }
    public StockEpuiseException(string produit) : base($"Stock épuisé pour {produit}")
    {
        Produit = produit;
    }
}

// Système robuste
public class SystemeCafeRobuste
{
    private Dictionary<string, decimal> prix;
    private Dictionary<string, int> stock;
    private List<string> historiqueErreurs;

    public SystemeCafeRobuste()
    {
        InitialiserDonnees();
        historiqueErreurs = new List<string>();
    }

    private void InitialiserDonnees()
    {
        prix = new Dictionary<string, decimal>
        {
            {"Espresso", 2.50m},
            {"Cappuccino", 4.00m},
            {"Latte", 4.50m},
            {"Americano", 3.00m}
        };

        stock = new Dictionary<string, int>
        {
            {"Espresso", 10},
            {"Cappuccino", 5},
            {"Latte", 3},
            {"Americano", 8}
        };
    }

    public void ProcesserCommande(string client, string produit, int quantite)
    {
        string idCommande = Guid.NewGuid().ToString()[..8];
        
        try
        {
            Console.WriteLine($"🔄 Commande {idCommande} - Traitement en cours...");
            
            // Validations
            ValiderParametres(client, produit, quantite);
            ValiderDisponibilite(produit, quantite);
            
            // Traitement
            decimal total = CalculerTotal(produit, quantite);
            ProcesserPaiement(total);
            MettreAJourStock(produit, quantite);
            
            // Succès
            Console.WriteLine($"✅ Commande {idCommande} terminée avec succès !");
            Console.WriteLine($"   Client : {client}");
            Console.WriteLine($"   Produit : {quantite}x {produit}");
            Console.WriteLine($"   Total : {total:C2}");
        }
        catch (ArgumentException ex)
        {
            GererErreur($"Commande {idCommande}", ex, "Paramètres invalides");
        }
        catch (StockEpuiseException ex)
        {
            GererErreur($"Commande {idCommande}", ex, "Problème de stock");
            ProposerAlternatives(ex.Produit);
        }
        catch (InvalidOperationException ex)
        {
            GererErreur($"Commande {idCommande}", ex, "Erreur de traitement");
        }
        catch (Exception ex)
        {
            GererErreur($"Commande {idCommande}", ex, "Erreur inattendue");
        }
        finally
        {
            Console.WriteLine($"📝 Commande {idCommande} archivée.\n");
        }
    }

    private void ValiderParametres(string client, string produit, int quantite)
    {
        if (string.IsNullOrWhiteSpace(client))
            throw new ArgumentException("Nom client requis");
        
        if (string.IsNullOrWhiteSpace(produit))
            throw new ArgumentException("Nom produit requis");
        
        if (quantite <= 0 || quantite > 10)
            throw new ArgumentException("Quantité doit être entre 1 et 10");
    }

    private void ValiderDisponibilite(string produit, int quantite)
    {
        if (!prix.ContainsKey(produit))
            throw new ArgumentException($"Produit '{produit}' non disponible au menu");
        
        if (!stock.ContainsKey(produit) || stock[produit] < quantite)
            throw new StockEpuiseException(produit);
    }

    private decimal CalculerTotal(string produit, int quantite)
    {
        return prix[produit] * quantite;
    }

    private void ProcesserPaiement(decimal montant)
    {
        // Simulation d'un paiement qui peut échouer
        Random random = new Random();
        if (random.Next(1, 20) == 1) // 5% de chance d'échec
        {
            throw new InvalidOperationException("Erreur de paiement - Carte refusée");
        }
    }

    private void MettreAJourStock(string produit, int quantite)
    {
        stock[produit] -= quantite;
    }

    private void GererErreur(string contexte, Exception ex, string type)
    {
        string messageErreur = $"[{DateTime.Now:HH:mm:ss}] {contexte} - {type}: {ex.Message}";
        historiqueErreurs.Add(messageErreur);
        
        Console.WriteLine($"❌ {type}: {ex.Message}");
        
        // Log détaillé pour debug
        Console.WriteLine($"   Détail technique: {ex.GetType().Name}");
    }

    private void ProposerAlternatives(string produitDemande)
    {
        Console.WriteLine("💡 Alternatives disponibles :");
        foreach (var item in stock.Where(s => s.Value > 0))
        {
            Console.WriteLine($"   - {item.Key} ({item.Value} disponibles) - {prix[item.Key]:C2}");
        }
    }

    public void AfficherStatut()
    {
        Console.WriteLine("📊 === STATUT DU SYSTÈME ===");
        Console.WriteLine("Stock actuel :");
        foreach (var item in stock)
        {
            string statut = item.Value > 5 ? "✅" : item.Value > 0 ? "⚠️" : "❌";
            Console.WriteLine($"  {statut} {item.Key} : {item.Value} unités");
        }
        
        Console.WriteLine($"\nErreurs enregistrées : {historiqueErreurs.Count}");
        if (historiqueErreurs.Count > 0)
        {
            Console.WriteLine("Dernières erreurs :");
            foreach (string erreur in historiqueErreurs.TakeLast(3))
            {
                Console.WriteLine($"  {erreur}");
            }
        }
    }

    static void Main()
    {
        var systeme = new SystemeCafeRobuste();
        
        Console.WriteLine("☕ === SYSTÈME DE CAFÉ ROBUSTE ===\n");
        
        // Tests de commandes
        systeme.ProcesserCommande("Marie", "Cappuccino", 2);      // ✅ Normal
        systeme.ProcesserCommande("", "Espresso", 1);             // ❌ Client vide
        systeme.ProcesserCommande("Paul", "Thé", 1);              // ❌ Produit inexistant
        systeme.ProcesserCommande("Julie", "Latte", 5);           // ❌ Stock insuffisant
        systeme.ProcesserCommande("Tom", "Americano", 15);        // ❌ Quantité trop élevée
        systeme.ProcesserCommande("Emma", "Espresso", 2);         // ✅ Normal
        
        // Statut final
        systeme.AfficherStatut();
    }
}
```

---

## 8. Bonnes pratiques de gestion d'exceptions

### ✅ Exceptions spécifiques
```csharp
// ✅ Bon - Exception spécifique
catch (FileNotFoundException ex)
{
    Console.WriteLine("Fichier non trouvé");
}

// ❌ Éviter - Trop général
catch (Exception ex)
{
    // Capture tout, difficile à déboguer
}
```

### ✅ Messages d'erreur utiles
```csharp
// ✅ Message informatif
throw new ArgumentException($"Stock insuffisant pour {produit}. Disponible: {stockActuel}, Demandé: {quantite}");

// ❌ Message peu utile
throw new Exception("Erreur");
```

### ✅ Logging approprié
```csharp
// ✅ Log avec contexte
catch (Exception ex)
{
    logger.LogError($"Erreur lors de la commande {commandeId} pour {client}: {ex.Message}");
    // Puis gestion utilisateur
}
```

### ✅ Nettoyage avec `finally` ou `using`
```csharp
// ✅ Avec using (automatique)
using (var connexion = new DatabaseConnection())
{
    // Travail avec la connexion
} // Fermeture automatique

// ✅ Avec finally (manuel)
FileStream fichier = null;
try
{
    fichier = new FileStream("data.txt", FileMode.Open);
    // Travail avec le fichier
}
finally
{
    fichier?.Close();
}
```

---

## Exercices pratiques

### Exercice 1 : Calculatrice robuste
Créez une calculatrice qui gère toutes les erreurs possibles (division par zéro, formats invalides, etc.).

### Exercice 2 : Lecteur de fichier sécurisé
Créez un système qui lit des commandes depuis un fichier avec gestion complète des erreurs.

### Exercice 3 : API de café resiliente
Créez une classe qui simule un service web avec retry automatique en cas d'erreur.

---

## Conclusion

La gestion d'exceptions est l'art de **transformer les problèmes en solutions** ! Elle nous permet de :

- ✅ **Anticiper les erreurs** avec des validations
- ✅ **Gérer les exceptions** avec `try...catch...finally`
- ✅ **Créer des exceptions métier** spécifiques
- ✅ **Logger et tracer** pour le débogage
- ✅ **Offrir une expérience utilisateur** fluide même en cas d'erreur

Comme un barista expérimenté qui sait gérer toutes les situations imprévues, un développeur maîtrisant les exceptions crée des applications fiables et professionnelles !

**Prochaine étape :** Nous découvrirons les méthodes et fonctions pour organiser et réutiliser notre code ! ☕

---

*Pratiquez avec ces exemples et créez vos propres gestionnaires d'erreurs. Un bon code, c'est comme un bon café : préparé avec soin et attention aux détails ! 🚀*