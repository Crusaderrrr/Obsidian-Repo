---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - JavaScript
  - express_js
  - node_js
  - programming
note type: Informational Note
---
In order to **Create an API** we should:
- Create a *models* folder for models of documents from [[Modeling Relationships with Mongoose]] 
- Create a *routes* folder for routes that will handle *HTTP requests* (CRUD)
- Add a reference to the `index.js` file of routes so the API works 

### Key Moments
**Models**:
- We need to make a `mongoose.model()` based on a `mongoose.Schema()`, schema is just a *blueprint* (instructions) for a document, and *model* represents the collection and provides methods to interact with the database.
**Example**:
```JavaScript
const Rental = mongoose.model('Rental', new mongoose.Schema({
  customer: {
    type: new mongoose.Schema({
      name: {
        type: String,
        required: true,
        minlength: 5,
        maxlength: 50
      },
      phone: {
        type: String,
        required: true,
        minlength: 8,
        maxlength: 16
      },
      isPrime: {
        type: Boolean,
        default: false
      },
    }),
    required: true
  },
  car: {
    type: new mongoose.Schema({
      modelName: {
        type: String,
        required: true,
        trim: true,
        minlength: 5,
        maxlength: 255
      },
      dailyRentalRate: {
        type: Number,
        required: true,
        min: 0,
        max: 255
      }
    }),
    required: true
  },
  rentedOn: {
    type: Date,
    required: true,
    default: Date.now
  },
  returnedOn: {
    type: Date
  },
  rent: {
    type: Number,
    min: 0
  }
}));
```

**Imports**:
- We need to import those models in *routes file*:
```JavaScript
const { Customer } = require('../models/customer');
const { Car } = require('../models/car');
const { Rental, validateRental: validate } = require('../models/rental')
```
to use them in CRUD requests.
