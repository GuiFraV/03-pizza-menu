## Composants de l'application de la Pizzeria

L'application est structurée autour de plusieurs composants qui permettent de représenter différentes parties de l'interface utilisateur

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
### 2. **Composant Headert**:
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