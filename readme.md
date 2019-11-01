# pwa-technos
Projet additionnel à "cours-pwa-pratique" afin de gérer les données de l'application PWA avec Firebase Functions.

Le FaaS (Function-as-a-Service) est un service Cloud lié au serverless computing et aux architectures serverless. Les développeurs de logiciels peuvent s’en servir pour déployer une fonction individuelle. La fonction démarre en quelques millisecondes et traite des requêtes individuelles, puis le processus s’achève.
https://www.lebigdata.fr/faas-definition

Donc nous allons mettre en place un FAAS avec Firebase.
Firebase car c'est une bonne solution assez complète, rachetée par Google il y a deux ans, elle s'est étoffée d'outils interessant et continue de croitre. Nous en avons parlé dans le cadre des push notifications et nous allons réellement l'utiliser pour gérer nos données.

Assez facile à mettre en place cela nous permet d'associer à la fois les données et la gestion serveur permettant de les gérer. Autrement nous aurions besoin d'un service de base de données comme mongoDB et de publier un serveur nodejs chez un hébergeur pour le traitement des requêtes.


1. Création d'un projet Firebase
Donc commençons par créer notre compte firebase et notre projet "pwa-technos" : https://firebase.google.com/
Ajoutez votre nom si besoin à la suite "pwa-technos-nom"
Désactivez Analytics pour le moment nous n'en avons pas besoin.
Dans les paramètres du projet, choisir l'emplacement de la ressource cloud en europe (rgpd)

2. Création du projet en local
Avec le terminal créez un nouveau dossier "pwa-technos" et entrez dedans puis suivez les instructions
```
mkdir pwa-technos
cd pwa-technos
npm install -g firebase-tools
firebase login
firebase init functions
```
Questions : réponses
Select project : existing project (pwa-technos)
Select a default Firebase project for this directory : pwa-technos
What language would you like to use to write Cloud Functions? : Javascript
Do you want to use ESLint to catch probable bugs and enforce style? : n
Do you want to install dependencies with npm now? : y

Créer la base de donnée en real time : Firebase / Database / 
Vous pouvez ajouter un exemple pour visualiser le résultat


3. Installez les dépendances, récupérez le fichier index.js et déployer les endpoints
3.1 Cors : Cross-Origin Resource Sharing
```
npm i -S cors
```

3.2 Copiez collez le fichier index.js

3.3 Déployez
```
firebase deploy
```
(firebase deploy --only functions:nomFunction)


4. Testez vos api
Visualisez vos function dans Firebase / Développer / Functions
Installez sur votre ordinateur "Postman", créez une collection, ajoutez votre première requête
(Récupérer vos url dans Firebase / Functions)

4.1 Ajouter un item : https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/addTechno
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


4.2 Récupérer la liste des items : GET > https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/getTechnos
> récupération des 3 items


4.3 Supprimer un item de la liste : DELETE > https://us-central1-xxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/deleteTechno
Avec dans Params "id" : "keyid2"
> Suppression de l'item 2


Notre service tiers fonctionne maintenant correctement.
Nous pouvons revenir au projet initial.