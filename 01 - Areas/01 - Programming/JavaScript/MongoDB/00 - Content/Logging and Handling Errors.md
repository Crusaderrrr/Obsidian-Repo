---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - node_js
  - mongodb
note type: Informational Note
---
### Server Selection Error 
In the `cars.js` we have an issue in handling GET request:
```JavaScript
router.get('/', async (req, res) => {
  try {
    const car = await Car.find().sort('name');
    res.send(car);
  } catch (error) {
    res.status(500).send('Something Failed') // 500 -> server error
  }
});
```
before we didn't implement the `.catch()` method for the Promise, now yes with **try-catch block**.

We can eliminate the try-catch by creating a middleware function:
```JavaScript
module.exports = function asyncMiddleware (handler) {
  return async (req, res, next) => {
    try {
      await handler(req, res)
    } catch (error) {
      next(error)
    }
  }
};
```

and we can implement if like that, after importing:
```JavaScript
router.get('/',asyncMiddleware(async (req, res) => {
  const car = await Car.find().sort('name');
  res.send(car);
}));
```
### Error Middleware 
To make it simpler to modify behavior when error occurs, we can create a new middleware function `error.js:
```JavaScript
module.exports = function(err, req, res, next) {
  // Log the error
  res.status(500).send('Something Failed') // 500 -> server error
};
```
then we import it on the top of the `index.js` file. 
And we `app.use(error);` after all the middleware functions we have.


## The Best Way
Just to install a `npm i express-async-errors` that just need to be imported in `index.js`. And if error occurs, this module will handle it.

### Logging Errors 
The library - `winston`
It helps with handling errors and it's information (when, how, etc.)
We need to modify our `error.js` middleware:
```JavaScript
const winston = require('winston');

const logger = winston.createLogger({

    transports: [
      new winston.transports.File({filename: 'error.log', level: 'error', format: winston.format.combine(winston.format.timestamp(), winston.format.json())}),

      new winston.transports.Console({format: winston.format.combine(winston.format.colorize(), winston.format.simple()), level: 'info'})
    ]
  });

module.exports = function(err, req, res, next) {
  logger.error({message: err.message})
  res.status(500).send('Something Failed').end() // 500 -> server error
};
```
**Description of the code**:
- Creates a logger function that manipulates logging errors
- This logger is configured with an array of *transports*:
	- Transports determine where log messages are sent and how they are formatted.
	- Logs are written to a file named `error.log`
	- **Level**: Set to 'error', meaning only messages logged at the *error level* or higher (e.g., error, but not info or debug) are written to this file.
	- Console transport determines behavior in the console

#### Logging to MongoDB
Uses: `winston-mongodb` module.
In `error.js` we just need to require it: `require('winston-mongodb');`
and we add:
```JavaScript
logger.add(new winston.transports.MongoDB({db: "mongodb://127.0.0.1:27017/FareWheels"}))
```
in the same file..
The next time the error will be stored in MongoDB

#### Uncaught Exceptions 
Those are errors that occur outside of the Express and could not be caught.
```JavaScript
logger.exitOnError = false;
logger.exceptions.handle(
  new winston.transports.File({ filename: 'exceptions.log'})
);
```

or 

```JavaScript
exceptionHandlers: [
    new winston.transports.File({ filename: "exceptions.log"})
  ],
  exitOneError: false,
```
inside the logger.

#### Promise Rejection 
The same as with uncaught errors:
```JavaScript
rejectionHandlers: [
    new winston.transports.File({filename: "rejections.log"})
  ],
```
inside of the logger

or 

```JavaScript
logger.rejections.handle(
  new winston.transports.File({
    filename: "rejections.log"
  })
)
```

### Extracting 
Here we will extract and structure better our application.
Create a `initialize` folder and add these files:
![[Pasted image 20250505203057.png]]

#### Routes 
We need to create a new folder: `initialize` and create a file `routes.js` there:
```JavaScript
const config = require('config');
const companies = require('../routes/companies');
const home = require('../routes/home');
const customers = require('../routes/customers');
const cars = require('../routes/cars');
const rentals = require('../routes/rentals');
const users = require('../routes/users');
const auth = require('../routes/auth');
const express = require('express');
const error = require('../middleware/error')

module.exports = function (app) {
  app.use(express.json());
  app.use(express.urlencoded({ extended: true}));
  app.use(express.static('public'));

  app.use("/api/companies", companies);
  app.use("/", home);
  app.use("/api/customers", customers);
  app.use("/api/cars", cars);
  app.use("/api/rentals", rentals);
  app.use("/api/users", users);
  app.use("/api/auth", auth)
  
  app.use(error);
};
```

All of these were moved from `index.js`

#### Logging logic
```JavaScript
require("express-async-errors");

const winston = require('winston');
require('winston-mongodb');

const logger = winston.createLogger({
  transports: [
    new winston.transports.File({
      filename: 'error.log',
      level: 'error',
      format: winston.format.combine(
        winston.format.timestamp(),
        winston.format.json()
      )
    }),
    new winston.transports.Console({
      format: winston.format.combine(
        winston.format.colorize(),
        winston.format.simple()
      ),
      level: 'info'
    })
  ],
  // exceptionHandlers: [
  //   new winston.transports.File({ filename: "exceptions.log"})
  // ],
  // exitOneError: false,
  // rejectionHandlers: [
  //   new winston.transports.File({filename: "rejections.log"})
  // ],
});

logger.add(
  new winston.transports.MongoDB({
    db: "mongodb://127.0.0.1:27017/FareWheels",
    level: "error"
  })
);

logger.exitOnError = false;

logger.exceptions.handle(
  new winston.transports.File({
    filename: 'exceptions.log'
  }),
  new winston.transports.Console({
  })
);
logger.rejections.handle(
  new winston.transports.File({
    filename: "rejections.log"
  })
)

module.exports.logger = logger;
```

#### Database
```JavaScript
const { logger } = require('./logging');
const mongoose = require('mongoose');
  
module.exports = function () {
	  mongoose  .connect('mongodb+srv://admin:tP9GwCG5jZojsOcf@farewheels.jn9lcej.mongodb.net/FareWheels?retryWrites=true&w=majority&appName=FareWheels')
    .then(() => logger.info('Connected to MongoDB'));
};
```
we don't use `.catch()` block because we already have **winston** that handles all the errors.

#### Config
```JavaScript
const config = require('config');

module.exports = function () {
  if (!config.get("jwtSecretKey")) {
    throw new Error('FATAL_ERROR: JWT Secret Key is not defined')
  }
};
```
if there is no token provided: `"message":"uncaughtException: FATAL_ERROR: JWT Secret Key is not defined`

#### Joi 
```JavaScript
const Joi = require('joi');

module.exports = function () {
  Joi.objectId = require('joi-objectid')(Joi);
};
```

#### Server 
```JavaScript
const port = process.env.PORT || 3000;
const { logger } = require('./logging');

module.exports = function (app) {
  app.listen(port, () => logger.info(`Listening on port ${port}...`));
};
```
we use app as an argument because we have a dependency `app.listen(...`