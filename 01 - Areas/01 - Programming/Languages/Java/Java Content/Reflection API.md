This is a java package, also an API, that is used to manipulate classes using their metadata.

**Simple example**:
```java
public class SpringBootApplication {
	public static void run(Class<?> mainClass) {
		// call methods
		// scan annotations
		// scan package names
		// etc.
	}
}

//===============================Usage========================================

SpringBootApplication.run(MyApp.class);
```

**Some features**:
- *Class inspection* (package name, name, parent class, etc.)
- *Field access* (read, write)
- *Method invocation*
- *Instantiation without* `new`
- *Annotation reading* 


<mark style="background:#ff4d4f">IMPORTANT</mark> - all fields and methods can be accessed, even private

> [!attention]
> The use of reflection API is **slower** then direct method invocation, or any other operation

A normal method call is compiled to a direct bytecode instruction. A reflective call goes through the JVM's metadata layer — it has to resolve the method, check access, and dispatch dynamically at runtime.