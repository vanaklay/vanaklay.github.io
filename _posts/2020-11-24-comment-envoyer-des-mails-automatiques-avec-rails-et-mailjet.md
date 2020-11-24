---
layout: post
author: Vanak
---

## 1. Introduction
Rails dispose d'un outil de gestion des envois d'e-mail plutôt bien conçu : Action Mailer. Grâce à lui, tu vas pouvoir automatiser l'envoi de certains e-mails selon les critères que tu définiras (actions de tes utilisateurs, événements ou alertes données, etc..). Nous allons donc t'apprendre à paramétrer Action Mailer et à l'utiliser de façon automatisée.

## 2. Historique et contexte
Les e-mails font, de nos jours, partie intégrante de l'expérience utilisateur d'un site web moderne. Sans eux, impossible de garder le contact avec tes utilisateurs, leur faire changer de mot de passe ou encore les prévenir d'un évènement important lié à leurs comptes (nouveau commentaire ? nouveau message ?). Maintenant que tu sais poser les bases d'une application Rails complète (routes, models, views et controllers), on va lui ajouter les fonctionnalités additionnelles qui en feront un service fonctionnel et professionnel.

## 3. La ressource
### 3.1. Les concepts de base de l'Action Mailer
L'Action Mailer est organisé en plusieurs éléments au sein d'une app Rails :

