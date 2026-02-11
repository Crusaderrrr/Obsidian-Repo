---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
This is the part of Spring that manages application security.
It consists of **5 principles**: 
1. *Authentication* -> Who is it?
2. *Authorization* -> Can he do that?
3. *Principal* -> Currently logged in user
4. *Granted Authority* -> some kind of role based authorization
5. *Roles*

- [Spring Security Configuration](https://spring.io/guides/gs/securing-web)
- [[UserDetailsService]]
- [[LDAP]]
- [[JWT Authentication]]
- [[CSRF Token]]
- [[BCryptPasswordEncoder]]

---
# What it does?
- Adds mandatory authentication for URLs
- Adds login form
- Handles logic errors
- Creates a user and sets a default password

---
# Authentication Flow
- [[Spring Security Authentication flow.canvas|Spring Security Authentication flow]]

---

> [!error] Deprecated content

Spring Security has **authentication manager**, which performs all the auth operations, but we don't need to interact with it directly. Instead we work with *AuthenticaitonManagerBuilder*, which we need to configure.

In SS there is class that has a `configure()` method that takes in AuthenticationManager as  parameter and allows us to *extend* it or *override* its methods.

--- 

# Modules
- **Password Encryption** with BCrypt
	
- **JWT / Token based Authentication**: Replace form login with stateless token authentication, usually with custom filters.
    
- **OAuth2 / OIDC Login**: Integration with external authentication providers using `.oauth2Login()`.
    
- **Custom UserDetailsService**: Instead of in-memory users, load from a database or external provider.
    
- **Session Management**: Configure session policies like stateless or concurrent session controls.
    
- **CSRF Protection**: Configure or disable as needed for your API or app type.
    
- **HTTP Basic Authentication**: Use `.httpBasic()` for basic auth instead of form login.
    
- **CORS Configuration**: Manage CORS policies within the HTTP security configuration.

---
# Authentication

### JDBC 
- It needs a `dataSource` [[Database]].
- Has default schema with two tables: 
	- `users (username, password, enables)`
	- `authorities (username, priority)`
- If you database's schema differs, should specify this in the configuration
- Compatible with any database (PostgreSQL, MySQL, etc.)

### JPA 
- It includes ORM implementation (Hibernate).
- It uses **DaoAuthenticationProvider**

Two **dependencies**:
- Spring Data JPA
- Driver for the database (PostgreSQL, etc. )

**Configuration**:
1. Create an implementation of [[UserDetailsService]]
2. Create an implementation of *JPA Repository*, which provides some basic database query logic (can be extended)
3. Define the necessary *models*
4. Configure Database connection in `application.properties`

 