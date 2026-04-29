**Sometimes constructing an object is expensive** — it may involve database calls, complex configuration, or heavy initialization. If you need many similar objects, it's cheaper to clone a pre-configured one and only tweak what differs

The most basic *example*:
```java
public abstract class Shape implements Cloneable {
    String color;

    public Shape clone() {
        try {
            return (Shape) super.clone(); // shallow copy
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }
}

public class Circle extends Shape {
    int radius;

    public Circle(String color, int radius) {
        this.color = color;
        this.radius = radius;
    }
}

// Usage
Circle original = new Circle("red", 10);
Circle copy = (Circle) original.clone();
copy.color = "blue"; // original is untouched
```

In Java there is already an interface `Clonable` that can be used.

`super.clone()` means that `Object.clone()` is called, because [[Keywords|super]] refers to a parent class, but here is no parent class, only interface. Also it would result in an error if the class that calls `super.clone()` is not implementing the `Clonable` interface.