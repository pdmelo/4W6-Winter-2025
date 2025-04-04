### Props And State

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

### 🔗Hooks

Hooks in React are functions that let you use state and lifecycle features in functional components without needing class components. They were introduced in React 16.8 and allow for a cleaner and more modular way to manage component logicFunctions that allow you to use state, side effects, and other React features in functional components without classes.

**Common React Hooks:**

1. **useState** – Manages state in functional components.

2. **useEffect** – Handles side effects like fetching data or subscribing to events.

3. **useContext** – Consumes values from a React context.

4. **useRef** – References DOM elements or persists values between renders.

5. **useMemo** – Optimizes performance by memoizing values.

6. **useCallback** – Memoizes functions to prevent unnecessary re-renders.

   

#### 🔑 Two of Core Hooks we will look at 

2. **useState** - Adds state to functional components.

```jsx
const [count, setCount] = useState(0);
```

2. **useEffect** - Handles side effects like data fetching or DOM updates.

```jsx
useEffect(() => { /* side effect */ }, [dependencies]);
```
-----


### 🌐 Handling Events in React

Events in React are similar to JavaScript, but use **camelCase**. Example:

```typescript
<button onClick={() => alert('Clicked!')}>Click Me</button>
```
React event handlers are written inside curly braces

```typescript
onClick={display} 
```

instead of ` onclick="display()"`

