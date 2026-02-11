---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
These are API endpoints, which handle HTTP requests, such as GET, POST, PUT, DELETE. 
- Every controller can have many methods
- Often, every method corresponds to a single URL
- Normally, methods return Strings, but also can return JSON for example
- A method can have any name

Controllers use mappings that correspond to HTTP requests:
- [[@GetMapping]] 
- @PostMapping 
- @PutMapping
- @DeleteMapping
- @PutMapping

There is another annotation:
*@RequestMapping*:
```java
@Controller
@RequestMapping("/people")
public class PersonController {...
```
All the method of this class will have `/people` at the beginning.