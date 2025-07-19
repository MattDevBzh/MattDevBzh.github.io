---
layout: post
title: "Méthodes et fonctions en C# : Les recettes secrètes de votre café"
date: 2025-01-31
---

![Illustration méthodes et fonctions](/assets/images/methodes-illustration.svg)

Dans un café, chaque barista a ses **recettes secrètes** : comment obtenir la mousse parfaite, préparer l'espresso idéal, ou calculer rapidement les prix. En programmation C#, les **méthodes et fonctions** sont ces recettes réutilisables qui rendent notre code organisé et efficace ! ☕

**Objectif de cet article :** Apprendre les bases des méthodes pour créer du code réutilisable et bien organisé.

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

**Pourquoi utiliser des méthodes ?**
- ✅ Éviter de répéter le même code
- ✅ Organiser le programme en parties logiques
- ✅ Faciliter les tests et corrections
- ✅ Rendre le code plus facile à comprendre

---

## 1. Méthodes simples : Sans paramètres ni retour

Ces méthodes sont parfaites pour débuter ! Elles exécutent simplement une série d'actions.

### Syntaxe de base
```csharp
public static void NomMethode()
{
    // Ce que fait la méthode
}
```

### Exemple : Actions simples du café
```csharp
class MonCafe
{
    // Méthode pour afficher le message d'accueil
    public static void AfficherAccueil()
    {
        Console.WriteLine("☕ Bienvenue dans notre café !");
        Console.WriteLine("Que puis-je vous servir aujourd'hui ?");
    }

    // Méthode pour nettoyer la machine
    public static void NettoyerMachine()
    {
        Console.WriteLine("🧹 Nettoyage de la machine à café...");
        Console.WriteLine("✅ Machine propre et prête !");
    }

    static void Main()
    {
        AfficherAccueil();  // Appel de la méthode
        NettoyerMachine();  // Appel de la méthode
    }
}
```

### ⚠️ Erreurs courantes à éviter

```csharp
// ❌ ERREUR : Nom peu clair
public static void Faire()
{
    Console.WriteLine("Je fais quelque chose...");
}

// ❌ ERREUR : Méthode trop longue et fait trop de choses
public static void FaireTout()
{
    Console.WriteLine("Accueil");
    Console.WriteLine("Nettoyage");
    Console.WriteLine("Commande");
    Console.WriteLine("Facturation");
    // ... 50 lignes de plus
}

// ✅ CORRECT : Nom explicite et responsabilité claire
public static void AfficherAccueil()
{
    Console.WriteLine("☕ Bienvenue dans notre café !");
}
```

**Règle d'or :** Une méthode = Une seule responsabilité

---

## 2. Méthodes avec paramètres : Personnaliser les recettes

Les paramètres permettent de "personnaliser" une méthode. C'est comme donner des ingrédients spécifiques à une recette.

### Exemple simple : Saluer un client
```csharp
class ServiceCafe
{
    // Méthode avec un paramètre
    public static void SaluerClient(string nomClient)
    {
        Console.WriteLine($"☕ Bonjour {nomClient} ! Que puis-je vous servir ?");
    }

    // Méthode avec plusieurs paramètres
    public static void PreparerCafe(string typeCafe, string nomClient)
    {
        Console.WriteLine($"🔥 Préparation d'un {typeCafe} pour {nomClient}");
        Console.WriteLine("✅ Votre café est prêt !");
    }

    static void Main()
    {
        SaluerClient("Marie");
        PreparerCafe("Cappuccino", "Marie");
        
        SaluerClient("Paul");
        PreparerCafe("Espresso", "Paul");
    }
}
```

### ⚠️ Erreurs courantes avec les paramètres

```csharp
// ❌ ERREUR : Trop de paramètres
public static void CommandeCompliquee(string client, string cafe, string taille, 
    bool sucre, bool lait, string temperature, bool emporter, string notes, 
    bool reduction, string moyenPaiement)
{
    // Impossible à utiliser !
}

// ❌ ERREUR : Paramètres dans le mauvais ordre
public static void PreparerCafe(string nomClient, string typeCafe)
{
    // Confusion possible : qui est quoi ?
}

// ✅ CORRECT : Paramètres clairs et limités
public static void PreparerCafe(string typeCafe, string nomClient)
{
    Console.WriteLine($"Préparation d'un {typeCafe} pour {nomClient}");
}
```

**Règle d'or :** Maximum 3-4 paramètres par méthode

---

## 3. Méthodes qui retournent une valeur

Parfois, on veut que notre méthode nous **donne un résultat**. C'est comme demander à un barista "Quel est le prix de ce café ?"

### Syntaxe avec retour
```csharp
public static [type] NomMethode()
{
    // Calculs...
    return resultat;  // On retourne la réponse
}
```

### Exemple : Calculer le prix d'une commande
```csharp
class CalculsCafe
{
    // Méthode qui retourne un nombre
    public static double CalculerPrix(string typeCafe)
    {
        if (typeCafe == "Espresso")
            return 2.50;
        else if (typeCafe == "Cappuccino")
            return 4.00;
        else
            return 3.00;  // Prix par défaut
    }

    // Méthode qui retourne vrai/faux
    public static bool EstEnStock(string produit)
    {
        // Simulation : on suppose que l'espresso est toujours en stock
        return produit == "Espresso";
    }

    static void Main()
    {
        // On récupère la valeur retournée
        double prix = CalculerPrix("Cappuccino");
        Console.WriteLine($"Prix du cappuccino : {prix:C2}");

        bool dispo = EstEnStock("Espresso");
        if (dispo)
        {
            Console.WriteLine("✅ Espresso disponible !");
        }
    }
}
```

