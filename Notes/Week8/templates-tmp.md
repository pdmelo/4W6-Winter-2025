# Dynamic HTML

## What is Dynamic HTML?

- HTML that updates based on data or user interaction.
- Used in web applications, CMS, and real-time dashboards.



## Handlebars Templating Engine

### What is Handlebars?

- A simple templating engine for generating HTML dynamically.
- Uses placeholders `{{ }}` to insert data into templates.
- Keeps logic separate from presentation.
- Handlebars can be used for both **server-side** and **client-side** rendering.
  - **Server-Side Rendering (SSR)**: In Node.js applications, Handlebars is often used with Express to generate HTML before sending it to the browser.
  - **Client-Side Rendering (CSR)**: Handlebars can also be used in the browser to dynamically update content using JavaScript.

### **Key Features of Handlebars**

- **Simplicity**: Uses minimal syntax.
- **Logic-less Templates**: No complex logic inside templates.
- **Reusable Components**: Supports partials (reusable templates).
- **Conditionals & Loops**: Includes `if`, `else`, and `each` helpers.
- **Precompilation**: Improves performance by compiling templates into JavaScript functions.

### **Handlebars Example**

Template

```hbs
<h1>Hello, {{name}}!</h1>
{{#if isAdmin}}
  <p>Welcome, Admin!</p>
{{/if}}
<ul>
  {{#each users}}
    <li>{{this.name}} - {{this.role}}</li>
  {{/each}}
</ul>
```

Using JavaScript

```js

const Handlebars = require('handlebars');
const templateSource = `<h1>Hello, {{name}}!</h1>`;
const template = Handlebars.compile(templateSource);
const result = template({ name: "Alice" });
console.log(result); // Output: <h1>Hello, Alice!</h1>
```

Using Typescript

```Terminal
npm install handlebars
```

```ts
import * as Handlebars from "handlebars";

// Define the Handlebars template
const templateSource = `
<h1>Hello, {{name}}!</h1>
{{#if isAdmin}}
  <p>Welcome, Admin!</p>
{{/if}}
<ul>
  {{#each users}}
    <li>{{this.name}} - {{this.role}}</li>
  {{/each}}
</ul>
`;

// Compile the template
const template = Handlebars.compile(templateSource);

// Define the data structure
interface User {
  name: string;
  role: string;
}

interface TemplateData {
  name: string;
  isAdmin: boolean;
  users: User[];
}

// Example data
const data: TemplateData = {
  name: "Alice",
  isAdmin: true,
  users: [
    { name: "John Doe", role: "Editor" },
    { name: "Jane Smith", role: "Admin" },
  ],
};

// Generate the HTML
const outputHTML = template(data);

// Print the generated HTML
console.log(outputHTML);

```





## Ways to Generate Dynamic HTML

1. **Server-Side Rendering (SSR)**

2. **Client-Side Rendering (CSR)**

   



## Templating Engines

- Injects data into HTML templates.
- Examples:
  - **Handlebars.js** (JavaScript)
  - **Pug (Jade)** (Node.js)
  - **EJS** (Node.js)
  - **Twig** (PHP)
  - **Jinja2** (Python)

## **Server-Side Rendering (SSR)**

- Generates HTML on the server before sending it to the browser.
- Examples:
  - **Next.js** (React)
  - **Nuxt.js** (Vue.js)
  - **SvelteKit** (Svelte)
- **Use Case**: Better for SEO, performance, and initial page load speed.



## **Client-Side Rendering (CSR)**

- Updates HTML dynamically in the browser.

- Examples:

  - **React.js**
  - **Vue.js**
  - **Angular.js**

- **Use Case**: Best for interactive applications.

  

## **JavaScript DOM Manipulation**

- Modifies HTML elements using JavaScript.
- Examples:

```
document.getElementById("myElement").innerHTML = "<p>Hello World!</p>";
```

- **Use Case**: Simple dynamic updates without frameworks.



## **Choosing the Right Method**

| **Use Case**          | **Best Solution**                            |
| --------------------- | -------------------------------------------- |
| SEO & Performance     | SSR (Next.js, Nuxt.js) or SSG (Gatsby, Hugo) |
| Fully Dynamic Web App | CSR (React, Vue, Angular)                    |
| Simple Templating     | Handlebars, Pug, EJS                         |
| Basic JS Manipulation | Vanilla JS, jQuery                           |
| Modular UI            | Web Components                               |