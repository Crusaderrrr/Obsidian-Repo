---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Original [Spring guide](https://spring.io/guides/gs/authenticating-ldap)
**LDAP** (Lightweight Directory Access Protocol). 
- Stores organizational information (it handles a organization "tree", )
- In terms of Spring it refers to use of LDAP as a protocol to authenticate and authorize users
- Is used with LDAP server 

**Configuration**:
1. Add dependencies.
2. Configure connection in `application.properties`
3. Define `ldap-data.ldif` files in templates with data representation settings.
4. Configure LDAP inside the `SecutiryConfiguration` according with the files above.

---
## When to use it?

LDAP is basically used *inside corporations and organizations* that have a hierarchy of workers to manage their systems better based on roles and access needs. LDAP provides a centralized directory service to store and organize user information hierarchically, reflecting organizational structure