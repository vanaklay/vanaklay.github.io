---
layout: post
author: Vanak
---

La vie d’Emily va t-elle se compliquer dans la saison 2 ?

Je viens de terminer la série Emily in Paris sur netflix et je comprends parfaitement pourquoi Emily tombe amoureuse de son voisin de paillasson [Gabriel](https://fr.wikipedia.org/wiki/Lucas_Bravo). Il est plutôt BG et semble bien cuisiner.

![](/assets/img/enumerators.png)

Quel est le rapport entre cette série et Ruby ? Simplement que je suis aussi tombé amoureux de Ruby… pareil voisin de paillasson, plutôt BG dans la lecture du code, simple, prometteur malgré qu’on l’annonce dans le déclin et contrairement à la vie d’Emily, ton code ne vas pas être dirty…

Tu sais le code où il y a les boucles dans les boucles qui ont un `if statement` dans une autre boucle, le code bien dégueulasse de mes débuts quoi...
```ruby
for machin in machins do 
  if machin != nil
    for item in machin do
      for atom in item do
        for neutron in atom do
        end
      end
    end
  end
end
```
Puis quand tu lances ça, tu as tout qui explose parce que tu as oublié un `end` quelque part…

T’imagines tout le temps que tu perds à écrire toutes ces lignes de codes puis si ça pète de vérifier. Alors là, c’est juste sur quelques lignes, mais imagines sur une app qui a plusieurs dizaines de milliers de lignes de codes … Tu es dead…

Si je te disais qu’il y a un mec chez Ruby qui a voulu t’empécher de devenir Champion du monde du lancer de PC et te simplifier ta vie de codeur Ruby pour écrire du code plus lisible et moins dirty.

Moins de stress qu’Emily se serait génial non ?

![](https://www.wmagazine.com/wp-content/uploads/2020/09/emily-in-paris.jpeg?w=640px)

En ruby, tu as les méthodes `Enumerators`.

Un peu comme Emily in Paris qui enchaine les petites aventures nocturnes avec ses amoureux, j’ai passé mes nuits sur plusieurs langages de programmation (javascript, python, php, C#), alors oui peut être que je n’ai pas poussé leurs apprentissages à fond mais vraiment les `Enumerators` c’est la vie.

Tu as une petite avancée sur javascript depuis ES6, Python avec les list comprehension et Php … wait for it… ça ne me vient pas à l’esprit.

Dans cet article, c’est exactement ce à quoi on va s’intéresser. Je vais te présenter 5 enumerators pour simplifier ta vie de développeur Ruby.

## Hey Mec c’est quoi un Enumerator ?
Les `Enumerators` sont des méthodes codés dans Ruby pour t’aider à faire des itérations, donc des boucles, sur des hashs ou des arrays plus simplement et en écrivant moins de codes.

## Comment était la vie sans les Enumerators ?
Imagines que ton job est de savoir avec quels gars, Emily Cooper n’a pas échangé de cours de langue française.

Sachant qu’elle n’a pas encore embrassé Luc, nous avons un array de plusieurs noms sur lequel faire une boucle puis filtrer avec une condition pour retirer Luc.

En code ça donne ça :
```ruby
peoples = ["Luc","Gabriel", "Thomas", "Camille"]
list_kissed = []
for people in peoples do
  if people != "Luc"
    list_kissed.push(people)
  end 
end
list_kissed #=> ["Gabriel","Thomas", "Camille"]
```
7 lignes de code pour retirer le pauvre Luc de la liste d’Emily.

Heureusement Ruby a été développé pour rendre le code accessible et beau pour le développeur mais également pour les humains normaux. Merci à toi, inconnu développeur de la team `Matz`, je te kiff !

## Each et Each_with_index
Avec cet enumerator, tu peux accéder à chaque élément d’un array ou d’un hash et jouer avec.
```ruby
peoples = ["Luc","Gabriel", "Thomas", "Camille"]
list_kissed = []
peoples.each do |people|
  if people != "Luc"
    list_kissed.push(people)
  end 
end
list_kissed #=> ["Gabriel","Thomas", "Camille"]
```
Okay, rien d’impressionnant et c’est exactement comme avec une boucle `for in` classique. En fait oui, mais comme c’est le premier enumerator créé, je voulais quand même te le présenter parce qu’il ne vient pas seul. Il vient avec son pote `each_with_index`, et là tu peux récupérer l’index de l’itération dans ton `each`, ce qui t’évite de faire un `.times do`.

Regardes un peu :
```ruby
peoples = ["Luc","Gabriel", "Thomas", "Camille"]
peoples.each_with_index do |people, i|
  puts "#{i} - #{people}"
end
#=> 0 - Luc
#=> 1 - Gabriel
#=> 2 - Thomas
#=> 3 - Camille
```
Cela peut servir si tu as besoin d’avoir l’index.

## Select
Allez on rentre dans le dur.

Avec `select`, tu récupéres dans un array ou dans un hash les éléments qui remplissent la condition donnée.
```ruby
peoples = ["Luc","Gabriel", "Thomas", "Camille"]
list_kissed = peoples.select{|people| people if people != "Luc" }
list_kissed #=> ["Gabriel","Thomas", "Camille"]
```
Ce que fait le select ici, c’est qu’il te retourne dans un array `list_kissed` (ça marche également pour un hash), un élément `people` de l’array `peoples` en filtrant avec notre condition `if people != "Luc"`. Tu vois c’est plutôt pratique, ça tient sur une ligne et c’est lisible.

## Reject
Avec `reject`, tu peux récupérer dans un array ou dans un hash, les éléments qui ne remplissent pas la condition donnée.
```ruby
peoples = ["Luc","Gabriel", "Thomas", "Camille"]
list_kissed = peoples.reject{|people| people if people == "Luc" }
list_kissed #=> ["Gabriel","Thomas", "Camille"]

peoples = { "Luc" => "male", "Gabriel" => "male", "Camille" => "lady","Antoine" => "male", "Sylvie" => "lady", "Julien" => "male"}
ladies_in_paris = peoples.reject{|people,sexe| people if sexe == "male" }
ladies_in_paris #=> {"Camille"=>"lady", "Sylvie"=>"lady"} 
reject fonctionne à l’inverse de select. C’est à toi de voir.
```
## Map
Avec la méthode `map`, tu récupères le résultat dans un array ou dans un hash, chaque élément que tu peux modifier.
```ruby
peoples = ["Luc", "Gabriel", "Thomas", "Camille", "Antoine", "Sylvie", "Julien", "Pierre", "Mindy"]
list_in_paris = peoples.map { |people| people.upcase }
list_in_paris #=> ["LUC", "GABRIEL", "THOMAS", "CAMILLE", "ANTOINE", "SYLVIE", "JULIEN", "PIERRE", "MINDY"]
```
Tu vois que pour chaque élément de l’array de base, je modifie sa casse en majuscule.

## Reduce
La méthode `reduce` te permet d’obtenir la valeur total dans un array ou dans un hash. Par exemple, tu veux savoir le nombre de minutes que j’ai passé à regarder toute la saison 1…

Rien de plus simple, tu fais un `each` en initialisant un compteur à zéro et tu l’incrémentes de la durée :
```ruby
total_minutes = 0
saison_one = [24, 25, 23, 24, 27, 25, 23, 25, 24]
total_minutes = saison_one.each {|duration| total_minutes += duration }
total_minutes #=> 220
```
Ou bien un reduce :
```ruby
saison_one = [24, 25, 23, 24, 27, 25, 23, 25, 24]
total_minutes = saison_one.reduce{|sum, number| sum + number }
total_minutes #=> 220
```
Le `sum` est ici un accumulateur qui va remplacer l’initialisation d’un compteur, et la méthode te retourne cet accumulateur.

Allez cadeau pour toi qui est arrivé jusqu’ici…

Ou bien tu fais `.sum` à l’array seulement :
```ruby
saison_one = [24, 25, 23, 24, 27, 25, 23, 25, 24]
total_minutes = saison_one.sum
total_minutes #=> 220
```

## Map! Select! Reject!
Avec toutes ces méthodes tu peux commencer à frimer en société ! Et pour paraître encore plus arrogant, laisses moi te donner encore une dernère manip.

Lorsque que tu appliques ta méthode par exemple `.map` à ton array, tu recrées un nouvel array et ne modifies pas l’ancien. Alors que si tu appliques `.map!` avec un point d’exclamation, tu modifies l’array de base :
```ruby
peoples = ["Luc","Gabriel", "Thomas", "Camille"]
list_kissed = peoples.select{|people| people if people != "Luc" }
list_kissed #=> ["Gabriel","Thomas", "Camille"]

peoples.select!{|people| people if people != "Luc" }
peoples #=> ["Gabriel","Thomas", "Camille"]
```
Encore moins de variables à déclarer mais tu remplaces ton array initial. A toi de voir, c’est toi le chef !

![](https://assets.afcdn.com/story/20201006/2090136_w980h638c1cx300cy148cxt0cyt0cxb620cyb420.jpg)

Voilà tu viens de voir 5 méthodes enumerators qui vont te simplifier la vie de développeur Ruby.

Avec un `map`, tu peux récupérer un hash ou bien un array en modifiant chaque élément de l’objet de base.

Avec un `select`, tu peux récupérer un hash ou un array en conservant seulement les éléments qui remplissent ta condition. Pour le `reject` c’est l’inverse.

Avec un `reduce`, tu t’évites des calculs mentaux.

Enfin avec un `each`, tu peux juste te la péter…

J’espère que cet article t’aidera dans l’apprentissage du langage de programmation Ruby et si tu bloques n’hésites pas à poster ton problème en m’envoyant un email à contact@vanaklay.com. Je prendrai le temps de t’aider à trouver une solution.

A bientôt !

## Remerciements 
* A tous les sites où j'ai piquer les images de cet article ! 
* A la Team Felicita pour la relecture, Martin Louvard.