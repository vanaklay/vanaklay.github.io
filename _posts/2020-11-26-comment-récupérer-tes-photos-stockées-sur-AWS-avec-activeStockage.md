---
layout: post
author: Vanak
---

## 1. Introduction
Active Storage est une fonctionnalité sympathique de Rails qui permet à un utilisateur de votre app de mettre en ligne des fichiers qui pourront ensuite être utilisés dans son site web. L'exemple typique est le fait d'envoyer une photo de profil : celle-ci est alors stockée dans le cloud et l'app Rails peut l'appeler à tout moment afin de l'afficher où bon vous semble. Il est bien évidemment possible de l'utiliser pour d'autres fichiers comme des pdf ou autres.

## 2. Historique et contexte
ActiveStorage est une nouveauté assez récente dans Rails car introduite dans la version 5.2. Avant ça, il fallait forcément passer par des applications tierces pour effectuer de l'upload (Paperclip, Shrine ou CarrierWave pour ne citer qu'elles). À présent, on gère cela en natif ! Ce qui est cool pour une fonctionnalité, somme toute très courante dans les app web modernes.

## 3. La ressource
### 3.1. Les concepts de base d'Active Storage

Active Storage permet facilement à tes utilisateurs d'uploader des fichiers et de lier ces fichiers à des objets de ta BDD. En environnement de développement, Active Storage permet une sauvegarde en local afin d'effectuer des tests. En production, il faudra le configurer afin que les fichiers soient stockés dans des services comme Amazon S3, Google Cloud, ou Microsoft Azure (Malheureusement, ils sont tous payants).

Au niveau de l'app Rails, Active Storage fonctionne grâce à l'existence de 2 tables dans ta BDD : `active_storage_blobs` et `active_storage_attachments`. Nous allons voir comment mettre tout ça en route.

### 3.2. Mettre en place Active Storage
Allez, on va pratiquer en mettant sur pied un premier Active Storage ensemble.

#### 3.2.1. Les bases pour bosser

Commence par préparer tout ce qu'il faut pour disposer d'une application de test :

* Génère une application Rails test_active_storage et va dans son dossier ;
* Crée-lui un model User (sans aucun champ additionnel) ;
* Crée un users_controller avec un show en faisant $ rails g controller users show ;
* A présent, crée ta BDD (si tu es en PostGre) et passe la migration.
  
#### 3.2.2. Installation d'Active Storage
Pour installer Active Storage sur ton app, lance $ rails active_storage:install. Cette commande a pour effet de générer une migration permettant de créer 2 tables dans ta BDD :

* `active_storage_blobs` : qui contient toutes les métadonnées des fichiers uploadés (taille, nom, type, etc.).
* `active_storage_attachments` : une table jointe entre tes modèles et les uploads.
Par curiosité, va dans ton dossier `/db/migrate/` pour jeter un œil à la migration : ça te permet de voir les champs qui vont constituer ces 2 tables.

Maintenant passe la migration.