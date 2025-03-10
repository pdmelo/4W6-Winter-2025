# 🛤️3.1 JSX Exercise

## 🎯 Objectives

1. **Understand** the basics of jsx syntax in a React application using React .

2. **Create** Single pages and display content.

3. **Implement** components using Classes and Functiions.

------
## 🔨 Setup

1. Open a terminal and navigate to your project folder: `~/web-ii/exercises/`.
2. Run `npx create-react-app 2.2-jsx-routing --template typescript` to generate a new React project with TypeScript.
3. Navigate into the project folder: `cd 2.2-jsx-routing`.
4. Install React Router: `npm install react-router-dom`.
5. Start the project: `npm start`.

------

## 📌 Part 1: Understanding the JSX Syntax

The `App.jsx` is the entry point to the React application.

1. The `<hgroup>` tag is **used to surround a heading and one or more <p> elements**.
1. Open `src/App.jsx`and and declare a variable `name` with a value and replace the h1 html tag,  see example below:

	```jsx
	import React from "react";
	
	function App = () => {
	  const name = "Pokemons!";
	  return (
	    <div>
	      <h1>Meet my {name}</h1>
       </div>
	  );
	};
	
	export default App;
	```
2. You can also embed styles in the html, lets make the name italics and add colour to it. Notice the **double curly brackets** on the style, that is because you're returning an object. So the outer `{}` brackets are for returning a variable, and the inner `{}` brackets are for creating an object.

   ```jsx
   <h1>Meet the <i style={{color:"SteelBlue"}}>{name}</i></h1>
	```

3. We could add other html tags like a button

   ```jsx
   <button className="outline" onClick={()=> alert('Hi there')}>Click Me</button>
	```
**Key Points:**

- JSX allows embedding JavaScript expressions within curly braces `{}`.
- It’s used to render HTML-like elements inside the JavaScript code.

## 📌 Part 2: Creating Reusable Components
There are 3 different way of using  Components in React. We will look at two today.

### **Method 1 : Class Components**
A React component can be created using a class. The class name should start with an uppercase letter and extend `React.Component`

```
class Welcome extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return <h1>Meet my {this.props.name}</h1>;
	}
}
```
Now replace the h1 tag in the `App()` function with the Component class, delete the earlier declation of the variable `name`
```
<Welcome name="Pokemons" />
```

### **Method 2. Functional Components**

​	Functional components are simpler and are commonly used in modern React development.

```jsx
function Greeting(props) {
	return <h1>Hello {props.name}</h1>;
}
```
** Key Points:**

- The `Hello` component accepts a `name` prop and dynamically displays the greeting message.
- Props allow components to receive dynamic values.

Added the new function in the `App` function, your end result would look like this. 

```jsx
return (
		<div className="container">
			<article>
				<hgroup>
					<Welcome name="Pokemons" />
					<Greeting name="Pikachu" />
					<p>
						Each with <b>unique abilities </b> and                                                   personalities.<br/>
					    Together, we embark on <b>countless adventures</b> and
						face every challenge that comes our way
					</p>
					<button
						className="outline"
						onClick={() => alert("Hi there")}
					>
						Click Me
					</button>
				</hgroup>
			</article>
		</div>
	);
```
** Key Points:**

- The `Greeting` component accepts a `name` prop and dynamically displays the greeting message.
-  Props allow components to receive dynamic values.

----

## 📌 Part 3: Working with Lists and JSX

### 1. **Without using a component.**
Modify `App.js` to render a list of names

declare an  array `myPokemons` with some values. Display the `myPokemons` array in your App component without using a separate component, you can use the .map() function to render the list directly inside JSX. 

```jsx
			<ul>
			  {myPokemons.map((pokemon, index) => (
					<li key={index}>{pokemon}</li>
				))}
			</ul>

```
**Key Points:**

- The `map` function is used to iterate over the array of names and render a `Greeting` component for each name.

-----



### 2. **With Components.** [TODO]
  Declare a component function called `PokemonList`, call it in the `App` function 

  ```jsx
  <PokemonList pokemons={myPokemons} />
  ```


------
## 📥 Submission

Take screenshots of:

The app displaying the name and greeting.
The app displaying dynamic greetings for different names.
The list of Pokemons rendered from an array using a functional component.


Submit all screenshots on Moodle.
