---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - node_js
  - JavaScript
  - programming
  - express_js
note type:
---
### GET
```JavaScript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello World!');
})

app.get('/api/courses', (req, res) => {
    res.send([1, 2, 3]);
})

app.listen(3000, () => console.log('Listening on port 3000'));
```
When visiting `http://localhost:3000` - will see Hello World! message
When visiting `http://localhost:3000/api/courses` - will see [1,2,3] array

```javascript
app.get('/api/courses/:id', (req, res) => {
    const course = courses.find(c => c.id === parseInt(req.params.id));
    if (!course) return res.status(404).send('The course with the given ID was not found.');
    res.send(course);
});
```
This code means that we want to GET data from a course id, we check if it exists, if not -> error 404, if yes -> give that data from course array that we defined before.

### POST
Before we do anything, we need to:
```javascript
app.use(express.json())
```
This method returns middleware

```javascript
app.post('/api/courses', (req, res) => {
    const course = {
        id: courses.length + 1,
        name: req.body.name
    };
    courses.push(course); // publish the new course 
    res.send(course); // return the new object to the client
});
```

**Testing the endpoint**:
We need to use a *Postman API*

In order to handle correctly POST requests, there is a need of validation of a values that are being input.
Also there is a useful Node package - *npm joi*
```javascript
const Joi = require('joi');

...

app.post(...
// define shema
	const schema = Joi.object({
	        name: Joi.string().min(3).required()
	    });
	const result = schema.validate(req.body);
```

The result code is looks like that:
```JavaScript
app.post('/api/courses', (req, res) => {
    // Validate the request body
    const schema = Joi.object({
        name: Joi.string().min(3).required()
    });

    const result = schema.validate(req.body);

	// if raised error it will display the cause
    if (result.error) {
        // If validation fails, send a 400 Bad Request response
        res.status(400).send(result.error.details[0].message);
        return;
    }
  
    const course = {
        id: courses.length + 1,
        name: req.body.name
    };
    courses.push(course);
    res.send(course);
});
```

### PUT
```JavaScript
app.put('/api/courses/:id', (req, res) => {
    // Look up the course
    // if not existing, return 404
    const course = courses.find(c => c.id === parseInt(req.params.id));
    if (!course) return res.status(404).send('The course with the given ID was not found.');

    //validate the course
    // if invalid, return 400 - Bad Request
    const { error } = validateCourse(req.body); // object destruction

    if (error) {
        // If validation fails, send a 400 Bad Request response
        res.status(400).send(error.details[0].message);
        return;
    }

    // Update course
    course.name = req.body.name;

    // return the updated course
    res.send(course);
});

  
// validation function with Joi
const validateCourse = (course) => {
    const schema = Joi.object({
        name: Joi.string().min(3).required()
    });
    return schema.validate(course);
};
```
Here we use Joi scheme to create a validation function that we are gonna use in PUT and POST requests. Also, we use object destruction for result, we only need an error. Thank to the Joi validation function we can simplify the error message `name: Joi.string().min(3).required()` this means that **name** is a *string*, minimum *3 characters* long and *required*. 

### DELETE
```JavaScript
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
```

Here we use the same syntax and code as we used earlier. But we find a course with `indexOf()` method and DELETE it by its index. To delete a course we need to use postman API and navigate to /api/course/:id of the course we want to delete.