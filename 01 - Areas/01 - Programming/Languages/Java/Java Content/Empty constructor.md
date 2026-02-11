---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Sometimes we need to define an **empty constructor**:

## JPA and Hibernate

When hibernate fetches some data from the database (e.g. User) it follows these steps:
1. Create an empty entity `new User()` (because it does not know what fields it has).
2. Populate this entity with some data `user.setId(...)`, `user.setName(...)`

If we do not provide an empty constructor for it, Hibernate **cannot execute the first step** (create an empty entity).

## JSON Deserialization

The process is identical:
1. Create an empty instance 
2. Populate it with values

> [!important]

The Java compiler only gives you a free default no-argument constructor *if you don't define any other constructors yourself*.