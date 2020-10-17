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
Par exemple, lorsque tu appelles une méthode sur un `string` comme `str.length`, tu exécutes en fait une méthode de la `class String`. Lorsque tu appelles une méthode sur un `array` comme `arr.join(" ")`, idem tu exécutes une méthode de la `class Array`. 

Cela marche également pour les `numbers`, les `class`, les `modules` sauf pour les `methodes` et les `blocks`. 

La raison pour laquelle la POO est importante en Ruby est que quasiment tout est imbriqué dans des `class`.

## Comment fonctionne une `class` ?

Une `class` est une description formelle de la façon dont un objet est conçu, c'est-à-dire des attributs et des méthodes dont il dispose. Tu peux voir ça comme un moule dont les objets sont produits à partir de ce moule.

![](https://www.cdiscount.com/pdt2/4/4/5/1/700x700/auc0659314876445/rw/24-savon-mini-muffin-silicone-cavity-biscuits-de-p.jpg)

Ok, je t'ai buzzé avec GOT et là je te montres des cupcakes... 

Avant de passer dans le vif du sujet, tu dois savoir qu'il existe une convention respecter :
* Tu dois utiliser le [CamelCase](https://fr.wikipedia.org/wiki/Camel_case) pour définir ta class : `class MySuperGotCharacter`. N'oublies pas de clôturer ta class avec `end` sinon tu risques d'avoir un message d'erreur.
* Tu dois utiliser un fichier `.rb` pour chaque class que tu définis. 
  ```
  .
  |-- lib
        |-- my_super_got_character.rb
  ```
* A l'intérieur de tes classes, tu dois toujours écrire tes méthodes et variables en snake_case, `def fais_quelque_chose`.

### Définir une `class` et créer des instances

Créons ensemble une class `Personnage` qui sera donc un moule pour créer tes différents personnages préférés.

Cela se passe comme ça dans le fichier `my_super_got_character.rb` :
```ruby
  #./lib/my_super_got_character.rb
  class Personnage
  end
```
Bravo, tu viens de créer ta première `class` ... rien de fou.

Maintenant que nous avons un moule pour créer des personnages, nous allons créer des objets provenant de ce moule. On appelle ça créer une `instance` de la class `Personnage`.

Nous allons donner vie à Daenerys, honneur aux femmes et puis ... je ne vais pas te spoiler la série. 

Là où tu as besoin de créer une instance, nous allons faire appelle à une méthode `.new` qui par défaut provient des propriétés des [class](https://ruby-doc.org/core-2.5.3/Class.html) en Ruby :
```ruby
  #./app.rb
  daenerys = Personnage.new
  puts daenerys
  --> <Personnage:0x00007ffdba196800>
```
Voilà on vient de donner vie à Daenerys, ce qui est matérialisé avec `<Personnage:0x00007ffdba196800>` qui nous dit que c'est une instance de la class Personnage.

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

### Attributs d'une `class`

Les attributs sont des variables qui définiront ces instances. C'est ce qu'on va appeler des `variables d'instance`.

Par exemple quand nous avons créé l'instance `daenerys`, on aimerait lui donner plus d'informations comme son prénom, son nom, sa couleur de cheveux, ses origines, quel statut social, où elle vit, son 06... ou bien si elle est encore vivante, parce qu'ils meurent beaucoup et vite dans GOT.

Bref... Pourquoi ? parce que pour le moment elle n'existe que sous la forme `<Personnage:0x00007ffdba196800>`. 

Revenons dans notre fichier `my_super_got_character.rb` et ajoutons ces variables à notre class `Personnage`. Ces variables sont facilement identifiables dans le code, car elles ont un @ devant leur nom :
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
La méthode `initialize` dans une class est une méthode spéciale pour instancier un objet de cette class avec des attributs.
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

Pour résoudre ce conflit géopolitique, il faut rendre accessible ces variables d'instance depuis notre `class Personnage` et pour cela tu as plusieurs possiblités: 
* `attr_reader` : Tu donnes accès seulement à la lecture de la variable d'instance. Par exemple, tu sais que le prénom et le nom de famille ne devrait pas trop changer hors mariage... et que c'est censé rester fixe. Nous ajoutons une ligne spéciale à notre class suivi des variables d'instance que nous voulons rendre éligible à la lecture. `:name` et `:last_name` font références aux variables d'instance `@name` et `@last_name`.
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
* `attr_accessor` : Tu donnes le droit de lire et d'écrire sur la variable d'instance. Autant donner tous les droits à chacun de nos variables d'instance.
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

### Méthodes d'une `class`

### Vous avez dit `self` ?

Apparté, vois-tu la différence entre `Personnage.new` et `daenerys.name` ?


