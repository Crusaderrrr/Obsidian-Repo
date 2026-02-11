---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
This is a **blueprint** for a class that specifies a set of abstract methods.

This is a list of abstract methods. If the class is implementing an interface, it *should* implement all its methods. As these methods are abstract `@override` should be used.

```java
public class Rabbit implements Prey {
	@Override
	public void flee() {
		System.out.println("The rabbit is running away")
	}
}
```

A class can implement multiple interfaces:
```java
public class Fish implements Prey, Predator {
...
}
```

*Example*:
```java
// Interface declaration
public interface Animal {
    int LEGS = 4; // constant (public static final by default)
    void eat();    // abstract method
    void move();   // abstract method

    // Default method (Java 8+)
    default void sleep() {
        System.out.println("Sleeping...");
    }

    // Static method (Java 8+)
    static void info() {
        System.out.println("Animals are living beings.");
    }
}

// Implementing the interface in a class
public class Dog implements Animal {
    public void eat() {
        System.out.println("Dog eats bone.");
    }
    public void move() {
        System.out.println("Dog runs.");
    }
}

// Using the interface
public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();      // Output: Dog eats bone.
        d.move();     // Output: Dog runs.
        d.sleep();    // Output: Sleeping...
        Animal.info();// Output: Animals are living beings.
    }
}
```

| Aspect                            | Static Methods                             | Default Methods                                  |
| --------------------------------- | ------------------------------------------ | ------------------------------------------------ |
| Associated With                   | Interface itself                           | Instances of implementing classes                |
| How Called                        | `InterfaceName.staticMethod()`             | `instance.defaultMethod()`                       |
| Can Implementations Override      | No                                         | Yes                                              |
| Purpose                           | Utility/helper functions for the interface | Provide default behavior to implementing classes |
| Inherited by Implementing Classes | No                                         | Yes                                              |