1. Des mailers, qui sont ni plus ni moins que des sortes de controllers appliqués aux e-mails. Tout comme les controllers "normaux", ils contiennent des méthodes qui vont faire des appels à la BDD (via les models) et ensuite envoyer des e-mails (au lieu d'envoyer des pages web à des navigateurs).

2. Des views, qui sont des sortes de templates des e-mails à envoyer. Tout comme les views de ton site, elles sont personnalisées grâce à du code Ruby inclus dedans (pour rajouter un nom, un e-mail, le contenu d'un objet récupéré en BDD, etc.). Il existe deux types de views : les .text.erb et les .html.erb car on peut envoyer des e-mails au format HTML comme au format text.

Au final, il faut considérer qu'Action Mailer a un fonctionnement très proche du MVC classique de Rails sauf qu'au lieu d'afficher des pages HTML sur un navigateur, il envoie des fichiers HTML ou text par e-mail.

### 3.2. Mettre en place ton premier Action Mailer
Afin d'apprendre à te servir de ce service, on te propose de pratiquer directement.

#### 3.2.1. Les bases pour bosser
Commence par préparer tout ce qu'il faut pour disposer d'une application de test:
   * Génère une application Rails test_action_mailer ;
  ```sh
    $ rails new -d prostgresql test_action_mailer 
  ```
   * Crée-lui un model User avec des champs name (string) et email (string) ;
  ```sh
    $ rails generate model User name:string email:string
  ```
  N'oublies pas que pour créer un model suivant les conventions d'écritures `Rails`, on utilise le Camelcase singulier.
   * Crée une BDD (si tu es en PostGre) et passe la migration.
  ```sh
    $ rails db:create db:migrate
  ```
  En une ligne, tu crées ta base de donnée PostgreSql et tu fais la migration.

#### 3.2.2. Ton premier mailer
À présent, on va générer un mailer avec `$ rails g mailer UserMailer`. On l'a appelé UserMailer dans l'idée qu'à terme, il pourrait gérer tous les e-mails à destination des utilisateurs. On pourrait aussi avoir un `AdminMailer` qui enverrait les e-mails aux gestionnaires du site.

Maintenant, jette un œil au mailer que tu viens de générer dans `app/mailers/user_mailer.rb` : il est vide mais hérite de ApplicationMailer que tu pourras retrouver à `app/mailers/application_mailer.rb`.

On va éditer le mailer pour rajouter une méthode dont le rôle sera simple : envoyer un e-mail de bienvenue à tous les utilisateurs s'inscrivant sur notre site. Rajoute donc les lignes suivantes :
  ```ruby
  default from: 'no-reply@monsite.fr'
 
  def welcome_email(user)
    #on récupère l'instance user pour ensuite pouvoir la passer à la view en @user
    @user = user 

    #on définit une variable @url qu'on utilisera dans la view d’e-mail
    @url  = 'http://monsite.fr/login' 

    # c'est cet appel à mail() qui permet d'envoyer l’e-mail en définissant destinataire et sujet.
    mail(to: @user.email, subject: 'Bienvenue chez nous !') 
  end
  ```

  La première ligne permet de définir la valeur de `default[:from]`. Le hash `default` permet de définir tout un ensemble de valeurs par défaut : celles-ci sont écrasées si la méthode d'envoi d’e-mail définit une valeur autre. Ici, l'objectif est que nos e-mails affichent toujours une adresse d’e-mail d'envoi : soit celle définie par la méthode du mailer, soit, à défaut, `no-reply@monsite.fr`.

#### 3.2.3. Ta première mailer view
On va créer le template de notre e-mail de bienvenue.
Pour ça, crée un fichier `welcome_email.html.erb` dans `app/views/user_mailer/`. Bien évidemment le nom est extrêmement important : il doit être identique à celui de la méthode `welcome_email` et placé dans le dossier `views/user_mailer/` qui contient tous les templates e-mails relatifs au mailer UserMailer. Le contenu du template sera le suivant :

```ruby
<!DOCTYPE html>
<html>
  <head>
    <meta content='text/html; charset=UTF-8' http-equiv='Content-Type' />
  </head>
  <body>
    <h1>Salut <%= @user.name %> et bienvenue chez nous !</h1>
    <p>
      Tu t'es inscrit sur monsite.fr en utilisant l'e-mail suivant : <%= @user.email %>.
    </p>
    <p>
      Pour accéder à ton espace client, connecte-toi via : <%= @url %>.
    </p>
    <p> À très vite sur monsite.fr !
  </body>
</html>
```

On va aussi prévoir une version texte pour les utilisateurs qui n'aiment pas les e-mails en HTML. C'est toujours mieux de prévoir les deux ! Pour cela, crée également un fichier `welcome_email.text.erb` dans `app/views/user_mailer/` et son contenu sera le suivant :

```ruby
Salut <%= @user.name %> et bienvenue chez nous !
==========================================================
 
Tu t'es inscrit sur monsite.fr en utilisant l'e-mail suivant : <%= @user.email %>.
 
Pour accéder à ton espace client, connecte-toi via : <%= @url %>.
 
À très vite sur monsite.fr !
```

#### 3.2.4. Définir l'envoi automatique
Tout est prêt côté Action Mailer : il ne reste plus qu'à définir à quel moment notre app Rails doit effectuer l'envoi. Pour ceci, voici quelques exemples de cas :

* Si tu veux envoyer un email à la création d'un utilisateur, c'est un callback `after_create` dans le model `User`
* Si tu veux envoyer un email quand un utilisateur vient de prendre un RDV sur Doctolib, c'est un callback `after_create` à la création d'un Appointment
* Si tu veux envoyer une newsletter hebdomadaire, c'est un Service qui tourne de manière hebdomadaire (on verra comment faire des services cette semaine 😉)
* Un email pour réinitialiser le mot de passe peut se mettre dans le controller

Dans notre cas, on veut envoyer un e-mail juste après la création d'un utilisateur : il serait logique que ce travail revienne au model car 1) c'est lui qui crée l'utilisateur donc autant qu'il fasse les 2 actions et 2) Fat model Skinny controller, duuuuuude !

Du coup, va dans ton model User et rajoute la ligne suivante :
```ruby
class User < ApplicationRecord
  after_create :welcome_send

  def welcome_send
    UserMailer.welcome_email(self).deliver_now
  end

end
```

On a utilisé un callback qui permet juste après l'inscription en base d'un nouvel utilisateur, d'appeler la méthode d'instance `welcome_send`. Celle-ci ne fait qu'appeler le mailer `UserMailer` en lui faisant exécuter `welcome_email` avec, pour seule entrée, l'instance créée (d'où le `self`).

À noter qu'on rajoute ensuite un `deliver_now` pour envoyer immédiatement l’e-mail. Il est possible d'utiliser un `deliver_later` mais son fonctionnement en production est moins évident : il faut savoir gérer les tâches asynchrones avec `Active Job`… On ne va pas rentrer là-dedans pour le moment.

En résumé, nous venons de paramétrer la chaîne d'actions suivante :
1. Un utilisateur est créé en BDD par le model
2. Grâce au callback `after_create`, on exécute la méthode `welcome_send` sur l'instance qui vient d'être sauvée en BDD
3. `welcome_send` dit, en résumé, "exécute NOW la méthode `welcome_email` située dans le mailer `UserMailer`"
4. `welcome_email` va appeler 2 templates en leur mettant à disposition une instance `@user` qui est l'utilisateur créé et une variable `@url` qui est juste un string. Cette méthode enverra ensuite les 2 templates à `@user.email` avec comme sujet "Bienvenue chez nous".
5. Les 2 templates (un HTML et un text) sont personnalisés avec les entrées en Ruby (`@user.name`, `@user.email` et `@url`) avant d'être balancés par e-mail.

Pourtant, si tu fais le test en créant en console un utilisateur, à part le template e-mail qui s'affiche dans le terminal, tu ne verras rien de très concret. En effet, Rails n'est pas en mesure d'envoyer comme ça des e-mails sans disposer d'un serveur SMTP configuré ! C'est notre prochaine étape.

### 3.3. Configurer les paramètres d'Action Mailer
Tu sais maintenant comment mettre en place un Action Mailer de base : il est temps de le paramétrer pour qu'il puisse envoyer des e-mails pour de vrai. Dans Rails, on peut définir les paramètres selon l'environnement dans lequel notre application tourne :
* Si elle tourne en `environnement de développement` (c'est le mode par défaut quand tu lances le serveur sur ton ordi), tu veux pouvoir tester l'affichage de l’e-mail mais éviter de spammer les utilisateurs avec tes tests.
* Si elle tourne en `environnement de production` (c'est le mode par défaut sur Heroku. Tu peux aussi le lancer depuis ton ordi), là tu veux que les e-mails soient envoyés pour de vrai.

#### 3.3.1. La config en développement
Ici le cahier des charges serait le suivant : on veut pouvoir
* vérifier que notre app Rails déclenche bien des envois d’e-mails (=> ça confirmerait que la chaîne entière d’Action Mailer est bien codée et sans bug) ;
* vérifier la tronche des e-mails qu'on envoie ;
* ne surtout pas envoyer des e-mails par erreur, histoire de ne pas prendre le risque de spammer de vrais clients pendant nos tests.

Pour ça on va utiliser une gem assez cool qui s'appelle `Letter Opener`. Son fonctionnement ? Dès qu'un e-mail doit être envoyé par ton app Rails, celui-ci est automatiquement ouvert dans ton navigateur web.

Testons-la immédiatement sur ton app `test_action_mailer` :
* Mets la gem `letter_opener` dans le groupe de développement de ton Gemfile
```ruby
group :development do
  # Dans ce groupe la
  gem 'letter_opener'
end
```
puis 
```sh 
$ bundle install 
```
* Maintenant va dans `config/environments/development.rb` (fichier contenant les paramètres de ton environnement de développement) et colle les lignes `config.action_mailer.delivery_method = :letter_opener` et `config.action_mailer.perform_deliveries = true`
```ruby
Rails.application.configure do
  # Les autres config.
  # J'ai mis ici pour grouper les config.action_mailer
  config.action_mailer.perform_caching = false

  config.action_mailer.delivery_method = :letter_opener
  
  config.action_mailer.perform_deliveries = true
  # Les autres config.
end
```
La ligne avec `perform_deliveries = true` permet d'éteindre (en la passant à false) tout envoi d'email de la part de ton app Rails. C'est bon de savoir qu'elle existe !

Maintenant que la gem est installée et configurée, va dans la console Rails et créé un utilisateur à la volée (par exemple : `User.create(name:"Féfé", email: "féfé@yopmail.com"))`. Tu devrais voir un visuel de l’e-mail que tu as rédigé en HTML s'afficher dans ton navigateur ! Si ce n'est pas le cas, tu as raté une étape de mon pas à pas…

#### 3.3.2. La config en production
##### a) Choisir un service d'envoi
Ici, le cahier des charges est simple : on veut pouvoir envoyer des vrais e-mails. C'est tout.

Pour le faire, tu as le choix entre plein de services différents : Mandrill by MailChimp, Postmark, Amazon SES, etc. Nous, on a une préférence pour [MailJet](https://fr.mailjet.com/) à THP (ils sont efficaces, pas chers et français 🇫🇷 🐓).

Commence par créer un compte chez [eux](https://fr.mailjet.com/). Présentes toi brièvement, pas la peine d'enregistrer des coordonnées bancaires, valides ta commande et confirmes l'inscription. 

Une fois ton compte validé, tu vas choisir le rôle `Développeur`.

Puis choisis l'option `Relais SMTP` comme méthode d'envoie. Je t'explique tout ça plus bas pourquoi.

##### b) Sauver la clef d'API de façon sécurisée
A partir de là tu vas avoir des informations essentielles. MailJet va te crée une clé Api qu'on va devoir mettre en sécurité dans ton app. Pour ça, rien de mieux que la gem `dotenv` appliquée à Rails.

Voici les étapes :
1. Ajoute gem `dotenv-rails` à ton Gemfile et fait le `$ bundle install`
2. Crée un fichier `.env` à la racine de ton application.
3. Ouvre-le et écris dedans les informations suivantes : `MAILJET_LOGIN='apikey'` et `MAILJET_PWD='ta_clef_API'` en remplaçant bien sûr ta_clef_API par la clef que tu viens de générer. N'oublie pas les guillemets !
4. Et l'étape cruciale qu'on oublie trop souvent : ouvre le fichier `.gitignore` à la racine de ton app Rails et écris `.env` dedans.

##### c) Paramétrer le SMTP avec les infos de MailJet
Parfait : tu as une clef API de MailJet et tu es prêt à l'utiliser. Il ne te reste qu'à entrer les configurations SMTP de MailJet dans ton app. Va dans `/config/environment.rb` et rajoute les lignes suivantes :
```ruby
ActionMailer::Base.smtp_settings = {
  :user_name => ENV['MAILJET_LOGIN'],
  :password => ENV['MAILJET_PWD'],
  :domain => 'monsite.fr', # information à récupérer dans Adresses d'envoi
  :address => 'in-v3.mailjet.com', # Serveur SMTP
  :port => 587,
  :authentication => :plain,
  :enable_starttls_auto => true
}
```

##### d) Passer les clefs d'API à Heroku
Maintenant que tes clefs d'API sont bien au chaud dans ton .env, il faut trouver un moyen pour qu'`Heroku` les ait. Sans elles, ton app Rails déployée chez eux n'a aucune chance de pouvoir accéder au service MailJet !

Pour que ça marche, tu vas devoir passer des commandes:
```sh
$ heroku config:set MAILJET_LOGIN='ta_clé_api'
$ heroku config:set MAILJET_PWD='ta_clé_api'
```
Cela va créer l'équivalent du contenu du fichier `.env` sur ton `Heroku`. Comme le fichier `.env` est inscrit dans ton fichier `.gitignore`, ce fichier n'est pas `pusher` sur Heroku. Donc Heroku n'a pas ta clé Api MailJet pour pouvoir faire le boulot.

##### e) Tester l'envoi
Tout est prêt à présent ! Si ton site web est déployé en production sur Heroku, Heroku a les clefs pour parler à MailJet : tu peux donc faire un test en créant un nouvel utilisateur.
Mais dans un premier temps, tu peux faire plus simple en testant une fois l'envoi directement depuis l'environnement de développement (ton ordi).

1. Enlève la ligne `config.action_mailer.delivery_method = :letter_opener` du fichier `config/environments/development.rb`
2. Va sur ton compte MailJet, dans `Adresses d'envoi` puis dans la section `Adresses` pour récupérer les informations suivantes : `domaine` et `adresse email`
3. Dans `app/mailers/user_mailer.rb`, modifies `default from: 'no-reply@monsite.fr'` avec l'adresse email récupérée et dans `/config/environment.rb`, modifies `:domain => 'monsite.fr'` avec le domaine
4. Va dans ta console Rails
5. Créé un utilisateur avec une adresse en @yopmail.com
6. Va vérifier que l’e-mail est bien arrivé sur [http://www.yopmail.com/](http://www.yopmail.com/)





