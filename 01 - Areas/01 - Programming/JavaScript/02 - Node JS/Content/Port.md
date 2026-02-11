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
We have a **process** global object that has a **env** method, which is short for environmental variables.
```JavaScript
const port = process.env.PORT || 3000
```
`PORT` is a environmental variable and the code means that, if the PORT is set, we are going to use this, if not -> we use `port = 3000`
The updated code will look like that:
```JavaScript
const express = require('express');
const app = express(); 

app.get('/', (req, res) => {
    res.send('Hello World!');
});  

app.get('/api/courses', (req, res) => {
    res.send([1, 2, 3]); 
});
 
const port = process.env.PORT || 3000

app.listen(port, () => console.log(`Listening on port ${port}...`));
```

`$env:PORT = 5000` - PowerShell command to set the port to 5000
