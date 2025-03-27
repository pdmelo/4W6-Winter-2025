# 🛤️3.3 `useEffect` Hook Exercise

## 🎯 Objectives

1. **Understand** what the `useEffect` Hook is and why it is used in React.
2. **Use** the `useEffect` Hook to perform side effects in a functional component.
3. **Modify** a React component to fetch and display data dynamically.

## 🔨 Setup

1. We will continue using the same folder as the last exercise `3-react`.
2. Start Docker Desktop.
3. All our dependencies are already installed.
4. In VS Code, hit `CMD/CTRL + SHIFT + P` and search + run `dev container: open folder in container`.
5. In the terminal of VS Code, hit the `+` icon to open a new terminal instance.
6. Navigate to the client folder.
7. Start the React server: `npm run dev`.

## Part 1: Understanding `useEffect` in React

The `useEffect` Hook allows you to **perform side effects** in function components. 

In React, a **side effect** refers to any operation that affects something outside the function’s scope or lifecycle. This includes things like:

- Fetching data from an API
- Updating the DOM manually
- Setting up subscriptions (e.g. event listeners)
- Updating local storage
- Changing the document title

### Why are Side Effects Important?

- React components should be **pure functions**, meaning they return the same output for the same input without modifying anything outside their scope.
- However, some operations (like fetching data) **must happen outside the rendering process**—this is where **side effects** come in.

- `useEffect` is run after the first render and after every update.

- If `useEffect` returns a function, then that function is treated as a "cleanup" operation that React will call when the component unmounts. 

  - But, since it is run after every render, it also cleans up effects from the previous render before running effects the next time.

### **When Would You Use `useEffect`?**

  - **Fetching data from an API** when a component mounts.

  - **Setting up event listeners** (like `window.addEventListener`).

  - **Performing cleanup tasks** (like clearing timers) when a component unmounts.

    

### **🔹`useEffect` Syntax**
#### 🔹Basic Syntax

```jsx
useEffect(() => {
    // Code to run
});
```
👉 The function inside `useEffect` **runs after the component renders**.

-------

#### **🔹 `useEffect` with No Dependencies** (Runs on Every Render)
```jsx
useEffect(() => {
  console.log("Component rendered!");
});
```
👉Runs on:
-  Initial mount
- Every state/prop update

>[!Caution]
>Avoid infinite loops! If the effect updates state, it will cause a re-render and repeat infinitely.
-------
#### **🔹 `useEffect` with an Empty Dependency Array** (Runs Once on Mount)

```jsx
useEffect(() => {
    // Code to run
}, []);
```
👉**Runs only once** when the component **mounts** (like `componentDidMount` in class components).

- Great for **fetching data** or **event listeners**.

-------
#### 🔹 `useEffect` with Dependencies** (Runs When Dependencies Change)

```
useEffect(() => {
    // Perform appropriate update
}, [stateVar1, stateVar2]);
```
👉**Runs only when `StateVar1` or `StateVar2`changes**.

-  Useful for watching **specific state or props**.

-------
#### 🔹 Clean up in `useEffect` (Component Unmounting)

```
useEffect(() => {
    // Perform appropriate update
    return () => {
       // Perform cleanup operation
    }
});
```
-------
## Part 2: Using `useEffect` for Logging
**Without dependencies**
Modify `App.jsx` to log a message when the component mounts.

```jsx
import { useEffect, useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Component mounted");
  }); // with no dependency means it will run on every update.

  return (
    <div className="container">
      <h1>Counter: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default App;
```
**Key Points:**

- Watch the Console on the developer tools for ***"Component Mounted"*** , every time you click on Increase, it will print the "Component Mounted" 
- `useEffect(() => { console.log("Component mounted"); })` runs **everytime there is an update**

#### **With dependencies**
Modify `App.jsx` to log a message when the component mounts.

```jsx
  useEffect(() => {
    console.log("Component mounted");
  },[]); // run only once when the component mounts
 
```
**Key Points:**

- Watch the Console on the developer tools for ***"Component Mounted"*** , there is no update on the Console everytime you click on Increase 

- The empty dependency array `[]` ensures the effect doesn’t run on updates.

- `useEffect(() => { console.log("Component mounted"); })` runs **only once when the component mounts**.

>[!Note]
>Notice the Console loges   ***"Component Mounted"*** twice. React's Strict Mode in development causes `useEffect` to execute twice((only in development) ) on mount.Open `main.jsx` to confirm the Strict mode.React unmounts and re-mounts the component immediately, causing your effect to run twice.

## Part 3. `useEffect` on  Updating on State Change

Modify `App.jsx` so that clicking the button fetches a new Pokémon.

```
import { useEffect, useState } from "react";

function App() {
  const [pokemonId, setPokemonId] = useState(1);
  const [pokemon, setPokemon] = useState(null);

  useEffect(() => {
    console.log(`Count changed: ${count}`);
  }, [count]); // Runs whenever `count` changes

   return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default App;
```
**Key Points:**

