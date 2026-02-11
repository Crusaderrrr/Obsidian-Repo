---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
This is hierarchy of the classes.
If we have a parent class `Animal`:
```java
public class Animal {
	boolean isAlive;

	Animal () {
		isAlive = true;
	}

	void eat(){
		System.out.println("The animal is eating");
	}
}
```

We can extend this class with two more classes like `Cat` and `Dog`:
```java
public class Cat extends Animal {

}

public class Dog extends Animal {

}
```

- After this all the `Animal` methods and variables will be accessible within `Dog` and `Cat` classes.
- These classes can also have their own methods.
## Advantages
- If we have 1000 classes where we need to make changes and all these classes have the same methods, we can link them to one parent class and make all the necessary changes in one place.
- **DRY**