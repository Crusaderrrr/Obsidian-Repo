---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - JavaScript
  - node_js
  - RESTful_API
  - programming
  - express_js
note type: Informational Note
---
**Representational State Transfer** - convention for building HTTP services or an *architectural style* for designing networked applications.
We use HTTP to manipulate data with **CRUD** operations:
- Create
- Read 
- Update 
- Delete

For example, we have a company Fair Wheels, its exposition is:
- `http://fairwheels.com/api/customers`
	- `http://` can be `https://`
	- domain - `fairwheels.com`
	- `api` - not compulsory
	- `customers` - refers to our collection of customers
		- all the operations with customers can be done by sending HTTP request 

**HTTP request** is a keyword:
- GET - request data
- POST - creating data 
- PUT - updating data
- DELETE - deleting data

- To get the list of customers we need to send `GET` request to `/api/customers` and service should send something like this:
```JavaScript
[
{"id" : 1, "name": "name1"}
{"id" : 2, "name": "name2"}
...
]
```

- If we want a single customer, we should send a `GET` request to `/api/customers/1`
- If we want to *update* a customer we should send a `PUT` request to this endpoint `/api/customer/1` and we should include a customer object in a body of the request, like `{name: ''}`
- If we want to *delete* a customer we just need to send a `DELETE` request without any objects to `/api/customers/1`
- if we want to *create* a customer we need to send `POST` request to `/api/customers` with the object of this customer in the request's body

**List**:
- `GET /api/customers` 
- `GET /api/customers/1`
- `PUT /api/customers/1`
- `DELETE /api/customers/1` 
- `POST /api/customers` 

## Use of Express.js
```JavaScript
const express = requre('express'); // importing module 

const app = express();

// routes
app.get()
app.post()
add.put()
add.delete()
```

