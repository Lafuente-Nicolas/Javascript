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

## Directives d’attribut

### [ngStyle] : appliquer des styles dynamiques

La directive `[ngStyle]` permet de **modifier les styles CSS d’un élément dynamiquement** à partir d’un objet TypeScript.

---

### 📌 Syntaxe :
```html
<p [ngStyle]="{ color: 'red', fontWeight: 'bold' }">Texte stylé</p>
```
Fonctionnement :

- `[ngStyle]` attend un objet JavaScript contenant des paires propriété: valeur.

- Les propriétés CSS sont écrites en camelCase (ex. : backgroundColor, fontSize).

##  [ngClass] : appliquer des classes CSS dynamiques

La directive `[ngClass]` permet de **gérer dynamiquement les classes CSS** à appliquer à un élément, selon des conditions définies dans le composant.

---

###  Syntaxes possibles :
```html
<!-- Ajouter une ou plusieurs classes -->
<p [ngClass]="'ma-classe'"></p>
<p [ngClass]="['classe1', 'classe2']"></p>

<!-- Appliquer une classe selon une condition -->
<p [ngClass]="{ 'erreur': isError, 'valide': !isError }"></p>
```
#### Fonctionnement :

`[ngClass]` accepte :

- Une chaîne (1 seule classe)

- Un tableau (plusieurs classes)

- Un objet avec conditions ({ classe: condition })

## Pipes

Les **pipes Angular** permettent de transformer les données à afficher dans le template HTML. Voici les plus couramment utilisés : `uppercase`, `date`, `currency`, et `json`.

---

### Pipe `uppercase`

Transforme une chaîne de caractères en **majuscules**.

```html
<p>{{ 'bonjour' | uppercase }}</p>
```

➡️ **Résultat** : `BONJOUR`

---

### Pipe `date`

Permet de formater une date.

```html
<p>{{ today | date }}</p>
<!-- Affiche : 4 juin 2025 -->

<p>{{ today | date:'fullDate' }}</p>
<!-- Affiche : mercredi 4 juin 2025 -->

<p>{{ today | date:'shortTime' }}</p>
<!-- Affiche : 14:35 -->
```

Dans le fichier TypeScript :

```ts
today = new Date();
```

---

### Pipe `currency`

Affiche une **valeur monétaire** avec le symbole approprié.

```html
<p>{{ 99.99 | currency }}</p>
<!-- Affiche : €99.99 -->

<p>{{ 99.99 | currency:'USD' }}</p>
<!-- Affiche : $99.99 -->

<p>{{ 99.99 | currency:'EUR':'symbol':'4.2-2' }}</p>
<!-- Affiche : €99.99 -->
```

---

### Pipe `json`

Affiche un **objet JavaScript** ou un tableau au format JSON.

```html
<pre>{{ user | json }}</pre>
```

Dans le fichier TypeScript :

```ts
user = { nom: 'Nicolas', age: 19 };
```
 **Résultat** :
```json
{
  "nom": "Nicolas",
  "age": 19
}
```
---

### Récapitulatif

| Pipe      | Utilité                       | Exemple                             |
|-----------|-------------------------------|-------------------------------------|
| `uppercase` | Majuscules                  | `{{ 'bonjour' | uppercase }}`       |
| `date`     | Formatage de date            | `{{ today | date:'fullDate' }}`     |
| `currency` | Affichage de devise          | `{{ 50 | currency:'EUR' }}`         |
| `json`     | Affichage d'objet/array      | `{{ user | json }}`                 |

---

Astuce : Les pipes sont **non-destructifs** – ils ne modifient pas la donnée dans le TypeScript, uniquement dans l’affichage.

### Enchaîner plusieurs pipes

#### Exemple :

Supposons que tu as une date et que tu veux :

- Formater la date (date)

- Transformer le résultat en majuscules (uppercase)
```html
<p>Date formatée en majuscules : {{ dateDuJour | date:'fullDate' | uppercase }}</p>
```
## Formulaires avec FormsModule

### Importer FormsModule avec `[(ngModel)]`
- Le module FormsModule contient les directives pour gérer le binding avec les formulaires template-driven (ex. : `[(ngModel)]`).

- Sans importer FormsModule, Angular ne reconnaîtra pas la directive ngModel et tu auras une erreur.

```ts
import { FormsModule } from '@angular/forms';
```

### `(ngSubmit)`

  - `(ngSubmit)` est un événement Angular qui se déclenche lorsque l’utilisateur soumet un formulaire HTML (avec un bouton de type submit).

  - Il te permet de capturer l’action d’envoi du formulaire pour exécuter une fonction dans ton composant (ex : valider, envoyer des données, etc.).

### Ajouter des validations de base (required, minlength, etc.)

- `required` → champ obligatoire

- `minlength="3"` → minimum 3 caractères

- `#nomInput="ngModel"` → référence locale au contrôle du champ pour vérifier son état

- `nomInput.invalid && nomInput.touched` → afficher les erreurs uniquement si le champ est invalide et a été touché

