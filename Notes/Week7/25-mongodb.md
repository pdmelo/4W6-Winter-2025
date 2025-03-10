## 🗄️ MongoDB # 2.2 - Database Exercise

### 🎯 Objectives

1. **Understand** the fundamental concepts of NoSQL databases and MongoDB's document model.
2. **Explain** the role of MongoDB in modern web development and how it integrates with Node.js applications.
3. **Implement** a basic Node.js server that uses MongoDB to store and retrieve data.
4. **Set up** MongoDB locally or using a cloud service like MongoDB Atlas.
5. **Perform** basic CRUD (Create, Read, Update, Delete) operations with MongoDB from a Node.js app.

### 🔨 Setup

1. Open your terminal and navigate to your `~/web-ii/exercises/` directory.

2. Visit [MongoDB's official website](https://www.mongodb.com/) and either set up a local MongoDB server or create a free account on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

3. For local setup, make sure MongoDB is installed and running. You can verify this by running `mongod` to start the MongoDB server and `mongo` to enter the MongoDB shell.

4. Clone the repository for this exercise by copying the URL from GitHub, then run:

   ```
   git clone <paste URL here>
   ```

   Rename the folder to `~/web-ii/exercises/2.2-mongodb/`.

5. Open VS Code and install necessary dependencies by running:

   ```
   npm install
   ```



### 🔍 Context

Earlier this week, you worked with basic HTTP operations using Node.js. Now, we’re expanding on that by introducing MongoDB, a NoSQL database that stores data in flexible, JSON-like documents. You will integrate MongoDB with your existing Node.js server to manage a Pokemon collection.