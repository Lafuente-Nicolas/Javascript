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

## `@Component` 

Le décorateur `@Component` est une fonction spéciale d’Angular qui transforme une classe TypeScript en composant Angular.

exemple : 

imaginons on veut créer un header
```
ng generate component header
```

cela va créer 
```
src/app/header/header.component.ts
src/app/header/header.component.html
src/app/header/header.component.scss
src/app/header/header.component.spec.ts
```

## composant enfant dans app.component.html

Le fichier footer.component.ts contient :
```ts
@Component({
  selector: 'app-footer',  // ← c’est ça qu’on va utiliser
  templateUrl: './footer.component.html',
  styleUrls: ['./footer.component.scss']
})
export class FooterComponent {}
```
```html
<!-- app.component.html -->
<app-header></app-header>      <!-- composant enfant 1 -->
<main>
  <p>Bienvenue dans mon application Angular !</p>
</main>
<app-footer></app-footer>      <!-- composant enfant 2 -->
```

## Lier HTML et TypeScript

### l’interpolation {{ message }} 

L’interpolation te permet d’afficher des données TypeScript dans ton HTML.

- En gros : tu écris une variable dans ton .ts, et tu l’utilises dans ton .html avec {{ ... }}.

#### Fonctionnement :

- Angular remplace {{ message }} dans le HTML par la valeur de la propriété message définie dans le fichier .ts du composant.

###  Exemple :

#### TypeScript (`app.component.ts`)
```ts
export class AppComponent {
  message = 'Bonjour Angular !';
}
```
#### HTML (app.component.html)
```html
<h1>{{ message }}</h1>
```
#### Résultat affiché dans le navigateur :
```
Bonjour Angular !
```
### Property Binding : `[src]="imageUrl"`

La **liaison de propriété** permet de **lier une propriété HTML à une variable TypeScript**.

---

####  Syntaxe :
```html
<img [src]="imageUrl">
```
### Exemple complet :

#### TypeScript (app.component.ts)
```ts
export class AppComponent {
  imageUrl = 'https://via.placeholder.com/150';
}
```
#### HTML (app.component.html)
```html
<img [src]="imageUrl" alt="Image dynamique">
```
###  Event Binding : `(click)="increment()"`

L’**event binding** permet d’**écouter un événement DOM** (comme un clic) et d’exécuter une méthode TypeScript en réponse.

---

###  Syntaxe :
```html
<button (click)="increment()">Clique moi</button>
```
#### Fonctionnement :

- Quand l’utilisateur clique sur le bouton, Angular appelle la fonction increment() du composant.

### Exemple :

#### TypeScript (app.component.ts)
```ts
export class AppComponent {
  count = 0;

  increment() {
    this.count++;
  }
}
```

#### HTML (app.component.html)
```html
<p>Compteur : {{ count }}</p>
<button (click)="increment()">Incrémenter</button>
```
###  Two-way Binding avec `[(ngModel)]`

Le **two-way binding** permet de **lier une variable TypeScript à un champ du formulaire** (comme un champ texte), **dans les deux sens** :
- Quand l’utilisateur saisit quelque chose, la variable est mise à jour.
- Quand la variable change, la valeur affichée dans le champ est mise à jour aussi.

---

###  Syntaxe :
```html
<input [(ngModel)]="username">
```
#### Fonctionnement :

- `[(ngModel)]` combine [property binding] `([value])` et (event binding) ((input)).

- Il est très utile pour les formulaires dynamiques.

### Exemple :

#### TypeScript (app.component.ts)
```ts
export class AppComponent {
  username = '';
}
```

#### HTML (app.component.html)
```html
<input [(ngModel)]="username" placeholder="Entrez votre nom">
<p>Bonjour {{ username }} !</p>
```
## Directives structurelles

### `*ngIf` : afficher ou masquer un élément selon une condition

La directive **`*ngIf`** permet d’**afficher un élément HTML seulement si une condition est vraie**.

---

### 📌 Syntaxe :
```html
<p *ngIf="isVisible">Ce texte est visible si isVisible vaut true.</p>
```
### Fonctionnement :

- Si `isVisible` est true, l’élément est ajouté au DOM.

- Si `isVisible` est false, l’élément n’est pas présent du tout dans la page (pas juste masqué avec du CSS).

### Exemple :

### TypeScript (app.component.ts)
```ts
export class AppComponent {
  isVisible = true;
}
```

#### HTML (app.component.html)
```html
<button (click)="isVisible = !isVisible">
  Afficher / Masquer le message
</button>

<p *ngIf="isVisible">Bonjour, je suis visible !</p>
```
### *ngFor : afficher une liste d’éléments

La directive **`*ngFor`** permet de **répéter un élément HTML** pour chaque item d’un tableau.

---

###  Syntaxe :
```html
<li *ngFor="let fruit of fruits">{{ fruit }}</li>
```
#### Fonctionnement :

- Angular parcourt le tableau fruits.

- À chaque tour, il crée un `<li>` avec la valeur de l’élément courant.

- La variable fruit représente l’élément actuel de la boucle.

### Exemple :

#### TypeScript (app.component.ts)
```ts
export class AppComponent {
  fruits = ['Pomme', 'Banane', 'Fraise'];
}
```

#### HTML (app.component.html)
```html
<ul>
  <li *ngFor="let fruit of fruits">{{ fruit }}</li>
</ul>
```

#### Résultat :
```
Une liste avec :

    Pomme

    Banane

    Fraise
```

### *ngIf...else avec `<ng-template>`

Avec `*ngIf`, tu peux afficher un **bloc alternatif** quand la condition est fausse, grâce à **`else`** et **`<ng-template>`**.

---

### 📌 Syntaxe :
```html
<p *ngIf="isLoggedIn; else notLogged">Bienvenue !</p>
<ng-template #notLogged>
  <p>Veuillez vous connecter.</p>
</ng-template>
```
### Fonctionnement :

- Si `isLoggedIn` vaut `true`, Angular affiche le premier `<p>`.
- Sinon, il affiche le contenu du `<ng-template #notLogged>`.

---

###  Exemple complet :

####  TypeScript (`app.component.ts`)
```ts
export class AppComponent {
  isLoggedIn = false;
}
```
#### HTML (app.component.html)
```HTML
<button (click)="isLoggedIn = !isLoggedIn">
  Se connecter / Se déconnecter
</button>

<p *ngIf="isLoggedIn; else notLogged">Bienvenue, utilisateur !</p>

<ng-template #notLogged>
  <p>Accès refusé. Merci de vous connecter.</p>
</ng-template>
```
#### Résultat :

- Quand `isLoggedIn = true` → affiche « Bienvenue, utilisateur ! »

- Quand `isLoggedIn = false` → affiche « Accès refusé. Merci de vous connecter. »