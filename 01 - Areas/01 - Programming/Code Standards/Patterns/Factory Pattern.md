---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - patterns
  - clean_code
note type: Informational Note
---
Sometimes using `new` operator isn't so efficient and leads to bugs and high coupling, which is bad.

There is a *Simple Factory*, which is not a pattern, it is idiom of programming. And many confuse it  with **Factory pattern**.

This is how it works (example with pizza store):
![[Pasted image 20250821154706.png]]
Basically, it encapsulates the logic of creation of new objects, the program does it for us, using some logic, like:
![[Pasted image 20250821154857.png]]

This is how factory method should be declared:
![[Pasted image 20250821155018.png]]

## How Simple Factory Works:

1. A factory class (e.g., `SimplePizzaFactory`) has a method (e.g., `createPizza(type)`) that takes input (like a pizza type).
2. Depending on the input, the factory instantiates and returns an appropriate subclass object (like `CheesePizza`, `PepperoniPizza`, etc.).
3. The client code requests objects through this factory instead of directly calling constructors.
4. This encapsulates object creation and allows easy addition of new products by modifying the factory without changing the client.

---

# Factory method pattern

**It is not a Simple Factory**.
It is a way of design, when the base class is defining the method to create an object, but the actual sub-class decides how to implement this method and which object is gonna be created.

This is **visual explanation**:
[[Factory method (explanation).canvas|Factory method (explanation)]]

This is the structure of classes and interfaces (concrete - classes that implement interfaces):
![[Pasted image 20250821161349.png]]
```java
// Абстрактный продукт
abstract class Product {
    public abstract void use();
}

// Конкретные продукты
class ConcreteProductA extends Product {
    @Override
    public void use() {
        System.out.println("Используется продукт A");
    }
}

class ConcreteProductB extends Product {
    @Override
    public void use() {
        System.out.println("Используется продукт B");
    }
}

// Абстрактный создатель с фабричным методом
abstract class Creator {
    // Фабричный метод
    public abstract Product factoryMethod();

    public void operation() {
        Product product = factoryMethod();
        product.use();
    }
}

// Конкретные создатели
class ConcreteCreatorA extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProductA();
    }
}

class ConcreteCreatorB extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProductB();
    }
}

// Клиентский код
public class FactoryMethodExample {
    public static void main(String[] args) {
        Creator creatorA = new ConcreteCreatorA();
        creatorA.operation();  // Используется продукт A

        Creator creatorB = new ConcreteCreatorB();
        creatorB.operation();  // Используется продукт B
    }
}
```
