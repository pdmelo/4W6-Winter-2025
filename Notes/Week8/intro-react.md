# React

**MVC (Model-View-Controller)** is a design pattern for organizing code.<br>
**Model:** Manages data and business logic.<br>
**View:** Responsible for presenting data to the user.<br>
**Controller:** Handles user inputs and updates the Model & View.

## Understanding the View in MVC
- The **View** is the UI layer that displays data to the user.
- It gets updates from the **Model** and re-renders accordingly.
- Common implementation: Server-rendered templates (e.g., EJS, Handlebars).
- **Limitations:**
    - Full-page reloads required for updates.
    - Less interactive and slower for dynamic content.

As web applications became more complex, traditional Views became inefficient. The rise of Single-Page Applications (SPAs) helped create more dynamic experiences.<br>

**Key requirements:**

   - Efficient updates without full-page reloads.
   - Better user experience with smooth interactions.
   - Maintainable and reusable UI components.

## ⚛️ Meet React - Modern solution for the View

- A JavaScript library for building **interactive UIs**. .
- Developed by **Facebook (Meta)**.
- Instead of server-rendered templates, React uses components to manage Views dynamically.
- Efficient with **Virtual DOM**.
- Used for **single-page applications (SPA)**.

- Why Use React?
	- **Reusability**: Build UI components once and use them everywhere. 
	- **Performance**: Efficient updates with Virtual DOM. 
	- **Community Support**: Large ecosystem & many tools. 
	- **Declarative UI**: Focus on **what** to render, not **how**.
	- **Strong Ecosystem**: Works with frameworks like Next.js.

**React vs Traditional Views**

| Feature       | Traditional View      | React View                         |
| ------------- | --------------------- | ---------------------------------- |
| Rendering     | Server-side templates | Client-side rendering              |
| Performance   | Page reloads          | Efficient updates with Virtual DOM |
| Interactivity | Limited               | High (components, event handling)  |
| Reusability   | Difficult             | Component-based                    |

**Example: traditional template vs a React component**

```html
<!-- Traditional Server-side Template (EJS) -->
<h1>Hello, <%= user.name %>!</h1>

// React component
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```
**Explanation:**
-  Traditional templates rely on server-side rendering and require full page reloads.
-  React components render dynamically on the client without reloading.


## ⚙️ React Core Concepts
- **Components:** Reusable UI building blocks.
- **JSX:** Combines JavaScript and HTML-like syntax.
- **State & Props:** Manage dynamic data.
- **Virtual DOM:** Efficient rendering.
- **Hooks:** Modern way to handle state and side effects.



### 🏗 Components

- The **building blocks** of React apps.
- Encapsulated, reusable pieces of UI.
- Two types:
  - **Functional Components** (modern, recommended)
  - **Class Components** (older, still supported)

**Example Functional Component:**

```jsx
const Welcome = () => {
  return <h1>Hello, React!</h1>;
};
```

------



### 📜 JSX: JavaScript + XML

- A **syntax extension** for JavaScript  that allows writing UI elements using an HTML-like syntax.
- **Not a template language**—Transpiled by Babel to standard JS.

Example:

```jsx
const element = <h1>Welcome to React!</h1>;
```

Traditional JavaScript (without JSX):

```jsx
const element = React.createElement('h1', null, 'Welcome to React!');
```

JSX makes code more readable and maintainable!

------

### 🔄 Props & State

#### 🎒 Props (Properties)

- Used to **pass data** to components.
- **Read-only** (immutable).
- Allow data to be passed from parent to child components.

Example:

```tsx
const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};
```

Usage:

```tsx
<Greeting name="Alice" />
```

------

#### 🔥 State (Component Memory)

- Stores **dynamic data** in components.ie Data is mutable
- Uses the `useState` hook (functional components).

Example:

```tsx
import { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};
```

------

### 🌐 Handling Events in React

Events in React are similar to JavaScript, but use **camelCase**. Example:

```tsx
<button onClick={() => alert('Clicked!')}>Click Me</button>
```

------
### 📡 React & The Virtual DOM

- What is the DOM?
  - A representation of the webpage.
- Instead of updating the real DOM directly, React:
  1. Creates a virtual copy of the DOM.
  2. Compares the new and old versions (diffing algorithm).
  3. Updates only the necessary parts or the updated parts of the real DOM.

------

### 🔗 Hooks
Functions that allow you to use state, side effects, and other React features in functional components without classes.

🔑 Two of Core Hooks we will look at 
2. **useState** - Adds state to functional components.
```jsx

const [count, setCount] = useState(0);
```
2. **useEffect** - Handles side effects like data fetching or DOM updates.
```jsx
useEffect(() => { /* side effect */ }, [dependencies]);
```



### Developer Tools

You can add the [React Developer Tool](https://react.dev/learn/react-developer-tools) extension on your browser. It adds React debugging tools to the Chrome Developer Tools