---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - node_js
  - JavaScript
  - programming
  - React_JS
  - express_js
note type: Informational Note
---
In Node.js, a **Promise** is like a "promise" you make to do something later. It’s a way to handle tasks that take time (like fetching data from the internet, reading a file, or waiting for a timer) without blocking your code. Instead of waiting for the task to finish, a Promise lets your code keep running and tells you, "I’ll let you know when I’m done—or if something goes wrong."

A Promise can have three states:

1. **Pending**: The task is still running (not done yet).
2. **Fulfilled**: The task finished successfully, and you get the result.
3. **Rejected**: The task failed, and you get an error.
### Why Use Promises?
Imagine you’re ordering food delivery:
- You place the order (the task starts).
- You don’t sit and wait—you do other things (your code keeps running).
- When the food arrives, you eat (task success). If the restaurant cancels, you’re notified (task failure).

### Creating a Promise
```JavaScript
const myPromise = new Promise((resolve, reject) => {
	// Executing of asynchronous functions
})

myPromise
	.then(value => {
		// Do if successful
		// value - argument for resolve function
	})
	.catch(error => {
		// Do if rejected
		// error - argument for reject function
	})
```

### fetch() method 
We can send requests with this method to this web site  

**Two promise** based function to send requests:
```JavaScript
const getData = (url) => 
	new Promise((resolve, reject) => 
		fetch(url)
			.then(response => response.json())
			.then(json => resolve(json))
			.catch(error => reject(error)	
	)

getData('http://...') 
	.then(data => console.log(data))
	.catch(error => console.log(error.message))
```

### async/await 
- it is a special syntax for promises
```JavaScript
async function asyncFn() {
	// Always returns Promise 
}
```

```JavaScript
const asyncFn = async () => {
	// Always returns Promise
}
```

*Example*:
```JavaScript
const asyncFn = async () => {
	return 'Success!'
}

asyncFn()
```
This function will return Promise that will be instantly resolved and his result will be str 'Success!'

*Example 2*:
```JavaScript
const asyncFn = async () => {
	return 'Success!'
}

asyncFn()
	.then(value => console.log(value)) // Success!
```

*Error example*:
```JavaScript
const asyncFn = async () => {
	throw new Error('There was an error')
}

asyncFn()
	.then(value => console.log(value)) 
	.catch(error => console.log(error.message)) // There was an error
```

#### await
- wait for result or other Promise
- can be only used in *async* functions 

```JavaScript
const asyncFn = async () => {
	await <Promise>
}
```