---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
# Aggregation 
It establishes a **has-a relationship**.

Books and Library:
- Library can have books 
- Books can be inside library
- If we delete library that had books, all the books will remain.

# Composition
It establishes a **part-of relationship**.

Car and Engine:
- Car has Engine
- Engine is a part of Car (defined in constructor of the Car)
- If we delete Car, the engine will also be deleted.