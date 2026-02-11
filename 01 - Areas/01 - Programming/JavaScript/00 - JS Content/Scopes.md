---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
note type: Informational Note
---
The scope is a "space" in code where the variable is accessible and it depends on what keyword was used when declared a variable.
# Function scoped

`var` *keyword*
It means that the variable declared with var is accessible **inside the function** where it was declared and **inside any other nested functions**, regardless of any blocks (`if`, `for`, etc.).
```javascript
function test() { 
	if (true) { 
		var x = 10; 
	} 
	console.log(x); // 10 (accessible anywhere in the function) 
} 
test(); 
// console.log(x); // Error: x is not defined (not accessible outside the function)
```

# Block scope 

`let`, `const` *keywords*
A variable is **block scoped** if it is accessible **only within the nearest pair of curly braces** `{}` where it was declared (such as inside an `if`, `for`, or any code block).

```javascript
if (true) { 
	let y = 20; 
	const z = 30; 
	console.log(y); // 20 (accessible here) 
	console.log(z); // 30 (accessible here) 
} 
console.log(y); // Error: y is not defined (not accessible outside the block) 
console.log(z); // Error: z is not defined (not accessible outside the block)
```
