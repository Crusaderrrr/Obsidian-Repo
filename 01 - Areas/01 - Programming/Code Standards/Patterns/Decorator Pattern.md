---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - patterns
note type: Informational Note
---
This is kind of pattern that helps to build structures, that are based on **composition and inheritance**. 

---
# Definition
Паттерн Декоратор динамически наделяет объект новыми возможностями и является гибкой альтернативой субклассированию в области расширения функциональности.

Follows the *Open-Closed* principle from [[SOLID]]. That helps with developing.

*My thoughts*:
That pattern is used to wrap objects one in another, without using inheritance, but using composition. 

--- 

Some more of **my explanations**:
- Instead of needing to define thousands of structures, for example like `CoffeeMochaWhip`, `CoffeeMochaDarkChocolateWhip`, etc.
- We can *Dynamically* define this structures by wrapping a base object like that: `Coffee coffee = new Coffee(new Mocha(new Mocha(new DarkChocolate())))`