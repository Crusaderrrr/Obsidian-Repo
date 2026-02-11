---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Spring Boot provides an abstraction over traditional and lightweight Spring Framework, adds some functionality.
- It is used for faster development 
- The configuration is very simple
- Can be used with any additional Spring modules:
	- [[Spring Security]]
	- [[Spring MVC|Spring Web]] (which is Spring MVC for Spring Framework, but its functionality is auto configured) 
	- [[Spring Data JPA]]
- It autoconfigures [[Dispatcher Servlet]] for us.

---
# Pros

When we use a Spring Framework with Spring MVC we need the following things:
- **DAO layer**, where all the database query logic lies.
- Manually configure DispatcherServlet
- Define models 

When using Spring Boot this process gets easier:
- DAO layer is implemented for us and we need to only extend the `JpaRepository` interface, which will provide a DAO logic
- DispatcherServlet is autoconfigured
- Entities and Tables are autocreated
- We need to implement [[UserDetailsService]]