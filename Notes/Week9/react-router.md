# React Router Exercise

## 🎯 Objectives

1. **Understand** what React Router is and why it's used in React applications..
2. **Use** React Router to navigate between pages without full page reloads.
3. **Use** dynamic routes and URL parameters to display different content based on the URL.
4. **Navigate** programmatically using React Router hooks.

## Why Use React Router?

React Router allows us to build single-page applications (SPAs) that can:

- Navigate between pages without full page reloads.

- Use dynamic routing based on URL parameters.

- Implement nested routes for better structure.

- Redirect users programmatically..

## 🔨 Setup

1. Using the terminal, navigate to your `~/web-ii/exercises/` folder.
2. Go to [the repository for this exercise](https://github.com/JAC-CS-Web-Programming-II-W25/E3-React-Template) and click `Code -> 📋` to copy the URL.
3. Clone the Git repo from the CLI `git clone <paste URL from GitHub>` (without the angle brackets) or using a GUI client like [GitHub Desktop](https://desktop.github.com/).
   - You may have to use the `HTTPS` or `SSH` URL to clone depending on your settings. If one doesn’t work, try the other by clicking `Use SSH` or `Use HTTPS` above the 📋, and copy the new URL.
   -
4. Rename the cloned folder to `~/web-ii/exercises/3.4-router`.
5. Start Docker Desktop.
6. All our dependencies are already installed.
7. In VS Code, hit `CMD/CTRL + SHIFT + P` and search + run `dev container: open folder in container`.
8. In the terminal of VS Code, hit the `+` icon to open a new terminal instance.
9. cd to `client` to run `npm run dev` to start the react server.

## 🔍 Context

React Router is a standard **routing library ** for React applications. It allows navigation between different views or components in a single-page application (SPA) without requiring a full page reload.

## Part 1: Setting Up The App

1. In the components folder, create two components `Home.jsx` and `About.jsx` with a some data.

2. Add this style in the index.css. (Use the colors that please your eyes...and mine !)

   ```css
   .nav {
     background-color: rgb(163, 169, 228);
     color: whitesmoke;
     display: flex;
     justify-content: space-between;
     padding: 0 1rem;
   }
   .nav a {
     color: whitesmoke;
   }
   ```

## Part 2: Setting Up the page routing the old way(JS).

1. Create a new component `NavBarOld.jsx` and the following code.

```jsx
function NavBarOld() {
  return (
    <nav className="nav">
      <ul>
        <li>
          <a href="/">Home</a>
        </li>
        <li>
          <a href="/about">About</a>
        </li>
      </ul>
    </nav>
  );
}
export default NavBarOld;
```

2. Update the `App.jsx` to include the following code, with `NavBarOld` component.

```jsx
function App() {
  let component;
  //log this to understand the what it returns
  console.log(window.location);

  switch (window.location.pathname) {
    case "/":
      component = <Home />;
      break;
    case "/about":
      component = <About />;
      break;
  }
  return (
    <>
      <article>
        <NavBarOld />
        {component}
      </article>
    </>
  );
}
export default App;
```

## Part 2: Setting Up Page Routing using React Router

`BrowserRouter` is a component from `react-router-dom` that enables **client-side routing** in a React. It manages navigation without causing a full-page reload.

1. Modify `App.jsx` to wrap the app with **BrowserRouter** and define basic routes.Pay attention to the imports..

```jsx
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import Home from "./Home";
import About from "./About";

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}

export default App;
```

### Additional Notes

#### Navigating Between Pages

2. Create a new component `Navbar` , Use the `Link` component instead of `< a >` tags. Pay attention to the imports,It requires the `Link` react library from `react-router-dom`..
   - Unlike a traditional `<a href="...">`, `Link` **does not refresh the page**. Instead, it updates the URL and renders the corresponding route using React Router.

```
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```

3. Update the `App.jsx` to replace`NavBarOld` with `Navbar` it should works as smoothly.

   ```jsx
   <Router>
     <Navbar />
     <Routes>
       <Route path="/" element={<Home />} />
       <Route path="/about" element={<About />} />
     </Routes>
   </Router>
   ```

#### Using URL Parameters

Define dynamic routes using `:` before a parameter name:

```jsx
import { useParams } from "react-router-dom";

function Pokemon() {
  let { username } = useParams();
  return <h1>Profile of {username}</h1>;
}
```

Set up the route in the `App.js`:

```jsx
<Route path="/profile/:username" element={<Pokemon />} />
```

In the `Navbar`

```jsx
<Link to="/profile/Pikachu">Pikachu's Profile</Link>
```

#### Redirects and Navigation

Use `useNavigate` to programmatically navigate.

- `useNavigate` is a hook from **React Router v6** that allows you to programmatically navigate between pages

```jsx
import { useNavigate } from "react-router-dom";

function Home() {
  const navigate = useNavigate();
  return <button onClick={() => navigate("/about")}>Go to About</button>;
}
```

## Summary

- React Router enables SPA navigation without full page reloads.
- Routes are defined using `Routes` and `Route`.
- Navigation is handled using `Link` and `useNavigate`.
- URL parameters allow dynamic routing.

React Router is an essential tool for structuring and navigating React applications effectively.
