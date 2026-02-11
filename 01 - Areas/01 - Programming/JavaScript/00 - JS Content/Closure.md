---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
note type: Informational Note
---
A closure is a feature of JavaScript that allows creation of functions that are capable of remembering the data from the outer function:
```javascript
function outer() {
	let count = 0; 
	function inner() { 
		count++; 
		console.log(count); 
	} 
	return inner; 
} 
const counter = outer(); 
counter(); // 1 
counter(); // 2
```

This can be used for *encapsulation* and to hide sensitive data or implementation details.
