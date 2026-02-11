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
The structure need to be better,.
We need to distribute the code to other files like this:
![[Pasted image 20250420202917.png]]
- So the `logger.js` is a middleware function
- routes are parts or pages of our site:
	- courses 
	- home
- views folder is needed for *Pug* 
- and finally app.js which is main file that sums all the pages 

Home.js:
```JavaScript
const express = require("express");
const router = express.Router();

router.get('/', (req, res) => {
    res.render("index", { title: "My Express App", message: "Hello"})
});

module.exports = router;
```
We need to export it as a router and use `express.Router()` function which is used to create a **modular, mountable route handler** in Express. It allows you to define routes in a separate file or module and then use them in your main application. We need to do so in *all the files*. 

App.js:
```JavaScript
const debug = require('debug')('app:startup');
const config = require('config');
const morgan = require('morgan');
const { log, auth } = require('./middleware/logger');
const courses = require('./routes/courses'); // this 
const home = require('./routes/home'); // this 
const express = require('express');
const app = express();

app.use("/api/courses", courses); 
app.use("/", home);
```
line 10 means that:
1. - This line mounts the [courses](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) router (imported from `./routes/courses`) to the `/api/courses` path.
    - The [courses](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) router is likely defined in the `routes/courses.js` file using express.Router
2. **Path Prefix**:
    - All routes defined in the *courses* router will now be prefixed with `/api/courses`.

So we can use just `/` instead of `/api/courses`, but we need to use `/:id` for stuff like that.
```JavaScript
router.get('/', (req, res) => {
    res.send(courses);
});

router.put('/:id', (req, res) => {
    // Look up the course
    // if not existing, return 404
    const course = courses.find(c => c.id === parseInt(req.params.id));
    if (!course) return res.status(404).send('The course with the given ID was not found.');
    
    //validate the course
    // if invalid, return 400 - Bad Request
    const { error } = validateCourse(req.body);
    // If validation fails, send a 400 Bad Request response
    if (error) return res.status(400).send(error.details[0].message);

    // Update course
    course.name = req.body.name;
    // return the updated course
    res.send(course);
});
```

# MongoDB structure
![[Pasted image 20250424141533.png]]

We add a new folder `models` where we are gonna store models, because they will be huge and overwhelm the code. 

In the file `customer.js` we import all the necessary modules ( Joi, mongoose ) and paste *Customer Model* and *Validating function*.

Then we need to export it:
```JavaScript
exports.Customer = Customer;
exports.validate = validateCustomer;
```

and import them in `index.js`, there are 2 ways of do so:
**First way**:
- directly import with `require()` function:
```JavaScript
const customer = require('../models/customer')
```
but we would need to call Customer model as customer.Customer and this ugly and not efficient.

**Second way** (recommended):
- we use object destructure:
```JavaScript
const { Customer, validate } = require('../models/customer')
```