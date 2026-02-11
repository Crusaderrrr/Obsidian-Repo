---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
`@Component` annotation is used to make spring create an object by itself.

So, when spring creates a component, from now it is called **Bean**. Which is an object created and controlled by Spring.

# How does this work?
If Spring is connected to a project, when the application starts, Spring is beginning to read all the code.

1. Read the code...
```java
@Component  // Spring: uh, I need to create a new object...
public class Sword implements Weapon {
	// some logic
}
```

2. Create new Object...
```java
Sword sword = new Sword();
```

3. Receive a new object in memory.
4. Puts this new object into *vault*.

## What is this *vault*?

This is an internal Spring's place in RAM to store Beans and it is called **ApplicationContext**. It is basically a *HashMap*, where key is a name of the Object ("sword"), that is a name of the class, starting with a small letter,  and value is an object itself (`new Sword()`). 


## Bean Lifecycle
![[Pasted image 20250820181126.png]]

- `init` method 
	- Is executed on **initialization of the bean**
	- Initialization of resources, appealing to external files, database init
- `destroy` method
	- Is executed on **bean destruction**. (or on app termination)
	- Resource cleaning, closing I/O, closing db access.
	- *No Destroy method for prototype beans*. 
- **Both of these methods** should not take any arguments 
- `factory` method
	- this method creates new object by itself
	- we don't need to create an objects
	- if Singleton is used -> only one object will be created, opposite if prototype
```xml
<bean id="musicBean"
	class="com.example.demo.ClassicalMusic"
	init-method="doMyInit"
	destroy-method="doMyDestroy"
	factopry-method="getCLassicalMusic">
</bean>
```