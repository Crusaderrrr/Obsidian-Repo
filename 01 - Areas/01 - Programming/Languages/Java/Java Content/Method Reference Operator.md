---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
A Method Reference Operator looks like this: `::`. 
It is used to make a reference to the method of any instance, like a class or object, etc.
It is used for conciseness, readability, and avoiding boilerplate code

It can be used in many situations, even in [[Streams]]. 

*Examples*:
```java
list.forEach(item -> System.out.println(item));
// could be done like that:
list.forEach(System.out::println);

// Example with map:
.map(s -> s.toUpperCase())
.map(String::toUpperCase)
```
- `String::toUpperCase` is a reference to the `toUpperCase` method of the String class.