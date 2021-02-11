---
layout: post
author: vanak
---

Tu te souviens lorsqu'on rentrait des fonctions mathématiques dans notre TX-82 et puis quand on le lançais, ça nous affichait un super graphique ?
Tu l'avais écrit une fois et tu partageais ta découverte en le montrant à pleins de personnes pour essayer d'être la star (Instagram n'existait pas encore…).

![](https://cdn-images-1.medium.com/max/1600/1*Uuf-_yJY1AuEC4YDfFk9mA.png)

Maintenant que tu es devenu une star du code, tu as en même temps créer un robot-clone de toi qui exécute toutes les actions que tu lui envoies. 
Covid oblige, c'est lui qui va faire les courses à ta place. Chaque matin, tu lui écris d'aller chercher un croissant à la boulangerie, à midi un sandwich. 

Imagines si tu as 2 robots…

Tu vas devoir écrire chaque bloc de code dans chaque robot… 

Ne serait-ce pas surprenant s'il y avait un moyen pour regrouper ces actions et les utiliser à chaque fois que tu en as besoin ? 
Voilà à quoi servent les méthodes. Les méthodes te permettent de créer un bout de code en lui donnant un nom, puis d'exécuter ce code n'importe où dans ton programme. 

Dans cette ressource, je vais te montrer comment définir des méthodes en C# et comment s'en servir.

## 1. Historique
A mon avis, le mec qui a pensé aux fonctions devait avoir des tâches ingrates et répétitives chaque jour, le bouton `Ctrl` de son clavier devait être usé à mort à force de faire des copie-coller. Pour se libérer de ces tâches ingrates, il a écrit la librairie `fonction` pour pouvoir dupliquer des fonctions qu'il crée.

Les fonctions en informatique existent depuis le début et sont inspirées des fonctions mathématiques.

## 2. La ressource
### 2.1 Pourquoi utiliser des méthodes ?
![](https://cdn-images-1.medium.com/max/1600/1*yzgJ-66YvsokIvqw93jiJQ.png)
Les méthodes sont un élément central dans le développement avec C#.

Tu verras dans ta vie de développeur que pour produire un code maintenable et applicable à grande échelle, tu seras obligé d'utiliser de bonnes pratiques de codage.

En C#, toutes les instructions de ton programme doivent être placées dans des méthodes. Comme je te l'ai dit plus haut, une méthode représente une série d'opérations ou une tâche à faire.

Utiliser les méthodes permet de structurer ton code en découpant de manière logique les choses à faire. Découper et classer un mini-problème dans une méthode va rendre ton code plus lisible et compréhensif.

En plus, le fait de limité la responsabilité d'une méthode à un type de tâche uniquement va t'aider à corriger plus rapidement lorsque tu seras confronté à un bug. Tu auras l'air cool et sympathique parce que n'importe qui pourra relire ton code.

Que des avantages, non ?

L'inconvénient en C# est de bien comprendre son écriture après ça à toi la gloire.

### 2.2 Comment l'ordinateur interprète t'il les méthodes ?
Pour comprendre comment l'ordinateur interprète les méthodes va dans ton `Visual Studio`, crées un nouveau projet `methodTest` et colles le code suivant entre les accolades de la `class Program`: 
```cs
  static void Main(string[] args)
  {
    string prenom = TonPrenom();
    string nom = TonNom();
    Bonjour(prenom, nom);
  }

  private static void Bonjour(string prenom, string nom)
  {
    Console.WriteLine($"Bonjour, {nom} {prenom}");
  }

  private static string TonPrenom()
  {
    Console.WriteLine("Quel est ton prénom ?");
    Console.Write("> ");
    string prenom = Console.ReadLine();
    return prenom;
  }

  private static string TonNom()
  {
    Console.WriteLine("Quel est ton nom ?");
    Console.Write("> ");
    string nom = Console.ReadLine();
    return nom;
  }
```
Définis ce projet comme projet de démarrage et lances ce programme. Amuses-toi un peu.

Maintenant ce code semble un peu barbare pour toi jeune `Padawan`, et je me suis donné pour objectif qu'à la fin de cette ressource, tu sois plus à l'aise.

Ce qu'on va faire c'est qu'on va lire ensemble ces codes et je t'expliquerai un par un le contenu. 

Tout d'abord, on commence avec : 
```cs
  static void Main(string[] args)
  {
    string prenom = TonPrenom();
    string nom = TonNom();
    Bonjour(prenom, nom);
  }
```
Comment l'ordinateur sait que c'est une méthode ? Avec la signature de la méthode : `static void Main(string[] args)`. Là l'ordi sait que tu viens de `déclarer` une méthode qui s'appelle `Main` qui est une méthode `procédure` (on verra à quoi ça correspond plus bas) et qui est `static` (ça on le verra un autre jour avec les classes). 

A l'intérieur, il va lire ligne par ligne. 
Avec `string prenom` et `string nom`, il récupère les résultats de l'`exécution` des méthodes `TonPrenom` et `TonNom` puis va exécuter la méthode `Bonjour`.

Maintenant d'où viennent ces méthodes exécutées dans la méthode `Main` ? Avec la suite du code :

```cs
  private static void Bonjour(string prenom, string nom)
  {
    Console.WriteLine($"Bonjour, {nom} {prenom}");
  }
```
Cette méthode a pour signature `private static void Bonjour` avec deux paramètres `(string prenom, string nom)`. Au moment où cette méthode sera exécutée, il va afficher le message `Bonjour, nom prenom`. 
Ce que tu vois à travers ces lignes de codes est la `déclaration d'une méthode`. C'est dedans que tu vas mettre les instructions de ta méthode.

Ensuite : 
```cs
  private static string TonPrenom()
  {
    Console.WriteLine("Quel est ton prénom ?");
    Console.Write("> ");
    string prenom = Console.ReadLine();
    return prenom;
  }

  private static string TonNom()
  {
    Console.WriteLine("Quel est ton nom ?");
    Console.Write("> ");
    string nom = Console.ReadLine();
    return nom;
  }
```
Ces méthodes vont retourner une valeur c'est pour ça que dans la signature de la méthode à la place de `void`, on a le `type de retour`, ici tu vas attendre en retour de la méthode une valeur de type `string`.

Le mot clé `private` est le niveau d'accès de la méthode, il y a plusieurs niveau d'accès on verra ça en détail dans une autre ressource consacrée aux classes. Ici, tu as juste besoin de savoir qu'il est accessible seulement à l'intérieur de la classe `Program`.

Tu as vu, chaque méthode va remplir une tâche unique. Ces deux dernières méthodes vont te demander des informations, la méthode `Bonjour` va afficher un message et la méthode `Main` chapautte le tout. En effet, la méthode `Main` est le point d'entrée de ton application, le chef d'orchestre.

### 2.3 Les différentes signatures de méthodes
### 2.3.1 Les méthodes de base
Comme tu l'as vu, la méthode `TonPrenom` après un traitement (récupérer la saisie du clavier) renvoie une valeur. C'est pour ça que tu l'as déclaré avec la signature suivante : 
```
<niveau d'accès> <type de retour> <Nom de la fonction> ()
{
  Code de traitement
  retour <valeur>;
}  
```

### 2.3.2 Les méthodes procédures
La méthode `Bonjour` ne renvoie aucune valeur mais fait du traitement dans son code, c'est ce qu'on appelle une méthode procédure.
L'ordinateur va le reconnaitre grâce à sa signature : 
```
<niveau d'accès> void <Nom de la fonction>()
{
  Code de traitement;
}
```
Tu peux lui ajouté le mot clé `return` pour raccourcir le traitement, si tu veux quitter la méthode selon un contexte précis.

### 2.3.3 Les méthodes avec paramètres
Ces méthodes peuvent aussi avoir un ou plusieurs paramètres comme dans le cas de notre méthode `Bonjour(string nom, string prenom)`. Les paramètres sont des variables locales à une méthode et dont la valeur est fournie à partir de l'exécution de la méthode (On dit qu'on donne des arguments à l'exécution). 

Tu déclares un paramètre en précisant son type dans la signature de la méthode : 
```
<niveau d'accès> <type de retour> <Nom de la méthode> (<type> <nom de la variable local>)
{
  traitement avec la variable local
}
```
Puis lorsque tu exécutes ta méthode, tu lui donnes le nombre d'arguments dont elle a besoin, dans le cas de la méthode `Bonjour`, deux :
```cs
  // Déclaration
  private static void Bonjour(string prenom, string nom)
  {
    Console.WriteLine($"Bonjour, {nom} {prenom}");
  }


  static void Main(string[] args)
  {
    string prenom = TonPrenom();
    string nom = TonNom();
    // Exécution
    Bonjour(prenom, nom);
  }
```

Tu peux aussi avoir des paramètres optionnels, c'est à dire que tu n'es pas obligé de donner des arguments pendant l'exécution de la méthode. Pour pouvoir utiliser ce pouvoir, tu dois obligatoirement fournir une valeur par défaut à chacun des paramètres optionnels et doivent être placés après les paramètres normaux :
```cs
public void Bonjour(string nom, string prenom, bool codeur = true )
{
  if (codeur == true)
  {
    Console.WriteLine($"Bonjour {nom} {prenom}");
  }
  else
  {
    Console.WriteLine("Que fais tu ici ?");
  }
}

Bonjour(nom, prenom); ==> "Bonjour nom prenom"
Bonjour(nom, prenom, false); ==> "Que fais tu ici ?"
Bonjour(nom, prenom, true); ==> "Bonjour nom prenom"
```

### 2.3.4 Les méthodes avec paramètres en écriture : out et ref
Tu risques d'avoir un peu mal à la tête après ce que je vais de te faire découvrir ici et maintenant.

![](https://cdn-images-1.medium.com/max/1600/1*MeVkl4YqBnDqTkcXOGiYxA.jpeg)

Par moment, tu auras besoin de passer une variable dans ta méthode, la traiter dans ta méthode et retourner une autre valeur que celle de départ.

Un peu comme Pimp my Ride, tu envoies une vieille voiture au garage et puis on te ressort une voiture super stylée avec jantes de folies etc... 

Le problème avec C# et les méthodes c'est lorsque tu appelles une méthode et que tu lui passes en argument une variable de type valeur. Tu modifies la valeur de la variable dans ta méthode et puis tu retournes cette valeur, en fait rien ne se passe (pas vraiment rien) et la valeur n'a pas été modifiée.

Pourquoi ? Tout simplement parce que tu donnes à ta méthode seulement la valeur qu'il y a dans ta variable au lieu de lui donner la référence en mémoire de cette valeur. 

Pour bien comprendre, crées un nouveau projet `MyRefMethode` et colles le code suivant à la place du `Main` par défaut :
```cs
  static void Main(string[] args)
  {
    int annee = 2021;

    Console.WriteLine($"Avant méthode, annee = {annee}");

    NouvelleAnnee(annee);

    Console.WriteLine($"Après méthode, annee = {annee}");

  }

  private static int NouvelleAnnee(int annee)
  {
    return annee++;
  }
```
Dans le code ci-dessus, tu as déclaré une variable de type value `int` et assignes `2021` à la valeur. Ensuite tu déclares une méthode `NouvelleAnnee` qui reçoit un type value `annee` dans laquelle tu ajoutes 1 à la variable que tu passeras en argument.

Lances le code et vérifies que fait le code.

La méthode ne semble rien faire puisque que la variable `annee` renvoie toujours la même valeur. En fait la méthode fonctionne sauf que en C#, c'est un peu particulier avec les types valeur. Par défaut, un paramètre d'une fonction est en lecture seule, c'est à dire que ta méthode va juste lire la valeur contenue dans ta variable et ne pas affecter de nouvelle valeur.

Par contre si tu ajoutes ce petit mot clé magique `ref` devant le paramètre, la donne va changer : 
```cs
  static void Main(string[] args)
  {
    int annee = 2021;

    Console.WriteLine($"Avant méthode, annee = {annee}");

    NouvelleAnnee(ref annee);

    Console.WriteLine($"Après méthode, annee = {annee}");

  }

  private static int NouvelleAnnee( ref int annee)
  {
    return annee++;
  }
```
Vérifies que fait ce mot-clé magique. 

Qu'est ce que tu viens de faire cette fois ci ? Au lieu de lui passer une copie, tu lui passes la référence entière de ta variable qui a l'option d'être modifiable. Pour ça, tu dois retenir que pour les `value-type`, lorsque tu veux modifier sa valeur dans ta méthode, tu dois d'abord avoir une valeur initialisée et passer devant le mot clé `ref`.

Maintenant, tu as un deuxième cas de figure proche du `ref`, le `out`.

Cette fois-ci, tu n'as pas de valeur initialisée et ta méthode va retourner plusieurs valeurs. Impossible de retourner plusieurs valeurs dans une méthode simple à moins de retourner dans une liste, un tableau ou un tuple. 

```cs
  static void Main(string[] args)
  {
    int age;
    Console.WriteLine("Quel est ton age ? ");

    bool ok = int.TryParse(Console.ReadLine(), out age);
    
    if (ok)
    {
      Console.WriteLine($"Tu as {age} ans");
    }
    else
    {
      Console.WriteLine("Ce n'est pas un age ça...");
    }
  }
```
Ici, tu déclares une variable de type int `age` mais tu ne l'initialises pas. 
Tu demandes ensuite à l'utilisateur de saisir un age lorsque tu passes `Console.ReadLine()` comme argument de la méthode `TryParse` (méthode des `int`). Tu sais que `Console.ReadLine()` va te retourner un `string` alors que tu as déclaré ta variable en `int`. Ce que fait la méthode `TryParse`, c'est qu'elle va tester en premier paramètre si ce que tu tapes avec ton clavier est une valeur numérique et si c'est bien cela, va stocker dans la variable de retour `out age` tout en renvoyant un booléen pour être tester ensuite.

Ici, tu viens de renvoyer avec la méthode `TryParse`, deux valeurs : `out age` et un booléen. 

### 2.4 Les surcharges
Ok, tu as vu beaucoup de signatures de méthodes. Des méthodes qui retournent des valeurs, des méthodes qui ne retournent rien mais font des choses dans leurs comportements. Des méthodes sans paramètres etc. 

Entre autre, tu as créé une méthode avec 2 paramètres que tu as utilisé pour faire un petit calcul : 
```cs
  static void Main(string[] args)
  {
    int a = 20;
    int b = 30;

    Calcul(a, b);

  }

  private static int Calcul(int a, int b)
  {
    return a + b;
  }
```
Maintenant que tu es doué.e avec les méthodes, tu te sens capable d'implémenter les méthodes avec des `out` en paramètre, du coup tu écris le code suivant : 
```cs
static void Main(string[] args)
{
  int a = 20;
  int b = 30;

  int c;

  Calcul(a, b, out c);

}

private static int Calcul(int a, int b, out int c)
{
  c = a * b;
  return a + b;
}
```
Ok ça semble correct et ça fonctionne. Le truc c'est que des fois tu n'as pas besoin du `out` et juste de faire l'addition. Là est le problème. 

Dans ce cas de figure, tu as la possibilité de surcharger une méthode. What ? 

Yes, en C#, tu peux définir plusieurs méthodes qui ont le même nom mais une signature différente. C'est ce qu'on appelle les `surchages` de méthode. En gros, tu as ta méthode de base qui fait un traitement, tu peux avoir la même méthode avec un paramètre, et la même méthode avec 2 paramètres.

## 3. Points importants à retenir

Tu viens de voir comment créer des méthodes en C# pour les réutiliser lorsque tu en as besoin.
Tu as vu : 

* Les méthodes procédures qui font un traitement mais ne renvoient rien. Tu peux les repérer facilement avec le mot clé `void` dans leur signature.
* Les méthodes qui renvoient une valeur. N'oublies pas de mettre le type de retour dans la signature de ta méthode.
* Les méthodes avec des paramètres. Tu donnes des arguments au moment d'exécuter ces méthodes.

N'oublies pas que lorsque tu passes en argument une variable de type valeur dans une méthode, par défaut ce ne sera qu'une copie de la valeur qui sera envoyée, tu devras utiliser le mot clé `ref` pour modifier sa valeur en référence.

## 4. Pour aller plus loin

Comme d'habitude, la documentation de [Microsoft](https://docs.microsoft.com/fr-fr/dotnet/csharp/programming-guide/classes-and-structs/methods) est la ressource pour aller plus loin.

