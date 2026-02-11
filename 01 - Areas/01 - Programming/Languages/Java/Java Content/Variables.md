---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
# Intro

A Java variable can be **Primitive** or **Reference**:
- <mark style="background: #ABF7F7A6;">Primitive</mark> - simple value that is stored directly in memory (*stack*).
	- `int` - a whole number 
	- `double` ~ float
	- `char` - character (letters, '!',  '$')
	- `boolean` - true/false
- <mark style="background: #ABF7F7A6;">Reference</mark> - memory address (*stack*) that points to the *heap*.
	- `string` 
	- `array`
	- `object`

*Example*:
`int age = 21;` // 21
`in age = 30.5` // Error

We can make a combined str + int log:
`System.out.println("Idi nahuy " + age + " times")` // Idi nahuy 21 time

**String**
- Declaration: `String name = "Nikita";`
- `.substring(start, end)` method is indexing by a string. End is excluded. *Returns a new string*
- Also instead of using `==` or `===`, there is a method `.equals("string")`

![[Pasted image 20250731171810.png]]

# Scope

**Local scope**:
```java
static void doSomething() {
	int x = 1;
}
```
- Defined inside the method or curly braces {}.

**Class scope**:
```java
public class Main {
	static int x = 3;
...
}
```
- Better for constants and OOP