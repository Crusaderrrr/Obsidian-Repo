---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - node_js
  - JavaScript
  - programming
note type: Informational Note
---
This is a JavaScript framework.
Express.js documentation: [click](https://expressjs.com/en/5x/api.html)

# Content
- [[RESTful Services]]
- [[CRUD requests]]
- [[Params]]
- [[Port]]
- [[Middleware functions]]
- [[Environment]]
- [[Templating Engines]]
- [[Integrating Database]]
- [[Structure]]

# nodemon
**Nodemon** is a Node.js *global* tool that automatically restarts your application when it detects file changes in the directory. It's mainly used during development to speed up testing and debugging.
# Final Code
```JavaScript
const Joi = require('joi'); // Importing Joi(class) for validation
const express = require('express');
const app = express();

app.use(express.json()); // Middleware to parse JSON bodies

const courses = [
    { id: 1, name: 'course1' },
    { id: 2, name: 'course2' },
    { id: 3, name: 'course3' },
];

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.get('/api/courses', (req, res) => {
    res.send(courses);
});

  

app.post('/api/courses', (req, res) => {
    // Validate the request body
    const { error } = validateCourse(req.body);
    if (error) return res.status(400).send(error.details[0].message);
    const course = {
        id: courses.length + 1,
        name: req.body.name
    };
    
    courses.push(course);
    res.send(course);
});

  

app.put('/api/courses/:id', (req, res) => {
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
  

app.delete('/api/courses/:id', (req, res) => {
    // Look up the course
    // not existing, return 404
    const course = courses.find(c => c.id === parseInt(req.params.id));
    if (!course) return res.status(404).send('The course with the given ID was not found.');

    //delete course
    const index = courses.indexOf(course); //get the index of the course to be deleted
    courses.splice(index, 1); //delete course

    //return the same course
    res.send(course);
});

  

const validateCourse = (course) => {
    const schema = Joi.object({
        name: Joi.string().min(3).required()
    });
    return schema.validate(course);
};

  
app.get('/api/courses/:id', (req, res) => {
    const course = courses.find(c => c.id === parseInt(req.params.id));
    if (!course) return res.status(404).send('The course with the given ID was not found.');
    res.send(course);
});


// PORT
const port = process.env.PORT || 3000
app.listen(port, () => console.log(`Listening on port ${port}...`));
```

I have changed the line:
```JavaScript
if (error) {
	// If validation fails, send a 400 Bad Request response
	res.status(400).send(error.details[0].message);
	return;
}
```

To:
```JavaScript
if (error) return res.status(400).send(error.details[0].message);
```