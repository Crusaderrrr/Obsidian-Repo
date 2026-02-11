---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
# Generics in Java

- **Generics** allow you to write classes, interfaces, and methods with a placeholder for types.
- They enable **type safety** by allowing you to specify the type of objects a collection or method can work with.
- Example: `List<String>` means a list that holds only `String` objects.
- Benefits:
  - Prevents runtime errors by catching type mismatches at compile time.
  - Eliminates the need for type casting.
  - Improves code reusability and readability.
- Syntax uses angle brackets: `<T>`, `<E>`, `<K, V>`, etc., where letters stand for "Type", "Element", "Key", "Value", etc.

Example method with generics:
```java
public <T> void printArray(T[] array) {  
	for (T element : array) {  
		System.out.println(element);  
	}  
}
```

Bro Code Example:
```java
public class Box<T> {

	T item;

	public void setItem(T item) {
		this.item = item;
	}

	public T getItem() {
		return this.item;
	}
	
}
```
*Good explanation*:
- Basically we have implemented a simple real box
- We can put something inside
- We can take it from there 
- It can be anything we want (String, int, double, etc.)

*Types*:
- **T**: Type
- **E**: Element
- **K**: Key
- **N**: Number
- **V**: Value
