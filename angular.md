# Angular

##  Angular CLI

- Créer une application avec `ng new mon-app`
- Lancer le serveur de développement avec `ng serve`
- Générer un composant avec `ng generate component`
- Générer un service avec `ng generate service`
- Lister toutes les commandes disponibles avec `ng help`

## l’architecture d’un projet Angular

- **src/** : Contient tout le code source de l’application Angular.

- **app/** : Dossier principal où sont placés les composants, services et modules de ton app.

- **assets/** : Contient les fichiers statiques (images, icônes, polices, etc.).

- **environments/** : Gère la configuration de l’application selon l’environnement (développement ou production).

- **index.html** : Page HTML principale dans laquelle Angular injecte l’application.

- **styles.scss** : Fichier global pour les styles CSS/SCSS de l’app.

- **main.ts** : Fichier principal qui démarre l’application Angular en lançant le module racine (`AppModule`).

- **app.module.ts** : Fichier qui déclare le module principal de l’application, où sont enregistrés les composants, services et autres modules.

- **angular.json** : Fichier de configuration global d’Angular CLI, qui définit la structure du projet, les chemins, les styles, les scripts et les options de build/serve/test.

##  Qu'est-ce qu'une SPA (Single Page Application) ?

Une **SPA (Single Page Application)** est une application web qui fonctionne sur **une seule page HTML**.  
Au lieu de recharger toute la page à chaque action, seule une **partie du contenu est mise à jour dynamiquement**, grâce à JavaScript.

###  Avantages :
- Navigation **rapide et fluide** (pas de rechargement complet de page).
- Expérience utilisateur proche d’une **application mobile**.
- Moins de trafic entre le client et le serveur.

###  Fonctionnement :
- Une seule page (`index.html`) est chargée au début.
- Angular (ou un autre framework) gère ensuite l’affichage des vues selon les actions de l’utilisateur.
- Les données sont souvent récupérées via des **API** sans recharger la page.

###  Exemple :
Quand tu cliques sur "Accueil" ou "Contact" dans un site Angular, le navigateur **ne recharge pas la page**, mais affiche une nouvelle vue grâce au **Angular Router**.
