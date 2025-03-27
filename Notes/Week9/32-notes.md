# 🛤️3.2 useState Notes

## React Components with Hooks



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

### 2. **With a Input Field[TODO]

Create a new component called `PokemonList.jsx` in a separate file. Now modify `App.jsx` to use this component

```jsx
import { useState } from "react";
import PokemonList from "./PokemonList";

function App() {
    const [newPoke, setPoke] = useState("");
	const [myPokemons, setMyPokemons] = useState(["Charmander", "Bulbasaur", "Squirtle"]);

	const addPokemon = (newPoke) => {
		setMyPokemons([...myPokemons, newPoke]);
		setPoke(""); //Clear input after adding.
	};

	return (
		<div className="container">
			<h1>My Pokemons</h1>
			<PokemonList pokemons={myPokemons} />
			<br />
				<input
					type="text"
					value={newPoke}
					onChange={(e) => setPoke(e.target.value)}
				/>
				<button onClick={() => addPokemon(newPoke)}>Add Pokemon</button>
		</div>
	);
}

export default App;

```

## 📌 Part 6: Background colour [TODO]

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

**Conditional rendering.**

```
- Conditional rendering (`{pokemon ? (...) : <p>Loading...</p>}`) ensures we show a loading message before data is available.
```

**Example on show buton** 

```
const [showUpdate, setShowUpdate] = useState(false);

const onSave = () => {
    setShowUpdate(true); // Trigger component visibility
};

return (
    <div>
        <button onClick={onSave}>Edit</button>
        {showUpdate && <UpdateTodo todo={todo} />}
    </div>
);

```

