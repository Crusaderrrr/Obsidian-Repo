---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
*Example of the component*:
```java
@Component
@RequiredArgsConstructor
public class Character {
	@Qualifier("${difficulty.weapon}")
	private final Weapon weapon;
}
```

**application.yaml** file:
```yaml
difficulty:
	weapon: sword
```

This shows, that Spring is more flexible for instant changes.
Here, when changing the weapon, Spring automatically will change it when it changes in `application.yaml` file.
To apply changes we need to reload the program, very simple!