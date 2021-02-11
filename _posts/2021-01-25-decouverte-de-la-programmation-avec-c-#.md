---
layout: post
author: vanak
---

Dans cette ressource, tu vas découvrir les bases de la programmation avec _C#_ (C sharpe). Tu verras comment créer un programme, comment déclarer tes premières variables, et quelques types de données de base.

![](https://miro.medium.com/max/1400/1*Uuf-_yJY1AuEC4YDfFk9mA.png)

## 1. Contexte et historique

Avant de connaître les joies et les pleurs du langage _C#_, tu dois comprendre dans quel écosystème tu vas te retrouver. 

En 2002, C# a été commercialisé par Microsoft pour développer sur sa plateforme Dot NET (.NET).

Pour ceux qui connaissent c’était aussi la fin de NSYNC…

![](https://miro.medium.com/max/1400/1*9WTlnR_ZFynXP1qC_dybEw.jpeg)

Cet écosystème .NET est composé : 
* Du langage de programmation __C#__ 
* D'un environnement de développement intégré (EDI) qui est __Visual Studio__
* D'un framework __.NET__
* D'une machine virtuelle qui va exécuter le code : le __CLR__ (Common Language Runtime)

### 1.1 C#, un langage les plus polyvalents

Le langage C# dérive du C++ et est très proche au niveau de la syntaxe du Java. 

Au fil des versions (on est à la version 9), C# s'est imposé comme un langage moderne, simple, orienté objet et généraliste. Il est _managé_ (pas la peine de gérer la mémoire) et fortement _typé_. Que du bonheur quoi. 

En plus il permet de développer des applications mobiles (__Xamarin__), des applications web (__ASP.NET MVC__, __ASP.NET CORE__), des applications bureau (__WPF__) et rien que pour toi, des jeux vidéos (__Unity__).

### 1.2 Visual Studio

Microsoft a sorti là un bijou pour les programmeurs fainéants dont je fais parti. 

Dans l'absolu, on peut utiliser n'importe quel éditeur de texte pour coder en C# mais avec Visual Studio, tu vas gagner en productivité.

A l'intérieur de la carrosserie, tu vas pouvoir trouver un bon éditeur de texte, un bon __compilateur__, un __débogueur__, un __intellisense__ (ton deuxième cerveau) et c'est vraiment bien fait pour te faciliter la vie de développeur.

### 1.3 Le framework .NET

C'est un ensemble d'outils et de composants logiciels qui permet de développer un type d'application pour un Os donné.

Il se décline en 4 sous ensembles : 
* .__NET Framework__ pour uniquement la création d'application Windows (__ASP.NET__ pour le web)
* __.NET CORE__ pour les applications multi-plateformes (Linux, Mac, Windows)
* __Xamarin/Mono__ pour les applications cross-plateformes mobiles (Android, Windows et MacOS)
* __.NET Standard__ partagé par les précédents frameworks

### 1.4 Le CLR (Common Language Runtime)

Le __Common Language Runtime__ est la machine virtuelle du framework .NET. 

Il va faire tourner une sorte de bytecode nommé Common Intermediate Language (CIL). 
Puis le compilateur à la volée va transformer le code __CIL__ en code natif spécifique au système d'exploitation (le __JIT Compiler__). 

Grosso Modo, il va transformer ton code C# écrit sur ton IDE Visual Studio en code compréhensible par la machine.

![](https://miro.medium.com/max/1248/1*qARmo9nhMrd9p-nkWTQ22A.jpeg)

## 2. La ressource
### 2.1 Ta première solution
Pour faire cet exercice, tu vas devoir installé Visual Studio Community sur ton ordinateur. Pour faire cet exemple, j'utilise un Mac mais cela ne change pas grand chose pour la version Windows.

Tu vas devoir créer un nouveau projet dans une nouvelle solution. Une solution est un conteneur logique qui regroupe un ensemble de projets distincts pouvant être liés entre eux et le projet forme le code source d'une application ou d'une bibliothèque de classes.

![](https://miro.medium.com/max/1400/1*zKFOtbWlTAdSbTyA3ChvXA.png)

![](https://miro.medium.com/max/1400/1*BY6ugFaTM7hHv1JYwAaKBw.png)

![](https://miro.medium.com/max/1400/1*XkWfBCt3JNRnnwFIY_1tzg.png)

![](https://miro.medium.com/max/1400/1*LnAR_1bDbU1gnnt5rG5k2g.png)

### 2.2 Ton premier programme
### 2.2.1 First program
Bon maintenant que tu as réussi à créer ta solution et ton premier projet, on va lui ajouter un peu de code. 

Tu vas te retrouver avec un fichier `Program.cs`, tous les fichiers en C# se terminent en `.cs`.

```cs
using System;

namespace MyFirstProgram
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
Le `using` est un import de librairie pour utiliser les classes qui existent dans cette librairie (Il se peut que tu aies plusieurs `using` selon la version du framework que tu utilises (par exemple sur Windows qui utilise `.NET Framework`)).

Le `namespace` est l'environnement de ton projet. 

La classe `Program` est la classe qui va exécuter ton program et le `static void Main` est le point d'entré de ton code. C'est cette méthode qui va lancer ton projet. C'est dedans qu'on va commencer à s'amuser avec notre premier code.

A l'intérieur de la méthode `Main`, tu vas remplacer `"Hello World!"` par : 
```cs
  Console.WriteLine("Bonjour, monde!");
```

Sur ton explorateur de solution (par défaut, il est à gauche sur Mac et à droite sur Windows), tu vas faire un clic droit sur le nom de ton projet et le mettre comme projet de démarrage.

Puis lance le programme en cliquant sur le bouton ▶️ (sur Windows, tu peux appuyer sur `Ctrl + F5`):

![](https://miro.medium.com/max/1400/1*09VGaa3GU6T8LxJTHucYfw.png)

Si tout se passe bien, tu vas avoir un terminal qui te dit `Bonjour, monde!`. Bravo tu viens de lancer ton premier programme.

J'ai entendu ta petie voix qui se demande que veut dire ce code ? 

`Console.WriteLine` veut tout simplement dire qu'on va utiliser la classe `Console` (on verra plus tard ce qu'est une classe) qui s'occupe d'appeler ton terminal et on va appeller sa méthode `WriteLine` qui va récupérer ce que tu lui donne entre `""` pour l'afficher.

### 2.2.2 Programs
On va créer plusieurs projets dans cette solution.

Sur l'explorateur de solution, tu vas faire un clic droit sur le nom de la solution et tu vas ajouter un nouveau projet qu'on va nommer `MySecondProgram`.

A l'intérieur de la méthode `Main`, tu vas copier le code ci-dessous : 
```cs
Console.WriteLine("Bonjour, monde !");
Console.WriteLine("Ton terminal te redis encore une fois : Bonjour, monde !");
Console.Write("Oui je te parle ...");
Console.Write("On va beaucoup se parler dans les jours à venir");
```
Exécute-le et vérifies ce que fait ce code. Vois-tu une différence ? D'après toi, quelle est la différence entre `Console.WriteLine` et `Console.Write` ?

Crées un autre projet `MyThirdProgram` et dans le `Main` remplaces le code par celui ci : 
```cs
for (int i = 0; i < 10; i++)
{
    Console.WriteLine("Bonjour le monde !");
}
```
Vérifies ce que fait ce code...

Crées un autre projet `MyFourthProgram` et pareil dans le `Main`, colles ce code : 
```cs
Console.WriteLine("Bonjour, monde !");
// Ceci est un commentaire
Console.WriteLine("Ton terminal te redis encore une fois : Bonjour, monde !");
Console.Write("Oui je te parle ..."); // Ceci est un autre commentaire
Console.Write("Il est passé où le commentaire ?");
/* Ceci est un long commentaire
    sur plusieurs lignes
    Tu me vois dans le terminal ?
  */
```
D'après toi, que font `//` et `/* */` ?

Crées un autre projet `MyFifthProgram` et colles ce code : 
```cs
string myFirstString = "Bonjour Monde !";
Console.WriteLine(myFirstString);
```
D'après toi, que va faire ce programme ? Exécute-le et vérifies...

Crées un autre projet `MySixthProgram` et le code ci-dessous : 
```cs
Console.WriteLine(10);
Console.WriteLine(10 + 13);
Console.WriteLine(24 - 7);
Console.WriteLine(24 * 10);
Console.WriteLine(60 / 5);
```
Tu connais le refrain... 

Allez crées un dernier projet `MySeventhProgram` et puis colles le code ci-dessous : 
```cs
int birthYear = 1998;
if (birthYear == 1998)
{
  Console.WriteLine("Et 1 et 2 et 3 zéro, la lala la la lalalala...");
}
```
D'après toi que fait ce code ? Exécute-le...

Bon on s'est bien amusé ! Tu viens de découvrir pas mal de chose sympathique, d'accord tu ne comprends pas tous ces codes mais ça va arriver.

Il se peut que ton `Builder` ne fonctionne pas exactement comme tu l'espérais et qu'il affiche en `console` (terminal) le précédent code... Pas de panique, il faut nettoyer un peu ta solution. Dans ta barre des menus tout en haut, va dans l'onglet `Générer` puis sélectionne `Nettoyer la solution` et relance un `Démarrer`.

### 2.3 Les variables

La notion de variable est fondamentale en informatique. Tu dois absolument connaître cette notion si tu veux devenir développeur parce que tu vas en manipuler beaucoup. 

### 2.3.1 Variable 

Une variable est un symbol. Elle associe un nom à une valeure. Une variable c'est comme une boite étiquettée avec un nom et à l'intérieur, tu y mets les affaires correspondantes.

En C#, cette variable a un type, c'est le petit mot-clé que tu as aperçu dans nos exemples dans la partie au dessus.

Une variable se déclare comme ça : `type nomDeVariable = valeur ;` avec le nom de la variable en `camelCase` (Début en minuscule puis majuscule à chaque mot).

Prenons quelques exemples : 
```cs
string aString = "Bonjour monde";
char aCharacter = 'A';
int aInteger = 10;
double aDouble = 2.5;
```
Dans ce programme, tu as écrit 4 choses : 
* Tu as déclaré une variable `aString` de type `string` et tu as assigné la valeur `"Bonjour monde"`
* Ensuite tu as déclaré une variable `aCharacter` de type `char` et tu as assigné la valeur `'A'`
* Puis tu as déclaré une variable `aInteger` de type `int` et tu as assigné la valeur `10`
* Enfin tu as déclaré une variable `aDouble` de type `double` et tu as assigné la valeur `2.5`

Comme son nom l'indique, cela va être un élément dont la valeur peut changer mais pas sa nature.

### 2.3.2 Const

Contrairement à la variable simple, une `const` est un dérivé de variable mais dont la valeur ne changera pas.

Une `const` se déclare : `const + type + NomDeVariable = valeur ;` avec le nom de la variable en `PascalCase` (Majuscule en début de mot)
```cs
const string MyLastName = "Pan";
const string MyFirstName = "Peter";
const int MyBirthYear = 670;
```

Voilà tu viens de découvrir les variables, on va compliquer un peu la donne dans le prochain chapitre.

### 2.4 Les types de données simples
Les types de données sont également une notion très importante en informatique et particulièrement sur C#. 

Les types de données sont un peu ce que tu peux mettre dans les variables. Tu en as vu plusieurs exemples dans le chapitre précédent : `string`, `int`, `char`, `double`. 

Les variables ont forcément un type. On dit que le langage C# est fortement typé ou a un typage statique. C'est à dire que tu dois absolument lui donné un type.

Ce type peut être définit au moment de la déclaration de la variable.

Pour autant, C# autorise le mot-clé `var` à la déclaration. `L'inférence de type` permet au compileur de reconnaître le type de la variable au moment de l'initialisation de la variable.

Si l'inférence de type ne permet pas de reconnaître le type, C# autorise le typage `dynamique`.

Maintenant ces types se classent sous 2 catégories.

### 2.4.1 Les types primitifs simples

Un type primitif est un `type valeur` (value-type). C# fournit les types valeur intégrés (`type primitif`) suivant :  
* Les types numériques intégraux (`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`)
* Les types numériques à virgule flottante (`double`, `float`, `decimal`)
* Les `Boolean` (`true`, `false`)
* Le `Char`, un seul caractère (`A`, `a`)

Tu va choisir ton type en fonction de la plage de ton nombre et de la taille en mémoire. 

Tu ne vas pas trop te compliquer la vie pour le moment et tu vas utiliser pour l'instant ces types primitifs simples ci-dessous : 
* En général, tu vas utiliser les integer `int` pour mettre un nombre à une action. 
* Les double `double` vont te servir à faire des opérations mathématiques même si tu peux le faire aussi avec les `int`.
* Les booléens `bool` te permettront de faire des conditions : si c'est ok tu continues de lire la suite.
* Les caractères `char` te permettront de mettre en majuscule ton joli prénom par exemple.

Ok, passons un peu à la pratique !

Même refrain, crées un nouveau projet `MyFirstPrimitive` et n'oublies pas de le mettre comme projet de démarrage :

```cs
int one = 1;
int two = 2;
Console.WriteLine(one + two);
```
Lances le programme et vérifies ce qu'il fait. Ok, tu peux faire des additions avec des `int`.

Remplaces le précédent code avec celui ci : 

```cs
double one = 1.5;
double two = 2.7;
Console.WriteLine(one + two);
```
D'après toi que va faire ce code ? 

Changes maintenant avec celui là : 
```cs
int a = 1;
double b = 5.6;
Console.WriteLine(a + b);
```
Que fait le code ? 

Modifies maintenant avec ce code là : 
```cs
bool oui = true;
bool non = false;
Console.WriteLine(oui + non); 
```
Que fait le code ? Tu as vu Visual Studio est plus intelligent, passes ta souris sur ce qui est surligné en rouge, qu'est ce qui te raconte ?

Enfin un dernier bout de code pour la route : 
```cs
char a = 'A';
char b = 'a';
Console.WriteLine(a + b);
```
D'après toi que fait ce code ? 162 ? C'est quoi ça ? En fait chaque caractère est représenté par sa valeur `ASCII` et la référence du caractère `A` est 65 et celle de `a` est 97, donc 65 + 97 = 162.

### 3.4.2 Les types références

Il existe un autre type de variable qui est le type référence. 

Les variables de type référence font référence à leurs données contrairement aux variables de type valeur qui contiennent leurs données. 

Grosso modo en créant une variable de type référence, la valeur a une référence (une adresse) à l'emplacement mémoire de l'objet. 

Les types références sont les suivants : 
* Les `class` 
* Les `interface`
* Les `delegate`
* Les `enregistrement`
* Les `dynamic`
* Les `object`
* Les `string`

Le type référence le plus connu et que tu as déjà manipulé est le type `string` pour chaîne de caractères. Il est toujours sous des doubles guillemets `""`.

Allez tu vas manipuler quelques chaînes de caractères. 

Crées un nouveau projet `MyString` et colles le code ci-dessous : 
```cs
  string hello = "Hello";
  string world = "World";
  Console.WriteLine(hello + world);
```
D'après toi que va faire ce code ? On appelle cette opération `concaténer` des chaînes de caractères. Par contre, c'est moche, non ? 

Changes le code avec celui là : 
```cs
  string hello = "Hello";
  string world = "World";
  Console.WriteLine(hello + " " + world); 
```
Qu'est-ce que tu remarques ? Un espace est considéré comme un `string` ou plutôt un `char`. 

Maintenant remplaces avec ce code là : 
```cs
  string hello = "Hello";
  string world = "World";
  char a = 'A';
  Console.WriteLine($"{hello} {world} {a}");
```
D'après toi que fait le code ? On appelle ça un `string interpolation`.

Encore un dernier code avec les strings : 
```cs
  string hello = "Hello";
  string world = "World";
  char a = 'A';
  Console.WriteLine("{0} {1} {2}", hello, a, world);
```
Alors qu'est-ce que ça donne ? On appelle ça un `composite formatting`.

Prends celui qui te plait le plus, perso je vais utiliser le `string interpolation`. Mais ça c'est moi...

Ouh beaucoup d'informations, mais ce qui est bien c'est que tu as manipulé un peu de code.

![](https://miro.medium.com/max/1000/1*mLFh2XXNiZfoT_O9_YvHEQ.gif)

### 2.5 Le contrôle du flux (Control flow)

Encore une notion fondamentale de programmation, le contrôle de flux (`control flow`). C'est quoi le `control flow` ? C'est contrôler la direction que doit prendre ton code... Okay je t'ai perdu...

Quand ton ordi lit le code, il va suivre les instructions lignes par lignes (séquentiellement). Il crée un flux. Avec le `control flow` tu vas pouvoir rediriger les instructions en fonction d'une condition.

### 2.5.1 If statement

Imagines qu'il est midi et que tu décides d'aller acheter un sandwich à la boulangerie du coin. Ton camarade codeur est en plein déboguage et n'a pas le temps d'y aller avec toi. Il te demande si tu peux lui prendre un sandwich.

Par contre il précise que s'il n'a pas de sandwich au poulet, tu lui prends à la place un sandwich au fromage.

Tu cours à la boulangerie et il n'y a plus de sandwich au poulet donc pour ton pote, tu lui prends un au fromage.

En code ça donne ça : 
```cs
  int numberOfChickenSand = 1;

  if (numberOfChickenSand == 0)
  {
    Console.WriteLine("J'achète pour mon pote un sandwich au fromage.");
  }
  else
  {
    Console.WriteLine("Je lui prend un sandwich au poulet.");
  }
```
D'après toi que fait ce code ? Modifies `numberOfChickenSand` avec la valeur 0 et relances ton code. Vois tu la différence ?

### 2.5.2 Switch Case
Maintenant tu es en train de te détendre en regardant Netflix. Bon on est d'accord il y a tellement de choix que tu perds plus ton temps à choisir qu'à mater ta série préférée. Bref...

Voilà que tu as déchiffré l'algorithme de Netflix et que celui ci te propose que quelque choix en fonction du nombre de temps que tu passes à coder.

Le truc c'est que tu peux coder 30 minutes, 1 heure, 2 heures, 3 heures, 4 heures 30 etc... Avec des `if else statement`, tu vas vite te retrouver avec beaucoup de ligne. 

![](https://miro.medium.com/max/516/1*Cn1fvq-m7q7zQC8D2vzXjg.png)

Ici tu as une donnée (le temps passé à coder) et en fonction de cette donnée, il y a un choix. Pour cela, tu vas utiliser le `switch case statement` : 

```cs
  int numberOfCoding = 6;

  switch (numberOfCoding)
  {
    case 1:
      Console.WriteLine("CS 50");
      break;
    case 2:
      Console.WriteLine("CS 50");
      break;
    case 3:
      Console.WriteLine("Dix pour cent");
      break;
    case 4:
      Console.WriteLine("Suits");
      break;
    case 5:
      Console.WriteLine("Emily in Paris");
      break;
    case 6:
      Console.WriteLine("Lupin");
      break;
    default:
      Console.WriteLine("Ce cas de figure n'existe pas...");
      break;
  }
```
D'après toi que fait le code ? Changes la valeur de `numberOfCoding` et amuses toi un instant...

### 2.6 Les boucles (Loops)

Dernière notion fondamentale et tu seras prêt pour faire des petits programmes sympa. 

### 2.6.1 For loop
Imaginons qu'il est 18h et que tu sors faire une petite pause en prenant l'air et en écoutant une musique. Il y a un song que tu veux écouter pendant ta pause plusieurs fois.

A l'ancienne, dès que la chanson se terminait, tu appuyais à nouveau sur play et ainsi de suite le temps de ta pause.

Comme d'habitude, tu crées un nouveau projet `MyFirstLoops` et colles le code suivant : 
```cs
  Console.WriteLine("Plays my favorite song");
  Console.WriteLine("Plays my favorite song");
  Console.WriteLine("Plays my favorite song");
  Console.WriteLine("Plays my favorite song");
```
A ton avis, que fait ce code ? C'est répétitif et il doit bien y avoir un moyen d'écouter ton song préféré sans avoir à appuyer plusieurs fois sur play. 

Changes ce précédent code avec celui là : 
```cs
for (int i = 0; i < 4; i++)
{
    Console.WriteLine("Plays my favorite song");
}
```
Alors ? Cela fait exactement la même chose que le précédent code sans écrire plusieurs fois la même chose.

Cette notion s'appelle une boucle (`loop`) et te permet de répéter plusieurs fois la même chose (le code entre les accolades). Ici, tu viens de voir la boucle `for` (For loop). 

Mets en commentaire le précédent code puis colles celui ci : 
```cs
  Console.WriteLine("--- i ---");
  for (int i = 0; i < 4; i++)
  {
      Console.WriteLine(i);
  }

  Console.WriteLine("--- index ---");
  for (int index = 0; index < 4; index++)
  {
      Console.WriteLine(index);
  }

  Console.WriteLine("--- otherVariable ---");
  for (int otherVariable = 0; otherVariable < 4; otherVariable++)
  {
      Console.WriteLine(otherVariable);
  }
```
D'après toi que fait ce code ? 

Comme tu peux le voir, il fait des boucles identiques commençant par 0. En informatique, on a l'habitude de commencer à compter à partir de 0, commences à t'y habituer...

Avec la boucle `for`, tu peux lui donner une variable de départ `int i`, une variable de fin `i < 4` et après chaque tour la valeur de `i` s'incrémente (`i++`).

### 2.6.2 While loop

Passons à un autre type de boucle, la boucle `while`. 

Contrairement, à la boucle `for` qui a forcément une variable de fin, la boucle `while` peut continuer à boucler tant que la condition donnée est vraie.

Qu'est ce que je veux dire par ça...

Imagines que tu oublies le chargeur de ton ordi chez toi et que tu es en train d'apprendre à coder dans un lieu public. 

Tu vas continuer à coder `tant que` la batterie de ton ordi tient le coup, mais dès qu'elle est vidée, tu es forcé.e de t'arrêter (mouais comme par hasard tu as oublié de charger ton ordi...). 

En code, ça va te donner un truc comme ça : (crées un nouveau projet `MyWhileLoop` et colles celui là)
```cs
  int batterie = 100;

  while (batterie > 10)
  {
      Console.WriteLine($"Niveau de batterie : {batterie}");
      Console.WriteLine("Tu codes");
      batterie -= 10;
  }
```
Exécutes ce code. Tant que la valeur de la batterie est supérieur à 10, le message `Tu Codes` va s'afficher sur le terminal. Et dès qu'il est inférieur à 10, tu sors de la boucle `while`.

Maintenant changes ce qui est entre les parenthèses par `true` et lances le code... 

Une boucle infinie ! Arrête le code avec `ctrl + c` et éteins ton terminal. 

![](https://miro.medium.com/max/488/1*39diz83UZexNZ0b7ucBXkQ.gif)

Lorsque tu utilises une boucle `while`, n'oublies pas de mettre une `condition d'arrêt`. Ce que tu as fait dans le code précédent c'est que tu as `décrémenté` de 10 la variable `batterie` pour qu'un moment il sera inférieur à la `condition d'arrêt`.

En cherchant un peu sur le net, tu vas découvrir qu'il existe une variante du `while` le `do while`. Ce qu'il va faire c'est qu'il va exécuter une première le code puis rentrer dans la boucle.

## 3. Points importants à retenir
* Tu as vu que C# fait parti de l'écosystème .NET qui est une réponse à Java pour créer du code sous Windows. Cet écosystème est composé du framework `.NET`, du langage `C#`, d'un éditeur de code `Visual Code` et d'un `Common Language Runtime`
* Tu as vu la première notion fondamentale en informatique, l'utilisation des variables. En C#, il existe 2 types, un type primitif qui stock la valeur donnée et un type référence qui va pointer la valeur vers un espace en mémoire. Les principaux sont les integer (`int`), les nombres à virgule double (`double`), les caractères individuels (`char`), les valeurs booléens (`bool`) et les chaînes de caractères (`string`).
* Tu as vu comment contrôler la direction de la lecture du code avec les `if statement` et les `switch case`
* Et tu as vu comment répéter plusieurs fois la même chose avec les boucles `for` et les `while`.

## 4. Pour aller plus loin

Rien de tel que la documentation de [Microsoft](https://docs.microsoft.com/fr-fr/dotnet/csharp/)...

