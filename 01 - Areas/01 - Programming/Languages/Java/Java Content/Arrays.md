---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
Arrays in java is a reference data type. This means that if we have created an array and we use the array name in `System.out.print()` we will see the link to the array in the memory.
# Defining an Array
```java
// 1
String [] arr = {"name1", "name2"};
// 2
ArrayList<String> list = new ArrayList<>(); list.add("Alice"); list.add("Bob");
// 3
ArrayList<String> list = new ArrayList<>(Arrays.asList("Alice", "Bob", "Charlie"));
// 4
ArrayList<String> list = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));
// 5
ArrayList<String> list = new ArrayList<>(10); // capacity of 10
```

- `List.of()` method is very useful. No modules need to be imported.

*Example*:
```java
public static void main(String[] args) {
	String[] fruits = {"apple", "orange", "banana"};
	fruits[0] = "pineapple"; // change or add
	int numOfFruits = fruits.length; // length

	for (int i = 0; i < fruits.length; i++) {
		System.out.print(fruits[i]);
	}

	//other approach
	for (String fruit : fruits) {
		System.out.print(fruit);
	}
}
```

# Sorting arrays 
Need to import `java.util.Arrays`

to use it we need to call `Arrays.sort(array);`

# 2D arrays 
```java
String[][] groceries = {fruits, vegetables, meat};
```

This is an array which elements are also arrays. Like a matrix.

# Array of objects

This could be achieved by creating a class, creating some instances of this class (objects). And then add this object to an array:
```java
public class Car {
...
}

Car[] cars = {car1, car2, car3};

// Iteration by the objects
for (Car car : cars) {
	System.out.println(car);
}
```