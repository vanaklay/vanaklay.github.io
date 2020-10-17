---
layout: post
author: Vanak
---

Mais quel rapport entre la POO et Games of thrones, tu vas me dire ? En fait aucun... 😅 Je vais juste m'aider de GOT pour t'expliquer dans cet article la Programmation Orienté Objet, POO pour les intimes... 

![](https://www.mepixels.com/cache/55036954/game-of-thrones-14-1140x1140-zOXrLdxSl.jpeg)

## Un paradigme de programmation

Avant de commencer, la Programmation Orienté Objet est un [paradigme de programmation](https://fr.wikipedia.org/wiki/Paradigme_(programmation)). Je ne vais pas rentrer dans les détails ici mais sache que grosso modo c'est une façon de voir ton progamme. Une sorte de structure pour ton programme.

Pourquoi la POO est-elle importante dans Ruby ? 

Fondamentalement, quasiment tout est Objet en Ruby contrairement à d'autres langages de programmation.
Par exemple, lorsque tu appelles une méthode sur un `string` comme `str.length`, tu exécutes en fait une méthode de la `classe String`. Lorsque tu appelles une méthode sur un `array` comme `arr.join(" ")`, idem tu exécutes une méthode de la `classe Array`. 

Cela marche également pour les `numbers`, les `class`, les `modules` sauf pour les `methodes` et les `blocks`. 

La raison pour laquelle la POO est importante en Ruby est que quasiment tout est imbriqué dans des classes.

## Comment fonctionne une `classe` ?

Une `classe` est une description formelle de la façon dont un objet est conçu, c'est-à-dire des attributs et des méthodes dont il dispose. Tu peux voir ça comme un moule dont les objets sont produits à partir de ce moule.

![](https://www.cdiscount.com/pdt2/4/4/5/1/700x700/auc0659314876445/rw/24-savon-mini-muffin-silicone-cavity-biscuits-de-p.jpg)

Ok, je t'ai buzzé avec GOT et là je te montres des cupcakes... 

Avant de passer dans le vif du sujet, tu dois savoir qu'il existe une convention respecter :
* Tu dois utiliser le [CamelCase](https://fr.wikipedia.org/wiki/Camel_case) pour définir ta classe : `class MySuperGotCharacter`. N'oublies pas de clôturer ta classe avec `end` sinon tu risques d'avoir un message d'erreur.
* Tu dois utiliser un fichier `.rb` pour chaque classe que tu définis. 
  ```
  .
  |-- lib
        |-- my_super_got_character.rb
  ```
* A l'intérieur de tes classes, tu dois toujours écrire tes méthodes et variables en snake_case, `def fais_quelque_chose`.

### Définir une classe et créer des instances

Créons ensemble une classe `Personnage` qui sera donc un moule pour créer tes différents personnages préférés.

Cela se passe comme ça dans le fichier `my_super_got_character.rb` :
```ruby
  #./lib/my_super_got_character.rb
  class Personnage
  end
```
Bravo, tu viens de créer ta première classe ... rien de fou.

Maintenant que nous avons un moule pour créer des personnages, nous allons créer des objets provenant de ce moule. On appelle ça créer une `instance` de la classe `Personnage`.

Nous allons donner vie à Daenerys, honneur aux femmes et puis ... je ne vais pas te spoiler la série. 

Là où tu as besoin de créer une instance, nous allons faire appelle à une méthode `.new` qui par défaut provient des propriétés des [classes](https://ruby-doc.org/core-2.5.3/Class.html) en Ruby :
```ruby
  #./app.rb
  daenerys = Personnage.new
  puts daenerys
  --> <Personnage:0x00007ffdba196800>
```
Voilà on vient de donner vie à Daenerys, ce qui est matérialisé avec `<Personnage:0x00007ffdba196800>` qui nous dit que c'est une instance de la classe Personnage.

Faisons la même chose avec Jon Snow : 
```ruby
  #./app.rb
  jon = Personnage.new
  puts jon
  --> <Personnage:0x00007ffdbda34568>
```
Cool, nous avons créé 2 personnages Daenerys et Jon mais ils ne font rien de spécial et se ressemblent.
![](https://psycatgames.com/fr/magazine/party-games/star-wars/feature-image_hu5a56dfb1404b6a1913a8a4cd67019ba4_1927497_1600x900_fill_q75_box_center.jpg)
Ajoutons leurs quelques attributs pour rendre plus réel nos personnages. 

### Attributs d'une classe

Les attributs sont des variables qui définiront ces instances. C'est ce qu'on va appeler des `variables d'instance`.

Par exemple quand nous avons créé l'instance `daenerys`, on aimerait lui donner plus d'informations comme son prénom, son nom, sa couleur de cheveux, ses origines, quel statut social, où elle vit, son 06... ou bien si elle est encore vivante, parce qu'ils meurent beaucoup et vite dans GOT.

Bref... Pourquoi ? parce que pour le moment elle n'existe que sous la forme `<Personnage:0x00007ffdba196800>`. 

Revenons dans notre fichier `my_super_got_character.rb` et ajoutons ces variables à notre classe `Personnage`. Ces variables sont facilement identifiables dans le code, car elles ont un @ devant leur nom :
```ruby
  #./lib/my_super_got_character.rb
  class Personnage
    def initialize(name, last_name, position="Inconnu", is_alive=true)
      @name = name
      @last_name = last_name
      @position = position
      @is_alive = is_alive
    end
  end
```
La méthode `initialize` dans une classe est une méthode spéciale pour instancier un objet de cette classe avec des attributs.
Lorsque tu fais `daenerys = Personnage.new`, le `.new` fait référence à la méthode `initialize`. Par défaut, la méthode `initialize` est vide et ce que nous venons de faire est juste de la remplir avec des paramètres que nous aimerions donner à nos personnages. 

Rendons Daenerys plus réelle dans notre fichier `app.rb` :
```ruby
  #./app.rb
  daenerys = Personnage.new("Daenerys", "Targaryen", "Essos")
  puts daenerys
  --> <Personnage:0x00007ffdba196800>
```
Pour le moment rien ne semble avoir changé. En effet, nous avons bien créé un nouveau personnage `daenerys` mais comment fait-on pour accéder à ces attributs, aux variables de cette instance ?

Pour y accéder, rien de plus simple que de faire `instance_créé.variable` : 
```ruby
  #./app.rb
  daenerys = Personnage.new("Daenerys", "Targaryen", "Essos")
  puts daenerys
  --> <Personnage:0x00007ffdba196800>
  puts daenerys.name 
  --> NoMethodError (undefined method `name' for #<Personnage:0x00007ffdba196800 @name="Daenerys", @last_name="Targaryen">)
```
🤔 ??? !!! 
Undefined method ??? Et oui, lorsque tu fais `.name`, Ruby pense que tu appelles une méthode de l'élément avant le point. 

Pour résoudre ce conflit géopolitique, il faut rendre accessible ces variables d'instance depuis notre classe `Personnage` et pour cela tu as plusieurs possiblités: 
* `attr_reader` : Tu donnes accès seulement à la lecture de la variable d'instance. Par exemple, tu sais que le prénom et le nom de famille ne devrait pas trop changer hors mariage... et que c'est censé rester fixe. Nous ajoutons une ligne spéciale à notre classe suivi des variables d'instance que nous voulons rendre éligible à la lecture. `:name` et `:last_name` font références aux variables d'instance `@name` et `@last_name`.
  ```ruby
    #./lib/my_super_got_character.rb
    class Personnage
      # ---- #
      attr_reader :name, :last_name
      # ---- #
      def initialize(name, last_name, position="Inconnu", is_alive=true)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
      end
    end
  ```
* `attr_writer` : Tu donnes accès seulement à l'écriture de la variable d'instance.
  ```ruby
    #./lib/my_super_got_character.rb
    class Personnage
      # ---- #
      attr_writer :is_alive
      # ---- #
      def initialize(name, last_name, position="Inconnu", is_alive=true)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
      end
    end
  ```
* `attr_accessor` : Tu donnes les droits de lire et d'écrire sur la variable d'instance. Autant donner tous les droits à chacun de nos variables d'instance.
  ```ruby
    #./lib/my_super_got_character.rb
    class Personnage
      # ---- #
      attr_accessor :name, :last_name, :position, :is_alive
      # ---- #
      def initialize(name, last_name, position="Inconnu", is_alive=true)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
      end
    end
  ```

Voilà nous avons accès à la fois à la lecture et à l'écriture des variables d'instance.
```ruby
  #./app.rb
  daenerys = Personnage.new("Daenerys", "Targaryen", "Essos")
  puts daenerys
  --> <Personnage:0x00007ffdba196800>
  puts daenerys.name 
  --> Daenerys
  puts daenerys.position
  --> "Essos"
  daenerys.position = "Mereen"
  puts daenerys.position
  --> "Mereen"
  puts daenerys.is_alive
  --> true
  daenerys.is_alive = false
  puts daenerys.is_alive
  --> WHO KNOWS ? ✨
```

### Méthode d'instance d'une classe

Cool, nous avons donné vie à nos personnages. Maintenant, donnons leurs la possibilité de réaliser des actions. Dans une classe, ces actions sont matérialisées dans des `méthodes d'instance`. Ce seront toutes les actions que pourront faire nos personnages comme partir dans une autre ville, tuer un adversaire, monter sur un dragon etc...

Retour sur notre fichier `my_super_got_character.rb`, faisons quelque chose de simple, juste donner la capacité de marcher:
```ruby
    #./lib/my_super_got_character.rb
    class Personnage
      attr_accessor :name, :last_name, :position, :is_alive
      def initialize(name, last_name, position="Inconnu", is_alive=true)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
      end
      # ---- #
      def walk
        return "#{@name.capitalize} marche"
      end
      # ---- #
    end
  ```
  Voyons comment cela ressort dans notre fichier `app.rb`:
```ruby
  #./app.rb
  daenerys = Personnage.new("Daenerys", "Targaryen", "Essos")
  puts daenerys.walk
  --> Daenerys marche 🚶‍♀️
```
Cela marche plutôt bien... Ajoutons un paramètre à notre `méthode d'instance walk`.
```ruby
    #./lib/my_super_got_character.rb
    class Personnage
        (...code précédent)
      # ---- #
      def walk(to_town)
        return "#{@name.capitalize} marche vers #{to_town}"
      end
      # ---- #
    end
```
```ruby
  #./app.rb
  daenerys = Personnage.new("Daenerys", "Targaryen", "Essos")
  puts daenerys.walk("Meereen")
  --> Daenerys marche vers️ Meereen
```
Ok, c'est bien sympa tout ça mais dans GOT, il y a du sang ! 

![](https://media.tenor.com/images/8166c957c2b2b755f76407740b0cba06/tenor.gif)

Alors on va ajouter une autre action possible à nos personnages, le droit de tuer un adversaire ! 

```ruby
    #./lib/my_super_got_character.rb
    class Personnage
        (...code précédent)
      # ---- #
      def kill(people)
        return "#{@name.capitalize} tue #{people.capitalize}"
      end
      # ---- #
    end
```
Il me semble que la personne qui tue le plus de monde dans cette série c'est Jaime Lannister.
```ruby
  #./app.rb
  jaime = Personnage.new("Jaime", "Lannister", "Port-Royal")
  puts jaime.walk("Vivesaigues")
  --> Jaime marche vers️ Vivesaigues
  puts jaime.kill("les fils de Lord Karstark")
  --> Jaime tue Les fils de Lord Karstark
```

## Vous avez dit `self` ?

Aparté, vois-tu la différence entre `Personnage.new` et `jaime.kill` ?

A première vue, ce sont 2 méthodes de la classe `Personnage`. Et c'est exact sauf qu'elles ne s'utilisent pas de la même façon.

Nous avons avec `jaime.kill`, une méthode d'instance qui permet d'éxécuter une action sur l'instance créé. Et de l'autre côté nous avons `Personnage.new`, une méthode de classe qui permet d'éxécuter une méthode sur la classe globale, dans notre cas sur la classe `Personnage`.

### Méthode de classe et variable de classe

Une méthode de classe se définit un peu comme une méthode d'instance sauf qu'il faut lui rajouter `self.` devant son nom. Comme nous l'avons vu plus haut, cette méthode ne concerne que de manière global la classe en question. 

Une variable de classe se définit par un double `@@` devant le nom de ta variable et est toujours écrit juste après les droits sur les variables.
```ruby
    #./lib/my_super_got_character.rb
    class Personnage
      attr_accessor :name, :last_name, :position, :is_alive
      # -- Variable de classe -- #
      @@number_of_characters_created = 0
      # ----------------------- #
      def initialize(name, last_name, position="Inconnu", is_alive=true)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
        # -- On initialise le compteur -- #
        @@number_of_characters_created =  @@number_of_characters_created + 1
        # ------------------------------ #
      end
      
      # -- Méthode de classe -- #
      def self.count
        return "Le nombre de personnages créés est de : #{@@number_of_characters_created}"
      end
      # ---------------------- #
    end
```
La différence entre une variable de classe et une variable d'instance est que nous ne pouvons pas accéder aux variables de classes directement même si nous lui donnons les droits `attr_accessor`. Les variables de classe ne concerne que de manière global la classe en question. Pour avoir accès, nous sommes obligés de passer par une méthode de classe.
```ruby
  #./app.rb
  jaime = Personnage.new("Jaime", "Lannister", "Port-Royal")
  daenerys = Personnage.new("Daenerys", "Targaryen", "Essos")
  jon = Personnage.new("Jon", "Snow", "Le Mur")
  puts Personnage.count
  --> Le nombre de personnages créés est de : 3
  puts Personnage.number_of_characters_created
  --> NoMethodError (undefined method `number_of_characters_created' for Personnage:Class)
```

## Dons du ciel ou héritage génétique ? 
La grande intrigue de GOT est bien sûr la guerre de pouvoir entre les différentes familles pour le trône de Fer.
![](https://www.game-of-thrones.fr/wp-content/uploads/2019/03/cropped-game-of-thrones-saison-8-wallapaper-tous-les-personnages.jpg)

Du coup, il faut donner une appartenance de chacun de nos personnages à une famille distincte.

Pour cela, tu vas me dire, créons une classe par famille ! Exactement... sauf que si nous créons directement une classe pour chaque famille notre code ressemblera à ça :
```ruby
    #./lib/stark.rb
    class Stark
      attr_accessor :name, :last_name, :position, :is_alive
      @@number_of_characters_created = 0
      def initialize(name, last_name, position="Inconnu", is_alive=true)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
        @@number_of_characters_created =  @@number_of_characters_created + 1
      end
      def self.count
        return "Le nombre de personnages créés est de : #{@@number_of_characters_created}"
      end
    end
```
... plusieurs fois en fonction de chaque famille. Pas très DRY comme code sachant qu'on rajoutera des spécificités de chaque famille.

Et bien avec Ruby, tu as la notion d'héritage de classe parent. Quand une classe hérite de son parent, elle récupère toutes les propriétés de son parent, les attributs et les méthodes. Cela permet de créer 2 types d'objets différents, un membre de la famille Stark et un personnage lambda mais qui sont très proches parce qu' ils ont des caractéristiques communes.

Pour faire cela, retournons sur notre fichier `stark.rb` où nous devons faire appelle à notre fichier `my_super_got_character.rb` :
```ruby
    #./lib/stark.rb
    require_relative 'my_super_got_character'
    class Stark < my_super_got_character
      attr_accessor :wolf
      @@stark_member = 0
      def initialize(name, last_name, position="Winterfell", is_alive=true, wolf_name)
        @name = name
        @last_name = last_name
        @position = position
        @is_alive = is_alive
        @wolf = wolf_name
        @@stark_member = @@stark_member + 1
      end
    end
```
Avec la ligne `class Stark < my_super_got_character`, nous disons que la classe Stark hérite des propriétés de la classe my_super_got_character. 

J'ai rajouté les lignes `wolf` et `@@stark_member` dans notre méthode initialize et aussi ouvert les droits pour `wolf`.

Etant donné que la classe Stark hérite des propriétés de sa classe parente, je n'ai pas besoin d'ouvrir les droits pour les autres variables et je peux même simplifier encore plus l'écriture pour éviter les répétitions. Nous ajoutons le mot clé `super()` suivi entre parenthèses des variables héritées de la classe parente :
```ruby
    #./lib/stark.rb
    require_relative 'my_super_got_character'
    class Stark < my_super_got_character
      attr_accessor :wolf
      @@stark_member = 0
      def initialize(name, last_name, position="Winterfell", is_alive=true, wolf_name)
        @wolf = wolf_name
        @@stark_member = @@stark_member + 1
        # -- super héritage de la classe parente -- #
        super(name, last_name, position, is_alive)
        # ----------------------------------------- #
      end
    end
```
C'est plus propre non ? Et en pratique ?
```ruby
  #./app.rb
  ned = Stark.new("Ned", "Stark", wolf_name="unknow")
  robb = Stark.new("Robb", "Stark", wolf_name="Vent Gris")
  jon = Stark.new("Jon", "Snow", wolf_name="Loup Blanc")
  puts ned.name
  --> Ned
  puts robb.position
  --> Winterfell
  puts jon.wolf
  --> Loup Blanc
```

## Soirée privée !
Fin de la saison 3, le mariage d'Edmure Tully aux Jumeaux. 
![](https://vignette.wikia.nocookie.net/game-of-thrones-le-trone-de-fer/images/c/c0/Banni%C3%A8re_Stark_en_train_de_br%C3%BBler.png/revision/latest/scale-to-width-down/1000?cb=20150211112028&path-prefix=fr)

Je ne sais pas pour toi mais j'aimerai bien savoir qui était de mèche ou pas, et pour ça on va créer une méthode dans la classe Personnage qui va analyser si ce personnage créé est un traître ou non. Bien entendu, ce complot était discrètement organisé dans le dos des Stark. 
Les voyous ne voulaient pas que cette méthode se sache. 

Et bien dans une classe, tu peux exactement écrire ce genre de méthode, une méthode privée qui ne sort pas de la classe elle-même et une méthode publique qui peut être appelée depuis l'extérieur. 

### Méthode privée
Pour définir une méthode privée, rien de plus simple que d'ajouter toutes tes méthode sous le mot clé `private` et hop elle n'est accessible que dans la classe. Vive les complots !

Evidemment toutes les méthodes au dessus du mot clé `private` sont des méthodes publiques...
```ruby
    #./lib/my_super_got_character.rb
    class Personnage
      (code précédent)
      # -- Méthode publique -- #
      def may_i_have_your_attention_please
      end
      # ------------------- #

      private
      # -- Méthode privée -- #
      def check_if_traitor
        # tu codes ici ce que fait ta méthode
      end
      # ------------------- #
    end
```
```ruby
  #./app.rb
  roose_bolton = Personnage.new("Roose", "Bolton", "Fort-Terreur")
  robb = Personnage.new("Robb", "Stark", "Winterfell")
  puts roose_bolton.check_if_traitor
  --> NoMethodError (private method `check_if_traitor' called for #<P:0x00007ffdbda5ca68>)
```

Voilà comment Games Of Thrones m'a réconcilié avec la programmation orientée objet ! 

Je te remercie d'avoir eu le courage d'aller jusqu'au bout de cette article. 🙏

J'espère que ça t'aidera à avoir une meilleure compréhension de la POO et que tu vas l'utiliser à mort dans tes projets à base de Ruby.

## Spécials remerciements 
* [Fandom](https://gameofthrones.fandom.com/fr/wiki/Wiki_Game_of_Thrones) pour les images que j'ai utilisés pour cette article.
* [THP](https://www.thehackingproject.org/) pour m'avoir ouvert les yeux sur le monde fantastique de Ruby.
* [Vivadata](https://vivadata.org/) pour l'inspiration de cette article, la découverte du monde du code, Python et le machine learning.




