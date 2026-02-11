---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
This is a method of logic encapsulation, which is called **Data Access Object**.

For example:
- we have a person model
- we want to make queries to our db to manipulate person data
- we encapsulate the logic of querying db in `PersonDAO` class 
- this class will be connected to a `Person` class model and will exchange data with both: db and this class