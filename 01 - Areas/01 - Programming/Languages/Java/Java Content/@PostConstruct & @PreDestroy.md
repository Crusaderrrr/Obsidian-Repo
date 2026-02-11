---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
##  `@PostConstruct` and `@PreDestroy`

```java
@Component
public class ClassicalMusic implements Music {
	
	@PostConstruct
	public void doMyInit() {
		System.out.println("Doing my initialization");
	}
	
	@PreDestroy
	public void doMyDestroy() {
		System.out.println("Doing my destruction");
	}
}
```

Those define **init** and **destroy** methods.
