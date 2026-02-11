---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
# What is DependencyInjection?

For example, we have a code from [[How Spring works]]. And we start our app.
After that, Spring sees that there is a dependency in this code on line 5:
```java
@Component
@RequiredArgsConstructor
public class Character {
	@Qualifier("${difficulty.weapon}")
	private final Weapon weapon; // dependency

	public Character (Weapon weapon) {
		this.weapon = weapon;
	}
}
```

That means that firstly Spring needs to inject this dependency (create and inject this weapon).

To do so, it looks for this Weapon in **ApplicationContext** and creates a Character Object after injecting the dependency of Weapon.

In the end, it adds a Character Object to AppContext.

This works very fast because of HashMap used in ApplicationContext.

---

# Ways of use
- Via **constructor** (`<consturctor-arg ref="">`)
- Via **setter** (`<property name="" ref="">` + create empty constructor)
	- The thing is that if the name of the setter is (e.g.) `setMusic`, then the `name` should be `name="music"`, if the setter was `setSong` -> `name="song"`.
	- Can be created a `.properties` file, where values for class variables can be stored. Like that:
```xml
    <context:property-placeholder location="classpath:musicPlayer.properties"/>

    <bean id="musicBean"
            class="com.example.demo.RockMusic">
    </bean>

    <bean id="musicPlayer"
            class="com.example.demo.MusicPlayer">
        <property name="music" ref="musicBean"/>

        <property name="name" value="${musicPlayer.volume}"/>
        <property name="volume" value="${musicPlayer.volume}"/>
    </bean>
```
```properties
musicPlayer.name=Some name
musicPlayer.volume=72
```

- There are many configurations of injection (scope, factory method, etc.)
- Via **XML**, **annotations** or **Java-code**
- This process can be automized (**Autowiring**)