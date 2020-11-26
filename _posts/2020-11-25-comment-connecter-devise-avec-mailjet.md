---
layout: post
author: Vanak
---

## 1. Rappel
Devise permet de créer un système d'authentification complet en générant pour toi :

* L'inscription, avec mot de passe et e-mail sécurisé ;
* La notion de login, logout, session, current user ;
* La récupération de mot de passe par e-mail ;
* La confirmation de compte par e-mail ;
* Le comptage de login ;
* Le logout après un certain temps d'inactivité ;
* Le blocage de compte après un certain nombre de tentative de login ratées.

## 2. La ressource
### 2.1. Les fonctionnalités de Devise
Chaque fonctionnalités de Devise est inclus dans un module qu'on peut activer ou non :

Database Authenticatable : possibilité de stocker les mots de passe dans leur version hashée pour valider l'authenticité d'un utilisateur pendant sa connexion (la base quoi) ;
* Registerable : possibilité de créer un compte via un formulaire. Aussi, possibilité d'éditer et de supprimer son compte ;
* Recoverable : possibilité de réinitialiser le mot de passe et d'envoyer des instructions par e-mail ;
* Rememberable : possibilité d'utiliser le fameux cookie remember me (la session reste ouverte) ;
* Validatable : possibilité de donner des validations pour les e-mails et mots de passe (taille, regex, etc) ;
* Omniauthable : possibilité de gestion de OmniAuth (un service pour se connecter via son compte Google, Facebook ou autre) ;
* Confirmable : possibilité de forcer la confirmation par e-mail du compte ;
* Trackable : possibilité de tracker le nombre de login, leurs timestamps, et les adresses IP ;
* Timeoutable : possibilité d'expirer des sessions après un certain temps d'inactivité ;
* Lockable : possibilité de verrouiller un compte après trop de tentatives échouées de connexions ;
Nous allons voir dans cette ressource les plus importantes : Database Authenticatable, Registerable, Recoverable, Rememberable, Validatable.

### 2.2. Présentation de Devise
Nous allons faire un petit pas à pas pour que tu puisses voir les éléments importants de Devise. Prêt ? En avant : commence par créer une app bidon rails. Ensuite, fais chaque opération en même temps que je la décris.

#### 2.2.1. Installation
Normalement tu as déjà installé `devise` et on est prêt à démarrer.

Pour rappel, après avoir générer ton `devise:install`, 2 nouveaux fichiers se sont crées dans ton app : 
* `config/initializers/devise.rb` : le fichier de configuration de Devise. On s'en servira par exemple pour paramétrer le service que l'on va utiliser pour les envois d'e-mails ;
* `config/locales/devise.en.yml` : un fichier contenant les messages d'erreur de Devise. Tu pourras utiliser ses version françaises quand tu seras plus à l'aise avec la gem.

Après avoir créé les fichiers, le terminal va t'afficher un message avec 4 actions indispensables à mener. La plus importante est la première : il faut que tu paramètres bien Action Mailer afin que Devise puisse passer par lui pour envoyer des emails (notamment pour réinitialiser un mot de passe). Hier nous avons vu comment faire les branchements ActionMailer en local et sur Heroku : assure-toi toujours qu'il y a au moins l'information suivante dans le fichier `config/environments/production.rb` :

```ruby
config.action_mailer.perform_deliveries = true
config.action_mailer.default_url_options = { :host => 'online-shop-thp-staging.herokuapp.com' }
```

Et dans `config/environment.rb` :
```ruby
ActionMailer::Base.smtp_settings = {
  :user_name => ENV['MAILJET_LOGIN'],
  :password => ENV['MAILJET_PWD'],
  :domain => 'gmail.com', # information à récupérer dans Adresses d'envoi
  :address => 'in-v3.mailjet.com', # Serveur SMTP
  :port => 587,
  :authentication => :plain,
  :enable_starttls_auto => true
}
```


