# 2.4 - Express Exercise

## 🎯 Objectives

1. **Understand** how Express simplifies HTTP server creation in Node.js.
2. **Learn** how to set up an Express application with TypeScript.
3. **Implement** route handling for different HTTP methods (GET, POST, PUT, DELETE).
4. **Use** middleware for request parsing and logging.
5. **Structure** a small Express API using TypeScript best practices.

## 🔨 Setup

1. Navigate to your project folder:

   ```bash
   cd ~/web-ii/exercises/
   ```

2. Go to [the repository for this exercise](https://github.com/JAC-CS-Web-Programming-II-W25/E2.4-Express-Template) and click `Code -> 📋` to copy the URL.

   ```bash
   git clone <paste URL from GitHub>
   ```

3. Rename the cloned folder to `~/web-ii/exercises/2.4-express/`

4. Start Docker Desktop.

5. In VS Code, hit `CMD/CTRL + SHIFT + P` and search + run `dev container: open folder in container`.

6. In the terminal of VS Code, hit the `+` icon to open a new terminal instance. Run `ls` to make sure you’re in the root directory of the exercise and that you see `package.json`.

7. Run `npm install` to install all our dependencies.

## 🔍 Context

We previously explored the fundamentals of HTTP And router using Node.js's `http` module. Now, we will use **[Express]((https://expressjs.com/)**, a minimal framework that simplifies server creation and request handling.

## 🚦 Let’s Go

### Part 1: Setting Up the Express Server

We will separate the server starter from all routing information.

1. Create a new file `server.ts` and add the following code:

   ```typescript
   import express from "express";
   import pokemonRouter from "./router";
   import { getHome } from "./controller"; // ideally should not be in the controller.

   const app = express();
   const port = 3000;

   // Middleware to parse incoming JSON requests
   app.use(express.json());

   /**
    * Home route
    * Responds with a welcome message when the root URL is accessed.
    */
   app.get("/", getHome);

   app.use("/pokemon", pokemonRouter);
   /**
    * Starts the Express server and listens on the specified port.
    */
   app.listen(port, () => {
     console.log(`Server running at http://localhost:${port}/`);
   });
   ```

2. Start the server by running:

   ```bash
    npm run server
   ```

3. Test with cURL:

   ```bash
   curl -X GET http://localhost:3000/
   ```

### Part 2: Route Data Structures & Registration

1. In the router.ts define your route for the endpoints. :

   ```ts
   import { Router } from "express";
   import {
     createPokemon,
     deletePokemon,
     getAllPokemon,
     getOnePokemon,
     updatePokemon,
   } from "./controller";
   
   const pokemonRouter: Router = Router();
   
   pokemonRouter.get("/", getAllPokemon);
   
   pokemonRouter.get("/:id", getOnePokemon);
   
   pokemonRouter.post("/", createPokemon);
   
   pokemonRouter.put("/:id", updatePokemon);
   
   pokemonRouter.delete("/:id", deletePokemon);
   
   export default pokemonRouter;
   ```

### Part 2: Updating the Controller to work with express

The http module is replaced with express. Most of the code from the previous exercise remains the same. Pay attention to the express responses.

- You dont need the req.on and req.end as this is automatically handled by express.
- Express automatically handles request body parsing when using express.json().
- Directly accesses req.body instead of manually collecting chunks.

```typescript
import { Request, Response } from "express";
```

---

### **Testing**

Using cURL, test all your routes to ensure everything is working so far. For example::

```bash
curl -v http://localhost:3000/pokemon

curl -v http://localhost:3000/pokemon/1

curl -v -X POST -H "Content-Type: application/json" -d '{"name": "Bulbasaur", "type": "Grass"}' http://localhost:3000/pokemon

curl -v -X PUT -H "Content-Type: application/json" -d '{"type": "Poison"}' http://localhost:3000/pokemon/2

curl -v -X DELETE http://localhost:3000/pokemon/1

```

## Conclusion

- Express provides a simpler and more scalable way to build HTTP servers compared to the `http` module.

- Middleware like `express.json()` makes request parsing easier.

## 📚 Submission

1. Perform the following cURL operations without the `-v` flag:
   1. `POST` a new `/pokemon`.
   2. `GET` the `/pokemon/2` that was inserted.
   3. `UPDATE` the `/pokemon/2` to have a different name.
   4. `GET` all the `/pokemon` to verify the name was changed.
   5. `DELETE` the `/pokemon/2`.
   6. `GET` all `/pokemon?type=Water` to get only Water Pokemon.
   7. `GET` all `/pokemon?sortBy=name` to get all Pokemon sorted alphabetically by name.

Take a screenshot (or several if they all don’t fit in one) of the output so that I can see **all statements were run successfully**. Submit the screenshot you took to the Moodle dropbox for this exercise.
