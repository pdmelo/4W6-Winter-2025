# Question and Answers
## 1.  Why do we explicitly import   { IncomingMessage, ServerResponse } 

### 1. **Type Safety in TypeScript**

- In TypeScript, `IncomingMessage` and `ServerResponse` are types that define the request and response objects.
- Explicitly importing them allows you to use them for type annotations, improving type safety in your HTTP server logic.

```ts
import http, { IncomingMessage, ServerResponse } from "http";

const server = http.createServer((req: IncomingMessage, res: ServerResponse) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello, world!");
});

server.listen(3000);

```

### 2. **Avoiding Namespace References (`http.IncomingMessage`)**

- Without explicit imports, you would have to reference them using `http.IncomingMessage` and `http.ServerResponse`, which can be more verbose.

```ts
import * as http from "http";

const server = http.createServer((req: http.IncomingMessage, res: http.ServerResponse) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello, world!");
});

```

### 3. Clarity
It helps other developers understand that you are only working with IncomingMessage and ServerResponse, rather than the entire http module.