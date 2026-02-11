---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
- This means **many** (POLY) forms (MORPH). 
- Can be achieved by using interfaces also
If we want to put different object to one array, the type of array should be a superclass of all the objects:
```java
Vehicle vehicles = {car, bike, boat};
```

car, bike and boat are objects made from classes, these classes are subclasses of the `Vehicle` class.

# Runtime polymorphism
When the method that gets executed is decided at the runtime based on the actual type of the object.

```java
Animal animal;

System.out.print("Would you like a dog or a cat? (1 = dog, 2 = cat): ");
int choice = scanner.nextInt();

if (choice == 1) {
	animal = new Dog();
	animal.speak();
}
else if (choice == 2) {
	animal = new Cat();
	animal.speak();
}
```

