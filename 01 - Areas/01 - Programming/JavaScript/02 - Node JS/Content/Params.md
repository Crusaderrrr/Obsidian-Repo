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
```JavaScript
app.get('/api/courses/:id', (req, res) => {
    res.send(req.params.id);
});
```
In this code `:id` can be any variable, like `coursesId`, it represents id of a particular course, and then sends a parameters of a course that has this `id`.

So, if we navigate to `http://localhost:5000/api/courses/1` we will se `1` this is the id of a course with id = 1.

`params` is an object

---
```javascript
app.get('/api/posts/:year/:month', (req, res) => {
    res.send(req.params);
});
```
If we navigate to the `http://localhost:5000/api/posts/2023/01` it will give us an object with the year and month we searched

`http://localhost:5000/api/posts/2023/01?sortBy=name` at the end after ? is a query string parameters, we can read them by:
```javascript
app.get('/api/posts/:year/:month', (req, res) => {
    res.send(req.query);
});

```
After navigating to the page we will see {sortBy : "name"}