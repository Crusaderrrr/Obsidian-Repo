---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
#### 1. Difference between interface and abstract class
| Feature              | Abstract Class                     | Interface                                                 |
| -------------------- | ---------------------------------- | --------------------------------------------------------- |
| **Methods**          | Abstract + concrete methods        | Abstract (pre-Java 8), default/static/private (Java 8+) ​ |
| **Variables**        | Any type (instance, static, final) | Only `public static final` constants                      |
| **Inheritance**      | `extends` (single only)            | `implements` (multiple allowed)                           |
| **Constructors**     | ✅ Can have constructors            | ❌ No constructors                                         |
| **Access Modifiers** | public/private/protected/package   | All `public` by default                                   |
| **State**            | ✅ Can have instance variables      | ❌ No instance variables​                                  |
*Class* - for related classes 
*Interface* - for unrelated classes