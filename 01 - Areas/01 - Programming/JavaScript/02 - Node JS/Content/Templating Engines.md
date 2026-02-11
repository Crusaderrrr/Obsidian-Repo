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
Used to send an **HTML** file as a response to the client.
On of them is *pug*

```JavaScript
app.set('view engine', 'pug');
app.set('views', './views'); // default (optional)
```

`app.set('view engine', 'pug')`:
- This line sets the **view engine** for your Express application to `pug`.
- A **view engine** is used to render dynamic HTML pages. In this case, the `pug` template engine (formerly known as `Jade`) is being used.
- With this setting, you can create `.pug` files in the `views` directory, and Express will use the `pug` engine to render them into HTML when you call *res.render* in your route handlers.

**Example**: If you have a `views/index.pug` file like this:
```Pug
html
    head
        title= title
    body
        h1= message
```

On our page we will see a Hello message