### ⚠️ Erreurs courantes avec les retours

```csharp
// ❌ ERREUR : Oublier le return
public static double CalculerPrix(string cafe)
{
    if (cafe == "Espresso")
        2.50;  // ERREUR : manque return !
}

// ❌ ERREUR : Return non atteignable
public static double CalculerPrix(string cafe)
{
    Console.WriteLine("Calcul en cours...");
    return 2.50;
    Console.WriteLine("Terminé");  // ERREUR : jamais exécuté !
}

// ✅ CORRECT : Return clairement défini
public static double CalculerPrix(string cafe)
{
    Console.WriteLine("Calcul en cours...");
    return 2.50;
}
```

---

## 4. Méthodes avec paramètres ET retour

C'est la combinaison la plus utile ! On donne des informations ET on récupère un résultat.

### Exemple : Calculatrice de café
```csharp
class CalculatriceCafe
{
    // Calcul avec quantité
    public static double CalculerTotal(string typeCafe, int quantite)
    {
        double prixUnitaire = 0;
        
        switch (typeCafe)
        {
            case "Espresso":
                prixUnitaire = 2.50;
                break;
            case "Cappuccino":
                prixUnitaire = 4.00;
                break;
            case "Latte":
                prixUnitaire = 4.50;
                break;
            default:
                prixUnitaire = 3.00;
                break;
        }
        
        return prixUnitaire * quantite;
    }

    // Calcul avec remise
    public static double AppliquerRemise(double prix, int pourcentageRemise)
    {
        double remise = prix * pourcentageRemise / 100;
        return prix - remise;
    }

    static void Main()
    {
        // Commande simple
        double total = CalculerTotal("Cappuccino", 3);
        Console.WriteLine($"3 Cappuccinos : {total:C2}");

        // Avec remise de 10%
        double prixAvecRemise = AppliquerRemise(total, 10);
        Console.WriteLine($"Avec remise 10% : {prixAvecRemise:C2}");
    }
}
```

---

## 5. Bonnes pratiques à retenir

### ✅ Règles importantes

1. **Nom explicite** : On doit comprendre ce que fait la méthode juste en lisant son nom
2. **Une seule responsabilité** : Une méthode fait une seule chose, mais bien
3. **Paramètres limités** : Maximum 3-4 paramètres
4. **Courte et lisible** : Une méthode doit tenir sur un écran

### Exemples de bons noms
```csharp
// ✅ CORRECT : Verbes d'action clairs
public static void AfficherMenu()
public static double CalculerPrix()
public static bool VerifierStock()
public static void PreparerCafe()

// ❌ ÉVITER : Noms vagues
public static void Faire()
public static void Traiter()
public static void Action()
```

### ⚠️ Pièges à éviter dans la programmation

```csharp
// ❌ PIÈGE : Méthode qui fait trop de choses
public static void GererCafe()
{
    // Préparer café
    // Calculer prix
    // Afficher facture
    // Nettoyer machine
    // Gérer stock
    // ... STOP ! Trop de responsabilités !
}

// ❌ PIÈGE : Paramètres confus
public static void Commander(string a, string b, int c, bool d)
{
    // Qui se souvient de ce que représente 'a', 'b', 'c', 'd' ?
}

// ❌ PIÈGE : Méthode sans commentaire avec logique complexe
public static double Calculer(double x, int y, bool z)
{
    if (z && y > 5)
        return x * 0.9 * y;
    else if (!z)
        return x * y * 1.1;
    return x * y;
    // Que fait ce code exactement ?
}
```

---

## 6. Exercice pratique simple

**Créez un petit programme de café avec 3 méthodes :**

1. Une méthode pour afficher le menu
2. Une méthode pour calculer le prix d'une commande
3. Une méthode pour dire merci au client

**Solution exemple :**
```csharp
class MiniCafe
{
    public static void AfficherMenu()
    {
        Console.WriteLine("=== MENU ===");
        Console.WriteLine("1. Espresso - 2,50€");
        Console.WriteLine("2. Cappuccino - 4,00€");
    }

    public static double CalculerCommande(int choix, int quantite)
    {
        double prix = (choix == 1) ? 2.50 : 4.00;
        return prix * quantite;
    }

    public static void RemercierClient(string nom)
    {
        Console.WriteLine($"Merci {nom} ! À bientôt ! ☕");
    }

    static void Main()
    {
        AfficherMenu();
        double total = CalculerCommande(2, 2);  // 2 cappuccinos
        Console.WriteLine($"Total : {total:C2}");
        RemercierClient("Marie");
    }
}
```

---

## Conclusion

Les méthodes sont les **briques de base** de la programmation ! Elles nous permettent de :

- ✅ **Organiser le code** en blocs logiques
- ✅ **Réutiliser des fonctionnalités** sans duplication
- ✅ **Faciliter la maintenance** et les corrections
- ✅ **Rendre le code plus lisible**

**Prochaine étape :** Maintenant que vous maîtrisez les méthodes de base, vous pouvez explorer les classes et objets pour créer des programmes encore plus sophistiqués !

**Félicitations !** Vous savez maintenant créer vos propres "recettes de code" ! ☕

---