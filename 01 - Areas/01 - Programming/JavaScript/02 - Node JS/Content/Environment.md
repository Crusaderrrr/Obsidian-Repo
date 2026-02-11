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
We can change development environment in order to show on which stage it is.
*Environment examples*:
- Development 
- Production
- ...

To set the environment we can use a `$env:NODE_ENV='production'` or any other environment 
Then we can either use some modules or not, depending on the environment.
```JavaScript
console.log(`Node_env: ${process.env.NODE_ENV}`); // show Node environment 
console.log(`app: ${app.get('env')}`); // show app env

// if dev env -> use morgan module 
if (app.get('env') === 'development') {
	app.use(morgan('tiny'))
}
```

We need to install `config module` and can create a `config` folder with files like: `production.json`, `development.json`, `default.json`. In order to simplify work with environments.

`default.json`
```JavaScript
{
    "name": "My Express Course"
}
```

`development.json`
```JavaScript
{
    "name": "My Express App - Development",
    "mail": {
        "host": "dev-mail-server"        
    }
}
```

`production.json`
```JavaScript
{
    "name": "My Express App - Production",
    "mail": {
        "host": "prod-mail-server"        
    }
}
```

With adding this to our code:
```JavaScript
const config = require('config');

console.log("Application Name: " + config.get('name')); // dev or prod
console.log("Mail server: " + config.get('mail.host')); // dev or prod
```
With changing the environment, the result of this code will change too.

# Password
It is important not to put any secret data or passwords to these files.
To store a password it is better to use environmental variables: 
- `$env:app_password=1234` - setting the password
-  **IMPORTANT** Now we create a file `custom-environment-variables.json` and store the password variable there:
```JavaScript
{
    "mail": {
        "password": "app_password"        
    }
}
```

```JavaScript
const config = require('config');

console.log("Application Name: " + config.get('name')); // dev or prod
console.log("Mail server: " + config.get('mail.host')); // dev or prod
console.log("Mail server: " + config.get('mail.password')); // 1234
```

# Debugging 
Install the debug module with `npm i debug`. 
Create two debug functions:
```JavaScript
const startDebugger = require('debug')('app:startup');
const dbDebugger = require('debug')('app:db');

if (app.get('env') === 'development') {
    app.use(morgan('tiny'));
    startDebugger('Morgan enabled...')
};
```

Set the environment variable:
`$env:DEBUG="app:startup"`
On startup we will get the next information:
```JavaScript
//Application Name: My Express App - Development
//Mail server: dev-mail-server
//Mail password: 1234
  //app:startup Morgan enabled... +0ms
//Listening on port 3000...
```

If we don't want to see the debug info:
`$env:DEBUG=""`

Also we can set various debuggers:
`$env:DEBUG="app:startup", "app:db"`

If we want to use all of them:
`$env:DEBUG="app:*"`