---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
note type: Informational Note
---
**Примитивные**: string, number, bigint, boolean, undefined, symbol, null.
**Объекты**: object, array, function.

*Bigint*: 
- data type that allows us to work with numbers that are bigger or smaller that **number** type supports. 
- To declare it: `const big = 1234567890123456789012345678901234567890n;`  add `n` at the end.
- Does not support Math module operations.

*Symbol*: 
- Unique, unchangeable primitive data type added in **ES6**.
- Every symbol is unique even if was created with the same description:
  ```javascript
const sym1 = Symbol('id');
const sym2 = Symbol('id');
console.log(sym1 === sym2); // false
```
- Its main purpose is to create a unique identifications for an object properties, in order to prevent a name conflict. 