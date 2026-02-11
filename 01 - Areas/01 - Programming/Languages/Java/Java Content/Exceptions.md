---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
# What is an Exception
An **exception** is an event that disrupts a normal flow of the program.
Exception handling is a mechanism to handle runtime errors such as *ClassNotFound*, *IO*, *SQL*, etc.

Problem occurs -> Create Exception -> Throw Exception -> Handle Exception

# Error vs Exception

| Error                     | Exception                              |
| ------------------------- | -------------------------------------- |
| Imposible to recover from | Possible to recover from               |
| Are of Unchecked Type     | It can be either checked or unchecked  |
| Happen at runtime         | Can happen at runtime and compile time |
| Caused by the environment | Caused by application                  |

# Exception Hierarchy
![[Pasted image 20250817162502.png]]

| Checked                                 | Unchecked              |
| --------------------------------------- | ---------------------- |
| Checked by the compiler at compile time | Occurs on execution    |
| Cannot be ignored and must be handled   | aka runtime exceptions |
|                                         | Ignored on compilation |
*Format Exception example*:
```java
class Exception {
	public static void main(String[] args) {
		try {
			// code
		} 
		catch (Exception e) {
			// code
		}
	}
}
```