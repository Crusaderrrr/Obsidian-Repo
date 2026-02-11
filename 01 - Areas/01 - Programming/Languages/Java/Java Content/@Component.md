---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
##  `@Component`

- It is used to tell Spring to create bean.
- We can specify the *id*, if not specified, default id is set. Default is the name of the class but starting with small letter `rockMusic`

To use this annotation we need to add this line: 
`<context:component-scan base-package="com.example.demo"/> ` to applicationContext.xml

*Example*:
```java
@Component("componentId")
public class SomeClass {}
```