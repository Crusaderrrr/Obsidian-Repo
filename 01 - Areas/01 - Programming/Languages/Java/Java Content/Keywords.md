---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
# Static
Makes a variable or a method belong to the class rather than to any specific object.
Commonly used for utility methods or shared resources.
### Variable
```java
public class Friend {
	static int numOfFriedns;
	String name

	Friend (String name) {
		this.name = name;
		numOfFriends++;
	}
}
```

- If `numOfFrineds` is not static, every new Friend object will have its own `numOfFriends`.
- Otherwise, the `numOfFriends` is gonna be the same for every object of this class. This means that when creating a new instance, this variable is gonna be +1 and from every of the created instances we will see the same number - amount of created instances.

### Method
- Static method are called directly with the class name, not the object.
```java
public class Friend {
	static int numOfFriedns;
	String name

	Friend (String name) {
		this.name = name;
		numOfFriends++;
	}

	static void showFriends() {
		System.out.println("You have " + numOfFriends + " friends");
	}
}
```

- in static methods we don't need to use `this.numOfFriends` instead we use just `numOfFriends`. 
It can be called like that:
```java
Friend.showFrineds(); //number of Frined objects
```

# Super
This is a special keyword, that means *parent* (subclass <- superclass). 
Is used in constructors and method overriding.

*For example* if we have a `Person` parent class with this constructor:
```java
Person(String first, String last) {
	this.first = first;
	this.last = last;
}
```
And we want to create a `Student` child class, but with modified constructor (adding a **gpa** parameter). We need to use *super*.
```java
Student(String first, String last, double gpa) {
	super(first, last);
	this.gpa = gpa;
}
```

# Final
Used to restrict user access to a certain variable or a method, class.
### Variable
If defined with a variable, this variable becomes constant and **cannot be changed** after defining.
```java
final int MAX_VALUE = 100;
```

### Method
If the method is defined with it, it **cannot be overridden**. 
```java
class Parent {
    final void show() {
        System.out.println("This is a final method.");
    }
}
```

### Class
A class defined with this keyword **cannot be extended**.
```java
final class Utility {
    // class body
}
```