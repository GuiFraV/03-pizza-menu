## Composants de l'application de la Pizzeria
### 👉 [LIVE PREVIEW ICI](https://03-pizza-menu-omega.vercel.app/, 'Menu pizza en ligne') | <a href="https://03-pizza-menu-omega.vercel.app/" target="_blank">LIVE PREVIEW ICI</a> 👈


L'application est structurée autour de plusieurs composants qui permettent de représenter différentes parties de l'interface utilisateur
## 🍕 Table des matières 🍕

  1. [Composant App](#1-composant-app)
  
  2. [Composant Header](#2-composant-header)
  
  3. [Composant Menu](#3-composant-menu)
  
  4. [Composant Footer](#4-composant-footer)
  
  5. [Composant Pizza](#5-composant-pizza)
  
  6. [Rendu de l'application](#6-rendu-de-lapplication)
  
  7. [Rendu avec React avant la version 18](#7-rendu-avec-react-avant-la-version-18)
  
  8. [Données des Pizzas](#8-données-des-pizzas)
  
  9. [Améliorations du composant Menu](#9-améliorations-du-composant-menu)
  
  10. [Améliorations du composant Footer](#10-améliorations-du-composant-footer)

  11. [Styles et CSS](#11-styles-et-css)

  12. [Gestion des Pizzas Épuisées](#12-gestion-des-pizzas-épuisées)

  13. [Améliorations du composant Menu](#13-améliorations-du-composant-menu)

  14. [Améliorations du composant Footer](#14-améliorations-du-composant-footer)

  15. [Styles et CSS (Mise à jour)](#15-styles-et-css-mise-à-jour)

### 1. **Composant App**:
Le composant App est le point d'entrée de l'application. Il structure l'ensemble de l'application en combinant les composants **`<Header>`**, **`<Menu>`** et **`<Footer>`**.

```javascript
function App() {
    return (
        <div>
            <Header />  
            <Menu />
            <Footer />
        </div>
    );
}
```
### 2. **Composant Header**:
Ce composant affiche simplement le titre de l'application, représentant le nom de la pizzeria.
```javascript
function Header() {
    return <h1>Fast React Pizza Co.</h1>
}
```
### 3. **Composant Menu**:
Ici, je montre le menu de la pizzeria. Pour le moment, il affiche quatre pizzas identiques, mais idéalement, chaque instance de Pizza représenterait une pizza différente.

```javascript
function Menu() {
    return (
        <div>
            <h2>Our menu</h2>
            <Pizza />
            <Pizza />
            <Pizza />
            <Pizza />
        </div>
    )
}
```

### 4. **Composant Footer**:
Ce composant affiche l'heure actuelle et indique si la pizzeria est actuellement ouverte ou fermée.

```javascript
function Footer() {
    const hour = new Date().getHours();
    const openHour = 12;
    const closeHour = 22;
    const isOpen = hour >= openHour && hour <= closeHour
    return <footer>{new Date().toLocaleTimeString()}. We're currently open !</footer>
}
```

### 5. **Composant Pizza**:
Chaque instance de ce composant représente une pizza. Actuellement, il affiche des détails fixes sur la "Pizza Margherita", mais il pourrait être étendu pour afficher des informations sur différentes pizzas.

```javascript
function Pizza(){
    return ( 
        <div>
            <img src='pizzas/spinaci.jpg' alt='Pizza spinaci'/>
            <h2>Pizza Margherita</h2>
            <p>Tomato and mozarella</p>
        </div> 
    );
}
```

### 6. **Rendu de l'application**:
**React v18** : Dans cette version de React, j'utilise la nouvelle API de rendu concurrentiel pour afficher mon application.

```javascript
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <React.StrictMode> 
        <App /> 
    </React.StrictMode>
);
```
- Avec React v18, une nouvelle API pour le rendu concurrentiel a été introduite. **ReactDOM.createRoot()** crée un "root" pour mon application React. Je passe l'élément DOM où je veux que mon application React soit montée, généralement un élément avec l'ID **root**.
- **root.render()** est utilisé pour rendre mon application React dans cet élément.
- **<React.StrictMode>** est un utilitaire qui vérifie les problèmes potentiels dans mon application pendant le développement. C'est une bonne pratique de l'utiliser car il peut m'aider à identifier des problèmes avant qu'ils ne deviennent de réels problèmes.

### 7. **Rendu avec React avant la version 18**:
```javascript
// React.render(<App />);
```

- Avant React v18, le rendu était plus direct. J'aurais simplement utilisé **ReactDOM.render()** pour rendre mon application. Cette ligne est commentée car elle montre comment c'était fait avant, mais elle n'est pas utilisée dans ce code.

**En résumé**, ce code est un exemple de base d'une application React qui affiche "Hello React !" dans un élément **`<h1>`**. Il montre également comment le rendu est effectué dans React v18 par rapport aux versions antérieures.

### 8. **Données des Pizzas**:

Un tableau pizzaData contient les informations sur différentes pizzas, y compris le nom, les ingrédients, le prix, le nom de la photo et un indicateur pour savoir si la pizza est épuisée ou non.

```javascript
const pizzaData = [
    {
    name: "Focaccia",
    ingredients: "Bread with italian olive oil and rosemary",
    price: 6,
    photoName: "pizzas/focaccia.jpg",
    soldOut: false,
    },
    // ... autres pizzas ...
];
```

### 9. **Améliorations du composant Menu**:

Le composant Menu a été amélioré pour afficher dynamiquement une liste de pizzas à partir du tableau pizzaData. Si aucune pizza n'est disponible, aucune liste ne sera affichée.

```javascript
function Menu() {
    const pizzas = pizzaData;
    const numPizzas = pizzas.length;

    return (
        <main className='menu'>
            <h2>Our menu</h2>
            {numPizzas > 0 &&(     
                <ul className='pizzas'>
                    {pizzas.map((pizza) => (
                        <Pizza pizzaObj={pizza} key={pizza.name}/>
                    ))}
                </ul>
            )}
        </main>
    )

```

### 10. **Améliorations du composant Footer**:

Le composant Footer a été mis à jour pour afficher un message indiquant si la pizzeria est ouverte ou fermée en fonction de l'heure actuelle. De plus, un bouton "Order" a été ajouté pour permettre aux utilisateurs de passer une commande.

```javascript
function Footer() {
    const hour = new Date().getHours();
    const openHour = 12;
    const closeHour = 22;
    const isOpen = hour >= openHour && hour <= closeHour;

    return (
        <footer className='footer'>
            <div className='order'>
                {isOpen && (
                    <p>
                        We're open until {closeHour}:00. Come visit us or order online.
                    </p>
                )}
                <button className='btn'>Order</button>
            </div>
        </footer>
    )
}
```

### 11. **Styles et CSS**:

Des classes CSS ont été ajoutées pour améliorer la mise en forme et la présentation des composants. Par exemple, la classe 'container' pour le composant App, 'header' pour le composant Header, et ainsi de suite.

```css
.container {
    max-width: 1200px;
    margin: 0 auto;
}

.header {
    background-color: #333;
    color: #fff;
    padding: 20px 0;
    text-align: center;
}

/* ... autres styles ... */
```

### 12. **Gestion des Pizzas Épuisées**:

Le composant **`Pizza`** a été amélioré pour gérer les pizzas qui sont épuisées. Si une pizza est marquée comme épuisée (avec la propriété **`soldOut`** définie sur **`true`**), elle sera affichée avec le texte "Sold out" au lieu du prix.

```javascript
function Pizza({ pizzaObj }) {
    return ( 
        <li className={ `pizza ${pizzaObj.soldOut ? 'sold-out' : ''} `}>
            <img src={pizzaObj.photoName} alt={pizzaObj.name}/>
            <div>
                <h3>{pizzaObj.name}</h3>
                <p>{pizzaObj.ingredients}</p>
                <span>{pizzaObj.soldOut ? 'Sold out' : pizzaObj.price}</span>
            </div>
        </li> 
    );
}
```
### 13. **Améliorations du composant Menu**:

Le composant **`Menu`**` a été mis à jour pour afficher un message différent en fonction du nombre de pizzas disponibles. Si aucune pizza n'est disponible, un message indiquant que le menu est en cours d'élaboration sera affiché.

```javascript
function Menu() {
    const pizzas = pizzaData;
    const numPizzas = pizzas.length;

    return (
        <main className='menu'>
            <h2>Our menu</h2>
            {numPizzas > 0  ? (    
                <>
                    <p>
                        Authentic Italian cuisine. 6 creative dishes to choose from. All
                        from our stone oven, all organic, all delicious.
                    </p>
                    <ul className='pizzas'>
                        {pizzas.map((pizza) => (
                            <Pizza pizzaObj={pizza} key={pizza.name}/>
                        ))}
                    </ul>
                </>   
            ) : <p>We're still working on our menu. Please come back later :) </p>
            }
        </main>
    )
}
```

### 14. **Améliorations du composant Footer**:

Le composant **`Footer`** a été mis à jour pour afficher les heures d'ouverture et de fermeture de la pizzeria. Un nouveau composant **`Order`** a été introduit pour afficher les informations de commande lorsque la pizzeria est ouverte.

```javascript
function Footer() {
    const hour = new Date().getHours();
    const openHour = 8;
    const closeHour = 22;
    const isOpen = hour >= openHour && hour <= closeHour;

    return (
        <footer className='footer'>
            {isOpen ? (
                <Order closeHour={closeHour} openHour={openHour} /> 
            ) : (
                <p>We're happy to welcome you between {openHour}:00 and {closeHour}:00.</p>
            )}
        </footer>
)}

function Order({ closeHour, openHour }) {
    return ( 
        <div className='order'>
            <p>
                We're open from {openHour}:00 to {closeHour}:00. Come visit us or order online.
            </p>
            <button className='btn'>Order</button>
        </div>
    );
}
```

### 15. **Styles et CSS (Mise à jour)**:

Des classes CSS supplémentaires ont été ajoutées pour gérer l'affichage des pizzas épuisées et pour améliorer la mise en forme générale.

```css
.pizza.sold-out {
    opacity: 0.5;
}

/* ... autres styles ... */
```