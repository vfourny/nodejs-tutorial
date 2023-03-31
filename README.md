# Introduction à NODEJS et Express

## Prérequis

- Node (dernière version LTS)
- Postman
- Editeur de code

## Préparation du TP

### Création du serveur

Une fois le projet cloné rendez-vous dans le dossier de ce dernier depuis un terminal. 
Utilisez les commandes suivantes pour initialiser votre projet : `npm init`.

Créer ensuite un fichier javascript servant de point d'entrée et correspondant à la clé main de votre **package.json** (index.js par défaut).

A l'intérieur de ce fichier grâce à la méthode **createServer** vous allez créer un objet serveur basé sur le package **http** (automatiquement disponible via nodejs).
Cet objet serveur fera trois choses:

- Il affichera dans le terminal un message indiquant que le serveur est bien démarré en précisant son port
- Nous afficherons aussi dans la console l'url indiqué dans la requête
- Enfin la réponse **end** du serveur devra être un message indiquant "Hello world".

Enfin vous n'avez plus qu'à dire à votre serveur d'écouter sur le port 3000 avec la fonction `listen()`

### Amélioration de l'environnement de développement

Afin de développer plus rapidement grâce au rechargement à chaud (hot reload) nous allons installer le package **nodemon** avec la commande `npm install nodemon`. Choisissez selon votre préférence une installation globale ou locale du paquet. S'il s'agit d'une installation locale n'oubliez pas de mettre à jour votre script de démarrage.

Ensuite dans la partie script de votre **package.json** nous allons créer un script *dev* qui sera utilisé en phase de développement. Ce dernier réalisera simplement la commande suivante: `nodemon nom_fichier_main`.

Désormais vous pouvez utiliser `npm run dev` au lieu de `node nom_fichier_main`.

## Débuter avec Express

Désormais nous allons utiliser express pour réaliser nos interactions avec le serveur. En effet ce dernier englobe une multitude de méthodes HTTP qui permettent d'éviter de réécrire la gestion complète d'un serveur.

Commençons par installer express avec la commande `npm install express`. Vous trouverez la doc complète d'express [ici](https://expressjs.com/fr/).

Retournez dans votre fichier main et supprimer son contenu. Nous allons recommencer en utilisant directement **express** au lieu de **http**. Servez-vous des exemples du cours.

Importez **express** dans votre fichier main de la même manière que vous l'avez fait pour le package **http**. Puis initialisez le serveur avec la foncton **express()**.

Il ne reste plus qu'à demander à votre serveur d'écouter sur le port de votre choix (3000 par défaut). La fonction d'écoute prendra en second paramètre une fonction de callback qui renverra un message console indiquant que le serveur a bien démarré.

Testez votre application avec Postman ou votre navigateur.

## Création des routes

### GET

Vous allez devoir créer deux routes GET différentes:

- La première sera une route GET qui utilisera l'endpoint '/' et renverra comme réponse un code status HTML 204 (No Response).
- La seconde route sera une route GET qui utilisera l'endpoint '/:name'. Cet endpoint prendra la valeur renseignée à la place de *name* dans les **params** de la requête. La réponse affichera ensuite cette valeur comme message. La réponse enverra aussi un statut code 200 (Response).

Vous testerez vos routes sur Postman.

### POST

Pour commencer il va falloir rajouter le package [body-parser](https://www.npmjs.com/package/body-parser). Ce package va permettre de récupérer le body des requêtes post et de pouvoir le formatter pour le rendre utilisable.

Une fois installé, dans votre fichier main au niveau de la zone des *require* ajouter cette ligne `const bodyParser = require('body-parser')`.
Puis ajouter la ligne suivante après l'instanciation d'**express()** : `app.use(bodyParser.text())`.
Vous devriez avoir un résultat similaire:

```javascript
const express = require('express')
const bodyParser = require('body-parser');

const app = express()
app.use(bodyParser.text())
```

*Remarque: La fonction use est un middleware, c'est à dire un morceau de code qui s'execute avant chaque requête quelque soit son type (GET, POST, PATCH, ...). Si vous voulez en savoir plus sur les middlewares vous trouverez plus d'informations [ici](https://expressjs.com/fr/guide/using-middleware.html).*

Lorsque vous ferez des requêtes Postman vous pourrez désormais insérer du texte dans l'onglet Body de votre requête. N'oubliez pas de la paramétrer en mode RAW.

Créer une route **POST** pointant sur l'endpoint *write*. Cet endpoint récupèrera le body de la requête et écrira sa valeur dans un fichier data.txt
Pour écrire un fichier en NodeJS vous pouvez utiliser le package **fs** qui est un package interne à Node et ne necessite pas de npm install. Importez le simplement comme n'importe quel autre package. Vous utilisez la méthode **appendFile** de ce package. Renseignez-vous dans la documentation sur son utilisation.
