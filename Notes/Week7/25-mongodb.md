## 🗄️ MongoDB # 2.5 - Database Exercise

### 🎯 Objectives

1. **Understand** the fundamental concepts of NoSQL databases and MongoDB's document model.
2. **Explain** the role of MongoDB in modern web development and how it integrates with Node.js applications.
3. **Implement** a basic Node.js server that uses MongoDB to store and retrieve data.
4. **Set up** MongoDB on the docker..
5. **Perform** basic CRUD (Create, Read, Update, Delete) operations with MongoDB from a Node.js app.

### 🔨 Setup

1. Open your terminal and navigate to your `~/web-ii/exercises/` directory.

2.

3. For this exercise  MongoDB is installed on the docker, available on the port specified in the fields

4. Clone the repository for this exercise by copying the URL from GitHub, then run:

   ```
   git clone <paste URL here>
   ```

   Rename the folder to `~/web-ii/exercises/2.5-mongodb/`.

5. Open VS Code and install necessary dependencies by running:

   ```
   npm install
   ```



### 🔍 Context

In E1.3, we had the Docker to spin up two containers. One for running our application code, and one for running our database server. We used the PSQL client to connect to the database and execute SQL commands.

In this exercise, we’re going to do the same thing, but with MongoDB databse.  The first thing to do is open `model.ts` and notice at the top is a module we’re importing: [mongodb](https://github.com/porsager/postgres). This library is going to allow us to connect to the MongoDB database we’re running in our Docker container.

For review, check out the [MongoDB Notes](../Notes/Week7/mongodb) before starting this exercise. We will be using the Express router from the previous exercise to route the endpoints.



## 🚦 Let’s Go

### Part 1: Creating a Database and Collection

1. In the `model.ts`, initialize the mongdb database.

```tsx
export async function initDB() {
	try {
		const url = `mongodb://${process.env.MONGO_USER}:${process.env.MONGO_PWD}@${process.env.MONGO_HOST}/`;

		// Initialize MongoDB client
		client = new MongoClient(url);
		await client.connect();
		console.log("Connected to MongoDb");

		const db = client.db(DATABASE_NAME);

	} catch (err) {
		if (err instanceof MongoError) {
			console.error("MongoDB connection failed:", err.message);
			throw err;
		} else {
			console.error("Unexpected error:", err);
			throw err;
		}
	}
}
```

2. Now we will create a collection for the Pokemons if it doesn't exist.In the `try` section , after the db is initialized. add the following code.

```tsx
   
   		// Get the list of existing collections in the database
   		const collections = await db.listCollections().toArray();
   		const collectionNames = collections.map((col) => col.name);
   
   		// Create "pokemon" collection if it does not exist
   		if (!collectionNames.includes("Pokemon")) {
   			console.log('Creating "pokemon" collection...');
   			await db.createCollection("pokemon");
   		}
   
   		// Reference to the "pokemon" collection
   		pokemonCollection = db.collection("pokemon");
```

   

3. Now that we have a collection , we will add the initial document if doesn't already exist. This step can be omitted or data could added directly using curl.

```tsx
          // Check if the collection is empty and insert initial data if needed
   		const userCount = await pokemonCollection.countDocuments();
   
   		if (userCount === 0) {
   			console.log("Inserting initial pokemons...");
   			await pokemonCollection.insertMany(database);
   		}
```
4. Add a funciton to return the document.
```tsx
export async function getAll(): Promise<Collection<Pokemon> | undefined> {
	return pokemonCollection;
}
```
-----
### Part 2: Updating the Controller to access the Mongodb database.   

1. Import the function to getAll from model to access data from the database.

```
   import {getAll} from "./model";
```
2. Now update the `getAllPokemon` function in the `controller.ts` file.

>[!NOTE] **Cursor**
>In Node, when you make certain calls to the MongoDb that can return multiple pieces of information, you don't get back the actual data. 
>Instead, you get back a special object called a [Cursor](https://www.mongodb.com/docs/drivers/node/current/fundamentals/crud/read-operations/cursor/).
>
>The purpose of a cursor is to avoid sending a very large amount of data all at once, and >instead allow the app to iterate over it as appropriate.
>Recall: NoSQL databases can be enormous.
>In this class, we'll skip the finesse and just use the brute-force approach of converting the cursor to an array.  
>This will force all the data to be loaded into a JavaScript array.
>If cursor is the result of a collection.find() call, then cursor.toArray() will give you a JavaScript array of all the results.
>Important: This toArray() operation is asynchronous since it involves getting data from the online database.


```
const pokemonCollection = await getAll();

```
3. Send appropriate response back to server 
```tsx
if (pokemonCollection) {
		const pokemon = await pokemonCollection.find().toArray(); // Fetch pokemons as an array
			
		res.status(200).json({
			success: "Pokemon Collection Found",
			pokemon,
			});
} else {
			res.status(500).json({
				success: false,
				message: "Pokemon Collection does not exists",
			});
		}
```



4. Then add a try-catch block to capture an internal Server error

```tsx
   try {
   		const pokemonCollection = await getAll(); // Get collection
   		if (pokemonCollection) {
   			const pokemon = await pokemonCollection.find().toArray(); // Fetch pokemons as an array
   			//console.log(pokemon);
   			res.status(200).json({
   				success: "Pokemon Collection Found",
   				pokemon,
   			});
   		} else {
   			res.status(500).json({
   				success: false,
   				message: "Pokemon Collection does not exists",
   			});
   		}
   	} catch (error) {
   		res.status(500).json({
   			success: false,
   			message: "Internal server error",
   		});
   	}
```
----

### Part 3: Updating the Server engine with express router.

1. We will update the `servet.ts` to initialize the Mongodb database by importing the `initdb` function from `model.ts`

   ```tsx
   import { initDB } from "./model";
   
   initDB();
   ```

   - Start the server by running `npm run server`.

### Part 4: Processing Requests and running test.
Open a separate terminal window. We’ll use this one to make cURL requests and see the server responses.

Using cURL, test all your routes to ensure everything is working so far. For example

```bash
curl -v http://localhost:3000/pokemon

curl -v http://localhost:3000/pokemon/:id

curl -v -X POST -H "Content-Type: application/json" -d '{"name": "Bulbasaur", "type": "Grass"}' http://localhost:3000/pokemon

curl -v -X PUT -H "Content-Type: application/json" -d '{"type": "Poison"}' http://localhost:3000/pokemon/2

curl -v -X DELETE http://localhost:3000/pokemon/:id
```
----



## 📚 Submission

1. Perform the following cURL operations without the `-v` flag:

   1. `POST` a new `/pokemon`.
   2. `GET` the `/pokemon/:_id` that was inserted.
   3. `UPDATE` the `/pokemon/:_id` to have a different name.
   4. `GET` all the `/pokemon` to verify the name was changed.
   5. `DELETE` the `/pokemon/:_id`.
   6. `GET` all `/pokemon?type=Water` to get only Water Pokemon.
   7. `GET` all `/pokemon?sortBy=name` to get all Pokemon sorted alphabetically by name.

Take a screenshot (or several if they all don’t fit in one) of the output so that I can see **all statements were run successfully**. Submit the screenshot you took to the Moodle dropbox for this exercise.
