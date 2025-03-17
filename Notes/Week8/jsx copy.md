# 🛤️3.1 JSX Exercise:

## 🎯 Objectives

1. **Understand** the basics of client-side routing in a React application using React Router with TypeScript.
2. **Create** multiple pages/components and navigate between them.
3. **Implement** dynamic routing with URL parameters.
4. **Utilize** query parameters to filter and sort displayed data.
5. **Apply** programmatic navigation and redirects.

---

## 🔨 Setup

1. Open a terminal and navigate to your project folder: `~/web-ii/exercises/`.
2. Run `npx create-react-app 2.2-jsx-routing --template typescript` to generate a new React project with TypeScript.
3. Navigate into the project folder: `cd 2.2-jsx-routing`.
4. Install React Router: `npm install react-router-dom`.
5. Start the project: `npm start`.

---

## 📌 Part 1: Setting Up Routes

### Install and Configure React Router

Modify `main.jsx` to wrap the app with a router:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

### Create Pages for Navigation

Inside `src/`, create a `pages/` folder and add the following components:

#### `Home.tsx`

```tsx
import React from "react";

const Home: React.FC = () => {
  return <h1>Welcome to the Home Page</h1>;
};

export default Home;
```

#### `About.tsx`

```tsx
import React from "react";

const About: React.FC = () => {
  return <h1>About Us</h1>;
};

export default About;
```

#### `NotFound.tsx`

```tsx
import React from "react";

const NotFound: React.FC = () => {
  return <h1>404 - Page Not Found</h1>;
};

export default NotFound;
```

### Define Routes in `App.tsx`

```tsx
import React from "react";
import { Routes, Route, Link } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import NotFound from "./pages/NotFound";

const App: React.FC = () => {
  return (
    <div>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </div>
  );
};

export default App;
```

### Test Navigation

Run `npm start`, and use the navbar links to test navigating between `Home` and `About`. Enter an invalid URL to see the `NotFound` page.

---

## 📌 Part 2: Dynamic Routing with URL Parameters

Modify `pages/` by adding a new file `PokemonDetail.tsx`:

```tsx
import React from "react";
import { useParams } from "react-router-dom";

type PokemonParams = {
  id: string;
};

const PokemonDetail: React.FC = () => {
  const { id } = useParams<PokemonParams>();
  return <h1>Details for Pokémon ID: {id}</h1>;
};

export default PokemonDetail;
```

### Add Route in `App.tsx`

```tsx
import PokemonDetail from "./pages/PokemonDetail";

// Inside <Routes>:
<Route path="/pokemon/:id" element={<PokemonDetail />} />;
```

### Test Dynamic Routing

Go to `http://localhost:3000/pokemon/25` in the browser. It should display:

> Details for Pokémon ID: 25

---

## 📌 Part 3: Query Parameters for Filtering and Sorting

Modify `pages/` by adding `PokemonList.tsx`:

```tsx
import React from "react";
import { useLocation } from "react-router-dom";

type Pokemon = {
  id: number;
  name: string;
  type: string;
};

const pokemonData: Pokemon[] = [
  { id: 1, name: "Bulbasaur", type: "Grass" },
  { id: 4, name: "Charmander", type: "Fire" },
  { id: 7, name: "Squirtle", type: "Water" },
];

const useQuery = () => {
  return new URLSearchParams(useLocation().search);
};

const PokemonList: React.FC = () => {
  const query = useQuery();
  const typeFilter = query.get("type");
  const sortBy = query.get("sortBy");

  let filteredData = pokemonData;
  if (typeFilter) {
    filteredData = filteredData.filter(
      (p) => p.type.toLowerCase() === typeFilter.toLowerCase()
    );
  }
  if (sortBy === "name") {
    filteredData.sort((a, b) => a.name.localeCompare(b.name));
  }

  return (
    <div>
      <h1>Pokémon List</h1>
      <ul>
        {filteredData.map((p) => (
          <li key={p.id}>
            {p.name} ({p.type})
          </li>
        ))}
      </ul>
    </div>
  );
};

export default PokemonList;
```

### Test Query Parameters

- `http://localhost:3000/pokemon?type=Water` (Filters by Water type)
- `http://localhost:3000/pokemon?sortBy=name` (Sorts alphabetically)

---

## 📥 Submission

Take screenshots of:

- The navigation working between pages.
- A dynamic Pokémon details page (`/pokemon/1`).
- A filtered and sorted Pokémon list using query parameters.
- A programmatic navigation action (button click to Pokémon details).

Submit all screenshots to the designated submission portal.

🎉 **Congratulations! You've implemented TypeScript-based routing with React Router!** 🚀
