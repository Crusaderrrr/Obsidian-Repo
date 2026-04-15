**Best practice**:
```java
public class Circle { 
	private static final double PI = 3.14159; 
}
```

The decision on whether it should be `static` or not comes down to:
- If we use `static` then the only one instance of that variable is created in memory for ALL the instances of that class
- If we DON'T use it, then every instance would have its own:
```java
// Per-instance — each object has its own 
private final String userId;
```