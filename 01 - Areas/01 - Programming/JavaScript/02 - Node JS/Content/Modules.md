---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - node_js
  - JavaScript
  - programming
  - express_js
note type: Informational Note
---
# Module
Every JS file is a **module** if it uses `module.export` and `require()`
Modules are useful because of:
- They make the code cleaner 
- Every module exports *only* functions, which will be necessary in other files or modules

*Example*:
First file, from where we export (logger.js)
```JavaScript
const url = 'http://pseudologger.io/log'
const myLog = (message) => {
    console.log(message);
};

module.exports.log = myLog // exporting an object
```

Second file, where we import (app.js)
```JavaScript
const logger = require("./logger") // path to an imported file

logger.log("message")
```

**But**, we also can export a single function:
```JavaScript
const url = 'http://pseudologger.io/log'

cons myLog = (message) => {
	console.log(message);
};

module.exports = myLog // exporting a single function
```

And than, we can call this function *directly*:
```JavaScript
const logger = require("./logger") // path to an imported file

logger("message")
```
if we want to rename a function `logger()` we need to press *f2*


# Path Module
It has a useful function: `path.parse('node:parse')`
To use it, firstly we need to import it:
```JavaScript
const path = require("node:path");

const pathObj = path.parse(__filename);
console.log(pathObj) // down there
```
this `console.log()` gives us an object that has (root, dir, base, ext, name) elements.

# Operating System Module
Firs and foremost, we need to import it:
```JavaScript
const os = require("node:os");
```
There are many functions in this module, such as:
- `os.freemem()` - free memory
- `os.totalmem()` - total memory
- And so forth in the node.js documentation

# File System Module 
To load fs module:
```JavaScript
const fs = require('node:fs/promises');
```
or
```JavaScript
const fs = require('node:fs');
```
There are 2 types of APIs:
- **Asynchronous** 
	- *Callback API* (perform all operations asynchronously, without blocking the event loop, then invoke a callback function upon completion or error)
	- *Promise based API* (provides asynchronous file system methods that return promises)
- **Synchronous** (perform all operations synchronously blocking the event loop until the operation completes or fails)

*Promise example*:
```JavaScript
import * as fs from "node:fs/promises";
try {
    const files = await fs.readdir("./");
    for (const file of files)
        console.log(file);

} catch (error) {
    console.log("Error reading directory:", error);
}
```
It is the code when using **Promises**. It *ALWAYS* requires an **await** before the function.

*Callback example*:
```JavaScript
const { unlink } = require('node:fs');

unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('successfully deleted /tmp/hello');
});
```

*Synchronous example*:
```JavaScript
const { unlinkSync } = require('node:fs');

try {
  unlinkSync('/tmp/hello');
  console.log('successfully deleted /tmp/hello');
} catch (err) {
  // handle the error
}
```


# Event module
An **Event** is basically a signal that indicates that something has happened in our application.
Such as in previous modules we need to import this one.
```JavaScript
const EventEmiter = require('node:events');
import { EventEmitter } from 'node:events'; // EventEmitter is a class

const emitter = new EventEmitter(); // emitter is an object

// Register a listener (can use emitter.addListener();)
emitter.on("massageLogged", () => {
	console.log("Listener called...");
})

// Raise an event
emitter.emit("massageLogged");
```

A **class** is a *Human*, and **objects** are *us* (we are instances of this class)

There are 10 methods, but the ones we will use more are:
- `.emit()` - emits a noise, signals that event has happened
- `emitter.on(arg1: eventName, arg2: callbackFunc)` - used to make listener that will

`EventEmitter` is a core class for Node.js, modules such as *http* or *os* are using this class internally.

Also, we can return some additional arguments to the emitted massage. To do so, we need to add an object with these argument to the massage. And add arg, e, or eventArg to the function.

```JavaScript
emitter.on("massageLogged", (arg) => { // arg, e or eventArg
	console.log("Listener called...");
})

// Raise an event
emitter.emit("massageLogged", {'Id': 1, "url": "url"}); // adding an object
```

Using **class** instead of a function gives us extensibility, so we can export a class, not the only function. `export default Logger;`
When defining a **Class**, its name has to start from the capital letter (example: Logger). The function
`myLog` becomes a method. And we need to use *this* keyword instead of emitter which we don't ever need. 
*That class*:
```JavaScript
class Logger extends EventEmitter {
    myLog(message) {
        // send an HTTP request
        console.log(message);

        // raise an event
        this.emit('logging', { id: 1, url: 'url' });
    };
};
```

In the file, where we export Logger class:
```JavaScript
import Logger from './logger.js'
const logger = new Logger(); // creating a new emitter based on Logger class
```
also, we don't need emitter object and can delete it.

So, finally, our files will look like that:
**logger.js**:
```JavaScript
import EventEmitter from 'node:events';

const url = 'http://pseudologger.io/log'

class Logger extends EventEmitter { //creating a class based on EventEmitter
    myLog(message) {
        // send an HTTP request
        console.log(message);
        
        // raise an event
        this.emit('logging', { id: 1, url: 'url' });
    };
};

export default Logger; // exporting the created class
```

**app.js**:
```JavaScript
import EventEmitter from 'node:events';
import Logger from './logger.js'; // importing EE class

// Register an eventEmitter based on class from logger.js
const logger = new Logger();

// Register a listener
logger.on('logging', (arg) => {
    console.log('Listener called...', arg);
});

logger.myLog('message'); // logging a massage 
```

To sum up:
- If we want to create an EventEmitter, we need to create a lass like `Logger` that extends EE
	- this class will have all the functionality
	- we can expand this functionality `myLog` function that becomes a method inside the class
	- if we want to emit the event, we need to use *this* keyword `this.emit(...)`
- in the `app.js` we will need to use the instance of a class we created `Logger` not the EventEmitter


# HTTP Module 
The `http.createServer(res, req)` is a fundamental method of this module.

```JavaScript
import * as http from 'node:http';

const server = http.createServer();

server.on("connection", socket => {
    console.log("New connection...");
});

server.listen(3000);

console.log("listening on port 3000...");
```

This code means that:
- we import a http module 
- we create a server http
- `server.on("", socket)` here we add a listener register, and if listener catches an event, the massage `New connection...` will be logged in the console
- then we create a listener on a port 3000 and logging a massage `listening on port 3000...`

```JavaScript
import * as http from 'node:http';

const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.write("hello world");
        res.end();
    }

    if (req.url === '/api/courses') {
        res.write(JSON.stringify([1, 2, 3]));
        res.end();
    }
});

server.listen(3000);
console.log("listening on port 3000...");
```
With this code we make the same thing, but:
- we create a *req*ues and *res*ponse arguments, to controle the server behavior:
	- if request is a url -> server responds with `hello world`
	- if request is a url with /api/courses -> server responds with a JSON file as a string