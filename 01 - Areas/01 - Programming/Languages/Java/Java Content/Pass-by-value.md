---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
**Java is a pass-by-value language**.
## Primitive Type
When the variable is passed to the method, its value is copied, and the method operates with a copy of the original value. So, any operation over the value inside the method will not affect the actual value of the variable.
## Non-primitive Type
Also, exists a **pass-by-reference** construction, where actions inside the method, where the variable is passed as a parameter, affect the actual value of this variable.

So, when the object (non-primitive) is passed to the method, actually, the *copy of the reference* to the object's value in the heap is passed, and the changes applied to the objects data inside the method will reflect on the data in the heap, except, if the reference is not changes in the method.