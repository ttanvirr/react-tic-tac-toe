# Initial setups

## React with JavaScript + Vite

```bash
npm create vite@latest
```

Select JavaScript from the options

- Open the project directory in your code editor
- Open the terminal and install dependencies

```bash
npm install
```

#### Run the app

```bash
npm run dev
```

- Check if you see the default page by Vite React in the browser.

# The Tic Tac Toe app

#### Refactor/Clean up codes

- Remove the App.css file
- In App.jsx remove everything and paste the following codes

App.jsx

```jsx
export default function Square() {
  return <button className="square">X</button>
}
```

- In index.css replace everything with the following:

index.css

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

#### Run the app

```bash
npm run dev
```

- Check if you see the button with X in the browser

## Components

The code in App.jsx creates a component.

`In React, a component is a piece of reusable code that represents a part of a user interface.`

Let’s look at the component line by line to see what’s going on:

App.jsx

```jsx
export default function Square() {
  return <button className="square">X</button>
}
```

1. The first line defines a function called 'Square'. The `export` JavaScript keyword makes this function accessible outside of this file. The `default` keyword tells that it’s the main function in this file.

2. The second line returns a button. The `return` JavaScript keyword means whatever comes after is returned as a value to the caller of the function.

3. `<button>` is a JSX element. A `JSX` element is a combination of JavaScript code and HTML tags that describes what you’d like to display.

4. className="square" is a button `property or prop` that tells CSS how to style the button

## index.css

- This is the main css file created by vite-react

## main.jsx

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

- it is the bridge between the component you created in the App.jsx file and the web browser.
- React DOM library talk to web browsers
- the App component is imported and called here

## Building the board

Currently the board is only a single square, but we need nine! If we just try and copy paste our square to make two squares like this:

App.jsx

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

To fix this, in the App.js file, update the Square component to look like this:

App.jsx

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

App.jsx

```jsx
export default function Board() {
  //...
}
```

## Re-usable component

With how you’ve built the board so far you would need to copy-paste the code that updates the square nine times!
Instead of copy-pasting, `React’s component architecture allows you to create a reusable component to avoid messy, duplicated code.`

First, you are going to copy the line defining your first square (<button className="square">1</button>) from your Board component into a new Square component and then you’ll update the Board component to render that Square component using JSX syntax::

- Component names must start with capital letter

App.jsx

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

## Passing data through prop

To fix the current issue, you will use props to pass the value each square should have from the parent component (Board) to its child (Square).

- Update the Square component to read the `value` prop that you’ll pass from the Board:

App.jsx

```jsx
function Square({ value }) {
  return <button className="square">{value}</button>
}
```

- Props can be destructured within curley braces as function argument
- To use the variable props we again need curley braces. Curley braces are the way to 'escape into JavaScript' from JSX.
- Now we should see empty board, because the `Board` component hasn’t passed the value prop to each Square component it renders yet.
- To fix it you’ll add the value prop to each Square component rendered by the Board component:

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

## Making an interactive component (useState hook)

Let’s fill the Square component with an X when you click it.

- Declare a function called handleClick inside of the Square.
- Then, add onClick to the props of the button JSX element returned from the Square:

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
- Let’s store the current value of the Square in state, and change it when the Square is clicked.

- Import useState at the top of the file.
- Remove the value prop from the Square component. Instead, add a new line at the start of the Square that calls useState. Have it return a state variable called value:

**App.jsx**

```jsx
import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    //...
```

- `value` stores the value and `setValue` is a function that can be used to change the value. The null passed to useState is used as the initial value for this state variable.

- Since the Square component no longer accepts props anymore, you’ll remove the value prop from all nine of the Square components created by the Board component:

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

- Now you’ll change Square to display an “X” when clicked.
- Replace the console.log("clicked!"); event handler with setValue('X');.

**App.jsx**

```jsx
function handleClick() {
  setValue("X")
}
```

- By calling this set function from an onClick handler, you’re telling React to re-render that Square (with value= 'X') whenever its <button> is clicked.
- Click on any Square, and “X” should show up.
- Each Square has its own state: the value stored in each Square is completely independent of the others.

## React Developer Tools
