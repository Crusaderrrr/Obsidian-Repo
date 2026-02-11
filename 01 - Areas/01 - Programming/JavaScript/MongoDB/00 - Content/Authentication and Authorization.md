---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - mongodb
  - node_js
note type: Informational Note
---

**Admin object**:
```json
{
    "name": "Admin",
    "email": "admin@gmail.com",
    "password": "12345678",
    "x-auth-token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2ODFiNDY2MDc5Yjk3Y2MyMWRjNTYzZWUiLCJpYXQiOjE3NDY2MTc5NTN9.imBQtpCa5sWceReBHmh67vJm73q-bKvsvR0eyV8hDWo"
}
```


**Authentication** is a process of identifying whether the user is who they claim they are.
**Authorization** if the user has the right to perform an operation.

To make it possible we need to *register* (POST) users `api/users`
Also, we need to *login* (POST) users `/api/logins`

Firstly we need to create a normal endpoint `api/users` with user model and users.js to handle http requests.

In order to not register one user many times, we need to implement this feature in our user model:
```JavaScript
const User = mongoose.model('User', new mongoose.Schema({
  name: {
    type: String,
    required: true,
    minlength: 2,
    maxlength: 25
  },
  email: {
    type: String,
    unique: true, // this feature
    required: true,
    minlength: 7,
    maxlength: 255
...
```
and also modify a POST request:
```JavaScript
 let user = await User.findOne({email: req.body.email})
 if (user) return res.status(400).send("user already registered");
```

We can send specific user's data to user after register:
```JavaScript
  res.send({
    name: user.name,
    email: user.email
  });
```

Though, there is a useful method to make it with **lodash**:
```JavaScript
  user = new User(_.pick(req.body, ['name', 'email', 'password']))

  await user.save();
  res.send(_.pick(user, ['id', 'name', 'email']));
```
from now we don't need to put a huge amount of code.

### Hashing Passwords
We need to `npm i bcript`
```JavaScript
const bcrypt = require('bcrypt');

async function run() {
  const salt = await bcrypt.genSalt(20) //returns a Promise
  const hashed = await bcrypt.hash('1234', salt)
  console.log(salt);
  console.log(hashed);
}

run(); // $2b$20$kkBHUGwsTfsdBCdQtHp6ve -> slat
	   // $2b$10$d2VjTrfV1cO09375kkRi5.xc1gYJJ4pELVbwILpcIg.AIoIhXKCU6 -> hashed 
```

now we need to add this code to the request handler (users.js) on lines *17-19*:
```JavaScript
router.post('/', async (req, res) => {
  const { error } = validate(req.body);
  if (error) return res.status(400).send(error.details[0].message);

  let user = await User.findOne({email: req.body.email})
  if (user) return res.status(400).send("user already registered");

  user = new User(_.pick(req.body, ['name', 'email', 'password']))
  const salt = await bcrypt.genSalt(10) // this 
  user.password = await bcrypt.hash(user.password, salt) // and this 

  await user.save();
  res.send(_.pick(user, ['id', 'name', 'email']));
});
```

### Authenticating 
```JavaScript
const express = require('express');
const _ = require('lodash');
const bcrypt = require('bcrypt');
const router = express.Router();
const { User } = require('../models/user')

router.post('/', async (req, res) => {
  const { error } = validate(req.body);
  if (error) return res.status(400).send(error.details[0].message);

  let user = await User.findOne({email: req.body.email})
  if (!user) return res.status(400).send("Invalid email or password");
  
  const validPassword = await bcrypt.compare(req.body.password, user.password);
  if (!validPassword) return res.status(400).send("Invalid email or password");
  
  res.send(true);
});

function validate(user) {
  const schema = Joi.object({
    email: Joi.string().max(255).required().email(),
    password:Joi.string().min(8).max(255).required()
  })
  return schema.validate(user);
};

module.exports = router;
```

That's a new routes module - `/api/auth` that is authenticating our users. 
We have defined a new *validate function* in this file and in POST request we validate whether email and password are correct or not.

## JSON Web Token
- it is a long string that identifies a user (passport)
- when we make first http request server sends us a **JWT** 
- for the next *api calls* we will need to use this JWT 
- Those JWT are stored in browser's memory
This is how it looks:
![[Pasted image 20250502220302.png]]

### Generating Authentication Tokens 
Before we send the info to a user, we need to encode it as a jwt token
```JavaScript
router.post('/', async (req, res) => {
...
  const token = jwt.sign({ _id: user._id }, "jwtSecretKey")
  res.send(token);
});
```
the operation on the 3 line is: `jwt.sign(payload, secretOrPrivateKey)`
The key is stored securely. This operation encrypts data into a jwt token, which can be decoded on the *jwt.io* website. 

