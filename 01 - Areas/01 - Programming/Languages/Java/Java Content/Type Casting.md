---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
**Type casting** is the process of converting a variable from one data type to another. This is often necessary when you need to perform operations between variables of different types, or when you need to store a value of one type in a variable of another type. In Java, type casting can be either implicit (automatic) or explicit (requiring a cast operator).

## Implicit (automatic)
```java
public class Main { 
	public static void main(String[] args) { 
		int myInt = 9; 
		double myDouble = myInt; // Automatic casting: int to double 
		
		System.out.println(myInt); // Outputs 9 
		System.out.println(myDouble); // Outputs 9.0 
	} 
}
```

## Explicit (with operator)
```java
public class Main {
  public static void main(String[] args) {
    double myDouble = 9.78d;
    int myInt = (int) myDouble; // Manual casting: double to int

    System.out.println(myDouble); // Outputs 9.78
    System.out.println(myInt);    // Outputs 9
  }
}
```