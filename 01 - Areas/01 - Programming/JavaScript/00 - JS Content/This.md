---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
note type: Informational Note
---
This is a special keyword that is used inside a function to refer to a particular area, depending on where it was called:

1. **В методе объекта:**
```javascript
const user = { 
	name: "Alice", 
	greet() { 
		console.log(this.name); // 'Alice' 
	} 
}; 

user.greet();
``` 

2.  **В обычной функции:**
```javascript
function show() { 
	console.log(this); 
} 

show(); // window (или global в Node.js) в нестрогом режиме, undefined в strict[1][2][4]
```

3. **В стрелочной функции:**
```javascript
const obj = { 
	value: 10, 
	foo: () => { 
		console.log(this.value); // undefined
	} 
}; 

obj.foo();
```
- Arrow function does not have its own *this*.

4. **С помощью call/apply/bind:**
```javascript
function sayHi() {
	console.log(this.name); 
} 

const person = { name: "Bob" }; 
sayHi.call(person); // 'Bob'
```