---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
The constructor of the class that uses arguments to create an object.
*Example*:
```java
public class Student {

	Student (Sting name, int age, double gpa) {
		this.name = name;
		this.age = age;
		this.gpa = gpa;
	}
	// Class methods like:

	void study() {
		System.out.println(this.name + "is studying."); //uses the name of
		                                                //the entity that                                                             //called
	}
}


// Creating an object
public class Main {
	public static void main(String[] args) {

		Student student = new Student("Nikita", 19, 3.2);
	}
}
```

# Overloaded constructors
Works like overloaded methods in [[Methods]]. Multiple different instances of constructor of the same class, but with different amount of arguments.