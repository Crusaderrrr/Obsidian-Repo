Creational pattern
Used when we need to construct an object with many fields, with possibly nulls.
Allows us create objects with only necessary fields set.

**Simple builder**:
```java
public class CarBuilder {
	private int id;
	private String brand;
	private String model;
	private String color;
	...
	
	public CardBuilder id(int id) {
		this.id = id;
	}
	
	public CardBuilder brand(String brand) {
		this.brand = brand;
	}
	
	public CardBuilder model(String model) {
		this.model = model;
	}
	
	public CardBuilder color(String color) {
		this.color = color;
	}
	
	public Car build() {
		return new Car(id, brand, model, color)
	}
}

// Class that is built
public class Car {...}
```

---

The **Director** is a class that defines **the order in which to call the builder's steps** — it knows _what_ to build and _in what sequence_, but not _how_ each step is implemented.

**Example**:
```java
class Director {
    private HouseBuilder builder;

    Director(HouseBuilder builder) { this.builder = builder; }

    void buildStandardHouse() {
        builder.buildFoundation();
        builder.buildWalls();
        builder.buildRoof();
    }
}
```

In order to optimize that code we could create a `Builder` interface and use it in the constructor, so the classes that implement that interface could be used in the `Director`'s methods.