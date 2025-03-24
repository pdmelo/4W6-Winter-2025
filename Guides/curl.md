# cURL


Here's a breakdown of how to use cURL for different HTTP request types, along with examples:

## Basics of cURL

-   [**cURL**](https://curl.se/) is a powerful command-line tool for transferring data and making network requests using various protocols, including HTTP.
-   **General Syntax:** `curl [options] [URL]`

## GET Requests

-   The default method when using cURL.
-   Used to fetch data from a server.

### Example (get all Pokemon)

```bash
curl -v http://localhost:3000/pokemon
```

### Example (get one Pokemon by ID)

```bash
curl -v http://localhost:3000/pokemon/1
```

## POST Requests

-   Used to send data to a server (e.g., submitting forms, uploading data).
-   Use the `-X POST` option.
-   Use the `-d` option to specify the data being sent.

### Example (form-like data)

```bash
curl -v -X POST -d "name=Charmander&type=Fire" http://localhost:3000/pokemon
```

### Example (JSON data)

```bash
curl -v -X POST -H "Content-Type: application/json" -d '{"name": "Squirtle", "type": "Water"}' http://localhost:3000/pokemon
```

## PUT Requests

-   Used to update existing resources on a server.
-   Use the `-X PUT` option.
-   Use the `-d` option to specify the updated data.

### Example (form-like data)

```bash
curl -v -X PUT -d "type=Flying" http://localhost:3000/pokemon/2
```

### Example (JSON data)

```bash
curl -v -X PUT -H "Content-Type: application/json" -d '{"type": "Psychic"}' http://localhost:3000/pokemon/2
```

## DELETE Requests

-   Used to delete a resource on a server.
-   Use the `-X DELETE` option.

### Example

```bash
curl -v -X DELETE http://localhost:3000/pokemon/1
```
## Additional Options

-   `-w "\n" ` : print a newline after the response.	
-   `| jq` : Pipes the response to jq for [pretty-printing](https://mkyong.com/web/how-to-pretty-print-json-output-in-curl/)

## Additional Notes

-   **Verbose Output:** Add the `-v` option to see detailed information about the request and response.
-   **cURL's power extends far beyond these basics.** Check out the manual (`man curl`) or online resources for features like file uploads, authentication, and more.

## Important Considerations

-   The server receiving your requests needs to be set up to handle the respective HTTP method you're using.
-   Pay attention to data formats (e.g., JSON, form-encoded) and the server's requirements.
