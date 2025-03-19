# 🛤️3.1 JSX Exercise

## React Components with Hooks

## 🎯 Objectives

1. **Understand** what Hooks are and why they are used in React.

2. **Use** the `useState` Hook to manage state in a functional component.

3. **Modify** state dynamically using event handlers.


---

## 🔨 Setup

1. Open a terminal and navigate to your project folder: `~/web-ii/exercises/`.
2. Run `npx create-react-app 2.2-jsx-routing --template typescript` to generate a new React project with TypeScript.
3. Navigate into the project folder: `cd 2.2-jsx-routing`.
4. Install React Router: `npm install react-router-dom`.
5. Start the project: `npm start`.

---

## Components in Separate file.
1. Create a folder called components. Add a new file `Greeting.jsx`
``` jsx
  export default (props) => {
  return <h1>Hello <i>{props.name}</i></h1>
}
```

2. In `App.jsx` import the files

   ```jsx
   import Welcome from './components/Greeting';
   ```

   

3. Use the component same as before in the `App()` funciton

## 📌 Part 1: Understanding Hooks in React

Hooks allow you to **use state and other React features inside functional components**, without needing a class component. The most commonly used Hook is `useState`, which lets components store and update state.

1. **Example1 : Using `useState` variables**

   Modify `App.jsx` to include state management:

   ```jsx
   import { useState } from "react";
   
   function App() {
       //declare state variables
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
   
   ### **Key Points:**
   
   - `useState(0)` initializes `count` with a value of `0`.
   
   - `setCount` is used to **update** the state when the buttons are clicked.
   
   - Clicking "Increase" **increments** `count`, and clicking "Decrease" **decrements** it.
   
2. **Example 2 : Using `useState` variables**
   
   ```jsx
   import { useState } from "react";
   
   function Welcome() {
   	const [name, setName] = useState("Pikachu");
   
   	return (
   		<div>
   			<h1>Meet my {name}</h1>
   			<button onClick={() => setName("Charmander")}>Change Name</button>
   		</div>
   	);
   }
   ```
   
   

## 📌 Part 2: Passing State as Props

We can pass state as **props** to another component.

### **Step 1: Create a `Counter` Component**

Create a new file `Counter.jsx`:

```
export default Counter({ count }) {
	return <h1>Counter: {count}</h1>;
}
```

### 2. **Step 2: Use the `Counter` Component in `App.jsx`**

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
- `Counter` **receives** `count` as a prop and **displays it**.
- State is **controlled in `App.jsx`** but can be displayed anywhere using props.

---

## 📌 Part 3: Updating State Dynamically

### **Example: Updating State with User Input**

Modify `App.jsx` to include a text input field that updates a Pokemon’s name.

```jsx
import { useState } from "react";

function App() {
	const [name, setName] = useState("Charmander");

	return (
		<div className="container">
			<h1>Meet my Pokémon: {name}</h1>
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

- `useState("Charmander")` initializes the Pokémon name.

- The input field updates `name` whenever a user types.

-----

## 📌 Part 4: Working with Lists and Hooks

  ### 1. **Without a Component**

  Modify `App.jsx` to **use state for a Pokémon list** and update it dynamically.

```jsx
import { useState } from "react";

function App() {
	const [myPokemons, setMyPokemons] = useState(["Charmander", "Bulbasaur", "Squirtle"]);

	const addPokemon = () => {
		setMyPokemons([...myPokemons, "Pikachu"]);
	};

	return (
		<div className="container">
			<h1>My Pokémons</h1>
			<ul>
				{myPokemons.map((pokemon, index) => (
					<li key={index}>{pokemon}</li>
				))}
			</ul>
			<button onClick={addPokemon}>Add Pikachu</button>
		</div>
	);
}

export default App;

```

### **Key Points:**

- `useState` initializes `myPokemons` as an array.
- Clicking the button adds "Pikachu" to the list.

### 2. **With a Component** [TODO]

Create a new component called `PokemonList.jsx` in a separate file. Now modify `App.jsx` to use this component

```jsx
import { useState } from "react";
import PokemonList from "./PokemonList";

function App() {
	const [myPokemons, setMyPokemons] = useState(["Charmander", "Bulbasaur", "Squirtle"]);

	const addPokemon = () => {
		setMyPokemons([...myPokemons, "Pikachu"]);
	};

	return (
		<div className="container">
			<h1>My Pokémons</h1>
			<PokemonList pokemons={myPokemons} />
			<button onClick={addPokemon}>Add Pikachu</button>
		</div>
	);
}

export default App;

```

## 📌 Part 5: Event Listeners in React

### **Understanding Event Listeners**

Event listeners allow React components to **respond to user actions**, such as clicks, mouse movements, or key presses.

### **Example: Handling Click Events**

Modify `App.jsx` to include an event listener that changes the background color when a button is clicked.

```jsx
import { useState } from "react";

function App() {
	const [bgColor, setBgColor] = useState("white");

	const changeColor = () => {
		const colors = ["red", "blue", "green", "yellow", "purple"];
		const randomColor = colors[Math.floor(Math.random() * colors.length)];
		setBgColor(randomColor);
	};

	return (
		<div className="container" style={{ backgroundColor: bgColor, padding: "20px" }}>
			<h1>Click the button to change background color</h1>
			<button onClick={changeColor}>Change Color</button>
		</div>
	);
}

export default App;

```

**Key Points:**

- `onClick` listens for button clicks.
- `changeColor` picks a random color and updates the state.
- The background color changes dynamically based on state updates.

- bgColor is the state variable that holds the current background color.
- setBgColor is the function that updates bgColor.
- The initial color is "white", as set by useState("white").
- When the changeColor function is called (on button click), it updates bgColor with a new random color.

---

## 📥 Submission

Take screenshots of:
 The app displaying a counter with `useState`.
 The app updating state dynamically (e.g., changing the Pokémon name).
 The app rendering a list of Pokémons, both with and without a component.

Submit all screenshots on Moodle.
