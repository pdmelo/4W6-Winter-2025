# Rest API Best Practices
- So far, we've created some simple endpoints and seen how visiting a particular URL can initiate a particular action in your server code
  - E.g., Route a specific endpoint to a specific controller function, passing in the appropriate request data/parameters

- The term **REST** stands for **RE**presentational **S**tate **T**ransfer
- It is an architectural style that was created as part of the development of Web standards

- In the REST architectural style, data and functionality are considered resources and are accessed using Uniform Resource Identifiers (URIs).
  - i.e., Each resource has a unique name

- Any information that we can name can be a resource
  - E.g., document, image, collection of other resources, a user, a post

- The resources are acted upon by using a set of simple, well-defined operations. 
  - E.g., Http Get, Post, Put, Delete

- The resources have to be decoupled from their representation so that clients can access the content in various formats, such as HTML, XML, plain text, PDF, JPEG, JSON, and others.

- REST APIs work by fielding requests for a resource and returning all relevant information about the resource, translated into a format that clients can easily interpret.

- Clients can also modify items on the server and even add new items to the server through a REST API.

- **Representational State Transfer**: This means that when a client requests a resource using a REST API, the server *transfers* back the current *state* of the resource in a standardized *representation*.

## Key Properties of a REST API
- **Client-Server**
  - Client and server are separate and can evolve independently
    - i.e., separation of concerns / loose coupling
- **Stateless**
  - API calls can be made independently of each other
  - Each API call contains all the data needed to complete that request
    - Should not rely on data being stored on the server
    - E.g., contains the user id
  - Implies that the server cannot take advantage of any previously stored context information
  - Implies that all session state is stored on the client, not the server
    - Every request by the client is interpreted by the server as a brand new ask — the server remembers nothing about past requests.
  - **Benefits:**
    - Stateless transfers greatly reduce the amount of server memory needed
    - Improved odds of a successful response (since server is not required to take additional action to retrieve old data) 
    - Improved scalability – don't worry about more memory being used or overloading the server with requests
- **Uniform Interface**
  - Interface provides an unchanging, standardized means of communicating between the client and server 
    - E.g., using HTTP with URI resources, CRUD and JSON.

## Best Practices for naming REST API endpoints
Read the description here [best-practices-for-naming-rest-api-endpoint](https://blog.dreamfactory.com/best-practices-for-naming-rest-api-endpoints/)

-  **Use Nouns to Name URIs**
- **name your URIs with plural nouns**
- **Use Clear, Unabridged Names That Are Intuitive**
- **Separate Words with Hyphens**
- **Use Lowercase Letters**
- **Avoid Special Characters**
- **Avoid File Extensions**
