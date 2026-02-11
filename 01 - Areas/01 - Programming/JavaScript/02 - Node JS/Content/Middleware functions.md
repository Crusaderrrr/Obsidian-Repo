---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - JavaScript
  - node_js
  - programming
  - express_js
note type: Informational Note
---
Middleware functions in Express.js are functions that have access to the request (*req*), response 
(*res*), and the next middleware function in the application's request-response cycle. They are used to execute code, modify the request/response objects, end the request-response cycle, or call the next middleware in the stack.

There is a web page of the express middleware: [click](https://expressjs.com/en/resources/middleware.html)
### JSON
The example of my code is:
```JavaScript
app.use(express.json());
```
This middleware function is used to redirect data to another middleware function.

```JavaScript
app.use((req, res, next) => {
    console.log("Logging...");
    next();
}); 

app.use((req, res, next) => {
    console.log("Authenticating...");
    next();
});
```
These are two middleware functions, when sending request to the server the first will work and send: "Logging..." message, if `next();` parameter doesn't exist, the next function won't start working.
So, `next();` is used to permit working to the next middleware function.

**Also**, we can define the middleware functions in other files and export them.
Create a new `logger.js` file:
```JavaScript
const log = (req, res, next) => {
    console.log("Logging...");
    next();
}

module.exports = log;
```
Create and export a function.

In our `app.js` file:
```JavaScript
const logger = require('./logger')

app.use(logger); // use middleware function
```

So, if middleware function receives JSON file, it will set the req.body and then it will pass control to the next middleware function.

### URL encoded

`app.use(express.urlencoded());` this enables middleware to parse incoming request bodies with URL-encoded data (e.g., form submissions). It extracts key-value pairs from the request body (like *name=John&age=25*) and makes them available in req.body as an object (e.g., `{ name: 'John', age: '25' }`). By default, it uses the **extended**: false option, meaning it only handles simple data (not nested objects).

### Static
With this function is used to serve static files.
if we create a folder `public` and inside create a **readme.txt** file, so
```JavaScript
app.use(express.static('public'));
```
Navigating to the localhost is gonna show us the readme.txt text

### Morgan
This needs to be installed firstly, `npm i`
Is used to show the request information.