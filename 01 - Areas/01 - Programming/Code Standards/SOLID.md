---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - clean_code
note type: Informational Note
---
Solid are some sort of rules for OOP, that allow coders write maintainable, logic and clear code. It was invented by *Robert C. Matin* (aka uncle Bob) who wrote the book "Clear code".

### This abbreviature is translated as:
- <mark style="background: #ABF7F7A6;">Single Responsibility Principle</mark>
	- **One class solves only one task**
 - <mark style="background: #ABF7F7A6;">Open-closed Principle</mark>
	- **Programming essences should be opened for extension, but closed for modification**
	- *Abstractions* can help with this, it means that some complex implementation details are hidden and we show only the details that are needed by the user.
	- *Interfaces* can also help, they tell us what can objects do, but not how they do it. Look, if we have a house building plan, and there you have things that house should have, but not specified how to build it.
	- *An example of this principle*: 
		When we want to implement a payment with cash, card or phone, we should not create a single `Payment` class, instead we need to create a `PaymentProcessor` class and extend it with new classes like `CashPaymentProcessor`, `CreditCardPaymentProcessor`, and more, if we do it like that it gets easier to extend this with new features.
- <mark style="background: #ABF7F7A6;">Liskov Substitution Principle</mark>
	- **Derived classes should replace their basic classes**
	- *Barbara Liskov* was a scientist in the area of the CS and specially OOP.
	- Here we are talking about child and parent classes, and this principle tells us that we should implement such *child classes that could replace their parent clases*.
	- For example if we have a `Figure` class with `get_area()` method, in other child classes like `Square` or `Triangle` we will modify the `get_area()` method, not implement it again.
- <mark style="background: #ABF7F7A6;">Interface Segregation Principle</mark> 
	- **Clients should not depend on interfaces they do not use**
	- We should create a simple interfaces without any unnecessary methods.
	- The code should be written in a way that makes it reusable.
- <mark style="background: #ABF7F7A6;">Dependency Inversion Principle</mark>
	- **Higher level modules should not depend low level modules. Both of module types should depend on abstractions. Abstractions should not depend on details, however details should depend on abstractions**
	- Almost every piece of code has decencies. 
	- This principle means that this dependencies that connect different parts of program should be created via abstractions. It is necessary to use *Interfaces* and *Abstraction classes* and use previous 4 principles. 


> [!attention]
> There are some disadvantages of SOLID
- Not everybody knows it, and this affect the deployment to the team.
- It requires more time.
- It is not universal and not suitable for every project.
- Not always makes code cleaner.