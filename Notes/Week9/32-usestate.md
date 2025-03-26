# 🛤️3.2 `useState` Hook Exercise

## 🎯 Objectives

1. **Understand**  what Hooks are and why they are used in React.
2. **Use** the `useState` Hook to manage state in a functional component.
3. **Modify** state dynamically using event handlers.


## 🔨 Setup

1. We will continue using the same folder as the last exercise `3-react` .
2. Start Docker Desktop
3. All Our dependencies are already installed.
4. In VS Code, hit `CMD/CTRL + SHIFT + P` and search + run `dev container: open folder in container`.
5. In the terminal of VS Code, hit the `+` icon to open a new terminal instance
6. Navigate to the `client` folder.
7. Start the react server: `npm run dev`.


## 🔍 Context: Understanding Hooks in React
[Hooks](https://pdmelo.github.io/4W6-Winter-2025/#/Notes/Week8/react?id=hooks) allow you to use the  **state** and other React **features** inside **functional components**, without needing a class component. The most commonly used Hook is `useState`, which lets functional components to store and update state.

In React, **state** refers to a component’s dynamic data—values that can change over time and trigger re-renders when updated.

State can store various types of data, such as:

- Numbers (e.g., a counter value)
- Strings (e.g., user input in a form)
- Booleans (e.g., a toggle switch state)
- Objects (e.g., user profile details)
- Arrays (e.g., a list of tasks in a to-do app)


## Part 1 : Using `useState` and Dynamic Updates
**Example 1. Using `useState` for a Counter**
Modify `App.jsx` to include state management.

1. Import `useState` from react.

   ```jsx
   import { useState } from "react";
   
   function App() {
     //declare state variable,count starts at 0
     const [count, setCount] = useState(0);
   
     return (
       <div className="container">
         <h1>Counter: {count}</h1>
         <button onClick={() => setCount(count + 1)}>Increase</button>
         <button onClick={() => setCount(count - 1)}>Decrease</button>
       </div>
     );
   }
   
   export default App;
   ```

**Key Points:**
   - `useState(0)` initializes `count` with a value of `0`.
   - **`count`** – Holds the current state value.
   - `setCount` **updates** the state when buttons are clicked.
   - **Buttons** – Clicking them updates the state, causing React to re-render the component with the new count.

**Example 2 : Changing a HTML element**
Add a toggle function to change the colour of the text to red if blue, and vice versa. Watch the change using Inspect on the browser.

   ```jsx
   import { useState } from "react";
   
   function Greeting(props) {
     const [color, setColor] = useState("green");
	
     return (
       <div>
        <h1 style={{ color: color }}>Meet my {props.name}</h1>
         <button onClick={() => setColor(color === "blue" ? "red" : "blue")}>
				Toggle Colour
			</button>
       </div>
     );
   }
   ```
**Key Points:**
- `useState` Initializes `color` state with `"green"`
- `setColor` updates it..
- **Dynamic Styling** – The `<h1>` element’s text colour is dynamically set based on the `color` state.
- Clicking "Change Name" **updates** `name` dynamically.

>[!NOTE]
>`color === "blue" ? "red" : "blue"` **can be extracted into a separate function:**
> 
	 ```jsx
	 const toggle = (color) => {
	 return color === "blue" ? "red" : "blue";
	 };

>```jsx
// this can then be called using
	<button onClick={() => setColor( toggle(color) }>
				Toggle Colour
	</button>


## Part 2: Passing State as Props
We can pass state as **props** to another component.

**Step 1: Create a `Counter` Component**

Create a new file `Counter.jsx`. 

```jsx
import React from "react";

export default function Counter({ count }) {
	return <p>Counter: {count}</p>;
}
```
**Step 2: Use the `Counter` Component in `App.jsx`**

Modify `App.jsx` to pass the state as a prop:

```jsx
import { useState } from "react";
import Counter from "./Counter";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div className="container">
      <Counter count={count} />
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <button onClick={() => setCount(count - 1)}>Decrease</button>
    </div>
  );
}

export default App;
```

**Key Points:**
- `App.jsx` **manages the state** (`count`).
- `Counter`component  **receives** `count` as a prop, using `destructing` in the function, so it can accesses `count` directly instead of using `props.count`
- State is **controlled in `App.jsx`** but can be displayed anywhere using props.
- The curly brackets {} in JSX (count={count}) tell React that count is a JavaScript expression and should be evaluated.


## Part 3: Event Listeners in React

Event listeners allow React components to **respond to user actions**, such as clicks, mouse movements, or key presses. Events in React are similar to JavaScript, but use **camelCase** for event names.

**Updating State Dynamically with user input**

Modify `App.jsx` to include a text input field that updates a Pokemon’s name.

```jsx
import { useState } from "react";

function App() {
  const [name, setName] = useState("Charmander");

  return (
    <div className="container">
      <h1>Meet my Pokemon: {name}</h1>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
    </div>
  );
}

export default App;
```

**Key Points:**

- `useState("Charmander")` initializes the Pokemon name.

- The input field updates `name` whenever a user types.

> [!NOte]
>
> (e) => setName(e.target.value)  This is a callback function and it could be extracted into its own function within the same component .For example:
>
> ```jsx
> const eventhandler = (e) => {
> 
> setName(e.target.value)
> 
> };
> ```
>
> 
>
> ```jsx
> <input type="text" value={name} onChange={evenHandler} />
> ```




##  Part 4 Working with Lists and Hooks

1. **Without a Component**

Modify `App.jsx` to use `useState` for a **Pokemon list** and update it dynamically.

```jsx
import { useState } from "react";

function App() {
  const [myPokemons, setMyPokemons] = useState([
    "Charmander",
    "Bulbasaur",
    "Squirtle",
  ]);

  //event handler to add new value to existing array of pokemons  
  const addPokemon = () => {
    setMyPokemons([...myPokemons, "Pikachu"]);
  };

  return (
    <div className="container">
      <h1>My Pokemons</h1>
      <PokemonList pokemons={myPokemons} />
      <button onClick={() => addPokemon()}>Add Pikachu</button>
    </div>
  );
}

export default App;
```
**Key Points:**
- `useState` initializes `myPokemons` as an array.
- Clicking the button adds "Pikachu" to the list.

##  Part 5 [TODO]
Make the Pokemon list more dynamic **With a Input Field** 

Modify `App.jsx` to use the **Part 3** to accept a pokemon from the user and add it to the list.

## Part 6 [TODO]
Modify App.jsx to include an event listener that changes the background color when a button is clicked.

## 📥 Submission

Take screenshots of:

- The app displaying a counter with `useState`.
- The app updating state dynamically  changing the Pokemon name).
- The app dynamically adding to the list of Pokemons.
- The app dynamically changing background color on click of a button

Submit all screenshots on Moodle.

