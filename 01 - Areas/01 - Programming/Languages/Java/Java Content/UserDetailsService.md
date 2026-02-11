---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
# UserDetailsService
This is an **interface** with the main method `loadUserByUsername()`.
It should be implemented and along with the method. 

There are **built-in implementations**:
- *InMemoryUserDetailsManager*
- *JdbcUserDetailsManager*
- *LdapUserDetailsManager*

# UserDetails
The method **returns** `UserDetails` object. 
`UserDetails` is also an interface and needs to be implemented with its methods such as `getUsername()`, `getPassword()`, etc. 

This object is used in **Authentication process**.