- `useEffect` runs **whenever** `**count**` **changes**.
- Clicking the button increments `pokemonId`, triggering a new API request.
- The UI updates dynamically with the fetched Pokémon.



## Part 4: Fetching Data using `useEffect` 

1. Create a `json` file `pokemonList.json` in the `public` folder. Add some data for example a list of Pokemons with id , name and type.
2. Create an new component `FetchData.jsx`.

```jsx
import { useState, useEffect } from "react";
import PokemonList from "./PokemonList";

const FetchData = () => {
	const [pokemon, setPokemon] = useState([]);

	async function fetchPokemon() {
		const response = await fetch("pokemonList.json");
		const data = await response.json();

		setPokemon(data);
	}

	useEffect(() => {
		fetchPokemon();
	}, []); //ensure its runs just once

	return (
		<div>
			<h4>List of Pokemon</h4>
			<PokemonList pokemons={pokemon} />
		</div>
	);
};

export default FetchData;
```
3. Update the `PokemonList` to now map an object instead of an array.

   ```jsx
   {props.pokemons.map((pokemon) => (
   					<li key={pokemon.id}> {pokemon.name} </li>
   				))}
   ```

   

4. Modify `App.jsx` to fetch Pokemon data  from `Fetchdata`.

**Key Points:**

- `fetch("pokemonList.json")` retrieves Pokemon data from a file..
- `useEffect` runs **once when the component mounts**.
- The `pokemon` state stores fetched data and is displayed dynamically.



## Part 5: cleanup on unmount `useEffect` 

1. Create a new component Clock.jsx. 

```jsx
import { useState, useEffect } from "react";

function Clock() {
	const [time, setTime] = useState(new Date().toLocaleTimeString());

	useEffect(() => {
		const interval = setInterval(() => {
			setTime(new Date().toLocaleTimeString());
		}, 1000);

		return () => clearInterval(interval); // Cleanup to avoid memory leaks
	}, []);

	return (
		<div>
			<p>Current Time: {time}</p>
		</div>
	);
}

export default Clock;
```

**Key Points:**

1. **Side Effect (`useEffect`)**:

   - When the component mounts, `useEffect` sets up a repeating action using `setInterval`.
   - `setInterval` runs a function every **1 second**, updating `time` with the new current time.
   - The `useEffect` dependency array (`[]`) ensures this effect runs **only once** when the component mounts.

2. **Cleanup** `clearInterval`

   - This is the **cleanup function**, which React calls when the component **unmounts**.
   - `clearInterval(interval)` stops the interval from running to prevent memory leaks or errors.
   - Without this cleanup, if the component is removed from the UI, the interval would keep running, leading to unwanted side effects

>[!Note]
> `clearInterval` is part of the `setInterval/clearInterval` pair in JavaScript.
> `setInterval` is used to repeatedly execute a function after a specified delay (in milliseconds).
> `clearInterval` is used to stop an interval that was started with `setInterval`.

Modify the `App.jsx` to include the clock component, But first declare a Boolean state, `showClock`. The Clock will be displayed on onclick of a button.

```
const [showClock, setShowClock] = useState(true);
```

We will use conditional rendering here

````jsx
 <div>
     <button onClick={() => setShowClock(!showClock)}>Toggle Clock</button>
     {showClock && <Clock />}
 </div>
````

>[!Note]
> **Conditional Rendering in React :**
>In React, conditional rendering allows us to dynamically render components or elements based on a condition. In the given App function, the component Clock is displayed based on the state variable `showClock`.
>
>- If `showClock` is true, <Clock /> is rendered.
>- If `showClock` is false, React doesn't render anything.

Once you have the clock functioning on the app. Remove the cleanup in the `useEffect`

```jsx
return () => clearInterval(interval); // remove this line.
```

**What Happens When We Click the Button?**

- Initially, the `Clock` is mounted and starts the `setInterval`, updating the time every second.

- When you click the `Toggle Clock` button:

  - The `Clock` component unmounts (disappears from the UI).

  - But the interval is still running in the background because we didn't use `clearInterval`!

- If you click the button again and re-mount the component:
  - A new interval is created.

Now two intervals are running at the same time, updating state twice per second.

If you toggle the component multiple times, intervals keep stacking up, making the clock update multiple times per second.

##  Summary

| `useEffect(() => {})`                      | Runs on every render        |
| ------------------------------------------ | --------------------------- |
| `useEffect(() => {}, [])`                  | Runs **only once** on mount |
| `useEffect(() => {}, [count])`             | Runs when `count` changes   |
| `useEffect(() => { return () => {} }, [])` | Runs cleanup on unmount     |

## 📥 Submission

Take screenshots of:

- The console log showing "Component mounted" when count increases(Without dependencies).
- The Pokemon data being displayed after fetching.


Submit all screenshots on Moodle.