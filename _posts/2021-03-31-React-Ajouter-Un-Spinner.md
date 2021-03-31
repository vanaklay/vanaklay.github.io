---
layout: post
author: vanak
---

Comme tu as des données sur FireStore, tu n'as plus besoin des données en dur que tu as écrit au préalable de la conception de l'app.
Pour ça, tu vas dans `item.reducer` et dans `INITIAL_STATE`, tu ajoutes `null` à la clé de ton item : `itemsList`.

Maintenant au `mounting` de la page où tu charges tes données, les données vont arriver de façon asynchrome sauf que tu appliques des méthodes sur les données qui étaient en dur. 

Tu vas avoir un problème de `TypeError: Cannot read property 'map' of null`. Et oui, tu ne peux pas faire un `.map` sur quelques choses qui est `null`. Ici, tu viens d'ajouter `null` à `itemsList`. 

Pour réparer cette erreur, tu vas ajouter un spinner qui va faire patienter l'utilisateur de ton app pendant que la page réalise sa tâche asynchrone.

Et en même voir l'utilisation en live d'un `terneray operator`.

## 1. La ressource
### 1.1 Modification dans le fichier selector

Avant d'ajouter le spinner, tu vas modifier un peu le code dans le fichier `item.selectors` : 
* Dans la `const selectItemsList`, dans le deuxième paramètre de la méthode `createSelector`, tu modifies la méthode par celle ci :
```js
  item => item.itemsList ? item.itemsList : null
```

Ce que tu viens de faire c'est qu'au lieu de retourner directement la liste des données `itemList`, qui rappelles toi est initialisée à `null`, tu fais un test sous forme `ternary operator`. C'est un peu comme un `if else statement` sauf qu'il s'écrit sur une ligne.

Tu fais le test suivant : 
* si `item.itemsList` est vrai (rappelles toi aussi que `null` est égal à `false`) : `item.itemsList ? `. Un peu comme si tu poses une question
* Si c'est vrai tu fais l'expression qui vient après le point d'intérogation (?) ` item.itemsList`
* Sinon tu fais l'expression qui est après les deux points (:) ` null`, ici retournes `null`

Maintenant si tu sauvegardes ton travail et que tu lances ton app, tu vas toujours avoir la même erreur.

### 1.2 Ajout du dossier with-spinner

Continues par créer un Spinner component dans le dossier components. Pour ça crées un nouveau dossier `with-spinner` et dedans deux fichiers : `WithSpinner.js` et son css `WithSpinner.css`.

Dans le fichier css, tapes les codes suivant : 
```css
  .SpinnerOverlay {
  height: 60vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  }

  .SpinnerContainer {
    display: inline-block;
    width: 50px;
    height: 50px;
    border: 3px solid rgba(195, 195, 195, 0.6);
    border-radius: 50%;
    border-top-color: #636767;
    animation: spin 1s ease-in-out infinite;
    -webkit-animation: spin 1s ease-in-out infinite;
  }

  @keyframes spin {
    to {
      -webkit-transform: rotate(360deg);
    }
  }

  @-webkit-keyframes spin {
    to {
      -webkit-transform: rotate(360deg);
    }
  }
```

Puis dans le fichier js : 
```js
  import React from 'react';
  import './WithSpinner.css';

  const WithSpinner = WrappedComponent => {
    const Spinner = ({ isLoading, ...othersProps }) => {
      return isLoading ? (
        <div className='SpinnerOverlay'>
          <div className='SpinnerContainer'></div>
        </div>
      ) : (
        <WrappedComponent {...othersProps} />
      )
    }
    return Spinner;
  };

  export default WithSpinner;
```
Dans ce component `WithSpinner`, tu reçois le component à entourer comme paramètre. A l'intérieur, tu as une méthode `Spinner` qui te retourne en fonction de l'état du paramètre `isLoading` (ça retourne un booléen) soit ton Spinner, soit le component wrapper.

Pour cela, tu as utilisé un `ternary operator` : `isLoading ? renvoie ça : renvoie plutôt ça`.

Puis tu retournes ce qui est renvoyer par la méthode `Spinner`.

Ce que tu viens d'implémenter s'appelle un High Order Component (HOC). C'est une méthode qui prends en paramètre le component que tu veux entourer de supers pouvoirs venant du HOC. Ici, c'est le pouvoir d'être en mode `isLoading`.

Très bien tout ça, maintenant où tu mets ce Spinner ? A ton avis, quel component ou quelle page sait quand les données sont bien chargées dans ton Redux ? 

Yes, dans la page `OrderPage`, là où tu lances pendant la phase de `mounting` la méthode `convertCollectionsSnapshotToMap`, méthode qui récupère depuis Firebase les données que tu as besoin.

C'est cette page qui sait exactement quand la récupération de données est terminé et donc est capable de transmettre le message en déclanchant une action (mettre isLoading à false) dans Redux.

### 1.3 Modification du component concerné par la récupération de données

Importes le WithSpinner HOC et `useState` dans ta page `OrderPage` :
```js
import React, { useState } from 'react';
import WithSpinner from '../../components/with-spinner/WithSpinner'; 
```

Tu auras besoin de `useState` pour fixer le state de `isLoading`. 

Juste avant ton composant `OrderPage`, tu vas créer un component intermédiaire :
```js
const ItemsHOC = WithSpinner(Items);
```
Ce component va utiliser le HOC WithSpinner en wrappant le component `Items` que tu utilisais pour retourner ta liste d'items. A la place d'utiliser le component `Items`, tu utilises `ItemsHOC` dans ton code : 
```js
  return (
    <div className="container-fluid">
      <div className="row">
        <div className="col-12 col-md-8 vh-100 overflow-auto">
          <ItemsHOC isLoading={isLoading}/>
        </div>
        <div className="col-12 col-md-4 shadow vh-100 d-flex">
          <Basket />
        </div>
      </div>
    </div>
  )
```
En même temps, tu en profites pour lui passer en props `isLoading` qu'il a besoin pour déterminer quoi retourner.

Avant le `useEffetc`, ajoutes ton `useState` : 
```js
const [isLoading, setIsLoading] = useState(true);

useEffect(() => {
    const collectionRef = firestore.collection('items');
    collectionRef.onSnapshot(async snapshot => {
      const collectionMap = await convertCollectionsSnapshotToMap(snapshot);
      updateCollections(collectionMap);
      setIsLoading(false);
    });
  },[updateCollections]);
```
Ajoutes dans le `useEffect`, le setIsLoading(false), ainsi dès que les données sont bien remontées, `isLoading` passe à `false` et donc ton WithSpinner va retourner le component qui est wrappé sans erreur.

Essaies de retirer la ligne `setIsLoading(false);` et lances ton app, normalement tu dois voir le spinner qui tourne. Bravo.

## 2. Ce que tu dois retenir
Voilà tu viens de mettre en place un spinner qui permet d'animer un peu ton app et prévenir ton utilisateur qu'il se passe quelques choses dans ton app et qu'il doit patienter un peu.

Pour ça tu as vu :
* Un `ternary operator` pour créer un test et renvoyer une expression en fonction de ce test
* Comment ajouter des supers pouvoirs avec les High Order Component qui ajoutent des fonctionnalités à un component existant
* Comment faire une petite animation en css

## 3. Pour aller plus loin

* Pour en savoir plus sur les animations en css [w3schools.com](https://www.w3schools.com/css/css3_animations.asp)


