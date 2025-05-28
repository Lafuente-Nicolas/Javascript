# 🌐 Cours Complet sur le DOM en JavaScript

---

## 🔹 1. Qu’est-ce que le DOM ?

**DOM** signifie **Document Object Model**.  
C’est une **interface de programmation (API)** qui permet à JavaScript d’**interagir avec le contenu HTML/CSS** d’une page web.

Le DOM **représente la page web comme un arbre d’objets**. Chaque balise HTML devient un **nœud (node)**.

### Exemple visuel :

```html
<html>
  <body>
    <h1>Hello</h1>
    <p>Bienvenue sur mon site</p>
  </body>
</html>
```

Arbre DOM :

```
- html
  └── body
      ├── h1 → "Hello"
      └── p  → "Bienvenue sur mon site"
```

---


## 🔹 2. Accéder aux éléments du DOM

### Méthodes principales :

| Méthode                             | Description                                      |
|-------------------------------------|--------------------------------------------------|
| `document.getElementById()`         | Sélection par ID                                 |
| `document.getElementsByClassName()` | Sélection par classe (HTMLCollection)           |
| `document.getElementsByTagName()`   | Sélection par balise (HTMLCollection)           |
| `document.querySelector()`          | Sélection avec un **sélecteur CSS**             |
| `document.querySelectorAll()`       | Sélection multiple (NodeList)                   |

### Exemples :

```javascript
const titre = document.getElementById('monTitre');
const paragraphes = document.getElementsByTagName('p');
const bouton = document.querySelector('.btn');
```

---

## 🔹 3. Modifier le contenu et les styles

### 🔸 Modifier le texte :


```javascript
titre.textContent = 'Nouveau Titre';
titre.innerHTML = '<em>Titre en italique</em>';
```

### 🔸 Modifier les styles :

```javascript
titre.style.color = 'red';
titre.style.fontSize = '2rem';
```

---

## 🔹 4. Manipuler les attributs

```html
<img id="image" src="chat.png" alt="Chat mignon">
```

```javascript
const image = document.getElementById('image');

image.getAttribute('src'); // "chat.png"
image.setAttribute('src', 'chien.png');
image.setAttribute('alt', 'Chien mignon');
```

---

## 🔹 5. Ajouter / Supprimer des classes CSS

```javascript
titre.classList.add('important');
titre.classList.remove('important');
titre.classList.toggle('important'); // Ajoute si absente, retire si présente
```

---

## 🔹 6. Créer et insérer des éléments

```javascript
const nouveauParagraphe = document.createElement('p');
nouveauParagraphe.textContent = "Je suis nouveau !";

document.body.appendChild(nouveauParagraphe); // Ajout à la fin
```

Autres méthodes :
- `parentNode.insertBefore(newElement, referenceElement)`
- `element.prepend()`
- `element.append()`

---

## 🔹 7. Supprimer des éléments

```javascript
const aSupprimer = document.getElementById('a-supprimer');
aSupprimer.remove();
```

---

## 🔹 8. Gérer les événements (event listeners)

### Méthode moderne :

```javascript
const bouton = document.querySelector('#mon-bouton');

bouton.addEventListener('click', function () {
  alert('Bouton cliqué !');
});
```

### Autres événements utiles :

| Événement      | Déclenchement                    |
|----------------|----------------------------------|
| `click`        | Clic sur un élément              |
| `mouseover`    | Souris passe au-dessus           |
| `mouseout`     | Souris quitte l’élément          |
| `submit`       | Soumission d’un formulaire       |
| `keydown`      | Touche pressée au clavier        |

---

## 🔹 9. Exemple complet

### HTML

```html
<button id="changeTitre">Changer le titre</button>
<h1 id="titre">Mon Titre</h1>
```

### JS

```javascript
const bouton = document.getElementById('changeTitre');
const titre = document.getElementById('titre');

bouton.addEventListener('click', () => {
  titre.textContent = 'Titre modifié avec JavaScript !';
  titre.style.color = 'blue';
});
```

---

## 🔹 10. Bonnes pratiques

✅ Manipuler le DOM **après le chargement de la page**  
→ utiliser `DOMContentLoaded` :

```javascript
document.addEventListener('DOMContentLoaded', () => {
  // Le DOM est prêt
});
```

✅ Utiliser `querySelector`/`querySelectorAll` autant que possible  
✅ Ne pas abuser des modifications directes dans des boucles (coût en performance)

---

