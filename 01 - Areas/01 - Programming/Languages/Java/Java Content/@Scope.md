---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
# Singleton

This type of scope means that Spring create a single instance of the object to store in **ApplicationContext**. 
If there are more than one class that uses the Object from AppContext, both or all the classes/Objects with this dependency will use the same instance of the Object from AC.

Using `getBean()` on the context, the same object will be returned.

This type of scope is used on **stateless bean**.

*For example*, if we have `MusicPlayer` bean and we use Singleton on it, and we change the volume of the bean, it will be changed for all the objects created with that bean.

# Prototype

This is the oposite for Singleton, every new bean that is created, has its own state. (**stateful**)

```java
@Component
@Scope("prototype")
public class Mace implements Weapon {
	// logic
}
```

`@Scope` here means that Spring will need to create this Bean only when someone (other Bean, class, etc.) asks for it, and every time this Bean will be new (new instance).

It could also be done like that:
- in applicationContext.xml we need to add a `scope="prototype'` property to the bean.

##  `@Scope`

This is a scope annotation, as told below it can be *singleton*(One object for all instances) or *prototype*(new object for every instance).

![[Pasted image 20250820193400.png]]