### Storing secret key in env variable 
Install `npm i config`
In `auth.js`:
```JavaScript
const config = require('config');
...
router.post('/', async (req, res) => {
...
  const token = jwt.sign({ _id: user._id }, config.get("jwtSecretKey"))
  res.send(token);
});
```

In `index.js`:
```JavaScript
const config = require('config');
...
if (!config.get("jwtSecretKey")) {
	console.log("FATAL_ERROR: JWT Secret Key is not defined")
	process.exit(1); // terminate a Node.js process (0: no err, 1: err)
}
```

We need to create two files:
- `default.json` - define the **default configuration settings** for your application
- `custom-environment-variables.json` - map configuration properties to environment variables

Then set the env variable: `$env:farewheels_jwtSecretKey="mySecureKey"`, so this is new jwt key.

**Returning Headers** in the response:
```JavaScript
router.post('/', async (req, res) => {
...
	const token = jwt.sign({ _id: user._id }, config.get("jwtSecretKey"))
	res.header('x-auth-token', token).send(_.pick(user, ['id', 'name', 'email']));
});
```
The response: 
![[Pasted image 20250503180556.png]]

`x-` - *necessary prefix for custom header* 

Now we can implement a useful function in `user.js` that we will use in the `users.js` and `auth.js`. This function will generate the user's token.

`user.js`:
```JavaScript
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    minlength: 2,
    maxlength: 25
  },
  email: {
    type: String,
    unique: true,
    required: true,
    minlength: 7,
    maxlength: 255
  },
  password: {
    type: String,
    required: true,
    minlength: 8,
    maxlength: 1024
  }
});

userSchema.methods.generateAuthToken = function () {
  const token = jwt.sign({ _id: this._id }, config.get("jwtSecretKey"))
  return token;
}
```
- we make a variable for the userSchema , then we create a new function that generates a token.
- The `.methods` property allows you to add custom instance methods to the schema. These methods can be called on individual documents created from the schema.

`users.js`:
```JavaScript
router.post(...)
...
  const token = user.generateAuthToken();
```

`auth.js`:
```JavaScript
router.post('/', async (req, res) => {
  const { error } = validate(req.body);
  if (error) return res.status(400).send(error.details[0].message);

  let user = await User.findOne({email: req.body.email})
  if (!user) return res.status(400).send("Invalid email or password");

  const validPassword = await bcrypt.compare(req.body.password, user.password);
  if (!validPassword) return res.status(400).send("Invalid email or password");

  const token = user.generateAuthToken();

  res.send(token);
});
```

### Authentication Middleware 
We can create a new middleware function in `middleware` folder.
We create a new `auth.js` file there:
```JavaScript
const jwt = require("jsonwebtoken");
const config = require('config');  

module.exports = function (req, res, next) {
  const token = req.header('x-auth-token');
  if (!token) return res.status(401).send('Access denied. No token provided');

  try {
    const decoded = jwt.verify(token, config.get('jwtSecretKey'));
    req.user = decoded;
    next();
  } catch (ex) {
    res.status(400).send('Invalid token')
  }
};
```
- we export directly without defining a function.
- this middleware is used to authenticate users  
- `const token = req.header('x-auth-token');` retrieves the value of the `x-auth-token` header from the request. This header **is expected to contain the JWT** sent by the client for authentication.
- `const decoded = jwt.verify(token, config.get('jwtSecretKey'));` attempts to verify the JWT using the `jwt.verify` method from the *jsonwebtoken* library. It uses the secret key `(jwtSecretKey)` retrieved from the config module (as set in your earlier context). If the token is valid, **decoded contains the payload (data) embedded in the token.**

Also, we can authorize if the user **isAdmin**:
Create a middleware function with a new `admin.js` file:
```JavaScript
module.exports = function (req, res, next) {
	if (!req.user.isAdmin) res.status(403).send("Access denied") // status "Forbidden"
	next();
};
```

and then we can implement it in `companies.js`:
```JavaScript
router.delete("/:id", [auth, admin], async (req, res) => {
    const company = await Company.findByIdAndDelete(req.params.id);

    if (!company) return res.status(404).send('The course with the given ID was not found.');

    res.send(company);
});
```
The `[auth, admin]` means that firstly will work those two middleware functions, and then if everything is okay, the delete request will be executed.



### Where to store JWT
*NOT IN DATABASE* -> it is not safe 
But if we store it in database, at least we need to encrypt it. 
Those tokens give access to the api endpoints and contain passwords and important data, that should not be stolen
**It is better to store them on the client**. 
When sending the token from client to the server - use HTTPS.
