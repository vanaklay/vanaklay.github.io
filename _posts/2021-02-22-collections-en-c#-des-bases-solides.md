---
layout: post
author: vanak
---

Tu t'es déjà retrouvé à faire les courses et à un moment donné tu te retrouves débordé d'articles entre tes mains parce que tu n'as pas pris de panier à l'entrée du magasin ? (Non, ça n'arrive qu'à moi... ok...)

Tout ça pour dire qu'avec C# ces paniers s'appellent des `Collections`, tu vas pouvoir mettre des données dans un panier.

Aujourd'hui, ma mission est de te faire comprendre les collections en C# et comment en mettre partout dans ton code.

## 1. Historique et Contexte
Il est fréquent que ton application doive manipuler de grandes quantités de données. Pour faire ceci, le framework .NET (tu sais, la structure de base sur quoi le langage C# repose) fournit plusieurs structures de données, regroupées sous l'appellation `collections`. Les collections sont des structures de données importantes en programmation. 

Tu adapteras la bonne structure en fonction de la situation, par exemple si tu as besoin de stocker des données par type, avec ou sans ordre. 

Ici, tu verras 3 types de structures à savoir les tableaux (`Arrays`), les listes (`List`) et les dictionnaires (`Dict`).

## 2. Ressources
### 2.1 Les tableaux avec C#
Un tableau (`Array` in English) te permet de stocker plusieurs variables chacune ayant une place (un index) précise au sein du tableau (N'oublies pas que tu commences à compter un index en partant de 0). 

Tu as 3 manières de déclarer un tableau : 
```cs
```

cities contient actuellement 3 entrées et tu peux confirmer cela grâce à la méthode .length : en entrant cities.length dans IRB, tu obtiens bien en retour l'Integer 3. Tu peux appeler une des variables stockées dans ce array en utilisant son index (variant, ici, de zéro à deux). Par exemple, si tu tapes cities[0], tu dois obtenir en retour "Paris". Si par contre tu fais le test avec une valeur d'index non renseignée (comme cities[3]), tu obtiens nil.

Tu peux tout à fait stocker ce que tu veux dans un array : tous les types de variables sont acceptés… même les arrays ! Exemple : miscellaneous = ["Zoé", 145000, true, ["bleu", "noir", false]]. Ainsi, si on fait miscellaneous[3], on obtient un array. Et si on fait miscellaneous[3][1] on obtient "noir", la variable n° 2 du sous-array lui-même situé à l'index n°3 de miscellaneous. 🤯

Tu peux très facilement modifier une entrée d'un array. Exemple :

Le problème avec les tableaux c'est que tu dois d'abord allouer une quantité en mémoire au moment de sa création puis tu ne pourras plus modifier sa quantité après. Tu te doutes bien que les developpeurs de Microsoft ont trouvé une alternative à ça, les `listes`.

### 2.2 Les listes avec C#
Comme un tableau, avec les listes tu vas pouvoir stocker plusieurs variables mais de même type. 


### 2.3 Les dictionnaires avec C#
Dans ce cours, tu vas apprendre à maîtriser les tables de hashage (ou hash), un type de données assez proche des arrays et indispensable quand on fait de la programmation. Les Hash sont extrêmement pratiques (incontournables même) quand on veut stocker des données.

Les hash et arrays sont des types de données aussi universels que les booléens, strings, integers, et floats. Ils sont à la base de l'univers de la programmation et tout bon codeur doit les maîtriser parfaitement.

Après avoir découvert l'univers des arrays, nous allons aborder les hash sur lesquels tu as déjà un peu travaillé lors de la semaine 0. Hier, on a créé des utilisateurs pour notre application et ce serait cool de pouvoir associer une adresse e-mail à un mot de passe, non ? Ça tombe bien les Hash c'est fait pour stocker ça. Mais pas que, on va voir tout ça avec le cours de Learn Ruby The Hard Way.

Note que l'utilisation de hash, plutôt que d'array, est conseillée en Ruby (même si cela dépend de ton usage exacte). En effet, un hash permet une organisation plus claire des données et est facile à parcourir avec .each do |key,value|. De plus, c'est une très bonne porte d’entrée sur JavaScript où les API avec lesquelles tu vas communiquer utilisent des hashs de données.

## 3. Ce que tu dois retenir

Un array est un tableau (sur une ligne) qu'on déclare ainsi cities = ["Paris", "Lyon", "Montpellier"].
Son index commence à zéro donc cities[0] = "Paris".
Tu peux facilement modifier son contenu : cities[1] = "Marseille" donnera : cities = ["Paris", "Marseille", "Montpellier"]


## 4. Pour aller plus loin