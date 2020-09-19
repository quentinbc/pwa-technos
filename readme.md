# pwa-technos
![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg) ![forthebadge](https://forthebadge.com/images/badges/made-with-javascript.svg)

_Projet additionnel à "cours-pwa-pratique" afin de gérer les données en CRUD de l'application PWA avec Firebase Functions_

**Ci-dessous l'explicatif vous permettant de réaliser le résultat de ce projet**


## 1. Création d'un projet Firebase 🔥
* Créez un compte firebase et votre projet "pwa-technos" : https://firebase.google.com/
* Ajoutez votre nom si besoin à la suite "pwa-technos-nom"
* Désactivez Analytics pour le moment nous n'en avons pas besoin.
* Si vous souhaitez que cos données soient gérées dans l'Union Européenne (pour la RGPD) : dans les paramètres du projet, choisissez l'emplacement de la ressource cloud en Europe
* Créer la base de donnée en "Real Time" : Firebase / Database


## 2. Création du projet en local
Avec le terminal créez un dossier "pwa-technos" en dehors de tout projet en cours, entrez dedans puis suivez les instructions
```
mkdir pwa-technos
cd pwa-technos
npm install -g firebase-tools
firebase login
firebase init functions
```

Questions : réponses pour ``firebase init functions``

- Select project : existing project (pwa-technos)
- Select a default Firebase project for this directory : pwa-technos
- What language would you like to use to write Cloud Functions? : Javascript
- Do you want to use ESLint to catch probable bugs and enforce style? : n
- Do you want to install dependencies with npm now? : y


## 3. Installez et déployer les endpoints
Entrez dans le dossier ``cd functions``


### 3.1 Cors : Cross-Origin Resource Sharing
Installez ``cors``qui permet à un client d'accèder à votre serveur malgré le fait qu'il ne soit pas sur le même domaine (protocole, port ou domaine différent)
```
npm i -S cors
```


### 3.2 Copiez collez le fichier index.js
Copiez collez le fichier dans ``functions/index.js`` : 
https://github.com/quentinbc/pwa-technos/blob/master/functions/index.js


### 3.3 Déployez
Dans le terminal exécuter : 
```
firebase deploy
```
_Pour déployer uniquement une fonction ``firebase deploy --only functions:nomFunction``_



## 4. Testez vos api
* Pour récupérer les url d'api visualisez vos function dans "Firebase / Développer / Functions" 
* Utilisez POSTWOMAN pour vos tests d'api : https://postwoman.io/


### 4.1 Ajouter un item
Créer votre requête POSTWOMAN avec en url (utiliser votre url d'api) : _https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/addTechno_
* Tester en **GET** et vous obtiendrez le résultat : ``{"message":"Not allowed"}``
* Tester en **POST** avec les datas suivantes à ajouter dans **Body / raw / JSON (application/json)** de votre requête POSTMAN
```
{
"id":"keyid1",
"name":"Nom techno 1",
"description" : "Description Techno 1",
"url" : "Url Techno 1"
}
```
> ajouter 3 items en changeant le num à chaque fois
Vérifiez dans votre Firebase / Database que vous obtenez bien votre collection d'objets.


### 4.2 Récupérer la liste des items
Créer votre nouvelle requête POSTWOMAN avec un appel **GET** et l'url : _https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/getTechnos_
> Vous devriez récupérer les 3 items


### 4.3 Supprimer un item
Créer votre nouvelle requête POSTWOMAN avec un appel **DELETE** et l'url : _https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/deleteTechno_
Ajoutez les données suivantes dans **Params** ``"id" : "keyid2"``
> Vous devriez obtenir la liste des items sans l'item n°2


_Bravo 👏 votre service tiers de Firebase Function fonctionne correctement_
