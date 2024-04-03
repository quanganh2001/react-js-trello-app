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

We divide the app into 3 parts, a container with
- nav app (1)
- nav board (2)
- board columns (3)

It's time to write some CSS code to make our App layout
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

100vh: set the container's height equal to your screen's height (vh - view height)

A simple question to ask yourself when deciding between grid or flexbox is:
- do I only need to control the layout by row or column - use a flexbox
- do I need to control the layout by row and column - use a grid

we use grid layout with (each item is a row)
- first nav: height = 40px;
- second nav: height = 50px;
- the third div: height = 1fr, means that it's height = available space. ( = 100vh - 40px - 50px)

line-height to increase the div's height.
## Define global scss variables
Define scss variables at the top, so if we need to change the css, we only need the code here.
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
board-columns include many single column. Each column has:
- title (eg: brain storm) -> use header tag
- an unlist to show all todo list. Each li tag is a todo
- a footer: does the action "add new todo"

sometime a column has an image first, let's create an image at the top of each card.
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

`height: calc(100% - #{$gap})`: set a height for `.column`

We calculate the 'single column height, by taking its parent height (100% of `div.board-columns`), then minus $gap (=10px)

`> *` means select all child elements recursively.
## CSS li, img tags
- The `list-style-type` specifies the type of `list-item` marker in a list.
- set to none to remove bullets from ul lists
- We many have many todos (each todo is a li tag), so set `overflow-y: auto` for this (enable a vertical scroll)
- each li tag, we set background color to white.
- With li tags, we set padding to have more space. Add margin to distinguish them.
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
- `&:not(:last-child)` to NOT apply 'CSS' to the last `li` tag.
- In this case, we don't want the last `li` tag has a `margin: 10px;` with the footer.
- `display: block` to take up the whole width.

We do the trick here:
- first: calculate the image width, by increasing x2 `$gap` => set the image's width equal the `li` tag.

We must do this, cuz the `li` tag use a padding: (x2 $gap = padding left + padding right)
- second: to remove the `padding-top` and the `padding-left` (lit tag has `padding: $gap`), use the negative margin.
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
- We use `webkit-scrollbar` in order to customizing the scrollbar. Use `webkit-appearance: none` to hide the 'original scroll'.
- `-webkit-scrollbar:vertical` => to make a vertical scroll. Set width of the new scroll is 11px.
- `-webkit-scrollbar-thumb`: the draggable scrolling handle => set color.
- Do the trick with `border-right`
  - by setting this property, the 'showing scroll` width = 'original scroll' - 'border right width'.
  - In this case: scroll width = 11px (original) - 5px => new scroll's width = 7px;
You can change `border-right` color to see the difference.
## Customize ox-scroll
We CSS the ox-scroll like th same with the oy-scroll, only need to use 'horizontal', and set the height for ox-scroll.
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