- Le bouton est désactivé tant que le formulaire est invalide (`[disabled]="monForm.invalid"`)

### Afficher les erreurs de validation avec *ngIf

#### exemple :

Avec `*ngIf`, on affiche les messages d’erreur uniquement quand un champ est invalide et que l’utilisateur a déjà interagi avec lui, pour guider sans gêner l’expérience utilisateur.

```ts
<form #monForm="ngForm" (ngSubmit)="onSubmit()" novalidate>
  <label for="prenom">Prénom :</label>
  <input
    id="prenom"
    name="prenom"
    type="text"
    [(ngModel)]="prenom"
    required
    minlength="4"
    #prenomInput="ngModel"
  />

  <!-- Affichage des erreurs avec *ngIf -->
  <div *ngIf="prenomInput.invalid && prenomInput.touched" style="color: red;">
    <div *ngIf="prenomInput.errors?.['required']">
      Le prénom est obligatoire.
    </div>
    <div *ngIf="prenomInput.errors?.['minlength']">
      Le prénom doit contenir au moins 4 caractères.
    </div>
  </div>

  <button type="submit" [disabled]="monForm.invalid">Envoyer</button>
</form>
```
## Configuration du Routing dans Angular v20

---

### 1. Créer 3 composants (avec Angular CLI)

```bash
ng generate component home  
ng generate component contact   
ng generate component about
```
### 2. Créer le fichier app-routing.ts
```ts
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { ContactComponent } from './contact/contact.component';
import { AboutComponent } from './about/about.component';

export const appRoutes: Routes = [
  { path: '', component: HomeComponent },           // Page d'accueil, URL "/"
  { path: 'contact', component: ContactComponent }, // Page Contact, URL "/contact"
  { path: 'about', component: AboutComponent },     // Page À propos, URL "/about"
];
```
### 3. Modifier app.ts pour utiliser le routing
```ts
import { Component } from '@angular/core';
import { RouterModule } from '@angular/router';
import { appRoutes } from './app-routing';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterModule.forRoot(appRoutes)],
  template: `
    <nav>
      <a routerLink="">Accueil</a> |
      <a routerLink="contact">Contact</a> |
      <a routerLink="about">À propos</a>
    </nav>
    <router-outlet></router-outlet>
  `,
})
export class AppComponent {}
```
- `<router-outlet>` est un emplacement où Angular affichera la page correspondant à l’URL.

- Les liens routerLink permettent de naviguer entre les pages sans recharger.

#### Résultat attendu

- Quand tu vas sur /, tu vois la page Accueil.

- Quand tu vas sur /contact, tu vois la page Contact.

- Quand tu vas sur /about, tu vois la page À propos.

### Ajouter `<router-outlet>` dans app.component.html

Qu’est-ce que `<router-outlet>` ?

- C’est une balise Angular spéciale qui sert de point d’ancrage pour afficher les composants correspondant aux routes.

- Quand tu navigues vers une URL, Angular charge le composant associé dans cette balise.

#### Comment l’ajouter ?

Dans ton fichier `app.component.html`, il suffit d’insérer :
```html
<nav>
  <a routerLink="">Accueil</a> |
  <a routerLink="contact">Contact</a> |
  <a routerLink="about">À propos</a>
</nav>

<router-outlet></router-outlet>
```

- Ici, le menu avec les liens utilise routerLink pour naviguer.

- Le contenu affiché changera dans la zone `<router-outlet>` selon la route active.

#### Résumé

- Sans `<router-outlet>`, Angular ne saura pas où afficher les pages liées au routing.

- C’est obligatoire pour que le système de navigation fonctionne.

### Ajouter une route avec paramètre `(:id)`
 
- Une route avec paramètre permet d’afficher une page différente selon l’id dans l’URL.

Par exemple :

    /produit/1 → montre le produit numéro 1

    /produit/2 → montre le produit numéro 2

### 1. Crée une route avec paramètre

Dans app-routing.ts :
```ts
import { Routes } from '@angular/router';
import { DetailComponent } from './detail/detail.component';

export const appRoutes: Routes = [
  { path: 'produit/:id', component: DetailComponent }
];
```
### 2. Dans DetailComponent, tu récupères le paramètre id
```ts
import { Component } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-detail',
  standalone: true,
  template: `
    <h2>Détail du produit</h2>
    <p>Produit numéro : {{ id }}</p>
  `
})
export class DetailComponent {
  id = '';

  constructor(private route: ActivatedRoute) {
    this.route.params.subscribe(params => {
      this.id = params['id'];
    });
  }
}
```
### 3. Dans le menu de navigation (ex. app.component.ts)
```html
<a routerLink="/produit/1">Produit 1</a>
<a routerLink="/produit/2">Produit 2</a>
<router-outlet></router-outlet>
```
#### Résultat

- Tu cliques sur "Produit 1" → URL devient /produit/1 → Affiche Produit numéro : 1

- Tu cliques sur "Produit 2" → URL devient /produit/2 → Affiche Produit numéro : 2