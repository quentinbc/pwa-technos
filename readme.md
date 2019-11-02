# pwa-technos
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)][![forthebadge](https://forthebadge.com/images/badges/made-with-javascript.svg)]

_Projet additionnel à "cours-pwa-pratique" afin de gérer les données en CRUD de l'application PWA avec Firebase Functions.

Ci-dessous l'explicatif vous permettant de réaliser le résultat de ce projet.


## 1. Création d'un projet Firebase
* Créez un compte firebase et votre projet "pwa-technos" : https://firebase.google.com/
* Ajoutez votre nom si besoin à la suite "pwa-technos-nom"
* Désactivez Analytics pour le moment nous n'en avons pas besoin.
* Si vous souhaitez que cos données soient gérées dans l'Union Europééenne (pour la RGPD) : dans les paramètres du projet, choisissez l'emplacement de la ressource cloud en europe
* Créer la base de donnée en real time : Firebase / Database


## 2. Création du projet en local
Avec le terminal créez un nouveau dossier "pwa-technos" et entrez dedans puis suivez les instructions
```
mkdir pwa-technos
cd pwa-technos
npm install -g firebase-tools
firebase login
firebase init functions
```

Questions : réponses pour ``firebase login``

- Select project : existing project (pwa-technos)
- Select a default Firebase project for this directory : pwa-technos
- What language would you like to use to write Cloud Functions? : Javascript
- Do you want to use ESLint to catch probable bugs and enforce style? : n
- Do you want to install dependencies with npm now? : y


## 3. Installez et déployer les endpoints
Entrez dans le dossier ``cd functions``

### 3.1 Cors : Cross-Origin Resource Sharing
Installez ``cors``qui permet à un client d'accèder à votre serveur malgrè le fait qu'il ne soit pas sur le même domaine (protocole, port ou domaine différent)
```npm i -S cors```

### 3.2 Copiez collez le fichier index.js
Récupérez le fichier dans ``_functions/index.js``


### 3.3 Déployez
```
firebase deploy
```
_Pour déployer uniquement une fonction ``firebase deploy --only functions:nomFunction``



## 4. Testez vos api
* Visualisez vos function dans Firebase / Développer / Functions. 
* Installez sur votre ordinateur "Postman", créez une collection, ajoutez votre première requête (récupérée vos url dans Firebase / Functions)

### 4.1 Ajouter un item : https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/addTechno
Testez en GET et vous obtiendrez le résultat : {"message":"Not allowed"}
Testez en POST avec les datas suivantes : dans Body : raw : JSON (application/json)
```
{
"id":"keyid1",
"name":"Nom techno 1",
"description" : "Description Techno 1",
"url" : "Url Techno 1",
"unsynced" : false
}
```
> ajouter 3 items en changeant le num à chaque fois


### 4.2 Récupérer la liste des items : GET > https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/getTechnos
> récupération des 3 items


### 4.3 Supprimer un item de la liste : DELETE > https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/deleteTechno
Avec dans Params "id" : "keyid2"
> Suppression de l'item 2


_Bravo votre service tiers de Firebase Function fonctionne maintenant correctement.