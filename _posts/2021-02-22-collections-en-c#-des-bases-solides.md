---
layout: post
author: vanak
---

Tu t'es déjà retrouvé.e à faire les courses et à un moment donné tu te retrouves débordé.e d'articles entre tes mains parce que tu n'as pas pris de panier à l'entrée du magasin ? (Non, ça n'arrive qu'à moi... ok...)

Tout ça pour dire qu'avec C# ces paniers s'appellent des `Collections`, tu vas pouvoir mettre des données dans un panier.

Aujourd'hui, ma mission est de te faire comprendre les collections en C# et comment en mettre partout dans ton code.

![](https://miro.medium.com/max/1400/1*V0T1HfunNPPaNFM5vhpmCw.png)

## 1. Historique et Contexte
Il est fréquent que ton application doive manipuler de grandes quantités de données. Pour faire cela, le framework .NET (tu sais, la structure de base sur quoi le langage C# repose) fournit plusieurs structures de données, regroupées sous l'appellation `collections`. Les collections sont des structures de données importantes en programmation, encore. 

Tu adapteras la bonne structure en fonction de la situation, par exemple si tu as besoin de stocker des données par type, avec ou sans ordre. 

Ici, tu verras 3 types de structures à savoir les tableaux (`Arrays`), les listes (`List`) et les dictionnaires (`Dictionary`).

## 2. Ressources
### 2.1 Les tableaux avec C#
Tu sais qu'une variable permet de stocker une valeur et bien un tableau (`Array` in English) te permet de stocker plusieurs variables. Chacune d'elles a une place (un index) précise au sein de ton tableau (N'oublies pas que tu commences à compter un index en partant de 0). 

Par exemple, tu vas faire les courses et comme tu es bien organisé.e, tu prépares une liste. A l'intérieur, tu inscris du lait, des pâtes, de la litière et surtout du PQ. 

Tu as 3 manières de déclarer ce tableau : 
```cs
  // Manière N°1 
  type[] NomDeVariable = new type[NombreDelement];
  string[] TableauDeCourses = new string[4];
  // Ici Tu instancies un tableau de 4 éléments de type string que tu bloques en mémoire
  // Tu verras ce que veux dire le mot-clé new au moment de voir la Programmation Orientée Objet 
  TableauDeCourses[0] = "lait"; // Puis tu assignes à chaque emplacement une valeur, ici à l'emplacement 0
  TableauDeCourses[1] = "pâtes"; 
  TableauDeCourses[2] = "litière";
  TableauDeCourses[3] = "PQ"; // Si tu ne mets aucune valeur, tu vas allouer de l'espace en mémoire pour rien

  // Manière N°2
  string[] TableauDeCourses2 = new string[4] { "lait", "pâtes", "litière", "PQ" };
  // Ici au moment où tu instancies ton tableau, tu mets directement les valeurs correspondantes

  // Manière N°3
  string[] TableauDeCourses3 = { "lait", "pâtes", "litière", "PQ" };
  // Tu assignes directement des valeurs au tableau
  // Si tu viens d'un autre langage de programmation, tu auras plus l'habitude avec celui là
```

Pour accéder à chaque élément de ton tableau, tu vas utiliser les crochets ([]) et mettre l'index à l'intérieur :
```cs
  TableauDeCourses[2]; 
  // En appelant ton tableau avec l'index 2, tu obtiens le troisième élément de ton tableau : "litière"
```

Tu peux facilement faire une boucle `for` ou une boucle `foreach` avec un tableau pour accéder à chaque élément :
```cs
  for (var i = 0; i < TableauDeCourses.Length; i++)
  {
    Console.WriteLine(TableauDeCourses[i]);
  }

  foreach (var item in TableauDeCourses)
  {
    Console.WriteLine(item);
  }
```
`TableauDeCourses.Length` te permet de connaître la longueur de ton tableau et `TableauDeCourses[i]` à chaque élément en utilisant la variable `i` de ta boucle.

Par contre, si tu appelles une valeur avec un index non renseigné (comme TableauDeCourses[5]), au moment de compiler, tu auras une belle exception. Pas très agréable si c'est un utilisateur qui s'en aperçoit.

Tu peux très facilement modifier une valeur d'un tableau :
```cs
  TableauDeCourses[2] = "CocaCola zero";
```

Au fur et à mesure que tu remplis ton panier, tu veux rayer un élément de ta liste de courses. Le problème avec les tableaux c'est que tu dois d'abord allouer une quantité en mémoire au moment de sa création puis tu ne pourras plus modifier sa quantité après. Du coup, l'emplacement est toujours alloué en mémoire, imagines que tu dois gérer un entrepôt comme Amazon, tu n'imagines pas le gaspillage de mémoire ?

![](https://miro.medium.com/max/960/1*k7Yb4KgdRabP6eC3kt1BEw.gif)

Tu te doutes bien que les développeurs de Microsoft ont trouvé une alternative à ça, les `listes`.

### 2.2 Les listes avec C#
Comme un tableau, avec les listes tu vas pouvoir stocker plusieurs variables sauf que tu vas pouvoir faire plus de choses comme ajouter ou supprimer un élément.

Tu as 2 manières de déclarer une liste : 
```cs
  // Manière 1
  List<Type> NomDeVariable = new List<Type>();
  List<string> listeDeCourses = new List<string>(); // Si ça surligne en rouge, n'oublies pas de faire le using 
  listeDeCourses.Add("Chips"); // Puis tu lui ajoutes un élément à chaque fois
  listeDeCourses.Add("Coca"); // Chaque élément aura son index
  listeDeCourses.Add("PQ");
  listeDeCourses.Add("Mouchoirs");

  // Manière 2
  List<string> listeDeCourses2 = new List<string>() { "Chips", "Coca", "PQ", "Mouchoirs" }; 
```

Tu peux accéder à un élément de ta liste comme avec les tableaux : 
```cs
  listeDeCourses[2];
  // Tu obtiens "PQ"
```

Tu peux également boucler dessus : 
```cs
  foreach (var item in listeDeCourses)
  {
    Console.WriteLine(item);
  } 

  for (int i = 0; i < listeDeCourses.Count; i++)
  {
      Console.WriteLine(listeDeCourses[i]);
  }
```
A la différence du tableau, pour connaître la longueur d'une liste, tu fais un `.Count`.

Tu peux ajouter autant d'éléments que tu le souhaites et également en supprimer, pour ça tu as 2 méthodes :
```cs
  // Méthode 1 
  listeDeCourses.remove("Coca"); // Tu lui donnes quoi supprimer

  // Méthode 2
  listeDeCourses.removeAt(2) // Tu lui donnes l'index de l'élément à supprimer
```

Ok, c'est plutôt pratique. Maintenant, tu connais déjà le prix de chaque article et pour ne pas te faire arnaquer, tu veux leurs associer un prix. Pour ça tu peux utiliser les dictionnaires.

### 2.3 Les dictionnaires avec C#
Les dictionnaires (`Dictionary`) fonctionnent avec une relation `clé-valeur`. Les dictionnaires sont extrêmement pratiques quand tu veux stocker des données.

Tu as mis tes articles dans ton panier et ce serait cool de savoir à combien est le total de l'addition, non ? Pour faire cela, tu as besoin de connaître le prix de chaque article. 

Avec le dictionnaire, tu vas simplement mettre face à face, l'article et son prix, une relation `clé-valeur` : 
```cs
  Dictionary<TypeDeLaClé, TypeDeLaValeur> NomDuDictionnaire = new Dictionary<TypeDeLaClé, TypeDeLaValeur>();
  Dictionary<string, double> panierDeCourse = new Dictionary<string, double>();
  // Tu instancies un dictionnaire en lui donnant entre chevrons à gauche le type de la clé et à droite le type de la valeur

  panierDeCourse.Add("Coca", 1.30); // Pour ajouter un élément au dictionnaire, tu utilises la méthode .Add et tu fournis 
                                    // la clé et la valeur
  panierDeCourse.Add("PQ", 2.40); 

  panierDeCourse["kiwe"] = 0.99; // Tu peux aussi ajouter un élément en mettant la clé entre crochet et assigné une valeur
```

Pour accéder à un élément, tu ne pourras y accéder que si tu connais la clé : 
```cs
  panierDeCourse["Coca"];
```
Contrairement aux tableaux et aux listes, les dictionnaires n'ont pas d'ordre. Ils sont non ordonnés. Si tu regardes bien, une liste est un dictionnaire avec comme clé, l'index. Le fait d'être non ordonné est très important pour ton ordinateur. 

Pourquoi ? Parce que parcourir une liste un par un est plus long à faire que d'aller directement à la valeur grâce à la clé. La prochaine fois que tu devras ranger ton bureau, tu pourras dire que c'est plus rapide de trouver un élément dans ce désordre que de vérifier chaque tas bien ranger... 

Comme avec les autres collections, tu peux faire des boucles, utiliser des méthodes sur tes dictionnaires.

## 3. Ce que tu dois retenir
Ces 3 types de structure te permettent de stocker plusieurs données dans un conteneur de différentes manières selon le cas d'usage :
* Avec un tableau, tu détermines sa taille et son type au départ. Tu peux facilement modifier son contenu en sélectionnant l'emplacement et assigner une valeur : `TableauDeCourses[2] = "CocaCola zero";`
* Avec une liste, tu peux modifier sa contenance. Tu peux ajouter ou supprimer des éléments de ta liste : `listeDeCourses.remove("Coca");`
* Avec un dictionnaire, tu peux associer une clé à une valeur et tu peux y accéder plus rapidement qu'avec une liste ou un tableau : 
`panierDeCourse["Coca"];`

## 4. Pour aller plus loin
En cherchant un peu, tu remarques qu'il existe une collection `ArrayList` dans laquelle tu peux mettre différents types à l'intérieur, comme ce n'est pas une bonne pratique, j'ai fait l'impasse dessus mais sache que si ton imagination l'emporte et que tu as besoin d'avoir plusieurs types dans ta liste, tu peux l'utiliser.

Tu peux aussi avoir des `listes de liste`. Des `dictionnaires de listes`...

Bien entendu la doc de [Microsoft](https://docs.microsoft.com/fr-fr/dotnet/api/system.collections.generic.list-1?view=net-5.0) va te permettre de découvrir d'autres collections et d'autres méthodes applicables à nos 3 collections.

![](https://miro.medium.com/max/440/1*g6zHVkagNf4S2ZKmy-KSbQ.gif)
