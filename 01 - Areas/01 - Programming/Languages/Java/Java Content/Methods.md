---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
There is no functions in Java, there are **Methods**.
If we wanna call a method inside one *static* method, the nested one should also have static keyword. 

```java
static void greet(String name, int age) {
	System.out.println("Hey $s, you are %d years old", name, age)
}

//also could something like this
static double square(double number) { return number * number; }

//calling a method 
double result = square(2); // 4
```

# Overloaded methods
These are methods that share the same name, but different parameters.
Used to make a program more felxible.

*Example*:
```java
static double add(double a, double b) {
	return a + b;
}
static double add(double a, double b, double c) {
	return a + b + c;
}

//now we can perfor two types of operations without getting an error
double res1 = add(1, 2); // 3
double res2 = add(1, 2, 3); // 6
```

# Varargs
```java
static void add(int... numbers) {
	//code
}
```

This basically works like `*args` in Python. *Int* is type (could be double, byte, etc.), *numbers* is a variable name.

# Method overriding
When we have a child class that needs to implement a different behavior that the parent one, we should specify the `@Override` quote.

*For example*: if we have `Animal` parent class and `Cat`, `Dog` and `Fish` child classes. `Animal` has one method `move()` that prints something like this: **"The animal is running"**, but `Fish` swim, they don't run. So, in `Fish` class we add `@Override` before a method and modify it so fish class gives us this: **"The animal is swimming"**, on `move()`.

- Also adding this keyword is a good approach that could help debugging.

# .toString() Method

If we print an object directly the hash will be logged to the console.
To make details appear instead of a hash we do this:
```java
public class Person {
	@Override
	public String toString() {
		return this.name + " " + this.lastName + " " + this.age;
	}
}
```

By doing so, when calling
```java
Person person1 = new Person("Nikita", "Bulash", 19)
System.out.println(person1); // Nikita Bulash 19 (not a hash)
```