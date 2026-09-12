# Table of contents <!-- omit in toc -->

- [1. Initial setups](#1-initial-setups)
  - [1.1. React with JavaScript + Vite](#11-react-with-javascript--vite)
      - [1.1.0.1. Run the app](#1101-run-the-app)
- [2. The Tic Tac Toe app](#2-the-tic-tac-toe-app)
  - [2.1. Refactor/Clean up codes](#21-refactorclean-up-codes)
  - [2.3. Components](#23-components)
  - [2.4. index.css](#24-indexcss)
  - [2.5. main.jsx](#25-mainjsx)
  - [2.6. Building the board](#26-building-the-board)
  - [2.7. Re-usable component](#27-re-usable-component)
  - [2.8. Passing data through prop](#28-passing-data-through-prop)
  - [2.9. Making an interactive component (useState hook)](#29-making-an-interactive-component-usestate-hook)
  - [2.10. React Developer Tools](#210-react-developer-tools)
  - [2.11. Lifting state up](#211-lifting-state-up)
  - [2.12. Why immutability is important](#212-why-immutability-is-important)

# 1. Initial setups

## 1.1. React with JavaScript + Vite

```bash
npm create vite@latest
```

Select JavaScript from the options

- Open the project directory in your code editor
- Open the terminal and install dependencies

```bash
npm install
```

#### 1.1.0.1. Run the app

```bash
npm run dev
```

- Check if you see the default page by Vite React in the browser.

# 2. The Tic Tac Toe app

## 2.1. Refactor/Clean up codes

- Remove the App.css file
- In App.jsx remove everything and paste the following codes

`App.jsx`

```jsx
export default function Square() {
  return <button className="square">X</button>
}
```

- In `index.css` replace everything with the following:

```css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

h1 {
  margin-top: 0;
  font-size: 22px;
}

h2 {
  margin-top: 0;
  font-size: 20px;
}

h3 {
  margin-top: 0;
  font-size: 18px;
}

h4 {
  margin-top: 0;
  font-size: 16px;
}

h5 {
  margin-top: 0;
  font-size: 14px;
}

h6 {
  margin-top: 0;
  font-size: 12px;
}

code {
  font-size: 1.2em;
}

ul {
  padding-inline-start: 20px;
}

* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: "";
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

- Run the app

  ```bash
  npm run dev
  ```

- Check if you see the button with `X` in the browser

## 2.3. Components

The code in `App.jsx` creates a component.

`In React, a component is a piece of reusable code that represents a part of a user interface.`

Let’s look at the component line by line to see what’s going on:

`App.jsx`

```jsx
export default function Square() {
  return <button className="square">X</button>
}
```

1. The first line defines a function called 'Square'. The `export` JavaScript keyword makes this function accessible outside of this file. The `default` keyword tells that it’s the main function in this file.

2. The second line returns a button. The `return` JavaScript keyword means whatever comes after is returned as a value to the caller of the function.

3. `<button>` is a JSX element. A `JSX` element is a combination of JavaScript code and HTML tags that describes what you’d like to display.

4. className="square" is a button `property or prop` that tells CSS how to style the button

## 2.4. index.css

- This is the main css file created by vite-react

## 2.5. main.jsx

```jsx
import { StrictMode } from "react"
import { createRoot } from "react-dom/client"
import "./index.css"
import App from "./App.jsx"

createRoot(document.getElementById("root")!).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

- it is the bridge between the component you created in the `App.jsx` file and the web browser.
- React DOM library talk to web browsers
- the App component is imported and called here

## 2.6. Building the board

Currently the board is only a single square, but we need nine! If we just try and copy paste our square to make two squares like this:

`App.jsx`

```jsx
export default function Square() {
  return <button className="square">X</button><button className="square">X</button>;
}
```

You'll get an error.

- React components need to return a single JSX element and not multiple adjacent JSX elements like two buttons.
- To fix this you can use any wrapper element like `<div>` or Fragments (<> and </>) to wrap multiple adjacent JSX elements like this:

App.jsx

```jsx
<>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
  <button className="square">X</button>
</>
```

We created nine buttons.

But The squares are all in a single line, not in a grid like you need for our board.

To fix this, in the `App.js` file, update the Square component to look like this:

`App.jsx`

```jsx
export default function Square() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>

      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>

      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  )
}
```

- the className `board-row` is defined in index.css
- Now we have our tic-tac-toe board
- At this point let's rename out component as Board instead of Square (that makes sense)

`App.jsx`

```jsx
export default function Board() {
  //...
}
```

## 2.7. Re-usable component

With how you’ve built the board so far you would need to copy-paste the code that updates the square nine times!
Instead of copy-pasting, `React’s component architecture allows you to create a reusable component to avoid messy, duplicated code.`

First, you are going to copy the line defining your first square (`<button className="square">1</button>`) from your `Board` component into a new `Square` component and then you’ll update the `Board` component to render that `Square` component using JSX syntax:

> [!NOTE]
> Component names must start with capital letter

`App.jsx`

```jsx
function Square() {
  return <button className="square">1</button>
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>

      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>

      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  )
}
```

Oh no! Now each square says “1”.

## 2.8. Passing data through prop

To fix the current issue, you will use props to pass the value each square should have from the parent component (`Board`) to its child (`Square`).

Update the `Square` component to read the `value` prop that you’ll pass from the `Board`:

`App.jsx`

```jsx
function Square({ value }) {
  return <button className="square">{value}</button>
}
```

- Props can be destructured within curley braces as function argument
- To use the variable props we again need curley braces. Curley braces are the way to 'escape into JavaScript' from JSX.
- Now we should see empty board, because the `Board` component hasn’t passed the value prop to each `Square` component it renders yet.
- To fix it you’ll add the value prop to each `Square` component rendered by the `Board` component:

App.jsx

```jsx
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>

      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>

      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  )
}
```

Now you should see a grid of numbers again:

![alt text](doc_images/image01.png)

## 2.9. Making an interactive component (useState hook)

Let’s fill the `Square` component with an `X` when you click it.

- Declare a function called `handleClick` inside of the `Square`.
- Then, add `onClick` to the props of the button JSX element returned from the Square:

```jsx
function Square({ value }) {
  function handleClick() {
    console.log("clicked")
  }

  return (
    <button className="square" onClick={handleClick}>
      {value}
    </button>
  )
}
```

If you click on a square now, you should see a log saying "clicked!" in the Console tab of the Browser Dev Tool.

- As a next step, you want the Square component to “remember” that it got clicked, and fill it with an “X” mark. To “remember” things and update values, components use `state`.

- React provides a special function called `useState` that you can call from your component.
- Let’s store the current value of the `Square` in state, and change it when the `Square` is clicked.

- Import `useState` at the top of the file.
- Remove the `value` prop from the `Square` component. Instead, add a new line at the start of the `Square` that calls `useState`. Have it return a state variable called `value`:

**App.jsx**

```jsx
import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    //...
```

- `value` stores the value and `setValue` is a function that can be used to change the value. The null passed to `useState` is used as the initial value for this state variable.

- Since the `Square` component no longer accepts props anymore, you’ll remove the value prop from all nine of the `Square` components created by the `Board` component:

**App.jsx**

```jsx
// ...

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>

      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>

      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  )
}
```

- Now you’ll change `Square` to display an `“X”` when clicked.
- Replace the `console.log("clicked!");` event handler with `setValue('X');`.

**App.jsx**

```jsx
function handleClick() {
  setValue("X")
}
```

- By calling this set function from an onClick handler, you’re telling React to re-render that Square (with value= 'X') whenever its `<button>` is clicked.
- Click on any square, and `“X”` should show up.
- Each square has its own state: the value stored in each square is completely independent of the others.

## 2.10. React Developer Tools

React Developer Tools let you check the props and the state of your React components. It is available as a Chrome, Firefox, and Edge browser extension.

After you install the extension, a new `Components` tab will appear in your browser Developer Tools for sites using React.

To inspect a particular component on the screen, use the inspect button in the top left corner of the Components tab.

## 2.11. Lifting state up

Currently, each `Square` component maintains a part of the game’s state. To check for a winner in a tic-tac-toe game, the `Board` would need to somehow know the state of each of the 9 `Square` components.

the best approach is to store the game’s state in the parent `Board` component instead of in each `Square`. The `Board` component can tell each `Square` what to display by passing a prop.

> [!NOTE]
> To collect data from multiple children, or to have two child components communicate with each other, declare the shared state in their parent component instead. The parent component can pass that state back down to the children via props. This keeps the child components in sync with each other and with their parent.

Let's edit the `Board` component so that it declares a state variable named `squares` that defaults to an array of 9 nulls corresponding to the 9 squares:

**App.jsx**

```jsx
// ...
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    // ...
  );
}
```

Now your `Board` component needs to pass the value prop down to each `Square` that it renders:

**App.jsx**

```jsx
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null))
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} />
        <Square value={squares[1]} />
        <Square value={squares[2]} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} />
        <Square value={squares[4]} />
        <Square value={squares[5]} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} />
        <Square value={squares[7]} />
        <Square value={squares[8]} />
      </div>
    </>
  )
}
```

Next, edit the `Square` component to receive the value prop from the `Board` component. Remove the `Square` component’s own stateful tracking of value and the button’s `onClick` prop:

**App.jsx**

```jsx
function Square({ value }) {
  return <button className="square">{value}</button>
}
```

At this point you should see an empty tic-tac-toe board.

Next, you need to change what happens when a Square is clicked.

_Since state is private to a component that defines it, you cannot update the `Board`’s state directly from `Square`._

Instead, you’ll pass down a function from the `Board` component to the `Square` component, and you’ll have `Square` receive that function as props and call it when a square is clicked.

**App.jsx**

```jsx
function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  )
}
```

Now you’ll connect the `onSquareClick` prop to a function in the `Board` component, named `'handleClick'`. Then define the function to update squares array.

`App.jsx`

```jsx
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null))

  function handleClick() {
    const nextSquares = squares.slice()
    nextSquares[0] = "X"
    setSquares(nextSquares)
  }

  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={handleClick} />
        // ...
      </div>
      // ...
    </>
  )
}
```

The `handleClick` function creates a copy of the squares array (`nextSquares`) with the JavaScript `slice()` Array method.

Your `handleClick` function is hardcoded to update the index for the upper left square (0). Let’s update `handleClick` to be able to update any square.

```jsx
// ...
function handleClick(i) {
  const nextSquares = squares.slice()
  nextSquares[i] = "X"
  setSquares(nextSquares)
}
// ...
```

Next, you will need to pass that `i` to `handleClick`.

```jsx
<Square value={squares[0]} onSquareClick={handleClick(0)} />
```

`But this doesn’t work.` The `handleClick(0)` will call the function too early before the click. Eventually, this will lead to an infinite loop.

Let’s fix this and update all Square calls:

```jsx
export default function Board() {
  // ...
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  )
}
```

Notice the new `() =>` syntax. When the square is clicked, the code after the `=>` “arrow” will run.

Now you can again add X’s to any square on the board by clicking on them. But this time all the state management is handled by the `Board` component!

> [!NOTE]
> The `<button>` element is a built-in component and its `onClick` property is also buit-in. For custom components like `Square`, you could give any name to the `Square`’s `onSquareClick` prop or Board’s `handleClick` function. In React, it’s conventional to use `onSomething` names for props which represent events and `handleSomething` for the function definitions which handle those events.

## 2.12. Why immutability is important
