# Write Hello World with ReactJS
- Type `npm uninstall react react-dom`
- Type `npm install react@17.0.2 react-dom@17.0.2`
# Desgin Trello App layout with React Hook
- Type: `npm config set legacy-peer-deps true`
- Type `npm install node-sass`
- Change file to `App.scss`
## Design App Layout
```js
function App() {
  return (
    <div className="trello-master">
      <nav className="navbar app">App bar</nav>
      <nav className="navbar board">Board bar</nav>
      <div className="board-columns">
        boad columns
      </div>
    </div>
  );
}

export default App;
```
## CSS App Layout
```scss
.trello-master {
  height: 100vh;
  display: grid;
  grid-template-rows: 40px 50px 1fr;
  line-height: 1.3em;
  background-color: $board-bg-color;
}
```
## Define global scss variables
```scss
$board-bg-color: aqua;
$gap: 10px;

.trello-master {
  height: 100vh;
  display: grid;
  grid-template-rows: 40px 50px 1fr;
  background-color: $board-bg-color;

  .navbar {
    padding-left: $gap;
    display: flex;
    align-items: center;

    &.app {

    }

    &.board {

    }
    
  }
}
```
## CSS Navigation bar
```scss
$navbar-app-bg-color: #0067a3;
$navbar-board-bg-color: #0079bf;

.navbar {
    padding-left: $gap;
    display: flex;
    align-items: center;

    &.app {
        font-size: 1.5rem;
        background-color: $navbar-app-bg-color;
    }

    &.board {
        font-size: 1.1rem;
        background-color: $navbar-board-bg-color;
    }
}
```
## Design single column
```jsx
<div className="column">
    <header>Brainstorm</header>
    <ul>
        <li>
            <img src="https://trello.com/1/cards/5e20e0e72365b93c7a291206/attachments/5e20e0e72365b93c7a291207/previews/5e20e0e72365b93c7a29120c/download/Design.png" alt="Design logo" />
            Design & Research
        </li>
        <li>second</li>
    </ul>
    <footer>Add another card</footer>
</div>
```
## CSS single column
```scss
$list-bg-color: #ebecf0;
$gap: 10px;
$column-header-height: 36px;
$column-footer-height: 36px;
$column-border-radius: 5px;

.column {
    flex: 0 0 auto;
    width: 300px;
    height: calc(100% - #{$gap});

    > * {
        background-color: $list-bg-color;
        color: #333;
        padding: 0 8px;
    }

    header {
        padding-left: 15px;
        height: $column-header-height;
        line-height: $column-header-height;
        font-size: 16px;
        font-weight: bold;
        border-top-left-radius: $column-border-radius;
        border-top-right-radius: $column-border-radius;
    }

    footer {
        padding-left: 10px;
        height: $column-footer-height;
        line-height: $column-footer-height;
        border-bottom-left-radius: $column-border-radius;
        border-bottom-right-radius: $column-border-radius;
    }
}
```
## CSS li, img tags
```scss
$card-border-radius: 3px;

ul {
    list-style-type: none;
    margin: 0;
    max-height: calc(100% - #{$column-header-height} - #{$column-footer-height});
    overflow-y: auto;

    li {
        background-color: white;
        padding: $gap;
        border-radius: $card-border-radius;
        box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);

        &:not(:last-child) {
            margin-bottom: $gap;
        }

        img {
            display: block;

            width: calc(100% + 2 * #{$gap});
            margin: -$gap 0 $gap (-$gap);

            border-top-left-radius: $card-border-radius;
            border-top-right-radius: $card-border-radius;
        }
    }
}
```
## Scroll vertical
```scss
&::-webkit-scrollbar {
    -webkit-appearance: none;
}

&::-webkit-scrollbar:vertical {
    width: 11px;
}
```
## Customize oy-scroll 
```scss
&::-webkit-scrollbar-thumb {
    background-color: darken($color: $list-bg-color, $amount: 15);
    border-right: 5px solid $list-bg-color;
}
```
## Customize ox-scroll
```scss
gap: 10px;
overflow-x: auto;

&::-webkit-scrollbar {
    -webkit-appearance: none;
}

&::-webkit-scrollbar:horizontal {
    height: 11px;
}

&::-webkit-scrollbar-thumb {
    background-color: rgba(255, 255, 255, .24);
    border-radius: 5px solid $list-bg-color;
}
```