---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
# If
This is such as in **JavaScript**:
```java
if (condition1) {
	//code
	
} esle if (condition2) {
	//code
	
} else {
	//code
	
}
```

There can be dozen *else if* statements.
In general all the logic like `!= or ==` is like in java script.

# Ternary operator
```java
int score = 55;

String passOrFail = (score >= 60) ? "PASS" : "FAIL";
```
*works like in JS*

## Switch
```java
String day = ...;

switch (day) {
	case "Monday" -> System.out.print("Ебать того всё...");
	case "Tuseday" -> ...
	...
	// could be: case "Monday", "Tuseday", etc. -> ...;
	default -> System.out.print("This is not a day"); 
}
```
*works like in JS* 

# Logical Operators

They are like in JS also (and work the same way):
- `&&` - AND
- `||` - OR
- `!` - NOT