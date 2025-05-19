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
