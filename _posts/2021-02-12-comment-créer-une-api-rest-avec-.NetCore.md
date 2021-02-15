---
layout: post
author: vanak
---

Tu veux profiter des vacances d'hiver pour faire un peu de ski, tu vas sur ton site favori de voyage LastMinute.com et tu fais une recherche de séjour disponible. 

Le site lance alors sa routine et va chercher le séjour qu'il te faut pour te relaxer des longues heures que tu passes devant ton écran. Curieux et codeur, tu te demandes ce qu'il est en train de mouliner...

![](https://miro.medium.com/max/1400/1*HX31jbHTQTqQT6tkWsTrfQ.png)

Il est en fait en train de se connecter à plusieurs serveurs pour trouver selon tes critères la bonne destination. Il va passer par des API proposées par les autres sites. 

Qu'est-ce une API ? Et bien c'est mon job aujourd'hui de te faire découvrir ce qu'est une API et comment en créer une avec .NET Core.

## 1. Historique et Contexte
### 1.1 Qu'est-ce qu'une API ?
API signifie Application Programming Interface. En gros, c'est un programme qui permet à deux ou plusieurs machines qui ne parlent pas le même langage de communiquer entre elles. 

Par exemple pour LastMinute.com, tu cliques sur le bouton rechercher. Le site va se connecter à plusieurs sites partenaires et leurs demander s'ils ont le voyage qui correspond à tes critères de recherche:

```
LastMinute.com : "Gros, tu as ça dans ta base de donnée ?"
AirFrance.com : "Non mec, je suis en PLS à cause du COVID"
Luftansa.de : "Nein mec, on n'accepte que les ressortissants allemands"
JeVoyageEnFrance.com : "Yes mec, tiens le voilà le super séjour"
LastMinute.com : "Cool, merci JeVoyageEnFrance.com"
```

Cette connexion va se faire via une `API` développée par le site partenaire pour accéder à certaines informations (ici savoir si ce voyage est dans leur base de donnée). 

Par exemple les API de la [Ratp](https://data.ratp.fr/explore/?sort=modified) te permettent de connaître les horaires en temps réels de ta ligne de métro ou de ton TER mais pas forcément qui travaillent à la Ratp parce que cette donnée n'est pas accessible via leur API.

Ces API ne sont pas forcément développées dans le même langage de programmation que le site demandeur mais respectent certaines règles notamment le modèle `REST`.

### 1.2 Qu'est-ce que REST ?
De ton côté, tu vas créer des API dites `REST`.

Le modèle REST est proposé en 2000 par __Roy Fielding__. REST signifie Representational State Transfert et est un style d'architecture logicielle. Le modèle REST repose sur une relation Client Serveur. 

Tu sais que le protocole `HTTP` (__HyperText Transfert Protocol__) te permet d'interagir avec internet. Et bien, la façon de communiquer avec les API est identique, tu vas utiliser 4 verbes du protocole HTTP
* La méthode `GET` pour afficher des ressources
* La méthode `POST` pour envoyer des informations à créer en ressource
* La méthode `PUT` pour modifier une information d'une ressource
* La méthode `DELETE` pour effacer une ressource

Avec cette API, tu vas pouvoir donner accès à toutes les ressources que tu décides de partager. 

Ainsi, si ton client a une application mobile, il pourra se connecter à tes données via le chemin que tu lui donnes, souvent une URL (tu verras ça plus bas). Un autre client a une application web et pourra également se connecter à ton API et interagir avec même si son application est développer en Javascript.

En réponse des requêtes sur tes API, tes clients vont recevoir un document soit au format XML (Extensible Markup Language) et plus souvent au format JSON (Javascript Object Notation).

### 1.3 Qu'est-ce que JSON ?
C'est un fichier pour structurer des données d'une façon lisible par un humain et également lisible par un ordinateur. 
Tu vas associer un couple clé-valeur dans un objet javascript : 
```js
  {
    "nom" : "Antoine",
    "prenom": "DesConnes",
    "email": "antoinedesconnes@pas.fr"
  }
```

Très bien, tu viens de finir ta partie de Question Pour Un Champion, tu vas passer au chose sérieuse.

## 2. La Ressource
### 2.1 La RESTAttitude avec .NET CORE
Bizarrement, le site LastMinute.com ne trouve pas ton séjour alors que les vacances commencent bientôt. Avec tes talents de codeur et principalement tes talents de scrappeur (en récupérant des données d'une façon moins orthodoxe), tu décides de créer tes propres ressources pour devenir un fournisseur de donnée. Pour ça, tu vas créer une API avec le surprenant __framework .NET CORE__ dans sa version 3.1. 

### 2.2 Créer un projet .NET CORE
Tu vas commencer par créer une nouvelle solution et un nouveau projet avec le framework .NET CORE. 

![](/assets/img/db/01.png)
![](/assets/img/db/02.png)
![](/assets/img/db/03.png)
![](/assets/img/db/04.png)

Maintenant que ton projet est créé, tu vas faire un peu de nettoyage dans ton explorateur de solution pour retirer les fichiers créés par défaut au lancement.

Supprimes le fichier `WeatherForecast.cs` à la racine du projet et dans le dossier Controllers, le fichier `WeatherForecastController`. 

![](/assets/img/db/05.png)

### 2.3 Importer les Packages NuGet 
Tu vas ensuite installer les librairies (Packages NuGet) que tu auras besoin pour faire tourner ton API : 
* EntityFrameworkCore en version 3.1.12 comme ORM (Object Relational Mapping) pour les relier les tables de ta base de données en classe C#.
* EntityFrameworkCore.SqlServer en version 3.1.12
* EntityFrameworkCore.Design en version 3.1.12

Pour ça, tu vas faire un clic droit sur le nom de ton projet puis cliquer sur `Gérer les packages NuGet`.

![](/assets/img/db/06.png)
![](/assets/img/db/07.png)
![](/assets/img/db/08.png)
![](/assets/img/db/09.png)

### 2.4 Créer un dossier Models
Partant du principe Code First, tu vas d'abord écrire tes classes C# dans un dossier `Models` puis les transposer en tables dans ta base de données.

Ajoutes à ton projet un dossier `Models` puis dedans ajoutes une classe `Voyage`.

Dans cette classe `Voyage`, tapes le code suivant entre les accolades de la méthode `public class Voyage` : 
```cs
  public int Id { get; set; }
  public string NomDuVoyage { get; set; }
  public string Lieu { get; set; }
  public string Pays { get; set; }
  public int Prix { get; set; }
```
![](/assets/img/db/10.png)

![](/assets/img/db/11.png)

Cette classe sera la table `Voyage` que tu retrouveras dans ta DB après.

### 2.5 Ajouter les classes Stagiaire, ApplicationDbContext
Tu crées ensuite une autre classe `ApplicationDbContext` dans ton dossier `Models`. Cette classe sera le conteneur qui va prendre la responsabilité de mapper les tables avec les classes C#.

Tapes le code suivant comme sur l'image en dessous :
```cs
  public class ApplicationsDbContext: DbContext
  {
    public ApplicationsDbContext(DbContextOptions<ApplicationsDbContext> options)
    : base(options)
    {

    }

    public DbSet<Voyage> Voyages { get; set; }
  }
```
![](/assets/img/db/12.png)
![](/assets/img/db/13.png)

La classe `ApplicationsDbContext` va coordonner les fonctionnalités de Entity Framework pour la classe `Voyage`. Ce conteneur va spécifier quelles classes seront inclus dans le modèle en BD. Ici, la propriété `DbSet<Voyage> Voyages` est un set d'entité qui deviendra la DB ayant comme table `Voyage`.

Avec `: base(options)`, tu renvois les options au constructeur de la classe `DbContext` qui seront passées en argument lors de l'exécution.

### 2.6 Modifier le fichier Startup.cs
Dans le fichier `Startup.cs`, tu vas ajouter le conteneur (`ApplicationsDbContext`) comme service dans la méthode `ConfigureServices` : 
```cs
  services.AddDbContext<ApplicationsDbContext>(options => 
          options.UseSqlServer(Configuration.GetConnectionString("APICotext")));
```
Là tu viens d'ajouter un service qui va être appelé à l'exécution de ton programme. En gros, tu dis à ton app d'utiliser les services de Sql Server avec les connexions qui se trouvent dans ton fichier `appsettings.json`.

![](/assets/img/db/14.png)


### 2.7 Modifier le fichier appsettings.json
Maintenant, tu vas modifier le fichier `appsettings.json` pour transmettre les informations concernant ta BD qui se trouve sur Sql Server. 

Ajoutes après la dernière ligne le code suivant : 
```json
  "ConnectionStings": {
    "APIContext": "Server=RemplaceIciParLeNomDuServeur;Database=UnNomDeDb;Trusted_Connection=True"
  }
```
![](/assets/img/db/15.png)
![](/assets/img/db/16.png)
![](/assets/img/db/17.png)


### 2.8 Lancer PM
Ensuite tu vas lancer la console du Gestionnaire de package pour créer les fichiers de migrations. Ces fichiers de migrations te permettront de créer une relation durable avec ta DB sur Sql Server.

![](/assets/img/db/18.png)

Commences par lancer un `Générer une solution` puis tester si tu as les outils nécessaires pour travailler. Dans la console, tapes le code suivant : 
```
  PM> dotnet ef
```
Si tu vois une licorne c'est que tu as les outils nécessaires, sinon tu dois taper ce code : 
```
 PM> dotnet tool install --global dotnet-ef
```
Si tu ne rencontres aucun autre soucis, retapes la première commande et si tu as bien la licorne continues.

Ensuite tu vas créer un dossier `Migrations` directement avec la console : 
```
 PM> dotnet ef migrations add PremierMigration --project NomDuProjet
```
Remplaces `NomDuProjet` par le nom de ton projet. 

Si tout se passe bien, tu devrais avoir un nouveau dossier `Migrations` qui a été créé.

![](/assets/img/db/19.png)


Si tu as une erreur `Use dotnet build`, fais `Générer la solution` et ça devrait passer. 

Pourquoi faire un `Générer la solution` ? Lorsque tu modifies des fichiers statics de ton projet comme tu l'as fait avec le fichier `appsettings.json`, tu dois lancer un `Générer` pour que ton projet le prend en compte.

Dernier code à taper sur la console : 
```
 PM> dotnet ef database update --project WebMyAPICore
```
Remplaces `WebMyAPICore` par le nom de ton projet. Si tout se passe comme prévu, tu vas avoir ta DB de créer sur Sql Server. 
Vas checker sur `SQL Server Management Studio`.

![](/assets/img/db/20.png)


### 2.9 Créer un controller
Encore 2 étapes et tu pourras tester ton API. 

Tu vas maintenant ajouter un controller. C'est lui qui va donner les URL d'accès pour interagir avec ton API.

Cliques droit sur le dossier `Controllers` puis ajouter puis `Nouvel élément généré automatiquement...`.

![](/assets/img/db/21.png)

Ensuite, dans les éléments communs, cliques sur `API` puis sélectionnes `Contrôleur d'API avec actions, utilisant EF` et ajouter.

![](/assets/img/db/22.png)


Puis choisis la classe de modèle `Voyage`, la classe de contexte de données `ApplicationsDbContext`, donnes un nom, souvent il est généré automatiquement puis ajouter.

![](/assets/img/db/23.png)


Voilà, tu viens de créer les accès à ton API.

Vas sur le fichier que ton projet vient de créer.

![](/assets/img/db/24.png)


Dans `VoyagesController`, son constructeur utilise l'injection de dépendance pour injecter le contexte de donnée. Avec l'injection de dépendance, tu fournis des services à travers le constructeur à tous les composants qui ont besoins. Le contexte sera alors utilisé dans toutes les méthodes REST de `VoyagesController`.

En parcourant ton controller, tu as tous les URLs d'accès aux méthodes. Par exemple pour afficher tous les voyages, l'URL sera `https://44386/api/voyages`. 

Comment tu peux le savoir ? 

Notes l'URL qui est devant le verbe `GET` : `api/Voyages`. Ceci est un `EndPoint`, le point d'accès. Tu trouveras l'`URL de base` dans le fichier `launchSettings.json`.

![](/assets/img/db/25.png)

### 2.10 Modifier le fichier launchSettings.json 
Dernière modification, remplaces la valeur des 2 clés `launchUrl` par le `EndPoint` que tu as noté.

![](/assets/img/db/26.png)

Fais un `Générer` puis lances `IIS Express`. 

Si tu n'as pas de page avec une erreur 4XX, c'est que ton API fonctionne. Bravo.

Pour teste en profondeur ton API, tu peux utiliser :
* Le logiciel Postman
* L'extension Chrome Advanced REST Client

## 3. Points importants à retenir

Ce que tu viens d'apprendre: 
* Qu'est ce qu'une API REST 
* Les étapes pas à pas pour créer une API Rest.

## 4. Pour aller plus loin
La documentation de [Microsoft](https://docs.microsoft.com/fr-fr/aspnet/core/tutorials/first-web-api?view=aspnetcore-5.0&tabs=visual-studio).
