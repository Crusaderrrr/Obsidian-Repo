---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
For every XML tag there is a @Configuration annotation.

While using XML config, we need to specify the path to applicationContext.xml file with instructions, but it should be different when using java annotaions:
![[Pasted image 20250821114443.png]]

---

**For bean creation**:
```xml
<bean id="someBean"
	class="com.example.demo.SomeBean">
<bean/>	
```
this is equal to:
```java
@Configuration
public class SpringConfig {
	@Bean
	public SomeBean someBean() {
		return new SomeBean();
	}
}
```
we also can use @Scope annotation here.

---
## Dependency injection with annotaions:
![[Pasted image 20250821114606.png]]

---

## Value injection from external file

If we have an xml file with some values:
![[Pasted image 20250821114929.png]]

